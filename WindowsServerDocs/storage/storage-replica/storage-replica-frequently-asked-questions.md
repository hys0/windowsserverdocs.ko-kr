---
title: 저장소 복제본에 대한 질문과 대답
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/26/2019
ms.assetid: 12bc8e11-d63c-4aef-8129-f92324b2bf1b
ms.openlocfilehash: e832dce3eed7d0e5103254fb48683726b82af2e6
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475943"
---
# <a name="frequently-asked-questions-about-storage-replica"></a>저장소 복제본에 대한 질문과 대답

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

이 항목에서는 저장소 복제본에 대한 FAQ(자주 묻는 질문)의 답변을 제공합니다.

## <a name="FAQ1"></a> 저장소 복제본은 Azure에서 지원 됩니까?
예 Azure를 사용 하 여 다음 시나리오를 사용할 수 있습니다.

1. Azure 내에서 서버-투-서버 복제 (동기적으로 또는 하나 또는 두 개의 데이터 센터 장애 도메인에서 IaaS Vm 간에 비동기적으로 또는 비동기적으로 두 개의 별도 지역 간에)
2. Azure와 온-프레미스 서버-투-서버 비동기 복제 (VPN 또는 Azure ExpressRoute 사용)
3. Azure 내에서 클러스터 간 복제 (동기적으로 또는 하나 또는 두 개의 데이터 센터 장애 도메인에서 IaaS Vm 간에 비동기적으로 또는 비동기적으로 두 개의 별도 지역 간에)
4. Azure와 온-프레미스 클러스터 간 비동기 복제 (VPN 또는 Azure ExpressRoute 사용)

Azure에서 게스트 클러스터링에 추가 정보에서 찾을 수 있습니다. [Microsoft Azure에서 IaaS VM 게스트 클러스터 배포](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126)합니다.

중요 한 참고 사항:

