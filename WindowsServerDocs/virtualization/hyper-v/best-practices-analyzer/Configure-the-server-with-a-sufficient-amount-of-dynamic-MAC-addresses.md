---
title: 동적 MAC 주소에 대 한 충분 한 양의로 서버 구성
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a2804519-9790-4006-80b6-e990a8f505fe
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: fc444225c38ef7e8605ec328cfe3f8184b2fd307
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870734"
---
# <a name="configure-the-server-with-a-sufficient-amount-of-dynamic-mac-addresses"></a>동적 MAC 주소에 대 한 충분 한 양의로 서버 구성

>적용 대상: Windows Server 2016

*이 항목은 모범 사례 분석기 검사에서 식별 한 특정 문제를 해결 하는 데 사용 됩니다. 이 항목의 정보에 대해 실행 Hyper-v 모범 사례 분석기 했 고이 항목에서 다루는 문제가 발생 하는 컴퓨터에만 적용 해야 합니다. 모범 사례 및 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)합니다.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*사용 가능한 동적 MAC 주소 수가 낮습니다.*  
  
## <a name="impact"></a>영향  
  
*동적 MAC 주소가 없습니다. 사용 가능한 경우 동적 MAC 주소를 사용 하도록 구성 된 가상 컴퓨터를 시작할 수 없습니다.*  
  
## <a name="resolution"></a>해결 방법  
  
*가상 스위치 관리자를 사용 하 여 보고 동적 주소 범위를 확장 합니다.*  
  


