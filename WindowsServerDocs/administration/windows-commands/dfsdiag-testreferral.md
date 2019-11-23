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

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

분산 파일 시스템 확인 \(DFS\) 다음 테스트를 수행 하 여 조회 합니다.  
  
-   인수 없이 DFSpath 매개 변수를 사용 하는 경우이 명령은 조회 목록에 트러스트 된 도메인이 모두 포함 되는지 확인 합니다.  
  
-   도메인을 지정 하는 경우이 명령은 도메인 컨트롤러의 상태 검사를 수행 하 \(dfsdiag \/testdcs\) 하 고 로컬 호스트의 사이트 연결 및 도메인 캐시를 테스트 합니다.  
  
-   도메인을 지정 하 고 \\SYSvol 또는 \\NETLOGON을 지정 하는 것 외에도 도메인을 지정 하는 것과 동일한 상태 검사를 수행 하는 것 외에도,이 명령은 SYSvol 또는 NETLOGON 조회에 대 한 TTL (time To Live \(TTL\) 900 초의 기본값을 일치 하는지 확인 합니다.  
  
-   도메인을 지정 하는 경우와 동일한 상태 검사를 수행 하는 것 외에도 네임 스페이스 루트를 지정 하는 경우 명령은 dfsdiag \/Testdfs 구성\) \(DFS 구성 검사를 수행 하 고, 네임 스페이스 무결성 검사 \(dfsdiag \/Testdfs 무결성\)을 수행 합니다.  
  
-   DFS 폴더 \(링크\)를 지정 하는 경우, 네임 스페이스 루트를 지정 하는 것과 동일한 상태 검사를 수행 하는 것 외에도, 명령은 \(dfsdiag \/testsites\) 폴더 대상에 대 한 사이트 구성의 유효성을 검사 하 고 로컬 호스트의 사이트 연결에 대 한 유효성을 검사 합니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|\/DFSpath:<path for getting referrals>|이 DFS 경로 다음 중 하나일 수 있습니다.<br /><br />-   \(빈\): 트러스트 된 도메인을 테스트 합니다.<br />-   \\\\도메인: 도메인 컨트롤러 조회<br />-   \\\\도메인\\sysvol: SYSvol 조회.<br />NETLOGON: NETLOGON 조회를 \\도메인\\-   \\합니다.<br />-   \\\\<Domain or server>\\<Namespace Root>: 네임 스페이스 루트 조회<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS 폴더 \(링크\) 조회|  
|\/전체|도메인 및 루트 조회에만 적용 됩니다. 레지스트리와 active directory 도메인 서비스 \(AD DS\)간에 사이트 연결 정보의 일관성을 확인 합니다.|  
  
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
  

