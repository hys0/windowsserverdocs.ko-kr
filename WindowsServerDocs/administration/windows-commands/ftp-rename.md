---
title: ftp 이름 바꾸기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 80d1a15f038017444c7654a44748bfd22be8e487
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438386"
---
# <a name="ftp-rename"></a>ftp: 이름 바꾸기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 파일을 이름을 바꿉니다.   
## <a name="syntax"></a>구문  
```  
rename <FileName> <NewFileName>  
```  
### <a name="parameters"></a>매개 변수  

|   매개 변수   |                 설명                 |
|---------------|---------------------------------------------|
|  <FileName>   | 이름을 바꿀 파일을 지정 합니다. |
| <NewFileName> |        새 파일 이름을 지정합니다.         |

## <a name="BKMK_Examples"></a>예제  
원격 파일 이름 바꾸기 **example.txt** 에 **example1.txt**  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
