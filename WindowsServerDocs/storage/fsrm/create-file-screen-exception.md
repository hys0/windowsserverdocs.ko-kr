---
title: 파일 차단 예외 만들기
description: 이 문서에서는 파일 차단 예외를 만드는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c496151ed1f38cd1f2c604bd227627a586e582c6
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473700"
---
# <a name="create-a-file-screen-exception"></a>파일 차단 예외 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

경우에 따라 파일 차단에 대 한 예외를 허용 해야 합니다. 예를 들어 파일 서버에서 비디오 파일을 차단 하려고 하지만 학습 그룹에서 컴퓨터 기반 교육을 위한 비디오 파일을 저장 하도록 허용 해야 합니다. 다른 파일 차단이 차단 되는 파일을 허용 하려면 *파일 화면 예외*를 만듭니다.

파일 차단 예외는 지정 된 예외 경로에서 폴더 및 모든 하위 폴더에 적용 되는 모든 파일 차단을 탑승 하는 특수 한 형식의 파일 화면입니다. 즉, 부모 폴더에서 파생 된 규칙에 대 한 예외를 만듭니다.

> [!Note]
> 파일 화면이 이미 정의 되어 있는 부모 폴더에는 파일 차단 예외를 만들 수 없습니다. 하위 폴더에 예외를 할당 하거나 기존 파일 화면을 변경 해야 합니다.

<br />
파일 그룹을 할당 하 여 파일 화면 예외에 허용 되는 파일 형식을 결정 합니다.

## <a name="to-create-a-file-screen-exception"></a>파일 화면 예외를 만들려면

1.  **파일 차단 관리**에서 **파일 화면** 노드를 클릭 합니다.

2.  **파일 화면**을 마우스 오른쪽 단추로 클릭 하 고 **파일 화면 예외 만들기** 를 클릭 하거나 **작업** 창에서 **파일 화면 예외 만들기** 를 선택 합니다. 그러면 **파일 화면 예외 만들기** 대화 상자가 열립니다.

3.  **예외 경로** 텍스트 상자에 예외가 적용 될 경로를 입력 하거나 선택 합니다. 이 예외는 선택한 폴더와 모든 하위 폴더에 적용 됩니다.

4.  파일 차단에서 제외할 파일을 지정 하려면 다음을 수행 합니다.

    -   파일 **그룹**에서 파일 차단에서 제외 하려는 각 파일 그룹을 선택 합니다. (파일 그룹에 대 한 확인란을 선택 하려면 파일 그룹 레이블을 두 번 클릭 합니다.)
    -   파일 그룹이 포함 하 고 제외 하는 파일 형식을 확인 하려면 파일 그룹 레이블을 클릭 하 고 **편집**을 클릭 합니다.
    -   새 파일 그룹을 만들려면 **만들기**를 클릭 합니다.

5.  **확인**을 클릭합니다.

## <a name="additional-references"></a>추가 참조

-   [파일 차단 관리](file-screening-management.md)
-   [차단을 위한 파일 그룹 정의](define-file-groups-for-screening.md)


