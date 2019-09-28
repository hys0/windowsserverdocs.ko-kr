---
title: TLS (Schannel SSP)
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 05/16/2018
ms.openlocfilehash: e103e985592e6aed150ccd3e1a87e56f19621dbe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403382"
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>Windows 10 및 Windows Server 2016의 TLS (Schannel SSP) 변경 내용

>적용 대상: Windows Server (반기 채널), Windows Server 2016 및 Windows 10

## <a name="cipher-suite-changes"></a>암호 그룹 변경 내용

Windows 10, 버전 1511 및 Windows Server 2016에서는 MDM (모바일 장치 관리)을 사용 하 여 암호 그룹 순서를 구성 하는 지원을 추가 합니다.

암호 그룹 우선 순위 변경의 경우 [Schannel의 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)을 참조 하세요.

다음 암호 그룹에 대 한 지원이 추가 되었습니다.

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) (Windows 10, 버전 1507 및 Windows Server 2016)
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) (Windows 10, 버전 1507 및 Windows Server 2016)

다음 암호 그룹에 대해 DisabledByDefault를 변경 합니다.

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) (Windows 10 버전 1703)
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) (Windows 10 버전 1703)
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) (Windows 10 버전 1703)
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) (Windows 10 버전 1703)
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) (Windows 10 버전 1703)
- Windows 10의 TLS_RSA_WITH_RC4_128_SHA 버전 1709
- Windows 10의 TLS_RSA_WITH_RC4_128_MD5 버전 1709

Windows 10, 버전 1507 및 Windows Server 2016부터 SHA 512 인증서는 기본적으로 지원 됩니다.

### <a name="rsa-key-changes"></a>RSA 키 변경

Windows 10, 버전 1507 및 Windows Server 2016 클라이언트 RSA 키 크기에 대 한 레지스트리 구성 옵션을 추가 합니다.

자세한 내용은 [KeyExchangeAlgorithm-CLIENT RSA key 크기](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes)를 참조 하세요.

### <a name="diffie-hellman-key-changes"></a>Diffie-hellman 키 변경

Windows 10, 버전 1507 및 Windows Server 2016에서는 Diffie-hellman 키 크기에 대 한 레지스트리 구성 옵션을 추가 합니다.

자세한 내용은 [KeyExchangeAlgorithm 키 크기](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes)를 참조 하세요.

### <a name="sch_use_strong_crypto-option-changes"></a>SCH_USE_STRONG_CRYPTO 옵션 변경 내용

Windows 10, 버전 1507 및 Windows Server 2016에서 [SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx) 옵션은 이제 NULL, MD5, DES 및 내보내기 암호화를 사용 하지 않도록 설정 합니다.

## <a name="elliptical-curve-changes"></a>타원형 곡선 변경

Windows 10, 버전 1507 및 Windows Server 2016에서는 컴퓨터 구성 > 관리 템플릿 > 네트워크 > SSL 구성 설정에서 타원형 곡선에 대 한 그룹 정책 구성을 추가 합니다. ECC 곡선 순서 목록에는 사용할 수 없는 지원 되는 곡선이 사용 되는 것 뿐만 아니라 타원형 곡선이 선호 되는 순서를 지정 합니다. 
 
다음 타원형 곡선에 대 한 지원이 추가 되었습니다.

- BrainpoolP256r1 (RFC 7027) (Windows 10, 버전 1507 및 Windows Server 2016)
- BrainpoolP384r1 (RFC 7027) (Windows 10, 버전 1507 및 Windows Server 2016) 
- BrainpoolP512r1 (RFC 7027) (Windows 10, 버전 1507 및 Windows Server 2016)
- Curve25519 (RFC draft-Curve25519) (Windows 10, 버전 1607 및 Windows Server 2016)

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>SealMessage & UnsealMessage의 디스패치 수준 지원

Windows 10, 버전 1507 및 Windows Server 2016 디스패치 수준에서 SealMessage/UnsealMessage에 대 한 지원을 추가 합니다.

## <a name="dtls-12"></a>DTLS 1.2

Windows 10, 버전 1607 및 Windows Server 2016 DTLS 1.2 (RFC 6347)에 대 한 지원을 추가 합니다.

## <a name="httpsys-thread-pool"></a>HTTP. SYS 스레드 풀 

Windows 10, 버전 1607 및 Windows Server 2016은 HTTP에 대 한 TLS 핸드셰이크를 처리 하는 데 사용 되는 스레드 풀의 크기에 대 한 레지스트리 구성을 추가 합니다. 시스템.

레지스트리 경로: 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

CPU 코어 당 최대 스레드 풀 크기를 지정 하려면 **MaxAsyncWorkerThreadsPerCpu** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 원하는 크기로 변경 합니다. 구성 되지 않은 경우 최대값은 CPU 코어 당 2 개의 스레드입니다.

## <a name="next-protocol-negotiation-npn-support"></a>다음 프로토콜 협상 (NPN) 지원

