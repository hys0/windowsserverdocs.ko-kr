---
title: 클러스터 운영 체제 롤링 업그레이드
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
ms.date: 03/27/2018
ms.openlocfilehash: f56c036768de7c1afcf3327135a7ff7d7a690a8b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440145"
---
# <a name="cluster-operating-system-rolling-upgrade"></a>클러스터 운영 체제 롤링 업그레이드

> 적용 대상: Windows Server 2019, Windows Server 2016

클러스터 OS 롤링 업그레이드 관리자가 Hyper-v 또는 스케일 아웃 파일 서버 워크 로드를 중지 하지 않고 클러스터 노드의 운영 체제를 업그레이드 합니다. 이 기능을 사용하면 SLA(서비스 수준 계약)의 가동 중지 시간 위반을 피할 수 있습니다.

클러스터 OS 롤링 업그레이드는 다음과 같은 이점이 있습니다.

- Hyper-v 가상 머신 및 스케일 아웃 파일 서버 (SOFS) 워크 로드를 실행 하는 장애 조치 클러스터를 가동 중지 시간 없이 (클러스터의 모든 클러스터 노드에서 실행) Windows Server 2016 (클러스터의 모든 노드에서 실행) 하는 Windows Server 2012 R2에서 업그레이드할 수 있습니다. Windows Server 2016 장애 조치 하는 데 걸리는 시간 (일반적으로 5 분) 동안 SQL Server와 같은 다른 클러스터 워크 로드를 사용할 수 없게 됩니다 수 있습니다.  
- 이 추가 하드웨어가 필요 하지 않습니다. 추가 추가할 수는 있지만 클러스터 노드가 일시적으로 클러스터 OS 롤링 업그레이드 하는 동안 클러스터의 가용성을 개선 하기 위해 작은 클러스터를 처리 합니다.  
- 클러스터를 중지 하거나 다시 시작 필요 하지 않습니다.  
- 새 클러스터를 필요 하지 않습니다. 기존 클러스터 업그레이드 됩니다. 또한 Active Directory에 저장 하는 기존 클러스터 개체가 사용 됩니다.  
- 업그레이드 프로세스는 고객 임의성이 반환 된 "지점-의-없음-결과"에서 모든 클러스터 노드의 경우 Windows Server 2016을 실행 하는 때까지 및 업데이트 ClusterFunctionalLevel PowerShell cmdlet를 실행할 때 되돌릴 수 있습니다.  
- 클러스터 OS 혼합 모드에서 실행 하는 동안 패치 및 유지 관리 작업을 지원할 수 있습니다.  
- PowerShell 및 WMI를 통해 자동화를 지원합니다.  
- 클러스터 공용 속성 **ClusterFunctionalLevel** 속성 Windows Server 2016 클러스터 노드에서 클러스터의 상태를 나타냅니다. 장애 조치 클러스터에 속해 있는 Windows Server 2016 클러스터 노드에서 PowerShell cmdlet을 사용 하 여이 속성을 쿼리할 수 있습니다.  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    값이 **8** 클러스터는 Windows Server 2012 R2 기능 수준에서 실행 중임을 나타냅니다. 값이 **9** 클러스터는 Windows Server 2016 기능 수준에서 실행 중임을 나타냅니다.  

이 가이드는 클러스터 OS 롤링 업그레이드 프로세스, 설치 단계, 기능 제한 사항 및 질문과 대답 (Faq)의 다양 한 단계를 설명 하 고 Windows Server 2016에서 다음과 같은 클러스터 OS 롤링 업그레이드 시나리오에 적용할 수 있습니다:  
- Hyper-v 클러스터  
- 스케일 아웃 파일 서버 클러스터  

다음 시나리오는 Windows Server 2016에서 지원 되지 않습니다.  
-  클러스터 공유 저장소로 가상 하드 디스크 (.vhdx 파일)를 사용 하 여 게스트 클러스터 OS 롤링 업그레이드  

