---
title: rpcinfo
description: 원격 컴퓨터에서 프로그램을 나열 하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c342232-a8f0-42ff-8f11-d18c4981f5ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: d25a806c63f959ec659a6dd692d9efd5b394a64c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820093"
---
# <a name="rpcinfo"></a>rpcinfo

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에서 프로그램을 나열합니다. **rpcinfo** 명령줄 유틸리티는 원격 프로시저 호출 (RPC) RPC 서버를 하 고 그 결과 보고 합니다.

## <a name="syntax"></a>구문
```
rpcinfo [/p [<Node>]] [/b <Program version>] [/t <Node Program> [<version>]] [/u <Node Program> [<version>]]
```

#### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/p [ \< Node>]|지정 된 호스트에 포트 매퍼를 사용 하 여 등록 된 모든 프로그램을 나열 합니다. 노드 (컴퓨터) 이름을 지정 하지 않는 경우 로컬 호스트의 포트 매퍼 프로그램에 쿼리 합니다.|
|/b \< 프로그램 버전>|지정 된 프로그램 및 포트 매퍼에 등록 하는 버전에 있는 모든 네트워크 노드에서 응답을 요청 합니다. 프로그램 이름 또는 번호와 버전 번호를 지정 해야 합니다.|
|/t \< 노드 프로그램> [ \< 버전>]|지정된 된 프로그램을 호출 하는 TCP 전송 프로토콜을 사용 합니다. 노드 (컴퓨터) 이름과 프로그램 이름을 모두 지정 해야 합니다. 버전을 지정 하지 않으면 프로그램 모든 버전을 호출 합니다.|
|/u \< 노드 프로그램> [ \< 버전>]|지정된 된 프로그램을 호출 하는 UDP 전송 프로토콜을 사용 합니다. 노드 (컴퓨터) 이름과 프로그램 이름을 모두 지정 해야 합니다. 버전을 지정 하지 않으면 프로그램 모든 버전을 호출 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="examples"></a>예
모든 프로그램에 등록 된 포트 맵 편집기를 나열 하려면 다음을 입력 합니다.
```
rpcinfo /p [<Node>]
```
지정된 된 프로그램에 있는 네트워크 노드에서 응답을 요청 하려면 다음을 입력 합니다.
```
rpcinfo /b <Program version>
```
프로그램을 호출 하 여 전송 제어 프로토콜 (TCP)을 사용 하려면 다음을 입력 합니다.
```
rpcinfo /t <Node Program> [<version>]
```
사용자 데이터 그램 프로토콜 (UDP)를 사용 하 여 프로그램을 호출 합니다.
```
rpcinfo /u <Node Program> [<version>]
```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
