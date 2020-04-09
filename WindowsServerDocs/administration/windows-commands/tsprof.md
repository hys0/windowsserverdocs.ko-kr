---
title: tsprof
description: 원격 데스크톱 서비스 사용자 구성 정보를 한 사용자에서 다른 사용자로 복사 하는 tsprof에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 27047868-b706-4208-b7e0-1437a2325dd3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b1037b6daff467a71517917d423e4cbe87a97f2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832476"
---
# <a name="tsprof"></a>tsprof

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

한 사용자에서 다른 원격 데스크톱 서비스 사용자 구성 정보를 복사합니다.
원격 데스크톱 서비스 사용자 구성 정보는 로컬 사용자 및 그룹 및 active directory 사용자 및 컴퓨터에 대 한 원격 데스크톱 서비스 확장에 표시 됩니다.

**tsprof** 사용자에 대 한 프로필 경로를 설정할 수도 있습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
tsprof /update {/domain:<DomainName> | /local} /profile:<path> <UserName>
tsprof /copy {/domain:<DomainName> | /local} [/profile:<path>] <Src_usr> <Dest_usr>
tsprof /q {/domain:<DomainName> | /local} <UserName>
```

### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/update|*도메인 > < 도메인*의 <*사용자 이름*>에 대 한 프로필 경로 정보를 <*프로필 경로*>에 업데이트 합니다.|
|/domain:\<DomainName >|동작을 적용할 도메인의 이름을 지정 합니다.|
|로컬 /|로컬 사용자 계정에만 작업을 적용합니다.|
|/profile:\<경로 >|로컬 사용자 및 그룹 및 active directory 사용자 및 컴퓨터의 원격 데스크톱 서비스 확장에 표시 된 프로필 경로를 지정 합니다.|
|\<사용자 이름 >|서버 프로필 경로를 업데이트 하거나 쿼리할 사용자의 이름을 지정 합니다.|
|/copy|\<*sourceuser*>의 사용자 구성 정보를 *destinationuser*> \<복사 하 고 \<*destinationuser*>에 대 한 프로필 경로 정보를 \<*프로필 경로*>으로 업데이트 합니다. \<*sourceuser*> 및 \<*destinationuser*>는 모두 로컬 이거나 도메인 \<*DomainName*>에 있어야 합니다.|
|\<Src_usr >|사용자 구성 정보를 복사해 올 사용자의 이름을 지정 합니다.|
|\<Dest_usr >|사용자 구성 정보를 복사 하려면 원하는 사용자의 이름을 지정 합니다.|
|/q|대상 서버 프로필 경로 쿼리 하려는 사용자의 현재 프로필 경로 표시 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의
-   **Tsprof** 명령은 windows server 2008를 실행 하는 컴퓨터에 터미널 서버 역할 서비스를 설치한 경우 나 windows server 2008 r 2를 실행 하는 컴퓨터에서 RD 세션 호스트 역할 서비스를 설치한 경우에만 사용할 수 있습니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와
-   사용자 구성 정보를 LocalUser1에서 LocalUser2를 복사 하려면 다음을 입력 합니다.
    ```
    tsprof /copy /local LocalUser1 LocalUser2
    ```
-   LocalUser1에 대 한 원격 데스크톱 서비스 프로필 경로를 c:\profiles 이라는 디렉터리로 설정 하려면 다음을 입력 합니다.
    ```
    tsprof /update /local /profile:c:\profiles LocalUser1
    ```

## <a name="additional-references"></a>추가 참조
- 명령줄 [구문 키](command-line-syntax-key.md)
[원격 데스크톱 서비스 (Terminal Services) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
