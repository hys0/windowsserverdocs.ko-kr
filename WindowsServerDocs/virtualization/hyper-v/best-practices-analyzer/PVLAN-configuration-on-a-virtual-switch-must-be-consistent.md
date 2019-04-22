---
title: PVLAN 구성 가상 스위치에는 일치 해야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4db63bcc-7a54-4f19-98a6-c274c3956d51
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: b7d6d068027aa9497b00138bd1d889ea86aa3308
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813254"
---
# <a name="pvlan-configuration-on-a-virtual-switch-must-be-consistent"></a>PVLAN 구성 가상 스위치에는 일치 해야 합니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016| 
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>**문제점**  
*개인 가상 로컬 영역 네트워크 PVLAN ()는 하나 이상의 가상 네트워크 어댑터에 올바르게 구성 되지 않았습니다.*  
  
## <a name="impact"></a>**Impact**  
*PVLAN 가상 컴퓨터 간에 네트워크 트래픽을 올바르게 격리 될 수 있습니다.*  
  
## <a name="resolution"></a>**해결 방법**  
*Windows PowerShell cmdlet, Set-vmnetworkadaptervlan를 사용 하 여 PVLAN을 올바르게 구성.*  
  


