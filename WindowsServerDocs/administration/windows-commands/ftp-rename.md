---
title: ftp 이름 바꾸기
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 977baa042a6b0d9c23db7cb398bee997c2049227
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376021"
---
# <a name="ftp-rename"></a>ftp: 이름 바꾸기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 파일의 이름을 바꿉니다.   
## <a name="syntax"></a>구문  
```  
rename <FileName> <NewFileName>  
```  
### <a name="parameters"></a>매개 변수  

|   매개 변수   |                 설명                 |
|---------------|---------------------------------------------|
|  <FileName>   | 이름을 바꿀 파일을 지정 합니다. |
| <NewFileName> |        새 파일 이름을 지정합니다.         |

## <a name="BKMK_Examples"></a>예와  
원격 파일의 **예 .txt** 를 **example1** 로 바꿉니다.  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
