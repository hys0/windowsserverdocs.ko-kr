---
title: netcfg
description: 워크스테이션을 배포 하는 데 사용 되는 경량 버전의 Windows 인 WinPE (Windows 사전 설치 환경)를 설치 하는 netcfg 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6910f7e3f3d2f100942897bd9712293f7eb0f4d9
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354263"
---
# <a name="netcfg"></a>netcfg

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 사전 설치 환경 (WinPE) 워크스테이션을 배포 하는 데 사용 되는 Windows의 경량 버전을 설치 합니다.

## <a name="syntax"></a>구문

```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| /v | 자세한 정보 표시 모드에서 실행 됩니다. |
| /e | 설치 및 제거 중에 서비스 환경 변수를 사용 합니다. |
| /winpe | WinPE (Windows 사전 설치 환경) 용 TCP/IP, NetBIOS 및 Microsoft 클라이언트를 설치 합니다. |
| /l | INF 파일의 위치를 제공 합니다. |
| /C | 설치할 구성 요소의 클래스를 제공 합니다. **프로토콜**, **서비스**또는 **클라이언트**입니다. |
| /i | 구성 요소 ID를 제공 합니다. |
| /s | 어댑터에 대 한 **\ta** 또는 net 구성 요소의 **n** 을 포함 하 여 표시할 구성 요소의 유형을 제공 합니다. |
| /b | 경로 이름을 포함 하는 문자열이 뒤에 오는 경우 바인딩 경로를 표시 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |                                                    |

### <a name="examples"></a>예

C:\oemdir\example.inf를 사용 하 여 프로토콜 *예제* 를 설치 하려면 다음을 입력 합니다.

```
netcfg /l c:\oemdir\example.inf /c p /i example
```

*MS_Server* 서비스를 설치 하려면 다음을 입력 합니다.

```
netcfg /c s /i MS_Server
```

Windows 사전 설치 환경에 대 한 TCP/IP, NetBIOS 및 Microsoft 클라이언트를 설치 하려면 다음을 입력 합니다.

```
netcfg /v /winpe
```

구성 요소 *MS_IPX* 설치 되어 있는지 여부를 표시 하려면 다음을 입력 합니다.

```
netcfg /q MS_IPX
```

구성 요소 *MS_IPX*를 제거 하려면 다음을 입력 합니다.

```
netcfg /u MS_IPX
```

설치 된 모든 net 구성 요소를 표시 하려면 다음을 입력 합니다.

```
netcfg /s n
```

*MS_TCPIP*포함 된 바인딩 경로를 표시 하려면 다음을 입력 합니다.

```
netcfg /b ms_tcpip
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
