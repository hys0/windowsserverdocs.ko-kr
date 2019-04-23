---
title: 장애 조치 시 사용 하 여 복제 가상 컴퓨터를 장애 조치 TCP/IP 설정을 구성합니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c16fbc95c9d679611d57327992a6621d58d4e201
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855754"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>장애 조치 시 사용 하 여 복제 가상 컴퓨터를 장애 조치 TCP/IP 설정을 구성합니다

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
*고정 IP 주소를 사용 하 여 구성 하는 복제본 가상 컴퓨터가 장애 조치의 경우 상응 주 가상 컴퓨터에서에서 다른 IP 주소를 사용 하도록 구성 되어야 합니다.*  
  
## <a name="impact"></a>영향  
*주 가상 컴퓨터를 지 원하는 작업을 사용 하 여 클라이언트 장애 조치 후 복제본 가상 컴퓨터에 연결할 못할 수 있습니다. 또한 기본 가상 컴퓨터의 원래 IP 주소 올바르지 않을 경우 복제본 가상 컴퓨터 네트워크 토폴로지에서 합니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*복제본 가상 머신이 장애 조치 시 사용 해야 하는 IP 주소를 구성 하려면 Hyper-v 관리자를 사용 합니다.*  
  


