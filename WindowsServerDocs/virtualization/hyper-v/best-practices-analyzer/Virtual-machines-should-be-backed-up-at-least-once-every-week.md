---
title: 매주 한 번 이상를 가상 컴퓨터를 백업 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 6cb425f92926aa1823ed89cd26afccc2d962603d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855036"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>매주 한 번 이상를 가상 컴퓨터를 백업 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|오류|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*지난 주에 하나 이상의 가상 머신이 백업 되지 않았습니다.*  
  
## <a name="impact"></a>영향  
*가상 컴퓨터에 문제가 발생 하 고 최근 백업이 존재 하지 않는 경우 중요 한 데이터가 손실 될 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*가상 컴퓨터의 백업이 한 주에 한 번 이상 실행 되도록 예약 합니다. 이 가상 컴퓨터가 복제본이 고 해당 주 가상 컴퓨터를 백업 중인 경우 또는 주 가상 컴퓨터이 고 해당 복제본이 백업 중인 경우이 규칙을 무시할 수 있습니다.*  
  


