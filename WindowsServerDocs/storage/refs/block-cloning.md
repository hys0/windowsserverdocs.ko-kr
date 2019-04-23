---
ms.assetid: fd427da3-3869-428f-bf2a-56c4b7d99b40
title: ReFS에서 블록 복제
description: ''
author: gawatu
ms.author: gawatu
manager: gawatu
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage-file-systems
ms.openlocfilehash: 54165700209320eee50fc63d98d78cbf4a92d053
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838114"
---
# <a name="block-cloning-on-refs"></a>ReFS에서 블록 복제

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

블록 복제는 응용 프로그램을 대신하여 파일 시스템에게 일정 범위의 파일 바이트를 복사하도록 지시하는데, 대상 파일은 원본 파일과 같을 수도 있고 다를 수도 있습니다. 복사 작업은 안타깝게도 비용이 많이 듭니다. 비용이 많이 드는 기본 물리적 데이터에 대한 읽기 및 쓰기를 발생시키기 때문입니다. 

그러나 ReFS에서의 블록 복제는 파일 데이터를 읽고 쓰는 대신 비용이 적게 드는 메타데이터 작업으로 복사를 수행합니다. ReFS에서는 여러 개의 파일이 같은 논리 클러스터(볼륨에서의 물리적 위치)를 공유할 수 있으므로 복사 작업이 파일의 특정 영역을 별도의 물리적 위치로 다시 매핑하기만 하면 되어 비용이 많이 드는 물리적 작업이 빠르고 논리적인 작업으로 바뀝니다. 따라서 더 빠르게 복사 작업을 완료할 수 있고 기본 저장소에 발생하는 입출력이 줄어듭니다. 이러한 개선 사항은 가상화 작업에도 이점으로 작용합니다. 블록 복제 작업 시 .vhdx 검사점 병합 작업 속도가 크게 빨라지기 때문입니다. 또한 여러 개의 파일이 같은 논리 클러스터를 공유할 수 있으므로 동일한 데이터가 물리적으로 여러 번 저장되지 않아서 저장소 용량을 개선할 수 있습니다. 
  
## <a name="how-it-works"></a>작동 방법 

ReFS에서의 블록 복제는 파일 데이터 작업을 메타데이터 작업으로 변환합니다. 이러한 최적화 작업을 수행하기 위해 ReFS는 복사된 영역에 대한 메타데이터에 참조 개수를 적용합니다. 이 참조 개수는 동일한 물리적 영역을 참조하는 별개의 파일 영역 수를 기록합니다. 따라서 여러 개의 파일이 동일한 물리적 데이터를 공유할 수 있습니다.

![여러 개의 파일이 동일한 영역을 참조할 때 참조 개수 업데이트 표시](media/ref-count-example.gif)

각 논리 클러스터에 대한 참조 개수를 기록함으로써 ReFS는 파일 간의 분리를 유지합니다. 공유 영역에 대한 쓰기는 쓰기 시 할당 메커니즘을 발생시키고, ReFS는 들어오는 쓰기를 위한 새 영역을 할당합니다. 이 메커니즘을 통해 공유 논리 클러스터의 무결성이 유지됩니다. 

### <a name="example"></a>예제
두 개의 파일 X와 Y가 있고, 각 파일은 세 개의 영역으로 구성되며, 각 영역은 별개의 논리 클러스터에 매핑된다고 가정해 보겠습니다.

![두 파일은 각각 별개의 영역 3개가 있고, 모든 영역은 참조 개수가 1인 영역에 매핑됩니다.](media/block-clone-1.png)

이제 응용 프로그램이 파일 X에서 파일 Y로 블록 복제 작업을 보내서 영역 A와 B가 영역 E의 오프셋에 복사되도록 하려고 한다고 가정합니다. 다음 파일 시스템 상태와 같은 결과를 얻게 됩니다.

![블록 복제 영역에 참조 개수 2가 표시됩니다.](media/block-clone-2.png)

이 파일 시스템 상태는 블록 복제 영역의 복제 성공을 보여줍니다. ReFS는 단지 VCN에서 LCN으로의 매핑만을 업데이트하여 이 복사 작업을 수행하기 때문에 물리적 데이터를 읽지도 않고, 파일 Y의 물리적 데이터가 덮어쓰여지지도 않았습니다. 파일 X와 Y는 이제 논리 클러스터를 공유하며, 이는 테이블의 참조 개수에 나타나 있습니다. 어떠한 데이터도 물리적으로 복사되지 않았기 때문에 ReFS는 볼륨 소비를 줄입니다. 

이제 응용 프로그램이 파일 X의 영역 A를 덮어쓰려 한다고 가정해 보겠습니다. ReFS는 공유 영역을 복제하고, 참조 개수를 적절하게 업데이트하고, 새로 복제된 영역에 들어오는 쓰기를 수행합니다. 따라서 파일 간 분리가 유지됩니다.   

![새 영역 G에 쓰고 참조 개수를 업데이트함으로써 분리 유지](media/block-clone-3.png)

쓰기를 수정한 후에도 두 파일은 B 영역을 여전히 공유합니다. A 영역이 클러스터보다 클 경우 수정된 클러스터만 복제되며 남은 부분은 공유된 채로 남아 있습니다.


## <a name="functionality-restrictions-and-remarks"></a>기능 제한 및 설명
- 원본과 대상 영역은 클러스터 경계에서 시작하고 끝나야 합니다. 
- 복제된 영역의 길이는 4GB 미만이어야 합니다. 
- 같은 물리적 영역에 매핑할 수 있는 파일 영역의 최대 수는 8175입니다.
- 대상 영역은 파일의 끝을 지나도록 확장할 수 없습니다. 응용 프로그램이 복제된 데이터로 대상 영역을 확장하고자 한다면 먼저 [SetEndOfFile](https://msdn.microsoft.com/library/windows/desktop/aa365531(v=vs.85).aspx)을 호출해야 합니다. 
- 원본 및 대상 영역이 같은 파일에 있는 경우 두 영역이 겹쳐서는 안 됩니다. (응용 프로그램은 겹치지 않도록 블록 복제 작업을 여러 개의 블록 복제로 분할함으로써 계속 실행될 수 있습니다.)
- 원본 및 대상 파일은 같은 ReFS 볼륨에 있어서는 안 됩니다. 
- 원본 및 대상 파일은 [Integrity Streams](https://msdn.microsoft.com/library/windows/desktop/gg258117(v=vs.85).aspx) 설정이 같아야 합니다. 
- 원본 파일이 스파스인 경우 대상 파일도 스파스여야 합니다. 
- 블록 복제 작업은 공유 편의적 잠금([2단계 편의적 잠금](https://msdn.microsoft.com/library/windows/desktop/aa365713(v=vs.85).aspx)이라고도 함)을 중단합니다.
- ReFS 볼륨은 Windows Server 2016으로 포맷되어야 하며, 장애 조치(Failover) 클러스터링을 사용 중인 경우 포맷할 때 클러스터링 기능 수준은 Windows Server 2016 이상이어야 합니다. 

## <a name="see-also"></a>참조

-   [ReFS 개요](refs-overview.md)
-   [ReFS의 무결성 스트림](integrity-streams.md)
-   [저장소 공간 다이렉트 개요](../storage-spaces/storage-spaces-direct-overview.md)
-   [DUPLICATE_EXTENTS_DATA](https://msdn.microsoft.com/library/windows/desktop/mt590821(v=vs.85).aspx)
-   [FSCTL_DUPLICATE_EXTENTS_TO_FILE](https://msdn.microsoft.com/library/windows/desktop/mt590823(v=vs.85).aspx)
