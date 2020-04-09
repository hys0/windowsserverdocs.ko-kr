---
title: change user
description: 사용자 변경에 대 한 Windows 명령 항목으로, 원격 데스크톱 세션 호스트 서버에 대 한 설치 모드를 변경 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6202f024-8cf5-411e-89b1-ee37ff46499d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b13fe66991d6e8bbb91938b550236f3aa9f51ee9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848066"
---
# <a name="change-user"></a>change user

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 서버에 대 한 설치 모드를 변경 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
change user {/execute | /install | /query}
```
### <a name="parameters"></a>매개 변수

| 매개 변수 |                                                                                                 설명                                                                                                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| / 실행  |                                                                .Ini 파일을 홈 디렉터리에 매핑할을 수 있습니다. 이것이 기본 설정입니다.                                                                 |
| /install  | 홈 디렉터리에.ini 파일 매핑을 사용 하지 않습니다. 모든.ini 파일 읽고 시스템 디렉터리에 기록 됩니다. Rd 세션 호스트 서버에 응용 프로그램을 설치할 때 .ini 파일 매핑을 사용 하지 않도록 설정 해야 합니다. |
|  / 쿼리   |                                                                             .Ini 파일 매핑에 대 한 현재 설정을 표시합니다.                                                                              |
|    /?     |                                                                                     명령 프롬프트에 도움말을 표시합니다.                                                                                     |

## <a name="remarks"></a>주의
- 사용 하 여 **변경 사용자 /install** 시스템 디렉터리에서 응용 프로그램에 대 한.ini 파일을 만드는 응용 프로그램을 설치 하기 전에 합니다. 이러한 파일은 사용자 고유의.ini 파일을 만들 때 원본으로 사용 됩니다. 응용 프로그램을 설치한 후 사용 하 여 **사용자 변경 / 실행** 표준.ini 파일을 매핑할으로 되돌리려고 합니다.
- 처음으로 애플리케이션을 실행 하는 홈 디렉터리에서.ini 파일에 대 한 검색 합니다. .Ini 파일 시스템 디렉터리에서 발견 되는 홈 디렉터리에는 없는 표시 되지만 원격 데스크톱 서비스.ini 파일에 복사 홈 디렉터리, 각 사용자가 애플리케이션.ini 파일의 고유 복사본을가지고 있는지 확인 합니다. 모든 새.ini 파일은 홈 디렉터리에 생성 됩니다.
- 사용자 마다 애플리케이션에 대 한.ini 파일의 고유 복사본을가지고 있어야 합니다. 이렇게 하면 다른 사용자 (예: 서로 다른 기본 디렉터리 또는 화면 해상도) 호환 되지 않는 애플리케이션 구성이 않는 것을 방지할 수 있습니다.
- 설치 모드에서 시스템의 경우 (즉, **변경 사용자 /install**), 몇 가지 작업이 수행 됩니다. 만든 모든 레지스트리 항목은 **\Software** 하위 키 또는 **\software** 하위 키에서 **HKEY_LOCAL_MACHINE \software\microsoft\windows NT\Currentversion\Terminal Server\Install**아래에 숨겨집니다. 하위 키에 추가 **HKEY_CURRENT_USER** 아래에 복사 됩니다는 **\SOFTWARE** 하위, 키 및 하위 키에 추가 **HKEY_LOCAL_MACHINE** 아래에 복사 됩니다는 **\MACHINE** 하위 키입니다. 응용 프로그램이 GetWindowsdirectory와 같은 시스템 호출을 사용 하 여 Windows 디렉터리를 쿼리하면, rd 세션 호스트 서버는 systemroot 디렉터리를 반환 합니다. .Ini 파일 항목을 모두 WritePrivateProfileString, 같은 시스템 호출을 사용 하 여 추가 되 면 시스템 루트 디렉터리에 있는.ini 파일에 추가 됩니다.
- 시스템 실행 모드를 반환 하는 경우 (즉, **change user**), 응용 프로그램 아래에 레지스트리 항목을 읽을 하려고 시도 하 고 **HKEY_CURRENT_USER** 아래에서 키의 복사본이 있는지 여부를 확인, 존재 하지 않는 원격 데스크톱 서비스는 **\Terminal Server\Install** 하위 키입니다. 이 경우 하위 키가 **HKEY_CURRRENT_USER**의 적절 한 위치에 복사 됩니다. 애플리케이션을 존재 하지 않는.ini 파일에서 읽은 하려고 하는 경우 해당.ini 파일 시스템 루트 아래 원격 데스크톱 서비스를 검색 합니다. .Ini 파일 시스템 루트에 있으면 사용자의 홈 디렉터리의 \Windows 하위 디렉터리에 복사 됩니다. 응용 프로그램에서 Windows 디렉터리를 쿼리하면 rd 세션 호스트 서버는 사용자의 홈 디렉터리에 대 한 \Windows 하위 디렉터리를 반환 합니다.
- 로그온 할 때 원격 데스크톱 서비스는 시스템.ini 파일이 컴퓨터에.ini 파일 보다 최신 인지 확인 합니다. 시스템 버전 새 버전인 경우.ini 파일은 대체 또는 최신 버전으로 병합 합니다. 이 든 아니든 INISYNC 비트가 0x40에 따라 달라 집니다, 그리고이.ini 파일에 대해 설정 됩니다. .Ini 파일의 이전 버전은 Inifile.ctx로 이름이 변경 됩니다. 시스템 레지스트리 값을 아래 하는 경우는 **\Terminal Server\Install** 하위 키 아래에서 사용 중인 버전 보다 최신인 **HKEY_CURRENT_USER**, 하위 키의 버전 삭제 되어의 새 하위 키로 대체 **\Terminal Server\Install**합니다.
  ## <a name="examples"></a><a name=BKMK_examples></a>예와
- .Ini 파일을 홈 디렉터리에 매핑할을 사용 하지 않으려면 다음을 입력 합니다.
  ```
  change user /install
  ```
- .Ini 파일을 홈 디렉터리에 매핑할을 사용 하려면 다음을 입력 합니다.
  ```
  change user /execute
  ```
- .Ini 파일 매핑에 대 한 현재 설정의 표시 하려면 다음을 입력 합니다.
  ```
  change user /query
  ```
  ## <a name="additional-references"></a>추가 참조
  - 명령줄 [구문 키](command-line-syntax-key.md)
  [변경](change.md)
  [원격 데스크톱 서비스 (터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
