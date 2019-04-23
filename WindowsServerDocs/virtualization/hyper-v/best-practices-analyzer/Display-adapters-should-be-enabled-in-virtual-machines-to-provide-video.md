---
title: 디스플레이 어댑터를 비디오 기능을 제공 하도록 virtual machines에서 사용 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8d61461db471a876ddf46c1e5fec6992ffa80373
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870694"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>디스플레이 어댑터를 비디오 기능을 제공 하도록 virtual machines에서 사용 해야

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)합니다.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*가상 컴퓨터에서 Microsoft 가상 컴퓨터 버스 비디오 장치를 비활성화할 수 있습니다.*  
  
Microsoft 가상 머신 버스 비디오 장치는 Hyper-v 가상 머신을 사용 하도록 최적화 된 가상 비디오 어댑터. 가상 컴퓨터를 Microsoft 가상 머신 버스 비디오 장치를 사용 하도록 구성 되지 않았습니다, 비디오 어댑터를 레거시 사용 됩니다. Microsoft 가상 머신 버스 비디오 장치 레거시 비디오 어댑터를 보다 효율적으로 수행 되었습니다.  
  
## <a name="impact"></a>영향  
  
*다음 가상 컴퓨터에 대 한 비디오 성능이 저하 됩니다.*  
  
\<가상 머신 이름 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*Microsoft 가상 컴퓨터 버스 비디오 장치를 사용 하도록 설정 하려면 게스트 운영 체제에서 장치 관리자를 사용 합니다.*  
  
장치 관리자를 사용 하는 데 필요한 단계는 운영 체제에 따라 달라 집니다. 자세한 내용은 게스트 운영 체제에서 도움말을 참조 합니다.  
  


