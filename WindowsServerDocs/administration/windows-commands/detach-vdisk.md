---
title: 분리 vdisk
description: 선택한 가상 하드 디스크 (VHD)가 호스트 컴퓨터의 로컬 하드 디스크 드라이브로 나타나지 않도록 하는 detach vdisk에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5e64559650597eb8d15e28075f74704fdf338a6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716666"
---
# <a name="detach-vdisk"></a>분리 vdisk

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

선택한 VHD (가상 하드 디스크)가 호스트 컴퓨터의 로컬 하드 디스크 드라이브로 나타나지 않도록 합니다. VHD를 분리 하는 경우에 다른 위치에 복사할 수 있습니다.  
  
> [!NOTE]  
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
detach vdisk [noerr]  
```  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|noerr|스크립팅에 사용 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|  
  
## <a name="remarks"></a>설명  
  
-   VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="examples"></a>예  
선택한 VHD를 분리 하려면 다음을 입력 합니다.  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
  
-   [연결 vdisk](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  

-   [세부 정보 vdisk](detail-vdisk.md)  
  
-   [vdisk 확장](expand-vdisk.md)  
  
-   [Vdisk를 병합 합니다.](merge-vdisk.md)  
  
-   [vdisk 선택](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

