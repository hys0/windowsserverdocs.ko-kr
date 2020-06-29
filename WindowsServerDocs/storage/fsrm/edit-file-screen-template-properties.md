---
title: 파일 차단 템플릿 속성 편집
description: 이 문서에서는 파일 화면 템플릿 속성을 편집 하는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: cb0ab9105aeded58b2ef3de9e5eb86fe823d6b5b
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473530"
---
# <a name="edit-file-screen-template-properties"></a>파일 차단 템플릿 속성 편집

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 화면 템플릿을 변경 하는 경우 원래 파일 화면 템플릿을 사용 하 여 만든 파일 화면으로 이러한 변경 내용을 확장 하는 옵션이 있습니다. 원본 템플릿이나 원래 템플릿에서 파생 된 모든 파일 화면과 일치 하는 파일 화면을 수정 하도록 선택할 수 있습니다. 파일 차단이 생성 된 이후 변경 된 내용에 관계 없이 원래 템플릿에서 파생 됩니다. 이 기능을 사용 하면 모든 변경을 수행 하는 하나의 중앙 지점을 제공 하 여 파일 화면의 속성을 업데이트 하는 프로세스를 간소화할 수 있습니다.

> [!Note]
> 원래 템플릿에서 파생 된 모든 파일 화면에 변경 내용을 적용 하는 경우에는 사용자가 만든 모든 사용자 지정 파일 화면 속성을 덮어씁니다.

## <a name="to-edit-file-screen-template-properties"></a>파일 화면 템플릿 속성을 편집 하려면

1.  **파일 화면 템플릿**에서 수정 하려는 템플릿을 선택 합니다.

2.  파일 화면 템플릿을 마우스 오른쪽 단추로 클릭 하 고 **템플릿 속성 편집** 을 클릭 하거나, **작업** 창의 **선택한 파일 화면 템플릿**에서 **템플릿 속성 편집**을 선택 합니다. 그러면 **파일 화면 템플릿 속성** 대화 상자가 열립니다.

3.  다른 템플릿의 속성을 수정 된 템플릿의 기반으로 복사 하려면 **템플릿에서 속성 복사** 드롭다운 목록에서 템플릿을 선택 합니다. 그런 다음 **복사**를 클릭 합니다.

4.  필요한 모든 변경을 수행 합니다. 설정 및 알림 옵션은 파일 화면 템플릿을 만들 때 사용할 수 있는 옵션과 동일 합니다.

5.  템플릿 속성 편집을 마쳤으면 **확인**을 클릭 합니다. 이렇게 하면 **템플릿에서 파생 된 파일 업데이트 화면** 대화 상자가 열립니다.

6.  적용할 업데이트 유형 선택:

    -   원본 템플릿을 사용 하 여 만든 후 수정 된 파일 화면이 있고 변경 하지 않으려는 경우 **원래 템플릿과 일치 하는 파생 된 파일 화면에만 템플릿 적용**을 클릭 합니다. 이 옵션은 원래 템플릿 속성을 사용 하 여 만들어진 이후 편집 되지 않은 파일 화면만 업데이트 합니다.
    -   원본 템플릿을 사용 하 여 만든 기존 파일 화면을 모두 수정 하려면 **모든 파생 파일 화면에 템플릿 적용**을 클릭 합니다.
    -   기존 파일 차단을 변경 되지 않은 상태로 유지 하려면 **파생 된 파일 화면에 템플릿 적용 안 함**을 클릭 합니다.

7.  **확인**을 클릭합니다.

## <a name="additional-references"></a>추가 참조

-   [파일 차단 관리](file-screening-management.md)
-   [파일 차단 템플릿 만들기](create-file-screen-template.md)


