---
title: NPS 프록시 서버 부하 분산
description: Windows Server 2016 및 Windows 10 VPN 기능 및 기능에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 528280e6-b47e-489f-b310-b257d434aa0d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 04f466f7646fc5109af7379cab1240d8cd6829ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874404"
---
# <a name="nps-proxy-server-load-balancing"></a>NPS 프록시 서버 부하 분산

적용 대상: Windows Server 2016

가상 사설망 (VPN) 서버 및 무선 액세스 지점과 같은 네트워크 액세스 서버는 원격 인증 전화 접속 사용자 서비스 (RADIUS) 클라이언트 연결 요청을 만들고 NPS와 같은 RADIUS 서버 보냅니다. 일부 경우에는 NPS 나타날 연결 요청을 너무 많이 한 번에 성능 저하 또는 오버 로드. 오버 로드는 NPS 때 자세한 NPSs 네트워크에 추가 하 고 부하 분산을 구성 하는 것이 좋습니다. 하나 이상의 NPSs의 오버 로드를 방지 하기 위해 여러 NPSs 간에 들어오는 연결 요청을 균등 하 게 배포 하는 경우 부하 분산 호출 됩니다.

부하 분산에 특히 유용합니다.

- 확장할 수 있는 인증 프로토콜 전송 계층 보안을 사용 하는 조직은 \(EAP-TLS\) 또는 Protected Extensible Authentication Protocol \(PEAP\)TLS 인증에 대 한 합니다. 사용자 또는 클라이언트 컴퓨터 인증 한 서버 인증용 인증서를 사용 하는 이러한 인증 방법, RADIUS 프록시 서버에 로드 되므로 암호 기반 인증 방법의 사용할 때 보다 더 많은.
- 지속적인 서비스 가용성을 유지 해야 하는 조직.
- 인터넷 서비스 공급자 \(Isp\) 다른 조직에 대 한 VPN 액세스를 아웃소싱하는 합니다. 아웃소싱 된 VPN 서비스 인증 트래픽의 큰 볼륨을 생성할 수 있습니다.

프로그램 NPSs 전송 연결 요청의 부하를 분산 하는 데 사용할 수는 두 가지가 있습니다.

- 여러 RADIUS 서버에 연결 요청을 보내는 네트워크 액세스 서버를 구성 합니다. 예를 들어, 20 무선 액세스 지점 및 RADIUS 서버 두 경우 모두 RADIUS 서버에 연결 요청을 보내는 각 액세스 지점을 구성 합니다. 부하를 분산 하 고 우선 순위가 지정 된 순서로 여러 RADIUS 서버에 연결 요청을 보낼 액세스 서버를 구성 하 여 각 네트워크 액세스 서버에서 장애 조치를 제공할 수 있습니다. 이 부하 분산 방법은 일반적으로 많은 수의 RADIUS 클라이언트를 배포 하지 않는 소규모 조직에 가장 적합 합니다.
- NPS를 RADIUS 프록시로 구성 된 여러 NPSs 또는 다른 RADIUS 서버 간의 분산 연결 요청의 부하를 사용 합니다. 예를 들어 100 무선 액세스 지점, 하나의 NPS 프록시 및 세 명의 RADIUS 서버를 설정한 경우 액세스 지점 NPS 프록시에 모든 트래픽을 전송 하도록 구성할 수 있습니다. NPS 프록시에서 프록시 세 RADIUS 서버 간의 연결 요청을 균등 하 게 배분 되도록 부하 분산을 구성 합니다. 이 부하 분산 방법은 많은 RADIUS 클라이언트 및 서버에 있는 중간 규모 및 대규모 조직에 가장 적합 합니다.

대부분의 경우에서 부하 분산 하는 가장 좋은 방법은 두 명의 NPS 프록시 서버에 연결 요청을 전송 하 고 RADIUS 서버 사이에서 균형을 로드 하려면 NPS 프록시 구성 RADIUS 클라이언트를 구성 하는 것입니다. 이 방법은 장애 조치 및 NPS 프록시 및 RADIUS 서버에 대해 부하 분산을 제공 합니다.

## <a name="radius-server-priority-and-weight"></a>RADIUS 서버의 우선 순위 및 가중치

NPS 프록시 구성 프로세스 중 원격 RADIUS 서버 그룹을 만들고 하 다음 각 그룹에 RADIUS 서버를 추가 합니다. 부하 분산을 구성 하려면 원격 RADIUS 서버 그룹 당 RADIUS 서버가 둘 이상 있어야 합니다. 그룹 구성원을 추가 하는 동안 또는 그룹 멤버는 RADIUS 서버를 만든 후 부하 분산 탭에서 다음 항목을 구성 하려면 추가 RADIUS 서버 대화 상자에 액세스할 수 있습니다.

