---
title: ftp 이름 바꾸기
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5dc5006c82df8417a8652a9c0ba20f7f1a002e7f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725105"
---
# <a name="ftp-rename"></a>ftp: 이름 바꾸기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 파일의 이름을 바꿉니다.   
## <a name="syntax"></a>구문  
```  
rename <FileName> <NewFileName>  
```  
#### <a name="parameters"></a>매개 변수  

|   매개 변수   |                 설명                 |
|---------------|---------------------------------------------|
|  <FileName>   | 이름을 바꿀 파일을 지정 합니다. |
| <NewFileName> |        새 파일 이름을 지정합니다.         |

## <a name="examples"></a>예  
원격 파일의 **예 .txt** 를 **example1** 로 바꿉니다.  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
