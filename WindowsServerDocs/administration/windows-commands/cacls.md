---
title: cacls
description: Cacls 명령에 대 한 참조 문서입니다. 이 명령은 더 이상 사용 되지 않으며 이후 버전의 Windows에서는 지원 되지 않습니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7719728f2c1cb7ce629e199a51ee211ea5781401
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924846"
---
# <a name="cacls"></a>cacls

>[!IMPORTANT]
> 이 명령은 더 이상 사용 되지 않습니다. [Icacls](icacls.md) 를 대신 사용 하세요.

표시 하거나 지정 된 파일에 대해 임의 액세스 제어 목록 (DACL)을 수정 합니다.

## <a name="syntax"></a>구문

```
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<filename>` | 필수 요소. 지정 된 파일의 Acl을 표시합니다. |
| /t | 현재 디렉터리와 모든 하위 디렉터리에서 지정 된 파일의 Acl을 변경합니다. |
| /m | 볼륨의 Acl 디렉터리에 탑재 합니다. |
| /l | 는 대상 대신 기호화 된 링크 자체에서 작동 합니다. |
| /s:sddl | Acl을 SDDL 문자열에 지정 된 Acl로 바꿉니다. 이 매개 변수는 **/e**, **/g**, **/r**, **/p**또는 **/d** 매개 변수와 함께 사용할 수 없습니다. |
| /e | ACL을 바꾸지 않고 편집 합니다. |
| /C | 액세스 거부 오류가 발생 한 후 계속 합니다. |
| `/g user:<perm>` | 사용 권한에 대 한 유효한 값을 포함 하 여 지정 된 사용자 액세스 권한을 부여 합니다.<ul><li>**n** -없음</li><li>**r** -읽기</li><li>**w** -쓰기</li><li>**c** -변경 (쓰기)</li><li>**f** -모든 권한</li></ul> |
| /r 사용자 [...] | 지정 된 사용자의 액세스 권한을 취소 합니다. **/E** 매개 변수와 함께 사용할 경우에만 유효 합니다. |
| `[/p user:<perm> [...]` | 사용 권한에 대 한 유효한 값을 포함 하 여 지정 된 사용자의 액세스 권한을 바꿉니다.<ul><li>**n** -없음</li><li>**r** -읽기</li><li>**w** -쓰기</li><li>**c** -변경 (쓰기)</li><li>**f** -모든 권한</li></ul> |
| [/p 사용자 [...] | 지정 된 사용자 액세스를 거부 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="sample-output"></a>샘플 출력

| 출력 | 액세스 제어 항목 (ACE)에 적용 됩니다. |
-------- | ------------------------------------- |
| OI | 개체 상속 합니다. 이 폴더 및 파일입니다. |
| CI | 컨테이너 상속 합니다. 이 폴더 및 하위 폴더입니다. |
| IO | 만 상속 합니다. ACE는 현재 파일/디렉터리에는 적용 되지 않습니다. |
| 출력 메시지 없음 | 이 폴더에만 합니다. |
| (OI) (CI) | 이 폴더, 하위 폴더 및 파일입니다. |
| (OI) (CI) IO) | 하위 폴더 및 파일만 합니다. |
| (CI) IO) | 하위 폴더만 합니다. |
| (OI) IO) | 파일에만 해당 합니다. |

#### <a name="remarks"></a>설명

- 와일드 카드를 사용할 수 있습니다 (**?** 및 **&#42;**)를 지정 하 여 여러 파일을 지정 합니다.

- 둘 이상의 사용자를 지정할 수 있습니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [icacls](icacls.md)
