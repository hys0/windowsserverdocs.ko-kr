---
title: ftp 이름 바꾸기
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bbe159f2833ce52921b46e46881a1d7aed8c5df8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843026"
---
# <a name="ftp-rename"></a>ftp: 이름 바꾸기

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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

## <a name="examples"></a><a name=BKMK_Examples></a>예와  
원격 파일의 **예 .txt** 를 **example1** 로 바꿉니다.  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
