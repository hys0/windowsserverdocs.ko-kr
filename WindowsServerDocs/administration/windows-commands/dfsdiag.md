---
title: dfsdiag
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61a6ab9a90e4d0220cfe27d2d21120be19b9ff1f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378313"
---
# <a name="dfsdiag"></a>dfsdiag



`Dfsdiag` 명령 DFS 네임 스페이스에 대 한 진단 정보를 제공 합니다.

## <a name="syntax"></a>구문

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[Dfsdiag TestDCs](dfsdiag-testdcs.md)|도메인 컨트롤러 구성을 확인합니다.|
|[Dfsdiag TestSites](dfsdiag-testsites.md)|검사 사이트 연결 합니다.|
|[Dfsdiag Testdfs 구성](dfsdiag-testdfsconfig.md)|DFS 네임 스페이스 구성을 확인합니다.|
|[Dfsdiag Testdfs 무결성](dfsdiag-testdfsintegrity.md)|DFS 네임 스페이스의 무결성을 확인합니다.|
|[Dfsdiag TestReferral](dfsdiag-testreferral.md)|조회 응답을 확인합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)