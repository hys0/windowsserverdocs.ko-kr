---
title: 네트워크 컨트롤러 고가용성
description: 에 대 한 네트워킹 SDN (소프트웨어) Windows Server 2016에서 네트워크 컨트롤러 고가용성에 알아보려면이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 334b090d-bec4-4e67-8307-13831dbdd1d8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dbd3ae9f4c1f1fc3035fae9ace880046312df2f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813354"
---
# <a name="network-controller-high-availability"></a>네트워크 컨트롤러 고가용성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 사용 하 여 네트워크 컨트롤러 높은 가용성 및 확장성에 대 한 구성을 소프트웨어 정의 네트워킹에 대해 자세히 알아보려면 \(SDN\)합니다.

데이터 센터에서 SDN을 배포 하는 경우 네트워크 컨트롤러 하 여 중앙에서 배포, 모니터링 및 테 넌 트 통신에 대 한 RAS 게이트웨이, 소프트웨어 부하 분산 장치, 가상 네트워킹 정책 등 여러 네트워크 요소를 관리 데이터 센터 방화벽 서비스 품질 정책을 \(QoS\) SDN 정책을, 하이브리드 네트워킹 정책 등입니다.

네트워크 컨트롤러가 SDN 관리의 기초 이므로 수 있습니다. 높은 가용성과 수 있는 기능 쉽게 확장 또는 축소 네트워크 컨트롤러 노드 데이터 센터 요구를 사용 하 여 네트워크 컨트롤러 배포에 대 한 중요 한 것입니다.

단일 컴퓨터 클러스터로 네트워크 컨트롤러를 배포할 수 있지만 최소 3 개의 컴퓨터를 사용 하 여 여러 컴퓨터 클러스터에 네트워크 컨트롤러를 배포 하의 높은 가용성 및 장애 조치 해야 합니다.

>[!NOTE]
>두 서버 컴퓨터 또는 가상 머신에서 네트워크 컨트롤러를 배포할 수 있습니다 \(Vm\) Windows Server 2016 Datacenter edition을 실행 하는입니다. Vm에서 네트워크 컨트롤러를 배포 하는 경우 Vm Datacenter edition도 실행 하는 Hyper-v 호스트에서 실행 되어야 합니다. 네트워크 컨트롤러를 Windows Server 2016 Standard edition에서 사용할 수 없는 경우

## <a name="network-controller-as-a-service-fabric-application"></a>네트워크 컨트롤러를 서비스 패브릭 응용 프로그램

고가용성 및 확장성을 얻으려면 네트워크 컨트롤러는 Service Fabric에서 사용 합니다. Service Fabric 응용 프로그램 쉽게 관리 및 확장 가능한, 안정적으로 작성 하는 분산된 시스템 플랫폼을 제공 합니다.

플랫폼으로 Service Fabric 확장 가능한 분산된 시스템 구축에 필요한 기능을 제공 합니다. 리더, 실패 감지, 부하 분산 등 선택, 인스턴스 간에 상태 정보를 동기화 할 여러 운영 체제 인스턴스에서 호스팅 서비스를 제공 합니다.

>[!NOTE]
>Azure에서 Service Fabric에 대 한 정보를 참조 하세요 [Azure Service Fabric의 개요](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview)합니다.

여러 컴퓨터에서 네트워크 컨트롤러를 배포할 때 Service Fabric 클러스터에서 네트워크 컨트롤러는 단일 Service Fabric 응용 프로그램으로 실행 됩니다. 운영 체제 인스턴스의 집합을 연결 하 여 Service Fabric 클러스터를 구성할 수 있습니다.

네트워크 컨트롤러 응용 프로그램은 여러 상태 저장 서비스 패브릭 서비스의 구성 됩니다. 각 서비스 실제 네트워크 관리, 가상 네트워크 관리, 방화벽 관리 또는 게이트웨이 관리와 같은 네트워크 기능을 담당합니다. 

각 Service Fabric 서비스에는 하나의 주 복제본과 두 개의 보조 복제본에 있습니다. 기본 서비스 복제본 두 보조 서비스 복제본은 주 복제본 인 비활성화 되었거나 사용할 수 없는 이유로 상황에서 고가용성을 제공 하는 동안 요청을 처리 합니다.

