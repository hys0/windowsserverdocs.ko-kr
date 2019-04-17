---
title: "롤링 업그레이드 클러스터 운영 체제"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2017
ms.openlocfilehash: 8463c163294a4d2223a74b7cfeaea6ac5ae4fcfe
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-operating-system-rolling-upgrade"></a>롤링 업그레이드 클러스터 운영 체제

> 에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016

클러스터 OS 배포 업그레이드 관리자를 클러스터 노드에서 운영 체제의 Hyper-v 또는 확장 파일 서버 작업 중단 없이 업그레이드할 수 있습니다. 이 기능을 사용 하 여, 작동 중지 저하 문제에 대 한 서비스 계약 (SLA 수준) 방지할 수 있습니다.

클러스터 OS 배포 업그레이드는 다음 이점을 제공합니다.

- Hyper-v 가상 컴퓨터가 및 확장 파일 서버 (SOFS) 작업을 실행 하는 장애 클러스터 Windows Server 2016 (Windows Server 2012 r 2 (모든 노드에서 클러스터의 실행)에서 업그레이드할 수 있습니다. 클러스터의 일부 클러스터 노드에서 실행) 작동 중단 없이 합니다. (일반적으로 5 분) Windows Server 2016에 장애 하는 데 걸리는 시간 동안 SQL Server 등 기타 클러스터 작업 사용할 수 없게 됩니다 수 있습니다.  
- 하면 모든 추가 하드웨어가 필요 하지 않습니다. 추가 추가할 수는 있지만 클러스터 노드에서 일시적으로 클러스터 OS 배포 업그레이드 하는 동안 클러스터의 사용 가능 시간을 개선 하기 위해 작은 클러스터로 처리 합니다.  
- 클러스터 중지 되거나 다시 시작 필요가 없습니다.  
- 새 클러스터 필요 하지 않습니다. 기존 클러스터 업그레이드 됩니다. 또한, Active Directory에 저장 된 기존 클러스터 개체 사용 됩니다.  
- 업그레이드 프로세스는 Update-ClusterFunctionalLevel PowerShell cmdlet 실행 될 때와 Windows Server 2016 실행 하는 고객 choses "지점-의-아니요-반품" 모두 클러스터 노드에서 때까지 되돌릴 수 있습니다.  
- 클러스터 혼합 OS 모드에서 실행 하면서 패치 및 유지 관리 작업을 지원할 수 있습니다.  
- PowerShell 및 WMI 통해 자동화를 지원합니다.  
- 클러스터 공개 속성 **ClusterFunctionalLevel** 속성 Windows Server 2016 클러스터 노드에서 클러스터의 상태를 표시 합니다. 이 속성 PowerShell cmdlet Windows Server 2016 클러스터 노드에서 클러스터 장애 조치에 속하는에서 사용 하 여 쿼리 될 수 있습니다.  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    값 **8** 클러스터 Windows Server 2012 r 2 기능 수준에서 실행 되 고 있는지를 나타냅니다. 값 **9** 클러스터 Windows Server 2016 기능 수준에서 실행 되 고 있는지를 나타냅니다.  

이 가이드 클러스터 OS 배포 업그레이드 프로세스, 설치 단계가, 기능이 제한 사항 및 (Faq)를 자주 묻는 질문의 다양 한 단계에 설명 하 고 Windows Server 2016 클러스터 OS 배포 업그레이드 다음과 같은 경우에 적용 됩니다.  
- Hyper-v 클러스터  
- 확장 파일 서버 클러스터  

Windows Server 2016에서는 다음과 같은 경우 지원 되지 않습니다.  
-  가상 하드 디스크를 사용 하 여 클러스터 클러스터의 게스트 OS를 업그레이드 배포 (.vhdx file) 공유 저장소로  

