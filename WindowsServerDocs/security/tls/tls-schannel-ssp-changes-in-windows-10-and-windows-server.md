---
title: TLS (Schannel SSP)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 6e1a229bfc7063597f8994c71bbaec5637d084a4
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>Windows 10 및 Windows Server 2016에 변경 내용을 TLS (Schannel SSP)

>적용 대상: Windows Server 2016 및 Windows 10

## <a name="cipher-suite-changes"></a>암호화 제품군 변경

Windows 10 버전 1511이 릴리스, Windows Server 2016 구성 모바일 디바이스 관리 (MDM)를 사용 하 여 암호화 제품군 주문에 대 한 지원을 추가 합니다.

암호화 제품군 우선 순위 주문 변경 내용을 참조 [Schannel에서 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)합니다.

다음 암호 그룹에 대 한 지원이 추가 되었습니다.

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) Windows 10 버전 1507와 Windows Server 2016에
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) Windows 10 버전 1507와 Windows Server 2016에

DisabledByDefault 다음 암호 그룹에 대 한 변경 합니다.

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) Windows 10 버전 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) Windows 10 버전 1703
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) Windows 10 버전 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) Windows 10 버전 1703
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) Windows 10 버전 1703
- Windows 10 버전 1709 TLS_RSA_WITH_RC4_128_SHA
- Windows 10 버전 1709 TLS_RSA_WITH_RC4_128_MD5

Windows 10 버전 1507 및 Windows Server 2016 년 s h A 512 부터는 인증서 기본적으로 지원 됩니다.

### <a name="rsa-key-changes"></a>주요 변경 내용은 RSA

Windows 10 버전 1507 및 Windows Server 2016 클라이언트 RSA 주요 크기 레지스트리 구성 옵션을 추가합니다.

자세한 내용은 참조 [KeyExchangeAlgorithm-클라이언트 RSA 주요 크기](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes)합니다.

### <a name="diffie-hellman-key-changes"></a>주요 변경 내용은 등 세션

Windows 10 버전 1507 및 Windows Server 2016 레지스트리 키 크기 등 세션에 대 한 구성 옵션을 추가합니다.

자세한 내용은 참조 [KeyExchangeAlgorithm-등 세션 주요 크기](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes)합니다.

### <a name="schusestrongcrypto-option-changes"></a>SCH_USE_STRONG_CRYPTO 옵션 변경

Windows 10 버전 1507 Windows Server 2016 [SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx) 이제 비활성화 널 m d 5 DES, 옵션 및 암호화 내보내기 합니다.

## <a name="elliptical-curve-changes"></a>원형 곡선 변경

Windows 10 버전 1507 및 Windows Server 2016 추가 컴퓨터 구성 원형 곡선에 대 한 그룹 정책 구성을 > 관리 템플릿 > 네트워크 > SSL 구성 설정 합니다. ECC 곡선 순서 목록 원형 곡선 기본 되는 순서를 지정으로 활성화 되지 않는 지원 되는 곡선 수 있도록 합니다. 
 
다음 원형 곡선에 대 한 지원이 추가 되었습니다.

- BrainpoolP256r1 (RFC 7027) Windows 10 버전 1507와 Windows Server 2016에
- BrainpoolP384r1 (RFC 7027) Windows 10 버전 1507와 Windows Server 2016에 
- BrainpoolP512r1 (RFC 7027) Windows 10 버전 1507와 Windows Server 2016에
- Curve25519 (RFC 초안-ietf-tls-curve25519)에서 Windows 10 버전 1607 및 Windows Server 2016

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>발송 SealMessage 및 UnsealMessage 수준 지원

Windows 10 버전 1507 및 Windows Server 2016 발송 수준 SealMessage/UnsealMessage에 대 한 지원을 추가합니다.

## <a name="dtls-12"></a>DTLS 1.2

Windows 10 버전 1607 및 Windows Server 2016 DTLS 1.2 (RFC 6347)에 대 한 지원을 추가합니다.

## <a name="httpsys-thread-pool"></a>HTTP.SYS 스레드 풀 

Windows 10 버전 1607 및 Windows Server 2016 용 HTTP.SYS.

레지스트리 경로 다음과 같습니다. 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

CPU 핵심 별로 최대 스레드 풀 크기를 지정 하려면 작성 한 **MaxAsyncWorkerThreadsPerCpu** 항목 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 다음 원하는 크기 DWORD 값을 변경 합니다. 구성 되지 않은 경우 최대 CPU 핵심 당 2 스레드입니다.

## <a name="next-protocol-negotiation-npn-support"></a>다음 프로토콜 협상 (NPN) 지원

