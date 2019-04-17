---
title: "인증 및 Active Directory Domain Services 클레임 <DICT__Active Directory Federation Services>Active Directory Federation Services에서에서 복합 < / DICT__Active Directory Federation Services >"
description: "다음 문서 복합 인증과 adfs에서 AD DS 클레임에 설명 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f5f80cbcbdb2deca9b098014627365b8ea819b5f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="compound-authentication-and-ad-ds-claims-in-ad-fs"></a>인증과 adfs에서 AD DS 클레임 복합
Windows Server 2012 복합 인증을 도입 Kerberos 인증을 향상 됩니다.  복합 인증 두 id를 포함 하도록 Kerberos 허용 서비스 (TGS) 요청을 사용할 수 있습니다. 

- 사용자의 id
- Id 사용자의 디바이스입니다.  

Windows를 확장 하 여 복합 인증을 수행 [Kerberos 유연한 인증 보안 터널링 (패스트), 또는 Kerberos armoring](https://technet.microsoft.com/library/hh831747.aspx)합니다. 

ADFS 2012와 이상 버전 AD DS Kerberos 인증 티켓에 있는 디바이스 또는 사용자 클레임 발급 소비 수 있게 합니다. Adfs의 이전 버전 엔진 Kerberos에서 사용자 및 그룹 보안 Sid (식별자) 읽을 수 있지만 모든 읽을 수 없었습니다 클레임 Kerberos 티켓에 포함 된 정보를 요구 합니다.

Active Directory Domain Services (AD DS)를 사용 하 여 연결 된 응용 프로그램에 대 한 액세스 제어 풍부한 수 있게-발급 한 사용자와 디바이스 AD FS(Active Directory Federation Services)와 함께 요구합니다.

## <a name="requirements"></a>요구 사항
1.  연결 된 응용 프로그램에 액세스 하 여 컴퓨터를 사용 하 여 ADFS 인증 해야 **Windows 통합 인증**합니다. 
    - Windows 통합 인증은 백 엔드 AD FS 서버에 연결할 때만 사용할 수 있습니다.
    - 컴퓨터는 Federation 서비스 이름에 대 한 백 엔드 AD FS 서버에 연결할 수 있어야 합니다.
    - 광고 FS 서버 인트라넷 설정에서 기본으로 만들기 인증 방법으로 Windows에 통합 인증 제공 해야 합니다.

2.  정책 **클레임 복합 인증 및 Kerberos armoring Kerberos 클라이언트 지원** 복합 인증에 의해 보호 되는 연결 된 응용 프로그램에 액세스 하는 모든 컴퓨터에 적용 합니다. 숲 시나리오 크로스 또는 단일 숲 발생 하는 경우 해당 됩니다.

3.  AD FS 서버 주택 도메인 있어야는 **KDC 인증과 Kerberos armoring 클레임 복합에 대 한 지원이** 도메인 컨트롤러에 적용 되는 정책 설정 합니다.

## <a name="steps-for-configuring-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 ADFS 구성 단계
다음 단계를 사용 하 여 구성 복합 인증 및 청구 

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>1 단계: KDC 클레임, 복합 인증 및 Kerberos armoring 기본 도메인 컨트롤러 정책에서 지원 사용
1.  도구를 선택 하는 서버 관리자 **그룹 정책 관리**합니다.
2.  아래로 이동는 **기본 도메인 컨트롤러 정책**마우스 오른쪽 단추로 클릭 하 고 선택 **편집**합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc1.png)
3.  에 **그룹 정책 편집기 관리**, **컴퓨터 구성**, 확장 **정책**, 확장 **관리 템플릿**, 확장 **시스템**, **KDC**합니다.
4.  두 번 클릭 바로 창에서 **KDC 클레임, 복합 인증 및 Kerberos armoring에 대 한 지원은**합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc2.png)
5.  새 대화 상자 창에서을 청구에 대 한 지원을 KDC 설정 **사용**합니다.
6.  옵션 선택 **지원 되는** 드롭다운 메뉴에서 **적용** 및 **확인**합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc3.png)

### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>2 단계: 사용 Kerberos 클라이언트 클레임, 지원 복합 인증 Kerberos armoring 연결 된 응용 프로그램에 액세스 하는 컴퓨터에서

