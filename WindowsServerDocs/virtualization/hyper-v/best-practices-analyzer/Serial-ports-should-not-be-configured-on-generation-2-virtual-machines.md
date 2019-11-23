---
title: 2 세대 가상 컴퓨터에서 직렬 포트를 구성 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8a8c15076921efa0e1e791a18c6a45ea1bf27b0e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364732"
---
# <a name="serial-ports-should-not-be-configured-on-generation-2-virtual-machines"></a>2 세대 가상 컴퓨터에서 직렬 포트를 구성 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제점**  
*하나 이상의 2 세대 가상 컴퓨터에 직렬 포트가 구성 되어 있습니다.*  
  
## <a name="impact"></a>**식**  
*다음 가상 컴퓨터에 대 한 성능에 영향을 줄 수 있습니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*의도적인 경우 추가 작업이 필요 하지 않습니다. 그렇지 않은 경우에는 Hyper-v 관리자 또는 Windows PowerShell을 사용 하 여 가상 컴퓨터의 직렬 포트에서 연결 문자열을 제거 하는 것이 좋습니다.*  
  


