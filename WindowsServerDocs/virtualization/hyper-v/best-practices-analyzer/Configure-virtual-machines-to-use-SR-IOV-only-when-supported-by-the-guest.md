---
title: 게스트 운영 체제에서 지 원하는 경우에 SR-IOV를 사용 하 여 가상 컴퓨터 구성
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 33cf5b68-e43e-47ef-adbc-6b266c1d4dce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e5c2acb21fe8b11e8f020c6d2ab1742116c23b28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833364"
---
# <a name="configure-virtual-machines-to-use-sr-iov-only-when-supported-by-the-guest-operating-system"></a>게스트 운영 체제에서 지 원하는 경우에 SR-IOV를 사용 하 여 가상 컴퓨터 구성

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
*하나 이상의 가상 컴퓨터는 단일 루트 I/O 가상화 (SR-IOV)를 사용 하도록 구성 되어 있지만 게스트 운영 체제는 SR-IOV를 지원 하지 않습니다.*  
  
## <a name="impact"></a>영향  
*SR-IOV 가상 함수는 다음 가상 컴퓨터에 할당 되지 않습니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*SR-IOV를 지원 하지 않는 게스트 운영 체제를 실행 하는 모든 가상 머신에서 SR-IOV를 사용 하지 않도록 설정 합니다.*  
  
SR-IOV는 64 비트 Windows 게스트 일부 에서만에서 지원 됩니다. 자세한 내용은 다음을 참조 하십시오. [생성 및 게스트에서 Hyper-v 기능 호환성](../Hyper-V-feature-compatibility-by-generation-and-guest.md)합니다.  
  


