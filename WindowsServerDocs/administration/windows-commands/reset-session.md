---
title: reset session
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 67a4e910ba87209c9700f2242f7859a6cc9e725f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384532"
---
# <a name="reset-session"></a>reset session

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 세션을 다시 설정 (삭제) 할 수 있습니다.  
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.  

> [!NOTE]  
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.  

## <a name="syntax"></a>구문  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

## <a name="parameters"></a>매개 변수  

|매개 변수|설명|  
|-------|--------|  
|\< 세션 이름 >|다시 설정 하려면 세션의 이름을 지정 합니다. 세션의 이름을 확인 하려면는 **세션 쿼리** 명령입니다.|  
|\<SessionID >|다시 설정 하는 세션의 ID를 지정 합니다.|  
|/server: \<ServerName >|다시 설정 하려는 세션에 있는 터미널 서버를 지정 합니다. 그렇지 않으면 현재 rd 세션 호스트 서버가 사용 됩니다.|  
|/v|수행 중인 작업에 대 한 정보를 표시 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  

## <a name="remarks"></a>설명  
-   언제 든 사용자 자신의 세션 다시 설정할 수 있지만 대 한 모든 액세스 권한을 다른 사용자의 세션을 다시 설정 사용 권한이 있어야 합니다.  
-   수를 사용자에 게 경고 없이 사용자의 세션을 다시 설정 하는 세션에서 데이터가 손실 될 수 있습니다.  
-   세션을 다시 설정 해야 작동 하지 않거나 응답을 멈춘 경우에 있습니다.  
-   **/server** 매개 변수는 사용 하는 경우에 필요 **세션 다시 설정** 원격 서버에서.  

## <a name="BKMK_examples"></a>예와  
- 지정 된 rdp-tcp #6 세션을 다시 설정 하려면 다음을 입력 합니다.  
  ```  
  reset session rdp-tcp#6  
  ```  
- 세션 ID가 3을 사용 하 여 세션을 다시 설정 하려면 다음을 입력 합니다.  
  ```  
  reset session 3  
  ```  

#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
[원격 데스크톱 서비스 &#40;터미널 서비스&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)  
