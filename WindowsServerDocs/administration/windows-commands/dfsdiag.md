---
title: dfsdiag
description: DFS 네임 스페이스에 대 한 진단 정보를 제공 하는 dfsdiag 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97f39d740bc321ebcece69ff0690dfac7aab6567
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928666"
---
# <a name="dfsdiag"></a>dfsdiag

DFS 네임 스페이스에 대 한 진단 정보를 제공 합니다.

## <a name="syntax"></a>구문

```
dfsdiag /testdcs [/domain:<domain name>]
dfsdiag /testsites </machine:<server name>| /DFSPath:<namespace root or DFS folder> [/recurse]> [/full]
dfsdiag /testdfsconfig /DFSRoot:<namespace>
dfsdiag /testdfsintegrity /DFSRoot:<DFS root path> [/recurse] [/full]
dfsdiag /testreferral /DFSpath:<DFS path to get referrals> [/full]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| [dfsdiag testdcs](dfsdiag-testdcs.md) | 도메인 컨트롤러 구성을 확인합니다. |
| [dfsdiag testsites](dfsdiag-testsites.md) | 검사 사이트 연결 합니다. |
| [dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md) | DFS 네임 스페이스 구성을 확인합니다. |
| [dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md) | DFS 네임 스페이스의 무결성을 확인합니다. |
| [dfsdiag testreferral](dfsdiag-testreferral.md) | 조회 응답을 확인합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
