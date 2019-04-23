---
title: 가상 블록 사이의 차이점 보관용 디스크 또는 동적 가상 하드 디스크의 실제 디스크 섹터 맞춤 불일치를 방지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4973c199a5507d00e15da8f621a09f0c602a29fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833864"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>가상 블록 사이의 차이점 보관용 디스크 또는 동적 가상 하드 디스크의 실제 디스크 섹터 맞춤 불일치를 방지

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*하나 이상의 가상 하드 디스크에 대 한 맞춤 불일치가 발견 되었습니다.*  
  
### <a name="impact"></a>영향  
*가상 하드 디스크에 저장 된 경우 물리적 디스크 섹터 크기가 4k, 가상 머신 또는 가상 하드 디스크를 사용 하는 응용 프로그램의 성능 문제가 발생할 수 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*가상 하드 디스크 만들기 마법사를 사용 하 여 새 VHD 형식 또는 VHDX 형식의 가상 하드 디스크를 만들고 원본 디스크와 기존 가상 하드 디스크를 지정 합니다. 새 가상 하드 디스크는 가상 블록 및 실제 디스크 간 정렬을 사용 하 여 만들어집니다.*  
  


