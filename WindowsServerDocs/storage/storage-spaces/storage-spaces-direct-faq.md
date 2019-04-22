---
title: 저장소 공간 다이렉트-질문과 대답
description: 직접 저장소 공간에 대 한 방법에 대해 알아봅니다
keywords: 저장소 공간
ms.prod: windows-server-threshold
ms.author: kaushik
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: b17aa7ddc783e95fbcc19fe3913192d245133c7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818914"
---
# <a name="storage-spaces-direct---frequently-asked-questions-faq"></a>저장소 공간 다이렉트-질문과 대답 (FAQ)

이 문서에서는 몇 가지 일반적인 나열 및 관련 된 질문과 대답 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)합니다.

## <a name="when-you-use-storage-spaces-direct-with-3-nodes-can-you-get-both-performance-and-capacity-tiers"></a>3 개의 노드를 사용 하 여 저장소 공간 다이렉트을 사용 하는 경우 하면 얻을 수 성능 및 용량 계층?

예 2-노드 또는 3 노드 저장소 공간 다이렉트 구성에서 성능 및 용량 계층을 모두 가져올 수 있습니다. 그러나 2 용량 장치 했는지 확인 해야 합니다. 모든 세 가지 종류의 장치를 사용 해야 함을 의미 합니다. NVME, SSD 및 HDD 중에서 선택 합니다.
 
## <a name="refs-file-system-provides-real-time-tiaring-with-storage-spaces-direct-does-refs-provides-the-same-functionality-with-shared-storage-spaces-in-2016"></a>Refs 파일 시스템 저장소 공간 다이렉트를 사용 하 여 실시간 tiaring를 제공합니다. REFS 동일한 기능을 제공 공유 저장소 공간을 사용 하 여 2016?

아니요, 2016 사용 하 여 공유 저장소 공간을 사용 하 여 계층화 실시간 얻이 없습니다. 저장소 공간 다이렉트에 해당 됩니다. 
 
## <a name="can-i-use-an-ntfs-file-system-with-storage-spaces-direct"></a>저장소 공간 다이렉트를 사용 하 여 NTFS 파일 시스템을 사용할 수 있습니까?
  
예, 저장소 공간 다이렉트를 사용 하 여 NTFS 파일 시스템을 사용할 수 있습니다. 하지만 REFS 것이 좋습니다. NTFS는 실시간 계층화를 제공 하지 않습니다. 
 
## <a name="i-have-configured-2-node-storage-spaces-direct-clusters-where-the-virtual-disk-is-configured-as-2-way-mirror-resiliency-if-i-add-a-new-fault-domain-will-the-resiliency-of-the-existing-virtual-disk-change"></a>2 노드 저장소 공간 다이렉트 클러스터의 경우 가상 디스크가 양방향 미러 복원 력으로 구성 되어 있는 구성 했습니다. 새 장애 도메인을 추가 하면 기존 가상 디스크의 복원 력을 변경 됩니까?

새 장애 도메인을 추가한 후 사용자가 만든 새 가상 디스크는 3 방향 미러도 이동 합니다. 그러나 기존 가상 디스크를 2 방향 미러 디스크 유지 됩니다. 새 복원 력의 이점을 얻을 수 기존 볼륨에서 새 가상 디스크에 데이터를 복사할 수 있습니다.
 
## <a name="the-storage-spaces-direct-was-created-using-the-autoconfig0-switch-and-the-pool-created-manually-when-i-try-to-query-the-storage-spaces-direct-pool-to-create-a-new-volume-i-get-a-message-that-says-enable-clusters2d-again-what-should-i-do"></a>저장소 공간 다이렉트를 사용 하 여 만들어진 여 autoconfig:0 스위치 및 수동으로 만든 풀 새 볼륨을 만들려면 저장소 공간 다이렉트는 풀 쿼리 하려고 할 때 메시지가 "Enable-ClusterS2D 다시." 라는 제가 뭘 해야 하나요?

기본적으로 사용 S2D cmdlet을 사용 하 여 저장소 공간 다이렉트를 구성할 때 cmdlet은 모든 작업을 수행 하기. 풀 및 계층을 만듭니다. Autoconfig:0를 사용할 때는 모든 수동으로 수행 해야 합니다. 만 풀을 만든 경우 계층을 반드시 생성 되지 않습니다. 계층을 전혀 만들지 하거나 연결 된 장치에 해당 하는 방식으로 계층을 만들지 않은 경우 "Enable-ClusterS2D 다시" 오류 메시지를 받을 수 있습니다. 프로덕션 환경에서 자동 구성 스위치를 사용 하지 않는 것이 좋습니다. 
 
## <a name="is-it-possible-to-add-a-spinning-disk-hdd-to-the-storage-spaces-direct-pool-after-you-have-created-storage-spaces-direct-with-ssd-devices"></a>만든 후 저장소 공간 다이렉트 SSD 장치를 사용 하 여 회전 디스크 (HDD) 저장소 공간 다이렉트는 풀에 추가할 수는?

아니요. 기본적으로 단일 장치 유형을 사용 하 여 풀을 만들 경우 캐시 디스크를 구성 하지 않습니다 하 고 모든 디스크는 용량에 사용 됩니다. NVME 디스크 구성에 추가할 수 있습니다 및 NVME 디스크 캐시에 대 한 구성 됩니다.
 
