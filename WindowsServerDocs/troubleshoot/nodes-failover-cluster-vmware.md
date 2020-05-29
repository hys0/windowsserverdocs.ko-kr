---
title: 활성 장애 조치 (failover) 클러스터 구성원에서 노드 제거
description: 이 문서에서는 활성 장애 조치 (failover) 클러스터 멤버 자격에서 제거 된 노드를 찾는 문제를 해결 합니다.
ms.prod: windows-server
ms.technology: server-general
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 6613bf09c3588637cfe03cb7647e4fed358b760c
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150331"
---
# <a name="nodes-being-removed-from-failover-cluster-membership-on-vmware-esx"></a>VMWare ESX의 장애 조치 (Failover) 클러스터 구성원에서 제거 되는 노드

이 문서에서는 노드가 VMWare ESX에 호스트 되는 경우 활성 장애 조치 (failover) 클러스터 멤버 자격에서 제거 된 노드를 찾는 문제를 해결 합니다.

## <a name="symptom"></a>증상

문제가 발생 하면 이벤트 뷰어의 시스템 이벤트 로그에 표시 됩니다.

![이벤트 1135](media/nodes-failover-cluster-vmware/1135.png)

## <a name="resolution"></a>해결 방법

인바운드 버퍼가 너무 적게 설정 되어 많은 양의 트래픽을 처리할 수 없기 때문에 VMXNET3 어댑터에서 인바운드 네트워크 패킷을 삭제 하는 한 가지 문제가 있습니다. 성능 모니터를 사용 하 여 "Network Interface\Packets Received 버렸습니다" 카운터를 살펴보면 이것이 문제 인지 쉽게 확인할 수 있습니다.

![카운터 추가](media/nodes-failover-cluster-vmware/0527.png)

이 카운터를 추가한 후 평균, 최소 및 최대 수를 확인 하 고 0 보다 큰 값 이면 수신 버퍼를 어댑터에 맞게 조정 해야 합니다. 이 문제는 VMWare의 기술 자료에 설명 되어 있습니다. [VMXNET3 vNIC/4.x의 게스트 OS 수준에서 큰 패킷 손실](https://kb.vmware.com/s/article/2039495)입니다.
