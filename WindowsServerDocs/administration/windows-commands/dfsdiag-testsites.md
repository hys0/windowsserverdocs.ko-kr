---
title: Dfsdiag TestSites
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6486c79cfa58bb262fd3161ad0801e84185b6629
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873974"
---
# <a name="dfsdiag-testsites"></a>Dfsdiag TestSites

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active directory Domain Services의 구성을 확인 \(AD DS\) 확인 하 여 사이트 역할을 네임 스페이스 서버나 폴더는 해당 서버 \(링크\) 대상 모든 도메인에 대 한 동일한 사이트 연결 컨트롤러입니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|\/컴퓨터:<server name>|사이트 연결을 확인 하는 서버의 이름입니다.|  
|\/DFSpath:<namespace root or DFS folder>|네임 스페이스 루트 또는 분산 파일 시스템 \(DFS\) 폴더 \(링크\) 사이트 연결을 확인 하려는 대상을 사용 합니다.|  
|\/Recurse|열거 하 고 지정 된 네임 스페이스 루트 아래의 모든 폴더 대상에 대 한 사이트 연결을 확인 합니다.|  
|\/전체|AD DS 및 서버의 레지스트리에 동일한 사이트 연결 정보를 포함을 확인 합니다.|  
  
## <a name="BKMK_Examples"></a>예제  
TBD를 입력 합니다.  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
  
TBD를 입력 합니다.  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
TBD를 입력 합니다.  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

