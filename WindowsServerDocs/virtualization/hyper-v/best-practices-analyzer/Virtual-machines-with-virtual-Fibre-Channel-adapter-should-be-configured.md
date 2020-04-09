---
title: 파이버 채널 기반 스토리지에 고가용성을 위해 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터를 구성 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: e04b52fc98fd79024970ed525e902132d97701e6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855006"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>파이버 채널 기반 스토리지에 고가용성을 위해 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터를 구성 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|정보|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>**문제**  
*하나 이상의 가상 컴퓨터는 하나의 HBA (호스트 버스 어댑터)에만 연결 된 가상 파이버 채널 어댑터를 사용 하 여 구성 되므로 파이버 채널 기반 저장소에 대해 항상 사용 가능한 연결이 없습니다.*  
  
## <a name="impact"></a>**식**  
*호스트 버스 어댑터의 오류로 인해 저장소와 가상 컴퓨터 간의 파이버 채널 연결이 차단 될 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*가상 머신에서 호스트 버스 어댑터에 다른 연결을 추가 하 고 게스트 운영 체제에서 MPIO (다중 경로 i/o)를 구성 하 여 중복 파이버 채널 연결을 설정 합니다.*  
  


