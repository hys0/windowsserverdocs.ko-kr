---
title: 매주 한 번 이상를 가상 컴퓨터를 백업 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ec11b067de2c9f8cbb3a17731caa0dc526bf54a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393241"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>매주 한 번 이상를 가상 컴퓨터를 백업 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*지난 주에 하나 이상의 가상 머신이 백업 되지 않았습니다.*  
  
## <a name="impact"></a>영향  
*가상 컴퓨터에 문제가 발생 하 고 최근 백업이 존재 하지 않는 경우 중요 한 데이터가 손실 될 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해결 방법  
*가상 컴퓨터의 백업이 한 주에 한 번 이상 실행 되도록 예약 합니다. 이 가상 컴퓨터가 복제본이 고 해당 주 가상 컴퓨터를 백업 중인 경우 또는 주 가상 컴퓨터이 고 해당 복제본이 백업 중인 경우이 규칙을 무시할 수 있습니다.*  
  


