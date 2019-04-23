---
title: bitsadmin getsecurityflags
description: Windows 명령 항목에 대 한 **bitsadmin getsecurityflags** -URL 리디렉션에 대 한 HTTP 보안 플래그를 보고 하 고 전송 하는 동안 서버 인증서의 수행을 확인 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97d889b54c4b0de0230c50e1d7c8d21617ea881a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835854"
---
#<a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

URL 리디렉션 및 검사에 대 한 보안 플래그 보고서 HTTP 전송 하는 동안 서버 인증서에서 수행 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetSecurityFlags <Job> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제
다음 예제에서는 명명 된 작업에서 securitly 플래그를 검색 *myJob*합니다.

```
C:\>bitsadmin /GetSecurityFlags myJob 
```

## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)