다음 그림에서는 5 개의 컴퓨터를 사용 하 여 네트워크 컨트롤러 서비스 패브릭 클러스터를 보여 줍니다. 네 가지 서비스는 5 개의 컴퓨터 간에 분산 됩니다. 소프트웨어 부하 분산 서비스, 게이트웨이 서비스 방화벽 \(SLB\) 서비스 및 가상 네트워크 \(Vnet\) 서비스입니다.  4 개의 서비스 각각 하나의 기본 서비스 복제본과 두 보조 서비스 복제본을 포함합니다.

![네트워크 컨트롤러 서비스 패브릭 클러스터](../../../media/Network-Controller-HA/Network-Controller-HA.jpg)

## <a name="advantages-of-using-service-fabric"></a>Service Fabric을 사용할 때의 장점

다음은 Service Fabric을 사용 하 여 네트워크 컨트롤러 클러스터에 대 한 주요 장점입니다.

### <a name="high-availability-and-scalability"></a>고가용성 및 확장성

네트워크 컨트롤러는 데이터 센터 네트워크의 핵심 이기 때문에 모두 오류에 탄력적으로 대처 하 고 시간이 지남에 따라 데이터 센터 네트워크에서 agile 변경할 수 있도록 충분히 가능 합니다. 다음과 같은 기능이 이러한 기능을 제공합니다. 

- **신속한 장애 조치**합니다. Service Fabric은 매우 빠른 장애 조치를 제공 합니다. 여러 활성 보조 서비스 복제본을 항상 사용할 수 있습니다. 운영 체제 인스턴스를 하드웨어 오류로 인해 사용할 수 없는 경우에 주 복제본에 즉시 승격 됩니다 보조 복제본 중 하나입니다. 
- **눈금의 민첩성**합니다. 쉽고 빠르게 확장할 수 인스턴스 수천 몇 가지 인스턴스에서 이러한 신뢰할 수 있는 서비스 있으며 다음 리소스 요구 사항에 따라 몇 가지 인스턴스로 돌아옵니다. 

### <a name="persistent-storage"></a>영구 저장소

네트워크 컨트롤러 응용 프로그램에는 해당 구성 및 상태에 대 한 대용량 저장소 요구 사항이 있습니다. 응용 프로그램 에서도 사용할 수 있어야 계획적 및 비계획적 정전에서. 이 작업을 위해 Service Fabric은 키-값 저장소를 제공 \(KVS\) 복제, 트랜잭션 및 지속형 저장소입니다.

### <a name="modularity"></a>모듈화

가상 네트워크 서비스와 방화벽 서비스를 빌드할 때에 같은 각 네트워크 서비스를 사용 하 여 모듈식 아키텍처를 사용 하 여 네트워크 컨트롤러는\-에서 개별 서비스로 합니다. 

이 응용 프로그램 아키텍처에는 다음과 같은 이점을 제공합니다.

1. 모듈화와 지원 되는 서비스의 각 독립 개발을 허용 하는 네트워크 컨트롤러 성능은 향상 되어야 합니다. 예를 들어, 다른 서비스 또는 네트워크 컨트롤러의 정상적인 작동에 영향을 주지 않고 소프트웨어 부하 분산 서비스를 업데이트할 수 있습니다.
2. 네트워크 컨트롤러 모듈화 네트워크 진화 함에 따라 새 서비스를 추가할 수 있습니다. 기존 서비스에 영향을 주지 않고 새로운 서비스를 네트워크 컨트롤러에 추가할 수 있습니다.

>[!NOTE]
>Windows Server 2016에서 네트워크 컨트롤러에 타사 서비스를 추가 지원 되지 않습니다.

Service Fabric 모듈화는 개발, 배포 및 응용 프로그램 서비스 편의성을 최대화 하기 위해 서비스 모델 스키마를 사용 합니다.

## <a name="network-controller-deployment-options"></a>네트워크 컨트롤러 배포 옵션

System Center Virtual Machine Manager 사용 하 여 네트워크 컨트롤러 배포 \(VMM\)를 참조 하십시오 [VMM 패브릭에서 SDN 네트워크 컨트롤러 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)합니다.

스크립트를 사용 하 여 네트워크 컨트롤러를 배포 하려면 참조 [소프트웨어 정의 네트워크 인프라를 사용 하 여 스크립트를 배포](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)합니다.

Windows PowerShell을 사용 하 여 네트워크 컨트롤러를 배포 하려면 참조 [Windows PowerShell을 사용 하 여 네트워크 컨트롤러 배포](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)

네트워크 컨트롤러에 대 한 자세한 내용은 참조 하세요. [네트워크 컨트롤러](Network-Controller.md)합니다.