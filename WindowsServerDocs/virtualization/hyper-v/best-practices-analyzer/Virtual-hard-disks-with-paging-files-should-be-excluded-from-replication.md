---
title: 페이징 파일을 사용 하는 가상 하드 디스크 복제에서 제외 되어야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: c0be8a5f-64a1-488a-944e-bb913bb90517
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8b6289a82c83f3dcfc0de299250ce19ee3782678
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850124"
---
# <a name="virtual-hard-disks-with-paging-files-should-be-excluded-from-replication"></a>페이징 파일을 사용 하는 가상 하드 디스크 복제에서 제외 되어야 합니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|정보|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*페이징 파일 복제에 참여 하에서 제외 되어야 하지만 제외 되는 디스크가 없습니다.*  
  
## <a name="impact"></a>영향  
*페이징 파일 경험 많은 양의 입/출력 작업 복제에 참여 하려면 더 많은 리소스를 불필요 하 게 해야 합니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*아직 수행 하는 경우에 Windows 페이징 파일에 대 한 별도 가상 하드 디스크를 만듭니다. 초기 복제 이미 완료 하는 경우 Hyper-v 관리자를 사용 하 여 복제를 제거 합니다. 그런 다음 복제를 다시 구성 하 고 복제에서 페이징 파일로 가상 하드 디스크를 제외 합니다.*  
  


