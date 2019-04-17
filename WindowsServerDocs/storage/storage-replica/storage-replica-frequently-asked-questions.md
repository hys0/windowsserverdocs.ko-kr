---
title: "저장소 복제본에 대한 질문과 대답"
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 07/20/2017
ms.assetid: 12bc8e11-d63c-4aef-8129-f92324b2bf1b
ms.openlocfilehash: f29ca24a39e00f5142fe700e6abb09d1673acf7b
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="frequently-asked-questions-about-storage-replica"></a>저장소 복제본에 대한 질문과 대답

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 저장소 복제본에 대한 FAQ(자주 묻는 질문)의 답변을 제공합니다.

## <a name="FAQ1"></a> 저장소 복제본은 Nano 서버에서 지원됩니까?  
예.  

> [!NOTE]
> 설치하는 동안 **저장소** Nano Server 패키지를 사용해야 합니다. Nano Server 배포에 대한 자세한 내용은 [Nano Server 시작](https://technet.microsoft.com/library/mt126167.aspx)을 참조하세요.  

다음과 같이 PowerShell 원격을 사용하여 Nano Server에 저장소 복제본을 설치합니다.  

1. 클라이언트 신뢰 목록에 Nano Server를 추가합니다.  
   > [!NOTE]
   > 이 단계는 컴퓨터가 Active Directory 도메인 서비스 포리스트의 구성원이 아니거나 신뢰할 수 없는 포리스트에 속하지 않은 경우에만 필요합니다. PSSession 원격에 NTLM 지원을 추가하지만 이는 보안상의 이유로 기본적으로 해제되어 있습니다. 자세한 내용은 [PowerShell 원격 보안 고려 사항](https://msdn.microsoft.com/powershell/scriptiwinrmsecurity)을 참조하세요.  

   ```  
       Set-Item WSMan:\localhost\Client\TrustedHosts "<computer name of Nano Server>"  
   ```  
2.  저장소 복제본 기능을 설치하려면 관리 컴퓨터에서 다음 cmdlet을 실행합니다.  

    ```  
    Install-windowsfeature -Name storage-replica,RSAT-Storage-Replica -ComputerName <nano server> -Restart -IncludeManagementTools  
    ```  

    Windows Server 2016의 Nano 서버에서 `Test-SRTopology` cmdlet을 사용하려면 CredSSP를 통해 원격 스크립트 호출을 실행해야 합니다. 다른 저장소 복제본 cmdlet과 달리 `Test-SRTopology`는 원본 서버에서 로컬로 실행해야 합니다.   
Nano Server에서 원격 PSSession을 통해 다음을 실행합니다.  

    >[!NOTE]
    >CREDSSP는 `Test-SRTopology` cmdlet에서 Kerberos 이중 홉을 지원하는 데 필요하며, 분산 시스템 자격 증명을 자동으로 처리하는 다른 저장소 복제본 cmdlet에는 필요하지 않습니다. 일반적인 상황에서는 CREDSSP를 사용하지 않는 것이 좋습니다. CREDSSP에 대한 대체 방식은 다음 Microsoft 블로그 게시물 "PowerShell Remoting Kerberos Double Hop Solved Securely(안전하게 해결된 PowerShell 원격 Kerberos 이중 홉)" - https://blogs.technet.microsoft.com/ashleymcglone/2016/08/30/powershell-remoting-kerberos-double-hop-solved-securely/을 참조하세요. 

        Enable-WSManCredSSP -role server       

    관리 컴퓨터에서 다음을 실행합니다.  

         Enable-WSManCredSSP Client -DelegateComputer <remote server name>  

         $CustomCred = Get-Credential  

         Invoke-Command -ComputerName sr-srv01 -ScriptBlock { Test-SRTopology <commands> } -Authentication Credssp -Credential $CustomCred  

       그런 다음 관리 컴퓨터에 결과를 복사하거나 경로를 공유합니다. Nano에는 필요한 그래픽 라이브러리가 없으므로 Test-SRTopology를 사용하여 결과를 처리하고 차트가 포함된 보고서 파일을 생성할 수 있습니다. 예:  

        Test-SRTopology -GenerateReport -DataPath \\sr-srv05\c$\temp  


## <a name="FAQ2"></a> 초기 동기화 중에 복제 진행률을 확인하려면 어떻게 해야 합니까?  
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

## <a name="FAQ3"></a>복제에 사용할 특정 네트워크 인터페이스를 지정할 수 있습니까?  

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

## <a name="FAQ4"></a> 일 대 다 복제(A-B-C) 또는 전이적 복제를 구성할 수 있습니까?  
Windows Server 2016에서는 불가능합니다. 이 릴리스에서는 서버, 클러스터 또는 확장 클러스터 노드의 일 대 일 복제만 지원합니다. 이는 이후 릴리스에서 변경될 수 있습니다. 물론, 특정 볼륨 쌍의 다양한 서버 간에 어떤 방향으로든 복제를 구성할 수 있습니다. 예를 들어, 서버 1은 해당 D 볼륨을 서버 2에 복제할 수 있으며, 서버 3으로부터 E 볼륨을 복제할 수 있습니다.

## <a name="FAQ5"></a> 저장소 복제본에서 복제되는 볼륨을 확장하거나 축소할 수 있습니까?  
볼륨을 확장할 수 있지만 축소할 수는 없습니다. 기본적으로 저장소 복제본은 관리자가 복제되는 볼륨을 확장하지 않도록 방지합니다. 크기 조정 전에 원본 그룹의 `Set-SRGroup -AllowVolumeResize $TRUE` 옵션을 사용하세요. 예:

1. 원본 컴퓨터에 대한 사용: `Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. 선호하는 기술을 사용하여 볼륨 확장하기
3. 원본 컴퓨터에 대한 사용: `Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE` 

## <a name="FAQ6"></a>읽기 전용 액세스를 위해 대상 볼륨을 온라인 상태로 전환할 수 있습니까?  
Windows Server 2016 RTM에는 "RS1" 릴리스라고 하는 것이 없습니다. 복제가 시작될 때 저장소 복제본이 대상 볼륨을 분리합니다. 

그러나 Windows Server, 버전 1709에서는 이제 "테스트 장애 조치"라고 하는 대상 저장소 탑재 옵션을 이용할 수 있습니다. 이를 수행하려면 현재 대상에서 복제되고 있지 않은 미사용 NTFS 또는 ReFS 포맷 볼륨이 있어야 합니다. 그런 다음 테스트 및 백업을 목적으로 복제된 저장소의 스냅숏을 일시적으로 탑재할 수 있습니다. 

예를 들어 대상 서버 "SRV2"의 복제 그룹 "RG2"에 있는 볼륨 "D:"를 복제되지 않은 SRV2의 "T:"로 복제 시 테스트 장애 조치를 만들려면

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`
 
복제된 볼륨 D:는 이제 SRV2에서 액세스할 수 있습니다. 이를 정상적으로 읽고 쓸 수 있고, 파일을 복사하거나 온라인 백업을 실행하여 안전한 보관을 위해 다른 곳에 저장할 수도 있습니다.

테스트 장애 조치 스냅숏을 제거하고 변경 사항을 취소:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`
 
단기 일시 작업에 대해서만 테스트 장애 조치 기능을 사용해야 합니다. 장기 사용 용도가 아닙니다. 사용 중인 경우 실제 대상 볼륨으로의 복제는 계속됩니다. 

## <a name="FAQ7"></a> 확장 클러스터에서 SOFS(스케일 아웃 파일 서버)를 구성할 수 있습니까?  
기술적으로 가능하지만 SOFS에 연결된 계산 노드에서는 사이트 인식이 지원되지 않으므로 이는 Windows Server 2016에서 권장되는 구성이 아닙니다. 일반적으로 대기 시간이 하위 밀리초 단위인 캠퍼스 거리 네트워킹을 사용하는 경우 이 구성은 보통 문제 없이 작동합니다.   

클러스터 간 복제를 구성하는 경우 저장소 복제본은 두 클러스터 간에 복제할 때 저장소 공간 다이렉트 사용을 포함하여 스케일 아웃 파일 서버를 완전히 지원합니다.  

## <a name="FAQ8"></a>저장소 복제본을 사용하여 확장 클러스터에서 저장소 공간 다이렉트를 구성할 수 있습니까?  
이 구성은 Windows Server 2016에서 지원되지 않습니다.  이는 이후 릴리스에서 변경될 수 있습니다. 클러스터 간 복제를 구성하는 경우 저장소 복제본은 저장소 공간 다이렉트 사용을 포함하여 스케일 아웃 파일 서버 및 Hyper-V 서버를 완전히 지원합니다.  

## <a name="FAQ9"></a>비동기 복제를 구성하려면 어떻게 해야 합니까?  

`New-SRPartnership -ReplicationMode`를 지정하고 **Asynchronous** 인수를 제공합니다. 기본적으로 저장소 복제본의 모든 복제는 동기식입니다. `Set-SRPartnership -ReplicationMode`를 사용하여 모드를 변경할 수도 있습니다.  

## <a name="FAQ10"></a>확장 클러스터의 자동 장애 조치(failover)를 방지하려면 어떻게 해야 합니까?  
자동 장애 조치(failover)를 방지하려면 PowerShell을 사용하여 `Get-ClusterNode -Name "NodeName").NodeWeight=0`을 구성하면 됩니다. 그러면 재해 복구 사이트에서 각 노드에 대한 응답이 제거됩니다. 그런 다음 기본 사이트의 노드에서 `Start-ClusterNode -PreventQuorum`을 사용하고 재해 사이트의 노드에서 `Start-ClusterNode -ForceQuorum`을 사용하여 장애 조치(failover)를 강제 적용할 수 있습니다. 자동 장애 조치(failover)를 방지하는 그래픽 옵션은 없으며, 자동 장애 조치(failover) 방지는 권장되지 않습니다.  

## <a name="FAQ11"></a>가상 컴퓨터 복원력을 사용하지 않도록 설정하려면 어떻게 해야 합니까?  
새 Hyper-V 가상 컴퓨터 복원력 기능이 실행되지 않도록 하여 재해 복구 사이트에서 장애 조치(failover)하는 대신 가상 컴퓨터를 일시 중지하려면 다음을 실행합니다. `(Get-Cluster).ResiliencyDefaultPeriod=0`  

## <a name="FAQ12"></a> 초기 동기화 시간을 줄이려면 어떻게 해야 합니까?  

씬 프로비전된 저장소를 사용하여 초기 동기화 속도를 높이는 것이 한 가지 방법입니다. 저장소 복제본은 클러스터되지 않은 저장소 공간, Hyper-V 동적 디스크 및 SAN LUN을 포함하여 씬 프로비전된 저장소를 쿼리하고 자동으로 사용합니다.  

대역폭 사용을 줄이기 위해 경우에 따라, 대상 볼륨에 복원된 백업, 이전 스냅숏, 이전 복제, 복사된 파일 등을 통해 기본 사이트의 일부 데이터 하위 집합이 있는지 확인한 다음 장애 조치(Failover) 클러스터 관리자의 시드됨 옵션 또는 `New-SRPartnership`을 사용하는 방식으로 시드된 데이터 볼륨을 사용할 수도 있습니다. 볼륨이 대개 비어 있는 경우 시드된 동기화를 사용하여 시간 및 대역폭 사용을 줄일 수 있습니다.

## <a name="FAQ13"></a> 복제 관리를 사용자에게 위임할 수 있습니까?  

Windows Server 2016에서 `Grant-SRDelegation` cmdlet을 사용하면 됩니다. 로컬 관리자 그룹의 구성원이 아니더라도 복제를 만들거나 수정하거나 제거할 수 있는 권한이 있으므로 서버 간, 클러스터 간 및 확장 클러스터 복제 시나리오에서 특정 사용자를 설정할 수 있습니다. 예:  

    Grant-SRDelegation -UserName contso\tonywang  

이 cmdlet은 사용자가 관리하려는 서버에서 로그오프했다가 다시 로그온해야 변경 내용이 적용됨을 알립니다. `Get-SRDelegation` 및 `Revoke-SRDelegation`을 사용하여 추가로 제어할 수 있습니다.  

## <a name="FAQ13"></a> 복제된 볼륨에 대한 백업 및 복원 옵션은 무엇입니까?
저장소 복제본은 원본 볼륨의 백업 및 복원을 지원합니다. 또한 원본 볼륨의 스냅숏 만들기 및 복원도 지원합니다. 저장소 복제본으로 보호되는 대상 볼륨은 탑재되지도 않고 액세스할 수도 없으므로 백업하거나 복원할 수 없습니다. 원본 볼륨이 손실된 재해가 발생한 경우 `Set-SRPartnership`을 사용하여 이전 대상 볼륨을 읽기/쓰기 가능한 원본이 되도록 승격하면 이 볼륨을 백업하거나 복원할 수 있습니다. `Remove-SRPartnership` 및 `Remove-SRGroup`으로 복제를 제거하여 해당 볼륨을 읽기/쓰기 가능하도록 다시 탑재할 수도 있습니다.
주기적인 응용 프로그램 일치 스냅숏을 만들려면 원본 서버에서 VSSADMIN.EXE를 사용하여 복제된 데이터 볼륨의 스냅숏을 만들면 됩니다. 예를 들어 저장소 복제본으로 F: 볼륨을 복제하는 경우 다음을 실행합니다.

    vssadmin create shadow /for=F:
그런 다음 복제 방향을 전환하거나 복제를 제거하거나 단순히 동일한 원본 볼륨에 계속 있는 경우 모든 스냅숏을 특정 시점으로 복원할 수 있습니다. 예를 들어 여전히 F:를 사용하는 경우 다음을 실행합니다.

    vssadmin list shadows
     vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
예약된 작업을 정기적으로 실행하도록 이 도구를 예약할 수도 있습니다. VSS 사용에 대한 자세한 내용은 [Vssadmin](https://technet.microsoft.com/library/cc754968.aspx)을 검토하세요. 로그 볼륨은 백업할 필요가 없습니다. 이 작업은 VSS에서 무시됩니다.
Windows Server 백업, Microsoft Azure 백업, Microsoft DPM 또는 다른 스냅숏, VSS, 가상 컴퓨터 또는 파일 기반 기술은 볼륨 계층 내에서 사용되는 경우 저장소 복제본에서 지원됩니다. 저장소 복제본은 블록 기반 백업 및 복원을 지원하지 않습니다.

## <a name="FAQ14"></a> 대역폭 사용을 제한하도록 복제를 구성할 수 있습니까?
예, SMB 대역폭 제한을 사용하면 됩니다. 이는 모든 저장소 복제본 트래픽에 적용되는 전역 설정이므로 이 서버의 모든 복제에 영향을 줍니다. 일반적으로 이는 모든 볼륨 데이터를 전송해야 하는 저장소 복제본 초기 동기화 설정에만 필요합니다. 초기 동기화 후에 필요한 경우 네트워크 대역폭이 너무 낮아 IO 워크로드에 사용할 수 없으면 IO를 줄이거나 대역폭을 늘립니다.

이는 비동기 복제에만 사용해야 합니다(참고: 초기 동기화는 동기식을 지정한 경우에도 항상 비동기식임).
또한 네트워크 QoS 정책을 사용하여 저장소 복제본 트래픽을 구성할 수 있습니다. 일치율이 매우 높은 시드된 저장소 복제본 복제를 사용하는 경우에도 전체 초기 동기화 대역폭 사용량이 크게 줄어듭니다.


대역폭 제한을 설정하려면 다음을 사용합니다.

    Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x

대역폭 제한을 보려면 다음을 사용합니다.

    Get-SmbBandwidthLimit -Category StorageReplication

대역폭 제한을 제거하려면 다음을 사용합니다.

    Remove-SmbBandwidthLimit -Category StorageReplication
    
## <a name="FAQ15"></a>저장소 복제본에 필요한 네트워크 포트는 무엇입니까?
저장소 복제본은 복제 및 관리에 SMB와 WSMAN을 사용합니다. 즉, 다음 포트가 필요합니다.

   445(SMB - 복제 전송 프로토콜) 5445(iWARP SMB - iWARP RDMA 네트워킹을 사용하는 경우에만 필요) 5895 (WSManHTTP - WMI/CIM/PowerShell 관리 프로토콜)

참고: Test-SRTopology cmdlet에는 ICMPv4/ICMPv6가 필요하지만 복제나 관리에는 필요하지 않습니다.

## <a name="FAQ15"></a>어떤 것이 로그 볼륨 모범 사례입니까?
로그의 최적 크기는 환경과 워크로드에 따라 크게 달라지며, 워크로드가 수행하는 쓰기 IO의 양에 따라 결정됩니다. 

1.  로그가 더 크거나 작다고 해서 속도가 빨라지거나 느려지지 않습니다.
2.  예를 들어 더 큰 로그와 더 작은 로그는 10GB의 데이터 볼륨 대 10TB 데이터 볼륨에 미치는 영향이 다르지 않습니다.

로그가 더 크다는 것은 간단하게 없어지기 전에 더 많은 쓰기 IO를 수집하고 유지하는 것입니다. 이를 통해 네트워크 중단이나 대상이 오프라인되는 것과 같은 원본과 대상 컴퓨터 사이의 서비스 중단이 길어져도 그 피해가 줄어듭니다. 로그가 10시간의 쓰기를 보유하고 있고 네트워크가 2시간 동안 중단된 경우, 네트워크가 원본을 복구할 때 동기화되지 않은 차이점만 대상으로 매우 빠르게 복사하므로 매우 신속하게 다시 보호 상태를 유지할 수 있습니다. 로그가 10시간의 쓰기를 보유하고 있고 중단이 2일인 경우, 원본은 비트맵이라고 하는 다른 로그에서 복원되며 동기화 상태로 돌아가는 데 더 느립니다. 동기화되면 로그 사용으로 돌아갑니다.

로그가 회전되는 속도를 알려주는 SR 성능 카운터가 있어, 이를 통해 몇 가지 결정을 내릴 수 있습니다. 또한 Test-SRTopology cmdlet도 이 기능을 합니다. 기본적으로 기존 워크로드의 쓰기 IO를 보고 분, 시간, 일 단위로 얼마나 많은 IO가 로그를 지날지 결정합니다.

저장소 복제는 모든 쓰기 성능을 로그에 의존합니다. 로그 성능은 복제 성능에 매우 중요합니다. 로그가 모든 쓰기 IO를 직렬화하고 순차화하므로 로그 볼륨의 성능은 데이터 볼륨보다 좋아야 합니다. 로그 볼륨에는 항상 SSD와 같은 플래시 미디어를 사용해야 합니다. SQL 데이터베이스 로그 볼륨에서 다른 워크로드의 실행을 절대 허용하지 않은 것과 마찬가지로 로그 볼륨에서는 절대 다른 워크로드가 실행되지 않도록 해야 합니다. 

다시 강조: 로그 저장소는 데이터 저장소보다 빨라야 하며, 로그 볼륨은 다른 워크로드에 사용되지 않아야 합니다.

## <a name="FAQ16"></a> 확장 클러스터 토폴로지, 클러스터 간 토폴로지, 서버 간 토폴로지의 차이점은 무엇입니까?  
저장소 복제본의 세 가지 주요 구성은 확장 클러스터, 클러스터 간, 서버 간입니다. 각자 다른 장점을 가지고 있습니다.

확장 클러스터 토폴로지는 Hyper-V 사설 클라우드 클러스터, SQL Server FCI와 같이 오케스트레이션을 사용한 자동 장애 조치(failover)가 필요한 워크로드에 이상적입니다. 또한 장애 조치(Failover) 클러스터 관리자를 사용하는 기본 제공 그래픽 인터페이스도 있습니다. 이 구성은 영구 예약을 통해 저장소 공간, SAN, iSCSI, RAID의 기본 비대칭 클러스터 공유 저장소를 활용합니다. 이 구성은 2개 노드만으로도 실행할 수 있습니다.

클러스터 간 토폴로지는 두 개의 별도 클러스터를 사용하며 수동 장애 복구(failover)를 원하는 관리자에게 이상적입니다. 특히 두 번째 사이트가 재해 복구를 위해 준비되었으며 일상 업무에 사용되지 않는 경우에 좋습니다. 오케스트레이션은 수동입니다. 확장 클러스터와 달리, 이 구성에서는 저장소 공간 다이렉트를 사용할 수 있습니다. 이 구성은 4개 노드만으로도 실행할 수 있습니다. 

서버 간 토폴로지는 클러스터링할 수 없는 하드웨어를 실행하는 고객에 이상적입니다. 이 구성은 수동 장애 조치(failover)와 오케스트레이션이 필요합니다. 이는 지사와 중앙 데이터 센터 사이의 저렴한 배포에 이상적입니다. 특히 비동기 복제를 사용할 경우 유용합니다. 이 구성은 단일 마스터 재해 복구 시나리오를 위해 사용되는 DFSR 보호 파일 서버의 인스턴스를 종종 대체합니다.

모든 경우, 토폴로지는 물리적 하드웨어와 가상 컴퓨터에서 모두 실행할 수 있습니다. 가상 컴퓨터의 경우 기본 하이퍼바이저에 Hyper-V가 필요하지 않으며 VMware, KVM, Xen 등일 수 있습니다.

저장소 복제본에는 서버 자체 모드도 있는데, 이 모드에서는 동일한 컴퓨터의 두 다른 볼륨으로 복제 원본과 대상을 지정할 수 있습니다.

## <a name="FAQ17"></a> 저장소 복제본 또는 이 가이드의 문제를 보고하려면 어떻게 해야 합니까?  
저장소 복제본에 대한 기술 지원을 받으려면 [Microsoft TechNet 포럼](https://social.technet.microsoft.com/Forums/windowsserver/en-US/home?forum=WinServerPreview)에 게시하면 됩니다. 저장소 복제본에 대한 질문 또는 이 설명서에 대한 문제를 전자 메일(srfeed@microsoft.com)로 보낼 수도 있습니다. 디자인 변경 요청의 경우 https://windowsserver.uservoice.com 사이트가 권장되며 여기서 다른 고객으로부터 아이디어에 대한 지원 및 피드백을 받을 수 있습니다.



## <a name="related-topics"></a>관련 항목  
- [저장소 복제본 개요](storage-replica-overview.md) 
- [공유 저장소를 사용하여 확장 클러스터 복제](stretch-cluster-replication-using-shared-storage.md)  
- [서버 간 저장소 복제](server-to-server-storage-replication.md)  
- [클러스터 간 저장소 복제](cluster-to-cluster-storage-replication.md)  
- [저장소 복제본: 알려진 문제](storage-replica-known-issues.md)  

## <a name="see-also"></a>참고 항목  
- [저장소 개요](../storage.md)  
- [Windows Server 2016의 저장소 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)  
