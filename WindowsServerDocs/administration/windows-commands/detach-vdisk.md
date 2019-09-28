---
title: Vdisk를 분리 합니다.
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4850f9f17218178f210820dd4c6ca96fd918accc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378692"
---
# <a name="detach-vdisk"></a>Vdisk를 분리 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

선택한 가상 하드 디스크를 중지 \(VHD\) 호스트 컴퓨터에서 로컬 하드 디스크 드라이브로 표시 합니다. VHD를 분리 하는 경우에 다른 위치에 복사할 수 있습니다.  
  
> [!NOTE]  
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
detach vdisk [noerr]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|noerr|스크립팅에 사용 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|  
  
## <a name="remarks"></a>설명  
  
-   VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="BKMK_Examples"></a>예와  
선택한 VHD를 분리 하려면 다음을 입력 합니다.  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
-   [연결 vdisk](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  
  
  
  
-   [세부 정보 vdisk](detail-vdisk.md)  
  
-   [vdisk 확장](expand-vdisk.md)  
  
-   [Merge vdisk](merge-vdisk.md)  
  
-   [vdisk 선택](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