1.  연결 된 응용 프로그램에 액세스 하 여 컴퓨터에 적용 되는 그룹 정책에의 **그룹 정책 편집기 관리**, **컴퓨터 구성**, 확장 **정책**, 확장 **관리 템플릿**, 확장 **시스템**를 선택 하 고 **Kerberos**합니다.
2.  그룹 정책 편집기 관리 창의 오른쪽 창에서 두 번 클릭 **클레임, 복합 인증 및 Kerberos armoring Kerberos 클라이언트 지원 합니다.**
3.  새 대화 상자 창에서 Kerberos 클라이언트 지원을 설정 **사용** 클릭 **적용** 및 **확인**합니다.
![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc4.png)
4.  그룹 정책 관리 편집기 닫습니다.

### <a name="step-3-ensure-the-ad-fs-servers-have-been-updated"></a>3 단계: ADFS 서버 업데이트 되었는지 확인 합니다.
다음 업데이트 ADFS 서버에 설치 되어 있는지 확인 해야 합니다.

|업데이트|설명|
|----- | ----- |
|[KB2919355](https://www.microsoft.com/download/details.aspx?id=42335)|(KB2919355, KB2932046, KB2934018, KB2937592, KB2938439 포함) 누적 보안 업데이트|
|[KB2959977](https://www.microsoft.com/download/details.aspx?id=42530)|Server 2012 r 2 용 업데이트|
|[3052122 핫픽스](https://support.microsoft.com/help/3052122/update-adds-support-for-compound-id-claims-in-ad-fs-tokens-in-windows)|이 업데이트의 Active Directory Federation Services 복합 ID 청구에 대 한 지원을 추가합니다.|

### <a name="step-4-configure-the-primary-authentication-provider"></a>4 단계: 구성 주 인증 공급자

1. 주 인증 공급자 설정 **Windows 인증** 광고 FS 인트라넷 설정에 대 한 합니다.
2. AD FS 관리에서 아래 **인증 정책**선택 **주 인증** 고 **글로벌 설정** 클릭 **편집**합니다.
3. **글로벌 인증 정책 편집** 아래 **인트라넷** 선택 **Windows 인증**합니다.
4. 클릭 **적용** 및 **확인**합니다.

![그룹 정책 관리](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc5.png)

5. 사용 하 여 사용할 수 있는 PowerShell은 **설정 AdfsGlobalAuthenticationPolicy** cmdlet 합니다.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>한 WID 주 AD FS 서버의 명령을 실행 해야 하는 PowerShell 농장을 기초 합니다.
>기반 SQL 농장 그룹의 모든 ADFS 서버의 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-5--add-the-claim-description-to-ad-fs"></a>5 단계: ADFS 클레임 설명 추가
1.  다음 청구 설명을 그룹에 추가 합니다. 이 청구 설명 ADFS 2012 r 2에 기본적으로 제공 되며 수동으로 추가 해야 합니다.
2.  AD FS 관리에에서 **서비스**를 마우스 오른쪽 단추로 클릭 **설명 주장** 선택한 **추가 대 한 주장**
3.  클레임 설명에 다음 정보를 입력 합니다.
    - 표시 이름: Windows ' 디바이스 그룹 ' 
    - 클레임 설명: 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' '
4. 두 상자에 확인란을 선택 합니다.
5. 클릭 **확인**합니다.

![대 한 주장](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc6.png)

6. 사용 하 여 사용할 수 있는 PowerShell은 **추가 AdfsClaimDescription** cmdlet 합니다.
``` powershell
Add-AdfsClaimDescription -Name 'Windows device group' -ClaimType 'https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup' `
-ShortName 'windowsdevicegroup' -IsAccepted $true -IsOffered $true -IsRequired $false -Notes 'The windows group SID of the device' 
```


>[!NOTE]
>한 WID 주 AD FS 서버의 명령을 실행 해야 하는 PowerShell 농장을 기초 합니다.
>기반 SQL 농장 그룹의 모든 ADFS 서버의 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-6--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>6 단계: 사용를 SupportedEncryptionTypes 특성 복합 인증 비트

1.  ADFS 서비스 사용 하 여 실행할 지정 된 계정에를 SupportedEncryptionTypes 특성 비트 사용 복합 인증은 **설정 ADServiceAccount** PowerShell cmdlet 합니다.  

>[!NOTE]
>서비스 계정을 변경 하면 다음을 실행 하 여 수동으로 복합 인증을 설정 해야 하는 경우는 **설정 ADUser compoundIdentitySupported: $true** Windows PowerShell cmdlet.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  ADFS 서비스를 다시 시작 합니다.

>[!NOTE]
>'CompoundIdentitySupported' 새 서버 (2012R2/2016)이 작동 하지 않음-다음과 같은 오류에 동일한 gMSA 진정한, 설치도 설정 **설치 ADServiceAccount: 서비스 계정 설치할 수 없습니다. 오류 메시지: ' 제공된 컨텍스트 일치 하지 않습니다 대상.'**.
>
>**해결 방법**: CompoundIdentitySupported $false 일시적으로 설정 합니다. 이 단계를 수행 하면 ADFS WindowsDeviceGroup 클레임 발급 중지 합니다. Set-ADServiceAccount-신원 ' ADFS 서비스 계정 ' CompoundIdentitySupported: $false 새 서버에는 gMSA 설치 하 고 다음 CompoundIdentitySupported $True를 다시 사용 하도록 설정 합니다.
CompoundIdentitySupported 해제 한 후 다시 사용 ADFS 서비스를 다시 시작 필요 하지 않습니다.

### <a name="step-7-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>7 단계: 업데이트에 대 한 Active Directory 광고 FS 클레임 공급자 신뢰

1. 광고 FS 클레임 공급자 신뢰 'WindowsDeviceGroup' 클레임에 대해 다음 '통과' 클레임 규칙을 포함 하기로 Active Directory에 대 한 업데이트 합니다.
2.  **AD FS 관리**, 클릭 **클레임 공급자 신뢰** 및 오른쪽 창 righ 클릭 **Active Directory** 선택 하 고 **편집 클레임 규칙**합니다.
3.  에 **편집 클레임 규칙에 대 한 활성 디렉터** 클릭 **규칙 추가**합니다.
4.  에 **변환 클레임 규칙 마법사 추가** 선택 **통과 또는 필터 수신 클레임** 클릭 **다음**합니다.
5.  표시 이름 추가 하 고 선택 **Windows 디바이스 그룹** 에서 **수신 클레임 유형** 드롭다운 합니다.
6.  클릭 **완료**합니다.  클릭 **적용** 및 **확인**합니다. 
![대 한 주장](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc7.png)

### <a name="step-8-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>8 단계: 'WindowsDeviceGroup' 클레임 예상 되는 위치를 사용 하지 않고 파티에 유사한 '통과' 또는 '변형' 클레임 규칙을 추가 합니다.
2.  **AD FS 관리**, 클릭 **의존 파티 신뢰** 및 오른쪽 창 righ 클릭 RP 및 선택 **클레임 규칙 편집**합니다.
3.  에 **발급 변환 규칙** 클릭 **규칙 추가**합니다.
4.  에 **변환 클레임 규칙 마법사 추가** 선택 **통과 또는 필터 수신 클레임** 클릭 **다음**합니다.
5.  표시 이름 추가 하 고 선택 **Windows 디바이스 그룹** 에서 **수신 클레임 유형** 드롭다운 합니다.
6.  클릭 **완료**합니다.  클릭 **적용** 및 **확인**합니다.
![대 한 주장](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc8.png)


##<a name="steps-for-configuring-ad-fs-in-windows-server-2016"></a>Windows Server 2016에 ADFS 구성 단계
다음은 Windows Server 2016 용 복합 인증 Adfs에서 구성에 대 한 단계 설명 합니다.

### <a name="step-1--enable-kdc-support-for-claims-compound-authentication-and-kerberos-armoring-on-the-default-domain-controller-policy"></a>1 단계: KDC 클레임, 복합 인증 및 Kerberos armoring 기본 도메인 컨트롤러 정책에서 지원 사용
1.  도구를 선택 하는 서버 관리자 **그룹 정책 관리**합니다.
2.  아래로 이동는 **기본 도메인 컨트롤러 정책**마우스 오른쪽 단추로 클릭 하 고 선택 **편집**합니다.
3.  에 **그룹 정책 편집기 관리**, **컴퓨터 구성**, 확장 **정책**, 확장 **관리 템플릿**, 확장 **시스템**, **KDC**합니다.
4.  두 번 클릭 바로 창에서 **KDC 클레임, 복합 인증 및 Kerberos armoring에 대 한 지원은**합니다.
5.  새 대화 상자 창에서을 청구에 대 한 지원을 KDC 설정 **사용**합니다.
6.  옵션 선택 **지원 되는** 드롭다운 메뉴에서 **적용** 및 **확인**합니다.


### <a name="step-2-enable-kerberos-client-support-for-claims-compound-authentication-and-kerberos-armoring-on-computers-accessing-federated-applications"></a>2 단계: 사용 Kerberos 클라이언트 클레임, 지원 복합 인증 Kerberos armoring 연결 된 응용 프로그램에 액세스 하는 컴퓨터에서

1.  연결 된 응용 프로그램에 액세스 하 여 컴퓨터에 적용 되는 그룹 정책에의 **그룹 정책 편집기 관리**, **컴퓨터 구성**, 확장 **정책**, 확장 **관리 템플릿**, 확장 **시스템**를 선택 하 고 **Kerberos**합니다.
2.  그룹 정책 편집기 관리 창의 오른쪽 창에서 두 번 클릭 **클레임, 복합 인증 및 Kerberos armoring Kerberos 클라이언트 지원 합니다.**
3.  새 대화 상자 창에서 Kerberos 클라이언트 지원을 설정 **사용** 클릭 **적용** 및 **확인**합니다.
4.  그룹 정책 관리 편집기 닫습니다.

### <a name="step-3-configure-the-primary-authentication-provider"></a>3 단계: 구성 주 인증 공급자

1. 주 인증 공급자 설정 **Windows 인증** 광고 FS 인트라넷 설정에 대 한 합니다.
2. AD FS 관리에서 아래 **인증 정책**선택 **주 인증** 고 **글로벌 설정** 클릭 **편집**합니다.
3. **글로벌 인증 정책 편집** 아래 **인트라넷** 선택 **Windows 인증**합니다.
4. 클릭 **적용** 및 **확인**합니다.
5. 사용 하 여 사용할 수 있는 PowerShell은 **설정 AdfsGlobalAuthenticationPolicy** cmdlet 합니다.

``` powershell
Set-AdfsGlobalAuthenticationPolicy -PrimaryIntranetAuthenticationProvider 'WindowsAuthentication'
```
>[!NOTE]
>한 WID 주 AD FS 서버의 명령을 실행 해야 하는 PowerShell 농장을 기초 합니다.
>기반 SQL 농장 그룹의 모든 ADFS 서버의 PowerShell 명령을 실행할 수 있습니다.

### <a name="step-4--enable-the-compound-authentication-bit-on-the-msds-supportedencryptiontypes-attribute"></a>4 단계: 사용를 SupportedEncryptionTypes 특성 복합 인증 비트

1.  ADFS 서비스 사용 하 여 실행할 지정 된 계정에를 SupportedEncryptionTypes 특성 비트 사용 복합 인증은 **설정 ADServiceAccount** PowerShell cmdlet 합니다.  

>[!NOTE]
>서비스 계정을 변경 하면 다음을 실행 하 여 수동으로 복합 인증을 설정 해야 하는 경우는 **설정 ADUser compoundIdentitySupported: $true** Windows PowerShell cmdlet.

``` powershell
Set-ADServiceAccount -Identity “ADFS Service Account” -CompoundIdentitySupported:$true 
```
2.  ADFS 서비스를 다시 시작 합니다.

>[!NOTE]
>'CompoundIdentitySupported' 새 서버 (2012R2/2016)이 작동 하지 않음-다음과 같은 오류에 동일한 gMSA 진정한, 설치도 설정 **설치 ADServiceAccount: 서비스 계정 설치할 수 없습니다. 오류 메시지: ' 제공된 컨텍스트 일치 하지 않습니다 대상.'**.
>
>**해결 방법**: CompoundIdentitySupported $false 일시적으로 설정 합니다. 이 단계를 수행 하면 ADFS WindowsDeviceGroup 클레임 발급 중지 합니다. Set-ADServiceAccount-신원 ' ADFS 서비스 계정 ' CompoundIdentitySupported: $false 새 서버에는 gMSA 설치 하 고 다음 CompoundIdentitySupported $True를 다시 사용 하도록 설정 합니다.
CompoundIdentitySupported 해제 한 후 다시 사용 ADFS 서비스를 다시 시작 필요 하지 않습니다.

### <a name="step-5-update-the-ad-fs-claims-provider-trust-for-active-directory"></a>광고 FS 클레임 공급자에 대 한 Active Directory 신뢰 5 단계: 업데이트

1. 광고 FS 클레임 공급자 신뢰 'WindowsDeviceGroup' 클레임에 대해 다음 '통과' 클레임 규칙을 포함 하기로 Active Directory에 대 한 업데이트 합니다.
2.  **AD FS 관리**, 클릭 **클레임 공급자 신뢰** 및 오른쪽 창 righ 클릭 **Active Directory** 선택 하 고 **편집 클레임 규칙**합니다.
3.  에 **편집 클레임 규칙에 대 한 활성 디렉터** 클릭 **규칙 추가**합니다.
4.  에 **변환 클레임 규칙 마법사 추가** 선택 **통과 또는 필터 수신 클레임** 클릭 **다음**합니다.
5.  표시 이름 추가 하 고 선택 **Windows 디바이스 그룹** 에서 **수신 클레임 유형** 드롭다운 합니다.
6.  클릭 **완료**합니다.  클릭 **적용** 및 **확인**합니다. 


### <a name="step-6-on-the-relying-party-where-the-windowsdevicegroup-claims-are-expected-add-a-similar-pass-through-or-transform-claim-rule"></a>6 단계: 'WindowsDeviceGroup' 클레임 예상 되는 위치를 사용 하지 않고 파티에 유사한 '통과' 또는 '변형' 클레임 규칙을 추가 합니다.
2.  **AD FS 관리**, 클릭 **의존 파티 신뢰** 및 오른쪽 창 righ 클릭 RP 및 선택 **클레임 규칙 편집**합니다.
3.  에 **발급 변환 규칙** 클릭 **규칙 추가**합니다.
4.  에 **변환 클레임 규칙 마법사 추가** 선택 **통과 또는 필터 수신 클레임** 클릭 **다음**합니다.
5.  표시 이름 추가 하 고 선택 **Windows 디바이스 그룹** 에서 **수신 클레임 유형** 드롭다운 합니다.
6.  클릭 **완료**합니다.  클릭 **적용** 및 **확인**합니다.

## <a name="validation"></a>유효성 검사
'WindowsDeviceGroup' 클레임 릴리스의 유효성을 검사 하 고 테스트 만들어.Net 4.6 사용 하 여 인식 응용 프로그램을 요구 합니다. 군 SDK 4.0와
ADFS의 의존 파티도 응용 프로그램을 구성 하 고 위의 단계에 지정 된 청구 규칙 업데이트 합니다.
ADFS의 통합 인증 Windows 공급자를 사용 하 여 응용 프로그램에 인증 캐스트할 다음 청구 됩니다.
![유효성 검사](media/AD-FS-Compound-Authentication-and-AD-DS-claims/gpmc9.png)

컴퓨터/장치에 대 한 주장 풍부한 액세스 제어에 대해 이제 소모 될 수 있습니다.

예를 들어 다음 **AdditionalAuthenticationRules** 없으면-The 인증 사용자 보안 그룹의 회원 MFA 호출할 ADFS 알려주는 "-1-5-21-2134745077-1211275016-3050530490-1117"와 컴퓨터 (는 어디에 사용자는 보안 그룹 "S-1-5-21-2134745077-1211275016-3050530490-1115 (WindowsDeviceGroup)" 구성원이 아닙니다에서 인증)

그러나 위의 조건 중 하나를 충족 하는 경우 MFA 호출 하지는 않습니다.

```
'NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1115"])
&& NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "S-1-5-21-2134745077-1211275016-3050530490-1117"])
=> issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
```