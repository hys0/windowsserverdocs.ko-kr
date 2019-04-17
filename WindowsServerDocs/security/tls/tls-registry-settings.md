---
title: "전송 TLS (Layer Security) 레지스트리 설정"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 08/07/2017
ms.openlocfilehash: 8ccfacc367a5d32438bebf22798479a07f6cbdfc
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="transport-layer-security-tls-registry-settings"></a>전송 TLS (Layer Security) 레지스트리 설정

>적용 대상: (세미콜론 연간 채널) Windows Server, Windows Server 2016, Windows Server 2008 R2, Windows Server 2008, Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista

IT 전문가 위한이 참조 항목 Transport Layer Security TLS () 프로토콜을 통해는 Schannel 보안 지원 SSP 소켓 SSL (Secure Layer) 프로토콜 Windows 구현에 대 한 지원 되는 레지스트리 설정이 정보가 포함 됩니다. 레지스트리 하위 및 관리 하 고 Schannel SSP 문제 해결이 항목 도움말 적용 항목 TLS 및 SSL 프로토콜 특히 합니다. 

>[!Caution]
>이 정보는 문제를 해결 하거나 해야 설정이 적용 됩니다 확인 하는 경우 사용에 대 한 참조도 제공 됩니다. 편집 하지 않으면 직접 레지스트리 다른 대안이 않는 것이 좋습니다.
>레지스트리에 대 한 수정은 레지스트리 편집기에 또는 Windows 운영 체제에서 확인 되지 않았습니다 적용 되기 전에. 결과적으로, 잘못 된 값을 저장할 수를 및 시스템에서 복구할 수 없는 오류가 발생할 수 있습니다. 가능 하면 레지스트리를 직접 편집 하는 대신 사용 하 여 그룹 정책 또는 Microsoft Management Console (MMC) 등 기타 Windows 도구 작업을 수행 합니다. 레지스트리를 편집 해야 하는 경우 주의 합니다. 

## <a name="certificatemappingmethods"></a>CertificateMappingMethods 

기본적으로이 항목의에서 존재 하지 않습니다. 기본값은 아래에 나열 된 모든 네 인증서 매핑 방법을 지원 됩니다.

서버 응용 프로그램 필요 클라이언트 인증, Schannel 자동으로 사용자 계정에 클라이언트 컴퓨터에서 제공 되는 인증서 지도 하려고 합니다. 사용자에 게 만들어 매핑 인증서 정보 Windows 사용자 계정에 연결 하는 클라이언트 인증서를 사용 하 여 로그인 인증할 수 있습니다. 만들고 인증서 매핑 후 클라이언트가 클라이언트 인증서 제공 될 때마다 서버 응용 프로그램이 자동으로 연결 해당 사용자 적절 한 Windows 사용자 계정 합니다.

대부분의 경우에는 인증서는 두 가지 방법 중 하나에서 사용자 계정에 매핑됩니다. 

- 단일 인증서 (일대일) 단일 사용자 계정에 매핑됩니다.
- 여러 인증서 한 사용자 계정 (매핑 다 일)에 매핑됩니다.

기본적으로 Schannel 공급자가 우선 순위에 나열 된 다음 네 가지 인증서 매핑 방법 사용.

1. Kerberos 사용자에 대 한 서비스 (S4U) 인증서 매핑
2. 사용자 계정 이름 매핑
3. 일대일 (라고도 주제/발행인이 매핑)
4. 다 일 매핑

해당 되는 버전:에 지정 된 대로 **에 적용 됩니다.** 이 항목의 시작 부분에 있는 목록입니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="ciphers"></a>암호

