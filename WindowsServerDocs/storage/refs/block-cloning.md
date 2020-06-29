---
ms.assetid: fd427da3-3869-428f-bf2a-56c4b7d99b40
title: ReFS에 대 한 복제 차단
author: gawatu
ms.author: gawatu
manager: gawatu
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: storage-file-systems
ms.openlocfilehash: c74e8744c22e2be174c1f1297e0472e5f32e1fe8
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475410"
---
# <a name="block-cloning-on-refs"></a>ReFS에 대 한 복제 차단

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

블록 복제는 응용 프로그램을 대신 하 여 파일 시스템에 파일 바이트의 범위를 복사 하도록 지시 합니다. 여기서 대상 파일은 원본 파일과 동일 하거나 다른 위치에 있을 수 있습니다. 불행 하 게도 복사 작업은 비용이 많이 드는 실제 데이터에 대 한 읽기 및 쓰기 비용이 많이 들기 때문에 비용이 많이 듭니다.

그러나 ReFS에서 복제를 차단 하면 파일 데이터를 읽고 쓰는 대신 저비용의 메타 데이터 작업으로 복사를 수행 합니다. ReFS에서는 여러 개의 파일이 같은 논리 클러스터(볼륨에서의 물리적 위치)를 공유할 수 있으므로 복사 작업이 파일의 특정 영역을 별도의 물리적 위치로 다시 매핑하기만 하면 되어 비용이 많이 드는 물리적 작업이 빠르고 논리적인 작업으로 바뀝니다. 이렇게 하면 복사를 더 빠르게 완료 하 고 기본 저장소에 대 한 i/o를 줄일 수 있습니다. 이러한 향상 된 기능은 가상화 작업에도 도움이 됩니다. 즉, 블록 복제 작업을 사용할 때 vhdx 검사점 병합 작업을 크게 가속화 합니다. 또한 여러 파일이 동일한 논리적 클러스터를 공유할 수 있기 때문에 동일한 데이터는 물리적으로 여러 번 저장 되지 않으므로 저장소 용량이 향상 됩니다.

## <a name="how-it-works"></a>작동 방법

ReFS에 대 한 복제 차단 파일 데이터 작업을 메타 데이터 작업으로 변환 합니다. 이러한 최적화를 위해 ReFS는 복사 된 영역에 대 한 메타 데이터에 대 한 참조 횟수를 제공 합니다. 이 참조 횟수는 동일한 물리적 영역을 참조 하는 고유한 파일 영역 수를 기록 합니다. 이렇게 하면 여러 파일이 동일한 물리적 데이터를 공유할 수 있습니다.

![여러 파일이 동일한 영역을 참조 하는 경우 참조 횟수 업데이트 표시](media/ref-count-example.gif)

ReFS는 각 논리 클러스터에 대 한 참조 횟수를 유지 하므로 파일 간의 격리가 중단 되지 않습니다. 공유 영역에 대 한 쓰기는 할당 쓰기 메커니즘을 트리거합니다. 여기서 ReFS는 들어오는 쓰기에 대 한 새 영역을 할당 합니다. 이 메커니즘은 공유 논리 클러스터의 무결성을 유지 합니다.

### <a name="example"></a>예제
각 파일이 세 개의 지역으로 구성 되 고 각 지역은 별도의 논리 클러스터에 매핑되는 두 개의 파일 (X 및 Y)이 있다고 가정 합니다.

![각각에 대 한 참조 개수가 1 인 지역에 매핑되는 세 개의 고유한 지역이 있는 두 개의 파일](media/block-clone-1.png)

이제 응용 프로그램이 X에서 파일 Y로의 블록 복제 작업을 실행 한다고 가정 합니다. 지역 A와 B는 지역 E의 오프셋에 복사 됩니다. 다음 파일 시스템 상태를 반환 합니다.

![참조 횟수는 차단 된 복제 영역에 대해 2를 표시 합니다.](media/block-clone-2.png)

