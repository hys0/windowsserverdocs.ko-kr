---
title: NPS로 처리되는 동시 인증 늘리기
description: 이 항목에서는 Windows Server 2016의 동시 인증이 네트워크 정책 서버를 구성 하는 방법에 지침을 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fd930e34a4adf6c55812385b691df3e3575a4280
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818264"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>NPS로 처리되는 동시 인증 늘리기

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 정책 서버 동시 인증 구성에 대 한 지침은이 항목에서는 사용할 수 있습니다.

네트워크 정책 서버를 설치한 경우 \(NPS\) 도메인 외의 컴퓨터에서 컨트롤러 및 NPS 수신 하는 많은 수의 초당 인증 요청의 수를 늘려 NPS 성능을 향상 시킬 수 있습니다 NPS와 도메인 컨트롤러 간에 허용 되는 동시 인증입니다.

이렇게 하려면 다음 레지스트리 키를 편집 해야 합니다. 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

명명 된 새 값을 추가 **MaxConcurrentApi** 2에서 5 사이의 값을를 할당 합니다. 

>[!CAUTION]
>값을 할당 하는 경우 **MaxConcurrentApi** 너무를 NPS에 도메인 컨트롤러에서 과도 한 로드를 배치할 수 있습니다.

NPS를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.