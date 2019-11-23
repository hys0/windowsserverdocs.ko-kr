---
title: 장애 조치 후 복구 스냅샷은 제거 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4b8574956fb1b46ca0cf9678187fffcd68c2d261
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393531"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>장애 조치 후 복구 스냅샷은 제거 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016| 
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제점**  
*장애 조치 (failover) 된 가상 머신에 하나 이상의 복구 스냅숏이 있습니다.*  
  
## <a name="impact"></a>**식**  
*스냅숏 파일을 저장 하는 실제 디스크에서 사용 가능한 공간을 사용할 수 있습니다. 이 문제가 발생 하면 실제 저장소에서 추가 디스크 작업을 수행할 수 없습니다. 실제 저장소를 사용 하는 모든 가상 컴퓨터에 영향을 줄 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*장애 조치 (failover) 된 각 가상 머신에 대해 Windows PowerShell의 Start-vmfailover cmdlet을 사용 하 여 복구 스냅숏을 제거 하 고 장애 조치 (failover) 완료를 표시 합니다.*  
  


