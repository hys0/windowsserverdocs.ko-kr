---
ms.assetid: d11acbc2-40c6-4ab2-9514-2bc3ad81499a
title: 데이터 중복 제거의 새로운 기능
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 04/17/2019
ms.openlocfilehash: 44a08443312d4e48b8fa518755e2a9b7aa50643c
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476088"
---
# <a name="whats-new-in-data-deduplication"></a>데이터 중복 제거의 새로운 기능

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

[데이터 중복 제거](overview.md) 매우 뛰어난 성능 제공을 유연 하 고 사설 클라우드 규모에서 관리 하도록 Windows Server에 최적화 되었습니다. Windows Server의 소프트웨어 정의 저장소 스택에 대 한 자세한 내용은 참조 하십시오 [What's New in Windows Server에서 저장소](../whats-new-in-storage.md)합니다.

데이터 중복 제거는 Windows Server 2019에서 다음과 같은 향상 된 기능을 가집니다.

| 기능 | 새로운 기능 또는 업데이트된 기능 | 설명 |
|---------------|----------------|-------------|
| ReFS 지원  | 단추를 사용하여 새            | 최대 10 배 이상의 데이터 중복 제거 및 ReFS 파일 시스템에 대 한 압축을 사용 하 여 동일한 볼륨에 저장 합니다. (있기 [하나만 클릭](https://www.youtube.com/watch?v=PRibTacyKko&feature=youtu.be) 를 Windows Admin Center 사용 하 여 켭니다.) 다중 스레드 사후 처리 아키텍처 유지 성능에 미치는 영향을 최소화 하는 동안 절감 비율이 최대화 하는 선택적 압축을 사용 하 여 가변 크기 청크 저장소입니다. 볼륨을 지 원하는 최대 64TB 및 각 파일의 첫 번째 4TB 중복 제거 됩니다.|

데이터 중복 제거에 Windows Server 2016부터 다음과 같은 향상 기능이 있습니다.

| 기능 | 새로운 기능 또는 업데이트된 기능 | 설명 |
|---------------|----------------|-------------|
| [대규모 볼륨 지원](whats-new.md#large-volume-support) | 업데이트됨 | Windows Server 2016 이전에는 특별히 예상되는 변동에 대비해 볼륨의 크기를 조정해야 했으며, 10TB가 넘는 볼륨은 중복 제거에 적합하지 않았습니다. Windows Server 2016에서는 데이터 중복 제거에서 최대 64TB의 볼륨 크기를 지원합니다. |
| [대용량 파일 지원](whats-new.md#large-file-support) | 업데이트됨 | Windows Server 2016 이전에는 크기가 1TB에 가까운 파일은 중복 제거에 적합하지 않았습니다. Windows Server 2016에서는 최대 1TB의 파일이 완전히 지원됩니다. |
| [Nano Server에 대 한 지원](whats-new.md#nano-server-support) | 단추를 사용하여 새 | 데이터 중복 제거는 Windows Server 2016의 새로운 Nano Server 배포 옵션에서 사용할 수 있으며 완전히 지원됩니다. |
| [간소화 된 백업 지원](whats-new.md#simple-backup-support) | 단추를 사용하여 새 | Windows Server 2012 R2에서는 일련의 수동 구성 단계를 통해 Microsoft의 [Data Protection Manager](https://technet.microsoft.com/library/hh758173.aspx)와 같은 가상화된 백업 응용 프로그램을 지원했습니다. Windows Server 2016에서는 가상화된 백업 응용 프로그램에 대한 데이터 중복 제거의 원활한 배포를 위해 새로운 기본 사용 유형(백업)이 추가되었습니다.|
| [클러스터 OS 롤링 업그레이드 지원](whats-new.md#cluster-upgrade-support) | 단추를 사용하여 새 | 데이터 중복 제거는 Windows Server 2016의 [클러스터 OS 롤링 업그레이드](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md) 기능을 완전히 지원합니다. |

## <a name="large-volume-support"></a>대규모 볼륨 지원

**이와 같은 변경을 통해 더해지는 가치**  
Windows Server 2012 R2에서 데이터 중복 제거를 통해 최상의 성능을 얻기 위해서는 최적화 작업이 데이터 변경 또는 "변동" 속도에 맞출 수 있도록 볼륨 크기를 적절히 조정해야 합니다. 일반적으로 이는 데이터 중복 제거가 워크로드의 쓰기 패턴에 따라 10TB 이하의 볼륨에서만 효과가 있음을 의미합니다.

Windows Server 2016에서는 최대 64TB의 볼륨에서 데이터 중복 제거가 뛰어난 효과를 제공합니다.

**달라진 기능**  
Windows Server 2012 R2 데이터 중복 제거 작업 파이프라인에서는 각 볼륨에 단일 스레드 및 I/O 큐를 사용합니다. 최적화 작업이 뒤처져 볼륨에 대한 전체 절감률이 저하되지 않도록 하려면 대규모 데이터 집합을 소규모 볼륨으로 분할해야 합니다. 적절한 볼륨 크기는 해당 볼륨의 예상 변동률에 따라 달라집니다. 평균적으로 최대값은 높은 변동 볼륨의 경우 6-7TB이고 낮은 변동 볼륨의 경우 9-10TB입니다.

Windows Server 2016에서는 데이터 중복 제거 작업 파이프라인이 각 볼륨에 대해 여러 I/O 큐를 사용하여 병렬로 여러 스레드를 실행하도록 다시 설계되었습니다. 따라서 이전에는 데이터를 여러 개의 작은 볼륨으로 분할해야만 가능했던 성능을 얻을 수 있게 되었습니다. 이 변경 내용이 다음 이미지에 나와 있습니다.

![Windows Server 2012 R2와 Windows Server 2016의 데이터 중복 제거 작업 파이프라인을 비교하는 시각화](media/server-2016-dedup-job-pipeline.png)

이러한 최적화는 최적화 작업뿐만 아니라 [모든 데이터 중복 제거 작업](understand.md#job-info)에 적용됩니다.

## <a name="large-file-support"></a>대용량 파일 지원
**이와 같은 변경을 통해 더해지는 가치**  
Windows Server 2012 R2에서 대용량 파일은 데이터 중복 제거 처리 파이프라인의 성능 저하로 인해 데이터 중복 제거에 적합하지 합니다. Windows Server 2016에서는 최대 1TB 파일의 중복 제거가 매우 효율적이므로 관리자는 보다 광범위한 워크로드에 중복 제거 절감 효과를 적용할 수 있습니다. 예를 들어 일반적으로 백업 워크로드와 관련된 대용량 파일의 중복 제거를 수행할 수 있습니다.

**달라진 기능**  
Windows Server 2016에서는 데이터 중복 제거에서 새로운 스트림 맵 구조 및 기타 "세부적인" 개선 사항을 활용하여 최적화 처리량 및 액세스 성능을 개선합니다. 또한 이제는 중복 제거 처리 파이프라인이 다시 시작하는 대신 장애 조치(failover) 후 최적화 진행을 재개할 수 있습니다. 이러한 변경 내용으로 인해 최대 1TB 파일에 대한 중복 제거가 매우 효율적입니다.

## <a name="nano-server-support"></a>Nano Server에 대 한 지원
**이와 같은 변경을 통해 더해지는 가치**  
Nano Server는 Windows Server 2016의 새로운 헤드리스 배포 옵션으로, Windows Server Core 배포 옵션보다 매우 작은 시스템 리소스 설치 공간이 필요하며, 훨씬 더 빠르게 시작되고, 필요한 업데이트 및 다시 시작 횟수가 더 적습니다. 데이터 중복 제거는 Nano Server에서 완전히 지원됩니다. Nano Server에 대한 자세한 내용은 [Nano Server 시작](../../get-started/getting-started-with-nano-server.md)을 참조하세요.

## <a name="simple-backup-support">가상화된 백업 응용 프로그램에 대한 간소화된 구성</a>
**이와 같은 변경을 통해 더해지는 가치**  
가상화된 백업 응용 프로그램에 대한 데이터 중복 제거는 Windows Server 2012 R2에서 지원되는 시나리오이지만 중복 제거 설정을 수동으로 조정해야 합니다. Windows Server 2016에서는 가상화된 백업 응용 프로그램에 대한 중복 제거 구성이 크게 간소화되었습니다. 볼륨에 대해 중복 제거를 사용하도록 설정하는 경우 일반용 파일 서버 및 VDI에 대한 옵션과 마찬가지로 미리 정의된 사용 유형 옵션이 사용됩니다.

## <a name="cluster-upgrade-support">클러스터 OS 롤링 업그레이드 지원</a>
**이와 같은 변경을 통해 더해지는 가치**  
데이터 중복 제거를 실행하는 Windows Server 장애 조치(failover) 클러스터에 Windows Server 2012 R2 버전의 데이터 중복 제거를 실행하는 노드와 Windows Server 2016 버전의 데이터 중복 제거를 실행하는 노드가 혼합되어 있을 수 있습니다. 이 향상된 기능은 클러스터 롤링 업그레이드 중 중복 제거된 모든 볼륨에 대한 완전한 데이터 액세스를 제공하므로 기존 Windows Server 2012 R2 클러스터에서 모든 노드를 한 번에 업그레이드하기 위한 가동 중지 시간 없이 새 버전의 데이터 중복 제거를 점진적으로 롤아웃할 수 있습니다.

**달라진 기능**<br />
이전 버전의 Windows Server에서는 Windows Server 장애 조치(failover) 클러스터의 모든 노드가 동일한 Windows Server 버전이어야 했습니다. Windows Server 2016부터는 클러스터 롤링 업그레이드 기능을 통해 클러스터를 혼합 모드로 실행할 수 있습니다. 데이터 중복 제거는 클러스터 롤링 업그레이드 중 완전한 데이터 액세스를 제공하기 위해 이 새로운 혼합 모드 클러스터 구성을 지원합니다.
