---
title: dfsdiag TestSites
description: 네임 스페이스 서버 또는 폴더 (링크) 대상 역할을 하는 서버가 모든 도메인 컨트롤러에서 동일한 사이트 연결을 갖고 있는지 확인 하 여 AD DS (active directory 도메인 서비스) 사이트의 구성을 확인 하는 dfsdiag TestSites에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68048699a812beac94fa121d6801da5f42e5393b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719561"
---
# <a name="dfsdiag-testsites"></a>dfsdiag TestSites

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

네임 스페이스 서버나 폴더 (링크) 대상 역할을 하는 서버가 모든 도메인 컨트롤러에서 동일한 사이트 연결을 갖고 있는지 확인 하 여 AD DS (active directory 도메인 서비스) 사이트의 구성을 확인 합니다.

## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|\/컴퓨터<server name>|사이트 연결을 확인 하는 서버의 이름입니다.|  
|\/DFSpath<namespace root or DFS folder>|사이트 연결을 확인할 대상이 포함 된 네임 스페이스 루트 또는 분산 파일 시스템 (DFS) 폴더 (링크)입니다.|  
|\/Recurse|열거 하 고 지정 된 네임 스페이스 루트 아래의 모든 폴더 대상에 대 한 사이트 연결을 확인 합니다.|  
|\/차지|AD DS와 서버의 레지스트리에 동일한 사이트 연결 정보가 포함 되어 있는지 확인 합니다.|  
  
## <a name="examples"></a>예  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
 
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

