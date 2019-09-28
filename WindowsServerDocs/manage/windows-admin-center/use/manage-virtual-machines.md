---
title: Windows 관리 센터를 사용 하 여 Virtual Machines 관리
description: Windows 관리 센터 (Project Honolulu)를 사용 하 여 Hyper-v 호스트 및 가상 컴퓨터 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 02a33383b466e8bade2db0bbddaff66f0196954c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356862"
---
# <a name="managing-virtual-machines-with-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 Virtual Machines 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

서버 또는 클러스터에서 Hyper-v 역할을 사용 하는 경우 [서버](manage-servers.md), [장애 조치 (Failover) 클러스터](manage-failover-clusters.md) 또는 [하이퍼 수렴 형 클러스터](manage-hyper-converged.md) 연결에서 Virtual Machines 도구를 사용할 수 있습니다. Virtual Machines 도구를 사용 하 여 Windows Server 2012 이상을 실행 하는 Hyper-v 호스트 (데스크톱 경험을 사용 하 여 설치 하거나 Server Core로 설치)를 관리할 수 있습니다. Hyper-v 서버 2012, 2016 및 2019도 지원 됩니다.

## <a name="key-features"></a>주요 기능

Windows 관리 센터에서 Virtual Machines 도구의 주요 사항은 다음과 같습니다.

- **높은 수준의 Hyper-v 호스트 리소스 모니터링** 단일 대시보드의 전체 CPU 및 메모리 사용량, IO 성능 메트릭, Hyper-v 호스트 서버 또는 전체 클러스터에 대 한 VM 상태 경고 및 이벤트를 확인 합니다.
- **Hyper-v 관리자 및 장애 조치(Failover) 클러스터 관리자 기능을 함께 제공 하는 통합 환경** 클러스터의 모든 가상 머신을 보고 고급 관리 및 문제 해결을 위해 단일 가상 머신으로 드릴 다운 합니다.
- **가상 컴퓨터 관리를 위한 단순화 된 간단한 워크플로.** 가상 머신을 만들고, 관리 하 고, 복제 하기 위해 IT 관리 시나리오에 맞게 조정 된 새로운 UI 환경

Windows 관리 센터에서 수행할 수 있는 몇 가지 Hyper-v 작업은 다음과 같습니다.