## <a name="i-have-configured-a-2-rack-fault-domain-rack-1-has-2-fault-domains-rack-2-has-1-fault-domain-each-server-has-4-capacity-100-gb-devices-can-i-use-all-1200-gb-of-space-from-the-pool"></a>2-랙을 장애 도메인을 구성 했습니다. 랙 1에 2 개의 장애 도메인, 랙 2에 1 개의 장애 도메인입니다. 각 서버에 4 용량 100GB 장치가 있습니다. 풀에서 모든 1,200 10GB의 공간을 사용할 수 있습니까?

아니요, 800GB만 사용할 수 있습니다. 랙 장애 도메인에서 삭제할 각 있으므로 2 방향 미러 구성 및 다른 랙에 해당 중복 land 있는지 확인 해야 합니다.
 
## <a name="what-should-the-cache-size-be-when-i-am-configuring-storage-spaces-direct"></a>캐시 크기 때 될 내용을 저장소 공간 다이렉트 독립?

캐시 작업 집합에 맞게 크기가 조정 됩니다 (적극적으로 되는 데이터 읽기 또는 특정된 시점에 기록) 응용 프로그램 및 워크 로드.

## <a name="how-can-i-determine-the-size-of-cache-that-is-being-used-by-storage-spaces-direct"></a>저장소 공간 다이렉트에서 사용 되는 캐시의 크기는 어떻게 확인할 수 있습니까?

기본 제공 유틸리티 PerfMon을 사용 하 여 캐시 누락을 검사 합니다. 캐시 누락 reads/sec 클러스터 저장소 하이브리드 디스크 카운터에서 검토 합니다. 너무 많은 읽기 캐시를 누락 하는 경우 캐시는 소형 및 확장 하려고 해야 합니다. 
 
## <a name="is-there-a-calculator-that-shows-the-exact-size-of-the-disks-that-are-being-set-aside-for-cache-capacity-and-resiliency-that-would-enable-me-to-plan-better"></a>캐시, 용량 및 더 효과적으로 계획을 사용할 수 있는 복원 력 따로 설정 하는 디스크의 정확한 크기를 표시 하는 계산기가 있나요?

저장소 공간 계산기를 사용 하 여 계획 하는 데 사용할 수 있습니다. 에 제공 됩니다 http://aka.ms/s2dcalc합니다.
 
## <a name="what-is-the-best-configuration-that-you-would-recommend-when-configuring-6-servers-and-3-racks"></a>6 대의 서버 및 3 개의 랙을 구성 하는 경우에 권장 하는 최상의 구성 이란?

3 방향 미러 복원 력 가상 디스크를 각 랙에 2 개 서버를 사용 하십시오. 랙에 배치 됩니다 방식에서 os 구성을 제공 하는 경우에 랙 구성을 제대로 작동 해야 합니다. 
 
## <a name="can-i-enable-maintenance-mode-for-a-specific-disk-on-a-specific-server-in-storage-spaces-direct-cluster"></a>저장소 공간 다이렉트 클러스터에서 특정 서버의 특정 디스크에 대 한 유지 관리 모드를 사용할 수 있나요?

예, 특정 디스크 및 특정 장애 도메인의 저장소 유지 관리 모드를 사용할 수 있습니다. 사용-StorageMaintenanceMode 명령 노드를 일시 중지에 자동으로 호출 됩니다. 다음 명령을 실행 하 여 특정 디스크에 대해 설정할 수 있습니다.

```powershell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Enable-StorageMaintenanceMode
```

## <a name="is-storage-spaces-direct-supported-on-my-hardware"></a>저장소 공간 다이렉트 내 하드웨어 지원?

지원을 확인 하려면 하드웨어 공급 업체에 문의 하 여는 것이 좋습니다. 하드웨어 공급 업체는 하드웨어 및 여부 지원 되는지 여부에 대 한 설명에 솔루션을 테스트 합니다. 예를 들어, 당시이 문서의 작성 R730와 같은 서버 / R730xd R630 8 개 이상의 드라이브 슬롯이 있는 SES를 지원할 수 있습니다 하 고 저장소 공간 다이렉트와 호환 됩니다. Dell은 저장소 공간 다이렉트를 사용 하 여 HBA330만 지원합니다. R620은 SES를 지원 하지 않습니다 하 고 저장소 공간 다이렉트와 호환 되지 않습니다.

지원 하드웨어에 대 한 내용은 다음 웹 사이트로 이동 합니다. Windows Server 카탈로그
 
## <a name="how-does-storage-spaces-direct-make-use-of-ses"></a>방법에서는 저장소 공간 다이렉트 활용 SES?

저장소 공간 다이렉트를 사용 하 여 인클로저 서비스 SES (SCSI) 매핑 줄임 데이터 및 메타 데이터의 복원 력 있는 방식으로 장애 도메인에 분산 되어 있는지 확인 합니다. 하드웨어는 SES를 지원 하지 않으면, 인클로저와의 매핑이 지원 되지 않습니다 및 데이터 배치 중복이 되지 않습니다.
 
## <a name="what-command-can-you-use-to-check-the-physical-extent-for-a-virtual-disk"></a>명령은 가상 디스크에 대 한 실제 범위를 확인 하는 데 사용할 수 있습니까?
  
이것:

```powershell
get-virtualdisk -friendlyname “xyz” | get-physicalextent
```
