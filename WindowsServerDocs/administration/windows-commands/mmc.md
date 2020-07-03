---
title: mmc
description: 특정 mmc 콘솔을 열거나, 작성자 모드에서 mmc를 열거나, 32 비트 또는 64 비트 버전의 mmc를 열도록 지정할 수 있는 mmc 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7bfa4030-ce42-40fb-922f-2f5145a80872
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c93416c9939d37e8d672a7e8d52d01ddfebd48e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935759"
---
# <a name="mmc"></a>mmc

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mmc 명령줄 옵션을 사용 하 여 특정 **mmc** 콘솔을 열거나, 작성자 모드에서 **mmc** 를 열거나, 32 비트 또는 64 비트 버전의 **mmc** 를 열도록 지정할 수 있습니다.

## <a name="syntax"></a>구문

```
mmc <path>\<filename>.msc [/a] [/64] [/32]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<path>\<filename>.msc` | **mmc** 를 시작 하 고 저장 된 콘솔을 엽니다. 저장된 된 콘솔 파일에 대 한 전체 경로 파일 이름을 지정 해야 합니다. 콘솔 파일을 지정 하지 않으면 **mmc** 에서 새 콘솔을 엽니다. |
| /a | 만든이 모드에서 저장된 된 콘솔을 엽니다.  저장 된 콘솔을 변경 하는 데 사용 합니다. |
| /64 | 64 비트 버전의 **mmc** (mmc64)를 엽니다. Microsoft 64 비트 운영 체제를 실행 하 고 64 비트 스냅인을 사용 하려는 경우에이 옵션을 사용 합니다. |
| /32 | 32 비트 버전의 **mmc** (mmc32)를 엽니다. Microsoft 64 비트 운영 체제를 실행 하는 경우 32 비트만 스냅인 인 경우이 명령줄 옵션을 사용 하 여 mmc를 열어 32 비트 스냅인을 실행할 수 있습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="remarks"></a>설명

- 환경 변수를 사용 하 여 콘솔 파일의 명시적 위치에 의존 하지 않는 명령줄 또는 바로 가기를 만들 수 있습니다. 예를 들어, 콘솔 파일의 경로를 시스템 폴더에는 경우 (예를 들어 **mmc c:\winnt\system32\console_name.msc**), 확장 가능한 데이터 문자열을 사용 하 여 **%systemroot%** 위치를 지정 (**mmc%systemroot%\system32\console_name.msc**). 이는 다른 컴퓨터에서 작업 하는 조직의 사용자에 게 작업을 위임 하는 경우에 유용할 수 있습니다.

- **/A** 옵션을 사용 하 여 콘솔을 열면 기본 모드에 관계 없이 작성자 모드에서 열립니다. 이렇게 하면 파일에 대 한 기본 모드 설정이 영구적으로 변경 되지 않습니다. 이 옵션을 생략 하면 mmc는 기본 모드 설정에 따라 콘솔 파일을 엽니다.

- 작성자 모드에서 **mmc** 또는 콘솔 파일을 연 후 **콘솔** 메뉴에서 **열기** 를 클릭 하 여 기존 콘솔을 열 수 있습니다.

- 명령줄을 사용 하 여 **mmc** 및 저장 된 콘솔을 여는 바로 가기를 만들 수 있습니다. 와 작동 하는 명령줄 명령은 **실행** 명령에 **시작** 메뉴에서 모든 명령 프롬프트 창에서 바로 가기, 또는 배치 파일 또는 명령을 호출 하는 프로그램입니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
