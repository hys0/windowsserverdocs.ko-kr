---
title: nfsshare
description: NFS (네트워크 파일 시스템) 공유를 제어 하는 nfsshare 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 437a2615-335a-442f-9713-d50d5f3983a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4901e0c9ee0701261dc6abb8cfd69cc02d4dd02e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932046"
---
# <a name="nfsshare"></a>nfsshare

NFS (네트워크 파일 시스템) 공유를 제어 합니다. 매개 변수 없이 사용이 명령은 NFS 용 서버에서 내보낸 모든 NFS (네트워크 파일 시스템) 공유를 표시 합니다.

## <a name="syntax"></a>구문

```
nfsshare <sharename>=<drive:path> [-o <option=value>...]
nfsshare {<sharename> | <drive>:<path> | * } /delete
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -o anon =`{yes|no}` | 익명 (매핑되지 않음) 사용자가 공유 디렉터리에 액세스할 수 있는지 여부를 지정 합니다. |
| -o rw =`[<host>[:<host>]...]` | *호스트*에서 지정 된 호스트 또는 클라이언트 그룹에 의해 공유 디렉터리에 대 한 읽기/쓰기 액세스를 제공 합니다. 호스트와 그룹 이름을 콜론 (**:**)으로 구분 해야 합니다. *호스트* 를 지정 하지 않으면 모든 호스트와 클라이언트 그룹 ( **ro** 옵션으로 지정 된 그룹 제외)에서 읽기/쓰기 액세스 권한을 얻습니다. 모두는 **ro** 또는 **rw** 옵션 설정, 모든 클라이언트가 공유 디렉터리에 대 한 읽기 / 쓰기 액세스 권한이 있습니다. |
| -o ro =`[<host>[:<host>]...]` | *호스트*에서 지정 된 호스트 또는 클라이언트 그룹에 의해 공유 디렉터리에 대 한 읽기 전용 액세스를 제공 합니다. 호스트와 그룹 이름을 콜론 (**:**)으로 구분 해야 합니다. *호스트* 를 지정 하지 않으면 **rw** 옵션을 사용 하 여 지정한 모든 클라이언트는 읽기 전용 액세스 권한을 얻게 됩니다. 하나 이상의 클라이언트에 대해 **ro** 옵션이 설정 되어 있지만 **rw** 옵션이 설정 되지 않은 경우 **ro** 옵션으로 지정 된 클라이언트만 공유 디렉터리에 액세스할 수 있습니다. |
| -o encoding =`{euc-jp|euc-tw|euc-kr|shift-jis|Big5|Ksc5601|Gb2312-80|Ansi)` | NFS 공유에서 구성할 언어 인코딩을 지정 합니다. 공유에서 한 언어만 사용할 수 있습니다. 이 값은 다음 값 중 하나를 포함할 수 있습니다.<ul><li>**euc-jp:** 일본어</li><li>**euc-hy 다음과 같이 합니다.** 중국어</li><li>**euc-kr:** 한국어</li><li>**shift-jis:** 일본어</li><li>**Big5:** 중국어</li><li>**Ksc5601:** 한국어</li><li>**Gb2312-80:** 중국어 간체</li><li>**Ansi:** ANSI 인코딩</li></ul> |
| -o anongid =`<gid>` | 익명 (매핑되지 않음) 사용자가 gid를 GID (그룹 식별자 *)로 사용* 하 여 공유 디렉터리에 액세스 하도록 지정 합니다. 기본값은 **-2**입니다. 익명 GID는 익명 액세스를 사용할 수 없는 경우에도 매핑되지 않은 사용자가 소유 하는 파일의 소유자를 보고할 때 사용 됩니다. |
| -o anonuid =`<uid>` | 익명 (매핑되지 않음) 사용자가 uid (사용자 id)로 *uid* 를 사용 하 여 공유 디렉터리에 액세스 하도록 지정 합니다. 기본값은 **-2**입니다. 익명 UID는 익명 액세스를 사용할 수 없는 경우에도 매핑되지 않은 사용자가 소유 하는 파일의 소유자를 보고할 때 사용 됩니다. |
| -o 루트 =`[<host>[:<host>]...]` | *호스트*에 의해 지정 된 호스트 또는 클라이언트 그룹의 공유 디렉터리에 대 한 루트 액세스를 제공 합니다. 호스트와 그룹 이름을 콜론 (**:**)으로 구분 해야 합니다. *호스트* 를 지정 하지 않으면 모든 클라이언트에서 루트 액세스를 가져옵니다. **Root** 옵션이 설정 되지 않은 경우 클라이언트에 공유 디렉터리에 대 한 루트 액세스 권한이 없는 것입니다. |
| /delete | *Sharename* 또는 `<drive>:<path>` 가 지정 된 경우이 매개 변수는 지정 된 공유를 삭제 합니다. 와일드 카드 (*)를 지정 하는 경우이 매개 변수는 모든 NFS 공유를 삭제 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- *Sharename* 이 유일한 매개 변수인 경우이 명령은 *sharename*으로 식별 된 NFS 공유의 속성을 나열 합니다.

- *Sharename* 및를 사용 하는 경우 `<drive>:<path>` 이 명령은로 식별 된 폴더 `<drive>:<path>` 를 *sharename*으로 내보냅니다. **/Delete** 옵션을 사용 하면 지정 된 폴더는 NFS 클라이언트에서 사용할 수 없게 됩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [네트워크 파일 시스템 서비스 명령 참조](services-for-network-file-system-command-reference.md)

- [NFS cmdlet 참조](https://docs.microsoft.com/powershell/module/nfs)
