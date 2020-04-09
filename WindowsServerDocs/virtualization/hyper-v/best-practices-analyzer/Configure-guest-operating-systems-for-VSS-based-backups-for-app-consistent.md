---
title: Hyper-v 복제본에 대 한 애플리케이션 일치 스냅샷을 사용할 수 있도록 VSS 기반 백업에 대 한 게스트 운영 체제를 구성 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f7a77b2cb743f478525f839e1c64ecc892b3fb04
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862066"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>Hyper-v 복제본에 대 한 애플리케이션 일치 스냅샷을 사용할 수 있도록 VSS 기반 백업에 대 한 게스트 운영 체제를 구성 합니다.

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
*응용 프로그램에 일관 된 스냅숏을 사용 하려면 복제에 참여 하는 가상 컴퓨터의 게스트 운영 체제에서 VSS (볼륨 섀도 복사본 서비스)를 사용 하도록 설정 하 고 구성 해야 합니다.*  
  
## <a name="impact"></a>영향  
*복제 구성에서 응용 프로그램 일치 스냅숏이 지정 된 경우에도 Hyper-v는 VSS가 구성 되지 않은 경우이 스냅숏을 사용 하지 않습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*가상 컴퓨터 연결을 사용 하 여 가상 컴퓨터에 integration services를 설치 합니다.*  
  


