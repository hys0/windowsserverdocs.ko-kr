---
title: 프로덕션 환경에서 서버 작업을 실행 하는 가상 컴퓨터에서 가상 하드 디스크를 차이점 보관용 VHD 포맷을 사용 하지 마십시오
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 272de33d-2708-4679-8564-ee28848a2839
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: a11959266db4c9f3da73123c41a211198f27b9a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857726"
---
# <a name="avoid-using-vhd-format-differencing-virtual-hard-disks-on-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>프로덕션 환경에서 서버 작업을 실행 하는 가상 컴퓨터에서 가상 하드 디스크를 차이점 보관용 VHD 포맷을 사용 하지 마십시오

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제**  
*하나 이상의 가상 컴퓨터에서 VHD 형식의 차이점 보관용 가상 하드 디스크를 사용 합니다.*  
  
## <a name="impact"></a>**식**  
*전원 오류가 발생 하는 경우 VHD 형식 차이점 보관용 가상 하드 디스크에 일관성 문제가 발생할 수 있습니다. 전원 오류가 발생 했을 때 수정 되는 .vhd 파일의 섹터에 대 한 불완전 하거나 잘못 된 업데이트를 실제 디스크에서 수행 하는 경우 일관성 문제가 발생할 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*가상 머신을 종료 하 고 VHD 형식 차이점 보관용 가상 하드 디스크의 체인을 VHDX 형식으로 변환 하거나 체인을 고정 가상 하드 디스크에 병합 합니다. VHDX 형식에는 전원 오류로 인 한 손상 으로부터 디스크를 보호 하는 데 도움이 되는 안정성 메커니즘이 있습니다. 그러나 특정 시점에 이전 버전의 Windows에 연결 될 가능성이 있는 경우에는 가상 하드 디스크를 변환 하지 마십시오. Windows Server 2012 이전의 windows 릴리스는 VHDX 형식을 지원 하지 않습니다.*  
  


