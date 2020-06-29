---
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
title: 스토리지 공간 다이렉트 드라이브 선택
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: 19679a6838d583ef93175f5f95aa21e8aeca9b36
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475260"
---
# <a name="choosing-drives-for-storage-spaces-direct"></a>스토리지 공간 다이렉트 드라이브 선택

>적용 대상: Windows 2019, Windows Server 2016

이 항목에서는 성능 및 용량 요구 사항을 충족 하기 위해 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md) 드라이브를 선택 하는 방법에 대 한 지침을 제공 합니다.

## <a name="drive-types"></a>드라이브 종류

현재 스토리지 공간 다이렉트는 다음과 같은 세 가지 유형의 드라이브로 작동 합니다.

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>NVMe</b> (비휘발성 메모리 Express)는 PCIe 버스에 직접 앉아 있는 반도체 드라이브를 나타냅니다. 일반적인 폼 팩터는 2.5 "U. 2, PCIe 추가 기능 카드 (AIC) 및 M. 2입니다. NVMe는 현재 지원 되는 다른 종류의 드라이브 보다 낮은 대기 시간으로 더 높은 IOPS 및 IO 처리량을 제공 합니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px" >
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>SSD</b> 는 기존 SATA 또는 SAS를 통해 연결 하는 반도체 드라이브를 나타냅니다.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>HDD</b> 는 광범위 한 저장소 용량을 제공 하는 회전, 자기 하드 디스크 드라이브를 의미 합니다.
        </td>
    </tr>
</table>

## <a name="built-in-cache"></a>기본 제공 캐시

스토리지 공간 다이렉트은 기본 제공 서버 쪽 캐시를 갖추고 있습니다. 이는 크고 영구적인 실시간 읽기/쓰기 캐시입니다. 여러 유형의 드라이브가 있는 배포에서는 "가장 빠른" 유형의 모든 드라이브를 사용 하도록 자동으로 구성 됩니다. 나머지 드라이브는 용량에 사용됩니다.

자세한 내용은 [스토리지 공간 다이렉트의 캐시 이해](understand-the-cache.md)를 참조 하세요.

## <a name="option-1--maximizing-performance"></a>옵션 1 – 성능 최대화

모든 데이터에 대 한 임의 읽기 및 쓰기에 대해 예측 가능 하 고 균일 한 밀리초의 대기 시간을 확보 하거나 매우 높은 IOPS ( [600만 이상](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m)에서 수행 됨) 또는 IO 처리량을 달성할 수 있도록 하려면 ( [1tb 이상](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s)) "모두-플래시"로 이동 해야 합니다.

현재는 다음 세 가지 방법으로이 작업을 수행할 수 있습니다.

