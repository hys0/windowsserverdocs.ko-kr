---
title: NPS 프록시 서버 부하 분산
description: 이 항목을 사용 하 여 Windows Server 2016 및 Windows 10 VPN 기능에 대해 알아볼 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 528280e6-b47e-489f-b310-b257d434aa0d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2d138b9891fb3cfa8e15060be312ff945942c660
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405429"
---
# <a name="nps-proxy-server-load-balancing"></a>NPS 프록시 서버 부하 분산

적용 대상: Windows Server 2016

VPN (가상 사설망) 서버 및 무선 액세스 지점과 같은 네트워크 액세스 서버인 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 클라이언트는 연결 요청을 만들고 NPS와 같은 RADIUS 서버에 보냅니다. 경우에 따라 NPS에서 한 번에 너무 많은 연결 요청을 수신 하 여 성능이 저하 되거나 오버 로드 될 수 있습니다. NPS가 오버 로드 되 면 네트워크에 NPSs를 추가 하 고 부하 분산을 구성 하는 것이 좋습니다. 하나 이상의 NPSs의 오버 로드를 방지 하기 위해 들어오는 연결 요청을 여러 NPSs 간에 균등 하 게 분산 하는 경우이를 부하 분산 이라고 합니다.

부하 분산은 특히 다음과 같은 경우에 유용 합니다.

