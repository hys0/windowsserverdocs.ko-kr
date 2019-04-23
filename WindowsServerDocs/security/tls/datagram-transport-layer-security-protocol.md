---
title: 데이터그램 전송 계층 보안 프로토콜
description: Windows Server 보안
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
ms.date: 05/16/2018
ms.openlocfilehash: b32ebafff5e41d5c3140f008f6f391852f2f3474
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870794"
---
# <a name="datagram-transport-layer-security-protocol"></a>데이터그램 전송 계층 보안 프로토콜

Windows Server (반기 채널), Windows Server 2016, Windows 10

IT 전문가 위한이 참조 항목에서는 Schannel 보안 지원 공급자 (SSP)의 일부인 데이터 그램 전송 계층 보안 (DTLS) 프로토콜을 설명 합니다.

## <a name="BKMK_DTLS"></a>
DTLS 프로토콜이 Schannel SSP에서 Windows Server 2012 및 Windows 8에 도입 된, 데이터 그램 프로토콜에 대 한 통신 개인 정보를 제공 합니다. 버전은 Windows 버전에서 지원 하는 DTLS에 대 한 내용은 [TLS/SSL (Schannel SSP)의 프로토콜](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx)합니다. 이 프로토콜을 통해 클라이언트 및 서버 응용 프로그램은 도청, 변조 또는 메시지 위조를 방지할 수 있도록 설계된 방식으로 통신할 수 있습니다. DTLS 프로토콜은 TLS(전송 계층 보안) 프로토콜을 기반으로 하고 이와 동등한 보안 기능을 보장함으로써 IPsec을 사용하거나 사용자 지정 응용 프로그램 계층 보안 프로토콜을 설계할 필요성을 줄여줍니다.

데이터 그램은 게임이 나 보안 비디오 회의 등의 미디어 스트리밍에 공통 됩니다. 개발자는 클라이언트와 서버 간 통신을 보호 하는 Windows 인증 보안 지원 공급자 인터페이스 (SSPI) 모델의 컨텍스트 내에서 DTLS 프로토콜을 사용 하도록 응용 프로그램을 개발할 수 있습니다. DTLS 프로토콜은 사용자 데이터 그램 프로토콜 (UDP)을 기반으로 빌드됩니다. DTLS는 새로운 보안 장치의 발명을 최소화 하 고 코드 및 인프라 재사용을 최대화할 최대한 TLS와 유사 하 되도록 설계 되었습니다.

암호 그룹 구성에 사용할 수 있는 TLS에 대 한 구성할 수 있습니다 이러한 뒤에 패턴화 됩니다. RC4 허용 되지 않습니다. Schannel 계속 생성 CNG (Cryptography Next)를 사용 합니다. 이 Windows Vista에 도입 된 FIPS 140 인증을 활용 합니다.

## <a name="see-also"></a>참조

[IETF RFC 4347 데이터 그램 전송 계층 보안](http://tools.ietf.org/html/rfc4347)


