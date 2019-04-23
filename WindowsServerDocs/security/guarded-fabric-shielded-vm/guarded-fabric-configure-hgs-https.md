---
title: Https 통신을 위해 HGS 구성
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 83529a5bdb4547b9881bb307a8a4cd526552d02c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829004"
---
# <a name="configure-hgs-for-https-communications"></a>HTTPS 통신을 위해 HGS 구성

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

HGS 서버를 초기화 하는 경우 기본적으로 HTTP 전용 통신을 위해 IIS 웹 사이트를 구성 합니다 것입니다.
HGS에서 전송 되는 모든 중요 한 자료는 항상 암호화 메시지 수준 암호화를 사용 하 여 HTTPS를 SSL 인증서를 사용 하 여 HGS를 구성 하 여 또한 설정할 수 있습니다. 더 높은 수준의 보안을 원하는 경우.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

