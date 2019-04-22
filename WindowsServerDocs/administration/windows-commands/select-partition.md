---
title: 파티션을 선택합니다
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c7d5675aa6c33ddbe1e5e873e1a7cf7a2e8f8017
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824964"
---
# <a name="select-partition"></a>파티션을 선택합니다

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 파티션을 선택한 다음 포커스를 이동 합니다. 이 명령은 현재 선택된 된 디스크에 포커스를가지고 있는 파티션을 표시 하려면 데도 사용할 수 있습니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
select partition=<n>  
```  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|partition\=<n>|포커스를 받을 파티션의 수입니다. 사용 하 여 현재 선택 된 디스크에 모든 파티션에 대 한 숫자를 볼 수는 **파티션 목록이** DiskPart 명령을 합니다.|  
  
## <a name="remarks"></a>설명  
  
-   파티션을 선택 하기 전에 먼저 선택 해야 사용 하 여 디스크는 **디스크 선택** 명령입니다.  
  
-   없는 파티션 번호를 지정 하는 경우이 명령은 현재 선택된 된 된 디스크에 포커스를가지고 있는 파티션을 표시 합니다.  
  
-   해당 파티션이 있는 볼륨을 선택 하면 파티션이 자동으로 선택 됩니다.  
  
-   파티션이 해당 볼륨을 선택 하는 경우 볼륨 자동으로 선택 됩니다.  
  
## <a name="BKMK_examples"></a>예제  
포커스 파티션 3 입력 합니다.  
  
```  
select partitition=3  
```  
  
현재 선택된 된 디스크에 포커스를가지고 있는 파티션을 표시 하려면 다음을 입력 합니다.  
  
```  
select partition  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

