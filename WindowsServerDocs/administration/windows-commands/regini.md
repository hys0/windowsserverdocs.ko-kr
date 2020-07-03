---
title: regini
description: 명령줄 또는 스크립트에서 레지스트리를 수정 하 고 하나 이상의 텍스트 파일에서 사전 설정 된 변경 내용을 적용 하는 regini.exe 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5ff18dc3-5bd8-400a-b311-fd73a3267e8c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 56e2d4505db56248b6e4ce9c11caaae1df9a4f08
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931009"
---
# <a name="regini"></a>regini

명령줄 또는 스크립트를에서 레지스트리를 수정 하 고 하나 이상의 텍스트 파일에 미리 설정 된 변경 내용을 적용 합니다. 만들 지정, 수정 또는 레지스트리 키에 대 한 권한을 수정 하는 것 외에도 레지스트리 키를 삭제 합니다.

regini.exe에서 레지스트리를 변경 하는 데 사용 하는 텍스트 스크립트 파일의 형식 및 내용에 대 한 자세한 내용은 [명령줄 또는 스크립트에서 레지스트리 값 또는 사용 권한을 변경 하는 방법](https://support.microsoft.com/help/264584/how-to-change-registry-values-or-permissions-from-a-command-line-or-a)을 참조 하세요.

## <a name="syntax"></a>구문

```
regini [-m \\machinename | -h hivefile hiveroot][-i n] [-o outputwidth][-b] textfiles...
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| -m`<\\computername>` | 레지스트리를 수정할 수 있는 원격 컴퓨터 이름을 지정 합니다. ** \\ ComputerName**형식을 사용 합니다. |
| -h`<hivefile hiveroot>` | 수정 하려면 로컬 레지스트리 하이브를 지정 합니다. 형식에서 하이브 파일의 이름 및 루트 하이브를 지정 해야 **hivefile hiveroot**합니다. |
| -i`<n>` | 명령 출력에서 레지스트리 키의 트리 구조를 나타내기 위해 사용 하는 들여쓰기 수준을 지정 합니다. 레지스트리 키의 현재 권한을 이진 형식으로 가져오는 **regdmp.exe** 도구는 들여쓰기를 4의 배수로 사용 하므로 기본값은 **4**입니다. |
| -o`<outputwidth>` | 문자에서 명령 출력의 너비를 지정합니다. 출력 명령 창에 표시 하려면, 기본값은 창의 너비입니다. 기본값은 파일에 출력 하는 경우 **240** 문자입니다. |
| -b | **regini.exe** 출력이 이전 버전의 **regini.exe**와 이전 버전과 호환 되도록 지정 합니다. |
| textfiles | 레지스트리 데이터를 포함 하는 하나 이상의 텍스트 파일의 이름을 지정 합니다. ANSI 또는 유니코드 텍스트 파일을 나열할 수 있습니다. |

#### <a name="remarks"></a>설명

다음 지침은 **regini.exe**를 사용 하 여 적용 하는 레지스트리 데이터를 포함 하는 텍스트 파일의 내용에 주로 적용 됩니다.

- 줄 끝 주석 문자로 세미콜론을 사용 합니다. 행의 첫 번째 공백이 아닌 문자 여야 합니다.

- 백슬래시를 사용 하 여 줄의 연속 작업을 나타냅니다. 이 명령은 백슬래시 최대 (제외)에서 모든 문자를 무시 합니다 다음 줄의 첫 번째 공백이 아닌 문자. 백슬래시 앞에 둘 이상의 공백을 포함 하는 경우 단일 공백으로 바뀝니다.

- 하드 탭 문자를 사용 하 여 들여쓰기를 제어 합니다. 이 들여쓰기는 레지스트리 키의 트리 구조를 나타냅니다. 그러나 이러한 문자는 해당 위치에 관계 없이 단일 공간으로 변환 됩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
