---
title: "데이터 그램 Transport Layer Security 프로토콜"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57b8873a-ad9c-4f2c-93e0-a2af352c6965
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 31c1cf1f3218c0511a4407b560be30d0c6f86233
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# 데이터 그램 Transport Layer Security 프로토콜

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 용 참조 여기서의는 Schannel 보안 지원 SSP 참가 하는 데이터 그램 Transport Layer Security (DTLS) 프로토콜에 설명 합니다.

## <a name="BKMK_DTLS"></a>
Windows 8 및 Windows Server 2012에서 Schannel SSP에 소개 된, DTLS 프로토콜 통신 데이터 그램 프로토콜에 대 한 개인 정보 보호를 제공 합니다. Windows 버전에서는 버전은 지원 어떤 DTLS에 대 한 내용은 [TLS/SSL (Schannel SSP)에서 프로토콜](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx)합니다. 프로토콜은 클라이언트 및 서버 응용 프로그램이 도청을, 변조, 또는 메시지 위조 하지 못하도록 설계 된 하는 방식에서 통신할 수 있습니다. DTLS 프로토콜 Transport Layer Security TLS () 프로토콜을 기반으로 하며 보장 동일한 보안 IPsec 사용을 줄이기 또는 사용자 지정 응용 프로그램 layer security 프로토콜 디자인을 제공 합니다.

데이터 그램 스트리밍 미디어 게임 또는 보안 비디오 회의 등의 일반적인 됩니다. 개발자 보안 클라이언트 및 서버 간 통신을 위해 Windows 인증 보안 공급자 SSPI (지원 인터페이스) 모델의 컨텍스트에서 DTLS 프로토콜을 사용 하도록 응용 프로그램을 개발할 수 있습니다. DTLS 프로토콜 사용자 데이터 그램 Protocol (UDP) 위에 만들어집니다. DTLS은 새 보안 발명 최소화 하 고 최대화 코드 및 인프라 다시 사용할 수 있도록 금액을 최대한 tls 유사한 되도록 설계 되어 있습니다.

구성에 맞게 사용할 수 있는 암호 그룹 tls 구성할 수 있는 있고 됩니다. R c 4 허용 되지 않습니다. Schannel Cryptography Next Generation (CNG)를 사용 하 여 계속 합니다. 이 Windows Vista에서 도입 된 FIPS 140 인증 활용 합니다.

## 참조 하십시오

[IETF RFC 4347 데이터 그램 Transport Layer Security](http://tools.ietf.org/html/rfc4347)


