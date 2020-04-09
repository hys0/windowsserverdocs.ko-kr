---
title: ftp prompt_1
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d16f70226e91e2e845480be8d83481fd76af173
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843156"
---
# <a name="ftp-prompt_1"></a>ftp: prompt_1

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**프롬프트** 모드를 설정 및 해제 합니다.   
## <a name="syntax"></a>구문  
```  
prompt  
```  
#### <a name="parameters"></a>매개 변수  
없음  
## <a name="remarks"></a>주의  
- 기본적으로 **prompt** 는 on입니다.  
- 파일을 선택적으로 검색 하거나 저장할 수 있도록 여러 파일을 전송 하는 동안 **ftp** 프롬프트가 표시 됩니다.  **Mget** 및 **mput** 모든 파일 전송 ( **프롬프트가** 꺼져 있는 경우)  
  ## <a name="examples"></a><a name=BKMK_Examples></a>예와  
  프롬프트 모드를 설정 및 해제 합니다.  
  ```  
  prompt  
  ```  
  ## <a name="additional-references"></a>추가 참조  
- - [명령줄 구문 키](command-line-syntax-key.md)  
