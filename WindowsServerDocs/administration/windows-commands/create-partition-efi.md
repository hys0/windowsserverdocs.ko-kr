---
title: 파티션 efi 만들기
description: Itanium 기반 컴퓨터의 gpt (GUID 파티션 테이블) 디스크에 EFI (Extensible 펌웨어 인터페이스) 시스템 파티션을 만드는 create partition efi에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cfc1fca-6515-4a4d-bfae-615fa8045ea9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc505dcbd94cf616b4ea160501ed1eadc1456a18
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719267"
---
# <a name="create-partition-efi"></a>파티션 efi 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Itanium 기반 컴퓨터에서는 gpt (GUID 파티션 테이블) 디스크에 EFI (Extensible 펌웨어 인터페이스) 시스템 파티션을 만듭니다.

## <a name="syntax"></a>구문  
  
```  
create partition efi [size=<n>] [offset=<n>] [noerr]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|  매개 변수  |                                                                                             설명                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  크기가\=<n>  |                         메가바이트 단위로 파티션의 크기 \(MB\)합니다. 크기를 지정 하는 경우에 현재 지역에서 사용 가능한 공간이 더 이상 없는 파티션을 계속 합니다.                         |
| 이동\=<n> |             (킬로바이트)의 오프셋 \(KB\), 파티션을 만들 때에 있습니다. 오프셋이, 파티션은 저장 하는 데 충분히 큰 첫 번째 디스크에에서 배치 됩니다.              |
|    noerr    | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |
  
## <a name="remarks"></a>설명  
  
-   파티션이 만들어지면 새 파티션으로 포커스 제공 됩니다.  
  
-   이 작업을 수행 하려면 gpt 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="examples"></a>예  
선택된 된 디스크에 EFI 파티션을 1000 메가바이트를 만들려면 다음을 입력 합니다.  
  
```  
create partition efi size=1000  
```  
  
## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
  

  

