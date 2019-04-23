---
title: 외부 가상 스위치에 바인딩된 VMQ를 사용할 수 있는 실제 네트워크 어댑터에서 VMQ는 사용할 수 있어야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 93d1b155-bf44-46b0-bb69-d34d5b30e574
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9a552c15675e6ca7a7310c8c9eaec883653987be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889474"
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
*가상 머신 큐 (VMQ)의 네트워크 어댑터 수 있지만 기능이 사용할 수 없습니다.*  
  
## <a name="impact"></a>**Impact**  
*Windows가 다음과 같은 네트워크 어댑터에 사용 가능한 하드웨어 오프 로드의 활용 하기 위해 수 없습니다.*  
  
\<네트워크 어댑터의 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*Enable NetAdapterVmq Windows PowerShell cmdlet을 사용 하 여 또는 네트워크 어댑터에 대 한 고급 속성 사용자 인터페이스를 사용 하 여 VMQ를 사용 하도록 설정 합니다.*  
  