이 파일 시스템 상태는 복제 된 블록 영역이 성공적으로 중복 되는 것을 나타냅니다. ReFS는 VCN을 LCN 매핑으로만 업데이트 하 고, 물리적 데이터를 읽지 않았거나, 파일 Y의 물리적 데이터를 덮어쓰는 방법으로이 복사 작업을 수행 합니다. 이제 X 및 Y 파일은 테이블의 참조 횟수를 반영 하 여 논리적 클러스터를 공유 합니다. 실제로 복사 된 데이터가 없으므로 ReFS는 볼륨의 용량 소비를 줄입니다.

이제 응용 프로그램이 X 파일에서 지역 A를 덮어쓰려고 한다고 가정 합니다. ReFS는 공유 지역을 복제 하 고, 참조 횟수를 적절 하 게 업데이트 하 고, 새로 복제 된 지역에 들어오는 쓰기를 수행 합니다. 이렇게 하면 파일 간의 격리가 유지 됩니다.

![새 지역 G에 쓰고 참조 횟수를 업데이트 하 여 격리 유지](media/block-clone-3.png)

수정 후에는 지역 B가 두 파일 모두에서 계속 공유 됩니다. 지역 A가 클러스터 보다 큰 경우 수정 된 클러스터만 중복 되 고 나머지 부분은 공유 된 상태로 유지 됩니다.


## <a name="functionality-restrictions-and-remarks"></a>기능 제한 사항 및 설명
- 원본 및 대상 지역은 클러스터 경계에서 시작 하 고 끝나야 합니다.
- 복제 된 영역의 길이는 4GB 미만 이어야 합니다.
- 동일한 물리적 지역에 매핑할 수 있는 최대 파일 영역 수는 8175입니다.
- 대상 지역은 파일의 끝을 지나서 확장 해서는 안 됩니다. 응용 프로그램이 복제 된 데이터로 대상을 확장 하려는 경우 먼저 [SetEndOfFile](https://msdn.microsoft.com/library/windows/desktop/aa365531(v=vs.85).aspx)를 호출 해야 합니다.
- 원본 및 대상 지역이 동일한 파일에 있는 경우 겹치지 않아야 합니다. 응용 프로그램은 블록 복제 작업을 더 이상 겹치지 않는 여러 블록 클론으로 분할 하 여 계속할 수 있습니다.
- 원본 및 대상 파일은 동일한 ReFS 볼륨에 있어야 합니다.
- 원본 및 대상 파일의 [무결성 스트림](https://msdn.microsoft.com/library/windows/desktop/gg258117(v=vs.85).aspx) 설정이 동일 해야 합니다.
- 원본 파일이 스파스 인 경우 대상 파일도 스파스 여야 합니다.
- 블록 복제 작업을 수행 하면 공유 된 Oplocks가 중단 됩니다 ( [수준 2 oplocks](https://msdn.microsoft.com/library/windows/desktop/aa365713(v=vs.85).aspx)로도 인식 됨).
- ReFS 볼륨은 Windows Server 2016로 포맷 되어 있어야 하 고 장애 조치 (Failover) 클러스터링을 사용 하는 경우 형식 지정 시 클러스터링 기능 수준이 Windows Server 2016 이상 이어야 합니다.

## <a name="additional-references"></a>추가 참조

-   [ReFS 개요](refs-overview.md)
-   [ReFS 무결성 스트림](integrity-streams.md)
-   [스토리지 공간 다이렉트 개요](../storage-spaces/storage-spaces-direct-overview.md)
-   [DUPLICATE_EXTENTS_DATA](https://msdn.microsoft.com/library/windows/desktop/mt590821(v=vs.85).aspx)
-   [FSCTL_DUPLICATE_EXTENTS_TO_FILE](https://msdn.microsoft.com/library/windows/desktop/mt590823(v=vs.85).aspx)
