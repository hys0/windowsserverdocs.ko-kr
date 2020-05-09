---
title: 스토리지 공간 다이렉트-질문과 대답
description: 스토리지 공간 다이렉트 방법 알아보기
ms.prod: windows-server
ms.author: kaushik
ms.technology: storage-spaces
ms.topic: article
author: kaushika-msft
ms.date: 10/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5c033a5a810d1cdedeb4c733ba4bf0ac99e669f0
ms.sourcegitcommit: 3483f886f331b9d954a0e5dba8e910dbe5ee5765
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2020
ms.locfileid: "82977251"
---
# <a name="storage-spaces-direct---frequently-asked-questions-faq"></a>스토리지 공간 다이렉트-질문과 대답 (FAQ)

이 문서에서는 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md)와 관련 된 몇 가지 일반적인 질문과 대답을 나열 합니다.

## <a name="when-you-use-storage-spaces-direct-with-3-nodes-can-you-get-both-performance-and-capacity-tiers"></a>3 개 노드가 포함 된 스토리지 공간 다이렉트를 사용 하는 경우 성능 및 용량 계층을 모두 얻을 수 있나요?

예, 2 노드 또는 3 노드 스토리지 공간 다이렉트 구성에서 성능 및 용량 계층을 모두 가져올 수 있습니다. 그러나 두 개의 용량 장치가 있는지 확인 해야 합니다. 즉, NVME, SSD 및 HDD의 세 가지 유형의 장치를 모두 사용 해야 합니다.

## <a name="refs-file-system-provides-real-time-tiering-with-storage-spaces-direct-does-refs-provide-the-same-functionality-with-shared-storage-spaces-in-2016"></a>Refs 파일 시스템은 스토리지 공간 다이렉트를 사용 하 여 실시간 계층화를 제공 합니다. REFS는 2016의 공유 저장소 공간과 동일한 기능을 제공 하나요?

아니요, 2016을 사용 하 여 공유 저장소 공간에 대 한 실시간 계층화를 얻지 않습니다. 스토리지 공간 다이렉트에만 해당 됩니다.

## <a name="can-i-use-an-ntfs-file-system-with-storage-spaces-direct"></a>스토리지 공간 다이렉트에 NTFS 파일 시스템을 사용할 수 있나요?

예, 스토리지 공간 다이렉트에 NTFS 파일 시스템을 사용할 수 있습니다. 그러나 REFS를 권장 합니다. NTFS는 실시간 계층화를 제공 하지 않습니다.

## <a name="i-have-configured-2-node-storage-spaces-direct-clusters-where-the-virtual-disk-is-configured-as-2-way-mirror-resiliency-if-i-add-a-new-fault-domain-will-the-resiliency-of-the-existing-virtual-disk-change"></a>가상 디스크가 양방향 미러 복원 력으로 구성 된 2 개의 노드 스토리지 공간 다이렉트 클러스터를 구성 했습니다. 새 장애 도메인을 추가 하는 경우 기존 가상 디스크의 복원 력을 변경 하나요?

새 장애 도메인을 추가 하면 새로 만든 가상 디스크는 3 방향 미러로 이동 됩니다. 그러나 기존 가상 디스크는 양방향 미러된 디스크로 유지 됩니다. 기존 볼륨에서 새 가상 디스크로 데이터를 복사 하 여 새로운 복원 력을 얻을 수 있습니다.

## <a name="the-storage-spaces-direct-was-created-using-the-autoconfig0-switch-and-the-pool-was-created-manually-when-i-try-to-query-the-storage-spaces-direct-pool-to-create-a-new-volume-i-get-a-message-saying-enable-clusters2d-again-what-should-i-do"></a>자동 구성을 사용 하 여 스토리지 공간 다이렉트를 만들었습니다. 0 스위치와 풀을 수동으로 만들었습니다. 스토리지 공간 다이렉트 풀을 쿼리하여 새 볼륨을 만들려고 하면 "Enable-clusters2d를 다시 사용 합니다." 라는 메시지가 표시 됩니다.   어떻게 해야 합니까?

기본적으로 사용 하 여 스토리지 공간 다이렉트를 구성 하면 cmdlet은 모든 작업을 수행 합니다. 풀 및 계층을 만듭니다. 자동 구성: 0을 사용 하는 경우 모든 항목을 수동으로 수행 해야 합니다. 풀만 만든 경우 계층이 반드시 생성 되는 것은 아닙니다. 연결 된 장치에 해당 하는 방식으로 모든 계층 또는 만들지 않은 계층을 만들지 않은 경우에는 "Enable-clusters2d" 오류 메시지가 표시 됩니다. 프로덕션 환경에서는 autoconfig 스위치를 사용 하지 않는 것이 좋습니다.

## <a name="is-it-possible-to-add-a-spinning-disk-hdd-to-the-storage-spaces-direct-pool-after-you-have-created-storage-spaces-direct-with-ssd-devices"></a>SSD 장치를 사용 하 여 스토리지 공간 다이렉트를 만든 후에는 스토리지 공간 다이렉트 풀에 회전 디스크 (HDD)를 추가할 수 있나요?

아니요. 기본적으로 단일 장치 유형을 사용 하 여 풀을 만드는 경우 캐시 디스크가 구성 되지 않으며 모든 디스크가 용량에 사용 됩니다. 구성에 NVME 디스크를 추가할 수 있으며, NVME 디스크는 캐시에 대해 구성 됩니다.

