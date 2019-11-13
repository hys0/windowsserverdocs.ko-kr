---
title: 네트워크에서 복제 트래픽을 제한 하는 정책을 구성합니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5b3afd594f56973007a2f0f4318de8a8c7a98209
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365106"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>네트워크에서 복제 트래픽을 제한 하는 정책을 구성합니다

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*복제에서 사용할 수 있는 네트워크 대역폭의 양에는 제한이 없을 수 있습니다.*  
  
## <a name="impact"></a>영향  
*네트워크 대역폭은 복제 트래픽으로 인해 완전히 영향을 받을 수 있으므로 다른 중요 한 네트워크 작업에 영향을 줍니다. 이는 다음 포트에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해결 방법  
*네트워크 트래픽을 제한 하는 다른 방법을 사용 하는 경우이를 무시할 수 있습니다. 그렇지 않으면 그룹 정책 편집기를 사용 하 여 네트워크 트래픽을 복제 서버의 관련 포트로 제한 하는 정책을 구성 합니다.*  
  
  


