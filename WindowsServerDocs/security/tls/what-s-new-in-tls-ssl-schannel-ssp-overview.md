---
title: "TLS-개요 SSL (Schannel SSP)"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8836345-16bb-4dcc-8d2b-2b9b687456a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: b846ed54a1f7c8ef7a85ea9f836ffa75d0036ae6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="overview-of-tls---ssl-schannel-ssp"></a>개요 tls-SSL (Schannel SSP)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목 기능에 Schannel 보안 지원 SSP, Windows Server 2012 R2, Windows Server 2012, Windows 8.1 및 Windows 8 (TLS (Transport Layer Security)는 소켓 SSL (Secure Layer), 및 데이터 그램 Transport Layer Security (DTLS) 인증 프로토콜을 포함 하 여 변경 내용을 설명 합니다.

Schannel는 보안 지원 SSP 표준 인증 SSL, TLS 및 DTLS 인터넷 프로토콜을 구현 하는입니다. 보안 지원 공급자 Interface (SSPI)은 API Windows 시스템 인증을 포함 하 여 보안 관련 기능을 수행 하는 데 사용 합니다. SSPI는 Schannel SSP 포함 하 여 여러 보안 지원 (규칙이) 공급자에 게 일반 인터페이스 같은 기능을

For more information about Microsoft's implementation of TLS and SSL in the Schannel SSP, see the [TLS/SSL Technical Reference (2003)](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx).


##<a name="tlsssl-schannel-ssp-features"></a>TLS/SSL (Schannel SSP) 기능
다음에 Schannel SSP TLS의 기능을 설명

### <a name="tls-session-resumption"></a>TLS 세션 다시 시작
신뢰할 수 없는 네트워크에서 응용 프로그램 사이 전송 된 데이터를 보호 하는 Transport Layer Security TLS () 프로토콜 Schannel 보안 지원 공급자의 구성 요소로 사용 됩니다. TLS/SSL 서버와 클라이언트 컴퓨터 인증 하 고 메시지 인증된 당사자 간에 암호화도 사용할 수 있습니다.

디바이스 자주 TLS 서버에 연결 하는 세션 만료 인해 다시 연결 해야 합니다. Windows 8.1 및 Windows Server 2012 r 2에는 이제 RFC 5077 (TLS 서버 쪽 상태를 않고도 재시작 세션)를 지원합니다. 이 수정 된 Windows Phone 및 Windows RT 디바이스를 제공합니다.

-   서버에서 감소 리소스 사용

-   감소 대역폭을 효율성 클라이언트 연결 개선

-   연결 resumptions 인해 TLS 핸드셰이크에 사용 시간을 감소 합니다.

> [!NOTE]
> Windows 8에서 RFC 5077 클라이언트 측 구현 추가 되었습니다.

비저장 TLS 세션 다시 시작에 대 한 정보를 IETF 문서를 참조 하세요. [RFC 5077 합니다.](http://www.ietf.org/rfc/rfc5077)

### <a name="application-protocol-negotiation"></a>응용 프로그램 프로토콜 협상
 Windows 8.1 및 Windows Server 2012 r 2 지원 클라이언트 측 TLS 응용 프로그램 프로토콜 협상 응용 프로그램 프로토콜 HTTP 2.0 표준 과정의 일환으로 활용 하 고 사용자가 Google 이나 Twitter와 같은 온라인 서비스에 액세스할 수 있도록 SPDY 프로토콜을 실행 하는 앱을 사용 합니다.

**작동 방식**

클라이언트 및 서버 응용 프로그램 지원 되는 응용 프로그램 프로토콜 Id, 기본 설정의 내림차순에서 목록이 제공 하 여 응용 프로그램 프로토콜 협상 확장을 사용 합니다. TLS 클라이언트 목록이 프로토콜 클라이언트에서 지 원하는 응용 프로그램 Layer 프로토콜 협상 (ALPN) 확장 ClientHello 메시지에 포함 하 여 응용 프로그램 프로토콜 협상 원하는 것을 나타냅니다.

TLS 클라이언트는 서버에 요청을를 TLS 서버 클라이언트도 지원 하는 가장 기본 응용 프로그램 프로토콜에 대 한 지원 되는 프로토콜 목록을 읽습니다. 이러한 프로토콜 발견 되 면 서버 및 선택한 프로토콜 id 응답 핸드셰이크 평소 대로 계속 합니다. 일반적인 응용 프로그램 프로토콜 없는 경우 핸드셰이크 심각한 오류 경고를 보냅니다.

### <a name="BKMK_TrustedIssuers"></a>클라이언트 인증을 위해 신뢰할 수 있는 발급자 관리
인증 클라이언트 컴퓨터의 SSL 또는 TLS을 사용 하 여 필요한 경우 신뢰할 수 있는 인증 발급자 목록이 보내려면 서버를 구성할 수 있습니다. 이 목록은 서버를 신뢰 하는 인증서 발급자 한 포함 이며 대 한 힌트를 선택 하는 클라이언트 인증서에 대 한는 여러 인증서 클라이언트 컴퓨터를 수 있습니다. 또한 클라이언트 컴퓨터 서버에 전송 인증서 체인 구성 된 신뢰할 수 있는 발급자 목록과 비교 유효성 검사 해야 합니다.

Windows Server 2012 및 Windows 8 전에 응용 프로그램 또는 프로세스 Schannel SSP (HTTP.sys 및 IIS 포함)를 사용 하는 클라이언트 인증 인증서 신뢰할 목록 (CTL)을 통해 지원 신뢰할 수 있는 발급자 목록을 제공할 수 있습니다.

Windows Server 2012 및 Windows 8을 변경한 기본 인증 프로세스를:

-   신뢰할 수 있는 발행인이 CTL 기반 목록 관리 더 이상 지원 합니다.

-   신뢰할 수 있는 발행인이 목록 기본적으로 보낼 수 있는 동작 꺼져: SendTrustedIssuerList 레지스트리 키 기본값은 이제 0 (기본적으로 꺼져) 1 대신 합니다.

-   이전 버전의 Windows 운영 체제에 호환성 그대로 유지 됩니다.

**어떤 값이 추가 되나요?**

Windows Server 2012 부터는 신뢰 목록의 사용으로 바뀌었습니다 인증서 스토어 기반 구현 합니다. 따라서 certutil.exe 같은 명령줄 도구 뿐만 아니라 PowerShell 공급자의 기존 인증서 관리 commandlets 통해 보다 친숙 한 효율성 수 있습니다.

Schannel SSP (16 KB)를 지원 하는지 신뢰할 수 있는 인증 기관 목록의 최대 크기는 Windows Server 2012에서 Windows Server 2008 R2 동일 하 게 있지만 관련된 인증서 메시지에 포함 되지 않은 되도록 새 전용된 인증서를 인증 발급자 클라이언트에 대 한 저장 합니다.

**어떻게 작동 하나요?**

Windows Server 2012에서 신뢰할 수 있는 발급자 목록을 구성 인증서 저장소;를 사용 하 여 기본 글로벌 컴퓨터 인증서 스토어 및 인 사이트 마다 선택적 합니다. 다음과 같이 목록의 원본이 결정 됩니다.

-   원본으로 사용할 수 됩니다 사이트에 대해 구성 특정 자격 증명 스토어 경우

-   인증서 응용 프로그램 정의 스토어에 있는 경우 다음 Schannel 검사는 **클라이언트 인증 발급자** 로컬 컴퓨터에 저장 하 고 인증서 있는 경우 해당 스토어를 사용 하 여 원본으로 합니다. 인증서 하거나 스토어에서 발견 되 면 루트 신뢰할 수 있는 스토어 검사 됩니다.

-   Schannel 공급자가 사용 글로벌 또는 로컬 스토어 인증서를 포함 되어 있는 **신뢰할 수 있는 루트 Certifictation 기관** 신뢰할 수 있는 발급자 목록의 원본으로 저장 됩니다. (Windows Server 2008 r 2에 대 한 문제입니다.)

하는 경우는 **신뢰할 수 있는 Certifictation 기관** 데 사용 된 저장소에 루트 (자체 서명), 인증 기관 발행인이 인증서의 조합, 캐나다 발행인이 인증서만 서버에 기본적으로 전송 됩니다.

**신뢰할 수 있는 발급자에 대 한 인증서 저장소를 사용 하 여 Schannel 구성 하는 방법**

Schannel SSP 아키텍처 Windows Server 2012에서 기본적으로를 사용할지 위에서 설명한 대로 스토어 발급자 신뢰할 수 있는 목록을 관리할 수 있습니다. 인증서를 관리 하려면 Certutil 같은 명령줄 도구 뿐만 아니라 PowerShell 공급자의 기존 인증서 관리 commandlets도 사용할 수 있습니다.

For information about managing certificates using the PowerShell provider, see [AD CS Administration Cmdlets in Windows](https://technet.microsoft.com/library/hh848365(v=wps.620).aspx).

For information about managing certificates using the certificate utility, see [certutil.exe](https://technet.microsoft.com/library/cc732443.aspx).

For information about what data, including the application-defined store, is defined for an Schannel credential, see [SCHANNEL_CRED structure (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379810(v=vs.85).aspx).

**신뢰 모드에 대 한 기본값**

다음과 같이 세 가지 클라이언트 인증 신뢰 모드가 Schannel 공급자가 지원 됩니다. The trust mode controls how validation of the client's certificate chain is performed and is a system-wide setting controlled by the REG_DWORD "ClientAuthTrustMode" under HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\Schannel.

|값|신뢰 모드|설명|
|-----|-------|--------|
|0|컴퓨터 보안 (기본)|클라이언트 인증서 신뢰할 수 있는 발급자 목록의 인증서에서 발급가 필요 합니다.|
|1|단독 루트 보안|클라이언트 인증서 체인 신뢰할 수 있는 발행인이 발신자 지정 된 저장소에 포함 된 루트 인증서에는 해야 합니다. 인증서는 신뢰할 수 있는 발급자 목록에서 발행인이에서 발급도 해야|
|2|캘리포니아 단독 보안|중간 된 인증서 또는 발신자 지정에서 루트 인증서에 클라이언트 인증서 체인 발행인이 스토어 신뢰할 수 있는 필요 합니다.|

For information about authentication failures due to trusted issuers configuration issues, see Knowledge Base article [280256](https://support.microsoft.com/kb/2802568).

### <a name="BKMK_SNI"></a>서버 이름 표시기 (SNI) 확장 TLS 지원
서버 이름 표시 기능 많은 가상 이미지 단일 서버에서 실행 중인 경우 서버를 식별할 수 있게 적절 한 수 있도록 SSL와 TLS 프로토콜을 확장 합니다. 제대로 클라이언트 컴퓨터와 서버 간 통신을 보호 하기 위해 클라이언트 컴퓨터 서버에서 디지털 인증서를 요청 합니다. 요청에 응답 서버를 인증서 보냅니다 후 클라이언트 컴퓨터 검사할 통신을 암호화를 사용 하 여 프로세스를 진행 하 일반 요청 응답 exchange 합니다. 그러나 가상 호스팅 시나리오 각각 자체 잠재적으로 고유한 인증서를 여러 개의 도메인 한 서버 호스트 됩니다. 이 경우에 서버에 클라이언트 컴퓨터에 보낼 수 있는 인증서 미리 알 수 없습니다. SNI 하면 프로토콜을 앞부분 대상 도메인 알리는 클라이언트 컴퓨터 및 적절 한 인증서를 올바르게 서버가를 통해 합니다.

**어떤 값이 추가 되나요?**

이 추가 기능은 다음과 같습니다.

-   호스트 IP 단일 및 포트에서 여러 SSL 웹 사이트 수 있습니다.

-   여러 SSL 웹 사이트 단일 웹 서버에서 호스트 되는 경우 메모리 사용량을 줄일

-   더 많은 사용자가 동시에 내 SSL 웹 사이트에 연결할 수 있습니다.

-   클라이언트 인증 프로세스 중에 올바른 인증서 선택 하기 위한 힌트 컴퓨터 인터페이스를 통해 최종 사용자에 게 제공할 수 있도록 합니다.

**작동 방식**

Schannel SSP는 메모리 캐시 허용 클라이언트에 대 한 클라이언트 연결 된 상태를 유지 합니다. 이렇게 하면 다음에 방문할 전체 SSL 핸드셰이크 적용 없이 SSL 서버에 신속 하 게 다시 연결 하는 클라이언트 컴퓨터 있습니다.  인증서 관리가 효율적으로 사용 이전 운영 체제 버전을 비교는 하나의 Windows Server 2012에서 호스트 하는 더 많은 사이트를 허용 합니다.

최종 사용자 선택 하는 것에 대 한 힌트를 제공 하는 예상 인증서 발행인이 이름 목록을 생성 하 여 최종 사용자가 인증서 선택 향상 되었습니다. 이 목록은 그룹 정책을 사용 하 여 구성할 수 있습니다.

### <a name="BKMK_DTLS"></a>데이터 그램 Transport Layer Security (DTLS)
DTLS 1.0 버전 프로토콜 Schannel 보안 지원 공급자에 게 추가 되었습니다. DTLS 프로토콜 통신 데이터 그램 프로토콜에 대 한 개인 정보 보호를 제공합니다. 프로토콜은 클라이언트/서버를 응용 프로그램이 도청을, 변조 또는 메시지 위조 하지 못하도록 설계 된 하는 방식에서 통신할 수 있습니다. DTLS 프로토콜 Transport Layer Security TLS () 프로토콜에 따라와 동일한 보안 보장 IPsec 사용을 줄이기 또는 사용자 지정 응용 프로그램 layer security 프로토콜 디자인을 제공 합니다.

**어떤 값이 추가 되나요?**

데이터 그램 스트리밍 미디어 게임 또는 보안 비디오 회의 등의 일반적인 됩니다. DTLS 프로토콜 Schannel 공급자에 게 추가 보안 컴퓨터 클라이언트 및 서버 간 통신에 친숙 한 Windows SSPI 모델을 사용할 수가 있습니다. DTLS은 가능한 한 새로운 보안 발명 최소화 하 고 코드 및 인프라 다시 사용할 수 있도록 금액을 최대화 하로 tls 유사한 되도록 설계 되어 신중 하 게 됩니다.

**작동 방식**

응용 프로그램을 통해 UDP DTLS를 사용 하는 Windows 8 및 Windows Server 2012에서 SSPI 모델을 사용할 수 있습니다. 구성 유사한 TLS 구성 하는 방법에 대 한 특정 암호 그룹 사용할 수 있습니다. Schannel은 Windows Vista에서 도입 된 FIPS 140 인증 이용 CNG 암호화 공급자를 사용 하 여 계속 합니다.

### <a name="BKMK_Deprecated"></a>사용 하지 않는 기능
Windows 8 및 Windows Server 2012에 대 한 Schannel SSP에는 사용 하지 않는 기능 또는 기능 없습니다.

## <a name="see-also"></a>참조 하십시오
-   [개인 클라우드 보안 모델 래퍼 기능](https://social.technet.microsoft.com/wiki/contents/articles/6756.private-cloud-security-model-wrapper-functionality.aspx)



