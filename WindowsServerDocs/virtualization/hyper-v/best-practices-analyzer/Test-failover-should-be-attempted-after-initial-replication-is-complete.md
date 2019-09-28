---
title: 테스트 장애 조치를 시도 하 여 초기 복제가 완료 된 후
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cea7eeaa-c1a7-4f87-89be-d4e1208c546f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ec3ad3994227eb14d1d2e53842c755af76ac538d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364704"
---
# <a name="test-failover-should-be-attempted-after-initial-replication-is-complete"></a>테스트 장애 조치를 시도 하 여 초기 복제가 완료 된 후

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="problem"></a>문제점  
*하나 이상의 월에 테스트 장애 조치 (failover)가 없습니다.*  
  
## <a name="impact"></a>영향  
*은 계획 되거나 계획 되지 않은 장애 조치 (failover)가 성공 하거나 장애 조치 (failover) 후 작업을 계속 진행할 것인지 확인 하지 않습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
@no__t-가상 머신 목록 >  
  
## <a name="resolution"></a>해결 방법  
*Hyper-v 관리자를 사용 하 여 테스트 장애 조치 (failover)를 수행 합니다.*  
  


