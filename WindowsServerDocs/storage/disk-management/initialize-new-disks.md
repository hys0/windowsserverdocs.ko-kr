---
title: 새 디스크 초기화
description: 디스크 관리를 통해 새 디스크를 초기화하여 사용하도록 준비하는 방법입니다. 또한 문제 해결에 대한 링크도 포함되어 있습니다.
ms.date: 12/20/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c2cb88d5b30be28a8ab7709e3a3908ce82ae8408
ms.sourcegitcommit: bfe9c5f7141f4f2343a4edf432856f07db1410aa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75352354"
---
# <a name="initialize-new-disks"></a>새 디스크 초기화

> **적용 대상:** Windows 10, Windows 8.1, Windows 7, Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

PC에 새 디스크를 추가했으나 파일 탐색기에 표시되지 않으면 사용하기 위해 [드라이브 문자를 추가](change-a-drive-letter.md)하거나 먼저 초기화해야 할 수 있습니다. 아직 포맷되지 않은 드라이브만 초기화할 수 있습니다. 디스크를 초기화하면 모든 내용이 Windows에서 사용할 준비가 됩니다. 그러면 디스크를 포맷한 후 파일을 저장할 수 있습니다.

> [!WARNING]
> 디스크에 관심이 있는 파일이 이미 있으면 초기화하지 않도록 합니다. 초기화하면 모든 파일을 잃게 됩니다. 대신, 디스크 문제를 해결하여 파일을 읽을 수 있는지 확인하는 것이 좋습니다. [디스크의 상태가 초기화되지 않음 또는 디스크가 완전히 누락됨](troubleshooting-disk-management.md#disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps)을 참조하세요.

## <a name="to-initialize-new-disks"></a>새 디스크 초기화

디스크 관리를 사용하여 새 디스크를 초기화하는 방법은 다음과 같습니다. PowerShell을 사용하려는 경우 [initialize-disk](https://docs.microsoft.com/powershell/module/storage/initialize-disk) cmdlet을 대신 사용합니다.

1. 디스크 관리를 관리자 권한으로 엽니다.
 
    이렇게 하려면 작업 표시줄의 검색 상자에 **디스크 관리**를 입력하고 **디스크 관리**를 길게 선택(또는 마우스 오른쪽 단추로 클릭)한 다음, **관리자 권한으로 실행** > **예**를 선택합니다. 관리자 권한으로 열 수 없으면 대신, **컴퓨터 관리**를 입력하고 **스토리지** > **디스크 관리**로 이동합니다.
1. 디스크 관리에서 초기화하고자 하는 디스크를 마우스 오른쪽 단추로 클릭하고 **디스크 초기화**를 클릭합니다(그림 참조). 디스크가 *오프라인*으로 표시되면 먼저 마우스 오른쪽 단추로 클릭하고 **온라인**을 선택합니다.

     일부 USB 드라이브에는 초기화할 수 있는 옵션이 없으며 포맷된 후 [드라이브 문자](change-a-drive-letter.md)가 지정됩니다.

    ![디스크 초기화 바로 가기 메뉴와 포맷되지 않은 디스크를 보여 주는 디스크 관리 기능](media/uninitialized-disk.PNG)
2. **디스크 초기화** 대화 상자(그림 참조)에서 올바른 디스크를 선택했는지 확인한 후 **확인**을 클릭하여 기본 파티션 스타일을 적용합니다. 파티션 스타일(MBR 또는 GPT)을 변경해야 할 경우 [파티션 스타일 정보 - GPT 및 MBR](#about-partition-styles---gpt-and-mbr)를 참조하세요.

     디스크 상태가 **초기화**에서 **온라인** 상태로 바로 변경됩니다. 어떤 이유로든 초기화가 실패하는 경우 [디스크의 상태가 초기화되지 않음 또는 디스크가 완전히 누락됨](troubleshooting-disk-management.md#disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps)을 참조하세요.

    ![GPT 파티션 스타일이 선택된 디스크 초기화 대화 상자](media/initialize-disk.PNG)

3. 드라이브에서 할당되지 않은 공간을 길게 누른(또는 마우스 오른쪽 단추로 클릭) 다음, **새 단순 볼륨**을 선택합니다.
4. **다음**을 선택하고, 볼륨 크기를 지정하고(전체 드라이브를 사용하는 기본값을 그대로 유지할 수 있음), **다음**을 선택합니다.
5. 볼륨에 할당하려는 드라이브 문자를 지정하고, **다음**을 선택합니다.
6. 사용하려는 파일 시스템(일반적으로 NTFS)을 지정하고, **다음**, **마침**을 차례로 선택합니다.

## <a name="about-partition-styles---gpt-and-mbr"></a>파티션 스타일 정보 - GPT 및 MBR

디스크는 파티션이라는 여러 청크로 나눌 수 있습니다. 파티션이 하나만 있는 경우를 비롯하여 각 파티션의 파티션 스타일은 GTP 또는 MBR이어야 합니다. Windows는 디스크의 데이터에 액세스하는 방법을 이해하기 위해 파티션 스타일을 사용합니다.

별로 흥미로운 내용은 아니지만 결론적으로 오늘날에는 일반적으로 파티션 스타일을 걱정할 필요가 없습니다. Windows에서 적절한 디스크 유형을 자동으로 사용하기 때문입니다.

대부분의 PC는 하드 드라이브 및 SSD에 대해 GPT(GUID 파티션 테이블) 디스크 유형을 사용합니다. GPT가 좀 더 강력하며 2TB보다 큰 볼륨을 허용합니다. 이전의 MBR(마스터 부트 레코드) 디스크 유형은 32비트 PC, 오래된 PC 및 메모리 카드와 같은 이동식 드라이브에서 사용됩니다.

디스크를 MBR에서 GPT로 또는 그 반대로 변환하려면 먼저 디스크에서 모든 볼륨을 삭제하고 디스크에 있는 모든 항목을 지워야 합니다. 자세한 내용은 [MBR 디스크를 GPT 디스크로 변환](change-an-mbr-disk-into-a-gpt-disk.md) 또는 [MBR 디스크를 GPT 디스크로 변환](change-a-gpt-disk-into-an-mbr-disk.md)을 참조하세요.