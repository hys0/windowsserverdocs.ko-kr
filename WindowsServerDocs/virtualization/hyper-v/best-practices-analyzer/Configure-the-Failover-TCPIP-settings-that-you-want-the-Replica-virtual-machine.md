---
title: 장애 조치 시 사용 하 여 복제 가상 컴퓨터를 장애 조치 TCP/IP 설정을 구성합니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3f2681694d87b34369b29be6216ebec9210c6024
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366293"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>장애 조치 시 사용 하 여 복제 가상 컴퓨터를 장애 조치 TCP/IP 설정을 구성합니다

>적용 대상: Windows Server 2016
 
모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>문제점  
*고정 IP 주소로 구성 된 복제본 가상 컴퓨터는 장애 조치 (failover) 시 해당 주 가상 컴퓨터와 다른 IP 주소를 사용 하도록 구성 해야 합니다.*  
  
## <a name="impact"></a>영향  
*주 가상 머신에서 지원 되는 워크 로드를 사용 하는 클라이언트는 장애 조치 (failover) 후 복제본 가상 머신에 연결 하지 못할 수 있습니다. 또한 주 가상 컴퓨터의 원래 IP 주소는 복제본 가상 컴퓨터 네트워크 토폴로지에서 유효 하지 않습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해결 방법  
*Hyper-v 관리자를 사용 하 여 장애 조치 (failover) 시 복제본 가상 컴퓨터에서 사용 해야 하는 IP 주소를 구성 합니다.*  
  


