---
title: irftp
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad8a0b9b49d90223f830081f5a99c40995d9e4ef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375357"
---
# <a name="irftp"></a>irftp

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

적외선 연결을 통해 파일을 전송합니다.    
## <a name="syntax"></a>구문  
```  
irftp [<Drive>:\] [[<path>] <FileName>] [/h][/s]  
```  

### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|Drive: \|은 적외선 링크를 통해 전송 하려는 파일이 포함 된 드라이브를 지정 합니다.|  
|path 이름도|파일의 이름 또는 집합 적외선 연결을 통해 전송 하려는 경우 파일의 위치를 지정 합니다. 파일 집합을 지정 하면 각 파일에 대 한 전체 경로 지정 해야 합니다.|  
|/h|숨김된 모드를 지정합니다. 숨김된 모드를 사용 하면 무선 연결 대화 상자를 표시 하지 않고 파일 전송 됩니다.|  
|/s|파일 또는 명령줄을 사용 하 여 드라이브, 경로 및 파일 이름을 지정 하지 않고 전송 하려는 경우 파일 집합을 선택할 수 있도록 무선 연결 대화 상자를 엽니다.|  

## <a name="remarks"></a>설명  
-   이 명령을 사용 하기 전에 적외선 연결을 통해 통신 하려는 장치 적외선 기능이 및 제대로 작동 했는지와 적외선 연결 장치 사이 설정 되어 있는지 확인 합니다.  
-   매개 변수 없이 사용 하거나 사용해 서 **/s**, **irftp** 열립니다는 **무선 연결** 대화 상자에서 파일을 명령줄을 사용 하지 않고 전송 하려는 경우를 선택할 수 있습니다.  

## <a name="BKMK_Examples"></a>예와  
Example.txt 적외선 연결을 통해 보냅니다.  
```  
irftp c:\example.txt  
```  

## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
