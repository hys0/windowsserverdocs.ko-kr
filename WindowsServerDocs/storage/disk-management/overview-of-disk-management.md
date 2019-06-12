---
title: 디스크 관리 개요
description: 디스크 관리는 새 드라이브를 초기화, 볼륨 확장, 축소 파티션 및 드라이브 문자 변경 등의 고급 저장소 작업을 수행할 수 있는 Windows에서 시스템 유틸리티입니다.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a3885ae6b09ad431fd1ea5e4c593e02c7bb274d9
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812551"
---
# <a name="overview-of-disk-management"></a>디스크 관리 개요

> **적용 대상:** Windows 10, Windows 8.1, Windows 7, Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디스크 관리는 고급 저장소 작업을 수행할 수 있는 Windows에서 시스템 유틸리티입니다. 일부의 디스크 관리에 대 한 적합 한 작업은 다음과 같습니다.

- 새 드라이브를 설치 하려면 참조 [새 드라이브를 초기화할](initialize-new-disks.md)합니다.
- 볼륨에 포함 되지 않은 이미 동일한 드라이브에 볼륨의 공간으로 확장 참조 [기본 볼륨을 확장](extend-a-basic-volume.md)합니다.
- 파티션을 축소 하기 위해 일반적으로 인접 한 파티션을 확장할 수 있습니다, 있도록 볼 [기본 볼륨 축소](shrink-a-basic-volume.md)합니다.
- 참조를 드라이브 문자를 변경 하거나 새 드라이브 문자를 할당 하려면 [드라이브 문자 변경](change-a-drive-letter.md)합니다.

![3 개의 파티션과-값인 499 MB 시스템 파티션을, Windows에 대 한 더 큰 C 드라이브로 및 다른 값인 499 MB 파티션 복구에 대 한 일반적인 드라이브를 표시 하는 디스크 관리](media/disk-management.png)

> [!TIP]
>  오류가 발생할 경우 이러한 절차를 수행 하는 경우 작동 하지 않는 살펴볼을 수행 합니다 [디스크 관리 문제 해결](troubleshooting-disk-management.md) 항목입니다. -도움이 되지 않으면 놀라지 마십시오. 많은 정보는를 [Microsoft 커뮤니티](https://answers.microsoft.com/en-us/windows) 사이트-검색 해 보세요 합니다 [파일, 폴더 및 저장소](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639) 섹션을 여전히 도움이 필요한 경우 게시 그곳에 질문 하 고 Microsoft 나 다른 멤버를 커뮤니티를 시도 합니다. 이러한 항목을 개선 하는 방법에 대 한 의견이 있는 경우 주시길 부탁 드립니다! 대답 해 합니다 *이 페이지를 유용?* 있습니다 또는이 항목의 맨 아래에서 공용 주석 스레드 프롬프트를 두고 의견을 남겨 주세요.

몇 가지 일반적인 작업 수행 하려는 하지만 Windows의 다른 도구를 사용 하는:

- 디스크 공간을 확보 하려면 참조 [Windows 10의 드라이브 공간을 확보 하기](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)합니다.
- 드라이브 조각 모음을 참조 하세요 [Windows 10 PC를 조각 모음](https://support.microsoft.com/help/4026701/windows-defragment-your-windows-10-pc)합니다.
- 여러 하드 드라이브를 사용 하 고 RAID와 마찬가지로 함께 풀링하면, 참조 [저장소 공간](https://support.microsoft.com/help/12438/windows-10-storage-spaces)입니다.

## <a name="about-those-extra-recovery-partitions"></a>이러한 추가 복구 파티션 정보

Windows 기본 드라이브 (일반적으로 C:\에 3 개의 파티션을 일반적으로 포함 됩니다 (의견 읽은 것!) 궁금 하는 경우 드라이브):

![0 보여 주는 세 개의 파티션-EFI 시스템 파티션을, Windows 파티션과 복구 파티션을 디스크합니다](media/windows-partitions.png)

- **EFI 시스템 파티션을** -(부팅)을 시작 하려면 최신 Pc에 의해 사용이 PC와 운영 체제입니다.
- **Windows 운영 체제 드라이브 (c:)** -Windows가 설치 되어 있고 일반적으로 앱 및 파일의 나머지 부분을 배치 하는 위치입니다.
- **복구 파티션을** -문제가 시작 되었거나 다른 심각한 문제에 실행 되는 경우 Windows를 복구할 수 있도록 특수 한 도구가 저장 되는 위치입니다.

디스크 관리는 100% 사용 가능한 것으로 EFI 시스템 파티션과 복구 파티션을 표시 될 수 있습니다, 있지만 있는 합니다. 이러한 파티션은 PC가 정상적으로 작동 해야 하는 매우 중요 한 파일을 사용 하 여 전체 매우 일반적입니다. PC를 시작 하 고 문제 로부터 복구할 수 있도록 해당 작업을 수행 하려면 이러한 하는 것이 좋습니다.

## <a name="see-also"></a>참조

- [디스크 관리](manage-disks.md)
- [기본 볼륨 관리](manage-basic-volumes.md)
- [디스크 관리 문제 해결](troubleshooting-disk-management.md)
- [Windows 10에서 복구 옵션](https://support.microsoft.com/help/12415/windows-10-recovery-options)
- [Windows 10으로 업데이트 한 후 손실 된 파일 찾기](https://support.microsoft.com/help/12386/windows-10-find-lost-files-after-update)
- [백업 및 파일 복원](https://support.microsoft.com/help/17143/windows-10-back-up-your-files)
- [복구 드라이브 만들기](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)
- [시스템 복원 지점 만들기](https://support.microsoft.com/help/4027538/windows-create-a-system-restore-point)
- [BitLocker 복구 키 찾기](https://support.microsoft.com/help/4026181/windows-find-my-bitlocker-recovery-key)
