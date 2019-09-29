---
title: change user
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6202f024-8cf5-411e-89b1-ee37ff46499d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 771e39182c17b9a6710e49eff2f5302e539bdbb5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379566"
---
# <a name="change-user"></a>change user

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에 대 한 설치 모드를 변경 합니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.
> ## <a name="syntax"></a>구문
> ```
> change user {/execute | /install | /query}
> ```
> ## <a name="parameters"></a>매개 변수
> 
> | 매개 변수 |                                                                                                 설명                                                                                                  |
> |-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | / 실행  |                                                                .Ini 파일을 홈 디렉터리에 매핑할을 수 있습니다. 이것이 기본 설정입니다.                                                                 |
> | /install  | 홈 디렉터리에.ini 파일 매핑을 사용 하지 않습니다. 모든.ini 파일 읽고 시스템 디렉터리에 기록 됩니다. Rd 세션 호스트 서버에 응용 프로그램을 설치할 때 .ini 파일 매핑을 사용 하지 않도록 설정 해야 합니다. |
> |  / 쿼리   |                                                                             .Ini 파일 매핑에 대 한 현재 설정을 표시합니다.                                                                              |
> |    /?     |                                                                                     명령 프롬프트에 도움말을 표시합니다.                                                                                     |
> 
> ## <a name="remarks"></a>설명
> - 사용 하 여 **변경 사용자 /install** 시스템 디렉터리에서 응용 프로그램에 대 한.ini 파일을 만드는 응용 프로그램을 설치 하기 전에 합니다. 이러한 파일은 사용자 고유의.ini 파일을 만들 때 원본으로 사용 됩니다. 응용 프로그램을 설치한 후 사용 하 여 **사용자 변경 / 실행** 표준.ini 파일을 매핑할으로 되돌리려고 합니다.
> - 처음으로 응용 프로그램을 실행 하는 홈 디렉터리에서.ini 파일에 대 한 검색 합니다. .Ini 파일 시스템 디렉터리에서 발견 되는 홈 디렉터리에는 없는 표시 되지만 원격 데스크톱 서비스.ini 파일에 복사 홈 디렉터리, 각 사용자가 응용 프로그램.ini 파일의 고유 복사본을가지고 있는지 확인 합니다. 모든 새.ini 파일은 홈 디렉터리에 생성 됩니다.
> - 사용자 마다 응용 프로그램에 대 한.ini 파일의 고유 복사본을가지고 있어야 합니다. 이렇게 하면 다른 사용자 (예: 서로 다른 기본 디렉터리 또는 화면 해상도) 호환 되지 않는 응용 프로그램 구성이 않는 것을 방지할 수 있습니다.
> - 설치 모드에서 시스템의 경우 (즉, **변경 사용자 /install**), 몇 가지 작업이 수행 됩니다. 만든 모든 레지스트리 항목은 **\Software** 하위 키 또는 **\software** 하위 키의 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentversion\Terminal Server\Install**아래에 숨겨집니다. **HKEY_CURrenT_USER** 에 추가 된 하위 키는 **\software** 하위 키 아래에 복사 되 고 **HKEY_LOCAL_MACHINE** 에 추가 된 하위 키는 **\software** 하위 키 아래에 복사 됩니다. 응용 프로그램이 GetWindowsdirectory와 같은 시스템 호출을 사용 하 여 Windows 디렉터리를 쿼리하면, rd 세션 호스트 서버는 systemroot 디렉터리를 반환 합니다. .Ini 파일 항목을 모두 WritePrivateProfileString, 같은 시스템 호출을 사용 하 여 추가 되 면 시스템 루트 디렉터리에 있는.ini 파일에 추가 됩니다.
> - 시스템이 실행 모드 (즉, **사용자/execute**)로 반환 되 고 응용 프로그램에서 **HKEY_CURrenT_USER** 아래에 존재 하지 않는 레지스트리 항목을 읽으려고 하면 원격 데스크톱 서비스는 키의 복사본이 다음 위치에 있는지 확인 합니다. **\Terminal Server\Install** 하위 키입니다. 이 경우 하위 키가 **HKEY_CURrenT_USER**의 적절 한 위치에 복사 됩니다. 응용 프로그램을 존재 하지 않는.ini 파일에서 읽은 하려고 하는 경우 해당.ini 파일 시스템 루트 아래 원격 데스크톱 서비스를 검색 합니다. .Ini 파일 시스템 루트에 있으면 사용자의 홈 디렉터리의 \Windows 하위 디렉터리에 복사 됩니다. 응용 프로그램에서 Windows 디렉터리를 쿼리하면 rd 세션 호스트 서버는 사용자의 홈 디렉터리에 대 한 \Windows 하위 디렉터리를 반환 합니다.
> - 로그온 할 때 원격 데스크톱 서비스는 시스템.ini 파일이 컴퓨터에.ini 파일 보다 최신 인지 확인 합니다. 시스템 버전 새 버전인 경우.ini 파일은 대체 또는 최신 버전으로 병합 합니다. 이 든 아니든 INISYNC 비트가 0x40에 따라 달라 집니다, 그리고이.ini 파일에 대해 설정 됩니다. .Ini 파일의 이전 버전은 Inifile.ctx로 이름이 변경 됩니다. **\Terminal Server\Install** 하위 키 아래의 시스템 레지스트리 값이 **HKEY_CURrenT_USER**의 버전 보다 최신인 경우 하위 키 버전이 삭제 되 고 **\terminal Server\Install**의 새 하위 키로 대체 됩니다.
>   ## <a name="BKMK_examples"></a>예와
> - .Ini 파일을 홈 디렉터리에 매핑할을 사용 하지 않으려면 다음을 입력 합니다.
>   ```
>   change user /install
>   ```
> - .Ini 파일을 홈 디렉터리에 매핑할을 사용 하려면 다음을 입력 합니다.
>   ```
>   change user /execute
>   ```
> - .Ini 파일 매핑에 대 한 현재 설정의 표시 하려면 다음을 입력 합니다.
>   ```
>   change user /query
>   ```
>   #### <a name="additional-references"></a>추가 참조
>   [명령줄 구문 키](command-line-syntax-key.md)@no__t[변경](change.md)
>   [원격 데스크톱 서비스 &#40;터미널&#41; 서비스 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
