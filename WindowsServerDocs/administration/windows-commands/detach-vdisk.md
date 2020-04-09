---
title: 분리 vdisk
description: 호스트 컴퓨터에서 선택한 VHD (가상 하드 디스크)를 로컬 하드 디스크 드라이브로 표시 하지 않도록 하는 detach vdisk에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 14eb66031841624156afb03f492e2afce5bc56f0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846506"
---
# <a name="detach-vdisk"></a>분리 vdisk

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
  
## <a name="remarks"></a>주의  
  
-   VHD는 선택 하 고이 작업이 성공 하기 위해 분리 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="examples"></a><a name=BKMK_Examples></a>예와  
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
  
-   [Merge vdisk](merge-vdisk.md)  
  
-   [vdisk 선택](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

