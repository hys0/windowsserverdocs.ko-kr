---
title: icacls
description: 지정 된 파일에 대 한 DACL (임의 액세스 제어 목록)을 표시 하거나 수정 하 고 저장 된 Dacl을 지정 된 디렉터리의 파일에 적용 하는 icacls 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 403edfcc-328a-479d-b641-80c290ccf73e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/21/2018
ms.openlocfilehash: dcf4fa9fa9205a762ead99ac4a8486ac04c23514
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724871"
---
# <a name="icacls"></a>icacls

지정된 파일의 DACL(임의 액세스 제어 목록)을 표시 또는 수정하고 저장한 DACL을 지정된 디렉터리의 파일에 적용합니다.

> [!NOTE]
> 이 명령은 더 이상 사용 되지 않는 [cacls 명령을](cacls.md)바꿉니다.

## <a name="syntax"></a>구문

```
icacls <filename> [/grant[:r] <sid>:<perm>[...]] [/deny <sid>:<perm>[...]] [/remove[:g|:d]] <sid>[...]] [/t] [/c] [/l] [/q] [/setintegritylevel <Level>:<policy>[...]]
icacls <directory> [/substitute <sidold> <sidnew> [...]] [/restore <aclfile> [/c] [/l] [/q]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<filename>` | Dacl을 표시 하려는 파일을 지정 합니다. |
| `<directory>` | Dacl을 표시 하려는 디렉터리를 지정 합니다. |
| /t | 현재 디렉터리 및 하위 디렉터리에서 지정 된 모든 파일에 작업을 수행합니다. |
| /C | 파일 오류 불구 하 고 작업을 계속 합니다. 오류 메시지가 계속 표시 됩니다. |
| /l | 대상 대신 기호화 된 링크에서 작업을 수행 합니다. |
| /q | 성공 메시지를 표시 하지 않습니다. |
| [/ 저장 `<ACLfile>` [/t] [/c] [/l] [/q]] | Dacl에 일치 하는 모든 파일에 대 한 저장 *ACLfile* 나중에 사용할 수 있는 **/복원**합니다. |
| [/ setowner `<username>` [/t] [/c] [/l] [/q]] | 지정된 된 사용자에 일치 하는 모든 파일의 소유자를 변경합니다. |
| [/findsid `<sid>` [/t] [/c] [/l] [/q]] | 지정된 된 보안 식별자 (SID)를 명시적으로 언급 하는 DACL을 포함 하는 일치 하는 모든 파일을 찾습니다. |
| [/ 확인 [/t] [/c] [/l] [/q]] | 정식 하지 않거나 길이 ACE (액세스 제어 항목) 수와 일치 하지 않는 Acl 사용 하 여 모든 파일을 찾습니다. |
| [/reset [/t] [/c] [/l] [/q]] | 기본값은 대체 Acl 일치 하는 모든 파일에 대 한 Acl을 상속합니다. |
| [/grant [: r] \<sid>:<perm>[...]] | 사용자 액세스 권한을 지정 하는 권한을 부여 합니다. 사용 권한을 이전에 부여 된 명시적 사용 권한을 바꿉니다.<p>**: R**을 추가 하지 않으면 이전에 부여한 모든 명시적 사용 권한에 권한이 추가 됩니다. |
| [/거부 \<sid>:<perm>[...]] | 명시적으로 지정 된 사용자 액세스 권한을 거부합니다. 명시적 거부 ACE 명시 된 사용 권한에 대해 추가 되 고 모든 명시적 권한 부여에 동일한 사용 권한이 제거 됩니다. |
| [/remove`[:g | :d]]` `<sid>`[...] /t /c /l /q | DACL에서 지정된 된 SID의 모든 항목을 제거합니다. 이 명령은 다음을 사용할 수도 있습니다.<ul><li>**: g** -지정 된 SID에 부여 된 모든 권한을 제거 합니다.</li><li>**:d** -지정 된 SID에 대 한 모든 거부 된 권한을 제거 합니다. |
| [/setintegritylevel [(CI) (OI)] `<Level>:<Policy>`[...]] | 일치 하는 모든 파일에는 무결성 ACE를 명시적으로 추가합니다. 수준은 다음과 같이 지정할 수 있습니다.<ul><li>**l** -낮음</li><li>**m**-보통</li><li>**h** -높음</li></ul>ACE 무결성에 대 한 상속 옵션은 수준 전후의 디렉터리에만 적용 됩니다. |
| [대체 / `<sidold> <sidnew>` [...]] | 기존 SID (*sidold*)를 새 sid (*sidold*)로 바꿉니다. `<directory>` 매개 변수와 함께를 사용 해야 합니다. |
| 복원/ `<ACLfile>` [/c] [/l] [/q] | 에서 `<ACLfile>` 지정 된 디렉터리의 파일에 저장 된 dacl을 적용 합니다. `<directory>` 매개 변수와 함께를 사용 해야 합니다. |
| /inheritancelevel:`[e | d | r]` | 다음이 될 수 있는 상속 수준을 설정 합니다.<ul><li>**e** -상속 사용</li><li>**d** -상속을 사용 하지 않도록 설정 하 고 ace를 복사 합니다.</li><li>**r** -상속 된 모든 ace를 제거 합니다.</li></ul> |

## <a name="remarks"></a>설명

- Sid는 숫자 또는 친숙 한 이름 형식을 사용할 수 있습니다. 숫자 형식을 사용 하는 경우 **&#42;** 와일드 카드 문자를 SID의 시작 부분으로 접사.

- 이 명령은 다음과 같이 ACE 항목의 정식 순서를 유지 합니다.  

    - 명시적 거부

    -  명시적 권한 부여

    - 상속 된 거부

    - 상속 된 권한 부여

- `<perm>` 옵션은 다음 형식 중 하나로 지정할 수 있는 사용 권한 마스크입니다.

    - 단순한 권한 시퀀스:

      - **F** -모든 권한

      - **M**-액세스 수정

      - **RX** -액세스 읽기 및 실행

      - **R** -읽기 전용 액세스

      - **W** -쓰기 전용 액세스

    - 특정 권한 괄호 안에 쉼표로 구분 된 목록:

      - **D** -삭제

      - **RC** -읽기 컨트롤

      - **WDAC** -DAC 쓰기

      - **WO** -쓰기 소유자

      - **S** -동기화

      - **AS** 액세스 시스템 보안

      - **MA** -최대 허용

      - **GR** -일반 읽기

      - **GW** -일반 쓰기

      - **GE** -일반 실행

      - **GA** -일반 모두

      - **RD** -데이터 읽기/목록 디렉터리

      - **WD** -데이터 쓰기/파일 추가

      - **AD** -데이터 추가/하위 디렉터리 추가

      - **팅** -확장 된 특성 읽기

      - **Wea** -확장 특성 쓰기

      - **X** -실행/트래버스

      - **DC** -하위 삭제

      - **RA** -특성 읽기

      - **WA** -특성 쓰기

  - 상속 권한은 다음 중 한 `<perm>` 가지 형식으로 나타날 수 있으며 디렉터리에만 적용 됩니다.

      - **(OI)** -개체 상속

      - **(CI)** -컨테이너 상속

      - **(IO)** -상속만

      - **(NP)** -상속을 전파 하지 않습니다.

## <a name="examples"></a>예

모든 파일에 대 한 Dacl는 C:\Windows 디렉터리 및 하위 디렉터리를 ACLFile 파일을 저장 하려면 다음을 입력 합니다.

```
icacls c:\windows\* /save aclfile /t
```

C:\Windows 디렉터리 및 하위 디렉터리에 있는 ACLFile 내의 모든 파일에 대 한 Dacl을 복원 하려면 다음을 입력 합니다.

```
icacls c:\windows\ /restore aclfile
```

사용자에 게 이름이 Test1 인 파일에 대 한 DAC 삭제 및 쓰기 권한을 부여 하려면 다음을 입력 합니다.

```
icacls test1 /grant User1:(d,wdac)
```

이름이 Test2 인 파일에 대 한 SID S-1-1-0 Delete 및 Write DAC 권한으로 정의한 사용자를 부여 하려면 다음을 입력 합니다.

```
icacls test2 /grant *S-1-1-0:(d,wdac)
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
