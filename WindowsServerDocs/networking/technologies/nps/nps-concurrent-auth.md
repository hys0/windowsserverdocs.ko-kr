---
title: NPS로 처리되는 동시 인증 늘리기
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버 동시 인증을 구성 하는 방법에 대 한 지침을 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 31dec30ba3c843b78974daa7a1e4ed6893b1ebbd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396433"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>NPS로 처리되는 동시 인증 늘리기

>적용 대상: Windows Server(반기 채널), Windows Server 2016

네트워크 정책 서버 동시 인증을 구성 하는 방법에 대 한 지침은이 항목을 참조 하세요.

도메인 컨트롤러가 아닌 컴퓨터에 네트워크 정책 서버 \(NPS @ no__t-1을 설치한 경우 NPS에서 초당 많은 수의 인증 요청을 수신 하는 경우 동시 수를 늘려서 NPS 성능을 향상 시킬 수 있습니다. NPS와 도메인 컨트롤러 간에 허용 되는 인증입니다.

이렇게 하려면 다음 레지스트리 키를 편집 해야 합니다. 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

**MaxConcurrentApi** 라는 새 값을 추가 하 고 2에서 5 사이의 값을 할당 합니다. 

>[!CAUTION]
>너무 높은 **MaxConcurrentApi** 에 값을 할당 하면 NPS는 도메인 컨트롤러에 과도 한 부하를 놓을 수 있습니다.

NPS를 관리 하는 방법에 대 한 자세한 내용은 [네트워크 정책 서버 관리](nps-manage-top.md)를 참조 하세요.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.