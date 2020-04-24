---
title: 디스크 관리 개요
description: 디스크 관리는 새로운 드라이브 초기화, 볼륨 확장, 파티션 축소, 드라이브 문자 변경과 같은 고급 스토리지 작업을 수행할 수 있도록 해주는 Windows의 시스템 유틸리티입니다.
ms.date: 06/07/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 46ed1256ed9039311939f9de12ea46416443be9c
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "71402149"
---
# <a name="overview-of-disk-management"></a>디스크 관리 개요

> **적용 대상:** Windows 10, Windows 8.1, Windows 7, Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디스크 관리는 고급 스토리지 작업을 수행할 수 있도록 해주는 Windows의 시스템 유틸리티입니다. 다음은 디스크 관리가 제공하는 몇 가지 이점입니다.

- 새 드라이브를 설치하려면 [새 드라이브 초기화](initialize-new-disks.md)를 참조하세요.
- 동일한 드라이브의 볼륨에 아직 속하지 않은 공간으로 볼륨을 확장하려면 [기본 볼륨 확장](extend-a-basic-volume.md)을 참조하세요.
- 파티션을 축소하려면 일반적으로 인접한 파티션을 확장할 수 있도록 [기본 볼륨 축소](shrink-a-basic-volume.md)를 참조하세요.
- 드라이브 문자를 변경하거나 새 드라이브 문자를 할당하려면 [드라이브 문자 변경](change-a-drive-letter.md)을 참조하세요.

![499MB 시스템 파티션, Windows용 대용량 C 드라이브, 복구용 다른 499MB 파티션 등 세 개의 파티션이 있는 일반적인 드라이브를 보여주는 디스크 관리](media/disk-management.png)

> [!TIP]
>  이러한 절차를 수행할 때 오류가 발생하거나 무언가가 작동하지 않는 경우 [디스크 관리 문제 해결](troubleshooting-disk-management.md) 항목을 살펴보세요. 해결되지 않는다고 놀라지 마세요! [Microsoft 커뮤니티](https://answers.microsoft.com/en-us/windows) 사이트에 수 많은 정보가 있습니다. [파일, 폴더 및 스토리지](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639) 섹션을 검색해보고, 그래도 도움이 필요하면 질문을 게시하세요. 그러면 Microsoft 또는 커뮤니티의 다른 멤버로부터 도움을 받을 수 있습니다. 이러한 문서의 개선 방안에 대한 피드백이 있으면 주저하지 말고 의견을 알려주세요! *이 페이지가 도움이 되었나요?* 메시지에 답변을 하거나 이 문서의 맨 아래에 있는 공개 코멘트 스레드에 의견을 남겨주세요.

Windows에서 다른 도구를 사용하는 몇 가지 일반적인 작업은 다음과 같습니다.

- 디스크 공간을 확보하려면 [Windows 10의 드라이브 공간 확보](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)를 참조하세요.
- 드라이브의 조각 모음을 수행하려면 [Windows 10 PC 조각 모음](https://support.microsoft.com/help/4026701/windows-defragment-your-windows-10-pc)을 참조하세요.
- 여러 하드 드라이브를 사용하고 RAID처럼 함께 풀링하려면 [스토리지 공간](https://support.microsoft.com/help/12438/windows-10-storage-spaces)을 참조하세요.

## <a name="about-those-extra-recovery-partitions"></a>이러한 추가 복구 파티션 정보

궁금한 경우(사용자의 코멘트를 읽음!) Windows는 일반적으로 기본 드라이브에 세 개의 파티션(일반적으로 C:\ 드라이브)을 포함합니다.

![EFI 시스템 파티션, Windows 파티션, 복구 파티션 등 세 개의 파티션이 표시된 디스크 0](media/windows-partitions.png)

- **EFI 시스템 파티션** - 최신 PC에서 PC 및 운영 체제를 시작하기 위해(부팅) 사용됩니다.
- **Windows 운영 체제 드라이브(C:)** - Windows가 설치되어 있고 일반적으로 앱 및 파일의 나머지 부분을 배치하는 위치입니다.
- **복구 파티션** - Windows를 시작하는 데 문제가 있거나 다른 심각한 문제가 발생할 경우 복구하는 데 도움이 되는 특수한 도구가 저장되어 있습니다.

디스크 관리에서는 EFI 시스템 파티션과 복구 파티션이 100% 비었다고 표시될 수도 있지만, 거짓말입니다. 이 파티션들은 일반적으로 사용자의 PC가 제대로 작동하는 데 필요한 정말 중요한 파일들로 가득 차있습니다. PC를 시작하고 문제로부터 복구하는 데 도움을 주기 위해서는 그냥 내버려 두는 것이 가장 좋습니다.

## <a name="see-also"></a>참고 항목

- [디스크 관리](manage-disks.md)
- [기본 볼륨 관리](manage-basic-volumes.md)
- [디스크의 관리 문제 해결](troubleshooting-disk-management.md)
- [Windows 10의 복구 옵션](https://support.microsoft.com/help/12415/windows-10-recovery-options)
- [Windows 10으로 업데이트한 후 손실된 파일 찾기](https://support.microsoft.com/help/12386/windows-10-find-lost-files-after-update)
- [파일 백업 및 복원](https://support.microsoft.com/help/17143/windows-10-back-up-your-files)
- [복구 드라이브 만들기](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)
- [시스템 복원 지점 만들기](https://support.microsoft.com/help/4027538/windows-create-a-system-restore-point)
- [내 BitLocker 복구 키 찾기](https://support.microsoft.com/help/4026181/windows-find-my-bitlocker-recovery-key)
