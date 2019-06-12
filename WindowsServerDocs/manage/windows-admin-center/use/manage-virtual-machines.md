---
title: Windows Admin Center 사용 하 여 Virtual Machines 관리
description: Hyper-v 호스트 및 Windows Admin Center (프로젝트 브라 티)를 사용 하 여 virtual machines 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 84e1ce7864f04550ee25253bcf038afdd7b919fe
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811680"
---
# <a name="managing-virtual-machines-with-windows-admin-center"></a>Windows Admin Center 사용 하 여 Virtual Machines 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

가상 컴퓨터 도구는에서 사용할 수 있습니다 [Server](manage-servers.md)를 [장애 조치 클러스터](manage-failover-clusters.md) 또는 [Hyper-Converged 클러스터](manage-hyper-converged.md) 서버 또는 클러스터에서 Hyper-v 역할을 사용 하는 경우 연결 합니다. 가상 컴퓨터 도구를 사용 하 여 Windows Server 2012를 실행 하는 Hyper-v 호스트를 관리 하려면 또는 데스크톱 경험 또는 Server Core 설치 중 하나는 나중에 있습니다. Hyper-V Server 2012, 2016 및 2019도 지원 됩니다.

## <a name="key-features"></a>주요 기능

Windows Admin Center는 가상 머신 도구의 주요 기능은 다음과 같습니다.

- **고급 Hyper-v 호스트 리소스 모니터링 합니다.** 하나의 대시보드에서 전체 CPU 및 메모리 사용량, IO 성능 메트릭, VM 상태 경고 및 Hyper-v 호스트 서버 또는 전체 클러스터에 대 한 이벤트를 봅니다.
- **Hyper-v 관리자 및 장애 조치 클러스터 관리자 기능을 결합 하는 통합 된 환경.** 클러스터 전체에 걸쳐 모든 가상 컴퓨터를 확인 하거나 고급 관리 및 문제 해결에 대 한 단일 가상 컴퓨터를 드릴 다운 합니다.
- **가상 컴퓨터 관리에 대 한 간단한 강력 하 고 워크플로.** 새 UI 환경을 만들고 관리 하 고 가상 머신을 복제 하는 IT 관리 시나리오에 맞게 합니다.

다음은 일부의 Windows Admin Center 수행할 수 있는 Hyper-v 작업:

