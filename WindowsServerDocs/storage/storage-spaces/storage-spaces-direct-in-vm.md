---
title: 가상 컴퓨터에서 저장소 공간 다이렉트를 사용 하 여
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: -예를 들어 Microsoft Azure 가상 컴퓨터 게스트 클러스터에서 저장소 공간 다이렉트를 배포 하는 방법입니다.
ms.localizationpriority: medium
ms.openlocfilehash: a741475d09ab7f7ab29f158ef55378ca9a37beac
ms.sourcegitcommit: 52883945fd6e6bb5c24bd81944ca4bc0c5e6a216
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "8964615"
---
# 게스트 가상 컴퓨터 클러스터에서 저장소 공간 다이렉트를 사용 하 여

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서 설명한 것 처럼 가상 컴퓨터 게스트 클러스터 또는 실제 서버 클러스터에서 저장소 공간 다이렉트를 배포할 수 있습니다. 이러한 유형의 배포 응용 프로그램의 가용성을 높이기 위해 응용 프로그램 고가용성 솔루션을 사용할 수 있도록 공용 또는 개인 클라우드 기반 Vm 세트로에서 가상 공유 저장소를 제공 합니다.

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## Azure Iaas VM 게스트 클러스터 배포

[Azure 템플릿](https://github.com/robotechredmond/301-storage-spaces-direct-md) 게시 감소 복잡성 된, 가장 구성 방법과 Azure Iaas VM에 저장소 공간 다이렉트 배포의 속도. Azure에서 배포 하기 위한 권장 되는 솔루션입니다.

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## 요구 사항

가상화 된 환경에서 저장소 공간 다이렉트를 배포 때는 다음 사항을 고려해 야 합니다.

> [!TIP]
> Azure 템플릿에 자동으로 구성의 고려 사항 및 Azure IaaS Vm에 배포 하는 경우 권장 되는 솔루션은 아래입니다.

-   2 노드 최소 및 최대 3 개의 노드

-   2 노드 배포 (파일 공유 감시 또는 클라우드 감시) 감시를 구성 해야 합니다.

-   3-노드 배포 아래쪽 1 노드와 다른 노드에서 하나 이상의 디스크 손실을 허용할 수 있습니다.  2 노드는 종료 하는 경우 가상 디스크에서는 어조 오프 라인 노드 중 하나를 반환 될 때까지 합니다.  

-   오류 도메인에 배포할 가상 컴퓨터를 구성 합니다.

    -   Azure – 가용성 설정 구성

    -   Hyper-v-노드 간에 Vm을 구분 하는 Vm에서 AntiAffinityClassNames 구성

    -   VMware – 형식의 DRS 규칙을 만들어 구성 VM VM 백신 선호도 규칙 ' 별도 가상 컴퓨터 "ESX 호스트에서 Vm을 구분 합니다. 저장소 공간 다이렉트를 사용 하 여 사용 하도록 제공 된 디스크 Paravirtual SCSI (PVSCSI) 어댑터를 사용 해야 합니다. Windows Server를 사용 하 여 PVSCSI 지원에 대 한 참조 https://kb.vmware.com/s/article/1010398.

-   짧은 대기 시간을 활용 고성능 저장소-Azure 프리미엄 저장소 관리 / 디스크가 필요

-   구성 된 캐싱 없이 장치를 사용 하 여 플랫 저장소 디자인 배포

-   각 VM에 게 제공 하는 2 개의 가상 데이터 디스크의 최소 (VHD / VHDX / VMDK)

    이 숫자는 완전 배포 보다 다릅니다 실제 오류를 사용할 수 없는 파일로 가상 디스크를 구현할 수 있습니다.

-   다음 PowerShell cmdlet을 실행 하 여 상태 관리 서비스에 자동 드라이브 교체 기능을 사용 하지 않도록 설정:

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name “System.Storage.PhysicalDisk.AutoReplace.Enabled” -value “False”
    ```

-   지원 되지 않습니다: 호스트 수준 가상 디스크 스냅숏/복원

    백업 및 저장소 공간 다이렉트 볼륨에서 데이터를 복원 기존의 게스트 수준 백업 솔루션을 대신 사용 합니다.

-   가능한 VHD를 더 큰 복원 력을 제공 / VHDX / VMDK 저장소 대기 시간 게스트 클러스터에서 저장소 공간 I/O 제한 시간 값을 늘립니다.

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    16 진수 7530에 해당 하는 10 진수은 30000, 30 초입니다. 기본값은 6 초는 1770 16 진수 또는 6000 소수점은 note 합니다.

## 참고 항목

[저장소 공간 다이렉트 배포, 동영상 및 단계별 지침에 대 한 추가 VM에서 Azure Iaas 템플릿](https://blogs.msdn.microsoft.com/clustering/2017/02/14/deploying-an-iaas-vm-guest-clusters-in-microsoft-azure/).

[추가 저장소 공간 개요를 직접] (https://docs.microsoft.com/en-us/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
