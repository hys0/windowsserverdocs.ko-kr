---
title: 네트워크 어댑터가 여러 개 사용 가능 해야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6b043900c6fde4522e5805a1f0c1a635de335e31
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364803"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>네트워크 어댑터가 여러 개 사용 가능 해야 합니다.

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  

다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.

## <a name="issue"></a>문제점  
  
*이 서버는 단일 네트워크 어댑터를 사용 하 여 구성 되며, 관리 운영 체제와 실제 네트워크에 액세스 해야 하는 모든 가상 컴퓨터에서 공유 되어야 합니다.*  
  
## <a name="impact"></a>영향  
  
*관리 운영 체제에서 네트워킹 성능이 저하 될 수 있습니다.*  
  
## <a name="resolution"></a>해결 방법  
  
*이 컴퓨터에 네트워크 어댑터를 더 추가 합니다. 관리 운영 체제에서 단독 사용을 위해 하나의 네트워크 어댑터를 예약 하려면 외부 가상 네트워크에서 사용할 수 있도록 네트워크 어댑터를 구성 하지 마십시오.*  
  
컴퓨터에 네트워크 어댑터를 추가 하는 방법에 대 한 정보를 컴퓨터 또는 네트워크 어댑터에 대 한 설명서를 참조 하십시오. 그런 다음이 관리 운영 체제에 대 한 단독으로 예약 하려면 하지에 연결할 가상 스위치.   
  


