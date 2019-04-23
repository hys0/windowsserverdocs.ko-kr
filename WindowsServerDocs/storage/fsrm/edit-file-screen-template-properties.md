---
title: 파일 차단 템플릿 속성 편집
description: 이 문서에서는 파일 차단 템플릿 속성을 편집하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 31ca46707a32d23a5dd9606c57bcaec5d6e53a80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846894"
---
# <a name="edit-file-screen-template-properties"></a>파일 차단 템플릿 속성 편집

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 차단 템플릿을 변경할 경우, 해당 변경 사항을 원본 파일 차단 템플릿으로 생성된 파일 차단으로 확장할 수 있는 옵션을 가지게 됩니다. 원래 템플릿과 일치하는 파일 차단만 수정하거나, 파일 차단이 생성된 후의 모든 수정에 관계없이 원본 템플릿에서 파생된 모든 파일 차단을 수정하도록 선택할 수 있습니다. 이 기능은 모든 변경 사항을 적용할 수 있는 하나의 중앙 지점을 제공하여 파일 차단의 속성을 업데이트하는 과정을 간소화합니다.

> [!Note]
> 원본 템플릿에서 파생된 모든 파일 차단에 변경 내용을 적용하면 사용자가 만든 사용자 지정 파일 차단 속성을 덮어씁니다.

## <a name="to-edit-file-screen-template-properties"></a>파일 차단 템플릿 속성을 편집하려면

1.  **파일 차단 템플릿**에서 수정할 템플릿을 선택합니다.

2.  파일 화면 템플릿을 마우스 오른쪽 단추로 클릭 하 고 클릭 **템플릿 속성 편집** (또는 합니다 **동작** 창 아래에 있는 **파일 화면 템플릿 선택**선택,  **템플릿 속성 편집**.) 열립니다는 **파일 화면 템플릿 속성** 대화 상자.

3.  다른 템플릿의 속성을 복사하여 수정된 템플릿의 기반으로 사용하려면 **템플릿에서 속성 복사** 드롭다운 목록에서 템플릿을 선택합니다. 그런 다음 **복사**를 클릭합니다.

4.  필요한 모든 내용을 변경합니다. 설정 및 알림 옵션은 파일 차단 템플릿을 만들 때 사용 가능한 것과 동일합니다.

5.  템플릿 속성 편집을 마쳤으면 **확인**을 클릭합니다. 이렇게 하면 **템플릿에서 파생된 파일 차단 업데이트** 대화 상자가 열립니다.

6.  적용할 업데이트 유형을 선택합니다.

    -   원본 템플릿을 사용하여 생성된 후 수정된 파일 차단이 있고 이를 변경하고 싶지 않다면 **원본 템플릿과 일치하는 파생된 파일 차단에만 템플릿 적용**을 클릭합니다. 이 옵션은 원본 템플릿 속성으로 생성된 후 편집되지 않은 파일 차단만 업데이트합니다.
    -   원본 템플릿을 사용하여 생성된 모든 기존 파일 차단을 수정하려면 **파생된 모든 파일 차단에 템플릿 적용**을 클릭합니다.
    -   기존 파일 차단을 변경하지 않고 유지하려면 **파생된 파일 차단에 템플릿 적용 안 함**을 클릭합니다.

7.  **확인**을 클릭합니다.

## <a name="see-also"></a>참조

-   [파일 차단 관리](file-screening-management.md)
-   [파일 화면 템플릿 만들기](create-file-screen-template.md)


