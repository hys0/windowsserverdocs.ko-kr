---
title: 디바이스 상태 증명
H1: 해당 없음
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e7b77a4-1c6a-4c21-8844-0df89b63f68d
author: brianlic-msft
ms.date: 10/12/2016
ms.openlocfilehash: 4ee77fba1e82179f6998959b494628e97ac23390
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284222"
---
# <a name="device-health-attestation"></a>디바이스 상태 증명

>적용 대상: Windows Server 2016

Windows 10 버전 1507에 도입된 DHA(장치 상태 증명)에는 다음과 같은 기능이 포함되어 있습니다.

-   [OMA(Open Mobile Alliance) 표준](http://openmobilealliance.org/)에 따라 Windows 10 MDM(모바일 장치 관리) 프레임워크와 통합됩니다.

-   펌웨어 또는 개별 형식으로 프로비전된 TPM(신뢰할 수 있는 플랫폼 모듈)이 있는 장치를 지원합니다.

-   운영 비용에 대한 최소한의 영향으로(또는 영향 없이) 하드웨어에서 모니터링되고 증명되는 보안 수준을 높일 수 있습니다.

Windows Server 2016부터 이제 조직 내에서 서버 역할로 DHA 서비스를 실행할 수 있습니다. 이 항목에서는 장치 상태 증명 서버 역학을 설치하고 구성하는 방법을 알아봅니다.

## <a name="overview"></a>개요

DHA를 사용하여 다음에 대한 장치 상태를 평가할 수 있습니다.
  
-   TPM 1.2 또는 2.0을 지원하는 Windows 10 및 Windows 10 모바일 장치  
-   인터넷에 액세스할 수 있는 Active Directory를 통해 관리되는 온-프레미스 장치, 인터넷에 액세스할 수 없는 Active Directory를 통해 관리되는 장치, Azure Active Directory를 통해 관리되는 장치 또는 Active Directory와 Azure Active Directory 둘 다를 사용하는 하이브리드 배포


### <a name="dha-service"></a>DHA 서비스

DHA 서비스는 장치에 대한 TPM 및 PCR 로그의 유효성을 검사한 다음 DHA 보고서를 생성합니다. Microsoft는 다음 세 가지 방법으로 DHA 서비스를 제공합니다.

- **DHA 클라우드 서비스** 지리적으로 부하 분산되고 전 세계 여러 지역에서 액세스하는 데 최적화된 Microsoft에서 관리하는 무료 DHA 서비스입니다.

- **DHA 온-프레미스 서비스** Windows Server 2016에 도입된 새로운 서버 역할입니다. Windows Server 2016 라이선스가 있는 고객에게 무료로 제공됩니다.

- **DHA Azure 클라우드 서비스** Microsoft Azure의 가상 호스트입니다. 이 작업을 수행하려면 DHA 온-프레미스 서비스에 대한 라이선스와 가상 호스트가 필요합니다.

DHA 서비스는 MDM 솔루션과 통합되어 다음과 같은 이점을 제공합니다. 

-   기존 장치 관리 통신 채널을 통해 장치에서 받은 정보를 DHA 보고서와 결합합니다.
-   하드웨어에서 증명되고 보호되는 데이터를 기반으로 보다 안전하고 신뢰할 수 있는 보안 결정을 내립니다.

다음은 DHA를 사용하여 조직의 자산에 대한 보안 수준을 강화할 수 있는 방법을 보여 주는 예입니다.

1. 다음 부팅 구성/특성을 확인하는 정책을 만듭니다.
   - 보안 부팅
   - BitLocker
   - ELAM
2. MDM 솔루션이 이 정책을 적용하고 DHA 보고서 데이터를 기반으로 수정 작업을 트리거합니다.  예를 들어 다음을 확인할 수 있습니다.
   - 보안 부팅이 사용하도록 설정되고, 장치에서 로드된 신뢰할 수 있는 코드가 인증되었으며, Windows 부팅 로더가 변조되지 않았는지 여부
   - 신뢰할 수 있는 부팅에서 장치가 시작되는 동안 로드된 Windows 커널 및 구성 요소의 디지털 서명을 성공적으로 확인했는지 여부
   - 계획 부팅에서 원격으로 확인할 수 있는 TPM으로 보호된 감사 추적을 생성했는지 여부
   - BitLocker가 사용하도록 설정되고 장치가 꺼져 있는 동안 데이터를 보호하는지 여부
   - ELAM이 초기 부팅 단계에서 사용하도록 설정되고 런타임으로 모니터링하는지 여부
  
#### <a name="dha-cloud-service"></a>DHA 클라우드 서비스

DHA 클라우드 서비스는 다음과 같은 이점을 제공합니다.

-   MDM 솔루션에 등록된 장치에서 받은 TCG 및 PCR 장치 부팅 로그를 검토합니다. 
-   장치의 TPM 칩으로 수집 및 보호되는 데이터를 기반으로 장치가 시작된 방식을 설명하는 변조 방지 및 변조 증명 보고서(DHA 보고서)를 만듭니다. 
-   보호된 통신 채널에서 보고서를 요청한 MDM 서버에 DHA 보고서를 전달합니다.

#### <a name="dha-on-premises-service"></a>DHA 온-프레미스 서비스

DHA 온-프레미스 서비스는 DHA 클라우드 서비스에서 제공하는 모든 기능을 제공합니다.  또한 다음을 지원합니다.

 - 사용자 고유의 데이터 센터에서 DHA 서비스를 실행하여 성능을 최적화할 수 있습니다.
 - DHA 보고서가 네트워크에서 유출되지 않는지 확인할 수 있습니다.

#### <a name="dha-azure-cloud-service"></a>DHA Azure 클라우드 서비스

이 서비스는 Microsoft Azure에서 가상 호스트로 실행된다는 점을 제외하고는 DHA 온-프레미스 서비스와 동일한 기능을 제공합니다.

### <a name="dha-validation-modes"></a>DHA 유효성 검사 모드

EKCert 또는 AIKCert 유효성 검사 모드로 실행되도록 DHA 온-프레미스 서비스를 설정할 수 있습니다. DHA 서비스는 보고서를 생성할 때 AIKCert 또는 EKCert 유효성 검사 모드에서 생성했음을 나타냅니다. AIKCert과 EKCert 유효성 검사 모드는 EKCert 신뢰 체인이 최신 상태로 유지되는 한 동일한 보안 보증을 제공합니다.

#### <a name="ekcert-validation-mode"></a>EKCert 유효성 검사 모드

EKCert 유효성 검사 모드는 인터넷에 연결되지 않은 조직의 장치에 최적화되어 있습니다. EKCert 유효성 검사 모드로 실행되는 DHA 서비스에 연결하는 장치는 인터넷에 직접 액세스할 수 **없습니다**.

DHA가 EKCert 유효성 검사 모드로 실행되는 경우에는 종종(대략 1년에 5~10번) 업데이트해야 하는 엔터프라이즈 관리 신뢰 체인에 의존합니다. 

Microsoft는 승인된 TPM 제조업체에 대한 신뢰할 수 있는 루트 및 중간 CA의 집계된 패키지를 공개적으로 액세스할 수 있는 .cab 보관 파일에 게시합니다. 피드를 다운로드하고 유효성을 검사한 후 장치 상태 증명을 실행하는 서버에 설치해야 합니다.

보관 파일의 예 [ https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab ](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab)합니다.

#### <a name="aikcert-validation-mode"></a>AIKCert 유효성 검사 모드

AIKCert 유효성 검사 모드는 인터넷에 액세스할 수 없는 운영 환경에 최적화되어 있습니다. AIKCert 유효성 검사 모드로 실행되는 DHA 서비스에 연결하는 장치는 인터넷에 직접 액세스할 수 있어야 하며 Microsoft에서 AIK 인증서를 받을 수 있습니다. 

## <a name="install-and-configure-the-dha-service-on-windows-server-2016"></a>Windows Server 2016에서 DHA 서비스 설치 및 구성

다음 섹션을 사용하여 Windows Server 2016에서 DHA를 설치하고 구성할 수 있습니다.

### <a name="prerequisites"></a>사전 요구 사항

DHA 온-프레미스 서비스를 설치하고 확인하려면 다음이 필요합니다.

- Windows Server 2016을 실행하는 서버
- 최신 Windows Insider 빌드를 실행하는 일반/준비 상태의 TPM(1.2 또는 2.0) 설치 Windows 10 클라이언트 장치(하나 이상)
- 실행할 유효성 검사 모드(EKCert 또는 AIKCert) 결정
- 다음 인증서:
  - **DHA SSL 인증서** 내보낼 수 있는 프라이빗 키가 있으며 엔터프라이즈 신뢰할 수 있는 루트에 연결된 x.509 SSL 인증서입니다. 이 인증서는 서버 간(DHA 서비스와 MDM 서버) 통신과 서버-클라이언트(DHA 서비스와 Windows 10 장치) 통신을 포함하여 전송 중인 DHA 데이터 통신을 보호합니다.
  - **DHA 서명 인증서** 내보낼 수 있는 프라이빗 키가 있으며 엔터프라이즈 신뢰할 수 있는 루트에 연결된 x.509 인증서입니다. DHA 서비스는 디지털 서명에 이 인증서를 사용합니다. 
  - **DHA 암호화 인증서** 내보낼 수 있는 프라이빗 키가 있으며 엔터프라이즈 신뢰할 수 있는 루트에 연결된 x.509 인증서입니다. DHA 서비스는 암호화에 이 인증서를 사용합니다. 


### <a name="install-windows-server-2016"></a>Windows Server 2016 설치

Windows 배포 서비스 등의 기본 설정된 설치 방법을 사용하거나 부팅 가능한 미디어, USB 드라이브 또는 로컬 파일 시스템에서 설치 관리자를 실행하여 Windows Server 2016을 설치합니다. DHA 온-프레미스 서비스를 처음 구성하는 경우 **데스크톱 환경** 설치 옵션을 사용하여 Windows Server 2016을 설치해야 합니다.

### <a name="add-the-device-health-attestation-server-role"></a>장치 상태 증명 서버 역할 추가

서버 관리자를 사용하여 장치 상태 증명 서버 역할 및 해당 종속성을 설치할 수 있습니다. 

Windows Server 2016을 설치하면 장치가 다시 시작되고 서버 관리자가 열립니다. 서버 관리자가 자동으로 시작되지 않으면 **시작**을 클릭한 다음 **서버 관리자**를 클릭합니다.

1.  **역할 및 기능 추가**를 클릭합니다.
2.  **시작하기 전** 페이지에서 **다음**을 클릭합니다.
3.  **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭한 다음 **다음**을 클릭합니다.
4.  **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭하고 서버를 선택한 후 **다음**을 클릭합니다.
5.  **서버 역할 선택** 페이지에서 **장치 상태 증명** 확인란을 선택합니다.
6.  **기능 추가**를 클릭하여 다른 필요한 역할 서비스 및 기능을 설치합니다.
7.  **다음**을 클릭합니다.
8.  **기능 선택** 페이지에서 **다음**을 클릭합니다.
9.  **웹 서버 역할(IIS)** 페이지에서 **다음**을 클릭합니다.
10. **역할 서비스 선택** 페이지에서 **다음**을 클릭합니다.
11. **장치 상태 증명 서비스** 페이지에서 **다음**을 클릭합니다.
12. **설치 선택 확인** 페이지에서 **설치**를 클릭합니다.
13. 설치가 완료되면 **닫기**를 클릭합니다.

### <a name="install-the-signing-and-encryption-certificates"></a>서명 및 암호화 인증서 설치

다음 Windows PowerShell 스크립트를 사용하여 서명 및 암호화 인증서를 설치합니다. 지문에 대 한 자세한 내용은 참조 하세요. [방법: 인증서의 지문 검색](https://msdn.microsoft.com/library/ms734695.aspx)합니다.

```
$key = Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Thumbprint -like "<thumbprint>"}
$keyname = $key.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
$keypath = $env:ProgramData + "\Microsoft\Crypto\RSA\MachineKeys\" + $keyname
icacls $keypath /grant <username>`:R
  
#<thumbprint>: Certificate thumbprint for encryption certificate or signing certificate
#<username>: Username for web service app pool, by default IIS_IUSRS
```

### <a name="install-the-trusted-tpm-roots-certificate-package"></a>신뢰할 수 있는 TPM 루트 인증서 패키지 설치

신뢰할 수 있는 TPM 루트 인증서 패키지를 설치하려면 해당 패키지를 추출하여 조직에서 신뢰하지 않는 신뢰 체인을 제거한 다음 setup.cmd를 실행합니다.

#### <a name="download-the-trusted-tpm-roots-certificate-package"></a>신뢰할 수 있는 TPM 루트 인증서 패키지 다운로드

인증서 패키지를 설치 하기 전에에서 신뢰할 수 있는 TPM 루트의 최신 목록을 다운로드할 수 있습니다 [ https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab ](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab)합니다.

> **중요:** 패키지를 설치 하기 전에 Microsoft에서 디지털 서명 되었는지 확인 합니다.

#### <a name="extract-the-trusted-certificate-package"></a>신뢰할 수 있는 인증서 패키지를 추출합니다.
다음 명령을 실행하여 신뢰할 수 있는 인증서 패키지를 추출합니다.
```
mkdir .\TrustedTpm
expand -F:* .\TrustedTpm.cab .\TrustedTpm
```

#### <a name="remove-the-trust-chains-for-tpm-vendors-that-are-not-trusted-by-your-organization-optional"></a>조직에서 신뢰하지 *않는* TPM 공급업체에 대한 신뢰 체인을 제거합니다(선택 사항).

조직에서 신뢰하지 않는 TPM 공급업체 신뢰 체인에 대한 폴더를 삭제합니다.

> **참고:** AIK 인증서 모드를 사용 하는 경우 Microsoft 발행 한 AIK 인증서의 유효성을 검사 하려면 Microsoft 폴더가 필요 합니다.

#### <a name="install-the-trusted-certificate-package"></a>신뢰할 수 있는 인증서 패키지 설치
.cab 파일에서 설치 스크립트를 실행하여 신뢰할 수 있는 인증서 패키지를 설치합니다.

```
.\setup.cmd
```

### <a name="configure-the-device-health-attestation-service"></a>장치 상태 증명 서비스 구성

Windows PowerShell을 사용하여 DHA 온-프레미스 서비스를 구성할 수 있습니다.

```
Install-DeviceHealthAttestation -EncryptionCertificateThumbprint <encryption> -SigningCertificateThumbprint <signing> -SslCertificateStoreName My -SslCertificateThumbprint <ssl> -SupportedAuthenticationSchema "<schema>"

#<encryption>: Thumbprint of the encryption certificate
#<signing>: Thumbprint of the signing certificate
#<ssl>: Thumbprint of the SSL certificate
#<schema>: Comma-delimited list of supported schemas including AikCertificate, EkCertificate, and AikPub
```

### <a name="configure-the-certificate-chain-policy"></a>인증서 체인 정책 구성

다음 Windows PowerShell 스크립트를 실행하여 인증서 체인 정책을 구성합니다.

```
$policy = Get-DHASCertificateChainPolicy
$policy.RevocationMode = "NoCheck"
Set-DHASCertificateChainPolicy -CertificateChainPolicy $policy
```

## <a name="dha-management-commands"></a>DHA 관리 명령

다음은 DHA 서비스를 관리하는 데 유용한 몇 가지 Windows PowerShell 예입니다.

### <a name="configure-the-dha-service-for-the-first-time"></a>처음으로 DHA 서비스 구성

```
Install-DeviceHealthAttestation -SigningCertificateThumbprint "<HEX>" -EncryptionCertificateThumbprint "<HEX>" -SslCertificateThumbprint "<HEX>" -Force
```

### <a name="remove-the-dha-service-configuration"></a>DHA 서비스 구성 제거

```
Uninstall-DeviceHealthAttestation -RemoveSslBinding -Force
```
### <a name="get-the-active-signing-certificate"></a>활성 서명 인증서 가져오기

```
Get-DHASActiveSigningCertificate
```
### <a name="set-the-active-signing-certificate"></a>활성 서명 인증서 설정

```
Set-DHASActiveSigningCertificate -Thumbprint "<hex>" -Force
```

> **참고:** 이 인증서 DHA 서비스를 실행 하는 서버에 배포 되어 있어야 합니다 **LocalMachine\My** 인증서 저장소입니다. 활성 서명 인증서가 설정되면 기존 활성 서명 인증서가 비활성 서명 인증서 목록으로 이동합니다.

### <a name="list-the-inactive-signing-certificates"></a>비활성 서명 인증서 나열
```
Get-DHASInactiveSigningCertificates
```

### <a name="remove-any-inactive-signing-certificates"></a>비활성 서명 인증서 제거
```
Remove-DHASInactiveSigningCertificates -Force
Remove-DHASInactiveSigningCertificates  -Thumbprint "<hex>" -Force
```

> **참고:** 만 *하나의* 비활성 인증서 (모든 유형)에 언제 든 지 서비스에 존재할 수 있습니다. 더 이상 필요 없는 경우 비활성 인증서 목록에서 인증서를 제거해야 합니다.

### <a name="get-the-active-encryption-certificate"></a>활성 암호화 인증서 가져오기

```
Get-DHASActiveEncryptionCertificate
```

### <a name="set-the-active-encryption-certificate"></a>활성 암호화 인증서 설정

```
Set-DHASActiveEncryptionCertificate -Thumbprint "<hex>" -Force
```

장치의 **LocalMachine\My** 인증서 저장소에 인증서를 배포해야 합니다. 

활성 암호화 인증서가 설정되면 기존 활성 암호화 인증서가 비활성 암호화 인증서 목록으로 이동합니다.

### <a name="list-the-inactive-encryption-certificates"></a>비활성 암호화 인증서 나열

```
Get-DHASInactiveEncryptionCertificates
```
### <a name="remove-any-inactive-encryption-certificates"></a>비활성 암호화 인증서 제거

```
Remove-DHASInactiveEncryptionCertificates -Force
Remove-DHASInactiveEncryptionCertificates -Thumbprint "<hex>" -Force 
```

### <a name="get-the-x509chainpolicy-configuration"></a>X509ChainPolicy 구성 가져오기 

```
Get-DHASCertificateChainPolicy
```
### <a name="change-the-x509chainpolicy-configuration"></a>X509ChainPolicy 구성 변경

```
$certificateChainPolicy = Get-DHASInactiveEncryptionCertificates
$certificateChainPolicy.RevocationFlag = <X509RevocationFlag>
$certificateChainPolicy.RevocationMode = <X509RevocationMode>
$certificateChainPolicy.VerificationFlags = <X509VerificationFlags>
$certificateChainPolicy.UrlRetrievalTimeout = <TimeSpan>
Set-DHASCertificateChainPolicy = $certificateChainPolicy
```

## <a name="dha-service-reporting"></a>DHA 서비스 보고

다음은 DHA 서비스가 MDM 솔루션에 보고하는 메시지 목록입니다. 

- **200** HTTP 정상. 인증서가 반환되었습니다.
- **400** 잘못된 요청. 잘못된 요청 형식, 잘못된 상태 인증서, 인증서 서명이 일치하지 않음, 잘못된 상태 증명 Blob 또는 잘못된 상태 Blob. 진단에 사용할 수 있는 오류 코드 및 오류 메시지와 함께 응답 스키마에서 설명하는 메시지가 포함될 수도 있습니다.
- **500** 내부 서버 오류. 서비스에서 인증서를 발행하지 못하도록 하는 문제가 발생한 경우에 발생할 수 있습니다.
- **503** 서버 과부하를 방지하기 위해 스로틀에서 요청을 거부함 
