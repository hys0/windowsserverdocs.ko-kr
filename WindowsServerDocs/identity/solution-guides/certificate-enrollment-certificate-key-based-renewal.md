---
title: 사용자 지정 포트에서 인증서 키 기반 갱신에 대 한 인증서 등록 웹 서비스 구성
description: ''
author: Deland-Han
ms.author: delhan
manager: dcscontentpm
ms.date: 11/1/2019
ms.topic: article
ms.prod: windows-server
ms.openlocfilehash: a5fea6681376abf6ea9ada67e31b10369256ea81
ms.sourcegitcommit: 9e123d475f3755218793a130dda88455eac9d4ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73413460"
---
# <a name="configuring-certificate-enrollment-web-service-for-certificate-key-based-renewal-on-a-custom-port"></a>사용자 지정 포트에서 인증서 키 기반 갱신에 대 한 인증서 등록 웹 서비스 구성

<!-- <Author(s): Jitesh Thakur, Meera Mohideen, Ankit Tyagi.-->  

## <a name="summary"></a>요약

이 문서에서는 인증서 키 기반 갱신을 수행 하기 위해 443 이외의 사용자 지정 포트에서 인증서 등록 웹 서비스 (또는 CEP (인증서 등록 정책)/CES (인증서 등록 서비스)를 구현 하는 단계별 지침을 제공 합니다. CEP 및 CES의 자동 갱신 기능을 활용 합니다.

또한이 문서에서는 CEP 및 CES가 작동 하는 방식에 대해 설명 하 고 설치 지침을 제공 합니다.

> [!Note]
> 이 문서에 포함 된 워크플로는 특정 시나리오에 적용 됩니다. 다른 상황에서는 동일한 워크플로가 작동 하지 않을 수 있습니다. 그러나 원칙은 동일 하 게 유지 됩니다.
>
> 고 지 사항:이 설정은 CEP 및 CES 서버에 대 한 기본 HTTPS 통신에 포트 443을 사용 하지 않으려는 특정 요구 사항에 대해 만들어집니다. 이 설정은 가능 하지만 지원 가능성은 제한적입니다. 제공 된 웹 서버 구성에서 최소한의 편차를 사용 하 여이 가이드를 신중 하 게 수행 하는 경우 고객 서비스 및 지원에 가장 도움이 될 수 있습니다.

## <a name="scenario"></a>시나리오

이 예의 경우 지침은 다음 구성을 사용 하는 환경을 기반으로 합니다.

- AD CS (Active Directory 인증서 서비스) PKI (공개 키 인프라)가 있는 Contoso.com 포리스트입니다.

- 서비스 계정으로 실행 되는 하나의 서버에 구성 된 두 개의 CEP/CES 인스턴스 한 인스턴스는 초기 등록에 사용자 이름 및 암호를 사용 합니다. 다른는 갱신 전용 모드에서 키 기반 갱신에 인증서 기반 인증을 사용 합니다.

- 사용자에 게 사용자 이름 및 암호 자격 증명을 사용 하 여 컴퓨터 인증서를 등록 하는 작업 그룹 또는 도메인에 가입 되지 않은 컴퓨터가 있습니다.

- 사용자가 HTTPS를 통해 CEP 및 CES에서 연결 하는 것은 49999와 같은 사용자 지정 포트에서 발생 합니다. 이 포트는 동적 포트 범위에서 선택 되며 다른 모든 서비스에서 정적 포트로 사용 되지 않습니다.

- 인증서 수명이 끝에 가까워지면 컴퓨터는 인증서 기반 CES 키 기반 갱신을 사용 하 여 동일한 채널을 통해 인증서를 갱신 합니다.

![배포](media/certificate-enrollment-certificate-key-based-renewal-1.png)

## <a name="configuration-instructions"></a>구성 지침

### <a name="overview"></a>개요 

1. 키 기반 갱신에 대 한 템플릿을 구성 합니다.

2. 필수 구성 요소로 서, 사용자 이름 및 암호 인증을 위해 CEP 및 CES 서버를 구성 합니다.   
   이 환경에서는 인스턴스를 "CEPCES01"로 참조 합니다.

3.  동일한 서버에서 인증서 기반 인증을 위해 PowerShell을 사용 하 여 다른 CEP 및 CES 인스턴스를 구성 합니다. CES 인스턴스는 서비스 계정을 사용 합니다.

    이 환경에서는 인스턴스를 "CEPCES02"로 참조 합니다. 사용 되는 서비스 계정은 "cepcessvc"입니다.

4.  클라이언트 쪽 설정을 구성 합니다.

### <a name="configuration"></a>구성

이 섹션에서는 초기 등록을 구성 하는 단계를 제공 합니다.

> [!Note]
> 또한 CES를 사용할 모든 사용자 서비스 계정, MSA 또는 GMSA을 구성할 수 있습니다.

필수 구성 요소로 서, 사용자 이름 및 암호 인증을 사용 하 여 서버에서 CEP 및 CES를 구성 해야 합니다.

#### <a name="configure-the-template-for-key-based-renewal"></a>키 기반 갱신을 위한 템플릿 구성

기존 컴퓨터 템플릿을 복제 하 고 템플릿의 다음 설정을 구성할 수 있습니다.

1. 인증서 템플릿의 주체 이름 탭에서 **요청** 및 **자동 등록 갱신 요청에 대 한 기존 인증서의 주체 정보 사용** 옵션을 선택 했는지 확인 합니다.
   새 템플릿 ![](media/certificate-enrollment-certificate-key-based-renewal-2.png) 

2. **발급 요구 사항** 탭으로 전환한 다음 **CA 인증서 관리자 승인** 확인란을 선택 합니다.
   ![발급 요구 사항](media/certificate-enrollment-certificate-key-based-renewal-3.png) 

3. 이 템플릿의 **cepcessvc** 서비스 계정에 **읽기** 및 **등록** 권한을 할당 합니다.

4. CA에 새 템플릿을 게시 합니다.

> [!Note]
> 호환 되는 Windows Server 2016 이상 버전으로 설정 된 경우 템플릿이 표시 되지 않는 알려진 문제가 있으므로 템플릿의 호환성 설정이 **Windows server 2012** r 2로 설정 되어 있는지 확인 합니다. 자세한 읽으십시오 windows server [2016 이상 기반 ca 또는 CEP 서버에서 Windows server 2016 CA 호환 인증서 템플릿을 선택할 수 없음 ](https://support.microsoft.com/en-in/help/4508802/cannot-select-certificate-templates-in-windows-server-2016)을 참조 하세요.


#### <a name="configure-the-cepces01-instance"></a>CEPCES01 인스턴스 구성

##### <a name="step-1-install-the-instance"></a>1 단계: 인스턴스 설치

CEPCES01 인스턴스를 설치 하려면 다음 방법 중 하나를 사용 합니다.

**방법 1**

사용자 이름 및 암호 인증에 CEP 및 CES를 사용 하도록 설정 하는 단계별 지침은 다음 문서를 참조 하세요.

[인증서 등록 정책 웹 서비스 지침](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831625(v=ws.11))

[인증서 등록 웹 서비스 지침](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831822(v=ws.11)#configure-a-ca-for-the-certificate-enrollment-web-service)

> [!Note]
> 사용자 이름 및 암호 인증의 CEP 및 CES 인스턴스를 모두 구성 하는 경우 "키 기반 갱신 사용" 옵션을 선택 하지 않아야 합니다.

**방법 2**

다음 PowerShell cmdlet을 사용 하 여 CEP 및 CES 인스턴스를 설치할 수 있습니다.

```PowerShell
Import-Module ServerManager
Add-WindowsFeature Adcs-Enroll-Web-Pol
Add-WindowsFeature Adcs-Enroll-Web-Svc
```

```PowerShell
Install-AdcsEnrollmentPolicyWebService -AuthenticationType Username -SSLCertThumbprint "sslCertThumbPrint"
```

이 명령은 인증에 사용자 이름과 암호를 사용 하도록 지정 하 여 인증서 등록 정책 웹 서비스 (CEP)를 설치 합니다. 

> [!Note]
> 이 명령에서 \<**Sslcertthumbprint**\>은 IIS를 바인딩하는 데 사용 되는 인증서의 지문입니다.

```PowerShell
Install-AdcsEnrollmentWebService -ApplicationPoolIdentity -CAConfig "CA1.contoso.com\contoso-CA1-CA" -SSLCertThumbprint "sslCertThumbPrint" -AuthenticationType Username
```

이 명령은 **CA1.contoso.com** 의 컴퓨터 이름에 인증 기관을 사용 하는 CES (인증서 등록 웹 서비스)와 **c a 1**의 ca 일반 이름을 사용 합니다. CES id는 기본 응용 프로그램 풀 id로 지정 됩니다. 인증 유형이 **username**입니다. SSLCertThumbPrint은 IIS를 바인딩하는 데 사용 되는 인증서의 지문입니다.

##### <a name="step-2-check-the-internet-information-services-iis-manager-console"></a>2 단계 인터넷 정보 서비스 (IIS) 관리자 콘솔 확인

설치가 완료 되 면 인터넷 정보 서비스 (IIS) 관리자 콘솔에 다음 표시가 표시 될 것입니다.
![IIS 관리자](media/certificate-enrollment-certificate-key-based-renewal-4.png) 

**기본 웹 사이트**에서 **KeyBasedRenewal_ADPolicyProvider_CEP_Certificate**을 선택 하 고 **응용 프로그램 설정**을 엽니다. **ID** 와 **URI**를 확인 합니다.

관리를 위해 **친숙 한 이름을** 추가할 수 있습니다.

#### <a name="configure-the-cepces02-instance"></a>CEPCES02 인스턴스 구성

##### <a name="step-1-install-the-cep-and-ces-for-key-based-renewal-on-the-same-server"></a>1 단계: 동일한 서버에 키 기반 갱신을 위한 CEP 및 CES를 설치 합니다. 

PowerShell에서 다음 명령을 실행 합니다.

```PowerShell
Install-AdcsEnrollmentPolicyWebService -AuthenticationType Certificate -SSLCertThumbprint "sslCertThumbPrint" -KeyBasedRenewal
```

이 명령은 인증서 등록 정책 웹 서비스 (CEP)를 설치 하 고 인증에 인증서를 사용 하도록 지정 합니다. 

> [!Note]
> 이 명령에서 \<SSLCertThumbPrint\>은 IIS를 바인딩하는 데 사용 되는 인증서의 지문입니다. 

키 기반 갱신을 통해 인증서 클라이언트는 인증을 위해 기존 인증서의 키를 사용 하 여 인증서를 갱신할 수 있습니다. 키 기반 갱신 모드에서 서비스는 키 기반 갱신에 대해 설정 된 인증서 템플릿만 반환 합니다.

```PowerShell
Install-AdcsEnrollmentWebService -CAConfig "CA1.contoso.com\contoso-CA1-CA" -SSLCertThumbprint "sslCertThumbPrint" -AuthenticationType Certificate -ServiceAccountName "Contoso\cepcessvc" -ServiceAccountPassword (read-host "Set user password" -assecurestring) -RenewalOnly -AllowKeyBasedRenewal
```

이 명령은 **CA1.contoso.com** 의 컴퓨터 이름에 인증 기관을 사용 하는 CES (인증서 등록 웹 서비스)와 **c a 1**의 ca 일반 이름을 사용 합니다. 

이 명령에서 인증서 등록 웹 서비스 id는 **cepcessvc** 서비스 계정으로 지정 됩니다. 인증 유형이 **certificate**입니다. **Sslcertthumbprint** 은 IIS를 바인딩하는 데 사용 되는 인증서의 지문입니다.

**RenewalOnly** cmdlet을 사용 하면 CES를 갱신 전용 모드로 실행할 수 있습니다. 또한 **AllowKeyBasedRenewal** CMDLET은 CES가 등록 서버에 대 한 키 기반 갱신 요청을 허용 하도록 지정 합니다. 이러한 인증서는 보안 주체에 직접 매핑되지 않는 인증에 대 한 유효한 클라이언트 인증서입니다.

> [!Note]
> 서비스 계정은 서버에서 **Iisusers** 그룹의 일부 여야 합니다.

##### <a name="step-2-check-the-iis-manager-console"></a>2 단계 IIS 관리자 콘솔 확인

성공적으로 설치한 후에는 IIS 관리자 콘솔에 다음 표시가 표시 될 것입니다.
![IIS 관리자](media/certificate-enrollment-certificate-key-based-renewal-5.png) 

**기본 웹 사이트** 아래에서 **KeyBasedRenewal_ADPolicyProvider_CEP_Certificate** 을 선택 하 고 **응용 프로그램 설정**을 엽니다. **ID** 와 **URI**를 적어 둡니다. 관리를 위해 **친숙 한 이름을** 추가할 수 있습니다.

> [!Note]
> 인스턴스가 새 서버에 설치 되어 있고 id가 다르고 id가 재시도가 id가 CEPCES01 인스턴스에 사용 된 ID와 동일한 지 확인 합니다. 값을 직접 복사 하 여 붙여 넣을 수 있습니다.

#### <a name="complete-certificate-enrollment-web-services-configuration"></a>인증서 등록 웹 서비스 구성 완료

CEP 및 CES의 기능을 대신 하 여 인증서를 등록할 수 있으려면 작업 그룹의 컴퓨터 Active Directory 계정을 구성 하 고 서비스 계정에 대해 제한 된 위임을 구성 해야 합니다.

##### <a name="step-1-create-a-computer-account-of-the-workgroup-computer-in-active-directory"></a>1 단계: Active Directory에서 작업 그룹 컴퓨터의 컴퓨터 계정 만들기

이 계정은 키 기반 갱신에 대 한 인증 및 인증서 템플릿에 대 한 "Active Directory에 게시" 옵션에 사용 됩니다.

![새 개체](media/certificate-enrollment-certificate-key-based-renewal-6.png) 
 
##### <a name="step-2-configure-the-service-account-for-constrained-delegation-s4u2self"></a>2 단계: 제한 된 위임에 대 한 서비스 계정 구성 (위해 s4u2self)

다음 PowerShell 명령을 실행 하 여 제한 된 위임 (위해 s4u2self 또는 any authentication protocol)을 사용 하도록 설정 합니다.

```PowerShell
Get-ADUser -Identity cepcessvc | Set-ADAccountControl -TrustedToAuthForDelegation $True
Set-ADUser -Identity cepcessvc -Add @{'msDS-AllowedToDelegateTo'=@('HOST/CA1.contoso.com','RPCSS/CA1.contoso.com')}
```

> [!Note]
> 이 명령에서 <cepcessvc>은 서비스 계정이 고 < > C A 1는 인증 기관입니다.

> [!Important]
> Microsoft는 제한 된 위임을 사용 하 여 동일한 작업을 수행 하기 때문에이 구성에서 CA에 RENEWALONBEHALOF 플래그를 사용 하도록 설정 하지 않습니다. 이렇게 하면 서비스 계정에 대 한 권한을 CA의 보안에 추가 하지 않아도 됩니다.

##### <a name="step-3-configure-a-custom-port-on-the-iis-web-server"></a>3 단계: IIS 웹 서버에서 사용자 지정 포트 구성

1. IIS 관리자 콘솔에서 기본 웹 사이트를 선택 합니다.

2. 작업 창에서 사이트 바인딩 편집을 선택 합니다. 

3. 기본 포트 설정을 443에서 사용자 지정 포트로 변경 합니다. 예제 스크린샷에서는 49999의 포트 설정을 보여 줍니다.
   포트 변경 ![](media/certificate-enrollment-certificate-key-based-renewal-7.png) 

##### <a name="step-4-edit-the-ca-enrollment-services-object"></a>4 단계: CA 등록 서비스 개체 편집

1. 도메인 컨트롤러에서 adsiedit를 엽니다.

2. 구성 파티션에 연결 하 고 CA 등록 서비스 개체로 이동 합니다.
   
   CN = ENTCA, CN = 등록 서비스, CN = Public Key Services, CN = Services, CN = Configuration, DC = contoso, DC = com

3. 개체를 편집 하 고 응용 프로그램 설정에서 발견 된 CEP 및 CES 서버 Uri와 사용자 지정 포트를 사용 하 여 Mspki-site-name 특성이 특성을 변경 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

   140 https://cepces.contoso.com:49999/ENTCA_CES_UsernamePassword/service.svc/CES0   
   181 https://cepces.contoso.com:49999/ENTCA_CES_Certificate/service.svc/CES1

   ![ADSI 편집](media/certificate-enrollment-certificate-key-based-renewal-8.png) 

#### <a name="configure-the-client-computer"></a>클라이언트 컴퓨터 구성

클라이언트 컴퓨터에서 등록 정책 및 자동 등록 정책을 설정 합니다. 이렇게 하려면 다음 단계를 따르세요.

1. **시작** > **실행**을 선택 하 고 **gpedit.msc**를 입력 합니다.

2. **컴퓨터 구성** > **Windows 설정** > **보안 설정**으로 이동한 다음 **공개 키 정책**을 클릭 합니다.

3. 다음 스크린샷의 설정과 일치 하도록 **인증서 서비스 클라이언트-자동 등록 정책을** 사용 하도록 설정 합니다.
   ![인증서 그룹 정책](media/certificate-enrollment-certificate-key-based-renewal-9.png)
 
4. **인증서 서비스 클라이언트-인증서 등록 정책**을 사용 하도록 설정 합니다.

   a. **추가** 를 클릭 하 여 등록 정책을 추가 하 고 ADSI에서 편집한 **USERNAMEPASSWORD** 로 CEP URI를 입력 합니다.
   
   b. **인증 유형**으로 **사용자 이름/암호**를 선택 합니다.
   
   c. 우선 순위를 **10**으로 설정 하 고 정책 서버의 유효성을 검사 합니다.
      ![등록 정책](media/certificate-enrollment-certificate-key-based-renewal-10.png)

   > [!Note]
   > 포트 번호가 URI에 추가 되 고 방화벽에서 허용 되는지 확인 합니다.

5. 인증서를 등록 하는 컴퓨터에 대 한 첫 번째 인증서를 등록 합니다.
   ![등록 정책](media/certificate-enrollment-certificate-key-based-renewal-11.png)

   KBR 템플릿을 선택 하 고 인증서를 등록 합니다.
   ![등록 정책](media/certificate-enrollment-certificate-key-based-renewal-12.png)

6. **Gpedit.msc** 를 다시 엽니다. **인증서 서비스 클라이언트-인증서 등록 정책**을 편집 하 고 키 기반 갱신 등록 정책을 추가 합니다.

   a. **추가**를 클릭 하 고 ADSI에서 편집한 **인증서** 를 사용 하 여 CEP URI를 입력 합니다. 
   
   b. 우선 순위 **1**을 설정 하 고 정책 서버의 유효성을 검사 합니다. 인증 하 고 처음에 등록 한 인증서를 선택 하 라는 메시지가 표시 됩니다.

   ![등록 정책](media/certificate-enrollment-certificate-key-based-renewal-13.png) 

> [!Note]
> 키 기반 갱신 등록 정책의 우선 순위 값이 사용자 이름 암호 등록 정책 우선 순위 보다 낮은 지 확인 합니다. 첫 번째 기본 설정은 가장 낮은 우선 순위로 지정 됩니다.

## <a name="testing-the-setup"></a>설치 테스트

자동 갱신이 작동 하는지 확인 하려면 동일한 키를 사용 하 여 수동 갱신이 작동 하는지 확인 합니다. 사용자 이름 및 암호를 입력 하 라는 메시지가 표시 되어서는 안 됩니다.  또한 등록할 때 "인증서를 선택 하 라는 메시지가 표시 됩니다. 이는 예정된 동작입니다.

컴퓨터 개인 인증서 저장소를 열고 "보관 된 인증서" 보기를 추가 합니다. 이렇게 하려면 다음 방법 중 하나를 사용 합니다.

### <a name="method-1"></a>방법 1 

다음 명령을 실행합니다.

```PowerShell
certreq -machine -q -enroll -cert <thumbprint> renew
```

![명령을 사용합니다.](media/certificate-enrollment-certificate-key-based-renewal-14.png)

### <a name="method-2"></a>방법 2

인증서의 유효 기간이 만료 되 면 8의 배수로 시간 설정을 이동 합니다.

예를 들어 예제 인증서는 4:00에 해당 월의 18 일에 실행 되 고, 20에서 4:00에 만료 되며, 2 일 유효성 설정 및 8 시간 갱신 설정이 있습니다. 자동 등록 엔진은 약 8 시간 간격으로 다시 시작 될 때 트리거됩니다.

따라서 시간을 오후 8:10 시로 이동 하는 경우 19 일에서 **Certutil-pulse** 를 실행 하 여 AE 엔진을 트리거하려면 인증서를 등록 합니다.

![명령을 사용합니다.](media/certificate-enrollment-certificate-key-based-renewal-15.png)
 
테스트가 완료 되 면 시간 설정을 원래 값으로 되돌리고 클라이언트 컴퓨터를 다시 시작 합니다.

> [!Note]
> 이전 스크린샷에서는 CA 날짜가 여전히 18로 설정 되어 있으므로 자동 등록 엔진이 예상 대로 작동 하는 것을 보여 주는 예입니다. 따라서 인증서가 계속 발급 됩니다. 실제 상황에서는 이러한 많은 양의 갱신이 발생 하지 않습니다.

## <a name="references"></a>참조

[테스트 랩 가이드: 인증서 키 기반 갱신 시연](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj590165(v%3Dws.11))

[인증서 등록 웹 서비스](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/Certificate-Enrollment-Web-Services/ba-p/397385)

[AdcsEnrollmentPolicyWebService](https://docs.microsoft.com/powershell/module/adcsdeployment/install-adcsenrollmentpolicywebservice?view=win10-ps)

[AdcsEnrollmentWebService](https://docs.microsoft.com/powershell/module/adcsdeployment/install-adcsenrollmentwebservice?view=win10-ps)

참고 항목

[Windows Server 보안 포럼](https://aka.ms/adcsforum)

[Active Directory 인증서 서비스 (AD CS) PKI (공개 키 인프라)에 대 한 FAQ (질문과 대답)](https://aka.ms/adcsfaq)

[Windows PKI 설명서 참조 및 라이브러리](https://social.technet.microsoft.com/wiki/contents/articles/987.windows-pki-documentation-reference-and-library.aspx)

[Windows PKI 블로그](https://blogs.technet.com/b/pki/)

[웹 등록 프록시 페이지의 사용자 지정 서비스 계정에서 Kerberos 제한 된 위임 (S4U2Proxy 또는 Kerberos만)을 구성 하는 방법](https://support.microsoft.com/help/4494313/configuring-web-enrollment-proxy-for-s4u2proxy-constrained-delegation)