---
title: TLS (전송 계층 보안) 레지스트리 설정
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-tls-ssl
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic
ms.date: 02/28/2019
ms.openlocfilehash: d65b314d6896c886ce606d2b649fcfd7309c583b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820286"
---
# <a name="transport-layer-security-tls-registry-settings"></a>TLS (전송 계층 보안) 레지스트리 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10

IT 전문가를 위한이 참조 항목에는 TLS (전송 계층 보안) 프로토콜의 Windows 구현에 대 한 지원 되는 레지스트리 설정 정보와 Schannel 보안 지원을 통한 SSL(Secure Sockets Layer) (SSL) 프로토콜이 포함 되어 있습니다. 공급자 (SSP). 이 항목에서 설명 하는 레지스트리 하위 키와 항목은 Schannel SSP, 특히 TLS 및 SSL 프로토콜을 관리 하 고 문제를 해결 하는 데 도움이 됩니다. 

> [!CAUTION]
> 이 정보는 문제를 해결하거나 필요한 설정이 적용되었는지 확인할 때 사용할 참조로 제공됩니다.
> 다른 대안이 없는 경우가 아니면 레지스트리를 직접 편집하지 않는 것이 좋습니다.
> 레지스트리 수정 내용은 적용되기 전에 레지스트리 편집기 또는 Windows 운영 체제에서 유효성이 검사되지 않습니다.
> 따라서 잘못된 값이 저장될 수 있으며, 이로 인해 시스템에서 복구할 수 없는 오류가 발생할 수 있습니다.
> 가능하면 레지스트리를 직접 편집하는 대신 그룹 정책 또는 MMC(Microsoft Management Console)와 같은 다른 Windows 도구를 사용하여 작업을 수행합니다.
> 레지스트리를 편집해야 하는 경우 각별히 주의하세요.

## <a name="certificatemappingmethods"></a>CertificateMappingMethods 

이 항목은 기본적으로 레지스트리에 없습니다. 기본값은 아래에 나열된 인증서 매핑 방법 4개가 모두 지원되는 것입니다.

서버 애플리케이션에 클라이언트 인증이 필요한 경우 Schannel이 클라이언트 컴퓨터에서 사용자 계정에 제공하는 인증서를 자동으로 매핑하려고 합니다. 인증서 정보를 Windows 사용자 계정에 연결하는 매핑을 만들어 클라이언트 인증서를 사용하여 로그인하는 사용자를 인증할 수 있습니다. 인증서 매핑을 만들고 사용하도록 설정하면 클라이언트가 클라이언트 인증서를 제공할 때마다 서버 애플리케이션이 해당 사용자를 적절한 Windows 사용자 계정에 자동으로 연결합니다.

대부분의 경우 인증서는 다음 두 가지 방법 중 하나로 사용자 계정에 매핑됩니다. 

- 단일 인증서가 단일 사용자 계정에 매핑됩니다(일대일 매핑).
- 여러 인증서가 하나의 사용자 계정에 매핑됩니다(다대일 매핑).

기본적으로 Schannel 공급자는 기본 설정 순서대로 나열된 다음 4개의 인증서 매핑 방법을 사용합니다.

1. Kerberos S4U(Service-For-User) 인증서 매핑
2. 사용자 계정 이름 매핑
3. 일대일 매핑(주체/발급자 매핑이라고도 함)
4. 다대일 매핑

해당 하는 버전:이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 것과 같습니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="ciphers"></a>Ciphers

