---
title: 복구
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 940b0931671d5f3c2137fafe4ae73b7cecd0160e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821194"
---
# <a name="repair"></a>복구

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

복구 하는 RAID\-지정된 된 동적 디스크를 사용 하 여 실패 한 디스크 영역을 대체 하 여 포커스를 사용 하 여 5 볼륨입니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|disk\=<n>|실패 한 디스크 영역을 대체 하는 동적 디스크를 지정 합니다.|  
|align\=<n>|모든 볼륨 또는 파티션 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. *n* 는 킬로바이트의 수는 \(KB\) 가장 가까운 맞춤 경계선을 디스크의 시작 부분에서.|  
|noerr|만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|  
  
## <a name="remarks"></a>설명  
  
-   지정 된 동적 디스크는 RAID에 실패 한 디스크 영역의 전체 크기 보다 크거나 여유 공간이 있어야 합니다.\-5 볼륨입니다.  
  
-   raid에서 볼륨\-5 배열을이 작업이 성공 하기 위해 선택 해야 합니다. 사용 하 여는 **볼륨 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="BKMK_examples"></a>예제  
동적 디스크 4로 바꾸어 포커스가 있는 볼륨을 바꾸려면를 입력 합니다.  
  
```  
repair disk=4  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

