---
title: 스토리지 복제본에 대한 질문과 대답
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/15/2020
ms.assetid: 12bc8e11-d63c-4aef-8129-f92324b2bf1b
ms.openlocfilehash: 9978fd3e926ade4680ca6563d9d39b0851d893e9
ms.sourcegitcommit: 568b924d32421256f64abfee171304f1daf320d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85070486"
---
# <a name="frequently-asked-questions-about-storage-replica"></a>스토리지 복제본에 대한 질문과 대답

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

이 항목에서는 스토리지 복제본에 대한 FAQ(자주 묻는 질문)의 답변을 제공합니다.

## <a name="is-storage-replica-supported-on-azure"></a><a name="FAQ1"></a>Azure에서 저장소 복제본이 지원 되나요?
예. Azure에서 다음 시나리오를 사용할 수 있습니다.

1. Azure 내에서 서버 간 복제 (하나 또는 두 개의 데이터 센터 장애 도메인의 IaaS Vm 간에 동기식 또는 비동기적으로 또는 두 개의 별도 지역 간에 비동기적으로 또는 비동기적으로)
2. Azure와 온-프레미스 간의 서버 간 비동기 복제 (VPN 또는 Azure Express 경로 사용)
3. Azure 내에서 클러스터 간 복제 (하나 또는 두 개의 데이터 센터 장애 도메인의 IaaS Vm 간에 동기식 또는 비동기적으로 또는 두 개의 별도 지역 간에 비동기적으로 또는 비동기적으로)
4. Azure와 온-프레미스 간의 클러스터 간 비동기 복제 (VPN 또는 Azure Express 경로 사용)

Azure의 게스트 클러스터링에 대 한 추가 정보는 [Microsoft Azure의 IAAS VM 게스트 클러스터 배포](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126)에서 찾을 수 있습니다.

중요:

