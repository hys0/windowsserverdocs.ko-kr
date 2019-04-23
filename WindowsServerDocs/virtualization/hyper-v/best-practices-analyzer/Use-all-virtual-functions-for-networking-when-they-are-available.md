---
title: 사용할 때의 네트워킹에 대 한 모든 가상 함수를 사용 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3ad120ffa689f1f7dcae832432e216ebda57e62f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877794"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>사용할 때의 네트워킹에 대 한 모든 가상 함수를 사용 합니다.

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
*일부 하드웨어 가속 기능 사용 되지 않습니다.*  
  
## <a name="impact"></a>영향  
*이 구성은 필요한 것 보다 더 높은 것으로 전체 CPU 사용률을 발생할 수 있습니다. 네트워킹 성능 다음 가상 컴퓨터에 적합 하지 않을 수 있습니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*SR-IOV 및 가상 컴퓨터에 필요한 네트워킹 기능을 사용 하 여이 구성을 충돌 하지 않는 경우 실제 하드웨어에서 지 원하는 경우 SR-IOV에 대 한 가상 네트워크 어댑터를 구성 하는 것이 좋습니다.*  
  


