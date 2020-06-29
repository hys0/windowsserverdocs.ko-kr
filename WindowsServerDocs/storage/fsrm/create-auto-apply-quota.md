---
title: 할당량 자동 적용 만들기
description: 이 문서에서는 할당량 템플릿에 따라 할당량 자동 적용을 만드는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 38354a6c6e39f58574a64c752bb86800f3fc3039
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474070"
---
# <a name="create-an-auto-apply-quota"></a>할당량 자동 적용 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

할당량 자동 적용을 사용 하 여 할당량 템플릿을 부모 볼륨이 나 폴더에 할당할 수 있습니다. 그러면 파일 서버 리소스 관리자 해당 템플릿을 기반으로 하는 할당량을 자동으로 생성 합니다. 기존 하위 폴더와 나중에 만든 하위 폴더 각각에 대해 할당량이 생성 됩니다.

예를 들어 요청 시 생성 되는 하위 폴더, 로밍 프로필 사용자 또는 새 사용자에 대해 자동 적용 할당량을 정의할 수 있습니다. 하위 폴더가 생성 될 때마다 부모 폴더의 템플릿을 사용 하 여 새 할당량 항목이 자동으로 생성 됩니다. 이렇게 자동으로 생성 된 할당량 항목은 **할당량** 노드에서 개별 할당량으로 볼 수 있습니다. 각 할당량 항목은 별도로 유지 관리할 수 있습니다.

## <a name="to-create-an-auto-apply-quota"></a>할당량 자동 적용을 만들려면

1.  **할당량 관리**에서 **할당량** 노드를 클릭 합니다.

2.  **할당량**을 마우스 오른쪽 단추로 클릭 한 다음 **할당량 만들기** 를 클릭 하거나 **작업** 창에서 **할당량 만들기** 를 선택 합니다. 그러면 **할당량 만들기** 대화 상자가 열립니다.

3.  **할당량 경로**아래에서 할당량 프로필이 적용 될 부모 폴더의 이름을 입력 하거나 찾습니다. 자동 적용 할당량은이 폴더의 각 하위 폴더 (현재 및 미래)에 적용 됩니다.

4.  **템플릿 자동 적용을 클릭 하 고 기존 및 새 하위 폴더에 할당량 만들기**를 클릭 합니다.

5.  **이 할당량 템플릿에서 속성 파생**아래의 드롭다운 목록에서 적용 하려는 할당량 템플릿을 선택 합니다. 각 템플릿의 속성은 **할당량 속성 요약**아래에 표시 됩니다.

6.  **만들기**를 클릭합니다.

> [!Note]
> **할당량** 노드를 선택 하 고 **새로 고침**을 선택 하 여 자동으로 생성 된 모든 할당량을 확인할 수 있습니다. 부모 볼륨 또는 폴더의 각 하위 폴더와 할당량 자동 적용 프로필에 대 한 개별 할당량이 나열 됩니다.

## <a name="additional-references"></a>추가 참조

-   [할당량 관리](quota-management.md)
-   [할당량 자동 적용 속성 편집](edit-auto-apply-quota-properties.md)