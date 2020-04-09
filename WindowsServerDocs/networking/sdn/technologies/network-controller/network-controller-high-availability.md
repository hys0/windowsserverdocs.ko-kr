---
title: 네트워크 컨트롤러 고가용성
description: 이 항목을 사용 하 여 Windows Server 2016에서 SDN (소프트웨어 정의 네트워킹)의 네트워크 컨트롤러 고가용성에 대해 알아볼 수 있습니다.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 334b090d-bec4-4e67-8307-13831dbdd1d8
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: 3c6d18dcf1071eabaabe9acc29713a7b9a226a84
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859656"
---
# <a name="network-controller-high-availability"></a>네트워크 컨트롤러 고가용성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 소프트웨어 정의 네트워킹 \(SDN\)의 네트워크 컨트롤러 고가용성 및 확장성 구성에 대해 알아볼 수 있습니다.

데이터 센터에 SDN을 배포 하는 경우 네트워크 컨트롤러를 사용 하 여 RAS 게이트웨이, 소프트웨어 부하 분산 장치, 테 넌 트 통신에 대 한 가상 네트워킹 정책, 데이터 센터 방화벽 정책 \(, SDN 정책의 QoS\), 하이브리드 네트워킹 정책 등을 비롯 한 여러 네트워크 요소를 중앙에서 배포, 모니터링 및 관리할 수 있습니다.

네트워크 컨트롤러는 SDN 관리의 cornerstone 때문에 네트워크 컨트롤러 배포에서 고가용성을 제공 하 고, 데이터 센터 요구에 맞게 네트워크 컨트롤러 노드를 쉽게 확장 하거나 축소할 수 있는 기능을 제공 하는 것이 중요 합니다.

네트워크 컨트롤러를 단일 컴퓨터 클러스터로 배포할 수 있지만 고가용성 및 장애 조치 (failover)를 위해 최소 3 대의 컴퓨터를 사용 하는 다중 컴퓨터 클러스터에 네트워크 컨트롤러를 배포 해야 합니다.

>[!NOTE]
>서버 컴퓨터 또는 Windows Server 2016 Datacenter edition을 실행 하는 가상 컴퓨터 \(Vm\)에서 네트워크 컨트롤러를 배포할 수 있습니다. Vm에 네트워크 컨트롤러를 배포 하는 경우에는 Datacenter edition을 실행 하는 Hyper-v 호스트에서 Vm이 실행 되 고 있어야 합니다. Windows Server 2016 Standard edition에서는 네트워크 컨트롤러를 사용할 수 없습니다.

## <a name="network-controller-as-a-service-fabric-application"></a>Service Fabric 응용 프로그램으로 서의 네트워크 컨트롤러

고가용성 및 확장성을 얻기 위해 네트워크 컨트롤러는 Service Fabric에 의존 합니다. Service Fabric는 확장 가능 하 고 안정적 이며 쉽게 관리 되는 응용 프로그램을 빌드하기 위한 분산 시스템 플랫폼을 제공 합니다.

플랫폼으로 Service Fabric 확장 가능한 분산 시스템을 구축 하는 데 필요한 기능을 제공 합니다. 여러 운영 체제 인스턴스에서 서비스 호스팅을 제공 하 고, 인스턴스 간의 상태 정보를 동기화 하 고, 리더로 선택 a 리더, 오류 검색, 부하 분산 등을 제공 합니다.

>[!NOTE]
>Azure의 Service Fabric에 대 한 자세한 내용은 [azure Service Fabric 개요](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview)를 참조 하세요.

여러 컴퓨터에 네트워크 컨트롤러를 배포 하는 경우 네트워크 컨트롤러는 Service Fabric 클러스터에서 단일 Service Fabric 응용 프로그램으로 실행 됩니다. 운영 체제 인스턴스 집합을 연결 하 여 Service Fabric 클러스터를 구성할 수 있습니다.

네트워크 컨트롤러 응용 프로그램은 여러 상태 저장 Service Fabric 서비스로 구성 됩니다. 각 서비스는 실제 네트워크 관리, 가상 네트워크 관리, 방화벽 관리 또는 게이트웨이 관리와 같은 네트워크 기능을 담당 합니다. 

각 Service Fabric 서비스에는 하나의 주 복제본과 두 개의 보조 복제본이 있습니다. 주 서비스 복제본은 요청을 처리 하는 반면, 두 보조 서비스 복제본은 몇 가지 이유로 주 복제본을 사용 하지 않도록 설정 하거나 사용할 수 없는 경우 고가용성을 제공 합니다.

