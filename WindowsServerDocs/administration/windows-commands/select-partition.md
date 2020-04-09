---
title: 파티션 선택
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97145d73cbbe1bdc9b27e545b047b78fe89e4984
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834806"
---
# <a name="select-partition"></a>파티션 선택

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 파티션을 선택 하 고 포커스를 이동 합니다. 이 명령은 현재 선택된 된 디스크에 포커스를가지고 있는 파티션을 표시 하려면 데도 사용할 수 있습니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
select partition=<n>  
```  
  
### <a name="parameters"></a>매개 변수  
  
|   매개 변수    |                                                                                    설명                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 파티션\=<n> | 포커스를 받을 파티션의 수입니다. 사용 하 여 현재 선택 된 디스크에 모든 파티션에 대 한 숫자를 볼 수는 **파티션 목록이** DiskPart 명령을 합니다. |
  
## <a name="remarks"></a>주의  
  
-   파티션을 선택 하기 전에 먼저 선택 해야 사용 하 여 디스크는 **디스크 선택** 명령입니다.  
  
-   파티션 번호가 지정 되지 않은 경우이 명령은 현재 선택 된 디스크에 포커스를가지고 있는 파티션을 표시 합니다.  
  
-   해당 하는 파티션이 있는 볼륨을 선택 하면 파티션이 자동으로 선택 됩니다.  
  
-   파티션이 해당 볼륨으로 선택 된 경우 볼륨이 자동으로 선택 됩니다.  
  
## <a name="examples"></a><a name=BKMK_examples></a>예와  
포커스 파티션 3 입력 합니다.  
  
```  
select partitition=3  
```  
  
현재 선택된 된 디스크에 포커스를가지고 있는 파티션을 표시 하려면 다음을 입력 합니다.  
  
```  
select partition  
```  
  
## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
  

  

