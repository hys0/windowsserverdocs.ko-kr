---
title: 스토리지 공간 다이렉트 클러스터를 Windows Server 2019로 업그레이드
description: Vm을 실행 하는 동안 또는 중지 된 상태에서 스토리지 공간 다이렉트 클러스터를 Windows Server 2019로 업그레이드 하는 방법입니다.
author: robhindman
ms.author: robhind
manager: eldenc
ms.date: 03/06/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-spaces
ms.openlocfilehash: 9966ee0fd3c0a2d1df0180bf177dec03343efc14
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867193"
---
# <a name="upgrade-a-storage-spaces-direct-cluster-to-windows-server-2019"></a>스토리지 공간 다이렉트 클러스터를 Windows Server 2019로 업그레이드

이 항목에서는 스토리지 공간 다이렉트 클러스터를 Windows Server 2019로 업그레이드 하는 방법에 대해 설명 합니다. [클러스터 OS 롤링 업그레이드 프로세스](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md) 를 사용 하 여 windows server 2016에서 windows server 2019로 스토리지 공간 다이렉트 클러스터를 업그레이드 하는 방법에는 네 가지가 있습니다. 두 가지 방법으로 vm을 실행 중인 상태로 유지 하 고 vm을 중지 하는 두 가지 방법이 있습니다. 각 접근 방식의 장점과 약점은 서로 다르므로 조직의 요구 사항에 가장 적합 한 것을 선택 합니다.

- Vm이 클러스터의 각 서버에서 **실행 되는 동안 전체 업그레이드** -이 옵션을 선택 하면 vm 가동 중지 시간이 발생 하지 않지만 각 서버가 업그레이드 된 후 저장소 작업 (미러 복구)이 완료 될 때까지 기다려야 합니다.

- 클러스터의 각 서버에서 **vm이 실행 되는 동안 클린 운영 체제 설치** -이 옵션을 선택 하면 vm 가동 중지 시간이 발생 하지 않지만 각 서버가 업그레이드 된 후 저장소 작업 (미러 복구)이 완료 될 때까지 기다려야 하므로 각 서버와 앱 및 역할.

- 클러스터의 각 서버에서 **vm이 중지 되는 동안 전체 업그레이드** -이 옵션을 선택 하면 vm 가동 중지 시간이 발생 하지만 저장소 작업 (미러 복구)을 기다릴 필요가 없으므로 속도가 더 빠릅니다.

- **클린-OS 설치** 클러스터의 각 서버에서 vm이 중지 되는 동안이 옵션을 선택 하면 vm 가동 중지 시간이 발생 하지만 저장소 작업 (미러 복구)을 기다릴 필요 없이 더 빠르게 수행할 수 있습니다.

## <a name="prerequisites-and-limitations"></a>사전 요구 사항 및 제한 사항

업그레이드를 계속 하기 전에 다음을 수행 합니다.

- 업그레이드 프로세스 중에 문제가 발생 하는 경우 백업을 사용할 수 있는지 확인 합니다.

- 하드웨어 공급 업체에 Windows Server 2019에서 지원할 서버에 대 한 BIOS, 펌웨어 및 드라이버가 있는지 확인 합니다.

업그레이드 프로세스에서 알아야 할 몇 가지 제한 사항이 있습니다.

