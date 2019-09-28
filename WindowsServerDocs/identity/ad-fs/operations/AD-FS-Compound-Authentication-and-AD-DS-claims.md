---
title: Active Directory Federation Services의 복합 인증 및 Active Directory Domain Services 클레임
description: 다음 문서에서는 AD FS의 복합 인증 및 AD DS 클레임에 대해 설명 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 78db6f8b6961cecea55b8d371e9abf952cafdab3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358672"
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>AD FS의 복합 인증 및 AD DS 클레임
Windows Server 2012는 복합 인증을 도입 하 여 Kerberos 인증을 향상 시킵니다.  복합 인증을 사용 하면 Kerberos TGS (티켓 부여 서비스) 요청에 다음 두 개의 id를 포함할 수 있습니다. 

- 사용자의 id입니다.
- 사용자 장치의 id입니다.  

Windows [에서는 FAST (Kerberos 유연한 인증 보안 터널링) 또는 kerberos 아머 링 (armoring)을](https://technet.microsoft.com/library/hh831747.aspx)확장 하 여 복합 인증을 수행 합니다. 

AD FS 2012 이상 버전에서는 Kerberos 인증 티켓에 상주 하는 AD DS 발급 된 사용자 또는 장치 클레임을 사용할 수 있습니다. 이전 버전의 AD FS에서 클레임 엔진은 Kerberos에서 사용자 및 그룹 Sid (보안 Id)만 읽을 수 있지만 Kerberos 티켓에 포함 된 클레임 정보는 읽을 수 없습니다.

Active Directory Domain Services (AD DS) 발급 된 사용자 및 장치 클레임을 사용 하 여 페더레이션 응용 프로그램에 대 한 보다 다양 한 액세스 제어를 Active Directory Federation Services (AD FS)로 사용할 수 있습니다.

## <a name="requirements"></a>요구 사항
1.  페더레이션 응용 프로그램에 액세스 하는 컴퓨터는 **Windows 통합 인증**을 사용 하 여 AD FS에 인증 해야 합니다. 
    - Windows 통합 인증은 백 엔드 AD FS 서버에 연결 하는 경우에만 사용할 수 있습니다.
    - 컴퓨터에서 페더레이션 서비스 이름에 대 한 백 엔드 AD FS 서버에 연결할 수 있어야 합니다.
    - AD FS 서버는 인트라넷 설정에서 Windows 통합 인증을 기본 인증 방법으로 제공 해야 합니다.

2.  복합 인증으로 보호 되는 페더레이션 응용 프로그램에 액세스 하는 모든 컴퓨터에 **클레임 복합 인증 및 kerberos 아머 링 (armoring)에 대 한 kerberos 클라이언트 지원** 정책이 적용 되어야 합니다. 이는 단일 포리스트 또는 포리스트 간 시나리오의 경우 적용할 수 있습니다.

3.  AD FS 서버 도메인에는 도메인 컨트롤러에 적용 되는 **클레임 복합 인증 및 Kerberos 아머 링 (armoring)에 대 한 KDC 지원** 정책 설정이 있어야 합니다.

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 AD FS를 구성 하는 단계
복합 인증 및 클레임을 구성 하는 데 다음 단계를 사용 합니다. 

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>1단계:  기본 도메인 컨트롤러 정책에서 클레임, 복합 인증 및 Kerberos 아머 링 (armoring)에 대 한 KDC 지원 사용
1.  서버 관리자에서 도구, **그룹 정책 관리**를 선택 합니다.
2.  **기본 도메인 컨트롤러 정책**으로 이동 하 고 마우스 오른쪽 단추를 클릭 한 다음 **편집**을 선택 합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  **그룹 정책 관리 편집기** **컴퓨터 구성**에서 **정책**, **관리 템플릿**, **시스템**을 차례로 확장 하 고 **KDC**를 선택 합니다.
4.  오른쪽 창에서 **클레임, 복합 인증 및 Kerberos 아머 링 (armoring)에 대 한 KDC 지원**을 두 번 클릭 합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  새 대화 상자 창에서 클레임에 대 한 KDC 지원을 **사용**으로 설정 합니다.
6.  옵션 아래의 드롭다운 메뉴에서 **지원** 을 선택 하 고 **적용** 및 **확인**을 클릭 합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>2단계: 페더레이션 응용 프로그램에 액세스 하는 컴퓨터에서 클레임, 복합 인증 및 Kerberos 아머 링 (armoring)에 대 한 Kerberos 클라이언트 지원 사용

1.  페더레이션 응용 프로그램에 액세스 하는 컴퓨터에 적용 되는 그룹 정책 **그룹 정책 관리 편집기**의 **컴퓨터 구성**에서 **정책**, **관리 템플릿**, 시스템을 차례로 확장 합니다.을 선택 하 고 **Kerberos**를 선택 합니다.
2.  그룹 정책 관리 편집기 창의 오른쪽 창에서 **클레임, 복합 인증 및 kerberos 아머 링 (armoring)에 대 한 kerberos 클라이언트 지원** 을 두 번 클릭 합니다.
3.  새 대화 상자 창에서 Kerberos 클라이언트 지원을 **사용** 으로 설정 하 고 **적용** 및 **확인**을 클릭 합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  그룹 정책 관리 편집기를 닫습니다.

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>3단계: AD FS 서버가 업데이트 되었는지 확인 합니다.
AD FS 서버에 다음 업데이트가 설치 되어 있는지 확인 해야 합니다.

|업데이트|설명|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|누적 보안 업데이트 (KB2919355, KB2932046, KB2934018, KB2937592, KB2938439 포함)|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|Server 2012 R2 업데이트|
|[핫픽스 3052122](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|이 업데이트는 Active Directory Federation Services의 복합 ID 클레임에 대 한 지원을 추가 합니다.|

### <a name="step-4-configure-the-primary-authentication-provider"></a>4단계: 기본 인증 공급자 구성

1. AD FS 인트라넷 설정에 대해 기본 인증 공급자를 **Windows 인증** 으로 설정 합니다.
2. AD FS 관리의 **인증 정책**에서 **기본 인증** 을 선택 하 고 **전역 설정** 에서 **편집**을 클릭 합니다.
3. **인트라넷** 의 **전역 인증 정책 편집** 에서 **Windows 인증**을 선택 합니다.
4. **적용** 및 **확인을**클릭 합니다.

![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. PowerShell을 사용 하 여 **AdfsGlobalAuthenticationPolicy** cmdlet을 사용할 수 있습니다.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID 기반 팜에서 PowerShell 명령은 기본 AD FS 서버에서 실행 되어야 합니다.
>SQL 기반 팜에서는 팜의 구성원 인 모든 AD FS 서버에서 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>5단계:  AD FS에 클레임 설명 추가
1. 팜에 다음 클레임 설명을 추가 합니다. 이 클레임 설명은 ADFS 2012 r 2에서 기본적으로 제공 되지 않으며 수동으로 추가 해야 합니다.
2. AD FS 관리의 **서비스**에서 **클레임 설명** 을 마우스 오른쪽 단추로 클릭 하 고 **클레임 설명 추가** 를 선택 합니다.
3. 클레임 설명에 다음 정보를 입력 합니다.
   - 표시 이름: ' Windows 장치 그룹 ' 
   - 클레임 설명: '<https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup>' '
4. 두 상자 모두에 체크를 놓습니다.
5. **확인**을 클릭합니다.

![클레임 설명](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. PowerShell을 사용 하 여 **AdfsClaimDescription** cmdlet을 사용할 수 있습니다.
   ``` powershell
   Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
   -ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device' 
   ```


>[!NOTE]
>WID 기반 팜에서 PowerShell 명령은 기본 AD FS 서버에서 실행 되어야 합니다.
>SQL 기반 팜에서는 팜의 구성원 인 모든 AD FS 서버에서 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>6단계:  의 msds-primary-computer-Supported Types 특성에서 복합 인증 비트를 사용 하도록 설정 합니다.

1.  **Uninstall-adserviceaccount** PowerShell cmdlet을 사용 하 여 AD FS 서비스를 실행 하도록 지정한 계정의의 msds-primary-computer-supported 특성에서 복합 인증 비트를 사용 하도록 설정 합니다.  

>[!NOTE]
>서비스 계정을 변경 하는 경우 **compoundIdentitySupported: $true** Windows PowerShell cmdlet을 실행 하 여 복합 인증을 수동으로 사용 하도록 설정 해야 합니다.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2. ADFS 서비스를 다시 시작 합니다.

>[!NOTE]
>' CompoundIdentitySupported '가 true로 설정 되 면 새 서버 (2012r2/2016)에 동일한 gMSA을 설치 하는 데 실패 합니다 **. 설치-uninstall-adserviceaccount: 서비스 계정을 설치할 수 없습니다. 오류 메시지: ' 제공 된 컨텍스트가 대상과 일치 하지 않습니다. '** .
>
>**해결 방법**: CompoundIdentitySupported를 $false로 임시로 설정 합니다. 이 단계를 수행 하면 ADFS가 WindowsDeviceGroup 클레임 발급을 중지 합니다. Uninstall-adserviceaccount-Identity ' ADFS 서비스 계정 '-CompoundIdentitySupported $false: 새 서버에 gMSA를 설치 하 고 CompoundIdentitySupported를 다시 $True로 설정 합니다.
CompoundIdentitySupported 및) 준비가를 사용 하지 않도록 설정 하면 ADFS 서비스를 다시 시작할 필요가 없습니다.

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>7단계: Active Directory에 대 한 AD FS 클레임 공급자 트러스트를 업데이트 합니다.

1. ' WindowsDeviceGroup ' 클레임에 대 한 다음 ' 통과 ' 클레임 규칙을 포함 하도록 Active Directory에 대 한 AD FS 클레임 공급자 트러스트를 업데이트 합니다.
2.  **AD FS 관리**에서 **클레임 공급자 트러스트** 를 클릭 하 고 오른쪽 창에서 **Active Directory** 를 Righ 클릭 하 고 **클레임 규칙 편집**을 선택 합니다.
3.  **Active Director에 대 한 클레임 규칙 편집** 에서 **규칙 추가**를 클릭 합니다.
4.  **변환 클레임 규칙 추가 마법사** 에서 **들어오는 클레임 통과 또는 필터링** 을 선택 하 고 **다음**을 클릭 합니다.
5.  표시 이름을 추가 하 고 **들어오는 클레임 유형** 드롭다운에서 **Windows 장치 그룹** 을 선택 합니다.
6.  **마침**을 클릭합니다.  **적용** 및 **확인을**클릭 합니다. 
![클레임 설명](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>8단계: ' WindowsDeviceGroup ' 클레임이 필요한 신뢰 당사자에서 유사한 ' 통과 ' 또는 ' 변환 ' 클레임 규칙을 추가 합니다.
2. **AD FS 관리**에서 신뢰 당사자 **트러스트** 를 클릭 하 고 오른쪽 창에서 RP를 Righ 클릭 하 고 **클레임 규칙 편집**을 선택 합니다.
3. **발급 변환 규칙** 에서 **규칙 추가**를 클릭 합니다.
4. **변환 클레임 규칙 추가 마법사** 에서 **들어오는 클레임 통과 또는 필터링** 을 선택 하 고 **다음**을 클릭 합니다.
5. 표시 이름을 추가 하 고 **들어오는 클레임 유형** 드롭다운에서 **Windows 장치 그룹** 을 선택 합니다.
6. **마침**을 클릭합니다.  **적용** 및 **확인을**클릭 합니다.
   ![클레임 설명](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


## <a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Windows Server 2016에서 AD FS를 구성 하는 단계
다음은 Windows Server 2016에 대 한 AD FS에서 복합 인증을 구성 하는 단계를 자세히 설명 합니다.

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>1단계:  기본 도메인 컨트롤러 정책에서 클레임, 복합 인증 및 Kerberos 아머 링 (armoring)에 대 한 KDC 지원 사용
1.  서버 관리자에서 도구, **그룹 정책 관리**를 선택 합니다.
2.  **기본 도메인 컨트롤러 정책**으로 이동 하 고 마우스 오른쪽 단추를 클릭 한 다음 **편집**을 선택 합니다.
3.  **그룹 정책 관리 편집기** **컴퓨터 구성**에서 **정책**, **관리 템플릿**, **시스템**을 차례로 확장 하 고 **KDC**를 선택 합니다.
4.  오른쪽 창에서 **클레임, 복합 인증 및 Kerberos 아머 링 (armoring)에 대 한 KDC 지원**을 두 번 클릭 합니다.
5.  새 대화 상자 창에서 클레임에 대 한 KDC 지원을 **사용**으로 설정 합니다.
6.  옵션 아래의 드롭다운 메뉴에서 **지원** 을 선택 하 고 **적용** 및 **확인**을 클릭 합니다.


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>2단계: 페더레이션 응용 프로그램에 액세스 하는 컴퓨터에서 클레임, 복합 인증 및 Kerberos 아머 링 (armoring)에 대 한 Kerberos 클라이언트 지원 사용

1.  페더레이션 응용 프로그램에 액세스 하는 컴퓨터에 적용 되는 그룹 정책 **그룹 정책 관리 편집기**의 **컴퓨터 구성**에서 **정책**, **관리 템플릿**, 시스템을 차례로 확장 합니다.을 선택 하 고 **Kerberos**를 선택 합니다.
2.  그룹 정책 관리 편집기 창의 오른쪽 창에서 **클레임, 복합 인증 및 kerberos 아머 링 (armoring)에 대 한 kerberos 클라이언트 지원** 을 두 번 클릭 합니다.
3.  새 대화 상자 창에서 Kerberos 클라이언트 지원을 **사용** 으로 설정 하 고 **적용** 및 **확인**을 클릭 합니다.
4.  그룹 정책 관리 편집기를 닫습니다.

### <a name="step-3-configure-the-primary-authentication-provider"></a>3단계: 기본 인증 공급자 구성

1. AD FS 인트라넷 설정에 대해 기본 인증 공급자를 **Windows 인증** 으로 설정 합니다.
2. AD FS 관리의 **인증 정책**에서 **기본 인증** 을 선택 하 고 **전역 설정** 에서 **편집**을 클릭 합니다.
3. **인트라넷** 의 **전역 인증 정책 편집** 에서 **Windows 인증**을 선택 합니다.
4. **적용** 및 **확인을**클릭 합니다.
5. PowerShell을 사용 하 여 **AdfsGlobalAuthenticationPolicy** cmdlet을 사용할 수 있습니다.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID 기반 팜에서 PowerShell 명령은 기본 AD FS 서버에서 실행 되어야 합니다.
>SQL 기반 팜에서는 팜의 구성원 인 모든 AD FS 서버에서 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>4단계:  의 msds-primary-computer-Supported Types 특성에서 복합 인증 비트를 사용 하도록 설정 합니다.

1.  **Uninstall-adserviceaccount** PowerShell cmdlet을 사용 하 여 AD FS 서비스를 실행 하도록 지정한 계정의의 msds-primary-computer-supported 특성에서 복합 인증 비트를 사용 하도록 설정 합니다.  

>[!NOTE]
>서비스 계정을 변경 하는 경우 **compoundIdentitySupported: $true** Windows PowerShell cmdlet을 실행 하 여 복합 인증을 수동으로 사용 하도록 설정 해야 합니다.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2. ADFS 서비스를 다시 시작 합니다.

>[!NOTE]
>' CompoundIdentitySupported '가 true로 설정 되 면 새 서버 (2012r2/2016)에 동일한 gMSA을 설치 하는 데 실패 합니다 **. 설치-uninstall-adserviceaccount: 서비스 계정을 설치할 수 없습니다. 오류 메시지: ' 제공 된 컨텍스트가 대상과 일치 하지 않습니다. '** .
>
>**해결 방법**: CompoundIdentitySupported를 $false로 임시로 설정 합니다. 이 단계를 수행 하면 ADFS가 WindowsDeviceGroup 클레임 발급을 중지 합니다. Uninstall-adserviceaccount-Identity ' ADFS 서비스 계정 '-CompoundIdentitySupported $false: 새 서버에 gMSA를 설치 하 고 CompoundIdentitySupported를 다시 $True로 설정 합니다.
CompoundIdentitySupported 및) 준비가를 사용 하지 않도록 설정 하면 ADFS 서비스를 다시 시작할 필요가 없습니다.

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>5단계: Active Directory에 대 한 AD FS 클레임 공급자 트러스트를 업데이트 합니다.

1. ' WindowsDeviceGroup ' 클레임에 대 한 다음 ' 통과 ' 클레임 규칙을 포함 하도록 Active Directory에 대 한 AD FS 클레임 공급자 트러스트를 업데이트 합니다.
2.  **AD FS 관리**에서 **클레임 공급자 트러스트** 를 클릭 하 고 오른쪽 창에서 **Active Directory** 를 Righ 클릭 하 고 **클레임 규칙 편집**을 선택 합니다.
3.  **Active Director에 대 한 클레임 규칙 편집** 에서 **규칙 추가**를 클릭 합니다.
4.  **변환 클레임 규칙 추가 마법사** 에서 **들어오는 클레임 통과 또는 필터링** 을 선택 하 고 **다음**을 클릭 합니다.
5.  표시 이름을 추가 하 고 **들어오는 클레임 유형** 드롭다운에서 **Windows 장치 그룹** 을 선택 합니다.
6.  **마침**을 클릭합니다.  **적용** 및 **확인을**클릭 합니다. 


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>6단계: ' WindowsDeviceGroup ' 클레임이 필요한 신뢰 당사자에서 유사한 ' 통과 ' 또는 ' 변환 ' 클레임 규칙을 추가 합니다.
2. **AD FS 관리**에서 신뢰 당사자 **트러스트** 를 클릭 하 고 오른쪽 창에서 RP를 Righ 클릭 하 고 **클레임 규칙 편집**을 선택 합니다.
3. **발급 변환 규칙** 에서 **규칙 추가**를 클릭 합니다.
4. **변환 클레임 규칙 추가 마법사** 에서 **들어오는 클레임 통과 또는 필터링** 을 선택 하 고 **다음**을 클릭 합니다.
5. 표시 이름을 추가 하 고 **들어오는 클레임 유형** 드롭다운에서 **Windows 장치 그룹** 을 선택 합니다.
6. **마침**을 클릭합니다.  **적용** 및 **확인을**클릭 합니다.

## <a name="validation"></a>유효성 검사
' WindowsDeviceGroup ' 클레임 릴리스의 유효성을 검사 하려면 .Net 4.6을 사용 하 여 테스트 클레임 인식 응용 프로그램을 만듭니다. WIF SDK 4.0를 사용 합니다.
ADFS에서 응용 프로그램을 신뢰 당사자로 구성 하 고 위의 단계에 지정 된 대로 클레임 규칙을 사용 하 여 업데이트 합니다.
ADFS의 Windows 통합 인증 공급자를 사용 하 여 응용 프로그램을 인증 하는 경우 다음 클레임이 캐스트 됩니다.
![유효성 검사](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

이제 더 다양 한 액세스 제어를 위해 컴퓨터/장치에 대 한 클레임이 소비 될 수 있습니다.

예를 들어, 다음 **Additionalauthenticationrules** 는 인증 사용자가 보안 그룹 "-1-5-21-2134745077-1211275016-3050530490-1117" 및 컴퓨터 (여기서는 사용자 인 경우)의 멤버가 아닌 경우 MFA를 호출 하도록 AD FS에 지시 합니다. 에서 인증 중)은 보안 그룹 "S-1-5-21-2134745077-1211275016-3050530490-1115 (WindowsDeviceGroup)"의 구성원이 아닙니다.

그러나 위의 조건 중 하나라도 충족 되 면 MFA를 호출 하지 마세요.

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```
