---
title: 파일 차단 예외 만들기
description: 이 문서에서는 파일 차단 예외를 만드는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 1f0e93cb2535862b9259d438de00c3b769c2282c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866304"
---
# <a name="create-a-file-screen-exception"></a>파일 차단 예외 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

경우에 따라 파일 차단에 예외를 허용해야 할 수 있습니다. 예를 들어, 파일 서버에서 비디오 파일을 차단하려고 하지만 교육 그룹이 컴퓨터 기반 교육을 위한 비디오 파일을 저장하도록 허용해야 할 수 있습니다. 다른 파일 차단을 통해 차단되는 파일을 허용하려면 *파일 차단 예외*를 만듭니다.

파일 차단 예외는 모든 파일 차단을 재정의하는 특별한 유형의 파일 차단으로, 지정된 예외 경로의 폴더와 모든 하위 폴더에 적용됩니다. 즉, 상위 폴더에서 파생된 모든 규칙에 대한 예외를 만듭니다.

> [!Note]
> 파일 차단이 이미 정의된 부모 폴더에는 파일 차단 예외를 만들 수 없습니다. 하위 폴더에 예외를 할당하거나 기존 파일 차단을 변경해야 합니다.

<br />
어떤 파일 형식이 파일 차단 예외에서 허용되는지 판단하는 파일 그룹을 할당합니다.

## <a name="to-create-a-file-screen-exception"></a>파일 차단 예외를 만들려면

1.  **파일 차단 관리**에서 **파일 차단** 노드를 클릭합니다.

2.  **파일 차단**을 마우스 오른쪽 단추로 클릭하고 **파일 차단 예외 만들기**를 클릭하거나 **작업** 창에서 **파일 차단 예외 만들기**를 선택합니다. 이렇게 하면 **파일 차단 예외 만들기** 대화 상자가 열립니다.

3.  **예외 경로** 입력란에 예외가 적용될 경로를 입력하거나 선택합니다. 예외는 선택한 폴더와 모든 하위 폴더에 적용됩니다.

4.  파일 차단에서 제외할 파일을 지정하려면:

    -   **파일 그룹**에서 파일 차단에서 제외할 각 파일 그룹을 선택합니다. (파일 그룹에 대한 확인란을 선택하려면 파일 그룹 레이블을 두 번 클릭합니다.)
    -   파일 그룹 포함 및 제외 되는 파일 형식 파일 그룹 레이블을 클릭 하 고 클릭 하려는 경우 **편집**합니다.
    -   새 파일 그룹을 만들려면 **만들기**를 클릭합니다.

5.  **확인**을 클릭합니다.

## <a name="see-also"></a>참조

-   [파일 차단 관리](file-screening-management.md)
-   [차단에 대 한 파일 그룹을 정의 합니다.](define-file-groups-for-screening.md)


