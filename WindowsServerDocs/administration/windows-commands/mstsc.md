---
title: mstsc
description: 원격 데스크톱 세션 호스트 서버 또는 다른 원격 컴퓨터에 대 한 연결을 만들고, 기존 원격 데스크톱 연결 (.rdp) 구성 파일을 편집 하 고, 클라이언트 연결 관리자를 사용 하 여 만든 레거시 연결 파일을 새 .rdp 연결 파일로 마이그레이션하는 mstsc 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 59801227-1e7e-4dbd-96e6-f54102a3ce92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a6620cc2f954e43a6e68369f9b1f3480c1fc508c
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354353"
---
# <a name="mstsc"></a>mstsc

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버 또는 다른 원격 컴퓨터에 대 한 연결을 만들고, 기존 원격 데스크톱 연결 (.rdp) 구성 파일을 편집 하 고, 클라이언트 연결 관리자를 사용 하 여 만든 레거시 연결 파일을 새 .rdp 연결 파일로 마이그레이션합니다.

## <a name="syntax"></a>구문

```
mstsc.exe [<connectionfile>] [/v:<server>[:<port>]] [/admin] [/f] [/w:<width> /h:<height>] [/public] [/span]
mstsc.exe /edit <connectionfile>
mstsc.exe /migrate
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ------------|
| `<connectionfile>` | 연결에.rdp 파일의 이름을 지정합니다. |
| /v:`<server>[:<port>]` | 원격 컴퓨터와 선택적으로 연결 하려면 포트 번호를 지정 합니다. |
| /admin | 서버 관리에 대 한 세션에 연결할 수 있습니다. |
| /f | 전체 화면 모드에서 원격 데스크톱 연결을 시작합니다. |
| /w`<width>` | 원격 데스크톱 창의 너비를 지정합니다. |
| /h`<height>` | 원격 데스크톱 창의 높이 지정합니다. |
| 공용 / | 공개 모드에서 원격 데스크톱을 실행합니다. 공개 모드에서는 암호와 비트맵이 캐시 되지 않습니다. |
| /span | 원격 데스크톱 너비와 높이를 필요에 따라 여러 모니터에 걸쳐 로컬 가상 데스크톱과 일치 합니다. |
| /edit`<connectionfile>` | 편집을 위해 지정 된.rdp 파일을 엽니다. |
| / 마이그레이션 | 레거시 연결 생성 된 파일을 클라이언트 연결 관리자를 사용 하 여을 새로운.rdp 연결 파일로 마이그레이션합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 기본 .rdp는 사용자의 **Documents** 폴더에 숨겨진 파일로 각 사용자에 대해 저장 됩니다.

- 사용자가 만든 .rdp 파일은 기본적으로 사용자의 **Documents** 폴더에 저장 되지만 어디에 나 저장할 수 있습니다.

- 모니터에 걸쳐 확장 하려면 모니터는 동일한 해상도를 사용 해야 하며 가로로 정렬 되어야 합니다 (즉, side-by-side). 지원은 현재 없습니다 클라이언트 시스템에서 세로로 여러 모니터를 확장 합니다.

### <a name="examples"></a>예

전체 화면 모드에서 세션에 연결 하려면 다음을 입력 합니다.

```
mstsc /f
```

편집을 위해 파일 *이름이 .rdp* 인 파일을 열려면 다음을 입력 합니다.

```
mstsc /edit filename.rdp
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
