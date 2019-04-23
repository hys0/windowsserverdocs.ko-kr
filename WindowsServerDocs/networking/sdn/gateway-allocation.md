---
title: 게이트웨이 대역폭 할당
description: ''
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: 3c259b96e1a8ee27888a5cccc50b285a2f7cb8c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850434"
---
# <a name="gateway-bandwidth-allocation"></a>게이트웨이 대역폭 할당

>적용 대상: Windows Server

Windows Server 2016, IPsec, GRE 및 L3에 대 한 개별 터널 대역폭 총 게이트웨이 용량 비율로 있었습니다. 따라서 고객은 표준 TCP 대역폭 게이트웨이 VM에서이 필요에 따라 게이트웨이 용량을 제공 됩니다.

게이트웨이에서 최대 IPsec 터널 대역폭 (3/20)로 제한 되었습니다 또한\*고객이 제공한 게이트웨이 용량입니다. 따라서 예를 들어 게이트웨이 용량 100mbps로 설정 하면 다음 IPsec 터널 용량은 것 150 Mbps입니다. GRE 및 L3 터널에 대 한 동등한 비율 1 월 5 되며 1/2, 각각.

대부분의 배포에 대 한 작업이 있지만 고정된 비율 모델 처리량이 높은 환경에 대 한 적절 한 없습니다. 된 데이터 전송 요금이 높은 경우에 (예:, 40gbps 보다 많은 요청)에서 SDN 게이트웨이 터널 내부 원인으로 인해 제한의 최대 처리량입니다.

Windows Server 2019에 터널 종류에 대 한 최대 처리량은 수정 됨:

-   IPsec 5gbps =

-   GRE 15 Gbps =

-   L3 5gbps =

따라서에 게이트웨이 호스트/v M에서 훨씬 높은 처리량을 사용 하 여 Nic를 지원할 경우에 사용할 수 있는 최대 터널 처리량은 고정 되어 있습니다. 이 처리 하는 또 다른 문제는 임의로 과도 한 프로 비전 게이트웨이 게이트웨이 용량에 대 한 매우 높은 숫자로 제공 될 때 발생 합니다.

## <a name="gateway-capacity-calculation"></a>게이트웨이 용량 계산

이상적으로 게이트웨이 처리량 용량 게이트웨이 VM에 사용할 수 있는 처리량을 설정합니다. 따라서 예를 들어, 단일 게이트웨이 VM 있고 기본 호스트 NIC 처리량은 25 g b p s 게이트웨이 처리량을 설정할 수 있습니다 25 Gbps도 하 합니다.

IPsec 연결에 대해서만 게이트웨이 사용 하는 경우 최대 사용 가능한 고정 용량은 5gbps입니다. 따라서 예를 들어, 게이트웨이의 IPsec 연결을 프로 비전 하는 경우 하나만 제공할 수 있습니다 (수신 + 송신) 하는 집계 대역폭을 5gbps로 합니다.

IPsec 및 GRE 연결에 대 한 게이트웨이 사용 하는 경우에 최대 5의 IPsec 1.2gbps 이상의 처리량 또는 최대 15의 GRE 1.2gbps 이상의 처리량을 제공할 수 있습니다. 따라서 예를 들어 2의 IPsec 1.2gbps 이상의 처리량을 프로 비전 할 경우 게이트웨이 또는 왼쪽 9의 GRE 1.2gbps 이상의 처리량에 프로 비전에 남아 있는 3 IPsec g b p s의 처리량입니다.

더 수학적 용어에서이 넣으려면:

- 게이트웨이 용량 총 25 Gbps =

- 총 사용 가능한 IPsec 용량 5gbps (고정) =

- 사용 가능한 GRE 용량을 총 15 Gbps (고정) =

- 이 게이트웨이에 대 한 IPsec 처리량 비율 = 25/5 = 5gbps

- 이 게이트웨이에 GRE 처리량 비율 = 25/15 5 = 3/g b p s

예를 들어, 고객에 게 2의 IPsec 1.2gbps 이상의 처리량을 할당 하는 경우:

남은 사용 가능한 용량 게이트웨이에서 게이트웨이 – IPsec 처리량 비율의 총 용량 = * IPsec 처리량 할당 (사용 되는 용량)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25–5*2 = 15 Gbps

게이트웨이에 할당할 수 있는 나머지 IPsec 처리량 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5-2 = 3 요금 5gbps

게이트웨이에 할당할 수 있는 남은 GRE 처리량 = 게이트웨이/GRE 처리량 비율의 남은 용량 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;15*3/5 = 9 Gbps

처리량 비율 게이트웨이의 총 용량에 따라 달라 집니다. 한 가지 주의할 점은 총 용량 게이트웨이 VM은 사용할 수 있는 TCP 대역폭을 설정 해야 하는 경우 게이트웨이에서 호스트 되는 여러 Vm에 있는 경우 그에 따라 게이트웨이의 총 용량을 조정 해야 합니다.

또한 게이트웨이 용량 사용 가능한 총 터널 용량 보다 작은 경우, 총 사용 가능한 터널 용량은 게이트웨이 용량으로 설정 됩니다. 예를 들어, 4 g b p s 게이트웨이 용량으로 설정한 경우 GRE, IPsec 및 L3에 사용 가능한 총 용량 설정은 4 Gbps 1gbps를 각 터널에 대 한 처리량 비율을 유지 합니다.

## <a name="windows-server-2016-behavior"></a>Windows Server 2016 동작

Windows Server 2016에 대 한 게이트웨이 용량 계산 알고리즘 변경 되지 않습니다. Windows Server 2016에서는 최대 IPsec 터널 대역폭 (3/20)로 제한 되었습니다\*게이트웨이에서 게이트웨이 용량입니다. GRE 및 L3 터널에 대 한 동등한 비율 된 1 월 5 및 1/2, 각각.

로 업그레이드 하는 Windows Server 2016에서 Windows Server 2019 하는 경우:

1.  **GRE 및 L3 터널:** 네트워크 컨트롤러 노드 Windows Server 2019로 업데이트 되 면 적용 하는 Windows Server 2019 할당 논리

2.  **IPSec 터널:** Windows Server 2016 게이트웨이 할당 논리 게이트웨이 풀의 모든 게이트웨이 Windows Server 2019에 업그레이드 될 때까지 함수를 계속 합니다. 게이트웨이 풀의 모든 게이트웨이에 대 한로 Azure 게이트웨이 서비스를 설정 해야 합니다 **자동**합니다.

>[!NOTE]
>Windows Server 2019로 업그레이드 한 후 게이트웨이 되는 과도 하 게 프로 비전 된 (할당 논리는 Windows Server 2016에서 Windows Server 2019로 변경)으로 가능성이 있습니다. 이 경우 게이트웨이에서 기존 연결은 계속 존재 합니다. 게이트웨이에 대 한 REST 리소스에는 게이트웨이 과도 하 게 프로 비전 된 경고가 throw 됩니다. 이 경우 일부 연결이 다른 게이트웨이를 이동 해야 합니다.

---