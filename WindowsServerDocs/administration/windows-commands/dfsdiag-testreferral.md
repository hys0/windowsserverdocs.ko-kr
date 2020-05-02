---
title: dfsdiag TestReferral
description: 분산 파일 시스템 (DFS) 조회를 확인 하는 dfsdiag TestReferral에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b4c616181d367a8a95efe6484f74af0ff88cc5f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719563"
---
# <a name="dfsdiag-testreferral"></a>dfsdiag TestReferral

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 테스트를 수행 하 여 분산 파일 시스템 (DFS) 조회를 확인 합니다.

- 인수 없이 DFSpath 매개 변수를 사용 하는 경우이 명령은 조회 목록에 트러스트 된 도메인이 모두 포함 되는지 확인 합니다.

- 도메인을 지정 하면이 명령은 도메인 컨트롤러 (dfsdiag/testdcs)의 상태 검사를 수행 하 고 로컬 호스트의 사이트 연결 및 도메인 캐시를 테스트 합니다.

- 도메인 및 \SYSvol 또는 \NETS를 지정 하는 경우와 동일한 상태 검사를 수행 하는 것 외에도 도메인을 지정 하는 경우 명령은 SYSvol 또는 NETLOGON 조회의 ttl (time To Live)이 기본값인 900 초와 일치 하는지 확인 합니다.

- 도메인을 지정 하는 경우와 동일한 상태 검사를 수행 하는 것 외에도 네임 스페이스 루트를 지정 하면이 명령은 DFS 구성 검사 (dfsdiag/TestDFSConfig)와 네임 스페이스 무결성 검사 (dfsdiag/TestDFSIntegrity)를 수행 합니다.

- DFS 폴더 (링크)를 지정 하는 경우 네임 스페이스 루트를 지정 하는 것과 동일한 상태 검사를 수행 하는 것 외에도, 명령은 폴더 대상 (dfsdiag/testsites)에 대 한 사이트 구성의 유효성을 검사 하 고 로컬 호스트의 사이트 연결에 대 한 유효성을 검사 합니다.

## <a name="syntax"></a>구문

```
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
| DFSpath<path for getting referrals>|이 DFS 경로 다음 중 하나일 수 있습니다.<p>-   \(blank\): 트러스트 된 도메인을 테스트 합니다.<br />-   \\\\도메인: 도메인 컨트롤러 조회<br />-   \\\\도메인\\SYSvol: SYSvol 조회<br />-   \\\\Netlogon의\\doma: netlogon 조회<br />-   \\\\<Domain or server>\\<Namespace Root>: 네임 스페이스 루트 조회<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS 폴더 \(링크\) 조회|
|/Full|도메인 및 루트 조회에만 적용 됩니다. 레지스트리와 active directory 도메인 서비스 \(AD DS\)간의 사이트 연결 정보 일관성을 확인 합니다.|

## <a name="examples"></a>예

```
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace
```

```
dfsdiag /TestReferral /DFSpath:
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)