Windows 10 버전 1703 부터는 다음 프로토콜 협상 (NPN) 제거 되 고 더 이상 지원.

## <a name="pre-shared-key-psk"></a>미리 공유 키 (PSK)

Windows 10 버전 1607 및 Windows Server 2016 PSK 키 교환 알고리즘 (RFC 4279)에 대 한 지원을 추가합니다.

다음 PSK 암호 그룹에 대 한 지원이 추가 되었습니다.

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487)에서 Windows 10 버전 1607 및 Windows Server 2016
- Windows 10 버전 1607 및 Windows Server 2016에 TLS_PSK_WITH_AES_256_CBC_SHA384(RFC 5487)
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487)에서 Windows 10 버전 1607 및 Windows Server 2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487)에서 Windows 10 버전 1607 및 Windows Server 2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487)에서 Windows 10 버전 1607 및 Windows Server 2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487)에서 Windows 10 버전 1607 및 Windows Server 2016

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>세션 다시 시작 하지 않고 서버 쪽 상태 서버 쪽 성능 향상

Windows 10 버전 1507 및 Windows Server 2016 Windows Server 2012에 비해 많음 세션 티켓 30% 더 세션 resumptions 초당 제공 합니다.

## <a name="session-hash-and-extended-master-secret-extension"></a>세션 해시 및 확장된 마스터 시크릿 확장

Windows 10 버전 1507 및 Windows Server 2016 RFC 7627에 대 한 지원을 추가: Transport Layer Security TLS () 세션 해시 및 마스터 시크릿 확장 확장 합니다.

Windows 10 및 Windows Server 2016 필요 타사가이 변경으로 인해 [CNG SSL 공급자](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) 업데이트 NCRYPT_SSL_INTERFACE_VERSION_3를 지원 하 고 새 인터페이스가에 대해 설명 합니다.


## <a name="ssl-support"></a>SSL 지원

Windows 10 버전 1607 및 Windows Server 2016 부터는 TLS 클라이언트 및 서버 SSL 3.0 기본적으로 비활성화 되어 있습니다. 즉, 응용 프로그램 또는 서비스를 통해 SSPI SSL 3.0 요청 특히, 하지 않으면 클라이언트는 제공 하거나 SSL 3.0 동의 하지 고 서버 SSL 3.0 선택 하지 것입니다.

Windows 10 버전 1607 및 Windows Server 2016부터, SSL 2.0 제거 되 고 더 이상 지원.

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>Windows TLS을 준수 하는 호환 되지 않는 TLS 클라이언트와 연결에 대 한 TLS 1.2 요구 사항에 대 한 변경

TLS 1.2 클라이언트 사용 하는 ["signature_algorithms" 확장](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1) 나타내는 서버에 서명/hash algorithm 쌍은 디지털 서명이 (즉, 서버 인증서 및 서버 키 교환)에 사용할 수 있습니다. 또한 TLS 1.2 RFC 서버 인증서 메시지 적용 "signature_algorithms" 확장을 위한 필요 합니다.

"클라이언트"signature_algorithms"확장을 제공한 경우 다음 모든 인증서 서버에서 제공 해야가 서명 확장명을 표시 하는 콘텐츠의 해시/서명 알고리즘 쌍."

실제로, 일부 제 3 자 TLS 클라이언트 하거나 하지 않는 모든 서명이 포함 하 여 "signature_algorithms" 확장에 동의 하 게 알고리즘 쌍 해시 TLS 1.2 RFC 및 실패 준수 완전히 확장 생략 (후자의 서버에 알립니다 클라이언트 RSA, DSA 또는 ECDSA SHA1 지원).

만 종종 TLS 서버에 endpoint 의미 서버 클라이언트의 요구 사항을 충족 하는 인증서를 항상 제공 수 없는 별 구성 한 인증서 합니다.

Windows 10 및 Windows Server 2016 년 Windows TLS 스택 하기 전에 엄격히 정책을 준수 TLS 1.2 RFC 요구 사항, 연결 실패 RFC 호환 되지 않는 TLS 클라이언트 및 상호 운용성 문제 발생 합니다. Windows 10 및 Windows Server 2016에서 제한 된 편안히 하 고 서버 서버의 옵션만 TLS 1.2 RFC에 부합 하지 않는 인증서를 보낼 수 있습니다. 다음 클라이언트 계속 하거나 핸드셰이크 종료할 수 있습니다.

서버와 클라이언트 인증서를 확인할 때 Windows TLS 스택 엄격히 TLS 1.2 RFC 준수 및 클라이언트 및 서버 인증서에 하기로 서명 및 hash 알고리즘을 통해만 합니다.


