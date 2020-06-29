---
title: 차단을 위한 파일 그룹 정의
description: 이 문서에서는 파일 그룹을 정의 하 여 파일 그룹에 대 한 네임 스페이스, 파일 화면 예외 또는 파일 그룹 저장소 보고서를 만드는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e38dee0381b33bb9d11b038de715a4420906e131
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474330"
---
# <a name="define-file-groups-for-screening"></a>차단을 위한 파일 그룹 정의

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 *그룹* 은 파일 그룹에 대 한 네임 스페이스를 정의 하는 데 사용 되는 파일 **그룹** 저장소 보고서를 파일 화면, 파일 화면 예외 또는 파일입니다. 다음으로 그룹화 되는 파일 이름 패턴 집합으로 구성 됩니다.

-   **포함할 파일**: 그룹에 속한 파일
-   **제외할 파일**: 그룹에 속하지 않은 파일

> [!Note]
> 편의를 위해 파일 **그룹 보고서에서** 파일 화면, 파일 화면 예외, 파일 화면 템플릿 및 파일의 속성을 편집 하는 동안 파일 그룹을 만들고 편집할 수 있습니다. 이러한 속성 시트에서 변경한 모든 파일 그룹은 작업 중인 현재 항목으로 제한 되지 않습니다.

## <a name="to-create-a-file-group"></a>파일 그룹을 만들려면

1.  **파일 차단 관리**에서 **파일 그룹** 노드를 클릭 합니다.

2.  **작업** 창에서 **파일 그룹 만들기**를 클릭 합니다. 그러면 **파일 그룹 만들기 속성** 대화 상자가 열립니다.

    또는 파일 그룹에 대 한 속성을 편집 하는 동안 파일 화면 예외, 파일 화면 템플릿 또는 파일 **그룹별 파일** 보고서를 편집 하는 동안 **파일 그룹 유지 관리**에서 **만들기**를 클릭 합니다.

3.  **파일 그룹 속성 만들기** 대화 상자에서 파일 그룹의 이름을 입력 합니다.

4.  포함할 파일 및 제외할 파일 추가:

    -   파일 그룹에 포함할 각 파일 집합에 대해 **포함할 파일** 상자에 파일 이름 패턴을 입력 한 다음 **추가**를 클릭 합니다.
    -   파일 그룹에서 제외 하려는 각 파일 집합에 대해 **제외할 파일** 상자에 파일 이름 패턴을 입력 한 다음 **추가**를 클릭 합니다.
        표준 와일드 카드 규칙이 적용 ** \* 됩니다.** 예를 들어 .exe는 모든 실행 파일을 선택 합니다.

5.  **확인**을 클릭합니다.

## <a name="additional-references"></a>추가 참조

-   [파일 차단 관리](file-screening-management.md)
-   [파일 화면 만들기](create-file-screen.md)
-   [파일 차단 예외 만들기](create-file-screen-exception.md)
-   [파일 차단 템플릿 만들기](create-file-screen-template.md)
-   [스토리지 보고서 관리](storage-reports-management.md)


