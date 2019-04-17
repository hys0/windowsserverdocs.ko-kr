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
ms.assetid: 1b7b0432-1bef-4912-8c9a-8989d47a4da9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: afd0b70264dba1e720f95e40d3d201c2c5bf1c64
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="tls---ssl-schannel-ssp-overview"></a>TLS-개요 SSL (Schannel SSP)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목에서는 Schannel 보안 서비스 공급자 (SSP)를 사용 하 여 실제 응용 프로그램에 Microsoft의 구현 및 소프트웨어 요구 사항 외 추가 리소스 변경 사항을 Windows 8 및 Windows Server 2012에 대 한 설명 하 여 Windows의 TLS/SSL 구현을 도입 되었습니다.

**Did you mean:**

-   [Schannel 보안 패키지](https://msdn.microsoft.com/library/ms678421.aspx)

-   [보안 채널](https://msdn.microsoft.com/library/windows/desktop/aa380123.aspx)

-   [Transport Layer Security 프로토콜](https://msdn.microsoft.com/library/windows/desktop/aa380516.aspx)

## <a name="BKMK_OVER"></a>TLS\SSL \(Schannel\) 설명
Schannel 주소 \(SSL\) 및 Transport Layer Security \(TLS\) 구현 하는 보안 지원 공급자 \(SSP\)는 인터넷 프로토콜 표준 인증 합니다.

보안 지원 공급자 인터페이스 \(SSPI\)는 API Windows 시스템 security\ 관련 기능 인증 등을 수행 하는 데 사용 합니다. 일반적인 인터페이스 Schannel SSP 포함 하 여 여러 보안 지원 공급자 \(SSPs\)를 SSPI 기능을

1.0 민 1.1, 1.2 주소 \(SSL\) 프로토콜 버전 2.0 및 데이터 그램 Transport Layer Security \(DTLS\) 1.0, 버전 및 개인 커뮤니케이션 전송 3.0 \(PCT\) 프로토콜 Transport Layer Security \(TLS\) 프로토콜 버전 키 공개 암호화를 기반으로 합니다. 보안 채널 \(Schannel\) 인증 프로토콜 제품군 이러한 프로토콜을 제공합니다. 모든 Schannel 프로토콜 client\/서버 모델을 사용 합니다.

## <a name="BKMK_APP"></a>실용적인 응용 프로그램
네트워크를 관리 하는 경우 한 가지 문제는 응용 프로그램 신뢰할 수 없는 네트워크에서 간에 전송 되는 데이터를 보안이 합니다. TLS\SSL 컴퓨터 클라이언트 및 서버 인증을 다음 프로토콜 인증된 당사자 간에 메시지 암호화를 사용 하 여 사용할 수 있습니다.

예를 들어, TLS\SSL에 사용할 수 있습니다.

-   거래는 e\ 상거래 웹 사이트와 SSL\ 보안

-   인증 된 클라이언트는 SSL\ 보안 웹 사이트에 대 한 액세스

-   원격 액세스

-   SQL 액세스

-   E\ 메일

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
TLS\SSL 프로토콜 클라이언트 \ 서버 모델을 사용 하 고 공개 키 인프라 필요한 인증서 인증을 기반으로 합니다.

## <a name="BKMK_INSTALL"></a>서버 관리자 정보
구성 단계가 TLS, SSL 또는 Schannel 구현 하는 데 필요한 합니다.

