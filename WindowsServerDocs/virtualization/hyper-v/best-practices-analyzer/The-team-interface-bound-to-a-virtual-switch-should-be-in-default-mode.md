---
title: 가상 스위치에 바인딩된 팀 인터페이스 기본 모드 여야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 22e5ad0eed6e6ea07a83150762b76163442f2c5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872164"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>가상 스위치에 바인딩된 팀 인터페이스 기본 모드 여야 합니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제점**  
*일부 가상 스위치 팀 인터페이스에 바인딩되어 있지만 팀 인터페이스를 가상 스위치에 모든 Vlan에서 트래픽을 전달 하지 않습니다.*  
  
## <a name="impact"></a>**Impact**  
*다음 가상 스위치는 모든 Vlan에 대 한 액세스를 사용할 수 없습니다: \n{0}*  
  
## <a name="resolution"></a>**해결 방법**  
*서버 관리자를 사용 하 여 또는 집합 NetLbfoTeamNic Windows PowerShell cmdlet를 기본 모드로 팀 인터페이스를 다시 설정 합니다.*  
  