다음 그림은 5 대의 컴퓨터를 포함 하는 네트워크 컨트롤러 Service Fabric 클러스터를 보여 줍니다. 5 대의 컴퓨터에 배포 되는 4 개의 서비스: 방화벽 서비스, 게이트웨이 서비스, 소프트웨어 부하 분산 \(SLB\) 서비스 및 가상 네트워크 \(Vnet\) 서비스.  각각의 네 가지 서비스에는 하나의 기본 서비스 복제본과 두 개의 보조 서비스 복제본이 포함 됩니다.

![네트워크 컨트롤러 Service Fabric 클러스터](../../../media/Network-Controller-HA/Network-Controller-HA.jpg)

## <a name="advantages-of-using-service-fabric"></a>Service Fabric 사용의 이점

네트워크 컨트롤러 클러스터에 Service Fabric를 사용 하는 경우의 주요 이점은 다음과 같습니다.

### <a name="high-availability-and-scalability"></a>고가용성 및 확장성

네트워크 컨트롤러는 데이터 센터 네트워크의 핵심 이므로 오류에 대 한 복원 력을 보장 하 고 시간 경과에 따라 데이터 센터 네트워크의 민첩 한 변화를 수용할 수 있을 만큼 확장 가능 해야 합니다. 다음 기능은 이러한 기능을 제공 합니다. 

- **빠른 장애 조치 (failover)** . Service Fabric은 매우 빠른 장애 조치 (failover)를 제공 합니다. 여러 핫 보조 서비스 복제본을 항상 사용할 수 있습니다. 하드웨어 오류로 인해 운영 체제 인스턴스를 사용할 수 없게 되 면 보조 복제본 중 하나가 주 복제본으로 즉시 승격 됩니다. 
- **규모의 민첩성**. 리소스 요구 사항에 따라 몇 가지 인스턴스에서 최대 수천 개의 인스턴스로 이러한 신뢰할 수 있는 서비스를 쉽고 빠르게 확장할 수 있습니다. 

### <a name="persistent-storage"></a>영구 스토리지

네트워크 컨트롤러 응용 프로그램의 구성 및 상태에 대 한 저장소 요구 사항이 크게 설정 되어 있습니다. 또한 응용 프로그램은 계획 되거나 계획 되지 않은 중단에서 사용할 수 있어야 합니다. 이러한 목적을 위해 Service Fabric는 복제 된 트랜잭션 및 지속형 저장소 인 키-값 저장소 \(KVS\)를 제공 합니다.

### <a name="modularity"></a>성과

네트워크 컨트롤러는 모듈형 아키텍처를 사용 하 여 설계 되었으며, 각 네트워크 서비스 (예: 가상 네트워크 서비스 및 방화벽 서비스)가 개별 서비스로\-빌드 되었습니다. 

이 응용 프로그램 아키텍처는 다음과 같은 이점을 제공 합니다.

1. 네트워크 컨트롤러 모듈화를 사용 하면 지원 되는 각 서비스를 독립적으로 개발할 수 있습니다. 예를 들어 다른 서비스 또는 네트워크 컨트롤러의 정상적인 작동에 영향을 주지 않고 소프트웨어 부하 분산 서비스를 업데이트할 수 있습니다.
2. 네트워크 컨트롤러 모듈화를 통해 네트워크가 진화 함에 따라 새 서비스를 추가할 수 있습니다. 기존 서비스에 영향을 주지 않고 새 서비스를 네트워크 컨트롤러에 추가할 수 있습니다.

>[!NOTE]
>Windows Server 2016에서는 타사 서비스를 네트워크 컨트롤러에 추가 하는 것이 지원 되지 않습니다.

Service Fabric 모듈화는 서비스 모델 스키마를 사용 하 여 응용 프로그램 개발, 배포 및 서비스의 용이성을 최대화 합니다.

## <a name="network-controller-deployment-options"></a>네트워크 컨트롤러 배포 옵션

VMM\)\(System Center Virtual Machine Manager을 사용 하 여 네트워크 컨트롤러를 배포 하려면 [vmm 패브릭에서 SDN 네트워크 컨트롤러 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)을 참조 하세요.

스크립트를 사용 하 여 네트워크 컨트롤러를 배포 하려면 [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)를 참조 하세요.

Windows PowerShell을 사용 하 여 네트워크 컨트롤러를 배포 하려면 [Windows powershell을 사용 하 여 네트워크 컨트롤러 배포](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md) 를 참조 하세요.

네트워크 컨트롤러에 대 한 자세한 내용은 [네트워크 컨트롤러](Network-Controller.md)를 참조 하세요.