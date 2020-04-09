---
title: 가상 스위치에 바인딩된 팀 인터페이스는 기본 모드에 있어야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: fe19de5dd380d08c01c917da9d4e2ef9465de042
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854606"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>가상 스위치에 바인딩된 팀 인터페이스는 기본 모드에 있어야 합니다.

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
*일부 가상 스위치는 팀 인터페이스에 바인딩되므로 팀 인터페이스는 모든 Vlan의 트래픽을 가상 스위치로 전달 하지 않습니다.*  
  
## <a name="impact"></a>**식**  
*다음 가상 스위치는 모든 Vlan에 대 한 액세스 권한을 가질 수 없습니다. \n{0}*  
  
## <a name="resolution"></a>**해결 방법**  
*서버 관리자 또는 Windows PowerShell cmdlet NetLbfoTeamNic를 사용 하 여 팀 인터페이스를 기본 모드로 다시 설정 합니다.*  
  