Windows 10 버전 1703부터 다음 프로토콜 협상 (NPN)이 제거 되었으며 더 이상 지원 되지 않습니다.

## <a name="pre-shared-key-psk"></a>미리 공유한 키 (PSK)

Windows 10, 버전 1607 및 Windows Server 2016에서는 PSK 키 교환 알고리즘 (RFC 4279)에 대 한 지원을 추가 합니다.

다음 PSK 암호 그룹에 대 한 지원이 추가 되었습니다.

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) (Windows 10, 버전 1607 및 Windows Server 2016)
- TLS_PSK_WITH_AES_256_CBC_SHA384 (RFC 5487) (Windows 10, 버전 1607 및 Windows Server 2016)
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) (Windows 10, 버전 1607 및 Windows Server 2016)
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) (Windows 10, 버전 1607 및 Windows Server 2016)
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) (Windows 10, 버전 1607 및 Windows Server 2016)
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) (Windows 10, 버전 1607 및 Windows Server 2016)

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>서버 쪽 상태 서버 쪽 성능 향상 없이 세션 다시 시작

Windows 10, 버전 1507 및 Windows Server 2016은 Windows Server 2012와 비교 하 여 세션 티켓을 사용 하는 초당 30% 더 많은 세션 재개 제공 합니다.

## <a name="session-hash-and-extended-master-secret-extension"></a>세션 해시 및 확장 된 마스터 보안 확장

Windows 10, 버전 1507 및 Windows Server 2016 RFC 7627에 대 한 지원을 추가 합니다. TLS (전송 계층 보안) 세션 해시 및 확장 된 마스터 보안 확장 프로그램입니다.

이러한 변경으로 인해 Windows 10 및 Windows Server 2016에는 NCRYPT_SSL_INTERFACE_VERSION_3을 지원 하 고이 새 인터페이스를 설명 하는 타사 [CNG SSL 공급자](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) 업데이트가 필요 합니다.


## <a name="ssl-support"></a>SSL 지원

Windows 10, 버전 1607 및 Windows Server 2016부터 TLS 클라이언트 및 서버 SSL 3.0은 기본적으로 사용 하지 않도록 설정 되어 있습니다. 즉, 응용 프로그램 또는 서비스에서 SSPI를 통해 특별히 SSL 3.0을 요청 하지 않는 한, 클라이언트는 SSL 3.0를 제공 하거나 수락 하지 않으며 서버는 SSL 3.0를 선택 하지 않습니다.

Windows 10 버전 1607 및 Windows Server 2016부터 SSL 2.0은 제거 되었으며 더 이상 지원 되지 않습니다.

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>비규격 TLS 클라이언트와의 연결에 대 한 TLS 1.2 요구 사항을 준수 하는 Windows TLS의 변경 내용

TLS 1.2에서 클라이언트는 ["signature_algorithms" 확장](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1) 을 사용 하 여 디지털 서명 (예: 서버 인증서 및 서버 키 교환)에서 사용할 수 있는 서명/해시 알고리즘 쌍을 서버에 표시 합니다. TLS 1.2 RFC는 또한 서버 인증서 메시지에 "signature_algorithms" 확장을 적용 해야 합니다.

"클라이언트에서" signature_algorithms "확장을 제공한 경우 서버에서 제공 하는 모든 인증서가 해당 확장에 표시 되는 해시/서명 알고리즘 쌍으로 서명 되어야 합니다."

실제로 일부 타사 TLS 클라이언트는 TLS 1.2 RFC를 준수 하지 않고 "signature_algorithms" 확장에서 허용 하려는 모든 서명 및 해시 알고리즘 쌍을 포함 하는 데 실패 하거나 확장을 완전히 생략 합니다 (후자는를 나타냅니다. 클라이언트가 RSA, DSA 또는 ECDSA를 사용 하는 SHA1만 지 원하는 서버입니다.

TLS 서버에는 일반적으로 끝점 당 하나의 인증서만 구성 되어 있으므로 서버에서 항상 클라이언트의 요구 사항을 충족 하는 인증서를 제공할 수는 없습니다.

Windows 10 및 Windows Server 2016 이전 버전에서는 Windows TLS 스택이 TLS 1.2 RFC 요구 사항을 엄격히 준수 하 여 RFC 비규격 TLS 클라이언트 및 상호 운용성 문제에 대 한 연결에 오류가 발생 했습니다. Windows 10 및 Windows Server 2016에서 제약 조건은 완화 되며 서버에서 TLS 1.2 RFC를 준수 하지 않는 인증서 (서버의 유일한 옵션)를 보낼 수 있습니다. 그러면 클라이언트가 핸드셰이크를 계속 하거나 종료할 수 있습니다.

서버 및 클라이언트 인증서의 유효성을 검사할 때 Windows TLS 스택은 TLS 1.2 RFC를 엄격 하 게 준수 하 고 서버 및 클라이언트 인증서에서 협상 된 시그니처와 해시 알고리즘만 허용 합니다.


