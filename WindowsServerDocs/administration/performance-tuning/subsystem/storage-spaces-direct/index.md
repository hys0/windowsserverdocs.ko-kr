---
title: 스토리지 공간 다이렉트의 성능 조정
description: 스토리지 공간 다이렉트는 사용하는 하드웨어의 캐시 구성에 따라 자동으로 성능을 조정하며, 자세한 내용은 이 문서에 설명되어 있습니다.
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.assetid: 15a519fa-37cc-4d84-a9fe-097d33bb71ea
author: phstee
ms.author: vshankar; danlo; clausjor; stevenek
ms.date: 4/14/2017
ms.openlocfilehash: a24bbdb83ec1b08f56989368a4831549c594f6c0
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80851606"
---
# <a name="performance-tuning-for-storage-spaces-direct"></a>스토리지 공간 다이렉트의 성능 조정

Windows Server 기반 소프트웨어 정의 스토리지 솔루션인 스토리지 공간 다이렉트를 사용하면 자동으로 성능이 조정되기 때문에, 열 개수를 수동으로 지정하고, 사용하는 하드웨어의 캐시를 구성하고, 공유 SAS 스토리지 솔루션을 사용하여 수동으로 설정해야 할 필요가 없습니다. 배경 정보는 [Windows Server 2016의 스토리지 공간 다이렉트](../../../../storage/storage-spaces/storage-spaces-direct-overview.md)를 참조하세요.

스토리지 공간 다이렉트 소프트웨어 스토리지 버스 캐시는 시스템에 있는 스토리지 유형에 따라 자동으로 구성됩니다. 인식되는 3가지 유형은 **HDD**, **SSD**, **NVMe**입니다. 캐시는 읽기 및/또는 쓰기 캐싱을 위해 가장 빠른 스토리지를 적절하게 클레임하고, 데이터의 영구 스토리지에는 비교적 느린 스토리지를 사용합니다.

다음 표에는 기본값이 요약되어 있습니다.

| 스토리지 유형 | 캐시 구성 |
| --- | --- |
| 단일 유형 | 스토리지 유형이 하나만 있으면, 소프트웨어 스토리지 버스 캐시가 구성되지 않습니다. |
| SSD+HDD 또는 NVMe+HDD | 가장 빠른 스토리지가 캐시 계층으로 구성되고 캐시가 읽기와 쓰기를 모두 수행합니다. |
| SSD+SSD 또는 NVMe+NVMe | 고속+고속 옵션은 내구성이 낮은 스토리지와 높은 스토리지의 조합을 목표로 합니다. 예를 들어 캐시에는 10 DWPD(Drive Writes Per Day) NAND를 사용하고 용량에는 1.5 DWPD NAND 플래시 SSD를 사용합니다. 스토리지 공간 다이렉트에 캐시 디바이스를 식별하는 일련의 모델 문자열을 제공하면 설정이 가능합니다. 자세한 내용은 [Enable-StorageSpacesDirect](https://technet.microsoft.com/library/mt589697.aspx) cmdlet 참조(`CacheDeviceModel`)를 참조하세요. <br><br>고속+고속 시스템에서는 쓰기만 캐시됩니다. 읽기는 캐시되지 않습니다. |

SSD 또는 NVMe 디바이스를 통한 캐싱은 기본적으로 쓰기 캐싱만 사용합니다. 그 이유는 용량 디바이스가 빠르기 때문에 읽은 콘텐츠를 캐시 디바이스로 이동하는 경우 가치가 제한되기 때문입니다. 이것이 적용되지 않는 경우도 있지만 읽기 캐시를 활성화하면 주의를 기울여야 합니다. 읽기 캐시를 활성화하면 성능을 향상시키지 않고 캐시 디바이스 내구성을 불필요하게 소모할 수 있기 때문입니다. 다음과 같은 예제가 있습니다.

* **NVme+SSD** 읽기 캐시를 활성화하면 읽기 IO가 PCIe 연결을 활용하거나 집계된 SSD에 비해 NVMe 디바이스의 IOPS 성능이 향상되는 이점이 있습니다. <br>NVMe 디바이스의 상대 대역폭 기능과 SSD에 연결되는 HBA 때문에 대역폭 지향 시나리오에서 이것이 사실일 수 있습니다.  증가된 성능이 실현되기 전에 IOPS의 CPU 비용이 시스템을 제한할 수 있는 IOPS 지향 시나리오의 경우에는 그렇지 않을 수 있습니다. 
* **NVMe+NVMe** 마찬가지로, 캐시 NVMe의 읽기 용량이 결합된 용량 NVMe보다 크면, 읽기 캐시를 활성화할만한 가치가 있을 수 있습니다. <br>이러한 구성에서 읽기 캐시의 좋은 경우는 드물 것으로 예상되는 경우입니다.

캐시 구성 보기 및 변경에는 [Get-ClusterStorageSpacesDirect](https://technet.microsoft.com/library/mt634616.aspx) 및 [Set-ClusterStorageSpacesDirect](https://technet.microsoft.com/library/mt763265.aspx) cmdlet을 사용하세요. `CacheModeHDD` 및 `CacheModeSSD` 속성은 지정된 유형의 용량 미디어에서 캐시가 작동하는 방식을 정의합니다.

## <a name="see-also"></a>참고 항목

- [스토리지 공간 다이렉트 이해](../../../../storage/storage-spaces/understand-storage-spaces-direct.md)
- [스토리지 공간 다이렉트 계획](../../../../storage/storage-spaces/plan-storage-spaces-direct.md)
- [파일 서버에 대한 성능 조정](../../role/file-server/index.md)
- [소프트웨어 정의 스토리지 설계 고려 사항 가이드](https://technet.microsoft.com/library/mt243829.aspx)(Windows Server 2012 R2 및 공유 SAS 스토리지용)
