---
title: change
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eee52bbb24824ea01f9c55a4bfe6e3e60ad2ab58
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379551"
---
# <a name="change"></a>change

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

로그온, COM 포트 매핑 및 설치 모드에 대 한 원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버 설정을 변경 합니다.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.
> ## <a name="syntax"></a>구문
> ```
> change logon
> change port
> change user
> ```
> ## <a name="parameters"></a>매개 변수
> 
> |            매개 변수            |                                                   설명                                                   |
> |---------------------------------|-----------------------------------------------------------------------------------------------------------------|
> | [change logon](change-logon.md) | Rd 세션 호스트 서버의 클라이언트 세션에서 로그온을 사용 하거나 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다. |
> |  [change port](change-port.md)  |                MS-DOS 응용 프로그램과 호환 되도록 COM 포트 매핑을 나열 하거나 변경 합니다.                |
> |  [change user](change-user.md)  |                            rd 세션 호스트 서버에 대 한 설치 모드를 변경 합니다.                             |
> 
> #### <a name="additional-references"></a>추가 참조
> [명령줄 구문 키](command-line-syntax-key.md)
> [원격 데스크톱 서비스 & #40; 터미널 서비스 및 #41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
