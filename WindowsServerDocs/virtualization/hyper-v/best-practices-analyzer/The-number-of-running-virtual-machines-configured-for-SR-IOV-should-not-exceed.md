---
title: SR-IOV에 대 한 구성 된 가상 컴퓨터를 실행할 수 있는 가상 컴퓨터에 사용할 수 있는 가상 함수의 수를 넘지 않아야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e63df9283927437f9cfc62c052d83b07fe599b34
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829754"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>SR-IOV에 대 한 구성 된 가상 컴퓨터를 실행할 수 있는 가상 컴퓨터에 사용할 수 있는 가상 함수의 수를 넘지 않아야

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
*않습니다 충분히 가상 함수를 실행 중인 단일 루트 I/O 가상화 (SR-IOV)에 대해 구성 된 가상 컴퓨터 수에 대해 사용할 수 있습니다.*  
  
## <a name="impact"></a>영향  
*네트워킹 성능 다음 가상 컴퓨터에 적합 하지 않을 수 있습니다.*  
   
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*SR-IOV 가상 함수를 필요로 하지 않는 하나 이상의 가상 머신에서 SR-IOV를 사용 하지 않도록 설정 하는 것이 좋습니다.*  
  