1. Azure는 공유 VHDX 게스트 클러스터링을 지원 하지 않으므로 Windows 장애 조치 클러스터 가상 머신 클래식 공유 저장소 영구 디스크 예약 클러스터링 또는 저장소 공간 다이렉트에 대 한 iSCSI 대상을 사용 해야 합니다.
2. 저장소 복제본 기반 저장소 공간 다이렉트의 클러스터링에 대 한 Azure Resource Manager 템플릿은 [Azure 지역 간에 재해 복구를 위해 저장소 복제본을 사용 하 여 저장소 공간 다이렉트 SOFS 클러스터 만들기](https://aka.ms/azure-storage-replica-cluster)합니다.  
3. 클러스터 (클러스터 간의 액세스 권한을 부여 하는 것에 대 한 클러스터 Api 필요) 하는 Azure에서 클러스터 RPC 통신에 CNO에 대 한 네트워크 액세스를 구성 해야 합니다. TCP 포트 49152 위에 동적 범위 및 TCP 포트 135 허용 해야 합니다. 참조 [빌드-Azure IAAS VM에서 Windows Server 장애 조치 클러스터 네트워크 2 및 생성 부](https://blogs.technet.microsoft.com/askcore/2015/06/24/building-windows-server-failover-cluster-on-azure-iaas-vm-part-2-network-and-creation/)합니다.  
4. 각 노드 비대칭 클러스터의 저장소 복제본에서 복제 된 루프백 iSCSI를 사용는 2 노드 게스트 클러스터를 사용 하는 것이 가능 합니다. 하지만이 성능이 매우 저하 있 및 매우 제한 된 워크 로드 또는 테스트에 사용 해야 합니다.  

## <a name="FAQ2"></a> 초기 동기화 중에 복제 진행률을 보려면 어떻게 해야 합니까?  
대상 서버의 저장소 복제본 관리 이벤트 로그에 표시되는 이벤트 1237 메시지에 복사된 바이트 수와 남은 바이트 수가 10초마다 표시됩니다. 대상에서 하나 이상의 복제된 볼륨에 대한 **\Storage Replica Statistics\Total Bytes Received**를 표시하는 저장소 복제본 성능 카운터를 사용할 수도 있습니다. 또한 Windows PowerShell을 사용하여 복제 그룹을 쿼리할 수 있습니다. 예를 들어 다음 샘플 명령은 대상에 있는 그룹의 이름을 가져온 다음 10초마다 **Replication 2**라는 하나의 그룹을 쿼리하여 진행률을 표시합니다.  

```  
Get-SRGroup

do{
    $r=(Get-SRGroup -Name "Replication 2").replicas
    [System.Console]::Write("Number of remaining bytes {0}`n", $r.NumOfBytesRemaining)
    Start-Sleep 10
}until($r.ReplicationStatus -eq 'ContinuouslyReplicating')
Write-Output "Replica Status: "$r.replicationstatus

```  

## <a name="FAQ3"></a>복제에 사용 되는 특정 네트워크 인터페이스를 지정할 수 있습니까?  

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

    Set-SRNetworkConstraint -SourceComputerName sr-srv01 -SourceRGName group1 -SourceNWInterface "Cluster Network 1","Cluster Network 2" -DestinationComputerName sr-srv03 -DestinationRGName group2 -DestinationNWInterface "Cluster Network 1","Cluster Network 2"  

## <a name="FAQ4"></a> 일대다 복제 또는 (b c A) 전이적 복제를 구성할 수 있나요?  
아니요, 저장소 복제본의 서버, 클러스터 또는 확장 클러스터 노드 하나씩만 복제를 지원합니다. 이는 이후 릴리스에서 변경될 수 있습니다. 물론, 특정 볼륨 쌍의 다양한 서버 간에 어떤 방향으로든 복제를 구성할 수 있습니다. 예를 들어, 서버 1은 해당 D 볼륨을 서버 2에 복제할 수 있으며, 서버 3으로부터 E 볼륨을 복제할 수 있습니다.

## <a name="FAQ5"></a> 확장 하거나 저장소 복제본에서 복제 되는 볼륨을 축소할 수 있습니까?  
볼륨을 확장할 수 있지만 축소할 수는 없습니다. 기본적으로 저장소 복제본은 관리자가 복제되는 볼륨을 확장하지 않도록 방지합니다. 크기 조정 전에 원본 그룹의 `Set-SRGroup -AllowVolumeResize $TRUE` 옵션을 사용하세요. 예를 들어 다음과 같은 가치를 제공해야 합니다.

1. 원본 컴퓨터에 대해 사용 합니다. `Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. 선호하는 기술을 사용하여 볼륨 확장하기
3. 원본 컴퓨터에 대해 사용 합니다. `Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE` 

## <a name="FAQ6"></a>읽기 전용 액세스에 대 한 대상 볼륨을 온라인을 가져올 수 있습니까?  
Windows Server 2016에서는 불가능합니다. 복제가 시작될 때 저장소 복제본이 대상 볼륨을 분리합니다. 

그러나 Windows Server 2019 및 버전부터 Windows 서버 반기 채널 1709 대상 저장소를 탑재 하는 옵션 수 있게 되었습니다.-이 기능은 "테스트 장애 조치" 이라고 합니다. 이를 수행하려면 현재 대상에서 복제되고 있지 않은 미사용 NTFS 또는 ReFS 포맷 볼륨이 있어야 합니다. 그런 다음 테스트 및 백업을 목적으로 복제된 저장소의 스냅숏을 일시적으로 탑재할 수 있습니다. 

예를 들어 대상 서버 "SRV2"의 복제 그룹 "RG2"에 있는 볼륨 "D:"를 복제되지 않은 SRV2의 "T:"로 복제 시 테스트 장애 조치를 만들려면

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`
 
복제된 볼륨 D:는 이제 SRV2에서 액세스할 수 있습니다. 읽고 일반적으로 쓸 수, 파일을 복사 또는 d: 경로에서 보관을 위해 다른 위치에 저장 하는 온라인 백업을 실행 합니다. T: 볼륨 로그 데이터가 포함 됩니다.

테스트 장애 조치 스냅숏을 제거하고 변경 사항을 취소:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`
 
단기 일시 작업에 대해서만 테스트 장애 조치 기능을 사용해야 합니다. 장기 사용 용도가 아닙니다. 사용 중인 경우 실제 대상 볼륨으로의 복제는 계속됩니다. 

## <a name="FAQ7"></a> 확장 클러스터에서 스케일 아웃 파일 서버 (SOFS)를 구성할 수 있습니까?  
기술적으로 가능 하지만 SOFS에 연결 된 계산 노드에서 사이트 인식이 지원 부족으로 인해 권장된 구성이 아닙니다. 캠퍼스 거리 네트워킹에 일반적으로 대기 시간이 하위 밀리초를 사용 하는 경우이 구성은 일반적으로 문제 없이 작동 합니다.   

클러스터 간 복제를 구성하는 경우 저장소 복제본은 두 클러스터 간에 복제할 때 저장소 공간 다이렉트 사용을 포함하여 스케일 아웃 파일 서버를 완전히 지원합니다.  

## <a name="FAQ7.5"></a> CSV 확장 클러스터에서 또는 클러스터 간에 복제할 필요 합니까?  
아니요. CSV 또는 파일 서버 역할을 같은 클러스터 리소스를 소유한 영구 디스크 예약 (PDR)를 사용 하 여 복제할 수 있습니다. 

클러스터 간 복제를 구성하는 경우 저장소 복제본은 두 클러스터 간에 복제할 때 저장소 공간 다이렉트 사용을 포함하여 스케일 아웃 파일 서버를 완전히 지원합니다.  

## <a name="FAQ8"></a>구성할 수 있습니까 저장소 공간 다이렉트 저장소 복제본을 사용 하 여 확장 클러스터에서?  
Windows Server에서 지원 되는 구성이 아닙니다. 이는 이후 릴리스에서 변경될 수 있습니다. 클러스터 간 복제를 구성하는 경우 저장소 복제본은 저장소 공간 다이렉트 사용을 포함하여 스케일 아웃 파일 서버 및 Hyper-V 서버를 완전히 지원합니다.  

## <a name="FAQ9"></a>비동기 복제를 구성 하려면 어떻게 해야 하나요?  

`New-SRPartnership -ReplicationMode`를 지정하고 **Asynchronous** 인수를 제공합니다. 기본적으로 저장소 복제본의 모든 복제는 동기식입니다. `Set-SRPartnership -ReplicationMode`를 사용하여 모드를 변경할 수도 있습니다.  

## <a name="FAQ10"></a>확장 클러스터의 자동 장애 조치는 어떻게 방지할 수 있나요?  
자동 장애 조치(failover)를 방지하려면 PowerShell을 사용하여 `Get-ClusterNode -Name "NodeName").NodeWeight=0`을 구성하면 됩니다. 그러면 재해 복구 사이트에서 각 노드에 대한 응답이 제거됩니다. 그런 다음 기본 사이트의 노드에서 `Start-ClusterNode -PreventQuorum`을 사용하고 재해 사이트의 노드에서 `Start-ClusterNode -ForceQuorum`을 사용하여 장애 조치(failover)를 강제 적용할 수 있습니다. 자동 장애 조치(failover)를 방지하는 그래픽 옵션은 없으며, 자동 장애 조치(failover) 방지는 권장되지 않습니다.  

## <a name="FAQ11"></a>가상 머신 복원 력이 함
새 Hyper-v 가상 머신 복원 력 기능에서 실행 하 고 재해 복구 사이트로 장애 조치 하는 대신 가상 컴퓨터 일시 중지를 방지 하려면 실행 `(Get-Cluster).ResiliencyDefaultPeriod=0`  

## <a name="FAQ12"></a> 초기 동기화에 대 한 시간을 줄이는 방법

씬 프로비전된 저장소를 사용하여 초기 동기화 속도를 높이는 것이 한 가지 방법입니다. 저장소 복제본은 클러스터되지 않은 저장소 공간, Hyper-V 동적 디스크 및 SAN LUN을 포함하여 씬 프로비전된 저장소를 쿼리하고 자동으로 사용합니다.  

또한 대역폭 사용량을 줄이기 위해 시드 된 데이터 볼륨을 사용할 수 있으며 경우에 따라 시간에 대상 없도록 함으로써 볼륨 다음 장애 조치 클러스터 관리자의 시드 됨 옵션을 사용 하는 기본에서 데이터의 일부 하위 집합 또는 `New-SRPartnership`합니다. 볼륨이 대개 비어 있는 경우 시드된 동기화를 사용하여 시간 및 대역폭 사용을 줄일 수 있습니다. 여러 가지 방법으로 다양 한 수준의 효율성을 사용 하 여 시드 데이터를 수 있습니다.

1. 이전 복제-일반 초기를 사용 하 여 복제 하 여 동기화 로컬 디스크와 볼륨을 포함, 복제 제거, 대상 디스크를 배송 하는 노드 간에 다른 곳에서 다음 옵션은 시드를 사용 하 여 복제를 추가 합니다. 저장소 복제본을 블록 복사본 미러를 보장 하 고 복제 하는 작업만 델타 블록 이것이 가장 효과적인 방법입니다.
2. 스냅숏 복원 하거나 복원 스냅숏 기반 백업 대상 볼륨에 볼륨 기반 스냅숏으로 복원 하 여 없어야 블록 레이아웃에서 최소한의 차이로 합니다. 블록은 미러 이미지 중 볼륨 스냅숏이 덕분 일치할 것으로 예상 대로 이것이 다음 가장 효과적인 방법입니다.
3. 복사 된 파일-하기 전에 사용 된 적이 없는 대상에 새 볼륨을 만들고 전체 robocopy /MIR 트리를 수행 하 여 데이터를 복사 블록 일치 될 가능성이 있습니다. Windows 파일 탐색기를 사용 하 여 트리의 일부를 복사 또는 블록 일치 하는 항목을 만들지 않습니다. 파일을 수동으로 복사할 시드의 이상 효과적인 메서드입니다.

## <a name="FAQ13"></a> 복제를 관리 하는 사용자를 위임할 수 있습니까?  

사용할 수는 `Grant-SRDelegation` cmdlet. 로컬 관리자 그룹의 구성원이 아니더라도 복제를 만들거나 수정하거나 제거할 수 있는 권한이 있으므로 서버 간, 클러스터 간 및 확장 클러스터 복제 시나리오에서 특정 사용자를 설정할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

    Grant-SRDelegation -UserName contso\tonywang  

이 cmdlet은 사용자가 관리하려는 서버에서 로그오프했다가 다시 로그온해야 변경 내용이 적용됨을 알립니다. `Get-SRDelegation` 및 `Revoke-SRDelegation`을 사용하여 추가로 제어할 수 있습니다.  

## <a name="FAQ13"></a> 새로운 내 백업 및 복원 복제 된 볼륨에 대 한 옵션?
저장소 복제본은 원본 볼륨의 백업 및 복원을 지원합니다. 또한 원본 볼륨의 스냅샷 만들기 및 복원도 지원합니다. 저장소 복제본으로 보호되는 대상 볼륨은 탑재되지도 않고 액세스할 수도 없으므로 백업하거나 복원할 수 없습니다. 원본 볼륨이 손실된 재해가 발생한 경우 `Set-SRPartnership`을 사용하여 이전 대상 볼륨을 읽기/쓰기 가능한 원본이 되도록 승격하면 이 볼륨을 백업하거나 복원할 수 있습니다. `Remove-SRPartnership` 및 `Remove-SRGroup`으로 복제를 제거하여 해당 볼륨을 읽기/쓰기 가능하도록 다시 탑재할 수도 있습니다.
주기적인 응용 프로그램 일치 스냅샷을 만들려면 원본 서버에서 VSSADMIN.EXE를 사용하여 복제된 데이터 볼륨의 스냅샷을 만들면 됩니다. 예를 들어 저장소 복제본으로 F: 볼륨을 복제하는 경우 다음을 실행합니다.

    vssadmin create shadow /for=F:
그런 다음, 복제 방향을 전환하거나 복제를 제거하거나 단순히 동일한 원본 볼륨에 계속 있는 경우 모든 스냅샷을 특정 시점으로 복원할 수 있습니다. 예를 들어 여전히 F:를 사용하는 경우 다음을 실행합니다.

    vssadmin list shadows
     vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
예약된 작업을 정기적으로 실행하도록 이 도구를 예약할 수도 있습니다. VSS 사용에 대한 자세한 내용은 [Vssadmin](../../administration/windows-commands/vssadmin.md)을 검토하세요. 로그 볼륨은 백업할 필요가 없습니다. 이 작업은 VSS에서 무시됩니다.
Windows Server 백업, Microsoft Azure 백업, Microsoft DPM 또는 다른 스냅샷, VSS, 가상 컴퓨터 또는 파일 기반 기술은 볼륨 계층 내에서 사용되는 경우 저장소 복제본에서 지원됩니다. 저장소 복제본은 블록 기반 백업 및 복원을 지원하지 않습니다.

## <a name="FAQ14"></a> 대역폭 사용량을 제한 하도록 복제를 구성할 수 있나요?
예, SMB 대역폭 제한을 사용하면 됩니다. 이는 모든 저장소 복제본 트래픽에 적용되는 전역 설정이므로 이 서버의 모든 복제에 영향을 줍니다. 일반적으로 이는 모든 볼륨 데이터를 전송해야 하는 저장소 복제본 초기 동기화 설정에만 필요합니다. 초기 동기화 후에 필요한 경우 네트워크 대역폭이 너무 낮아 IO 워크로드에 사용할 수 없으면 IO를 줄이거나 대역폭을 늘립니다.

이는 비동기 복제에만 사용해야 합니다(참고: 초기 동기화는 동기식을 지정한 경우에도 항상 비동기식임).
또한 네트워크 QoS 정책을 사용하여 저장소 복제본 트래픽을 구성할 수 있습니다. 일치율이 매우 높은 시드된 저장소 복제본 복제를 사용하는 경우에도 전체 초기 동기화 대역폭 사용량이 크게 줄어듭니다.


대역폭 제한을 설정하려면 다음을 사용합니다.

    Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x

대역폭 제한을 보려면 다음을 사용합니다.

    Get-SmbBandwidthLimit -Category StorageReplication

대역폭 제한을 제거하려면 다음을 사용합니다.

    Remove-SmbBandwidthLimit -Category StorageReplication
    
## <a name="FAQ15"></a>저장소 복제본에는 어떤 네트워크 포트가 필요 합니까?
저장소 복제본은 복제 및 관리에 SMB와 WSMAN을 사용합니다. 즉, 다음 포트가 필요합니다.

 445 (SMB-복제 전송 프로토콜, 클러스터 RPC 관리 프로토콜) (iWARP SMB-iWARP RDMA 네트워킹을 사용 하는 경우에 필요) 5445 5985 (WSManHTTP-powershell/WMI/CIM 관리 프로토콜)

참고: Test-srtopology cmdlet 필요 ICMPv4/ICMPv6, 복제 또는 관리 합니다.

## <a name="FAQ15.5"></a>로그 볼륨 모범 사례는 무엇입니까?
로그의 최적의 크기는 환경 및 워크 로드, 매우 다양 하 고 얼마나 그런가요 쓰기 IO 워크 로드가 수행 결정 됩니다. 

1.  로그가 더 크거나 작다고 해서 속도가 빨라지거나 느려지지 않습니다.
2.  예를 들어 더 큰 로그와 더 작은 로그는 10GB의 데이터 볼륨 대 10TB 데이터 볼륨에 미치는 영향이 다르지 않습니다.

로그가 더 크다는 것은 간단하게 없어지기 전에 더 많은 쓰기 IO를 수집하고 유지하는 것입니다. 이를 통해 네트워크 중단이나 대상이 오프라인되는 것과 같은 원본과 대상 컴퓨터 사이의 서비스 중단이 길어져도 그 피해가 줄어듭니다. 로그가 10시간의 쓰기를 보유하고 있고 네트워크가 2시간 동안 중단된 경우, 네트워크가 원본을 복구할 때 동기화되지 않은 차이점만 대상으로 매우 빠르게 복사하므로 매우 신속하게 다시 보호 상태를 유지할 수 있습니다. 로그가 10시간의 쓰기를 보유하고 있고 중단이 2일인 경우, 원본은 비트맵이라고 하는 다른 로그에서 복원되며 동기화 상태로 돌아가는 데 더 느립니다. 동기화되면 로그 사용으로 돌아갑니다.

저장소 복제는 모든 쓰기 성능을 로그에 의존합니다. 로그 성능은 복제 성능에 매우 중요합니다. 로그가 모든 쓰기 IO를 직렬화하고 순차화하므로 로그 볼륨의 성능은 데이터 볼륨보다 좋아야 합니다. 로그 볼륨에는 항상 SSD와 같은 플래시 미디어를 사용해야 합니다. SQL 데이터베이스 로그 볼륨에서 다른 워크로드의 실행을 절대 허용하지 않은 것과 마찬가지로 로그 볼륨에서는 절대 다른 워크로드가 실행되지 않도록 해야 합니다. 

다시 합니다. 로그 저장소 데이터 저장소 보다 빠릅니다 되며 로그 볼륨을 다른 워크 로드에 대 한 사용 되지 해야 것이 좋습니다.

Test-srtopology 도구를 실행 하 여 로그 크기 조정 권장 사항을 가져올 수 있습니다. 또는 로그 크기 관행 수 있도록 기존 서버에서 성능 카운터를 사용할 수 있습니다. 수식은 간단: 작업에서 데이터 디스크 처리량 (Avg Write Bytes/Sec)를 모니터링 하 고 사용 하 여 다양 한 크기의 로그를 채우는 데 걸리는 시간을 계산 합니다. 예를 들어, 데이터 디스크 처리량 50 MB/s 하면 120GB/50MB 초 또는 2400 초 40 분에서 120 GB의 로그입니다. 따라서 대상 서버에 연결할 수 래핑된 로그 하기 전에 연결할 수 있는 시간 40 분입니다. 로그를 래핑합니다. 대상을 다시 연결할 수 있게 하지만 경우 소스는 기본 로그 대신 비트 맵 로그를 통해 블록을 재생 합니다. 로그의 크기에 성능에 영향을 줄이 없습니다.

원본 클러스터에서 데이터 디스크에만 백업 해야 합니다. 저장소 복제본 로그 디스크 해야 하지 백업할 하므로 백업 저장소 복제본 작업과 충돌할 수 있습니다.

## <a name="FAQ16"></a> 클러스터와 클러스터 간 및 서버-투-서버 토폴로지 및 확장 클러스터를 선택 하는 이유는?  
세 가지 기본 구성에서 저장소 복제본 상태가: 클러스터, 클러스터 간 및 서버-투-서버를 확장 합니다. 각자 다른 장점을 가지고 있습니다.

확장 클러스터 토폴로지는 Hyper-V 사설 클라우드 클러스터, SQL Server FCI와 같이 오케스트레이션을 사용한 자동 장애 조치(failover)가 필요한 워크로드에 이상적입니다. 또한 장애 조치(Failover) 클러스터 관리자를 사용하는 기본 제공 그래픽 인터페이스도 있습니다. 이 구성은 영구 예약을 통해 저장소 공간, SAN, iSCSI, RAID의 기본 비대칭 클러스터 공유 저장소를 활용합니다. 이 구성은 2개 노드만으로도 실행할 수 있습니다.

클러스터 간 토폴로지는 두 개의 별도 클러스터를 사용하며 수동 장애 복구(failover)를 원하는 관리자에게 이상적입니다. 특히 두 번째 사이트가 재해 복구를 위해 준비되었으며 일상 업무에 사용되지 않는 경우에 좋습니다. 오케스트레이션은 수동입니다. 확장 클러스터와는 달리 저장소 공간 다이렉트 사용할 수 있습니다 (사용 하 여 주의-클러스터 간 설명서 및 저장소 복제본 FAQ 참조)이 구성. 이 구성은 4개 노드만으로도 실행할 수 있습니다. 

서버 간 토폴로지는 클러스터링할 수 없는 하드웨어를 실행하는 고객에 이상적입니다. 이 구성은 수동 장애 조치(failover)와 오케스트레이션이 필요합니다. 비동기 복제를 사용 하는 경우에 특히 중앙 데이터 센터 및 지사 간에 저렴 한 배포에 대 한 이상적입니다. 이 구성은 단일 마스터 재해 복구 시나리오를 위해 사용되는 DFSR 보호 파일 서버의 인스턴스를 종종 대체합니다.

모든 경우, 토폴로지는 물리적 하드웨어와 가상 컴퓨터에서 모두 실행할 수 있습니다. 가상 컴퓨터의 경우 기본 하이퍼바이저에 Hyper-V가 필요하지 않으며 VMware, KVM, Xen 등일 수 있습니다.

저장소 복제본에는 서버 자체 모드도 있는데, 이 모드에서는 동일한 컴퓨터의 두 다른 볼륨으로 복제 원본과 대상을 지정할 수 있습니다.

## <a name="FAQ18"></a> 데이터 중복 제거는 저장소 복제본 지원 되나요?

예, 데이터 Deduplcation 저장소 복제본 지원 됩니다. 원본 서버에서 볼륨에 데이터 중복 제거를 사용 하 고 대상 서버를 복제 하는 동안 볼륨의 중복 제거 된 복사본을 받습니다.

수행 해야 하는 동안 *설치* 원본 및 대상 서버에서 데이터 중복 제거 (참조 [설치 및 데이터 중복 제거를 사용 하도록 설정 하면](../data-deduplication/install-enable.md)), 것이 중요 하지에 *사용*대상 서버에서 데이터 중복 제거 합니다. 저장소 복제본에 원본 서버에만 쓰기 수 있습니다. 데이터 중복 제거 볼륨에 쓰기를 사용 하면에 원본 서버 에서만 실행 해야 합니다. 

## <a name="FAQ19"></a> Windows Server 2016 및 Windows Server 2019 간에 복제할 수 있습니까?

만들기는 지원 되지 않습니다 아쉽게도 *새* Windows Server 2016 및 Windows Server 2019 간의 파트너 관계입니다. 서버 또는 Windows Server 2016 및 Windows Server 2019를 실행 하는 클러스터를 안전 하 게 업그레이드할 수 있습니다 *기존* 파트너 관계는 계속 작동 합니다.

그러나 Windows Server 2019의 향상 된 복제 성능을 얻으려면, 파트너 관계의 모든 멤버 Windows Server 2019 실행 해야 하며 관련 된 복제 그룹 및 (시드 된 데이터를 사용 하 여이 다시 만들어야 기존 파트너 관계를 삭제 해야 합니다. 만들 때 파트너 관계 Windows Admin Center 또는 새로 만들기-SRPartnership cmdlet을 사용 하 여).

## <a name="FAQ17"></a> 저장소 복제본 또는이 가이드를 사용 하 여 문제를 보고 하려면 어떻게 해야 하나요?  
저장소 복제본에 대한 기술 지원을 받으려면 [Microsoft TechNet 포럼](https://social.technet.microsoft.com/Forums/windowsserver/en-US/home?forum=WinServerPreview)에 게시하면 됩니다. 저장소 복제본에 대한 질문 또는 이 설명서에 대한 문제를 전자 메일(srfeed@microsoft.com)로 보낼 수도 있습니다. https://windowsserver.uservoice.com 인 사이트가 디자인 변경 요청에 대 한 기본 아이디어에 대 한 지원 및 피드백을 제공 하도록 동료 고객에 게 있습니다.



## <a name="related-topics"></a>관련 항목  
- [저장소 복제본 개요](storage-replica-overview.md) 
- [공유 저장소를 사용 하 여 확장 클러스터 복제](stretch-cluster-replication-using-shared-storage.md)  
- [서버 간 저장소 복제](server-to-server-storage-replication.md)  
- [클러스터 간 저장소 복제](cluster-to-cluster-storage-replication.md)  
- [스토리지 복제본: 알려진된 문제](storage-replica-known-issues.md)  

## <a name="see-also"></a>관련 항목  
- [저장소 개요](../storage.md)  
- [스토리지 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)  
