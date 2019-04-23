---
title: 저장소 공간 다이렉트에 대 한 드라이브 대칭 고려 사항
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/08/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: 629e49a0c1919286d8e4f418b3e99d69e720f4fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866884"
---
# <a name="drive-symmetry-considerations-for-storage-spaces-direct"></a>저장소 공간 다이렉트에 대 한 드라이브 대칭 고려 사항 

> 적용 대상: Windows Server 2019, Windows Server 2016

[저장소 공간 다이렉트](storage-spaces-direct-overview.md) 모든 서버에 동일한 드라이브를 정확 하 게 하는 경우 가장 잘 작동 합니다.

실제로이 불가능 한 항상 인식 합니다. 저장소 공간 다이렉트는 조직의 요구 사항 증가 함에 따라 규모를 오랫동안 실행 하도록 설계 되었습니다. 현재 있습니다 구입한 spacious 3TB 하드 드라이브 내년 경우가 항목을 찾을 작은 불가능 합니다. 따라서 어느 정도의 혼합 및 일치가 지원 됩니다.

이 항목에서는 제약 조건에 설명 하 고 지원 및 미지원 구성의 예를 제공 합니다.

## <a name="constraints"></a>제약 조건

### <a name="type"></a>형식

모든 서버가 동일한 있어야 [종류의 드라이브](choosing-drives.md#drive-types)합니다.

예를 들어, NVMe 서버만 있으면 말아야 *모든* NVMe 있어야 합니다.

### <a name="number"></a>Number

모든 서버에는 각 유형의 드라이브 수가 있어야 합니다.

예를 들어, 서버 하나에 6 개 SSD 있으면 말아야 *모든* 6 SSD가 있습니다.

   > [!NOTE]
   > 실패 하는 중에 일시적으로 또는 추가 하거나 드라이브를 제거 하는 동안 다른 드라이브의 수에 대 한 괜찮습니다.

### <a name="model"></a>Model

동일한 모델 및 펌웨어 버전을 가능한 경우 드라이브를 사용 하는 것이 좋습니다. 그렇게 할 수 없으면 최대한 비슷하게 드라이브를 신중 하 게 선택 합니다. 것이 좋습니다 급격 하 게 다른 성능 또는 지속 시간과 특성을 사용 하 여 동일한 유형의 혼합 및 일치가 드라이브를 (하지 않는 한 캐시 하나 이며 다른 하나는 용량) 저장소 공간 다이렉트 IO를 균등 하 게 배포 하 고 모델에 따라 구별 하지 때문에 .

   > [!NOTE]
   > 혼합 및 일치 유사한 SATA 및 SAS 드라이브를 괜찮습니다.

### <a name="size"></a>크기

가능 하면 동일한 크기의 드라이브를 사용 하는 것이 좋습니다. 다양 한 크기의 용량 드라이브를 사용 하 여 사용할 수 없는 일부 용량에 있으며 다양 한 크기의 캐시 드라이브를 사용 하 여 캐시 성능이 향상 되지 않을 수 있습니다. 자세한 내용은 다음 섹션을 참조 하세요.

   > [!WARNING]
   > 서버에 걸쳐 서로 다른 용량 드라이브 크기 용량 방치 될 수 있습니다.

## <a name="understand-capacity-imbalance"></a>용량 불균형 이해:

저장소 공간 다이렉트는 용량 불균형을 강력한 드라이브 및 서버 에서입니다. 않으므로 이러한 불균형은 심각한 인 경우에 모두 계속 작동 합니다. 그러나 여러 가지 요인에 따라 모든 서버에서 사용할 수 없는 용량 하지 사용할 수 있습니다.

이 문제가 발생 하는 이유를 확인 하려면 아래 간소화 된 그림을 고려 합니다. 각 색이 지정 된 상자 미러된 데이터의 복사본을 하나를 나타냅니다. 상자에 표시 하는 예를 들어,', 및 '은 동일한 데이터의 세 가지 복사본입니다. 서버 내결함성, 이러한 복사본을 적용할 *해야* 서로 다른 서버에 저장 합니다.

### <a name="stranded-capacity"></a>방치 용량

를 그릴 때 Server 1 (10TB) 및 서버 2 (10TB)는 전체입니다. 서버 3에 더 큰 드라이브가 해당 총 용량 보다 큰 (15 TB). 그러나 서버 3에 자세한 3 방향 미러 데이터를 저장 해야 서버 1-2 서버에서 복사본도 전체 이미는 합니다. 서버 3에서 남은 5TB 용량을 사용할 수 없습니다 – 것 *"남겨진"* 용량입니다.

![3 방향 미러, 3 명의 서버를 남겨진 용량](media/drive-symmetry-considerations/Size-Asymmetry-3N-Stranded.png)

### <a name="optimal-placement"></a>최적의 배치

10TB, 10TB, 10TB 15의 용량 및 3 방향 미러 복원 력의 경우 4 명의 서버와 반대로, 것 *는* 그려지는으로 모든 사용 가능한 용량을 사용 하는 방식으로 복사본을 유효 하 게 배치할 수 있습니다. 이것이 가능 때마다 저장소 공간 다이렉트 할당자를 찾을 최적의 배치를 사용 하 여 없습니다 방치 용량을 유지 합니다.

![3 방향 미러, 4 대의 서버 없는 방치 용량](media/drive-symmetry-considerations/Size-Asymmetry-4N-No-Stranded.png)

서버 수, 복원 력을 용량 불균형 및 기타 요인의 심각도 방치 용량 인지 영향을 줍니다. **이 가장 좋습니다 일반 규칙은 모든 서버에서 사용할 수 있는 유일한 용량 사용 가능 하도록 보장 되는 것으로 가정 합니다.**

## <a name="understand-cache-imbalance"></a>캐시 불균형 이해:

저장소 공간 다이렉트는 캐시 불균형을 강력한 드라이브 및 서버 에서입니다. 않으므로 이러한 불균형은 심각한 인 경우에 모두 계속 작동 합니다. 또한 저장소 공간 다이렉트 항상 사용를 최대한 사용 가능한 모든 캐시 합니다.

그러나 다양 한 크기의 캐시 드라이브를 사용 하 여 향상 되지는 캐시 성능 예측 가능 하 게 또는 균일 하 게: IO를 [바인딩 드라이브](understand-the-cache.md#server-side-architecture) 드라이브 더 큰 캐시를 사용 하 여 성능이 향상된 될 수 있습니다. 저장소 공간 다이렉트 바인딩 간에 IO를 균등 하 게 배포 하 고 캐시-용량 비율에 따라 구별 하지 않습니다.

![캐시 불균형](media/drive-symmetry-considerations/Cache-Asymmetry.png)

   > [!TIP]
   > 참조 [캐시 이해](understand-the-cache.md) 캐시 바인딩에 대 한 자세한 내용을 보려면.

## <a name="example-configurations"></a>예제 구성

일부 지원 되거나 지원 되지 않는 구성은 다음과 같습니다.

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-models-between-servers"></a>![지원됨](media/drive-symmetry-considerations/supported.png) 서버 간에 서로 다른 모델 지원:

처음 두 서버 NVMe 모델 "X"를 사용 하지만 세 번째 서버는 매우 비슷하지만 NVMe 모델 "Z"를 사용 합니다.

| 서버 1                    | 서버 2                    | 서버 3                    |
|-----------------------------|-----------------------------|-----------------------------|
| 2x NVMe 모델 X (캐시)    | 2x NVMe 모델 X (캐시)    | 2x Z NVMe 모델 (캐시)    |
| SSD 모델 Y x 10 (용량) | SSD 모델 Y x 10 (용량) | SSD 모델 Y x 10 (용량) |

이 지원 됩니다.

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-models-within-server"></a>![지원됨](media/drive-symmetry-considerations/supported.png) 서버 내에서 서로 다른 모델 지원:

모든 서버는 몇 가지 다양 한 HDD 모델은 매우 유사 "Y"와 "Z"를 사용 합니다. 모든 서버에는 총 10 개의 HDD에 있습니다.

| 서버 1                   | 서버 2                   | 서버 3                   |
|----------------------------|----------------------------|----------------------------|
| 2x SSD 모델 X (캐시)    | 2x SSD 모델 X (캐시)    | 2x SSD 모델 X (캐시)    |
| HDD 모델 Y x 7 (용량) | HDD 모델 Y x 5 (용량) | HDD 모델 Y x는 1 (용량) |
| HDD 모델 Z x 3 (용량) | HDD 모델 Z x 5 (용량) | HDD 모델 Z x는 9 (용량) |

이 지원 됩니다.

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-sizes-across-servers"></a>![지원됨](media/drive-symmetry-considerations/supported.png) 서버에 걸쳐 다양 한 크기 지원.

처음 두 서버는 4TB HDD를 사용 하지만 세 번째 서버에서 매우 유사한 6TB HDD를 사용 합니다.

| 서버 1                | 서버 2                | 서버 3                |
|-------------------------|-------------------------|-------------------------|
| 2 x 800 GB NVMe (캐시) | 2 x 800 GB NVMe (캐시) | 2 x 800 GB NVMe (캐시) |
| 4 x 4TB HDD (용량) | 4 x 4TB HDD (용량) | 4 x 6 TB HDD (용량) |

이 지원 되지만 방치 용량에 발생 합니다.

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-sizes-within-server"></a>![지원됨](media/drive-symmetry-considerations/supported.png) 서버 내에서 다양 한 크기 지원.

모든 서버는 몇 가지 다양 한 1.2TB와 매우 비슷한 1.6TB SSD 사용합니다. 모든 서버에는 총 4 개 SSD에 있습니다.

| 서버 1                 | 서버 2                 | 서버 3                 |
|--------------------------|--------------------------|--------------------------|
| 3 x 1.2 TB SSD (캐시)   | 2 x 1.2 TB SSD (캐시)   | 4 x 1.2 TB SSD (캐시)   |
| 1 x 1.6 TB SSD (캐시)   | 2 x 1.6 TB SSD (캐시)   | -                        |
| 20 x 4TB HDD (용량) | 20 x 4TB HDD (용량) | 20 x 4TB HDD (용량) |

이 지원 됩니다.

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-different-types-of-drives-across-servers"></a>![지원되지 않음](media/drive-symmetry-considerations/unsupported.png) 지원 되지 않습니다: 다른 유형의 서버에 걸쳐 드라이브

서버 1 NVMe 갖지만 다른 하지 않습니다.

| 서버 1            | 서버 2            | 서버 3            |
|---------------------|---------------------|---------------------|
| 6 x NVMe (캐시)    | -                   | -                   |
| -                   | 6 x SSD (캐시)     | 6 x SSD (캐시)     |
| 18 x HDD (용량) | 18 x HDD (용량) | 18 x HDD (용량) |

이 지원 되지 않습니다. 두 가지 유형의 드라이브를 모든 서버에서 동일 해야 합니다.

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-different-number-of-each-type-across-servers"></a>![지원되지 않음](media/drive-symmetry-considerations/unsupported.png) 지원 되지 않습니다: 서버에서 각 유형의 여러

서버 3에는 파티션보다 더 많은 드라이브에 있습니다.

| 서버 1            | 서버 2            | 서버 3            |
|---------------------|---------------------|---------------------|
| 2 x NVMe (캐시)    | 2 x NVMe (캐시)    | 4 x NVMe (캐시)    |
| 10 x HDD (용량) | 10 x HDD (용량) | 20 x HDD (용량) |

이 지원 되지 않습니다. 각 유형의 드라이브 수가 모든 서버에서 동일 해야 합니다.

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-only-hdd-drives"></a>![지원되지 않음](media/drive-symmetry-considerations/unsupported.png) 지원 되지 않습니다:만 HDD 드라이브

모든 서버에만 HDD 드라이브가 연결 되어 있습니다.

|서버 1|서버 2|서버 3|
|-|-|-| 
|18 x HDD (용량) |18 x HDD (용량)|18 x HDD (용량)|

이 지원 되지 않습니다. 추가 최소 두 개의 캐시 드라이브가 (NvME 또는 SSD) 각 서버에 연결 해야 합니다.

## <a name="summary"></a>요약

정리 하자면, 클러스터의 모든 서버에 동일한 종류의 드라이브 및 각 유형의 동일한 수 있어야 합니다. 혼합 및 일치 드라이브 모델 및 위의 고려 하 여 필요에 따라 드라이브 크기가 지원 됩니다.

| 제약 조건                               |               |
|------------------------------------------|---------------|
| 동일한 종류의 모든 서버에서 드라이브     | **필수**  |
| 모든 서버에서 각 유형의 만큼 | **필수**  |
| 모든 서버에서 동일한 드라이브 모델        | 권장   |
| 모든 서버에 동일한 드라이브 크기         | 권장   |

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 하드웨어 요구 사항](storage-spaces-direct-hardware-requirements.md)
- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
