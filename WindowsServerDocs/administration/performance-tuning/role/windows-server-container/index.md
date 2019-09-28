---
title: Windows 서버 컨테이너에 대한 성능 튜닝
description: Windows Server 16의 컨테이너에 대한 성능 튜닝 추천 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: DavSo; Ericam; YaShi
author: akino
ms.date: 10/16/2017
ms.openlocfilehash: 890632c9e8adf221e56ffa91331e5371a3fcdf86
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384945"
---
# <a name="performance-tuning-windows-server-containers"></a>Windows 서버 컨테이너에 대한 성능 튜닝

## <a name="introduction"></a>소개
Windows Server 2016은 OS에 기본 제공된 컨테이너 기술을 지원하는 최초의 Windows 버전입니다. Server 2016에서는 두 가지 유형의 컨테이너, 즉 Windows Server 컨테이너와 Hyper-V 컨테이너를 사용할 수 있습니다. 각 컨테이너 유형은 Windows Server 2016의 Server Core 또는 Nano Server SKU를 지원합니다. 

이러한 구성에는 시나리오에 적합한 성능을 이해하는 데 도움이 되도록 아래에서 자세히 설명하는 성능상의 여러 가지 의미가 있습니다. 또한 성능에 영향을 주는 구성에 대해 자세히 설명하고, 이러한 각 옵션의 장단점을 설명합니다.

### <a name="windows-server-container-and-hyper-v-containers"></a>Windows Server 컨테이너 및 Hyper-V 컨테이너

Windows Server 컨테이너와 Hyper-V 컨테이너는 많은 동일한 이동성 및 일관성 이점을 제공하지만 격리 보장 및 성능 특성 측면에서 차이가 있습니다.

**Windows Server 컨테이너**는 프로세스 및 네임 스페이스 격리 기술을 통해 애플리케이션 격리를 제공합니다. Windows Server 컨테이너는 컨테이너 호스트와 호스트에서 실행되는 모든 컨테이너와 커널을 공유합니다.

**Hyper-v 컨테이너**는 고도로 최적화된 가상 머신에서 각 컨테이너를 실행하여 Windows Server 컨테이너에서 제공하는 격리를 확장합니다. 이 구성에서 컨테이너 호스트의 커널은 Hyper-V 컨테이너와 공유되지 않습니다.

Hyper-V 컨테이너에서 제공하는 추가 격리는 대부분 컨테이너와 컨테이너 호스트 간 격리의 하이퍼바이저 계층을 통해 이루어집니다. 이렇게 하면 Windows Server 컨테이너와 달리 시스템 파일과 이진 파일의 공유를 줄여 전체적으로 스토리지와 메모리의 사용 공간을 늘릴 수 있으므로 컨테이너 밀도에 영향을 줍니다. 또한 일부 네트워크, 스토리지 IO 및 CPU 경로에 필요한 추가 오버헤드가 있습니다.

### <a name="nano-server-and-server-core"></a>Nano Server 및 Server Core

