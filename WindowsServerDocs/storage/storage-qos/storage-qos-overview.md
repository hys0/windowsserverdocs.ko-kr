---
title: 저장소 서비스 품질
ms.prod: windows-server
manager: dongill
ms.author: JGerend
ms.technology: storage-qos
ms.topic: get-started-article
ms.assetid: 8dcb8cf9-0e08-4fdd-9d7e-ec577ce8d8a0
author: kumudd
ms.date: 10/10/2016
ms.openlocfilehash: ed7d7ca4f41784f2ae12220eb2e30077e2467175
ms.sourcegitcommit: 056d355516f199e8a505c32b9aa685d0cde89e44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2020
ms.locfileid: "79518748"
---
# <a name="storage-quality-of-service"></a>저장소 서비스 품질

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

Windows Server 2016의 스토리지 서비스 품질(QoS)은 Hyper-V 및 스케일 아웃 파일 서버 역할을 사용하여 가상 컴퓨터의 스토리지 성능을 중앙에서 모니터링하고 관리하는 방법을 제공합니다. 이 기능은 동일한 파일 서버 클러스터를 사용하여 여러 가상 컴퓨터 간에 스토리지 리소스 공정성을 개선하며 정규화된 IOPS 단위로 정책 기반 최소 및 최대 성능 목표를 구성할 수 있도록 합니다.  

Windows Server 2016의 저장소 QoS를 사용하여 다음을 수행할 수 있습니다.  

-   **잡음이 있는 환경 문제를 완화 합니다.** 기본적으로 스토리지 QoS는 단일 가상 컴퓨터가 모든 스토리지 리소스를 사용하고 다른 가상 컴퓨터의 스토리지 대역폭을 소진할 수 없도록 합니다.  

-   **종단 간 저장소 성능을 모니터링 합니다.** 스케일 아웃 파일 서버에 저장된 가상 컴퓨터가 시작하는 즉시 해당 성능이 모니터링됩니다. 실행 중인 모든 가상 컴퓨터의 성능 정보와 스케일 아웃 파일 서버 클러스터의 구성을 단일 위치에서 볼 수 있습니다.  

-   **기업에 필요한 워크로드별 저장소 I/O 관리** 저장소 QoS 정책은 가상 컴퓨터에 대한 성능 최소값 및 최대값을 정의하고 이러한 값이 충족되는지 확인합니다. 이는 조밀한 환경 및 과도하게 프로비전된 환경에서도 가상 컴퓨터에 일관된 성능을 제공합니다. 정책을 충족할 수 없는 경우 VM이 정책을 벗어나거나 잘못된 정책이 할당되었을 때 경고를 추적할 수 있습니다.  

이 문서에서는 기업에서 새로운 저장소 QoS 기능을 활용하는 방법을 설명합니다. Windows Server, Windows Server 장애 조치(failover) 클러스터링, 스케일 아웃 파일 서버, Hyper-V 및 Windows PowerShell에 대한 이전 작업 지식이 있다고 가정합니다.

## <a name="BKMK_Overview"></a>설명은  
이 섹션에서는 저장소 QoS를 사용하기 위한 요구 사항, 저장소 QoS를 사용하는 소프트웨어 정의 솔루션의 개요 및 저장소 QoS 관련 용어 목록을 설명합니다.  

### <a name="BKMK_Requirements"></a>저장소 QoS 요구 사항  
저장소 QoS는 두 가지 배포 시나리오를 지원합니다.  