- [Hyper-v 호스트 리소스 및 성능 모니터링](#monitor-hyper-v-host-resources-and-performance)
- [가상 컴퓨터 인벤토리 보기](#view-virtual-machine-inventory)
- [새 가상 컴퓨터 만들기](#create-a-new-virtual-machine)
- [가상 컴퓨터 설정 변경](#change-virtual-machine-settings)
- [가상 컴퓨터를 다른 클러스터 노드로 실시간 마이그레이션](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [단일 가상 컴퓨터에 대 한 고급 관리 및 문제 해결](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [Hyper-v 호스트를 통해 가상 컴퓨터 관리 (VMConnect)](#manage-a-virtual-machine-through-the-hyper-v-host-vmconnect)
- [Hyper-v 호스트 설정 변경](#change-hyper-v-host-settings)
- [Hyper-v 이벤트 로그 보기](#view-hyper-v-event-logs)
- [Azure Site Recovery를 사용 하 여 가상 머신 보호](#protect-virtual-machines-with-azure-site-recovery)

## <a name="monitor-hyper-v-host-resources-and-performance"></a>Hyper-v 호스트 리소스 및 성능 모니터링

![Virtual Machines 요약 화면](../media/manage-virtual-machines/virtual-machines-summary.png)

1. 왼쪽 탐색 창에서 **Virtual Machines** 도구를 클릭 합니다.
2. **Virtual Machines** 도구, **요약** 탭 및 **인벤토리** 탭의 맨 위에는 두 개의 탭이 있습니다. **요약** 탭에서는 다음을 포함 하 여 현재 서버 또는 전체 클러스터에 대 한 hyper-v 호스트 리소스 및 성능을 전체적으로 보여 줍니다.
    - 상태별로 그룹화 되어 실행 중, 꺼짐, 일시 중지 및 저장 된 Vm 수
    - 최근 상태 경고 또는 Hyper-v 이벤트 로그 이벤트 (경고는 Windows Server 2016 이상을 실행 하는 하이퍼 수렴 형 클러스터에만 사용할 수 있음)
    - 호스트 vs 게스트 분석의 CPU 및 메모리 사용량
    - 가장 많이 사용 되는 CPU 및 메모리 리소스를 사용 하는 상위 Vm
    - IOPS 및 IO 처리량에 대 한 라이브 및 기록 데이터 꺾은선형 차트 (Storage performance 꺾은선형 차트는 Windows Server 2016 이상을 실행 하는 하이퍼 수렴 형 클러스터에만 사용할 수 있습니다. 기록 데이터는 Windows Server 2019를 실행 하는 하이퍼 수렴 형 클러스터에만 사용할 수 있습니다.

## <a name="view-virtual-machine-inventory"></a>가상 컴퓨터 인벤토리 보기

![Virtual Machines 인벤토리 화면](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. 왼쪽 탐색 창에서 **Virtual Machines** 도구를 클릭 합니다.
2. **Virtual Machines** 도구, **요약** 탭 및 **인벤토리** 탭의 맨 위에는 두 개의 탭이 있습니다. **인벤토리** 탭은 현재 서버 또는 전체 클러스터에서 사용할 수 있는 가상 컴퓨터를 나열 하 고 개별 가상 컴퓨터를 관리 하는 명령을 제공 합니다. 다음을 할 수 있습니다.
    - 현재 서버 또는 클러스터에서 실행 되는 가상 컴퓨터의 목록을 표시 합니다.
    - 클러스터에 대 한 가상 컴퓨터를 보고 있는 경우 가상 컴퓨터의 상태와 호스트 서버를 확인 합니다. 또한 Azure Site Recovery를 사용 하 여 메모리 부족, 메모리 수요 및 할당 된 메모리, 가상 컴퓨터의 작동 시간, 하트 비트 상태 및 보호 상태를 포함 하 여 호스트 관점의 CPU 및 메모리 사용량을 확인 합니다.
    - [새 가상 컴퓨터를 만듭니다](#create-a-new-virtual-machine).
    - 가상 컴퓨터를 삭제, 시작, 해제, 종료, 일시 중지, 다시 시작, 다시 설정 또는 이름을 바꿉니다. 또한 가상 컴퓨터를 저장 하거나 저장 된 상태를 삭제 하거나 검사점을 만듭니다.
    - [가상 컴퓨터에 대 한 설정을 변경](#change-virtual-machine-settings)합니다.
    - Hyper-v 호스트를 통해 VMConnect을 사용 하 여 가상 컴퓨터 콘솔에 연결 합니다.
    - [Azure Site Recovery를 사용 하 여 가상 컴퓨터를 복제](#protect-virtual-machines-with-azure-site-recovery)합니다.
    - 시작, 종료, 저장, 일시 중지, 삭제, 다시 설정 등 여러 Vm에서 실행할 수 있는 작업의 경우 여러 Vm을 선택 하 고 한 번에 작업을 실행할 수 있습니다.

참고: 클러스터에 연결 된 경우 가상 컴퓨터 도구는 클러스터 된 가상 컴퓨터만 표시 합니다. 또한 나중에 클러스터 되지 않은 가상 머신을 표시할 예정입니다.

## <a name="create-a-new-virtual-machine"></a>새 가상 컴퓨터 만들기

![새 가상 컴퓨터 만들기 화면](../media/manage-virtual-machines/new-vm.png)

1. 왼쪽 탐색 창에서 **Virtual Machines** 도구를 클릭 합니다.
2. Virtual Machines 도구 맨 위에서 **인벤토리** 탭을 선택한 다음 **새로** 만들기를 클릭 하 여 새 가상 컴퓨터를 만듭니다.
3. 가상 컴퓨터 이름을 입력 하 고 1 세대와 2 세대 가상 컴퓨터를 선택 합니다.
4. 클러스터에서 가상 컴퓨터를 만드는 경우 처음에 가상 컴퓨터를 만들 호스트를 선택할 수 있습니다. Windows Server 2016 이상을 실행 하는 경우 도구에서 호스트 권장 사항을 제공 합니다.
5. 가상 컴퓨터 파일의 경로를 선택 하십시오. 드롭다운 목록에서 볼륨을 선택 하거나 **찾아보기** 를 클릭 하 여 폴더 선택기를 사용 하 여 폴더를 선택 합니다. 가상 컴퓨터 구성 파일 및 가상 하드 디스크 파일은 선택한 볼륨 또는 경로의 `\Hyper-V\\[virtual machine name]` 경로 아래에 있는 단일 폴더에 저장 됩니다.

   >[!Tip]
   > 폴더 선택에서 **폴더 이름** 필드에 경로를 입력 하 여 네트워크에서 사용 가능한 SMB 공유를 찾을 수 있습니다 ```\\server\share```. VM 저장소에 네트워크 공유를 사용 하려면 [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)가 필요 합니다.

6. 가상 프로세서 수를 선택 하 고, 중첩 된 가상화를 사용 하도록 설정할지 여부를 선택 하 고, 메모리 설정, 네트워크 어댑터, 가상 하드 디스크를 구성 하 고, .iso 이미지 파일이 나 네트워크에서 운영 체제를 설치할지 여부를 선택 합니다.
7. **만들기**를 클릭하여 가상 컴퓨터를 만듭니다.
8. 가상 컴퓨터를 만들고 가상 컴퓨터 목록에 표시 되 면 가상 컴퓨터를 시작할 수 있습니다.
9. 가상 컴퓨터가 시작 되 면 VMConnect를 통해 가상 컴퓨터의 콘솔에 연결 하 여 운영 체제를 설치할 수 있습니다. 목록에서 가상 컴퓨터를 선택 하 고 **추가** > **연결** 을 클릭 하 여 .rdp 파일을 다운로드 합니다. 원격 데스크톱 연결 앱에서 .rdp 파일을 엽니다. 가상 컴퓨터의 콘솔에 연결 하는 중 이므로 Hyper-v 호스트의 관리자 자격 증명을 입력 해야 합니다.

## <a name="change-virtual-machine-settings"></a>가상 컴퓨터 설정 변경

![가상 컴퓨터 설정 화면](../media/manage-virtual-machines/vm-settings.png)

1. 왼쪽 탐색 창에서 **Virtual Machines** 도구를 클릭 합니다.
2. Virtual Machines 도구 맨 위에서 **인벤토리** 탭을 선택 합니다. 목록에서 가상 컴퓨터를 선택 하 고 **추가** > **설정**을 클릭 합니다.
3. **일반**, **보안**, **메모리**, **프로세서**, **디스크**, **네트워크**, **부팅 순서** 및 **검사점** 탭 사이를 전환 하 고 필요한 설정을 구성한 **후 저장을 클릭 하** 여 저장 합니다. 현재 탭의 설정입니다. 사용 가능한 설정은 가상 컴퓨터의 세대에 따라 달라 집니다. 또한 일부 설정은 가상 컴퓨터를 실행 하기 위해 변경할 수 없으며 먼저 가상 컴퓨터를 중지 해야 합니다.

## <a name="live-migrate-a-virtual-machine-to-another-cluster-node"></a>가상 컴퓨터를 다른 클러스터 노드로 실시간 마이그레이션

클러스터에 연결 된 경우 가상 컴퓨터를 다른 클러스터 노드로 실시간 마이그레이션할 수 있습니다.

1. 장애 조치 (Failover) 클러스터 또는 하이퍼 수렴 형 클러스터 연결에서 왼쪽 탐색 창에 있는 **Virtual Machines** 도구를 클릭 합니다.
2. Virtual Machines 도구 맨 위에서 **인벤토리** 탭을 선택 합니다. 목록에서 가상 컴퓨터를 선택 하 고 **추가** > **이동**을 클릭 합니다.
3. 사용 가능한 클러스터 노드 목록에서 서버를 선택 하 고 **이동**을 클릭 합니다.
4. 이동 진행에 대 한 알림이 Windows 관리 센터의 오른쪽 위 모서리에 표시 됩니다. 이동에 성공 하면 가상 컴퓨터 목록에서 호스트 서버 이름이 변경 된 것을 볼 수 있습니다.

## <a name="advanced-management-and-troubleshooting-for-a-single-virtual-machine"></a>단일 가상 컴퓨터에 대 한 고급 관리 및 문제 해결

![단일 가상 머신 세부 정보 화면](../media/manage-virtual-machines/vm-details.png)

단일 가상 컴퓨터 페이지에서 단일 가상 컴퓨터에 대 한 자세한 정보 및 성능 차트를 볼 수 있습니다.

1. 왼쪽 탐색 창에서 **Virtual Machines** 도구를 클릭 합니다.
2. Virtual Machines 도구 맨 위에서 **인벤토리** 탭을 선택 합니다. 가상 컴퓨터 목록에서 가상 컴퓨터의 이름을 클릭 합니다.
3. 단일 가상 컴퓨터 페이지에서 다음을 수행할 수 있습니다.
    - 가상 컴퓨터에 대 한 자세한 정보를 확인 합니다.
    - CPU, 메모리, 네트워크, IOPS 및 IO 처리량에 대 한 라이브 및 기록 데이터 꺾은선형 차트 보기 (기록 데이터는 Windows Server 2019를 실행 하는 하이퍼 수렴 형 클러스터에만 사용할 수 있음)
    - 검사점을 보고, 만들고, 적용 하 고, 이름을 바꾸고, 삭제 합니다.
    - 가상 컴퓨터의 가상 하드 디스크 (.vhd) 파일, 네트워크 어댑터 및 호스트 서버에 대 한 세부 정보를 확인 합니다.
    - 가상 컴퓨터를 삭제, 시작, 해제, 종료, 일시 중지, 다시 시작, 다시 설정 또는 이름을 바꿉니다. 또한 가상 컴퓨터를 저장 하거나 저장 된 상태를 삭제 하거나 검사점을 만듭니다.
    - [가상 컴퓨터에 대 한 설정을 변경](#change-virtual-machine-settings)합니다.
    - Hyper-v 호스트를 통해 VMConnect을 사용 하 여 가상 머신 콘솔에 연결 합니다.
    - [Azure Site Recovery를 사용 하 여 가상 컴퓨터를 복제](#protect-virtual-machines-with-azure-site-recovery)합니다.

## <a name="manage-a-virtual-machine-through-the-hyper-v-host-vmconnect"></a>Hyper-v 호스트를 통해 가상 컴퓨터 관리 (VMConnect)

![웹 브라우저를 통해 VM 연결](../media/manage-virtual-machines/vm-connect.png)

1. 왼쪽 탐색 창에서 **Virtual Machines** 도구를 클릭 합니다.
2. Virtual Machines 도구 맨 위에서 **인벤토리** 탭을 선택 합니다. 목록에서 가상 컴퓨터를 선택 하 고 **추가** > **연결** 또는 **RDP 파일 다운로드**를 클릭 합니다. **Connect** 를 통해 Windows 관리 센터에 통합 된 원격 데스크톱 웹 콘솔을 통해 게스트 VM과 상호 작용할 수 있습니다. **Rdp 파일 다운로드** 는 원격 데스크톱 연결 응용 프로그램 (mstsc)을 사용 하 여 열 수 있는 .rdp 파일을 다운로드 합니다. 두 옵션은 모두 VMConnect를 사용 하 여 Hyper-v 호스트를 통해 게스트 VM에 연결 하 고 Hyper-v 호스트 서버에 대 한 관리자 자격 증명을 입력 해야 합니다.

## <a name="change-hyper-v-host-settings"></a>Hyper-v 호스트 설정 변경

![Hyper-v 호스트 설정 화면](../media/manage-virtual-machines/host-settings.png)

1. 서버, 하이퍼 수렴 형 클러스터 또는 장애 조치 (Failover) 클러스터 연결에서 왼쪽 탐색 창의 맨 아래에 있는 **설정** 메뉴를 클릭 합니다.
2. Hyper-v 호스트 서버 또는 클러스터에서 다음 섹션을 포함 하는 **Hyper-v 호스트 설정** 그룹이 표시 됩니다.
    - 범주로 가상 하드 디스크 및 가상 머신 파일 경로 및 하이퍼바이저 일정 유형 변경 (지원 되는 경우)
    - 고급 세션 모드
    - NUMA 스패닝
    - 실시간 마이그레이션
    - 저장소 마이그레이션
3. 하이퍼 수렴 형 클러스터 또는 장애 조치 (Failover) 클러스터 연결에서 Hyper-v 호스트 설정을 변경 하는 경우 모든 클러스터 노드에 변경 내용이 적용 됩니다.

## <a name="view-hyper-v-event-logs"></a>Hyper-v 이벤트 로그 보기

Virtual Machines 도구에서 직접 Hyper-v 이벤트 로그를 볼 수 있습니다.

1. 왼쪽 탐색 창에서 **Virtual Machines** 도구를 클릭 합니다.
2. Virtual Machines 도구 위쪽에서 **요약** 탭을 선택 합니다. 오른쪽 위에 있는 이벤트 섹션에서 **모든 이벤트 보기**를 클릭 합니다.
3. 이벤트 뷰어 도구는 왼쪽 창에 Hyper-v 이벤트 채널을 표시 합니다. 오른쪽 창에서 이벤트를 볼 채널을 선택 합니다. 장애 조치 (failover) 클러스터 또는 하이퍼 수렴 형 클러스터를 관리 하는 경우 이벤트 로그에 모든 클러스터 노드에 대 한 이벤트가 표시 되 고 컴퓨터 열에 호스트 서버가 표시 됩니다.

## <a name="protect-virtual-machines-with-azure-site-recovery"></a>Azure Site Recovery를 사용 하 여 가상 머신 보호

Windows 관리 센터를 사용 하 여 온-프레미스 가상 머신을 Azure Site Recovery 구성 하 고 Azure에 복제할 수 있습니다. [자세히 알아보기](../azure/azure-site-recovery.md)

## <a name="more-coming"></a>추가 예정

Windows 관리 센터의 가상 컴퓨터 관리는 적극적으로 개발 중 이며 곧 새 기능이 추가 될 예정입니다. UserVoice의 기능에 대 한 상태 및 투표를 확인할 수 있습니다.

- [가상 컴퓨터 가져오기/내보내기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)
- [폴더의 가상 컴퓨터 정렬](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)
- [추가 가상 컴퓨터 설정 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)
- [Hyper-v 복제본 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)
- [가상 컴퓨터 소유권 위임](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)
- [가상 컴퓨터 복제](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)
- [기존 가상 컴퓨터에서 템플릿 만들기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)
- [Hyper-v 호스트에서 가상 컴퓨터 보기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)
- [새 가상 컴퓨터 창에서 VLAN 구성](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)

[모든 또는 새 기능 제안을 참조 하십시오](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D).
