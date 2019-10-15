---
title: 핫 플러그 끄고 hot 저장소 수 있으려면 SCSI 컨트롤러와 가상 컴퓨터를 구성 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 511e1172-aeef-463d-b5dd-2bffae411ff1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5b901ee8f11942b8ad50a3c34c53354a5998e105
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365075"
---
# <a name="configure-a-virtual-machine-with-a-scsi-controller-to-be-able-to-hot-plug-and-hot-unplug-storage"></a>핫 플러그 끄고 hot 저장소 수 있으려면 SCSI 컨트롤러와 가상 컴퓨터를 구성 합니다.

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사에 대한 자세한 내용은*  [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*SCSI 컨트롤러를 사용 하 여 구성 되지 않은 가상 컴퓨터가 있습니다.*  
  
## <a name="impact"></a>영향  
  
*다음 가상 컴퓨터에 대 한 저장소를 핫 플러그 인 하거나 핫 플러그를 해제할 수 없습니다.*  
  
@no__t-가상 머신 이름의 목록 >  
  
핫 플러그를 뽑거나 hot 저장 하는 기능 쉽게 가동 중지 시간 없이 가상 컴퓨터의 저장소 요구를 관리할 수 있습니다. SCSI 컨트롤러 없이 가상 컴퓨터는 추가 하거나 저장소를 제거 하기 전에를 종료 해야 합니다.  
  
## <a name="resolution"></a>해결 방법  
  
*이 가상 컴퓨터에 대 한 저장소를 핫 플러그 또는 핫 플러그 인할 필요가 없는 경우 아무 작업도 필요 하지 않습니다. 그렇지 않으면 가상 컴퓨터를 종료 하 고 구성에 SCSI 컨트롤러를 추가 합니다.*  
  
핫플러그 SCSI 컨트롤러를 사용 하 여 hot 저장소를 분리 하는 게스트 운영 체제의 현재 버전의 integration services 실행 되어야 합니다.  
  


