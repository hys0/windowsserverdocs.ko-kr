---
title: HTTPS 통신에 대 한 HGS 구성
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: de57a4026a33561760ad36fd78d732352b3aa340
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856846"
---
# <a name="configure-hgs-for-https-communications"></a>HTTPS 통신에 대 한 HGS 구성

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

기본적으로, HGS 서버를 초기화할 때 HTTP 전용 통신을 위한 IIS 웹 사이트가 구성 됩니다.
HGS로/에서 전송 되는 모든 중요 한 자료는 항상 메시지 수준 암호화를 사용 하 여 암호화 됩니다. 그러나 더 높은 수준의 보안을 원하는 경우 SSL 인증서를 사용 하 여 HGS를 구성 하 여 HTTPS를 사용 하도록 설정할 수도 있습니다.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

