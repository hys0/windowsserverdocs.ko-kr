---
title: TLS/SSL 개요 (Schannel SSP)
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-tls-ssl
ms.topic: article
ms.assetid: 1b7b0432-1bef-4912-8c9a-8989d47a4da9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/16/2018
ms.openlocfilehash: 0d963116fc9f22482398b38482f0c3c49f4be505
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475520"
---
# <a name="tlsssl-overview-schannel-ssp"></a>TLS/SSL 개요 (Schannel SSP)

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

IT 전문가를 위한이 항목에서는 Schannel SSP (보안 서비스 공급자)를 사용 하는 Windows의 TLS 및 SSL 구현을 소개 합니다. 여기에는 실용적인 응용 프로그램, Microsoft 구현의 변경 내용, 소프트웨어 요구 사항 및 Windows Server 2012 및 Windows 8에 대 한 추가 리소스가 나와 있습니다.

## <a name="description"></a><a name="BKMK_OVER"></a>설명
Schannel은 TLS(전송 계층 보안) 및 SSL(Secure Sockets Layer) 인터넷 표준 인증 프로토콜을 구현한 SSP(Security Support Provider)입니다.

SSPI(Security Support Provider Interface)는 인증을 비롯한 보안 관련 기능을 수행하기 위해 Windows 시스템에서 사용되는 API입니다. SSPI는 Schannel SSP를 비롯 한 여러 Ssp에 대 한 공용 인터페이스로 작동 합니다.

TLS 버전 1.0, 1.1 및 1.2, SSL 버전 2.0 및 3.0 뿐만 아니라 데이터 그램 전송 계층 보안 \( DTLS \) 프로토콜 버전 1.0 및 개인 통신 전송 \( PCT \) 프로토콜은 공개 키 암호화를 기반으로 합니다. Schannel 인증 프로토콜 모음은 이러한 프로토콜을 제공합니다. 모든 Schannel 프로토콜에서는 클라이언트/서버 모델이 사용됩니다.

## <a name="applications"></a><a name="BKMK_APP"></a>애플리케이션
네트워크를 관리할 때의 한 가지 문제는 신뢰할 수 없는 네트워크를 통해 애플리케이션 간에 전송되는 데이터를 보호하는 것입니다. TLS 및 SSL을 사용 하 여 서버와 클라이언트 컴퓨터를 인증 한 다음이 프로토콜을 사용 하 여 인증 된 당사자 간의 메시지를 암호화할 수 있습니다.

예를 들어 다음과 같은 작업에 TLS/SSL을 사용할 수 있습니다.

-   전자 상거래 웹 사이트와의 SSL 보안 트랜잭션
-   인증된 클라이언트의 SSL 보안 웹 사이트 액세스
-   원격 액세스
-   SQL 액세스
-   전자 메일

## <a name="requirements"></a><a name="BKMK_SOFT"></a>요구 사항
TLS 및 SSL 프로토콜은 클라이언트/서버 모델을 사용 하며 공개 키 인프라가 필요한 인증서 인증을 기반으로 합니다.

## <a name="server-manager-information"></a><a name="BKMK_INSTALL"></a>서버 관리자 정보
TLS, SSL 또는 Schannel을 구현 하는 데 필요한 구성 단계는 없습니다.

## <a name="additional-references"></a>추가 참조 ##

-   [Schannel 보안 패키지](https://docs.microsoft.com/windows/desktop/com/schannel)
-   [보안 채널](https://docs.microsoft.com/windows/desktop/SecAuthN/secure-channel)
-   [전송 계층 보안 프로토콜](https://docs.microsoft.com/windows/desktop/SecAuthN/transport-layer-security-protocol)
