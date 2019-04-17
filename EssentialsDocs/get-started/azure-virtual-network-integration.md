---
title: "Azure 가상 네트워크 통합"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 21057359967c73d8d9fc434694b8f203ad5c1f6a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
#<a name="azure-virtual-network-integration"></a>Azure 가상 네트워크 통합

>Windows Server 2016 Essentials에 적용 됩니다.

조직에서는 클라우드 컴퓨팅을 하 게,으로 거의 모든 리소스가 100% 한 번에 이동, 되지만 대신 접근는 몇 가지 리소스는 클라우드에서 장소와 일부는 온-프레미스 여전히 합니다. 이 하는 방법도 쉽게 뿐 아니라 조직에서는 클라우드를 일부 컴퓨팅 리소스 이동에 대 한 하지만 획득 새 하드웨어를 않고도 IT 인프라 자랄 수 있도록 합니다.

하이브리드 이렇게 컴퓨팅을 구현 서로 통신할 수 원활 하 게 방법은 두 위치에에서 리소스에 대 한이 필요 합니다. Azure 가상 네트워킹 조직 지점 간 (P2P)를 만들 수 있도록 Azure 서비스 또는 인 사이트 (S2S) 가상 개인 네트워크를 실행 하는 Azure 가상 컴퓨터와 저장) (등 보입니다 응용 프로그램 및 리소스 원활 하 게 액세스 하는 로컬 네트워크에 있는 것으로 리소스는입니다.

Azure 가상 네트워크의 구성 복잡 한 될 수 있습니다. Windows Server Essentials 2016 네트워크 환경에 대 한 가장 적합 한 기본값을 선택할 수 있는 간단한 마법사를 통해 Azure 가상 네트워크 쉽게 구성할 수 있습니다. 스크린샷을 아래와 같이 새 Azure 가상 네트워크 통합 작업 Azure 가상 네트워킹 소개 하 고 통합 시작 하려면 바로 링크를 제공 하는 Windows 필수 패키지 대시보드의 Microsoft 클라우드 서비스 섹션을 추가 되었습니다.

![Windows Server Essentials 대시보드의 홈페이지에서 시작 탭을 보여 주는 스크린샷 합니다. 시작 탭 서비스 섹션을 선택한 후 하 고 Azure 가상 네트워크를 현재 사용할 수 없음을 Microsoft 클라우드 서비스 통합 아래 대시보드 나타냅니다.](media/azure-virtual-network-1.PNG)

클릭 하면는 **이제 통합** 위의 스크린샷에 Azure 가상 네트워킹에 대 한 링크는 대화 상자가 Microsoft Azure 계정에 로그인 하는 메시지가 표시 됩니다. Microsoft Azure 계정이 없는 경우에 리디렉션합니다는 계정 Azure 등록 portal에는이 화면에 하나의 등록 하는 옵션은 다음과 같습니다.

![통합 있는 Azure 가상 네트워크 마법사의 기호에 하려면 Microsoft Azure 페이지를 보여 주는 스크린샷 합니다.](media/azure-virtual-network-2.PNG)

로그인 하는 기능에 azure 되 면 나타납니다 Azure 가상와 연결을 원하는 어떤 구독을 선택할 수 있는 옵션으로 서비스 네트워킹:

![Azure 가상 네트워크 마법사 통합의 내 Microsoft Azure 구독 페이지를 보여 주는 스크린샷 합니다.](media/azure-virtual-network-3.PNG)

선택한 후 Azure 가상 네트워킹에 사용 하려는 Azure 구독 있는 Azure 가상 새 네트워크를 만들 수 있는 옵션이 나타납니다 또는 하나 이미 설정 되어에서이 구독을 없으면 드롭다운 상자를 사용할 수 표시 됩니다. 또한 Azure 가상 네트워크는 로컬 네트워크 리소스를 식별 하기 위해 사용 하는 로컬 네트워크의 이름을 선택 합니다. 마지막으로,을 호스트할 수 Azure 가상 네트워크 원하는 Azure 지역을 선택 합니다. 실제로 로컬 네트워크에 있는 위치를 선택 하는 것이 대역폭 속도 리소스 Azure 서비스에 개최 될 수 있습니다와 통신에 대 한 최적화 하기 위해 일반적으로 좋습니다.

![통합 있는 Azure 가상 네트워크 마법사의 설정를 Azure 가상 네트워크 페이지를 보여 주는 스크린샷 합니다.](media/azure-virtual-network-4.PNG)

통합 하는 프로세스의 마지막 단계에서 VPN 장치 S2S VPN 연결에 사용할 수를 설치 하는 것입니다. 가장 소기업 서버가 몇 환경에을 한 Microsoft Azure에 연결 하는 VPN 라우터 구성 하 고 IT 담당자 부족 하므로 리소스에 로컬 네트워크에 연결 하는 Azure 가상 네트워크 리소스에에서 액세스 하기 위해에 VPN 서버의와 Windows Server Essentials 서버 설정에 기본적으로 선택이 됩니다. 하지만 사용 하려는 다른 서버 귀하의 환경에 VPN 서버의으로 또는 VPN 라우터 사용 하려는 경우 해당 옵션을 선택할 수 있습니다.

라우터 유형 및 모델의 변동, 인해 Windows Server Essentials 자동으로 구성할 VPN 라우터 시도 하지 않습니다. Azure 가상 네트워킹을 적절 한 연결을 위해 필요한 Azure 라우팅 구성에 대 한 장치 형식의 알립니다만이 통합 마법사에서 VPN 라우터를 선택 합니다.

통합 마법사를 완료 되 면 새 탭 Azure 가상 네트워크에 대 한 Windows Server Essentials 대시보드에 표시 됩니다.

![Windows Server Essentials 대시보드의 Azure VNet 페이지를 보여 주는 스크린샷 합니다. Azure 가상 네트워크 탭이 선택 하 고 구성으로 상태를 보여 줍니다.](media/azure-virtual-network-5.PNG)

>! 클라우드에서 Azure 가상 네트워크의 구성을 완료 참고 걸릴 수 있습니다 시간이 오래 위쪽 30 분. 이 시간 동안 구성 상태 대시보드의 Azure 가상 네트워크 상태 페이지에 표시 됩니다.

Azure 가상 네트워크의 구성을 완료 되 면 상태가 연결을 변경 하 고 Azure 가상 데이터 시작/종료, 게이트웨이 IP 주소, IP 주소 및 계정 정보 로컬 네트워크의 세부 정보 표시 됩니다.

![Windows Server Essentials 대시보드의 Azure VNet 페이지를 보여 주는 스크린샷 합니다. Azure 가상 네트워크 탭을 선택 하 고 연결 됨, 상태로 표시 되 고이 상태 정보에서 가상 네트워크의 세부 정보 표시 됩니다.](media/azure-virtual-network-6.PNG)

작업 창 대시보드의 오른쪽에 있는 수행할 수 있는 Azure 가상 네트워크와 다양 한 작업 됩니다.

-   **Azure VNET에서 연결 끊기** Azure 가상 네트워크를 설정 하는 무료 인데 하는 온-프레미스와 기타 VNETs Azure에서 연결 하는 VPN 게이트웨이의 충전 합니다. 모든 청구를 중지 Azure VNET에서 분리 됩니다.

-   **VPN 디바이스를 통해 전환** VPN 라우터에 VPN 서버의에서 변경 하려는이 작업 수 있게 스위치를 확인 하 고 Azure VNET 알릴 수 있습니다.

-   **Azure VNET 구성** 이 작업 리디렉션하여 하 고 Azure 포털 구성 페이지에 Azure VNET에 대 한 고급 구성 옵션을 Azure VNET 변경할 수 있습니다.

-   **새로 고침 상태** 연결 상태에 / 아웃 데이터를 포함 하 여 Azure VNET 업데이트 상태 페이지를 새로 고칩니다.

-   **Azure VNET 통합 사용 안 함** Azure VNET의 연결이 끊어지기 및 Windows Server Essentials 대시보드에서 통합 제거 합니다. Note Azure VNET 삭제 되지는 않습니다, 나중에 다시 부합 Azure VNET 대시보드 하려는 경우 Azure에서 설정이 계속 유지 됩니다.

-   **더 많은 대 한 Azure VNET 알아보세요**[https://azure.microsoft.com/en-us/services/virtual-network/](https://azure.microsoft.com/en-us/services/virtual-network/)합니다.

<a name="see-also"></a>참조 하십시오
--------
[Windows Server Essentials 시작](get-started.md)
