---
title: 차이점 보관용 가상 하드 디스크를 사용 하는 가상 컴퓨터 때 충분 한 실제 디스크 공간을 사용할 수
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 71f99aab-f994-4022-9da0-d661965b95ac
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3827d149d2d691b4ecd7fe6ae8f6d7255c85a31c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364873"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-differencing-virtual-hard-disks"></a>차이점 보관용 가상 하드 디스크를 사용 하는 가상 컴퓨터 때 충분 한 실제 디스크 공간을 사용할 수

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*하나 이상의 가상 컴퓨터에서 차이점 보관용 가상 하드 디스크를 사용 하 고 있습니다.*  
  
## <a name="impact"></a>영향  
가상 하드 디스크에 대 한 쓰기가 발생 하는 경우 공간을 할당할 수 있도록 @no__t 차이점 보관용 가상 하드 디스크에는 호스팅 볼륨의 사용 가능한 공간이 필요 합니다. 사용 가능한 공간이 부족 한 상태에서 물리적 저장소를 사용 하는 모든 가상 컴퓨터를 저하 될 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다. *  
  
@no__t-가상 머신 목록 >  
  
## <a name="resolution"></a>해결 방법  
*사용 가능한 디스크 공간을 모니터링 하 여 가상 하드 디스크 확장에 사용할 수 있는 공간이 충분 한지 확인 합니다. 차이점 보관용 가상 하드 디스크의 부모에 병합 하는 것이 좋습니다. Hyper-v 관리자에서 부모 가상 하드 디스크를 확인 하려면 차이점 보관용 디스크를 검사 합니다. 다른 차이점 보관용 디스크에서 공유 하는 부모 디스크를 차이점 보관용 디스크를 병합 하는 경우 해당 작업에는 다른 차이점 보관용 디스크와 사용할 수 없게 하는 부모 디스크 간의 관계를 손상 됩니다. 부모 가상 하드 디스크가 공유 되지 않았는지 확인 한 후에는 디스크 편집 마법사를 사용 하 여 차이점 보관용 디스크를 부모 가상 하드 디스크에 병합할 수 있습니다.*  
  


