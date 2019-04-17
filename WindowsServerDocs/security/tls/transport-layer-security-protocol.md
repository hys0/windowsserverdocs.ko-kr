---
title: "Transport Layer Security 프로토콜"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de510bb0-a9f6-4bbe-8f8a-8dd7473bbae8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 94c81a79e5f3fd8fc22eafde3de8bd3d0bdd73f0
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# Transport Layer Security 프로토콜

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목에서는 Transport Layer Security TLS () 프로토콜 작동 하 고 TLS 1.0 TLS 1.1, 1.2 TLS IETF rfc 링크를 제공 하는 방법을 설명 합니다.

TLS (및 SSL) 프로토콜은 응용 프로그램 프로토콜 계층 사이의 TCP/IP 계층, 보안 및 응용 프로그램 데이터 transport layer를 보낼 수 있습니다. 응용 프로그램 계층 transport layer 사이의 프로토콜 작동 하기 때문에 TLS와 SSL 여러 응용 프로그램 layer 프로토콜을 지원할 수 있습니다.

TLS와 SSL 가정 사용 중인 연결 향하는 전송, 일반적으로 TCP 합니다. 프로토콜은 클라이언트 및 서버 검색할 응용 프로그램을을 다음 보안 위험이 수 있습니다.

-   메시지 위조

-   메시지 가로채기

-   메시지 위조

2 계층으로 TLS 및 SSL 프로토콜 나눌 수 있습니다. 첫 번째 layer 응용 프로그램 프로토콜 및 세 가지 핸드셰이킹 프로토콜 구성: 경우 흐름 제어 프로토콜, 변경 암호화 사양 프로토콜 및 경고 프로토콜 합니다. 두 번째 layer 기록 프로토콜입니다. 다음 이미지에는 다양 한 계층 및 요소 보여 줍니다.

**프로토콜 계층 TLS 및 SSL**


Schannel SSP 수정 하지 않고 TLS와 SSL 프로토콜을 구현 합니다. SSL 프로토콜 독점, 이지만 인터넷 엔지니어링 작업 힘 공개 TLS 사양 생성 합니다. Windows 버전에서는 버전은 지원 어떤 TLS 또는 SSL에 대 한 정보를 참조 하세요. [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx)합니다. 다음 표에서 각 TLS 버전에 대 한 사양을 합니다. 각 설정에 대 한 정보가 들어 있습니다.

-   TLS 녹화 프로토콜

-   TLS 핸드셰이킹 프로토콜: \-변경 암호화 사양 프로토콜 \-프로토콜 알림

-   암호화 계산

-   필수 암호 그룹

-   응용 프로그램 데이터 프로토콜

[RFC 5246-Transport Layer Security (TLS) 프로토콜 버전 1.2](http://tools.ietf.org/html/rfc5246)

[RFC 4346-Transport Layer Security (TLS) 프로토콜 버전 1.1](http://tools.ietf.org/html/rfc4346)

[RFC 2246-1.0 TLS 프로토콜 버전](http://tools.ietf.org/html/rfc2246)

## <a name="BKMK_SessionResumption"></a>TLS 세션 다시 시작
Windows Server 2012 r 2에 소개 된, Schannel SSP TLS 세션 재개 서버 쪽 부분이 구현 했습니다. Windows 8에서 RFC 5077 클라이언트 측 구현 추가 되었습니다.

종종 TLS 서버에 연결 하는 디바이스를 다시 연결 해야 합니다. 세션 재시작 TLS 재개 약어 TLS 핸드셰이크 하므로 TLS 연결을 설정 하는 비용을 줄일 수 있습니다. 이 쉽게 TLS 서버를 다른 사용자의 TLS 세션 다시 시작 하려면 그룹 수 있도록 하 여 더 많은 재개 시도 수 있습니다. 이 수정 사항을 지 원하는 Windows Phone 및 Windows RT 디바이스를 포함 하 여 RFC 5077 TLS 클라이언트에 대 한 다음 절약을 제공 합니다.

-   서버에서 감소 리소스 사용

-   감소 대역폭을 효율성 클라이언트 연결 개선

-   연결 resumptions 인해 TLS 핸드셰이크에 사용 시간 감소

비저장 TLS 세션 다시 시작에 대 한 정보를 IETF 문서를 참조 하세요. [RFC 5077 합니다.](http://www.ietf.org/rfc/rfc5077)

## <a name="BKMK_AppProtocolNego"></a>응용 프로그램 프로토콜 협상
 Windows Server 2012 r 2와 클라이언트 측 TLS 응용 프로그램 프로토콜 협상 수 있도록 해 주는 Windows 8.1 도입 지원 합니다. 응용 프로그램 프로토콜 HTTP 2.0 표준 과정의 일환으로 활용할 수 및 사용자가 SPDY 프로토콜을 실행 하는 앱을 사용 하 여 Google 이나 Twitter와 같은 온라인 서비스에 액세스할 수 있습니다.

응용 프로그램 프로토콜 협상 작동 하는 방법에 대 한 정보를 참조 하세요. [Transport Layer Security TLS () 응용 프로그램 프로토콜 협상 확장 계층](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05)합니다.

## <a name="BKMK_SNI"></a>서버 이름 표시 확장에 대 한 지원이 TLS
서버 이름 표시 (SNI) 기능 많은 가상 이미지 단일 서버에서 실행 중인 경우 서버를 식별할 수 있게 적절 한 수 있도록 SSL와 TLS 프로토콜을 확장 합니다. 가상 호스팅 시나리오에서 몇 가지 도메인 (각각 자체 잠재적으로 고유한 인증서) 서버에 호스트 됩니다. 이 경우에 서버에 클라이언트를 전송 하는 인증서 미리 알 수 없습니다. SNI 클라이언트 프로토콜을 앞부분 대상 도메인 알릴 수 있으며이 적절 한 인증서를 올바르게 서버를 통해 합니다.

이 추가 기능은 다음과 같습니다.

-   포트 조합 단일 인터넷 프로토콜에 여러 SSL 웹 사이트를 개최 수 있습니다.

-   여러 SSL 웹 사이트 단일 웹 서버에서 호스트 되는 경우 메모리 사용량을 줄일

-   더 많은 사용자가 SSL 웹 사이트를 동시에 연결할 수 있습니다.



