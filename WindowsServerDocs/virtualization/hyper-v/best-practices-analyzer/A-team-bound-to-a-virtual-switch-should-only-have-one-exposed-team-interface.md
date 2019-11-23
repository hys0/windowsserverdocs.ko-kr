---
title: 가상 스위치에 바인딩된 팀 하나의 노출 된 팀 인터페이스 하나만
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1074f086-1a2e-42e1-b58c-f55e657d5ce1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6baa9e4ae900c9b671003872b4eb4589efb2f085
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365402"
---
# <a name="a-team-bound-to-a-virtual-switch-should-only-have-one-exposed-team-interface"></a>가상 스위치에 바인딩된 팀 하나의 노출 된 팀 인터페이스 하나만

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
*하나 이상의 가상 스위치는 여러 팀 인터페이스가 있는 팀에 바인딩되어 있습니다.*  
  
## <a name="impact"></a>**식**  
*다음 가상 스위치는 Vlan 및 다른 팀 인터페이스에서 사용 하는 대역폭에 대 한 액세스 권한이 없을 수 있습니다.*  
  
\<가상 스위치 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*Windows PowerShell cmdlet NetLbfoTeamNic를 사용 하 여 기본 팀 인터페이스가 아닌 팀에서 모든 팀 인터페이스를 제거 합니다.*  
  


