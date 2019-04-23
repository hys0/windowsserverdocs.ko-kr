---
title: ascii ftp
description: 'Windows 명령 항목에 대 한 ftp ascii '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7bcca3f29cec8ff5c30256dfd123acc7fbb804d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849194"
---
# <a name="ftp-ascii"></a>ftp: ascii

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ASCII 파일 전송 유형을 설정합니다.   
## <a name="syntax"></a>구문  
```  
ascii  
```  
### <a name="parameters"></a>매개 변수  
none  
## <a name="remarks"></a>설명  
-   기본 파일 전송 유형이 ASCII입니다.  
-   ASCII 모드에서는 네트워크 표준 문자 집합 사이에 문자 변환이 수행 됩니다. 예를 들어, 줄의 끝 문자는 대상 운영 체제에 따라 필요에 따라 변환 됩니다.  
-   **ftp** ASCII 및 이진 이미지 파일 전송 형식을 모두 지원 합니다. ASCII 텍스트 파일을 전송할 때 사용 합니다. 이진 파일 전송에 대 한 자세한 내용은 참조 하세요. **ftp: 이진** 추가 참조 합니다.  
## <a name="BKMK_Examples"></a>예제  
ASCII 파일 전송 유형을 설정 합니다.  
```  
ascii  
```  
## <a name="additional-references"></a>추가 참조  
-   [ftp: binary](ftp-binary.md)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
