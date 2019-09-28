---
title: dfsdiag Testdfs 무결성
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7f344e2d1fecc542efc39688f20165fd3e39a04a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378434"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag Testdfs 무결성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

분산 파일 시스템의 무결성을 검사 \(DFS\) 다음 테스트를 수행 하 여 네임 스페이스:  
  
-   DFS 메타 데이터 손상 또는 도메인 컨트롤러 간의 불일치를 확인 합니다.  
  
-   액세스 구성의 유효성을 검사\-DFS 메타 데이터와 네임 스페이스 서버 공유 간의 일치 하는지 확인 하는 열거형을 기반으로 합니다.  
  
-   중복 된 DFS 폴더 검색 \(링크\), 중복 된 폴더 및 폴더 대상 겹치는 폴더입니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|@no__t 0DFSRoot: <DFS root path>|DFS 네임 스페이스를 진단 합니다.|  
|\/ 재귀|네임 스페이스 interlinks 테스트 등을 수행 합니다.|  
|\/Full|모든 폴더 대상에 대 한 공유 및 NTFS Acl 및 클라이언트 쪽 구성의 일관성을 확인 합니다. 또한 online 속성이 설정 되었는지 확인 합니다.|  
  
## <a name="BKMK_Examples"></a>예와  
TBD를 입력 합니다.  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

