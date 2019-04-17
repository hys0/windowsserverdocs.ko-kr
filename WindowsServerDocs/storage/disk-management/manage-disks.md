---
title: "디스크 관리"
description: "이 문서에서는 디스크를 관리하는 방법을 설명합니다."
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ae96071733b961fbe65551120894c21c633db83e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="manage-disks"></a>디스크 관리

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목과 하위 항목에서는 디스크 관리를 사용하여 컴퓨터의 디스크를 관리하는 것에 관하여 설명합니다. 각기 다른 파티션 스타일 간 디스크 변환과 Windows의 새 디스크 온라인 상태 처리 방법에 관한 정보가 포함됩니다.

## <a name="converting-disk-types"></a>디스크 유형 변환

디스크 관리를 통해 다양한 유형 및 파티션 스타일 사이에서 디스크를 변경할 수 있지만 (드라이브를 다시 포맷하지 않는 이상) 되돌릴 수 없는 작업이 몇 가지 있습니다. 응용 프로그램에 가장 적합한 디스크 유형과 파티션 스타일을 신중하게 고려해야 합니다.

다음 표는 다양한 파티션 스타일 사이에서의 디스크 변환 옵션을 보여줍니다.

| 디스크 유형 | MBR로 변환  | GPT로 변환| 동적으로 변환 |
| ---- | --- | --- |--- |
| <p>MBR(마스터 부트 레코드)</p> | <p>--</p> | <p>허용됩니다(디스크에 볼륨이 없는 경우).</p> | <p>허용되지만 디스크가 부팅 불가능해질 수 있습니다. 다음을 참조하세요.</p> |
| <p>GPT(GUID 파티션 테이블)</p> | <p>허용됩니다(디스크에 볼륨이 없는 경우).</p> | <p>--</p>  | <p>허용되지만 디스크가 부팅 불가능해질 수 있습니다. 다음을 참조하세요.</p> |


> [!NOTE]
> 다중 부팅 시나리오에서 하나의 운영 체제로 부팅했고, 대체 운영 체제가 포함된 기본 MBR 디스크를 동적 디스크로 변환한 경우 대체 운영 체제로는 더 이상 부팅할 수 없습니다.

## <a name="online-and-offline-status"></a>온라인 및 오프라인 상태

디스크 관리는 디스크의 온라인 및 오프라인 상태를 표시합니다. 

Windows에서 기본적으로 모든 새로 검색한 디스크는 읽기 및 쓰기 권한이 탑재된 온라인 상태로 설정됩니다. Windows Server에서 기본적으로 새로 검색한 디스크는 공유 버스(예: SCSI, iSCSI, SAS(Serial Attached SCSI) 또는 파이버 채널)에 있는 경우 외에는 읽기 및 쓰기 권한이 탑재된 온라인 상태로 설정됩니다. 공유 버스에 있는 디스크는 검색되었을 때 처음에는 오프라인 상태로 설정됩니다.

디스크가 오프라인 상태인 경우 디스크를 초기화하거나 디스크에서 볼륨을 만들기 전에 온라인 상태로 설정해야 합니다. 

-  디스크 이름을 마우스 오른쪽 단추로 클릭하고 적절한 작업을 선택하여 디스크를 온라인 또는 오프라인 상태로 설정합니다.

## <a name="see-also"></a>참고 항목

-   [새 디스크 초기화](initialize-new-disks.md)
-   [디스크를 다른 컴퓨터로 이동](move-disks-to-another-computer.md)
-   [동적 디스크를 기본 디스크로 변경](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [마스터 부트 레코드 디스크를 GUID 파티션 테이블 디스크로 변경](change-an-mbr-disk-into-a-gpt-disk.md)
-   [GUID 파티션 테이블 디스크를 마스터 부트 레코드 디스크로 변경](change-a-gpt-disk-into-an-mbr-disk.md)
-   [가상 하드 디스크 관리](manage-virtual-hard-disks.md)