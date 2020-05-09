---
title: dfsdiag testsites
description: 네임 스페이스 서버 또는 폴더 (링크) 대상 역할을 하는 서버가 모든 도메인 컨트롤러에서 동일한 사이트 연결을 갖고 있는지 확인 하 여 AD DS (active directory 도메인 서비스) 사이트의 구성을 확인 하는 dfsdiag testsites에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54eb7c7ec44d7cd4872960ca29cd3146b710f472
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992848"
---
# <a name="dfsdiag-testsites"></a>dfsdiag testsites

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

네임 스페이스 서버나 폴더 (링크) 대상 역할을 하는 서버가 모든 도메인 컨트롤러에서 동일한 사이트 연결을 갖고 있는지 확인 하 여 AD DS (active directory 도메인 서비스) 사이트의 구성을 확인 합니다.

## <a name="syntax"></a>구문

```
dfsdiag /testsites </machine:<server name>| /DFSpath:<namespace root or DFS folder> [/recurse]> [/full]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `/machine:<server name>` | 사이트 연결을 확인 하는 서버의 이름입니다. |
| `/DFSpath:<namespace root or DFS folder>` | 사이트 연결을 확인할 대상이 포함 된 네임 스페이스 루트 또는 분산 파일 시스템 (DFS) 폴더 (링크)입니다. |
| /recurse | 열거 하 고 지정 된 네임 스페이스 루트 아래의 모든 폴더 대상에 대 한 사이트 연결을 확인 합니다. |
| /full | AD DS 및 서버의 레지스트리에 동일한 사이트 연결 정보가 포함 되어 있는지 확인 합니다. |

## <a name="examples"></a>예

*Machine\MyServer*에서 사이트 연결을 확인 하려면 다음을 입력 합니다.

```
dfsdiag /testsites /machine:MyServer
```

분산 파일 시스템 (DFS) 폴더를 확인 하 여 사이트 연결을 확인 하려면 AD DS와 서버의 레지스트리가 동일한 사이트 연결 정보를 포함 하는지 확인 합니다.

```
dfsdiag /TestSites /DFSpath:\\contoso.com\namespace1\folder1 /full
```

지정 된 네임 스페이스 루트의 모든 폴더 대상에 대 한 사이트 연결을 열거 하 고 확인 하는 AD DS 것과 함께 네임 스페이스 루트를 확인 하 여 사이트 연결을 확인 하려면 다음을 입력 합니다.

```
dfsdiag /testsites /DFSpath:\\contoso.com\namespace2 /recurse /full
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [dfsdiag 명령](dfsdiag.md)
