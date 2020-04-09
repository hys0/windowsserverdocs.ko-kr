---
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: 온-프레미스 장치 기반 조건부 액세스 구성
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 19e139df53cd1c076f8d5597c1c68b8ffe2cfe91
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817176"
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>등록 된 디바이스를 사용 하 여 구성 온-프레미스 조건부 액세스


다음 문서는 설치 및 등록 된 디바이스를 사용 하 여 온-프레미스 조건부 액세스 구성 과정을 안내 합니다.

![조건부 액세스](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

## <a name="infrastructure-pre-requisites"></a>인프라에 대 한 필수 정보
다음과 같은 필요한 필수 조건는 온-프레미스 조건부 액세스로 시작 하기 전에 필요 합니다. 

|요구 사항|설명
|-----|-----
|Azure AD premium Azure AD 구독 | 장치 다시에 대 한 쓰기 프레미스 조건부 액세스 기능에 사용할 수 있도록 [무료 평가판을 세밀 하 게 됩니다.](https://azure.microsoft.com/trial/get-started-active-directory/)  
|Intune 구독|장치 규정 준수 시나리오-에 대 한 MDM 통합에만 필요[무료 평가판을 세밀 하 게 됩니다.](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0)
|Azure AD 연결|2015 년 11 월 QFE 이상.  최신 버전 가져오기 [여기](https://www.microsoft.com/download/details.aspx?id=47594)합니다.  
|Windows Server 2016|10586 또는 AD FS에 대 한 최신 빌드  
|Windows Server 2016 Active Directory 스키마|스키마 수준 85 이상이 필요 합니다.
|Windows Server 2016 도메인 컨트롤러|이는 비즈니스 키 신뢰 배포의 Hello에만 필요 합니다.  추가 정보는 [여기](https://aka.ms/whfbdocs)에서 찾을 수 있습니다.  
|Windows 10 클라이언트|10586 빌드 또는 최신, 위 도메인에 가입 된 Windows 10 도메인 가입 및 Microsoft Passport에 대 한 작업 시나리오에 필요  
|Azure AD Premium 라이선스가 할당 된 azure AD 사용자 계정|디바이스 등록에 대 한  


 
## <a name="upgrade-your-active-directory-schema"></a>Active Directory 스키마 업그레이드
등록 된 장치에서 온-프레미스 조건부 액세스를 사용 하려면 먼저 AD 스키마를 업그레이드 해야 합니다.  다음 조건이 충족 되어야 합니다.
    - 스키마는 버전 85 이상 이어야 합니다.
    - 이는 AD FS 가입 된 포리스트에만 필요 합니다.

> [!NOTE]
> Windows Server 2016에서 스키마 버전 (수준 85 이상)으로 업그레이드 하기 전에 Azure AD Connect을 설치한 경우 Azure AD Connect 설치를 다시 실행 하 고 온-프레미스 AD 스키마를 새로 고쳐의 msds-primary-computer-KeyCredentialLink에 대 한 동기화 규칙이 구성 되어 있는지 확인 해야 합니다.

### <a name="verify-your-schema-level"></a>스키마 수준 확인
스키마 수준을 확인 하려면 다음을 수행 합니다.

1.  ADSIEdit 또는 LDP를 사용 하 여 스키마 명명 컨텍스트에 연결할 수 있습니다.  
2.  ADSIEdit를 사용 하 여 "CN = Schema, CN = Configuration, DC =<domain>, DC =<com>을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  포리스트 정보를 사용 하 여 도메인 및 com 부분을 사용 합니다.
3.  특성 편집기에서 objectVersion 특성을 찾아 사용자의 버전을 알려 줍니다.  

![ADSI 편집](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)  

다음 PowerShell cmdlet을 사용할 수도 있습니다. 개체를 스키마 명명 컨텍스트 정보로 바꿉니다.

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion
    
```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png) 

업그레이드에 대 한 자세한 내용은 [Windows Server 2016로 도메인 컨트롤러 업그레이드](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2016.md)를 참조 하세요. 

## <a name="enable-azure-ad-device-registration"></a>Azure AD 장치 등록 사용  
이 시나리오를 구성 하려면 Azure ad에서 디바이스 등록 기능을 구성 해야 합니다.  

이 작업을 수행 하려면 아래 단계를 수행 [조직에서 Azure AD 조인 설정](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-setup/)  

## <a name="setup-ad-fs"></a>AD FS를 설치 합니다.  
1. 만들기는 [새 AD FS 2016 팜](https://technet.microsoft.com/library/dn486775.aspx)합니다.   
2.  또는 [마이그레이션할](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md) AD FS 2012 r 2에서에서 ad FS 2016 팜  
4. 배포 [Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectfed-whatis/) 사용자 지정 경로 사용 하 여 AD FS를 Azure AD에 연결 합니다.  

## <a name="configure-device-write-back-and-device-authentication"></a>장치 쓰기 되돌림 및 장치 인증 구성  
> [!NOTE]
> Express 설정을 사용 하 여 Azure AD Connect 실행 한 경우 올바른 AD 개체가 생성 됩니다.  그러나 대부분의 AD FS 시나리오에서 Azure AD Connect를 실행할 때 AD FS를 구성 하는 사용자 지정 설정 하므로 다음 단계는 필요 합니다.  

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>AD FS 장치 인증에 대 한 AD 개체 만들기  
장치 인증에 대 한 AD FS 팜을 아직 구성 되지 않은 경우 (표시 서비스에서 AD FS 관리 콘솔에서이 장치 등록->)는 올바른 AD DS 개체를 만들고 구성 하려면 다음 단계를 사용 합니다.  

![장치 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>참고:에서 아래 명령이 필요한 Active Directory 관리 도구, 따라서 페더레이션 서버는 도메인 컨트롤러도 하는 경우 먼저 설치 1 아래 단계를 사용 하 여 도구입니다.  그렇지 않은 경우 1 단계를 건너뛸 수 있습니다.  

1.  실행 된 **추가 역할 및 기능** 마법사 및 선택 기능 **원격 서버 관리 도구** -> **역할 관리 도구** -> **AD DS 및 AD LDS 도구** 모두 선택->는 **Windows PowerShell 용 Active Directory 모듈** 및 **AD DS 도구**합니다.

![장치 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)
  
2. AD FS 주 서버에서 엔터프라이즈 관리자 (EA) 권한 가진 AD DS 사용자로 로그인 하 고 관리자 권한 powershell 프롬프트를 열고 확인 합니다.  그런 다음 다음 PowerShell 명령을 실행 합니다.  
    
   `Import-module activedirectory`  
   `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" ` 
3. 팝업 창에서 예를 누릅니다.

>참고: AD FS 서비스 GMSA 계정을 사용 하도록를 구성 하는 경우 계정 이름을 입력 "domain\accountname$" 형식

![장치 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device3.png)  

위의 PSH 다음 개체를 만듭니다.  


- AD 도메인 파티션 아래 RegisteredDevices 컨테이너  
- 장치 등록 서비스 컨테이너 및 개체의 구성에서 서비스--> 장치 등록 구성-->  
- 장치 등록 서비스 DKM 컨테이너 및 개체의 구성에서 서비스--> 장치 등록 구성-->  

![장치 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device4.png)  

4. 이 작업이 완료 되 면 성공적으로 완료 메시지가 표시 됩니다.

![장치 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device5.png) 

###        <a name="create-service-connection-point-scp-in-ad"></a>Ad에서 서비스 연결 지점 (SCP) 만들기  
Windows 10 도메인 공간 (Azure AD에 자동 등록)를 설명 된 대로 여기 사용 하려는 경우 AD DS에 서비스 연결 지점을 만들려면 다음 명령을 실행합니다  
1.  Windows PowerShell을 열고 다음 명령을 실행 합니다.
    
    `PS C:>Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1" ` 

>참고: 필요한 경우 AdSyncPrep.psm1에서 파일을 복사 하면 Azure AD Connect 서버.  이 파일은 Program Files\Microsoft Azure Active Directory Connect\AdPrep

![장치 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device6.png)   

2. Azure AD 전역 관리자 자격 증명을 제공 합니다.  

    `PS C:>$aadAdminCred = Get-Credential`

![장치 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device7.png) 

3. 다음 PowerShell 명령을 실행 합니다. 

   `PS C:>Initialize-ADSyncDomainJoinedComputerSync -AdConnectorAccount [AD connector account name] -AzureADCredentials $aadAdminCred ` 

여기서 [AD 커넥터 계정 이름]는 온-프레미스를 추가 하는 경우 Azure AD Connect에서 구성 된 계정의 이름을 AD DS 디렉터리입니다.
  
위의 명령을 사용 Windows 10 찾도록 클라이언트를 올바른 Azure AD 도메인에 AD DS에 serviceConnectionpoint 개체를 만들어서 조인 합니다.  

### <a name="prepare-ad-for-device-write-back"></a>장치 쓰기 되돌림 AD 준비   
을 보장 하기 위해 AD DS 개체 및 컨테이너의 Azure AD에서 디바이스 후면 쓰기에 대 한 올바른 상태에는 다음을 수행 합니다.

1.  Windows PowerShell을 열고 다음 명령을 실행 합니다.  

    `PS C:>Initialize-ADSyncDeviceWriteBack -DomainName <AD DS domain name> -AdConnectorAccount [AD connector account name] ` 

여기서 [AD 커넥터 계정 이름]는 온-프레미스를 추가 하는 경우 Azure AD Connect에서 구성 된 계정의 이름을 domain\accountname 형식에서 AD DS 디렉터리  

위의 명령은 이미 존재 하지 않는 경우 AD DS에 다시 쓰기를 디바이스에 대 한 다음 개체를 만듭니다 및 지정된 된 AD connector 계정 이름에 대 한 액세스 허용  

- AD 도메인 파티션에 RegisteredDevices 컨테이너  
- 장치 등록 서비스 컨테이너 및 개체의 구성에서 서비스--> 장치 등록 구성-->  

### <a name="enable-device-write-back-in-azure-ad-connect"></a>장치 쓰기를 사용 합니다. Azure AD에서 다시 연결  
되기 전에, 수행 하지 않은 경우 Azure AD Connect에서 다시 장치 쓰기를 사용 하도록 설정 마법사를 한 번 실행 하 고 선택 하 여 **"사용자 지정 동기화 옵션"** , 한 후 장치 쓰기 되돌림에 대 한 확인란을 선택 하 고 위의 cmdlet을 실행 한 있는 포리스트를 선택 합니다.  

### <a name="configure-device-authentication-in-ad-fs"></a>AD FS에서 장치 인증을 구성 합니다.  
다음 명령을 실행 하 여 AD FS 정책을 구성 관리자 권한 PowerShell 명령 창을 사용 하 여,  

`PS C:>Set-AdfsGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true -DeviceAuthenticationMethod All` 

### <a name="check-your-configuration"></a>구성을 확인합니다  
참조용으로 아래는 포괄적인 목록이 AD DS 디바이스, 컨테이너 및 작동 하도록 디바이스 쓰기 저장 및 인증에 필요한 권한
 


- CN=RegisteredDevices,DC=&lt;domain&gt;에서 ms-DS-DeviceContainer 유형의 개체          
    - AD FS 서비스 계정에 대 한 읽기 액세스   
    - 읽기/쓰기 액세스는 Azure AD Connect sync AD 커넥터 계정</br></br>

- 컨테이너 CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=&lt;domain&gt;  
- 위의 컨테이너에서 장치 등록 서비스 DKM 컨테이너

![장치 등록](media/Configure-Device-Based-Conditional-Access-on-Premises/device8.png) 
 


- 개체의 CN에서 형식 serviceConnectionpoint =&lt;guid&gt;, CN = 장치 등록

- Configuration,CN=Services,CN=Configuration,DC=&lt;domain&gt;  
  - 읽기/쓰기 권한으로 새 개체에 지정 된 AD 커넥터 계정 이름으로</br></br> 


- 개체의 종류를 DeviceRegistrationServiceContainer CN에서 장치 등록 서비스, CN = 장치 등록 구성, CN = Services, CN = Configuration, DC = = & ltdomain >  


- 위의 컨테이너의 종류를 DeviceRegistrationService의 개체  

### <a name="see-it-work"></a>작업 표시  
새 클레임 및 정책을 평가 하려면 먼저 디바이스를 등록 합니다.  예를 들어에 대 한 설정 앱을 사용 하 여 시스템에서 Windows 10 컴퓨터-> Azure AD 조인 하거나 추가 단계를 수행 하는 자동 장치 등록을 통해 Windows 10 도메인 가입을 설정할 수 있습니다 [여기](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)합니다.  모바일 장치를 Windows 10 조인에 대 한 내용은 문서를 참조 [여기](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)합니다.  

가장 쉬운 평가 대 한 클레임의 목록을 표시 하는 테스트 애플리케이션을 사용 하 여 AD fs에 로그인 합니다. IsManaged, isCompliant, trusttype 등 새 클레임을 볼 수 있습니다.  작업에 대 한 Microsoft Passport를 사용 하면 클레임 prt도 표시 됩니다.  
 

## <a name="configure-additional-scenarios"></a>추가 시나리오를 구성 합니다.  
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>자동 등록에 대 한 Windows 10 도메인 가입 된 컴퓨터  
Windows 10 도메인에 대 한 자동 장치 등록을 사용 하도록 설정 하려면 컴퓨터를 가입, 1 및 2 단계에 따라 [여기](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)합니다.   
다음을 수행 하는 데 도움이 됩니다.  

1. AD DS에 서비스 연결 지점에 있는지, 그리고 적절 한 사용 권한이 확인 (위의 작업을이 개체를 만든 것 이지만 다시 저하 되지 않습니다).  
2. AD FS가 올바르게 구성 되었는지 확인  
3. AD FS 시스템에 사용 하도록 설정 하는 올바른 엔드포인트을 확인 하 고 클레임 규칙 구성   
4. 도메인에 가입 된 컴퓨터의 자동 디바이스 등록에 필요한 그룹 정책 설정 구성   

### <a name="microsoft-passport-for-work"></a>Microsoft Passport for Work   
Windows 10이 작업에 대 한 Microsoft Passport 설정에 대 한 자세한 내용은 참조 하십시오. [조직에서 작업에 대 한 Microsoft Passport를 사용 하도록 설정 합니다.](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)  

### <a name="automatic-mdm-enrollment"></a>자동 MDM 등록   
액세스 제어 정책에서 isCompliant 클레임을 사용할 수 있도록 등록 된 장치의 자동 MDM 등록을 단계에 따라 [여기 있습니다.](https://blogs.technet.microsoft.com/ad/2015/08/14/windows-10-azure-ad-and-microsoft-intune-automatic-mdm-enrollment-powered-by-the-cloud/)  

## <a name="troubleshooting"></a>문제 해결  
1.  오류가 발생 하는 경우 `Initialize-ADDeviceRegistration` 에 이미 있는 잘못 된 상태와 같은 개체에 대해 불평 하는 "drs 서비스 개체 찾았는지 필수 특성이 모두 없이", Azure AD Connect powershell 이전에 명령 및 AD DS의 부분을 갖게를 실행할 수 있습니다.  개체를 수동으로 삭제 하십시오 **CN = 장치 등록 Configuration, CN = Services, CN = Configuration, DC =&lt;도메인&gt;** 하 고 다시 시도 합니다.  
2.  Windows 10 도메인에 대 한 클라이언트 연결  
    1. 디바이스 인증 작동 확인, 도메인에 로그온 하려면 테스트 사용자 계정으로 클라이언트를 가입 합니다. 신속 하 게 프로 비전을 트리거할 잠금 해제 하는 데스크톱 적어도 한 번.   
    2. Stk 키 자격 증명을 확인 하는 지침은 AD DS 개체에 연결 (동기화 여전히 않아도 두 번 실행?)  
3.  디바이스가 이미 등록, 하지만 수 없는 또는 디바이스에 이미 등록 되지 않은 한 Windows 컴퓨터를 등록 하려고 하면 오류가 디바이스 등록 구성의 단편 레지스트리에 해야 합니다.  조사 하 고이 제거 하려면 다음 단계를 사용 합니다.  
    1. Windows 컴퓨터에서 Regedit 열고 이동 **HKLM\Software\Microsoft\Enrollments**   
    2. 이 키에서 GUID 형태로 많은 하위 키 수 됩니다.  ~ 17 값을 포함 하며 "6" [MDM 가입] "EnrollmentType"에 있는 하위 키 또는 "13" (Azure AD 조인)로 이동  
    3. 수정 **EnrollmentType** 에 **0** 
    4. 디바이스 등록 또는 등록을 다시 시도  

### <a name="related-articles"></a>관련 문서  
* [Azure Active Directory에 연결 된 Office 365 및 기타 앱에 대 한 액세스 보호](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)  
* [Office 365 서비스에 대 한 조건부 액세스 장치 정책](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-device-policies/)  
* [Azure Active Directory Device Registration를 사용 하 여 온-프레미스 조건부 액세스 설정](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)  
* [도메인에 가입 된 장치를 Windows 10 용 Azure AD 환경에 연결](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)  