- **우선 순위**합니다. 우선 순위를 NPS 프록시 서버는 RADIUS 서버의 중요도의 순서를 지정 합니다. 우선 순위 수준 1, 2 또는 3 등의 정수로 값을 할당 되어야 합니다. 낮을수록 수, 더 높은 우선 순위를 RADIUS 서버로 NPS 프록시를 제공 합니다. 예를 들어, RADIUS 서버 1의 가장 높은 우선 순위에 할당 된 경우 NPS 프록시 연결 요청을 RADIUS 서버로 먼저 보냅니다; 우선 순위 1 사용 하 여 서버를 사용할 수 없는 경우 NPS 연결 요청 우선 순위 2 사용 하 여 RADIUS 서버 등을 보냅니다. 여러 RADIUS 서버에 동일한 우선 순위를 지정할 수 있으며 다음 가중치 설정을 사용 하 여 부하를 분산 서로 수 있습니다.

- **가중치**합니다. NPS 얼마나 많은 연결을 확인 하려면이 가중치 설정은 각 보낼 요청을 사용 하 여 동일한 우선 순위 수준이 그룹 구성원을 하는 경우 멤버를 그룹화 합니다. 가중치 설정을 1에서 100 사이의 값을 할당 해야 하 고 값을 100%의 백분율을 나타냅니다. 예를 들어, 원격 RADIUS 서버 그룹 1의 우선 순위 수준 및 50 가중치 등급을 포함 하는 두 멤버가 있으면 NPS 프록시 각 RADIUS 서버로 연결 요청 중 50%를 전달 합니다.

- **고급 설정**합니다. 이러한 장애 조치 설정을 원격 RADIUS 서버를 사용할 수 있는지 확인 하려면 NPS에 대해 알아볼 수 있습니다. NPS를 RADIUS 서버로 사용할 수 없는 경우, 다른 그룹 멤버에 연결 요청을 보내기 시작할 수 있습니다. 이러한 설정을 사용 하 여 NPS 프록시 삭제; 요청 된 것으로 간주 되기 전에 RADIUS 서버 로부터 응답을 기다리는 시간 (초) 수를 구성할 수 있습니다. 없음으로; RADIUS 서버를 식별 하는 NPS 프록시 하기 전에 삭제 요청의 최대 수 고 NPS 프록시 하기 전에 요청 간에 경과 된 시간 (초) 수 없음으로 RADIUS 서버를 식별 합니다.

## <a name="configure-nps-proxy-load-balancing"></a>NPS 프록시 부하 분산 구성

부하 분산을 구성 하기 전에 얼마나 많은 원격 RADIUS 서버 그룹에 필요한 서버는 각 특정 그룹 및 각 서버에 대 한 우선 순위 및 가중치 설정을의 멤버를 포함 하는 배포 계획을 만듭니다.

>[!NOTE]
>다음 단계는 이미 배포 및 구성 된 RADIUS 서버를 가정 합니다.

프록시 서버와 원격 RADIUS 서버에 RADIUS 클라이언트의 전방 연결 요청을 프록시로 NPS를 구성 하려면 다음 작업을 수행 해야 합니다.

1. RADIUS 클라이언트를 배포 \(VPN 서버, 전화 접속 서버, 터미널 서비스 게이트웨이 서버, 802.1x 인증 스위치, 및 802.1x 무선 액세스 지점\) 및 NPS 프록시에 연결 요청을 보내도록 구성 서버입니다.

2. NPS 프록시에서 네트워크 액세스 서버를 RADIUS 클라이언트로 구성 합니다. 자세한 내용은 [RADIUS 클라이언트 구성](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-radius-clients-configure)합니다.

3. NPS 프록시를 하나 이상의 원격 RADIUS 서버 그룹을 만듭니다. 이 과정에서 RADIUS 서버를 원격 RADIUS 서버 그룹에 추가 합니다. 자세한 내용은 [원격 RADIUS 서버 그룹 구성](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-rrsg-configure)합니다.

4. NPS 프록시에서 원격 RADIUS 서버 그룹에 추가한 각 RADIUS 서버에 대 한 RADIUS 서버를 클릭 **부하 분산** 탭을 선택한 다음 구성 **우선 순위**하십시오 **가중치** 및 **고급 설정**합니다.

5. NPS 프록시에서 원격 RADIUS 서버 그룹을 인증 및 계정 요청을 전달할 연결 요청 정책을 구성 합니다. 원격 RADIUS 서버 그룹 당 하나의 연결 요청 정책을 만들어야 합니다. 자세한 내용은 [연결 요청 정책 구성](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-configure)합니다.


