---
title: cmdkey
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7080a3ae28fed722f17cf8311aa1e2fd3bece41f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854614"
---
# <a name="cmdkey"></a>cmdkey

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

저장된 사용자 이름과 암호 또는 자격 증명을 만들고 나열하고 삭제합니다.

## <a name="syntax"></a>구문
```
cmdkey [{/add:<TargetName>|/generic:<TargetName>}] {/smartcard|/user:<UserName> [/pass:<Password>]} [/delete{:<TargetName>|/ras}] /list:<TargetName>
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/add:<TargetName>|사용자 이름 및 암호를 목록에 추가합니다.<br /><br />매개 변수가 필요 <TargetName> 이 항목은 연결 하는 컴퓨터 또는 도메인 이름을 식별 합니다.|
|/generic:<TargetName>|목록에 일반 자격 증명을 추가합니다.<br /><br />매개 변수가 필요 <TargetName> 이 항목은 연결 하는 컴퓨터 또는 도메인 이름을 식별 합니다.|
|/smartcard|스마트 카드에서 자격 증명을 검색합니다.|
|/user:<UserName>|이 항목을 사용 하 여 저장할 사용자 또는 계정 이름을 지정 합니다. 하는 경우 *UserName* 는 제공 되지 않으면이 요청 됩니다.|
|/pass:<Password>|이 항목을 사용 하 여 저장할 암호를 지정 합니다. 하는 경우 *암호* 는 제공 되지 않으면이 요청 됩니다.|
|삭제/{0}:<TargetName> &#124; /ras}|목록에서 사용자 이름 및 암호를 삭제합니다. 하는 경우 *TargetName* 를 지정 하면 해당 항목은 삭제 됩니다. /Ras 지정 된 경우 저장 된 원격 액세스 항목이 삭제 됩니다.|
|/list:<TargetName>|저장 된 사용자 이름 및 자격 증명의 목록을 표시합니다. 하는 경우 *TargetName* 지정, 모든 저장 된 사용자 이름이 아니며 자격 증명에 나열 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="remarks"></a>설명
-   /smartcard 명령줄 옵션을 사용 하는 경우 시스템에서 둘 이상의 스마트 카드를 찾으면 **cmdkey** 모든 사용 가능한 스마트 카드에 대 한 정보를 표시 되며 다음 묻는 메시지를 사용 하는 하나를 지정 합니다.
-   암호는 저장 되 면 표시 되지 않습니다.
## <a name="BKMK_examples"></a>예제
모든 사용자 이름 및 저장 된 자격 증명의 목록을 표시 하려면 다음을 입력 합니다.
```
cmdkey /list
```
사용자 이름 및 사용자 Mikedan에 대 한 암호를 Kleo 암호를 사용 하 여 Server01 컴퓨터 액세스에 추가 하려면 다음을 입력 합니다.
```
cmdkey /add:server01 /user:mikedan /pass:Kleo
```
Server01 액세스할 때마다 사용자 이름 및 사용자 Mikedan Server01 컴퓨터에 액세스 하는 암호 및 암호에 대 한 프롬프트를 추가 하려면 다음을 입력 합니다.
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
