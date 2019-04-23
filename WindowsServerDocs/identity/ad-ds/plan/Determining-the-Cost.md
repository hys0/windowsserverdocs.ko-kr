---
ms.assetid: e3ea1f67-60d4-4566-b24c-37faa95c3b2a
title: 비용 결정
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0b34f1672311768d644c467fda10dc2fc643282d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847084"
---
# <a name="determining-the-cost"></a>비용 결정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

비용이 많이 드는 연결을 통해 저렴 한 연결을 선호 하는 사이트 링크 비용 값을 할당 합니다. 특정 응용 프로그램 및 도메인 컨트롤러 로케이터 (DCLocator) 및 분산 파일 시스템 네임 스페이스 (DFSN (), 같은 서비스에 가장 가까운 리소스를 찾을 수 비용 정보를 사용할 수도 있습니다. 지정한 도메인의 도메인 컨트롤러 사이트에 없는 경우 한 사이트에에서 클라이언트에서 연결한 도메인 컨트롤러를 확인 하려면 사이트 링크 비용을 사용할 수 있습니다. 클라이언트 가장 낮은 비용 할당 된 사이트 링크를 사용 하 여 도메인 컨트롤러에 연결 합니다.  
  
사이트 전체에서 비용 값을 정의 하는 것이 좋습니다. 일반적으로 비용 링크의 총 대역폭에 뿐만 아니라 가용성, 대기 시간 및 통화 링크 비용에 기반 합니다.  
  
사이트 링크에 배치 하는 비용을 확인 하려면 각 사이트 링크에 대 한 연결 속도 문서화 합니다. "지리적 위치 및 통신 링크" (DSSTOPO_1.doc) 워크시트를 참조 하세요 [네트워크 정보 수집](../../ad-ds/plan/Collecting-Network-Information.md) 것으로 확인 되는 연결 속도 대 한 정보에 대 한 합니다.  
  
다음 표에서 다양 한 유형의 네트워크에 대 한 속도 나열합니다.  
  
|네트워크 유형|속도|  
|----------------|---------|  
|매우 느린|56 킬로바이트 / 초 (Kbps)|  
|슬로우|64Kbps|  
|Integrated Services Digital Network ISDN)|64kbps 또는 128kbps|  
|프레임 릴레이|변수, 일반적으로 사이의 속도가 56kbps 1.5 초당 메가 비트 (Mbps)|  
|T1|1.5mbps|  
|T3|45 Mbps|  
|10BaseT|10mbps|  
|비동기 전송 모드 (ATM)|일반적으로 사이의 155 Mbps 622 Mbps 변수 속도|  
|100BaseT|100Mbps|  
|기가 비트 이더넷|1 기가 비트 (gbps)|  
  
다음 표를 사용 하 여 광역 네트워크 (WAN) 속도 링크 속도에 따라 각 사이트 링크 비용을 계산 합니다. 테이블에 나열 되지 않은 WAN 링크 속도 대 한 상대 비용 요소가 1,024 Kbps 단위로 측정 되는 사용 가능한 대역폭에 대 한 로그로 나누어 계산할 수 있습니다.  
  
|사용 가능한 대역폭 (Kbps)|비용|  
|--------------------------------|--------|  
|9.6|1,042|  
|19.2|798|  
|38.4|644|  
|56|586|  
|64|567|  
|128|486|  
|256|425|  
|512|378|  
|1,024|340|  
|2,048|309|  
|4,096|283|  
  
이러한 비용은 안정성 네트워크 링크 간 차이 반영 하지 않습니다. 복제에 대 한 해당 링크에 의존할 필요가 없습니다 되도록 대 한 오류가 발생 하기 쉬운 네트워크 연결에 더 높은 비용을 설정 합니다. 사이트 링크 비용을 더 높은 설정 하 여 사이트 링크를 실패 한 경우 복제 장애 조치를 제어할 수 있습니다.  
  