-   **스케일 아웃 파일 서버를 사용하는 Hyper-V** 이 시나리오에는 다음 두 클러스터가 모두 필요합니다.  

    -   스케일 아웃 파일 서버 클러스터인 저장소 클러스터  

    -   Hyper-V 역할을 사용하는 하나 이상의 서버가 있는 계산 클러스터  

    저장소 QoS의 경우 저장소 서버에 장애 조치(failover) 클러스터가 필요하지만 장애 조치(failover) 클러스터에 컴퓨팅 서버가 필요하지는 않습니다. 모든 서버(Storage 및 Compute 모두에 사용되는 서버)에서 Windows Server 2016을 실행해야 합니다.  

    평가용으로 배포된 스케일 아웃 파일 서버 클러스터가 없는 경우 기존 서버 또는 가상 컴퓨터를 사용하여 이를 구축하는 방법에 대한 단계별 지침은 [Windows Server 2012 R2 저장소: 저장소 공간, SMB 스케일 아웃 및 공유 VHDX(물리적)를 사용한 단계별 작업](https://blogs.technet.com/b/josebda/archive/2013/07/31/windows-server-2012-r2-storage-step-by-step-with-storage-spaces-smb-scale-out-and-shared-vhdx-physical.aspx)을 참조하세요.  

-   **클러스터 공유 볼륨을 사용 하는 hyper-v** 이 시나리오에는 다음 두 클러스터가 모두 필요합니다.  

    -   Hyper-V 역할을 사용하는 계산 클러스터  

    -   스토리지에 CSV(클러스터 공유 볼륨)를 사용하는 Hyper-V  

장애 조치(failover) 클러스터가 필요합니다. 모든 서버에서 동일한 버전의 Windows Server 2016을 실행해야 합니다.  

### <a name="BKMK_SolutionOverview"></a>소프트웨어 정의 저장소 솔루션에서 저장소 QoS 사용  
스토리지 서비스 품질은 스케일 아웃 파일 서버 및 Hyper-V에서 제공되는 Microsoft 소프트웨어 정의 스토리지 솔루션에 기본 제공됩니다. 스케일 아웃 파일 서버는 SMB3 프로토콜을 사용하여 Hyper-V 서버에 파일 공유를 노출합니다. 새로운 정책 관리자가 파일 서버 클러스터에 추가되어 중앙 스토리지 성능 모니터링을 제공합니다.  

![스케일 아웃 파일 서버와 저장소 QoS](media/overview-Clustering_SOFSStorageQoS.png)  

**그림 1: 스케일 아웃 파일 서버의 소프트웨어 정의 저장소 솔루션에서 저장소 QoS 사용**  

Hyper-V 서버에서 가상 컴퓨터를 시작하면 정책 관리자가 이를 모니터링합니다. 정책 관리자는 가상 컴퓨터의 성능을 적절히 제어하는 Hyper-V 서버에 저장소 QoS 정책과 모든 제한 또는 예약을 다시 전달합니다.  

저장소 QoS 정책 또는 가상 컴퓨터의 성능 요구 사항이 변경된 경우 정책 관리자는 동작을 조정하도록 Hyper-V 서버에 알립니다. 이 피드백 루프는 모든 가상 컴퓨터 VHD가 정의된 저장소 QoS 정책에 따라 일관성 있게 수행되도록 합니다.  

### <a name="BKMK_Glossary"></a>들은  

|용어|설명|  
|--------|---------------|  
|정규화된 IOPS|모든 스토리지 사용은 "정규화된 IOPS"로 측정됩니다.  이는 초당 스토리지 입력/출력 작업 수입니다.  8KB 이하인 IO는 하나의 정규화된 IO로 간주됩니다.  8KB보다 큰 모든 IO는 여러 개의 정규화된 IO로 처리됩니다. 예를 들어 256KB 요청은 32개의 정규화된 IOPS로 처리됩니다.<br /><br />Windows Server 2016에는 IO를 정규화하는 데 사용되는 크기를 지정할 수 있는 기능이 포함되어 있습니다.  스토리지 클러스터에서 정규화된 크기를 지정하여 전체 정규화 계산 클러스터에 적용할 수 있습니다.  기본값은 8KB입니다.|  
|흐름|Hyper-V Server에서 연 각 파일 핸들부터 VHD 또는 VHDX 파일까지가 "흐름"으로 간주됩니다. 가상 컴퓨터에 두 개의 가상 하드 디스크가 연결된 경우 파일당 파일 서버 클러스터로 하나의 흐름이 생성됩니다. VHDX가 여러 가상 컴퓨터와 공유하는 경우 가상 컴퓨터당 하나의 흐름이 생성됩니다.|  
|InitiatorName|각 흐름에 대해 스케일 아웃 파일 서버에 보고되는 가상 컴퓨터의 이름입니다.|  
|InitiatorID|가상 컴퓨터 ID와 일치하는 식별자입니다.  이는 가상 컴퓨터의 InitiatorName이 동일한 경우에도 항상 개별 흐름 가상 컴퓨터를 고유하게 식별하는 데 사용될 수 있습니다.|  
|정책|저장소 QoS 정책은 클러스터 데이터베이스에 저장되며 PolicyId, MinimumIOPS, MaximumIOPS, ParentPolicy 및 PolicyType 속성을 가집니다.|  
|PolicyId|정책의 고유 식별자입니다.  기본적으로 생성되지만 필요한 경우 지정할 수 있습니다.|  
|MinimumIOPS|정책에서 제공하는 최소 정규화된 IOPS입니다.  "예약"이라고도 합니다.|  
|MaximumIOPS|정책에서 제한하는 최대 정규화 IOPS입니다.  "제한"이라고도 합니다.|  
|집계 |지정된 MinimumIOPS 및 MaximumIOPS와 대역폭이 정책에 할당된 모든 흐름 간에 공유되는 정책 유형입니다. 해당 스토리지 시스템에 할당된 VHD의 모든 정책에는 공유할 수 있는 단일 I/O 대역폭 할당이 있습니다.|  
|Dedicated|지정된 Minimum 및 MaximumIOPs와 대역폭이 개별 VHD/VHDx에 대해 관리되는 정책 유형입니다.|  

## <a name="BKMK_SetUpQoS"></a>저장소 QoS를 설정 하 고 기본 성능을 모니터링 하는 방법  
이 섹션에서는 새 스토리지 QoS 기능을 사용하도록 설정하는 방법 및 사용자 지정 정책을 적용하지 않고 스토리지 성능을 모니터링하는 방법을 설명합니다.  

### <a name="BKMK_SetupStorageQoSonStorageCluster"></a>저장소 클러스터에서 저장소 QoS 설정  
이 섹션에서는 신규 또는 기존 장애 조치(failover) 클러스터와 Windows Server 2016를 실행하는 스케일 아웃 파일 서버에서 저장소 QoS를 사용하도록 설정하는 방법을 설명합니다.  

#### <a name="set-up-storage-qos-on-a-new-installation"></a>새로운 설치에 저장소 QoS 설정  
Windows Server 2016에서 새로운 장애 조치(failover) 클러스터 및 CSV(클러스터 공유 볼륨)를 구성한 경우 저장소 QoS 기능은 자동으로 설정됩니다.  

#### <a name="verify-storage-qos-installation"></a>저장소 QoS 설치 확인  
장애 조치(failover) 클러스터를 만들고 CSV 디스크를 구성한 후에는 **저장소 QoS 리소스**가 클러스터 코어 리소스로 표시되며 장애 조치(failover) 클러스터 관리자와 Windows PowerShell 모두에 표시됩니다. 이는 장애 조치(failover) 클러스터 시스템에서 이 리소스를 관리하도록 하여 이 리소스에 대해 아무 작업도 수행할 필요가 없도록 하기 위한 것입니다.  새로운 상태 서비스와 같은 다른 장애 조치(failover) 클러스터 시스템 리소스와 일관성을 유지하기 위해 장애 조치(Failover) 클러스터 관리자와 PowerShell 모두에 표시합니다.  

![저장소 QoS 리소스가 클러스터 코어 리소스에 표시됨](media/overview-Clustering_StorageQoSFCM.png)  

**그림 2: 장애 조치(Failover) 클러스터 관리자에서 클러스터 코어 리소스로 표시 되는 저장소 QoS 리소스**  

다음 PowerShell cmdlet을 사용하여 저장소 QoS 리소스의 상태를 볼 수 있습니다.  

```PowerShell  
PS C:\> Get-ClusterResource -Name "Storage Qos Resource"  

Name                   State      OwnerGroup        ResourceType                 
----                   -----      ----------        ------------                 
Storage Qos Resource   Online     Cluster Group     Storage QoS Policy Manager  
```  

### <a name="BKMK_SetupStorageQoSonComputeCluster"></a>계산 클러스터에서 저장소 QoS 설정  
Windows Server 2016의 Hyper-V 역할은 저장소 QoS에 대한 지원을 기본 제공하며 기본적으로 사용하도록 설정됩니다.  

#### <a name="install-remote-administration-tools-to-manage-storage-qos-policies-from-remote-computers"></a>원격 관리 도구를 설치하여 원격 컴퓨터에서 저장소 QoS 정책 관리  
원격 서버 관리 도구를 사용하여 컴퓨팅 호스트에서 흐름을 모니터링하고 저장소 QoS 정책을 관리할 수 있습니다.  이는 모든 Windows Server 2016 설치에서 선택적 기능으로 제공되며, [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=45520) 웹 사이트에서 Windows 10용으로 별도로 다운로드할 수 있습니다.

**RSAT-클러스터링** 선택적 기능에는 저장소 QoS를 포함하여 원격 관리 장애 조치(failover) 클러스터링용 Windows PowerShell 모듈이 포함됩니다.  

-   Windows PowerShell: Add-WindowsFeature RSAT-Clustering  

**RSAT-Hyper-V-Tools** 선택적 기능에는 Hyper-V의 원격 관리용 Windows PowerShell 모듈이 포함됩니다.  

-   Windows PowerShell: Add-WindowsFeature RSAT-Hyper-V-Tools  

#### <a name="deploy-virtual-machines-to-run-workloads-for-testing"></a>테스트를 위해 워크로드를 실행할 가상 컴퓨터 배포  
관련 워크로드가 있는 스케일 아웃 파일 서버에 일부 가상 컴퓨터를 저장해야 합니다.  권장 도구(DiskSpd) 및 몇 가지 사용 예를 포함하여 로드를 시뮬레이션하고 일부 스트레스 테스트를 수행하는 방법에 대한 몇 가지 팁은 [DiskSpd, PowerShell 및 스토리지 성능: 로컬 디스크와 SMB 파일 공유에 대한 IOPS, 처리량 및 대기 시간 측정](https://blogs.technet.com/b/josebda/archive/2014/10/13/diskspd-powershell-and-storage-performance-measuring-iops-throughput-and-latency-for-both-local-disks-and-smb-file-shares.aspx)을 참조하세요.  

이 가이드에 표시된 시나리오 예에는 5개의 가상 컴퓨터가 포함되어 있습니다. BuildVM1, BuildVM2, BuildVM3 및 BuildVM4는 스토리지 수요가 낮거나 보통인 데스크톱 워크로드를 실행합니다. TestVm1은 스토리지 수요가 높은 온라인 트랜잭션 처리 벤치마크를 실행합니다.  

### <a name="view-current-storage-performance-metrics"></a>현재 스토리지 성능 메트릭 보기  
이 섹션의 내용은 다음과 같습니다.  

-   `Get-StorageQosFlow` cmdlet을 사용하여 흐름을 쿼리하는 방법  

-   `Get-StorageQosVolume` cmdlet을 사용하여 볼륨 성능을 확인하는 방법  

#### <a name="query-flows-using-the-get-storageqosflow-cmdlet"></a>Get-StorageQosFlow cmdlet을 사용하여 흐름 쿼리  

Get-StorageQosFlow cmdlet은 Hyper-V Server에서 시작된 모든 현재 흐름을 보여 줍니다. 모든 데이터가 스케일 아웃 파일 서버 클러스터에서 수집되므로 스케일 아웃 파일 서버 클러스터의 모든 노드 또는 원격 서버(-CimSession 매개 변수 사용)에 대해 cmdlet을 사용할 수 있습니다.  

**다음 샘플 명령은 Get-StorageQoSFlow를 사용하여 서버에서 Hyper-V가 연 모든 파일을 보는 방법을 보여 줍니다**.  

```PowerShell
PS C:\> Get-StorageQosFlow  

InitiatorName    InitiatorNodeNam StorageNodeName  FilePath        Status  
                 e  
-------------    ---------------- ---------------  --------        ------  
                                  plang-fs3.pla... C:\ClusterSt... Ok  
                                  plang-fs2.pla... C:\ClusterSt... Ok  
                                  plang-fs1.pla... C:\ClusterSt... Ok  
                                  plang-fs3.pla... C:\ClusterSt... Ok  
                                  plang-fs2.pla... C:\ClusterSt... Ok  
                                  plang-fs1.pla... C:\ClusterSt... Ok  
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok  
BuildVM4         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok  
WinOltp1         plang-c1.plan... plang-fs1.pla... C:\ClusterSt... Ok  
BuildVM3         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok  
BuildVM1         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok  
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok  
BuildVM2         plang-c2.plan... plang-fs1.pla... C:\ClusterSt... Ok  
TR20-VMM         plang-z400.pl... plang-fs1.pla... C:\ClusterSt... Ok  
                                  plang-fs3.pla... C:\ClusterSt... Ok  
                                  plang-fs2.pla... C:\ClusterSt... Ok  
BuildVM4         plang-c2.plan... plang-fs2.pla... C:\ClusterSt... Ok  
WinOltp1         plang-c1.plan... plang-fs2.pla... C:\ClusterSt... Ok  
BuildVM3         plang-c2.plan... plang-fs2.pla... C:\ClusterSt... Ok  
WinOltp1         plang-c1.plan... plang-fs2.pla... C:\ClusterSt... Ok  
                                  plang-fs1.pla... C:\ClusterSt... Ok  
```  

다음 샘플 명령은 가상 컴퓨터 이름, Hyper-V 호스트 이름, IOPS 및 VHD 파일 이름을 IOPS별로 정렬하여 보여 주도록 서식이 지정되었습니다.  

```PowerShell  
PS C:\> Get-StorageQosFlow | Sort-Object StorageNodeIOPs -Descending | ft InitiatorName, @{Expression={$_.InitiatorNodeName.Substring(0,$_.InitiatorNodeName.IndexOf('.'))};Label="InitiatorNodeName"}, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName InitiatorNodeName StorageNodeIOPs Status File  
------------- ----------------- --------------- ------ ----  
WinOltp1      plang-c1                     3482     Ok IOMETER.VHDX  
BuildVM2      plang-c2                      544     Ok BUILDVM2.VHDX  
BuildVM1      plang-c2                      497     Ok BUILDVM1.VHDX  
BuildVM4      plang-c2                      316     Ok BUILDVM4.VHDX  
BuildVM3      plang-c2                      296     Ok BUILDVM3.VHDX  
BuildVM4      plang-c2                      195     Ok WIN8RTM_ENTERPRISE_VL_BU...  
TR20-VMM      plang-z400                    156     Ok DATA1.VHDX  
BuildVM3      plang-c2                       81     Ok WIN8RTM_ENTERPRISE_VL_BU...  
WinOltp1      plang-c1                       65     Ok BOOT.VHDX  
                                             18     Ok DefaultFlow  
                                             12     Ok DefaultFlow  
WinOltp1      plang-c1                        4     Ok 9914.0.AMD64FRE.WINMAIN....  
TR20-VMM      plang-z400                      4     Ok DATA2.VHDX  
TR20-VMM      plang-z400                      3     Ok BOOT.VHDX  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
                                              0     Ok DefaultFlow  
```  

다음 샘플 명령은 특정 가상 컴퓨터에 대한 스토리지 성능 및 설정을 쉽게 찾을 수 있도록 InitiatorName에 따라 흐름을 필터링하는 방법을 보여 줍니다.  

```PowerShell
PS C:\> Get-StorageQosFlow -InitiatorName BuildVm1 | Format-List

FilePath           : C:\ClusterStorage\Volume2\SHARES\TWO\BUILDWORKLOAD\BUILDVM1.V  
                     HDX  
FlowId             : ebfecb54-e47a-5a2d-8ec0-0940994ff21c  
InitiatorId        : ae4e3dd0-3bde-42ef-b035-9064309e6fec  
InitiatorIOPS      : 464  
InitiatorLatency   : 26.2684  
InitiatorName      : BuildVM1  
InitiatorNodeName  : plang-c2.plang.nttest.microsoft.com  
Interval           : 300000  
Limit              : 500  
PolicyId           : b145e63a-3c9e-48a8-87f8-1dfc2abfe5f4  
Reservation        : 500  
Status             : Ok  
StorageNodeIOPS    : 475  
StorageNodeLatency : 7.9725  
StorageNodeName    : plang-fs1.plang.nttest.microsoft.com  
TimeStamp          : 2/12/2015 2:58:49 PM  
VolumeId           : 4d91fc3a-1a1e-4917-86f6-54853b2a6787  
PSComputerName     :  
MaximumIops        : 500  
MinimumIops        : 500  
```  

`Get-StorageQosFlow` cmdlet에서 반환되는 데이터에는 다음이 포함됩니다.  

-   Hyper-V 호스트 이름(InitiatorNodeName)  

-   가상 컴퓨터의 이름 및 해당 ID(InitiatorName 및 InitiatorId)  

-   Hyper-V 호스트에서 관찰된 가상 디스크의 최근 평균 성능(InitiatorIOPS, InitiatorLatency)  

-   저장소 클러스터에서 관찰된 가상 디스크의 최근 평균 성능(StorageNodeIOPS, StorageNodeLatency)  

-   파일에 적용되는 현재 정책(있는 경우) 및 결과 구성(PolicyId, Reservation, Limit)  

-   정책 상태  

    -   **Ok** - 문제가 없습니다.  

    -   InsufficientThroughput - 정책이 적용되지만 최소 IOPS를 배달할 수 없습니다.  하나의 VM 또는 모든 VM에 대한 최소값이 스토리지 볼륨에서 배달할 수 있는 것보다 큰 경우에 발생할 수 있습니다.  

    -   **UnknownPolicyId** - Hyper-V 호스트의 가상 컴퓨터에 정책이 할당되었지만 파일 서버에 없습니다.  이 정책을 가상 컴퓨터 구성에서 제거하거나 파일 서버 클러스터에서 일치하는 정책을 만들어야 합니다.  

#### <a name="view-performance-for-a-volume-using-get-storageqosvolume"></a>Get-StorageQosVolume을 사용하여 볼륨 성능 보기  
흐름별 성능 메트릭 외에 스토리지 볼륨 수준별 스토리지 성능 메트릭도 수집됩니다.  이를 통해 정규화된 IOPS의 평균 총 사용률, 대기 시간 및 볼륨에 적용되는 집계 제한 및 예약을 쉽게 확인할 수 있습니다.  

```PowerShell
PS C:\> Get-StorageQosVolume | Format-List  

Interval       : 300000  
IOPS           : 0  
Latency        : 0  
Limit          : 0  
Reservation    : 0  
Status         : Ok  
TimeStamp      : 2/12/2015 2:59:38 PM  
VolumeId       : 434f561f-88ae-46c0-a152-8c6641561504  
PSComputerName :  
MaximumIops    : 0  
MinimumIops    : 0  

Interval       : 300000  
IOPS           : 1097  
Latency        : 3.1524  
Limit          : 0  
Reservation    : 1568  
Status         : Ok  
TimeStamp      : 2/12/2015 2:59:38 PM  
VolumeId       : 4d91fc3a-1a1e-4917-86f6-54853b2a6787  
PSComputerName :  
MaximumIops    : 0  
MinimumIops    : 1568  

Interval       : 300000  
IOPS           : 5354  
Latency        : 6.5084  
Limit          : 0  
Reservation    : 781  
Status         : Ok  
TimeStamp      : 2/12/2015 2:59:38 PM  
VolumeId       : 0d2fd367-8d74-4146-9934-306726913dda  
PSComputerName :  
MaximumIops    : 0  
MinimumIops    : 781  
```  

## <a name="BKMK_CreateQoSPolicies"></a>저장소 QoS 정책을 만들고 모니터링 하는 방법  
이 섹션에는 스토리지 QoS 정책을 만들고, 이러한 정책을 가상 컴퓨터에 적용하고, 정책이 적용된 후 스토리지 클러스터를 모니터링하는 방법을 설명합니다.  

### <a name="create-storage-qos-policies"></a>저장소 QoS 정책 만들기  
저장소 QoS 정책은 스케일 아웃 파일 서버 클러스터에서 정의 및 관리됩니다.  유연한 배포를 위해 필요한 만큼 정책을 만들 수 있습니다(스토리지 클러스터당 최대 10,000개).  

정책을 사용하여 가상 컴퓨터에 할당된 각 VHD/VHDX 파일을 구성할 수 있습니다. 여러 파일 및 가상 컴퓨터에서 동일한 정책을 사용하거나 각각 별도의 정책으로 구성할 수 있습니다.  여러 VHD/VHDX 파일 또는 여러 가상 컴퓨터가 동일한 정책을 사용하도록 구성된 경우에는 함께 집계되며 MinimumIOPS 및 MaximumIOPS를 공평하게 공유합니다. 여러 VHD/VHDX 파일 또는 가상 컴퓨터에 별도의 정책을 사용하는 경우에는 각각에 대해 최소값 및 최대값이 별도로 추적됩니다.  

서로 다른 가상 컴퓨터에 대해 유사한 여러 정책을 만들고 가상 컴퓨터의 스토리지 수요가 동일한 경우에는 유사한 IOPS 공유가 제공됩니다.  하나의 VM에 더 많이 필요하고 다른 VM에 덜 필요한 경우에는 IOPS가 해당 수요를 따릅니다.  

### <a name="types-of-storage-qos-policies"></a>저장소 QoS 정책 유형  
집계(이전의 SingleInstance)와 전용(이전의 MultiInstance) 두 가지 정책 유형이 있습니다. 집계 정책은 VHD/VHDX 파일과 가상 컴퓨터의 조합된 집합에 대한 최대값 및 최소값을 적용합니다. 실제로 지정된 집합의 IOPS 및 대역폭을 공유합니다. 전용 정책은 각 VHD/VHDx에 대해 최소값 및 최대값을 별도로 적용합니다. 따라서 여러 VHD/VHDx 파일에 유사한 제한을 적용하는 단일 정책을 쉽게 만들 수 있습니다.  

예를 들어 최소값이 300 IOPS이고 최대값이 500 IOPS인 집계 정책을 만들고 이 정책을 5개의 VHD/VHDx 파일에 적용한 경우 5개의 조합된 VHD/VHDx 파일은 최소 300 IOPS(수요가 있고 스토리지 시스템에서 해당 성능을 제공할 수 있는 경우)와 최대 500 IOPS 사이에서 보장됩니다. VHD/VHDx 파일의 IOPS 수요가 유사하게 높고 스토리지 시스템에서 이를 유지할 수 있는 경우 각 VHD/VHDx 파일에는 약 100 IOPS가 제공됩니다.  

그러나 유사한 제한이 있는 전용 정책을 만들어 5개의 가상 컴퓨터에 있는 VHD/VHDx 파일에 적용한 경우 각 가상 컴퓨터에는 300~500 IOPS가 제공됩니다. 가상 컴퓨터의 IOPS 수요가 유사하게 높고 스토리지 시스템에서 이를 유지할 수 있는 경우 각 가상 컴퓨터에는 약 500 IOPS가 제공됩니다. .  가상 컴퓨터 중 하나에 동일한 MulitInstance 정책이 구성된 여러 VHD/VHDx 파일이 있는 경우 VM의 전체 IO가 제한을 초과하지 않도록 제한을 공유합니다.  

따라서 동일한 성능 특성을 가지고 여러 개의 유사한 정책을 쉽게 만들려는 VHD/VHDx 파일 그룹이 있는 경우 단일 전용 정책을 사용하여 각 가상 컴퓨터의 파일에 적용할 수 있습니다.

단일 집계 정책에 할당 된 VHD/VHDx 파일의 수를 20 개 이하로 유지 합니다.  이 정책 유형은 클러스터에서 몇 개의 Vm을 사용 하 여 집계를 수행 하기 위한 것입니다.

### <a name="create-and-apply-a-dedicated-policy"></a>전용 정책 만들기 및 적용  
먼저 `New-StorageQosPolicy` cmdlet을 사용하여 다음 예와 같이 스케일 아웃 파일 서버에서 정책을 만듭니다.  

```PowerShell
$desktopVmPolicy = New-StorageQosPolicy -Name Desktop -PolicyType Dedicated -MinimumIops 100 -MaximumIops 200  
```  

그런 다음 Hyper-V Server에서 적절한 가상 컴퓨터의 하드 디스크 드라이브에 이 정책을 적용합니다.  이전 단계의 PolicyId를 적어 두거나 스크립트에 변수로 저장합니다.  

스케일 아웃 파일 서버에서 PowerShell을 사용하여 다음 예와 같이 저장소 QoS 정책을 만들고 해당 정책 ID를 가져옵니다.  

```PowerShell
PS C:\> $desktopVmPolicy = New-StorageQosPolicy -Name Desktop -PolicyType Dedicated -MinimumIops 100 -MaximumIops 200  

C:\> $desktopVmPolicy.PolicyId  

Guid  
----  
cd6e6b87-fb13-492b-9103-41c6f631f8e0  
```  

Hyper-V Server에서 PowerShell을 사용하여 다음 예와 같이 정책 ID를 사용하여 저장소 QoS 정책을 설정합니다.  

```PowerShell
Get-VM -Name Build* | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID cd6e6b87-fb13-492b-9103-41c6f631f8e0  
```  

### <a name="confirm-that-the-policies-are-applied"></a>정책이 적용되는지 확인  
`Get-StorageQosFlow` PowerShell cmdlet을 사용하여 다음 예와 같이 MinimumIOPs 및 MaximumIOPs가 적절한 흐름에 적용되는지 확인합니다.  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName |  
 ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName Status MinimumIops MaximumIops StorageNodeIOPs Status File  
------------- ------ ----------- ----------- --------------- ------ ----  
BuildVM1          Ok         100         200             250     Ok BUILDVM1.VHDX  
BuildVM2          Ok         100         200             251     Ok BUILDVM2.VHDX  
BuildVM3          Ok         100         200             252     Ok BUILDVM3.VHDX  
BuildVM4          Ok         100         200             233     Ok BUILDVM4.VHDX  
TR20-VMM          Ok          33         666               1     Ok DATA2.VHDX  
TR20-VMM          Ok          33         666               5     Ok DATA1.VHDX  
TR20-VMM          Ok          33         666               4     Ok BOOT.VHDX  
WinOltp1          Ok           0           0               0     Ok 9914.0.AMD6...  
WinOltp1          Ok           0           0            5166     Ok IOMETER.VHDX  
WinOltp1          Ok           0           0               0     Ok BOOT.VHDX  
```  

Hyper-V Server에서는 제공된 스크립트 **Get-VMHardDiskDrivePolicy.ps1**을 사용하여 가상 하드 디스크 드라이브에 적용되는 정책을 확인할 수도 있습니다.  

```PowerShell
PS C:\> Get-VM -Name BuildVM1 | Get-VMHardDiskDrive | Format-List  

Path                          : \\plang-fs.plang.nttest.microsoft.com\two\BuildWorkload  
                                \BuildVM1.vhdx  
DiskNumber                    :  
MaximumIOPS                   : 0  
MinimumIOPS                   : 0  
QoSPolicyID                   : cd6e6b87-fb13-492b-9103-41c6f631f8e0  
SupportPersistentReservations : False  
ControllerLocation            : 0  
ControllerNumber              : 0  
ControllerType                : IDE  
PoolName                      : Primordial  
Name                          : Hard Drive  
Id                            : Microsoft:AE4E3DD0-3BDE-42EF-B035-9064309E6FEC\83F8638B  
                                -8DCA-4152-9EDA-2CA8B33039B4\0\0\D  
VMId                          : ae4e3dd0-3bde-42ef-b035-9064309e6fec  
VMName                        : BuildVM1  
VMSnapshotId                  : 00000000-0000-0000-0000-000000000000  
VMSnapshotName                :  
ComputerName                  : PLANG-C2  
IsDeleted                     : False  
```  

### <a name="query-for-storage-qos-policies"></a>저장소 QoS 정책 쿼리  
`Get-StorageQosPolicy`는 구성 된 모든 정책과 스케일 아웃 파일 서버에 대 한 상태를 나열 합니다.  

```PowerShell
PS C:\> Get-StorageQosPolicy  

Name                 MinimumIops          MaximumIops          Status  
----                 -----------          -----------          ------  
Default              0                    0                    Ok  
Limit500             0                    500                  Ok  
SilverVm             500                  500                  Ok  
Desktop              100                  200                  Ok  
Limit500             0                    0                    Ok  
VMM                  100                  2000                 Ok  
Vdi                  1                    100                  Ok  
```  

상태는 시스템 작동 상태에 따라 시간이 지나면서 변경될 수 있습니다.  

-   **Ok** - 해당 정책을 사용하는 모든 흐름에 요청된 MinimumIOPs가 제공됩니다.  

-   **InsufficientThroughput** - 이 정책을 사용하는 하나 이상의 흐름에 Minimum IOPs가 제공되지 않습니다.  

또한 다음과 같이 `Get-StorageQosPolicy`에 정책을 파이프하여 정책을 사용하도록 구성된 모든 흐름의 상태를 가져올 수 있습니다.  

```PowerShell
PS C:\> Get-StorageQosPolicy -Name Desktop | Get-StorageQosFlow | ft InitiatorName, *IOPS, Status, FilePath -AutoSize  

InitiatorName MaximumIops MinimumIops InitiatorIOPS StorageNodeIOPS Status FilePat  
                                                                           h  
------------- ----------- ----------- ------------- --------------- ------ -------  
BuildVM4              100          50           187              17     Ok C:\C...  
BuildVM3              100          50           194              25     Ok C:\C...  
BuildVM1              200         100           195             196     Ok C:\C...  
BuildVM2              200         100           193             192     Ok C:\C...  
BuildVM4              200         100           187             169     Ok C:\C...  
BuildVM3              200         100           194             169     Ok C:\C...  
```  

### <a name="create-an-aggregated-policy"></a>집계 정책 만들기  
여러 가상 하드 디스크가 단일 IOPS 및 대역폭 풀을 공유하도록 하려는 경우 집계 정책을 사용할 수 있습니다.  예를 들어 두 가상 컴퓨터의 하드 디스크에 동일한 집계 정책을 적용하는 경우 수요에 따라 최소값이 분할됩니다.  두 디스크 모두 조합된 최소값이 보장되며, 합계가 지정된 최대 IOPS 또는 대역폭을 초과하지 않습니다.  

같은 방법을 사용하여 하나의 서비스를 구성하거나 다중 호스트 환경의 테넌트에 속한 가상 컴퓨터에 대한 모든 VHD/VHDx 파일에 단일 할당을 제공할 수도 있습니다.  

전용 정책과 집계 정책을 만드는 프로세스에는 지정되는 PolicyType 외에 차이점이 없습니다.  

다음 예에서는 집계 저장소 QoS 정책을 만들고 스케일 아웃 파일 서버에서 해당 policyID를 가져오는 방법을 보여 줍니다.  

```PowerShell
PS C:\> $highPerf = New-StorageQosPolicy -Name SqlWorkload -MinimumIops 1000 -MaximumIops 5000 -PolicyType Aggregated  
[plang-fs]: PS C:\Users\plang\Documents> $highPerf.PolicyId  

Guid  
----  
7e2f3e73-1ae4-4710-8219-0769a4aba072  
```  

다음 예에서는 위 예에서 가져온 policyID를 사용하여 Hyper-V Server에서 저장소 QoS 정책을 적용하는 방법을 보여 줍니다.  

```PowerShell
PS C:\> Get-VM -Name WinOltp1 | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID 7e2f3e73-1ae4-4710-8219-0769a4aba072  
```  

다음 예에서는 파일 서버에서 저장소 QoS 정책의 효과를 확인하는 방법을 보여 줍니다.  

```PowerShell
PS C:\> Get-StorageQosFlow -InitiatorName WinOltp1 | format-list InitiatorName, PolicyId, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, FilePath  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 250  
MaximumIops     : 1250  
StorageNodeIOPs : 0  
FilePath        : C:\ClusterStorage\Volume2\SHARES\TWO\BASEVHD\9914.0.AMD64FRE.WIN  
                  MAIN.141218-1718_SERVER_SERVERDATACENTER_EN-US.VHDX  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 250  
MaximumIops     : 1250  
StorageNodeIOPs : 0  
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\BOOT.VHDX  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 1000  
MaximumIops     : 5000  
StorageNodeIOPs : 4550  
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX  
PS C:\> Get-StorageQosFlow -InitiatorName WinOltp1 | for  
mat-list InitiatorName, PolicyId, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, FilePath  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 250  
MaximumIops     : 1250  
StorageNodeIOPs : 0  
FilePath        : C:\ClusterStorage\Volume2\SHARES\TWO\BASEVHD\9914.0.AMD64FRE.WIN  
                  MAIN.141218-1718_SERVER_SERVERDATACENTER_EN-US.VHDX  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 250  
MaximumIops     : 1250  
StorageNodeIOPs : 0  
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\BOOT.VHDX  

InitiatorName   : WinOltp1  
PolicyId        : 7e2f3e73-1ae4-4710-8219-0769a4aba072  
MinimumIops     : 1000  
MaximumIops     : 5000  
StorageNodeIOPs : 4550  
FilePath        : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX  
```  

각 가상 하드 디스크에는 해당 로드에 따라 조정된 MinimumIOPs 및 MaximumIOPs 값과 MaximumIobandwidth 값이 있습니다.  따라서 디스크 그룹에 사용되는 총 대역폭 양이 정책에 정의된 범위 내에서 유지됩니다.  위 예에서는 처음 두 개의 디스크가 유휴 상태이므로 세 번째 디스크에서 최대 MaximumIOPs를 사용할 수 있습니다.  처음 두 개의 디스크가 IO를 다시 실행하기 시작하면 세 번째 디스크의 MaximumIOPs가 자동으로 감소합니다.  

### <a name="modify-an-existing-policy"></a>기존 정책 수정  
정책을 만든 후 Name, MinimumIOPs, MaximumIOPs 및 MaximumIoBandwidth 속성을 변경할 수 있습니다.  그러나 정책 유형(집계/전용)은 정책을 만든 후 변경할 수 없습니다.  

다음 Windows PowerShell cmdlet에서는 기존 정책에 대한 MaximumIOPs 속성을 변경하는 방법을 보여 줍니다.  

```PowerShell
[DBG]: PS C:\demoscripts>> Get-StorageQosPolicy -Name SqlWorkload | Set-StorageQosPolicy -MaximumIops 6000  
```  

다음 cmdlet에서는 변경 내용을 확인합니다.  

```PowerShell
PS C:\> Get-StorageQosPolicy -Name SqlWorkload  

Name                    MinimumIops            MaximumIops            Status  
----                    -----------            -----------            ------  
SqlWorkload             1000                   6000                   Ok    

[plang-fs1]: PS C:\Users\plang\Documents> Get-StorageQosPolicy -Name SqlWorkload | Get-Storag  
eQosFlow | Format-Table InitiatorName, PolicyId, MaximumIops, MinimumIops, StorageNodeIops -A  
utoSize  

InitiatorName PolicyId                             MaximumIops MinimumIops StorageNodeIops  
------------- --------                             ----------- ----------- ---------------  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        1500         250               0  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        1500         250               0  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072        6000        1000            4507  
```  

## <a name="BKMK_KnownIssues"></a>일반적인 문제를 식별 하 고 해결 하는 방법  
이 섹션에서는 잘못된 저장소 QoS 정책을 사용하는 가상 컴퓨터를 찾는 방법, 일치하는 정책을 다시 만드는 방법, 가상 컴퓨터에서 정책을 제거하는 방법 및 저장소 QoS 정책 요구 사항을 충족하지 않는 가상 컴퓨터를 식별하는 방법을 설명합니다.  

### <a name="BKMK_FindingVMsWithInvalidPolicies"></a>잘못 된 정책이 있는 가상 컴퓨터 식별  

가상 컴퓨터에서 파일 서버를 제거하기 전에 파일 서버에서 정책이 삭제된 경우 가상 컴퓨터는 적용된 정책이 없는 것처럼 계속 실행됩니다.  

```PowerShell
PS C:\> Get-StorageQosPolicy -Name SqlWorkload | Remove-StorageQosPolicy  

Confirm  
Are you sure you want to perform this action?  
Performing the operation "DeletePolicy" on target "MSFT_StorageQoSPolicy (PolicyId =  
"7e2f3e73-1ae4-4710-8219-0769a4aba072")".  
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [?] Help (default is "Y"):  
```  

이제 흐름 상태가 "UnknownPolicyId"로 표시됩니다.  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName          Status MinimumIops MaximumIops StorageNodeIOPs          Status File  
-------------          ------ ----------- ----------- ---------------          ------ ----  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0              10              Ok Def...  
                           Ok           0           0              13              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
                           Ok           0           0               0              Ok Def...  
BuildVM1                   Ok         100         200             193              Ok BUI...  
BuildVM2                   Ok         100         200             196              Ok BUI...  
BuildVM3                   Ok          50          64              17              Ok WIN...  
BuildVM3                   Ok          50         136             179              Ok BUI...  
BuildVM4                   Ok          50         100              23              Ok WIN...  
BuildVM4                   Ok         100         200             173              Ok BUI...  
TR20-VMM                   Ok          33         666               2              Ok DAT...  
TR20-VMM                   Ok          25         975               3              Ok DAT...  
TR20-VMM                   Ok          75        1025              12              Ok BOO...  
WinOltp1      UnknownPolicyId           0           0               0 UnknownPolicyId 991...  
WinOltp1      UnknownPolicyId           0           0            4926 UnknownPolicyId IOM...  
WinOltp1      UnknownPolicyId           0           0               0 UnknownPolicyId BOO...  
```  

#### <a name="BKMK_RecreateMatchingPolicy"></a>일치 하는 저장소 QoS 정책 다시 만들기  
실수로 정책을 제거한 경우 이전 PolicyId를 사용하여 새 정책을 만들 수 있습니다.  먼저 필요한 PolicyId를 가져옵니다.  

```PowerShell
PS C:\> Get-StorageQosFlow -Status UnknownPolicyId | ft InitiatorName, PolicyId -AutoSize  

InitiatorName PolicyId  
------------- --------  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072  
WinOltp1      7e2f3e73-1ae4-4710-8219-0769a4aba072  
```  

그런 다음 해당 PolicyId를 사용하여 새 정책을 만듭니다.  

```PowerShell
PS C:\> New-StorageQosPolicy -PolicyId 7e2f3e73-1ae4-4710-8219-0769a4aba072 -PolicyType Aggregated -Name RestoredPolicy -MinimumIops 100 -MaximumIops 2000  

Name                    MinimumIops            MaximumIops            Status  
----                    -----------            -----------            ------  
RestoredPolicy          100                    2000                   Ok  
```  

마지막으로 정책이 적용되었는지 확인합니다.  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, Status, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName Status MinimumIops MaximumIops StorageNodeIOPs Status File  
------------- ------ ----------- ----------- --------------- ------ ----  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               8     Ok DefaultFlow  
                  Ok           0           0               9     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
                  Ok           0           0               0     Ok DefaultFlow  
BuildVM1          Ok         100         200             192     Ok BUILDVM1.VHDX  
BuildVM2          Ok         100         200             193     Ok BUILDVM2.VHDX  
BuildVM3          Ok          50         100              24     Ok WIN8RTM_ENTERPRISE_VL...  
BuildVM3          Ok         100         200             166     Ok BUILDVM3.VHDX  
BuildVM4          Ok          50         100              12     Ok WIN8RTM_ENTERPRISE_VL...  
BuildVM4          Ok         100         200             178     Ok BUILDVM4.VHDX  
TR20-VMM          Ok          33         666               2     Ok DATA2.VHDX  
TR20-VMM          Ok          33         666               2     Ok DATA1.VHDX  
TR20-VMM          Ok          33         666              10     Ok BOOT.VHDX  
WinOltp1          Ok          25         500               0     Ok 9914.0.AMD64FRE.WINMA...  
```  

#### <a name="BKMK_RemovePolicyFromVM"></a>저장소 QoS 정책 제거  

정책을 의도적으로 제거하거나 필요 없는 정책을 사용하여 VM을 가져온 경우 제거할 수 있습니다.  

```PowerShell
PS C:\> Get-VM -Name WinOltp1 | Get-VMHardDiskDrive | Set-VMHardDiskDrive -QoSPolicyID $null  
```  

PolicyId를 가상 하드 디스크 설정에서 제거하면 상태가 "Ok"로 변경되고 최소값 또는 최대값이 적용되지 않게 됩니다.  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName MinimumIops MaximumIops StorageNodeIOPs Status File  
------------- ----------- ----------- --------------- ------ ----  
                        0           0               0     Ok DefaultFlow  
                        0           0              16     Ok DefaultFlow  
                        0           0              12     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
                        0           0               0     Ok DefaultFlow  
BuildVM1              100         200             197     Ok BUILDVM1.VHDX  
BuildVM2              100         200             192     Ok BUILDVM2.VHDX  
BuildVM3                9           9              23     Ok WIN8RTM_ENTERPRISE_VL_BUILDW...  
BuildVM3               91         191             171     Ok BUILDVM3.VHDX  
BuildVM4                8           8              18     Ok WIN8RTM_ENTERPRISE_VL_BUILDW...  
BuildVM4               92         192             163     Ok BUILDVM4.VHDX  
TR20-VMM               33         666               2     Ok DATA2.VHDX  
TR20-VMM               33         666               1     Ok DATA1.VHDX  
TR20-VMM               33         666               5     Ok BOOT.VHDX  
WinOltp1                0           0               0     Ok 9914.0.AMD64FRE.WINMAIN.1412...  
WinOltp1                0           0            1811     Ok IOMETER.VHDX  
WinOltp1                0           0               0     Ok BOOT.VHDX  
```  

### <a name="BKMK_VMsThatDoNotMeetStorageQoSPoilicies"></a>저장소 QoS 정책을 충족 하지 않는 가상 머신 찾기  
**InsufficientThroughput** 상태는 다음 흐름에 할당됩니다.  

-   정책에 설정된 최소 IOPS가 정의된 흐름  

-   최소값을 충족하거나 초과하는 속도로 IO를 시작하는 흐름  

-   최소 IOP 속도에 도달하지 않은 흐름  

```PowerShell
PS C:\> Get-StorageQoSflow | Sort-Object InitiatorName | ft InitiatorName, MinimumIOPs, MaximumIOPs, StorageNodeIOPs, Status, @{Expression={$_.FilePath.Substring($_.FilePath.LastIndexOf('\')+1)};Label="File"} -AutoSize  

InitiatorName MinimumIops MaximumIops StorageNodeIOPs                 Status File  
------------- ----------- ----------- ---------------                 ------ ----  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0              15                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
                        0           0               0                     Ok DefaultFlow  
BuildVM3               50         100              20                     Ok WIN8RTM_ENTE...  
BuildVM3              100         200             174                     Ok BUILDVM3.VHDX  
BuildVM4               50         100              11                     Ok WIN8RTM_ENTE...  
BuildVM4              100         200             188                     Ok BUILDVM4.VHDX  
TR20-VMM               33         666               3                     Ok DATA1.VHDX  
TR20-VMM               78        1032             180                     Ok BOOT.VHDX  
TR20-VMM               22         968               4                     Ok DATA2.VHDX  
WinOltp1             3750        5000               0                     Ok 9914.0.AMD64...  
WinOltp1            15000       20000           11679 InsufficientThroughput IOMETER.VHDX  
WinOltp1             3750        5000               0                     Ok BOOT.VHDX  
```  

다음 예와 같이 **InsufficientThroughput**을 비롯한 모든 상태에 대해 흐름을 확인할 수 있습니다.  

```PowerShell
PS C:\> Get-StorageQosFlow -Status InsufficientThroughput | fl  

FilePath           : C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX  
FlowId             : 1ca356ff-fd33-5b5d-b60a-2c8659dc803e  
InitiatorId        : 2ceabcef-2eba-4f1b-9e66-10f960b50bbf  
InitiatorIOPS      : 12168  
InitiatorLatency   : 22.983  
InitiatorName      : WinOltp1  
InitiatorNodeName  : plang-c1.plang.nttest.microsoft.com  
Interval           : 300000  
Limit              : 20000  
PolicyId           : 5d1bf221-c8f0-4368-abcf-aa139e8a7c72  
Reservation        : 15000  
Status             : InsufficientThroughput  
StorageNodeIOPS    : 12181  
StorageNodeLatency : 22.0514  
StorageNodeName    : plang-fs2.plang.nttest.microsoft.com  
TimeStamp          : 2/13/2015 12:07:30 PM  
VolumeId           : 0d2fd367-8d74-4146-9934-306726913dda  
PSComputerName     :  
MaximumIops        : 20000  
MinimumIops        : 15000  
```  

## <a name="BKMK_Health"></a>저장소 QoS를 사용 하 여 상태 모니터링  
새로운 상태 서비스는 모든 노드에서 실행 가능한 이벤트를 확인할 단일 장소를 제공하여 저장소 클러스터의 모니터링을 간소화합니다. 이 섹션에서는 `debug-storagesubsystem` cmdlet을 사용하여 저장소 클러스터의 상태를 모니터링하는 방법을 설명합니다.  

### <a name="view-storage-status-with-debug-storagesubsystem"></a>Debug-StorageSubSystem을 사용하여 저장소 상태 보기  
클러스터 스토리지 공간도 단일 위치에서 스토리지 클러스터의 상태에 정보를 제공합니다. 이를 통해 관리자는 스토리지 배포에서 현재 문제를 신속하게 식별하고 문제가 접수되거나 해제될 대 모니터링할 수 있습니다.  

#### <a name="vm-with-invalid-policy"></a>잘못된 정책을 사용하는 VM  
잘못된 정책을 사용하는 VM도 스토리지 하위 시스템 상태 모니터링을 통해 보고됩니다.  다음은 이 문서의 [잘못된 정책을 사용하는 VM 찾기](#BKMK_FindingVMsWithInvalidPolicies)에 설명된 것과 동일한 상태의 예입니다.  

```PowerShell
C:\> Get-StorageSubSystem -FriendlyName Clustered* | Debug-StorageSubSystem  

EventTime                 :  
FaultId                   : 0d16d034-9f15-4920-a305-f9852abf47c3  
FaultingObject            :  
FaultingObjectDescription : Storage QoS Policy 5d1bf221-c8f0-4368-abcf-aa139e8a7c72  
FaultingObjectLocation    :  
FaultType                 : Storage QoS policy used by consumer does not exist.  
PerceivedSeverity         : Minor  
Reason                    : One or more storage consumers (usually Virtual Machines) are  
                            using a non-existent policy with id  
                            5d1bf221-c8f0-4368-abcf-aa139e8a7c72. Consumer details:  

                            Flow ID: 1ca356ff-fd33-5b5d-b60a-2c8659dc803e  
                            Initiator ID: 2ceabcef-2eba-4f1b-9e66-10f960b50bbf  
                            Initiator Name: WinOltp1  
                            Initiator Node: plang-c1.plang.nttest.microsoft.com  
                            File Path:  
                            C:\ClusterStorage\Volume3\SHARES\THREE\WINOLTP1\IOMETER.VHDX  
RecommendedActions        : {Reconfigure the storage consumers (usually Virtual Machines)  
                            to use a valid policy., Recreate any missing Storage QoS  
                            policies.}  
PSComputerName            :  
```  

#### <a name="lost-redundancy-for-a-storage-spaces-virtual-disk"></a>스토리지 공간 가상 디스크에 대한 중복성 손실  

이 예에서는 클러스터 저장소 공간에 3방향 미러로 만든 가상 디스크가 있습니다.  장애 디스크가 제거되었지만 대체 디스크가 추가되지 않았습니다.  저장소 하위 시스템에서 HealthStatus **Warning**으로 중복성 손실을 보고하지만 볼륨이 여전히 온라인 상태이므로 OperationalStatus는 **OK**입니다.  

```PowerShell
PS C:\> Get-StorageSubSystem -FriendlyName Clustered*  

FriendlyName                   HealthStatus                   OperationalStatus  
------------                   ------------                   -----------------  
Clustered Windows Storage o... Warning                        OK  

[plang-fs1]: PS C:\Users\plang\Documents> Get-StorageSubSystem -FriendlyName Clustered* | Deb  
ug-StorageSubSystem  

EventTime                 :  
FaultId                   : dfb4b672-22a6-4229-b2ed-c29d7485bede  
FaultingObject            :  
FaultingObjectDescription : Virtual disk 'Two'  
FaultingObjectLocation    :  
FaultType                 : VirtualDiskDegradedFaultType  
PerceivedSeverity         : Minor  
Reason                    : Virtual disk 'Two' does not have enough redundancy remaining to  
                            successfully repair or regenerate its data.  
RecommendedActions        : {Rebalance the pool, replace failed physical disks, or add new  
                            physical disks to the storage pool, then repair the virtual  
                            disk.}  
PSComputerName            :  
```  

### <a name="sample-script-for-continuous-monitoring-of-storage-qos"></a>저장소 QoS의 지속적인 모니터링을 위한 샘플 스크립트  

이 섹션에는 WMI 스크립트를 사용하여 일반적인 장애를 모니터링할 수 있는 방법을 보여 주는 샘플 스크립트가 포함되어 있습니다.  이 스크립트는 개발자가 상태 이벤트를 실시간으로 검색할 수 있는 시작점으로 설계되었습니다.  

**예제 스크립트:**  

```PowerShell
param($cimSession)  
# Register and display events  
Register-CimIndicationEvent -Namespace root\microsoft\windows\storage -ClassName msft_storagefaultevent -CimSession $cimSession  

while ($true)  
{  
     $e = (Wait-Event)  
     $e.SourceEventArgs.NewEvent  
     Remove-Event $e.SourceIdentifier  
}  
```  

## <a name="frequently-asked-questions"></a>질문과 대답  

### <a name="how-do-i-retain-a-storage-qos-policy-being-enforced-for-my-virtual-machine-if-i-move-its-vhdvhdx-files-to-another-storage-cluster"></a>해당 VHD/VHDx 파일을 다른 스토리지 클러스터로 이동하는 경우 내 가상 컴퓨터에 적용되는 스토리지 QoS 정책을 유지하려면 어떻게 해야 합니까?  

정책을 지정하는 VHD/VHDx 파일의 설정은 정책 ID의 GUID입니다.  정책을 만들 때 **PolicyID** 매개 변수를 사용하여 GUID를 지정할 수 있습니다.  이 매개 변수를 지정하지 않으면 임의의 GUID가 생성됩니다.  따라서 현재 VM이 해당 VHD/VHDx 파일을 저장하는 스토리지 클러스터의 PolicyID를 가져오고 대상 스토리지 클러스터에서 동일한 정책을 만든 다음 동일한 GUID를 사용하도록 지정할 수 있습니다.  VM 파일이 새 스토리지 클러스터로 이동하면 동일한 GUID를 가진 정책이 적용됩니다.  

System Center Virtual Machine Manager를 사용하여 여러 스토리지 클러스터에 걸쳐 정책을 적용할 수 있습니다. 이 방법을 사용하면 이 시나리오가 훨씬 쉬워집니다.  
### <a name="if-i-change-the-storage-qos-policy-why-dont-i-see-it-take-effect-immediately-when-i-run-get-storageqosflow"></a>저장소 QoS 정책을 변경한 경우 Get-StorageQoSFlow를 실행할 때 즉시 적용되지 않는 이유는 무엇입니까?  

정책의 최대값에 도달한 흐름이 있을 때 더 높거나 낮게 만들기 위해 정책을 변경한 경우 PowerShell cmdlet을 사용하여 흐름의 대기 시간/IOPS/대역폭을 즉시 확인할 수 있습니다. 흐름에 대한 정책 변경의 전체 영향이 표시되는 데 최대 5분이 걸립니다.  몇 초 내에 새 제한이 적용되지만 **Get-StorgeQoSFlow** PowerShell cmdlet에서는 5분 길이의 슬라이딩 윈도우를 통해 각 카운터의 평균을 사용합니다.  그렇지 않고 현재 값이 표시되며 PowerShell cmdlet을 여러 번 연속으로 실행한 경우 완전히 다른 값이 표시될 수 있습니다. IOPS 및 대기 시간 값은 초 단위로 크게 변동할 수 있기 때문입니다.

### <a name="BKMK_Updates"></a>Windows Server 2016에 추가 된 새로운 기능

Windows Server 2016에서 저장소 QoS 정책 유형 이름이 변경되었습니다.  **다중 인스턴스** 정책 유형은 **전용**으로, **단일 인스턴스** 정책 유형은 **집계**로 바뀌었습니다. 전용 정책의 관리 동작도 수정되었습니다. 동일한 **전용** 정책이 적용된 동일한 가상 컴퓨터 내의 VHD/VHDX 파일이 I/O 할당을 공유하지 않습니다.  

Windows Server 2016에는 두 가지 새로운 저장소 QoS 기능이 있습니다.  

-   **최대 대역폭**  

    Windows Server 2016의 저장소 QoS에는 정책에 할당된 흐름에서 사용할 수 있는 최대 대역폭을 지정하는 기능이 도입되었습니다.  **StorageQosPolicy** cmdlet에서 지정할 때 매개 변수는 **MaximumIOBandwidth**이고 출력은 초당 바이트 수로 표시됩니다.  
    **MaximimIops**와 **MaximumIOBandwidth**가 둘 다 정책에 설정된 경우에는 둘 다 적용되며, 흐름에서 도달할 첫 번째 항목이 흐름의 I/O를 제한합니다.  

-   **IOPS 정규화를 구성할 수 있습니다.**  

    저장소 QoS에서 IOPS 정규화를 사용합니다.  기본값은 정규화 크기 8K입니다.  Windows Server 2016의 스토리지 QoS에는 스토리지 클러스터의 다른 정규화 크기를 지정하는 기능이 도입되었습니다.  이 정규화 크기는 스토리지 클러스터의 모든 흐름에 영향을 주며 변경되는 즉시(몇 초 이내) 적용됩니다.  최소값은 1KB이고 최대값은 4GB입니다(4MB IO를 초과하는 것은 비정상적이므로 4MB 이하로 설정하는 것이 좋음).  

    정규화 계산 변경으로 인해 IOPS 정규화를 변경할 경우 저장소 QoS 출력에서 동일한 IO 패턴/처리량에 서로 다른 IOPS 숫자가 나타난다는 점을 고려해야 합니다.  스토리지 클러스터 간에 IOPS를 비교할 경우 사용되는 각 정규화 값을 확인할 수도 있습니다. 이는 보고되는 정규화된 IOPS에 영향을 주기 때문입니다.    

#### <a name="example-1-creating-a-new-policy-and-viewing-the-maximum-bandwidth-on-the-storage-cluster"></a>예 1: 새 정책 만들기 및 스토리지 클러스터에서 최대 대역폭 보기  
PowerShell에서 숫자로 표시되는 단위를 지정할 수 있습니다.  다음 예에서는 10MB를 최대 대역폭 값으로 사용합니다.  저장소 QoS는 이를 변환하여 초당 바이트 수로 저장합니다. 따라서 10MB는 10485760바이트/초로 변환됩니다.  

```PowerShell
PS C:\Windows\system32> New-StorageQosPolicy -Name HR_VMs -MaximumIops 1000 -MinimumIops 20 -MaximumIOBandwidth 10MB  

Name   MinimumIops MaximumIops MaximumIOBandwidth Status  
----   ----------- ----------- ------------------ ------  
HR_VMs 20          1000        10485760           Ok  

PS C:\Windows\system32> Get-StorageQosPolicy  

Name    MinimumIops MaximumIops MaximumIOBandwidth Status  
----    ----------- ----------- ------------------ ------  
Default 0           0           0                  Ok  
HR_VMs  20          1000        10485760           Ok  

PS C:\Windows\system32> Get-StorageQoSFlow | fL InitiatorName,FilePath,InitiatorIOPS,InitiatorLatency,InitiatorBandwidth  

InitiatorName      : testsQoS  
FilePath           : C:\ClusterStorage\Volume2\TESTSQOS\VIRTUAL HARD DISKS\TESTSQOS.VHDX  
InitiatorIOPS      : 5  
InitiatorLatency   : 1.5455  
InitiatorBandwidth : 37888  
```  

#### <a name="example-2-get-iops-normalization-settings-and-specify--a-new-value"></a>예 2: IOPS 정규화 설정 가져오기 및 새 값 지정  

다음 예에는 스토리지 클러스터 IOPS 표준화 설정(기본값 8KB)을 가져와 32KB로 설정한 다음 다시 표시하는 방법을 보여 줍니다.  바이트로 변환하는 대신 PowerShell을 사용하여 단위를 지정할 수 있으므로 이 예에서는 "32KB"를 지정합니다.   출력에는 초당 바이트 수로 값이 표시됩니다.  

```PowerShell
PS C:\Windows\system32> Get-StorageQosPolicyStore  

IOPSNormalizationSize  
---------------------  
8192  

PS C:\Windows\system32> Set-StorageQosPolicyStore -IOPSNormalizationSize 32KB  
PS C:\Windows\system32> Get-StorageQosPolicyStore  

IOPSNormalizationSize  
---------------------  
32768  
```    

## <a name="see-also"></a>참고 항목  
- [Windows Server 2016](../../get-started/windows-server-2016.md)  
- [Windows Server 2016의 저장소 복제본](../storage-replica/storage-replica-overview.md)  
- [Windows Server 2016의 스토리지 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)  
