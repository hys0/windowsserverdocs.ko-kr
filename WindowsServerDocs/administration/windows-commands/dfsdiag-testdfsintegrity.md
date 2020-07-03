---
title: dfsdiag testdfsintegrity
description: 분산 파일 시스템 (DFS) 네임 스페이스의 무결성을 검사 하는 dfsdiag testdfs 무결성 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7896174bb58c957e4c24b1c3f7e1b2bacc9f95f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930633"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag testdfsintegrity

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 테스트를 수행 하 여 분산 파일 시스템 (DFS) 네임 스페이스의 무결성을 검사 합니다.

- DFS 메타 데이터 손상 또는 도메인 컨트롤러 간의 불일치를 확인 합니다.

- 액세스 기반 열거 구성의 유효성을 검사 하 여 DFS 메타 데이터와 네임 스페이스 서버 공유 간에 일치 하는지 확인 합니다.

- 겹치는 DFS 폴더 (링크), 중복 폴더 및 폴더 대상이 겹치는 폴더를 검색 합니다.

## <a name="syntax"></a>구문

```
dfsdiag /testdfsintegrity /DFSroot: <DFS root path> [/recurse] [/full]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /DFSroot:`<DFS root path>` | DFS 네임 스페이스를 진단 합니다. |
| /recurse | Interlinks 네임 스페이스를 포함 하 여 테스트를 수행 합니다. |
| /full | 모든 폴더 대상의 클라이언트 쪽 구성과 함께 공유 및 NTFS Acl의 일관성을 확인 합니다. 또한 online 속성이 설정 되었는지 확인 합니다. |

## <a name="examples"></a>예

Interlinks를 포함 하 여 *com\MyNamespace*에서 DFS (분산 파일 시스템) 네임 스페이스의 무결성 및 일관성을 확인 하려면 다음을 입력 합니다.

```
dfsdiag /testdfsintegrity /DFSRoot:\contoso.com\MyNamespace /recurse /full
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [dfsdiag 명령](dfsdiag.md)
