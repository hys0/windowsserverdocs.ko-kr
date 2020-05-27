---
title: mstsc
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 59801227-1e7e-4dbd-96e6-f54102a3ce92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bee9dabe0e9344c7870e53ed34e4c9dd057cfc42
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820843"
---
# <a name="mstsc"></a>mstsc

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버 또는 다른 원격 컴퓨터에 대 한 연결을 만들고, 기존 원격 데스크톱 연결 (.rdp) 구성 파일을 편집 하 고, 클라이언트 연결 관리자를 사용 하 여 만든 레거시 연결 파일을 새 .rdp 연결 파일로 마이그레이션합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
mstsc.exe [<Connection File>] [/v:<Server>[:<Port>]] [/admin] [/f] [/w:<Width> /h:<Height>] [/public] [/span]
mstsc.exe /edit <Connection File>
mstsc.exe /migrate
```

### <a name="parameters"></a>매개 변수

|        매개 변수        |                                                         설명                                                         |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------|
|    <Connection File>    |                                   연결에.rdp 파일의 이름을 지정합니다.                                    |
|  /v: <Server \> [: <Port \> ] |                원격 컴퓨터와 선택적으로 연결 하려면 포트 번호를 지정 합니다.                 |
|         /admin          |                                   서버 관리에 대 한 세션에 연결할 수 있습니다.                                   |
|           /f            |                                    전체 화면 모드에서 원격 데스크톱 연결를 시작 합니다.                                    |
|       /w<Width>        |                                      원격 데스크톱 창의 너비를 지정합니다.                                      |
|       /h<Height>       |                                     원격 데스크톱 창의 높이 지정합니다.                                      |
|         공용 /         |                  공개 모드에서 원격 데스크톱을 실행합니다. 공개 모드, 암호 및 비트맵 캐시 되지 않습니다.                  |
|          /span          | 원격 데스크톱 너비와 높이를 필요에 따라 여러 모니터에 걸쳐 로컬 가상 데스크톱과 일치 합니다. |
| /edit<Connection File> |                                         편집을 위해 지정 된.rdp 파일을 엽니다.                                          |
|        / 마이그레이션         |       레거시 연결 생성 된 파일을 클라이언트 연결 관리자를 사용 하 여을 새로운.rdp 연결 파일로 마이그레이션합니다.       |
|           /?            |                                            명령 프롬프트에 도움말을 표시합니다.                                             |

## <a name="remarks"></a>설명
-   Default.rdp 각 사용자에 대 한 사용자의 Documents 폴더에 숨겨진 파일로 저장 됩니다. 사용자가.rdp 파일을 만든 사용자의 Documents 폴더에는 기본적으로 저장 되지만 원하는 위치에 저장할 수 있습니다.
-   모니터에 걸쳐를 모니터 해상도 사용 해야 하며 가로로 정렬 되어야 합니다 (즉, side by side 방식). 지원은 현재 없습니다 클라이언트 시스템에서 세로로 여러 모니터를 확장 합니다.

## <a name="examples"></a>예
-   전체 화면 모드에서 세션에 연결 하려면 다음을 입력 합니다.
    ```
    mstsc /f
    ```
-   편집을 위해 filename.rdp 라는 파일을 열려면 다음을 입력 합니다.
    ```
    mstsc /edit filename.rdp
    ```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
-   [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
