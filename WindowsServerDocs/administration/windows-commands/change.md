---
title: 변경
description: 로그온, COM 포트 매핑 및 설치 모드 원격 데스크톱 세션 호스트 서버 설정이 변경 되는 변경 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b1350b39633580dd60bbc0eb07e567029447d5f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922455"
---
# <a name="change"></a>변경

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

로그온, COM 포트 매핑 및 설치 모드에 대 한 서버 설정 원격 데스크톱 세션 호스트 변경 합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 확인 하려면 [Windows Server에서 원격 데스크톱 서비스의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))을 참조 하세요.

## <a name="syntax"></a>구문

 ```
 change logon
 change port
 change user
 ```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| [로그온 명령 변경](change-logon.md) | 원격 데스크톱 세션 호스트 서버의 클라이언트 세션에서 로그온을 사용 하거나 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다. |
| [포트 변경 명령](change-port.md) | 나열 하거나 MS-DOS 애플리케이션과 호환 되도록 COM 포트 매핑을 변경 합니다. |
| [사용자 변경 명령](change-user.md) | 원격 데스크톱 세션 호스트 서버에 대 한 설치 모드를 변경 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [원격 데스크톱 서비스(터미널 서비스) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
