---
title: netcfg
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c636b9a14d9dcee6f37409557ed2bcb87b1087d
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820873"
---
# <a name="netcfg"></a>netcfg

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 사전 설치 환경 (WinPE) 워크스테이션을 배포 하는 데 사용 되는 Windows의 경량 버전을 설치 합니다.
## <a name="syntax"></a>구문
```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```
#### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/v|**자세한 정보** 표시 모드에서 실행|
|/e|설치 및 제거 중 서비스 **환경** 변수 사용|
|/winpe|WinPE (Windows 사전 설치 환경) 용 TCP/IP, NetBIOS 및 Microsoft 클라이언트를 설치 합니다.|
|/l|INF의 **위치** 를 제공 합니다.|
|/C|설치할 구성 요소의 **클래스** 를 제공 합니다. 프로토콜, 서비스 또는 클라이언트|
|/i|구성 요소 **ID** 를 제공 합니다.|
|/s|**표시할**구성 요소의 형식을 제공 합니다.<p>\ta 어댑터, n = = net 구성 요소|
|/b|경로 이름을 포함 하는 문자열이 뒤에 오는 경우 **바인딩 경로**를 표시 합니다.|
|/?|명령 프롬프트에서 **도움말** 을 표시 합니다.|

## <a name="examples"></a>예

프로토콜을 설치 하려면 *예제* c:\oemdir\example.inf를 사용 하 여:
```
netcfg /l c:\oemdir\example.inf /c p /i example
```
설치 하는 *MS_Server* 서비스:
```
netcfg /c s /i MS_Server
```
Windows 사전 설치 환경에 대 한 TCP/IP, NetBIOS 및 Microsoft 클라이언트를 설치 하려면
```
netcfg /v /winpe
```
경우 구성 요소를 표시 하려면 *MS_IPX* 가 설치 되어 있습니다.
```
netcfg /q MS_IPX
```
구성 요소를 제거 하려면 *MS_IPX*:
```
netcfg /u MS_IPX
```
모두 표시 하려면 net 구성 요소를 설치 합니다.
```
netcfg /s n
```
*MS_TCPIP*를 포함 하는 바인딩 경로를 표시 하려면:
```
netcfg /b ms_tcpip
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
