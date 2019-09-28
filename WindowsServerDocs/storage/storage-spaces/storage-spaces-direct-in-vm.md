---
title: 가상 컴퓨터에서 스토리지 공간 다이렉트 사용
ms.prod: windows-server
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: '가상 컴퓨터 게스트 클러스터에 스토리지 공간 다이렉트를 배포 하는 방법 (예: Microsoft Azure)'
ms.localizationpriority: medium
ms.openlocfilehash: ab0ce792c5a948e763a48493a78ccdac7a6fe74c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366052"
---
# <a name="using-storage-spaces-direct-in-guest-virtual-machine-clusters"></a>게스트 가상 컴퓨터 클러스터에서 스토리지 공간 다이렉트 사용

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서 설명 하는 것 처럼 물리적 서버 클러스터 또는 가상 컴퓨터 게스트 클러스터에 스토리지 공간 다이렉트을 배포할 수 있습니다. 이러한 유형의 배포는 응용 프로그램 고가용성 솔루션을 사용 하 여 응용 프로그램의 가용성을 높일 수 있도록 사설 또는 공용 클라우드 기반의 Vm 집합에서 가상 공유 저장소를 제공 합니다.

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## <a name="deploying-in-azure-iaas-vm-guest-clusters"></a>Azure Iaas VM 게스트 클러스터에서 배포

Azure [템플릿이](https://github.com/robotechredmond/301-storage-spaces-direct-md) 게시 되 면 복잡성을 줄이고, 모범 사례를 구성 하 고, AZURE Iaas VM에서 스토리지 공간 다이렉트 배포의 속도를 구성 합니다. Azure에 배포 하기 위한 권장 솔루션입니다.

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## <a name="requirements"></a>요구 사항

가상화 된 환경에서 스토리지 공간 다이렉트 배포 하는 경우 다음 사항을 고려해 야 합니다.

> [!TIP]
> Azure 템플릿에서는 아래 사항을 자동으로 구성 하며, Azure IaaS Vm에 배포 하는 경우 권장 되는 솔루션입니다.

-   최소 2 개 노드 및 최대 노드 3 개

-   2 노드 배포는 미러링 모니터 서버 (클라우드 감시 또는 파일 공유 감시)를 구성 해야 합니다.

-   3 노드 배포는 1 개의 노드를 허용 하 고 다른 노드에서 하나 이상의 디스크 손실을 허용할 수 있습니다.  2 개의 노드가 종료 되 면 노드 중 하나가 반환 될 때까지 가상 디스크가 오프 라인 상태가 됩니다.  

-   장애 도메인 전체에 배포할 가상 컴퓨터 구성

    -   Azure-가용성 집합 구성

    -   Hyper-v – Vm에서 AntiAffinityClassNames를 구성 하 여 노드 간에 Vm을 분리 합니다.

    -   VMware – ESX 호스트 간에 Vm을 분리 하는 ' 별도 Virtual Machines "형식의 DRS 규칙을 만들어 VM-VM 선호도 방지 규칙을 구성 합니다. 스토리지 공간 다이렉트와 함께 사용 하기 위해 제공 되는 디스크는 PARAVIRTUAL (Paravirtual SCSI) 어댑터를 사용 해야 합니다. Windows Server에서 PARAVIRTUAL을 지원 하려면 https://kb.vmware.com/s/article/1010398 을 참조 하세요.

-   낮은 대기 시간/고성능 저장소 활용-Azure Premium Storage 관리 디스크가 필요 합니다.

-   캐싱 장치가 구성 되지 않은 플랫 저장소 디자인 배포

-   각 VM에 최소 2 개의 가상 데이터 디스크가 표시 됩니다 (VHD/VHDX/.VMDK).

    이 수는 가상 디스크를 실제 오류에 취약 하지 않은 파일로 구현할 수 있으므로 운영 체제 미 설치 배포와는 다릅니다.

-   다음 PowerShell cmdlet을 실행 하 여 상태 관리 서비스에서 자동 드라이브 교체 기능을 사용 하지 않도록 설정 합니다.

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name “System.Storage.PhysicalDisk.AutoReplace.Enabled” -value “False”
    ```

-   지원되지 않는 운영 체제: 호스트 수준 가상 디스크 스냅숏/복원

    대신 기존 게스트 수준 백업 솔루션을 사용 하 여 스토리지 공간 다이렉트 볼륨의 데이터를 백업 하 고 복원 합니다.

-   게스트 클러스터에서 가능한 VHD/VHDX/.VMDK 저장소 대기 시간에 대해 더 큰 복원 력을 제공 하려면 저장소 공간 i/o 시간 제한 값을 늘립니다.

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    16 진수 3만 7530에 해당 하는 10 진수는 30 초입니다. 기본값은 1770 16 진수 또는 6000 10 진수입니다 .이 값은 6 초입니다.

## <a name="see-also"></a>참조

[스토리지 공간 다이렉트, 비디오 및 단계별 가이드를 배포 하기 위한 추가 Azure IAAS VM 템플릿입니다](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126).

[추가 스토리지 공간 다이렉트 개요](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
