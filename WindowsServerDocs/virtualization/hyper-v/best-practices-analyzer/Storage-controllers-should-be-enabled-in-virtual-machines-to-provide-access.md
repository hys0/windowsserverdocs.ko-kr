---
title: 저장소 컨트롤러 사용 해야 가상 컴퓨터에 연결 된 저장소에 대 한 액세스를 제공 합니다.
description: 이 모범 사례 분석기 규칙에서 보고 한 문제를 해결 하는 지침을 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 532548a1-8ffe-4b5b-902e-ed2f0819012b
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f0d10ab4c419a6014a9edb4b7f721714dc92798d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393486"
---
# <a name="storage-controllers-should-be-enabled-in-virtual-machines-to-provide-access-to-attached-storage"></a>저장소 컨트롤러 사용 해야 가상 컴퓨터에 연결 된 저장소에 대 한 액세스를 제공 합니다.

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  

다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.

## <a name="issue"></a>문제점  
  
*가상 머신에서 하나 이상의 저장소 컨트롤러를 사용 하지 않도록 설정할 수 있습니다.*  
  
## <a name="impact"></a>영향  
  
*가상 컴퓨터는 사용 하지 않도록 설정 된 저장소 컨트롤러에 연결 된 저장소를 사용할 수 없습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 이름 목록 \<>  
  
## <a name="resolution"></a>해결 방법  
  
*게스트 운영 체제의 Device Manager를 사용 하 여 모든 저장소 컨트롤러를 사용 하도록 설정 합니다. 저장소 컨트롤러가 필요 하지 않은 경우 Hyper-v 관리자를 사용 하 여 가상 머신에서 제거 합니다.*  
  
장치 관리자를 사용 하는 방법에 대 한 자세한 내용은 게스트 운영 체제에서 도움말을 참조 합니다. 저장소 컨트롤러를 제거 하는 방법에 대 한 지침은 다음 절차를 참조 합니다.  
  
#### <a name="to-remove-a-scsi-storage-controller-from-the-virtual-machine"></a>가상 컴퓨터에서 SCSI 저장소 컨트롤러를 제거 하려면  
  
1.  Hyper-V 관리자를 엽니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **Hyper-v 관리자**합니다.  
  
2.  결과 창에서 아래 **가상 컴퓨터**, 구성 하려는 가상 컴퓨터를 선택 합니다.  
  
3.  가상 컴퓨터를 실행 하는 경우 가상 컴퓨터를 종료 합니다. 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 클릭 **종료**합니다.  
  
4.  **작업** 창의 가상 컴퓨터 이름에서 **설정**을 클릭합니다.  
  
5.  왼쪽된 창에서는 **설정을** 대화 상자의 **하드웨어**, 클릭 **SCSI 컨트롤러**합니다.  
  
6.  오른쪽 창에서 클릭 **제거**합니다.  
  


