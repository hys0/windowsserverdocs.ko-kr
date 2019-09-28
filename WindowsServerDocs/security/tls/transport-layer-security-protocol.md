---
title: 전송 계층 보안 프로토콜
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: aca2db3ae5bf424dd0f855d24c1ef771039c8b14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403380"
---
# <a name="transport-layer-security-protocol"></a>전송 계층 보안 프로토콜

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

IT 전문가를 위한이 항목에서는 TLS (Transport Layer Security) 프로토콜의 작동 방식에 대해 설명 하 고 TLS 1.0, TLS 1.1 및 TLS 1.2의 IETF Rfc에 대 한 링크를 제공 합니다.

TLS 및 SSL 프로토콜은 응용 프로그램 프로토콜 계층과 TCP/IP 계층 사이에 있으며,이를 통해 보안을 설정 하 고 전송 계층으로 응용 프로그램 데이터를 보낼 수 있습니다. 응용 프로그램 계층과 전송 계층 간에 프로토콜이 작동 하기 때문에 TLS 및 SSL은 여러 응용 프로그램 계층 프로토콜을 지원할 수 있습니다.

TLS 및 SSL은 일반적으로 TCP를 사용 하는 연결 지향 전송을 사용 하 고 있다고 가정 합니다. 이 프로토콜을 사용 하면 클라이언트 및 서버 응용 프로그램에서 다음과 같은 보안 위험을 감지할 수 있습니다.

-   메시지 변조

-   메시지 가로채기

-   메시지 위조

TLS 및 SSL 프로토콜은 두 계층으로 나눌 수 있습니다. 첫 번째 계층은 응용 프로그램 프로토콜과 핸드셰이크 프로토콜, 변경 암호화 사양 프로토콜 및 경고 프로토콜의 세 가지 핸드셰이킹 프로토콜로 구성 됩니다. 두 번째 계층은 레코드 프로토콜입니다. 다음 이미지는 다양 한 레이어 및 해당 요소를 보여 줍니다.

**TLS 및 SSL 프로토콜 계층**


Schannel SSP는 수정 하지 않고 TLS 및 SSL 프로토콜을 구현 합니다. SSL 프로토콜은 독점적 이지만 인터넷 엔지니어링 작업 Force는 공용 TLS 사양을 생성 합니다. Windows 버전에서 지원 되는 TLS 또는 SSL 버전에 대 한 자세한 내용은 [tls/ssl의 프로토콜 (SCHANNEL SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159(v=vs.85).aspx)을 참조 하세요. 다음 표에는 각 TLS 버전의 사양이 나열 되어 있습니다. 각 사양은 다음에 대 한 정보를 포함 합니다.

-   TLS 레코드 프로토콜

-   TLS 핸드셰이킹 프로토콜: \- 암호화 사양 프로토콜 \- 경고 프로토콜 변경

-   암호화 계산

-   필수 암호 그룹

-   응용 프로그램 데이터 프로토콜

[RFC 5246-TLS (Transport Layer Security) 프로토콜 버전 1.2](http://tools.ietf.org/html/rfc5246)

[RFC 4346-TLS (Transport Layer Security) 프로토콜 버전 1.1](http://tools.ietf.org/html/rfc4346)

[RFC 2246-TLS 프로토콜 버전 1.0](http://tools.ietf.org/html/rfc2246)

## <a name="BKMK_SessionResumption"></a>TLS 세션 다시 시작
Windows Server 2012 r 2에서 도입 된 Schannel SSP는 TLS 세션 재시작의 서버 쪽 부분을 구현 했습니다. Windows 8에서 RFC 5077의 클라이언트 쪽 구현이 추가 되었습니다.

TLS를 서버에 연결 하는 장치는 자주 다시 연결 해야 합니다. Tls 세션을 다시 시작 하면 단순화 된 TLS 핸드셰이크가 수반 되기 때문에 TLS 연결 설정 비용이 줄어듭니다. 이렇게 하면 TLS 서버 그룹이 서로의 TLS 세션을 다시 시작 하도록 허용 하 여 더 많은 다시 시작을 용이 하 게 합니다. 이 수정은 Windows Phone 및 Windows RT 장치를 포함 하 여 RFC 5077을 지 원하는 모든 TLS 클라이언트에 대해 다음과 같은 절감 액을 제공 합니다.

-   서버에서 리소스 사용량 감소

-   대역폭 감소로 인한 클라이언트 연결의 효율성 향상

-   연결의 재개로 인해 TLS 핸드셰이크에 소요 된 시간을 줄였습니다.

상태 비저장 TLS 세션 다시 시작에 대한 자세한 내용은 IETF 문서 [RFC 5077](http://www.ietf.org/rfc/rfc5077)을 참조하세요.

## <a name="BKMK_AppProtocolNego"></a>응용 프로그램 프로토콜 협상
 Windows Server 2012 R2 및 Windows 8.1는 클라이언트 쪽 TLS 응용 프로그램 프로토콜 협상을 허용 하는 지원을 도입 했습니다. 응용 프로그램은 HTTP 2.0 표준 개발의 일부로 프로토콜을 활용할 수 있으며, 사용자는 SPDY 프로토콜을 실행 하는 앱을 사용 하 여 Google 및 Twitter와 같은 온라인 서비스에 액세스할 수 있습니다.

응용 프로그램 프로토콜 협상의 작동 방식에 대 한 자세한 내용은 [TLS (Transport Layer Security) 응용 프로그램 계층 프로토콜 협상 확장 (영문)](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05)을 참조 하세요.

## <a name="BKMK_SNI"></a>서버 이름 표시 확장을 위한 TLS 지원
SNI (서버 이름 표시) 기능은 SSL 및 TLS 프로토콜을 확장 하 여 단일 서버에서 여러 가상 이미지가 실행 될 때 서버를 적절 하 게 식별할 수 있도록 합니다. 가상 호스팅 시나리오에서는 여러 도메인 (각각에 잠재적으로 고유한 인증서가 있는)이 한 서버에서 호스팅됩니다. 이 경우 서버는 클라이언트에 보낼 인증서를 사전에 알 수 없습니다. SNI를 사용 하면 클라이언트가 프로토콜의 이전에 대상 도메인에 알릴 수 있으며,이를 통해 서버에서 적절 한 인증서를 올바르게 선택할 수 있습니다.

다음과 같은 추가 기능을 이용할 수 있습니다.

-   단일 인터넷 프로토콜 및 포트 조합에서 여러 SSL 웹 사이트를 호스트할 수 있습니다.

-   여러 SSL 웹 사이트가 단일 웹 서버에서 호스팅될 때 메모리 사용량 절감

-   더 많은 사용자가 SSL 웹 사이트에 동시에 연결할 수 있습니다.



