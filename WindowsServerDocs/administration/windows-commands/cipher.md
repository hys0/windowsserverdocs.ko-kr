---
title: cipher
description: NTFS 볼륨에 있는 디렉터리와 파일의 암호화를 표시 하거나 변경 하는 암호화 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 78ef795e-0f87-4acd-8d15-192c972c0f41
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b07a0231b6cff6be9533136bf35ef013c854c2e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82713398"
---
# <a name="cipher"></a>cipher

NTFS 볼륨의 디렉터리 및 파일의 암호화를 표시하거나 변경합니다. 매개 변수 없이 사용 하는 경우 **암호화** 현재 디렉터리와 포함 된 파일의 암호화 상태를 표시 합니다.

## <a name="syntax"></a>구문

```
cipher [/e | /d | /c] [/s:<directory>] [/b] [/h] [pathname [...]]
cipher /k
cipher /r:<filename> [/smartcard]
cipher /u [/n]
cipher /w:<directory>
cipher /x[:efsfile] [filename]
cipher /y
cipher /adduser [/certhash:<hash> | /certfile:<filename>] [/s:directory] [/b] [/h] [pathname [...]]
cipher /removeuser /certhash:<hash> [/s:<directory>] [/b] [/h] [<pathname> [...]]
cipher /rekey [pathname [...]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| /b | 오류가 발생 하는 경우 중단 합니다. 기본적으로 **암호화** 계속 오류가 발생 하는 경우에 실행 합니다. |
| /C | 암호화 된 파일에 정보를 표시합니다. |
| /d | 지정 된 파일 또는 디렉터리를 해독합니다. |
| /e | 지정 된 파일 또는 디렉터리를 암호화합니다. 디렉터리는 나중에 추가 된 파일이 암호화 되도록 표시 됩니다. |
| /h | 파일을 표시 된 숨겨진 또는 시스템 특성입니다. 기본적으로 이러한 파일 암호화 또는 해독 됩니다. |
| /k | 파일 시스템 EFS (암호화) 파일과 함께 새 인증서 및 사용에 대 한 키를 만듭니다. 하는 경우는 **/k** 매개 변수를 지정 하면 다른 모든 매개 변수는 무시 됩니다. |
| r:`<filename>` [/smartcard] | EFS 복구 에이전트 키 및 인증서를 생성 한 후에.pfx 파일 (인증서와 프라이빗 키 포함) 및 (인증서만 포함)를.cer 파일로 기록 합니다. 경우 **/smartcard** 를 지정한 경우 복구 키 및 인증서는 스마트 카드를 기록 하 고.pfx 파일이 생성 됩니다. |
| /s`<directory>` | 지정 된 *디렉터리*의 모든 하위 디렉터리에서 지정 된 작업을 수행 합니다. |
| /u [/n] |  로컬 드라이브에 암호화 된 모든 파일을 찾습니다. 과 함께 사용할 경우는 **/n** 매개 변수 없는 업데이트 됩니다. 없이 사용 하는 경우 **/n**, **/u** 사용자의 파일 암호화 키 또는 현재 뿐 복구 에이전트의 키를 비교 하 고 변경 된 경우이 업데이트 합니다. 이 매개 변수 에서만 작동 **/n**합니다. |
| /w`<directory>` | 전체 볼륨에 사용 되지 않는 사용 가능한 디스크 공간에서 데이터를 제거합니다. 사용 하는 경우는 **/w** 매개 변수를 다른 모든 매개 변수는 무시 됩니다. 지정 된 디렉터리는 로컬 볼륨에 있는 모든 위치에 수 있습니다. 있으면 마운트 지점 또는 디렉터리를 가리키는 데이터의 다른 볼륨에에 해당 볼륨 제거 됩니다. |
| /x [: efsfile] [`<FileName>`] | 지정된 된 파일 이름에 EFS 인증서 및 키를 백업 합니다. 과 함께 사용할 경우 **: efsfile**, **/x** 파일을 암호화 하는 데 사용 된 사용자의 인증서를 백업 합니다. 그렇지 않으면 사용자의 현재 EFS 인증서 및 키 백업 됩니다. |
| /y | 로컬 컴퓨터에서 현재 EFS 인증서 축소판 그림을 표시합니다. |
| 사용자 \ 사용자 [/certhash:`<hash>` | /certfile:`<filename>`] |
| /rekey | 현재 구성 된 EFS 키를 사용 하 여 지정된 된 암호화 된 파일을 업데이트 합니다. |
| /removeuser /certhash:`<hash>` | 지정된 된 파일에서 사용자를 제거합니다. *해시* 제공 **/certhash** 제거 하는 인증서의 SHA1 해시를 이어야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="remarks"></a>설명

- 부모 디렉터리를 암호화 되지 않은 경우 수정 될 때 암호화 된 파일을 해독할 수 없습니다. 따라서 파일을 암호화 하는 경우 부모 디렉터리를 암호화 해야 합니다.

- 관리자는.cer 파일의 내용을 사용자에 대 한 복구 에이전트를 만들려면 EFS 복구 정책에 추가 하 고 개별 파일을 복구 하는.pfx 파일을 가져올 수 있습니다.

- 여러 디렉터리 이름과 와일드 카드를 사용할 수 있습니다.

- 매개 변수 사이 공백을 넣어야 합니다.

## <a name="examples"></a>예

현재 디렉터리에 각 파일과 하위 디렉터리의 암호화 상태를 표시 하려면 다음을 입력 합니다.

```
cipher
```

암호화 된 파일 및 디렉터리는 **E**로 표시 됩니다. 암호화 되지 않은 파일 및 디렉터리는 **U**로 표시 됩니다. 예를 들어 다음 출력은 현재 디렉터리와 모든 콘텐츠가 현재 암호화 되지 않았음을 나타냅니다.

```
Listing C:\Users\MainUser\Documents\
New files added to this directory will not be encrypted.
U Private
U hello.doc
U hello.txt
```

이전 예제에서 사용 되는 개인 디렉터리에 대 한 암호화를 사용 하려면 다음을 입력 합니다.

```
cipher /e private
```

다음과 같은 출력이 표시 됩니다.

```
Encrypting files in C:\Users\MainUser\Documents\
Private             [OK]
1 file(s) [or directorie(s)] within 1 directorie(s) were encrypted.
```

**암호화** 명령은 다음과 같은 출력을 표시 합니다.

```
Listing C:\Users\MainUser\Documents\
New files added to this directory will not be encrypted.
E Private
U hello.doc
U hello.txt
```

그러면 **개인** 디렉터리가 암호화 된 상태로 표시 됩니다.

### <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
