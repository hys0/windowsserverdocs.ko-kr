---
title: 이 서버에서 복제는 하나 이상의 가상 컴퓨터에 대 한 일시 중지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: e1119a40-eda3-4058-8648-7df81cbc6c29
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 17d50f116c6cee488367c924bfbce3791a8d879f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393535"
---
# <a name="replication-is-paused-for-one-or-more-virtual-machines-on-this-server"></a>이 서버에서 복제는 하나 이상의 가상 컴퓨터에 대 한 일시 중지

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*하나 이상의 가상 컴퓨터에 대해 복제가 일시 중지 되었습니다. 주 가상 컴퓨터가 일시 중지 된 동안에는 발생 하는 모든 변경 내용이 누적 되며 복제가 다시 시작 되 면 복제본 가상 컴퓨터로 전송 됩니다.*  
  
## <a name="impact"></a>영향  
*복제가 일시 중지 되는 동안 주 가상 머신에서 발생 하는 누적 된 변경 내용은 주 서버에서 사용 가능한 디스크 공간을 사용 합니다. 복제를 다시 시작한 후에는 복제 서버에 대 한 네트워크 트래픽이 많이 발생할 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해결 방법  
*복제 일시 중지가 의도 된 것인지 확인 합니다. 디스크 공간이 부족 하거나 네트워크 연결을 해결 하기 위해 복제가 일시 중지 된 경우 해당 문제가 해결 되는 즉시 복제를 다시 시작 합니다.*  
  