- EAP TLS\) 또는 보호 된 확장할 수 있는 인증 프로토콜을 사용 하는 조직에서는 인증을 위해 PEAP\)-TLS \(\(합니다. 이러한 인증 방법은 서버 인증을 위해 인증서를 사용 하 고 사용자 또는 클라이언트 컴퓨터 인증을 위해 인증서를 사용 하기 때문에, RADIUS 프록시 및 서버에 대 한 부하는 암호 기반 인증 방법을 사용 하는 경우 보다 더 많아집니다.
- 지속적인 서비스 가용성을 유지 해야 하는 조직
- 인터넷 서비스 공급자 \(Isp\) 다른 조직에 대 한 VPN 액세스를 아웃소싱 합니다. 아웃소싱 된 VPN 서비스는 대량의 인증 트래픽을 생성할 수 있습니다.

NPSs로 전송 되는 연결 요청의 부하를 분산 하는 데 사용할 수 있는 두 가지 방법은 다음과 같습니다.

- 여러 RADIUS 서버에 연결 요청을 보내도록 네트워크 액세스 서버를 구성 합니다. 예를 들어 20 개의 무선 액세스 지점과 두 개의 RADIUS 서버를 사용 하는 경우 각 액세스 지점에서 두 RADIUS 서버 모두에 연결 요청을 보내도록 구성 합니다. 지정 된 우선 순위에 따라 여러 RADIUS 서버에 연결 요청을 보내도록 액세스 서버를 구성 하 여 각 네트워크 액세스 서버에서 부하를 분산 하 고 장애 조치 (failover)를 제공할 수 있습니다. 이 부하 분산 방법은 일반적으로 많은 수의 RADIUS 클라이언트를 배포 하지 않는 소규모 조직에 적합 합니다.
- RADIUS 프록시로 구성 된 NPS를 사용 하 여 여러 n Pss 또는 다른 RADIUS 서버 간의 연결 요청 부하를 분산 합니다. 예를 들어, 100 무선 액세스 지점이 있는 경우 NPS 프록시 하나 및 RADIUS 서버 3 개를 사용 하는 경우 NPS 프록시로 모든 트래픽을 전송 하도록 액세스 지점이 구성 될 수 있습니다. NPS 프록시에서 프록시가 3 개의 RADIUS 서버 간에 연결 요청을 균등 하 게 분산 하도록 부하 분산을 구성 합니다. 이 부하 분산 방법은 RADIUS 클라이언트 및 서버가 많은 중소 규모의 조직에 가장 적합 합니다.

대부분의 경우 부하를 분산 하는 가장 좋은 방법은 두 NPS 프록시 서버에 연결 요청을 보내도록 RADIUS 클라이언트를 구성한 다음 RADIUS 서버 간에 부하를 분산 하도록 NPS 프록시를 구성 하는 것입니다. 이 방법은 NPS 프록시 및 RADIUS 서버에 대 한 장애 조치 (failover) 및 부하 분산을 모두 제공 합니다.

## <a name="radius-server-priority-and-weight"></a>RADIUS 서버 우선 순위 및 가중치

NPS 프록시 구성 프로세스 중에 원격 RADIUS 서버 그룹을 만든 다음 각 그룹에 RADIUS 서버를 추가할 수 있습니다. 부하 분산을 구성 하려면 원격 RADIUS 서버 그룹당 RADIUS 서버가 두 개 이상 있어야 합니다. 그룹 구성원을 추가 하는 동안 또는 그룹 구성원으로 RADIUS 서버를 만든 후에는 RADIUS 서버 추가 대화 상자에 액세스 하 여 부하 분산 탭에서 다음 항목을 구성할 수 있습니다.

- **우선 순위**입니다. 우선 순위 NPS 프록시 서버에 대 한 RADIUS 서버 중요도의 순서를 지정 합니다. 우선 순위 수준에는 정수 값 (예: 1, 2 또는 3)을 할당 해야 합니다. 숫자가 낮을수록 NPS 프록시가 RADIUS 서버에 부여 하는 우선 순위가 높습니다. 예를 들어, RADIUS 서버에 가장 높은 우선 순위 1이 할당 되 면 NPS 프록시는 먼저 RADIUS 서버에 연결 요청을 보냅니다. 우선 순위 1의 서버를 사용할 수 없는 경우 NPS는 우선 순위가 2 인 RADIUS 서버에 연결 요청을 보냅니다. 여러 RADIUS 서버에 동일한 우선 순위를 할당 한 다음 가중치 설정을 사용 하 여 이러한 서버 간에 부하를 분산할 수 있습니다.

- **가중치**. NPS는이 가중치 설정을 사용 하 여 그룹 멤버의 우선 순위 수준이 동일한 경우 각 그룹 구성원에 게 보낼 연결 요청 수를 결정 합니다. 가중치 설정에는 1에서 100 사이의 값을 할당 해야 하며 값은 100%의 백분율을 나타냅니다. 예를 들어, 원격 RADIUS 서버 그룹에 우선 순위 수준이 1이 고 가중치 등급이 50 인 두 개의 멤버가 있는 경우 NPS 프록시는 연결 요청의 50%를 각 RADIUS 서버에 전달 합니다.

- **고급 설정**입니다. 이러한 장애 조치 (failover) 설정은 NPS가 원격 RADIUS 서버를 사용할 수 없는지 여부를 확인 하는 방법을 제공 합니다. NPS에서 RADIUS 서버를 사용할 수 없는 것으로 확인 되 면 다른 그룹 구성원에 게 연결 요청을 보내기 시작할 수 있습니다. 이러한 설정을 사용 하면 NPS 프록시가 요청을 삭제 한 것으로 간주 하기 전에 RADIUS 서버에서 응답을 기다리는 시간 (초)을 구성할 수 있습니다. NPS 프록시가 RADIUS 서버를 사용할 수 없는 것으로 식별 하기 전까지 삭제 된 요청의 최대 수입니다. 그리고 NPS 프록시가 RADIUS 서버를 사용할 수 없는 것으로 식별 하기 전까지 요청 간에 경과 될 수 있는 시간 (초)입니다.

## <a name="configure-nps-proxy-load-balancing"></a>NPS 프록시 부하 분산 구성

부하 분산을 구성 하기 전에 필요한 원격 RADIUS 서버 그룹의 수, 각 특정 그룹의 구성원 인 서버 및 각 서버의 우선 순위 및 가중치 설정을 포함 하는 배포 계획을 만듭니다.

>[!NOTE]
>다음 단계에서는 RADIUS 서버를 이미 배포 하 고 구성 했다고 가정 합니다.

프록시 서버 역할을 하 고 RADIUS 클라이언트에서 원격 RADIUS 서버로 연결 요청을 전달 하도록 NPS를 구성 하려면 다음 작업을 수행 해야 합니다.

1. RADIUS 클라이언트 \(VPN 서버, 전화 접속 서버, 터미널 서비스 게이트웨이 서버, 802.1 X 인증 스위치 및 802.1 X 무선 액세스 지점이\)를 배포 하 고 NPS 프록시 서버에 연결 요청을 보내도록 구성 합니다.

2. NPS 프록시에서 네트워크 액세스 서버를 RADIUS 클라이언트로 구성 합니다. 자세한 내용은 [RADIUS 클라이언트 구성](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-radius-clients-configure)을 참조 하세요.

3. NPS 프록시에서 하나 이상의 원격 RADIUS 서버 그룹을 만듭니다. 이 과정에서 RADIUS 서버를 원격 RADIUS 서버 그룹에 추가 합니다. 자세한 내용은 [원격 RADIUS 서버 그룹 구성](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-rrsg-configure)을 참조 하세요.

4. NPS 프록시에서 원격 RADIUS 서버 그룹에 추가 하는 각 RADIUS 서버에 대해 RADIUS 서버 **부하 분산** 탭을 클릭 한 다음 **우선 순위**, **가중치**및 **고급 설정을**구성 합니다.

5. NPS 프록시에서 인증 및 계정 요청을 원격 RADIUS 서버 그룹으로 전달 하도록 연결 요청 정책을 구성 합니다. 원격 RADIUS 서버 그룹당 하나의 연결 요청 정책을 만들어야 합니다. 자세한 내용은 [연결 요청 정책 구성](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-configure)을 참조 하세요.


