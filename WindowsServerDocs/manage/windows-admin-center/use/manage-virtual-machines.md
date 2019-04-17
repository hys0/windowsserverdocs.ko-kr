---
title: Windows Admin Center를 사용 하 여 가상 컴퓨터 관리
description: Hyper-v 호스트 및 Windows Admin Center (Project Honolulu)를 사용 하 여 가상 컴퓨터 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 374ee30dcbaf9af3caa60ee85ec59fd3c158206b
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296755"
---
# Windows Admin Center를 사용 하 여 가상 컴퓨터 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

가상 컴퓨터 도구는 서버 또는 클러스터에서 Hyper-v 역할을 사용 하는 경우 [서버](manage-servers.md), [장애 조치 클러스터](manage-failover-clusters.md) 또는 [컨 버 지 드 클러스터](manage-hyper-converged.md) 연결에서 사용할 수 있습니다. 가상 컴퓨터 도구를 사용 하 여 Windows Server 2012를 실행 하는 Hyper-v 호스트 관리 또는 데스크톱 경험 또는 Server Core 설치 중 하나 이상을 합니다. Hyper-v Server 2012, 2016 및 2019도 지원 됩니다.

## 주요 기능

Windows Admin Center에서 가상 컴퓨터 도구의 주요 기능은 다음과 같습니다.

- **상위 수준에서 Hyper-v 호스트 리소스 모니터링 합니다.** 단일 대시보드에서 전체 CPU 및 메모리 사용량, IO 성능 메트릭, VM 상태 경고 및 Hyper-v 호스트 서버 또는 전체 클러스터에 대 한 이벤트를 봅니다.
- **통합된 환경을 Hyper-v 관리자 및 장애 조치 클러스터 관리자 기능을 결합 합니다.** 클러스터에서 모든 가상 컴퓨터를 살펴보고 고급 관리 및 문제 해결에 대 한 단일 가상 컴퓨터에 드릴 다운 합니다.
- **가상 컴퓨터 관리에 대 한 간소화 된, 하면서도 강력한 워크플로.** 새로운 UI 환경을 만들고 관리 하 고 가상 컴퓨터를 복제 하는 IT 관리 시나리오에 맞게 조정 합니다.

다음은 Windows Admin Center에서 할 수 있는 Hyper-v 작업 중 일부입니다.

