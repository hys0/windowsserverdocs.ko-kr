---
title: 가상 컴퓨터는 SR-IOV를 사용 하도록 구성 된 경우 가상 함수 드라이버 올바르게 작동 하는지 확인 하십시오.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8d3d0a5008b55d4823cef9a8dd2a7bce4a6a2a33
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852084"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>가상 컴퓨터는 SR-IOV를 사용 하도록 구성 된 경우 가상 함수 드라이버 올바르게 작동 하는지 확인 하십시오.

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
*가상 함수 드라이버 하나 이상의 가상 컴퓨터의 게스트 운영 체제에서 올바르게 작동 하지 않습니다.*  
  
## <a name="impact"></a>영향  
*네트워킹 성능 다음 가상 컴퓨터에 최적이 아닙니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*게스트 운영 체제에서 다음을 수행 합니다. 적절 한 드라이버가 설치 되 고 모든 네트워킹 장치가 활성화 되었으며 확인 오류나 경고에 대 한 이벤트 로그를 확인 합니다.*  
  


