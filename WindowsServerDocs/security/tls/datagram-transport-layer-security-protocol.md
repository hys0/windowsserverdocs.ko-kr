---
title: 데이터그램 전송 계층 보안 프로토콜
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-tls-ssl
ms.topic: article
ms.assetid: 57b8873a-ad9c-4f2c-93e0-a2af352c6965
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/16/2018
ms.openlocfilehash: d0c066b063cbfc8def54c2e0d02cbb0eaf7f1d40
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852926"
---
# <a name="datagram-transport-layer-security-protocol"></a>데이터그램 전송 계층 보안 프로토콜

Windows Server(반기 채널), Windows Server 2016, Windows 10

IT 전문가를 위한이 참조 항목에서는 Schannel SSP (Security Support Provider)의 일부인 DTLS (데이터 그램 전송 계층 보안) 프로토콜에 대해 설명 합니다.

## <a name="BKMK_DTLS"></a>
Windows Server 2012 및 Windows 8의 Schannel SSP에서 도입 된 DTLS 프로토콜은 데이터 그램 프로토콜에 대 한 통신 개인 정보를 제공 합니다. Windows 버전에서 지원 되는 DTLS 버전에 대 한 자세한 내용은 [TLS/SSL (SCHANNEL SSP)의 프로토콜](https://msdn.microsoft.com/library/windows/desktop/mt808159(v=vs.85).aspx)을 참조 하세요. 이 프로토콜을 통해 클라이언트 및 서버 애플리케이션은 도청, 변조 또는 메시지 위조를 방지할 수 있도록 설계된 방식으로 통신할 수 있습니다. DTLS 프로토콜은 TLS(전송 계층 보안) 프로토콜을 기반으로 하고 이와 동등한 보안 기능을 보장함으로써 IPsec을 사용하거나 사용자 지정 애플리케이션 계층 보안 프로토콜을 설계할 필요성을 줄여줍니다.

데이터 그램은 게임 또는 보안 비디오 회의와 같은 스트리밍 미디어에서 일반적입니다. 개발자는 Windows 인증 SSPI (Security Support Provider) 모델의 컨텍스트 내에서 DTLS 프로토콜을 사용 하 여 클라이언트와 서버 간의 통신을 보호 하는 응용 프로그램을 개발할 수 있습니다. DTLS 프로토콜은 UDP (사용자 데이터 그램 프로토콜)를 기반으로 빌드됩니다. DTLS는 새 보안 발명 최소화 하 고 코드 및 인프라 재사용의 양을 최대화 하기 위해 가능한 한 TLS와 유사 하 게 설계 되었습니다.

구성에 사용할 수 있는 암호 그룹은 TLS에 대해 구성할 수 있는 것 보다 먼저 패턴화 됩니다. RC4는 허용 되지 않습니다. Schannel은 CNG (Cryptography Next Generation)를 계속 사용 합니다. 이는 Windows Vista에 도입 된 FIPS 140 인증을 활용 합니다.

## <a name="see-also"></a>참고 항목

[IETF RFC 4347 데이터 그램 전송 계층 보안](http://tools.ietf.org/html/rfc4347)


                                        