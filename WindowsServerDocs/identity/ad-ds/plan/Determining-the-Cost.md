---
ms.assetid: e3ea1f67-60d4-4566-b24c-37faa95c3b2a
title: 비용 결정
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0ce7acddbfa9f7536f3d5a190c6968ea0d8cf6b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408876"
---
# <a name="determining-the-cost"></a>비용 결정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

비용 값을 사이트 링크에 할당 하 여 비용이 많이 드는 연결에서 저렴 한 연결을 선호 합니다. 도메인 컨트롤러 로케이터 (DCLocator) 및 분산 파일 시스템 네임 스페이스 (DFSN)와 같은 특정 응용 프로그램 및 서비스는 비용 정보를 사용 하 여 가장 가까운 리소스를 찾을 수 있습니다. 지정 된 도메인의 도메인 컨트롤러가 해당 사이트에 없는 경우 사이트 링크 비용을 사용 하 여 한 사이트의 클라이언트에서 연결 된 도메인 컨트롤러를 확인할 수 있습니다. 클라이언트는 할당 된 순위가 가장 낮은 사이트 링크를 사용 하 여 도메인 컨트롤러에 연결 합니다.  
  
비용 값은 사이트 전체에서 정의 하는 것이 좋습니다. 비용은 일반적으로 링크의 총 대역폭 뿐만 아니라 링크의 가용성, 대기 시간 및 통화 비용에 따라 결정 됩니다.  
  
사이트 링크에 적용할 비용을 결정 하려면 각 사이트 링크에 대 한 연결 속도를 문서화 합니다. 확인 한 연결 속도에 대 한 자세한 내용은 [네트워크 정보 수집](../../ad-ds/plan/Collecting-Network-Information.md) 의 "지리적 위치 및 통신 링크" (DSSTOPO_1) 워크시트를 참조 하십시오.  
  
다음 표에서는 다양 한 유형의 네트워크에 대 한 속도를 보여 줍니다.  
  
|네트워크 유형|속도|  
|----------------|---------|  
|매우 느림|초당 Kbps (초당 킬로 비트) 56|  
|슬로우|64Kbps|  
|ISDN (Integrated Services Digital Network)|64 kbps 또는 128 Kbps|  
|프레임 릴레이|가변 속도, 일반적으로 56 Kbps와 1.5 메가 비트/초 (Mbps)|  
|T1|1.5 Mbps|  
|T3|45 Mbps|  
|10BaseT|10mbps|  
|ATM (비동기 전송 모드)|가변 률 (일반적으로 155 Mbps ~ 622 Mbps)|  
|100BaseT|100Mbps|  
|기가 비트 이더넷|초당 1 기가 비트 (Gbps)|  
  
WAN (광역 네트워크 속도) 링크 속도에 따라 각 사이트 링크의 비용을 계산 하려면 다음 표를 사용 합니다. 표에 나열 되지 않은 WAN 링크 속도의 경우 1024를 사용 가능한 대역폭의 로그 (Kbps)로 나누어 상대적 비용 요인을 계산할 수 있습니다.  
  
|사용 가능한 대역폭 (Kbps)|비용|  
|--------------------------------|--------|  
|9.6|1042|  
|19.2|798|  
|38.4|644|  
|56|586|  
|64|567|  
|128|486|  
|256|425|  
|512|378|  
|1,024|340|  
|2048|309|  
|4,096|283|  
  
이러한 비용은 네트워크 링크 간의 안정성 차이를 반영 하지 않습니다. 복제에 대 한 링크를 사용 하지 않아도 되도록 오류가 발생 하기 쉬운 네트워크 링크에 대 한 비용을 더 많이 설정 합니다. 사이트 링크 비용을 더 높게 설정 하면 사이트 링크가 실패할 때 복제 장애 조치 (failover)를 제어할 수 있습니다.  
  


