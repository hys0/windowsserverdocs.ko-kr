---
title: Dfsdiag TestReferral
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: cd1b87befa8a9cfda5ea27a4ce5a5105ea1a1009
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848024"
---
# <a name="dfsdiag-testreferral"></a>Dfsdiag TestReferral

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

분산 파일 시스템 확인 \(DFS\) 다음 테스트를 수행 하 여 조회 합니다.  
  
-   인수 없이 DFSpath 매개 변수를 사용 하는 경우이 명령은 조회 목록에 모든 트러스트 된 도메인을 확인 합니다.  
  
-   이 명령은 도메인 컨트롤러의 상태 검사를 수행 도메인을 지정 하면 \(dfsdiag \/testdcs\) 사이트 연결 및 로컬 호스트의 도메인 캐시 하 고 테스트 합니다.  
  
-   도메인을 지정 하는 경우 및 \\SYSvol 또는 \\NETLOGON, 동일한 상태를 수행 하는 것 외에도 확인 도메인을 지정 하는 경우 명령을 확인 하는 Live를 시간 \(TTL\) NETLOGON 또는 SYSvol 조회 900 초 기본 값과 일치 합니다.  
  
-   도메인을 지정 하는 경우 명령은 DFS 구성 검사를 수행 하는 대로 확인 동일한 상태를 수행 하는 것 외에도 네임 스페이스 루트를 지정 하는 경우 \(dfsdiag \/TestDFSConfig\) 네임 스페이스 무결성 검사 \(dfsdiag \/TestDFSIntegrity\)합니다.  
  
-   DFS 폴더를 지정 하는 경우 \(링크\)를 수행 하는 것 외에도 동일한 상태를 확인 명령 폴더 대상에 대 한 사이트 구성의 유효성을 검사 네임 스페이스 루트를 지정 하면 \(dfsdiag \/ testsites\) 로컬 호스트의 사이트 연결의 유효성을 검사 합니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|\/DFSpath:<path for getting referrals>|이 DFS 경로 다음 중 하나일 수 있습니다.<br /><br />-   \(빈\): 트러스트 된 도메인을 테스트 합니다.<br />-   \\\\도메인: 도메인 컨트롤러 조회 합니다.<br />-   \\\\Domain\\SYSvol: SYSvol 조회 합니다.<br />-   \\\\도메인\\NETLOGON: NETLOGON 조회 합니다.<br />-   \\\\<Domain or server>\\<Namespace Root>: Namespace 루트 조회 합니다.<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS 폴더 \(링크\) 조회 합니다.|  
|\/전체|도메인 및 루트 조회에만 적용 됩니다. 사이트 연결 정보는 레지스트리와 active directory Domain Services의 일관성을 확인 합니다 \(AD DS\)합니다.|  
  
## <a name="BKMK_Examples"></a>예제  
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
  

