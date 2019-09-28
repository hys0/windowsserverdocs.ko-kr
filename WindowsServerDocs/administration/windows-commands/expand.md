---
title: expand
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a88222ffe9ff374626a6406c330a6660d992f96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377325"
---
# <a name="expand"></a>expand

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

하나 이상의 압축 된 파일을 확장 합니다. 설치 디스크에서 압축 된 파일을 검색 하려면이 명령을 사용할 수 있습니다.  
## <a name="syntax"></a>구문  
```  
expand [/r] <source> <destination>  
expand /r <source> [<destination>]  
expand /i <source> [<destination>]  
expand /d <source>.cab [/f:<files>]  
expand <source>.cab /f:<files> <destination>  
```  
### <a name="parameters"></a>매개 변수  

|  매개 변수  |                                                                                                                                                                   설명                                                                                                                                                                    |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /r      |                                                                                                                                                             확장 된 파일의 이름을 바꿉니다.                                                                                                                                                              |
|   원본    |                                                                              압축을 풀 파일을 지정 합니다. *소스* 드라이브 문자 및 콜론, 디렉터리 이름, 파일 이름, 또는 이들의 조합으로 구성 될 수 있습니다. 와일드 카드 ( **\\** \* 또는 **?** )를 사용할 수 있습니다.                                                                               |
| destination | 확장 하는 파일의 위치를 지정 합니다.<br /><br />*원본이* 여러 파일로 구성 되어 있고 **/r**을 지정 하지 않은 경우 *destination* 은 디렉터리 여야 합니다.<br /><br />*대상* 드라이브 문자 및 콜론, 디렉터리 이름, 파일 이름, 또는 이들의 조합으로 구성 될 수 있습니다.<br /><br />대상 파일 및 #124; 경로 지정 합니다. |
|     /i      |                                                                                                   확장 된 파일의 이름을 변경 하지만 디렉터리 구조는 무시 합니다.<br /><br />이 매개 변수는 다음에 적용 됩니다.  Windows Server 2008 R2 및 Windows 7                                                                                                    |
|     /d      |                                                                                                                              원본 위치에서 파일 목록을 표시합니다. 확장 하거나 파일을 추출 하지 않습니다.                                                                                                                              |
|     /f:     |                                                                                                                 확장 하려는 캐비닛 (.cab) 파일에 파일을 지정 합니다. 와일드 카드 ( **\\** \* 또는 **?** )를 사용할 수 있습니다.                                                                                                                 |
|     /?      |                                                                                                                                                       명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                       |

## <a name="remarks"></a>설명  
- 복구 콘솔에서 **확장** 사용  
  다른 매개 변수를 사용 하 여 **확장** 명령을 복구 콘솔에서 사용할 수 있습니다. 복구 콘솔에 대 한 자세한 내용은 Microsoft 기술 자료 [문서 314058](https://support.microsoft.com/kb/314058) 를 참조 하십시오.  
  ## <a name="additional-references"></a>추가 참조  
  [명령줄 구문 키](command-line-syntax-key.md)  