TLS/SSL 암호는 암호화 그룹 순서를 구성 하 여 제어 해야 합니다. 자세한 내용은 [TLS 암호 그룹 순서 구성](manage-tls.md#configuring-tls-cipher-suite-order)을 참조 하세요.

Schannel SSP에서 사용 되는 기본 암호 그룹 순서에 대 한 자세한 내용은 [TLS/SSL (SCHANNEL ssp)의 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)을 참조 하세요. 

## <a name="ciphersuites"></a>CipherSuites

그룹 정책, MDM 또는 PowerShell을 사용 하 여 TLS/SSL 암호 그룹을 구성 해야 합니다. 자세한 내용은 [Tls 암호 그룹 순서 구성](manage-tls.md#configuring-tls-cipher-suite-order) 을 참조 하세요.

Schannel SSP에서 사용 되는 기본 암호 그룹 순서에 대 한 자세한 내용은 [TLS/SSL (SCHANNEL ssp)의 암호 그룹](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)을 참조 하세요. 


## <a name="clientcachetime"></a>ClientCacheTime

이 항목은 운영 체제에서 클라이언트 쪽 캐시 항목을 만료하는 데 걸리는 시간(밀리초)을 제어합니다. 값이 0이면 보안 연결 캐싱이 해제됩니다. 이 항목은 기본적으로 레지스트리에 없습니다. 

클라이언트가 Schannel SSP를 통해 서버에 처음 연결하는 경우 전체 TLS/SSL 핸드셰이크가 수행됩니다. 완료되면 마스터 보안, 암호 그룹 및 인증서가 해당 클라이언트와 서버의 세션 캐시에 저장됩니다.

Windows Server 2008 및 Windows Vista 부터는 기본 클라이언트 캐시 시간이 10 시간입니다.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

기본 클라이언트 캐시 시간

## <a name="enableocspstaplingforsni"></a>EnableOcspStaplingForSni

OCSP (온라인 인증서 상태 프로토콜) 스테이플링을 사용 하면 인터넷 정보 서비스 (IIS)와 같은 웹 서버에서 TLS 핸드셰이크 중 클라이언트에 서버 인증서를 보낼 때 서버 인증서의 현재 해지 상태를 제공할 수 있습니다. 이 기능을 통해 웹 서버에서 서버 인증서의 현재 OCSP 상태를 캐시 하 고 여러 웹 클라이언트에 보낼 수 있으므로 OCSP 서버에 대 한 부하를 줄일 수 있습니다. 이 기능이 없으면 각 웹 클라이언트는 OCSP 서버에서 서버 인증서의 현재 OCSP 상태를 검색 하려고 시도 합니다. 이렇게 하면 해당 OCSP 서버에서 부하가 높아집니다. 

IIS 외에도, http.sys를 통한 웹 서비스는 Active Directory Federation Services (AD FS) 및 웹 응용 프로그램 프록시 (WAP)를 포함 하 여이 설정의 이점을 누릴 수 있습니다. 

기본적으로, 간단한 보안 (SSL/TLS) 바인딩을 사용 하는 IIS 웹 사이트에서는 OCSP 지원이 사용 됩니다. 그러나 IIS 웹 사이트에서 다음 유형의 보안 (SSL/TLS) 바인딩 중 하나 또는 둘 모두를 사용 하는 경우에는이 지원이 기본적으로 사용 되지 않습니다.
- 서버 이름 표시 필요
- 중앙 인증서 저장소 사용

이 경우 TLS 핸드셰이크 중 서버 hello 응답은 기본적으로 OCSP 스테이플 상태를 포함 하지 않습니다. 이 동작을 통해 성능이 향상 됩니다. Windows OCSP 스테이플링 구현은 수백 개의 서버 인증서로 확장 됩니다. SNI 및 CCS는 IIS를 사용 하 여 수천 개의 서버 인증서를 포함할 수 있는 수천 개의 웹 사이트로 확장할 수 있으므로이 동작을 기본적으로 사용 하도록 설정 하면 성능 문제가 발생할 수 있습니다.

해당 하는 버전: Windows Server 2012 및 Windows 8부터 모든 버전 

레지스트리 경로: [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL]

다음 키를 추가 합니다.

"EnableOcspStaplingForSni" = dword: 00000001

사용 하지 않도록 설정 하려면 DWORD 값을 0으로 설정 합니다.

"EnableOcspStaplingForSni" = dword: 00000000

> [!NOTE] 
> 이 레지스트리 키를 사용 하도록 설정 하면 성능에 영향을 줄 수 있습니다.

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

이 항목은 FIPS(Federal Information Processing) 규정 준수를 제어합니다. 기본값은 0입니다.

해당 하는 버전: Windows Server 2012 및 Windows 8부터 모든 버전 

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\LSA

Windows Server FIPS 암호 그룹: [SCHANNEL SSP에서 지원 되는 암호 그룹 및 프로토콜](https://technet.microsoft.com/library/dn786419.aspx)을 참조 하세요.

## <a name="hashes"></a>Hashes

TLS/SSL 해시 알고리즘은 암호 그룹 순서를 구성 하 여 제어 해야 합니다. 자세한 내용은 [TLS 암호 그룹 순서 구성](manage-tls.md#configuring-tls-cipher-suite-order) 을 참조 하세요.

## <a name="issuercachesize"></a>IssuerCacheSize

이 항목은 발급자 캐시의 크기를 제어하며 발급자 매핑과 함께 사용됩니다. Schannel SSP는 클라이언트 인증서의 직접 발급자 뿐만 아니라 클라이언트 인증서 체인의 모든 발급자를 매핑하려고 시도 합니다. 일반적인 경우지만 발급자가 계정에 매핑되지 않는 경우 서버는 동일한 발급자 이름을 반복해서 초당 수백 번 매핑하려고 합니다. 

이를 방지하기 위해 서버에는 부정 캐시가 있으므로 발급자 이름이 계정에 매핑되지 않는 경우 캐시에 추가되고 캐시 항목이 만료될 때까지 Schannel SSP에서 발급자 이름을 다시 매핑하려고 시도하지 않습니다. 이 레지스트리 항목은 캐시 크기를 지정합니다. 이 항목은 기본적으로 레지스트리에 없습니다. 기본값은 100입니다. 

해당 하는 버전: Windows Server 2008 및 Windows Vista부터 모든 버전

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="issuercachetime"></a>IssuerCacheTime

이 항목은 캐시 시간 제한 간격의 길이를 밀리초 단위로 제어합니다. Schannel SSP는 클라이언트 인증서의 직접 발급자 뿐만 아니라 클라이언트 인증서 체인의 모든 발급자를 매핑하려고 시도 합니다. 발급자가 계정에 매핑되지 않는 경우 서버는 동일한 발급자 이름을 반복해서 초당 수백 번 매핑하려고 합니다.

이를 방지하기 위해 서버에는 부정 캐시가 있으므로 발급자 이름이 계정에 매핑되지 않는 경우 캐시에 추가되고 캐시 항목이 만료될 때까지 Schannel SSP에서 발급자 이름을 다시 매핑하려고 시도하지 않습니다. 이 캐시는 시스템이 동일한 발급자를 계속 매핑하지 않도록 성능상의 이유로 유지됩니다. 이 항목은 기본적으로 레지스트리에 없습니다. 기본값은 10분입니다.

해당 하는 버전: Windows Server 2008 및 Windows Vista부터 모든 버전

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>KeyExchangeAlgorithm-클라이언트 RSA 키 크기

이 항목은 클라이언트 RSA 키 크기를 제어 합니다. 

키 교환 알고리즘의 사용은 암호 그룹 순서를 구성 하 여 제어 해야 합니다.

Windows 10, 버전 1507 및 Windows Server 2016에서 추가 되었습니다.

레지스트리 경로: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS

TLS 클라이언트에 대해 지원 되는 최소 범위의 RSA 키 비트 길이를 지정 하려면 **Clientminkeybitlength** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 원하는 비트 길이로 변경 합니다. 구성 되지 않은 경우 1024 비트가 최소값입니다. 

TLS 클라이언트에 대해 지원 되는 최대 RSA 키 비트 길이 범위를 지정 하려면 **Clientmaxkeybitlength** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 원하는 비트 길이로 변경 합니다. 구성 되지 않은 경우 최대값은 적용 되지 않습니다.

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>KeyExchangeAlgorithm-Diffie-hellman 키 크기

이 항목은 Diffie-hellman 키 크기를 제어 합니다. 

키 교환 알고리즘의 사용은 암호 그룹 순서를 구성 하 여 제어 해야 합니다.

Windows 10, 버전 1507 및 Windows Server 2016에서 추가 되었습니다.

레지스트리 경로: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie-Hellman

TLS 클라이언트에 대해 지원 되는 최소 범위의 Diffie-hellman 키 비트 길이를 지정 하려면 **Clientminkeybitlength** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 원하는 비트 길이로 변경 합니다. 구성 되지 않은 경우 1024 비트가 최소값입니다. 
 
TLS 클라이언트에 대해 지원 되는 최대 Diffie-hellman 키 비트 길이를 지정 하려면 **Clientmaxkeybitlength** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 원하는 비트 길이로 변경 합니다. 구성 되지 않은 경우 최대값은 적용 되지 않습니다. 
 
TLS 서버 기본값에 대해 Diffie-hellman (Man-in-the-middle) 키 비트 길이를 지정 하려면 **Serverminkeybitlength** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 원하는 비트 길이로 변경 합니다. 구성 되지 않은 경우 2048 비트가 기본값이 됩니다. 

## <a name="maximumcachesize"></a>MaximumCacheSize

이 항목은 최대 캐시 요소 수를 제어합니다. MaximumCacheSize를 0으로 설정하면 서버 쪽 세션 캐시가 사용되지 않고 다시 연결이 방지됩니다. MaximumCacheSize를 기본값보다 높게 늘리면 Lsass.exe가 추가 메모리를 사용합니다. 각 세션 캐시 요소에는 일반적으로 2-4kb의 메모리가 필요 합니다. 이 항목은 기본적으로 레지스트리에 없습니다. 기본값은 2만 요소입니다. 

해당 하는 버전: Windows Server 2008 및 Windows Vista부터 모든 버전

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="messaging--fragment-parsing"></a>메시징-조각 구문 분석

________________________________________
이 항목은 허용 될 조각화 된 TLS 핸드셰이크 메시지의 최대 허용 크기를 제어 합니다. 허용 되는 크기 보다 큰 메시지는 허용 되지 않으며 TLS 핸드셰이크는 실패 합니다. 이러한 항목은 기본적으로 레지스트리에 존재 하지 않습니다. 

값을 0x0으로 설정 하면 조각화 된 메시지가 처리 되지 않고 TLS 핸드셰이크가 실패 합니다. 이렇게 하면 현재 컴퓨터의 TLS 클라이언트 또는 서버가 TLS Rfc와 호환 되지 않습니다. 

최대 허용 크기는 최대 2 ^ 24-1 바이트까지 늘릴 수 있습니다. 클라이언트 또는 서버가 네트워크에서 확인 되지 않은 대량의 데이터를 읽고 저장할 수 있도록 허용 하는 것은 바람직하지 않으며 각 보안 컨텍스트에 추가 메모리가 사용 됩니다. 

Windows 7 및 Windows Server 2008 r 2에서 추가 되었습니다.
Windows XP, Windows Vista 또는 windows Server 2008에서 Internet Explorer를 사용 하 여 조각화 된 TLS/SSL 핸드셰이크 메시지를 구문 분석할 수 있는 업데이트를 사용할 수 있습니다.

레지스트리 경로: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Messaging

TLS 클라이언트에서 허용 하는 조각화 된 TLS 핸드셰이크 메시지의 최대 허용 크기를 지정 하려면 **messageaccept 클라이언트** 항목을 만듭니다. 항목을 만든 후 DWORD 값을 원하는 비트 길이로 변경 합니다. 구성 되지 않은 경우 기본값은 0x8000 바이트가 됩니다. 

클라이언트 인증이 없을 때 TLS 서버에서 허용 하는 조각화 된 TLS 핸드셰이크 메시지의 최대 허용 크기를 지정 하려면 **Messageaccept 서버** 항목을 만듭니다. 항목을 만든 후 DWORD 값을 원하는 비트 길이로 변경 합니다. 구성 되지 않은 경우 기본값은 0x4000 바이트가 됩니다. 

클라이언트 인증이 있을 때 TLS 서버에서 허용 하는 조각화 된 TLS 핸드셰이크 메시지의 최대 허용 크기를 지정 하려면 **messageaccept Serverclientauth** 항목을 만듭니다. 항목을 만든 후 DWORD 값을 원하는 비트 길이로 변경 합니다. 구성 되지 않은 경우 기본값은 0x8000 바이트가 됩니다. 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

이 항목은 신뢰할 수 있는 발급자 목록을 보낼 때 사용되는 플래그를 제어합니다. 클라이언트 인증에 대해 수백 개의 인증 기관을 신뢰하는 서버의 경우 발급자가 너무 많아 서버에서 클라이언트 인증을 요청할 때 클라이언트 컴퓨터에 모두 보낼 수 없습니다. 이런 경우에는 이 레지스트리 키를 설정할 수 있으며, 부분 목록을 보내는 대신 Schannel SSP에서 클라이언트에 목록을 보내지 않습니다.

신뢰할 수 있는 발급자 목록을 보내지 않으면 클라이언트 인증서가 요청될 때 클라이언트가 보내는 사항에 영향을 줄 수 있습니다. 예를 들어 Internet Explorer는 클라이언트 인증 요청을 받을 경우 서버에서 보낸 인증 기관 중 하나로 연결되는 클라이언트 인증서만 표시합니다. 서버에서 목록을 보내지 않은 경우 Internet Explorer는 클라이언트에 설치된 모든 클라이언트 인증서를 표시합니다. 

이 동작은 바람직할 수도 있습니다. 예를 들어 PKI 환경에 상호 인증서가 포함 된 경우 클라이언트 및 서버 인증서는 동일한 루트 CA를 갖지 않습니다. 따라서 Internet Explorer는 서버 Ca 중 하나에 연결 되는 인증서를 선택할 수 없습니다. 신뢰할 수 있는 발급자 목록을 보내지 않도록 서버를 구성하면 Internet Explorer에서 모든 인증서를 보냅니다.

이 항목은 기본적으로 레지스트리에 없습니다.

기본 신뢰할 수 있는 발급자 목록 보내기 동작

| Windows 버전 | 시간 |
|-----------------|------|
| Windows Server 2012 및 Windows 8 이상 | FALSE |
| Windows Server 2008 R2 및 Windows 7 및 이전 버전 | TRUE |

해당 하는 버전: Windows Server 2008 및 Windows Vista부터 모든 버전

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="servercachetime"></a>ServerCacheTime

이 항목은 운영 체제에서 서버 쪽 캐시 항목을 만료하는 데 걸리는 시간(밀리초)을 제어합니다. 값이 0이면 서버 쪽 세션 캐시가 사용되지 않고 다시 연결이 방지됩니다. ServerCacheTime을 기본값보다 높게 늘리면 Lsass.exe가 추가 메모리를 사용합니다. 각 세션 캐시 요소에는 일반적으로 2-4kb의 메모리가 필요 합니다. 이 항목은 기본적으로 레지스트리에 없습니다. 

해당 하는 버전: Windows Server 2008 및 Windows Vista부터 모든 버전

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

기본 서버 캐시 시간: 10 시간

## <a name="ssl-20"></a>SSL 2.0

이 하위 키는 SSL 2.0의 사용을 제어 합니다.

Windows 10, 버전 1607 및 Windows Server 2016부터 SSL 2.0이 제거 되어 더 이상 지원 되지 않습니다.
SSL 2.0 기본 설정에 대 한 자세한 내용은 [TLS/SSL (SCHANNEL SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)을 참조 하세요. 

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

SSL 2.0 프로토콜을 사용 하도록 설정 하려면 다음 표에 설명 된 대로 클라이언트 또는 서버 하위 키에서 **사용** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 

SSL 2.0 하위 키 표

| 하위 키 | 설명 |
|--------|-------------|
| 클라이언트 | SSL 클라이언트에서 SSL 2.0의 사용을 제어 합니다. |
| Server | SSL 서버에서 SSL 2.0의 사용을 제어 합니다. |

클라이언트 또는 서버에 대해 SSL 2.0을 사용 하지 않도록 설정 하려면 DWORD 값을 0으로 변경 합니다. SSPI 앱에서 SSL 2.0을 사용 하도록 요청 하는 경우 거부 됩니다. 

기본적으로 SSL 2.0을 사용 하지 않도록 설정 하려면 **DisabledByDefault** 항목을 만들고 DWORD 값을 1로 변경 합니다. SSPI 앱에서 SSL 2.0을 사용 하도록 요청 하는 경우 explcitly가 협상 될 수 있습니다. 

다음 예제에서는 레지스트리에서 SSL 2.0을 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![SSL 2.0 사용 안 함](images/ssl-2-registry-setting.png)


## <a name="ssl-30"></a>SSL 3.0

이 하위 키는 SSL 3.0의 사용을 제어 합니다.

Windows 10, 버전 1607 및 Windows Server 2016부터 SSL 3.0은 기본적으로 사용 하지 않도록 설정 되어 있습니다. SSL 3.0 기본 설정에 대 한 자세한 내용은 [TLS/SSL (SCHANNEL SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)을 참조 하세요. 

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

SSL 3.0 프로토콜을 사용 하도록 설정 하려면 다음 표에 설명 된 대로 클라이언트 또는 서버 하위 키에서 **사용** 항목을 만듭니다.  
이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 

SSL 3.0 하위 키 표

| 하위 키 | 설명 |
|--------|-------------|
| 클라이언트 | SSL 클라이언트에서 SSL 3.0의 사용을 제어 합니다. |
| Server | SSL 서버에서 SSL 3.0의 사용을 제어 합니다. |

클라이언트 또는 서버에 대해 SSL 3.0을 사용 하지 않도록 설정 하려면 DWORD 값을 0으로 변경 합니다.
SSPI 앱에서 SSL 3.0을 사용 하도록 요청 하는 경우 거부 됩니다. 

기본적으로 SSL 3.0을 사용 하지 않도록 설정 하려면 **DisabledByDefault** 항목을 만들고 DWORD 값을 1로 변경 합니다. SSPI 앱에서 SSL 3.0을 사용 하도록 명시적으로 요청 하는 경우 협상 될 수 있습니다. 

다음 예제에서는 레지스트리에서 SSL 3.0을 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![SSL 3.0 사용 안 함](images/ssl-3-registry-setting.png)

## <a name="tls-10"></a>TLS 1.0

이 하위 키는 TLS 1.0의 사용을 제어 합니다.

TLS 1.0 기본 설정에 대 한 자세한 내용은 [tls/SSL (SCHANNEL SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)을 참조 하세요.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.0 프로토콜을 사용 하도록 설정 하려면 다음 표에 설명 된 대로 Client 또는 Server 하위 키에서 **사용** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 

TLS 1.0 하위 키 표

| 하위 키 | 설명 |
|--------|-------------|
| 클라이언트 | TLS 클라이언트에서 TLS 1.0의 사용을 제어 합니다. |
| Server | TLS 서버에서 TLS 1.0의 사용을 제어 합니다. |

클라이언트 또는 서버에 대해 TLS 1.0을 사용 하지 않도록 설정 하려면 DWORD 값을 0으로 변경 합니다.
SSPI 앱이 TLS 1.0를 사용 하도록 요청 하는 경우 거부 됩니다. 

기본적으로 TLS 1.0을 사용 하지 않도록 설정 하려면 **DisabledByDefault** 항목을 만들고 DWORD 값을 1로 변경 합니다. SSPI 앱이 TLS 1.0를 사용 하도록 명시적으로 요청 하는 경우 협상 될 수 있습니다. 

다음 예제에서는 레지스트리에서 사용 하지 않도록 설정 된 TLS 1.0을 보여 줍니다.

![TLS 1.0 사용 안 함](images/tls-registry-setting.png)

## <a name="tls-11"></a>TLS 1.1

이 하위 키는 TLS 1.1의 사용을 제어 합니다.

TLS 1.1 기본 설정에 대 한 자세한 내용은 [tls/SSL (SCHANNEL SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)을 참조 하세요.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.1 프로토콜을 사용 하도록 설정 하려면 다음 표에 설명 된 대로 Client 또는 Server 하위 키에서 **사용** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 

TLS 1.1 하위 키 표

| 하위 키 | 설명 |
|--------|-------------|
| 클라이언트 | TLS 클라이언트에서 TLS 1.1의 사용을 제어 합니다. |
| Server | TLS 서버에서 TLS 1.1의 사용을 제어 합니다. |

클라이언트 또는 서버에 대해 TLS 1.1을 사용 하지 않도록 설정 하려면 DWORD 값을 0으로 변경 합니다.
SSPI 앱이 TLS 1.1를 사용 하도록 요청 하는 경우 거부 됩니다. 

기본적으로 TLS 1.1을 사용 하지 않도록 설정 하려면 **DisabledByDefault** 항목을 만들고 DWORD 값을 1로 변경 합니다. SSPI 앱이 TLS 1.1를 사용 하도록 명시적으로 요청 하는 경우 협상 될 수 있습니다. 

다음 예제에서는 레지스트리에서 사용 하지 않도록 설정 된 TLS 1.1을 보여 줍니다.

![TLS 1.1 사용 안 함](images/tls-11-registry-setting.png)

## <a name="tls-12"></a>TLS 1.2

이 하위 키는 TLS 1.2의 사용을 제어 합니다.

TLS 1.2 기본 설정에 대 한 자세한 내용은 [tls/SSL (SCHANNEL SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)을 참조 하세요.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.2 프로토콜을 사용 하도록 설정 하려면 다음 표에 설명 된 대로 Client 또는 Server 하위 키에서 **사용** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 

TLS 1.2 하위 키 표

| 하위 키 | 설명 |
|--------|-------------|
| 클라이언트 | TLS 클라이언트에서 TLS 1.2의 사용을 제어 합니다. |
| Server | TLS 서버에서 TLS 1.2의 사용을 제어 합니다. |

클라이언트 또는 서버에 대해 TLS 1.2을 사용 하지 않도록 설정 하려면 DWORD 값을 0으로 변경 합니다.
SSPI 앱이 TLS 1.2를 사용 하도록 요청 하는 경우 거부 됩니다. 

기본적으로 TLS 1.2을 사용 하지 않도록 설정 하려면 **DisabledByDefault** 항목을 만들고 DWORD 값을 1로 변경 합니다. SSPI 앱이 TLS 1.2를 사용 하도록 명시적으로 요청 하는 경우 협상 될 수 있습니다. 

다음 예제에서는 레지스트리에서 사용 하지 않도록 설정 된 TLS 1.2을 보여 줍니다.

![TLS 1.2 사용 안 함](images/tls-12-registry-setting.png)

## <a name="dtls-10"></a>DTLS 1.0

이 하위 키는 DTLS 1.0의 사용을 제어 합니다.

DTLS 1.0 기본 설정에 대 한 자세한 내용은 [TLS/SSL (SCHANNEL SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)을 참조 하세요.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

DTLS 1.0 프로토콜을 사용 하도록 설정 하려면 다음 표에 설명 된 대로 Client 또는 Server 하위 키에서 **사용** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 

DTLS 1.0 하위 키 표

| 하위 키 | 설명 |
|--------|-------------|
| 클라이언트 | DTLS 클라이언트에서 DTLS 1.0의 사용을 제어 합니다. |
| Server | DTLS 서버에서 DTLS 1.0의 사용을 제어 합니다. |

클라이언트 또는 서버에 대해 DTLS 1.0을 사용 하지 않도록 설정 하려면 DWORD 값을 0으로 변경 합니다.
SSPI 앱이 DTLS 1.0을 사용 하도록 요청 하는 경우 거부 됩니다. 

DTLS 1.0를 기본적으로 사용 하지 않도록 설정 하려면 **DisabledByDefault** 항목을 만들고 DWORD 값을 1로 변경 합니다. SSPI 앱이 DTLS 1.0을 사용 하도록 명시적으로 요청 하는 경우 협상 될 수 있습니다. 

다음 예제에서는 레지스트리에서 DTLS 1.0을 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![DTLS 1.0 사용 안 함](images/dtls-10-registry-setting.png)

## <a name="dtls-12"></a>DTLS 1.2

이 하위 키는 DTLS 1.2의 사용을 제어 합니다.

DTLS 1.2 기본 설정에 대 한 자세한 내용은 [TLS/SSL (SCHANNEL SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)을 참조 하세요.

레지스트리 경로: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

DTLS 1.2 프로토콜을 사용 하도록 설정 하려면 다음 표에 설명 된 대로 Client 또는 Server 하위 키에서 **사용** 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 

DTLS 1.2 하위 키 표

| 하위 키 | 설명 |
|--------|-------------|
| 클라이언트 | DTLS 클라이언트에서 DTLS 1.2의 사용을 제어 합니다. |
| Server | DTLS 서버에서 DTLS 1.2의 사용을 제어 합니다. |


클라이언트 또는 서버에 대해 DTLS 1.2을 사용 하지 않도록 설정 하려면 DWORD 값을 0으로 변경 합니다.
SSPI 앱이 DTLS 1.0을 사용 하도록 요청 하는 경우 거부 됩니다. 

DTLS 1.2를 기본적으로 사용 하지 않도록 설정 하려면 **DisabledByDefault** 항목을 만들고 DWORD 값을 1로 변경 합니다. SSPI 앱이 DTLS 1.2을 사용 하도록 명시적으로 요청 하는 경우 협상 될 수 있습니다. 

다음 예제에서는 레지스트리에서 DTLS 1.1을 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![DTLS 1.1 사용 안 함](images/dtls-11-registry-setting.png)


