---
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
title: 저장소 공간 다이렉트용 드라이브 선택
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 227906685d77c31587c66d1c292f20ca94775058
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881054"
---
# <a name="choosing-drives-for-storage-spaces-direct"></a>저장소 공간 다이렉트용 드라이브 선택

>적용 대상: Windows Server 2016

이 항목에서는 성능 및 용량 요구 사항을 충족하는 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)용 드라이브를 선택하는 방법에 대한 지침을 제공합니다.

## <a name="drive-types"></a>드라이브 종류

저장소 공간 다이렉트는 현재 세 가지 유형의 드라이브에서 작동합니다.

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>NVMe</b>(비휘발성 메모리 Express)는 PCIe 버스에 직접 장착된 반도체 드라이브를 의미합니다. 일반적인 폼 팩터는 2.5인치 U.2, PCIe 추가 기능 카드(AIC) 및 M.2입니다. NVMe는 현재 지원되는 드라이브 유형 중 가장 높은 IOPS 및 IO 처리량을 제공하고 대기 시간은 가장 짧습니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px" >
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>SSD</b>는 기존 SATA 또는 SAS를 통해 연결되는 반도체 드라이브를 의미합니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>HDD</b>는 대규모의 저장 용량을 제공하는 회전식 자기 하드 디스크 드라이브를 의미합니다.
        </td>
    </tr>
</table>

## <a name="built-in-cache"></a>기본 제공 캐시

저장소 공간 다이렉트에는 서버 쪽 캐시가 기본 제공됩니다. 대용량 실시간 영구 읽기 및 쓰기 캐시입니다. 여러 유형의 드라이브를 통한 배포에서 자동적으로 "가장 빠른" 유형의 모든 드라이브를 사용합니다. 나머지 드라이브는 용량에 사용됩니다.

자세한 내용은 [저장소 공간 다이렉트에서 캐시 이해](understand-the-cache.md)를 확인하세요.

## <a name="option-1--maximizing-performance"></a>옵션 1 – 성능 극대화

모든 데이터에 대한 임의의 읽기 쓰기 작업에서 예측 가능하고 일정한 밀리초 미만의 대기 시간을 원하거나, 최고의 IOPS([600만](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m) 이상) 또는 최고의 IO 처리량([1Tb/s](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s) 이상)을 원한다면 "플래시 전용"을 선택해야 합니다.

현재 이 작업을 수행할 수 있는 방법은 세 가지가 있습니다.

