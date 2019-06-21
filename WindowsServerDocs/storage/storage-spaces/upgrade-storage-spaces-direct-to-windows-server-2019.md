---
title: Windows Server 2019에 저장소 공간 다이렉트 클러스터 업그레이드
description: Windows Server 2019-하거나 실행 하는 Vm을 유지 하는 동안 중지 하는 동안 저장소 공간 다이렉트 클러스터를 업그레이드 하는 방법.
author: robhindman
ms.author: robhind
manager: eldenc
ms.date: 03/06/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-spaces
ms.openlocfilehash: 54be649cc1753fe07c94105a31a0b738fb030ee0
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284358"
---
# <a name="upgrade-a-storage-spaces-direct-cluster-to-windows-server-2019"></a>Windows Server 2019에 저장소 공간 다이렉트 클러스터 업그레이드

이 항목에서는 Windows Server 2019 저장소 공간 다이렉트 클러스터를 업그레이드 하는 방법을 설명 합니다. Windows server 2019 사용 하 여 Windows Server 2016에서 저장소 공간 다이렉트 클러스터를 업그레이드 하는 데 4 가지가 합니다 [클러스터 OS 롤링 업그레이드 프로세스](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md) -두 Vm이 실행 되는 유지와 관련 된 및 관련 된 두 개의 모든 Vm을 중지 합니다. 각 방법에는 서로 다른 강점 및 약점, 따라서 조직의 요구에 가장 잘 맞는 하나를 선택 합니다.

- **전체 업그레이드 Vm에서 실행 되는 동안** 클러스터의 각 서버의-이 옵션에 없는 VM 가동 중지 시간이 발생 하지만 저장소 작업이 (미러 복구) 각 서버를 업그레이드 한 후 완료 해야 합니다.

- **Vm에서 실행 되는 동안 정리 OS 설치** 클러스터의 각 서버의-이 옵션에 없는 VM 가동 중지 시간이 발생 하지만 각 서버와 모든 저장소 작업 (미러 복구)을 설정 해야 하 고 각 서버를 업그레이드 한 후 완료 대기 해야 합니다. 해당 앱 및 역할을 다시 합니다.

- **현재 위치 업그레이드 동안 Vm이 중지 됩니다** 클러스터의 각 서버에서-이 옵션에는 VM 가동 중지 시간이 발생 하지만 이므로 더 빠른 저장소 (미러 복구) 작업에 대 한 대기 필요가 없습니다.

- **Vm 중지 되어 있는 동안 정리 OS 설치** 클러스터의 각 서버의-이 옵션에는 VM 가동 중지 시간이 발생 하지만 이므로 더 빠른 저장소 (미러 복구)를 작업에 대 한 대기 필요가 없습니다.

## <a name="prerequisites-and-limitations"></a>필수 구성 요소 및 제한 사항

업그레이드 전에:

- 업그레이드 프로세스 중에 문제가 있는 경우 백업을 사용할 수 있는지 확인 합니다.

- 하드웨어 공급 업체 BIOS, 펌웨어 및 드라이버는 Windows Server 2019에 지 서버에 있는지 확인 합니다.

가지 알아야 할 업그레이드 프로세스를 사용 하 여 몇 가지 제한이 있습니다.

