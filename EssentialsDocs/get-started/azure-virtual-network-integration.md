---
title: Azure Virtual network 통합
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7d38505-cff5-4f15-9fd5-ae6dba15ce88
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 92c8241d861e72d5f9f409a334e6edbeed5eae4c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310572"
---
# <a name="azure-virtual-network-integration"></a>Azure Virtual network 통합

>적용 대상: Windows Server 2016 Essentials

조직에서 클라우드 컴퓨팅에 대 한 작업을 수행 하기 때문에 거의 모든 리소스를 한 번에 100% 이동 하는 것은 거의 없지만 일부 리소스는 클라우드에 있고 일부는 아직 온-프레미스에 있는 접근 방식을 사용 합니다. 이 하이브리드 접근 방식을 사용 하면 조직에서 일부 컴퓨팅 리소스를 클라우드로 쉽게 이동할 수 있을 뿐만 아니라 새로운 하드웨어를 획득 하지 않고도 IT 인프라를 확장할 수 있습니다.

이 하이브리드 방법을 컴퓨팅에 구현 하는 경우 두 위치의 리소스가 서로 통신 하는 원활한 방법이 필요 합니다. Azure 가상 네트워킹은 azure에서 실행 되는 리소스 (예: 가상 머신 및 저장소)가 Azure에서 실행 중인 리소스 (예: 가상 머신 및 저장소)를 만들 수 있도록 하는 azure 서비스입니다. 원활한 응용 프로그램 및 리소스 액세스를 위한 로컬 네트워크

Azure 가상 네트워크 구성은 복잡할 수 있습니다. Windows Server Essentials 2016를 사용 하면 네트워크 환경에 가장 적합 한 기본값을 선택 하는 데 도움이 되는 간단한 마법사를 통해 Azure Virtual network를 쉽게 구성할 수 있습니다. 아래 스크린샷에 표시 된 것 처럼 Azure 가상 네트워킹을 소개 하 고 통합을 시작 하기 위한 빠른 링크를 제공 하는 새로운 Azure Virtual network 통합 작업이 Windows Essentials 대시보드의 Microsoft 클라우드 Services 섹션에 추가 되었습니다. .

![Windows Server Essentials 대시보드의 홈 페이지에 있는 시작 탭을 보여 주는 스크린샷 시작 탭에서 서비스 섹션을 선택 하 고, 대시보드는 Azure Virtual network가 현재 사용 하지 않도록 설정 된 Microsoft 클라우드 Services 통합을 나타냅니다.](media/azure-virtual-network-1.PNG)

위의 스크린샷에서 Azure 가상 네트워킹에 대해 **지금 통합** 링크를 클릭 하면 Microsoft Azure 계정에 로그인 하 라는 대화 상자가 표시 됩니다. Microsoft Azure 계정이 없는 경우이 화면에서 등록 하는 옵션을 사용할 수 있습니다. 그러면 사용자가 Azure 계정 등록 포털로 리디렉션됩니다.

![Azure Virtual network와 통합 마법사의 Microsoft Azure에 로그인 페이지를 보여 주는 스크린샷](media/azure-virtual-network-2.PNG)

Azure에 로그인 하면 Azure 가상 네트워킹 서비스와 연결할 구독을 선택 하는 옵션이 제공 됩니다.

![Azure Virtual network와 통합 마법사의 내 Microsoft Azure 구독 페이지를 보여 주는 스크린샷](media/azure-virtual-network-3.PNG)

Azure 가상 네트워킹에 사용할 Azure 구독을 선택 하면 새 Azure 가상 네트워크를 만드는 옵션이 표시 됩니다. 또는이 구독에서 이미 설정 된 경우 드롭다운 상자에 사용할 수 있는 옵션이 표시 됩니다. 또한 Azure 가상 네트워크에서 로컬 네트워크의 리소스를 식별 하는 데 사용할 로컬 네트워크의 이름을 선택 합니다. 마지막으로, Azure Virtual network를 호스팅할 Azure 지역을 선택 합니다. 로컬 네트워크에 실제로 가장 가까운 위치를 선택 하는 것은 일반적으로 Azure 서비스에서 호스팅할 수 있는 리소스와 통신 하기 위한 대역폭 속도를 최적화 하는 데 가장 적합 합니다.

![Azure Virtual network와 통합 마법사의 Azure Virtual network 설정 페이지를 보여 주는 스크린샷](media/azure-virtual-network-4.PNG)

