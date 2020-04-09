---
title: 가상 블록 사이의 차이점 보관용 디스크 또는 동적 가상 하드 디스크의 실제 디스크 섹터 맞춤 불일치를 방지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 3f090f015f2179ba372e56d580477ef8d72d977f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857806"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>가상 블록 사이의 차이점 보관용 디스크 또는 동적 가상 하드 디스크의 실제 디스크 섹터 맞춤 불일치를 방지

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
*하나 이상의 가상 하드 디스크에 대 한 맞춤 불일치가 검색 되었습니다.*  
  
### <a name="impact"></a>영향  
*가상 하드 디스크가 섹터 크기가 4K 인 실제 디스크에 저장 된 경우 가상 하드 디스크를 사용 하는 응용 프로그램 또는 가상 컴퓨터에 성능 문제가 발생할 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*가상 하드 디스크 만들기 마법사를 사용 하 여 새 VHD 형식 또는 VHDX 형식의 가상 하드 디스크를 만들고 원본 디스크로 기존 가상 하드 디스크를 지정 합니다. 가상 블록과 실제 디스크를 정렬 하 여 새 가상 하드 디스크를 만듭니다.*  
  


