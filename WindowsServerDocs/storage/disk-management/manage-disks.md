---
title: 디스크 관리
description: 이 문서에서는 디스크를 관리하는 방법을 설명합니다.
ms.date: 12/21/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f4698dac683ff3769eb4403ae2750ad38a301022
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846194"
---
# <a name="manage-disks"></a>디스크 관리

> **적용 대상:** Windows 10, Windows 8.1, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목 및 하위 디스크 관리를 사용 하 여 컴퓨터에 디스크를 관리 하 고 다른 파티션 스타일 및 Windows에서 새 디스크의 온라인 상태를 처리 하는 방법 간에 디스크를 변환 하는 새 디스크를 초기화 하는 방법에 대 한 정보가 포함 되어 있습니다.

## <a name="online-and-offline-status"></a>온라인 및 오프라인 상태

디스크 관리 디스크를 온라인 인지를 표시 합니다 (사용 가능) 또는 오프 라인입니다.

Windows에서 기본적으로 모든 새로 검색한 디스크는 읽기 및 쓰기 권한이 탑재된 온라인 상태로 설정됩니다. Windows Server에서 기본적으로 새로 검색한 디스크는 공유 버스(예: SCSI, iSCSI, SAS(Serial Attached SCSI) 또는 파이버 채널)에 있는 경우 외에는 읽기 및 쓰기 권한이 탑재된 온라인 상태로 설정됩니다. 공유 버스에 디스크는 처음으로 감지 되는 오프 라인입니다.

디스크가 오프라인 상태인 경우 디스크를 초기화하거나 디스크에서 볼륨을 만들기 전에 온라인 상태로 설정해야 합니다.

디스크를 온라인 상태로 만드는 또는 오프 라인으로 전환 하려면 디스크 이름을 선택한 후 적절 한 조치를 마우스 오른쪽 단추로 클릭 합니다.





## <a name="see-also"></a>관련 항목

-   [새 디스크를 초기화 합니다.](initialize-new-disks.md)
-   [디스크를 다른 컴퓨터로 이동](move-disks-to-another-computer.md)
-   [동적 디스크를 기본 디스크로 변경](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [마스터 부트 레코드 디스크 GUID 파티션 테이블 디스크를 변경 합니다.](change-an-mbr-disk-into-a-gpt-disk.md)
-   [마스터 부트 레코드 디스크 GUID 파티션 테이블 디스크 변경](change-a-gpt-disk-into-an-mbr-disk.md)
-   [가상 하드 디스크 관리](manage-virtual-hard-disks.md)