---
title: 사용자 지정 파일 관리 작업 만들기
description: 이 문서에서는 사용자 지정 파일 관리 작업 및 사용자 지정 작업을 만드는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: bf1329c47fd5746bf0777415331ebcd7b882c5f1
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475580"
---
# <a name="create-a-custom-file-management-task"></a>사용자 지정 파일 관리 작업 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

만료는 항상 파일에 대해 수행 되는 작업은 아닙니다. 또한 파일 관리 작업을 사용 하 여 사용자 지정 명령을 실행할 수 있습니다.

> [!Note]
> 이 절차에서는 사용자가 파일 관리 작업에 대해 잘 알고 있다고 가정 하므로 사용자 지정 설정이 구성 된 **작업** 탭만 다룹니다.

## <a name="to-create-a-custom-task"></a>사용자 지정 태스크를 만들려면

1.  **파일 관리 작업** 노드를 클릭합니다.

2.  **파일 관리 작업**을 마우스 오른쪽 단추로 클릭 한 다음 **파일 관리 작업 만들기** 를 클릭 하거나 **작업** 창에서 **파일 관리 작업 만들기** 를 클릭 합니다. **파일 관리 작업 만들기** 대화 상자가 열립니다.

3.  **동작** 탭에서 다음 정보를 입력합니다.

    -   **유형** - 드롭다운 메뉴에서 **사용자 지정** 을 선택 합니다.
    -   **실행 파일**. 파일 관리 작업에서 파일을 처리할 때 실행할 명령을 입력 하거나 찾습니다. 이 실행 파일은 관리자 및 시스템 에서만 쓸 수 있도록 설정 해야 합니다. 다른 사용자에 게 실행 파일에 대 한 쓰기 권한이 있는 경우 올바르게 실행 되지 않습니다.
    -   **명령 설정**. 파일 관리 작업에서 파일을 처리할 때 실행 파일에 전달 되는 인수를 구성 하려면 **인수**라는 텍스트 상자를 편집 합니다. 텍스트에 추가 변수를 삽입 하려면 변수를 삽입 하려는 텍스트 상자의 위치에 커서를 놓고 삽입할 변수를 선택한 다음 **변수 삽입**을 클릭 합니다. 대괄호 안에 있는 텍스트는 실행 파일이 받을 수 있는 변수 정보를 삽입 합니다. 예를 들어 \[ 원본 파일 경로 \] 변수는 실행 파일에서 처리 해야 하는 파일의 이름을 삽입 합니다. 필요에 따라 **작업 디렉터리** 단추를 클릭 하 여 사용자 지정 실행 파일의 위치를 지정 합니다.
    -   **명령 보안**. 이 실행 파일에 대 한 보안 설정을 구성 합니다. 기본적으로 명령은 사용 가능한 가장 제한적인 계정인 로컬 서비스로 실행 됩니다.

4.  **확인**을 클릭합니다.

## <a name="additional-references"></a>추가 참조

-   [분류 관리](classification-management.md)
-   [파일 관리 작업](file-management-tasks.md)