![모두-플래시-배포-가능성](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **모든 NVMe.** 모든 NVMe를 사용 하면 예측 가능한 짧은 대기 시간을 포함 하 여 성능이 저하 됩니다. 모든 드라이브가 동일한 모델인 경우 캐시가 없습니다. Endurance 및 endurance NVMe 모델을 혼합할 수 있으며, 후자 ([설정 필요](understand-the-cache.md#manual-configuration))에 대 한 쓰기를 캐시 하도록 전자를 구성할 수도 있습니다.

2. **NVMe + SSD.** NVMe를 Ssd와 함께 사용 하면 NVMe가 자동으로 Ssd에 쓰기를 캐시 합니다. 이렇게 하면 쓰기를 캐시에 병합 하 고 필요한 경우에만 역직렬화 하 여 Ssd에서 마모를 줄일 수 있습니다. 이는 NVMe와 유사한 쓰기 특성을 제공 하는 반면 읽기는 고속 Ssd에서 직접 제공 됩니다.

3. **모든 SSD.** 모든 NVMe와 마찬가지로 모든 드라이브가 동일한 모델인 경우 캐시가 없습니다. Endurance 및 endurance 모델을 함께 사용 하는 경우에는 나중에 쓰기를 캐시 하도록 ([설정 필요](understand-the-cache.md#manual-configuration)) 이전을 구성할 수 있습니다.

   >[!NOTE]
   > 캐시 없이 모든-NVMe 또는 모든-SSD를 사용 하는 경우의 장점은 모든 드라이브에서 사용 가능한 저장소 용량을 얻는 것입니다. 캐싱에 "소요 되는" 용량은 더 작은 규모로 유용 합니다.

## <a name="option-2--balancing-performance-and-capacity"></a>옵션 2 – 성능 및 용량 분산

다양 한 응용 프로그램 및 워크 로드를 포함 하는 환경에서는 엄격한 성능 요구 사항과 상당한 저장소 용량을 필요로 하는 환경에서는 더 큰 Hdd을 위해 NVMe 또는 Ssd 캐싱을 "하이브리드"로 이동 해야 합니다.

![하이브리드 배포-가능성](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe + HDD**. NVMe 드라이브는 모두 캐시 하 여 읽기 및 쓰기를 가속화 합니다. 캐싱을 사용 하면 Hdd에서 쓰기에 집중할 수 있습니다. 캐싱은 대역과 버스트를 기록 하 고, 필요한 경우에만 쓰기를 허용 하 고, HDD IOPS 및 IO 처리량을 극대화 하는 인위적으로 직렬화 된 방식으로 쓰기를 취소할 수 있습니다. 이는 NVMe와 같은 쓰기 특성을 제공 하 고, 자주 또는 최근 데이터를 읽는 경우, NVMe와 유사한 읽기 특성도 제공 합니다.

2. **SSD + HDD**. 위의 경우와 유사 하 게, Ssd는 둘 모두를 캐시 하 여 읽기 및 쓰기를 가속화 합니다. 이는 SSD와 유사한 쓰기 특성 및 자주 또는 최근 데이터를 읽기 위해 SSD와 유사한 읽기 특성을 제공 합니다.

    3 가지 유형의 드라이브를 *모두* 사용 하는 exotic 옵션은 하나 더 있습니다.

3. **NVMe + SSD + HDD.** 이 세 가지 유형의 드라이브를 모두 사용 하 여 NVMe는 Ssd 및 Hdd 모두에 대 한 캐시를 구동 합니다. 따라서 Ssd에서 볼륨을 만들고, Hdd의 볼륨을 동일한 클러스터에서 side-by-side로 가속 하 여 만들 수 있습니다. 전자는 "모든 플래시" 배포와 정확히 동일 하며, 후자는 위에 설명 된 "하이브리드" 배포와 동일 합니다. 이는 개념적으로 독립적 용량 관리, 오류 및 복구 주기 등 두 개의 풀이 있는 것과 같습니다.

   >[!IMPORTANT]
   > SSD 계층을 사용 하 여 가장 성능이 중요 한 워크 로드를 모든 플래시에 저장 하는 것이 좋습니다.

## <a name="option-3--maximizing-capacity"></a>옵션 3 – 용량 최대화

대용량의 용량이 필요 하 고 보관, 백업 대상, 데이터 웨어하우스 또는 "콜드" 저장소와 같이 자주 쓰지 않는 워크 로드의 경우 용량에 대해 더 큰 Hdd를 사용 하 여 캐싱에 몇 개의 Ssd를 결합 해야 합니다.

![용량 극대화를 위한 배포 옵션](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSD + HDD**. Ssd는 읽기와 쓰기를 캐시 하 고, 버스트를 소개 하 고, 나중에 Hdd에 대해 최적화 된 준비 해제를 사용 하 여 SSD와 유사한 쓰기 성능을 제공 합니다.

>[!IMPORTANT]
>Hdd만 포함 된 구성은 지원 되지 않습니다. High endurance Ssd 캐싱은 낮은 endurance Ssd에 권장 되지 않습니다.

## <a name="sizing-considerations"></a>크기 조정 고려 사항

### <a name="cache"></a>캐시

모든 서버에는 적어도 두 개의 캐시 드라이브가 있어야 합니다 (중복성에 필요한 최소). 용량 드라이브의 수를 캐시 드라이브 수의 배수로 만드는 것이 좋습니다. 예를 들어 4 개의 캐시 드라이브가 있는 경우 7 또는 9 보다 8 개의 용량 드라이브 (1:2 비율)로 더 일관 된 성능을 경험할 수 있습니다.

응용 프로그램 및 워크 로드의 작업 집합을 수용 하기 위해 캐시 크기를 조정 해야 합니다. 즉, 지정 된 시간에 적극적으로 읽고 쓰는 모든 데이터입니다. 그 외에는 캐시 크기 요구 사항이 없습니다. Hdd를 사용 하 여 배포 하는 경우에는 각 서버에 4 x 4 TB HDD = 16tb의 1.6 800 용량이 있는 경우와 같이 공평 하 게 시작할 수 있습니다. 특히 매우 [높은 endurance](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/) ssd를 사용 하는 모든 플래시 배포의 경우 5%의 용량에 더 가까운 수준으로 시작 하는 것이 양호 합니다. 예를 들어 각 서버에 24 x 1.2 tb SSD = 28.8 tb의 용량이 있는 경우 2 x 750 GB NVMe = 1.5 tb의 서버 당 캐시가 포함 됩니다. 캐시 드라이브는 추후 언제든지 추가하거나 제거해서 조정할 수 있습니다.

### <a name="general"></a>일반

서버당 총 저장소 용량을 약 400 테라바이트 (TB)로 제한 하는 것이 좋습니다. 서버당 저장소 용량이 많을 수록, 소프트웨어 업데이트를 적용 하는 경우와 같이 가동 중지 또는 다시 부팅 후 데이터를 다시 동기화 하는 데 시간이 더 오래 걸립니다. 저장소 풀 당 현재 최대 크기는 Windows Server 2019의 경우 4 페타바이트 (PB) (4000 TB)이 고 Windows Server 2016의 경우 1 페타바이트입니다.

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- [스토리지 공간 다이렉트 캐시 이해](understand-the-cache.md)
- [하드웨어 요구 사항 스토리지 공간 다이렉트](storage-spaces-direct-hardware-requirements.md)
- [스토리지 공간 다이렉트에서 볼륨 계획](plan-volumes.md)
- [내결함성 및 스토리지 효율성](storage-spaces-fault-tolerance.md)
