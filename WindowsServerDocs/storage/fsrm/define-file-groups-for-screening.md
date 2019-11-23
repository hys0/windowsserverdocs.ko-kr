---
title: 차단을 위한 파일 그룹 정의
description: 이 문서에서는 파일 차단에 대한 네임스페이스, 파일 차단 예외 또는 파일 그룹별 파일 저장소 보고서를 만드는 데 사용되는 파일 그룹을 정의하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b56d7b0439e3dc6f1a2e0a1c96f761dbb77cb0a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394391"
---
# <a name="define-file-groups-for-screening"></a>차단을 위한 파일 그룹 정의

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

*파일 그룹*은 파일 차단에 대한 네임스페이스, 파일 차단 예외 또는 **파일 그룹별 파일** 저장소 보고서를 정의하는 데 사용됩니다. 파일 그룹은 파일 이름 패턴의 집합으로 구성되며, 이는 다음 기준으로 그룹화됩니다.

-   **포함할 파일**: 그룹에 속하는 파일
-   **제외할 파일**: 그룹에 속하지 않는 파일

> [!Note]
> 편의를 위해, 파일 차단, 파일 차단 예외, 파일 차단 템플릿, **파일 그룹별 파일** 보고서의 속성을 편집하는 동안 파일 그룹을 만들고 편집할 수 있습니다. 이러한 속성 시트에서 수행하는 모든 파일 그룹 변경은 작업 중인 현재 항목에 제한되지 않습니다.

## <a name="to-create-a-file-group"></a>파일 그룹을 만들려면

1.  **파일 차단 관리**에서 **파일 그룹** 노드를 클릭합니다.

2.  **작업** 창에서 **파일 그룹 만들기**를 클릭합니다. 이렇게 하면 **파일 그룹 속성 만들기** 대화 상자가 열립니다.

    (또는 파일 차단, 파일 차단 예외, 파일 차단 템플릿 또는 **파일 그룹별 파일** 보고서의 속성을 편집하는 동안 **파일 그룹 유지**에서 **만들기**를 클릭합니다.)

3.  **파일 그룹 속성 만들기** 대화 상자에 파일 그룹의 이름을 입력합니다.

4.  포함 및 제외할 파일 추가:

    -   파일 그룹에 포함하려는 파일 집합의 경우 **포함할 파일** 상자에 파일 이름 패턴을 입력한 다음 **추가**를 클릭합니다.
    -   파일 그룹에서 제외하려는 파일 집합의 경우 **제외할 파일** 상자에 파일 이름 패턴을 입력한 다음 **추가**를 클릭합니다.
        표준 와일드 카드 규칙이 적용 됩니다. 예를 들어 **\*** 는 모든 실행 파일을 선택 합니다.

5.  **확인**을 클릭합니다.

## <a name="see-also"></a>참고 항목

-   [파일 차단 관리](file-screening-management.md)
-   [파일 화면 만들기](create-file-screen.md)
-   [파일 차단 예외 만들기](create-file-screen-exception.md)
-   [파일 차단 템플릿 만들기](create-file-screen-template.md)
-   [스토리지 보고서 관리](storage-reports-management.md)


