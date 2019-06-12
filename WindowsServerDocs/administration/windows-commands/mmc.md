---
title: mmc
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bfa4030-ce42-40fb-922f-2f5145a80872
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4bdc093bd16ea08153b7dbc4a0e3380251f2ed7d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437335"
---
# <a name="mmc"></a>mmc

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mmc 명령줄 옵션을 사용 하 여 특정 열 수 있습니다 **mmc** 콘솔을 열고 **mmc** 작성자 모드로 지정은 32 비트 또는 64 비트 버전의 **mmc** 열립니다.
## <a name="syntax"></a>구문
```
mmc <path>\<filename>.msc [/a] [/64] [/32]
```
### <a name="parameters"></a>매개 변수

|       매개 변수        |                                                                                                 설명                                                                                                 |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <path>\\<filename>.msc |        시작 **mmc** 저장된 된 된 콘솔을 엽니다. 저장된 된 콘솔 파일에 대 한 전체 경로 파일 이름을 지정 해야 합니다. 콘솔 파일을 지정 하지 않으면 **mmc** 새 콘솔을 엽니다.         |
|           / a           |                                                               만든이 모드에서 저장된 된 콘솔을 엽니다.  저장 된 콘솔을 변경 하는 데 사용 합니다.                                                                |
|          /64           |                         64 비트 버전의 열립니다 **mmc** (m m c 64). Microsoft 64 비트 운영 체제를 실행 하 고 64 비트 스냅인을 사용 하려는 경우에이 옵션을 사용 합니다.                          |
|          /32           | 32 비트 버전의 열립니다 **mmc** (m m c 32). Microsoft 64 비트 운영 체제를 실행 하는 경우 32 비트 전용 스냅인을 사용 하는 경우이 명령줄 옵션을 사용 하 여 열고 mmc에서 32 비트 스냅인을 실행할 수 있습니다. |
|           /?           |                                                                                    명령 프롬프트에 도움말을 표시합니다.                                                                                     |

## <a name="remarks"></a>설명
- 사용 하는 <path> **\\** <filename> **.msc** 명령줄 옵션 환경 변수를 사용 하 여 명령줄 또는 콘솔 파일의 명시적인 위치에 종속 되지 않는 바로 가기를 만들 수 있습니다. 예를 들어, 콘솔 파일의 경로를 시스템 폴더에는 경우 (예를 들어 **mmc c:\winnt\system32\console_name.msc**), 확장 가능한 데이터 문자열을 사용 하 여 **%systemroot%** 위치를 지정 (**mmc%systemroot%\system32\console_name.msc**). 서로 다른 컴퓨터에서 작업 하는 조직에서 사람에 게 작업을 위임할 경우에 유용할 수 있습니다.
- 사용 하는 **/a** 명령줄 옵션은 기본 모드에 관계 없이 만든이 모드에서 열이 옵션을 콘솔을 열면 됩니다. 파일에 대 한 기본 모드 설정은 영구적으로 변경 되지 않습니다. 이 옵션을 생략 하면 mmc는 기본 모드 설정에 따라 콘솔 파일을 엽니다.
- 연 후 **mmc** 또는 콘솔 파일을 만든이 모드에서을 클릭 하 여 기존 콘솔을 열 수 있습니다 **엽니다** 에 **콘솔** 메뉴.
- 명령줄을 사용 하 여 열기에 대 한 바로 가기를 만들 수 있습니다 **mmc** 콘솔을 저장 합니다. 명령줄 명령을 사용 하 여 작동 합니다 **실행** 명령을 합니다 **시작** 메뉴, 명령 프롬프트 창에서 바로 가기, 또는 명령을 호출 하는 프로그램이 나 배치 파일.
  ## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)

