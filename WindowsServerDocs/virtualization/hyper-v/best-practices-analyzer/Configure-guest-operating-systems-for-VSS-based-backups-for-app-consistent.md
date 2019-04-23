---
title: Hyper-v 복제본에 대 한 응용 프로그램 일치 스냅숏을 사용할 수 있도록 VSS 기반 백업에 대 한 게스트 운영 체제를 구성 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: b4300dd4b7adc0cef8544215b5da62044a97301b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863894"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>Hyper-v 복제본에 대 한 응용 프로그램 일치 스냅숏을 사용할 수 있도록 VSS 기반 백업에 대 한 게스트 운영 체제를 구성 합니다.

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
*응용 프로그램에 일관 된 스냅숏을 볼륨 섀도 복사본 서비스 (VSS)가 사용 되 고 복제에 참여 하는 가상 머신의 게스트 운영 체제에서 구성 해야 합니다.*  
  
## <a name="impact"></a>영향  
*응용 프로그램 일치 스냅숏 복제 구성에 지정, 경우에 Hyper-v는 사용 하지 VSS를 구성 하지 않으면. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*가상 컴퓨터에서 integration services를 설치 하려면 가상 머신 연결을 사용 합니다.*  
  


