---
title: 복제에 참여 하려면 장애 조치 클러스터의 서버에서에서 구성 하는 Hyper-v 복제본 브로커 있어야
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 921d31aa63bcaaf0946c487d327144f5e29bcfe0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854586"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>복제에 참여 하려면 장애 조치 클러스터의 서버에서에서 구성 하는 Hyper-v 복제본 브로커 있어야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|오류|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*장애 조치 (failover) 클러스터의 경우 Hyper-v 복제본에서 개별 서버 이름 대신 Hyper-v 복제본 브로커 이름을 사용 해야 합니다.*  
  
## <a name="impact"></a>영향  
*가상 컴퓨터가 다른 장애 조치 (failover) 클러스터 노드로 이동 하는 경우 복제를 계속할 수 없습니다.*  
  
## <a name="resolution"></a>해결 방법  
*장애 조치(Failover) 클러스터 관리자를 사용 하 여 Hyper-v 복제본 브로커를 구성 합니다. Hyper-v 관리자에서 복제 구성에서 Hyper-v 복제본 브로커 이름을 서버 이름으로 사용 하는지 확인 합니다.*  
  


