---
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: "구성 조건부 액세스 장치 기반 온-프레미스"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 47afd0c6963bd8b8b4dde82650cf807c1954b40b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>등록 된 디바이스를 사용 하 여 구성 온-프레미스 조건부 액세스

>적용 대상: Windows Server 2016, Windows Server 2012 r 2  

다음 문서는 설치 하 고 등록 된 디바이스와 온-프레미스 조건부 액세스 구성 통해 안내 합니다.

![조건부 액세스](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

## <a name="infrastructure-pre-requisites"></a>인프라 필수
온-프레미스 조건부 액세스할 수 있는 하기 전에 다음과 같은 당 3 요구가 필요 합니다. 

|요구 사항|설명
|-----|-----
|Azure AD 프리미엄을 Azure AD 구독 | 프레미스 조건부 액세스-디바이스 쓰기 다시 사용 하도록 설정 하려면 [무료 평가판 괜찮습니다.](https://azure.microsoft.com/en-us/trial/get-started-active-directory/)  
|Intune 구독|장치 준수 시나리오-에 대 한 통합 MDM에만 필요[무료 평가판 괜찮습니다.](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0)
|Azure AD 연결|2015 년 11 월 QFE 이상 합니다.  최신 버전 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=47594)합니다.  
|Windows Server 2016|빌드 10586 이상 adfs  
|Windows Server 2016 Active Directory 스키마|스키마 수준 85 이상이 필요 합니다.
|Windows Server 2016 도메인 컨트롤러|이 기능은 Hello에 대 한 비즈니스 키 신뢰 배포용 필요 합니다.  자세한 내용은에서 찾아보실 수 [여기](https://aka.ms/whfbdocs)합니다.  
|Windows 10의 클라이언트|빌드 10586 되었거나 새로운, 위의 도메인에 가입만 작업 시나리오에 대 한 Windows 10 도메인 가입 및 Microsoft Passport 필요  
|Azure AD 사용자 계정에 할당 Azure AD 프리미엄 라이선스|장치를 등록 하기 위한  


 
## <a name="upgrade-your-active-directory-schema"></a>업그레이드 Active Directory 스키마
온-프레미스 조건부 액세스 등록 된 디바이스를 사용 하려면 먼저 광고 스키마를 업그레이드 해야 합니다.  다음 조건은 충족 해야 합니다.
    - 스키마 버전 85 이상이 있어야 합니다.
    - 이 기능은 필요 Adfs에 가입한 숲

> [!NOTE]
> Azure AD 연결 설치 프로그램 다시 실행 하는 온-프레미스 새로 고침 필요는 Windows Server 2016에 스키마 버전 (수준 85 이상)으로 업그레이드 하기 전에 Azure AD 연결을 설치한 경우 광고 스키마를 KeyCredentialLink 구성에 대 한 동기화 규칙 수 있도록 합니다.

### <a name="verify-your-schema-level"></a>스키마 수준을 확인합니다
스키마 잔량을 확인 하려면 다음을 수행 합니다.

1.  ADSIEdit 또는 LDP 사용 하 고 스키마 명명 컨텍스트에 연결할 수 있습니다.  
2.  ADSIEdit를 사용 하 여 마우스 오른쪽 단추로 클릭 "CN CN 스키마 = = DC 구성 =<domain>, DC =<com> 마우스 속성을 선택 합니다.  Relpace 도메인 및 숲 정보 com 부분입니다.
3.  특성 편집기에서 objectVersion 특성 찾아 알려, 버전입니다.  

![ADSI 편집](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)  

다음 PowerShell cmdlet (대체 개체 명명 상황에 맞는 정보 스키마를) 사용할 수 있습니다.

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion
    
```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png) 

업그레이드에 대 한 자세한 내용은 참조 [하기 위해 Windows Server 2016 도메인 컨트롤러 업그레이드](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2016.md)합니다. 

## <a name="enable-azure-ad-device-registration"></a>사용 Azure AD 디바이스 등록  
이 시나리오를 구성 하려면 Azure AD에 디바이스 등록 기능이 구성 해야 합니다.  

이 위해 아래 단계에 따라 [Azure AD에 연결할 조직에서 설정](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-setup/)  

## <a name="setup-ad-fs"></a>ADFS 설정  
1. 만들기는 [새 FS 2016 AD 농장](https://technet.microsoft.com/library/dn486775.aspx)합니다.   
2.  또는 [마이그레이션을](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md) AD FS 2012 r 2의에서 FS 2016 ad 농장  
4. 배포 [Azure AD 연결](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectfed-whatis/) ADFS Azure AD에 연결할 사용자 지정 경로 사용 합니다.  

## <a name="configure-device-write-back-and-device-authentication"></a>다시 디바이스 쓰기 및 디바이스 인증 구성  
> [!NOTE]
> 기본 설정을 사용 하 여 Azure AD 연결을 실행 하는 경우 올바른 광고 개체를 만들었습니다.  그러나 ADFS 가장 시나리오에서 Azure AD 연결 된으로 실행 ADFS 구성 하려면 사용자 지정 설정 않으므로 아래 절차는 필요 합니다.  

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>광고 FS 장치 인증을 위해 광고 개체 만들기  
ADFS 농장 구성 장치 인증 되지 않은 경우 (수이 태그가 표시 서비스에서 광고 FS Management console에서-> 장치 등록) 다음 단계를 사용 하 여 올바른 AD DS 개체 및 구성 만들 수 있습니다.  

![디바이스 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>참고:는 명령 아래 Active Directory 관리 도구 필요, 따라서 해당 federation 서버는 도메인 컨트롤러도 먼저 설치 1 아래 단계를 사용 하 여 도구입니다.  그렇지 않으면 1 단계를 건너뛸 수 있습니다.  

1.  실행는 **역할 추가 및 기능** 마법사 및 선택 기능 **원격 서버 관리 도구** -> **역할 관리 도구** -> **AD DS 및 광고 LDS 도구** 모두 선택->는 **Windows PowerShell 모듈 Active Directory** 및 **AD DS 도구**합니다.

![디바이스 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)
  
2.  ADFS 주 서버 (EA) Enterprise 관리자 권한이 있는 사용자가 광고 DS로 로그인 하 고 powershell을 관리자 권한 프롬프트를 열을 확인 합니다.  그런 다음 다음 PowerShell 명령을 실행 합니다.  
    
    `Import-module activedirectory`  
    `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" ` 
3.  팝업 창에 도달 예 했습니다.

>참고: ADFS 서비스를 GMSA 계정을 사용 하도록 구성 된 경우 입력 계정 이름을 "domain\accountname$" 형식

![디바이스 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device3.png)  

위의 PSH 다음 개체를 만듭니다.  


- 광고 도메인 파티션 아래의 RegisteredDevices 컨테이너  
- 디바이스 서비스 등록 컨테이너 및 구성에서 개체 서비스--> 장치 등록 구성-->  
- 디바이스 서비스 DKM 등록 컨테이너 및 구성에서 개체 서비스--> 장치 등록 구성-->  

![디바이스 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device4.png)  

4.  이 작업이 완료 되 면 메시지를 성공적으로 완료 표시 됩니다.

![디바이스 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device5.png) 

###        <a name="create-service-connection-point-scp-in-ad"></a>광고에 서비스 연결 지점 (SCP) 만들기  
사용 하 여 Azure AD에 등록 자동) (와 Windows 10 도메인 가입 설명 된 대로 여기 하려는 경우 AD ds에서 서비스 연결 지점을 만드는 뒤 다음 명령을 실행합니다  
1.  Windows PowerShell 열고 다음 명령을 실행 합니다.
    
    `PS C:>Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1" ` 

>참고: 필요한 경우 파일을 복사할 AdSyncPrep.psm1 Azure AD 연결 서버에서.  이 파일은 프로그램 서식 Azure Active Directory Connect\AdPrep

![디바이스 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device6.png)   

2. Azure AD 전역 관리자 자격 증명을 제공  

    `PS C:>$aadAdminCred = Get-Credential`

![디바이스 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device7.png) 

3.  다음 PowerShell 명령을 실행 합니다. 

    `PS C:>Initialize-ADSyncDomainJoinedComputerSync -AdConnectorAccount [AD connector account name] -AzureADCredentials $aadAdminCred ` 

[광고 커넥터 계정 이름]에 온-프레미스 추가할 때 Azure AD 연결으로 구성 된 계정 이름이 이루어지는 AD DS 디렉터리 합니다.
  
위의 명령 Windows 10 클라이언트가 올바른 찾을 수 있도록 AD ds에서 serviceConnectionpoint 개체를 만들어 참여를 Azure AD 도메인.  

### <a name="prepare-ad-for-device-write-back"></a>다시 디바이스 쓰기 광고 준비   
쓰기 뒷면 Azure AD의 장치에 대 한 올바른 상태로 설정 된 광고 DS 개체와 컨테이너 하려면 다음을 수행 합니다.

1.  Windows PowerShell 열고 다음 명령을 실행 합니다.  

    `PS C:>Initialize-ADSyncDeviceWriteBack -DomainName <AD DS domain name> -AdConnectorAccount [AD connector account name] ` 

[광고 커넥터 계정 이름]에 온-프레미스 추가할 때 Azure AD 연결으로 구성 된 계정 이름이 이루어지는 AD DS 디렉터리 domain\accountname 형식  

위의 이미 존재 하지 않는 경우 다음과 같은 개체 AD DS에 다시 디바이스 쓰기 만듭니다 명령과 지정된 된 광고 커넥터 계정 이름에 액세스할 수 있게  

- 광고 도메인 파티션에 RegisteredDevices 컨테이너  
- 디바이스 서비스 등록 컨테이너 및 구성에서 개체 서비스--> 장치 등록 구성-->  

### <a name="enable-device-write-back-in-azure-ad-connect"></a>쓰기 디바이스를 사용 하도록 설정 Azure AD에 다시 연결  
마법사를 한 번 실행 하 고 선택 하 여 되기 전에 수행 하지 않은 경우 사용 Azure AD 연결에 다시 디바이스 쓰기 **"동기화 옵션을 사용자 지정"**디바이스 쓰기 다시에 대 한 확인란을 선택 다음을 선택 하는 위의 cmdlet 실행 숲  

### <a name="configure-device-authentication-in-ad-fs"></a>Adfs의 장치 인증을 구성 합니다.  
다음 명령을 실행 하 여 ADFS 정책을 구성 높은 PowerShell 명령 창을 사용 하 여  

`PS C:>Set-AdfsGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true -DeviceAuthenticationMethod All` 

### <a name="check-your-configuration"></a>구성을 확인합니다  
참조를 위해 아래에 광고 DS 장치, 컨테이너 및 사용 권한을 디바이스 다시 쓰기 및 인증에 대해 작동 하는 데 필요한의 전체 목록을 보려면
 


- 타이핑 ms-DS-DeviceContainer CN에서의 개체 RegisteredDevices, DC = =&lt;도메인&gt;        
    - ADFS 서비스 계정에 대 한 읽기   
    - Azure AD 연결 동기화 광고 커넥터 계정에 대 한 액세스 읽기/쓰기</br></br>

- 컨테이너 CN = 디바이스 등록 구성 CN CN 서비스 = = DC 구성 =&lt;도메인&gt;  
- 컨테이너 디바이스 등록 서비스 DKM 위의 컨테이너

![디바이스 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device8.png) 
 


- 타이핑 serviceConnectionpoint CN에서의 개체 =&lt;guid&gt;, CN = 디바이스 등록

- 구성, CN CN 서비스 = = DC 구성 =&lt;도메인&gt;  
 - 새 개체에 지정 된 광고 커넥터 계정 이름에 대 한 액세스 읽기/쓰기</br></br> 


- 종류를 DeviceRegistrationServiceContainer CN에서의 개체 디바이스 등록 서비스 CN = = 디바이스 등록 구성 CN CN 서비스 = = DC 구성 = & ltdomain >  


- 위의 컨테이너 형식을 DeviceRegistrationService의  

### <a name="see-it-work"></a>작동 표시  
새로운 청구 및 정책 평가할, 장치를 등록 합니다.  예를 들어, 시스템 아래 설정 앱을 사용 하 여 Windows 10 컴퓨터에 대 한-Azure AD 가입 하거나 추가 단계를 수행 자동 장치 등록 된 Windows 10 도메인 가입을 설정할 수 있습니다 [여기](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)합니다.  모바일 디바이스에서 Windows 10에 참여에 대 한 내용은 문서를 참조 [여기](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)합니다.  

쉬운 평가 클레임 목록이 표시 되는 테스트 응용 프로그램을 사용 하 여 Adfs에 로그인 합니다. 새 클레임 isManaged, isCompliant trusttype 등 표시 됩니다.  Microsoft Passport 클라우드를 사용 하도록 설정 하는 경우 청구 prt도 표시 됩니다.  
 

## <a name="configure-additional-scenarios"></a>추가 시나리오를 구성 합니다.  
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>자동 등록에 대 한 Windows 10 도메인 가입 컴퓨터  
Windows 10 도메인에 대 한 자동 장치 등록을 사용 하도록 설정 하려면 컴퓨터 가입, 1, 2 단계에 따라 [여기](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)합니다.   
다음를 달성 하는 데 도움이 됩니다.  

1. AD ds에서 서비스 연결 지점에 있고 적절 한 권한이 있는지 확인 (위의이 개체 만들었습니다 있지만 다시 프 하지 않는).  
2. ADFS 제대로 구성 되어 있는지 확인  
3. ADFS 시스템에 사용 하는 올바른 끝점 확인 하 고 구성 규칙 주장   
4. 컴퓨터가 도메인에 가입 자동 장치를 등록에 필요한 그룹 정책 설정을 구성합니다   

### <a name="microsoft-passport-for-work"></a>회사에 대 한 Microsoft Passport   
회사에 대 한 Microsoft Passport와 Windows 10에서 정보를 참조 하세요. [조직에서 작업에 대 한 Microsoft Passport 사용 하도록 설정 합니다.](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)  

### <a name="automatic-mdm-enrollment"></a>자동 MDM 등록   
사용자 액세스 제어 정책에서 isCompliant 청구를 사용할 수 있도록의 등록 된 디바이스 자동 MDM 등록을 단계에 따라 [여기 합니다.](https://blogs.technet.microsoft.com/ad/2015/08/14/windows-10-azure-ad-and-microsoft-intune-automatic-mdm-enrollment-powered-by-the-cloud/)  

## <a name="troubleshooting"></a>문제 해결  
1.  오류가 발생 하는 경우 `Initialize-ADDeviceRegistration` 개체 이미에 잘못 된 상태와 같은 대 한 발생 하는 "drs 서비스 개체 발견 되었습니다 필요한 모든 특성을 않고도"를 Azure AD 연결 powershell 이전에 명령 및 부분 구성을 AD DS가지고 실행할 수 있습니다.  수동 개체의 삭제 해 보세요. **CN = 디바이스 등록 구성 CN CN 서비스 = = DC 구성 =&lt;도메인&gt; ** 하 고 다시 시도 합니다.  
2.  Windows 10 도메인에 가입 하는 클라이언트  
    1. 해당 장치 인증 작동 하는지 확인 하려면 도메인에 로그인 클라이언트 테스트 사용자 계정으로 참여 합니다. 신속 하 게 프로비저닝 트리거하, 잠그고 잠금 해제 하는 데스크톱 한 번 이상 합니다.   
    2. 광고 DS 개체에 지침 stk 주요 자격 증명을 확인 하려면 연결 (않는 동기화 해야 두 번 실행?)  
3.  등록 된 디바이스를 등록 한 이미, 있지만 수 없는 또는 장치 unenrolled 이미 있는 Windows 컴퓨터 하려고 하면 오류가 발생를 받을 경우 레지스트리에서 등록 구성 디바이스의 일부를 할 수 있습니다.  조사 하 고이 항목을 제거 하려면 다음 단계를 사용 합니다.  
    1. Windows 컴퓨터에서 Regedit 열고 이동 **HKLM\Software\Microsoft\Enrollments**   
    2. 이 키 GUID 형태로 많은 하위 수 됩니다.  ~ 17 값에는 "6" [MDM 가입] "EnrollmentType"가 하위 또는 "13" (Azure AD 가입)로 이동  
    3. 수정 **EnrollmentType** 에 **0** 
    4. 다시 등록 또는 디바이스 등록  

### <a name="related-articles"></a>관련된 문서  
* [Azure Active Directory에 연결 된 다른 앱 및 Office 365에 대 한 액세스 보호](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access/)  
* [Office 365 서비스에 대 한 조건 액세스 디바이스 정책](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-device-policies/)  
* [온-프레미스 조건부 액세스 Azure Active Directory 장치 등록을 사용 하 여 설정](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-device-registration-on-premises-setup)  
* [도메인 가입 디바이스에 대 한 Windows 10 환경 Azure AD에 연결](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-devices-group-policy/)  
