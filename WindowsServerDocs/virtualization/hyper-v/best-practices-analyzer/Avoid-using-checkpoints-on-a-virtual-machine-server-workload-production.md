---
title: 프로덕션 환경에서 서버 작업을 실행 하는 가상 컴퓨터에서 검사점을 사용 하지 마십시오
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1be75890-d316-495a-b9b7-be75fc1aac10
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f2486093e31143b7493665d3d1254f7034ad1415
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365223"
---
# <a name="avoid-using-checkpoints-on-a-virtual-machine-that-runs-a-server-workload-in-a-production-environment"></a>프로덕션 환경에서 서버 작업을 실행 하는 가상 컴퓨터에서 검사점을 사용 하지 마십시오

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사에 대한 자세한 내용은* [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  

다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.

> [!NOTE]  
> Windows Server 2012 R2 가상 머신 스냅샷 System Center Virtual Machine 관리에 사용되는 용어와 일치하도록 Hyper-v 관리자에서 가상 머신 검사점으로 바뀌었습니다. 자세한 내용은 다음을 참조 하십시오. [검사점 및 스냅샷 개요](https://technet.microsoft.com/library/dn818483.aspx)합니다.  
  
## <a name="issue"></a>문제점  
  
*하나 이상의 검사점이 있는 가상 머신을 찾았습니다.*  
  
## <a name="impact"></a>영향  
  
*검사점 파일을 저장 하는 실제 디스크에서 사용 가능한 공간을 사용할 수 있습니다. 이 문제가 발생 하면 실제 저장소에서 추가 디스크 작업을 수행할 수 없습니다. 실제 저장소를 사용 하는 모든 가상 컴퓨터에 영향을 줄 수 있습니다.*  
  
실행 된 경우 실제 디스크 공간이, 자동으로 검사점 또는 가상 하드 디스크는 디스크에 저장 된 모든 실행 중인 가상 컴퓨터를 일시 중지 될 수 있습니다. Hyper-v 관리자는 "일시 중지-중요"으로 이러한 가상 컴퓨터의 상태를 표시 합니다.  
  
## <a name="resolution"></a>해결 방법  
  
*가상 컴퓨터가 프로덕션 환경에서 서버 작업을 실행 하는 경우 가상 컴퓨터를 오프 라인으로 전환한 다음 Hyper-v 관리자를 사용 하 여 검사점을 적용 하거나 삭제 합니다. 검사점을 삭제 하려면 가상 컴퓨터를 종료 하 여 프로세스를 완료 해야 합니다.*  
  
> [!NOTE]  
> 프로덕션 검사점 표준 검사점 대신 사용할 수 있습니다. 자세한 내용은 다음을 참조 하십시오. [표준 또는 프로덕션 검사점 간의 선택](../manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)합니다.  
  


