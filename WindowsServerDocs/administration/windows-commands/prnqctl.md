---
title: prnqctl
description: 테스트 페이지를 인쇄 하거나 프린터를 일시 중지 하거나 다시 시작 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 377b448eb74f0a27228d8502ce149fb04869895b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722798"
---
# <a name="prnqctl"></a>prnqctl

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

테스트 페이지를 인쇄, 일시 중지 하거나 프린터를 다시 시작 및 프린터 큐를 삭제 합니다.  

## <a name="syntax"></a>구문  
```  
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <ServerName>]   
[-p <printerName>] [-u <UserName>] [-w <Password>]  
```  
### <a name="parameters"></a>매개 변수  

|매개 변수|설명|  
|-------|--------|  
|-Z|**-p** 매개 변수를 사용 하 여 지정 된 프린터에서 인쇄를 일시 중지 합니다.|  
|-M|지정 된 프린터에서 인쇄를 다시 시작 되는 **-p** 매개 변수입니다.|  
|-E|**-p** 매개 변수를 사용 하 여 지정 된 프린터에서 테스트 페이지를 인쇄 합니다.|  
|-X|지정 된 프린터에서 인쇄 작업을 모두 취소는 **-p** 매개 변수입니다.|  
|-s \<ServerName>|프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다.|  
|-p \<printerName>|관리 하려는 프린터의 이름을 지정 합니다. 필수 사항입니다.|  
|-u \<UserName>-w \<암호>|프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않으면, 작동 하려면 명령에 대 한 이러한 사용 권한이 있는 계정으로 로그온 해야 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  

## <a name="remarks"></a>설명  
- **Prnqctl.vbs** 명령은%windir%\system32\ printing_Admin_Scripts\\ <language> 디렉터리에 있는 Visual Basic 스크립트입니다. 이 명령을 사용 하려면 명령 프롬프트에서 **cscript** 다음에 prnqctl.vbs 파일의 전체 경로를 입력 하거나 디렉터리를 적절 한 폴더로 변경 합니다. 다음은 그 예입니다.   
  ```  
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl  
  ```  
- 사용자가 제공 하는 정보에 공백이 포함 된 경우 텍스트에 따옴표를 사용 합니다 (예 `"computer Name"`:).  

## <a name="examples"></a><a name="BKMK_examples"></a>예와  
\\\Server1 컴퓨터에서 공유 하는 Laserprinter1 프린터에서 테스트 페이지를 인쇄 하려면 다음을 입력 합니다.  
```  
cscript Prnqctl -e -s Server1 -p Laserprinter1  
```  
로컬 컴퓨터의 Laserprinter1 프린터에서 인쇄를 일시 중지 하려면 다음을 입력 합니다.  
```  
cscript Prnqctl -z -p Laserprinter1  
```  
로컬 컴퓨터에서 Laserprinter1 프린터의 모든 인쇄 작업을 취소 하려면 다음을 입력 합니다.  
```  
cscript Prnqctl -x -p Laserprinter1  
```  

## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
[인쇄 명령 참조](print-command-reference.md)  
