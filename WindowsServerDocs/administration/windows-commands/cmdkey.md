---
title: cmdkey
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fcd68ee-a14a-4b71-9300-c3f5c5d31e8e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc2b12cb53eef930d05c1e291de5574a8ba94306
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379311"
---
# <a name="cmdkey"></a>cmdkey

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

저장된 사용자 이름과 암호 또는 자격 증명을 만들고 나열하고 삭제합니다.

## <a name="syntax"></a>구문
```
cmdkey [{/add:<TargetName>|/generic:<TargetName>}] {/smartcard|/user:<UserName> [/pass:<Password>]} [/delete{:<TargetName>|/ras}] /list:<TargetName>
```
## <a name="parameters"></a>매개 변수

|             매개 변수             |                                                                                    설명                                                                                     |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         /add: <TargetName>          | 사용자 이름 및 암호를 목록에 추가 합니다.<br /><br />에는이 항목을 연결할 컴퓨터 또는 도메인 이름을 식별 하는 <TargetName>의 매개 변수가 필요 합니다. |
|       /generic: <TargetName>        |   일반 자격 증명을 목록에 추가 합니다.<br /><br />에는이 항목을 연결할 컴퓨터 또는 도메인 이름을 식별 하는 <TargetName>의 매개 변수가 필요 합니다.    |
|             /smartcard             |                                                                    스마트 카드에서 자격 증명을 검색 합니다.                                                                     |
|          /user: <UserName>          |                                 이 항목과 함께 저장할 사용자 또는 계정 이름을 지정 합니다. *사용자 이름을* 제공 하지 않으면 요청 됩니다.                                  |
|          /pass: <Password>          |                                       이 항목과 함께 저장할 암호를 지정 합니다. *암호* 를 제공 하지 않으면 요청 됩니다.                                        |
| /delete{: <TargetName> &#124; /ras} |  목록에서 사용자 이름 및 암호를 삭제 합니다. *TargetName* 을 지정 하면 해당 항목이 삭제 됩니다. /Ras가 지정 된 경우에는 저장 된 원격 액세스 항목이 삭제 됩니다.   |
|         /list: <TargetName>         |                  저장 된 사용자 이름 및 자격 증명 목록을 표시 합니다. *TargetName* 을 지정 하지 않으면 저장 된 모든 사용자 이름 및 자격 증명이 나열 됩니다.                   |
|                 /?                 |                                                                        명령 프롬프트에 도움말을 표시합니다.                                                                        |

## <a name="remarks"></a>설명
- /smartcard 명령줄 옵션을 사용 하는 경우 시스템에 둘 이상의 스마트 카드가 있으면 **cmdkey** 는 사용 가능한 모든 스마트 카드에 대 한 정보를 표시 한 다음 사용자에 게 사용할 항목을 지정 하 라는 메시지를 표시 합니다.
- 암호는 저장 된 후에는 표시 되지 않습니다.
  ## <a name="BKMK_examples"></a>예와
  저장 된 모든 사용자 이름 및 자격 증명 목록을 표시 하려면 다음을 입력 합니다.
  ```
  cmdkey /list
  ```
  Password Kleo를 사용 하 여 computer Server01에 액세스 하는 사용자 Mikedan에 대 한 사용자 이름 및 암호를 추가 하려면 다음을 입력 합니다.
  ```
  cmdkey /add:server01 /user:mikedan /pass:Kleo
  ```
  사용자 Mikedan의 사용자 이름 및 암호를 추가 하 여 computer Server01에 액세스 하 고 Server01에 액세스할 때마다 암호를 묻는 메시지를 표시 하려면 다음을 입력 합니다.
  ```
  cmdkey /add:server01 /user:mikedan
  ```
  원격 액세스에 저장 된 자격 증명을 삭제 하려면 다음을 입력 합니다.
  ```
  cmdkey /delete /ras
  ```
  Server01에 대해 저장 된 자격 증명을 삭제 하려면 다음을 입력 합니다.
  ```
  cmdkey /delete:Server01
  ```
  ## <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
