---
title: 스토리지 공간 다이렉트에서 내결함성 및 저장소 효율성
ms.prod: windows-server
ms.author: cosmosdarwin
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/11/2017
ms.assetid: 5e1d7ecc-e22e-467f-8142-bad6d82fc5d0
description: 미러링 및 패리티를 비롯 한 스토리지 공간 다이렉트의 복원 력 옵션에 대 한 설명입니다.
ms.localizationpriority: medium
ms.openlocfilehash: 540398e78b35d7cd61464e012d0f3ccfa85d7152
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475490"
---
# <a name="fault-tolerance-and-storage-efficiency-in-storage-spaces-direct"></a>스토리지 공간 다이렉트에서 내결함성 및 저장소 효율성

>적용 대상: Windows Server 2016

이 항목에서는 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 에서 사용할 수 있는 복원 력 옵션을 소개 하 고 각 요구 사항, 저장소 효율성 및 일반적인 장점과 장단점을 간략하게 설명 합니다. 또한 시작하기 위한 지침, 자세한 정보를 볼 수 있는 문서, 블로그 및 추가 콘텐츠도 안내합니다.

저장소 공간에 이미 익숙한 경우 [요약](#summary) 섹션으로 건너뛸 수 있습니다.

## <a name="overview"></a>개요

데이터에 대 한 저장소 공간은 주로 ' 복원 력 ' 이라고 하는 내결함성을 제공 하는 것입니다. 서버 전체에 분산 되 고 소프트웨어에서 구현 되는 경우를 제외 하 고는 RAID와 유사 하 게 구현 됩니다.

RAID와 마찬가지로 저장소 공간에서이 작업을 수행할 수 있는 몇 가지 방법이 있습니다 .이를 통해 내결함성, 저장소 효율성 및 계산 복잡성 간에 서로 다른 균형을 유지할 수 있습니다. 이러한 두 가지 범주는 ' 미러링 ' 및 ' 패리티 ', 후자는 ' 지우기 코딩 ' 이라고 합니다.

## <a name="mirroring"></a>미러링

미러링은 모든 데이터의 여러 복사본을 유지 하 여 내결함성을 제공 합니다. 이는 RAID-1과 매우 유사 합니다. 데이터를 스트라이프 하 고 배치 하는 방법은 중요 하지 않습니다 (자세한 내용은 [이 블로그](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/) 를 참조). 그러나 미러링을 사용 하 여 저장 된 데이터는 전체적으로 여러 번 기록 됩니다. 각 복사본은 독립적으로 실패 하는 것으로 간주 되는 다른 실제 하드웨어 (서버 마다 다른 드라이브)에 기록 됩니다.

Windows Server 2016에서 저장소 공간은 ' 양방향 ' 및 ' 3 방향 '의 두 가지 미러링 기능을 제공 합니다.

### <a name="two-way-mirror"></a>양방향 미러

양방향 미러링은 모든 항목의 복사본 두 개를 작성 합니다. 저장소 효율성이 50% – 1TB의 데이터를 쓰려면 최소한 2tb의 실제 저장소 용량이 필요 합니다. 마찬가지로 두 대 이상의 [하드웨어 ' 장애 도메인 '](../../failover-clustering/fault-domains.md) 이 필요 합니다. 즉, 스토리지 공간 다이렉트는 두 개의 서버를 의미 합니다.

![양방향 미러](media/Storage-Spaces-Fault-Tolerance/two-way-mirror-180px.png)

   >[!WARNING]
   > 서버를 셋 이상 사용 하는 경우에는 3 방향 mirorring을 대신 사용 하는 것이 좋습니다.

### <a name="three-way-mirror"></a>3방향 미러

3 방향 미러링은 모든 항목의 복사본 세 개를 작성 합니다. 저장소 효율성이 33.3% – 1TB의 데이터를 쓰려면 최소 3TB의 실제 저장소 용량이 필요 합니다. 마찬가지로 하드웨어 장애 도메인은 3 개 이상 필요 합니다. 즉, 스토리지 공간 다이렉트은 3 개의 서버를 의미 합니다.

3 방향 미러링은 [한 번에 두 개 이상의 하드웨어 문제 (드라이브 또는 서버)](#examples)를 안전 하 게 허용할 수 있습니다. 예를 들어, 갑자기 다른 드라이브나 서버에 오류가 발생할 때 한 서버를 다시 부팅 하는 경우 모든 데이터는 안전 하 게 유지 되 고 지속적으로 액세스할 수 있습니다.

![3 방향 미러](media/Storage-Spaces-Fault-Tolerance/three-way-mirror-180px.png)

## <a name="parity"></a>Parity

' 지우기 코딩 ' 이라고 하는 패리티 인코딩은 매우 [복잡](https://www.microsoft.com/research/wp-content/uploads/2016/02/LRC12-cheng20webpage.pdf)해질 수 있는 비트 산술 연산을 사용 하 여 내결함성을 제공 합니다. 이 방법은 미러링 보다 명확 하지 않으며, 아이디어를 얻는 데 도움이 될 수 있는 많은 유용한 온라인 리소스 (예: [코드를 지우기 위한이 타사 Dummies 가이드](http://smahesh.com/blog/2012/07/01/dummies-guide-to-erasure-coding/))가 있습니다. 내결함성을 손상 시 키 지 않고 저장소 효율성을 향상 Sufficed.

Windows Server 2016에서 저장소 공간은 두 가지 유형의 패리티 인 ' 단일 ' 패리티와 ' 이중 ' 패리티를 제공 하 고, 후자는 더 큰 규모에서 ' 로컬 재구성 코드 ' 라는 고급 기술을 채택 합니다.

> [!IMPORTANT]
> 대부분의 성능에 민감한 워크 로드에 대해 미러링을 사용 하는 것이 좋습니다. 워크 로드에 따라 성능 및 용량을 조정 하는 방법에 대해 자세히 알아보려면 [볼륨 계획](plan-volumes.md#choosing-the-resiliency-type)을 참조 하세요.

### <a name="single-parity"></a>단일 패리티
단일 패리티는 한 번에 하나의 오류에 대 한 내결함성을 제공 하는 하나의 비트 패리티 기호만 유지 합니다. RAID-5와 가장 유사 합니다. 단일 패리티를 사용 하려면 3 개 이상의 하드웨어 장애 도메인이 필요 합니다. 즉, 스토리지 공간 다이렉트은 3 개의 서버를 의미 합니다. 3 방향 미러링은 동일한 규모에서 더 많은 내결함성을 제공 하므로 단일 패리티를 사용 하지 않습니다. 그러나 사용을 안내 하는 경우에는 완전히 지원 됩니다.

   >[!WARNING]
   > 한 번에 하나의 하드웨어 장애로 안전 하 게 허용할 수 있으므로 단일 패리티를 사용 하지 않도록 합니다. 갑자기 다른 드라이브나 서버가 실패할 때 한 서버를 다시 부팅 하는 경우 가동 중지 시간이 발생 합니다. 서버가 3 대만 있는 경우에는 3 방향 미러링을 사용 하는 것이 좋습니다. 4 개 이상이 있는 경우 다음 섹션을 참조 하세요.

### <a name="dual-parity"></a>이중 패리티

이중 패리티는 두 비트 패리티 기호를 유지 하는 리드-솔로몬 오류 수정 코드를 구현 하 여 3 방향 미러링과 동일한 내결함성을 제공 합니다 (즉, 한 번에 최대 두 번까지 실패). 그러나 저장소 효율성이 향상 됩니다. RAID-6과 매우 비슷합니다. 이중 패리티를 사용 하려면 4 개 이상의 하드웨어 장애 도메인이 있어야 합니다. 즉, 스토리지 공간 다이렉트은 4 개 서버를 의미 합니다. 이 규모에서 저장소 효율성이 50% – 2tb의 데이터를 저장 하는 데는 1tb의 물리적 저장소 용량이 필요 합니다.

![이중 패리티](media/Storage-Spaces-Fault-Tolerance/dual-parity-180px.png)

이중 패리티의 저장소 효율성을 통해 더 많은 하드웨어 장애 도메인을 50% (최대 80%)까지 늘릴 수 있습니다. 예를 들어 7 개 (스토리지 공간 다이렉트, 7 대의 서버)에서 효율성은 66.7%로 이동 하 여 4tb의 데이터를 저장 하는 데 사용할 수 있습니다. 실제 저장소 용량은 6tb 뿐입니다.

![이중 패리티 수준](media/Storage-Spaces-Fault-Tolerance/dual-parity-wide-180px.png)

모든 규모에서 이중 파티 및 로컬 재구성 코드의 효율성은 [요약](#summary) 섹션을 참조 하세요.

### <a name="local-reconstruction-codes"></a>로컬 재구성 코드

Windows Server 2016의 저장소 공간에는 ' 로컬 재구성 코드 ' 또는 LRC 라는 Microsoft Research에서 개발한 고급 기술이 도입 되었습니다. 대규모의 경우 이중 패리티는 LRC를 사용 하 여 인코딩/디코딩을 몇 개의 작은 그룹으로 분할 하 여 쓰기를 수행 하거나 오류를 복구 하는 데 필요한 오버 헤드를 줄입니다.

HDD (하드 디스크 드라이브)를 사용 하 여 그룹 크기는 4 개의 기호입니다. SSD (반도체 드라이브)를 사용 하 여 그룹 크기는 6 개의 기호입니다. 예를 들어, 하드 디스크 드라이브 및 12 개의 하드웨어 장애 도메인 (10 개 서버)의 레이아웃은 다음과 같습니다. 4 개의 데이터 기호 그룹이 있습니다. 72.7% 저장소 효율성을 달성 합니다.

![local-reconstruction-codes](media/Storage-Spaces-Fault-Tolerance/local-reconstruction-codes-180px.png)

[로컬 재구성 코드에서 다양 한 오류 시나리오를 처리 하는 방법 및](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)매우 고유한 [Claus Joergensen](https://twitter.com/clausjor)에 의해 유용한 이유를 심층적으로 eminently 읽을 수 있는 연습을 진행 하는 것이 좋습니다.

## <a name="mirror-accelerated-parity"></a>미러 가속 패리티

Windows Server 2016부터 스토리지 공간 다이렉트 볼륨은 미러 파트 및 파트 패리티 일 수 있습니다. 첫 번째 위치를 미러된 부분에 쓰고 나중에 패리티 부분으로 점차적으로 이동 합니다. 효과적으로이는 [미러링을 사용 하 여 지우기 코딩을 가속화](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)합니다.

3 방향 미러 및 이중 패리티를 혼합 하려면 4 개 이상의 장애 도메인이 있어야 합니다. 4 개 이상의 서버를 의미 합니다.

미러 가속 패리티의 저장소 효율성은 모든 미러 또는 모든 패리티를 사용 하 여 얻을 수 있는 것 사이에 있으며 선택한 비율에 따라 달라 집니다. 예를 들어이 프레젠테이션의 37 분 표시에 포함 된 데모는 12 개 서버에서 [46%, 54% 및 65% 효율성을 달성 하는 다양 한 혼합](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s) 을 보여 줍니다.

> [!IMPORTANT]
> 대부분의 성능에 민감한 워크 로드에 대해 미러링을 사용 하는 것이 좋습니다. 워크 로드에 따라 성능 및 용량을 조정 하는 방법에 대해 자세히 알아보려면 [볼륨 계획](plan-volumes.md#choosing-the-resiliency-type)을 참조 하세요.

## <a name="summary"></a><a name="summary"></a>요약

이 섹션에서는 스토리지 공간 다이렉트에서 사용할 수 있는 복원 력 유형, 각 유형을 사용 하기 위한 최소 규모 요구 사항, 각 유형이 허용할 수 있는 오류 수 및 해당 저장소 효율성을 요약 합니다.

### <a name="resiliency-types"></a>복원 력 유형

|    복원력          |    실패 허용 오차       |    저장소 효율성      |
|------------------------|----------------------------|----------------------------|
|    양방향 미러      |    1                       |    50.0%                   |
|    3방향 미러    |    2                       |    33.3%                   |
|    이중 패리티         |    2                       |    50.0%-80.0%           |
|    혼합됨               |    2                       |    33.3%-80.0%           |

### <a name="minimum-scale-requirements"></a>최소 크기 조정 요구 사항

|    복원력          |    최소 필수 장애 도메인   |
|------------------------|-------------------------------------|
|    양방향 미러      |    2                                |
|    3방향 미러    |    3                                |
|    이중 패리티         |    4                                |
|    혼합됨               |    4                                |

   >[!TIP]
   > [섀시 또는 랙 내결함성을](../../failover-clustering/fault-domains.md)사용 하지 않는 경우 장애 도메인 수는 서버 수를 나타냅니다. 스토리지 공간 다이렉트에 대 한 최소 요구 사항을 충족 하는 한 각 서버의 드라이브 수는 사용할 수 있는 복원 력 유형에 영향을 주지 않습니다.

### <a name="dual-parity-efficiency-for-hybrid-deployments"></a>하이브리드 배포에 대 한 이중 패리티 효율성

이 표에서는 HDD (하드 디스크 드라이브)와 SSD (반도체 드라이브)를 모두 포함 하는 하이브리드 배포를 위해 각 규모에서 이중 패리티 및 로컬 재구성 코드의 저장소 효율성을 보여 줍니다.

|    장애 도메인      |    Layout           |    효율성   |
|-----------------------|---------------------|-----------------|
|    2                  |    –                |    –            |
|    3                  |    –                |    –            |
|    4                  |    RS 2 + 2           |    50.0%        |
|    5                  |    RS 2 + 2           |    50.0%        |
|    6                  |    RS 2 + 2           |    50.0%        |
|    7                  |    RS 4 + 2           |    66.7%        |
|    8                  |    RS 4 + 2           |    66.7%        |
|    9                  |    RS 4 + 2           |    66.7%        |
|    10                 |    RS 4 + 2           |    66.7%        |
|    11                 |    RS 4 + 2           |    66.7%        |
|    12                 |    LRC (8, 2, 1)    |    72.7%        |
|    13                 |    LRC (8, 2, 1)    |    72.7%        |
|    14                 |    LRC (8, 2, 1)    |    72.7%        |
|    15                 |    LRC (8, 2, 1)    |    72.7%        |
|    16                 |    LRC (8, 2, 1)    |    72.7%        |

### <a name="dual-parity-efficiency-for-all-flash-deployments"></a>모든 플래시 배포에 대 한 이중 패리티 효율성

이 표에서는 SSD (반도체 드라이브)만 포함 하는 모든 플래시 배포를 위한 각 규모에서 이중 패리티 및 로컬 재구성 코드의 저장소 효율성을 보여 줍니다. 패리티 레이아웃은 더 큰 그룹 크기를 사용 하 고 모든 플래시 구성에서 더 나은 저장소 효율성을 달성할 수 있습니다.

|    장애 도메인      |    Layout           |    효율성   |
|-----------------------|---------------------|-----------------|
|    2                  |    –                |    –            |
|    3                  |    –                |    –            |
|    4                  |    RS 2 + 2           |    50.0%        |
|    5                  |    RS 2 + 2           |    50.0%        |
|    6                  |    RS 2 + 2           |    50.0%        |
|    7                  |    RS 4 + 2           |    66.7%        |
|    8                  |    RS 4 + 2           |    66.7%        |
|    9                  |    RS 6 + 2           |    75.0%        |
|    10                 |    RS 6 + 2           |    75.0%        |
|    11                 |    RS 6 + 2           |    75.0%        |
|    12                 |    RS 6 + 2           |    75.0%        |
|    13                 |    RS 6 + 2           |    75.0%        |
|    14                 |    RS 6 + 2           |    75.0%        |
|    15                 |    RS 6 + 2           |    75.0%        |
|    16                 |    LRC (12, 2, 1)   |    80.0%        |

## <a name="examples"></a><a name="examples"></a>예제

서버가 두 개만 있는 경우를 제외 하 고는 3 방향 미러링 및/또는 이중 패리티를 사용 하는 것이 좋습니다 .이는 더 나은 내결함성을 제공 하기 때문입니다. 특히 두 개의 장애 도메인 (두 서버를 의미 하는 두 개의 장애 도메인을 스토리지 공간 다이렉트 사용 하 여 동시에 오류가 발생 하는 경우)에도 모든 데이터를 안전 하 고 지속적으로 액세스할 수 있습니다.

### <a name="examples-where-everything-stays-online"></a>모든 항목이 온라인 상태로 유지 되는 예

다음 6 개 예제에서는 3 방향 미러링 및/또는 이중 패리티를 허용할 **수** 있는 방법을 보여 줍니다.

- **1.** 한 드라이브가 손실 됩니다 (캐시 드라이브 포함).
- **2.** 서버 하나 손실

![내결함성-예-1-및-2](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-12.png)

- **3.** 한 서버와 하나의 드라이브가 손실 됩니다.
- **4.** 다른 서버에서 두 드라이브가 손실 됨

![fault-tolerance-examples-3-and-4](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-34.png)

- **5.** 최대 두 대의 서버가 영향을 받는 경우에는 두 개 이상의 드라이브가 손실 됩니다.
- **6.** 두 서버 손실

![내결함성-예-5-및-6](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-56.png)

... 모든 경우에서 모든 볼륨이 온라인 상태로 유지 됩니다. 클러스터가 쿼럼을 유지 관리 하는지 확인 합니다.

### <a name="examples-where-everything-goes-offline"></a>모든 항목이 오프 라인 상태가 되는 예

수명 주기 동안 저장소 공간은 충분 한 시간을 지정 하 여 각 시간 후에 전체 복원 력을 복원 하기 때문에 오류를 발생 시킬 수 있습니다. 그러나 최대 2 개의 장애 도메인은 지정 된 순간의 실패에 의해 안전 하 게 영향을 받을 수 있습니다. 따라서 다음은 3 방향 미러링 및/또는 이중 패리티를 허용할 **수 없는** 예입니다.

- **7.** 한 번에 세 개 이상의 서버에서 분실 된 드라이브
- **8.** 한 번에 세 개 이상의 서버가 손실 됨

![내결함성-예-7-및-8](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-78.png)

## <a name="usage"></a>사용량

[스토리지 공간 다이렉트에서 볼륨 만들기를](create-volumes.md)확인 합니다.

## <a name="additional-references"></a>추가 참조

아래의 모든 링크는이 항목 본문의 어딘가에 있습니다.

- [Windows Server 2016의 스토리지 공간 다이렉트](storage-spaces-direct-overview.md)
- [Windows Server 2016의 장애 도메인 인식](../../failover-clustering/fault-domains.md)
- [Microsoft Research에서 Azure의 코딩 지우기](https://www.microsoft.com/research/publication/erasure-coding-in-windows-azure-storage/)
- [로컬 재구성 코드 및 가속화 패리티 볼륨](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)
- [저장소 관리 API의 볼륨](https://blogs.technet.microsoft.com/filecab/2016/08/29/deep-dive-volumes-in-spaces-direct/)
- [Microsoft Ignite 2016의 저장소 효율성 데모](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s)
- [스토리지 공간 다이렉트에 대 한 용량 계산기 미리 보기](https://aka.ms/s2dcalc)
