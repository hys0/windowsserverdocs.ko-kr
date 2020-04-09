---
title: 경로
description: PATH 환경 변수를 설정 하는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1bfa1349-e79a-472b-a9e6-d7a91149ae8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb77cac3871dcf4a411638409de68d038a317d24
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837716"
---
# <a name="path"></a>경로



PATH 환경 변수 (실행 파일을 검색 하는 데 사용 되는 디렉터리 집합)에서 명령 경로 설정 합니다. 매개 변수 없이 사용 하는 경우 **경로** 현재 명령 경로 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
path [[<Drive>:]<Path>[;...][;%PATH%]]
path ;
```

### <a name="parameters"></a>매개 변수

|     매개 변수     |                                                                                                     설명                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [\<Drive >:]<Path> |                                                                            드라이브와 명령 경로에 설정 하는 디렉터리를 지정 합니다.                                                                             |
|         ;         | 명령 경로에서 디렉터리를 구분 합니다. 다른 매개 변수 없이 사용 하는 경우 **;** 기존 명령 경로 PATH 환경 변수를 지우고 Cmd.exe 현재 디렉터리 에서만에서 검색 하도록 지시 합니다. |
|      % PATH %       |                                                         PATH 환경 변수에 나열 된 디렉터리의 기존 집합에 명령 경로 추가 합니다.                                                         |
|        /?         |                                                                                         명령 프롬프트에 도움말을 표시합니다.                                                                                         |

## <a name="remarks"></a>주의

-   포함 하는 경우 **% PATH %** 구문에서 Cmd.exe 바꿉니다 PATH 환경 변수에 명령 경로 값 명령 프롬프트에서 이러한 값을 수동으로 입력할 필요가 없습니다.
-   현재 디렉터리를 명령 경로에 지정 된 디렉터리 하기 전에 항상 검색 됩니다.
-   확장명이 다른 하지만 같은 파일 이름을 공유 하는 디렉터리에 파일이 있을 수 있습니다. 예를 들어 회계 프로그램을 시작 하는 Accnt.com 라는 파일과 같은 디렉터리에 있는 계정 시스템 네트워크 서버에 연결 하 라는 다른 파일을 할 수 있습니다.

    Windows 운영 체제의 우선 순위는 다음 순서에서 기본 파일 이름 확장명을 사용 하 여 파일을 검색 합니다..exe,.com,.bat, 및. cmd. 같은 디렉터리에 있는 Accnt.com 동일한 디렉터리에 있는 경우를 실행 하려면 명령 프롬프트에서.bat 확장명을 포함 해야 합니다.
-   동일한 파일 이름 및 확장명, 명령 경로에 두 개 이상의 파일의 경우 **경로** 현재 디렉터리에 지정된 된 파일에 대 한 첫 번째 검색 이름을 지정 합니다. 다음 명령 경로 PATH 환경 변수에 나열 된 순서에 있는 디렉터리를 검색 합니다.
-   배치 하는 경우는 **경로** Windows 운영 체제는 자동으로 지정된 된 MS-DOS 하위 시스템 검색 경로 추가 컴퓨터에 로그온 할 때마다 Autoexec.nt 파일에 명령 합니다. Cmd.exe는 Autoexec.nt 파일을 사용 하지 않습니다. 바로 가기에서 시작할 때 Cmd.exe 내 컴퓨터/속성/고급/환경에 설정 된 환경 변수를 상속 합니다.

## <a name="examples"></a><a name="BKMK_examples"></a>예와

외부 명령에 대 한 C:\User\Taxes, B:\User\Invest, 및 B:\Bin 경로 검색 하려면 다음을 입력 합니다.

`path c:\user\taxes;b:\user\invest;b:\bin`

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)