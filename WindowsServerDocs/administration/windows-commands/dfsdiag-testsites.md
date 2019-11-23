---
title: dfsdiag TestSites
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: af72da64dd20d4b37824355a494cb8f97f597b28
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378384"
---
# <a name="dfsdiag-testsites"></a>dfsdiag TestSites

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

\(active directory 도메인 서비스의 구성에 대 한 AD DS\) 사이트를 확인 하는 사이트 \(\) 대상 네임 스페이스 서버 또는 폴더 역할을 하는 서버는 모든 도메인 컨트롤러에서 동일한 사이트 연결 합니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|\/컴퓨터:<server name>|사이트 연결을 확인 하는 서버의 이름입니다.|  
|\/DFSpath:<namespace root or DFS folder>|네임 스페이스 루트 또는 분산 파일 시스템 \(DFS\) 폴더 \(링크\) 사이트 연결을 확인 하려는 대상을 사용 합니다.|  
|\/재귀|열거 하 고 지정 된 네임 스페이스 루트 아래의 모든 폴더 대상에 대 한 사이트 연결을 확인 합니다.|  
|\/전체|AD DS와 서버의 레지스트리에 동일한 사이트 연결 정보가 포함 되어 있는지 확인 합니다.|  
  
## <a name="BKMK_Examples"></a>예와  
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
  

