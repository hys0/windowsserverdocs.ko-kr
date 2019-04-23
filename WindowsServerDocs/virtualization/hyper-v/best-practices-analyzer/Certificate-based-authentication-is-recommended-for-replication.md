---
title: 복제에 대 한 인증서 기반 인증 것이 좋습니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5bd131b48b009b43b6379f72f370b4179dea5a03
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873064"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>복제에 대 한 인증서 기반 인증 것이 좋습니다.

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
*Kerberos 인증에 대 한 복제를 위해 선택 하는 하나 이상의 가상 컴퓨터 구성 됩니다.*  
  
## <a name="impact"></a>**Impact**  
*복제 서버에 주 서버에서 복제 네트워크 트래픽은 암호화 되지 않습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*또 다른 방법은 암호화 하는 데 사용 중인 경우이 무시할 수 있습니다. 이 고, 그렇지 인증서 기반 인증을 선택 하려면 가상 머신 설정을 수정 합니다.*  
  


