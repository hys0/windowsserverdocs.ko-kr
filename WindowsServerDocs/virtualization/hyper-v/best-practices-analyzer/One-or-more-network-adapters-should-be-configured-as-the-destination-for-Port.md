---
title: 하나 이상의 네트워크 어댑터 포트 미러링에 대 한 대상으로 구성 해야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b83c166d-f010-47c4-a4bb-02167f2e3361
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b0b9ce90c9614332ca12ddb6a1467d38425d6ddf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861876"
---
# <a name="one-or-more-network-adapters-should-be-configured-as-the-destination-for-port-mirroring"></a>하나 이상의 네트워크 어댑터 포트 미러링에 대 한 대상으로 구성 해야

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
*하나 이상의 가상 컴퓨터에 포트 미러링의 원본으로 구성 된 네트워크 어댑터가 있지만 가상 스위치에 해당 대상이 없습니다.*  
  
## <a name="impact"></a>**식**  
*다음 가상 스위치 및 가상 컴퓨터에 대해 포트 미러링이 제대로 작동 하지 않습니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*Windows PowerShell 또는 Hyper-v 관리자를 사용 하 여 포트 미러링 구성을 완료 하거나 수정 합니다.*  
  


