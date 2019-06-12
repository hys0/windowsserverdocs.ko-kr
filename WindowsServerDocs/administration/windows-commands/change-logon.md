---
title: change logon
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41466260-aee9-4333-bcb6-178112c22afd Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45c171a1b14cf69abf039d57697cad933a2dd87b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434573"
---
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="change-logon"></a>change logon
또는 클라이언트 세션에서 로그온을 사용 하지 않도록 설정 하거나 현재 로그온 상태를 표시 합니다.
이 유틸리티는 시스템 유지 관리에 유용 합니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.
> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.
> ## <a name="syntax"></a>구문
> ```
> change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
> ```
> ## <a name="parameters"></a>매개 변수
> 
> |     매개 변수      |                                                       설명                                                        |
> |--------------------|--------------------------------------------------------------------------------------------------------------------------|
> |       / 쿼리       |                             사용 여부는 현재 로그온 상태를 표시 합니다.                              |
> |      같습니다.       |                              콘솔에서가 아니라 하지만 클라이언트 세션에서 로그온 수 있습니다.                              |
> |      /disable      |  이후에 로그온을 콘솔 있지만 클라이언트 세션에서 사용할 수 없습니다. 현재 로그온된 사용자가 영향을 주지 않습니다.   |
> |       /drain       |                 새 클라이언트 세션에서 로그온 할 수 없게 하 하지만 기존 세션에 다시 연결을 허용 합니다.                 |
> | /drainuntilrestart | 컴퓨터 다시 시작 되 면 기존 세션에 다시 연결을 허용 될 때까지 새 클라이언트 세션에서 로그온을 사용 하지 않도록 설정 합니다. |
> |         /?         |                                           명령 프롬프트에 도움말을 표시합니다.                                           |
> 
> ## <a name="remarks"></a>설명
> - 관리자만 사용할 수는 **로그온 변경** 명령입니다.
> - 시스템 다시 시작 하는 경우에 다시 로그온이 설정 됩니다. 클라이언트 세션에서 원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버에 연결 되어 및 로그온을 사용 하지 않도록 설정 한 다음 다시 로그온 하기 전에 로그 오프 하는 경우 세션에 다시 연결할 수 없습니다. 클라이언트 세션에서 로그온을 다시 활성화 하려면 콘솔에 로그온 합니다.
>   ## <a name="BKMK_examples"></a>예제
> - 현재 로그온 상태를 표시 하려면 다음을 입력 합니다.
>   ```
>   change logon /query
>   ```
> - 클라이언트 세션에서 로그온을 사용 하려면 다음을 입력 합니다.
>   ```
>   change logon /enable
>   ```
> - 클라이언트 로그온을 사용 하지 않으려면 다음을 입력 합니다.
>   ```
>   change logon /disable
>   ```
>   #### <a name="additional-references"></a>추가 참조
>   [명령줄 구문 키](command-line-syntax-key.md)
>   [변경할](change.md)
>   [Remote Desktop Services &#40;터미널&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
