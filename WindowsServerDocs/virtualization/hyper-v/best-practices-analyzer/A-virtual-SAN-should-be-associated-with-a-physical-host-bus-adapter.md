---
title: 가상 SAN 실제 호스트 버스 어댑터와 연결 되어야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 14bca69b-e779-4e90-b5c1-1b015625572f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9e86f8d9b9a4a87fd6457954c3a4723857faac3b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366693"
---
# <a name="a-virtual-san-should-be-associated-with-a-physical-host-bus-adapter"></a>가상 SAN 실제 호스트 버스 어댑터와 연결 되어야 합니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제점**  
*HBA (호스트 버스 어댑터)에 연결 하지 않고 가상 SAN (저장 영역 네트워크)을 구성 했습니다.*  
  
## <a name="impact"></a>**식**  
*구성 된 가상 SAN에 연결 된 가상 파이버 채널 어댑터를 사용 하 여 가상 컴퓨터를 구성 하면 가상 컴퓨터가 시작 되지 않습니다. 이는 다음과 같은 가상 San에 영향을 줍니다.*  
  
  
가상 San의 \<목록 >  
  
  
## <a name="resolution"></a>**해결 방법**  
*호스트 버스 어댑터에 연결 하 여 가상 SAN을 다시 구성 합니다.*  
  
  
  


