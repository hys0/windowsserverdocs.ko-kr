---
title: 게이트웨이 대역폭 할당
description: ''
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: ''
ms.author: lizross
author: eross-msft
ms.date: 08/22/2018
ms.openlocfilehash: 8e0709360449e1175988b14a963047ee72f26ade
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313031"
---
# <a name="gateway-bandwidth-allocation"></a>게이트웨이 대역폭 할당

>적용 대상: Windows Server

Windows Server 2016에서 IPsec, GRE 및 L3의 개별 터널 대역폭은 총 게이트웨이 용량의 비율입니다. 따라서 고객은 게이트웨이 VM에서이를 예상 하는 표준 TCP 대역폭을 기반으로 게이트웨이 용량을 제공 합니다.

또한 게이트웨이의 최대 IPsec 터널 대역폭이 (3/20)\*고객에 의해 제공 된 게이트웨이 용량으로 제한 되었습니다. 따라서 예를 들어 게이트웨이 용량을 100 Mbps로 설정 하면 IPsec 터널 용량은 150 Mbps가 됩니다. GRE 및 L3 터널에 해당 하는 비율은 각각 1/5 및 1/2입니다.

이는 대부분의 배포에 대해 작동 했지만 처리량이 높은 환경에서는 고정 비율 모델이 적합 하지 않습니다. 데이터 전송 속도가 높은 경우 (예를 들어 40 g b 이상)에도 내부 요소로 인해 SDN 게이트웨이 터널의 최대 처리량이 증가 합니다.

Windows Server 2019에서 터널 유형의 경우 최대 처리량은 고정 됩니다.

-   IPsec = 5gbps

-   GRE = 15gbps

-   L3 = 5gbps

따라서 게이트웨이 호스트/VM이 훨씬 높은 처리량의 Nic를 지 원하는 경우에도 사용 가능한 최대 터널 처리량은 고정 됩니다. 이 작업을 수행 하는 또 다른 문제는 게이트웨이 용량에 매우 높은 수를 제공 하는 경우 발생 하는 임의로 과도 한 프로 비전 게이트웨이입니다.

## <a name="gateway-capacity-calculation"></a>게이트웨이 용량 계산

게이트웨이 처리량 용량을 게이트웨이 VM에 사용할 수 있는 처리량으로 설정 하는 것이 가장 좋습니다. 예를 들어 단일 게이트웨이 VM이 있고 기본 호스트 NIC 처리량이 25gbps 인 경우 게이트웨이 처리량은 25gbps로도 설정할 수 있습니다.

IPsec 연결에 대해서만 게이트웨이를 사용 하는 경우 사용 가능한 최대 고정 용량은 5gbps입니다. 예를 들어 게이트웨이에서 IPsec 연결을 프로 비전 하는 경우 집계 대역폭 (들어오는 + 나가는)만 5gbps로 프로 비전 할 수 있습니다.

IPsec 및 GRE 연결 모두에 게이트웨이를 사용 하는 경우 최대 5gbps의 IPsec 처리량 또는 최대 15gbps의 GRE 처리량을 프로 비전 할 수 있습니다. 예를 들어, 2 Gbps의 IPsec 처리량을 프로 비전 하는 경우 게이트웨이에서 프로 비전 하는 데는 3gbps의 IPsec 처리량이 남아 있으며, 그 중에서는 9, GRE 처리량은 남아 있습니다.

이를 더 수학적 용어로 추가 하려면 다음을 수행 합니다.

- 게이트웨이의 총 용량 = 25gbps

- 사용 가능한 총 IPsec 용량 = 5gbps (고정)

- 총 사용 가능한 GRE 용량 = 15gbps (고정)

- 이 게이트웨이의 IPsec 처리량 비율 = 25/5 = 5gbps

- 이 게이트웨이의 GRE 처리량 비율 = 25/15 = 5/3 Gbps

예를 들어 고객에 게 2 Gbps의 IPsec 처리량을 할당 하는 경우:

게이트웨이의 남은 사용 가능한 용량 = 게이트웨이의 총 용량 – IPsec 처리량 비율 * 할당 된 IPsec 처리량 (사용 된 용량)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25 – 5 * 2 = 15gbps

게이트웨이에서 할당할 수 있는 나머지 IPsec 처리량 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5-2 = 3gbps

게이트웨이에서 할당할 수 있는 남은 GRE 처리량 = 게이트웨이/GRE 처리량 비율의 남은 용량 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;15 * 3/5 = 9gbps

처리량 비율은 게이트웨이의 총 용량에 따라 달라 집니다. 한 가지 주의할 점은 총 용량을 게이트웨이 VM에서 사용할 수 있는 TCP 대역폭으로 설정 해야 한다는 것입니다. 게이트웨이에서 여러 Vm을 호스트 하는 경우 게이트웨이의 총 용량을 적절 하 게 조정 해야 합니다.

또한 게이트웨이 용량이 사용 가능한 총 터널 용량 보다 작은 경우 사용 가능한 총 터널 용량은 게이트웨이 용량으로 설정 됩니다. 예를 들어 게이트웨이 용량을 4 Gbps로 설정 하면 IPsec, L3 및 GRE에 대해 사용 가능한 총 용량이 4 Gbps로 설정 되 고 각 터널의 처리량 비율은 1Gbps로 유지 됩니다.

## <a name="windows-server-2016-behavior"></a>Windows Server 2016 동작

Windows Server 2016에 대 한 게이트웨이 용량 계산 알고리즘은 변경 되지 않은 상태로 유지 됩니다. Windows Server 2016에서는 게이트웨이의 최대 IPsec 터널 대역폭이 (3/20)\*게이트웨이 용량으로 제한 되었습니다. GRE 및 L3 터널에 해당 하는 비율은 각각 1/5 및 1/2입니다.

Windows Server 2016에서 Windows Server 2019로 업그레이드 하는 경우:

1.  **GRE 및 L3 터널:** Windows Server 2019 할당 논리는 네트워크 컨트롤러 노드가 Windows Server 2019로 업데이트 된 후에 적용 됩니다.

2.  **IPSec 터널:** Windows Server 2016 게이트웨이 할당 논리는 게이트웨이 풀의 모든 게이트웨이가 Windows Server 2019로 업그레이드 될 때까지 계속 작동 합니다. 게이트웨이 풀에 있는 모든 게이트웨이의 경우 Azure 게이트웨이 서비스를 **자동**으로 설정 해야 합니다.

>[!NOTE]
>Windows Server 2019로 업그레이드 한 후에는 게이트웨이가 과도 하 게 프로 비전 됩니다. 즉, 할당 논리가 Windows Server 2016에서 Windows Server 2019로 변경 될 수 있습니다. 이 경우 게이트웨이의 기존 연결은 계속 존재 합니다. 게이트웨이의 REST 리소스는 게이트웨이가 과도 하 게 프로 비전 되었다는 경고를 발생 시킵니다. 이 경우 일부 연결을 다른 게이트웨이로 이동 해야 합니다.

---