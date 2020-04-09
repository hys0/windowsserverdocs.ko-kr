---
title: set_2
description: 섀도 복사본 만들기에 대 한 컨텍스트, 옵션, 자세한 정보 표시 모드 및 메타 데이터 파일을 설정 하는 set_2에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: acf24663-1a50-4321-b48d-1717655e9476
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fa467625997824a11b2303572a063d591f59bdd6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834386"
---
# <a name="set_2"></a>set_2

상황에 맞는, 옵션, 세부 정보 표시 모드 및 섀도 복사본 만들기에 대 한 메타 데이터 파일을 설정합니다. 매개 변수 없이 사용 하는 경우 **설정** 모든 현재 설정을 표시 합니다.

## <a name="syntax"></a>구문

```
set
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
set verbose {on|off}
set metadata <MetaData.cab>
```

## <a name="set-sub-commands"></a>하위 명령 설정

|하위 명령|설명|
|-----------|-----------|
|context|섀도 복사본 만들기에 대 한 컨텍스트를 설정합니다. 참조 [컨텍스트 설정](set-context.md) 구문 및 매개 변수입니다.|
|옵션|섀도 복사본 만들기에 대 한 옵션을 설정합니다. 참조 [옵션을 설정](set-option.md) 구문 및 매개 변수입니다.|
|자세한 정보 표시|자세한 정보를 출력 모드를 설정 하거나 해제 합니다. 참조 [verbose 설정](set-verbose.md) 구문 및 매개 변수입니다.|
|metadata|이름 및 그림자 만들기 메타 데이터 파일의 위치를 설정합니다. 참조 [메타 데이터 설정](set-metadata.md) 구문 및 매개 변수입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)