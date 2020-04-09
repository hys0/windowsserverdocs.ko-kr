---
title: 클러스터 운영 체제 롤링 업그레이드
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
manager: lizross
ms.date: 03/27/2018
ms.openlocfilehash: 8b2ea665542d57b12899a5993a62973c446485a7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828356"
---
# <a name="cluster-operating-system-rolling-upgrade"></a>클러스터 운영 체제 롤링 업그레이드

> 적용 대상: Windows Server 2019, Windows Server 2016

클러스터 OS 롤링 업그레이드를 사용 하면 관리자가 Hyper-v 또는 스케일 아웃 파일 서버 작업을 중지 하지 않고 클러스터 노드의 운영 체제를 업그레이드할 수 있습니다. 이 기능을 사용하면 SLA(서비스 수준 계약)의 가동 중지 시간 위반을 피할 수 있습니다.

클러스터 OS 롤링 업그레이드는 다음과 같은 이점을 제공 합니다.

- Hyper-v 가상 머신과 SOFS (스케일 아웃 파일 서버) 워크 로드를 실행 하는 장애 조치 (Failover) 클러스터는 가동 중지 시간 없이 클러스터의 모든 클러스터 노드에서 실행 되는 windows server 2012 r 2에서 Windows Server 2016로 업그레이드할 수 있습니다 (클러스터의 모든 노드에서 실행). SQL Server와 같은 다른 클러스터 워크 로드는 Windows Server 2016로 장애 조치 (failover) 하는 데 걸리는 시간 (일반적으로 5 분 미만) 동안 사용할 수 없습니다.  
- 추가 하드웨어는 필요 하지 않습니다. 하지만 클러스터 OS 롤링 업그레이드 프로세스 중에 클러스터의 가용성을 향상 시키기 위해 작은 클러스터에 일시적으로 클러스터 노드를 더 추가할 수 있습니다.  
- 클러스터를 중지 하거나 다시 시작할 필요가 없습니다.  
- 새 클러스터가 필요 하지 않습니다. 기존 클러스터가 업그레이드 됩니다. 또한 Active Directory에 저장 된 기존 클러스터 개체를 사용 합니다.  
- 모든 클러스터 노드가 Windows Server 2016를 실행 하 고 ClusterFunctionalLevel PowerShell cmdlet이 실행 될 때 고객이 "가 지점"을 사용할 때까지 업그레이드 프로세스를 되돌릴 수 있습니다.  
- 클러스터는 혼합 OS 모드에서 실행 되는 동안 패치 및 유지 관리 작업을 지원할 수 있습니다.  
- PowerShell 및 WMI를 통한 자동화를 지원 합니다.  
- Cluster public property **ClusterFunctionalLevel** 속성은 Windows Server 2016 클러스터 노드의 클러스터 상태를 나타냅니다. 이 속성은 장애 조치 (failover) 클러스터에 속한 Windows Server 2016 클러스터 노드에서 PowerShell cmdlet을 사용 하 여 쿼리할 수 있습니다.  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    값 **8** 은 클러스터가 Windows Server 2012 R2 기능 수준에서 실행 중임을 나타냅니다. 값 **9** 는 클러스터가 Windows Server 2016 기능 수준에서 실행 중임을 나타냅니다.  

이 가이드는 클러스터 OS 롤링 업그레이드 프로세스의 다양 한 단계, 설치 단계, 기능 제한 사항 및 Faq (질문과 대답)에 대해 설명 하며, Windows Server 2016의 다음 클러스터 OS 롤링 업그레이드 시나리오에 적용 됩니다.  
- Hyper-v 클러스터  
- 스케일 아웃 파일 서버 클러스터  

다음 시나리오는 Windows Server 2016에서 지원 되지 않습니다.  
-  가상 하드 디스크 (.vhdx 파일)를 공유 저장소로 사용 하 여 게스트 클러스터의 클러스터 OS 롤링 업그레이드  

