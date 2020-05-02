---
title: dfsdiag
description: DFS 네임 스페이스에 대 한 진단 정보를 제공 하는 dfsdiag에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d5a9b147994628ccad6a723311decbccbe82ec6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719546"
---
# <a name="dfsdiag"></a>dfsdiag

DFS 네임 스페이스에 대 한 진단 정보를 제공 합니다.

## <a name="syntax"></a>구문

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[Dfsdiag TestDCs](dfsdiag-testdcs.md)|도메인 컨트롤러 구성을 확인합니다.|
|[Dfsdiag TestSites](dfsdiag-testsites.md)|검사 사이트 연결 합니다.|
|[Dfsdiag TestDFSConfig](dfsdiag-testdfsconfig.md)|DFS 네임 스페이스 구성을 확인합니다.|
|[Dfsdiag TestDFSIntegrity](dfsdiag-testdfsintegrity.md)|DFS 네임 스페이스의 무결성을 확인합니다.|
|[Dfsdiag TestReferral](dfsdiag-testreferral.md)|조회 응답을 확인합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)