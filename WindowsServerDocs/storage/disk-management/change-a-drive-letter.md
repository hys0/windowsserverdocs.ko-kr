---
title: 드라이브 문자 변경
description: 디스크 관리를 사용하여 Windows에서 드라이브 문자를 변경하거나 할당하는 방법.
ms.date: 06/08/2020
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 424fa2c81954e022d7e1b297a60bd3415fdafa39
ms.sourcegitcommit: a538474d2c0a9520567f4e6ad0933f8660273098
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84505775"
---
# <a name="change-a-drive-letter"></a>드라이브 문자 변경

> **적용 대상:** Windows 10, Windows 8.1, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

드라이브에 할당된 드라이브 문자가 마음에 들지 않거나 아직 드라이브 문자가 없는 드라이브가 있으면 디스크 관리를 사용하여 변경할 수 있습니다. 대신 빈 폴더에 드라이브를 탑재하여 다른 폴더로 표시되도록 하려면 [폴더에 드라이브 탑재](assign-a-mount-point-folder-path-to-a-drive.md)를 참조하세요.

> [!IMPORTANT]
> Windows 또는 앱이 설치된 드라이브의 드라이브 문자를 변경하면 앱에서 해당 드라이브를 실행하거나 찾는 데 문제가 있을 수 있습니다. 이러한 이유로 Windows 또는 앱이 설치된 드라이브의 드라이브 문자는 변경하지 않는 것이 좋습니다.

드라이브 문자를 변경하는 방법은 다음과 같습니다.

1. 디스크 관리를 관리자 권한으로 엽니다.
    그러려면 시작 단추를 길게 누르거나 마우스 오른쪽 단추로 클릭한 다음, **디스크 관리**를 선택합니다.
1. 디스크 관리에서 드라이브 문자를 변경하거나 추가할 볼륨을 길게 누르거나 마우스 오른쪽 단추로 클릭한 다음, **드라이브 문자 및 경로 변경**을 선택합니다.

    ![드라이브를 표시하는 디스크 관리](media/change-drive-letter.png)
    > [!TIP]
    > **드라이브 문자 및 경로 변경** 옵션이 표시되지 않거나 회색으로 표시되면 볼륨이 드라이브 문자를 수신할 준비가 되지 않았을 수 있으며, 이 경우 드라이브가 할당되지 않은 상태여서 [초기화](initialize-new-disks.md)가 필요할 수 있습니다. 또는 EFI 시스템 파티션 및 복구 파티션의 경우 액세스하려는 것이 아닐 수도 있습니다. 액세스할 수 있는 드라이브 문자가 있는 포맷된 볼륨이 있지만 여전히 변경할 수 없는 경우에는, 안타깝게도 이 항목이 도움이 되지 않을 수 있습니다. 따라서 [Microsoft에 문의](https://support.microsoft.com/contactus/)하거나 PC 제조업체에 문의하시는 것이 좋습니다.

1. 드라이브 문자를 변경하려면 **변경**을 선택합니다. 드라이브 문자가 아직 없을 경우 하나 추가하려면 **추가**를 선택합니다.

    ![드라이브 문자 및 경로 변경 대화 상자](media/change-drive-letter2.png)
1. 새 드라이브 문자를 선택하고 **확인**을 선택한 다음, 드라이브 문자를 사용하는 프로그램이 제대로 실행되지 않을 수 있다는 메시지가 표시되면 **예**를 선택합니다.

    ![드라이브 문자 변경을 보여주는 드라이브 문자 및 경로 변경 대화 상자](media/change-drive-letter3.png)