- [Hyper-v 호스트 리소스 및 성능 모니터링](#monitor-hyper-v-host-resources-and-performance)
- [가상 컴퓨터 인벤토리 보기](#view-virtual-machine-inventory)
- [새 가상 머신 만들기](#create-a-new-virtual-machine)
- [가상 머신 설정 변경](#change-virtual-machine-settings)
- [다른 클러스터 노드로 가상 컴퓨터 실시간 마이그레이션](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [고급 관리 및 단일 가상 머신에 대 한 문제 해결](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [Hyper-v 호스트 (VMConnect)을 통해 가상 머신을 관리합니다](#manage-a-virtual-machine-through-the-hyper-v-host-vmconnect)
- [Hyper-v 호스트 설정 변경](#change-hyper-v-host-settings)
- [Hyper-v 이벤트 로그 보기](#view-hyper-v-event-logs)
- [Azure Site Recovery를 사용 하 여 가상 머신 보호](#protect-virtual-machines-with-azure-site-recovery)

## <a name="monitor-hyper-v-host-resources-and-performance"></a>Hyper-v 호스트 리소스 및 성능 모니터링

![Virtual Machines 요약 화면](../media/manage-virtual-machines/virtual-machines-summary.png)

1. 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 맨 위에 있는 탭 두 개가 합니다 **Virtual Machines** 도구를 **요약** 탭 및 **인벤토리** 탭. 합니다 **요약** 탭은 Hyper-v 호스트 리소스 및 현재 서버에 다음을 비롯 한 전체 클러스터 성능에 대 한 통찰력을 제공 합니다.
    - Off 이면 실행-상태별로 그룹화 하는 Vm 수가 일시 중지 및 저장
    - 최근 상태 경고 또는 Hyper-v 이벤트 로그 이벤트 (에 경고를 Windows Server 2016을 실행 하는 하이퍼 수렴 형 클러스터에 사용할 수 있는 이상)
    - 호스트 및 게스트에 대 한 분석을 사용 하 여 CPU 및 메모리 사용량
    - 가장 많은 CPU 및 메모리 리소스를 사용 하는 상위 Vm
    - 실시간 및 과거 데이터 IO 및 IOPS 처리량에 대 한 차트 줄 (저장소 성능 꺾은선형 차트는만 이상 Windows Server 2016을 실행 하는 하이퍼 수렴 형 클러스터에 사용할 수 있습니다. 기록 데이터를 Windows Server 2019를 실행 하는 하이퍼 수렴 형 클러스터 수만)

## <a name="view-virtual-machine-inventory"></a>가상 컴퓨터 인벤토리 보기

![Virtual Machines 인벤토리 화면](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 맨 위에 있는 탭 두 개가 합니다 **Virtual Machines** 도구를 **요약** 탭 및 **인벤토리** 탭. 합니다 **인벤토리** 탭 현재 서버 또는 전체 클러스터에서 사용할 수 있는 가상 컴퓨터를 나열 하 고 개별 가상 컴퓨터를 관리 하는 명령을 제공 합니다. 다음 작업을 수행할 수 있습니다.
    - 현재 서버 또는 클러스터에서 실행 중인 가상 컴퓨터의 목록을 봅니다.
    - 클러스터에 대 한 가상 컴퓨터를 보면 가상 머신의 상태와 호스트 서버를 보여 줍니다. 메모리 부족, 메모리 수요가 및 할당 된 메모리 및 가상 컴퓨터의 가동 시간, 하트 비트 상태 및 Azure Site Recovery를 사용 하 여 보호 상태를 포함 하 여 호스트 관점에서 CPU 및 메모리 사용량을 볼 수도 있습니다.
    - [새 가상 머신을 만들](#create-a-new-virtual-machine)합니다.
    - 삭제, 시작, 해제, 종료, 일시 중지, 다시 시작, 다시 설정 또는 가상 컴퓨터를 이름을 바꿉니다. 가상 컴퓨터 저장, 저장된 된 상태를 삭제 하거나 검사점을 만들 수도 있습니다.
    - [가상 컴퓨터에 대 한 설정을 변경](#change-virtual-machine-settings)합니다.
    - VMConnect를 사용 하 여 Hyper-v 호스트를 통해 가상 머신 콘솔에 연결 합니다.
    - [Azure Site Recovery를 사용 하 여 가상 머신을 복제](#protect-virtual-machines-with-azure-site-recovery)합니다.
    - 종료, 저장, 일시 중지, 시작 등의 여러 Vm에서 실행할 수 있는 작업에 대 한 삭제를 다시 설정, 여러 Vm을 선택 하 고 작업을 한 번에 실행할 수 있습니다.

참고: 클러스터에 연결 하는 경우 가상 컴퓨터 도구는 클러스터 된 가상 컴퓨터만 표시 됩니다. 또한 나중에 클러스터 되지 않은 가상 컴퓨터를 표시 하려면 예정입니다.

## <a name="create-a-new-virtual-machine"></a>새 가상 컴퓨터 만들기

![새 가상 머신 화면 만들기](../media/manage-virtual-machines/new-vm.png)

1. 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 가상 컴퓨터 도구의 맨 위에 있는 선택 합니다 **인벤토리** 탭을 클릭 한 다음 **새로 만들기** 새 가상 머신을 만들려면.
3. 가상 컴퓨터 이름을 입력 하 고 1 및 2 세대 가상 컴퓨터 중에서 선택 합니다.
4. 클러스터에서 가상 컴퓨터를 만들려는 경우 처음에 가상 컴퓨터를 만드는 호스트를 선택할 수 있습니다. Windows Server 2016 이상을 실행 하는 경우이 도구를 호스트 권장 사항을 제공 합니다.
5. 가상 머신 파일에 대 한 경로 선택 합니다. 드롭다운 목록에서 볼륨을 선택 하거나 클릭 **찾아보기** 폴더 선택기를 사용 하 여 폴더를 선택 합니다. 가상 머신 구성 파일과 가상 하드 디스크 파일에서 단일 폴더에 저장 됩니다는 `\Hyper-V\\[virtual machine name]` 선택한 볼륨의 경로 경로입니다.

   >[!Tip]
   > 폴더 선택에서 이동할 수 있습니다 네트워크의 모든 사용 가능한 SMB 공유의 경로 입력 하 여 합니다 **폴더 이름** 필드를 ```\\server\share```입니다. VM 저장소는 필요에 대 한 네트워크 공유를 사용 하 여 [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)합니다.

6. 중첩 된 가상화를 사용 하려면, 메모리 설정, 네트워크 어댑터, 가상 하드 디스크를 구성 하 고.iso 이미지 파일에서 또는 네트워크에서 운영 체제를 설치할 것인지 여부를 선택 하는지 여부를 가상 프로세서의 수를 선택 합니다.
7. **만들기**를 클릭하여 가상 컴퓨터를 만듭니다.
8. 가상 머신을 만들고 가상 컴퓨터 목록에 표시 됩니다, 가상 컴퓨터를 시작할 수 있습니다.
9. 가상 머신이 시작 되 면 운영 체제를 설치 하는 VMConnect 통해 가상 머신의 콘솔에 연결할 수 있습니다. 목록에서 가상 컴퓨터를 선택, 클릭 **자세한** > **Connect** .rdp 파일을 다운로드 합니다. 원격 데스크톱 연결 앱에.rdp 파일을 엽니다. 가상 머신의 콘솔에 연결할은이 때문에 Hyper-v 호스트의 관리자 자격 증명을 입력 해야 합니다.

## <a name="change-virtual-machine-settings"></a>가상 머신 설정 변경

![가상 머신 설정 화면](../media/manage-virtual-machines/vm-settings.png)

1. 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 가상 컴퓨터 도구의 맨 위에 있는 선택 된 **인벤토리** 탭 합니다. 목록에서 가상 컴퓨터를 선택 하 고 클릭 **자세한** > **설정을**합니다.
3. 사이 전환 합니다 **일반**, **보안**, **메모리**, **프로세서**를 **디스크**를 **네트워크**, **부팅 순서** 하 고 **검사점** , 탭 하 고, 필요한 설정을 구성 하 고, 클릭 **저장** 현재 탭을 저장 하려면 설정. 사용 가능한 설정을 가상 머신의 세대에 따라 달라 집니다. 또한 실행 중인 가상 컴퓨터에 대 한 일부 설정을 변경할 수 없습니다 하 고 가상 컴퓨터를 먼저 중지 해야 합니다.

## <a name="live-migrate-a-virtual-machine-to-another-cluster-node"></a>다른 클러스터 노드로 가상 컴퓨터 실시간 마이그레이션

클러스터에 연결 하는 경우 다른 클러스터 노드로 가상 컴퓨터를 실시간 마이그레이션할 수 있습니다.

1. 장애 조치 클러스터 또는 하이퍼 수렴 형 클러스터 연결을 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 가상 컴퓨터 도구의 맨 위에 있는 선택 된 **인벤토리** 탭 합니다. 목록에서 가상 컴퓨터를 선택 하 고 클릭 **자세한** > **이동**합니다.
3. 사용 가능한 클러스터 노드 목록에서 서버를 선택 하 고 클릭 **이동**합니다.
4. 이동 진행률에 대 한 알림은 Windows Admin Center 오른쪽 위 모서리에 표시 됩니다. 성공적으로 이동 하는 경우 가상 컴퓨터 목록에 변경 된 호스트 서버 이름을 표시 됩니다.

## <a name="advanced-management-and-troubleshooting-for-a-single-virtual-machine"></a>고급 관리 및 단일 가상 머신에 대 한 문제 해결

![단일 가상 머신 세부 정보 화면](../media/manage-virtual-machines/vm-details.png)

자세한 내용 및 단일 가상 머신 페이지에서 단일 가상 컴퓨터에 대 한 성능 차트를 볼 수 있습니다.

1. 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 가상 컴퓨터 도구의 맨 위에 있는 선택 된 **인벤토리** 탭 합니다. 가상 머신 목록에서 가상 머신의 이름을 클릭 합니다.
3. 단일 가상 머신 페이지에서 다음을 수행할 수 있습니다.
    - 가상 컴퓨터에 대 한 자세한 정보를 봅니다.
    - CPU, 메모리, 네트워크, IOPS 및 IO 처리량에 대 한 실시간 및 기록 데이터 꺾은선형 차트를 보려면 (기록 데이터를 Windows Server 2019를 실행 하는 하이퍼 수렴 형 클러스터에 사용할 수만)
    - 보기, 만들기, 적용, 이름 바꾸기 및 검사점을 삭제 합니다.
    - 가상 머신의 가상 하드 디스크 (.vhd) 파일, 네트워크 어댑터 및 호스트 서버에 대 한 정보를 봅니다.
    - 삭제, 시작, 해제, 종료, 일시 중지, 다시 시작, 다시 설정 또는 가상 컴퓨터를 이름을 바꿉니다. 가상 컴퓨터 저장, 저장된 된 상태를 삭제 하거나 검사점을 만들 수도 있습니다.
    - [가상 컴퓨터에 대 한 설정을 변경](#change-virtual-machine-settings)합니다.
    - VMConnect를 사용 하 여 Hyper-v 호스트를 통해 가상 머신 콘솔에 연결 합니다.
    - [Azure Site Recovery를 사용 하 여 가상 머신을 복제](#protect-virtual-machines-with-azure-site-recovery)합니다.

## <a name="manage-a-virtual-machine-through-the-hyper-v-host-vmconnect"></a>Hyper-v 호스트 (VMConnect)을 통해 가상 머신을 관리합니다

![웹 브라우저를 통해 VM에 연결](../media/manage-virtual-machines/vm-connect.png)

1. 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 가상 컴퓨터 도구의 맨 위에 있는 선택 된 **인벤토리** 탭 합니다. 목록에서 가상 컴퓨터를 선택 하 고 클릭 **자세한** > **Connect** 하거나 **다운로드 한 RDP 파일**합니다. **연결** Windows Admin Center 통합 하는 원격 데스크톱 웹 콘솔을 통해 게스트 VM 사용 하 여 상호 작용할 수 있게 됩니다. **RDP 파일 다운로드** 원격 데스크톱 연결 응용 프로그램 (mstsc.exe)를 사용 하 여 열 수 있는.rdp 파일이 다운로드 됩니다. 두 옵션 모두 VMConnect를 사용 하 여 Hyper-v 호스트를 통해 게스트 VM에 연결 하는 하 고 Hyper-v 호스트 서버에 대 한 관리자 자격 증명을 입력 해야 합니다.

## <a name="change-hyper-v-host-settings"></a>Hyper-v 호스트 설정 변경

![Hyper-v 호스트 설정 화면](../media/manage-virtual-machines/host-settings.png)

1. 서버, 하이퍼 수렴 형 클러스터 또는 장애 조치 클러스터 연결을 클릭 합니다 **설정을** 왼쪽 탐색 창의 맨 위에 있는 메뉴.
2. Hyper-v 호스트 서버 또는 클러스터에서에 표시 됩니다는 **Hyper-v 호스트 설정** 다음 섹션이 포함 된 그룹:
    - 일반: 하이퍼바이저 및 가상 하드 디스크 및 가상 컴퓨터 파일 경로 변경, 일정 유형 (지원) 하는 경우
    - 고급 세션 모드
    - NUMA 스패닝
    - 실시간 마이그레이션
    - 저장소 마이그레이션
3. 하이퍼 수렴 형 클러스터 또는 장애 조치 클러스터 연결의 설정 변경 내용을 모든 Hyper-v 호스트를 변경한 경우 변경 내용은 모든 클러스터 노드에 적용 됩니다.

## <a name="view-hyper-v-event-logs"></a>Hyper-v 이벤트 로그 보기

가상 머신 도구에서 직접 Hyper-v 이벤트 로그를 볼 수 있습니다.

1. 클릭 합니다 **가상 머신** 왼쪽 탐색 창에서 도구입니다.
2. 가상 컴퓨터 도구의 맨 위에 있는 선택 된 **요약** 탭 합니다. 오른쪽 위의 이벤트 섹션에서 클릭 **모든 이벤트 보기**합니다.
3. 이벤트 뷰어 도구 왼쪽된 창에서 하이퍼-V 이벤트 채널 표시 됩니다. 오른쪽 창에서 이벤트를 확인 하는 채널을 선택 합니다. 장애 조치 클러스터 또는 하이퍼 수렴 형 클러스터를 관리 하는 경우 호스트 서버 컴퓨터 열에 표시 하는 모든 클러스터 노드에 대 한 이벤트의 이벤트 로그에 표시 됩니다.

## <a name="protect-virtual-machines-with-azure-site-recovery"></a>Azure Site Recovery를 사용 하 여 가상 머신 보호

Azure Site Recovery를 구성 하 고 Azure에 온-프레미스 가상 컴퓨터를 복제 하려면 Windows Admin Center 사용할 수 있습니다. [자세히 알아보기](../azure/azure-site-recovery.md)

## <a name="more-coming"></a>향후 추가 예정

Windows Admin Center 가상 컴퓨터 관리는 적극적으로 개발 하 고 새로운 기능을 가까운 시일 안에 추가 됩니다. UserVoice에서 상태 및 기능에 대해 투표를 볼 수 있습니다.

- [가상 컴퓨터 가져오기/내보내기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)
- [폴더의 정렬 가상 컴퓨터](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)
- [추가 가상 머신 설정을 지원합니다](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)
- [Hyper-v 복제본 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)
- [가상 컴퓨터의 소유권을 위임](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)
- [가상 컴퓨터 복제](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)
- [기존 가상 머신에서 템플릿 만들기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)
- [Hyper-v 호스트 간에 가상 컴퓨터 보기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)
- [새 가상 머신 창에서 VLAN을 구성 합니다.](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)

[모든 참조 또는 새로운 기능 제안](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D)합니다.
