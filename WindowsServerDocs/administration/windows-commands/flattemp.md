---
title: flattemp
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 059a0960-1fd9-4382-87fe-a85d5dccdaea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a291c102d70ff9166a7bb0261e506792a49dc18
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844576"
---
# <a name="flattemp"></a>flattemp

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

하나의 임시 폴더를 사용 하지 않도록 설정 하거나 사용 합니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.

> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
flattemp {/query | /enable | /disable}
```

### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/ 쿼리|현재 설정을 쿼리합니다.|
|같습니다.|하나의 임시 폴더를 사용 하도록 설정 합니다. 사용자는 임시 폴더가 사용자의 홈 폴더에 있는 경우를 제외 하 고는 임시 폴더를 공유 합니다.|
|/disable|하나의 임시 폴더를 사용 하지 않도록 설정 합니다. 각 사용자의 임시 폴더는 별도의 폴더에 상주 합니다 (사용자의 세션 ID에 의해 결정 됨).|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의
-   **Flattemp** 명령은 windows server 2008를 실행 하는 컴퓨터에 터미널 서버 역할 서비스를 설치한 경우 나 windows server 2008 r 2를 실행 하는 컴퓨터에서 Rd 세션 호스트 역할 서비스를 설치한 경우에만 사용할 수 있습니다.
-   실행 하려면 관리자 자격 증명이 있어야 **flattemp**합니다.
-   각 사용자가 고유한 임시 폴더를 사용 하 여 **flattemp /enable** 하나의 임시 폴더 사용 하도록 설정 합니다.
-   여러 사용자 (일반적으로 가리키는 TEMP 및 TMP 환경 변수)에 대 한 임시 폴더를 만들기 위한 기본 방법은에 하위 폴더를 만들어는 **\Temp** 하위 폴더 이름으로 로그온 Id를 사용 하 여 폴더입니다. 예를 들어, TEMP 환경 변수 C:\Temp를 가리키는 경우 사용자 로그온 Id 4에 할당 된 임시 폴더 C:\Temp\4입니다. 사용 하 여 **flattemp**, \Temp 폴더에 직접 지정 하 고 하위 폴더를 구성 하지 않도록 합니다. Rd 세션 호스트 서버 로컬 드라이브나 공유 네트워크 드라이브에 있든 상관 없이 사용자 임시 폴더를 홈 폴더에 포함 하려는 경우에 유용 합니다. 사용 해야는 **flattemp /enable** 명령을 각 사용자는 별도 임시 폴더에 있을 때만 합니다.
-   사용자의 임시 폴더가 네트워크 드라이브에 있으면 애플리케이션 오류가 발생할 수 있습니다. 이 공유 네트워크 드라이브는 네트워크에서 일시적으로 사용할 수 없을 때 발생 합니다. 애플리케이션의 임시 파일 액세스 불가능 하거나 동기화 되지 않으므로 디스크 중지 된 경우에 따라 응답 합니다. 임시 폴더를 네트워크 드라이브로 이동 권장 되지 않습니다. 임시 폴더는 로컬 하드 디스크에 유지 하는 것이 기본값이입니다. 예기치 않은 동작이 나 특정 애플리케이션을 사용 하 여 디스크 손상 오류를 발생 하면 네트워크를 안정화 또는 임시 폴더를 로컬 하드 디스크를 다시 이동 합니다.
-   세션당 개별 임시 폴더를 사용 하지 않도록 설정 하는 경우 **flattemp** 설정은 무시 됩니다. 이 옵션은 원격 데스크톱 서비스 구성 도구에서 설정 됩니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와
-   하나의 임시 폴더에 대 한 현재 설정을 표시 하려면 다음을 입력 합니다.
    ```
    flattemp /query
    ```
-   하나의 임시 폴더를 사용 하려면 다음을 입력 합니다.
    ```
    flattemp /enable
    ```
-   하나의 임시 폴더를 사용 하지 않으려면 다음을 입력 합니다.
    ```
    flattemp /disable
    ```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)

[원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
