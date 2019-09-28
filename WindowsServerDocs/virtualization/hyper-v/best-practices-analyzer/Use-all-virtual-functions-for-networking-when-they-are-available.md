---
title: 사용할 수 있는 네트워킹에 모든 가상 함수 사용
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8798a7021b3df0113b8d957340d6d688acead5c7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393350"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>사용할 수 있는 네트워킹에 모든 가상 함수 사용

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
*일부 하드웨어 가속 기능이 활용 되 고 있지 않습니다.*  
  
## <a name="impact"></a>영향  
*이 구성으로 인해 전체 CPU 사용률이 필요한 것 보다 높을 수 있습니다. 다음 가상 머신에서는 네트워킹 성능이 최적이 아닐 수 있습니다.*  
  
@no__t-가상 머신 목록 >  
  
## <a name="resolution"></a>해결 방법  
*물리적 하드웨어가 SR-IOV를 지원 하 고이 구성이 가상 컴퓨터에 필요한 네트워킹 기능과 충돌 하지 않는 경우 SR-IOV에 대해 가상 네트워크 어댑터를 구성 하는 것이 좋습니다.*  
  


