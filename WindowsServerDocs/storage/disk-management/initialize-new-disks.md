---
title: 새 디스크 초기화
description: 디스크 관리를 사용 하도록 준비 하는 새 디스크를 초기화 하는 방법입니다. 또한 문제를 해결 하는 링크를 포함 합니다.
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7a275c372e1486b26821f797a7663eecbc3e8784
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812431"
---
# <a name="initialize-new-disks"></a>새 디스크 초기화

> **적용 대상:** Windows 10, Windows 8.1, Windows 7, Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용자 PC에 새 디스크를 추가 하 고 파일 탐색기에 표시 되지 않지만, 해야 [드라이브 문자를 추가](change-a-drive-letter.md), 또는 사용 하기 전에 초기화 합니다. 아직 포맷 된 드라이브를 초기화할 수 있습니다. 디스크 초기화를 모두 지웁니다 및 지나면 서식을 지정 하 고 파일을 저장할 수 있습니다 Windows 사용 하도록 준비 합니다.

> [!WARNING]
> 디스크에 이미 파일에서 관심 있는 경우 초기화 하지-모든 파일을 잃게 됩니다. 디스크 문제 해결 권장 대신 파일-을 읽을 수 있으면 참조 [디스크의 상태가 초기화 되지 않았습니다 또는 디스크가 누락 되었는지 완전히](troubleshooting-disk-management.md#a-disks-status-is-not-initialized-or-the-disk-is-missing)합니다.

## <a name="to-initialize-new-disks"></a>새 디스크 초기화

디스크 관리를 사용 하 여 새 디스크를 초기화 하는 방법을 다음과 같습니다. PowerShell을 사용 하 여 원할 경우 사용 합니다 [디스크 초기화](https://docs.microsoft.com/powershell/module/storage/initialize-disk) cmdlet 대신 합니다.

1. 디스크 관리를 관리자 권한으로 엽니다. 
 
    이렇게 하려면 작업 표시줄에서 검색 상자에를 입력 **디스크 관리**, 선택 및 저장 (또는 마우스 오른쪽 단추로 클릭) **디스크 관리**을 선택한 후 **관리자 권한으로 실행**  >  **예**합니다. 열 수 없으면이 관리자로 서, 입력 **컴퓨터 관리** 대신으로 이동한 다음 **저장소** > **디스크 관리**합니다.
1. 디스크 관리에서 초기화 하 고 클릭 하려는 디스크를 마우스 오른쪽 단추로 **디스크 초기화** (그림 참조). 으로 표시 되는 디스크 *오프 라인*, 먼저이 마우스 오른쪽 단추로 **Online**합니다.

     일부 USB 드라이브를 초기화할 수 없는 이므로 이러한 방금 서식이 설정으로 [드라이브 문자](change-a-drive-letter.md)합니다.

    ![표시 되는 디스크 초기화 바로 가기 메뉴를 사용 하 여 형식이 지정 되지 않은 디스크를 표시 하는 디스크 관리](media/uninitialized-disk.PNG)
2. 에 **디스크 초기화** (그림 참조) 대화 상자에서 올바른 디스크 선택 되어 있는지 확인 한 다음 클릭 확인 **확인** 기본 파티션 스타일을 적용할 합니다. 파티션 스타일 (MBR 또는 GPT) 참조를 변경 해야 할 경우 [GPT 및 MBR 파티션 스타일-에 대 한](#about-partition-styles---gpt-and-mbr)합니다.

     디스크 상태를 간단 하 게 변경 **Initializing** 하 고는 **Online** 상태입니다. 어떤 이유로 실패를 초기화 하는 경우 참조 [디스크의 상태가 초기화 되지 않았습니다 또는 디스크가 누락 되었는지 완전히](troubleshooting-disk-management.md#a-disks-status-is-not-initialized-or-the-disk-is-missing)합니다.

    ![선택한 GPT 파티션 스타일을 사용 하 여 디스크 초기화 대화 상자](media/initialize-disk.PNG)

## <a name="about-partition-styles---gpt-and-mbr"></a>GPT 및 MBR 파티션 스타일-정보

디스크는 파티션 이라는 여러 청크로 나눌 수 있습니다. 각 파티션은-하나만-있는 경우에 파티션 스타일이-MBR 또는 GPT를 갖습니다. Windows는 디스크의 데이터에 액세스 하는 방법을 이해 하려면 파티션 스타일을 사용 합니다.

아마도 이것이 대로으로 썼으며, 결론은이 오늘날 일반적으로 파티션 스타일에 걱정할 필요가-Windows에 자동으로 적절 한 디스크 유형을 사용 하는 합니다.

대부분의 Pc 하드 드라이브와 Ssd에 대 한 GUID 파티션 테이블 (GPT) 디스크 유형을 사용합니다. GPT 더 강력한 이며 2TB 보다 큰 볼륨에 대 한 허용 합니다. 이전 마스터 부트 레코드 (MBR) 디스크 형식의 32 비트 Pc, 오래 된 Pc 및 메모리 카드와 같은 이동식 드라이브에서 사용 됩니다.

디스크를 MBR GPT로 또는 그 반대로 변환할 먼저 경우 디스크에서 모든 볼륨을 삭제 하려면 디스크에 있는 모든 항목 지우기 자세한 내용은 참조 하세요. [MBR 디스크를 GPT 디스크로 변환](change-an-mbr-disk-into-a-gpt-disk.md), 또는 [MBR 디스크를 GPT 디스크로 변환](change-a-gpt-disk-into-an-mbr-disk.md)합니다.