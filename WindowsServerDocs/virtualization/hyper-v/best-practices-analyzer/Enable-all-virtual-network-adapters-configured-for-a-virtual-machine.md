---
title: 가상 컴퓨터에 대해 구성 된 모든 가상 네트워크 어댑터를 사용 하도록 설정
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: bdca25be4af41d0f6ddfafe885f8c2b1301b71fb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393652"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>가상 컴퓨터에 대해 구성 된 모든 가상 네트워크 어댑터를 사용 하도록 설정

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*가상 머신에서 하나 이상의 네트워크 어댑터를 사용 하지 않도록 설정할 수 있습니다.*  
  
## <a name="impact"></a>영향  
  
*다음 가상 컴퓨터는 네트워크에 연결 되어 있지 않을 수 있습니다.*  
  
가상 컴퓨터 이름 목록 \<>  
  
## <a name="resolution"></a>해결 방법  
  
*게스트 운영 체제의 Device Manager를 사용 하 여 모든 가상 네트워크 어댑터를 사용 하도록 설정 합니다. 어댑터가 필요 하지 않으면 Hyper-v 관리자를 사용 하 여 가상 머신에서 제거 합니다.*  
  


