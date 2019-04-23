---
title: 가상 컴퓨터에 모두 사용할 수 있는 통합 서비스를 제공 합니다.
description: 이 모범 사례 분석기 규칙에 의해 보고 된 문제를 해결 하려면 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2c4b2043-ad81-495e-aa7a-467f813bb3d2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c2b5137594f78980f87f6520ae4b4af8203aef32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883784"
---
# <a name="offer-all-available-integration-services-to-virtual-machines"></a>가상 컴퓨터에 모두 사용할 수 있는 통합 서비스를 제공 합니다.

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*Virtual machines에서 하나 이상의 사용 가능한 통합 서비스가 사용 되지 않습니다.*  
  
## <a name="impact"></a>영향  
  
*일부 기능이 다음 가상 컴퓨터에 사용할 되지 않습니다.*  
  
\<가상 머신 이름 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*의도적인 작업 인 경우 추가 조치가 필요 하지 않습니다. 그렇지 않은 경우 이러한 가상 컴퓨터의 설정에 모든 integration services를 제공 하는 것이 좋습니다.*  
  
가상 컴퓨터 설정을 통해 일부 통합 서비스의 가용성을 관리할 수 있습니다.   
  
#### <a name="to-manage-the-availability-of-integration-services-to-a-virtual-machine"></a>가상 컴퓨터에 통합 서비스의 가용성을 관리 하려면  
  
1.  Hyper-V 관리자를 엽니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **Hyper-v 관리자**합니다.  
  
2.  결과 창에서 아래 **가상 컴퓨터**, 구성 하려는 가상 컴퓨터를 선택 합니다.  
  
3.  **작업** 창의 가상 컴퓨터 이름에서 **설정**을 클릭합니다.  
  
4.  아래에서 **관리**, 클릭 **Integration Services**합니다.  
  
5.  Integration services의 목록에서 가상 컴퓨터에 제공 하려는 각 서비스에 대 한 확인란을 선택 합니다. 확인란을 사용할 수 없는 경우 해당 특정 통합 서비스는 가상 컴퓨터에서 실행 되는 게스트 운영 체제에서 지원 되지 않습니다.  
  


