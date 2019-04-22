---
title: 확장 된 파티션 만들기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ad7cb66-9c66-4153-b94e-1030a7225070
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa8d556822bc6caf4277812be818a0cf456e75dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818884"
---
# <a name="create-partition-extended"></a>확장 된 파티션 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포커스가 있는 디스크에는 확장 된 파티션을 만듭니다. 이 명령을 사용 하 여 마스터 부트 레코드에 대해서만 \(MBR\) 디스크.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|size\=<n>|파티션의 크기 (메가바이트)에서 지정 \(MB\)합니다. 크기를 지정 하는 경우 파티션을 확장 파티션의 가능한 공간이 없을 때까지 계속 합니다.|  
|offset\=<n>|(킬로바이트)에서 오프셋을 지정 \(KB\), 파티션을 만들 때에 있습니다. 없는 오프셋을 지정 하는 경우 새 파티션을 보유할 수 있도록 충분히 큰 디스크에 여유 공간 시작 부분에 파티션을 시작 됩니다.|  
|align\=<n>|모든 파티션 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 일반적으로 하드웨어 RAID 논리 단위 번호와 사용 \(LUN\) 성능을 향상 시키기 위해 배열입니다. <n> (킬로바이트)입니다 \(KB\) 가장 가까운 맞춤 경계선을 디스크의 시작 부분에서.|  
|noerr|만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|  
  
## <a name="remarks"></a>설명  
  
-   파티션이 만들어지면 포커스는 자동으로 새 파티션으로 이동 합니다.  
  
-   디스크당 확장된 파티션은 하나만 만들 수 있습니다.  
  
-   이 명령은 다른 확장된 파티션 내에서 확장된 파티션을 만들 하려고 하면 실패 합니다.  
  
-   논리 드라이브를 만들려면 먼저 확장된 파티션을 만들어야 합니다.  
  
-   이 작업을 수행 하려면 기본 MBR 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="BKMK_examples"></a>예제  
1000 메가바이트 확장된 파티션 크기에서를 만들려면 다음을 입력 합니다.  
  
```  
create partition extended size=1000  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

