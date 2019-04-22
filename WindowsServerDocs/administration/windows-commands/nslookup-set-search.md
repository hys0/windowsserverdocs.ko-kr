---
title: nslookup set search
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf952a0337e23c0426265c6c0a4a8387a6ab45e1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816994"
---
# <a name="nslookup-set-search"></a>nslookup set search



응답을 받을 때까지 요청에 DNS 도메인 검색 목록에서 도메인 이름 시스템 (DNS) 도메인 이름을 추가 합니다. 집합과 조회 요청 하나 이상의 기간을 포함 하는 경우에 적용 됩니다 있지만 뒤에 마침표 종료 하지 마십시오.

## <a name="syntax"></a>구문

```
set [no]search
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|**nosearch**|요청에 있는 DNS 도메인 검색 목록에 도메인 이름 시스템 (DNS) 도메인 이름 추가 중지 합니다.|
|**search**|응답을 받을 때까지 요청에 DNS 도메인 검색 목록에서 도메인 이름 시스템 (DNS) 도메인 이름을 추가 합니다. 기본 구문은 **검색**합니다.|
|{도움말 | ?}|간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)