TLS/SSL 암호가 암호화 제품군 순서를 구성 하 여 제어 해야 합니다. 자세한 내용은 참조 [TLS 암호 그룹 순서를 구성](manage-tls.md#configuring-tls-cipher-suite-order)합니다.

Schannel SSP에서 사용 되는 기본 암호화 제품군 주문에 대 한 내용은 [TLS/SSL (Schannel SSP)에서 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)합니다. 

##<a name="ciphersuites"></a>암호가

구성 SSL TLS/암호 그룹 완료 그룹 정책, PowerShell, 또는 MDM를 사용 하 여 [TLS 암호 그룹 순서를 구성](manage-tls.md#configuring-tls-cipher-suite-order) 대 한 자세한 내용은 합니다.

Schannel SSP에서 사용 되는 기본 암호화 제품군 주문에 대 한 내용은 [TLS/SSL (Schannel SSP)에서 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)합니다. 


## <a name="clientcachetime"></a>ClientCacheTime

이 항목 운영 체제 밀리초에서 클라이언트 측 캐시 항목 만료 되는 시간을 제어할 수 있습니다. 0 캐싱 보안 연결을 해제합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 

처음으로 전체 Schannel SSP 통해 서버에 연결 하는 클라이언트 TLS/SSL 핸드셰이크 수행 됩니다. 완료 되 면 마스터 암호, 암호 그룹이 및 인증서 세션 캐시 해당 클라이언트 및 서버에 저장 됩니다.

Windows Server 2008 및 Windows Vista 부터는 기본 클라이언트 캐시 시간에 10 시간입니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

기본 클라이언트 캐시 시간

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

이 항목 제어 연방 정보를 처리 (FIPS)를 준수 합니다. 기본값은 0 합니다.

해당 되는 버전:에 지정 된 대로 **에 적용 됩니다.** 이 항목의 시작 부분에 있는 목록입니다. 

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\LSA

Windows Server FIPS 제품군 암호화 된: 표시 [암호 그룹 지원 및 Schannel SSP에서 프로토콜](https://technet.microsoft.com/library/dn786419.aspx)합니다.

## <a name="hashes"></a>해시

TLS/SSL 해시 알고리즘 암호 그룹 순서를 구성 하 여 제어 해야 합니다. 참조 [TLS 암호 그룹 순서를 구성](manage-tls.md#configuring-tls-cipher-suite-order) 대 한 자세한 내용은 합니다.

## <a name="issuercachesize"></a>IssuerCacheSize

이 항목 발행인이 캐시의 크기를 제어 하 고 매핑 발행인이 함께 사용 됩니다. 클라이언트의 인증서 체인의 발급자 모든 연결 하려고 시도 Schannel SSP-클라이언트 인증서의 직접 발행인이 뿐만 아니라 합니다. 서버 동일한 지도를 시작할 수 발급자 일반적인 경우 계정에 매핑됩니다 하지 않는 경우 발행인이 수백 초당 번 반복 해 서 이름을 지정 합니다. 

이 방지 하려면 서버에 캐시 항목 발행인이 이름 계정을에 매핑됩니다 하지 않는, 캐시에 추가 되 고 Schannel SSP 발행인이 이름을 해야만 다시 매핑할 시도 하지는 경우 만료 되므로 부정 캐시 합니다. 이 레지스트리 항목이 캐시 크기를 지정합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 기본값은 100 합니다. 

해당 되는 버전:에 지정 된 대로 **에 적용 됩니다.** 이 항목의 시작 부분에 있는 목록입니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="issuercachetime"></a>IssuerCacheTime

이 항목 밀리초에서 캐시 시간 제한 기간의 길이 제어 합니다. 클라이언트의 인증서 체인의 발급자 모든 연결 하려고 시도 Schannel SSP-클라이언트 인증서의 직접 발행인이 뿐만 아니라 합니다. 서버 동일한 지도를 시작할 수 없는 발급자 일반적인 경우 계정 지도 하지 않는 경우 발행인이 수백 초당 번 반복 해 서 이름을 지정 합니다.

이 방지 하려면 서버에 캐시 항목 발행인이 이름 계정을에 매핑됩니다 하지 않는, 캐시에 추가 되 고 Schannel SSP 발행인이 이름을 해야만 다시 매핑할 시도 하지는 경우 만료 되므로 부정 캐시 합니다. 시스템 동일한 발급자 지도 하려고 계속 하지 않도록 성능 이유로이 캐시 유지 됩니다. 기본적으로이 항목의에서 존재 하지 않습니다. 기본값 10 분입니다.

해당 되는 버전:에 지정 된 대로 **에 적용 됩니다.** 이 항목의 시작 부분에 있는 목록입니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>KeyExchangeAlgorithm-클라이언트 RSA 크기 키

이 항목 클라이언트 RSA 주요 크기를 제어 합니다. 

사용 하 여 주요 교환 알고리즘 암호 그룹 순서를 구성 하 여 제어 해야 합니다.

Windows 10 버전 1507와 Windows Server 2016에 추가 합니다.

레지스트리 경로: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS

최소 지원 되는 범위의 RSA 주요 비트 길이 TLS 클라이언트를 지정 하려면 작성 한 **ClientMinKeyBitLength** 항목 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 DWORD 값 원하는 비트 길이를 변경 합니다. 구성 되지 않은 경우 최소 1024 비트 됩니다. 

최대 지원 되는 범위의 RSA 주요 비트 길이 TLS 클라이언트를 지정 하려면 작성 한 **ClientMaxKeyBitLength** 항목 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 DWORD 값 원하는 비트 길이를 변경 합니다. 구성 되지 않은 경우에 최대 적용 되지 않습니다.

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>KeyExchangeAlgorithm-등 세션 주요 크기

이 항목 등 세션 주요 크기를 제어 합니다. 

사용 하 여 주요 교환 알고리즘 암호 그룹 순서를 구성 하 여 제어 해야 합니다.

Windows 10 버전 1507와 Windows Server 2016에 추가 합니다.

레지스트리 경로: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie 세션

최소 지원 되는 범위의 많은-Helman 주요 비트 길이 TLS 클라이언트를 지정 하려면 작성 한 **ClientMinKeyBitLength** 항목 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 DWORD 값 원하는 비트 길이를 변경 합니다. 구성 되지 않은 경우 최소 1024 비트 됩니다. 
 
최대 지원 되는 범위의 많은-Helman 주요 비트 길이 TLS 클라이언트를 지정 하려면 작성 한 **ClientMaxKeyBitLength** 항목 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 DWORD 값 원하는 비트 길이를 변경 합니다. 구성 되지 않은 경우에 최대 적용 되지 않습니다. 
 
TLS 서버 기본 설정에 대 한 많은 Helman 키 비트 길이 지정 하려면 작성 한 **ServerMinKeyBitLength** 항목 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 DWORD 값 원하는 비트 길이를 변경 합니다. 구성 되지 않은 경우 기본 2048 비트 됩니다. 

## <a name="maximumcachesize"></a>MaximumCacheSize

이 항목의 캐시 요소 최대 수를 제어합니다. 0 MaximumCacheSize 설정 서버 쪽 세션 캐시를 사용할 수 없게 되 고 다시 연결 하면 됩니다. 기본값 위의 MaximumCacheSize 증가 Lsass.exe 추가 메모리 사용 하면 됩니다. 일반적으로 각 세션 캐시 요소 2-4 KB 메모리 필요합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 기본값은 20, 000 요소입니다. 

해당 되는 버전:에 지정 된 대로 **에 적용 됩니다.** 이 항목의 시작 부분에 있는 목록입니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="messaging--fragment-parsing"></a>어디서 나 메시지 – 구문 분석 함으로써 조각

________________________________________
이 항목 제어 최대 수락 조각화 된 TLS 핸드셰이크 메시지의 크기를 허용 합니다. 허용 되는 크기 보다 크게 메시지를 허용 하지 않습니다 고 TLS 핸드셰이크 실패 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 

값 0x0 설정 하면 조각화 된 메시지 하지 처리 되 고 TLS 핸드셰이크 실패 하 게 됩니다. 따라서 TLS 클라이언트 또는 서버 현재 컴퓨터에 TLS Rfc와 호환 됩니다. 

허용 되는 최대 최대 2 크기를 늘렸습니다 수 ^24 1 바이트 합니다. 클라이언트 또는 서버를 읽고 많은 양의 네트워크에서 확인 되지 않은 데이터를 저장할 수 있도록 좋은 방법이 아닙니다 하 고 각 보안 컨텍스트를 추가 메모리를 사용 합니다. 

Windows에서 7 및 Windows Server 2008 R2 추가 합니다.
Internet Explorer Windows XP, Windows Vista 또는 Windows Server 2008 조각화 된 TLS/SSL 핸드셰이크 메시지 분석을 사용 하는 업데이트를 사용할 수 있습니다.

레지스트리 경로: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Messaging

허용 크기 TLS 클라이언트 수락할 조각화 된 TLS 핸드셰이크 메시지의 최대를 지정 하려면 만들는 **MessageLimitClient** 항목 합니다. 항목을 만든 후 DWORD 값 원하는 비트 길이를 변경 합니다. 구성 되지 않은 경우 기본값 0x8000 바이트 됩니다. 

허용 크기 TLS 서버 클라이언트 인증이 없는 경우 수락할 조각화 된 TLS 핸드셰이크 메시지의 최대를 지정 하려면 만들는 **MessageLimitServer** 항목 합니다. 항목을 만든 후 DWORD 값 원하는 비트 길이를 변경 합니다. 구성 되지 않음 0x4000 바이트 기본값이 됩니다. 

허용 크기 클라이언트 인증 있으면 TLS 서버 수락할 조각화 된 TLS 핸드셰이크 메시지의 최대를 지정 하려면 만들는 **MessageLimitServerClientAuth** 항목 합니다. 항목을 만든 후 DWORD 값 원하는 비트 길이를 변경 합니다. 구성 되지 않은 경우 기본값 0x8000 바이트 됩니다. 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

이 항목 신뢰할 수 있는 발급자 목록이 보낼 때 사용 되는 플래그를 제어 합니다. 서버 인증 기관 클라이언트 인증을 위한는 수백 신뢰 하는 경우는을 보낼 수 있도록 너무 많은 발급자 서버에 대 한 클라이언트 컴퓨터 클라이언트 인증을 요청 하는 경우에 모두 합니다. 이 경우에이 레지스트리 키를 설정 하 고 일부 목록을 보내는 대신 Schannel SSP 보내지 않습니다 모든 목록을 클라이언트를 합니다.

신뢰할 수 있는 발급자 목록이 보내지 않으려면 클라이언트 클라이언트 인증서를 요청 하는 경우 전송 영향을 줄 수 있습니다. 예를 들어, Internet Explorer 클라이언트 인증에 대 한 요청을 받으면만 클라이언트 인증서 체인 최대 서버에서 전송 하는 인증 기관 중 하나를 표시 합니다. 서버가 목록을 보내지 된 모든 클라이언트로에 설치 되어 있는 클라이언트 인증서 Internet Explorer 표시 됩니다. 

이 문제는 것이 좋습니다 수 있습니다. 예를 들어, PKI 환경 상호 인증서를 포함 클라이언트 및 서버 인증서 없을 것 같은 루트, 캘리포니아 따라서 Internet Explorer 서버의 CAs 중 하나를 연결 하는 인증서를 선택한 수 없습니다. 신뢰할 수 있는 발행인이 목록 보내지 않도록 서버를 구성 하 여 Internet Explorer는 모든 인증서를 전송 합니다.

기본적으로이 항목의에서 존재 하지 않습니다.

기본 동작 신뢰할 수 있는 발행인이 목록 보내기

| Windows 버전 | 시간 |
|-----------------|------|
| Windows Server 2012 및 Windows 8 이상 | FALSE |
| Windows Server 2008 R2 및 Windows 7 및 이전 버전 | 진정한 |

해당 되는 버전:에 지정 된 대로 **에 적용 됩니다.** 이 항목의 시작 부분에 있는 목록입니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="servercachetime"></a>ServerCacheTime

이 항목 운영 체제는 서버 쪽 캐시 항목 만료 밀리초에서 시간을 제어할 수 있습니다. 0 서버 쪽 세션 캐시 하 고 방지 다시 연결 합니다. 기본값 위의 ServerCacheTime 증가 Lsass.exe 추가 메모리 사용 하면 됩니다. 일반적으로 각 세션 캐시 요소 2-4 KB 메모리 필요합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 

해당 되는 버전:에 지정 된 대로 **에 적용 됩니다.** 이 항목의 시작 부분에 있는 목록입니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

기본 서버 캐시 시간:에 10 시간

## <a name="ssl-20"></a>2.0 SSL

이 하위 SSL 2.0의 사용을 제어할 수 있습니다.

Windows 10 버전 1607 및 Windows Server 2016부터, SSL 2.0 제거 되 고 더 이상 지원.
SSL 2.0 기본 설정에 대 한 참고 [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)합니다. 

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

만들기 SSL 2.0 프로토콜을 사용 하도록 설정 하는 **사용** 항목에 적합 한 하위 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 1 DWORD 값을 변경 합니다. 프로토콜을 사용 하지 않으려면 DWORD 값 0 변경 합니다.

SSL 2.0 하위 키 표

| 하위 | 설명 |
|--------|-------------|
| 클라이언트 | 제어 SSL 2.0 SSL 클라이언트를 사용 합니다. |
| 서버 | SSL 2.0 SSL 서버에 사용을 제어할 수 있습니다. |
| DisabledByDefault | 기본적으로 SSL 2.0 하지 않으려면 플래그를 지정 합니다. |

## <a name="ssl-30"></a>3.0 SSL

이 하위 SSL 3.0의 사용을 제어할 수 있습니다.

Windows 10 버전 1607 및 Windows Server 2016 부터는 SSL 3.0 기본적으로 비활성화 되었습니다. SSL 3.0 기본 설정에 대 한 참고 [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)합니다. 

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

SSL 3.0 프로토콜을 사용 하도록 설정 하려면 해당 하위에 사용 가능 항목을 만듭니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 1 DWORD 값을 변경 합니다. 프로토콜을 사용 하지 않으려면 DWORD 값 0 변경 합니다.

하위 키 테이블 SSL 3.0

| 하위 | 설명 |
|--------|-------------|
| 클라이언트 | SSL 클라이언트에서 SSL 3.0의 사용을 제어할 수 있습니다. |
| 서버 | SSL 서버에 SSL 3.0의 사용을 제어할 수 있습니다. |
| DisabledByDefault | 기본적으로 SSL 3.0 하지 않으려면 플래그를 지정 합니다. |

## <a name="tls-10"></a>TLS 1.0

이 하위 TLS 1.0의 사용을 제어할 수 있습니다.

참조 TLS 1.0 기본 설정에 대 한 참조 [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)합니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

만들기 TLS 1.0 프로토콜을 사용 하지 않으려면는 **사용** 항목에 적합 한 하위 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 0 DWORD 값을 변경 합니다. 프로토콜을 사용 하려면 DWORD 값 1 변경 합니다.

TLS 1.0 하위 키 표

| 하위 | 설명 |
|--------|-------------|
| 클라이언트 | 제어 TLS 1.0 TLS 클라이언트를 사용 합니다. |
| 서버 | TLS 서버에서 TLS 1.0의 사용을 제어할 수 있습니다. |
| DisabledByDefault | 기본적으로 TLS 1.0 하지 않으려면 플래그를 지정 합니다. |

## <a name="tls-11"></a>1.1 TLS

이 하위 TLS 1.1의 사용을 제어할 수 있습니다.

1.1 TLS 기본 설정에 대 한 참고 [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)합니다.

>[!Note] 
>사용 하도록 설정 하 고 Windows Server 2008 R2 실행 하는 서버에 협상 TLS 1.1을 만들어야는 **DisabledByDefault** 항목에 적합 한 하위 (클라이언트, 서버) "0"로 설정 합니다. 레지스트리에서 항목이 활성화 된 나타나지 않습니다 하 고 "1" 기본적으로 설정 됩니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

만들기 TLS 1.1 프로토콜을 사용 하지 않으려면는 **사용** 항목에 적합 한 하위 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 0 DWORD 값을 변경 합니다. 프로토콜을 사용 하려면 DWORD 값 1 변경 합니다.

하위 키 테이블 TLS 1.1

| 하위 | 설명 |
|--------|-------------|
| 클라이언트 | 제어 TLS 1.1 TLS 클라이언트를 사용 합니다. |
| 서버 | TLS 서버에서 TLS 1.1의 사용을 제어할 수 있습니다. |
| DisabledByDefault | 기본적으로 TLS 1.1 하지 않으려면 플래그를 지정 합니다. |

## <a name="tls-12"></a>1.2 TLS

이 하위 TLS 1.2의 사용을 제어할 수 있습니다.

TLS 1.2 기본 설정에 대 한 참고 [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)합니다.

>[!Note] 
>사용 하도록 설정 하 고 Windows Server 2008 R2 실행 하는 서버에 협상 TLS 1.2 경우 만들어야는 **DisabledByDefault** 항목에 적합 한 하위 (클라이언트, 서버) "0"로 설정 합니다. 레지스트리에서 항목이 활성화 된 나타나지 않습니다 하 고 "1" 기본적으로 설정 됩니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

만들기 TLS 1.2 프로토콜을 사용 하지 않으려면는 **사용** 항목에 적합 한 하위 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 0 DWORD 값을 변경 합니다. 프로토콜을 사용 하려면 DWORD 값 1 변경 합니다.

하위 키 테이블 TLS 1.2

| 하위 | 설명 |
|--------|-------------|
| 클라이언트 | 제어 TLS 1.2 TLS 클라이언트를 사용 합니다. |
| 서버 | TLS 서버에서 TLS 1.2의 사용을 제어할 수 있습니다. |
| DisabledByDefault | 기본적으로 TLS 1.2 하지 않으려면 플래그를 지정 합니다. |

## <a name="dtls-10"></a>DTLS 1.0

이 하위 DTLS 1.0의 사용을 제어할 수 있습니다.

DTLS 1.0 기본 설정에 대 한 참고 [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)합니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

만들기 DTLS 1.0 프로토콜을 사용 하지 않으려면는 **사용** 항목에 적합 한 하위 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 0 DWORD 값을 변경 합니다. 프로토콜을 사용 하려면 DWORD 값 1 변경 합니다.

DTLS 1.0 하위 키 표

| 하위 | 설명 |
|--------|-------------|
| 클라이언트 | DTLS 클라이언트에서 DTLS 1.0의 사용을 제어할 수 있습니다. |
| 서버 | DTLS 서버의 DTLS 1.0의 사용을 제어할 수 있습니다. |
| DisabledByDefault | 기본적으로 DTLS 1.0 하지 않으려면 플래그를 지정 합니다. |

## <a name="dtls-12"></a>DTLS 1.2

이 하위 DTLS 1.2의 사용을 제어할 수 있습니다.

DTLS 1.2 기본 설정에 대 한 참고 [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)합니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

만들기 DTLS 1.2 프로토콜을 사용 하지 않으려면는 **사용** 항목에 적합 한 하위 합니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 0 DWORD 값을 변경 합니다. 프로토콜을 사용 하려면 DWORD 값 1 변경 합니다.

하위 키 테이블 DTLS 1.2

| 하위 | 설명 |
|--------|-------------|
| 클라이언트 | DTLS 클라이언트에서 DTLS 1.2의 사용을 제어할 수 있습니다. |
| 서버 | DTLS 서버의 DTLS 1.2의 사용을 제어할 수 있습니다. |
| DisabledByDefault | 기본적으로 DTLS 1.2 하지 않으려면 플래그를 지정 합니다. |

