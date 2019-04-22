---
title: 파이버 채널 기반 저장소에 고가용성을 위해 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터를 구성 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 203477a022f7c5f819ef7b99f1b8e37a0b8b0a9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816944"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>파이버 채널 기반 저장소에 고가용성을 위해 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터를 구성 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|정보|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>**문제점**  
*하나의 호스트 버스 어댑터 (HBA)에 연결 된 가상 파이버 채널 어댑터를 사용 하 여 해당 가상 컴퓨터 구성 되어 있으므로 하나 이상의 가상 컴퓨터 파이버 채널 기반 저장소를 항상 사용 가능한 연결을 부족 합니다.*  
  
## <a name="impact"></a>**Impact**  
*호스트 버스 어댑터의 오류는 저장소 및 가상 컴퓨터 간의 파이버 채널 연결을 차단할 수 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*호스트 버스 어댑터를 가상 머신에서 다른 연결을 추가 하 고 중복 된 파이버 채널 연결을 설정 하려면 게스트 운영 체제에서 다중 경로 I/O (MPIO)를 구성 합니다.*  
  


