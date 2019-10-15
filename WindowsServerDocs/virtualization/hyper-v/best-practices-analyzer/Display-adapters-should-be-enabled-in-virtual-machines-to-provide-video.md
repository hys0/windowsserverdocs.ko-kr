---
title: 비디오 기능을 제공 하기 위해 가상 머신에서 표시 어댑터를 사용 하도록 설정 해야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0c515c7fb1ed160dfee1e1b7303022082e936157
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364912"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>비디오 기능을 제공 하기 위해 가상 머신에서 표시 어댑터를 사용 하도록 설정 해야 합니다.

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사에 대한 자세한 내용은* [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*가상 머신에서 Microsoft Virtual Machine Bus 비디오 장치를 사용 하지 않도록 설정할 수 있습니다.*  
  
Microsoft 가상 컴퓨터 버스 비디오 장치는 Hyper-v 가상 컴퓨터에서 사용 하도록 최적화 된 가상 비디오 어댑터입니다. Microsoft 가상 컴퓨터 버스 비디오 장치를 사용 하도록 가상 컴퓨터를 구성 하지 않은 경우에는 레거시 비디오 어댑터가 사용 됩니다. Microsoft Virtual Machine Bus 비디오 장치는 레거시 비디오 어댑터 보다 성능이 뛰어납니다.  
  
## <a name="impact"></a>영향  
  
*다음 가상 컴퓨터에 대 한 비디오 성능이 저하 됩니다.*  
  
@no__t-가상 머신 이름의 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*게스트 운영 체제의 Device Manager를 사용 하 여 Microsoft 가상 컴퓨터 버스 비디오 장치를 사용 하도록 설정 합니다.*  
  
Device Manager를 사용 하는 데 필요한 단계는 운영 체제에 따라 달라 집니다. 자세한 내용은 게스트 운영 체제의 도움말을 참조 하십시오.  
  