![플래시 전용 배포 시나리오](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **모든 NVMe 합니다.** NVMe 전용을 사용하는 옵션은 가장 예측 가능성이 높은 짧은 대기 시간을 비롯한 최고의 성능을 제공합니다. 드라이브가 모두 같은 모델일 경우 캐시가 없습니다. 내구성이 높은 NVMe 모델과 낮은 MVMe 모델을 혼용할 수도 있고, 내구성이 높은 모델이 낮은 모델에 대한 쓰기를 캐싱하도록 구성할 수도 있습니다([설정 필요](understand-the-cache.md#manual)).

2. **NVMe + SSD.** NVMe를 SSD와 함께 사용할 경우 NVMe는 SSD로의 쓰기를 자동 캐시합니다. 따라서 쓰기가 캐시에서 병합되고 필요한 경우에 한해 전환되어 SSD의 마모가 감소합니다. 이는 NVMe와 유사한 쓰기 특성을 제공하는 동시에, 마찬가지로 빠른 SSD로부터 읽기가 직접 실행됩니다.

3. **All SSD.** NVMe 전용과 마찬가지로 드라이브가 모두 같은 모델일 경우 캐시가 없습니다. 내구성이 높은 NVMe 모델과 낮은 MVMe 모델을 혼용할 경우, 내구성이 높은 모델이 낮은 모델에 대한 쓰기를 캐싱하도록 구성할 수도 있습니다([설정 필요](understand-the-cache.md#manual)).

   >[!NOTE]
   > 캐시 없이 NVMe 전용 또는 SSD 전용을 사용할 경우 모든 드라이브에서 사용 가능한 저장소 용량을 확보할 수 있다는 이점이 있습니다. 캐싱에 "소모"되는 용량이 없으므로 규모가 작은 경우에 적합합니다.

## <a name="option-2--balancing-performance-and-capacity"></a>옵션 2 – 성능과 용량의 균형

다양한 응용 프로그램과 워크로드가 실행되는 환경에서는 엄격한 성능 요구 사항을 요구하는 경우와 상당한 저장소 용량을 요구하는 경우가 있으므로 더 큰 HDD에 NVMe 또는 SSD 캐싱 "하이브리드"를 선택해야 합니다.

![하이브리드 배포 시나리오](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe + HDD**. NVMe 드라이브는 읽기와 쓰기를 모두 캐싱함으로써 읽기 쓰기 속도를 높입니다. 읽기를 캐싱하면 HDD가 쓰기에 집중할 수 있습니다. 쓰기를 캐싱하면 버스트를 흡수하고, HDD IOPS와 IO 처리량을 극대화할 수 있는 인공적으로 직렬화된 방식으로 쓰기가 병합되고 필요한 경우에 한해 전환될 수 있습니다. 이것은 NVMe와 유사한 쓰기 특성을 제공하며 자주 또는 최근에 읽혀진 데이터의 경우 NVMe와 유사한 읽기 특성도 제공합니다.

2. **SSD + HDD**. 위와 마찬가지로 SSD는 읽기와 쓰기를 모두 캐싱함으로써 읽기 쓰기 속도를 높입니다. 이것은 SSD와 유사한 쓰기 특성을 제공하며 자주 또는 최근에 읽혀진 데이터의 경우 SSD와 유사한 읽기 특성도 제공합니다.

    또 하나의 다소 특이한 옵션이 있습니다. *세 가지 유형의 드라이브를 모두* 사용하는 것입니다.

3. **NVMe + SSD + HDD.** 세 가지 유형의 드라이브를 모두 사용할 때 NVMe는 SSD 및 HDD에 대한 캐시를 수행합니다. 이 옵션의 장점은 SSD에서 볼륨을 만들 수 있고, HDD에서 볼륨을 만들 수 있으며, 같은 클러스터에 나란히 만들 수 있고, NVMe로 속도를 높일 수 있다는 점입니다. 전자는 "플래시 전용" 배포와 똑같고, 후자는 정확하게 위에서 설명된 "하이브리드" 배포와 똑같습니다. 이는 개념적으로 두 개의 풀을 갖는 것과 유사하며, 용량 관리, 장애 및 복구 주기 등이 거의 독립적입니다.

   >[!IMPORTANT]
   > 성능이 가장 중요한 작업을 SSD 계층을 사용하여 플래시 전용에 배치하는 것이 좋습니다.

## <a name="option-3--maximizing-capacity"></a>옵션 3 – 용량 극대화

보관, 백업 대상, 데이터 웨어하우스 또는 '콜드' 저장소와 같이 대규모 용량이 필요하고 자주 기록하지 않는 작업의 경우 캐싱을 위한 소수의 SSD와 용량을 위한 다수의 HDD를 결합해야 합니다.

![용량 극대화를 위한 배포 옵션](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSD + HDD**. SSD는 읽기와 쓰기를 캐싱하고, 버스트를 흡수하고 SSD와 같은 쓰기 성능을 제공하며, 나중에 HDD로의 최적화된 전환을 수행합니다.

>[!IMPORTANT]
>Hdd 사용 하 여 구성만 지원 되지 않습니다. 낮은 지속 시간과 Ssd 캐싱 높은 지속 시간과 Ssd은 권장 되지 않습니다.

## <a name="sizing-considerations"></a>크기 조정 고려 사항

### <a name="cache"></a>캐시

모든 서버는 최소 2개의 캐시 드라이브가 있어야 합니다(중복성에 필요한 최소 조건). 용량 드라이브의 수를 캐시 드라이브 수의 배수가 되도록 하는 것이 좋습니다. 예를 들어 캐시 드라이브가 4개인 경우 7개나 9개보다는 8개의 용량 드라이브(1:2 비율)를 사용하는 것이 더 일관적인 성능을 보일 것입니다.

캐시의 응용 프로그램 및 워크 로드, 즉, 모든 데이터 읽기 및 쓰기 언제 든 지 적극적으로 작업 집합에 맞게 조정 합니다. 캐시 크기가 이보다 더 클 필요는 없습니다. Hdd 사용 하 여 배포의 경우 상당한 시작 지점 경우 용량의 – 10% 예를 들어, 각 서버에는 4 x 4TB HDD 다음 2 800GB SSD 용량 16TB = = 1.6TB 서버당 캐시 합니다. 에 대 한 모든 플래시 배포의 경우 특히 매우 [높은 지속 시간과](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/) Ssd가는 것이 시작 용량 – 예를 들어, 5%에 가까운 양호 각 서버에 24 x 1.2 TB SSD 28.8 TB의 용량을 2 번 750 GB NVMe x = = 1.5TB 서버당 캐시 합니다. 캐시 드라이브는 추후 언제든지 추가하거나 제거해서 조정할 수 있습니다.

### <a name="general"></a>일반

서버당 전체 저장소 용량은 약 100TB로 제한하는 것이 좋습니다. 서버당 저장소 용량이 클수록 소프트웨어 업데이트를 적용하는 경우 등에 가동 중지 시간이나 다시 부팅 후 데이터를 다시 동기화하는 데 필요한 시간이 더 길어집니다.

저장소 풀당 현재 최대 크기는 1PB, 즉 1,000TB입니다.

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [저장소 공간 다이렉트 캐시 이해](understand-the-cache.md)
- [저장소 공간 다이렉트 하드웨어 요구 사항](storage-spaces-direct-hardware-requirements.md)
- [저장소 공간 다이렉트 볼륨 계획](plan-volumes.md)
- [오류 허용 하 고 저장소 효율성](storage-spaces-fault-tolerance.md)
