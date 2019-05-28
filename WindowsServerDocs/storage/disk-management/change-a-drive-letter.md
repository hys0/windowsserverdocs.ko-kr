---
title: 드라이브 문자 변경
description: 변경 또는 디스크 관리를 사용 하 여 Windows에서 드라이브 문자를 할당 하는 방법.
ms.date: 10/24/2018
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 93da32a204c42b3f4fb503349ff732c9c050db31
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192632"
---
# <a name="change-a-drive-letter"></a>드라이브 문자 변경

> **적용 대상:** Windows 10, Windows 8.1, Windows 7, Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

드라이브에 할당 된 드라이브 문자 마음에 들지 않는 경우 드라이브 문자 아직 없는 드라이브 있다면 변경 하려면 디스크 관리를 사용할 수 있습니다.

> [!IMPORTANT]
> 응용 프로그램이 나 Windows가 설치 되어 있는 드라이브의 드라이브 문자를 변경 하는 경우 앱의 실행 하거나 해당 드라이브를 찾는 데 문제가 있을 수 있습니다. 이러한 이유로 Windows 또는 앱이 설치 된 드라이브의 드라이브 문자를 변경 하지 않는 것이 좋습니다.

드라이브 문자를 변경 하는 방법은 다음과 같습니다 (대신 빈에서 드라이브를 탑재 하도록 폴더 다른 폴더로 표시 되도록 참조 [드라이브에 탑재 지점 폴더 경로 지정할](assign-a-mount-point-folder-path-to-a-drive.md)).

1. 디스크 관리를 관리자 권한으로 엽니다. 
    이렇게 하려면 작업 표시줄에서 검색 상자에를 입력 **디스크 관리**, 선택 및 저장 (또는 마우스 오른쪽 단추로 클릭) **디스크 관리**을 선택한 후 **관리자 권한으로 실행**  >  **예**합니다. 열 수 없으면이 관리자로 서, 입력 **컴퓨터 관리** 대신으로 이동한 다음 **저장소** > **디스크 관리**합니다.
1. 디스크 관리에서 마우스 오른쪽 단추로 클릭 하거나 변경 하 고, 드라이브 문자를 추가 하 고, 다음을 선택 하려면 원하는 드라이브 **드라이브 문자 및 경로 변경**합니다.

    ![드라이브를 표시 하는 디스크 관리](media/change-drive-letter.png)
    > [!TIP]
    > 표시 되지 않는 경우는 **드라이브 문자 및 경로 변경** 옵션 또는 회색으로 가능한 볼륨에는 해당 되는 경우 드라이브 할당 되지 해야 하는 경우 드라이브 문자를 받을 준비가 되지 않았습니다. [를초기화합니다](initialize-new-disks.md). 또는 아마도 것은 아닙니다 액세스 하 여 EFI 시스템 파티션과 복구 파티션을의 경우. 액세스할 수 있는 드라이브 문자를 사용 하 여 서식이 지정 된 볼륨이 있는 여전히 변경할 수 없습니다를 확인 하는 경우 안타깝게도이 항목에서는 아마도 도와 드릴 수 없습니다, 것이 좋습니다 [Microsoft에 연락](https://support.microsoft.com/contactus/) 또는 제조업체에 PC에 대 한 자세한 도움말입니다.

1. 드라이브 문자를 변경 하려면 **변경**합니다. 드라이브 문자로 드라이브 아직 없을 경우 하나를 선택 추가할 **추가**합니다.

    ![드라이브 문자 및 경로 변경 대화 상자](media/change-drive-letter2.png)
1. 새 드라이브 문자를 선택 **확인**를 선택한 후 **예** 드라이브 문자를 사용 하는 프로그램이 제대로 실행 되지 않을 수 있습니다 하는 방법에 대 한 메시지가 표시 되 면 합니다.

    ![드라이브 문자를 변경 하는 변경 드라이브 문자 또는 경로 대화 상자 표시](media/change-drive-letter3.png)