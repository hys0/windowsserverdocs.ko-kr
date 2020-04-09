---
title: TLS-SSL (Schannel SSP) 개요
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-tls-ssl
ms.topic: article
ms.assetid: c8836345-16bb-4dcc-8d2b-2b9b687456a3
author: justinha
ms.author: justinha
manager: brianlic
ms.date: 05/16/2018
ms.openlocfilehash: 5478a97a6b333cfc92de100440d53a769a8c0fd9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855194"
---
# <a name="overview-of-tls---ssl-schannel-ssp"></a>TLS-SSL (Schannel SSP) 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

IT 전문가를 위한이 항목에서는 Windows Server 2012 R2, Windows Server 2012, Windows 8.1 및 Windows 8에 대 한 TLS (Transport Layer Security), SSL(Secure Sockets Layer) (SSL) 및 DTLS (데이터 그램 전송 계층 보안) 인증 프로토콜을 포함 하는 Schannel SSP (Security Support Provider)의 기능에 대 한 변경 내용에 대해 설명 합니다.

Schannel은 SSL, TLS 및 DTLS 인터넷 표준 인증 프로토콜을 구현한 SSP(Security Support Provider)입니다. SSPI(Security Support Provider Interface)는 인증을 비롯한 보안 관련 기능을 수행하기 위해 Windows 시스템에서 사용되는 API입니다. SSPI는 Schannel SSP를 포함한 몇몇 SSP(Security Support Provider)의 공용 인터페이스로 사용됩니다.

Schannel SSP에서 Microsoft의 TLS 및 SSL 구현에 대 한 자세한 내용은 [tls/Ssl 기술 참조 (2003)](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)를 참조 하세요.


## <a name="tlsssl-schannel-ssp-features"></a>TLS/SSL (Schannel SSP) 기능
다음은 Schannel SSP의 TLS 기능을 설명 합니다.

### <a name="tls-session-resumption"></a>TLS 세션 다시 시작
Schannel SSP(Security Support Provider)의 구성 요소인 TLS(전송 계층 보안) 프로토콜은 신뢰할 수 없는 네트워크에서 애플리케이션 간에 전송되는 데이터를 보호하는 데 사용됩니다. TLS/SSL을 사용하면 서버와 클라이언트 컴퓨터를 인증한 다음 인증된 파티 간의 메시지를 암호화할 수 있습니다.

서버에 TLS를 연결하는 장치는 세션 만료로 인해 다시 연결해야 하는 경우가 종종 있습니다. Windows 8.1 및 Windows Server 2012 R2는 이제 RFC 5077 (서버 쪽 상태 없이 TLS 세션 다시 시작)을 지원 합니다. 이 수정 사항은 다음을 통해 Windows Phone 및 Windows RT 장치를 제공 합니다.

-   서버에서 리소스 사용량 감소

-   대역폭 감소로 인한 클라이언트 연결의 효율성 향상

-   연결 재개로 인해 TLS 핸드셰이크에 소요된 시간 감소

> [!NOTE]
> Windows 8에서 RFC 5077의 클라이언트 쪽 구현이 추가 되었습니다.

