---
title: Https 통신에 대 한 HGS 구성
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f0cbf6a6dc1970499758a6a48bfaadb95c464ec1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403681"
---
# <a name="configure-hgs-for-https-communications"></a>HTTPS 통신에 대 한 HGS 구성

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

기본적으로, HGS 서버를 초기화할 때 HTTP 전용 통신을 위한 IIS 웹 사이트가 구성 됩니다.
HGS로/에서 전송 되는 모든 중요 한 자료는 항상 메시지 수준 암호화를 사용 하 여 암호화 됩니다. 그러나 더 높은 수준의 보안을 원하는 경우 SSL 인증서를 사용 하 여 HGS를 구성 하 여 HTTPS를 사용 하도록 설정할 수도 있습니다.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)] 