Windows Server 컨테이너와 Hyper-V 컨테이너는 Server Core 및 Windows Server 2016에서 사용할 수 있는 새로운 설치 옵션인 [Nano Server](https://technet.microsoft.com/windows-server-docs/compute/nano-server/getting-started-with-nano-server)를 지원합니다. 

Nano 서버는 프라이빗 클라우드 및 데이터 센터에 최적화된 원격 관리 서버 운영 체제입니다. Server Core 모드의 Windows Server와 유사하지만 훨씬 작고 로컬 로그온 기능이 없으며 64비트 응용 프로그램, 도구 및 에이전트에만 지원합니다. 디스크 공간을 훨씬 적게 차지하며 더 빠르게 시작합니다.

## <a name="container-start-up-time"></a>컨테이너 시작 시간
컨테이너 시작 시간은 컨테이너에서 가장 큰 이점을 제공하는 많은 시나리오의 주요 메트릭입니다. 따라서 컨테이너 시작 시간을 최적화하는 방법을 이해해야 합니다. 시작 시간을 향상시키기 위해 이해해야 할 튜닝 상의 몇 가지 절충 사항은 다음과 같습니다.

### <a name="first-logon"></a>첫 번째 로그온

Microsoft는 Nano Server와 Server Core에 대한 기본 이미지를 모두 제공합니다. Server Core용으로 제공되는 기본 이미지는 첫 번째 로그온(OOBE)과 관련된 시작 시간 오버헤드를 제거하여 최적화했습니다. Nano Server 기본 이미지에서는 그렇지 않습니다. 그러나 이 비용은 하나 이상의 계층을 컨테이너 이미지에 적용하여 Nano Server 기반 이미지에서 제거할 수 있습니다. 이미지에서 후속 컨테이너가 시작되면 첫 번째 로그온 비용이 발생하지 않습니다.
### <a name="scratch-space-location"></a>스크래치 공간 위치

컨테이너는 기본적으로 실행 중인 컨테이너의 수명 동안 컨테이너 호스트의 시스템 드라이브 미디어에 있는 임시 스크래치 공간을 스토리지에 사용합니다. 이 공간은 컨테이너의 시스템 드라이브 역할을 하며, 컨테이너 작업에서 수행되는 많은 쓰기 및 읽기 작업은 이 경로를 따릅니다. 회전하는 디스크 자기 미디어(HDD)에 시스템 드라이브가 있지만 더 빠른 스토리지 미디어(더 빠른 HDD 또는 SSD)를 사용할 수 있는 호스트 시스템의 경우 컨테이너 스크래치 공간은 다른 드라이브로 이동할 수 있습니다. 이 작업은 dockerd –g 명령을 사용하여 수행됩니다. 이 명령은 글로벌이며 시스템에서 실행되는 모든 컨테이너에 영향을 줍니다.

### <a name="nested-hyper-v-containers"></a>중첩된 Hyper-V 컨테이너
Windows Server 2016용 Hyper-V는 중첩된 하이퍼바이저 지원을 도입했습니다. 즉, 이제는 가상 머신 내에서 가상 머신을 실행할 수 있습니다. 이렇게 하면 여러 가지 유용한 시나리오가 열리지만, 실제 호스트에서 실행되는 두 가지 수준의 하이퍼바이저가 있으므로 하이퍼바이저로 인해 영향을 받는 일부 성능이 과장됩니다.

컨테이너의 경우 이는 가상 머신 내에서 Hyper-V 컨테이너를 실행할 때 영향을 줍니다. Hyper-V 컨테이너는 자체와 컨테이너 호스트 간의 하이퍼바이저 계층을 통해 격리를 제공하므로, 컨테이너 호스트가 Hyper-V 기반 가상 머신인 경우 컨테이너 시작 시간, 스토리지 IO, 네트워크 IO 및 처리량, CPU와 관련된 성능 오버헤드가 있습니다.

## <a name="storage"></a>저장 공간
### <a name="mounted-data-volumes"></a>탑재된 데이터 볼륨

컨테이너는 호스트 시스템 드라이브를 컨테이너 스크래치 공간에 컨테이너 사용할 수 있는 기능을 제공합니다. 그러나 컨테이너 스크래치 공간에는 컨테이너의 수명과 동일한 수명이 있습니다. 즉, 컨테이너가 중지되면 스크래치 공간과 관련된 모든 데이터가 사라집니다.

그러나 대부분의 시나리오에서는 컨테이너 수명과는 관계없이 데이터를 유지하는 것이 좋습니다. 이러한 경우 데이터 볼륨을 컨테이너 호스트에서 컨테이너로 탑재할 수 있도록 지원합니다. Windows Server 컨테이너의 경우 탑재된 데이터 볼륨과 관련된 무시할 수 있는 IO 경로 오버헤드가 있습니다(네이티브 성능에 가까움). 그러나 데이터 볼륨을 Hyper-V 컨테이너에 탑재하면 해당 경로에서 일부 IO 성능이 저하됩니다. 또한 이 영향도 가상 머신 내에서 Hyper-V 컨테이너를 실행할 때 과장됩니다.

### <a name="scratch-space"></a>스크래치 공간

Windows Server 컨테이너와 Hyper-V 컨테이너는 기본적으로 컨테이너 스크래치 공간으로 20GB 동적 VHD를 제공합니다. 두 컨테이너 유형에 대한 컨테이너 OS는 모두 해당 공간의 일부를 차지하며, 이는 시작된 모든 컨테이너에 적용됩니다. 따라서 시작된 모든 컨테이너는 스토리지에 어느 정도 영향을 주며, 워크로드에 따라 백업 스토리지 미디어를 최대 20GB까지 쓸 수 있습니다. 서버 스토리지 구성은 이를 고려하여 설계해야 합니다.
(스크래치 크기는 구성할 수 있습니다.)

## <a name="networking"></a>네트워킹
Windows Server 컨테이너와 Hyper-V 컨테이너는 다양한 네트워킹 구성의 요구 사항에 가장 적합한 다양한 네트워킹 모드를 제공합니다. 이러한 각 옵션은 고유한 성능 특성을 제공합니다.

### <a name="windows-network-address-translation-winnat"></a>WinNAT(Windows Network Address Translation)

각 컨테이너는 내부 사설 IP 접두사(예: 172.16.0.0/12)에서 IP 주소를 받습니다. 컨테이너 호스트에서 컨테이너 끝점으로의 포트 전달/매핑이 지원됩니다. Docker는 dockerd를 처음 실행할 때 기본적으로 NAT 네트워크를 만듭니다.

이러한 세 가지 모드 중 NAT 구성은 비용이 가장 많이 드는 네트워크 IO 경로이지만 최소한 구성만 필요합니다. 

Windows Server 컨테이너는 호스트 vNIC를 사용하여 가상 스위치에 연결합니다. Hyper-V 컨테이너는 가상 VM NIC(유틸리티 VM에 노출되지 않음)를 사용하여 가상 스위치에 연결합니다. 컨테이너에서 외부 네트워크와 통신하는 경우 패킷은 주소 변환이 적용된 WinNAT를 통해 라우팅되므로 약간의 오버헤드가 발생합니다.

### <a name="transparent"></a>투명

각 컨테이너 엔드포인트는 실제 네트워크에 직접 연결됩니다. 실제 네트워크의 IP 주소는 외부 DHCP 서버를 사용하여 정적 또는 동적으로 할당할 수 있습니다.

투명 모드는 네트워크 IO 경로 측면에서 비용이 가장 적게 듭니다. 외부 패킷은 컨테이너 가상 NIC에 직접 전달되어 외부 네트워크에 직접 액세스할 수 있습니다.

### <a name="l2-bridge"></a>L2 브리지
각 컨테이너 엔드포인트는 컨테이너 호스트와 동일한 IP 서브넷에 있습니다. IP 주소는 컨테이너 호스트와 동일한 접두사에서 정적으로 할당해야 합니다. 호스트의 모든 컨테이너 끝점은 계층 2 주소 변환으로 인해 MAC 주소가 동일합니다.

L2 브리지 모드는 외부 네트워크에 직접 액세스할 수 있으므로 WinNAT 모드보다 성능이 높지만, MAC 주소 변환도 도입하므로 투명 모드보다는 성능이 낮습니다.




