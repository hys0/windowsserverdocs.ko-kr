---
title: termserver 쿼리
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8a0a4608a16df0336b90ea5df281278ae47a503
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722697"
---
# <a name="query-termserver"></a>termserver 쿼리

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

네트워크에 있는 모든 원격 데스크톱 세션 호스트 (rd 세션 호스트) 서버 목록을 표시 합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.
> ## <a name="syntax"></a>구문
> ```
> query termserver [<ServerName>] [/domain:<Domain>] [/address] [/continue]
> ```
> ### <a name="parameters"></a>매개 변수
> 
> |    매개 변수     |                                                                        설명                                                                         |
> |------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |   <ServerName>   |                                               Rd 세션 호스트 서버를 식별 하는 이름을 지정 합니다.                                               |
> | /domain<Domain> | 터미널 서버를 쿼리 하는 도메인을 지정합니다. 현재 작업 중인 도메인을 쿼리 하는 경우 도메인을 지정할 필요가 없습니다. |
> |     / 주소     |                                                  각 서버에 대 한 네트워크 및 노드 주소를 표시합니다.                                                  |
> |    계속 해 서 /     |                                              각 정보 화면에 표시 되 면 일시 중지를 방지 합니다.                                               |
> |        /?        |                                                            명령 프롬프트에 도움말을 표시합니다.                                                            |
> 
> ## <a name="remarks"></a>설명
> - **query termserver** 는 네트워크에서 연결 된 모든 Rd 세션 호스트 서버를 검색 하 고 다음 정보를 반환 합니다.
>   - 서버 이름
>   - 네트워크 (및 노드 주소/주소 옵션을 사용 하는 경우)
>     ## <a name="examples"></a>예
> - 네트워크에 있는 모든 rd 세션 호스트 서버에 대 한 정보를 표시 하려면 다음을 입력 합니다.
>   ```
>   query termserver
>   ```
> - Server3 이라는 rd 세션 호스트 서버에 대 한 정보를 표시 하려면 다음을 입력 합니다.
>   ```
>   query termserver Server3
>   ```
> - CONTOSO 도메인의 모든 rd 세션 호스트 서버에 대 한 정보를 표시 하려면 다음을 입력 합니다.
>   ```
>   query termserver /domain:CONTOSO
>   ```
> - Server3 이라는 rd 세션 호스트 서버에 대 한 네트워크 및 노드 주소를 표시 하려면 다음을 입력 합니다.
>   ```
>   query termserver Server3 /address
>   ```
>   ## <a name="additional-references"></a>추가 참조
>   - [명령줄 구문 키](command-line-syntax-key.md)
>   [쿼리](query.md)
>   [원격 데스크톱 서비스 (Terminal Services) 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
