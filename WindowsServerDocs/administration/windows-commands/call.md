---
title: call
description: 부모 일괄 프로그램을 중지 하지 않고 다른 일괄 처리 프로그램을 호출 하는 call 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d34a41dc-e6c7-4467-bf6a-15cec704833e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/05/2018
ms.openlocfilehash: e73199b9d5633d5b3f1f7b8afd2bd35eb826bfd7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924832"
---
# <a name="call"></a>call

상위 일괄 프로그램을 중지 하지 않고 다른 하나의 일괄 처리 프로그램을 호출 합니다. **Call** 명령은 레이블을 호출 대상으로 허용 합니다.

> [!NOTE]
> 호출 아무런 효과도 명령 프롬프트에서 스크립트 또는 배치 파일 외부에서 사용 됩니다.

## <a name="syntax"></a>구문

```
call [drive:][path]<filename> [<batchparameters>] [:<label> [<arguments>]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `[<drive>:][<path>]<filename>` | 호출 하려는 일괄 프로그램의 이름과 위치를 지정 합니다. `<filename>`매개 변수는 필수 이며 .bat 또는 .cmd 확장명이 있어야 합니다. |
| `<batchparameters>` | 일괄 처리 프로그램에 필요한 명령줄 정보를 지정 합니다. |
| `:<label>` | 이동할 일괄 프로그램 제어를 원하는 레이블을 지정 합니다. |
| `<arguments>` | 에서 시작 하 여 일괄 처리 프로그램의 새 인스턴스로 전달 될 명령줄 정보를 지정 합니다 `:<label>` .|
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="batch-parameters"></a>일괄 처리 매개 변수

일괄 처리 스크립트 인수 참조 (**%0**, **%1**, ...)는 다음 표에 나열 됩니다.

일괄 처리 스크립트에서 **% &#42;** 값을 사용 하는 것은 모든 인수를 참조 합니다 (예: **%1**, **%2**, **%3**...).

일괄 처리 매개 변수에 대 한 다음과 같은 선택적 구문을 대신 사용할 수 있습니다 (**%n% n**):

| 일괄 매개 변수 | 설명 |
| --------------- | ----------- |
| % ~ 1 | **%1을 (를)** 확장 하 고 주변 따옴표를 제거 합니다. |
| % ~ f1 | 확장 **%1** 정규화 된 경로에 있습니다. |
| % ~ d 1 | 확장 **%1** 드라이브 문자로 합니다. |
| % ~ p1 | 확장 **%1** 만 경로에 있습니다. |
| % ~ n1 | 확장 **%1** 만 파일 이름으로 저장 합니다. |
| % ~ x1 | 확장 **%1** 파일 이름 확장명으로 합니다. |
| % ~ s1 | 확장 **%1** 짧은 이름만 포함 하는 정규화 된 경로입니다. |
| % ~ a1 | 확장 **%1** 파일 특성에 있습니다. |
| % ~ t1 | 확장 **%1** 파일의 시간과 날짜를 합니다. |
| % ~ z1 | 확장 **%1** 파일의 크기입니다. |
| % ~ $PATH: 1 | PATH 환경 변수에 나열 된 디렉터리를 검색 하 고 확장 **%1** 찾을 첫 번째 디렉터리의 정규화 된 이름에 있습니다. 환경 변수 이름이 정의 되지 않은 경우 파일은 검색에서 찾을 수 없습니다이 한정자는 빈 문자열로 확장 됩니다. |

다음 표에서 복합 결과 대 한 일괄 처리 매개 변수 한정자를 결합 하는 방법과 보여 줍니다.

| 일괄 매개 변수 한정자 | 설명 |
| ----------------------------- | ----------- |
| % ~ dp1 | 확장 **%1** 드라이브 문자와 경로를 합니다. |
| % ~ nx1 | 확장 **%1** 파일 이름과 확장명 전용입니다. |
| % ~ dp$ 경로: 1 | 에 대 한 PATH 환경 변수에 나열 되는 디렉터리 검색 **%1**, 을 드라이브 문자와 찾을 수 있는 첫 번째 디렉터리의 경로를 확장 하 여 합니다. |
| % ~ ftza1 | 확장 **%1** 유사한 출력을 표시 하는 **dir** 명령입니다. |

위의 예제에서 **%1** 경로 다른 유효한 값으로 대체 될 수 있습니다. **%~** 구문이 올바른 인수 번호로 종료 되었습니다. **%~** 한정자는 **% &#42;** 와 함께 사용할 수 없습니다.

### <a name="remarks"></a>설명

- 일괄 처리 매개 변수 사용:

    일괄 처리 매개 변수는 명령줄 옵션, 파일 이름, 일괄 처리 매개 변수 **%0** - **%9**및 변수 (예: **% 전송%**)를 포함 하 여 일괄 프로그램에 전달할 수 있는 모든 정보를 포함할 수 있습니다.

- `<label>`매개 변수 사용:

    매개 변수를 사용 하 여 **호출** `<label>` 을 사용 하면 새 일괄 처리 파일 컨텍스트를 만들고 지정 된 레이블 뒤에 있는 문에 제어를 전달 합니다. 배치 파일의 끝에 도달 하는 처음으로 (즉, 이동한 후 레이블에), 다음 문으로 제어가 반환는 **호출** 문입니다. 배치 파일의 끝에 도달 하는 두 번째 시간 배치 스크립트가 종료 됩니다.

- 파이프 및 리디렉션 기호 사용:

    `(|)`호출에는 파이프 또는 리디렉션 기호 ( `<` 또는 `>` )를 **call**사용 하지 마십시오.

- 재귀 호출 만들기

    자신을 호출 하는 일괄 처리 프로그램을 만들 수 있습니다. 그러나 종료 조건을 제공 해야 합니다. 그렇지 않으면 부모 및 자식 일괄 프로그램 끊임없이 루프 수 있습니다.

- 명령 확장 사용

    명령 확장을 사용 하는 **call** 경우 호출 `<label>` 의 대상으로를 호출 합니다. 올바른 구문은입니다.`call :<label> <arguments>`

## <a name="examples"></a>예

다른 batch 프로그램에서 checknew.bat 프로그램을 실행 하려면 부모 일괄 프로그램에서 다음 명령을 입력 합니다.

```
call checknew
```

부모 일괄 처리 프로그램에서 두 개의 일괄 처리 매개 변수를 허용 하 고 이러한 매개 변수를 checknew.bat에 전달 하려면 부모 배치 프로그램에서 다음 명령을 입력 합니다.

```
call checknew %1 %2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
