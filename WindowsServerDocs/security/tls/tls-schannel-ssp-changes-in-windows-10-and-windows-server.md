---
title: TLS (Schannel SSP)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 05/16/2018
ms.openlocfilehash: 030fd81e0c6ba0423f1fa73e680006766cf2b180
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890774"
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>Windows 10 및 Windows Server 2016의 TLS (Schannel SSP) 변경

>적용 대상: Windows Server (반기 채널), Windows Server 2016 및 Windows 10

## <a name="cipher-suite-changes"></a>암호화 Suite 변경 내용

Windows 10, 버전 1511 및 Windows Server 2016에는 모바일 장치 관리 (MDM)를 사용 하 여 암호화 제품군 순서의 구성에 대 한 지원을 추가 합니다.

암호화 suite 우선 순위 순서 변경 내용을 참조 하세요 [Schannel의 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)합니다.

다음 암호 그룹에 대 한 지원이 추가 되었습니다.

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) Windows 10 버전 1507 및 Windows Server 2016
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) Windows 10 버전 1507 및 Windows Server 2016

DisabledByDefault 다음 암호 그룹에 대 한 변경:

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) in Windows 10, version 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) in Windows 10, version 1703
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246)에서 Windows 10 버전 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246)에서 Windows 10 버전 1703
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246)에서 Windows 10 버전 1703
- Windows 10 버전 1709에서 TLS_RSA_WITH_RC4_128_SHA
- TLS_RSA_WITH_RC4_128_MD5 in Windows 10, version 1709

Windows 10, 버전 1507 및 Windows Server 2016 부터는 SHA 512 인증서는 기본적으로 지원 됩니다.

### <a name="rsa-key-changes"></a>RSA 키 변경

Windows 10, 버전 1507 및 Windows Server 2016 클라이언트 RSA 키 크기에 대 한 레지스트리 구성 옵션을 추가 합니다.

자세한 내용은 [KeyExchangeAlgorithm-클라이언트 RSA 키 크기](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes)합니다.

### <a name="diffie-hellman-key-changes"></a>Diffie-hellman 키 변경

Windows 10, 버전 1507 및 Windows Server 2016 Diffie-hellman 키 크기에 대 한 레지스트리 구성 옵션을 추가 합니다.

자세한 내용은 [KeyExchangeAlgorithm-Diffie-hellman 키 크기](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes)합니다.

### <a name="schusestrongcrypto-option-changes"></a>SCH_USE_STRONG_CRYPTO 옵션 변경

Windows 10, 버전 1507 및 Windows Server 2016 [SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx) 이제 사용 하지 않도록 설정 NULL, MD5, DES, 옵션 및 암호화를 내보냅니다.

## <a name="elliptical-curve-changes"></a>타원형 곡선 변경

Windows 10, 버전 1507 및 Windows Server 2016 추가 컴퓨터 구성에서 타원형 곡선에 대 한 그룹 정책 구성 > 관리 템플릿 > 네트워크 > SSL 구성을 설정 합니다. ECC 곡선이 순서 목록 타원형 곡선에 기본 설정 순서를 지정 뿐만 아니라 사용 되지 않는 지원 되는 곡선을 사용 하도록 설정 합니다. 
 
타원형 곡선에 대 한 지원이 추가 되었습니다.

- BrainpoolP256r1 (RFC 7027) Windows 10 버전 1507 및 Windows Server 2016
- BrainpoolP384r1 (RFC 7027) Windows 10 버전 1507 및 Windows Server 2016 
- BrainpoolP512r1 (RFC 7027) Windows 10 버전 1507 및 Windows Server 2016
- Curve25519 (RFC 초안-ietf-tls-curve25519) Windows 10 버전 1607 및 Windows Server 2016

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>SealMessage UnsealMessage에 대 한 디스패치 수준 지원

Windows 10, 버전 1507 및 Windows Server 2016 디스패치 수준 SealMessage/UnsealMessage에 대 한 지원을 추가합니다.

## <a name="dtls-12"></a>DTLS 1.2

Windows 10, 버전 1607 및 Windows Server 2016 DTLS 1.2 (RFC 6347) 지원을 추가합니다.

## <a name="httpsys-thread-pool"></a>HTTP입니다. SYS 스레드 풀 

Windows 10, 버전 1607 및 Windows Server 2016에는 HTTP에 대 한 TLS 핸드셰이크를 처리 하는 데 사용 되는 스레드 풀 크기의 레지스트리 구성을 추가 합니다. SYS입니다.

레지스트리 경로: 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

CPU 코어 당 최대 스레드 풀 크기를 지정 하려면 만듭니다는 **MaxAsyncWorkerThreadsPerCpu** 항목입니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 원하는 크기로 변경 합니다. 구성 되지 않은 경우 최대값은 CPU 코어당 2 스레드입니다.

