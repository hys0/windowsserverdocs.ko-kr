---
title: 섹터 크기가 가상 하드 디스크 파일을 저장 하는 물리적 스토리지의 섹터 크기 보다 작은 가상 하드 디스크를 사용 하지 마십시오
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b7cf994e-bf4b-4b1b-bad6-ecf7d46d105e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f7ea02ab83d3d896d2ad3681526133e23725b819
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857706"
---
# <a name="avoid-using-virtual-hard-disks-with-a-sector-size-less-than-the-sector-size-of-the-physical-storage-that-stores-the-virtual-hard-disk-file"></a>섹터 크기가 가상 하드 디스크 파일을 저장 하는 물리적 스토리지의 섹터 크기 보다 작은 가상 하드 디스크를 사용 하지 마십시오

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**체제별** <br />**컴퓨터**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제**  
*하나 이상의 가상 하드 디스크의 물리적 섹터 크기가 가상 하드 디스크 파일이 있는 저장소의 물리적 섹터 크기 보다 작습니다.*  
  
## <a name="impact"></a>**식**  
*가상 하드 디스크를 사용 하는 응용 프로그램 또는 가상 컴퓨터에서 성능 문제가 발생할 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*다음 중 하나를 수행 합니다.*  
  
-   *저장소 마이그레이션을 수행 하 여 가상 하드 디스크를 새 물리적 시스템으로 이동*  
  
-   *Windows PowerShell 또는 WMI를 사용 하 여 VHDX 형식의 가상 하드 디스크를 사용 하도록 설정 하 여 특정 섹터 크기를 보고 합니다.*  
  
-   *레지스트리 설정을 사용 하 여 VHD 형식의 가상 하드 디스크가 4k의 물리적 섹터 크기를 보고 하도록 설정 합니다.*  
  