- 를 사용 하려면 저장소 공간 다이렉트를 Windows Server 2019 빌드와 176693.292 이전의 고객은 저장소 공간 다이렉트 및 소프트웨어 정의 네트워킹 기능을 사용 하는 레지스트리 키에 대 한 Microsoft 지원에 문의 해야 합니다. 자세한 내용은 Microsoft 기술 자료를 참조 하세요 [4464776 문서](https://support.microsoft.com/help/4464776/software-defined-data-center-and-software-defined-networking)합니다.

- ReFS 볼륨을 사용 하 여 클러스터를 업그레이드 하는 경우 몇 가지 제한이 있습니다.

- 그러나 업그레이드는 ReFS 볼륨에서 완전히 지원 됩니다, 업그레이드 된 볼륨 이점을 제공 하지 않습니다 ReFS에서 Windows Server 2019의 향상 된 기능입니다. 패리티 미러 가속에 대 한 성능 향상된 등의 이러한 혜택에는 새로 만든 Windows Server 2019 ReFS 볼륨이 필요합니다. 즉, 사용 하 여 새 볼륨을 만드는 것은 `New-Volume` cmdlet 또는 서버 관리자. 다음은 일부 새 볼륨을 가져옵니다 ReFS 향상 된 기능입니다.

    - **지도 로그 바이패스**:만 (저장소 공간 다이렉트) 클러스터 된 시스템에 적용 되 고 독립 실행형 저장소 풀에 적용 되지 않습니다는 ReFS에서 성능 향상 시킵니다.

    - **압축** 다중 복원 력 있는 볼륨에 관련 된 Windows Server 2019 효율성 개선.

- Windows Server 2016 저장소 공간 다이렉트 클러스터 서버를 업그레이드 하기 전에 서버를 저장소 유지 관리 모드로 전환 하는 것이 좋습니다. 자세한 내용은 이벤트 5120 부분을 참조 하세요 [저장소 공간 다이렉트 해결](troubleshooting-storage-spaces.md)합니다. Windows Server 2016에서이 문제를 해결 하지만 모범 사례로 저장소 유지 관리 모드로 업그레이드 하는 동안 각 저장소 공간 다이렉트 서버를 전환 하는 것이 좋습니다.

- SET 스위치를 사용 하는 소프트웨어 정의 네트워킹 환경에 알려진된 문제가 없습니다. 이 문제는 Windows Server 2016 (이전 버전의 운영 체제를 실시간 마이그레이션)를 Windows Server 2019에서 Hyper-v VM으로 실시간 마이그레이션에 포함 됩니다. 성공적으로 실시간 마이그레이션을 위해 live-에서 Windows Server 2019로 마이그레이션 Windows Server 2016 되는 Vm에서 VM 네트워크 설정을 변경 하는 것이 좋습니다. 2019-01 D 핫픽스 롤업 패키지에서 Windows Server 2019에 대 한이 문제는 해결, 즉, 17763.292를 작성 합니다. 자세한 내용은 Microsoft 기술 자료를 참조 하세요 [4476976 문서](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976)합니다.

위의 알려진된 문제로 인해 일부 고객은 새 Windows Server 2019 클러스터를 빌드하고 아래에 설명 된 4 개의 프로세스 중 하나를 사용 하 여 Windows Server 2016 클러스터를 업그레이드 하는 대신 이전 클러스터에서 데이터를 복사를 고려할 수도 있습니다.

## <a name="performing-an-in-place-upgrade-while-vms-are-running"></a>Vm에서 실행 되는 동안 전체 업그레이드를 수행 합니다.

이 옵션에 없는 VM 가동 중지 시간이 발생 하지만 저장소 작업이 (미러 복구) 각 서버를 업그레이드 한 후 완료 해야 합니다. 개별 서버 업그레이드 프로세스 중 순차적으로 다시 시작 됩니다, 있지만 모든 Vm 뿐만 아니라 클러스터의 나머지 서버가 계속 실행 됩니다.

1. 확인을 클러스터의 모든 서버에 최신 Windows 업데이트를 설치 해야 합니다. 자세한 내용은 참조 하세요. [Windows Server 2016 및 Windows 10 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)합니다. 최소 설치 Microsoft 기술 자료 [4487006 문서](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2019 년 2 월 19 년). 빌드 번호 (참조 `ver` 명령) 14393.2828 이상 이어야 합니다.

2. 소프트웨어 정의 네트워킹 집합 스위치를 사용할 경우 관리자 권한 PowerShell 세션을 열고 클러스터의 모든 Vm에서 VM 실시간 마이그레이션 확인 검사를 사용 하지 않도록 설정 하려면 다음 명령을 실행 합니다.

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. 한 번에 하나의 클러스터 서버에서 다음 단계를 수행 합니다.

   1. Hyper-v VM 라이브 마이그레이션을 사용 하 여 업그레이드 하려는 서버 실행 중인 Vm을 이동 합니다.

   2. 다음 PowerShell 명령을 사용 하 여 클러스터 서버를 일시 중지-일부 내부 그룹 숨겨져 있는지 확인 합니다. 이 단계를 기울여 좋습니다-이미 라이브 상태인 하지 않은 경우 Vm을 마이그레이션 해제 서버를 이므로 생략할 수 이전 단계 선호 하는 경우이 cmdlet이 수행 됩니다.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. 다음 PowerShell 명령을 실행 하 여 저장소 유지 관리 모드에서 서버를 배치 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. 있는지 여부를 확인 하려면 다음 cmdlet을 실행 합니다 **OperationalStatus** 가치가 **유지 관리 모드**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   5. 실행 하 여 서버에서 Windows Server 2019 업그레이드 설치를 수행 **setup.exe** "개인 파일 및 앱 유지" 옵션을 사용 합니다. 설치를 완료 한 후 클러스터 및 클러스터에서 서버 유지 시작에 따라 자동으로 서비스를 수행 합니다.

   6. 새로 업그레이드 된 서버에 최신 Windows Server 2019 업데이트가 설치 되었는지 확인 합니다. 자세한 내용은 참조 하세요. [Windows 10 및 Windows Server 2019 기록을 업데이트](https://support.microsoft.com/help/4464619/windows-10-update-history)합니다. 빌드 번호 (참조 `ver` 명령) 17763.292 이상 이어야 합니다.

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

   9. 저장소 복구 작업을 종료 하 고 정상 상태로 반환 하는 모든 디스크를 기다립니다. 서버를 업그레이드 하는 동안 실행 중인 Vm 수에 따라 상당한 시간이 걸릴 수 있습니다. 실행 하는 명령은 다음과 같습니다.

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. 클러스터에서 다음 서버를 업그레이드 합니다.

5. 모든 서버가 Windows Server 2019에 업그레이드 된 후 클러스터 기능 수준을 업데이트 하려면 다음 PowerShell cmdlet을 사용 합니다.

   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > 이렇게 하려면 최대 4 주 동안이 기술적으로 클러스터 기능 수준을 가능한 한 빨리 업데이트 것이 좋습니다.

6. 클러스터 기능 수준을 업데이트 된 후 저장소 풀을 업데이트 하려면 다음 cmdlet을 사용 합니다. 에이 지점 같은 새 cmdlet `Get-ClusterPerf` 클러스터의 모든 서버에서 완벽 하 게 작동 됩니다.

   ```PowerShell
   Update-StoragePool
   ```

7. 필요에 따라 각 VM을 중지 하 여 VM 구성 수준을 업그레이드를 사용 하 여를 `Update-VMVersion` cmdlet을 다음 Vm을 다시 시작 합니다.

8. SET 스위치를 사용 하 여 소프트웨어 정의 네트워킹 사용 중인 사용 하는 경우 사용할 수 없는 VM의 실시간 마이그레이션 검사를 위에 설명 된 대로 다음 cmdlet을 다시 VM Live 확인 검사를 사용 하도록 설정 하려면:

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter  SkipMigrationDestinationCheck -Value 0
   ```

9. 클러스터가 업그레이드 예상 대로 작동 하는지 확인 합니다. 역할은 장애 조치 올바르게 및 실시간 마이그레이션 VM 클러스터에서 사용 하는 경우 Vm은 성공적으로 마이그레이션합니다.

10. 클러스터 유효성 검사를 실행 하 여 클러스터 유효성 검사 (`Test-Cluster`) 및 클러스터 유효성 검사 보고서를 검사 합니다.

## <a name="performing-a-clean-os-installation-while-vms-are-running"></a>Vm에서 실행 되는 동안 정리 OS 설치를 수행 합니다.

이 옵션에 없는 VM 가동 중지 시간이 발생 하지만 저장소 작업이 (미러 복구) 각 서버를 업그레이드 한 후 완료 해야 합니다. 개별 서버 업그레이드 프로세스 중 순차적으로 다시 시작 됩니다, 있지만 모든 Vm 뿐만 아니라 클러스터의 나머지 서버가 계속 실행 됩니다.

1. 클러스터의 모든 서버에 최신 업데이트가 실행 되 고 있는지 확인 합니다. 자세한 내용은 참조 하세요. [Windows Server 2016 및 Windows 10 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)합니다. 최소 설치 Microsoft 기술 자료 [4487006 문서](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2019 년 2 월 19 년). 빌드 번호 (참조 `ver` 명령) 14393.2828 이상 이어야 합니다.

2. 소프트웨어 정의 네트워킹 집합 스위치를 사용할 경우 관리자 권한 PowerShell 세션을 열고 클러스터의 모든 Vm에서 VM 실시간 마이그레이션 확인 검사를 사용 하지 않도록 설정 하려면 다음 명령을 실행 합니다.

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" |
   Set-ClusterParameter -Create SkipMigrationDestinationCheck -Value 1
   ```

3. 한 번에 하나의 클러스터 서버에서 다음 단계를 수행 합니다.

   1. Hyper-v VM 라이브 마이그레이션을 사용 하 여 업그레이드 하려는 서버 실행 중인 Vm을 이동 합니다.

   2. 다음 PowerShell 명령을 사용 하 여 클러스터 서버를 일시 중지-일부 내부 그룹 숨겨져 있는지 확인 합니다. 이 단계를 기울여 좋습니다-이미 라이브 상태인 하지 않은 경우 Vm을 마이그레이션 해제 서버를 이므로 생략할 수 이전 단계 선호 하는 경우이 cmdlet이 수행 됩니다.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   3. 다음 PowerShell 명령을 실행 하 여 저장소 유지 관리 모드에서 서버를 배치 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   4. 있는지 여부를 확인 하려면 다음 cmdlet을 실행 합니다 **OperationalStatus** 가치가 **유지 관리 모드**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   3.  다음 PowerShell 명령을 실행 하 여 클러스터에서 서버를 제거 합니다.  

       ```PowerShell
       Remove-ClusterNode <ServerName>
       ```

   4. 서버에서 Windows Server 2019 새로 설치를 수행: 실행 되는 형식 시스템 드라이브 **setup.exe** "Nothing"를 사용 하 여 옵션입니다. 구성 서버 id, 역할, 기능 및 설치가 완료 된 후 응용 프로그램 및 서버 다시 시작 해야 합니다.

   5. 서버에 Hyper-v 역할 및 장애 조치 클러스터링 기능 설치 (사용할 수는 `Install-WindowsFeature` cmdlet).

   6. 최신 저장소 및 네트워킹 하드웨어의 드라이버를 사용 하 여 저장소 공간 다이렉트를 사용 하 여에 대 한 서버 제조업체에서 승인 된 설치 합니다.

   7. 새로 업그레이드 된 서버에 최신 Windows Server 2019 업데이트가 설치 되었는지 확인 합니다. 자세한 내용은 참조 하세요. [Windows 10 및 Windows Server 2019 기록을 업데이트](https://support.microsoft.com/help/4464619/windows-10-update-history)합니다. 빌드 번호 (참조 `ver` 명령) 17763.292 이상 이어야 합니다.

   8. 다음 PowerShell 명령을 사용 하 여 클러스터에 서버에 다시 가입:

       ```PowerShell
       Add-ClusterNode
       ```

   9. 다음 PowerShell 명령을 사용 하 여 저장소 유지 관리 모드에서 서버를 제거 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   10. 저장소 복구 작업을 종료 하 고 정상 상태로 반환 하는 모든 디스크를 기다립니다. 서버를 업그레이드 하는 동안 실행 중인 Vm 수에 따라 상당한 시간이 걸릴 수 있습니다. 실행 하는 명령은 다음과 같습니다.

        ```PowerShell
        Get-StorageJob
        Get-VirtualDisk
        ```

4. 클러스터에서 다음 서버를 업그레이드 합니다.

5. 모든 서버가 Windows Server 2019에 업그레이드 된 후 클러스터 기능 수준을 업데이트 하려면 다음 PowerShell cmdlet을 사용 합니다.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   > 이렇게 하려면 최대 4 주 동안이 기술적으로 클러스터 기능 수준을 가능한 한 빨리 업데이트 것이 좋습니다.

6. 클러스터 기능 수준을 업데이트 된 후 저장소 풀을 업데이트 하려면 다음 cmdlet을 사용 합니다. 에이 지점 같은 새 cmdlet `Get-ClusterPerf` 클러스터의 모든 서버에서 완벽 하 게 작동 됩니다.

   ```PowerShell
   Update-StoragePool
   ```

7. 필요에 따라 각 VM을 중지 하 고 사용 하 여 VM 구성 수준을 업그레이드를 `Update-VMVersion` cmdlet 및 다음 Vm을 다시 시작 합니다.

8. SET 스위치를 사용 하 여 소프트웨어 정의 네트워킹 사용 중인 사용 하는 경우 사용할 수 없는 VM의 실시간 마이그레이션 검사를 위에 설명 된 대로 다음 cmdlet을 다시 VM Live 확인 검사를 사용 하도록 설정 하려면:

   ```PowerShell
   Get-ClusterResourceType -Cluster {clusterName} -Name "Virtual Machine" | 
   Set-ClusterParameter SkipMigrationDestinationCheck -Value 0
   ```

9. 클러스터가 업그레이드 예상 대로 작동 하는지 확인 합니다. 역할은 장애 조치 올바르게 및 실시간 마이그레이션 VM 클러스터에서 사용 하는 경우 Vm은 성공적으로 마이그레이션합니다.

10. 클러스터 유효성 검사를 실행 하 여 클러스터 유효성 검사 (`Test-Cluster`) 및 클러스터 유효성 검사 보고서를 검사 합니다.

## <a name="performing-an-in-place-upgrade-while-vms-are-stopped"></a>Vm이 중지 되는 동안 전체 업그레이드를 수행 합니다.

이 옵션은 VM 가동 중지 시간이 발생 하지만 저장소 작업 (미러 복구)을 각 서버를 업그레이드 한 후 완료 될 때까지 기다릴 필요가 없기 때문에 업그레이드 하는 동안 실행 되는 Vm을 유지 하는 경우 보다 적은 시간이 걸릴 수 있습니다. 개별 서버 업그레이드 프로세스 중 순차적으로 다시 시작 됩니다, 있지만 클러스터의 나머지 서버가 계속 실행 됩니다.

1. 클러스터의 모든 서버에 최신 업데이트가 실행 되 고 있는지 확인 합니다. 자세한 내용은 참조 하세요. [Windows Server 2016 및 Windows 10 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)합니다. 최소 설치 Microsoft 기술 자료 [4487006 문서](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2019 년 2 월 19 년). 빌드 번호 (참조 `ver` 명령) 14393.2828 이상 이어야 합니다.

2. 클러스터에서 실행 되는 Vm을 중지 합니다.

3. 한 번에 하나의 클러스터 서버에서 다음 단계를 수행 합니다.

   1. 다음 PowerShell 명령을 사용 하 여 클러스터 서버를 일시 중지-일부 내부 그룹 숨겨져 있는지 확인 합니다. 이 단계를를 기울여 사용 하는 것이 좋습니다.

        ```PowerShell
       Suspend-ClusterNode -Drain
       ```

   2. 다음 PowerShell 명령을 실행 하 여 저장소 유지 관리 모드에서 서버를 배치 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Enable-StorageMaintenanceMode
       ```

   3. 있는지 여부를 확인 하려면 다음 cmdlet을 실행 합니다 **OperationalStatus** 가치가 **유지 관리 모드**:

       ```PowerShell
       Get-PhysicalDisk
       ```

   4. 실행 하 여 서버에서 Windows Server 2019 업그레이드 설치를 수행 **setup.exe** "개인 파일 및 앱 유지" 옵션을 사용 합니다.  
   설치를 완료 한 후 클러스터 및 클러스터에서 서버 유지 시작에 따라 자동으로 서비스를 수행 합니다.

   5.  새로 업그레이드 된 서버에 최신 Windows Server 2019 업데이트가 설치 되었는지 확인 합니다.  
   자세한 내용은 참조 하세요. [Windows 10 및 Windows Server 2019 기록을 업데이트](https://support.microsoft.com/help/4464619/windows-10-update-history)합니다.
   빌드 번호 (참조 `ver` 명령) 17763.292 이상 이어야 합니다.

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

   8.  저장소 복구 작업을 종료 하 고 정상 상태로 반환 하는 모든 디스크를 기다립니다.  
   이 Vm을 실행 하지 않는 하므로 비교적 빠른 이어야 합니다. 실행 하는 명령은 다음과 같습니다.

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. 클러스터에서 다음 서버를 업그레이드 합니다.
5. 모든 서버가 Windows Server 2019에 업그레이드 된 후 클러스터 기능 수준을 업데이트 하려면 다음 PowerShell cmdlet을 사용 합니다.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   이렇게 하려면 최대 4 주 동안이 기술적으로 클러스터 기능 수준을 가능한 한 빨리 업데이트 것이 좋습니다.

6. 클러스터 기능 수준을 업데이트 된 후 저장소 풀을 업데이트 하려면 다음 cmdlet을 사용 합니다.  
   에이 지점 같은 새 cmdlet `Get-ClusterPerf` 클러스터의 모든 서버에서 완벽 하 게 작동 됩니다.

   ```PowerShell
   Update-StoragePool
   ```

7. 클러스터에서 Vm을 시작 하 고 제대로 작동 하 고 확인 합니다.

8. 필요에 따라 각 VM을 중지 하 고 사용 하 여 VM 구성 수준을 업그레이드를 `Update-VMVersion` cmdlet 및 다음 Vm을 다시 시작 합니다.

9. 클러스터가 업그레이드 예상 대로 작동 하는지 확인 합니다.  
   역할은 장애 조치 올바르게 및 실시간 마이그레이션 VM 클러스터에서 사용 하는 경우 Vm은 성공적으로 마이그레이션합니다.

10. 클러스터 유효성 검사를 실행 하 여 클러스터 유효성 검사 (`Test-Cluster`) 및 클러스터 유효성 검사 보고서를 검사 합니다.

## <a name="performing-a-clean-os-installation-while-vms-are-stopped"></a>Vm 중지 되어 있는 동안 정리 OS 설치를 수행 합니다.

이 옵션은 VM 가동 중지 시간이 발생 하지만 저장소 작업 (미러 복구)을 각 서버를 업그레이드 한 후 완료 될 때까지 기다릴 필요가 없기 때문에 업그레이드 하는 동안 실행 되는 Vm을 유지 하는 경우 보다 적은 시간이 걸릴 수 있습니다. 개별 서버 업그레이드 프로세스 중 순차적으로 다시 시작 됩니다, 있지만 클러스터의 나머지 서버가 계속 실행 됩니다.

1. 클러스터의 모든 서버에 최신 업데이트가 실행 되 고 있는지 확인 합니다.  
   자세한 내용은 참조 하세요. [Windows Server 2016 및 Windows 10 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)합니다.
   최소 설치 Microsoft 기술 자료 [4487006 문서](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) (2019 년 2 월 19 년). 빌드 번호 (참조 `ver` 명령) 14393.2828 이상 이어야 합니다.

2. 클러스터에서 실행 되는 Vm을 중지 합니다.

3. 한 번에 하나의 클러스터 서버에서 다음 단계를 수행 합니다.

   2. 다음 PowerShell 명령을 사용 하 여 클러스터 서버를 일시 중지-일부 내부 그룹 숨겨져 있는지 확인 합니다.  
      이 단계를를 기울여 사용 하는 것이 좋습니다.

       ```PowerShell
      Suspend-ClusterNode -Drain
      ```

   3. 다음 PowerShell 명령을 실행 하 여 저장소 유지 관리 모드에서 서버를 배치 합니다.

      ```PowerShell
      Get-StorageFaultDomain -type StorageScaleUnit | 
      Where FriendlyName -Eq <ServerName> | 
      Enable-StorageMaintenanceMode
      ```

   4. 있는지 여부를 확인 하려면 다음 cmdlet을 실행 합니다 **OperationalStatus** 가치가 **유지 관리 모드**:

      ```PowerShell
      Get-PhysicalDisk
      ```

   5. 다음 PowerShell 명령을 실행 하 여 클러스터에서 서버를 제거 합니다.  
    
      ```PowerShell
      Remove-ClusterNode <ServerName>
      ```

   6. 서버에서 Windows Server 2019 새로 설치를 수행: 실행 되는 형식 시스템 드라이브 **setup.exe** "Nothing"를 사용 하 여 옵션입니다.  
      구성 서버 id, 역할, 기능 및 설치가 완료 된 후 응용 프로그램 및 서버 다시 시작 해야 합니다.

   7. 서버에 Hyper-v 역할 및 장애 조치 클러스터링 기능 설치 (사용할 수는 `Install-WindowsFeature` cmdlet).

   8. 최신 저장소 및 네트워킹 하드웨어의 드라이버를 사용 하 여 저장소 공간 다이렉트를 사용 하 여에 대 한 서버 제조업체에서 승인 된 설치 합니다.

   9. 새로 업그레이드 된 서버에 최신 Windows Server 2019 업데이트가 설치 되었는지 확인 합니다.  
      자세한 내용은 참조 하세요. [Windows 10 및 Windows Server 2019 기록을 업데이트](https://support.microsoft.com/help/4464619/windows-10-update-history)합니다.
      빌드 번호 (참조 `ver` 명령) 17763.292 이상 이어야 합니다.

   10. 다음 PowerShell 명령을 사용 하 여 클러스터에 서버에 다시 가입:

      ```PowerShell
      Add-ClusterNode
      ```

   11. 다음 PowerShell 명령을 사용 하 여 저장소 유지 관리 모드에서 서버를 제거 합니다.

       ```PowerShell
       Get-StorageFaultDomain -type StorageScaleUnit | 
       Where FriendlyName -Eq <ServerName> | 
       Disable-StorageMaintenanceMode
       ```

   12. 저장소 복구 작업을 종료 하 고 정상 상태로 반환 하는 모든 디스크를 기다립니다.  
       서버를 업그레이드 하는 동안 실행 중인 Vm 수에 따라 상당한 시간이 걸릴 수 있습니다. 실행 하는 명령은 다음과 같습니다.

       ```PowerShell
       Get-StorageJob
       Get-VirtualDisk
       ```

4. 클러스터에서 다음 서버를 업그레이드 합니다.

5. 모든 서버가 Windows Server 2019에 업그레이드 된 후 클러스터 기능 수준을 업데이트 하려면 다음 PowerShell cmdlet을 사용 합니다.
    
   ```PowerShell
   Update-ClusterFunctionalLevel
   ```

   > [!NOTE]
   >   이렇게 하려면 최대 4 주 동안이 기술적으로 클러스터 기능 수준을 가능한 한 빨리 업데이트 것이 좋습니다.

6. 클러스터 기능 수준을 업데이트 된 후 저장소 풀을 업데이트 하려면 다음 cmdlet을 사용 합니다.  
   에이 지점 같은 새 cmdlet `Get-ClusterPerf` 클러스터의 모든 서버에서 완벽 하 게 작동 됩니다.

   ```PowerShell
   Update-StoragePool
   ```

7. 클러스터에서 Vm을 시작 하 고 제대로 작동 하 고 확인 합니다.

8. 필요에 따라 각 VM을 중지 하 고 사용 하 여 VM 구성 수준을 업그레이드를 `Update-VMVersion` cmdlet 및 다음 Vm을 다시 시작 합니다.

9. 클러스터가 업그레이드 예상 대로 작동 하는지 확인 합니다.  
   역할은 장애 조치 올바르게 및 실시간 마이그레이션 VM 클러스터에서 사용 하는 경우 Vm은 성공적으로 마이그레이션합니다.

10. 클러스터 유효성 검사를 실행 하 여 클러스터 유효성 검사 (`Test-Cluster`) 및 클러스터 유효성 검사 보고서를 검사 합니다.
