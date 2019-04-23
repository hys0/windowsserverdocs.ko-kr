---
title: nslookup server
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52a846b1084380d0b40d58d81c11d20dacb407bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869154"
---
# <a name="nslookup-server"></a>nslookup server

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 도메인 이름 시스템 (DNS) 도메인에 기본 서버를 변경합니다.
## <a name="syntax"></a>구문
```
server <DNSDomain>
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|<DNSDomain>|필수. 기본 서버에 대 한 새 DNS 도메인을 지정합니다.|
|{도움말 및 #124;?}|간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.|
## <a name="remarks"></a>설명
-   **서버** 명령은 현재의 기본 서버를 사용 하 여 지정된 된 DNS 도메인에 대 한 정보를 조회 합니다. 이 달리는 **lserver** 초기 서버를 사용 하는 명령입니다.
## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[nslookup lserver](nslookup-lserver.md)
