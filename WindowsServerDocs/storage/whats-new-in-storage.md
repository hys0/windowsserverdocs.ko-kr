---
ms.assetid: 0f2a7f7b-aca8-4e5d-ad67-4258e88bc52f
title: "Windows Server에서 제공되는 저장소의 새로운 기능"
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dongill
ms.technology: storage
ms.topic: article
author: kumudd
ms.date: 09/15/2016
ms.openlocfilehash: 9aab6246f7ddc86629834bf20a7d21cc4ce2ec8f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="whats-new-in-storage-in-windows-server-2016"></a>Windows Server 2016에서 제공되는 저장소의 새로운 기능

>적용 대상: WindowsServer 2016

이 항목에서는 Windows 2016에서 제공되는 저장소의 새로운 기능과 변경된 기능을 설명합니다.

## <a name="s2d"></a>직접 액세스 저장소 공간  
저장소 공간 다이렉트는 로컬 저장소가 있는 서버를 사용하여 확장 가능한 고가용성 저장소를 구축하도록 지원합니다. 이는 소프트웨어 정의 저장소 시스템의 배포 및 관리를 간소화하고 SATA SSD 및 NVMe 디스크 장치와 같이 이전에 공유 디스크를 사용하는 클러스터형 저장소 공간에서는 불가능했던 새로운 등급의 디스크 장치를 사용합니다.  

**이와 같은 변경을 통해 더해지는 가치**  
저장소 공간 다이렉트는 서비스 공급자와 기업이 로컬 저장소가 있는 산업 표준 서버를 사용하여 확장 가능한 고가용성 소프트웨어 정의 저장소를 구축할 수 있도록 지원합니다. 로컬 저장소가 있는 서버를 사용하면 복잡성이 감소하고, 확장성이 증가하며, SATA SSD와 같은 이전에 사용할 수 없었던 저장 장치를 사용하여 플래시 저장소 또는 NVMe SSD의 비용을 절감하고 성능을 개선할 수 있습니다.  

저장소 공간 다이렉트를 사용하면 공유 SAS 패브릭이 필요 없으므로 배포 및 구성이 간소화됩니다. 대신 빠르고 대기 시간이 낮은 CPU 효율적인 저장소에 SMB3 및 SMB 다이렉트(RDMA)를 활용함으로써 네트워크를 저장소 패브릭으로 사용합니다. 규모를 확장하려면 서버를 추가하여 저장소 용량 및 I/O 성능을 높이기만 하면 됩니다.  
자세한 내용은 [Windows Server 2016의 저장소 공간 다이렉트](storage-spaces/storage-spaces-direct-overview.md)를 참조하세요.  

**달라진 기능**  
이 기능은 Windows Server 2016의 새로운 기능입니다.  

## <a name="storage-replica"></a>저장소 복제본  
저장소 복제본을 통해 사이트 간에 장애 조치(failover) 클러스터를 확장할 뿐만 아니라 재해 복구를 위해 서버 또는 클러스터 간에 저장소에 상관없는 블록 수준의 동기 복제를 사용할 수 있습니다. 동기 복제를 사용하면 파일 시스템 수준에서 데이터가 손실되지 않고 크래시 일관성이 있는 볼륨을 사용하여 실제 사이트의 데이터를 미러링할 수 있습니다. 비동기 복제는 대도시 범위를 넘어 사이트를 확장합니다(데이터가 손실될 수도 있음).  

**이와 같은 변경을 통해 더해지는 가치**  
저장소 복제를 사용하면 다음을 수행할 수 있습니다.  

* 중요 업무용 워크로드의 계획된 중단 및 계획되지 않은 중단을 위한 단일 공급업체 재해 복구 솔루션을 제공합니다.
* 안정성, 확장성 및 성능이 검증된 SMB3 전송을 사용합니다.
* 대도시 거리로 Windows 장애 조치(failover) 클러스터를 확장합니다.
* 저장소 및 클러스터링에 Hyper-V, 저장소 복제본, 저장소 공간, 클러스터, 스케일 아웃 파일 서버, SMB3, 중복 제거 및 ReFS/NTFS와 같은 종단 간 Microsoft 소프트웨어를 사용합니다.
* 다음과 같이 비용 및 복잡성을 줄입니다. 
    * 하드웨어 제약이 없으므로 DAS 또는 SAN과 같은 특정 저장소 구성에 대한 요구 사항이 없습니다.
    * 상용 저장소 및 네트워킹 기술을 허용합니다.
    * 장애 조치(Failover) 클러스터 관리자를 통해 개별 노드 및 클러스터에 대한 그래픽 관리가 용이합니다.
    * Windows PowerShell을 통한 포괄적인 대규모 스크립팅 옵션을 포함합니다. 
