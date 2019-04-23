---
title: 가상 컴퓨터에 대해 구성 된 모든 가상 네트워크 어댑터를 사용 하도록 설정
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: fbb1ef5283f6ccf8dfa355a09a86040be80f53e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844234"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>가상 컴퓨터에 대해 구성 된 모든 가상 네트워크 어댑터를 사용 하도록 설정

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*가상 컴퓨터에서 하나 이상의 네트워크 어댑터를 비활성화할 수 있습니다.*  
  
## <a name="impact"></a>영향  
  
*다음 가상 컴퓨터 네트워크 연결이 없을 수 있습니다.*  
  
\<가상 머신 이름 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*모든 가상 네트워크 어댑터를 사용 하도록 설정 하려면 게스트 운영 체제에서 장치 관리자를 사용 합니다. 어댑터가 필요 하지 않은 경우 Hyper-v 관리자를 사용 하 여 가상 컴퓨터에서 제거 합니다.*  
  

