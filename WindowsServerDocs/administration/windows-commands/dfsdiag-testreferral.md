---
title: dfsdiag TestReferral
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af22520d2c89f9d9f9d91ea6f43a33f3ff9c57f1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378361"
---
# <a name="dfsdiag-testreferral"></a>dfsdiag TestReferral

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

분산 파일 시스템 확인 \(DFS\) 다음 테스트를 수행 하 여 조회 합니다.  
  
-   인수 없이 DFSpath 매개 변수를 사용 하는 경우이 명령은 조회 목록에 트러스트 된 도메인이 모두 포함 되는지 확인 합니다.  
  
-   도메인을 지정 하는 경우이 명령은 도메인 컨트롤러의 상태 검사를 수행 하 \(dfsdiag \/testdcs @ no__t-2를 수행 하 고 로컬 호스트의 사이트 연결 및 도메인 캐시를 테스트 합니다.  
  
-   도메인을 지정 하는 경우와 \\SYSvol 또는 \\NETS를 지정 하는 것 외에도,이 명령은 SYSvol 또는 NETLOGON 조회의 TTL (time To @no__t Live)이 다음의 기본값을 일치 하는지 확인 합니다. 900 초.  
  
-   도메인을 지정 하는 경우와 동일한 상태 검사를 수행 하는 것 외에도 네임 스페이스 루트를 지정 하는 경우 명령은 0dfsdiag \/Testdfs Config @ no__t-2와 네임 스페이스 무결성 검사 @no__t-@no__ 3dfsdiag를 @no__t 합니다. t-4Testdfs 무결성 @ no__t-5  
  
-   네임 스페이스 루트를 지정 하는 경우와 같은 상태 검사를 수행 하는 것 외에도 DFS 폴더 \(link @ no__t-1을 지정 하는 경우 명령은 폴더 대상 \(dfsdiag \/testsites @ no__t-4의 사이트 구성에 대 한 유효성을 검사 하 고 유효성을 검사 합니다. 로컬 호스트의 사이트 연결입니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|@no__t 0DFSpath: <path for getting referrals>|이 DFS 경로 다음 중 하나일 수 있습니다.<br /><br />-    @ no__t-1blank @ no__t-2: 트러스트 된 도메인을 테스트 합니다.<br />-    @ no__t-1 @ no__t-2Domain: 도메인 컨트롤러 조회<br />-    @ no__t-1 @ no__t-2Domain @ no__t-3SYSvol: SYSvol 조회.<br />-    @ no__t-1 @ no__t-2Domain @ no__t-3NETA: NETLOGON 조회.<br />-    @ no__t-1 @ no__t-2 @ no__t @ no__t-4 @ no__t-5: 네임 스페이스 루트 조회.<br />-    @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7: DFS 폴더 \(link @ no__t-1 개 조회|  
|\/Full|도메인 및 루트 조회에만 적용 됩니다. 레지스트리 및 active directory 도메인 서비스 \(AD DS @ no__t-1 간의 사이트 연결 정보 일관성을 확인 합니다.|  
  
## <a name="BKMK_Examples"></a>예와  
TBD를 입력 합니다.  
  
```  
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace  
```  
  
TBD를 입력 합니다.  
  
```  
dfsdiag /TestReferral /DFSpath:  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  

