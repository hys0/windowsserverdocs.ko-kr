---
title: 실시간 마이그레이션 트래픽에 대 한 하나 이상의 네트워크 이상 1gbps의 링크 속도 있어야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ef75f73bd934b863b146e93f4cdc7323e5d4c6fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837734"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>실시간 마이그레이션 트래픽에 대 한 하나 이상의 네트워크 이상 1gbps의 링크 속도 있어야 합니다.

>적용 대상: Windows Server 2016


  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*실시간 마이그레이션 트래픽에 대 한 네트워크 이상 1gbps의 링크 속도가 없습니다.*  
  
## <a name="impact"></a>영향  
*TCP 연결 시간 초과 인해 네트워크 연결 문제를 일으킬 수 있는 실시간 마이그레이션 속도 느리게 발생할 수 있습니다.*  
  
## <a name="resolution"></a>해결 방법  
*1gbps의 이상 속도가 실시간 마이그레이션 네트워크를 하나 이상 구성 합니다.*  
  
알아보려면 경우 적어도 1gbps의 연결 속도 지원할 수 기존 네트워크 어댑터 네트워크 하드웨어 공급 업체의 설명서를 참조 합니다.  
  


