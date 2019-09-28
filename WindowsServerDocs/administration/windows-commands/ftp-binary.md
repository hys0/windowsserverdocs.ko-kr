---
title: ftp 이진 파일
description: Ftp 이진에 대 한 Windows 명령 항목
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 48579523f44232dec3357a20e8082050cc5175e6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376577"
---
# <a name="ftp-binary"></a>ftp: 이진

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파일 전송 형식을 이진으로 설정 합니다.   
## <a name="syntax"></a>구문  
```  
binary  
```  
### <a name="parameters"></a>매개 변수  
없음  
## <a name="remarks-optional-section"></a>설명 <optional section>  
**ftp** 는 ASCII 및 이진 이미지 파일 전송 형식을 모두 지원 합니다. 실행 파일을 전송할 때 binary를 사용 합니다. 이진 모드에서 파일은 1 바이트 단위로 전송 됩니다. ASCII 파일 전송에 대 한 자세한 내용은 추가 참조에서 **ftp: ASCII** 를 참조 하세요.  
## <a name="BKMK_Examples"></a>예와  
파일 전송 유형을 이진으로 설정 합니다.  
```  
binary  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: ascii](ftp-ascii.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
