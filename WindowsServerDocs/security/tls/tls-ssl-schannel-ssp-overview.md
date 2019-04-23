---
title: TLS/SSL (Schannel SSP) 개요
description: Windows Server 보안
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
ms.date: 05/16/2018
ms.openlocfilehash: a6571e5e06e07fd62ad4cf39bab322b45c90a9f9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848604"
---
# <a name="tlsssl-overview-schannel-ssp"></a>TLS/SSL (Schannel SSP) 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

Microsoft의 구현 및 소프트웨어 요구 사항,이 항목에서는 IT 전문가 도입 Schannel 보안 서비스 공급자 (SSP)를 사용 하 여 실제 응용 프로그램을 설명 하 여 Windows에서 TLS 및 SSL 구현에 대 한 변경 및 Windows Server 2012 및 Windows 8에 대 한 추가 리소스입니다.

## <a name="BKMK_OVER"></a>설명
Schannel은 TLS(전송 계층 보안) 및 SSL(Secure Sockets Layer) 인터넷 표준 인증 프로토콜을 구현한 SSP(Security Support Provider)입니다.

SSPI(Security Support Provider Interface)는 인증을 비롯한 보안 관련 기능을 수행하기 위해 Windows 시스템에서 사용되는 API입니다. SSPI는 Schannel SSP를 포함 하 여 여러 Ssp 공용 인터페이스로 함수

TLS 버전 1.0, 1.1 및 1.2, SSL 버전 2.0 / 3.0, 데이터 그램 전송 계층 보안 뿐만 아니라 \(DTLS\) 프로토콜 버전 1.0 및 개인 통신 전송 \(PCT\) 프로토콜에 기반한 공개 키 암호화 합니다. Schannel 인증 프로토콜 모음은 이러한 프로토콜을 제공합니다. 모든 Schannel 프로토콜에서는 클라이언트/서버 모델이 사용됩니다.

## <a name="BKMK_APP"></a>응용 프로그램
네트워크를 관리할 때 발생하는 한 가지 문제는 신뢰할 수 없는 네트워크의 응용 프로그램 간에 전송되는 데이터를 보호하는 것입니다. 서버와 클라이언트 컴퓨터를 인증 하 고 다음 프로토콜을 사용 하 여 인증된 된 당사자 간의 메시지를 암호화 하려면 TLS 및 SSL을 사용할 수 있습니다.

예를 들어 다음과 같은 작업에 TLS/SSL을 사용할 수 있습니다.

-   전자 상거래 웹 사이트와의 SSL 보안 트랜잭션
-   인증된 클라이언트의 SSL 보안 웹 사이트 액세스
-   원격 액세스
-   SQL 액세스
-   전자 메일

## <a name="BKMK_SOFT"></a>요구 사항
TLS 및 SSL 프로토콜 클라이언트/서버 모델을 사용 및 공개 키 인프라를 해야 하는 인증서 인증을 기반으로 합니다.

## <a name="BKMK_INSTALL"></a>서버 관리자 정보
TLS, SSL 또는 Schannel을 구현 하는 데 필요한 구성 단계가 있습니다.

## <a name="see-also"></a>참조 ##

-   [Schannel 보안 패키지](https://docs.microsoft.com/windows/desktop/com/schannel)
-   [보안 채널](https://docs.microsoft.com/windows/desktop/SecAuthN/secure-channel)
-   [전송 계층 보안 프로토콜](https://docs.microsoft.com/windows/desktop/SecAuthN/transport-layer-security-protocol)
