---
title: "장치 상태 대"
H1: na
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology:
- techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e7b77a4-1c6a-4c21-8844-0df89b63f68d
author: brianlic-msft
ms.date: 10/12/2016
ms.openlocfilehash: d304ee3456f8db1e5b202c1d9221d1374a5251be
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="device-health-attestation"></a>장치 상태 대

>Windows Server 2016 적용 됩니다.

Windows 10 버전 1507에 도입 장치 건강 대 (DHA)는 다음과 같습니다.

-   Windows 10 Mobile 디바이스 관리 MDM () 프레임 워크에 맞춰와 통합 [열기 모바일 Alliance (OMA) 표준](http://openmobilealliance.org/)합니다.

-   장치를 신뢰할 수 있는 플랫폼 TPM () 펌웨어 또는 이산 형식 프로 비전을 지원 합니다.

-   하드웨어 조직의 보안 막대를 사용 하면 기업 모니터링 하 고 attested 최소한의 보안 또는 작업 비용에 영향을 주지 않습니다.

Windows Server 2016 부터는 이제 실행할 수 있습니다 DHA 서비스 서버 역할로 조직 내 합니다. 이 항목을 사용 하 여 설치 하 고 장치 건강 증명 서버 역할을 구성 하는 방법을 알아보세요.

## <a name="overview"></a>개요

장치 상태에 대 한 평가를 DHA를 사용할 수 있습니다.
  
-   TPM 1.2 또는 2.0 지 원하는 Windows 10 및 Windows 10 Mobile 디바이스입니다.  
-   온-프레미스 사용 하 여 Active Directory 인터넷에 액세스할 수 있는 장치 관리 Azure Active Directory 또는 Active Directory 및 Azure Active Directory를 사용 하 여 하이브리드 배포 하는 인터넷 액세스를 않고도 Active Directory를 사용 하 여 관리 되는 디바이스 관리 하는 디바이스입니다.


### <a name="dha-service"></a>DHA 서비스

DHA 서비스는 디바이스에 대 한 TPM 및 PCR 로그의 유효성을 검사을 다음 DHA 보고서를 표시 합니다. Microsoft는 세 가지 방법으로 DHA 서비스를 제공합니다.

- **DHA 클라우드 서비스**, 되는 무료 지리적-부하가, 전 세계의 다양 한 지역에서 액세스에 대 한 최적화 된 DHA A Microsoft 관리 되는 서비스입니다.

- **DHA 온-프레미스 서비스** Windows Server 2016에 도입 된 새로운 서버 역할 합니다. Windows Server 2016 라이선스가 있는 고객에 게 무료로 제공 됩니다.

- **DHA Azure 클라우드 서비스** 가상 호스트 Microsoft Azure에 있습니다. 이렇게 하려면 가상 호스트 및 라이선스 DHA 온-프레미스 서비스에 대 한 합니다.

DHA 서비스 MDM 솔루션을 통합 하 고 다음을 제공 합니다. 

-   결합 DHA 보고서와 함께 (기존 장치 관리 통신 채널)을 통해 디바이스에서 수신 하는 정보
-   더 안전 하 고 신뢰할 수 있는 보안 결정을 기반으로 하드웨어 attested 및 데이터를 보호 합니다.

DHA 조직의 자산에 대 한 보안 보호 막대를 사용 하는 방법을 보여 주는 예는 다음과 같습니다.

1. 부팅 구성/특성을 확인 하는 정책을 만들 있습니다.
  - 보안 부팅
  - BitLocker
  - ELAM
2. MDM 솔루션이이 정책이 적용 및 DHA 보고서 데이터에 따라 조치를 시작 합니다.  예를 들어 다음 확인할 수 있습니다.
  - 보안 부팅을 사용 하도록 설정 된, 디바이스는 의미를 신뢰할 수 있는 코드 로드 하 고 Windows 부팅 loader 손상 되지 않았음을 합니다.
  - Windows 커널 및 디바이스에서 시작 하는 동안 로드 된 구성 요소 디지털 서명 부팅을 성공적으로 확인 신뢰할 수 있습니다.
  - 계획된 부팅 만든 원격으로 확인할 수 있는 TPM 암호로 보호 된 감사 합니다.
  - BitLocker를 활성화 하 고 디바이스를 설정 하는 데이터 보호 냅니다.
  - ELAM 부팅 초기 단계에서 활성화 된 고 런타임은 있습니다.
  
#### <a name="dha-cloud-service"></a>DHA 클라우드 서비스

DHA 클라우드 서비스는 다음과 같은 이점을 제공합니다.

-   MDM 솔루션으로 등록 된 디바이스에서 수신 TCG 및 PCR 장치가 부팅 로그 검토 합니다. 
-   방지 훼손와 디바이스에 따라 데이터를 수집 하 고 디바이스의 TPM 칩에 의해 보호를 시작 하는 방법을 설명 하는 훼손 분명 하 게 보고서 (DHA 보고서)을 만듭니다. 
-   보호 통신 채널에 대 한 보고서를 요청한 MDM 서버에 DHA 보고서를 제공 합니다.

#### <a name="dha-on-premises-service"></a>온-프레미스 DHA 서비스

온-프레미스 DHA 서비스 DHA 클라우드 서비스에서 제공 되는 모든 기능을 제공 합니다.  또한 고객이 수 있습니다.

 - 데이터 센터에 DHA 서비스를 실행 하 여 성능을 최적화합니다
 - DHA 보고서 네트워크 남지 않습니다 있는지 확인

#### <a name="dha-azure-cloud-service"></a>DHA Azure 클라우드 서비스

이 서비스 DHA Azure 클라우드 서비스의 Microsoft Azure 가상 호스트도 실행 한다는 점을 제외 DHA 온-프레미스 서비스와 같은 기능을 제공 합니다.

### <a name="dha-validation-modes"></a>DHA 유효성 검사 모드

EKCert 또는 AIKCert 유효성 검사 모드에서 실행 하도록 DHA 온-프레미스 서비스를 설정할 수 있습니다. DHA 서비스 문제 보고서를 AIKCert 또는 EKCert 유효성 검사 모드로 발급 된 나타냅니다. AIKCert 및 EKCert 유효성 검사 모드 신뢰 EKCert 체인이 최신 상태로 유지으로 동일한 보안 보증을 제공 합니다.

#### <a name="ekcert-validation-mode"></a>EKCert 유효성 검사 모드

인터넷에 연결 되어 있지 않은 조직에서 디바이스가 EKCert 유효성 검사 모드 최적화 됩니다. 장치 EKCert 유효성 검사 모드에서 실행 되는 DHA 서비스에 연결 하려면 **하지** 직접 인터넷에 액세스할 수 있는 합니다.

DHA EKCert 유효성 검사 모드로 실행 되 고 신뢰 가끔 (약: 5-10 배 연간)를 업데이트 해야 하는 관리 하는 엔터프라이즈 체인 의존 합니다. 

(사용 가능 해지면)으로 Microsoft 게시 신뢰할 수 있는 루트 및 중간 캐나다의 승인된 TPM 제조업체에 대해 집계 된 패키지.cab 보관에서 공개적으로 액세스할 수 있는 보관에서 합니다. 피드 다운로드의 무결성의 유효성을 검사 하 고, 장치 건강 증명을 실행 하는 서버에 설치 해야 합니다.

An example archive is [https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab).

#### <a name="aikcert-validation-mode"></a>AIKCert 유효성 검사 모드

인터넷에 액세스할 수 있는 작업 환경 AIKCert 유효성 검사 모드 최적화 됩니다. AIKCert 유효성 검사 모드에서 실행 되는 DHA 서비스에 연결 하는 디바이스 직접 인터넷에 액세스할 수 있어야 하며 AIK 인증서 Microsoft 로부터 받을 수 있습니다. 

## <a name="install-and-configure-the-dha-service-on-windows-server-2016"></a>설치 및 Windows Server 2016에 DHA 서비스 구성

다음 섹션을 사용 하 여 Windows Server 2016에 설치 및 구성 DHA 가져올 수 있습니다.

### <a name="prerequisites"></a>필수

설정 하 고 DHA 온-프레미스 서비스를 확인 하려면 다음을 수행 해야 합니다.

- Windows Server 2016을 실행 하는 서버 합니다.
- 하나 이상의 Windows 10 클라이언트 장치 (1.2 또는 2.0)에 있는 최신 Windows Insider 실행 지울/준비 상태로 tpm 빌드입니다.
- EKCert 또는 AIKCert 유효성 검사 모드로 실행 것인지 결정 합니다.
- 다음 인증서 다음과 같습니다.
  - **DHA SSL 인증서** x.509 SSL 인증서를 내보낼 수 있는 개인 키로 엔터프라이즈 신뢰할 수 있는 루트에 연결 합니다. 이 인증서 DHA 데이터 통신 교통 서버를 비롯 하 여의 (DHA 서비스 및 MDM 서버) 및 서버 (DHA 서비스 및 Windows 10 장치) 클라이언트 통신을 보호합니다.
  - **DHA 서명 인증서** x.509 인증서를 내보낼 수 있는 개인 키로 엔터프라이즈 신뢰할 수 있는 루트에 연결 합니다. DHA 서비스 디지털 서명이 인증서를 사용합니다. 
  - **DHA 암호화 인증서** x.509 인증서를 내보낼 수 있는 개인 키로 엔터프라이즈 신뢰할 수 있는 루트에 연결 합니다. 또한 DHA 서비스 암호화이 인증서를 사용합니다. 


### <a name="install-windows-server-2016"></a>Windows Server 2016 설치

Windows Server 2016에 기본 설정된 설치 방법 등 Windows 배포 서비스를 사용 하거나 설치 관리자 부팅 가능한 미디어, USB 드라이브 또는 시스템 로컬 파일에서 실행를 설치 합니다. Windows Server 2016를 사용 하 여 설치 해야 처음 DHA 온-프레미스 서비스를 구성 하는 경우는 **데스크톱 경험** 추가 옵션입니다.

### <a name="add-the-device-health-attestation-server-role"></a>Add the Device Health Attestation server role

장치 상태 증명 서버 역할을 종속성 서버 관리자를 사용 하 여 설치할 수 있습니다. 

Windows Server 2016을 설치한 후 디바이스 다시 시작 되 고 서버 관리자를 엽니다. 서버 관리자 자동으로 시작 되지 않으면 클릭 **시작**을 차례로 클릭 하 고 **서버 관리자**합니다.

1.  클릭 **역할 및 기능을 추가**합니다.
2.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.
3.  에 **설치 유형을 선택** 페이지, 클릭 **역할 또는 기능 기반 설치**을 차례로 클릭 하 고 **다음**합니다.
4.  에 **선택 대상 서버** 페이지, 클릭 **서버 풀에서 서버를 선택**서버를 선택한 다음 **다음**합니다.
5.  에 **서버 역할을 선택할** 페이지를 **장치 건강 증명** 확인란을 선택 합니다.
6.  클릭 **기능 추가** 역할 서비스 및 기능 필요한 다른 설치할 수 있습니다.
7.  클릭 **다음**합니다.
8.  에 **기능 선택** 페이지, 클릭 **다음**합니다.
9.  에 **웹 역할 IIS ()** 페이지, 클릭 **다음**합니다.
10. 에 **역할 서비스 선택** 페이지, 클릭 **다음**합니다.
11. 에 **장치 건강 증명 서비스** 페이지, 클릭 **다음**합니다.
12. 에 **설치 선택을 확인** 페이지, 클릭 **설치**합니다.
13. 설치가 완료 되 면 클릭 **닫기**합니다.

### <a name="install-the-signing-and-encryption-certificates"></a>서명 및 암호화 인증서를 설치

다음 Windows PowerShell 스크립트를 사용 하 여 서명 및 암호화 인증서를 설치 해야 합니다. 지문에 대 한 자세한 내용은 참조 [하는 방법: 인증서의 지문 검색](https://msdn.microsoft.com/library/ms734695.aspx)합니다.

```
$key = Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Thumbprint -like "<thumbprint>"}
$keyname = $key.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
$keypath = $env:ProgramData + "\Microsoft\Crypto\RSA\MachineKeys\" + $keyname
icacls $keypath /grant <username>`:R
  
#<thumbprint>: Certificate thumbprint for encryption certificate or signing certificate
#<username>: Username for web service app pool, by default IIS_IUSRS
```

### <a name="install-the-trusted-tpm-roots-certificate-package"></a>신뢰할 수 있는 TPM 루트 인증서 패키지가 설치

신뢰할 수 있는 TPM 루트 인증서 패키지를 설치 하려면 추출, 하지 조직에서 신뢰할 수 있는 모든 신뢰할 수 있는 체인 제거 하 고 실행 해야 setup.cmd 합니다.

#### <a name="download-the-trusted-tpm-roots-certificate-package"></a>신뢰할 수 있는 TPM 루트 인증서 패키지 다운로드

Before you install the certificate package, you can download the latest list of trusted TPM roots from [https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab).

> **중요:** 패키지를 설치 하기 전에 것 Microsoft에서 디지털 서명 되었는지 확인 합니다.

#### <a name="extract-the-trusted-certificate-package"></a>신뢰할 수 있는 인증 패키지 추출
다음 명령을 실행 하 여 신뢰할 수 있는 인증 패키지를 압축을 풉니다.
```
mkdir .\TrustedTpm
expand -F:* .\TrustedTpm.cab .\TrustedTpm
```

#### <a name="remove-the-trust-chains-for-tpm-vendors-that-are-not-trusted-by-your-organization-optional"></a>보안 체인 있는 TPM 공급 업체 제거 *하지* (선택 사항) 조직에서 신뢰할 수 있는

조직에서 하지 신뢰할 수 있는 TPM 공급 업체 신뢰 체인에 대 한 폴더를 삭제 합니다.

> **참고:** Microsoft 폴더 발급 된 인증서 AIK Microsoft의 유효성을 검사 하기 위해서입니다 AIK 인증서 모드를 사용 하는 경우입니다.

#### <a name="install-the-trusted-certificate-package"></a>신뢰할 수 있는 인증 패키지가 설치
신뢰할 수 있는 인증 패키지 설치 스크립트.cab 파일에서 실행 하 여 설치 합니다.

```
.\setup.cmd
```

### <a name="configure-the-device-health-attestation-service"></a>장치 상태 증명 서비스 구성

Windows PowerShell 구성 DHA 온-프레미스 서비스를 사용할 수 있습니다.

```
Install-DeviceHealthAttestation -EncryptionCertificateThumbprint <encryption> -SigningCertificateThumbprint <signing> -SslCertificateStoreName My -SslCertificateThumbprint <ssl> -SupportedAuthenticationSchema "<schema>"

#<encryption>: Thumbprint of the encryption certificate
#<signing>: Thumbprint of the signing certificate
#<ssl>: Thumbprint of the SSL certificate
#<schema>: Comma-delimited list of supported schemas including AikCertificate, EkCertificate, and AikPub
```

### <a name="configure-the-certificate-chain-policy"></a>구성 인증서 체인 정책

다음 Windows PowerShell 스크립트를 실행 하 여 인증서 체인 정책의 구성 합니다.

```
$policy = Get-DHASCertificateChainPolicy
$policy.RevocationMode = "NoCheck"
Set-DHASCertificateChainPolicy -CertificateChainPolicy $policy
```

## <a name="dha-management-commands"></a>DHA 관리 명령

다음은 DHA 서비스를 관리 하는 데 도움이 되는 몇 가지 Windows PowerShell 예입니다.

### <a name="configure-the-dha-service-for-the-first-time"></a>처음으로 DHA 서비스 구성

```
Install-DeviceHealthAttestation -SigningCertificateThumbprint "<HEX>" -EncryptionCertificateThumbprint "<HEX>" -SslCertificateThumbprint "<HEX>" -Force
```

### <a name="remove-the-dha-service-configuration"></a>DHA 서비스 구성 제거

```
Uninstall-DeviceHealthAttestation -RemoveSslBinding -Force
```
### <a name="get-the-active-signing-certificate"></a>활성 서명 인증서 받기

```
Get-DHASActiveSigningCertificate
```
### <a name="set-the-active-signing-certificate"></a>활성 서명 인증서를 설정 합니다.

```
Set-DHASActiveSigningCertificate -Thumbprint "<hex>" -Force
```

> **참고:** 이 인증서 DHA 서비스 실행 하는 서버에 배포 해야는 **LocalMachine\My** 인증서 저장소. 현재 서명 인증서를 설정 하는 경우 기존 활성 서명 인증서 비활성 서명 인증서 목록이으로 이동 됩니다.

### <a name="list-the-inactive-signing-certificates"></a>비활성 서명 인증서 목록
```
Get-DHASInactiveSigningCertificates
```

### <a name="remove-any-inactive-signing-certificates"></a>비활성 서명 인증서 모두 제거
```
Remove-DHASInactiveSigningCertificates -Force
Remove-DHASInactiveSigningCertificates  -Thumbprint "<hex>" -Force
```

> **참고:** 만 *한* (모든 종류) 비활성 인증서 언제 든 지 서비스에 있을 수 있습니다. 더 이상 필요 후 인증서 비활성 인증서 목록이에서 제거 해야 합니다.

### <a name="get-the-active-encryption-certificate"></a>현재 암호화 인증서 받기

```
Get-DHASActiveEncryptionCertificate
```

### <a name="set-the-active-encryption-certificate"></a>현재 암호화 인증서 설정

```
Set-DHASActiveEncryptionCertificate -Thumbprint "<hex>" -Force
```

인증서에 디바이스에 배포 해야는 **LocalMachine\My** 인증서 저장소. 

현재 암호화 인증서를 설정 하는 경우 기존 encryption 활성 인증서 비활성 암호화 인증서의 목록으로 이동 합니다.

### <a name="list-the-inactive-encryption-certificates"></a>비활성 암호화 인증서 목록

```
Get-DHASInactiveEncryptionCertificates
```
### <a name="remove-any-inactive-encryption-certificates"></a>비활성 암호화 인증서 모두 제거

```
Remove-DHASInactiveEncryptionCertificates -Force
Remove-DHASInactiveEncryptionCertificates -Thumbprint "<hex>" -Force 
```

### <a name="get-the-x509chainpolicy-configuration"></a>X509ChainPolicy 구성 받기 

```
Get-DHASCertificateChainPolicy
```
### <a name="change-the-x509chainpolicy-configuration"></a>X509ChainPolicy 구성을 변경합니다

```
$certificateChainPolicy = Get-DHASInactiveEncryptionCertificates
$certificateChainPolicy.RevocationFlag = <X509RevocationFlag>
$certificateChainPolicy.RevocationMode = <X509RevocationMode>
$certificateChainPolicy.VerificationFlags = <X509VerificationFlags>
$certificateChainPolicy.UrlRetrievalTimeout = <TimeSpan>
Set-DHASCertificateChainPolicy = $certificateChainPolicy
```

## <a name="dha-service-reporting"></a>DHA 서비스 보고

다음은 MDM 솔루션을 DHA 서비스에 의해 보고 되는 메시지의 목록입니다. 

- **200** HTTP 확인 합니다. 인증서 반환 됩니다.
- **400** 잘못 요청 합니다. 잘못 된 요청 형식, 잘못 된 상태 인증서 인증서 서명 되지 않는 일치, 잘못 된 상태 증명 물방울 또는 잘못 된 상태 상태 물방울 합니다. 응답 응답 스키마 오류 코드와 진단 사용할 수 있는 오류 메시지에 설명 된 대로 메시지도 포함 되어 있습니다.
- **500** 내부 서버 오류가 발생 합니다. 이 서비스 인증서 실행 되지 않도록 하는 문제가 있는 경우 발생할 수 있습니다.
- **503** 조절을 서버 채우지 방지 하기 위해 요청을 거부 합니다. 
