---
title: 디스크 관리
description: 이 문서에서는 디스크를 관리하는 방법을 설명합니다.
ms.date: 06/07/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 0aac0b78e79949de94ebd20912b8c2b2db167339
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "71385875"
---
# <a name="manage-disks"></a>디스크 관리

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목과 하위 항목에서는 디스크 관리를 사용하여 컴퓨터의 디스크를 관리하는 방법을 설명하고, 새 디스크 초기화, 각기 다른 파티션 스타일 간 디스크 변환 및 Windows의 새 디스크 온라인 상태 처리 방법에 관한 정보를 포함합니다.

## <a name="online-and-offline-status"></a>온라인 및 오프라인 상태

디스크 관리는 디스크가 온라인 상태인지(사용 가능) 또는 오프라인 상태인지를 표시합니다.

Windows에서 기본적으로 모든 새로 검색한 디스크는 읽기 및 쓰기 권한이 탑재된 온라인 상태로 설정됩니다. Windows Server에서 기본적으로 새로 검색한 디스크는 공유 버스(예: SCSI, iSCSI, SAS(Serial Attached SCSI) 또는 파이버 채널)에 있는 경우 외에는 읽기 및 쓰기 권한이 탑재된 온라인 상태로 설정됩니다. 공유 버스에 있는 디스크는 검색되었을 때 처음에는 오프라인 상태로 설정됩니다.

디스크가 오프라인 상태인 경우 디스크를 초기화하거나 디스크에서 볼륨을 만들기 전에 온라인 상태로 설정해야 합니다.

디스크를 온라인 또는 오프라인 상태로 설정하려면 디스크 이름을 마우스 오른쪽 단추로 클릭하고 적절한 작업을 선택합니다.

## <a name="see-also"></a>참고 항목

-   [새 디스크 초기화](initialize-new-disks.md)
-   [디스크를 다른 컴퓨터로 이동](move-disks-to-another-computer.md)
-   [동적 디스크를 기본 디스크로 변경](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [마스터 부트 레코드 디스크를 GUID 파티션 테이블 디스크로 변경](change-an-mbr-disk-into-a-gpt-disk.md)
-   [GUID 파티션 테이블 디스크를 마스터 부트 레코드 디스크로 변경](change-a-gpt-disk-into-an-mbr-disk.md)
-   [가상 하드 디스크 관리](manage-virtual-hard-disks.md)