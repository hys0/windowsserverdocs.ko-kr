---
title: Azure 가상 네트워크 통합
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7d38505-cff5-4f15-9fd5-ae6dba15ce88
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 673cb5a2292bab113aefb1de37f80bf4d880b467
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433900"
---
# <a name="azure-virtual-network-integration"></a>Azure 가상 네트워크 통합

>적용 대상: Windows Server 2016 Essentials

클라우드 컴퓨팅에 대해 자체 방식을 확인 하는 조직에 거의 이동할 모든 해당 리소스의 100% 한 번에 있지만 대신 접근을 여기서 일부 리소스는 클라우드에서 및 온-프레미스에서 여전히 일부는. 이 하이브리드 접근 방식을 쉽게 뿐만 아니라 조직이 클라우드 컴퓨팅 리소스도 이동 되지만 새 하드웨어를 구입 하지 않고도 IT 인프라를 확장할 수 있도록 합니다.

이 하이브리드 접근 방식을 컴퓨팅을 구현, 서로 통신 하는 두 위치에서 리소스에 대 한 원활한 방법이 필요 합니다. Azure 가상 네트워킹은 지점간 P2P ()를 만들 수 있도록 하는 Azure 서비스 또는 사이트 간 (S2S) 가상 개인 네트워크 (예: 가상 머신 및 저장소) Azure 모양이 있는 것으로 실행 되는 리소스는 응용 프로그램 및 리소스에 대 한 원활한 액세스에 대 한 로컬 네트워크입니다.

Azure Virtual network의 구성이 복잡할 수 있습니다. Windows Server Essentials 2016을 사용 하 여 네트워크 환경에 가장 적합 한 기본값을 선택할 수 있도록 간단한 마법사를 통해 Azure 가상 네트워크를 쉽게 구성할 수 있습니다. 새 Azure 가상 네트워크 통합 작업을 통합을 시작 하려면 빠른 링크를 제공할 수 있을 뿐만 아니라 Azure 가상 네트워킹 소개 Windows Essentials 대시보드 Microsoft Cloud Services 섹션에 추가한 아래 스크린샷에 표시 된 것과 같이 .

![Windows Server Essentials 대시보드 홈 페이지의 시작 탭을 보여 주는 스크린샷. 시작 탭의 Services 섹션을 선택한 후 문서를 나타내고 대시보드 Microsoft 클라우드 서비스 통합에서 Azure Virtual network는 현재 사용 하지 않도록 합니다.](media/azure-virtual-network-1.PNG)

클릭할 때 합니다 **이제 통합** Microsoft Azure 계정에 로그인 하 라는 대화 상자가 나타납니다. 위의 스크린샷에서에서 Azure 가상 네트워킹에 대 한 링크입니다. Microsoft Azure 계정이 없으면 리디렉션됩니다 있습니다 Azure 계정 등록 포털에는이 화면에서 등록 하는 옵션을 해야 합니다.

![통합 된 Azure 가상 네트워크 마법사를 Microsoft Azure 로그인 페이지를 보여 주는 스크린샷.](media/azure-virtual-network-2.PNG)

일단 로그인에 Azure 나타납니다 Azure 가상을 사용 하 여 연결 하려는 구독을 선택 하는 옵션을 사용 하 여 서비스 네트워킹:

![Azure 가상 네트워크 마법사를 사용 하 여 통합의 Microsoft Azure 구독 내 페이지를 보여주는 스크린샷.](media/azure-virtual-network-3.PNG)

선택 하면 Azure 가상 네트워킹에 대 한 사용 하려는 Azure 구독을 새 Azure 가상 네트워크를 만드는 옵션을 사용 하 여 표시 됩니다 또는 하나가 이미 설치 되어이 구독 아래에 하는 경우 드롭다운 목록 상자를 사용할 수 있는 표시 됩니다. 또한 Azure Virtual network가 로컬 네트워크에서 리소스를 식별 하는 데 사용할 로컬 네트워크의 이름을 선택 합니다. 마지막으로 호스팅될 하기 위해 Azure 가상 네트워크를 만들려는 Azure 지역을 선택 합니다. 로컬 네트워크에 가장 가까운가 실제로 있는 위치를 선택 하는 것은 일반적으로 가장 적합 한 Azure 서비스에 호스트할 수 있습니다 하는 리소스와 통신 하기 위한 대역폭 속도 최적화:

![통합 된 Azure 가상 네트워크 마법사의 집합을 Azure 가상 네트워크 페이지를 보여주는 스크린샷.](media/azure-virtual-network-4.PNG)

통합 프로세스의 마지막 단계는 S2S VPN 연결에 사용할 VPN 장치를 설정 하는 것입니다. 기본적으로 선택 리소스는 VPN 서버와 Windows Server Essentials 서버를 설정 해야 합니다 이므로 대부분의 소규모 사업체 몇 서버만 해당 환경에 올바르게 Microsoft Azure에 연결할 VPN 라우터를 구성 하려면 IT 직원 부족, 로컬 네트워크에 연결 된 Azure 가상 네트워크의 리소스에 액세스 하기 위해. 그러나 사용 하려는 다른 서버 환경에서 VPN 서버 또는 VPN 라우터 사용 하려는 경우 이러한 옵션을 선택할 수 있습니다.

라우터 형식 및 모델 변형,으로 인해 Windows Server Essentials를 자동으로 VPN 라우터를 구성 하지 않습니다. 연결을 위해 Azure에서 필요한 적절 한 라우팅 구성에 대 한 장치 유형의 Azure 가상 네트워킹을 알림만이 통합 마법사에서 VPN 라우터를 선택 합니다.

통합 마법사를 완료 하면 새 탭은 Azure 가상 네트워킹에 대 한 Windows Server Essentials 대시보드에 표시 됩니다.

![Windows Server Essentials 대시보드의 Azure VNet 페이지를 보여 주는 스크린샷. Azure 가상 네트워크 탭을 선택 하 고 구성으로 상태를 보여 줍니다.](media/azure-virtual-network-5.PNG)

>! 클라우드에서 Azure Virtual network의 구성을 완료 하는 참고 위쪽으로 30 분에 시간이 오래 걸릴 수 있습니다. 이 시간 동안 구성의 상태는 대시보드는 Azure 가상 네트워크 상태 페이지에 표시 됩니다.

Azure 가상 네트워크의 구성을 완료 되 면 상태 연결 됨으로 변경 하 고 Azure 가상 네트워크 게이트웨이 IP 주소에서 데이터를, 로컬 IP 주소 및 계정 세부 정보 등의 세부 정보를 표시 합니다.

![Windows Server Essentials 대시보드의 Azure VNet 페이지를 보여 주는 스크린샷. Azure 가상 네트워크 탭을 선택 하 고, 연결 됨 '으로 상태를 표시 하 고이 상태 정보 아래에 있는 가상 네트워크의 세부 정보가 표시 됩니다.](media/azure-virtual-network-6.PNG)

대시보드의 오른쪽에 있는 작업 창에는 수행할 수 있는 Azure 가상 네트워크를 사용 하 여 다양 한 작업을 합니다.

-   **Azure VNET에서 연결 끊기** Azure Virtual network를 설정 하는 것은 무료 이지만 온-프레미스 및 Azure에서 다른 Vnet에 연결 하는 VPN gateway에 대 한 요금은 합니다. Azure VNET에서 연결을 끊는 모든 청구가 중지 됩니다.

-   **VPN 장치를 통해 전환** VPN 라우터를 VPN 서버에서 변경 하려는 하는 경우에이 작업 수 전환 하 고 Azure VNET에 게 알립니다.

-   **Azure VNET 구성** 이 작업을 사용 하면 Azure VNET에 대 한 Azure portal 구성 페이지로 리디렉션하여 Azure VNET의 고급 구성 옵션을 변경할 수 있습니다.

-   **상태 새로 고침** 입/출력 데이터를 포함 하 여 Azure VNET의 연결 상태를 업데이트, 상태 페이지를 새로 고칩니다.

-   **Azure VNET 통합 사용 안 함** Azure VNET을 연결 끊김 및 Windows Server Essentials 대시보드에서 통합을 제거 합니다. Note는 Azure VNET을 삭제 하지 않습니다, 나중에 대시보드를 사용 하 여 다시 Azure VNET에 통합 하려는 경우 Azure에서 설정이 계속 유지 됩니다.

-   **Azure VNET에 자세히 알아보려면** [ https://azure.microsoft.com/services/virtual-network/ ](https://azure.microsoft.com/services/virtual-network/)합니다.

<a name="see-also"></a>참조
--------
[Windows Server Essentials 시작](get-started.md)