1. Azure는 공유 VHDX 게스트 클러스터링을 지원 하지 않으므로 Windows 장애 조치 (Failover) 클러스터 가상 머신은 클래식 공유 저장소 영구 디스크 예약 클러스터링 또는 스토리지 공간 다이렉트에 대해 iSCSI 대상을 사용 해야 합니다.
2. [Azure 지역에서 재해 복구를 위해 저장소 복제본을 사용 하 여 스토리지 공간 다이렉트 SOFS 클러스터를 만드는](https://aka.ms/azure-storage-replica-cluster)스토리지 공간 다이렉트 기반 저장소 복제본 클러스터링에 대 한 템플릿이 Azure Resource Manager 있습니다.  
3. 클러스터에서 클러스터로의 RPC 통신을 클러스터링 하는 클러스터는 CNO에 대 한 네트워크 액세스를 구성 해야 합니다. Tcp 포트 135 및 TCP 포트 49152 위의 동적 범위를 허용 해야 합니다. [AZURE IAAS VM에서 Windows Server 장애 조치 (Failover) 클러스터 빌드-2 부 네트워크 및 만들기](https://blogs.technet.microsoft.com/askcore/2015/06/24/building-windows-server-failover-cluster-on-azure-iaas-vm-part-2-network-and-creation/)를 참조 하세요.  
4. 각 노드에서 저장소 복제본에 의해 복제 되는 비대칭 클러스터에 대해 루프백 iSCSI를 사용 하는 2 노드 게스트 클러스터를 사용할 수 있습니다. 그러나이로 인해 성능이 매우 저하 될 수 있으며, 매우 제한적인 작업 또는 테스트에만 사용 해야 합니다.  

## <a name="how-do-i-see-the-progress-of-replication-during-initial-sync"></a><a name="FAQ2"></a>초기 동기화 중에 복제 진행률이 표시 어떻게 할까요??  
대상 서버의 스토리지 복제본 관리 이벤트 로그에 표시되는 이벤트 1237 메시지에 복사된 바이트 수와 남은 바이트 수가 10초마다 표시됩니다. 대상에서 하나 이상의 복제된 볼륨에 대한 **\Storage Replica Statistics\Total Bytes Received**를 표시하는 스토리지 복제본 성능 카운터를 사용할 수도 있습니다. 또한 Windows PowerShell을 사용하여 복제 그룹을 쿼리할 수 있습니다. 예를 들어 다음 샘플 명령은 대상에 있는 그룹의 이름을 가져온 다음 10초마다 **Replication 2**라는 하나의 그룹을 쿼리하여 진행률을 표시합니다.  

```  
Get-SRGroup

do{
    $r=(Get-SRGroup -Name "Replication 2").replicas
    [System.Console]::Write("Number of remaining bytes {0}`n", $r.NumOfBytesRemaining)
    Start-Sleep 10
}until($r.ReplicationStatus -eq 'ContinuouslyReplicating')
Write-Output "Replica Status: "$r.replicationstatus

```  

## <a name="can-i-specify-specific-network-interfaces-to-be-used-for-replication"></a><a name="FAQ3"></a>복제에 사용할 특정 네트워크 인터페이스를 지정할 수 있습니까?  

예. `Set-SRNetworkConstraint`를 사용하면 됩니다. 이 cmdlet은 인터페이스 계층에서 작동하며, 클러스터 및 비 클러스터 시나리오 모두에서 사용됩니다.  
예를 들어 독립 실행형 서버(각 노드)를 사용하는 경우 다음을 실행합니다.  

```  
Get-SRPartnership  

Get-NetIPConfiguration  
```  
게이트웨이 및 인터페이스 정보(두 서버 모두에서)와 파트너 관계 방향을 확인합니다. 다음을 실행합니다.  

```  
Set-SRNetworkConstraint -SourceComputerName sr-srv06 -SourceRGName rg02 -  
SourceNWInterface 2 -DestinationComputerName sr-srv05 -DestinationNWInterface 3 -DestinationRGName rg01  

Get-SRNetworkConstraint  

Update-SmbMultichannelConnection  

```  

확장 클러스터에 대한 네트워크 제약 조건을 구성하려면 다음을 실행합니다.  

    Set-SRNetworkConstraint -SourceComputerName sr-cluster01 -SourceRGName group1 -SourceNWInterface "Cluster Network 1","Cluster Network 2" -DestinationComputerName sr-cluster02 -DestinationRGName group2 -DestinationNWInterface "Cluster Network 1","Cluster Network 2"

## <a name="can-i-configure-one-to-many-replication-or-transitive-a-to-b-to-c-replication"></a><a name="FAQ4"></a>일대다 복제 또는 전이적 (A-B에서 C로) 복제를 구성할 수 있나요?  
아니요. 저장소 복제본은 서버, 클러스터 또는 스트레치 클러스터 노드의 일대일 복제만 지원 합니다. 이는 이후 릴리스에서 변경될 수 있습니다. 물론, 특정 볼륨 쌍의 다양한 서버 간에 어떤 방향으로든 복제를 구성할 수 있습니다. 예를 들어, 서버 1은 해당 D 볼륨을 서버 2에 복제할 수 있으며, 서버 3으로부터 E 볼륨을 복제할 수 있습니다.

## <a name="can-i-grow-or-shrink-replicated-volumes-replicated-by-storage-replica"></a><a name="FAQ5"></a>저장소 복제본에 의해 복제 된 복제 된 볼륨을 늘리거나 줄일 수 있나요?  
볼륨을 확장 (확장) 할 수 있지만 축소할 수는 없습니다. 기본적으로 저장소 복제본은 관리자가 복제 된 볼륨을 확장 하지 못하도록 합니다. `Set-SRGroup -AllowVolumeResize $TRUE`크기를 조정 하기 전에 원본 그룹에서 옵션을 사용 합니다. 다음은 그 예입니다.

1. 원본 컴퓨터에 대해 사용:`Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. 선호 하는 모든 기술을 사용 하 여 볼륨 증가
3. 원본 컴퓨터에 대해 사용:`Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE` 

## <a name="can-i-bring-a-destination-volume-online-for-read-only-access"></a><a name="FAQ6"></a>읽기 전용 액세스를 위해 대상 볼륨을 온라인 상태로 전환할 수 있습니까?  
Windows Server 2016에서는 불가능합니다. 복제를 시작할 때 저장소 복제본이 대상 볼륨을 분리 합니다. 

그러나 Windows Server 2019 및 Windows Server 반기 채널에서 1709 버전부터 시작 하 여 대상 저장소를 탑재 하는 옵션을 사용할 수 있습니다 .이 기능을 "테스트 장애 조치 (Failover)" 라고 합니다. 이렇게 하려면 대상에서 현재 복제 하 고 있지 않은 사용 하지 않는 NTFS 또는 ReFS 형식의 볼륨이 있어야 합니다. 그런 다음 테스트 또는 백업을 위해 복제 된 저장소의 스냅숏을 일시적으로 탑재할 수 있습니다. 

예를 들어 대상 서버 "SRV2"의 복제 그룹 "RG2"에서 볼륨 "D:"를 복제 하 고 복제 되지 않는 SRV2에 "T:" 드라이브가 있는 테스트 장애 조치 (failover)를 만들려면 다음을 수행 합니다.

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`
 
이제 SRV2에서 복제 된 볼륨 D:에 액세스할 수 있습니다. D: 경로 아래에서이를 읽고, 파일을 복사 하거나, 보관을 위해 다른 위치에 저장 하는 온라인 백업을 실행할 수 있습니다. T: 볼륨에는 로그 데이터만 포함 됩니다.

테스트 장애 조치 (failover) 스냅숏을 제거 하 고 변경 내용을 취소 하려면:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`
 
단기 임시 작업에 대해서만 테스트 장애 조치 (failover) 기능을 사용 해야 합니다. 장기적으로 사용 하기 위한 것은 아닙니다. 사용 하는 경우 복제는 실제 대상 볼륨으로 계속 됩니다. 

## <a name="can-i-configure-scale-out-file-server-sofs-in-a-stretch-cluster"></a><a name="FAQ7"></a>스트레치 클러스터에서 SOFS (스케일 아웃 파일 서버)을 구성할 수 있나요?  
기술적으로는 가능 하지만 SOFS에 연결 하는 계산 노드에서 사이트 인식이 부족 하기 때문에이 구성은 권장 되지 않습니다. 일반적으로 대기 시간이 하위 밀리초 인 캠퍼스 거리 네트워킹을 사용 하는 경우이 구성은 일반적으로 문제 없이 작동 합니다.   

클러스터 간 복제를 구성하는 경우 스토리지 복제본은 두 클러스터 간에 복제할 때 스토리지 공간 다이렉트 사용을 포함하여 스케일 아웃 파일 서버를 완전히 지원합니다.  

## <a name="is-csv-required-to-replicate-in-a-stretch-cluster-or-between-clusters"></a><a name="FAQ7.5"></a>CSV가 스트레치 클러스터 또는 클러스터 간에 복제 하는 데 필요 한가요?  
아니요. 파일 서버 역할과 같은 클러스터 리소스가 소유 하는 CSV 또는 PDR (영구 디스크 예약)를 사용 하 여 복제할 수 있습니다. 

클러스터 간 복제를 구성하는 경우 스토리지 복제본은 두 클러스터 간에 복제할 때 스토리지 공간 다이렉트 사용을 포함하여 스케일 아웃 파일 서버를 완전히 지원합니다.  

## <a name="can-i-configure-storage-spaces-direct-in-a-stretch-cluster-with-storage-replica"></a><a name="FAQ8"></a>스토리지 복제본을 사용하여 확장 클러스터에서 스토리지 공간 다이렉트를 구성할 수 있습니까?  
이는 Windows Server에서 지원 되는 구성이 아닙니다. 이는 이후 릴리스에서 변경될 수 있습니다. 클러스터 간 복제를 구성하는 경우 스토리지 복제본은 스토리지 공간 다이렉트 사용을 포함하여 스케일 아웃 파일 서버 및 Hyper-V 서버를 완전히 지원합니다.  

## <a name="how-do-i-configure-asynchronous-replication"></a><a name="FAQ9"></a>비동기 복제를 구성하려면 어떻게 해야 합니까?  

`New-SRPartnership -ReplicationMode`를 지정하고 **Asynchronous** 인수를 제공합니다. 기본적으로 스토리지 복제본의 모든 복제는 동기식입니다. `Set-SRPartnership -ReplicationMode`를 사용하여 모드를 변경할 수도 있습니다.  

## <a name="how-do-i-prevent-automatic-failover-of-a-stretch-cluster"></a><a name="FAQ10"></a>확장 클러스터의 자동 장애 조치(failover)를 방지하려면 어떻게 해야 합니까?  
자동 장애 조치(failover)를 방지하려면 PowerShell을 사용하여 `Get-ClusterNode -Name "NodeName").NodeWeight=0`을 구성하면 됩니다. 그러면 재해 복구 사이트에서 각 노드에 대한 응답이 제거됩니다. 그런 다음 기본 사이트의 노드에서 `Start-ClusterNode -PreventQuorum`을 사용하고 재해 사이트의 노드에서 `Start-ClusterNode -ForceQuorum`을 사용하여 장애 조치(failover)를 강제 적용할 수 있습니다. 자동 장애 조치(failover)를 방지하는 그래픽 옵션은 없으며, 자동 장애 조치(failover) 방지는 권장되지 않습니다.  

## <a name="how-do-i-disable-virtual-machine-resiliency"></a><a name="FAQ11"></a>가상 머신 복원력을 사용하지 않도록 설정하려면 어떻게 해야 하나요?
새 Hyper-v 가상 컴퓨터 복원 기능이 실행 되지 않도록 하 여 재해 복구 사이트로 장애 조치 (failover) 하는 대신 가상 컴퓨터를 일시 중지 하려면 다음을 실행 합니다.`(Get-Cluster).ResiliencyDefaultPeriod=0`  

## <a name="how-can-i-reduce-time-for-initial-synchronization"></a><a name="FAQ12"></a>초기 동기화에 대 한 시간을 줄이려면 어떻게 해야 하나요?

씬 프로비전된 스토리지를 사용하여 초기 동기화 속도를 높이는 것이 한 가지 방법입니다. 스토리지 복제본은 클러스터되지 않은 스토리지 공간, Hyper-V 동적 디스크 및 SAN LUN을 포함하여 씬 프로비전된 스토리지를 쿼리하고 자동으로 사용합니다.  

또한 시드 된 데이터 볼륨을 사용 하 여 대상 볼륨에 주 복제본의 일부 데이터 하위 집합이 있는지 확인 한 다음 장애 조치(Failover) 클러스터 관리자 또는에서 시드 된 옵션을 사용 하 여 대역폭 사용량을 줄일 수 있습니다 `New-SRPartnership` . 볼륨이 대개 비어 있는 경우 시드된 동기화를 사용하여 시간 및 대역폭 사용을 줄일 수 있습니다. 다양 한 효율성를 사용 하 여 데이터 초기값을 위한 여러 가지 방법이 있습니다.

1. 이전 복제-디스크 및 볼륨을 포함 하는 노드 간에 로컬로 일반 초기 동기화를 사용 하 여 복제 하 고, 복제를 제거 하 고 대상 디스크를 다른 곳에 전달한 다음, 시드 옵션을 사용 하 여 복제를 추가 저장소 복제본이 블록 복사 미러를 보장 하 고 복제 하는 유일한 작업은 델타 블록 이기 때문에 가장 효과적인 방법입니다.
2. 스냅숏 또는 복원 된 스냅숏 기반 백업을 복원 했습니다. 볼륨 기반 스냅숏을 대상 볼륨으로 복원 하 여 블록 레이아웃에는 최소한의 차이가 있습니다. 블록은 미러 이미지가 되는 볼륨 스냅숏에 감사 하는 것이 가장 효과적인 다음 방법입니다.
3. 복사 된 파일-이전에 사용 된 적이 없는 새 볼륨을 만들어 데이터의 전체 robocopy/MIR 트리 복사본을 만든 후에는 블록 일치가 발생할 수 있습니다. Windows 파일 탐색기를 사용 하거나 트리의 일부를 복사 하면 많은 블록 일치 항목이 생성 되지 않습니다. 수동으로 파일을 복사 하는 것은 시드의 가장 효과적인 방법입니다.

## <a name="can-i-delegate-users-to-administer-replication"></a><a name="FAQ13"></a>사용자를 위임 하 여 복제를 관리할 수 있나요?  

Cmdlet을 사용할 수 있습니다 `Grant-SRDelegation` . 로컬 관리자 그룹의 구성원이 아니더라도 복제를 만들거나 수정하거나 제거할 수 있는 권한이 있으므로 서버 간, 클러스터 간 및 확장 클러스터 복제 시나리오에서 특정 사용자를 설정할 수 있습니다. 다음은 그 예입니다.  

    Grant-SRDelegation -UserName contso\tonywang  

이 cmdlet은 사용자가 관리하려는 서버에서 로그오프했다가 다시 로그온해야 변경 내용이 적용됨을 알립니다. `Get-SRDelegation` 및 `Revoke-SRDelegation`을 사용하여 추가로 제어할 수 있습니다.  

## <a name="what-are-my-backup-and-restore-options-for-replicated-volumes"></a><a name="FAQ13"></a>복제 된 볼륨에 대 한 백업 및 복원 옵션은 무엇 인가요?
스토리지 복제본은 원본 볼륨의 백업 및 복원을 지원합니다. 또한 원본 볼륨의 스냅샷 만들기 및 복원도 지원합니다. 스토리지 복제본으로 보호되는 대상 볼륨은 탑재되지도 않고 액세스할 수도 없으므로 백업하거나 복원할 수 없습니다. 원본 볼륨이 손실된 재해가 발생한 경우 `Set-SRPartnership`을 사용하여 이전 대상 볼륨을 읽기/쓰기 가능한 원본이 되도록 승격하면 이 볼륨을 백업하거나 복원할 수 있습니다. `Remove-SRPartnership` 및 `Remove-SRGroup`으로 복제를 제거하여 해당 볼륨을 읽기/쓰기 가능하도록 다시 탑재할 수도 있습니다.
주기적인 애플리케이션 일치 스냅샷을 만들려면 원본 서버에서 VSSADMIN.EXE를 사용하여 복제된 데이터 볼륨의 스냅샷을 만들면 됩니다. 예를 들어 스토리지 복제본으로 F: 볼륨을 복제하는 경우 다음을 실행합니다.

    vssadmin create shadow /for=F:
그런 다음 복제 방향을 전환하거나 복제를 제거하거나 단순히 동일한 원본 볼륨에 계속 있는 경우 모든 스냅샷을 특정 시점으로 복원할 수 있습니다. 예를 들어 여전히 F:를 사용하는 경우 다음을 실행합니다.

    vssadmin list shadows
     vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
예약된 작업을 정기적으로 실행하도록 이 도구를 예약할 수도 있습니다. VSS 사용에 대한 자세한 내용은 [Vssadmin](../../administration/windows-commands/vssadmin.md)을 검토하세요. 로그 볼륨은 백업할 필요가 없습니다. 이 작업은 VSS에서 무시됩니다.
Windows Server 백업, Microsoft Azure Backup, Microsoft DPM 또는 다른 스냅샷, VSS, 가상 머신 또는 파일 기반 기술은 볼륨 계층 내에서 사용되는 경우 스토리지 복제본에서 지원됩니다. 스토리지 복제본은 블록 기반 백업 및 복원을 지원하지 않습니다.

## <a name="can-i-configure-replication-to-restrict-bandwidth-usage"></a><a name="FAQ14"></a>대역폭 사용량을 제한 하도록 복제를 구성할 수 있나요?
예, SMB 대역폭 제한을 사용하면 됩니다. 이는 모든 스토리지 복제본 트래픽에 적용되는 전역 설정이므로 이 서버의 모든 복제에 영향을 줍니다. 일반적으로 이는 모든 볼륨 데이터를 전송해야 하는 스토리지 복제본 초기 동기화 설정에만 필요합니다. 초기 동기화 후에 필요한 경우 네트워크 대역폭이 너무 낮아 IO 워크로드에 사용할 수 없으면 IO를 줄이거나 대역폭을 늘립니다.

이는 비동기 복제에만 사용해야 합니다(참고: 초기 동기화는 동기식을 지정한 경우에도 항상 비동기식임).
또한 네트워크 QoS 정책을 사용하여 스토리지 복제본 트래픽을 구성할 수 있습니다. 일치율이 매우 높은 시드된 스토리지 복제본 복제를 사용하는 경우에도 전체 초기 동기화 대역폭 사용량이 크게 줄어듭니다.


대역폭 제한을 설정하려면 다음을 사용합니다.

    Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x

대역폭 제한을 보려면 다음을 사용합니다.

    Get-SmbBandwidthLimit -Category StorageReplication

대역폭 제한을 제거하려면 다음을 사용합니다.

    Remove-SmbBandwidthLimit -Category StorageReplication
    
## <a name="what-network-ports-does-storage-replica-require"></a><a name="FAQ15"></a>저장소 복제본에 필요한 네트워크 포트는 무엇 인가요?
저장소 복제본은 복제 및 관리를 위해 SMB 및 WSMAN을 사용 합니다. 즉, 다음 포트가 필요 합니다.

 445 (SMB 복제 전송 프로토콜, 클러스터 RPC 관리 프로토콜) 5445 (iWARP SMB-iWARP RDMA 네트워킹을 사용 하는 경우에만 필요) 5985 (WSManHTTP-관리 프로토콜 for WMI/CIM/PowerShell)

참고: Test-srtopology cmdlet에는 ICMPv4/ICMPv6이 필요 하지만 복제 또는 관리에는 필요 하지 않습니다.

## <a name="what-are-the-log-volume-best-practices"></a><a name="FAQ15.5"></a>로그 볼륨 모범 사례는 무엇 인가요?
최적의 로그 크기는 환경 및 워크 로드 마다 다르며, 워크 로드에서 수행 하는 쓰기 IO의 양에 따라 결정 됩니다. 

1.  로그 용량이 크거나 작으면 더 빠르거나 더 느리게 작동 하지 않습니다.
2.  예를 들어 더 크거나 작은 로그는 10GB 데이터 볼륨과 10TB의 데이터 볼륨에 대 한 베어링은 없습니다.

로그가 클 수록 수집 되 고 더 많은 쓰기 Io가 래핑 되기 전에 유지 됩니다. 이렇게 하면 원본 컴퓨터와 대상 컴퓨터 간에 서비스가 중단 될 수 있습니다. 예를 들어 네트워크 중단 또는 오프 라인 상태로 유지 됩니다. 로그가 10 시간 쓰기를 포함할 수 있고 네트워크가 2 시간 동안 중단 되는 경우 네트워크가 반환 될 때 원본에서 다시 동기화 된 변경 내용에 대 한 델타를 대상으로 빠르게 재생 하 고 신속 하 게 다시 보호할 수 있습니다. 로그가 10 시간을 유지 하 고 가동 중단이 2 일인 경우 이제 원본에서 비트맵 이라고 하는 다른 로그에서 재생 해야 하며, 동기화를 다시 시작 하는 속도가 느릴 수 있습니다. 동기화 된 후에는 로그를 사용 하 여로 돌아갑니다.

저장소 복제본은 모든 쓰기 성능에 대해 로그에 의존 합니다. 복제 성능에 중요 한 로그 성능입니다. 로그가 모든 쓰기 IO를 직렬화 하 고 sequentialize 로그 볼륨이 데이터 볼륨 보다 더 잘 작동 하는지 확인 해야 합니다. 항상 로그 볼륨에서 SSD와 같은 플래시 미디어를 사용 해야 합니다. 다른 워크 로드를 SQL database 로그 볼륨에서 실행할 수 없도록 하는 것과 같은 방식으로 로그 볼륨에서 다른 워크 로드를 실행 하는 것을 허용 해서는 안 됩니다. 

다시 한 번: 로그 저장소는 데이터 저장소 보다 빠르지만 다른 워크 로드에는 해당 로그 볼륨을 사용 하지 않는 것이 좋습니다.

Test-srtopology 도구를 실행 하 여 로그 크기 조정 권장 사항을 가져올 수 있습니다. 또는 기존 서버에서 성능 카운터를 사용 하 여 로그 크기를 judgement 할 수 있습니다. 수식은 단순 합니다. 작업에서 데이터 디스크 처리량 (Avg Write Bytes/Sec)을 모니터링 하 고이를 사용 하 여 다른 크기의 로그를 채우는 데 소요 되는 시간을 계산 합니다. 예를 들어 데이터 디스크 처리량이 50 m b/s 이면 120GB 로그가 120GB/50MB seconds 또는 2400 초 또는 40 분으로 래핑됩니다. 따라서 로그가 래핑 되기까지 대상 서버에 연결할 수 없는 시간은 40 분입니다. 로그가 래핑 되었지만 대상을 다시 연결할 수 있는 경우 원본은 주 로그 대신 비트 맵 로그를 통해 블록을 재생 합니다. 로그의 크기는 성능에 영향을 주지 않습니다.

원본 클러스터의 데이터 디스크만 백업 해야 합니다. 백업이 저장소 복제본 작업과 충돌 하기 때문에 저장소 복제본 로그 디스크를 백업 하면 안 됩니다.

## <a name="why-would-you-choose-a-stretch-cluster-versus-cluster-to-cluster-versus-server-to-server-topology"></a><a name="FAQ16"></a>스트레치 클러스터와 클러스터 간 토폴로지를 선택 하는 이유는 무엇 인가요?  
저장소 복제본은 확장 클러스터, 클러스터 간 및 서버 간의 세 가지 기본 구성으로 제공 됩니다. 각각에는 서로 다른 이점이 있습니다.

확장 클러스터 토폴로지는 Hyper-v 사설 클라우드 클러스터 및 SQL Server FCI와 같이 오케스트레이션을 사용 하 여 자동 장애 조치 (failover)가 필요한 워크 로드에 적합 합니다. 또한 장애 조치(Failover) 클러스터 관리자를 사용 하는 기본 제공 그래픽 인터페이스가 있습니다. 영구 예약을 통해 저장소 공간, SAN, iSCSI 및 RAID의 클래식 비대칭 클러스터 공유 저장소 아키텍처를 활용 합니다. 2 개 노드를 사용 하 여이를 실행할 수 있습니다.

클러스터 간 토폴로지는 서로 다른 두 클러스터를 사용 하며, 특히, 일상적인 사용이 아닌 재해 복구를 위해 두 번째 사이트를 프로 비전 한 경우에는 수동 장애 조치 (failover)를 원하는 관리자에 게 적합 합니다. 오케스트레이션이 수동입니다. 스트레치 클러스터와는 달리이 구성에서는 스토리지 공간 다이렉트를 사용할 수 있습니다. 자세한 내용은 저장소 복제본 FAQ 및 클러스터 간 설명서를 참조 하십시오. 4 개의 노드를 사용 하 여이를 실행할 수 있습니다. 

서버 간 토폴로지는 클러스터링 할 수 없는 하드웨어를 실행 하는 고객에 게 적합 합니다. 수동 장애 조치 (failover) 및 오케스트레이션이 필요 합니다. 특히 비동기 복제를 사용 하는 경우 지점과 중앙 데이터 센터 간의 저렴 한 배포에 적합 합니다. 이 구성은 주로 단일 마스터 재해 복구 시나리오에 사용 되는 DFSR 보호 파일 서버의 인스턴스를 바꿀 수 있습니다.

모든 경우에 토폴로지는 물리적 하드웨어 및 가상 컴퓨터에서 실행 되는 모두를 지원 합니다. 가상 컴퓨터의 경우 기본 하이퍼바이저에는 Hyper-v가 필요 하지 않습니다. VMware, KVM, Xen 등이 될 수 있습니다.

저장소 복제본에는 동일한 컴퓨터에서 서로 다른 두 볼륨으로 복제를 가리키기 위한 서버-셀프 모드도 있습니다.

## <a name="is-data-deduplication-supported-with-storage-replica"></a><a name="FAQ18"></a>저장소 복제본에서 데이터 중복 제거를 지원 하나요?

예, 데이터 Deduplcation는 저장소 복제본에서 지원 됩니다. 원본 서버의 볼륨에서 데이터 중복 제거를 사용 하도록 설정 하 고, 복제 중에 대상 서버에서 중복 제거 된 볼륨 복사본을 받습니다.

원본 서버와 대상 서버 모두에 데이터 중복 제거를 *설치* 해야 하지만 ( [데이터 중복 제거 설치 및 사용](../data-deduplication/install-enable.md)참조) 대상 서버에서 데이터 중복 제거를 *사용 하도록 설정* 하지 않는 것이 중요 합니다. 저장소 복제본은 원본 서버에만 쓰기를 허용 합니다. 데이터 중복 제거는 볼륨에 쓰기를 수행 하므로 원본 서버 에서만 실행 해야 합니다. 

## <a name="can-i-replicate-between-windows-server-2019-and-windows-server-2016"></a><a name="FAQ19"></a>Windows Server 2019 및 Windows Server 2016 간에 복제할 수 있나요?

아쉽게도 Windows Server 2019 및 Windows Server 2016 간에 *새* 파트너 관계 만들기를 지원 하지 않습니다. Windows server 2016를 실행 하는 서버 또는 클러스터를 Windows Server 2019로 안전 하 게 업그레이드할 수 있으며 *기존* 파트너 관계는 계속 작동 합니다.

그러나 Windows Server 2019의 향상 된 복제 성능을 얻으려면 파트너 관계의 모든 구성원이 Windows Server 2019를 실행 해야 하며, 기존 파트너 관계 및 연결 된 복제 그룹을 삭제 한 다음, Windows 관리 센터에서 또는 새-SRPartnership을 사용 하 여 파트너 관계를 만들 때에는 시드 된 데이터를 사용 하 여 다시 만들어야 합니다.

## <a name="how-do-i-report-an-issue-with-storage-replica-or-this-guide"></a><a name="FAQ17"></a>저장소 복제본 또는이 가이드의 문제를 보고 어떻게 할까요??  
스토리지 복제본에 대한 기술 지원을 받으려면 [Microsoft TechNet 포럼](https://social.technet.microsoft.com/Forums/windowsserver/en-US/home?forum=WinServerPreview)에 게시하면 됩니다. srfeed@microsoft.com저장소 복제본에 대 한 질문이 나이 설명서의 문제에 대 한 전자 메일을 보낼 수도 있습니다. <https://windowsserver.uservoice.com>사이트는 동료 고객이 아이디어에 대 한 지원 및 피드백을 제공할 수 있도록 설계 변경 요청에 대 한 기본 설정입니다.

## <a name="can-storage-replica-be-configured-to-replicate-in-both-directions"></a><a name="FAQ18"></a>저장소 복제본을 양방향으로 복제 하도록 구성할 수 있나요?
저장소 복제본은 단방향 복제 기술입니다.  볼륨 별로 원본에서 대상으로만 복제 됩니다.  이 방향은 언제 든 지 되돌릴 수 있지만 한 방향 으로만 유지 됩니다.  그러나이는 한 방향으로 볼륨 (원본 및 대상)을 복제 하는 것이 아니라 다른 드라이브 집합 (원본 및 대상)이 반대 방향으로 복제 될 수 없음을 의미 하지는 않습니다.  예를 들어 서버 간 복제를 구성 하려고 합니다.  Server1 및 s e r v e r 1에는 각각 드라이브 문자 L:, M:, N: 및 O가 있으며 드라이브 M: s 1에서 Server2로, 드라이브 O: s 1에서 s 1로 복제 합니다.  각 그룹에 대해 별도의 로그 드라이브가 있는 경우이 작업을 수행할 수 있습니다. 핵. 

- Server1 원본 드라이브 M: 원본 로그 드라이브가 있는 경우 L: Server2 대상 드라이브 M:에 복제 합니다.
- Server2 원본 드라이브 O: 원본 로그 드라이브가 있습니다. N: Server1 대상 드라이브에 복제: 대상 로그 드라이브 N:

## <a name="related-topics"></a>관련 항목  
- [스토리지 복제본 개요](storage-replica-overview.md) 
- [공유 저장소를 사용 하 여 확장 클러스터 복제](stretch-cluster-replication-using-shared-storage.md)  
- [서버 간 저장소 복제](server-to-server-storage-replication.md)  
- [클러스터 간 저장소 복제](cluster-to-cluster-storage-replication.md)  
- [저장소 복제본: 알려진 문제](storage-replica-known-issues.md)  

## <a name="see-also"></a>참고 항목  
- [스토리지 개요](../storage.yml)  
- [스토리지 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)  