클러스터 OS 롤링 업그레이드는 SCVMM (System Center Virtual Machine Manager) 2016에서 완벽 하 게 지원 됩니다. SCVMM 2016을 사용 하는 경우 클러스터를 업그레이드 하 고이 문서에서 설명 하는 단계를 자동화 하는 방법에 대 한 지침은 [VMM에서 Windows Server 2016로 hyper-v 호스트 클러스터의 롤링 업그레이드 수행](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade?view=sc-vmm-1807) 을 참조 하세요.  

## <a name="requirements"></a>요구 사항  
클러스터 OS 롤링 업그레이드 프로세스를 시작 하기 전에 다음 요구 사항을 완료 합니다.

- Windows Server (반기 채널), Windows Server 2016 또는 Windows Server 2012 r 2를 실행 하는 장애 조치 (Failover) 클러스터로 시작 합니다.
- 스토리지 공간 다이렉트 클러스터를 Windows Server로 업그레이드 하는 경우 1709 버전이 지원 되지 않습니다.
- 클러스터 워크 로드가 Hyper-v Vm 또는 스케일 아웃 파일 서버 이면 가동 중지 시간이 0 인 업그레이드를 예측할 수 있습니다.
- 다음 방법 중 하나를 사용 하 여 Hyper-v 노드에 SLAT (두 번째 수준 주소 지정 테이블)를 지 원하는 Cpu가 있는지 확인 합니다.  
        -SLAT 호환 여부를 검토 합니다. [ WP8 SDK Tip 01](https://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) 문서 CPU가 SLATs을 지원 하는지 확인 하는 두 가지 방법을 설명 합니다.  
        - [Coreinfo v 3.31](https://technet.microsoft.com/sysinternals/cc835722) 도구를 다운로드 하 여 CPU가 SLAT를 지원 하는지 확인 합니다.

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>클러스터 OS 롤링 업그레이드 중 클러스터 전환 상태

이 섹션에서는 클러스터 OS 롤링 업그레이드를 사용 하 여 Windows Server 2016로 업그레이드 되는 Windows Server 2012 R2 클러스터의 다양 한 전환 상태에 대해 설명 합니다.  

클러스터 운영 체제 롤링 업그레이드 프로세스 중에 클러스터 워크 로드를 계속 실행 하기 위해 클러스터 워크 로드를 Windows server 2012 R2 노드에서 Windows Server 2016 노드로 이동 하는 것은 두 노드가 모두 Windows Server 2012 R2 운영 체제를 실행 하는 것 처럼 작동 합니다. Windows Server 2016 노드가 클러스터에 추가 되 면 Windows Server 2012 R2 호환 모드에서 작동 합니다. "혼합 OS 모드" 라고 하는 새로운 개념 클러스터 모드를 사용 하면 서로 다른 버전의 노드가 동일한 클러스터에 존재할 수 있습니다 (그림 1 참조).  

클러스터 OS 롤링 업그레이드의 세 단계를 보여 주는 ![그림: 모든 노드 Windows Server 2012 R2, 혼합 OS 모드 및 모든 노드 Windows Server 2016](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**그림 1: 클러스터 운영 체제 상태 전환**  

Windows server 2016 노드가 클러스터에 추가 되 면 Windows Server 2012 R2 클러스터가 혼합 된 OS 모드로 전환 됩니다. 프로세스는 완전히 되돌릴 수 있습니다.-Windows Server 2016 노드는 클러스터에서 제거할 수 있으며 Windows Server 2012 R2 노드는이 모드에서 클러스터에 추가할 수 있습니다. 클러스터에서 ClusterFunctionalLevel PowerShell cmdlet이 실행 되 면 "반환 지점 없음"이 발생 합니다. 이 cmdlet을 성공적으로 수행 하려면 모든 노드가 Windows Server 2016 여야 하 고 모든 노드가 온라인 상태 여야 합니다.  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>운영 체제 롤링 업그레이드를 수행 하는 동안 4 개 노드 클러스터의 전환 상태

이 섹션에서는 노드가 Windows Server 2012 r 2에서 Windows Server 2016로 업그레이드 되는 공유 저장소를 사용 하는 클러스터의 네 가지 단계를 설명 하 고 설명 합니다.  

"1 단계"는 초기 상태 이며 Windows Server 2012 R2 클러스터부터 시작 합니다.  

초기 상태를 보여 주는 ![그림: 모든 노드 Windows Server 2012 R2](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**그림 2: 초기 상태: Windows Server 2012 R2 장애 조치 (Failover) 클러스터 (1 단계)**  

"2 단계"에서는 Windows Server 2016를 사용 하 여 두 노드를 일시 중지, 제거, 제거, 다시 포맷 및 설치 했습니다.  

클러스터를 혼합 OS 모드로 보여 주는 ![예제 4-노드 클러스터에서 두 개의 노드가 Windows Server 2016를 실행 하 고 두 노드에서 Windows Server 2012 r 2를 실행 하 고 있습니다](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**그림 3: 중간 상태: 혼합 OS 모드: Windows Server 2012 R2 및 Windows Server 2016 장애 조치 (Failover) 클러스터 (2 단계)**  

"3 단계"에서 클러스터의 모든 노드가 Windows Server 2016로 업그레이드 되 고 클러스터를 ClusterFunctionalLevel PowerShell cmdlet을 사용 하 여 업그레이드할 준비가 되었습니다.  

> [!NOTE]  
> 이 단계에서는 프로세스를 완전히 되돌릴 수 있으며 Windows Server 2012 R2 노드를이 클러스터에 추가할 수 있습니다.  

클러스터가 Windows Server 2016로 완전히 업그레이드 되었고 ClusterFunctionalLevel cmdlet이 클러스터 기능 수준을 Windows Server 2016까지 가져올 준비가 되었음을 보여 주는 ![그림](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**그림 4: 중간 상태: 모든 노드가 Windows Server 2016로 업그레이드 되 고 ClusterFunctionalLevel 준비 됨 (3 단계)**  

ClusterFunctionalLevelcmdlet가 실행 된 후 클러스터는 "4 단계"를 입력 합니다. 여기에서 새로운 Windows Server 2016 클러스터 기능을 사용할 수 있습니다.  

클러스터 롤링 OS 업그레이드가 성공적으로 완료 되었음을 보여 주는 ![그림 모든 노드가 Windows Server 2016로 업그레이드 되었으며 클러스터가 Windows Server 2016 클러스터 기능 수준에서 실행 되 고](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**그림 5: 최종 상태: Windows Server 2016 장애 조치 (Failover) 클러스터 (4 단계)**  

## <a name="cluster-os-rolling-upgrade-process"></a>클러스터 OS 롤링 업그레이드 프로세스

이 섹션에서는 클러스터 OS 롤링 업그레이드를 수행 하는 워크플로를 설명 합니다.  

클러스터를 업그레이드 하기 위한 워크플로를 보여 주는 ![그림](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**그림 6: 클러스터 OS 롤링 업그레이드 프로세스 워크플로**  

클러스터 OS 롤링 업그레이드에는 다음 단계가 포함 됩니다.  

1. 다음과 같이 운영 체제를 업그레이드 하기 위해 클러스터를 준비 합니다.  
    1. 클러스터 OS 롤링 업그레이드는 클러스터에서 한 번에 하나의 노드만 제거 해야 합니다. 운영 체제를 업그레이드 하기 위해 클러스터에서 클러스터 노드 중 하나를 제거 하는 경우 HA Sla를 유지 하기 위해 클러스터에 용량이 충분 한지 확인 합니다. 즉, 클러스터 OS 롤링 업그레이드 프로세스 중에 클러스터에서 하나의 노드가 제거 될 때 작업을 다른 노드로 장애 조치 (failover) 하는 기능이 필요 한가요? 클러스터 OS 롤링 업그레이드를 위해 클러스터에서 한 노드를 제거 하는 경우 클러스터에 필요한 작업을 실행할 수 있는 용량이 있나요?  
    2. Hyper-v 워크 로드의 경우 모든 Windows Server 2016 Hyper-v 호스트에 SLAT (두 번째 수준 주소 테이블)를 지 원하는 CPU가 있는지 확인 합니다. SLAT 가능 컴퓨터만 Windows Server 2016에서 Hyper-v 역할을 사용할 수 있습니다.  
    3. 모든 작업 백업이 완료 되었는지 확인 하 고 클러스터를 백업 하는 것이 좋습니다. 클러스터에 노드를 추가 하는 동안 백업 작업을 중지 합니다.  
    4. [`Get-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) cmdlet을 사용 하 여 모든 클러스터 노드가 온라인/running/up 있는지 확인 합니다 (그림 7 참조).  

        Start-clusternode cmdlet을 실행 한 결과를 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **그림 7: Start-clusternode cmdlet을 사용 하 여 노드 상태 확인**  

    5. CAU (클러스터 인식 업데이트)를 실행 하는 경우 **클러스터 인식 업데이트** UI 또는 [`Get-CauRun`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) cmdlet을 사용 하 여 cau가 현재 실행 되 고 있는지 확인 합니다 (그림 8 참조). 클러스터 OS 롤링 업그레이드 프로세스를 진행 하는 동안 CAU에서 노드를 일시 중지 및 배출 하지 않도록 [`Disable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) Cmdlet (그림 9 참조)을 사용 하 여 cau를 중지 합니다.  

        Invoke-caurun cmdlet의 출력을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **그림 8: [`Get-CauRun`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) Cmdlet을 사용 하 여 클러스터에서 클러스터 인식 업데이트가 실행 되 고 있는지 확인**  

        Add-cauclusterrole cmdlet의 출력을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **그림 9: [`Disable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) cmdlet을 사용 하 여 클러스터 인식 업데이트 역할 해제**  

2. 클러스터의 각 노드에 대해 다음을 완료 합니다.  
    1. 클러스터 관리자 UI를 사용 하 여 노드를 선택 하 고 일시 중지를 사용 합니다.노드를 드레이닝 하기 위한 드레이닝 메뉴 옵션 (그림 10 참조) 또는 [`Suspend-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) Cmdlet 사용 (그림 11 참조)  

        클러스터 관리자 UI를 사용 하 여 역할을 드레이닝 하는 방법을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **그림 10: 장애 조치(Failover) 클러스터 관리자를 사용 하 여 노드에서 역할 드레이닝**  

        Start-clusternode cmdlet의 출력을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **그림 11: [`Suspend-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) cmdlet을 사용 하 여 노드에서 역할 드레이닝**  

    2.  클러스터 관리자 UI를 사용 하 여 클러스터에서 일시 중지 된 노드를 **제거** 하거나 [`Remove-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) cmdlet을 사용 합니다.  

        Start-clusternode cmdlet의 출력을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **그림 12: [`Remove-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) cmdlet을 사용 하 여 클러스터에서 노드 제거**  

    3.  시스템 드라이브를 다시 포맷 하 고 setup.exe의 **사용자 지정: windows만 설치 (고급)** 설치 (그림 13 참조) 옵션을 사용 하 여 노드에서 windows Server 2016의 "클린 운영 체제 설치"를 수행 합니다. 클러스터 OS 롤링 업그레이드는 현재 위치 업그레이드를 권장 하지 않으므로 업그레이드를 선택 하지 마세요 **. Windows를 설치 하 고 파일, 설정 및 응용 프로그램 유지** 옵션을 선택 합니다.  

        선택한 사용자 지정 설치 옵션을 보여 주는 Windows Server 2016 설치 마법사의 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **그림 13: Windows Server 2016에 대 한 사용 가능한 설치 옵션**  

    4.  적절 한 Active Directory 도메인에 노드를 추가 합니다.  
    5.  Administrators 그룹에 적절 한 사용자를 추가 합니다.  
    6.  서버 관리자 UI 또는 Install-Add-windowsfeature PowerShell cmdlet을 사용 하 여 Hyper-v와 같이 필요한 서버 역할을 설치 합니다.  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  서버 관리자 UI 또는 Install-Add-windowsfeature PowerShell cmdlet을 사용 하 여 장애 조치 (Failover) 클러스터링 기능을 설치 합니다.  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  클러스터 워크 로드에 필요한 추가 기능을 설치 합니다.  
    9. 장애 조치(Failover) 클러스터 관리자 UI를 사용 하 여 네트워크 및 저장소 연결 설정을 확인 합니다.  
    10. Windows 방화벽을 사용 하는 경우 클러스터에 대 한 방화벽 설정이 올바른지 확인 합니다. 예를 들어 CAU (클러스터 인식 업데이트) 사용 클러스터에서 방화벽 구성이 필요할 수 있습니다.  
    11. Hyper-v 워크 로드의 경우 Hyper-v 관리자 UI를 사용 하 여 가상 스위치 관리자 대화 상자를 시작 합니다 (그림 14 참조).  

        사용 되는 가상 스위치의 이름이 클러스터의 모든 Hyper-v 호스트 노드에 대해 동일한 지 확인 합니다.  

        Hyper-v 가상 스위치 관리자 대화 상자의 위치를 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **그림 14: 가상 스위치 관리자**  

    12. Windows server 2016 노드 (Windows Server 2012 R2 노드를 사용 하지 않음)에서 장애 조치(Failover) 클러스터 관리자 (그림 15 참조)를 사용 하 여 클러스터에 연결 합니다.  

        클러스터 선택 대화](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)를 보여 주는 ![Screencap  
        **그림 15: 장애 조치(Failover) 클러스터 관리자을 사용 하 여 클러스터에 노드 추가**  

    13. 장애 조치(Failover) 클러스터 관리자 UI 또는 [`Add-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) Cmdlet (그림 16 참조) 중 하나를 사용 하 여 노드를 클러스터에 추가 합니다.  

        Start-clusternode cmdlet의 출력을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **그림 16: [`Add-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) cmdlet을 사용 하 여 클러스터에 노드 추가**  

        > [!NOTE]  
        > 첫 번째 Windows Server 2016 노드가 클러스터에 연결 되 면 클러스터가 "혼합 OS" 모드로 전환 되 고 클러스터 코어 리소스가 Windows Server 2016 노드로 이동 합니다. "혼합 OS" 모드 클러스터는 새 노드가 이전 노드와 호환 모드에서 실행 되는 완전 한 기능을 갖춘 클러스터입니다. "혼합 OS" 모드는 클러스터에 대 한 임시 모드입니다. 영구적이 지 않으며 고객이 4 주 내에 클러스터의 모든 노드를 업데이트할 것으로 예상 됩니다.  

    14. Windows Server 2016 노드가 클러스터에 성공적으로 추가 된 후에는 다음과 같이 클러스터 전체에서 작업의 균형을 다시 조정 하기 위해 클러스터 워크 로드 중 일부를 새로 추가 된 노드로 이동할 수 있습니다 (옵션).

        Move-clustervirtualmachinerole cmdlet의 출력을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **그림 17: [`Move-ClusterVirtualMachineRole`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) cmdlet을 사용 하 여 클러스터 워크 로드 (클러스터 VM 역할) 이동**  

        1. 가상 컴퓨터의 장애 조치(Failover) 클러스터 관리자에서 **실시간 마이그레이션** 를 사용 하거나 [`Move-ClusterVirtualMachineRole`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) cmdlet (그림 17 참조)을 사용 하 여 가상 컴퓨터의 실시간 마이그레이션을 수행 합니다.  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. 다른 클러스터 워크 로드의 경우 장애 조치(Failover) 클러스터 관리자 또는 [`Move-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterGroup?view=win10-ps) Cmdlet의 **Move** 를 사용 합니다.  

3. 모든 노드가 Windows Server 2016로 업그레이드 되 고 클러스터에 다시 추가 되었거나 나머지 Windows Server 2012 R2 노드가 제거 된 경우 다음을 수행 합니다.  

    > [!IMPORTANT]  
    > -   클러스터 기능 수준을 업데이트 한 후에는 Windows Server 2012 R2 기능 수준으로 돌아갈 수 없으며 Windows Server 2012 R2 노드를 클러스터에 추가할 수 없습니다.
    > -   [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) cmdlet이 실행 될 때까지 프로세스를 완전히 되돌릴 수 있으며 windows Server 2012 R2 노드를이 클러스터에 추가할 수 있으며 windows server 2016 노드를 제거할 수 있습니다.  
    > -   [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) cmdlet을 실행 한 후에는 새로운 기능을 사용할 수 있습니다.  

    1.  장애 조치(Failover) 클러스터 관리자 UI 또는 [`Get-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) cmdlet을 사용 하 여 클러스터에서 모든 클러스터 역할이 예상 대로 실행 되 고 있는지 확인 합니다. 다음 예제에서는 사용 가능한 저장소를 사용 하지 않고 CSV를 사용 합니다. 따라서 사용 가능한 저장소에는 **오프 라인** 상태가 표시 됩니다 (그림 18 참조).  

        ![Screencap-ClusterGroup cmdlet의 출력을 보여 주는](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **그림 18: [`Get-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) cmdlet을 사용 하 여 모든 클러스터 그룹 (클러스터 역할)이 실행 중인지 확인**  

    2.  [`Get-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) cmdlet을 사용 하 여 모든 클러스터 노드가 온라인 상태이 고 실행 중인지 확인 합니다.  
    3.  [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx) cmdlet을 실행 합니다. 오류가 반환 되어서는 안 됩니다 (그림 19 참조).  

        ClusterFunctionalLevel cmdlet의 출력을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **그림 19: PowerShell을 사용 하 여 클러스터의 기능 수준 업데이트**  

    4.  [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) cmdlet을 실행 한 후에는 새로운 기능을 사용할 수 있습니다.  

4. Windows Server 2016-정상 클러스터 업데이트 및 백업 다시 시작:  

    1. 이전에 CAU를 실행 한 경우 CAU UI를 사용 하 여 다시 시작 하거나 [`Enable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) cmdlet을 사용 합니다 (그림 20 참조).  

        Add-cauclusterrole](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png)의 출력을 보여 주는 ![Screencap  
        **그림 20: [`Enable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) cmdlet을 사용 하 여 클러스터 인식 업데이트 역할 사용**  

    2. 백업 작업을 다시 시작 합니다.  

5. Hyper-v Virtual Machines에서 Windows Server 2016 기능을 사용 하도록 설정 하 고 사용 합니다.  

    1. 클러스터가 Windows Server 2016 기능 수준으로 업그레이드 된 후 Hyper-v Vm 등의 많은 작업에는 새로운 기능이 제공 됩니다. 새 Hyper-v 기능 목록을 보려면 [가상 컴퓨터 마이그레이션 및 업그레이드를](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms) 참조 하세요.  

    2. 클러스터의 각 Hyper-v 호스트 노드에서 [`Get-VMHostSupportedVersion`](https://docs.microsoft.com/powershell/module/hyper-v/Get-VMHostSupportedVersion?view=win10-ps) cmdlet을 사용 하 여 호스트에서 지원 되는 hyper-v VM 구성 버전을 확인 합니다.  

        VMHostSupportedVersion cmdlet의 출력을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **그림 21: 호스트에서 지원 되는 Hyper-v VM 구성 버전 보기**  

   3. 클러스터의 각 Hyper-v 호스트 노드에서 Hyper-v VM 구성 버전은 사용자를 사용 하 여 간단한 유지 관리 기간을 예약 하 고, 가상 컴퓨터를 백업 및 해제 하 고, [`Update-VMVersion`](https://docs.microsoft.com/powershell/module/hyper-v/Update-VMVersion?view=win10-ps) cmdlet을 실행 하 여 업그레이드할 수 있습니다 (그림 22 참조). 이렇게 하면 가상 컴퓨터 버전이 업데이트 되 고 새 Hyper-v 기능이 사용 되므로 향후 Hyper-v 통합 구성 요소 (IC) 업데이트가 필요 하지 않습니다. 이 cmdlet은 VM을 호스팅하는 Hyper-v 노드에서 실행 하거나, `-ComputerName` 매개 변수를 사용 하 여 VM 버전을 원격으로 업데이트할 수 있습니다. 이 예제에서는 VM1의 구성 버전을 5.0에서 7.0으로 업그레이드 하 여 프로덕션 검사점 (응용 프로그램 일치 백업), 이진 VM 구성 파일 등이 VM 구성 버전과 관련 된 많은 새 Hyper-v 기능을 활용 합니다.  

       작업 중인 업데이트-VMVersion cmdlet을 보여 주는 ![Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
       **그림 22: 업데이트-VMVersion PowerShell cmdlet을 사용 하 여 VM 버전 업그레이드**  

6. 저장소 풀은 [업데이트-StoragePool](https://docs.microsoft.com/powershell/module/storage/Update-StoragePool?view=win10-ps) PowerShell cmdlet을 사용 하 여 업그레이드할 수 있습니다 .이 작업은 온라인 작업입니다.  

사설 클라우드 시나리오, 특히 Hyper-v 및 스케일 아웃 파일 서버 클러스터를 대상으로 하지만, 가동 중지 시간 없이 업그레이드 될 수 있지만 클러스터 역할에 클러스터 OS 롤링 업그레이드 프로세스를 사용할 수 있습니다.  

## <a name="restrictions--limitations"></a>제한 사항  
- 이 기능은 Windows server 2012 r 2에서 Windows Server 2016 버전에만 적용 됩니다. 이 기능은 windows server 2008, Windows Server 2008 R2 또는 Windows server 2012와 같은 이전 버전의 Windows Server를 Windows Server 2016로 업그레이드할 수 없습니다.  
- 각 Windows Server 2016 노드는 다시 포맷 하거나 새로 설치 해야 합니다. "내부" 또는 "업그레이드" 설치 유형을 권장 하지 않습니다.  
- Windows server 2016 노드를 클러스터에 추가 하려면 Windows Server 2016 노드를 사용 해야 합니다.  
- 혼합 OS 모드 클러스터를 관리 하는 경우 항상 Windows Server 2016를 실행 하는 상위 수준 노드에서 관리 작업을 수행 합니다. 하위 Windows Server 2012 R2 노드는 Windows Server 2016에 대해 UI 또는 관리 도구를 사용할 수 없습니다.  
- 일부 클러스터 기능이 혼합 OS 모드에 대해 최적화 되지 않았기 때문에 고객이 클러스터 업그레이드 프로세스를 신속 하 게 진행 하는 것이 좋습니다.  
- Windows server 2016 노드에서 하위 수준 Windows Server 2012 R2 노드로 장애 조치 (failover) 시 발생할 수 있는 호환성으로 인해 클러스터가 혼합 OS 모드에서 실행 되는 동안 Windows Server 2016 노드에서 저장소를 만들거나 크기를 조정 하지 마십시오.  

## <a name="frequently-asked-questions"></a>질문과 대답  
**혼합 OS 모드에서 장애 조치 (failover) 클러스터를 실행할 수 있는 기간**  
    고객은 4 주 이내에 업그레이드를 완료 하는 것이 좋습니다. Windows Server 2016에는 많은 최적화가 있습니다. Hyper-v와 스케일 아웃 파일 서버 클러스터의 가동 중지 시간을 총 4 시간 미만으로 업그레이드 했습니다.  

**이 기능을 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008로 다시 이식할 까 요?**  
    이 기능을 이전 버전으로 다시 이식할 계획이 없습니다. 클러스터 OS 롤링 업그레이드는 windows server 2012 R2 클러스터를 Windows Server 2016 이상으로 업그레이드 하기 위한 비전입니다.  

**클러스터 OS 롤링 업그레이드 프로세스를 시작 하기 전에 Windows Server 2012 R2 클러스터에 모든 소프트웨어 업데이트가 설치 되어 있어야 하나요?**  
    예, 클러스터 OS 롤링 업그레이드 프로세스를 시작 하기 전에 모든 클러스터 노드가 최신 소프트웨어 업데이트로 업데이트 되었는지 확인 합니다.  

**노드가 끄거나 일시 중지 된 상태에서 [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) cmdlet을 실행할 수 있나요?**  
    No. [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) cmdlet이 작동 하려면 모든 클러스터 노드가 및 active directory에 있어야 합니다.  

**클러스터 운영 체제 롤링 업그레이드는 모든 클러스터 워크 로드에서 작동 하나요? SQL Server에 대해 작동 합니까?**  
    예, 클러스터 OS 롤링 업그레이드는 모든 클러스터 워크 로드에 대해 작동 합니다. 그러나 Hyper-v 및 스케일 아웃 파일 서버 클러스터의 경우에는 가동 중지 시간이 0 일 뿐입니다. 대부분의 다른 워크 로드는 장애 조치 (failover) 시 일부 가동 중지 시간 (일반적으로 몇 분 정도)이 발생 하 고, 클러스터 OS 롤링 업그레이드 프로세스 중에 한 번 이상 장애 조치가 필요 합니다.  

**PowerShell을 사용 하 여이 프로세스를 자동화할 수 있나요?**  
    예, PowerShell을 사용 하 여 자동화 되도록 클러스터 OS 롤링 업그레이드를 설계 했습니다.  

**추가 워크 로드 및 장애 조치 (failover) 용량이 있는 대형 클러스터의 경우 여러 노드를 동시에 업그레이드할 수 있나요?**  
    예. OS를 업그레이드 하기 위해 클러스터에서 노드 하나를 제거 하면 클러스터는 장애 조치 (failover)를 위해 하나의 노드를 포함 하므로 장애 조치 (failover) 용량이 줄어듭니다. 워크 로드 및 장애 조치 용량이 충분 한 대용량 클러스터의 경우 여러 노드를 동시에 업그레이드할 수 있습니다. 클러스터 노드를 클러스터에 일시적으로 추가 하 여 클러스터 OS 롤링 업그레이드 프로세스 중에 향상 된 워크 로드 및 장애 조치 (failover) 용량을 제공할 수 있습니다.  

**[`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) 성공적으로 실행 된 후 클러스터에서 문제가 발견 되 면 어떻게 되나요?**  
    [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)를 실행 하기 전에 시스템 상태 백업을 사용 하 여 클러스터 데이터베이스를 백업한 경우 Windows Server 2012 R2 클러스터 노드에서 정식 복원을 수행 하 고 원래 클러스터 데이터베이스 및 구성을 복원할 수 있습니다.  

**시스템 드라이브를 다시 포맷 하 여 클린 OS 설치를 사용 하는 대신 각 노드에 대해 전체 업그레이드를 사용할 수 있나요?**  
    Windows Server의 현재 위치 업그레이드는 사용 하지 않는 것이 좋지만 기본 드라이버가 사용 되는 경우도 있습니다. 클러스터 노드의 전체 업그레이드 중에 표시 되는 모든 경고 메시지를 주의 깊게 읽으십시오.  

**Hyper-v 클러스터의 hyper-v VM에 Hyper-v 복제를 사용 하는 경우 클러스터 OS 롤링 업그레이드 프로세스 중 및 후에 복제가 그대로 유지 되나요?**  
    예, 클러스터 OS 롤링 업그레이드 프로세스 도중 및 후에 Hyper-v 복제본이 그대로 유지 됩니다.  

**SCVMM (System Center 2016 Virtual Machine Manager)을 사용 하 여 클러스터 OS 롤링 업그레이드 프로세스를 자동화할 수 있나요?**  
    예, System Center 2016에서 VMM을 사용 하 여 클러스터 OS 롤링 업그레이드 프로세스를 자동화할 수 있습니다.  

## <a name="see-also"></a>참고 항목  
-   [릴리스 정보: Windows Server 2016의 중요 한 문제](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Windows Server 2016의 새로운 기능](../get-started/What-s-New-in-windows-server-2016.md)  
-   [Windows Server 장애 조치 (Failover) 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)  
