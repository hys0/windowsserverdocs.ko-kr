---
title: dfsdiag Testdfs 구성
description: Dfsdiag Testdfs Config에 대 한 Windows 명령 항목으로, DFS (분산 파일 시스템) 네임 스페이스의 구성을 확인 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ffb75ba26b4ed90dbf5c8bfda80f4a81f986e46a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846336"
---
# <a name="dfsdiag-testdfsconfig"></a>dfsdiag Testdfs 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 작업을 수행 하 여 분산 파일 시스템 (DFS) 네임 스페이스의 구성을 확인 합니다.  
  
-   모든 네임 스페이스 서버에서 DFS 네임 스페이스 서비스가 실행 중이 고 해당 시작 유형이 자동으로 설정 되어 있는지 확인 합니다.  
  
-   DFS 레지스트리 구성 네임 스페이스 서버 간에 일관 되는지 확인 합니다.  
  
-   Windows Server 2008 이상을 실행 하는 클러스터 된 네임 스페이스 서버에서 다음 종속성의 유효성을 검사 합니다.  
  
    -   네임 스페이스 루트 리소스에 대 한 종속성 네트워크 이름 리소스입니다.  
  
    -   IP 주소 리소스에 네트워크 이름 리소스 종속성입니다.  
  
    -   실제 디스크 리소스에 네임 스페이스 루트 리소스 종속성입니다.

## <a name="syntax"></a>구문  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:<namespace>  
```  
  
#### <a name="parameters"></a>매개 변수  
  
|       매개 변수       |               설명               |
|-----------------------|-----------------------------------------|
| /DFSRoot:`<namespace>` | 진단할 네임 스페이스 (DFS 루트)입니다. |
  
## <a name="examples"></a><a name=BKMK_Examples></a>예와  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

