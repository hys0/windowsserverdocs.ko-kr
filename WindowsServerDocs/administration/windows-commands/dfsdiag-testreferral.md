---
title: dfsdiag testreferral
description: 분산 파일 시스템 (DFS) 조회를 확인 하는 dfsdiag testreferral 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 23abcd738170d5f53e12ae83c41d632d2d7ac738
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992931"
---
# <a name="dfsdiag-testreferral"></a>dfsdiag testreferral

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 테스트를 수행 하 여 분산 파일 시스템 (DFS) 조회를 확인 합니다.

- 인수 없이 **DFSpath*** 매개 변수를 사용 하는 경우 명령에서 조회 목록에 트러스트 된 도메인이 모두 포함 되어 있는지 확인 합니다.

- 도메인을 지정 하는 경우이 명령은 도메인 컨트롤러 (`dfsdiag /testdcs`)의 상태 검사를 수행 하 고 로컬 호스트의 사이트 연결 및 도메인 캐시를 테스트 합니다.

- 도메인 및 \SYSvol 또는 \NETS를 지정 하는 경우 명령은 SYSvol 또는 NETLOGON 조회의 **TTL (Time To Live)** 이 기본값인 900 초와 일치 하는지 확인 하는 것과 함께 동일한 도메인 컨트롤러 상태 검사를 수행 합니다.

- 네임 스페이스 루트를 지정 하는 경우이 명령은 DFS 구성 검사 (`dfsdiag /testdfsconfig`) 및 네임 스페이스 무결성 검사 (`dfsdiag /testdfsintegrity`)를 수행 하는 것과 함께 동일한 도메인 컨트롤러 상태 검사를 수행 합니다.

- DFS 폴더 (링크)를 지정 하는 경우 명령은 폴더 대상에 대 한 사이트 구성의 유효성 검사 (dfsdiag/testsites) 및 로컬 호스트의 사이트 연결 유효성 검사와 함께 동일한 네임 스페이스 루트 상태 검사를 수행 합니다.

## <a name="syntax"></a>구문

```
dfsdiag /testreferral /DFSpath:<DFS path to get referrals> [/full]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| DFSpath`<path to get referrals>` | 다음 중 하나일 수 있습니다.<ul><li>**Blank:** 트러스트 된 도메인만 테스트 합니다.</li><li>`\\Domain:`도메인 컨트롤러 조회만 테스트 합니다.</li><li>`\\Domain\SYSvol:`SYSvol 조회만 테스트 합니다.</li><li>`\\Domain\NETLOGON:`NETLOGON 조회만 테스트 합니다.</li><li>`\\<domain or server>\<namespace root>:`네임 스페이스 루트 조회만 테스트 합니다.</li><li>`\\<domain or server>\<namespace root>\<DFS folder>:`DFS 폴더 (링크) 조회만 테스트 합니다.</li></ul> |
| /full | 도메인 및 루트 조회에만 적용 됩니다. 레지스트리와 active directory 도메인 서비스 (AD DS) 간의 사이트 연결 정보에 대 한 일관성을 확인 합니다. |

## <a name="examples"></a>예

*Com\MyNamespace*의 분산 파일 시스템 (DFS) 조회를 확인 하려면 다음을 입력 합니다.

```
dfsdiag /testreferral /DFSpath:\\contoso.com\MyNamespace
```

모든 트러스트 된 도메인에서 분산 파일 시스템 (DFS) 조회를 확인 하려면 다음을 입력 합니다.

```
dfsdiag /testreferral /DFSpath:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [dfsdiag 명령](dfsdiag.md)
