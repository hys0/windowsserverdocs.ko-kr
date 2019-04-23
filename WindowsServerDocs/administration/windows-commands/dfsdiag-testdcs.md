---
title: Dfsdiag TestDCs
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 62956ae65d2311939ac0db6a4b86950f21dba407
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836604"
---
# <a name="dfsdiag-testdcs"></a>Dfsdiag TestDCs

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 도메인의 각 도메인 컨트롤러에는 다음과 같은 테스트를 수행 하 여 도메인 컨트롤러의 구성을 확인 합니다.  
  
-   확인 하는 분산 파일 시스템 \(DFS\) Namespace 서비스가 실행 되 고 해당 시작 유형이 자동으로 설정 되어 있습니다.  
  
-   사이트의 지원에 대 한 확인\-NETLOGON 및 SYSvol에 대 한 조회 비용을 지불 합니다.  
  
-   호스트 이름 및 IP 주소 여 사이트 연결의 일관성을 확인합니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|\/도메인:<Domain name>|확인 하려는 도메인입니다.|  
  
## <a name="remarks"></a>설명  
\/도메인은 선택적 매개 변수입니다. 기본값은 로컬 호스트에 추가 하는 로컬 도메인입니다.  
  
## <a name="BKMK_Examples"></a>예제  
Contoso.com 도메인의 도메인 컨트롤러의 구성을 확인 하려면 다음을 입력 합니다.  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

