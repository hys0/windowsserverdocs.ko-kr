---
title: 도움말
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75dbf94f-d79c-45b2-9463-c06648218f4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 404cefe879e8f63678f2cba90516fad9c216eb23
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842316"
---
# <a name="help"></a>도움말

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정한 명령에 사용할 수 있는 명령 또는 자세한 도움말 정보 목록을 표시합니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
help [<command>]  
```  
  
### <a name="parameters"></a>매개 변수  
  
| 매개 변수 |                              설명                              |
|-----------|-----------------------------------------------------------------------|
| <command> | 자세한 도움말 정보를 표시 하는 명령을 지정 합니다. |
  
## <a name="remarks"></a>주의  
  
-   명령을 지정 하지 않으면 가능한 모든 명령이 **도움말** 에 표시 됩니다.  
  
## <a name="examples"></a><a name=BKMK_examples></a>예와  
DiskPart에서 사용할 수 있는 모든 명령 목록을 표시 하려면 다음을 입력 합니다.  
  
```  
help  
```  
  
사용 하는 방법에 대 한 자세한 도움말 정보를 표시 하는 **파티션을 주 만들** 형식 DiskPart 명령을:  
  
```  
help create partition primary  
```  
  
## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
  

  