클러스터 OS 배포 업그레이드 하 여 시스템 센터 가상 컴퓨터 관리자 (SCVMM) 2016 완벽 하 게 지원 합니다. SCVMM 2016을 사용 하는 경우 [vmm에서 Windows Server 2016 Windows Server 2012 r 2 업그레이드 클러스터](https://technet.microsoft.com/library/mt445417.aspx) 클러스터의 업그레이드 및 자동화이 문서에 나와 있는 단계에 있습니다.  

## <a name="requirements"></a>요구 사항  
클러스터 OS 배포 업그레이드 프로세스를 시작 하기 전에 다음과 같은 요구 사항을 완료 합니다.

- 장애 조치 (세미콜론 연간 채널) Windows Server, Windows Server 2016 또는 Windows Server 2012 r 2 실행 클러스터 시작 합니다.
- Windows Server, Storage Spaces Direct 클러스터 업그레이드 버전 1709 지원 되지 않습니다.
- 확장 파일 서버 또는 Hyper-v Vm 클러스터 작업 인지에 0 가동 업그레이드를 기대할 수 있습니다.
- Hyper-v 노드 두 번째 수준 주소 표 SLAT (); 다음 방법 중 하나를 사용 하 여 원하는 Cpu 있는지 확인  
        -검토 하 고 [SLAT 호환 되는 얼마나 되나요? W p 8 SDK 팁 01](http://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) CPU SLATs를 지원 하는지 확인 하는 두 가지 방법을 설명 하는 문서  
        -다운로드는 [Coreinfo v3.31](https://technet.microsoft.com/sysinternals/cc835722) CPU SLAT 지원 하는지 확인 하는 도구입니다.

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>클러스터 클러스터 OS 배포 업그레이드 하는 동안 상태가 전환

이 섹션 클러스터 OS 배포 업그레이드를 사용 하 여 Windows Server 2016에 업그레이드 하는 Windows Server 2012 r 2 클러스터의 다양 한 전환 상태에 설명 합니다.  

Windows Server 2016에는 Windows Server 2012 r 2 노드에서 클러스터 작업 이동 클러스터 OS 배포 업그레이드 프로세스 중에 실행 클러스터 작업을 유지 하기 위해 노드 두 노드는 Windows Server 2012 r 2 운영 체제를 실행 하는 경우 작동 합니다. Windows Server 2016 노드의 클러스터에 추가 되 면 Windows Server 2012 r 2 호환 모드에서 작동 합니다. "혼합 OS 모드" 라고 하는 새로운 개념 클러스터 모드를 통해 노드 동일한에 존재 하 다른 버전의 클러스터 (1 그림 참조).  

![그림 클러스터 OS 롤링 업그레이드 하는 세 단계: 모든 노드 Windows Server 2012 R2, 혼합 OS 모드 및 모든 노드 Windows Server 2016](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**그림 1: 클러스터 운영 체제 상태 전환**  

Windows Server 2012 r 2 클러스터 Windows Server 2016 노드에서 클러스터에 추가 되 면 혼합 OS 모드로 전환 합니다. 프로세스는 완벽 하 게 되돌릴 수-Windows Server 2016 노드의 클러스터에서 제거할 수 및 Windows Server 2012 r 2 노드가이 모드에서는 클러스터에 추가 될 수 있습니다. "지점의 아니요 반환" Update-ClusterFunctionalLevel PowerShell cmdlet 클러스터에서 실행 될 때 발생 합니다. 성공 하려면이 cmdlet에 대 한 순서를 모든 노드 Windows Server 2016 있어야 하 고 모든 노드 온라인 상태 여야 합니다.  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>롤링 OS 업그레이드를 수행 하는 동안 4 노드에서 클러스터의 상태가 전환

이 섹션에서는 공유 저장 된 노드를 Windows Server 2016에 Windows Server 2012 r 2의 업그레이드와 클러스터의 네 가지 다른 단계에 설명 합니다.  

"1 단계" 상태가 초기-Windows Server 2012 r 2 클러스터 하 여 시작 합니다.  

![초기 상태를 보여주는: 모든 노드 Windows Server 2012 r 2](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**그림 2: 초기 상태: Windows Server 2012 r 2 장애 조치 클러스터 (1 단계)**  

"단계를 2", 두 노드 일시 중지, 소모, 제거, 다시 포맷 되어 Windows Server 2016을 사용 하 여 설치 합니다.  

![혼합 OS 모드에서 그림 클러스터: 예제 4 노드에서 클러스터에서 두 개의 노드 Windows Server 2016 실행 되 고 두 개의 노드 Windows Server 2012 r 2를 실행 하는](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**그림 3: 중간 상태: 모드 혼합 운영 체제: Windows Server 2012 r 2와 Windows Server 2016 장애 조치 (2 단계) 클러스터**  

"은 3 단계 하 고" 하 고 Windows Server 2016 업그레이드 모든 클러스터에서 노드에서 클러스터 Update-ClusterFunctionalLevel PowerShell cmdlet와 업그레이드할 준비가 되어 합니다.  

> [!NOTE]  
> 이 단계에서 프로세스를 완벽 하 게 전환할 수 있습니다 및 Windows Server 2012 r 2 노드가이 클러스터에 추가 될 수 있습니다.  

![클러스터 Windows Server 2016 최고로 업그레이드와 Windows Server 2016 최대 클러스터 기능 수준을 상태로 Update-ClusterFunctionalLevel cmdlet에 대 한 준비가 되 그림](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**그림 4: 중간 상태: Windows Server 2016을 준비 Update-ClusterFunctionalLevel (3 단계)로 업그레이드 하는 모든 노드**  

클러스터는 Update-ClusterFunctionalLevelcmdlet를 실행 한 후 "4 단계"을 새로운 Windows Server 2016 클러스터 기능을 사용할 수 있는 입력 합니다.  

![그림은 OS 업그레이드 롤링 클러스터 성공적으로 완료 된 것입니다. Windows Server 2016 업그레이드 된 모든 노드에서 클러스터 Windows Server 2016 클러스터 기능 수준에서 실행 되 고](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**그림 5: 최종 상태: Windows Server 2016 장애 조치 (4 단계) 클러스터**  

## <a name="cluster-os-rolling-upgrade-process"></a>업그레이드 프로세스 배포 클러스터 운영 체제

클러스터 OS 배포 업그레이드를 수행 하기 위한 워크플로 설명 합니다.  

![클러스터 업그레이드 워크플로 그림](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**업그레이드 프로세스 워크플로 배포 그림 6: 클러스터 운영 체제**  

클러스터 OS 배포 업그레이드는 다음 단계에 포함 됩니다.  

1. 다음과 같이 클러스터 운영 체제로 업그레이드를 준비 합니다.  
    1. 클러스터 OS 배포 업그레이드 한 번에 하나의 노드에서 클러스터에서 제거 해야 합니다. 운영 체제 업그레이드 클러스터에서 클러스터 노드에서 중 하나를 제거 하면 만들 Sla 유지 하기 위해 클러스터에 충분 한 용량 있는지 확인 합니다. 즉, 필요한 다른 노드로 장애 작업 하는 기능이 클러스터 OS 배포 업그레이드 프로세스 중 하나 노드에서 클러스터에서 제거 되 면? 클러스터는 클러스터 OS 배포 업그레이드에 대 한 한 노드에서 클러스터에서 제거 될 때 필요한 작업을 실행할 수 있는 용량이 있습니까?  
    2. Hyper-v 작업에 대 한 모든 Windows Server 2016 Hyper-v 호스트 두 번째 수준 주소 표 SLAT ()을 지원 CPU 있는지 확인 합니다. Windows Server 2016 SLAT 가능한 컴퓨터 에서만 Hyper-v 역할을 사용할 수 있습니다.  
    3. 확인 작업 백업의 완료 하 고 백업 클러스터 것이 좋습니다. 노드의 클러스터에 추가 하는 동안 백업 작동을 중지 합니다.  
    4. 모든 클러스터 노드에서 온라인 상태 인지 확인/를 사용 하 여 실행/위로 [`Get-ClusterNode`](https://technet.microsoft.com/library/ee460990.aspx)cmdlet (7 그림 참조).  

        ![실행 Get-ClusterNode cmdlet 결과 보여 주는 Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **그림 7: Get-ClusterNode cmdlet 사용 하 여 노드 상태 확인**  

    5. 클러스터 알고 업데이트 (CAU)를 실행 하는 경우 확인을 사용 하 여 CAU 현재 실행 중인 경우는 **클러스터 Aware 업데이트** UI를 또는 [`Get-CauRun`](https://technet.microsoft.com/library/hh847230.aspx)cmdlet (8 그림 참조). CAU 사용 중지는 [`Disable-CauClusterRole`](https://technet.microsoft.com/library/hh847219.aspx)cmdlet (참조 그림 9)를 일시 중지 하거나 클러스터 OS 배포 업그레이드 프로세스 중 CAU에 의해 소모 된 노드 방지 합니다.  

        ![Screencap Get-CauRun cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **그림 8:를 사용 하 여 [`Get-CauRun`](https://technet.microsoft.com/library/hh847230.aspx)cmdlet 클러스터 인식 업데이트 클러스터에서 실행 되 고 있는지 확인 하려면**  

        ![Screencap Disable-CauClusterRole cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **그림 9: 비활성화 사용 하 여 인식 업데이트 클러스터 역할은 [`Disable-CauClusterRole`](https://technet.microsoft.com/library/hh847219.aspx)cmdlet**  

2. 각 노드에서 클러스터에는 다음을 수행 합니다.  
    1. 노드를 선택 하 고 사용 하 여 클러스터 관리자 UI를 사용 하 여 **일시 중지 | 방전** 노드 방전 메뉴 옵션 (10 그림 참조)를 사용 하거나는 [`Suspend-ClusterNode`](https://technet.microsoft.com/library/ee461051.aspx)cmdlet (11 그림 참조).  

        ![Ui가 클러스터 관리자 역할 소모 하는 방법을 보여 주는 Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **클러스터 장애 조치 관리자를 사용 하 여 노드에서 드레이닝 역할 그림 10:**  

        ![Screencap Suspend-ClusterNode cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **그림 11: 역할을 사용 하 여 노드 으로부터 소모 하 고 [`Suspend-ClusterNode`](https://technet.microsoft.com/library/ee461051.aspx)cmdlet**  

    2.  클러스터 관리자 UI를 사용 하 여 **Evict** 일시 중지 된 노드에서 클러스터 또는 사용 하 여에서는 [`Remove-ClusterNode`](https://technet.microsoft.com/library/ee461001.aspx)cmdlet 합니다.  

        ![Screencap Remove-ClusterNode cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **그림 12: 사용 하 여 클러스터 노드가 제거 [`Remove-ClusterNode`](https://technet.microsoft.com/library/ee461001.aspx)cmdlet**  

    3.  시스템 드라이브를 포맷 하 고 사용 하 여 노드에서 "운영 체제를 새로 설치 하 고" Windows Server 2016을 수행는 **사용자 지정: Windows 설치만 (고급)** setup.exe 옵션 (그림 참조 13)를 설치 합니다. 선택 하 않도록는 **업그레이드: Windows 설치 및 유지 파일, 설정 및 응용 프로그램** 옵션 이후 OS 배포 업그레이드 클러스터 업그레이드 권장 하지 않습니다.  

        ![보여 주는 사용자 지정 설치 옵션을 선택 하 고 Windows Server 2016 설치 마법사 Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **Windows Server 2016에 대 한 사용 가능한 설치 옵션 그림 13:**  

    4.  노드 적절 한 Active Directory 도메인에 추가 합니다.  
    5.  관리자가 그룹에 해당 사용자를 추가 합니다.  
    6.  서버 관리자 UI 또는 Install-WindowsFeature PowerShell cmdlet, 사용 하 여 설치 Hyper-v 등 해야 하는 모든 서버 역할 합니다.  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  서버 관리자 UI 또는 Install-WindowsFeature PowerShell cmdlet, 사용 하 여 클러스터링 기능을 설치 합니다.  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  클러스터 작업에 필요한 추가 기능이 설치 합니다.  
    9. 클러스터 장애 조치 관리자 UI를 사용 하 여 저장소 및 네트워크 연결 설정을 확인 합니다.  
    10. Windows 방화벽을 사용 하는 경우 클러스터 방화벽 설정이 올바른지 확인 합니다. 예를 들어 클러스터 인식 업데이트 (CAU) 활성화 클러스터 방화벽 구성이 필요할 수 있습니다.  
    11. Hyper-v 작업에 대해 가상 스위치 관리자 대화를 시작 Hyper-v 관리자 UI를 사용 (14 그림 참조).  

        모든 Hyper-v 호스트 노드에서 클러스터에서에 대해 가상 스위치 이름을 사용 확인 동일 합니다.  

        ![Hyper-v 가상 스위치 관리자 대화의 위치를 보여 주는 Screencap](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **가상 스위치 관리자 그림 14:**  

    12. Windows Server 2016 노드에서 (Windows Server 2012 r 2 노드 사용 하지 않음), 클러스터 장애 조치 관리자를 사용 (참조 그림 15) 클러스터에 연결할 수 있습니다.  

        ![Screencap 선택 클러스터 대화 상자를 표시 합니다.](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)  
        **그림 15: 노드의 클러스터 장애 조치 관리자를 사용 하 여 클러스터에 추가**  

    13. 클러스터 장애 조치 관리자 UI를 사용 하거나 [`Add-ClusterNode`](https://technet.microsoft.com/library/ee461047.aspx)cmdlet 노드에서 클러스터에 추가 하려면 (참조 그림 16).  

        ![Screencap Add-ClusterNode cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **그림 16: 노드를 사용 하 여 클러스터에 추가 [`Add-ClusterNode`](https://technet.microsoft.com/library/ee461047.aspx)cmdlet**  

        > [!NOTE]  
        > 첫 번째 Windows Server 2016 노드에서 클러스터에 가입 하는 경우 클러스터 "혼합 OS" 모드 및 리소스를 Windows Server 2016 노드 이동 클러스터 core를 입력 합니다. "혼합 OS" 모드 클러스터 완벽 하 게 작동 새 노드 이전 노드와 호환성 모드에서 실행 되는 위치입니다. "혼합 OS" 모드는 클러스터에 대 한 일시적인 모드입니다. 것은 아닙니다 영구적 및 고객의 클러스터의 모든 노드 4 주 동안 업데이트 해야 합니다.  

    14. Windows Server 2016 노드 성공적으로 이동할 수 있습니다 (선택 사항) 클러스터 작업 중 일부를 새로 추가 된 노드로 균형을 다시 조정 작업 클러스터에서 다음과 같은 하기 위해 클러스터에 추가 됩니다.

        ![Screencap Move-ClusterVirtualMachineRole cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **사용 하 여 클러스터 작업 (VM 클러스터 역할) 그림 17: 이동 [`Move-ClusterVirtualMachineRole`](https://technet.microsoft.com/library/ee461041.aspx)cmdlet**  

        1. 사용 하 여 **실시간 마이그레이션** 가상 컴퓨터에 대 한 장애 클러스터 관리자 로부터 또는 [`Move-ClusterVirtualMachineRole`](https://technet.microsoft.com/library/ee461041.aspx)cmdlet (참조 그림 17) 가상 컴퓨터의 실시간 마이그레이션 수행할 수 있습니다.  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. 사용 하 여 **이동** 장애 조치 클러스터 관리자 또는 [`Move-ClusterGroup`](https://technet.microsoft.com/library/ee461002.aspx)클러스터 다른 작업에 대 한 cmdlet 합니다.  

3. 모든 노드를 Windows Server 2016로 업그레이드 클러스터를 다시 추가할 때 또는 Windows Server 2012 r 2 나머지 노드의 제거 되었을 때 다음을 수행 합니다.  

    > [!IMPORTANT]  
    > -   클러스터 기능 수준 업데이트 한 후 Windows Server 2012 r 2 기능 수준으로 다시 이동 수 없는 및 Windows Server 2012 r 2 노드의 클러스터에 추가할 수 없습니다.
    > -   될 때까지 [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)cmdlet 실행, 하는 과정은 완벽 하 게 되돌릴 수 및 Windows Server 2012 r 2 노드가이 클러스터에 추가 될 수 및 Windows Server 2016 노드 제거할 수 있습니다.  
    > -   이후에 [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)실행 cmdlet, 새로운 기능을 사용할 수 있습니다.  

    1.  클러스터 장애 조치 관리자 UI를 사용 하는 또는 [`Get-ClusterGroup`](https://technet.microsoft.com/library/ee461017.aspx)cmdlet, 모든 클러스터 역할 예상 대로 클러스터에서 실행 되는 확인 합니다. 다음 예제에서 사용 가능 저장 공간 사용 하지 않는, CSV 사용 되는 대신, 따라서 사용할 수 있는 저장소 표시 된 **오프 라인** 상태 (18 그림 참조).  

        ![Screencap Get-ClusterGroup cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **사용 하 여 그림 18: 실행 그룹 (클러스터 역할) 클러스터 모두 확인 하 고 [`Get-ClusterGroup`](https://technet.microsoft.com/library/ee461017.aspx)cmdlet**  

    2.  모든 클러스터 노드에서 온라인 상태 인지 확인 하 고 사용 하 여 실행는 [`Get-ClusterNode`](https://technet.microsoft.com/library/ee460990.aspx)cmdlet 합니다.  
    3.  실행는 [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)cmdlet-오류가 되돌려야 (19 그림 참조).  

        ![Screencap Update-ClusterFunctionalLevel cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **업데이트 PowerShell를 사용 하 여 클러스터의 기능 수준 그림 19:**  

    4.  이후에 [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)실행 cmdlet, 새로운 기능을 사용할 수 있습니다.  

4. Windows Server 2016-일반 클러스터 업데이트와 백업 다시 시작 합니다.  

    1. 이전에 CAU 실행 하는 것을 CAU UI를 사용 하 여를 다시 시작 하거나 사용 하 여는 [`Enable-CauClusterRole`](https://technet.microsoft.com/library/hh847229.aspx)cmdlet (20 그림 참조).  

        ![Screencap Enable-CauClusterRole 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png)  
        **사용 하 여 그림 20: 인식 업데이트 사용 가능 클러스터 역할은 [`Enable-CauClusterRole`](https://technet.microsoft.com/library/hh847229.aspx)cmdlet**  

    2. 백업 작업을 다시 시작 합니다.  

5. Hyper-v 가상 컴퓨터에서 Windows Server 2016 기능을 사용 하 여 및 사용 합니다.  

    1. Windows Server 2016 기능 수준을 클러스터로 업그레이드 후 Hyper-v Vm 같은 여러 작업 새로운 기능을 갖게 됩니다. Hyper-v의 새로운 기능 목록이 합니다. 참조 [업그레이드 가상 컴퓨터 및 마이그레이션](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms)  

    2. 각 Hyper-v 호스트의에서 노드에서 클러스터를 사용 하 여는 [`Get-VMHostSupportedVersion`](https://technet.microsoft.com/library/mt653838.aspx)cmdlet 호스트에서 지원 되는 Hyper-v VM 구성 버전을 볼 수 있습니다.  

        ![Screencap Get-VMHostSupportedVersion cmdlet 출력 표시](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **그림 21: Hyper-v VM 구성 버전은 호스트 지원 보기**  

   3.  각 Hyper-v 호스트 노드의 클러스터의, Hyper-v VM 구성 버전 간단한 유지 관리 창 사용자가 일정, 백업, 가상 컴퓨터 꺼도 및 실행 하 여 업그레이드 수 있는 [`Update-VMVersion`](https://technet.microsoft.com/library/mt484146.aspx)cmdlet (22 그림 참조). 이 가상 컴퓨터 버전을 업데이트 되며 회사 (Hyper-v 통합 구성 간) 향후 업데이트에 대 한 필요성을 제거 하는 새로운 Hyper-v 기능을 사용할 수 있습니다. 이 cmdlet VM에서 호스트 하는 Hyper-v 노드에서 실행 될 수는 또는 `-ComputerName`매개 VM 버전 원격으로 업데이트를 사용할 수 있습니다. 여기에서 여기 했습니다 v m 1 인의 구성 버전에서에서 업그레이드 5.0 7.0 이진 VM 구성 파일 프로덕션 검사점 (응용 프로그램 일관 된 백업) 등이 VM 구성 버전와 관련 된 새로운 여러 Hyper-v 기능을 활용할 수 있습니다.  

        ![Screencap Update-VMVersion cmdlet에 알림 표시](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
        **그림 22: VM 버전 Update-VMVersion PowerShell cmdlet 사용 하 여 업그레이드**  

4.  사용 하 여 저장소 풀 업그레이드할 수는 [업데이트 StoragePool](https://technet.microsoft.com/itpro/powershell/windows/storage/update-storagepool) PowerShell cmdlet-온라인 작업입니다.  

대상으로 개인 클라우드 시나리오를 특히 Hyper-v 하 고 확장 파일 서버 클러스터 클러스터 OS 배포 업그레이드 프로세스 작동 중단 없이 업그레이드할 수 있는 모든 클러스터 역할에 사용할 수 있습니다.  

## <a name="restrictions--limitations"></a>제한 / 제한  
- 이 기능은 Windows Server 2012 r 2에만 Windows Server 2016 버전에 대해서만 작동합니다. 이 기능은 Windows Server 2016 이전 버전의 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012와 같은 Windows Server 업그레이드할 수 없습니다.  
- 각 Windows Server 2016 노드만 포맷/새로 설치 해야 합니다. "위치" 또는 "업그레이드" 설치 유형을 것이 좋습니다.  
- Windows Server 2016 노드 Windows Server 2016 노드의 클러스터에 추가 하는 데 사용 해야 합니다.  
- 혼합 OS 모드 클러스터 관리 하는 경우 항상 Windows Server 2016을 실행 중인 상위 노드에서 관리 작업을 수행 합니다. Windows Server 2012 r 2 하위 노드 Windows Server 2016에 대 한 UI 또는 관리 도구를 사용할 수 없습니다.  
- 고객이 혼합 OS 모드에 대 한 일부 클러스터 기능을 최적화 되지 않으면 때문에 업그레이드 클러스터 프로세스 빠르게 이동 하는 것이 좋습니다.  
- 홈 그룹을 만들거나 저장소 Windows Server 2016 노드에서 클러스터 실행 되는 동안 혼합 OS 모드로 비 호환성으로 인해 장애 조치를 Windows Server 2016 노드에서 하위 수준 Windows Server 2012 r 2 노드를 크기 조정 되지 않도록 합니다.  

## <a name="frequently-asked-questions"></a>자주 묻는 질문  
**얼마나 오래 클러스터 장애 조치를 실행할 수 혼합 OS 모드로?**  
    고객이 4 주 내에서 업그레이드를 완료 하는 것이 좋습니다. Windows Server 2016에 최적화 여러 가지가 있습니다. 확장 파일 서버 0 가동와 4 시간 미만 전체 클러스터 및 Hyper-v 업그레이드 한 했습니다.  

**이 기능을 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 포트는 수 있나요?**  
    이전 버전으로 다시이 기능을 이식 하 없는 했습니다. 클러스터 OS 배포 업그레이드 및 Windows Server 2016에 Windows Server 2012 r 2 클러스터 업그레이드에 대 한 우리의 비전입니다.  

**클러스터 OS 배포 업그레이드 프로세스를 시작 하기 전에 설치 하는 모든 소프트웨어 업데이트를 Windows Server 2012 r 2 클러스터 필요 합니까?**  
    예, 클러스터 OS 배포 업그레이드 프로세스를 시작 하기 전에 최신 소프트웨어 업데이트 모든 클러스터 노드가 업데이트를 확인 합니다.  

**실행할 수 있는 [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)노드가 꺼져 있거나 일시 중지 하는 동안 cmdlet?**  
    아니요. 일부 클러스터 노드 및 현재 등록 해야는 [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)cmdlet 작동 하도록 합니다.  

**모든 클러스터 작업에 대해 작동 OS 배포 업그레이드 클러스터 합니까? SQL Server에 대 한 작동 하나요?**  
    예, OS 배포 업그레이드 클러스터 모든 클러스터 작업에 대해 작동합니다. 그러나 0-하기만 Hyper-v 및 확장 파일 서버 클러스터 됩니다. 대부분의 다른 작업 때 일부 작동 중지 (일반적으로 몇 분) 요금이 자녀가 클러스터 OS 배포 업그레이드 프로세스 중에 한 번 이상 장애 조치를 및 장애 필요 합니다.  

**PowerShell를 사용 하 여이 프로세스를 자동화 수 있나요?**  
    예, 클러스터 OS PowerShell를 사용 하 여 자동으로 업그레이드 롤링 설계 되었습니다.  

**추가 작업 및 장애 용량이 큰 클러스터로 업그레이드할 수 여러 노드 동시에 있나요?**  
    예입니다. 한 노드에서 클러스터 OS를 업그레이드 제거 되 면 클러스터 장애 조치를 덜 한 노드를 갖게 됩니다, 그리고 따라서는 감소 장애 조치 용량 합니다. 충분 한 작업 및 장애 용량이 큰 클러스터에 대 한 여러 노드 동시에 업그레이드할 수 있습니다. 일시적으로 클러스터 노드에서 클러스터 OS 배포 업그레이드 프로세스 중 향상 된 작업 및 장애 용량을 제공 하기 위해 클러스터에 추가할 수 있습니다.  

**후 내 클러스터의 문제가 발견 하면 어떻게 [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx)성공적으로 실행 되나요?**  
    사용자가 백업 클러스터 데이터베이스 실행 하기 전에 시스템 상태 백업 사용 하는 경우 [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx), 된 신뢰할 수 있다고 수행할 수 복원 Windows Server 2012 r 2 클러스터 노드에서 클러스터 데이터베이스 원래 및 구성 복원 합니다.  

**각 노드 시스템 드라이브를 포맷 하 여 OS 새로 설치를 사용 하는 대신에 대 한 업그레이드를 사용할 수 있나요?**  
    기본 드라이버를 사용 하는 경우에 따라 제대로 작동 하는지 확인 있지만 업그레이드 Windows Server의 사용 권장 하지 않습니다. 클러스터 노드에서의 현재 위치에서 업그레이드 하는 동안 모든 경고 메시지를 표시 잘 읽어 주세요.  

**내 Hyper-v 클러스터의 Hyper-v 복제 Hyper-v VM를 사용 하 고, 경우 복제 그대로 유지 됩니다 클러스터 OS 배포 업그레이드 프로세스가 완료 된 후 한 동안?**  
    예, 클러스터 OS 배포 업그레이드 프로세스가 완료 된 후 한 동안 Hyper-v 복제본 그대로 남아 있습니다.  

**클러스터 OS 배포 업그레이드 과정을 시스템 센터 2016 가상 컴퓨터 관리자 (SCVMM)을 사용할 수 있나요?**  
    예, 클러스터 OS 배포 업그레이드 프로세스 VMM 센터 2016 시스템에서에서 사용 하 여 자동화 수 있습니다.  

## <a name="see-also"></a>참조 하십시오  
-   [Windows Server 2016에서 중요 한 사항이 릴리스 정보:](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Windows Server 2016에서 새로운 기능](../get-started/What-s-New-in-windows-server-2016.md)  
-   [Windows Server에서 장애 조치 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)  