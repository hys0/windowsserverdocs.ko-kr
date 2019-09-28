---
title: tlntadmn
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78b61e8d-b953-44bb-8d57-f3b42da9e7a8 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1218a0238f90403edcd04db447ceeac1e10a1fdf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385735"
---
# <a name="tlntadmn"></a>tlntadmn

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

텔넷 서버 서비스를 실행 하는 로컬 또는 원격 컴퓨터를 관리 합니다.   
## <a name="syntax"></a>구문  
```  
tlntadmn [<computerName>] [-u <UserName>] [-p <Password>] [{start | stop | pause | continue}] [-s {<SessionID> | all}] [-k {<SessionID> | all}] [-m {<SessionID> | all}  <Message>] [config [dom = <Domain>] [ctrlakeymap = {yes | no}] [timeout = <hh>:<mm>:<ss>] [timeoutactive = {yes | no}] [maxfail = <attempts>] [maxconn = <Connections>] [port = <Number>] [sec {+ | -}NTLM {+ | -}passwd] [mode = {console | stream}]] [-?]  
```  
### <a name="parameters"></a>매개 변수  

|                   매개 변수                    |                                                                                                                                                       설명                                                                                                                                                        |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                \<computerName >                 |                                                                                                                    연결할 서버의 이름을 지정 합니다. 기본값은 로컬 컴퓨터입니다.                                                                                                                    |
|         -u \<UserName >-p \<Password >          |                                                관리 하려는 원격 서버에 대 한 관리 자격 증명을 지정 합니다. 이 매개 변수는 없는 하지 로그온 관리 자격 증명으로는 원격 서버를 관리 하려는 경우에 필요 합니다.                                                |
|                     start                      |                                                                                                                                            텔넷 서버 서비스를 시작 합니다.                                                                                                                                             |
|                      stop                      |                                                                                                                                             텔넷 서버 서비스를 중지 합니다.                                                                                                                                              |
|                     일시 중지                      |                                                                                                                          텔넷 서버 서비스를 일시 중지 합니다. 새 연결이 허용 됩니다.                                                                                                                          |
|                    계속 해 서                    |                                                                                                                                            텔넷 서버 서비스를 다시 시작 합니다.                                                                                                                                            |
|          -s {\<SessionID > &#124; all}          |                                                                                                                                             활성 텔넷 세션을 표시 합니다.                                                                                                                                             |
|          -k {\<SessionID > &#124; all}          |                                                                                                        텔넷 세션을 종료 합니다. 세션 ID를 입력 하 여 특정 세션을 종료 하거나 모두를 입력 하 여 모든 세션을 종료 합니다.                                                                                                         |
|    -m {\<SessionID > &#124; all} <Message>     |                                                   하나 이상의 세션에 메시지를 보냅니다. 특정 세션에 메시지를 보낼 세션 ID를 입력 하거나 모든 세션에 메시지를 보내려면 모두를 입력 합니다. 따옴표 사이에 보내려는 메시지를 입력 합니다.                                                   |
|             구성 dom = \<Domain >             |                                                                                                                                      서버에 대 한 기본 도메인을 구성합니다.                                                                                                                                       |
|      config ctrlakeymap = {예 &#124; 아니요}      |                                                                                     텔넷 서버에서 CTRL + A를 ALT로 해석할지 여부를 지정 합니다. **예** 를 입력 하 여 바로 가기 키를 매핑하거나 **no** 를 입력 하 여 매핑을 방지 합니다.                                                                                     |
|       config timeout = \<hh >: \<mm >: \<ss >       |                                                                                                                                 시, 분 및 초 시간 제한 기간을 설정합니다.                                                                                                                                 |
|     config timeoutactive = {예 &#124; 아니요      |                                                                                                                                            유휴 세션 제한 시간을 수 있습니다.                                                                                                                                             |
|          구성 maxfail = \< 회 시도 >          |                                                                                                                          연결을 끊기 전에 실패 한 로그온 시도의 최대 수를 설정 합니다.                                                                                                                          |
|        구성 maxconn = \<Connections >         |                                                                                                                                         최대 연결 수를 설정합니다.                                                                                                                                          |
|            구성 포트 = < \Number >             |                                                                                                                    텔넷 포트를 설정 합니다. 포트 1024 보다 작은 정수를 지정 해야 합니다.                                                                                                                    |
| config sec {+ &#124;-} NTLM {+ &#124;-} passwd | 로그온 시도 인증에 NTLM, 암호 또는 둘 다 사용 하 여 지정 합니다. 특정 유형의 인증을 사용 하려면 더하기 기호를 입력 ( **+** ) 형식 앞에 인증 합니다. 특정 형식의 인증을 사용 하 여를 방지 하려면 빼기 기호를 입력 ( **-** ) 형식 앞에 인증 합니다. |
|     구성 모드 = {콘솔 &#124; 스트림}      |                                                                                                                                             작업 모드를 지정합니다.                                                                                                                                             |
|                       -?                       |                                                                                                                                           명령 프롬프트에 도움말을 표시합니다.                                                                                                                                           |

## <a name="remarks"></a>설명  
-   서버 설정을 표시 하려면 입력 **tlntadmn** 매개 변수 없이 합니다.  
-   사용 하 여 **tlntadmn** 명령, 관리자 자격 증명으로 로컬 컴퓨터에 로그온 해야 합니다. 원격 컴퓨터를 관리 하려면 또한 원격 컴퓨터에 대 한 관리 자격 증명을 제공 해야 합니다. 로컬 컴퓨터와 원격 컴퓨터에 대 한 관리 자격 증명이 있는 계정으로 로컬 컴퓨터에 로그온 하 여 이렇게 수 있습니다. 이 메서드를 사용할 수 없는 경우 사용할 수 있습니다는 **-u** 및 **-p** 매개 변수를 원격 컴퓨터에 대 한 관리 자격 증명을 제공 합니다.  

## <a name="BKMK_Examples"></a>예와  
30 분으로 유휴 세션 제한 시간을 구성 합니다.  
```  
tlntadmn config timeout=0:30:0  
```  
활성 텔넷 세션을 표시 합니다.  
```  
tlntadmn -s  
```  

## <a name="additional-references"></a>추가 참조  
-   [텔넷 운영 가이드](https://technet.microsoft.com/library/cc753164(v=ws.10).aspx)  
-   [명령줄 구문 키](command-line-syntax-key.md)  
