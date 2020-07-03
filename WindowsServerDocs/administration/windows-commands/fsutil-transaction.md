---
title: fsutil transaction
description: NTFS 트랜잭션을 관리 하는 fsutil transaction 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 95cd9a8f62aa9dd64d46a875a90847a65589b447
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922338"
---
# <a name="fsutil-transaction"></a>fsutil transaction

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

NTFS 트랜잭션을 관리합니다.

## <a name="syntax"></a>구문

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <filename>
fsutil transaction [list]
fsutil transaction [query] [{files | all}] <GUID>
fsutil transaction [rollback] <GUID>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 커밋(commit) | 성공적인 암시적 또는 명시적 지정 된 트랜잭션 끝을 표시 합니다. |
| `<GUID>` | 트랜잭션을 나타내는 GUID 값을 지정 합니다. |
| fileinfo  | 지정된 된 파일에 대 한 트랜잭션 정보를 표시합니다. |
| `<filename>` | 전체 경로 파일 이름을 지정합니다. |
| list | 현재 실행 중인 트랜잭션을의 목록이 표시 됩니다. |
| Query | 지정된 된 트랜잭션에 대 한 정보를 표시합니다.<ul><li>`fsutil transaction query files`을 지정 하면 지정 된 트랜잭션에 대해서만 파일 정보가 표시 됩니다.</li><li>`fsutil transaction query all`을 지정 하면 트랜잭션에 대 한 모든 정보가 표시 됩니다.</li></ul> |
| 롤백 | 시작 부분에는 지정 된 트랜잭션을 롤백합니다. |

### <a name="examples"></a>예

파일 *c:\test.txt*에 대 한 트랜잭션 정보를 표시 하려면 다음을 입력 합니다.

```
fsutil transaction fileinfo c:\test.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [트랜잭션 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730726(v=ws.10))