클러스터 OS 롤링 업그레이드 하 여 System Center Virtual Machine Manager (SCVMM) 2016을 완전히 지원 됩니다. SCVMM 2016을 사용 하는 경우 참조 [VMM에서 Windows Server 2016에 Hyper-v 호스트 클러스터의 롤링 업그레이드를 수행](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade?view=sc-vmm-1807) 지침은이 문서에 설명 된 단계를 자동화 하 고 클러스터를 업그레이드 합니다.  

## <a name="requirements"></a>요구 사항  
클러스터 OS 롤링 업그레이드 프로세스를 시작 하기 전에 다음 요구 사항을 완료 합니다.

- Windows Server (반기 채널), Windows Server 2016 또는 Windows Server 2012 R2를 실행 하는 장애 조치 클러스터를 사용 하 여 시작 합니다.
- Windows server 저장소 공간 다이렉트 클러스터를 업그레이드, 버전 1709 지원 되지 않습니다.
- 클러스터 워크 로드 Vm Hyper-v 또는 스케일 아웃 파일 서버 이면 무중단 업그레이드를 예상할 수 있습니다.
- 두 번째 수준 주소 테이블 (SLAT)는 다음과 같은 방법 중 하나를 사용 하 여 지 원하는 Cpu의 Hyper-v 노드에 있는지 확인 하십시오  
        -검토를 [SLAT 호환 입니까? WP8 SDK 팁 01](http://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) CPU SLATs 지원 하는지 확인 하는 두 가지 방법에 설명 하는 문서  
        -다운로드 합니다 [Coreinfo v3.31](https://technet.microsoft.com/sysinternals/cc835722) CPU가 SLAT를 지원 하는지 확인 하는 도구입니다.

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>클러스터 OS 롤링 업그레이드 중 클러스터 전환 상태

이 섹션에서는 클러스터 OS 롤링 업그레이드를 사용 하 여 Windows Server 2016으로 업그레이드 되는 Windows Server 2012 R2 클러스터의 다양 한 전환 상태를 설명 합니다.  

클러스터 OS 롤링 업그레이드 프로세스를 Windows Server 2012 R2 노드에서 Windows Server 2016 클러스터 워크 로드를 이동 하는 동안 실행 중인 클러스터 워크 로드를 유지 하기 위해 노드 모두 노드 Windows Server 2012 R2 운영 체제를 실행 하는 경우에 따라 작동 합니다. Windows Server 2016 노드 클러스터에 추가 되 면 Windows Server 2012 R2 호환성 모드에서 작동 합니다. "OS 혼합 모드" 라는 새 개념적 클러스터 모드를 동일한에 서로 다른 버전의 노드 수 있습니다 (그림 1 참조)를 클러스터 합니다.  

![클러스터 OS 롤링 업그레이드는 세 가지 단계를 보여 주는 그림: 모든 노드가 Windows Server 2012 R2, OS 혼합 모드 및 모든 노드가 Windows Server 2016](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**그림 1: 클러스터 운영 체제 상태 전환**  

Windows Server 2012 R2 클러스터를 Windows Server 2016 노드 클러스터에 추가 되 면 OS 혼합 모드를 입력 합니다. 프로세스는 완벽 하 게 되돌릴 수-클러스터에서 Windows Server 2016 노드를 제거할 수 있습니다 하 고이 모드에서는 클러스터에 Windows Server 2012 R2 노드를 추가할 수 있습니다. "지점의 아니요 return" Update-clusterfunctionallevel PowerShell cmdlet는 클러스터에서 실행 될 때 발생 합니다. 성공 하려면이 cmdlet에 대 한 순서 대로 모든 노드는 Windows Server 2016 이어야 합니다 하 고 모든 노드가 온라인 상태 여야 합니다.  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>OS 롤링 업그레이드를 수행 하는 동안 4 개 노드 클러스터의 전환 상태

이 섹션에서는 있는 노드 Windows Server 2012 R2에서 Windows Server 2016으로 업그레이드 하는 공유 저장소를 사용 하 여 클러스터의 서로 다른 네 단계를 설명 합니다.  

"1 단계" 상태가 초기-Windows Server 2012 R2 클러스터를 사용 하 여 시작 합니다.  

![초기 상태를 보여 주는 그림: 모든 노드가 Windows Server 2012 R2](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**그림 2: 초기 상태: Windows Server 2012 R2 장애 조치 클러스터 (1 단계)**  

"은 2 단계 하 고", 두 노드 일시 중지 됨, 드레이닝, 제거, 다시 포맷 되었으며 Windows Server 2016을 사용 하 여 설치 합니다.  

![클러스터 OS 혼합 모드에서 보여 주는 그림: 예제 4 개 노드 클러스터에서 두 개의 노드가 실행 하는 Windows Server 2016 및 Windows Server 2012 R2를 실행 하는 두 노드](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**그림 3: 중간 상태: OS 혼합 모드: Windows Server 2012 R2 및 Windows Server 2016 장애 조치 클러스터 (2 단계)**  

"은 3 단계 하 고", Windows Server 2016으로 업그레이드 된 모든 클러스터의 노드 및 클러스터 업데이트 ClusterFunctionalLevel PowerShell cmdlet을 사용 하 여 업그레이드할 준비가 되었습니다.  

> [!NOTE]  
> 이 단계에서 프로세스를 완벽 하 게 되돌릴 수, 하 고이 클러스터에 Windows Server 2012 R2 노드를 추가할 수 있습니다.  

![클러스터는 Windows Server 2016으로 업그레이드 완벽 하 게 되었습니다 이며 있는지 Update-clusterfunctionallevel cmdlet에 대 한 준비 클러스터 기능 수준을 Windows Server 2016까지를 보여 주는 그림](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**그림 4: 중간 상태: Update-clusterfunctionallevel (단계 3)에 대 한 준비 된 Windows Server 2016으로 업그레이드 하는 모든 노드**  

업데이트-ClusterFunctionalLevelcmdlet을 실행 한 후 "4 단계", 새 Windows Server 2016 클러스터 기능을 사용할 수 있는 클러스터에 입력 합니다.  

![클러스터 롤링 OS 업그레이드를 성공적으로 완료 된; 보여 주는 그림 모든 노드 Windows Server 2016으로 업그레이드 되 고 클러스터가 실행 되는 Windows Server 2016 클러스터 기능 수준이](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**그림 5: 최종 상태입니다. Windows Server 2016 장애 조치 클러스터 (4 단계)**  

## <a name="cluster-os-rolling-upgrade-process"></a>클러스터 OS 롤링 업그레이드 프로세스

이 섹션에서는 클러스터 OS 롤링 업그레이드를 수행 하기 위한 워크플로 설명 합니다.  

![클러스터 업그레이드 워크플로 보여 주는 그림](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**그림 6: 클러스터 OS 롤링 업그레이드 프로세스 워크플로**  

클러스터 OS 롤링 업그레이드에는 다음 단계가 포함 됩니다.  

1. 다음과 같이 운영 체제 업그레이드에 대 한 클러스터를 준비 합니다.  
    1. 클러스터 OS 롤링 업그레이드는 클러스터에서 한 번에 하나의 노드를 제거 해야 합니다. 운영 체제 업그레이드에 대 한 클러스터에서 클러스터 노드 중 하나를 제거 하는 경우 HA Sla를 유지 하기 위해 클러스터에 충분 한 용량이 있는지 확인 합니다. 즉, 필요한 기능을 다른 노드로 장애 조치 작업을 하나의 노드 클러스터 OS 롤링 업그레이드 프로세스 중 클러스터에서 제거 되 면? 클러스터 1 노드 클러스터 OS 롤링 업그레이드에 대 한 클러스터에서 제거 되 면 필요한 워크 로드를 실행할 수 있는 용량이 있습니까?  
    2. Hyper-v 워크 로드에 대 한 모든 Windows Server 2016 Hyper-v 호스트 두 번째 수준 주소 테이블 (SLAT)을 지 원하는 CPU 있는지를 확인 합니다. SLAT 지원 컴퓨터만 Windows Server 2016의 Hyper-v 역할을 사용 합니다.  
    3. 확인 하는 모든 워크 로드 백업 완료 백업 클러스터는 것이 좋습니다. 클러스터에 노드를 추가 하는 동안 백업 작업을 중지 합니다.  
    4. 모든 클러스터 노드가 온라인 상태 인지 확인/실행/확대를 사용 하 여 [ `Get-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) cmdlet (그림 7 참조).  

        ![Get-clusternode cmdlet을 실행 결과 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **그림 7: Get-clusternode cmdlet를 사용 하 여 노드 상태를 확인 합니다.**  

    5. 클러스터 인식 업데이트 (CAU)를 실행 하는 경우 CAU를 사용 하 여 현재 실행 중인 경우 확인 합니다 **Aware 클러스터 업데이트** UI 또는 [ `Get-CauRun` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) cmdlet (그림 8 참조). CAU 사용을 중지 하는 [ `Disable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) cmdlet에서 일시 중지 되어 클러스터 OS 롤링 업그레이드 프로세스 동안 CAU에서 삭제 된 모든 노드를 방지 하기 위해 (참조 그림 9).  

        ![Get-caurun cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **그림 8: 사용 하는 [ `Get-CauRun` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) 클러스터 인식 업데이트를 클러스터에서 실행 중인지 확인 하는 cmdlet**  

        ![Disable-cauclusterrole cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **그림 9: 사용 하 여 클러스터 인식 업데이트 역할을 사용 하지 않도록 설정 합니다 [ `Disable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) cmdlet**  

2. 클러스터의 각 노드에 대해 다음을 수행 합니다.  
    1. 노드를 선택 하 고 사용 하 여 클러스터 관리자 UI를 사용 하 여 **일시 중지 | 드레이닝** 노드를 드레이닝 하려면 메뉴 옵션 (그림 10 참조) 하거나 사용 합니다 [ `Suspend-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) cmdlet (그림 11 참조).  

        ![클러스터 관리자 UI를 사용 하 여 역할을 드레이닝합니다 하는 방법을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **그림 10: 장애 조치 클러스터 관리자를 사용 하 여 노드에서 역할 드레이닝**  

        ![Suspend-clusternode cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **그림 11: 역할에서 사용 하 여 노드를 드레이닝 합니다 [ `Suspend-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) cmdlet**  

    2.  클러스터 관리자 UI를 사용 하 여 **제거** 사용 하거나 클러스터에서 일시 중지 된 노드를 [ `Remove-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) cmdlet.  

        ![노드 제거 cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **그림 12: 사용 하 여 클러스터에서 노드를 제거할 [ `Remove-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) cmdlet**  

    3.  시스템 드라이브를 다시 포맷 하 고 사용 하 여 노드 Windows Server 2016의 "운영 체제 새로 설치"를 수행 합니다 **사용자 지정 합니다. Windows만 설치 (고급)** setup.exe에서 설치 (그림 13 참조) 옵션입니다. 선택 하지 마십시오는 **업그레이드: Windows를 설치 하 고 파일, 설정 및 응용 프로그램 유지** 옵션 이므로 클러스터 OS 롤링 업그레이드에서 전체 업그레이드를 권장 하지 않습니다.  

        ![선택한 사용자 지정 설치 옵션을 보여 주는 Windows Server 2016 설치 마법사의 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **그림 13: Windows Server 2016에 대 한 사용 가능한 설치 옵션**  

    4.  적절 한 Active Directory 도메인에 노드를 추가 합니다.  
    5.  관리자 그룹에 적절 한 사용자를 추가 합니다.  
    6.  서버 관리자 UI 또는 Install-windowsfeature PowerShell cmdlet을 사용 해야 하는, Hyper-v와 같은 서버 역할을 설치 합니다.  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  서버 관리자 UI 또는 Install-windowsfeature PowerShell cmdlet을 사용 하 여 장애 조치 클러스터링 기능을 설치 합니다.  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  클러스터 워크 로드에 필요한 추가 기능을 설치 합니다.  
    9. 장애 조치 클러스터 관리자 UI를 사용 하 여 네트워크 및 저장소 연결 설정을 확인 합니다.  
    10. Windows 방화벽을 사용 하는 경우 클러스터에 대 한 방화벽 설정이 올바른지 확인 합니다. 예를 들어, 클러스터 인식 (CAU 업데이트) 사용 클러스터 방화벽 구성이 필요할 수 있습니다.  
    11. Hyper-v 워크 로드에 대 한 가상 스위치 관리자 대화 상자를 시작 하려면 Hyper-v 관리자 UI를 사용 (그림 14 참조).  

        사용 되는 가상 Switch(s)의 이름이 클러스터의 모든 Hyper-v 호스트 노드에 대해 동일한 지 확인 합니다.  

        ![Hyper-v 가상 스위치 관리자 대화의 위치를 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **그림 14: Virtual Switch Manager**  

    12. Windows Server 2016 노드 (Windows Server 2012 R2 노드를 사용 하지 마십시오), 장애 조치 클러스터 관리자를 사용 하 여 (참조 그림 15) 클러스터에 연결 합니다.  

        ![클러스터 선택 대화 상자를 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)  
        **그림 15: 장애 조치 클러스터 관리자를 사용 하 여 클러스터에 노드 추가**  

    13. 장애 조치 클러스터 관리자 UI를 사용 하 여 또는 [ `Add-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) cmdlet (참조 그림 16) 클러스터에 노드를 추가 합니다.  

        ![Add-clusternode cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **그림 16: 사용 하 여 클러스터에 노드 추가 [ `Add-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) cmdlet**  

        > [!NOTE]  
        > 첫 번째 Windows Server 2016 노드 클러스터에 조인 하면 클러스터가 "Mixed-OS" 모드를 입력 하 고 클러스터 코어 리소스는 Windows Server 2016 노드로 이동 합니다. "혼합-OS" 모드 클러스터를 완벽 하 게 작동 새 노드에서 이전 노드를 사용 하 여 호환성 모드에서 실행 되는 위치입니다. "혼합 OS" 모드는 클러스터에 대 한 일시적인 모드입니다. 영구 수 없습니다 하 고 고객은 해당 클러스터의 모든 노드에 4 주 동안 업데이트 해야 하는 키를 누릅니다.  

    14. Windows Server 2016 이후 노드에 성공적으로 이동할 수 있습니다 (선택 사항) 클러스터 워크 로드의 일부 새로 추가 된 노드 같이 클러스터 전체에서 작업 부하를 리 밸런스 하기 위해 클러스터에 추가 됩니다.

        ![Move-clustervirtualmachinerole cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **그림 17: 사용 하 여 클러스터 (클러스터 VM 역할) 워크 로드 이동 [ `Move-ClusterVirtualMachineRole` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) cmdlet**  

        1. 사용 하 여 **실시간 마이그레이션** 가상 머신에 대 한 장애 조치 클러스터 관리자에서 또는 [ `Move-ClusterVirtualMachineRole` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) cmdlet은 가상 머신의 실시간 마이그레이션을 수행 하려면 (참조 그림 17).  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. 사용 하 여 **이동** 장애 조치 클러스터 관리자에서 또는 [ `Move-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterGroup?view=win10-ps) 다른 클러스터 워크 로드에 대 한 cmdlet입니다.  

3. 모든 노드가 Windows Server 2016으로 업그레이드 되었으며 클러스터에 다시 추가 하는 경우, 나머지 모든 Windows Server 2012 R2 노드가 제거 된 경우 다음을 수행 합니다.  

    > [!IMPORTANT]  
    > -   클러스터 기능 수준을 업데이트 한 후에 Windows Server 2012 R2 기능 수준으로 다시 이동할 수 없습니다 및 클러스터에 Windows Server 2012 R2 노드를 추가할 수 없습니다.
    > -   될 때까지 합니다 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) cmdlet이 실행, 프로세스는 완벽 하 게 되돌릴 수 및이 클러스터에 Windows Server 2012 R2 노드를 추가할 수 있습니다 및 Windows Server 2016 노드를 제거할 수 있습니다.  
    > -   후 합니다 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) 실행 되는 cmdlet, 새 기능을 사용할 수 있습니다.  

    1.  장애 조치 클러스터 관리자 UI를 사용 하 여 또는 [ `Get-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) cmdlet을 예상 대로 클러스터에서 실행 되는 모든 클러스터 역할을 확인 합니다. 다음 예제에서 사용 가능한 저장소 사용 되지, CSV를 사용 하는 대신, 따라서 사용 가능한 저장소 표시는 **오프 라인** 상태 (그림 18 참조).  

        ![Get-clustergroup cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **그림 18: 사용 하 여 실행 되는 모든 클러스터 그룹 (클러스터 역할) 하 고 있는지 확인 합니다 [ `Get-ClusterGroup` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) cmdlet**  

    2.  모든 클러스터 노드가 온라인 상태 인지 확인 하 고 사용 하 여 실행 합니다 [ `Get-ClusterNode` ](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) cmdlet.  
    3.  실행 합니다 [ `Update-ClusterFunctionalLevel` ](https://technet.microsoft.com/library/mt589702.aspx) cmdlet 없음 오류를 반환 해야 (그림 19 참조).  

        ![Update-clusterfunctionallevel cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **그림 19: PowerShell을 사용 하는 클러스터의 클러스터 기능 수준을 업데이트 합니다.**  

    4.  후 합니다 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) 실행 되는 cmdlet, 새 기능을 사용할 수 있습니다.  

4. Windows Server 2016-일반 클러스터 업데이트 및 백업 다시 시작 합니다.  

    1. CAU를 이전에 실행 된 경우 CAU UI를 사용 하 여 다시 시작 하거나 사용 합니다 [ `Enable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) cmdlet (그림 20 참조).  

        ![Enable-cauclusterrole의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png)  
        **그림 20: 사용 하 여 사용 클러스터 인식 업데이트 역할 합니다 [ `Enable-CauClusterRole` ](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) cmdlet**  

    2. 백업 작업을 다시 시작 합니다.  

5. 사용 하도록 설정 하 고 Hyper-v Virtual Machines에서 Windows Server 2016 기능을 사용 합니다.  

    1. 클러스터를 Windows Server 2016 기능 수준으로 업그레이드 후 Hyper-v Vm과 같은 다양 한 워크 로드는 새 기능 해야 합니다. 새로운 Hyper-v 기능 목록은 합니다. 참조 [마이그레이션 및 업그레이드 virtual machines](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms)  

    2. 각 Hyper-v 호스트 클러스터의 노드를 사용 합니다 [ `Get-VMHostSupportedVersion` ](https://docs.microsoft.com/powershell/module/hyper-v/Get-VMHostSupportedVersion?view=win10-ps) 호스트에서 지원 되는 Hyper-v VM 구성 버전을 보려면 cmdlet.  

        ![Get-VMHostSupportedVersion cmdlet의 출력을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **그림 21: 호스트에서 지원 되는 Hyper-v VM 구성 버전 보기**  

   3. 각 노드에서 Hyper-v 호스트 클러스터의 Hyper-v VM 구성 버전 사용자를 사용 하 여 간단한 유지 관리 기간을 예약, 백업, virtual machines를 해제 하 고 실행 하 여 업그레이드할 있습니다 합니다 [ `Update-VMVersion` ](https://docs.microsoft.com/powershell/module/hyper-v/Update-VMVersion?view=win10-ps) cmdlet (참조 그림 22)입니다. 가상 머신 버전은 업데이트 되 고 나중에 Hyper-v 통합 구성 요소 (IC) 업데이트 하지 않아도 새로운 Hyper-v 기능을 사용 하도록 설정 됩니다. VM을 호스팅하는 Hyper-v 노드에서이 cmdlet을 실행할 수 있습니다 또는 `-ComputerName` VM 버전을 원격으로 업데이트 하려면 매개 변수를 사용할 수 있습니다. 이 예에서 여기 업그레이드 VM1의 구성 버전 5.0에서 프로덕션 검사점 (응용 프로그램 일치 백업) 등 이진 VM이 VM 구성 버전과 관련 된 여러 가지 새로운 Hyper-v 기능을 활용 하려면 7.0 구성 파일입니다.  

       ![실행 중인 업데이트 VMVersion cmdlet을 보여 주는 스크린샷](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
       **그림 22: 업데이트 VMVersion PowerShell cmdlet을 사용 하 여 VM 버전 업그레이드**  

6. 사용 하 여 저장소 풀을 업그레이드할 수 있습니다 합니다 [Update-storagepool](https://docs.microsoft.com/powershell/module/storage/Update-StoragePool?view=win10-ps) PowerShell cmdlet이 작업은 온라인 작업입니다.  

하지만 특히 Hyper-v 사설 클라우드 시나리오를 대상으로 하 고 클러스터 OS 롤링 업그레이드 프로세스 가동 중지 시간 없이 업그레이드할 수 있는 스케일 아웃 파일 서버 클러스터의 경우 모든 클러스터 역할에 사용할 수 있습니다.  

## <a name="restrictions--limitations"></a>제한 / 제한 사항  
- 이 기능은 Windows Server 2016 버전에만 Windows Server 2012 R2에 대해서만 작동합니다. 이 기능은 Windows Server 2016 이전 버전의 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012와 같은 Windows Server를 업그레이드할 수 없습니다.  
- 각 Windows Server 2016 노드를 다시 포맷 하거나 새로운 설치의 경우에 있어야 합니다. "내부" 또는 "업그레이드" 설치 유형 권장 되지 않습니다.  
- Windows Server 2016 노드 Windows Server 2016 노드 클러스터를 추가 하려면 사용 해야 합니다.  
- OS 혼합 모드 클러스터를 관리 하는 경우 항상 상위 그룹 노드에서 Windows Server 2016을 실행 하는 관리 작업을 수행 합니다. 하위 수준 Windows Server 2012 R2 노드 Windows Server 2016에 대 한 UI 또는 관리 도구를 사용할 수 없습니다.  
- 고객이 일부 클러스터 기능은 OS 혼합 모드에 대해 최적화 되어 있지 않으므로 클러스터 업그레이드 프로세스를 통해 신속 하 게 이동 하는 것이 좋습니다.  
- 만들기 또는 클러스터 실행 되는 동안 OS 혼합 모드에서 가능한 비 호환성으로 인해 장애 조치 시 Windows Server 2016 노드에서 하위 수준 Windows Server 2012 R2 노드를 Windows Server 2016 노드에서 저장소 크기를 조정 하지 마십시오.  

## <a name="frequently-asked-questions"></a>질문과 대답  
**기간 수 장애 조치 클러스터를 혼합 OS 모드로 실행**  
    4 주 동안 업그레이드를 완료 하려면 고객에 게를 사용 하는 것이 좋습니다. Windows Server 2016의 여러 가지 최적화가 있습니다. Hyper-v가 성공적으로 업그레이드 되었음 및 가동 중지 시간이 0을 사용 하 여 총 4 시간 이내에 클러스터를 스케일 아웃 파일 서버.  

**이 기능은 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 돌아가기 포팅하는?**  
    이 기능은 이전 버전으로 포트를 모든 계획이 없습니다. 클러스터 OS 롤링 업그레이드는 Windows Server 2016 이상 Windows Server 2012 R2 클러스터를 업그레이드 하는 것에 대 한 우리의 비전입니다.  

**Windows Server 2012 R2 클러스터에서 모든 소프트웨어 업데이트가 클러스터 OS 롤링 업그레이드 프로세스를 시작 하기 전에 설치 해야 하나요?**  
    예, 클러스터 OS 롤링 업그레이드 프로세스를 시작 하기 전에 모든 클러스터 노드에 최신 소프트웨어 업데이트를 사용 하 여 업데이트를 확인 합니다.  

**실행 수를 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) 노드가 일시 중지 되거나 해제 됩니다 하는 동안 cmdlet?**  
    아니요. 모든 클러스터 노드 및에 대 한 활성 회원 자격 이어야 합니다는 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) cmdlet이 작동 하려면.  

**모든 클러스터 워크 로드에 대 한 작동 클러스터 OS 롤링 업그레이드 하나요? SQL Server에 대 한 작동 합니까?**  
    예, 클러스터 OS 롤링 업그레이드는 모든 클러스터 워크 로드에 대 한 작동합니다. 그러나 Hyper-v 및 스케일 아웃 파일 서버 클러스터에 대 한 유일한 가동 것입니다. 대부분의 다른 워크 로드 가동 중지 시간이 (일반적으로 몇 분)을 때 발생은 현재 장애 조치 및 장애 조치는 클러스터 OS 롤링 업그레이드 프로세스 중 한 번 이상 필요 합니다.  

**PowerShell을 사용 하 여이 프로세스를 자동화할 수 있나요?**  
    예, 설계 했습니다 클러스터 OS 롤링 업그레이드 PowerShell을 사용 하 여 자동화할 수 있습니다.  

**추가 워크 로드 및 장애 조치 용량 있는 큰 클러스터로 업그레이드할 수 여러 노드가 동시에?**  
    예 하나의 노드 클러스터에서 OS 업그레이드로 제거 되 면 클러스터 장애 조치에 대 한 적은 노드 하나를 갖게 됩니다, 그리고 따라서 축소 된 장애 조치 용량은 됩니다. 충분 한 워크 로드 및 장애 조치 용량을 사용 하 여 대형 클러스터에 대 한 여러 노드가 동시에 업그레이드할 수 있습니다. 클러스터 OS 롤링 업그레이드 프로세스 동안 향상 된 워크 로드 및 장애 조치 용량을 제공 하는 클러스터에 클러스터 노드를 일시적으로 추가할 수 있습니다.  

**그렇다면 후 클러스터 내에서 문제를 검색 하려면 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) 성공적으로 실행 되었습니다.**  
    경우 수 있는 백업 클러스터 데이터베이스 시스템 상태 백업을 실행 하기 전에 [ `Update-ClusterFunctionalLevel` ](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)는 신뢰할 수 있다고 할 수 있습니다 Windows Server 2012 R2 클러스터 노드에 복원 하 고 원래 클러스터를 복원 합니다. 데이터베이스 및 구성 합니다.  

**시스템 드라이브를 다시 포맷 하는 정리 OS 설치를 사용 하는 대신 각 노드에 대 한 전체 업그레이드를 사용할 수 있나요?**  
    Windows Server의 전체 업그레이드의 사용을 권장 하지 않습니다 하지만 기본 드라이버의 사용 되는 일부 경우에서 작동 하는지 확인 합니다. 신중 하 게 읽어보세요 클러스터 노드의 현재 위치 업그레이드 중에 모든 경고 메시지를 표시 합니다.  

**Hyper-v 클러스터에서 Hyper-v VM에 대 한 Hyper-v 복제 사용 하 고, 경우 복제 그대로 유지 됩니다 클러스터 OS 롤링 업그레이드 프로세스 전후의?**  
    예, Hyper-v 복제본 클러스터 OS 롤링 업그레이드 프로세스 전후의 그대로 유지 됩니다.  

**클러스터 OS 롤링 업그레이드 프로세스를 자동화 하려면 System Center 2016 Virtual Machine Manager (SCVMM)를 사용할 수 있나요?**  
    예, System Center 2016의 VMM을 사용 하는 클러스터 OS 롤링 업그레이드 프로세스를 자동화할 수 있습니다.  

## <a name="see-also"></a>참조  
-   [릴리스 정보: Windows Server 2016의 중요한 이슈](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Windows Server 2016의 새로운 기능](../get-started/What-s-New-in-windows-server-2016.md)  
-   [Windows Server에서 장애 조치 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)  
