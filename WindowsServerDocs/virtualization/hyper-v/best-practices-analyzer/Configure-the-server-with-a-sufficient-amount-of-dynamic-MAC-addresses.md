---
title: 동적 MAC 주소에 대 한 충분 한 양의로 서버 구성
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a2804519-9790-4006-80b6-e990a8f505fe
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 1fe7b34abc8be9777a491a08016627e7b2a66a2a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862046"
---
# <a name="configure-the-server-with-a-sufficient-amount-of-dynamic-mac-addresses"></a>동적 MAC 주소에 대 한 충분 한 양의로 서버 구성

>적용 대상: Windows Server 2016

*이 항목에서는 모범 사례 분석기 검색에서 식별 한 특정 문제를 해결 하기 위한 것입니다. 이 항목의 정보는 Hyper-v 모범 사례 분석기를 실행 하 고이 항목에서 다루는 문제가 발생 한 컴퓨터에만 적용 해야 합니다. 모범 사례 및 검사에 대 한 자세한 내용은 모범 사례 분석기를 참조* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
  
*사용 가능한 동적 MAC 주소 수가 부족 합니다.*  
  
## <a name="impact"></a>영향  
  
*동적 MAC 주소를 사용할 수 없는 경우 동적 MAC 주소를 사용 하도록 구성 된 가상 컴퓨터를 시작할 수 없습니다.*  
  
## <a name="resolution"></a>해상도  
  
*가상 스위치 관리자를 사용 하 여 동적 주소의 범위를 확인 하 고 확장할 수 있습니다.*  
  


