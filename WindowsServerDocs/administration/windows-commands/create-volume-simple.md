---
title: 단순 볼륨 만들기
description: 지정 된 동적 디스크에서 단순 볼륨을 만드는 단순 볼륨 만들기에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f92bd9cf92dea258c6a49dd4cf75c4aae357c88e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716927"
---
# <a name="create-volume-simple"></a>단순 볼륨 만들기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 동적 디스크의 단순 볼륨을 만듭니다.  
  
> [!IMPORTANT]  
> Windows Vista의 경우이 DiskPart 명령은 Windows Vista Ultimate, Windows Vista Enterprise 및 Windows Vista Business edition 에서만 사용할 수 있습니다.
  
## <a name="syntax"></a>구문  
  
```  
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>매개 변수  
  
| 매개 변수  |                                                                                                                            설명                                                                                                                            |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 크기가\=<n>  |                                                                  메가바이트 단위로 볼륨의 크기 \(MB\)합니다. 크기를 지정 하는 경우 새 볼륨은 디스크에 남은 공간을 차지 합니다.                                                                   |
| 디스크로\=<n>  |                                                                                동적 디스크 볼륨이 만들어집니다. 없는 디스크를 지정 하는 경우 현재 디스크를 사용 합니다.                                                                                |
| 않아\=<n> | 모든 볼륨 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 일반적으로 하드웨어 RAID 논리 단위 번호와 사용 \(LUN\) 성능을 향상 시키기 위해 배열입니다. *n* 은 디스크의 시작부터 \(가장\) 가까운 맞춤 경계로 표시 되는 kb 수입니다. |
|   noerr    |                               스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.                                |
  
## <a name="remarks"></a>설명  
  
-   볼륨을 만든 후 포커스는 자동으로 새 볼륨으로 이동 합니다.  
  
## <a name="examples"></a>예  
1, 디스크에 크기가 1000 메가바이트의 볼륨을 만들려면 다음을 입력 합니다.  
  
```  
create volume simple size=1000 disk=1  
```  
  
## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
  

  

