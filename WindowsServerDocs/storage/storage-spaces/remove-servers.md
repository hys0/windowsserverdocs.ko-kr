---
title: 저장소 공간 다이렉트에서 서버 제거
ms.assetid: 9d8499a7-1307-473d-9f00-8a051164fad2
ms.prod: windows-server
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
description: Windows Server의 저장소 공간 다이렉트 클러스터에서 서버를 제거하는 방법.
ms.date: 2/5/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce8caef2b51279c97cc012045750b7a73d97a4ba
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322315"
---
# <a name="removing-servers-in-storage-spaces-direct"></a>저장소 공간 다이렉트에서 서버 제거

>적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 PowerShell을 사용하여 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)에서 서버를 제거하는 방법을 설명합니다.

## <a name="remove-a-server-but-leave-its-drives"></a>서버는 제거하고 드라이브는 남겨 두기

클러스터에 서버를 다시 추가하려는 경우 또는 다른 서버로 드라이브를 옮겨서 보관하려는 경우 저장소 풀에서 드라이브를 제거하지 *않고도* 클러스터에서 서버를 제거할 수 있습니다. 장애 조치(failover) 클러스터 관리자를 사용하여 서버를 제거하는 경우의 기본 동작입니다.

다음과 같이 PowerShell에서 [Remove-ClusterNode](https://technet.microsoft.com/library/hh847251.aspx) cmdlet을 사용합니다.

```PowerShell
Remove-ClusterNode <Name>
```

저장소 풀이 누락된 드라이브를 '기억'하고 다시 복원될 것으로 예상하기 때문에 이 cmdlet은 용량에 대한 고려 사항과 관계없이 빠르게 성공합니다. 누락된 드라이브로부터 데이터가 이동하지 않습니다. 누락된 상태로 유지되는 동안 **OperationalStatus**는 'Lost Communication'(연결이 끊어짐)'으로 표시되며 볼륨은 'Incomplete'(불완전)로 표시됩니다.

드라이브가 복원되면 이제 새로운 서버에 있는 경우에도 자동으로 감지되고 풀과 다시 연결됩니다.

   >[!WARNING]
   > 풀 데이터가 있는 드라이브를 하나의 서버에서 여러 개의 다른 서버로 배포하면 안 됩니다. 예를 들어 10개의 드라이브가 있는 서버 하나에 장애가 발생하는 경우(예: 마더 보드 또는 부팅 드라이브에 장애가 발생하는 경우) 사용자는 새로운 서버 하나에 10개의 드라이브를 모두 옮길 수 **있지만** 여러 개의 다른 서버에 개별적으로는 옮길 수 **없습니다**.

## <a name="remove-a-server-and-its-drives"></a>서버 및 드라이브 제거

클러스터에서 서버를 영구적으로 제거(때에 따라 '스케일 인'이라고도 함)하려는 경우 클러스터의 서버 제거 작업 *및* 저장소 풀의 드라이브 제거 작업을 수행할 수 있습니다.

다음과 같이 **Remove-ClusterNode** cmdlet 및 **-CleanUpDisks** 플래그(옵션)를 사용합니다.

```PowerShell
Remove-ClusterNode <Name> -CleanUpDisks
```

Windows에서 해당 서버에 저장된 모든 데이터를 클러스터의 다른 서버로 옮겨야 하기 때문에 이 cmdlet을 실행하는 데 시간이 오래 소요될 수 있습니다(때에 따라 몇 시간이 걸릴 수도 있음). 이 작업이 완료되면 저장소 풀에서 드라이브가 영구적으로 제거되어 영향을 받은 볼륨을 정상 상태로 되돌립니다.

### <a name="requirements"></a>요구 사항

영구적으로 스케일 인(서버 *및* 드라이브 제거)을 하려면 클러스터는 다음과 같은 두 가지 요구 사항을 충족해야 합니다. 그렇지 않은 경우 **Remove-ClusterNode -CleanUpDisks** cmdlet은 중단을 최소화하기 위해 데이터 이동 전에 즉시 오류를 반환합니다.

#### <a name="enough-capacity"></a>충분한 용량

먼저 모든 볼륨을 수용할 수 있도록 남은 서버에 충분 한 저장소 용량이 있어야 합니다.

예를 들어, 각각 10 x 1TB 드라이브를 가진 4개의 서버가 있는 경우 40TB의 전체 물리적 저장소 용량을 갖게 됩니다. 하나의 서버와 해당 드라이브를 모두 제거한 후에 30TB의 용량이 남습니다. 볼륨의 사용 공간이 30TB를 초과하면 나머지 서버에 맞지 않으므로 cmdlet은 오류를 반환하고 데이터를 옮기지 않습니다.

#### <a name="enough-fault-domains"></a>충분한 장애 도메인

두 번째로, 볼륨의 복원력을 제공하려면 충분한 장애 도메인(일반적으로 서버)이 있어야 합니다.

예를 들어 볼륨이 복원력을 위해 서버 수준으로 3방향 미러링을 사용하는 경우 최소 세 개의 서버가 없는 이상 해당 볼륨은 완전히 정상적인 상태가 될 수 없습니다. 정확히 세 개의 서버가 있고 이 중 하나의 서버와 해당 드라이브를 모두 제거하려는 경우 cmdlet은 오류를 반환하고 데이터를 옮기지 않습니다.

이 표는 각 복원력 유형에 필요한 최소 장애 도메인 수를 보여 줍니다.

|    복원력          |    필요한 최소 장애 도메인   |
|------------------------|-------------------------------------|
|    양방향 미러      |    2                                |
|    3방향 미러    |    3                                |
|    이중 패리티         |    4                                |

   >[!NOTE]
   > 장애 발생 또는 유지 관리 등 특정 시점에 잠시 동안 서버 수를 줄이는 것이 좋습니다. 그러나 볼륨을 완전히 정상적인 상태로 되돌리려면 위에 나열된 최소 서버 수가 있어야 합니다.

## <a name="see-also"></a>참고 항목

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
