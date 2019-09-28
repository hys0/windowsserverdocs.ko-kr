---
title: 일시 중지 하면 가상 컴퓨터 방지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 406b24edd4a7e87e32058006590ac7cd37206568
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366455"
---
# <a name="avoid-pausing-a-virtual-machine"></a>일시 중지 하면 가상 컴퓨터 방지

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
  
*이 서버에는 하나 이상의 가상 머신이 일시 중지 된 상태입니다.*  
  
## <a name="impact"></a>영향  
  
*사용 가능한 메모리의 양에 따라 추가 가상 컴퓨터를 실행 하지 못할 수 있습니다.*  
  
일시 중지 된 가상 컴퓨터의 할당 된 메모리를 놓지 마십시오 다른 가상 컴퓨터를 시작할 수 없는 메모리를 의미 하는 합니다.  
  
## <a name="resolution"></a>해결 방법  
  
*이 의도적인 경우 추가 작업이 필요 하지 않습니다. 그렇지 않은 경우 이러한 가상 컴퓨터를 다시 시작 하거나 종료 하는 것이 좋습니다.*  
  
#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>Hyper-v 관리자를 사용 하 여 가상 컴퓨터를 다시 시작 하려면  
  
1.  Hyper-V 관리자를 엽니다. (에서 **도구** 서버 관리자의 메뉴 클릭 **Hyper-v 관리자**.)  
  
2.  **가상 컴퓨터** 목록에서 가상 컴퓨터의 상태와 **일시 중지 된**합니다.  
  
    > [!IMPORTANT]  
    > 상태 **일시 중지 된 중요 한** 해당 가상 컴퓨터에 대 한 물리적 저장소에 남아 있는 사용 가능한 공간을 적게 차지 하는 경우에 발생 합니다. 이 상태의 가상 컴퓨터를 다시 시작 하려고 하기 전에 실제 저장소에 사용 가능한 공간을 늘리십시오.  
  
3.  각 가상 컴퓨터 이름을 마우스 오른쪽 단추로 클릭 하 여 **Resume**합니다. 이렇게 가상 컴퓨터를 실행 상태로 반환 됩니다. 그런 다음 가상 컴퓨터를 종료 하려는 경우 다시 마우스 선택 **종료**합니다.  
  
#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Windows PowerShell을 사용 하 여 가상 컴퓨터를 다시 시작 하려면  
  
필터링을 사용 하 여 하나의 명령으로 이렇게 하려면 하 고 나면 파이프라인 호스트의 모든 가상 컴퓨터를 가져옵니다. 형식:  
  
```  
get-vm | where state -eq 'paused' | resume-vm  
```  
  