* 가동 중지 시간을 줄이고, Windows의 고유한 안정성 및 생산성을 높입니다.  
* 지원 가능성, 성능 메트릭 및 진단 기능을 제공합니다.  

자세한 내용은 [Windows Server 2016의 저장소 복제본](storage-replica/storage-replica-overview.md)을 참조하세요.  

**달라진 기능**  
이 기능은 Windows Server 2016의 새로운 기능입니다.  

## <a name="storage-qos"></a>저장소 서비스 품질  
이제 저장소 QoS(서비스 품질)를 사용하여 중앙에서 종단 간 저장소 성능을 모니터링하고 Windows Server 2016의 Hyper-V 및 CSV 클러스터를 통해 관리 정책을 만들 수 있습니다.  

**이와 같은 변경을 통해 더해지는 가치**  
이제 CSV 클러스터에서 저장소 QoS 정책을 만들고 Hyper-V 가상 컴퓨터에서 하나 이상의 가상 디스크에 할당할 수 있습니다. 워크로드와 저장소 로드 변동에 따라 정책을 준수하도록 저장소 성능이 자동으로 재조정됩니다.  

* 각 정책은 가상 하드 디스크, 단일 가상 컴퓨터 또는 가상 컴퓨터 그룹, 서비스, 테넌트 등 데이터 흐름 모음에 적용할 예약(최소값) 및/또는 제한(최대값)을 지정할 수 있습니다.  
* Windows PowerShell 또는 WMI를 사용하여 다음 작업을 수행할 수 있습니다.  
    * CSV 클러스터에서 정책을 만듭니다.
    * CSV 클러스터에서 사용할 수 있는 정책을 열거합니다.
    * Hyper-V 가상 컴퓨터의 가상 하드 디스크에 정책을 할당합니다. 
    * 각 흐름의 성능 및 정책 내 상태를 모니터링합니다.  
* 여러 가상 하드 디스크에서 동일한 정책을 공유하는 경우 정책 최소값 및 최대값 설정 내에서 수요를 충족하도록 성능이 고르게 분산됩니다. 따라서 정책을 사용하여 하나의 가상 하드 디스크, 하나의 가상 컴퓨터, 서비스를 구성하는 여러 가상 컴퓨터 또는 한 테넌트가 소유한 모든 가상 컴퓨터를 관리할 수 있습니다.  

**달라진 기능**  
이 기능은 Windows Server 2016의 새로운 기능입니다. 최소 예약 관리, 단일 명령을 통한 클러스터 전반의 모든 가상 디스크의 흐름 모니터링 및 중앙 집중식 정책 기반 관리는 이전 버전의 Windows Server에서는 불가능했습니다.  

자세한 내용은 [저장소 서비스 품질](storage-qos/storage-qos-overview.md)을 참조하세요.

