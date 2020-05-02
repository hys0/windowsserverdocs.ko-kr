---
title: 라는 설치 관리자 실행 파일에 포함됩니다. 여기서
description: 지정 된 검색 패턴과 일치 하는 파일의 위치를 표시 하는에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0b3486a5-896b-4d92-84b8-e463a0b76487
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4cec462e0d3652a20abb6290cd20b1d9d88aab53
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725810"
---
# <a name="where"></a>라는 설치 관리자 실행 파일에 포함됩니다. 여기서



지정된 된 검색 패턴과 일치 하는 파일의 위치를 표시 합니다.



## <a name="syntax"></a>구문

```
where [/r <Dir>] [/q] [/f] [/t] [$<ENV>:|<Path>:]<Pattern>[ ...] 
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/r \<Dir>|지정된 된 디렉터리부터 재귀 검색을 나타냅니다.|
|/q|종료 코드 반환 (**0** 성공을 위한 **1** 실패에 대 한) 일치 하는 파일의 목록을 표시 하지 않고 있습니다.|
|/f|결과 표시는 **여기서** 인용 부호로 명령입니다.|
|/t|파일 크기 및 마지막으로 수정한 날짜와 일치 하는 각 파일의 시간을 표시 합니다.|
|[$\<ENV>:\|\<경로>:] \<패턴> [...]|검색 패턴 일치 하도록 파일을 지정 합니다. 하나 이상의 패턴이 필요 하며 패턴에 와일드 카드 문자 (**&#42;** 및 **?**)가 포함 될 수 있습니다. 기본적으로 **여기서** 현재 디렉터리와 PATH 환경 변수에 지정 된 경로 검색 합니다. 형식 $를 사용 하 여 검색 하려면 다른 경로 지정할 수 있습니다*ENV*:*패턴* (여기서 *ENV* 는 하나 이상의 경로 포함 하는 기존 환경 변수) 또는 형식을 사용 하 여 *경로*:*패턴* (여기서 *경로* 검색 하려는 디렉터리 경로). 이러한 선택적 형식으로 사용할 수 없습니다는 **/r** 명령줄 옵션입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   파일 이름 확장명을 지정 하지 않으면 기본적으로 PATHEXT 환경 변수에 나열 된 패턴에 추가 됩니다.
-   **여기서** 재귀 검색을 실행할 날짜 또는 크기와 같은 파일 정보를 표시 하 고 대신 로컬 컴퓨터에서 경로 환경 변수를 사용할 수 있습니다.

## <a name="examples"></a>예

현재 컴퓨터 및 해당 하위 디렉터리의 C 드라이브에 Test 라는 모든 파일을 찾으려면 다음을 입력 합니다.
```
where /r c:\ test 
```
공용 디렉터리의 모든 파일을 나열 하려면 다음을 입력 합니다.
```
where $public:*.*
```
모든 파일을 메모장에서 원격 컴퓨터, Computer1, 및 하위 디렉터리의 C 드라이브를 찾으려면 다음을 입력 합니다.
```
where /r \\computer1\c notepad.*
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)