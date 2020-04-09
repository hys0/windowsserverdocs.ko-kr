---
title: dfsdiag Testdfs 무결성
description: '**Dfsdiag Testdfs 무결성**에 대 한 Windows 명령 항목 분산 파일 시스템 (DFS) 네임 스페이스의 무결성을 검사 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 714b79369898338a4e4a6e4fad8487709ab4fc60
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846276"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag Testdfs 무결성

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 테스트를 수행 하 여 분산 파일 시스템 (DFS) 네임 스페이스의 무결성을 검사 합니다.

- DFS 메타 데이터 손상 또는 도메인 컨트롤러 간의 불일치를 확인 합니다.

- 액세스 기반 열거 구성의 유효성을 검사 하 여 DFS 메타 데이터와 네임 스페이스 서버 공유 간에 일치 하는지 확인 합니다.

- 겹치는 DFS 폴더 (링크), 중복 폴더 및 폴더 대상이 겹치는 폴더를 검색 합니다.

## <a name="syntax"></a>구문

```
dfsdiag /TestDFSIntegrity /DFSRoot: <DFS root path> [/Recurse] [/Full]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|-------|--------|
| /DFSRoot: `<DFS root path>`| DFS 네임 스페이스를 진단 합니다. |
| /Recurse | 네임 스페이스 interlinks 테스트 등을 수행 합니다. |
| /Full | 모든 폴더 대상에 대 한 공유 및 NTFS Acl 및 클라이언트 쪽 구성의 일관성을 확인 합니다. 또한 online 속성이 설정 되었는지 확인 합니다. |

## <a name="examples"></a><a name=BKMK_Examples></a>예와

```
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)

-   [dfsdiag](dfsdiag.md)


