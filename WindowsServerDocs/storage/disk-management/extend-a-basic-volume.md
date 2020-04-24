---
title: 기본 볼륨 확장
description: 빈 공간에 볼륨이 없고(할당되어 있지 않음) 확장하려는 볼륨 바로 뒤에 다른 볼륨이 없는 경우에만 Windows에서 공간을 기존 볼륨에 추가하여 드라이브의 빈 공간으로 확장할 수 있습니다. 이 문서에서는 이 작업을 수행하는 방법을 설명합니다.
ms.date: 12/19/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c72b242437c4c308da77a25e06f3d76e4c65f480
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "75351897"
---
# <a name="extend-a-basic-volume"></a>기본 볼륨 확장

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 이미지와 같이 빈 공간에 볼륨이 없고(할당되어 있지 않음) 확장하려는 볼륨 바로 뒤에 다른 볼륨이 없는 경우에만 디스크 관리를 사용하여 공간을 기존 볼륨에 추가하여 드라이브의 빈 공간으로 확장할 수 있습니다. 확장할 볼륨도 NTFS 또는 ReFS 파일 시스템으로 포맷해야 합니다.

:::image type="content" source="media/extend-volume-space-highlighted.png" alt-text="볼륨이 확장될 수 있는 사용 가능한 공간을 보여 주는 디스크 관리":::

## <a name="to-extend-a-volume-by-using-disk-management"></a>디스크 관리를 사용하여 볼륨 확장

드라이브의 볼륨 바로 뒤에 있는 빈 공간으로 볼륨을 확장하는 방법은 다음과 같습니다.

1. 디스크 관리를 관리자 권한으로 엽니다.

   이 작업을 수행하는 쉬운 방법은 작업 표시줄의 검색 상자에서 **컴퓨터 관리**를 입력하고, **컴퓨터 관리**를 길게 누른(또는 마우스 오른쪽 단추로 클릭) 다음, **관리자 권한으로 실행** > **예**를 차례로 선택하는 것입니다. 컴퓨터 관리가 열리면 **스토리지** > **디스크 관리**로 차례로 이동합니다.
2. 확장하려는 볼륨을 길게 누른(또는 마우스 오른쪽 단추로 클릭) 다음, **볼륨 확장**을 선택합니다.

   **볼륨 확장**이 회색으로 표시되면 다음을 확인합니다.
    - 디스크 관리 또는 컴퓨터 관리가 관리자 권한으로 열렸습니다.
    - 위의 그림과 같이 볼륨 바로 뒤에 할당되지 않은 공간(오른쪽)이 있습니다. 할당되지 않은 공간과 확장하려는 볼륨 사이에 다른 볼륨이 있는 경우 볼륨과 이 볼륨의 모든 파일을 삭제하거나(중요한 파일은 먼저 백업하거나 이동해야 함!), 데이터를 삭제하지 않고 볼륨을 이동할 수 있는 타사 디스크 분할 앱을 사용하거나, 볼륨 확장을 건너뛰고 대신 할당되지 않은 공간에 별도의 볼륨을 만들 수 있습니다.
    - 볼륨은 NTFS 또는 ReFS 파일 시스템으로 포맷됩니다. 다른 파일 시스템은 확장할 수 없으므로 볼륨의 파일을 이동하거나 백업한 다음, 볼륨을 NTFS 또는 ReFS 파일 시스템으로 포맷해야 합니다.
    - 디스크가 2TB보다 큰 경우 GPT 파티션 구성표를 사용하고 있는지 확인합니다. 디스크에서 2TB를 초과하여 사용하려면 GPT 파티션 구성표를 사용하여 초기화해야 합니다. GPT로 변환하려면 [MBR 디스크를 GPT 디스크로 변경](change-an-mbr-disk-into-a-gpt-disk.md)을 참조하세요.
    - 여전히 볼륨을 확장할 수 없는 경우 [Microsoft 커뮤니티 - 파일, 폴더 및 스토리지](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639) 사이트 검색을 시도하고, 답변을 찾을 수 없는 경우 질문을 이 사이트에 게시하여 Microsoft 또는 커뮤니티 내 다른 구성원의 도움을 받으세요. [Microsoft 지원에 문의](https://support.microsoft.com/contactus/)하셔도 됩니다.

3. **다음**을 선택한 다음, 마법사의 **디스크 선택** 페이지(여기에 표시되어 있음)에서 볼륨을 확장할 크기를 지정합니다. 일반적으로 사용 가능한 공간을 모두 사용하는 기본값을 사용할 수 있지만, 볼륨을 사용 가능한 공간에 추가로 만들려는 경우 더 작은 값을 사용할 수 있습니다.

   :::image type="content" source="media/extend-volume-wizard.png" alt-text="사용 가능한 공간을 모두 사용하도록 확장되는 볼륨을 보여 주는 볼륨 확장 마법사":::

4. **다음**, **마침**을 차례로 선택하여 볼륨을 확장합니다.

## <a name="to-extend-a-volume-by-using-powershell"></a>PowerShell을 사용하여 볼륨 확장

1. [시작] 단추를 길게 누른(또는 마우스 오른쪽 단추로 클릭) 다음, [Windows PowerShell(관리자)]을 선택합니다.
2. 다음 명령을 입력하여 확장하려는 볼륨을 최대 크기로 조정하고 이 볼륨의 드라이브 문자를 *$drive_letter* 변수로 지정합니다.

   ```PowerShell
   # Variable specifying the drive you want to extend
   $drive_letter = "C"

   # Script to get the partition sizes and then resize the volume
   $size = (Get-PartitionSupportedSize -DriveLetter $drive_letter)
   Resize-Partition -DriveLetter $drive_letter -Size $size.SizeMax
   ```

## <a name="see-slso"></a>참고 항목

- [Resize-Partition](https://docs.microsoft.com/powershell/module/storage/resize-partition)
- [Diskpart extend](https://docs.microsoft.com/windows-server/administration/windows-commands/extend)