- 176693.292 이전 버전의 Windows Server 2019 빌드를 사용 하도록 스토리지 공간 다이렉트 설정 하기 위해 고객은 스토리지 공간 다이렉트 및 소프트웨어 정의 네트워킹 기능을 사용할 수 있는 레지스트리 키에 대 한 Microsoft 지원에 문의 해야 할 수 있습니다. 자세한 내용은 Microsoft 기술 자료 [문서 4464776](https://support.microsoft.com/help/4464776/software-defined-data-center-and-software-defined-networking)를 참조 하십시오.

- ReFS 볼륨이 있는 클러스터를 업그레이드 하는 경우 다음과 같은 몇 가지 제한 사항이 있습니다.

- 업그레이드는 ReFS 볼륨에서 완전히 지원 되지만 업그레이드 된 볼륨은 Windows Server 2019의 ReFS 향상 기능을 활용 하지 못합니다. 미러 가속 패리티의 성능 향상과 같은 이러한 혜택에는 새로 만든 Windows Server 2019 ReFS 볼륨이 필요 합니다. 즉, `New-Volume` cmdlet 또는 서버 관리자를 사용 하 여 새 볼륨을 만들어야 합니다. 새 볼륨에서 얻을 수 있는 몇 가지 ReFS 향상 기능은 다음과 같습니다.

    - **지도 로그-바이패스**: 클러스터형 (스토리지 공간 다이렉트) 시스템에만 적용 되 고 독립 실행형 저장소 풀에는 적용 되지 않는 ReFS의 성능 향상입니다.

    - 다중 복원 력 볼륨과 관련 된 Windows Server 2019 **의 향상 된 효율성**

- Windows Server 2016 스토리지 공간 다이렉트 클러스터 서버를 업그레이드 하기 전에 서버를 저장소 유지 관리 모드로 전환 하는 것이 좋습니다. 자세한 내용은 [스토리지 공간 다이렉트 문제 해결](troubleshooting-storage-spaces.md)의 이벤트 5120 섹션을 참조 하십시오. Windows Server 2016에서는이 문제가 해결 되었지만 업그레이드 하는 동안 각 스토리지 공간 다이렉트 서버를 저장소 유지 관리 모드로 전환 하는 것이 좋습니다.

- 집합 스위치를 사용 하는 소프트웨어 정의 네트워킹 환경에는 알려진 문제가 있습니다. 이 문제에는 Windows Server 2019에서 Windows Server 2016 (이전 운영 체제로 실시간 마이그레이션)로의 Hyper-v VM 실시간 마이그레이션이 포함 됩니다. 실시간 마이그레이션을 성공적으로 수행 하려면 Windows Server 2019에서 Windows server 2016로 실시간 마이그레이션되는 vm의 VM 네트워크 설정을 변경 하는 것이 좋습니다. 이 문제는 2019-01D 핫픽스 롤업 패키지 즉, build 17763.292에서 Windows Server 2019에 대해 해결 되었습니다. 자세한 내용은 Microsoft 기술 자료 [문서 4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976)를 참조 하십시오.

위의 알려진 문제로 인해 일부 고객은 아래에 설명 된 네 가지 프로세스 중 하나를 사용 하 여 Windows Server 2016 클러스터를 업그레이드 하는 대신 새 Windows Server 2019 클러스터를 빌드하고 이전 클러스터에서 데이터를 복사 하는 것을 고려할 수 있습니다.

## <a name="performing-an-in-place-upgrade-while-vms-are-running"></a>Vm이 실행 되는 동안 전체 업그레이드 수행

이 옵션을 선택 하면 VM 가동 중지 시간이 발생 하지 않지만 각 서버가 업그레이드 된 후 저장소 작업 (미러 복구)이 완료 될 때까지 기다려야 합니다. 개별 서버는 업그레이드 프로세스 중에 순차적으로 다시 시작 되지만, 클러스터의 나머지 서버와 모든 Vm은 계속 실행 됩니다.

1. 클러스터의 모든 서버가 최신 Windows 업데이트를 설치 했는지 확인 합니다. 자세한 내용은 [windows 10 및 Windows Server 2016 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)을 참조 하세요. 최소한 Microsoft 기술 자료 [문서 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2 월 19 일, 2019)을 설치 하십시오. 빌드 번호 (명령 참조 `ver` )는 14393.2828 이상 이어야 합니다.

2. 설정 스위치로 소프트웨어 정의 네트워킹을 사용 하는 경우 관리자 권한 PowerShell 세션을 열고 다음 명령을 실행 하 여 클러스터의 모든 Vm에서 VM 실시간 마이그레이션 확인 확인을 사용 하지 않도록 설정 합니다.

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. 한 번에 하나의 클러스터 서버에서 다음 단계를 수행 합니다.

   1. Hyper-v VM 실시간 마이그레이션을 사용 하 여 업그레이드 하려고 하는 서버에서 실행 중인 Vm을 이동 합니다.

   2. 다음 PowerShell 명령을 사용 하 여 클러스터 서버를 일시 중지 합니다. 일부 내부 그룹은 숨겨집니다. 이 단계를 신중 하 게 수행 하는 것이 좋습니다. 서버에서 Vm을 아직 라이브 마이그레이션하지 않은 경우에는이 cmdlet을 사용 하 여 이전 단계를 건너뛸 수 있습니다.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. 다음 PowerShell 명령을 실행 하 여 서버를 저장소 유지 관리 모드로 전환 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. 다음 cmdlet을 실행 하 여 **OperationalStatus** 값이 **유지 관리 모드에**있는지 확인 합니다.

       ```PowerShell
       Get-PhysicalDisk
       ```

   5. **Setup.exe** 를 실행 하 고 "개인 파일 및 앱 유지" 옵션을 사용 하 여 서버에서 Windows server 2019의 업그레이드 설치를 수행 합니다. 설치가 완료 되 면 서버가 클러스터에 유지 되 고 클러스터 서비스가 자동으로 시작 됩니다.

   6. 새로 업그레이드 된 서버에 최신 Windows Server 2019 업데이트가 있는지 확인 합니다. 자세한 내용은 [windows 10 및 Windows Server 2019 업데이트 기록](https://support.microsoft.com/help/4464619/windows-10-update-history)을 참조 하세요. 빌드 번호 (명령 참조 `ver` )는 17763.292 이상 이어야 합니다.

   7. 다음 PowerShell 명령을 사용 하 여 저장소 유지 관리 모드에서 서버를 제거 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   8. 다음 PowerShell 명령을 사용 하 여 서버를 다시 시작 합니다.

       ```PowerShell
       Resume-ClusterNode
       ```

   9. 저장소 복구 작업이 완료 될 때까지 기다렸다가 모든 디스크가 정상 상태로 돌아갑니다. 서버를 업그레이드 하는 동안 실행 되는 Vm의 수에 따라 상당한 시간이 걸릴 수 있습니다. 실행할 명령은 다음과 같습니다.

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. 클러스터의 다음 서버를 업그레이드 합니다.

5. 모든 서버를 Windows Server 2019로 업그레이드 한 후에는 다음 PowerShell cmdlet을 사용 하 여 클러스터 기능 수준을 업데이트 합니다.

   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > 기술적으로는 가능한 한 빨리 클러스터 기능 수준을 업데이트 하는 것이 좋습니다. 단,이 작업을 수행 하는 데는 최대 4 주가 소요 됩니다.

6. 클러스터 기능 수준이 업데이트 된 후 다음 cmdlet을 사용 하 여 저장소 풀을 업데이트 합니다. 이 시점에서와 `Get-ClusterPerf` 같은 새 cmdlet은 클러스터의 모든 서버에서 완전히 작동 합니다.

   ```PowerShell
   Update-StoragePool
   ```

7. 필요에 따라 `Update-VMVersion` cmdlet을 사용 하 여 vm을 중지 하 고 vm을 다시 시작 하 여 vm 구성 수준을 업그레이드 합니다.

8. 위에서 설명한 대로 설정 된 스위치 및 사용 하지 않도록 설정 된 VM 실시간 마이그레이션 검사를 사용 하 여 소프트웨어 정의 네트워킹을 사용 하는 경우 다음 cmdlet을 사용 하 여 VM 실시간 확인 검사를 다시 사용 하도록 설정 합니다.

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter  SkipMigrationDestinationCheck -Value 0
   ```

9. 업그레이드 된 클러스터가 예상 대로 작동 하는지 확인 합니다. 역할은 올바르게 장애 조치 (failover) 해야 하며, VM 실시간 마이그레이션이 클러스터에서 사용 되는 경우 Vm이 성공적으로 실시간 마이그레이션됩니다.

10. 클러스터 유효성 검사 (`Test-Cluster`)를 실행 하 고 클러스터 유효성 검사 보고서를 검토 하 여 클러스터의 유효성을 검사 합니다.

## <a name="performing-a-clean-os-installation-while-vms-are-running"></a>Vm이 실행 되는 동안 클린 OS 설치 수행

이 옵션을 선택 하면 VM 가동 중지 시간이 발생 하지 않지만 각 서버가 업그레이드 된 후 저장소 작업 (미러 복구)이 완료 될 때까지 기다려야 합니다. 개별 서버는 업그레이드 프로세스 중에 순차적으로 다시 시작 되지만, 클러스터의 나머지 서버와 모든 Vm은 계속 실행 됩니다.

1. 클러스터의 모든 서버가 최신 업데이트를 실행 중인지 확인 합니다. 자세한 내용은 [windows 10 및 Windows Server 2016 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)을 참조 하세요. 최소한 Microsoft 기술 자료 [문서 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2 월 19 일, 2019)을 설치 하십시오. 빌드 번호 (명령 참조 `ver` )는 14393.2828 이상 이어야 합니다.

2. 설정 스위치로 소프트웨어 정의 네트워킹을 사용 하는 경우 관리자 권한 PowerShell 세션을 열고 다음 명령을 실행 하 여 클러스터의 모든 Vm에서 VM 실시간 마이그레이션 확인 확인을 사용 하지 않도록 설정 합니다.

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. 한 번에 하나의 클러스터 서버에서 다음 단계를 수행 합니다.

   1. Hyper-v VM 실시간 마이그레이션을 사용 하 여 업그레이드 하려고 하는 서버에서 실행 중인 Vm을 이동 합니다.

   2. 다음 PowerShell 명령을 사용 하 여 클러스터 서버를 일시 중지 합니다. 일부 내부 그룹은 숨겨집니다. 이 단계를 신중 하 게 수행 하는 것이 좋습니다. 서버에서 Vm을 아직 라이브 마이그레이션하지 않은 경우에는이 cmdlet을 사용 하 여 이전 단계를 건너뛸 수 있습니다.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. 다음 PowerShell 명령을 실행 하 여 서버를 저장소 유지 관리 모드로 전환 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. 다음 cmdlet을 실행 하 여 **OperationalStatus** 값이 **유지 관리 모드에**있는지 확인 합니다.

       ```PowerShell
       Get-PhysicalDisk
       ```

   3.  다음 PowerShell 명령을 실행 하 여 클러스터에서 서버를 제거 합니다.  

       ```PowerShell
       Remove-ClusterNode <ServerName>
       ```

   4. 서버에서 Windows Server 2019를 새로 설치 합니다. 시스템 드라이브 포맷을 수행 하 고 **setup.exe** 를 실행 한 다음 "없음" 옵션을 사용 합니다. 설치가 완료 되 고 서버가 다시 시작 된 후 서버 id, 역할, 기능 및 응용 프로그램을 구성 해야 합니다.

   5. 서버에 hyper-v 역할 및 장애 조치 (Failover) 클러스터링 기능을 설치 합니다 (cmdlet을 `Install-WindowsFeature` 사용할 수 있음).

   6. 스토리지 공간 다이렉트와 함께 사용 하기 위해 서버 제조업체에서 승인한 하드웨어의 최신 저장소 및 네트워킹 드라이버를 설치 합니다.

   7. 새로 업그레이드 된 서버에 최신 Windows Server 2019 업데이트가 있는지 확인 합니다. 자세한 내용은 [windows 10 및 Windows Server 2019 업데이트 기록](https://support.microsoft.com/help/4464619/windows-10-update-history)을 참조 하세요. 빌드 번호 (명령 참조 `ver` )는 17763.292 이상 이어야 합니다.

   8. 다음 PowerShell 명령을 사용 하 여 서버를 클러스터에 다시 가입 합니다.

       ```PowerShell
       Add-ClusterNode
       ```

   9. 다음 PowerShell 명령을 사용 하 여 저장소 유지 관리 모드에서 서버를 제거 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   10. 저장소 복구 작업이 완료 될 때까지 기다렸다가 모든 디스크가 정상 상태로 돌아갑니다. 서버를 업그레이드 하는 동안 실행 되는 Vm의 수에 따라 상당한 시간이 걸릴 수 있습니다. 실행할 명령은 다음과 같습니다.

        ```PowerShell
        Get-StorageJob
        Get-VirtualDisk
        ```

4. 클러스터의 다음 서버를 업그레이드 합니다.

5. 모든 서버를 Windows Server 2019로 업그레이드 한 후에는 다음 PowerShell cmdlet을 사용 하 여 클러스터 기능 수준을 업데이트 합니다.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > 기술적으로는 가능한 한 빨리 클러스터 기능 수준을 업데이트 하는 것이 좋습니다. 단,이 작업을 수행 하는 데는 최대 4 주가 소요 됩니다.

6. 클러스터 기능 수준이 업데이트 된 후 다음 cmdlet을 사용 하 여 저장소 풀을 업데이트 합니다. 이 시점에서와 `Get-ClusterPerf` 같은 새 cmdlet은 클러스터의 모든 서버에서 완전히 작동 합니다.

   ```PowerShell
   Update-StoragePool
   ```

7. 필요에 따라 각 vm을 중지 하 고 `Update-VMVersion` cmdlet을 사용 하 여 vm 구성 수준을 업그레이드 한 다음 vm을 다시 시작 합니다.

8. 위에서 설명한 대로 설정 된 스위치 및 사용 하지 않도록 설정 된 VM 실시간 마이그레이션 검사를 사용 하 여 소프트웨어 정의 네트워킹을 사용 하는 경우 다음 cmdlet을 사용 하 여 VM 실시간 확인 검사를 다시 사용 하도록 설정 합니다.

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" | 
   Set-ClusterParameter SkipMigrationDestinationCheck -Value 0
   ```

9. 업그레이드 된 클러스터가 예상 대로 작동 하는지 확인 합니다. 역할은 올바르게 장애 조치 (failover) 해야 하며, VM 실시간 마이그레이션이 클러스터에서 사용 되는 경우 Vm이 성공적으로 실시간 마이그레이션됩니다.

10. 클러스터 유효성 검사 (`Test-Cluster`)를 실행 하 고 클러스터 유효성 검사 보고서를 검토 하 여 클러스터의 유효성을 검사 합니다.

## <a name="performing-an-in-place-upgrade-while-vms-are-stopped"></a>Vm이 중지 된 상태에서 전체 업그레이드 수행

이 옵션은 VM 가동 중지 시간이 발생 하지만, 각 서버가 업그레이드 된 후 저장소 작업 (미러 복구)이 완료 될 때까지 기다릴 필요가 없기 때문에 업그레이드 중에 Vm을 실행 하는 것 보다 시간이 더 오래 걸릴 수 있습니다. 개별 서버는 업그레이드 프로세스 중에 순차적으로 다시 시작 되지만 클러스터의 나머지 서버는 계속 실행 됩니다.

1. 클러스터의 모든 서버가 최신 업데이트를 실행 중인지 확인 합니다. 자세한 내용은 [windows 10 및 Windows Server 2016 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)을 참조 하세요. 최소한 Microsoft 기술 자료 [문서 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2 월 19 일, 2019)을 설치 하십시오. 빌드 번호 (명령 참조 `ver` )는 14393.2828 이상 이어야 합니다.

2. 클러스터에서 실행 되는 Vm을 중지 합니다.

3. 한 번에 하나의 클러스터 서버에서 다음 단계를 수행 합니다.

   1. 다음 PowerShell 명령을 사용 하 여 클러스터 서버를 일시 중지 합니다. 일부 내부 그룹은 숨겨집니다. 이 단계를 신중 하 게 하는 것이 좋습니다.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   2. 다음 PowerShell 명령을 실행 하 여 서버를 저장소 유지 관리 모드로 전환 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   3. 다음 cmdlet을 실행 하 여 **OperationalStatus** 값이 **유지 관리 모드에**있는지 확인 합니다.

       ```PowerShell
       Get-PhysicalDisk
       ```

   4. **Setup.exe** 를 실행 하 고 "개인 파일 및 앱 유지" 옵션을 사용 하 여 서버에서 Windows server 2019의 업그레이드 설치를 수행 합니다.  
   설치가 완료 되 면 서버가 클러스터에 유지 되 고 클러스터 서비스가 자동으로 시작 됩니다.

   5.  새로 업그레이드 된 서버에 최신 Windows Server 2019 업데이트가 있는지 확인 합니다.  
   자세한 내용은 [windows 10 및 Windows Server 2019 업데이트 기록](https://support.microsoft.com/help/4464619/windows-10-update-history)을 참조 하세요.
   빌드 번호 (명령 참조 `ver` )는 17763.292 이상 이어야 합니다.

   6.  다음 PowerShell 명령을 사용 하 여 저장소 유지 관리 모드에서 서버를 제거 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   7.  다음 PowerShell 명령을 사용 하 여 서버를 다시 시작 합니다.

       ```PowerShell
       Resume-ClusterNode
       ```

   8.  저장소 복구 작업이 완료 될 때까지 기다렸다가 모든 디스크가 정상 상태로 돌아갑니다.  
   Vm이 실행 되 고 있지 않으므로 상대적으로 빨라야 합니다. 실행할 명령은 다음과 같습니다.

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. 클러스터의 다음 서버를 업그레이드 합니다.
5. 모든 서버를 Windows Server 2019로 업그레이드 한 후에는 다음 PowerShell cmdlet을 사용 하 여 클러스터 기능 수준을 업데이트 합니다.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   기술적으로는 가능한 한 빨리 클러스터 기능 수준을 업데이트 하는 것이 좋습니다. 단,이 작업을 수행 하는 데는 최대 4 주가 소요 됩니다.

6. 클러스터 기능 수준이 업데이트 된 후 다음 cmdlet을 사용 하 여 저장소 풀을 업데이트 합니다.  
   이 시점에서와 `Get-ClusterPerf` 같은 새 cmdlet은 클러스터의 모든 서버에서 완전히 작동 합니다.

   ```PowerShell
   Update-StoragePool
   ```

7. 클러스터에서 Vm을 시작 하 고 제대로 작동 하는지 확인 합니다.

8. 필요에 따라 각 vm을 중지 하 고 `Update-VMVersion` cmdlet을 사용 하 여 vm 구성 수준을 업그레이드 한 다음 vm을 다시 시작 합니다.

9. 업그레이드 된 클러스터가 예상 대로 작동 하는지 확인 합니다.  
   역할은 올바르게 장애 조치 (failover) 해야 하며, VM 실시간 마이그레이션이 클러스터에서 사용 되는 경우 Vm이 성공적으로 실시간 마이그레이션됩니다.

10. 클러스터 유효성 검사 (`Test-Cluster`)를 실행 하 고 클러스터 유효성 검사 보고서를 검토 하 여 클러스터의 유효성을 검사 합니다.

## <a name="performing-a-clean-os-installation-while-vms-are-stopped"></a>Vm이 중지 된 상태에서 클린 OS 설치 수행

이 옵션은 VM 가동 중지 시간이 발생 하지만, 각 서버가 업그레이드 된 후 저장소 작업 (미러 복구)이 완료 될 때까지 기다릴 필요가 없기 때문에 업그레이드 중에 Vm을 실행 하는 것 보다 시간이 더 오래 걸릴 수 있습니다. 개별 서버는 업그레이드 프로세스 중에 순차적으로 다시 시작 되지만 클러스터의 나머지 서버는 계속 실행 됩니다.

1. 클러스터의 모든 서버가 최신 업데이트를 실행 중인지 확인 합니다.  
   자세한 내용은 [windows 10 및 Windows Server 2016 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)을 참조 하세요.
   최소한 Microsoft 기술 자료 [문서 4487006](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2 월 19 일, 2019)을 설치 하십시오. 빌드 번호 (명령 참조 `ver` )는 14393.2828 이상 이어야 합니다.

2. 클러스터에서 실행 되는 Vm을 중지 합니다.

3. 한 번에 하나의 클러스터 서버에서 다음 단계를 수행 합니다.

   2. 다음 PowerShell 명령을 사용 하 여 클러스터 서버를 일시 중지 합니다. 일부 내부 그룹은 숨겨집니다.  
      이 단계를 신중 하 게 하는 것이 좋습니다.

       ```PowerShell
      Suspend-ClusterNode -Drain
      ```

   3. 다음 PowerShell 명령을 실행 하 여 서버를 저장소 유지 관리 모드로 전환 합니다.

      ```PowerShell
      Get-StorageFaultDomain -type StorageScaleUnit | 
      Where FriendlyName -Eq <ServerName> | 
      Enable-StorageMaintenanceMode
      ```

   4. 다음 cmdlet을 실행 하 여 **OperationalStatus** 값이 **유지 관리 모드에**있는지 확인 합니다.

      ```PowerShell
      Get-PhysicalDisk
      ```

   5. 다음 PowerShell 명령을 실행 하 여 클러스터에서 서버를 제거 합니다.  
    
      ```PowerShell
      Remove-ClusterNode <ServerName>
      ```

   6. 서버에서 Windows Server 2019를 새로 설치 합니다. 시스템 드라이브 포맷을 수행 하 고 **setup.exe** 를 실행 한 다음 "없음" 옵션을 사용 합니다.  
      설치가 완료 되 고 서버가 다시 시작 된 후 서버 id, 역할, 기능 및 응용 프로그램을 구성 해야 합니다.

   7. 서버에 hyper-v 역할 및 장애 조치 (Failover) 클러스터링 기능을 설치 합니다 (cmdlet을 `Install-WindowsFeature` 사용할 수 있음).

   8. 스토리지 공간 다이렉트와 함께 사용 하기 위해 서버 제조업체에서 승인한 하드웨어의 최신 저장소 및 네트워킹 드라이버를 설치 합니다.

   9. 새로 업그레이드 된 서버에 최신 Windows Server 2019 업데이트가 있는지 확인 합니다.  
      자세한 내용은 [windows 10 및 Windows Server 2019 업데이트 기록](https://support.microsoft.com/help/4464619/windows-10-update-history)을 참조 하세요.
      빌드 번호 (명령 참조 `ver` )는 17763.292 이상 이어야 합니다.

   10. 다음 PowerShell 명령을 사용 하 여 서버를 클러스터에 다시 가입 합니다.

      ```PowerShell
      Add-ClusterNode
      ```

   11. 다음 PowerShell 명령을 사용 하 여 저장소 유지 관리 모드에서 서버를 제거 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   12. 저장소 복구 작업이 완료 될 때까지 기다렸다가 모든 디스크가 정상 상태로 돌아갑니다.  
       서버를 업그레이드 하는 동안 실행 되는 Vm의 수에 따라 상당한 시간이 걸릴 수 있습니다. 실행할 명령은 다음과 같습니다.

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. 클러스터의 다음 서버를 업그레이드 합니다.

5. 모든 서버를 Windows Server 2019로 업그레이드 한 후에는 다음 PowerShell cmdlet을 사용 하 여 클러스터 기능 수준을 업데이트 합니다.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   기술적으로는 가능한 한 빨리 클러스터 기능 수준을 업데이트 하는 것이 좋습니다. 단,이 작업을 수행 하는 데는 최대 4 주가 소요 됩니다.

6. 클러스터 기능 수준이 업데이트 된 후 다음 cmdlet을 사용 하 여 저장소 풀을 업데이트 합니다.  
   이 시점에서와 `Get-ClusterPerf` 같은 새 cmdlet은 클러스터의 모든 서버에서 완전히 작동 합니다.

   ```PowerShell
   Update-StoragePool
   ```

7. 클러스터에서 Vm을 시작 하 고 제대로 작동 하는지 확인 합니다.

8. 필요에 따라 각 vm을 중지 하 고 `Update-VMVersion` cmdlet을 사용 하 여 vm 구성 수준을 업그레이드 한 다음 vm을 다시 시작 합니다.

9. 업그레이드 된 클러스터가 예상 대로 작동 하는지 확인 합니다.  
   역할은 올바르게 장애 조치 (failover) 해야 하며, VM 실시간 마이그레이션이 클러스터에서 사용 되는 경우 Vm이 성공적으로 실시간 마이그레이션됩니다.

10. 클러스터 유효성 검사 (`Test-Cluster`)를 실행 하 고 클러스터 유효성 검사 보고서를 검토 하 여 클러스터의 유효성을 검사 합니다.
