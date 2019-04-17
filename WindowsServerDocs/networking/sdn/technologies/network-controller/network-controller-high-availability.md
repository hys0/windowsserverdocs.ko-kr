---
title: 네트워크 컨트롤러 높은 공급 일
description: 이 항목에 대해 자세히 알아보려면 네트워크 컨트롤러 높은 가용성에 대 한 소프트웨어 정의 네트워킹 (SDN) Windows Server 2016에 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 334b090d-bec4-4e67-8307-13831dbdd1d8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f260f3e4d8ca5fcd998824327478c2fbe3c81875
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-controller-high-availability"></a>네트워크 컨트롤러 높은 공급 일

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

높은 가용성 네트워크 컨트롤러 및 소프트웨어 네트워킹 정의 \(SDN\) 확장성 구성에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.

SDN 데이터 센터에 배포 하는 경우 네트워크 컨트롤러 중앙 배포를 모니터링 하 고 RAS 게이트웨이, 부하 분산 소프트웨어가, 가상 네트워킹 정책 테 통신, 데이터 센터 방화벽 정책, SDN 정책, 네트워킹 정책 하이브리드 등에 \(QoS\) 서비스 품질에 대 한 많은 네트워크 요소 관리에 사용할 수 있습니다.

네트워크 컨트롤러 SDN 관리 초석 때문에 수 있습니다. 높은 가용성와 기능 위나 아래로 네트워크 컨트롤러 노드 배율 쉽게 datacenter 요구 하는 네트워크 컨트롤러 배포 중요 합니다.

하나의 컴퓨터 클러스터로 네트워크 컨트롤러, 배포할 수 있지만 세 컴퓨터 최소화 하 여 여러 기계 클러스터에서 네트워크 컨트롤러를 배포 하 장애 조치를 높이기 위해 해야 합니다.

>[!NOTE]
>네트워크 컨트롤러 중 서버 컴퓨터에 또는 Windows Server 2016 Datacenter 버전을 실행 하는 \(VMs\) 가상 컴퓨터에 배포할 수 있습니다. 네트워크 컨트롤러 Vm에서 배포 하는 경우는 Vm 실행 하는 Datacenter edition도 Hyper-v 호스트에서 실행 합니다. 네트워크 컨트롤러 Windows Server 2016 Standard edition에서 제공 되지 않습니다.

## <a name="network-controller-as-a-service-fabric-application"></a>서비스 패브릭 응용 프로그램으로 네트워크 컨트롤러

네트워크 컨트롤러 높은 사용 가능 시간 및 확장성을 위해 서비스 패브릭 의존 합니다. 서비스 패브릭 분산된 시스템 플랫폼 확장 가능 하 고 안정적인 빌드를 쉽게 관리 하는 응용 프로그램을 제공 합니다.

플랫폼, 서비스 패브릭 확장 분산된 시스템 빌드하는 데 필요한 기능을 제공 합니다. 서비스 호스트 상태 정보 리더, 오류 검색, 부하 분산 등 사용자층 인스턴스 간 동기화 여러 운영 체제 인스턴스에서 제공 됩니다.

>[!NOTE]
>Azure에서 패브릭 서비스에 대 한 내용은 [Azure 서비스 패브릭 개요](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview)합니다.

네트워크 컨트롤러 여러 대의 컴퓨터에 배포 하는 경우 서비스 패브릭 클러스터에서 네트워크 컨트롤러 단일 서비스 패브릭 응용 프로그램으로 실행 됩니다. 서비스 패브릭 클러스터 운영 체제의 집합을 연결 하 여 만들 수 있습니다.

네트워크 컨트롤러 응용 프로그램 여러 안정 된 서비스 패브릭 서비스의 구성 됩니다. 각 서비스에는 물리적 네트워크 관리, 가상 네트워크 관리, 방화벽 관리 게이트웨이 관리 등 네트워크 기능을 담당 합니다. 

각 서비스 패브릭 서비스에 1 주 복제본 및 두 보조 복제 있습니다. 두 보조 서비스 복제 높은 가용성 상황 주 복제본 사용 해제 몇 가지 이유로에서 제공 하는 동안 요청을 처리 하는 기본 서비스의 복제본 합니다.

