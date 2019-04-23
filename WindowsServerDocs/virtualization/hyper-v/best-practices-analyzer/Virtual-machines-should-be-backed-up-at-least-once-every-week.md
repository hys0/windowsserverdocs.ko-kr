---
title: 매주 한 번 이상를 가상 컴퓨터를 백업 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e079e3cb225ec9c712233bbf3efc85bb6f09b218
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826754"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>매주 한 번 이상를 가상 컴퓨터를 백업 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*지난 주에 하나 이상의 가상 컴퓨터 백업 되지 않았습니다.*  
  
## <a name="impact"></a>영향  
*가상 컴퓨터에서 문제가 발생 하 고 최근 백업이 존재 하지 않는 경우 상당한 데이터 손실이 발생할 수 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*가상 컴퓨터의 백업이 일주일에 한 번 이상 실행 되도록 예약 합니다. 무시할 수 있습니다이 규칙 또는이 가상 컴퓨터는 복제본 및 해당 기본 가상 머신 백업 되는 경우 주 가상 컴퓨터 이며 복제본 백업 중인 경우.*  
  


