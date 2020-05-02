---
title: ftp 유형
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5531da30118914599ed0f85bfd10bd02ae89ffcf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725082"
---
# <a name="ftp-type"></a>ftp: 형식

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

설정 하거나 파일 전송 유형을 표시 합니다.   
## <a name="syntax"></a>구문  
```  
type [<typeName>]  
```  
#### <a name="parameters"></a>매개 변수  

|  매개 변수   |            설명            |
|--------------|-----------------------------------|
| [<typeName>] | 파일 전송 유형을 지정합니다. |

## <a name="remarks"></a>설명  
- *typeName* 을 지정 하지 않으면 현재 형식이 표시 됩니다.  
- **ftp** 는 ASCII 및 이진 이라는 두 가지 파일 전송 형식을 지원 합니다.  
  기본 파일 전송 유형이 ASCII입니다.  **ascii** 명령은 텍스트 파일을 전송할 때 사용 됩니다. ASCII 모드에서는 네트워크 표준 문자 집합 사이에 문자 변환이 수행 됩니다. 줄 끝 문자 그대로 변환 되는 예를 들어 대상에서 운영 체제에 따라, 필요 합니다.  
  **이진** 명령은 실행 파일을 전송할 때 사용 해야 합니다. 이진 모드 파일은 1 바이트 단위로 이동 됩니다.  
  ## <a name="examples"></a>예  
  ASCII 파일 전송 유형을 설정 합니다.  
  ```  
  type ascii  
  ```  
  이진 파일 형식을 전송 설정 합니다.  
  ```  
  type binary  
  ```  
  ## <a name="additional-references"></a>추가 참조  
- - [명령줄 구문 키](command-line-syntax-key.md)  