- [Hyper-v 호스트 리소스 및 성능 모니터링](#monitor-hyper-v-host-resources-and-performance)
- [가상 컴퓨터 인벤토리 보기](#view-virtual-machine-inventory)
- [새 가상 컴퓨터 만들기](#create-a-new-virtual-machine)
- [가상 컴퓨터 설정 변경](#change-virtual-machine-settings)
- [다른 클러스터 노드로 가상 컴퓨터를 실시간 마이그레이션](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [고급 관리 및 단일 가상 컴퓨터에 대 한 문제 해결](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [Hyper-v 호스트 (VMConnect)를 통해 가상 컴퓨터 관리](#manage-a-virtual-machine-through-the-hyper-v-host-vmconnect)
- [Hyper-v 호스트 설정 변경](#change-hyper-v-host-settings)
- [Hyper-v 이벤트 로그 보기](#view-hyper-v-event-logs)
- [Azure Site Recovery를 사용 하 여 가상 컴퓨터를 보호](#protect-virtual-machines-with-azure-site-recovery)

## Hyper-v 호스트 리소스 및 성능 모니터링

![가상 컴퓨터 요약 화면](../media/manage-virtual-machines/virtual-machines-summary.png)

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. **가상 컴퓨터** 도구, **요약** 탭 및 **인벤토리** 탭 맨 위에 있는 두 개의 탭 있습니다. **요약** 탭 Hyper-v 호스트 리소스와 현재 서버 또는 다음을 비롯 한 전체 클러스터에 대 한 성능에 대 한 통찰력을 제공 합니다.
    - Off 실행-상태별으로 그룹화 된 Vm 수 일시 중지 및 저장
    - 최신 상태 경고 또는 Hyper-v 이벤트 로그 이벤트 (입니다 경고는만 Windows Server 2016을 실행 하는 하이퍼 수렴 형 클러스터에 사용할 수 있는 이상)
    - 호스트와 게스트 분석을 사용 하 여 CPU 및 메모리 사용량
    - 가장 CPU 및 메모리 리소스를 소비 하는 최상위 Vm
    - 실시간 및 기록 데이터 줄 IOPS 및 IO 처리량에 대 한 차트 (저장소 성능 줄 차트는만 이상 Windows Server 2016을 실행 하는 하이퍼 수렴 형 클러스터에 사용할 수 있습니다. 기록 데이터는 Windows Server 2019를 실행 하는 하이퍼 수렴 형 클러스터에 사용할 수 있는)

## 가상 컴퓨터 인벤토리 보기

![가상 컴퓨터 인벤토리 화면](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. **가상 컴퓨터** 도구, **요약** 탭 및 **인벤토리** 탭 맨 위에 있는 두 개의 탭 있습니다. **품목** 탭 현재 서버 또는 전체 클러스터에서 사용할 수 있는 가상 컴퓨터를 나열 하 고 개별 가상 컴퓨터를 관리 하기 위해 명령을 제공 합니다. 다음을 수행할 수 있습니다.
    - 현재 서버 또는 클러스터에서 실행 중인 가상 컴퓨터의 목록을 봅니다.
    - 클러스터에 대 한 가상 컴퓨터를 볼 경우 가상 컴퓨터의 상태 및 호스트 서버를 봅니다. 메모리 압력, 메모리 요구 및 할당 된 메모리 및 가상 컴퓨터의 가동 시간, 하트 비트 상태 및 Azure Site Recovery를 사용 하 여 보호 상태를 포함 하 여 호스트 관점에서 CPU 및 메모리 사용량을 볼 수도 있습니다.
    - [새 가상 컴퓨터 만들기](#create-a-new-virtual-machine).
    - 삭제, 시작, 해제, 종료, 일시 중지, 다시 시작, 다시 설정 또는 가상 컴퓨터 이름을 변경 합니다. 또한 가상 컴퓨터를 저장 하 고 저장된 된 상태를 삭제 하거나 검사점을 만듭니다.
    - [가상 컴퓨터에 대 한 설정 변경](#change-virtual-machine-settings)합니다.
    - VMConnect를 사용 하 여 Hyper-v 호스트를 통해 가상 컴퓨터 콘솔에 연결 합니다.
    - [Azure Site Recovery를 사용 하 여 가상 컴퓨터를 복제](#protect-virtual-machines-with-azure-site-recovery)합니다.
    - 시스템 종료, 저장, 일시 중지, 시작, 예: 여러 Vm에서 실행할 수 있는 작업에 대 한 삭제, 초기화, 여러 Vm을 선택 하 고 작업을 한 번에 실행할 수 있습니다.

참고: 클러스터에 연결 하는 경우 가상 컴퓨터 도구는만 표시 클러스터 된 가상 컴퓨터. 나중에 가상 컴퓨터 클러스터 되지 않은 표시 예정입니다.

## 새 가상 컴퓨터 만들기

![새 가상 컴퓨터 화면 만들기](../media/manage-virtual-machines/new-vm.png)

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. 가상 컴퓨터 도구 맨 **인벤토리** 탭을 선택 한 다음 **새** 새 가상 컴퓨터 만들기를 클릭 합니다.
3. 가상 컴퓨터 이름을 입력 하 고 1과 2 세대 가상 컴퓨터 간에 선택 합니다.
4. 클러스터에 가상 컴퓨터를 만들려는 경우 처음에 가상 컴퓨터를 만들 수 있는 호스트를 선택할 수 있습니다. Windows Server 2016 이상을 실행 하는 경우 도구는 드립니다 호스트 권장 지침을 제공 합니다.
5. 가상 컴퓨터 파일에 대 한 경로 선택 합니다. 드롭다운 목록에서 볼륨을 선택 하거나 **찾아보기** 폴더 선택기를 사용 하 여 폴더를 선택 합니다. 가상 컴퓨터 구성 파일 및 가상 하드 디스크 파일에 단일 폴더에 저장 됩니다 합니다 `\Hyper-V\\[virtual machine name]` 선택한 볼륨 또는 경로 경로입니다.

>[!Tip]
> 폴더 선택기를 찾아볼 수 네트워크에서 모든 사용 가능한 SMB 공유에 **폴더 이름** 필드에서 경로 입력 하 여 ```\\server\share```. VM 저장소에 대 한 네트워크 공유를 사용 하 여 [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)필요 합니다.

6. 중첩 된 가상화를 사용 하도록 설정 하려면, 가상 하드 디스크, 네트워크 어댑터, 메모리 설정 구성 및.iso 이미지 파일에서 또는 네트워크에서 운영 체제를 설치할 것인지 선택 여부 가상 프로세서 수를 선택 합니다.
7. 가상 컴퓨터를 만들려면 **만들기** 클릭 합니다.
8. 가상 컴퓨터 만들고 가상 컴퓨터 목록에 표시, 가상 컴퓨터를 시작할 수 있습니다.
9. 가상 컴퓨터가 시작 되 면 운영 체제를 설치 하려면 VMConnect 통해 가상 컴퓨터의 콘솔에 연결할 수 있습니다. 목록에서 가상 컴퓨터를 선택, **더 많은**을 클릭 > **연결** .rdp 파일을 다운로드 합니다. 원격 데스크톱 연결 앱에서.rdp 파일을 엽니다. 이 가상 컴퓨터의 콘솔에 연결을 하므로 Hyper-v 호스트의 관리자 자격 증명을 입력 해야 합니다.

## 가상 컴퓨터 설정 변경

![가상 컴퓨터 설정 화면](../media/manage-virtual-machines/vm-settings.png)

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. 가상 컴퓨터 도구 맨 **인벤토리** 탭 목록에서 가상 컴퓨터를 선택 하 고 **더 많은**을 클릭 선택 > **설정**합니다.
3. **일반**, **보안**, **메모리**, **프로세서**, **디스크**, **네트워크**, **부팅 순서** 및 **검사점** 탭 간에 전환 한 필요한 설정을 구성한 다음 저장 하려면 **저장** 을 클릭 합니다. 현재 탭의 설정 합니다. 사용 가능한 설정을 가상 컴퓨터의 생성에 따라 달라 집니다. 또한 가상 컴퓨터를 실행 하기 위한 일부 설정을 변경할 수 없습니다 하 고 가상 컴퓨터를 먼저 중지 해야 합니다.

## 다른 클러스터 노드로 가상 컴퓨터를 실시간 마이그레이션

클러스터에 연결 하는 경우 다른 클러스터 노드로 가상 컴퓨터를 실시간 마이그레이션할 수 있습니다.

1. 장애 조치 클러스터 또는 하이퍼 컨 버 지 드 클러스터 연결에서 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. 가상 컴퓨터 도구 맨 **인벤토리** 탭 목록에서 가상 컴퓨터를 선택 하 고 **더 많은**을 클릭 선택 > **이동**합니다.
3. 사용 가능한 클러스터 노드 목록에서 서버를 선택 하 고 **이동**을 클릭 합니다.
4. 이동 진행률에 대 한 알림 Windows 관리 센터의 오른쪽 위 모서리에 표시 됩니다. 이동 되 면 가상 컴퓨터 목록에서 변경 된 호스트 서버 이름을 표시 됩니다.

## 고급 관리 및 단일 가상 컴퓨터에 대 한 문제 해결

![단일 가상 컴퓨터 세부 정보 화면](../media/manage-virtual-machines/vm-details.png)

자세한 정보 및 단일 가상 컴퓨터 페이지에서 단일 가상 컴퓨터에 대 한 성능 차트를 볼 수 있습니다.

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. 가상 컴퓨터 도구 맨 위에 있는 가상 컴퓨터의 이름을 **인벤토리** 탭을 클릭 가상 컴퓨터 목록에서 선택 합니다.
3. 단일 가상 컴퓨터 페이지에서 다음을 수행할 수 있습니다.
    - 가상 컴퓨터에 대 한 자세한 정보를 확인 합니다.
    - CPU, 메모리, 네트워크, IOPS 및 IO 처리량 라이브 및 기록 데이터 줄 차트 보기 (기록 데이터는 Windows Server 2019를 실행 하는 하이퍼 수렴 형 클러스터에 사용할 수 있는)
    - 보기, 만들기, 적용, 이름 바꾸기 및 검사점을 삭제 합니다.
    - 가상 컴퓨터의 가상 하드 디스크 (.vhd) 파일, 네트워크 어댑터 및 호스트 서버에 대 한 정보를 봅니다.
    - 삭제, 시작, 해제, 종료, 일시 중지, 다시 시작, 다시 설정 또는 가상 컴퓨터 이름을 변경 합니다. 또한 가상 컴퓨터를 저장 하 고 저장된 된 상태를 삭제 하거나 검사점을 만듭니다.
    - [가상 컴퓨터에 대 한 설정 변경](#change-virtual-machine-settings)합니다.
    - VMConnect를 사용 하 여 Hyper-v 호스트를 통해 가상 컴퓨터 콘솔에 연결 합니다.
    - [Azure Site Recovery를 사용 하 여 가상 컴퓨터를 복제](#protect-virtual-machines-with-azure-site-recovery)합니다.

## Hyper-v 호스트 (VMConnect)를 통해 가상 컴퓨터 관리

![VM 웹 브라우저를 통해 연결](../media/manage-virtual-machines/vm-connect.png)

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. 가상 컴퓨터 도구 맨 **인벤토리** 탭 목록에서 가상 컴퓨터를 선택 하 고 **더 많은**을 클릭 선택 > **연결** 또는 **다운로드 RDP 파일**. **Connect** 를 사용 하면 Windows Admin Center를 통합 하 여 원격 데스크톱 웹 콘솔을 통해 게스트 VM 상호 작용할 수 있습니다. **다운로드 RDP 파일** 원격 데스크톱 연결 응용 프로그램 (mstsc.exe)을 사용 하 여 열 수 있는.rdp 파일을 다운로드 합니다. 두 옵션 모두 VMConnect Hyper-v 호스트를 통해 게스트 VM에 연결 하는 데 사용할 및 Hyper-v 호스트 서버에 대 한 관리자 자격 증명을 입력 해야 합니다.

## Hyper-v 호스트 설정 변경

![Hyper-v 호스트 설정 화면](../media/manage-virtual-machines/host-settings.png)

1. 서버, 하이퍼 컨 버 지 드 클러스터 또는 장애 조치 클러스터 연결을 왼쪽 탐색 창 맨 아래에서 **설정** 메뉴를 클릭 합니다.
2. Hyper-v 호스트 서버 또는 클러스터에서 다음 섹션을 사용 하 여 **Hyper-v 호스트 설정** 그룹을 볼 수 있습니다.
    - 일반: 변경 가상 하드 디스크 및 가상 컴퓨터 파일 경로 및 하이퍼바이저 일정 유형 (지원 경우)
    - 고급 세션 모드
    - NUMA 확장
    - 실시간 마이그레이션
    - 저장소 마이그레이션
3. 하이퍼 컨 버 지 드 클러스터 또는 장애 조치 클러스터 연결 설정을 변경 하는 Hyper-v 호스트를 설정 하면 변경 클러스터 노드 모두에 적용 됩니다.

## Hyper-v 이벤트 로그 보기

가상 컴퓨터 도구에서 직접 Hyper-v 이벤트 로그를 볼 수 있습니다.

1. 왼쪽 탐색 창에서 **가상 컴퓨터** 도구를 클릭 합니다.
2. 가상 컴퓨터 도구 맨 **요약** 탭을 선택 합니다. 맨 위 오른쪽 이벤트 섹션에서 **모든 이벤트 보기를**클릭 합니다.
3. 이벤트 뷰어 도구 왼쪽된 창에서 Hyper-v 이벤트 채널 표시 됩니다. 오른쪽 창에서 이벤트를 보려면 채널을 선택 합니다. 장애 조치 클러스터 또는 하이퍼 수렴 형 클러스터를 관리 하는 경우 모든 클러스터 노드를 컴퓨터 열에 표시 하는 호스트 서버에 대 한 이벤트 이벤트 로그에 표시 됩니다.

## Azure Site Recovery를 사용 하 여 가상 컴퓨터를 보호

Windows Admin Center는 Azure Site Recovery를 구성 하 고 온-프레미스 가상 컴퓨터가 Azure에 복제를 사용할 수 있습니다. [세부 정보](../azure/azure-site-recovery.md)

## 더 많은 이후

Windows Admin Center에서 가상 컴퓨터 관리는 적극적으로 개발 하 고 나중에 새로운 기능이 추가 됩니다. UserVoice에서 상태 및 기능에 대 한 응답을 볼 수 있습니다.

|기능 요청|
|-------|
|[가상 컴퓨터 가져오기/내보내기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)|
|[폴더의 가상 컴퓨터를 정렬](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)|
|[추가 가상 컴퓨터 설정 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)|
|[Hyper-v 복제본 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)|
|[가상 컴퓨터 소유권을 위임합니다](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)|
|[가상 컴퓨터 복제](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)|
|[기존 가상 컴퓨터에서 템플릿 만들기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)|
|[Hyper-v 호스트에서 가상 컴퓨터 보기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)|
|[새 가상 컴퓨터 창에서 VLAN 구성](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)|
|[**모두를 보거나 새로운 기능을 제안 합니다.**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D)|
