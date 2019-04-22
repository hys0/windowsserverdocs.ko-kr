---
title: 네트워크에서 복제 트래픽을 제한 하는 정책을 구성합니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2c1f1865fa1d611c0b5baaf981140f9807b51458
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818694"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>네트워크에서 복제 트래픽을 제한 하는 정책을 구성합니다

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*되지 않을 수 제한이 네트워크 대역폭의 양에 따라 복제가 사용 되도록 허용 합니다.*  
  
## <a name="impact"></a>영향  
*네트워크 대역폭 복제 트래픽이 다른 중요 한 네트워크 작업에 영향을 주는 의해 완전히 결정 될 수 있습니다. 이 다음 포트에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*다른 메서드를 사용 하 여 네트워크 트래픽을 제한 하는 경우이 무시할 수 있습니다. 복제본 서버의 관련 포트로 네트워크 트래픽을 제한 하는 정책을 구성 하려면 그룹 정책 편집기 사용 하십시오.*  
  
  


