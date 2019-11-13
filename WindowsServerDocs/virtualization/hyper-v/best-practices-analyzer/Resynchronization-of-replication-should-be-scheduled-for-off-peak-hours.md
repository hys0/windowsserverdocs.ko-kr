---
title: 사용량이 적은 시간에 대 한 복제의 다시 동기화 하도록 예약 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 379f8c8cd6744fe5db176efb55a84f231ce45857
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393513"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>사용량이 적은 시간에 대 한 복제의 다시 동기화 하도록 예약 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*주 가상 컴퓨터에 대 한 복제 다시 동기화는 사용량이 적은 시간에 예약 되지 않습니다.*  
  
## <a name="impact"></a>영향  
*가상 컴퓨터가 다시 동기화 해야 하는 상태에 있는 경우 더 긴 복제 로그 파일이 증가 하 고 주 가상 컴퓨터에서 복제 되지 않은 변경이 발생 합니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해결 방법  
*Hyper-v 관리자를 사용 하 여 사용량이 많지 않은 시간에 자동으로 다시 동기화를 수행 하도록 가상 컴퓨터의 복제 설정을 수정 합니다.*  
  