다음 그림에서는 5 컴퓨터와 네트워크 컨트롤러 서비스 패브릭 클러스터를 보여 줍니다. 네 서비스 5 컴퓨터 분산: 방화벽 서비스, 게이트웨이 서비스, 부하 분산 소프트웨어가 \(SLB\) 서비스 및 네트워크 가상 \(Vnet\) 서비스입니다.  한 주 서비스 복제와 두 보조 서비스 복제본 네 서비스의 각 포함 되어 있습니다.

![네트워크 컨트롤러 서비스 패브릭 클러스터](../../../media/Network-Controller-HA/Network-Controller-HA.jpg)

## <a name="advantages-of-using-service-fabric"></a>서비스 패브릭 사용할 때의 이점

네트워크 컨트롤러 클러스터 서비스 패브릭 사용 되는 주요 이점은 다음과가 같습니다.

### <a name="high-availability-and-scalability"></a>높은 사용 가능 시간 및 확장성

네트워크 컨트롤러 datacenter 네트워크의 핵심 때문에 실패 유연 하 게와 시간이 지남에 따라 datacenter 네트워크가 민첩 변경을 허용 충분히 확장 가능 해야 것입니다. 이러한 기능을 제공 하는 다음과 같은 기능: 

- **빠른 장애**합니다. 서비스 패브릭 초고속 장애 조치를 제공합니다. 여러 핫 보조 서비스 복제본을 항상 사용할 수 있습니다. 운영 체제 인스턴스를 하드웨어 오류로 인해 사용할 수 없는 경우 기본 복제도 확장 즉시 않습니다 보조 복제본 중 하나입니다. 
- **규모의 유연성**합니다. 쉽고 빠르게 이러한 신뢰할 수 있는 서비스에서 몇 가지 인스턴스 인스턴스 수천 최대 크기를 조정 하 했다가 다시 경우도 리소스 요구에 따라 합니다. 

### <a name="persistent-storage"></a>영구 저장소

네트워크 컨트롤러 응용 프로그램 해당 구성과 상태에 대 한 많은 메모리 요구 사항이 있습니다. 응용 프로그램 또한 해야 사용 가능한 계획된 중단과 갑작스러운된 합니다. 이 위해 서비스 패브릭 복제 트랜잭션 및 지속 스토어 있는 키 값 스토어 \(KVS\) 제공 합니다.

### <a name="modularity"></a>모듈

네트워크 컨트롤러와 가상 네트워크 서비스 및 방화벽 서비스 built\에서 개별 서비스와 같은 네트워크 서비스의 각 모듈식 아키텍처 설계 되었습니다. 

이 응용 프로그램 아키텍처 다음 혜택을 제공합니다.

1. 네트워크 컨트롤러의 모듈으로 지원 되는 서비스의 각 독립 개발 수 있게 발전 필요 합니다. 예를 들어, 다른 서비스 또는 네트워크 컨트롤러의 정상적인 작동이 영향을 주지 않고 부하 분산 소프트웨어가 서비스를 업데이트할 수 있습니다.
2. 네트워크 컨트롤러 모듈 네트워크 발전 함에 따라 새로운 서비스를 추가할을 수 있습니다. 새 서비스는 기존 서비스 영향을 주지 않고 네트워크 컨트롤러에 추가할 수 있습니다.

>[!NOTE]
>Windows Server 2016 네트워크 컨트롤러를 제 3 자 서비스의 추가 지원 되지 않습니다.

서비스 패브릭 모듈 서비스 모델 스키마 개발, 배포 및 응용 프로그램 서비스 접근성 최대화 하기 위해 사용 합니다.

## <a name="network-controller-deployment-options"></a>네트워크 컨트롤러 배포 옵션

네트워크 컨트롤러 System Center 가상 컴퓨터 Manager \(VMM\)를 사용 하 여 배포를 참조 [VMM 패브릭에서 SDN 네트워크 컨트롤러 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)합니다.

네트워크 컨트롤러 스크립트를 사용 하 여 배포를 참조 [는 소프트웨어 정의 네트워크 인프라를 사용 하 여 스크립트 배포](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)합니다.

네트워크 컨트롤러를 사용 하 여 Windows PowerShell 배포 참조 [Windows PowerShell를 사용 하 여 배포 네트워크 컨트롤러](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)

네트워크 컨트롤러에 대 한 자세한 내용은 참조 [네트워크 컨트롤러](Network-Controller.md)합니다.