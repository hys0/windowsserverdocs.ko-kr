---
title: 복제 트래픽에 대 한 압축을 권장 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 77a314e816c36f626ea3edb10b80f65e3897e7c5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365105"
---
# <a name="compression-is-recommended-for-replication-traffic"></a>복제 트래픽에 대 한 압축을 권장 합니다.

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
*네트워크를 통해 주 서버에서 복제 서버로 전송 되는 복제 트래픽이 압축 되지 않습니다.*  
  
## <a name="impact"></a>영향  
*복제 트래픽이 필요한 것 보다 더 많은 대역폭을 사용 합니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
@no__t-가상 머신 목록 >  
  
## <a name="resolution"></a>해결 방법  
@no__t hyper-v 관리자에서 가상 컴퓨터에 대 한 설정의 네트워크를 통해 전송 되는 데이터를 압축 하도록 Hyper-v 복제본을 구성 합니다. Hyper-v 외부의 도구를 사용 하 여 압축을 수행할 수도 있습니다. *  
  


