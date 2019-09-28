---
title: 외부 가상 스위치에 바인딩된 VMQ를 사용할 수 있는 실제 네트워크 어댑터에서 VMQ는 사용할 수 있어야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 93d1b155-bf44-46b0-bb69-d34d5b30e574
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e8607ee891ef693d4e4e7a868540237855aebd2e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393291"
---
# <a name="vmq-should-be-enabled-on-vmq-capable-physical-network-adapters-bound-to-an-external-virtual-switch"></a>외부 가상 스위치에 바인딩된 VMQ를 사용할 수 있는 실제 네트워크 어댑터에서 VMQ는 사용할 수 있어야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제점**  
*다음 네트워크 어댑터는 VMQ (가상 머신 큐)를 사용할 수 있지만이 기능을 사용할 수 없습니다.*  
  
## <a name="impact"></a>**식**  
*Windows는 다음과 같은 네트워크 어댑터에서 사용 가능한 하드웨어 오프 로드를 최대한 활용할 수 없습니다.*  
  
\< 개의 네트워크 어댑터 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*Set-netadaptervmq Windows PowerShell cmdlet을 사용 하거나 네트워크 어댑터용 고급 속성 사용자 인터페이스를 사용 하 여 VMQ를 사용 하도록 설정 합니다.*  
  


