---
title: cscript
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fba3cbca-594e-4663-bb22-4ee0f63a1ac6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ffdbd6f67e4e4c32022134191deabd861bf248b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827674"
---
# <a name="cscript"></a>cscript

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

명령줄 환경에서 실행 되도록 스크립트를 시작 합니다.
## <a name="syntax"></a>구문
```
cscript <Scriptname.extension> [/B] [/D] [/E:<Engine>] [{/H:cscript|/H:wscript}] [/I] [/Job:<Identifier>] [{/Logo|/NoLogo}] [/S] [/T:<Seconds>] [/X] [/U] [/?] [<ScriptArguments>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|Scriptname.extension|선택적 파일 이름 확장명을 가진 스크립트 파일의 경로 파일 이름을 지정합니다.|
|/B|경고, 스크립팅 오류 또는 입력된 프롬프트를 표시 하지 않는 일괄 처리 모드를 지정 합니다.|
|/D|디버거를 시작 합니다.|
|/E:<Engine>|스크립트를 실행 하는 데 사용 되는 엔진을 지정 합니다.|
|/H:cscript|스크립트를 실행 하는 것에 대 한 기본 스크립트 호스트를 cscript.exe를 등록 합니다.|
|/H:wscript|스크립트를 실행 하는 것에 대 한 기본 스크립트 호스트 wscript.exe를 등록 합니다. 기본값입니다.|
|/I|경고, 스크립팅 오류 및 입력된 프롬프트를 표시 하는 대화형 모드를 지정 합니다. 이 고 기본값의 반대 **/B**합니다.|
|/Job:<Identifier>|로 식별 되는 작업을 실행 *식별자* .wsf 스크립트 파일에 있습니다.|
|/ 로고|스크립트를 실행 하기 전에 Windows 스크립트 호스트 배너 콘솔에 표시 되도록 지정 합니다. 이 고 기본값의 반대 **/Nologo**합니다.|
|/Nologo|스크립트를 실행 하기 전에 Windows 스크립트 호스트 배너가 표시 되지 않도록 지정 합니다.|
|/S|현재 사용자에 대 한 현재 명령 프롬프트 옵션을 저장합니다.|
|/T:<Seconds>|스크립트를 초 단위로 실행할 수 있는 최대 시간을 지정 합니다. 최대 32, 767 초를 지정할 수 있습니다. 기본값은 시간 제한이 없습니다.|
|/U|입력 및 출력을 콘솔에서 리디렉션에 대 한 유니코드를 지정 합니다.|
|/X|디버거에서 스크립트를 시작합니다.|
|/?|사용 가능한 명령 매개 변수를 표시 하 고 사용 하기 위한 도움말을 제공 합니다. 이 입력 동일 **cscript.exe** 매개 변수 없이와 스크립트가 없습니다.|
|ScriptArguments|스크립트에 전달 되는 인수를 지정 합니다. 각 스크립트 인수 뒤에 슬래시와 합니다 (**/**).|
### <a name="remarks"></a>설명
-   이 작업을 수행할 때는 관리 자격 증명이 필요하지 않습니다. 보안을 위해 관리 자격 증명이 없는 사용자로 이 작업을 수행하는 것이 좋습니다.
-   명령 프롬프트를 열려면 합니다 **시작** 화면에서 입력 **cmd**를 클릭 하 고 **명령 프롬프트**합니다.
-   각 매개 변수는 선택 사항입니다. 그러나 스크립트를 지정 하지 않고 스크립트 인수를 지정할 수 없습니다. 스크립트 또는 스크립트의 인수를 지정 하지 않으면 cscript.exe cscript.exe 구문 및 유효한 호스트 옵션이 표시 됩니다.
-   **/T** 매개 변수는 타이머를 설정 하 여 스크립트의 과도 한 실행을 방지 합니다. 런타임에 지정된 된 값을 초과 하면 cscript는 스크립트 엔진 및 프로세스를 종료 합니다.
-   Windows 스크립트 파일 일반적으로 다음 파일 이름 확장명 중 하나는:.wsf,.vbs,.js 합니다.
-   개별 스크립트에 대 한 속성을 설정할 수 있습니다. 자세한 내용은 관련 항목을 참조 하십시오.
-   Windows 스크립트 호스트.wsf 스크립트 파일을 사용할 수 있습니다. 각.wsf 파일 여러 스크립팅 엔진을 사용 하 고 여러 작업을 수행할 수 있습니다.
-   연결 되지 않은 확장명을 가진 스크립트 파일을 두 번 클릭 합니다 **연결 프로그램** 대화 상자가 나타납니다. cscript 또는 wscript를 선택한 후 **항상이 프로그램을 사용 하 여이 파일 형식을 열**합니다. 이 파일 형식의 파일에 대 한 기본 스크립트 호스트 wscript.exe 또는 cscript를 등록합니다.
-   개별 스크립트에 대 한 속성을 설정할 수 있습니다. 참조 [추가 참조](#BKMK_references) 자세한 내용은 합니다.
-   Windows 스크립트 호스트.wsf 스크립트 파일을 사용할 수 있습니다. 각.wsf 파일 여러 스크립팅 엔진을 사용 하 고 여러 작업을 수행할 수 있습니다.

#### <a name="BKMK_references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