## <a name="i-have-configured-a-2-rack-fault-domain-rack-1-has-2-fault-domains-rack-2-has-1-fault-domain-each-server-has-4-capacity-100-gb-devices-can-i-use-all-1200-gb-of-space-from-the-pool"></a>2-랙 장애 도메인을 구성 했습니다. 랙 1에는 2 개의 장애 도메인이 있고, 랙 2에는 장애 도메인이 하나 있습니다. 각 서버에는 4 개의 용량 100 GB 장치가 있습니다. 풀에서 1200 GB의 공간을 모두 사용할 수 있나요?

아니요, 800 GB만 사용할 수 있습니다. 랙 장애 도메인에서 각 처와 중복 된 땅이 서로 다른 랙에 있는 2 방향 미러 구성이 있는지 확인 해야 합니다.

## <a name="what-should-the-cache-size-be-when-i-am-configuring-storage-spaces-direct"></a>스토리지 공간 다이렉트를 구성할 때 캐시 크기는 어떻게 되나요?

응용 프로그램 및 워크 로드의 작업 집합 (지정 된 시간에 적극적으로 읽거나 작성 되는 데이터)에 맞게 캐시 크기를 조정 해야 합니다.

## <a name="how-can-i-determine-the-size-of-cache-that-is-being-used-by-storage-spaces-direct"></a>스토리지 공간 다이렉트에서 사용 하는 캐시 크기를 확인 하려면 어떻게 해야 하나요?

기본 제공 유틸리티 PerfMon을 사용 하 여 캐시 누락을 검사 합니다. 클러스터 저장소 하이브리드 디스크 카운터에서 초당 캐시 누락 읽기 횟수를 검토 합니다. 캐시에 너무 많은 읽기가 없으면 캐시가의 크기가 부족 캐시를 확장할 수 있습니다.

## <a name="is-there-a-calculator-that-shows-the-exact-size-of-the-disks-that-are-being-set-aside-for-cache-capacity-and-resiliency-that-would-enable-me-to-plan-better"></a>더 나은 계획을 할 수 있는 캐시, 용량 및 복원 력을 위해 따로 설정 되는 디스크의 정확한 크기를 보여 주는 계산기가 있나요?

저장소 공간 계산기를 사용 하 여 계획을 지원할 수 있습니다. 에서 https://aka.ms/s2dcalc사용할 수 있습니다.

## <a name="what-is-the-best-configuration-that-you-would-recommend-when-configuring-6-servers-and-3-racks"></a>6 대의 서버와 3 개의 랙을 구성할 때 권장 되는 구성은 무엇 인가요?

3 방향 미러의 가상 디스크 복원 력을 얻으려면 각 랙에 2 대의 서버를 사용 합니다. 랙 구성은 랙에 배치 되는 방식으로 OS에 구성을 제공 하는 경우에만 제대로 작동 합니다.

## <a name="can-i-enable-maintenance-mode-for-a-specific-disk-on-a-specific-server-in-storage-spaces-direct-cluster"></a>스토리지 공간 다이렉트 클러스터의 특정 서버에 있는 특정 디스크에 대해 유지 관리 모드를 사용 하도록 설정할 수 있나요?

예, 특정 디스크 및 특정 장애 도메인에서 저장소 유지 관리 모드를 사용 하도록 설정할 수 있습니다. StorageMaintenanceMode 명령은 노드를 일시 중지할 때 자동으로 호출 됩니다. 다음 명령을 실행 하 여 특정 디스크에 대해이 기능을 사용 하도록 설정할 수 있습니다.

```powershell
Get-PhysicalDisk -SerialNumber <SerialNumber> | Enable-StorageMaintenanceMode
```

## <a name="is-storage-spaces-direct-supported-on-my-hardware"></a>하드웨어에서 스토리지 공간 다이렉트 지원 되나요?

하드웨어 공급 업체에 문의 하 여 지원을 확인 하는 것이 좋습니다. 하드웨어 공급 업체는 해당 하드웨어에서 솔루션을 테스트 하 고 지원 여부에 대 한 설명을 제공 합니다. 예를 들어,이 문서를 작성할 당시에는 R730/R730xd/R630와 같은 서버에서 드라이브 슬롯이 8 개를 초과 하는 서버는 SES를 지원할 수 있으며 스토리지 공간 다이렉트와 호환 됩니다. Dell은 스토리지 공간 다이렉트를 사용 하는 HBA330만 지원 합니다. R620는 SES를 지원 하지 않으며 스토리지 공간 다이렉트와 호환 되지 않습니다.

하드웨어 지원 정보에 대 한 자세한 내용을 보려면 Windows Server Catalog 웹 사이트로 이동 하세요.

## <a name="how-does-storage-spaces-direct-make-use-of-ses"></a>에서 SES를 사용 하 스토리지 공간 다이렉트 방법은 무엇 인가요?

스토리지 공간 다이렉트는 SES (SCSI 엔클로저 서비스) 매핑을 사용 하 여 데이터 줄임 및 메타 데이터가 장애 도메인 전체에 분산 되어 있는지 확인 합니다. 하드웨어에서 SES를 지원 하지 않는 경우 인클로저 매핑은 없으며 데이터 배치가 복원 되지 않습니다.

## <a name="which-command-can-you-use-to-check-the-physical-extent-for-a-virtual-disk"></a>가상 디스크의 물리적 범위를 확인 하는 데 사용할 수 있는 명령은 무엇입니까?

이것:

```powershell
get-virtualdisk -friendlyname "xyz" | get-physicalextent
```
