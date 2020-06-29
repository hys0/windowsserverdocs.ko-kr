---
title: 분류 속성 만들기
description: 이 문서에서는 지정 된 폴더 또는 볼륨 내의 파일에 값을 할당 하는 데 사용 되는 분류 속성에 대해 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f8e0ba45883385a2b2bf161b04f99f8077fdef28
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473760"
---
# <a name="create-a-classification-property"></a>분류 속성 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

분류 속성은 지정 된 폴더 또는 볼륨 내의 파일에 값을 할당 하는 데 사용 됩니다. 요구 사항에 따라 선택할 수 있는 다양 한 속성 형식이 있습니다. 다음 표에서는 사용 가능한 속성 유형을 정의 합니다.

|속성 | 설명 |
| --- | --- |
| 예/아니요 | **예** 또는 **아니요**일 수 있는 부울 속성입니다. 분류 중에 또는 파일 콘텐츠에서 여러 값을 결합 하는 경우 **No** Value는 **예** 값으로 재정의 되지 않습니다. |
| 날짜-시간 | 간단한 날짜/시간 속성입니다. 분류 중 또는 파일 콘텐츠에서 여러 값을 결합 하는 경우 충돌 하는 값이 다시 분류 되지 않습니다. |
| Number | 간단한 숫자 속성입니다. 분류 중 또는 파일 콘텐츠에서 여러 값을 결합 하는 경우 충돌 하는 값이 다시 분류 되지 않습니다. |
| 정렬 된 목록 | 고정 값의 목록입니다. 한 번에 하나의 값만 속성에 할당 될 수 있습니다. 분류 중 또는 파일 콘텐츠에서 여러 값을 결합 하는 경우 목록에서 가장 높은 값이 사용 됩니다. |
| String | 단순 문자열 속성입니다. 분류 하는 동안 여러 값을 결합 하거나 파일 내용에서 충돌 하는 값을 결합 하는 경우 다시 분류 되지 않습니다. |
| 다중 선택 | 속성에 할당할 수 있는 값의 목록입니다. 한 번에 두 개 이상의 값을 속성에 할당할 수 있습니다. 분류 중 또는 파일 콘텐츠에서 여러 값을 결합 하는 경우 목록의 각 값이 사용 됩니다. |
| 다중 문자열 | 속성에 할당할 수 있는 문자열 목록입니다. 한 번에 두 개 이상의 값을 속성에 할당할 수 있습니다. 분류 중 또는 파일 콘텐츠에서 여러 값을 결합 하는 경우 목록의 각 값이 사용 됩니다. |

<br />

다음 절차에서는 분류 속성을 만드는 과정을 안내 합니다.

## <a name="to-create-a-classification-property"></a>분류 속성을 만들려면

1.  **분류 관리**에서 **분류 속성** 노드를 클릭 합니다.

2.  **분류 속성**을 마우스 오른쪽 단추로 클릭 한 다음 **속성 만들기** 를 클릭 하거나 **작업** 창에서 **속성 만들기** 를 클릭 합니다. 그러면 **분류 속성 정의** 대화 상자가 열립니다.

3.  **속성 이름** 입력란에 속성의 이름을 입력 합니다.

4.  **설명** 텍스트 상자에 속성에 대 한 설명 (선택 사항)을 추가 합니다.

5.  **속성 유형** 드롭다운 메뉴의 목록에서 속성 유형을 선택 합니다.

6.  **확인**을 클릭합니다.

## <a name="additional-references"></a>추가 참조

-   [자동 분류 규칙 만들기](create-automatic-classification-rule.md)
-   [분류 관리](classification-management.md)