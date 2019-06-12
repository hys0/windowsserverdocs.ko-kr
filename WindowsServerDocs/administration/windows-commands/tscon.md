---
title: tscon
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d8cac59b2f5524df5a82e9c83424fd781f0ef7c8
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440929"
---
# <a name="tscon"></a>tscon

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 다른 세션에 연결합니다.  
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.  

> [!NOTE]  
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.  

## <a name="syntax"></a>구문  
```  
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]  
```  
## <a name="parameters"></a>매개 변수  

|매개 변수|설명|  
|-------|--------|  
|\<SessionID>|연결 하려는 세션의 ID를 지정 합니다. 옵션을 사용 하는 경우 **/dest:** <*SessionName*> 매개 변수를 연결 하려는 세션의 ID입니다.|  
|\<SessionName>|연결 하려는 세션의 이름을 지정 합니다.|  
|/dest:\<SessionName>|현재 세션의 이름을 지정합니다. 새 세션에 연결할 때이 세션 연결을 끊습니다.|  
|/password:\<pw>|연결 하려는 세션을 소유 하는 사용자의 암호를 지정 합니다. 이 암호는 연결 하는 사용자 세션을 소유 하지 않는 경우에 필요 합니다.|  
|/password:*|연결 하려는 세션을 소유 하는 사용자의 암호에 대 한 메시지를 표시 합니다.|  
|/v|수행 중인 작업에 대 한 정보를 표시 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  

## <a name="remarks"></a>설명  
-   모든 권한 액세스 했거나 다른 세션에 연결 하려면 특별 한 액세스 권한이 연결 해야 합니다.  
-   합니다 **/dest:** <*SessionName*> 매개 변수를 사용 하면 다른 세션에 다른 사용자의 세션을 연결할 수 있습니다.  
-   암호를 지정 하지 않는 경우는 <*암호*> 매개 변수 및 대상 세션이 아닌 현재 사용자에 게 속합니다 **tscon** 실패 합니다.  
-   콘솔 세션에 연결할 수 없습니다.  

## <a name="BKMK_examples"></a>예제  
- 세션 12 현재 rd 세션 호스트 서버에 연결 하 고 현재 세션을 끊고를 하려면 다음을 입력 합니다.  
  ```  
  tscon 12  
  ```  
- Mypass를 사용 하 여 현재 rd 세션 호스트 서버에서의 23 세션에 연결 하 고 현재 세션을 끊고를 하려면 다음을 입력 합니다.  
  ```  
  tscon 23 /password:mypass  
  ```  
- Term03 TERM05, 라는 세션에 세션을 연결 하 고 연결 되어 있는 경우 다음 TERM05, 세션 연결 끊기를 하려면 다음을 입력 합니다.  
  ```  
  tscon TERM03 /v /dest:TERM05  
  ```  
  #### <a name="additional-references"></a>추가 참조  
  [명령줄 구문 키](command-line-syntax-key.md)  
  [원격 데스크톱 서비스 &#40;터미널 서비스&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)  
