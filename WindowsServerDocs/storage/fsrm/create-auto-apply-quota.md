---
title: 할당량 자동 적용 만들기
description: 이 문서에서는 할당량 템플릿을 기반으로 할당량 자동 적용을 만드는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 68967ff920f25c05affc206ed45bad9275e781b6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394242"
---
# <a name="create-an-auto-apply-quota"></a>할당량 자동 적용 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

할당량 자동 적용을 사용하면 상위 볼륨 또는 폴더에 할당량 템플릿을 할당할 수 있습니다. 그런 다음 파일 서버 리소스 관리자가 템플릿을 기반으로 한 할당량을 자동으로 생성합니다. 할당량은 기존 하위 폴더와 앞으로 만들 하위 폴더에 대해 생성됩니다.

예를 들어 요청 시 생성되는 하위 폴더, 로밍 프로필 사용자 또는 새 사용자에 대한 하위 폴더를 위한 할당량 자동 적용을 정의할 수 있습니다. 하위 폴더를 만들 때마다 상위 폴더의 템플릿을 사용하여 새 할당량 항목이 자동으로 생성됩니다. 자동으로 생성된 이러한 할당량 항목은 **할당량** 노드의 개별 할당량으로 볼 수 있습니다. 각 할당량 항목은 별도로 유지 관리할 수 있습니다.

## <a name="to-create-an-auto-apply-quota"></a>할당량 자동 적용을 만들려면

1.  **할당량 관리**에서 **할당량** 노드를 클릭합니다.

2.  **할당량**을 마우스 오른쪽 단추로 클릭하고 **할당량 만들기**를 클릭하거나 **작업** 창에서 **할당량 만들기**를 선택합니다. 이렇게 하면 **할당량 만들기** 대화 상자가 열립니다.

3.  **할당량 경로** 아래에 이름을 입력하거나 할당량 프로필이 적용될 상위 폴더를 찾습니다. 할당량 자동 적용이 이 폴더의 각 하위 폴더(현재 및 이후)에 적용됩니다.

4.  **자동 적용 템플릿을 적용하고 기존 및 새 하위 폴더에 할당량 만들기**를 클릭합니다.

5.  **다음 할당량 템플릿에서 속성 파생**에서 적용하려는 할당량 템플릿을 드롭다운 목록에서 선택합니다. 각 템플릿의 속성은 **할당량 속성 요약** 아래 표시됩니다.

6.  **만들기**를 클릭합니다.

> [!Note]
> **할당량** 노드를 선택한 다음 **새로 고침**을 선택하여 자동으로 생성된 모든 할당량을 확인할 수 있습니다. 각 하위 폴더에 대한 개별 할당량과 상위 볼륨 및 폴더의 할당량 자동 적용 프로필이 나열됩니다.

## <a name="see-also"></a>참조

-   [할당량 관리](quota-management.md)
-   [할당량 자동 적용 속성 편집](edit-auto-apply-quota-properties.md)