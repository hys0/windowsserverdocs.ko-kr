---
title: 스토리지 공간 다이렉트에서 서버 제거
ms.assetid: 9d8499a7-1307-473d-9f00-8a051164fad2
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
description: Windows Server의 스토리지 공간 다이렉트 클러스터에서 서버를 제거 하는 방법
ms.date: 2/5/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dd888048edc96d6001492e92ba6d519c751bdaa
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474570"
---
# <a name="removing-servers-in-storage-spaces-direct"></a>스토리지 공간 다이렉트에서 서버 제거

>적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 PowerShell을 사용 하 여 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 에서 서버를 제거 하는 방법을 설명 합니다.

## <a name="remove-a-server-but-leave-its-drives"></a>서버를 제거 하지만 드라이브는 그대로 둡니다.

서버를 즉시 클러스터에 추가 하려는 경우 또는 해당 드라이브를 다른 서버로 이동 하 여 유지 하려는 경우 저장소 풀에서 해당 드라이브를 제거 *하지 않고* 클러스터에서 서버를 제거할 수 있습니다. 이는 장애 조치(Failover) 클러스터 관리자을 사용 하 여 서버를 제거 하는 경우의 기본 동작입니다.

PowerShell에서 [start-clusternode](https://technet.microsoft.com/library/hh847251.aspx) cmdlet을 사용 합니다.

```PowerShell
Remove-ClusterNode <Name>
```

저장소 풀은 누락 된 드라이브를 "기억" 하 여 다시 돌아올 것으로 예상 하므로 용량 고려 사항에 관계 없이이 cmdlet은 빠르게 성공 합니다. 누락 된 드라이브에서 멀리 떨어진 데이터 이동이 없습니다. 누락 된 상태로 유지 되는 경우에는 **OperationalStatus** 가 "통신 끊김"으로 표시 되 고 볼륨에 "불완전"이 표시 됩니다.

드라이브가 돌아오면 새 서버에 있는 경우에도 자동으로 검색 되어 풀과 연결 됩니다.

   >[!WARNING]
   > 한 서버에서 여러 다른 서버로 풀 데이터를 포함 하는 드라이브를 배포 하지 마십시오. 예를 들어 10 개의 드라이브가 있는 서버 하나에서 오류가 발생 하는 경우 (예를 들어 해당 마더보드 또는 부팅 드라이브는 실패 했기 때문에) 10 개의 드라이브를 모두 하나의 새 서버로 이동할 **수** 있지만 각각의 다른 서버에 개별적으로 이동할 **수는 없습니다** .

## <a name="remove-a-server-and-its-drives"></a>서버 및 해당 드라이브 제거

클러스터에서 서버를 영구적으로 제거 하려는 경우 (확장이 라고도 함) 클러스터에서 서버를 제거 하 *고* 저장소 풀에서 해당 드라이브를 제거할 수 있습니다.

선택적 **-cleanupdisks** 플래그와 함께 **start-clusternode** cmdlet을 사용 합니다.

```PowerShell
Remove-ClusterNode <Name> -CleanUpDisks
```

Windows에서 해당 서버에 저장 된 모든 데이터를 클러스터의 다른 서버로 이동 해야 하기 때문에이 cmdlet을 실행 하는 데 시간이 오래 걸릴 수 있습니다. 이 작업이 완료 되 면 드라이브가 저장소 풀에서 영구적으로 제거 되 고, 영향을 받은 볼륨이 정상 상태로 돌아갑니다.

### <a name="requirements"></a>요구 사항

영구적으로 규모를 확장 (서버 *와* 드라이브 제거) 하려면 클러스터가 다음 두 가지 요구 사항을 충족 해야 합니다. 그렇지 않은 경우 **start-clusternode-CleanUpDisks** cmdlet은 데이터 이동을 시작 하기 전에 오류를 즉시 반환 하 여 중단을 최소화 합니다.

#### <a name="enough-capacity"></a>충분 한 용량

먼저 모든 볼륨을 수용할 수 있도록 남은 서버에 충분 한 저장소 용량이 있어야 합니다.

예를 들어 4 대의 서버가 있고 각 서버에 10 x 1tb 드라이브가 있는 경우 총 40의 실제 저장소 용량을 사용할 수 있습니다. 서버와 해당 드라이브를 모두 제거한 후에는 30tb의 용량이 남아 있습니다. 볼륨의 차지가 함께 30tb를 초과 하는 경우 나머지 서버에 들어가지 않으므로 cmdlet은 오류를 반환 하 고 데이터를 이동 하지 않습니다.

#### <a name="enough-fault-domains"></a>충분 한 장애 도메인

두 번째로 볼륨의 복원 력을 제공 하는 데 충분 한 장애 도메인 (일반적으로 서버)이 있어야 합니다.

예를 들어 볼륨에서 복원 력을 위해 서버 수준에서 3 방향 미러링을 사용 하는 경우 서버를 3 개 이상 사용 하지 않으면 완전히 정상 상태가 아닙니다. 정확히 3 개의 서버가 있는 경우 하나 및 모든 드라이브를 제거 하려고 하면 cmdlet에서 오류를 반환 하 고 데이터를 이동 하지 않습니다.

다음 표에서는 각 복원 력 유형에 필요한 최소 장애 도메인 수를 보여 줍니다.

|    복원력          |    최소 필수 장애 도메인   |
|------------------------|-------------------------------------|
|    양방향 미러      |    2                                |
|    3방향 미러    |    3                                |
|    이중 패리티         |    4                                |

   >[!NOTE]
   > 오류가 발생 하거나 유지 관리 하는 경우와 같이 서버 수를 줄일 수 있습니다. 그러나 볼륨이 완전히 정상 상태가 되도록 하려면 위에 나열 된 최소 서버 수가 있어야 합니다.

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
