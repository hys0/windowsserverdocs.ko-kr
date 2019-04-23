---
title: 사용자 지정 파일 관리 작업 만들기
description: 이 문서에서는 사용자 지정 파일 관리 작업과 사용자 지정 작업을 만드는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: dd52a94657fb73d28b3bc1552a058b7f3ca954ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867264"
---
# <a name="create-a-custom-file-management-task"></a>사용자 지정 파일 관리 작업 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

만료는 항상 파일에서 수행되어야 하는 작업은 아닐 수 있습니다. 파일 관리 작업을 사용하면 사용자 지정 명령을 실행할 수 있습니다.

> [!Note]
> 이 절차는 사용자가 파일 관리 작업에 익숙하다고 가정하므로, 사용자 지정 설정이 구성되는 **작업** 탭만 다룹니다.

## <a name="to-create-a-custom-task"></a>사용자 지정 작업을 만들려면

1.  **파일 관리 작업** 노드를 클릭합니다.

2.  마우스 오른쪽 단추로 **파일 관리 작업**을 클릭한 다음 **파일 관리 작업 만들기**를 클릭하거나 **작업** 창에서 **파일 관리 작업 만들기**를 선택합니다. **파일 관리 작업 만들기** 대화 상자가 열립니다.

3.  **동작** 탭에서 다음 정보를 입력합니다.

    -   **유형** - 드롭다운 메뉴에서 **사용자 지정**을 선택합니다.
    -   **실행 파일**. 파일 관리 작업이 파일을 처리할 때 실행할 명령을 입력하거나 찾습니다. 이 실행 파일은 관리자와 시스템만 쓸 수 있도록 설정되어야 합니다. 다른 사용자가 실행 파일에 대한 쓰기 액세스 권한을 가질 경우, 제대로 실행되지 않습니다.
    -   **명령 설정**. 파일 관리 작업에서 파일을 처리할 때 실행 파일에 전달되는 인수를 구성하려면 **인수**라는 레이블이 지정된 입력란을 편집합니다. 텍스트에 추가 변수를 삽입하려면, 변수를 삽입할 텍스트 상자의 위치에 커서를 올리고, 삽입하려는 변수를 선택하고, **변수 삽입**을 클릭합니다. 괄호에 있는 텍스트는 실행 파일이 받을 수 있는 변수 정보를 삽입합니다. 예를 들어 합니다 \[원본 파일 경로\] 변수 실행 파일에 의해 처리 되어야 하는 파일의 이름을 삽입 합니다. 선택적으로, **작업 디렉터리** 단추를 클릭하여 사용자 지정 실행 파일의 위치를 지정할 수 있습니다.
    -   **명령 보안**. 이 실행 파일에 대한 보안 설정을 구성합니다. 기본적으로 명령은 사용할 수 있는 가장 제한적인 계정인 로컬 서비스로 실행됩니다.

4.  **확인**을 클릭합니다.

## <a name="see-also"></a>참조

-   [분류 관리](classification-management.md)
-   [파일 관리 작업](file-management-tasks.md)