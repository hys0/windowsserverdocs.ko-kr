---
title: Active Directory Federation Services의 인증 및 Active Directory Domain Services 클레임 복합
description: 다음 문서는 복합 인증 및 AD FS에서 AD DS 클레임을 설명합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 270fb6efd63e6355c410ee45d09e6fd16b14222b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867994"
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>AD FS의 복합 인증 및 AD DS 클레임
Windows Server 2012는 복합 인증을 도입 하 여 Kerberos 인증을 강화 합니다.  복합 인증을 사용 하면 두 개의 id를 포함 하는 Kerberos 티켓 부여 서비스 (TGS) 요청: 

- 사용자의 id
- 사용자의 장치 id입니다.  

Windows 기능을 확장 하 여 복합 인증을 수행 [Kerberos FAST Flexible Authentication Secure Tunneling (), 또는 Kerberos 아머 링](https://technet.microsoft.com/library/hh831747.aspx)합니다. 

AD FS 2012 및 이후 버전의 AD DS는 Kerberos 인증 티켓에 상주 하는 사용자 또는 장치 클레임을 발급 한 소비를 허용 합니다. AD FS의 이전 버전에서는 클레임 엔진 Kerberos에서 사용자 및 그룹 보안 식별자 (Sid) 읽을 수 있지만 읽을 수 없습니다는 Kerberos 티켓에 포함 된 정보를 클레임 합니다.

Active Directory Domain Services (AD DS)를 사용 하 여 페더레이션된 응용 프로그램에 대 한 다양 한 액세스 제어를 설정할 수 있습니다.-Active Directory Federation Services (AD FS)를 사용 하 여 함께 사용자 및 장치 클레임을 발급 합니다.

## <a name="requirements"></a>요구 사항
1.  페더레이션된 응용 프로그램에 액세스 하는 컴퓨터에 AD FS를 사용 하 여 인증 해야 합니다 **Windows 통합 인증**합니다. 
    - 백 엔드 AD FS 서버에 연결 하는 경우에 Windows 통합 인증이 제공 됩니다.
    - 컴퓨터는 페더레이션 서비스 이름에 대 한 백 엔드 AD FS 서버에 연결할 수 있어야 합니다.
    - AD FS 서버는 해당 인트라넷 설정에 기본 인증 방법으로 Windows 통합 인증을 제공 해야 합니다.

2.  정책을 **클레임, 복합 인증 및 Kerberos 아머 링에 대 한 Kerberos 클라이언트 지원** 복합 인증으로 보호 되는 페더레이션된 응용 프로그램에 액세스 하는 모든 컴퓨터에 적용 되어야 합니다. 이 경우 단일 포리스트 또는 포리스트 시나리오에 적용 됩니다.

3.  AD FS 서버를 보유 하는 도메인에 있어야 합니다 **클레임 복합 인증 및 Kerberos 아머 링에 대 한 KDC 지원** 정책 설정은 도메인 컨트롤러에 적용 합니다.

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2에서 AD FS를 구성 하는 단계
복합 인증 및 클레임을 구성 하기 위한 다음 단계를 사용 합니다. 

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>1단계:  클레임, 복합 인증 및 기본 도메인 컨트롤러 정책에서 Kerberos 아머 링에 대 한 KDC 지원 설정
1.  서버 관리자에서 도구를 선택 **그룹 정책 관리**합니다.
2.  아래로 이동 합니다 **기본 도메인 컨트롤러 정책**, 마우스 오른쪽 단추로 **편집**합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  에 **그룹 정책 관리 편집기**아래에 있는 **컴퓨터 구성**, 확장 **정책**를 확장 하 고 **관리 템플릿** 를 확장 하 고 **시스템**, 선택한 **KDC**합니다.
4.  오른쪽 창에서 두 번 클릭 **KDC의 클레임, 복합 인증 및 Kerberos 아머 링 지원**합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  새 대화 상자 창에 대 한 클레임에 대 한 KDC 지원 설정 **사용**합니다.
6.  옵션에서 선택 **지원 되는** 한 다음 클릭 하 고 드롭다운 메뉴에서 **적용** 하 고 **확인**합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>2단계: 클레임, 복합 인증 및 페더레이션된 응용 프로그램에 액세스 하는 컴퓨터에서 Kerberos 아머 링에 대 한 Kerberos 클라이언트 지원을 사용 하도록 설정

1.  페더레이션된 응용 프로그램에 액세스 하는 컴퓨터에 적용 된 그룹 정책에는 **그룹 정책 관리 편집기**아래에 있는 **컴퓨터 구성**를 확장 하 고 **정책**, 확장 **관리 템플릿**를 확장 **시스템**를 선택 하 고 **Kerberos**합니다.
2.  그룹 정책 관리 편집기 창의 오른쪽 창에서 두 번 클릭 **클레임, 복합 인증 및 Kerberos 아머 링에 대 한 Kerberos 클라이언트 지원 합니다.**
3.  새 대화 상자 창에서로 Kerberos 클라이언트 지원 **Enabled** 클릭 **적용** 하 고 **확인**.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  그룹 정책 관리 편집기를 닫습니다.

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>3단계: AD FS 서버가 업데이트 되었는지 확인 합니다.
AD FS 서버에서 다음 업데이트가 설치 되어 있는지 확인 해야 합니다.

|Update|설명|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|누적 보안 업데이트 (KB2919355 KB2932046, KB2934018, KB2937592, KB2938439 포함)|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|Server 2012 R2에 대 한 업데이트|
|[Hotfix 3052122](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|이 업데이트는 Active Directory Federation Services에서 복합 ID 클레임에 대 한 지원을 추가합니다.|

### <a name="step-4-configure-the-primary-authentication-provider"></a>4단계: 기본 인증 공급자로 구성

1. 기본 인증 공급자를 설정할 **Windows 인증** AD FS 인트라넷 설정에 대 한 합니다.
2. AD FS 관리에서 아래의 **인증 정책**를 선택 **기본 인증** 아래에서 **전역 설정** 클릭 **편집**합니다.
3. 온 **전역 인증 정책 편집** 아래에서 **인트라넷** 선택 **Windows 인증**합니다.
4. 클릭 **적용** 하 고 **확인**합니다.

![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. 사용할 수 있습니다 하는 PowerShell을 사용 하 여 **집합 AdfsGlobalAuthenticationPolicy** cmdlet.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID 팜의 기본 AD FS 서버에서 명령을 실행 해야 하는 PowerShell 기반 합니다.
>SQL 기반 팜에서 팜의 멤버인 모든 AD FS 서버에서 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>5단계:  AD fs 클레임 설명 추가
1.  팜에 클레임 설명을 추가 합니다. 이 클레임 설명은 2012 R2 ADFS에서에서 기본적으로 제공 되지 않으며 수동으로 추가 해야 하는 경우.
2.  AD FS 관리에서 아래의 **서비스**를 마우스 오른쪽 단추로 클릭 **클레임 설명** 선택한 **클레임 설명 추가**
3.  클레임 설명에 다음 정보를 입력 합니다.
    - 표시 이름: ' Windows 장치 그룹 ' 
    - Claim Description: 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
4. 두 상자에 확인란을 선택 합니다.
5. **확인**을 클릭합니다.

![클레임 설명](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. 사용할 수 있습니다 하는 PowerShell을 사용 하 여 **추가 AdfsClaimDescription** cmdlet.
``` powershell
Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
-ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device' 
```


>[!NOTE]
>WID 팜의 기본 AD FS 서버에서 명령을 실행 해야 하는 PowerShell 기반 합니다.
>SQL 기반 팜에서 팜의 멤버인 모든 AD FS 서버에서 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>6단계:  복합 인증 비트 Msds-supportedencryptiontypes 특성을 사용 하도록 설정

1.  비트를 사용 하 여 AD FS 서비스를 실행 하려면 지정한 계정의 Msds-supportedencryptiontypes 특성 복합 인증을 사용 합니다 **Set-adserviceaccount** PowerShell cmdlet.  

>[!NOTE]
>서비스 계정을 변경한 경우 실행 하 여 복합 인증을 수동으로 설정 해야 합니다 **compoundIdentitySupported Set-aduser: $true** Windows PowerShell cmdlet.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  ADFS 서비스를 다시 시작 합니다.

>[!NOTE]
>'CompoundIdentitySupported' 다음 오류 – 새 (2016 년 2012R2) 서버 실패에 동일한 gMSA의 true 이면 설치로 설정 되 면 **Install-adserviceaccount: 서비스 계정을 설치할 수 없습니다. 오류 메시지: ' 제공 된 컨텍스트 대상과 일치 하지 않았습니다.'** .
>
>**해결 방법**: CompoundIdentitySupported $false 일시적으로 설정 합니다. 이 단계를 수행 하면 ADFS WindowsDeviceGroup 클레임 발급을 중지 합니다. Set-adserviceaccount-Identity ' ADFS 서비스 계정 ' CompoundIdentitySupported: $false 새 서버에서 gMSA를 설치 하 고 다음 CompoundIdentitySupported $True에 다시 사용 하도록 설정 합니다.
CompoundIdentitySupported 않도록 설정 했다가 다시 활성화 한 다음 ADFS 서비스를 다시 시작할 필요가 없습니다.

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>7단계: Active Directory에 대 한 업데이트는 AD FS 클레임 공급자 트러스트

1. AD FS 클레임 공급자 트러스트 'WindowsDeviceGroup' 클레임에 대 한 다음 '통과' 클레임 규칙을 포함 하도록 Active directory를 업데이트 합니다.
2.  **AD FS 관리**, 클릭 **클레임 공급자 트러스트** 하 고 오른쪽 창에서 마우스 오른쪽 단추 클릭 **Active Directory** 선택한 **클레임 규칙 편집**.
3.  에 **Active Director에 대 한 클레임 규칙 편집** 클릭 **규칙 추가**합니다.
4.  에 **변환 클레임 규칙 추가 마법사** 선택 **통과 또는 들어오는 클레임 필터링** 누릅니다 **다음**합니다.
5.  표시 이름을 추가 하 고 선택 **Windows 장치 그룹** 에서 합니다 **들어오는 클레임 유형** 드롭 다운 합니다.
6.  **마침**을 클릭합니다.  클릭 **적용** 하 고 **확인**합니다. 
![클레임 설명](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>8단계: 'WindowsDeviceGroup' 클레임은 필요한 신뢰 당사자에서 유사한 '통과' 또는 '변환' 클레임 규칙을 추가 합니다.
2.  **AD FS 관리**, 클릭 **신뢰 당사자 트러스트** 하 고 오른쪽 창에서 마우스 오른쪽 단추 클릭 선택 고 RP **클레임 규칙 편집**.
3.  에 **발급 변환 규칙** 클릭 **규칙 추가**합니다.
4.  에 **변환 클레임 규칙 추가 마법사** 선택 **통과 또는 들어오는 클레임 필터링** 누릅니다 **다음**합니다.
5.  표시 이름을 추가 하 고 선택 **Windows 장치 그룹** 에서 합니다 **들어오는 클레임 유형** 드롭 다운 합니다.
6.  **마침**을 클릭합니다.  클릭 **적용** 하 고 **확인**합니다.
![클레임 설명](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


##<a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Windows Server 2016에서 AD FS를 구성 하는 단계
다음은 Windows Server 2016 용 AD FS에서 복합 인증을 구성 하는 단계를 설명 합니다.

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>1단계:  클레임, 복합 인증 및 기본 도메인 컨트롤러 정책에서 Kerberos 아머 링에 대 한 KDC 지원 설정
1.  서버 관리자에서 도구를 선택 **그룹 정책 관리**합니다.
2.  아래로 이동 합니다 **기본 도메인 컨트롤러 정책**, 마우스 오른쪽 단추로 **편집**합니다.
3.  에 **그룹 정책 관리 편집기**아래에 있는 **컴퓨터 구성**, 확장 **정책**를 확장 하 고 **관리 템플릿** 를 확장 하 고 **시스템**, 선택한 **KDC**합니다.
4.  오른쪽 창에서 두 번 클릭 **KDC의 클레임, 복합 인증 및 Kerberos 아머 링 지원**합니다.
5.  새 대화 상자 창에 대 한 클레임에 대 한 KDC 지원 설정 **사용**합니다.
6.  옵션에서 선택 **지원 되는** 한 다음 클릭 하 고 드롭다운 메뉴에서 **적용** 하 고 **확인**합니다.


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>2단계: 클레임, 복합 인증 및 페더레이션된 응용 프로그램에 액세스 하는 컴퓨터에서 Kerberos 아머 링에 대 한 Kerberos 클라이언트 지원을 사용 하도록 설정

1.  페더레이션된 응용 프로그램에 액세스 하는 컴퓨터에 적용 된 그룹 정책에는 **그룹 정책 관리 편집기**아래에 있는 **컴퓨터 구성**를 확장 하 고 **정책**, 확장 **관리 템플릿**를 확장 **시스템**를 선택 하 고 **Kerberos**합니다.
2.  그룹 정책 관리 편집기 창의 오른쪽 창에서 두 번 클릭 **클레임, 복합 인증 및 Kerberos 아머 링에 대 한 Kerberos 클라이언트 지원 합니다.**
3.  새 대화 상자 창에서로 Kerberos 클라이언트 지원 **Enabled** 클릭 **적용** 하 고 **확인**.
4.  그룹 정책 관리 편집기를 닫습니다.

### <a name="step-3-configure-the-primary-authentication-provider"></a>3단계: 기본 인증 공급자로 구성

1. 기본 인증 공급자를 설정할 **Windows 인증** AD FS 인트라넷 설정에 대 한 합니다.
2. AD FS 관리에서 아래의 **인증 정책**를 선택 **기본 인증** 아래에서 **전역 설정** 클릭 **편집**합니다.
3. 온 **전역 인증 정책 편집** 아래에서 **인트라넷** 선택 **Windows 인증**합니다.
4. 클릭 **적용** 하 고 **확인**합니다.
5. 사용할 수 있습니다 하는 PowerShell을 사용 하 여 **집합 AdfsGlobalAuthenticationPolicy** cmdlet.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>WID 팜의 기본 AD FS 서버에서 명령을 실행 해야 하는 PowerShell 기반 합니다.
>SQL 기반 팜에서 팜의 멤버인 모든 AD FS 서버에서 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>4단계:  복합 인증 비트 Msds-supportedencryptiontypes 특성을 사용 하도록 설정

1.  비트를 사용 하 여 AD FS 서비스를 실행 하려면 지정한 계정의 Msds-supportedencryptiontypes 특성 복합 인증을 사용 합니다 **Set-adserviceaccount** PowerShell cmdlet.  

>[!NOTE]
>서비스 계정을 변경한 경우 실행 하 여 복합 인증을 수동으로 설정 해야 합니다 **compoundIdentitySupported Set-aduser: $true** Windows PowerShell cmdlet.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  ADFS 서비스를 다시 시작 합니다.

>[!NOTE]
>'CompoundIdentitySupported' 다음 오류 – 새 (2016 년 2012R2) 서버 실패에 동일한 gMSA의 true 이면 설치로 설정 되 면 **Install-adserviceaccount: 서비스 계정을 설치할 수 없습니다. 오류 메시지: ' 제공 된 컨텍스트 대상과 일치 하지 않았습니다.'** .
>
>**해결 방법**: CompoundIdentitySupported $false 일시적으로 설정 합니다. 이 단계를 수행 하면 ADFS WindowsDeviceGroup 클레임 발급을 중지 합니다. Set-adserviceaccount-Identity ' ADFS 서비스 계정 ' CompoundIdentitySupported: $false 새 서버에서 gMSA를 설치 하 고 다음 CompoundIdentitySupported $True에 다시 사용 하도록 설정 합니다.
CompoundIdentitySupported 않도록 설정 했다가 다시 활성화 한 다음 ADFS 서비스를 다시 시작할 필요가 없습니다.

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>5단계: Active Directory에 대 한 업데이트는 AD FS 클레임 공급자 트러스트

1. AD FS 클레임 공급자 트러스트 'WindowsDeviceGroup' 클레임에 대 한 다음 '통과' 클레임 규칙을 포함 하도록 Active directory를 업데이트 합니다.
2.  **AD FS 관리**, 클릭 **클레임 공급자 트러스트** 하 고 오른쪽 창에서 마우스 오른쪽 단추 클릭 **Active Directory** 선택한 **클레임 규칙 편집**.
3.  에 **Active Director에 대 한 클레임 규칙 편집** 클릭 **규칙 추가**합니다.
4.  에 **변환 클레임 규칙 추가 마법사** 선택 **통과 또는 들어오는 클레임 필터링** 누릅니다 **다음**합니다.
5.  표시 이름을 추가 하 고 선택 **Windows 장치 그룹** 에서 합니다 **들어오는 클레임 유형** 드롭 다운 합니다.
6.  **마침**을 클릭합니다.  클릭 **적용** 하 고 **확인**합니다. 


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>6단계: 'WindowsDeviceGroup' 클레임은 필요한 신뢰 당사자에서 유사한 '통과' 또는 '변환' 클레임 규칙을 추가 합니다.
2.  **AD FS 관리**, 클릭 **신뢰 당사자 트러스트** 하 고 오른쪽 창에서 마우스 오른쪽 단추 클릭 선택 고 RP **클레임 규칙 편집**.
3.  에 **발급 변환 규칙** 클릭 **규칙 추가**합니다.
4.  에 **변환 클레임 규칙 추가 마법사** 선택 **통과 또는 들어오는 클레임 필터링** 누릅니다 **다음**합니다.
5.  표시 이름을 추가 하 고 선택 **Windows 장치 그룹** 에서 합니다 **들어오는 클레임 유형** 드롭 다운 합니다.
6.  **마침**을 클릭합니다.  클릭 **적용** 하 고 **확인**합니다.

## <a name="validation"></a>유효성 검사
'WindowsDeviceGroup' 클레임 릴리스의 유효성을 검사 하는 테스트를 만드는.Net 4.6을 사용 하 여 인식 응용 프로그램을 클레임입니다. With WIF SDK 4.0.
ADFS에서 신뢰 당사자로 응용 프로그램을 구성 하 고 위의 단계에서 지정 된 대로 클레임 규칙을 사용 하 여 업데이트 합니다.
ADFS의 Windows 통합 인증 공급자를 사용 하 여 응용 프로그램을 인증할 때는 다음 클레임이 캐스팅 합니다.
![유효성 검사](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

컴퓨터/장치에 대 한 클레임 보다 풍부한 액세스 제어에 대 한 이제 사용할 수 있습니다.

다음 예를 들어 **AdditionalAuthenticationRules** 인증 사용자 보안 그룹의 구성원이 아닌 경우-MFA를 호출 하도록 AD FS를 알려 줍니다 "-1-5-21-2134745077-1211275016-3050530490-1117"와 컴퓨터 (여기서는 사용자가 인증에서) "S-1-5-21-2134745077-1211275016-3050530490-1115 (WindowsDeviceGroup)" 보안 그룹의 구성원이 아닙니다

그러나 위의 조건 중 하나라도 충족 되는 MFA를 호출 하지 마십시오.

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```
