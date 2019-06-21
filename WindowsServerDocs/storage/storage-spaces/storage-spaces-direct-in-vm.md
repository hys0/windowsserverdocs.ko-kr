---
title: 가상 컴퓨터에서 저장소 공간 다이렉트를 사용 하 여
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: -예를 들어, Microsoft Azure 가상 컴퓨터 게스트 클러스터의 저장소 공간 다이렉트를 배포 하는 방법입니다.
ms.localizationpriority: medium
ms.openlocfilehash: d05afb5ee564b866dcd15ec6aa473cee608dbd8f
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284411"
---
# <a name="using-storage-spaces-direct-in-guest-virtual-machine-clusters"></a>게스트 가상 컴퓨터 클러스터에서 저장소 공간 다이렉트를 사용 하 여

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에 설명 된 대로 가상 컴퓨터 게스트 클러스터 또는 클러스터의 물리적 서버를 저장소 공간 다이렉트를 배포할 수 있습니다. 이 유형의 배포 응용 프로그램의 가용성 향상을 위해 응용 프로그램 고가용성 솔루션을 사용할 수 있도록 개인 또는 공용 클라우드를 기반으로 Vm의 여러 가상 공유 저장소를 제공 합니다.

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## <a name="deploying-in-azure-iaas-vm-guest-clusters"></a>Azure Iaas VM 게스트 클러스터에 배포

[Azure 템플릿](https://github.com/robotechredmond/301-storage-spaces-direct-md) 복잡성 게시 감소 되었습니다, 구성 모범 사례 및 Azure Iaas VM의 저장소 공간 다이렉트 배포의 속도. Azure에 배포 하기 위한 권장된 솔루션입니다.

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## <a name="requirements"></a>요구 사항

다음 고려 사항에는 가상화 된 환경에서 저장소 공간 다이렉트를 배포할 때 적용 됩니다.

> [!TIP]
> Azure 템플릿은 자동으로 구성 됩니다을 하는 Azure IaaS Vm에서 배포 하는 경우 권장 되는 솔루션에 대 한 고려 사항 아래.

-   노드 2의 최소 및 최대 3 개의 노드가

-   2 노드 배포 (클라우드 감시 또는 파일 공유 감시) 감시를 구성 해야 합니다.

-   3 노드 배포는 1 노드 작동 중단 및 다른 노드에서 하나 이상의 디스크의 손실을 허용할 수 있습니다.  2 노드를 종료 하는 경우 다음 가상 디스크에서는 오프 라인 상태가 노드 중 하나를 반환할 때까지.  

-   장애 도메인에 배포할 virtual machines 구성

    -   Azure 가용성 집합 구성

    -   하이퍼-V-노드 간에 Vm을 별도 Vm에 구성 AntiAffinityClassNames

    -   VMware – 형식의 DRS 규칙을 만들어 구성 VM 선호도 방지 규칙 ' 별도 Virtual Machines "ESX 호스트에 걸쳐 Vm을 구분 합니다. 저장소 공간 다이렉트를 사용 하 여 사용 하도록 제공 된 디스크 Pvscsi (PARAVIRTUAL SCSI) 어댑터를 사용 해야 합니다. Windows Server를 사용 하 여 PVSCSI 지원에 대 한 참조 https://kb.vmware.com/s/article/1010398 합니다.

-   활용 대기 시간이 짧은 고성능 저장소-Azure Premium Storage를 관리 / 디스크가 필요 하다는

-   구성 된 없는 캐싱 장치를 사용 하 여 플랫 저장소 디자인 배포

-   최소 각 VM에 제공 하는 2 개의 가상 데이터 디스크 (VHD / VHDX / VMDK)

    이 숫자 베어 메탈 배포에 비해 다른 이므로 실제 오류에 취약 하지 않은 파일로 가상 디스크를 구현할 수 있습니다.

-   다음 PowerShell cmdlet을 실행 하 여 상태 관리 서비스의 자동 드라이브 대체 기능을 사용 하지 않도록 설정 합니다.

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name “System.Storage.PhysicalDisk.AutoReplace.Enabled” -value “False”
    ```

-   지원되지 않는 운영 체제: 호스트 수준 가상 디스크 스냅숏/복원

    백업 및 복원 된 볼륨의 데이터를 저장소 공간 다이렉트에 기존 게스트 수준을 백업 솔루션을 대신 사용 합니다.

-   복원 력을 높이기 가능한 VHD에 있도록 / VHDX 게스트 클러스터에서 VMDK 저장소 대기 시간에 저장소 공간 I/O 제한 시간 값을 증가 /:

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    16 진수 7530를 10 진수로 변환이입니다. 30000, 30 초입니다. 기본값은 6 초는 1770 16 진수 또는 6000 소수 인지 note 합니다.

## <a name="see-also"></a>참조

[저장소 공간 다이렉트, 비디오 및 단계별 가이드 배포에 대 한 추가 Azure Iaas VM 템플릿](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126)합니다.

[추가 저장소 공간 다이렉트 개요](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
