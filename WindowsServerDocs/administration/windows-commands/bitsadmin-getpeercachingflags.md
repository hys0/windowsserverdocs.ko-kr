---
title: bitsadmin getpeercachingflags
description: Windows 명령 항목에 대 한 **bitsadmin getpeercachingflags** -작업의 파일을 캐시 동료에 게 제공 하 고 하 고 BITS 피어에서 작업에 대 한 콘텐츠를 다운로드 하는 경우를 결정 하는 플래그를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eabcc5cacdcc5f7f4de7178b5afeff2acc89d7a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862814"
---
#<a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

작업의 파일을 캐시 하 고 동료에 게 제공 하 고 BITS 피어에서 작업에 대 한 콘텐츠를 다운로드 하는 경우를 결정 하는 플래그를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetPeerCachingFlags <Job> 
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예제
다음 예제에서는 검색 이라는 작업에 대 한 플래그 *myJob*합니다.

```
C:\>bitsadmin /GetPeerCachingFlags myJob
```

## <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)


