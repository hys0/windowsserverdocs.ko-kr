---
title: nslookup set class
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e02a6f473a7c2dc6d6b66eb5b23fded930bc817
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856354"
---
# <a name="nslookup-set-class"></a>nslookup set class



쿼리 클래스를 변경 합니다. 클래스는 프로토콜 그룹 정보를 지정합니다.

## <a name="syntax"></a>구문

```
set class=<Class>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<클래스 >|기본 클래스는 IN입니다. 다음은이 명령에 대 한 유효한 값을 나열 합니다.</br>-에: 인터넷 클래스를 지정합니다.</br>- CHAOS: 혼돈 클래스를 지정합니다.</br>- HESIOD: Athena Hesiod 클래스를 지정합니다.</br>-모든: 앞에 나열 된 와일드 카드 중 하나를 지정 합니다.|
|{도움말 | ?}|간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.|

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)