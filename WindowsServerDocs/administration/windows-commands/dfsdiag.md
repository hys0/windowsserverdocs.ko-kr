---
title: dfsdiag
description: DFS 네임 스페이스에 대 한 진단 정보를 제공 하는 dfsdiag 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e9e0de18b48a4233b950ad6aa8f1e450a99da62
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992833"
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

| 매개 변수 | Description |
| --------- | ----------- |
| [dfsdiag testdcs](dfsdiag-testdcs.md) | 도메인 컨트롤러 구성을 확인합니다. |
| [dfsdiag testsites](dfsdiag-testsites.md) | 검사 사이트 연결 합니다. |
| [dfsdiag testdfs 구성](dfsdiag-testdfsconfig.md) | DFS 네임 스페이스 구성을 확인합니다. |
| [dfsdiag testdfs 무결성](dfsdiag-testdfsintegrity.md) | DFS 네임 스페이스의 무결성을 확인합니다. |
| [dfsdiag testreferral](dfsdiag-testreferral.md) | 조회 응답을 확인합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