## <a name="next-protocol-negotiation-npn-support"></a>다음 프로토콜 협상 (NPN) 지원

Windows 10 버전 1703부터 다음 프로토콜 협상 (NPN) 제거 되 고는 지원 되지 않습니다.

## <a name="pre-shared-key-psk"></a>미리 공유한 키 (PSK)

Windows 10, 버전 1607 및 Windows Server 2016에는 PSK 키 교환 알고리즘 (RFC 4279) 지원을 추가합니다.

다음 PSK 암호 그룹에 대 한 지원이 추가 되었습니다.

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) Windows 10 버전 1607 및 Windows Server 2016
- Windows 10 버전 1607 및 Windows Server 2016 TLS_PSK_WITH_AES_256_CBC_SHA384(RFC 5487)
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) Windows 10 버전 1607 및 Windows Server 2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) Windows 10 버전 1607 및 Windows Server 2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) Windows 10 버전 1607 및 Windows Server 2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) Windows 10 버전 1607 및 Windows Server 2016

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>서버 쪽 성능 향상 된 서버 쪽 상태 없이 세션 다시 시작

Windows 10, 버전 1507 및 Windows Server 2016 Windows Server 2012에 비해 세션 티켓을 사용 하 여 초당 30% 더 많은 세션 다시 시작을 제공 합니다.

## <a name="session-hash-and-extended-master-secret-extension"></a>세션 해시 및 확장 된 마스터 보안 확장

Windows 10, 버전 1507 및 Windows Server 2016에는 RFC 7627에 대 한 지원을 추가합니다. 전송 계층 보안 (TLS) 세션 해시 하 고 마스터 보안 확장 프로그램을 확장 합니다.

Windows 10 및 Windows Server 2016 필요한 타사가이 변경으로 인해 [CNG SSL 공급자](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) 업데이트 NCRYPT_SSL_INTERFACE_VERSION_3를 지원 하 고이 새 인터페이스에 설명 합니다.


## <a name="ssl-support"></a>SSL 지원

Windows 10, 버전 1607 및 Windows Server 2016 부터는 TLS 클라이언트와 서버 SSL 3.0 기본적으로 비활성화 됩니다. 즉, 응용 프로그램 또는 서비스 특히 SSPI 통해 SSL 3.0을 요청 하지 않는 한 클라이언트는 제공 하거나 SSL 3.0을 허용 하지 않습니다 서버는 SSL 3.0을 선택 하지 않습니다.

Windows 10 버전 1607 및 Windows Server 2016 부터는 SSL 2.0 제거 되 고는 지원 되지 않습니다.

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>Windows TLS을 준수 하는 호환 되지 않는 TLS 클라이언트와의 연결에 대 한 TLS 1.2 요구 사항 변경 내용

클라이언트에서 TLS 1.2를 사용 합니다 ["signature_algorithms" 확장](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1) 에 알리기 위해 서버는 서명/해시 알고리즘 쌍 (예: 서버 인증서 및 서버 키 교환을) 디지털 서명에서 사용할 수 있습니다. TLS 1.2 RFC에도 서버 인증서 메시지가 인식 "signature_algorithms" 확장은 필요 합니다.

"클라이언트"signature_algorithms"확장을 제공 하는 경우 다음 서버에서 제공 하는 모든 인증서 서명 되어야 합니다는 확장에 표시 되는 해시/서명을 알고리즘 쌍으로."

실제로 일부 타사 TLS 클라이언트 하거나 하지 않는 모든 서명을 포함 하는 "signature_algorithms" 확장에 적용할 알고리즘 쌍 해시 TLS 1.2 RFC 및 실패 준수 확장을 완전히 생략 (후자 나타냅니다 서버는 클라이언트 지원 SHA1 RSA, DSA 또는 ECDSA를 사용 하 여).

TLS 서버 종종에 하나의 인증서가 서버 클라이언트의 요구를 충족 하는 인증서를 항상 제공할 수 없습니다 것을 의미 하는 끝점 별로 구성 합니다.

Windows 10 및 Windows Server 2016, Windows TLS 스택 전에 엄격 하 게 준수 TLS 1.2 RFC 요구 사항을 RFC 호환 되지 않는 TLS 클라이언트와의 상호 운용성 문제를 사용 하 여 연결 실패의 결과입니다. Windows 10 및 Windows Server 2016에서 제약 조건을 완화 하 고 서버의 유일한 옵션인 경우 서버에서 TLS 1.2 rfc를 준수 하지 않는 인증서를 보낼 수 있습니다. 그런 다음 클라이언트 계속 하거나 핸드셰이크를 종료 될 수 있습니다.

서버 및 클라이언트 인증서 유효성 검사, Windows TLS 스택을 TLS 1.2 RFC 엄격 하 게 준수 하 고 협상 된 서명 및 해시 알고리즘을 서버 및 클라이언트 인증서에만 허용 합니다.


