---
title: Azure Site Recovery 서비스 통합
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/01/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 262701a6-8a97-4c4e-bfbf-9f8007c308d6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 29db78fdf38a6fab23d9a5ec5539c0606e2fbbaa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814486"
---
# <a name="azure-site-recovery-services-integration"></a>Azure Site Recovery 서비스 통합

>적용 대상: Windows Server 2016 Essentials

[Azure Site Recovery Services](https://docs.microsoft.com/azure/site-recovery/) 는 Azure에서 백업 자격 증명 모음에 VM (가상 머신)의 실시간 복제를 사용 하도록 설정 하 Microsoft Azure에서 제공 하는 서비스입니다. 하드웨어나 다른 오류로 인해 서버 또는 사이트의 작동이 중단 되는 경우, 백업 자격 증명 모음에 저장 된 VM 이미지가 Azure에서 실행 중인 VM으로 프로 비전 되는 Azure로 장애 조치할 수 있습니다. Azure 가상 네트워크와 함께 Azure로 장애 조치 (failover) 하는 경우 이전에 온-프레미스 서버에 연결 된 클라이언트 Pc가 Azure에서 실행 되는 서버에 투명 하 게 연결 됩니다.

Azure Site Recovery Services를 Windows Server Essentials와 통합 하는 것은 [Azure 가상 네트워킹](azure-virtual-network-integration.md)을 구성 하는 것과 같은 방식으로 시작 됩니다. 대시보드의 **Microsoft 클라우드 Services 통합** 페이지에서 대시보드의 오른쪽에 **있는 Azure Site Recovery 서비스와 통합** 을 클릭 합니다.

![Windows Server Essentials 대시보드의 홈 페이지에 있는 시작 탭을 보여 주는 스크린샷 시작 탭에서 서비스 섹션을 선택 하 고, 대시보드는 현재 Azure Recovery가 사용 하지 않도록 설정 된 Microsoft 클라우드 Services 통합을 나타냅니다.](media/azure-site-recovery-1.PNG)

Azure Virtual network 통합 및 Azure Backup 통합과 마찬가지로 기존 Azure 계정으로 Azure에 로그인 하거나 새 계정을 만들어야 합니다.

![Azure에 대 한 복제 사용 마법사의 Microsoft Azure에 로그인 페이지를 보여 주는 스크린샷 사용자가 Microsoft Azure에 아직 로그인 하지 않았기 때문에 로그인 단추가 표시 됩니다.](media/azure-site-recovery-2.PNG)

Azure에 성공적으로 로그인 하면 VM이 저장 되 고 호스팅될 Azure 지역 뿐만 아니라 Azure Site Recovery 서비스와 연결할 구독을 요청 하는 화면이 표시 됩니다.

![Azure에 대 한 복제 사용 마법사의 Microsoft Azure에 로그인 페이지를 보여 주는 스크린샷 사용자가 Microsoft Azure에 로그인 했으므로이 페이지는 구독, 저장소 계정 및 지역을 선택 하는 옵션을 제공 합니다.](media/azure-site-recovery-3.PNG)

구독 및 지역 선택 후에는 **Windows Server Essentials 대시보드에** **Azure 복구**라는 새 탭이 표시 됩니다. 네트워킹 검색은 지원 되는 호스트 서버 (Windows Server Hyper-v 2012 R2 이상 실행) 뿐만 아니라 개별 호스트의 가상 컴퓨터 (게스트)를 식별 하 고 열거 하기 위해 수행 됩니다.

![Windows Server Essentials 대시보드의 Azure 복구 페이지를 보여 주는 스크린샷 이러한 호스트에서 실행 되는 가상 컴퓨터와 함께 두 개의 Hyper-v 호스트가 표시 됩니다. 호스트 ramh157v01에서 이름이 m m-7 인 가상 컴퓨터를 선택 하 고이 가상 컴퓨터에 대해 Azure로의 복제를 현재 사용할 수 없습니다.](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>보호를 위해 게스트 가상 컴퓨터 사용

Azure 복구 창에 있는 가상 컴퓨터를 선택 하면 대시보드의 오른쪽에 있는 **azure로 복제 사용** 을 클릭 하 여 azure에 가상 컴퓨터 &trade;s 이미지를 준비 하 고 복사할 수 있습니다.

![Azure로 복제 사용 대화 상자를 보여 주는 스크린샷 호스트를 추가 하는 중에 진행률 표시줄이 표시 됩니다.](media/azure-site-recovery-5.PNG)

이 과정에서 Azure Site Recovery Service agent는 호스트 서버에 설치 되 고, 게스트 VM의 이미지가 저장 되는 백업 자격 증명 모음이 만들어지고, Azure로의 이미지 복제가 시작 됩니다. 복제 중인 VM의 크기에 따라 복제 프로세스를 완료 하는 데 몇 시간 또는 몇 일이 걸릴 수 있습니다. 전체 VM 이미지와 최신 델타를 Azure에 복제할 때까지 장애 조치 (failover) 작업을 사용할 수 없으며 VM이 보호 되지 않습니다. 복제가 완료 되 면 Azure 복구 창의 보호 상태 열이 사용: **복제** 에서 **사용**으로 변경 됩니다.

![Windows Server Essentials 대시보드의 Azure 복구 페이지를 보여 주는 스크린샷 이러한 호스트에서 실행 되는 가상 컴퓨터와 함께 두 개의 Hyper-v 호스트가 표시 됩니다. Ramh12v02 호스트의 가상 컴퓨터를 선택 하 고이 가상 컴퓨터에 대해 Azure로의 복제를 현재 사용할 수 있습니다.](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>게스트 VM을 Azure로 장애 조치 (Failover)

![Azure로 장애 조치 (Failover) VM 페이지를 보여 주는 스크린샷](media/azure-site-recovery-7.PNG)

보호 되는 가상 머신이 실패 하거나 보호 된 가상 머신이 실행 되는 호스트 서버가 실패 하는 경우 온-프레미스 가상 머신 또는 호스트 서버가 복구 되 고 사용 가능 해질 때까지 비즈니스 연속성을 유지 하기 위해 Azure로 장애 조치 (failover)를 수행할 수 있습니다. 위의 그림에 나와 있는 것 처럼 Azure Site Recovery Services에서 지원 되는 세 가지 유형의 장애 조치 (failover)가 있습니다.

-   **테스트 장애 조치 (Failover)** ƒA 정상 재해 복구 계획은 재해를 시뮬레이션 하는 기능을 통합 하 여 실제 재해가 발생 한 경우 가동 중지 시간을 최소화 합니다. 테스트 장애 조치 (Failover)는 복구 자격 증명 모음에 복제 된 VM 이미지를 사용 하 여 Azure에서 실행 중인 가상 머신으로 프로 비전 하 고 서버에 연결 하 여 비즈니스에 적용 되는 시나리오를 테스트할 수 있도록 합니다. 테스트 장애 조치 (failover) 중에는 재해 복구 테스트 중에 비즈니스를 방해 하지 않도록 로컬 가상 머신은 중단 없이 계속 실행 됩니다. 테스트 장애 조치 (Failover)가 완료 되 면 가상 머신을 프로 비전 해제 하 고 VHD를 삭제 하는 Azure Portal을 통해 테스트를 중지 합니다. 전체 테스트 장애 조치 (failover) 중에 복구 자격 증명 모음에 있는 VM 이미지는 발생 한 적이 없는 것 처럼 계속 해 서 온사이트 VM에서 복제 됩니다.

-   **계획 되지 않은 장애 조치 (failover** ) ƒAn 계획 되지 않은 장애 조치 (failover)는 호스트 서버에서 실행 되는 보호 된 호스트 서버 또는 VM의 실제 오류가 있을 때 발생 장애 조치 (failover)는 Windows Server Essentials 대시보드에서 수동으로 트리거하거나 오류가 발생 한 서버 자체가 Windows Server Essentials를 실행 하는 서버인 경우 Azure Portal에서 직접 트리거할 수 있습니다. 이 경우 계획 되지 않은 장애 조치 (Failover)는 복구 자격 증명 모음에 복제 된 VM 이미지를 사용 하 여 Azure에서 실행 중인 가상 머신으로 프로 비전 하며, 서버에 연결 하 여 비즈니스에 적용 되는 시나리오를 테스트할 수 있습니다. 서버를 온-프레미스에서 복원 하는 경우 Azure Portal에서 수동 장애 복구 (failback)를 트리거한 후 VM 이미지를 로컬 서버에 다시 복사할 수 있습니다.

-   계획 된 **장애 조치 (Failover)** ƒA 계획 된 장애 조치 (failover)는 계획 된 활동 (예: HW 유지 관리)이 서버 작동 중단을 수행 해야 하는 경우 수행할 수 있는 작업입니다. 계획 된 장애 조치 (failover) 시 Azure에서 복제 된 VM 이미지를 프로 비전 하는 것과 관련 하 여 동일한 프로세스가 수행 됩니다. 그러나 이렇게 하기 전에 로컬 서버가 종료 되기 전에 모든 변경 내용이 Azure에 복제 되도록 순차적으로 종료 됩니다. 계획 된 유지 관리가 완료 되 면 Windows Server Essentials 대시보드에서 장애 복구를 수동으로 트리거할 수 있습니다. 그러면 로컬 서버를 가져온 다음 Azure에서 VM을 프로 비전 해제 하 고를 삭제 하는 Azure Portal. VHD 파일. 온-프레미스 VM에서 Azure로의 복제는 정상적으로 계속 해 서 수행 됩니다.

위의 세 가지 경우에서 VM이 Azure로 장애 조치 (failover) 되 면 Windows Server Essentials 대시보드는 아래 그림과 같이 Azure에서 실행 되는 새 VM을 표시 합니다.

![Windows Server Essentials 대시보드의 Azure 복구 페이지를 보여 주는 스크린샷 Essentials 라는 호스트에 대해 Azure로의 복제를 사용 하도록 설정 했 고 Azure에서 실행 되는 Essentials-Test 라는 가상 머신은 호스트가 Azure로 장애 조치 (failover) 되었음을 나타냅니다.](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>참고 항목
--------
[Windows Server Essentials 시작](get-started.md)
