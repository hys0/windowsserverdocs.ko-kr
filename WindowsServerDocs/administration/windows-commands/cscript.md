---
title: cscript
description: 명령줄 환경에서 실행 되도록 스크립트를 시작 하는 cscript 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fba3cbca-594e-4663-bb22-4ee0f63a1ac6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7f6731c264fc5a22bee2d94b41a555431e48b42
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928839"
---
# <a name="cscript"></a>cscript

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

명령줄 환경에서 실행할 스크립트를 시작 합니다.

>[!IMPORTANT]
> 이 작업은 관리 자격 증명 없이도 수행할 수 있으므로 보안을 위해 관리 자격 증명이 없는 사용자로 이 작업을 수행하는 것이 좋습니다.

## <a name="syntax"></a>구문

```
cscript <scriptname.extension> [/b] [/d] [/e:<engine>] [{/h:cscript | /h:wscript}] [/i] [/job:<identifier>] [{/logo | /nologo}] [/s] [/t:<seconds>] [x] [/u] [/?] [<scriptarguments>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| scriptname | 선택적 파일 이름 확장명을 가진 스크립트 파일의 경로 파일 이름을 지정합니다. |
| /b | 경고, 스크립팅 오류 또는 입력된 프롬프트를 표시 하지 않는 일괄 처리 모드를 지정 합니다. |
| /d | 디버거를 시작합니다. |
| /e:`<engine>` | 스크립트를 실행 하는 데 사용 되는 엔진을 지정 합니다. |
| /h:cscript | cscript.exe 스크립트를 실행 하기 위한 기본 스크립트 호스트로 등록 합니다. |
| /h:wscript | wscript.exe 스크립트를 실행 하기 위한 기본 스크립트 호스트로 등록 합니다. 기본값입니다. |
| /i | 경고, 스크립팅 오류 및 입력된 프롬프트를 표시 하는 대화형 모드를 지정 합니다. 이는 기본값과의 반대입니다 `/b` . |
| /작업 (<identifier> | .Wsf 스크립트 파일의 *식별자* 로 식별 된 작업을 실행 합니다. |
| /logo | 스크립트를 실행 하기 전에 Windows 스크립트 호스트 배너 콘솔에 표시 되도록 지정 합니다. 이는 기본값과의 반대입니다 `/nologo` . |
| /nologo | 스크립트를 실행 하기 전에 Windows 스크립트 호스트 배너가 표시 되지 않도록 지정 합니다. |
| /s | 현재 사용자에 대 한 현재 명령 프롬프트 옵션을 저장합니다. |
| /t:<seconds> | 스크립트를 초 단위로 실행할 수 있는 최대 시간을 지정 합니다. 최대 32, 767 초를 지정할 수 있습니다. 기본값은 시간 제한이 없습니다. |
| /U | 입력 및 출력을 콘솔에서 리디렉션에 대 한 유니코드를 지정 합니다. |
| /x | 스크립트 디버거를 시작 합니다. |
| /? | 사용 가능한 명령 매개 변수를 표시 하 고 사용 하기 위한 도움말을 제공 합니다. 이는 매개 변수 없이 스크립트를 사용 하지 않고 **cscript.exe** 를 입력 하는 것과 같습니다. |
| scriptarguments | 스크립트에 전달 되는 인수를 지정 합니다. 각 스크립트 인수 앞에는 슬래시 ()를 붙여야 합니다 **/** . |

#### <a name="remarks"></a>설명

- 각 매개 변수는 선택 사항입니다. 그러나 스크립트를 지정 하지 않고 스크립트 인수를 지정할 수 없습니다. 스크립트나 스크립트 인수를 지정 하지 않으면 cscript.exe cscript.exe 구문과 유효한 호스트 옵션을 표시 합니다.

- **/T** 매개 변수는 타이머를 설정 하 여 스크립트의 과도 한 실행을 방지 합니다. 실행 시간이 지정 된 값을 초과 하면 cscript는 스크립트 엔진을 중단 하 고 프로세스를 종료 합니다.

- Windows 스크립트 파일 일반적으로 다음 파일 이름 확장명 중 하나는:.wsf,.vbs,.js 합니다. Windows 스크립트 호스트.wsf 스크립트 파일을 사용할 수 있습니다. 각.wsf 파일 여러 스크립팅 엔진을 사용 하 고 여러 작업을 수행할 수 있습니다.

- 연결 되지 않은 확장명을 가진 스크립트 파일을 두 번 클릭 하면 연결 **프로그램** 대화 상자가 나타납니다. Wscript.exe 또는 cscript를 선택 하 고 **항상이 프로그램을 사용 하 여이 파일 형식 열기를**선택 합니다. 이 파일 형식의 파일에 대 한 기본 스크립트 호스트로 wscript.exe 또는 cscript를 등록 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
