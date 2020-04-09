---
title: 변경
description: 로그온, COM 포트 매핑 및 설치 모드에 대 한 서버 설정 원격 데스크톱 세션 호스트 변경 되는 변경에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5d91f8d0941fc96e776c761b9c7037e58588df8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847956"
---
# <a name="change"></a>변경

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

로그온, COM 포트 매핑 및 설치 모드에 대 한 서버 설정 원격 데스크톱 세션 호스트 변경 합니다.

> [!NOTE]
> 터미널 서비스는 Windows Server 2008 R2에서 원격 데스크톱 서비스로 이름이 변경되었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문

 ```
 change logon
 change port
 change user
 ```
 
 ### <a name="parameters"></a>매개 변수
 
 |            매개 변수            |                                                   설명                                                   |
 |---------------------------------|-----------------------------------------------------------------------------------------------------------------|
 | [change logon](change-logon.md) | Rd 세션 호스트 서버의 클라이언트 세션에서 로그온을 사용 하거나 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다. |
 |  [change port](change-port.md)  |                MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 나열 하거나 변경 합니다.                |
 |  [change user](change-user.md)  |                            rd 세션 호스트 서버에 대 한 설치 모드를 변경 합니다.                             |
 
 ## <a name="additional-references"></a>추가 참조
 - 명령줄 [구문 키](command-line-syntax-key.md)
 [원격 데스크톱 서비스 (Terminal Services) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