## <a name="dedup"></a>데이터 중복 제거  
| 기능 | 새로운 기능 또는 업데이트된 기능 | 설명 |
|---------------|----------------|-------------|
| [대규모 볼륨 지원](data-deduplication/whats-new.md#large-volume-support) | 업데이트됨 | Windows Server 2016 이전에는 특별히 예상되는 변동에 대비해 볼륨의 크기를 조정해야 했으며, 10TB가 넘는 볼륨은 중복 제거에 적합하지 않았습니다. Windows Server 2016에서는 데이터 중복 제거 기능이 **최대 64TB**의 볼륨 크기를 지원합니다. |
| [대용량 파일 지원](data-deduplication/whats-new.md#large-file-support) | 업데이트됨 | Windows Server 2016 이전에는 크기가 1TB에 가까운 파일은 중복 제거에 적합하지 않았습니다. Windows Server 2016에서 **최대 1TB**의 파일이 완벽하게 지원됩니다. |
| [Nano Server 지원](data-deduplication/whats-new.md#nano-server-support) | 새로 만들기 | 데이터 중복 제거는 Windows Server 2016의 새로운 Nano Server 배포 옵션에서 사용할 수 있으며 완전히 지원됩니다. |
| [간소화된 백업 지원](data-deduplication/whats-new.md#simple-backup-support) | 새로 만들기 | Windows Server 2012 R2에서는 Microsoft의 [Data Protection Manager](https://technet.microsoft.com/en-us/library/hh758173.aspx)와 같은 가상화된 백업 응용 프로그램이 일련의 수동 구성 단계를 통해 지원되었습니다. Windows Server 2016에서는 가상화된 백업 응용 프로그램에 대한 중복 제거의 원활한 배포를 위해 새로운 기본 사용 유형인 "백업"이 추가되었습니다. |
| [클러스터 OS 롤링 업그레이드 지원](data-deduplication/whats-new.md#cluster-upgrade-support) | 새로 만들기 | 데이터 중복 제거는 Windows Server 2016의 [클러스터 OS 롤링 업그레이드](..//failover-clustering/cluster-operating-system-rolling-upgrade.md) 기능을 완벽하게 지원합니다. |

## <a name="smb-hardening-improvements"></a>SYSVOL 및 NETLOGON 연결에 대한 향상된 SMB 강화 기능  
Active Directory 도메인 서비스에 연결된 Windows 10 및 Windows Server 2016 클라이언트에서는 도메인 컨트롤러의 기본 SYSVOL 및 NETLOGON 공유에 SMB 서명 및 상호 인증(예: Kerberos)이 필요합니다.   

**이와 같은 변경을 통해 더해지는 가치**  
이 변경으로 메시지 가로채기 공격의 가능성이 줄어듭니다.   

**어떤 점이 달라졌나요?**  
SMB 서명 및 상호 인증을 사용할 수 없는 경우 Windows 10 또는 Windows Server 2016 컴퓨터는 도메인 기반 그룹 정책 및 스크립트를 처리하지 않습니다.  

> [!NOTE]  
> 이러한 설정에 대한 레지스트리 값은 기본적으로 존재하지 않지만 그룹 정책 또는 다른 레지스트리 값으로 재정의될 때까지 강화 규칙은 계속 적용됩니다.  

이러한 향상된 보안 기능(UNC 강화라고도 함)에 대한 자세한 내용은 Microsoft 기술 자료 문서 [3000483](http://support.microsoft.com/kb/3000483) 및 [MS15-011 및 MS15-014: 그룹 정책 강화](http://blogs.technet.microsoft.com/srd/2015/02/10/ms15-011-ms15-014-hardening-group-policy)를 참조하세요.  

## <a name="work-folders"></a>작업 폴더
작업 폴더 서버가 Windows Server 2016을 실행 중이고 작업 폴더 클라이언트가 Windows 10을 실행 중일 때의 변경 알림이 개선되었습니다.

**이와 같은 변경을 통해 더해지는 가치**<br>
Windows Server 2012 R2의 경우 파일 변경을 작업 폴더 서버와 동기화하면 클라이언트는 해당 변경에 대해 알리지 않고 업데이트될 때까지 최대 10분을 기다립니다.  Windows Sever 2016을 사용하면 작업 폴더 서버가 즉시 Windows 10 클라이언트에 알리므로 파일 변경 내용이 즉시 동기화됩니다.

**달라진 기능**<br>
이 기능은 Windows Server 2016의 새로운 기능입니다. 이 기능을 사용하려면 Windows Server 2016 작업 폴더 서버 및 클라이언트가 Windows 10이어야 합니다.

이전 클라이언트를 사용하거나 클라우드 폴더 서버가 Windows Server 2012 R2인 경우 클라이언트가 10분마다 변경 내용을 계속 폴링합니다.

## <a name="refs"></a>ReFS 
ReFS가 다음 번 반복으로 대규모 저장소 배포에 대하여 다양한 작업을 지원하며 데이터의 안정성, 복원력, 확장성을 제공합니다.     

**이와 같은 변경을 통해 더해지는 가치**<br>
ReFS로 향상되는 기능은 다음과 같습니다.

* ReFS는 새로운 저장소 계층 기능을 구현하여 성능을 향상시키고 저장소 용량을 늘립니다. 새로운 기능의 이점은 다음과 같습니다.
    * 동일한 가상 디스크에 여러 복원력 유형 포함(예: 성능 계층에서 미러링, 용량 계층에서 패리티 사용)
    * 유동적인 작업 집합에 대한 응답성 향상 
    * SMR(Shingleled Magnetic Recording) 미디어 지원 
* 블록 복제를 도입하면 .vhdx 검사점 병합 작업과 같은 VM 작업의 성능이 크게 향상됩니다.
* 새로운 ReFS 검사 도구를 이용하면 유출된 저장소의 복구가 가능하며 치명적인 손상으로부터 데이터를 복구하는 데 도움이 됩니다. 

**달라진 기능**<br>
Windows Server 2016에서 처음으로 제공하는 기능입니다. 

## <a name="see-also"></a>참고 항목  
* [Windows Server 2016의 새로운 기능](../get-started/what-s-new-in-windows-server-2016.md)  
