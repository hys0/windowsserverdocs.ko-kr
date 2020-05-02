---
title: 연결 끊기-클라이언트
description: 멀티 캐스트 전송 또는 네임 스페이스에서 클라이언트의 연결을 끊는 클라이언트의 연결 끊기에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 541e2e0acfa51d7b63cf6cfb27ff42874760e37d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720950"
---
# <a name="disconnect-client"></a>연결 끊기-클라이언트

멀티 캐스트 전송 또는 네임 스페이스의 클라이언트 연결을 끊습니다. 지정 하지 않으면 **/force**, 클라이언트도 대체 됩니다 다른 전송 메서드 (클라이언트에서이 기능을 지원) 하는 경우.

## <a name="syntax"></a>구문

```
WDSUTIL /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/ClientId:\<클라이언트 ID>|연결을 끊을 클라이언트의 ID를 지정 합니다. 클라이언트의 ID를 보려면 입력 **WDSUTIL /get-multicasttransmission /show:clients**합니다.|
|[/Server:\<서버 이름>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|[/Force]|설치를 완전히 중지 하 고 대체 (fallback) 메서드를 사용 하지 않습니다. 참고 Wdsmcast.exe 모든 대체 메커니즘을 지원 하지 않습니다. 이 옵션을 사용 하지 않는 경우 기본 동작은 다음과 같습니다.</br>-Windows 배포 서비스 클라이언트를 사용 하는 경우 클라이언트는 유 니 캐스팅을 사용 하 여 설치를 계속 합니다.</br>-Windows 배포 서비스 클라이언트를 사용 하지 않는 경우 설치가 실패 합니다.</br>중요: 설치가 실패 하 고 사용할 수 없는 상태로 컴퓨터가 방치 될 수 있으므로 주의 해 서이 옵션을 사용 해야 합니다.|

## <a name="examples"></a>예

클라이언트 연결을 끊으려면 다음을 입력 합니다.
```
WDSUTIL /Disconnect-Client /ClientId:1
```
클라이언트 연결을 끊을 강제 설치 실패를 입력 합니다.
```
WDSUTIL /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)