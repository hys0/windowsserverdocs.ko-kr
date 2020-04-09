---
title: 4 개 이하의 가상 프로세서와 함께 Windows 7을 실행 하는 가상 컴퓨터 구성
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8fcf0868-b543-4f94-aee7-35324346da55
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: da58833b33f25a8ce724dcbe46161ae99c8d1224
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862036"
---
# <a name="configure-virtual-machines-running-windows-7-with-no-more-than-4-virtual-processors"></a>4 개 이하의 가상 프로세서와 함께 Windows 7을 실행 하는 가상 컴퓨터 구성

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|오류|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제**  
*Windows 7을 실행 하는 가상 머신은 4 개 이상의 가상 프로세서로 구성 됩니다.*  
  
## <a name="impact"></a>**식**  
*Microsoft는 다음과 같은 가상 컴퓨터의 구성을 지원 하지 않습니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*가상 컴퓨터를 종료 하 고 하나 이상의 가상 프로세서를 제거 합니다.*  
  
#### <a name="to-remove-virtual-processors"></a>가상 프로세서를 제거 하려면  
  
1.  Hyper-V 관리자를 엽니다. **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **Hyper-V 관리자**를 클릭합니다.  
  
2.  결과 창에서 아래 **가상 컴퓨터**, 구성 하려는 가상 컴퓨터를 선택 합니다. 으로 가상 컴퓨터의 상태를 표시 해야 **오프**합니다. 그렇지 않은 경우 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **종료**합니다.  
  
3.  **작업** 창의 가상 컴퓨터 이름에서 **설정**을 클릭합니다.  
  
4.  탐색 창에서 **프로세서**합니다.  
  
5.  에 **프로세서** 페이지, 프로세서 수를 설정 **3** 클릭 하 고 **확인**합니다.  
  


