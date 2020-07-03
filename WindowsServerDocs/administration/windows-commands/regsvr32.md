---
title: regsvr32
description: 레지스트리에 명령 구성 요소로 .dll 파일을 등록 하는 regsvr32 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7a1a9247b66e5eb1a23c1f5ef33fbcb98c53bd7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930971"
---
# <a name="regsvr32"></a>regsvr32

레지스트리에 명령 구성 요소로.dll 파일을 등록합니다.

## <a name="syntax"></a>구문

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <Dllname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| /U | 서버 등록 취소합니다. |
| /s | 메시지 표시를 방지 합니다. |
| /n | **DllRegisterServer**를 호출할 수 없습니다. 이 매개 변수를 사용 하려면 **/i** 매개 변수도 사용 해야 합니다. |
| /i`<cmdline>` | 선택적 명령줄 문자열을 전달 (*명령줄*)를 **DllInstall**합니다. 이 매개 변수를 **/u** 매개 변수와 함께 사용 하면 **DllUninstall**이 호출 됩니다. |
| `<Dllname>` | 가 등록 하는.dll 파일의 이름입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

.Dll Active Directory 스키마를 등록 하려면 다음을 입력 합니다.

```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
