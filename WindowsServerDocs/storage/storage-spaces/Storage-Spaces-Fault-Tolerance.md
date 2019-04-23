---
title: 저장소 공간 다이렉트의 내결함성 및 저장소 효율성
ms.prod: windows-server-threshold
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/11/2017
ms.assetid: 5e1d7ecc-e22e-467f-8142-bad6d82fc5d0
description: 미러링 및 패리티를 포함하는 저장소 공간 다이렉트의 복원력 옵션에 대한 설명.
ms.localizationpriority: medium
ms.openlocfilehash: 4e6a29e82a85ec9570cda827060dfe1cdf192c53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849574"
---
# <a name="fault-tolerance-and-storage-efficiency-in-storage-spaces-direct"></a>저장소 공간 다이렉트의 내결함성 및 저장소 효율성

>적용 대상: Windows Server 2016

이 항목에서는 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)에서 사용 가능한 복원력 옵션을 소개하고 각 옵션의 확장 요구 사항, 저장소 효율성 및 일반적인 장단점을 설명합니다. 또한 시작하기 위한 지침, 자세한 정보를 볼 수 있는 문서, 블로그 및 추가 콘텐츠도 안내합니다.

저장소 공간에 익숙한 경우 [요약](#summary) 섹션으로 건너뛸 수 있습니다.

## <a name="overview"></a>개요

기본적으로 저장소 공간은 데이터에 대한 내결함성('복원력'이라고도 함)을 제공하기 위한 것입니다. 여러 서버로 분산되며 소프트웨어에서 구현된다는 점을 제외하면 RAID와 비슷합니다.

RAID와 마찬가지로 저장소 공간은 몇 가지 방법으로 내결함성을 제공합니다. 각 방법의 내결함성, 저장소 효율성 및 계산 복잡성에 대한 장단점이 서로 다릅니다. 이 기능은 크게 '미러링'과 '패리티'의 두 범주로 나뉘며 패리티를 '이레이저 코딩(erasure coding)'이라고도 합니다.

## <a name="mirroring"></a>미러링

미러링은 모든 데이터의 복사본 여러 개를 유지하여 내결함성을 제공합니다. RAID-1과 가장 비슷합니다. 데이터가 스트라이프 및 배치되는 방식은 꽤 복잡하지만 미러링을 사용하여 저장되는 모든 데이터는 여러 번 기록된다는 점은 확실한 사실입니다(자세히 알아보려면 [이 블로그](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/) 참조). 각 복사본은 실패하더라도 다른 하드웨어에 영향을 미치지 않는 서로 다른 물리적 하드웨어(다른 서버의 다른 드라이브)에 기록됩니다.

Windows Server 2016에서 저장소 공간은 '양방향'과 '3방향'의 두 가지 미러링 유형을 제공합니다.

### <a name="two-way-mirror"></a>양방향 미러

양방향 미러링은 모든 항목의 복사본을 두 개 기록합니다. 저장소 효율성은 50%입니다. 즉, 1TB의 데이터를 기록하려면 최소 2TB의 물리적 저장소 용량이 필요합니다. 마찬가지로, 최소 두 개의 [하드웨어 '오류 도메인'](../../failover-clustering/fault-domains.md)이 필요하며 저장소 공간 다이렉트 사용 시 이는 두 개의 서버가 필요함을 의미합니다.

![양방향 미러](media/Storage-Spaces-Fault-Tolerance/two-way-mirror-180px.png)

   >[!WARNING]
   > 세 개 이상의 서버를 사용하는 경우 대신 3방향 미러링을 사용하는 것이 좋습니다.

### <a name="three-way-mirror"></a>3방향 미러

3방향 미러링은 모든 항목의 복사본을 세 개 만듭니다. 저장소 효율성은 33.3%입니다. 즉, 1TB의 데이터를 기록하려면 최소한 3TB의 물리적 저장소 용량이 필요합니다. 마찬가지로, 최소 세 개의 하드웨어 오류 도메인이 필요하며 저장소 공간 다이렉트 사용 시 이는 세 개의 서버가 필요함을 의미합니다.

3방향 미러링은 [한 번에 두 개 이상 하드웨어 문제(드라이브 또는 서버)](#examples)를 안전하게 허용할 수 있습니다. 예를 들어 갑자기 또 다른 드라이브나 서버에 장애가 발생할 때 서버 하나를 재부팅하는 경우 모든 데이터가 안전하고 지속적으로 액세스할 수 있는 상태로 유지됩니다.

![3방향 미러](media/Storage-Spaces-Fault-Tolerance/three-way-mirror-180px.png)

## <a name="parity"></a>패리티

'이레이저 코딩'이라고도 하는 패리티 인코딩은 [매우 복잡해질 수 있는](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/LRC12-cheng20webpage.pdf) 비트 산술 연산을 사용하여 내결함성을 제공합니다. 이 유형은 미러링에 비해 작동 방식이 명료하지 않으며 많은 온라인 리소스(예: 타사 자료인 [Dummies Guide to Erasure Coding](http://smahesh.com/blog/2012/07/01/dummies-guide-to-erasure-coding/)(초보자를 위한 이레이저 코딩 가이드))를 통해 개념을 파악할 수 있습니다. 여기서는 내결함성의 저하 없이 저장소 효율성이 더 높다는 점만 이해하는 것으로 충분합니다.

Windows Server 2016에서 저장소 공간은 '단일' 패리티와 '이중' 패리티의 두 가지 패리티 유형을 제공합니다. 이중 패리티는 '로컬 재구성 코드'라고 하는 고급 기술을 더 큰 규모로 채용합니다.

> [!IMPORTANT]
> 성능이 가장 중요한 워크로드에 대한 미러링을 사용하는 것이 좋습니다. 워크로드에 따라 성능과 용량의 균형을 맞추는 방법에 관한 자세한 내용은 [볼륨 계획](plan-volumes.md#choosing-the-resiliency-type)을 참조하세요.

### <a name="single-parity"></a>단일 패리티
단일 패리티는 하나의 비트 패리티 기호만 유지하며 이에 따라 한 번에 하나의 오류에 대해서만 내결함성을 제공합니다. RAID-5와 가장 비슷합니다. 단일 패리티를 사용하려면 최소 세 개의 하드웨어 오류 도메인이 필요하며 저장소 공간 다이렉트 사용 시 이는 세 개의 서버가 필요함을 의미합니다. 동일한 규모일 때 3방향 미러링이 더 높은 내결함성을 제공하므로 단일 패리티의 사용은 권장하지 않습니다. 하지만 사용하려는 사용자를 위해 제공되며 완전히 지원됩니다.

   >[!WARNING]
   > 한 번에 하나의 하드웨어 오류만 허용할 수 있기 때문에 단일 패리티의 사용은 권장하지 않습니다. 갑자기 또 다른 드라이브나 서버에 장애가 발생할 때 서버 하나를 재부팅하는 경우 가동 중단 시간이 발생합니다. 서버가 세 개만 있는 경우에는 3방향 미러링을 사용하는 것이 좋습니다. 서버가 네 개 이상인 경우에는 다음 섹션을 참조하세요.

### <a name="dual-parity"></a>이중 패리티

이중 패리티는 리드-솔로몬 오류 보정 코드를 구현하여 두 개의 비트 패리티 기호를 유지하며 따라서 3방향 미러링과 동일한 내결합성을 제공하지만(즉, 한 번에 최대 두 개의 오류) 저장소 효율성은 더 높습니다. RAID-6과 가장 비슷합니다. 이중 패리티를 사용하려면 최소 네 개의 하드웨어 오류 도메인이 필요하며 저장소 공간 다이렉트 사용 시 이는 네 개의 서버가 필요함을 의미합니다. 이 규모에서 저장소 효율성은 50%입니다. 즉, 2TB의 데이터를 기록하려면 4TB의 물리적 저장소 용량이 필요합니다.

![이중 패리티](media/Storage-Spaces-Fault-Tolerance/dual-parity-180px.png)

이중 패리티의 저장소 효율성은 하드웨어 오류 도메인이 많을수록 높아집니다(50%에서 최대 80%까지). 예를 들어 하드웨어 오류 도메인이 일곱 개인 경우(저장소 공간 다이렉트 사용 시 일곱 개의 서버를 의미) 효율성은 66.7%로 높아집니다. 즉, 4TB의 데이터를 저장하려면 6TB의 물리적 저장소 용량만 있으면 됩니다.

![dual-parity-wide](media/Storage-Spaces-Fault-Tolerance/dual-parity-wide-180px.png)

모든 규모에서 이중 패리티 및 로컬 재구성 코드의 효율에 대해서는 [요약](#summary) 섹션을 참조하세요.

### <a name="local-reconstruction-codes"></a>로컬 재구성 코드

Windows Server 2016의 저장소 공간 기능에는 '로컬 재구성 코드' 또는 LRC라고 하는 Microsoft Research에서 개발한 고급 기술이 도입되었습니다. 대규모 환경에서 이중 패리티는 LRC를 사용하여 인코딩/디코딩을 몇 개의 더 작은 그룹으로 분할함으로써 기록 또는 오류 복구에 필요한 오버헤드를 줄입니다.

하드 디스크 드라이브(HDD) 사용 시 그룹 크기는 네 개의 기호이고 반도체 드라이브(SSD) 사용 시 그룹 크기는 여섯 개의 기호입니다. 예를 들어 다음은 하드 디스크 드라이브와 12개의 하드웨어 오류 도메인(12개의 서버를 의미)이 있을 때의 레이아웃 모습으로, 데이터 기호가 네 개인 그룹이 두 개 있습니다. 여기서 저장소 효율성은 72.7%입니다.

![local-reconstruction-codes](media/Storage-Spaces-Fault-Tolerance/local-reconstruction-codes-180px.png)

깊이 있지만 읽기 쉬운 것으로 유명한 [Claus Joergensen](https://twitter.com/clausjor)의 [로컬 재구성 코드가 여러 오류 시나리오를 처리하는 방식과 그 장점에 관한 글](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)을 참조하는 것이 좋습니다.

## <a name="mirror-accelerated-parity"></a>미러 가속 패리티

Windows Server 2016부터는 저장소 공간 다이렉트 볼륨이 일부는 미러이고 일부는 패리티일 수 있습니다. 미러링된 부분에 먼저 쓰기가 표시된 다음 패리티 부분으로 점차 이동합니다. 실제로 이 방식은 [미러링을 사용하여 이레이저 코딩을 가속화](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)합니다.

3방향 미러와 이중 패리티를 조합하려면 최소 네 개의 오류 도메인, 즉 네 개의 서버가 필요합니다.

미러-가속 패리티의 저장소 효율성은 미러만 사용할 때의 효율과 패리티만 사용할 때의 효율의 중간이며 선택하는 비율에 따라 달라집니다. 예를 들어 이 프레젠테이션의 37분 위치에 나오는 데모에서는 12대의 서버를 사용할 때 [46%, 54% 및 65%의 효율을 보이는 다양한 조합](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s)을 보여 줍니다.

> [!IMPORTANT]
> 성능이 가장 중요한 워크로드에 대한 미러링을 사용하는 것이 좋습니다. 워크로드에 따라 성능과 용량의 균형을 맞추는 방법에 관한 자세한 내용은 [볼륨 계획](plan-volumes.md#choosing-the-resiliency-type)을 참조하세요.

## <a name="summary"></a>요약

이 섹션에서는 저장소 공간 다이렉트에서 사용 가능한 복원력 유형, 각 유형을 사용하기 위한 최소 크기 요구 사항, 각 유형에서 내결함성을 가지는 오류 횟수 및 해당 저장소 효율성을 요약했습니다.

### <a name="resiliency-types"></a>복원력 유형

|    복원력          |    내결함성       |    저장소 효율성      |
|------------------------|----------------------------|----------------------------|
|    양방향 미러      |    1                       |    50.0%                   |
|    3방향 미러    |    2                       |    33.3%                   |
|    이중 패리티         |    2                       |    50.0% - 80.0%           |
|    혼합               |    2                       |    33.3% - 80.0%           |

### <a name="minimum-scale-requirements"></a>최소 규모 요구 사항

|    복원력          |    필요한 최소 장애 도메인   |
|------------------------|-------------------------------------|
|    양방향 미러      |    2                                |
|    3방향 미러    |    3                                |
|    이중 패리티         |    4                                |
|    혼합               |    4                                |

   >[!TIP]
   > [섀시 또는 랙 내결함성](../../failover-clustering/fault-domains.md)을 사용 중인 경우 이외에는 오류 도메인 수는 서버 수를 가리킵니다. 저장소 공간 다이렉트의 최소 요구 사항이 충족되는 경우에는 각 서버의 드라이브 수가 사용 가능한 복원력 유형에 영향을 미치지 않습니다. 

### <a name="dual-parity-efficiency-for-hybrid-deployments"></a>하이브리드 배포의 이중 패리티 효율

이 표에서는 하드 디스크 드라이브(HDD)와 반도체 드라이브(SSD)가 모두 포함된 하이브리드 배포에서 각 규모별 이중 패리티 및 로컬 재구성 코드의 저장소 효율성을 보여 줍니다.

|    오류 도메인      |    레이아웃           |    효율성   |
|-----------------------|---------------------|-----------------|
|    2                  |    –                |    –            |
|    3                  |    –                |    –            |
|    4                  |    RS 2+2           |    50.0%        |
|    5                  |    RS 2+2           |    50.0%        |
|    6                  |    RS 2+2           |    50.0%        |
|    7                  |    RS 4+2           |    66.7%        |
|    8                  |    RS 4+2           |    66.7%        |
|    9                  |    RS 4+2           |    66.7%        |
|    10                 |    RS 4+2           |    66.7%        |
|    11                 |    RS 4+2           |    66.7%        |
|    12                 |    LRC(8, 2, 1)    |    72.7%        |
|    13                 |    LRC(8, 2, 1)    |    72.7%        |
|    14                 |    LRC(8, 2, 1)    |    72.7%        |
|    15                 |    LRC(8, 2, 1)    |    72.7%        |
|    16                 |    LRC(8, 2, 1)    |    72.7%        |

### <a name="dual-parity-efficiency-for-all-flash-deployments"></a>플래시 전용 배포에서 이중 패리티 효율

이 표에서는 반도체 드라이브(SSD)만 포함된 플래시 전용 배포에서 각 규모별 이중 패리티 및 로컬 재구성 코드의 저장소 효율성을 보여 줍니다. 패리티 레이아웃은 플래시 전용 구성에서 더 큰 그룹 크기를 사용하고 더 높은 저장소 효율성을 달성할 수 있습니다.

|    오류 도메인      |    레이아웃           |    효율성   |
|-----------------------|---------------------|-----------------|
|    2                  |    –                |    –            |
|    3                  |    –                |    –            |
|    4                  |    RS 2+2           |    50.0%        |
|    5                  |    RS 2+2           |    50.0%        |
|    6                  |    RS 2+2           |    50.0%        |
|    7                  |    RS 4+2           |    66.7%        |
|    8                  |    RS 4+2           |    66.7%        |
|    9                  |    RS 6+2           |    75.0%        |
|    10                 |    RS 6+2           |    75.0%        |
|    11                 |    RS 6+2           |    75.0%        |
|    12                 |    RS 6+2           |    75.0%        |
|    13                 |    RS 6+2           |    75.0%        |
|    14                 |    RS 6+2           |    75.0%        |
|    15                 |    RS 6+2           |    75.0%        |
|    16                 |    LRC(12, 2, 1)   |    80.0%        |

## <a name="examples"></a>예제

서버가 두 대만 있는 경우 이외에는 더 높은 내결함성을 제공하므로 3방향 미러링 및/또는 이중 패리티를 사용하는 것이 좋습니다. 특히 두 개의 오류 도메인(저장소 공간 다이렉트 사용 시 두 개의 서버를 의미)이 동시 오류의 영향을 받더라도 모든 데이터가 안전하고 액세스 가능한 상태를 유지합니다.

### <a name="examples-where-everything-stays-online"></a>모두 온라인 상태일 때의 예제

이러한 여섯 개의 예제는 3방향 미러링 및/또는 이중 패리티로 허용 **가능한** 항목을 보여 줍니다.

- **1.**    분실 한 드라이브 (캐시 드라이브 포함)
- **2.**    하나의 서버 손실

![fault-tolerance-examples-1-and-2](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-12.png)

- **3.**    한 서버 및 단일 드라이브 손실
- **4.**    서로 다른 서버에서 두 개의 드라이브 손실

![fault-tolerance-examples-3-and-4](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-34.png)

- **5.**    두 서버에 가장 영향을 받는 한다면 두 개 이상의 드라이브 손실
- **6.**    두 서버 손실

![fault-tolerance-examples-5-and-6](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-56.png)

...모든 경우 모든 볼륨이 온라인 상태를 유지합니다. (클러스터에서 쿼럼이 유지되는지 확인)

### <a name="examples-where-everything-goes-offline"></a>모든 항목이 오프라인 상태가 되는 예제

저장소 공간은 시간이 충분하다면 오류가 각각의 오류 발생 후 완전한 복원력으로 복원되므로 제한 없는 수의 오류를 허용할 수 있습니다. 하지만 특정 시점에 최대 두 개의 오류 도메인이 영향을 받는 경우에만 안전합니다. 따라서 다음은 3방향 미러링 및/또는 이중 패리티에서 허용 **불가능한** 항목의 예제입니다.

- **7.** 한 번에 세 개 이상의 서버에서 드라이브 손실
- **8.** 3 개 이상의 서버를 한 번에 손실

![fault-tolerance-examples-7-and-8](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-78.png)

## <a name="usage"></a>사용법

[저장소 공간 다이렉트에서 볼륨 만들기](create-volumes.md)를 참조하세요.

## <a name="see-also"></a>참조

아래의 모든 링크는 이 항목의 본문에 포함되어 있습니다.

- [Windows Server 2016의에서 저장소 공간 다이렉트](storage-spaces-direct-overview.md)
- [Windows Server 2016의에서 장애 도메인 인식](../../failover-clustering/fault-domains.md)
- [Azure Microsoft Research에서 코딩 지우기](https://www.microsoft.com/en-us/research/publication/erasure-coding-in-windows-azure-storage/)
- [로컬 재구성 코드 및 가속화 패리티 볼륨](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)
- [저장소 관리 API의 볼륨](https://blogs.technet.microsoft.com/filecab/2016/08/29/deep-dive-volumes-in-spaces-direct/)
- [저장소 효율성 데모 microsoft Ignite 2016](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s)
- [용량 계산기 PREVIEW 저장소 공간 다이렉트](http://aka.ms/s2dcalc)