상태 비저장 TLS 세션 다시 시작에 대한 자세한 내용은 IETF 문서 [RFC 5077](http://www.ietf.org/rfc/rfc5077)을 참조하세요.

### <a name="application-protocol-negotiation"></a>응용 프로그램 프로토콜 협상
 Windows Server 2012 R2 및 Windows 8.1는 클라이언트 쪽 TLS 응용 프로그램 프로토콜 협상을 지원 하므로 응용 프로그램은 HTTP 2.0 표준 개발의 일부로 프로토콜을 활용할 수 있으며, 사용자는 SPDY 프로토콜을 실행 하는 앱을 사용 하 여 Google 및 Twitter와 같은 온라인 서비스에 액세스할 수 있습니다.

**작동 방식**

지원되는 애플리케이션 프로토콜 ID 목록을 기본 설정의 내림차순으로 제공하여 클라이언트 및 서버 애플리케이션이 애플리케이션 프로토콜 협상 확장을 사용하도록 설정합니다. TLS 클라이언트가 ClientHello 메시지에 클라이언트 지원 프로토콜 목록이 포함된 ALPN(Application Layer Protocol Negotiation) 확장을 포함시킴으로써 애플리케이션 프로토콜 협상을 지원한다는 것을 나타냅니다.

TLS 클라이언트가 서버에 요청을 보내면 TLS 서버가 클라이언트도 지원하는 가장 선호하는 애플리케이션 프로토콜에서 해당하는 지원 프로토콜 목록을 읽습니다. 이러한 프로토콜을 찾으면 서버는 선택한 프로토콜 ID로 응답하고 평상시처럼 핸드셰이크를 계속 진행합니다. 일반 애플리케이션 프로토콜이 없는 경우 서버는 심각한 핸드셰이크 오류 경고를 보냅니다.

### <a name="management-of-trusted-issuers-for-client-authentication"></a><a name="BKMK_TrustedIssuers"></a>클라이언트 인증에 대 한 신뢰할 수 있는 발급자 관리
클라이언트 컴퓨터의 인증에 SSL 또는 TLS를 사용해야 하는 경우 신뢰할 수 있는 인증서 발급자 목록을 보내도록 서버를 구성할 수 있습니다. 이 목록은 서버가 신뢰하는 인증서 발급자 집합을 포함하며 여러 인증서가 있는 경우 어떤 클라이언트 인증서를 선택할 것인가에 관해 클라이언트 컴퓨터에 힌트를 제공합니다. 또한 클라이언트 컴퓨터에서 서버로 보내는 인증서 체인은 신뢰할 수 있는 발급자 목록에 대해 유효성이 검사되어야 합니다.

Windows Server 2012 및 Windows 8 이전에는 Schannel SSP (http.sys 및 IIS 포함)를 사용 하는 응용 프로그램이 나 프로세스에서 CTL (인증서 신뢰 목록)을 통해 클라이언트 인증에 대해 지원 되는 신뢰할 수 있는 발급자 목록을 제공할 수 있었습니다.

Windows Server 2012 및 Windows 8에서는 기본 인증 프로세스가 다음과 같이 변경 되었습니다.

-   CTL 기반의 신뢰할 수 있는 발급자 목록 관리가 더 이상 지원되지 않습니다.

-   기본적으로 신뢰할 수 있는 발급자 목록을 전송 하는 동작은 off입니다. SendTrustedIssuerList 레지스트리 키의 기본값은 이제 1이 아닌 0 (기본적으로 해제)입니다.

-   이전 버전의 Windows 운영 체제와의 호환성은 유지됩니다.

**이는 어떤 값을 추가 하나요?**

Windows Server 2012부터 CTL 사용이 인증서 저장소 기반 구현으로 대체 되었습니다. 이를 통해 PowerShell 공급자의 기존 인증서 관리 commandlet 및 certutil.exe와 같은 명령줄 도구를 사용하여 더욱 친숙한 방법으로 관리할 수 있게 되었습니다.

Schannel SSP가 지 원하는 신뢰할 수 있는 인증 기관 목록의 최대 크기 (16kb)는 Windows Server 2008 r 2와 동일 하 게 유지 되지만, Windows Server 2012에는 관련 되지 않은 인증서가 메시지에 포함 되지 않도록 클라이언트 인증 발급자에 대 한 새로운 전용 인증서 저장소가 있습니다.

**어떻게 작동 하나요?**

Windows Server 2012에서는 신뢰할 수 있는 발급자 목록이 인증서 저장소를 사용 하 여 구성 됩니다. 하나의 기본 글로벌 컴퓨터 인증서 저장소와 사이트별로 하나는 선택 사항입니다. 목록의 원본은 다음과 같이 결정됩니다.

-   사이트의 대해 구성된 특정 인증서 저장소가 있는 경우 해당 인증서 저장소가 원본으로 사용됩니다.

-   인증서가 응용 프로그램 정의 저장소에 없으면 Schannel은 로컬 컴퓨터에서 **클라이언트 인증 발급자** 저장소를 확인하고 인증서가 있으면 해당 저장소를 원본으로 사용합니다. 인증서가 둘 중 어떤 저장소에도 없는 경우 신뢰할 수 있는 루트 저장소가 선택됩니다.

-   전역 또는 로컬 저장소에 인증서가 모두 없는 경우 Schannel 공급자는 신뢰할 수 있는 **루트 인증 기관** 저장소를 신뢰할 수 있는 발급자 목록의 원본으로 사용 합니다. 이는 Windows Server 2008 r 2의 동작입니다.

사용 된 **신뢰할 수 있는 루트 인증 기관** 저장소에 루트 (자체 서명 됨)와 ca (인증 기관) 발급자 인증서가 혼합 되어 있는 경우에는 기본적으로 ca 발급자 인증서만 서버로 전송 됩니다.

**신뢰할 수 있는 발급자에 대해 인증서 저장소를 사용 하도록 Schannel을 구성 하는 방법**

Windows Server 2012의 Schannel SSP 아키텍처는 기본적으로 위에 설명 된 대로 신뢰할 수 있는 발급자 목록을 관리 하는 저장소를 사용 합니다. 인증서를 관리하는 데 PowerShell 공급자의 기존 인증서 관리 commandlet 및 Certutil 같은 명령줄 도구를 계속 사용할 수 있습니다.

PowerShell 공급자를 사용하여 인증서를 관리하는 방법에 대한 자세한 내용은 [Windows의 AD CS 관리 Cmdlet](https://technet.microsoft.com/library/hh848365(v=wps.620).aspx)을 참조하세요.

인증서 유틸리티를 사용하여 인증서를 관리하는 방법에 대한 자세한 내용은 [certutil.exe](https://technet.microsoft.com/library/cc732443.aspx)를 참조하세요.

응용 프로그램 정의 저장소를 포함하여 Schannel 자격 증명에 대해 정의된 데이터에 대한 자세한 내용은 [SCHANNEL_CRED 구조(Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379810(v=vs.85).aspx)를 참조하세요.

**신뢰 모드의 기본값**

Schannel 공급자에서는 세 가지 클라이언트 인증 신뢰 모드를 지원합니다. 신뢰 모드는 클라이언트의 인증서 체인에 대 한 유효성 검사를 수행 하는 방법을 제어 하며, HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\Schannel.의 "ClientAuthTrustMode" REG_DWORD에서 제어 하는 시스템 차원 설정입니다.

|값|신뢰 모드|설명|
|-----|-------|--------|
|0|컴퓨터 신뢰(기본값)|클라이언트 인증서가 신뢰할 수 있는 발급자 목록의 인증서에서 발급되어야 합니다.|
|1|단독 루트 신뢰|클라이언트 인증서가 호출자가 지정한 신뢰할 수 있는 발급자 저장소에 포함된 루트 인증서에 연결되어야 합니다. 또한 인증서가 신뢰할 수 있는 발급자 목록의 발급자에 의해 발급되어야 합니다.|
|2|단독 CA 신뢰|클라이언트 인증서가 호출자가 지정한 신뢰할 수 있는 발급자 저장소의 루트 인증서 또는 중간 CA 인증서에 연결되어야 합니다.|

신뢰할 수 있는 발급자 구성 문제로 인한 인증 실패에 대한 자세한 내용은 기술 자료 문서 [280256](https://support.microsoft.com/kb/2802568)을 참조하세요.

### <a name="tls-support-for-server-name-indicator-sni-extensions"></a><a name="BKMK_SNI"></a>SNI (서버 이름 표시기) 확장을 위한 TLS 지원
SNI(서버 이름 표시기) 기능은 단일 서버에 다수의 가상 이미지가 실행되고 있을 때 서버를 올바르게 식별할 수 있도록 SSL 및 TLS 프로토콜을 확장합니다. 클라이언트 컴퓨터와 서버 간의 통신을 적절히 보호하기 위해 클라이언트 컴퓨터는 서버에서 디지털 인증서를 요청합니다. 이 요청에 대한 응답으로 서버가 인증서를 보내고 나면 클라이언트 컴퓨터가 이를 검사하여 암호화하는 데 사용하고 정상적인 요청-응답 교환을 진행합니다. 하지만 가상 호스팅 시나리오에서 잠재적으로 각각의 개별 인증서를 소유하고 있는 몇몇 도메인이 단일 서버에서 호스팅됩니다. 이 경우 서버는 클라이언트 컴퓨터로 보낼 인증서를 사전에 알 수 있는 방법이 없습니다. SNI를 사용하면 클라이언트 컴퓨터가 프로토콜에서 대상 도메인을 더 일찍 알릴 수 있으므로 서버가 적절한 인증서를 올바르게 선택할 수 있습니다.

**이는 어떤 값을 추가 하나요?**

다음과 같은 추가 기능을 이용할 수 있습니다.

-   단일 IP와 포트의 조합에서 여러 SSL 웹 사이트를 호스팅할 수 있음

-   여러 SSL 웹 사이트가 단일 웹 서버에서 호스팅될 때 메모리 사용량 절감

-   더 많은 사용자가 SSL 웹 사이트에 동시 연결할 수 있음

-   클라이언트 인증 프로세스가 진행되는 동안 올바른 인증서를 선택할 수 있도록 컴퓨터 인터페이스를 통해 최종 사용자에게 힌트를 제공할 수 있음

**작동 방식**

Schannel SSP는 클라이언트에 허용된 클라이언트 연결 상태의 메모리 내 캐시를 유지 관리합니다. 이에 따라 클라이언트 컴퓨터는 SSL 서버에 대한 후속 방문 시 완전한 SSL 핸드셰이크 없이도 SSL 서버에 곧바로 다시 연결할 수 있습니다.  인증서 관리를 효율적으로 사용 하면 이전 운영 체제 버전에 비해 더 많은 사이트를 단일 Windows Server 2012에 호스트할 수 있습니다.

올바른 인증서를 선택하도록 최종 사용자에게 힌트를 제공하는 믿을 만한 인증서 발급자 이름 목록을 구성할 수 있도록 하여 최종 사용자의 인증서 선택 환경이 개선되었습니다. 이 목록은 그룹 정책을 사용하여 구성할 수 있습니다.

### <a name="datagram-transport-layer-security-dtls"></a><a name="BKMK_DTLS"></a>DTLS (데이터 그램 전송 계층 보안)
DTLS 버전 1.0 프로토콜이 Schannel SSP(Security Support Provider)에 추가되었습니다. DTLS 프로토콜은 데이터그램 프로토콜에 대한 통신 보안을 제공합니다. 이 프로토콜을 통해 클라이언트/서버 애플리케이션은 도청, 변조 또는 메시지 위조를 방지할 수 있도록 설계된 방식으로 통신할 수 있습니다. DTLS 프로토콜은 TLS(전송 계층 보안) 프로토콜에 기반을 두고 이와 동등한 보안 기능을 보장함으로써 IPsec을 사용하거나 사용자 지정 애플리케이션 계층 보안 프로토콜을 설계할 필요성을 줄여줍니다.

**이는 어떤 값을 추가 하나요?**

데이터 그램은 게임 또는 보안 비디오 회의와 같은 스트리밍 미디어에서 일반적입니다. DTLS 프로토콜이 Schannel 공급자에게 추가되어 친숙한 Windows SSPI 모델을 사용해 클라이언트 컴퓨터와 서버 간의 통신을 보호할 수 있습니다. DTLS는 새로운 보안 장치의 발명을 최소화하고 코드 및 인프라를 다시 사용하는 분량을 최대화할 수 있도록 최대한 TLS와 유사하게 설계되었습니다.

**작동 방식**

UDP를 통해 DTLS를 사용 하는 응용 프로그램은 Windows Server 2012 및 Windows 8에서 SSPI 모델을 사용할 수 있습니다. TLS 구성 방법과 마찬가지로, 특정 암호화 모음을 구성에 사용할 수 있습니다. Schannel은 계속해서 CNG 암호화 공급자를 사용하므로 Windows Vista에 도입된 FIPS 140 인증을 활용할 수 있습니다.

### <a name="deprecated-functionality"></a><a name="BKMK_Deprecated"></a>사용 되지 않는 기능
Windows Server 2012 및 Windows 8 용 Schannel SSP에는 더 이상 사용 되지 않는 기능이 없습니다.

## <a name="see-also"></a>참고 항목
-   [사설 클라우드 보안 모델-래퍼 기능](https://social.technet.microsoft.com/wiki/contents/articles/6756.private-cloud-security-model-wrapper-functionality.aspx)



