---
title: 가상 컴퓨터는 동적 확장 가상 하드 디스크를 사용 하는 경우 충분 한 실제 디스크 공간을 사용할 수 있도록
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9e3e3e64-4b3a-4b9d-acf1-e4df61a04f1e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 53302d9e8fc4f960f0a1744d4ebd274b936eac5f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861946"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-dynamically-expanding-virtual-hard-disks"></a>가상 컴퓨터는 동적 확장 가상 하드 디스크를 사용 하는 경우 충분 한 실제 디스크 공간을 사용할 수 있도록

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*하나 이상의 가상 컴퓨터에서 동적 확장 가상 하드 디스크를 사용 하 고 있습니다.*  
  
## <a name="impact"></a>영향  
*동적 확장 가상 하드 디스크는 가상 하드 디스크에 대 한 쓰기가 발생 하는 경우 공간을 할당할 수 있도록 호스팅 볼륨의 사용 가능한 공간을 필요로 합니다. 사용 가능한 공간을 모두 사용 하는 경우 실제 저장소에 의존 하는 모든 가상 머신이 영향을 받을 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*사용 가능한 디스크 공간을 모니터링 하 여 확장에 사용할 수 있는 공간이 충분 한지 확인 합니다. 가상 컴퓨터를 종료 하 고 Hyper-v 관리자에서 디스크 편집 마법사를 사용 하 여이 가상 컴퓨터에 대 한 동적 확장 가상 하드 디스크를 고정 크기의 가상 하드 디스크로 변환 하는 것이 좋습니다.*  
  


