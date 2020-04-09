---
title: 스토리지 공간 다이렉트에 대 한 드라이브 대칭 고려 사항
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: b06d69c020ea38a2fb9f23df2cfd9cd4191ae315
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857556"
---
# <a name="drive-symmetry-considerations-for-storage-spaces-direct"></a>스토리지 공간 다이렉트에 대 한 드라이브 대칭 고려 사항 

> 적용 대상: Windows Server 2019, Windows Server 2016

[스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 는 모든 서버에 정확히 동일한 드라이브가 있는 경우에 가장 잘 작동 합니다.

실제로이는 실용적이 지 않습니다. 스토리지 공간 다이렉트은 몇 년 동안 실행 되도록 설계 되었으며 조직의 요구가 증가 함에 따라 규모를 확장 하는 것을 인식 합니다. 현재 spacious 3TB 하드 드라이브를 구입할 수 있습니다. 내년에는 작은 것을 찾을 수 없게 될 수 있습니다. 따라서 일부 혼합 및 일치는 지원 됩니다.

이 항목에서는 제약 조건에 대해 설명 하 고 지원 되거나 지원 되지 않는 구성의 예를 제공 합니다.

## <a name="constraints"></a>제약 조건

### <a name="type"></a>형식

모든 서버의 [드라이브 유형은](choosing-drives.md#drive-types)동일 해야 합니다.

예를 들어 한 서버에 NVMe가 있으면 *모두* nvme가 있어야 합니다.

### <a name="number"></a>번호

모든 서버의 드라이브 수는 각 유형과 동일 해야 합니다.

예를 들어 한 서버에 6 개의 SSD가 있는 경우 *모두* 6 개의 ssd를 포함 해야 합니다.

   > [!NOTE]
   > 오류가 발생 하거나 드라이브를 추가 또는 제거 하는 동안 드라이브 수가 일시적으로 달라질 수 있습니다.

### <a name="model"></a>모델

가능 하면 항상 동일한 모델 및 펌웨어 버전의 드라이브를 사용 하는 것이 좋습니다. 가능 하지 않은 경우 가능한 한 유사 하 게 드라이브를 선택 합니다. 스토리지 공간 다이렉트는 IO를 균등 하 게 분산 하 고 모델을 기반으로 판별 하지 않기 때문에 동일한 유형의 드라이브를 혼합 하 여 사용 하는 것은 서로 다른 성능 또는 endurance 특성을 사용 하지 않습니다 (하나는 캐시 및 기타 용량).

   > [!NOTE]
   > 유사한 SATA 및 SAS 드라이브를 혼합 하 고 일치 시킬 수 있습니다.

### <a name="size"></a>크기

가능 하면 항상 동일한 크기의 드라이브를 사용 하는 것이 좋습니다. 다른 크기의 용량 드라이브를 사용 하면 일부 사용 불가능 용량이 발생할 수 있으며, 크기가 다른 캐시 드라이브를 사용 하면 캐시 성능이 향상 되지 않을 수 있습니다. 자세한 내용은 다음 섹션을 참조하십시오.

   > [!WARNING]
   > 서버 전체에서 크기가 서로 다른 용량이 있으면 용량이 방치 될 수 있습니다.

## <a name="understand-capacity-imbalance"></a>이해: 용량 불균형

스토리지 공간 다이렉트는 드라이브와 서버 간에 용량이 불균형 하기에 매우 강력 합니다. 불균형이 심각 하더라도 모든 것이 계속 작동 합니다. 그러나 여러 가지 요인에 따라 모든 서버에서 사용할 수 없는 용량은 사용할 수 없습니다.

이 문제가 발생 하는 이유를 확인 하려면 아래 단순화 된 그림을 참조 하십시오. 색이 지정 된 각 상자는 미러된 데이터의 복사본 하나를 나타냅니다. 예를 들어, ' ' 및 ' '로 표시 된 상자는 동일한 데이터의 복사본 3 개입니다. 서버 내결함성을 인식 하려면 이러한 복사본을 다른 서버에 저장 *해야* 합니다.

### <a name="stranded-capacity"></a>남겨진 용량

그리고 서버 1 (10TB) 및 서버 2 (10TB)가 꽉 찬 경우 서버 3에는 더 큰 드라이브가 있으므로 총 용량이 더 큽니다 (15tb). 그러나 3 방향 미러 데이터를 서버 3에 저장 하려면 서버 1과 서버 2에 모두 복사 해야 합니다 .이는 이미 꽉 찬 것입니다. 서버 3에서 남아 있는 5gb의 용량을 사용할 수 없습니다. 즉, *"방치"* 된 용량입니다.

![3 방향 미러, 3 개의 서버, 남겨진 용량](media/drive-symmetry-considerations/Size-Asymmetry-3N-Stranded.png)

### <a name="optimal-placement"></a>최적 배치

반대로, 10tb, 10tb, 10TB, 1tb 용량과 1TB 용량과 3 방향 미러 복원 력으로 4 대의 서버를 사용 하 여 모든 사용 가능한 용량을 사용 하는 방식으로 복사본을 올바르게 *저장할 수 있습니다* . 가능 하면 스토리지 공간 다이렉트 할당자는 최적의 배치를 찾아 사용 하며,이는 남아 있는 용량을 유지 하지 않습니다.

![3 방향 미러, 4 대의 서버, 남겨진 용량 없음](media/drive-symmetry-considerations/Size-Asymmetry-4N-No-Stranded.png)

서버 수, 복원 력, 용량 불균형의 심각도 및 기타 요소는 용량이 부족 한지에 영향을 줍니다. **가장 신중 하 게 사용할 수 있는 것은 모든 서버에서 사용할 수 있는 용량을 항상 사용할 수 있다고 가정 하는 것입니다.**

## <a name="understand-cache-imbalance"></a>이해: 캐시 불균형

스토리지 공간 다이렉트는 드라이브와 서버 간에 캐시 불균형을 위한 강력한 방법입니다. 불균형이 심각 하더라도 모든 것이 계속 작동 합니다. 또한 스토리지 공간 다이렉트 항상 사용 가능한 모든 캐시를 최대한 사용 합니다.

그러나 크기가 다른 캐시 드라이브를 사용 하는 경우 캐시 성능이 균일 하지 않거나 예측 가능 하지 않을 수 있습니다. 더 큰 캐시 드라이브로 [바인딩을 구동](understand-the-cache.md#server-side-architecture) 하는 IO만 향상 된 성능을 볼 수 있습니다. 스토리지 공간 다이렉트 바인딩에서 IO를 균등 하 게 분산 하 고, 캐시-용량 비율에 따라 판별 되지 않습니다.

![캐시 불균형](media/drive-symmetry-considerations/Cache-Asymmetry.png)

   > [!TIP]
   > 캐시 바인딩에 대해 자세히 알아보려면 [캐시 이해](understand-the-cache.md) 를 참조 하세요.

## <a name="example-configurations"></a>구성 예

다음은 지원 되는 구성 및 지원 되지 않는 구성입니다.

### <a name="supported-supported-different-models-between-servers"></a>![지원](media/drive-symmetry-considerations/supported.png) 지원 됨: 서버 간 다른 모델

처음 두 서버는 NVMe 모델 "X"를 사용 하지만 세 번째 서버는 NVMe 모델 "Z"를 사용 합니다 .이는 매우 유사 합니다.

| 서버 1                    | 서버 2                    | 서버 3                    |
|-----------------------------|-----------------------------|-----------------------------|
| 2 x NVMe 모델 X (캐시)    | 2 x NVMe 모델 X (캐시)    | 2 x NVMe 모델 Z (캐시)    |
| 10 x SSD 모델 Y (용량) | 10 x SSD 모델 Y (용량) | 10 x SSD 모델 Y (용량) |

지원됩니다.

### <a name="supported-supported-different-models-within-server"></a>![지원](media/drive-symmetry-considerations/supported.png) 지원 됨: 서버 내의 다른 모델

모든 서버는 매우 유사한 HDD 모델 "Y"와 "Z"의 여러 조합을 사용 합니다. 모든 서버에는 총 10 개의 HDD가 있습니다.

| 서버 1                   | 서버 2                   | 서버 3                   |
|----------------------------|----------------------------|----------------------------|
| 2 x SSD 모델 X (캐시)    | 2 x SSD 모델 X (캐시)    | 2 x SSD 모델 X (캐시)    |
| 7 x HDD 모델 Y (용량) | 5 x HDD 모델 Y (용량) | 1 x HDD 모델 Y (용량) |
| 3 x HDD 모델 Z (용량) | 5 x HDD 모델 Z (용량) | 9 x HDD 모델 Z (용량) |

지원됩니다.

### <a name="supported-supported-different-sizes-across-servers"></a>![지원](media/drive-symmetry-considerations/supported.png) 지원 됨: 서버 간 다양 한 크기

처음 두 서버는 4 TB HDD를 사용 하지만 세 번째 서버는 매우 유사한 6tb HDD를 사용 합니다.

| 서버 1                | 서버 2                | 서버 3                |
|-------------------------|-------------------------|-------------------------|
| 2 x 800 NVMe (캐시) | 2 x 800 NVMe (캐시) | 2 x 800 NVMe (캐시) |
| 4 x 4TB HDD (용량) | 4 x 4TB HDD (용량) | 4 x 6TB HDD (용량) |

이는 지원 되지만 용량이 더 이상 발생 하지 않습니다.

### <a name="supported-supported-different-sizes-within-server"></a>![지원](media/drive-symmetry-considerations/supported.png) 지원 됨: 서버 내의 다른 크기

모든 서버는 1.2 TB와 매우 유사한 1.6 TB SSD 조합을 사용 합니다. 모든 서버에는 총 4 개의 SSD가 있습니다.

| 서버 1                 | 서버 2                 | 서버 3                 |
|--------------------------|--------------------------|--------------------------|
| 3 x 1.2 TB SSD (캐시)   | 2 x 1.2 TB SSD (캐시)   | 4 x 1.2 TB SSD (캐시)   |
| 1 x 1.6 TB SSD (캐시)   | 2 x 1.6 TB SSD (캐시)   | -                        |
| 20 x 4tb HDD (용량) | 20 x 4tb HDD (용량) | 20 x 4tb HDD (용량) |

지원됩니다.

### <a name="unsupported-not-supported-different-types-of-drives-across-servers"></a>![지원되지 않는](media/drive-symmetry-considerations/unsupported.png) 지원 되지 않음: 서버 간 여러 유형의 드라이브

서버 1에는 NVMe가 있지만 나머지는 그렇지 않습니다.

| 서버 1            | 서버 2            | 서버 3            |
|---------------------|---------------------|---------------------|
| 6 x NVMe (캐시)    | -                   | -                   |
| -                   | 6 x SSD (캐시)     | 6 x SSD (캐시)     |
| 18 x HDD (용량) | 18 x HDD (용량) | 18 x HDD (용량) |

이는 지원 되지 않습니다. 드라이브의 유형은 모든 서버에서 동일 해야 합니다.

### <a name="unsupported-not-supported-different-number-of-each-type-across-servers"></a>![지원되지 않는](media/drive-symmetry-considerations/unsupported.png) 지원 되지 않음: 서버 간 각 유형의 수가 다릅니다.

서버 3에 다른 드라이브 보다 더 많은 드라이브가 있습니다.

| 서버 1            | 서버 2            | 서버 3            |
|---------------------|---------------------|---------------------|
| 2 x NVMe (캐시)    | 2 x NVMe (캐시)    | 4 x NVMe (캐시)    |
| 10 x HDD (용량) | 10 x HDD (용량) | 20 x HDD (용량) |

이는 지원 되지 않습니다. 각 유형의 드라이브 수는 모든 서버에서 동일 해야 합니다.

### <a name="unsupported-not-supported-only-hdd-drives"></a>![지원되지 않는](media/drive-symmetry-considerations/unsupported.png) 지원 되지 않음: HDD 드라이브만

모든 서버에는 연결 된 HDD 드라이브만 있습니다.

|서버 1|서버 2|서버 3|
|-|-|-| 
|18 x HDD (용량) |18 x HDD (용량)|18 x HDD (용량)|

이는 지원 되지 않습니다. 각 서버에 연결 된 최소 두 개의 캐시 드라이브 (NvME 또는 SSD)를 추가 해야 합니다.

## <a name="summary"></a>요약

요약 하자면, 클러스터의 모든 서버는 동일한 유형의 드라이브와 각 유형의 동일한 수를 가져야 합니다. 위의 고려 사항에 따라 필요에 따라 드라이브 모델과 드라이브 크기를 혼합 하 고 일치 시킬 수 있습니다.

| 제약 조건                               |               |
|------------------------------------------|---------------|
| 모든 서버에서 동일한 유형의 드라이브     | **필수**  |
| 모든 서버에서 동일한 수의 각 형식 | **필수**  |
| 모든 서버에서 동일한 드라이브 모델        | 권장   |
| 모든 서버에서 동일한 드라이브 크기         | 권장   |

## <a name="see-also"></a>참고 항목

- [하드웨어 요구 사항 스토리지 공간 다이렉트](storage-spaces-direct-hardware-requirements.md)
- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
