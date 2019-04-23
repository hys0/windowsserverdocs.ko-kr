---
title: 전송 계층 보안 프로토콜
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de510bb0-a9f6-4bbe-8f8a-8dd7473bbae8
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: 77e3ee9d89bff7ab6e95ea47ffa141e6e1004ba4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853024"
---
# <a name="transport-layer-security-protocol"></a>전송 계층 보안 프로토콜

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

IT 전문가 위한이 항목에서는 전송 계층 보안 (TLS) 프로토콜을 작동 및 TLS 1.0, TLS 1.1 및 TLS 1.2에 대 한 링크는 IETF Rfc를 제공 하는 방법을 설명 합니다.

TLS (및 SSL) 프로토콜 사이 있는 응용 프로그램 프로토콜 계층 및 TCP/IP 계층에서 보안 및 전송 계층으로 응용 프로그램 데이터를 보낼 수 있습니다. 응용 프로그램 계층 사이의 전송 계층 프로토콜이 작동 하므로 TLS 및 SSL 여러 응용 프로그램 계층 프로토콜을 지원할 수 있습니다.

TLS 및 SSL 연결 지향 전송에 일반적으로 TCP를 사용 중인 것으로 가정 합니다. 프로토콜을 사용 하면 다음과 같은 보안 위험을 감지 클라이언트 및 서버 응용 프로그램:

-   메시지 변조

-   메시지 인터 셉 션

-   메시지 위조

TLS 및 SSL 프로토콜은 두 레이어로 나눌 수 있습니다. 첫 번째 계층 응용 프로그램 프로토콜 및 세 가지 핸드셰이킹 프로토콜 이루어져: handshake 프로토콜, 변경 암호 사양 프로토콜 및 경고 프로토콜입니다. 두 번째 계층 레코드 프로토콜입니다. 다음 이미지는 다양 한 계층 및 해당 요소를 보여 줍니다.

**TLS 및 SSL 프로토콜 계층**


Schannel SSP는 수정 없이 TLS 및 SSL 프로토콜을 구현합니다. SSL 프로토콜을 소유, 이지만 Internet Engineering Task Force 공용 TLS 사양을 생성 합니다. 버전 Windows 버전에서 지원 되는 TLS 또는 SSL에 대 한 내용은 [TLS/SSL (Schannel SSP)의 프로토콜](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx)합니다. 다음 표에서 각 TLS 버전에 대 한 사양을 나열합니다. 각 사양에 대 한 정보가 들어 있습니다.

-   TLS 레코드 프로토콜

-   TLS 핸드셰이킹 프로토콜: \- 암호화 사양 프로토콜을 변경 \- 프로토콜 경고

-   암호화 계산

-   필수 암호 그룹

-   응용 프로그램 데이터 프로토콜

[RFC 5246-Transport Layer Security (TLS) 프로토콜 버전 1.2](http://tools.ietf.org/html/rfc5246)

[RFC 4346-Transport Layer Security (TLS) 프로토콜 버전 1.1](http://tools.ietf.org/html/rfc4346)

[RFC 2246-TLS 프로토콜 버전 1.0](http://tools.ietf.org/html/rfc2246)

## <a name="BKMK_SessionResumption"></a>TLS 세션 다시 시작
Windows Server 2012 R2에 도입 된, Schannel SSP TLS 세션 재시작의 서버 쪽 부분을 구현 합니다. Windows 8에서 RFC 5077의 클라이언트 쪽 구현이 추가 되었습니다.

서버에 TLS를 자주 연결 되는 장치 다시 연결 해야 합니다. TLS 세션 재시작 재개는 약식된 TLS 핸드셰이크 반하므로 TLS 연결을 설정 하는 비용을 줄입니다. 이 다른 사용자의 TLS 세션 다시 시작 하려면 TLS 서버 그룹을 허용 하 여 자세한 다시 시작 시도를 용이해 집니다. 이 수정 TLS 지 원하는 클라이언트를 RFC 5077, Windows Phone 및 Windows RT 장치를 포함 하 여 다음 비용 절감을 제공 합니다.

-   서버에서 리소스 사용량 감소

-   대역폭 감소로 인한 클라이언트 연결의 효율성 향상

-   연결 재개로 인해 TLS 핸드셰이크에 소요 된 시간 감소

상태 비저장 TLS 세션 다시 시작에 대한 자세한 내용은 IETF 문서 [RFC 5077](http://www.ietf.org/rfc/rfc5077)을 참조하세요.

## <a name="BKMK_AppProtocolNego"></a>응용 프로그램 프로토콜 협상
 Windows Server 2012 R2 및 Windows 8.1는 클라이언트 쪽 TLS 응용 프로그램 프로토콜 협상을 허용 하는 지원이 추가 되었습니다. 응용 프로그램이 HTTP 2.0 표준 개발의 일부로 프로토콜을 활용 하 고 사용자가 SPDY 프로토콜을 실행 하는 앱을 사용 하 여 Google 및 Twitter와 같은 온라인 서비스에 액세스할 수 있습니다.

응용 프로그램 프로토콜 협상 작동 하는 방법에 대 한 자세한 내용은 [전송 계층 보안 (TLS) 응용 프로그램 계층 프로토콜 협상 확장](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05)합니다.

## <a name="BKMK_SNI"></a>서버 이름 표시 확장을 위한 TLS 지원
서버 이름 표시 (SNI) 기능은 단일 서버에서 많은 수의 가상 이미지를 실행할 때 서버를 올바르게 식별할 수 있도록 SSL 및 TLS 프로토콜을 확장 합니다. 가상 호스팅 시나리오에서는 여러 도메인 (잠재적으로 고유한 자체 인증서를 사용 하 여 각)는 하나 이상의 서버에서 호스트 됩니다. 이 경우 서버에 클라이언트에 보낼 인증서를 미리 알 수 없습니다. SNI 프로토콜의 앞부분에서 대상 도메인을 알리기 위해 클라이언트를 사용 하면 및 이렇게 하면 서버를 올바르게 적절 한 인증서를 선택 합니다.

다음과 같은 추가 기능을 이용할 수 있습니다.

-   단일 인터넷 프로토콜 및 포트 조합에서 여러 SSL 웹 사이트를 호스트할 수 있습니다.

-   여러 SSL 웹 사이트가 단일 웹 서버에서 호스팅될 때 메모리 사용량 절감

-   자세한 사용자가 SSL 웹 사이트에 동시에 연결할 수 있습니다.