통합 프로세스의 마지막 단계는 S2S VPN 연결에 사용 되는 VPN 장치를 설정 하는 것입니다. 대부분의 소규모 기업은 자신의 환경에 소수의 서버만 있으므로 IT 직원이 Microsoft Azure에 연결 하기 위해 VPN 라우터를 제대로 구성 하지 못하는 경우, Windows Server Essentials 서버를 해당 리소스가 있는 VPN 서버로 설정 하는 것이 기본적으로 선택 됩니다. Azure 가상 네트워크의 리소스에 액세스 하기 위해 로컬 네트워크에서에 연결 합니다. 그러나 사용자 환경의 다른 서버를 VPN 서버로 사용 하거나 VPN 라우터를 사용 하는 경우에는 이러한 옵션을 선택할 수 있습니다.

라우터 유형과 모델의 변형으로 인해 Windows Server Essentials는 VPN 라우터를 자동으로 구성 하려고 하지 않습니다. 이 통합 마법사에서 VPN 라우터를 선택 하면 Azure에서 연결 하는 데 필요한 적절 한 라우팅 구성에 대해 장치 유형의 Azure 가상 네트워킹에만 알림이 표시 됩니다.

통합 마법사가 완료 되 면 Azure 가상 네트워킹을 위한 Windows Server Essentials 대시보드에 새 탭이 표시 됩니다.

![Windows Server Essentials 대시보드의 Azure VNet 페이지를 보여 주는 스크린샷 Azure 가상 네트워크 탭이 선택 되어 있으며 상태를 구성 중으로 표시 합니다.](media/azure-virtual-network-5.PNG)

>! 참고 클라우드에서 Azure Virtual network의 구성을 완료 하는 데는 30 분까지 시간이 오래 걸릴 수 있습니다. 이 시간 동안 구성 상태는 대시보드의 Azure Virtual network 상태 페이지에 표시 됩니다.

Azure 가상 네트워크의 구성이 완료 되 면 상태가 연결 됨으로 변경 되 고 Azure 가상 네트워크의 세부 정보 (예: 데이터 입력/출력, 게이트웨이 IP 주소, 로컬 IP 주소 및 계정 정보)가 표시 됩니다.

![Windows Server Essentials 대시보드의 Azure VNet 페이지를 보여 주는 스크린샷 Azure 가상 네트워크 탭이 선택 되 고 상태가 연결 됨으로 표시 되며,이 상태 정보 아래에 가상 네트워크에 대 한 세부 정보가 표시 됩니다.](media/azure-virtual-network-6.PNG)

대시보드의 오른쪽에 있는 작업 창에는 Azure Virtual network를 사용 하 여 수행할 수 있는 다양 한 작업이 있습니다.

-   **AZURE VNET에서 연결 끊기** Azure 가상 네트워크 설정은 무료 이지만 온-프레미스 및 Azure의 다른 Vnet에 연결 되는 VPN gateway에 대 한 요금이 청구 됩니다. Azure VNET에서 연결을 끊으면 모든 청구를 중지 합니다.

-   **VPN 장치를 통해 전환** VPN 서버에서 VPN 라우터로 변경 하려는 경우이 작업을 통해 스위치를 설정 하 고 Azure VNET에 알릴 수 있습니다.

-   **AZURE VNET 구성** 이 작업을 통해 azure vnet의 Azure Portal 구성 페이지로 리디렉션하여 Azure VNET의 고급 구성 옵션을 변경할 수 있습니다.

-   **상태 새로 고침** 상태 페이지를 새로 고쳐 데이터를 포함 하거나 데이터를 포함 하 여 Azure VNET의 연결 상태를 업데이트 합니다.

-   **Azure VNET 통합 사용 안 함** Azure VNET의 연결을 끊고 Windows Server Essentials 대시보드에서 통합을 제거 합니다. Azure vnet을 삭제 하지 않습니다. 나중에 Azure VNET을 대시보드와 다시 통합 하려는 경우에도 Azure에서 설정이 유지 됩니다.

-   **AZURE VNET 에 대해 자세히 알아보세요** [https://azure.microsoft.com/services/virtual-network/](https://azure.microsoft.com/services/virtual-network/).

<a name="see-also"></a>참고 항목
--------
[Windows Server Essentials 시작](get-started.md)
