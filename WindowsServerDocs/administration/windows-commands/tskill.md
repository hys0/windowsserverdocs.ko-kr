---
title: tskill
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 697363c91837ff675a14099fd212f4f0753b739b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392336"
---
# <a name="tskill"></a>tskill

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에서 세션에서 실행 중인 프로세스를 종료 합니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|\<ProcessID >|종료 하려는 프로세스의 ID를 지정 합니다.|
|@no__t 0ProcessName >|종료 하려는 프로세스의 이름을 지정 합니다. 이 매개 변수는 와일드 카드 문자를 포함할 수 있습니다.|
|/server: \<ServerName >|종료 하려는 프로세스가 포함 된 터미널 서버를 지정 합니다. **/Server** 를 지정 하지 않으면 현재 RD 세션 호스트 서버가 사용 됩니다.|
|/id: \<SessionID >|지정 된 세션에서 실행 중인 프로세스를 종료 합니다.|
|/ a|모든 세션에서 실행 중인 프로세스를 종료 합니다.|
|/v|수행 중인 작업에 대 한 정보를 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
- **Tskill** 를 사용 하 여 관리자가 아닌 사용자에 게 속하는 프로세스만 종료할 수 있습니다. 관리자는 모든 **tskill** 기능에 대 한 모든 권한을 가지 며 다른 사용자 세션에서 실행 중인 프로세스를 종료할 수 있습니다.
- 세션 끝에서 실행 되는 모든 프로세스가 종료 되 면 세션도 종료 됩니다.
- *ProcessName* 및 **/server:** <em>ServerName</em> 매개 변수를 사용 하는 경우에도 **/id:** <em>SessionID</em> 또는 **/a** 매개 변수를 지정 해야 합니다.

## <a name="BKMK_examples"></a>예와
- 프로세스 6543을 종료 하려면 다음을 입력 합니다.
  ```
  tskill 6543
  ```
- 세션 5에서 실행 중인 "explorer" 프로세스를 종료 하려면 다음을 입력 합니다.
  ```
  tskill explorer /id:5
  ```
  #### <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
  [원격 데스크톱 서비스&#40; 터미널 서비스 및&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
