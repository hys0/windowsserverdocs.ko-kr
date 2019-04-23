---
title: 인터페이스 포트 프록시에 대 한 Netsh 명령
description: Netsh 인터페이스 포트 프록시 명령을 사용 하 여 IPv4 및 IPv6 네트워크 및 응용 프로그램 간의 프록시 역할을 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: 194a418fe6b33e312a3f2529e82d50d76cd15f4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842484"
---
# <a name="netsh-interface-portproxy-commands"></a>Netsh 인터페이스 포트 프록시 명령

사용 된 **netsh 인터페이스 포트 프록시** IPv4 및 IPv6 네트워크 사이의 응용 프로그램 프록시로 작동 하는 명령입니다. 다음과 같은 방법으로 프록시 서비스를 설정 하려면 다음이 명령을 사용할 수 있습니다.

-   IPv4 구성 된 컴퓨터 및 응용 프로그램 다른 IPv4 구성 된 컴퓨터 및 응용 프로그램에 전송 된 메시지입니다.

-   IPv4 구성 된 컴퓨터 및 응용 프로그램 메시지가 IPv6 구성로 보내는 컴퓨터 및 응용 프로그램.

-   IPv6 구성 된 컴퓨터 및 응용 프로그램 메시지가 IPv4 구성로 보내는 컴퓨터 및 응용 프로그램.

-   IPv6 구성 된 컴퓨터 및 응용 프로그램 다른 IPv6 구성 된 컴퓨터 및 응용 프로그램에 전송 된 메시지입니다.

배치 파일 또는 이러한 명령을 사용 하 여 스크립트를 작성할 때 각 명령이 시작 해야 합니다 **netsh 인터페이스 포트 프록시**합니다. 예를 들어, 사용 하는 경우는 **v4tov6 삭제** 서버가 수신 대기 하는 IPv4 주소 목록에서 IPv4 포트 및 주소를 삭제 하는 포트 프록시 서버를 배치 파일 또는 스크립트에는 다음 구문을 사용 해야를 지정 하는 명령:

```PowerShell
netsh interface portproxy delete v4tov6listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

사용할 수 있는 netsh 인터페이스 포트 프록시 명령은 다음과 같습니다.

-   [add v4tov4](#add-v4tov4)

-   [add v4tov6](#add-v4tov6)

-   [add v6tov4](#add-v6tov4)

-   [add v6tov6](#add-v6tov6)

-   [delete v4tov4](#delete-v4tov4)

-   [delete v4tov6](#delete-v4tov6)

-   [delete v6tov6](#delete-v6tov6)

-   [reset](#reset)

-   [set v4tov4](#set-v4tov4)

-   [set v4tov6](#set-v4tov6)

-   [setv6tov4](#set-v6tov4)

-   [set v6tov6](#set-v6tov6)

-   [모두 표시](#show-all)

-   [show v4tov4](#show-v4tov4)

-   [show v4tov6](#show-v4tov6)

-   [show v6tov4](#show-v6tov4)

-   [show v6tov6](#show-v6tov6)


## <a name="add-v4tov4"></a>v4tov4 추가

포트 프록시 서버 포트 및 IPv4 주소를 별도 TCP 연결을 설정한 후에 받은 메시지를 보내는 특정 포트 및 IPv4 주소와 maps에 전송 된 메시지 수신 대기 합니다.

### <a name="syntax"></a>구문

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수


| | |
|-----|--------|----------|
| **listenport**     | 지정 포트 번호 또는 서비스는 IPv4 포트를 수신 하는 이름입니다.                                                                                                                      | 필수 |
| **connectaddress** | 에 연결 하는 데 IPv4 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **connectport**    | 포트 번호 또는 서비스에서 IPv4 포트를 지정 연결할 이름입니다. 하는 경우 **connectport** 지정 하지 않으면 기본값은 값 **listenport** 로컬 컴퓨터의 합니다.              |          |
| **listenaddress**  | 수신 하는 대 한 IPv4 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **protocol**       | 사용할 프로토콜을 지정 합니다.                                                                                                                                                                    |          |

## <a name="add-v4tov6"></a>v4tov6 추가

포트 프록시 서버 포트 및 IPv6 주소를 별도 TCP 연결을 설정한 후에 받은 메시지를 보내는 특정 포트 및 IPv4 주소를 지도에 전송 된 메시지 수신 대기 합니다.

### <a name="syntax"></a>구문

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|-----------|-------------|----------|
| **listenport**     | 지정 포트 번호 또는 서비스는 IPv4 포트를 수신 하는 이름입니다.       | 필수 |
| **connectaddress** | 연결 하려는 IPv6 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **connectport**    | 포트 번호 또는 서비스에서 IPv6 포트를 지정 연결할 이름입니다. 하는 경우 **connectport** 지정 하지 않으면 기본값은 값 **listenport** 로컬 컴퓨터의 합니다.              |          |
| **listenaddress**  | 수신 하는 IPv4 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다.  |          |
| **protocol**       | 사용할 프로토콜을 지정 합니다.                                                                                                                                                                    |          |

## <a name="add-v6tov4"></a>v6tov4 추가

특정 포트 및 IPv6 주소 및 포트 및 IPv4 주소를 별도 TCP 연결을 설정한 후에 받은 메시지를 보낼를 maps에 전송 된 메시지에 대 한 포트 프록시 서버가 수신 대기 합니다.

### <a name="syntax"></a>구문

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|------------|-------------|----------|
| **listenport**     | 지정 포트 번호 또는 서비스에서 IPv6 포트를 수신 하는 이름입니다.              | 필수 |
| **connectaddress** | 에 연결 하는 데 IPv4 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **connectport**    | 포트 번호 또는 서비스에서 IPv4 포트를 지정 연결할 이름입니다. 하는 경우 **connectport** 지정 하지 않으면 기본값은 값 **listenport** 로컬 컴퓨터의 합니다.              |          |
| **listenaddress**  | 수신 하는 IPv6 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다.  |          |
| **protocol**       | 사용할 프로토콜을 지정 합니다.      |          |

## <a name="add-v6tov6"></a>v6tov6 추가

특정 포트 및 IPv6 주소 및 포트 및 IPv6 주소를 별도 TCP 연결을 설정한 후에 받은 메시지를 보낼를 maps에 전송 된 메시지에 대 한 포트 프록시 서버가 수신 대기 합니다.

### <a name="syntax"></a>구문

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|-------------|------------------|----------|
| **listenport**     | 지정 포트 번호 또는 서비스에서 IPv6 포트를 수신 하는 이름입니다.       | 필수 |
| **connectaddress** | 연결 하려는 IPv6 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **connectport**    | 포트 번호 또는 서비스에서 IPv6 포트를 지정 연결할 이름입니다. 하는 경우 **connectport** 지정 하지 않으면 기본값은 값 **listenport** 로컬 컴퓨터의 합니다.              |          |
| **listenaddress**  | 수신 하는 IPv6 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다.  |          |
| **protocol**       | 사용할 프로토콜을 지정 합니다.                                                                                                                                                                    |          |

## <a name="delete-v4tov4"></a>delete v4tov4

포트 프록시 서버는 IPv4 포트 및 주소는 서버가 수신 대기 목록에서 IPv4 주소를 삭제 합니다.

### <a name="syntax"></a>구문

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|-------------------|----------------------------------------------------------------------------------------------------------|----------|
| **listenport**    | 삭제 하는 IPv4 포트를 지정 합니다.                                                                       | 필수 |
| **listenaddress** | 삭제 하려면 IPv4 주소를 지정 합니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **protocol**      | 사용할 프로토콜을 지정 합니다.                                                                           |          |

## <a name="delete-v4tov6"></a>delete v4tov6

포트 프록시 서버는 서버가 수신 대기 하는 IPv4 주소 목록에서 IPv4 포트 및 주소를 삭제 합니다.

### <a name="syntax"></a>구문

```PowerShell 
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|-------------------|----------------------------------------------------------------------------------------------------------|----------|
| **listenport**    | 삭제 하는 IPv4 포트를 지정 합니다.                                                                       | 필수 |
| **listenaddress** | 삭제 하려면 IPv4 주소를 지정 합니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **protocol**      | 사용할 프로토콜을 지정 합니다.                                                                           |          |

## <a name="delete-v6tov4"></a>v6tov4 삭제

포트 프록시 서버는 서버가 수신 대기 하는 IPv6 주소 목록에서 IPv6 포트 및 주소를 삭제 합니다.

### <a name="syntax"></a>구문

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|-------------------|----------------------------------------------------------------------------------------------------------|----------|
| **listenport**    | 삭제 하는 IPv6 포트를 지정 합니다.                                                                       | 필수 |
| **listenaddress** | 삭제 하려면 IPv6 주소를 지정 합니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **protocol**      | 사용할 프로토콜을 지정 합니다.                                                                           |          |

## <a name="delete-v6tov6"></a>v6tov6 삭제

포트 프록시 서버는 서버는 수신 대기 하는 IPv6 주소 목록에서 IPv6 주소를 삭제 합니다.

### <a name="syntax"></a>구문

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|-------------------|----------------------------------------------------------------------------------------------------------|----------|
| **listenport**    | 삭제 하는 IPv6 포트를 지정 합니다.                                                                       | 필수 |
| **listenaddress** | 삭제 하려면 IPv6 주소를 지정 합니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **protocol**      | 사용할 프로토콜을 지정 합니다.                                                                           |          |

## <a name="reset"></a>다시 설정

IPv6 구성 상태를 다시 설정합니다.

### <a name="syntax"></a>구문

`reset`

## <a name="set-v4tov4"></a>집합 v4tov4

사용 하 여 만든 포트 프록시 서버에 있는 기존 항목의 매개 변수 값을 수정 합니다 **v4tov4 추가** 명령, 또는 maps 포트/주소 쌍 목록에 새 항목을 추가 합니다.

### <a name="syntax"></a>구문

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|--------------------|---------------------------|----------|
| **listenport**     | 지정 포트 번호 또는 서비스는 IPv4 포트를 수신 하는 이름입니다.     | 필수 |
| **connectaddress** | 에 연결 하는 데 IPv4 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **connectport**    | 포트 번호 또는 서비스에서 IPv4 포트를 지정 연결할 이름입니다. 하는 경우 **connectport** 지정 하지 않으면 기본값은 값 **listenport** 로컬 컴퓨터의 합니다.              |          |
| **listenaddress**  | 수신 하는 대 한 IPv4 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **protocol**       | 사용할 프로토콜을 지정 합니다.                                                                                                                                                                    |          |

## <a name="set-v4tov6"></a>집합 v4tov6

사용 하 여 만든 포트 프록시 서버에 있는 기존 항목의 매개 변수 값을 수정 합니다 **v4tov6 추가** 명령, 또는 maps 포트/주소 쌍 목록에 새 항목을 추가 합니다.

### <a name="syntax"></a>구문

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|--------------------|---------------------|----------|
| **listenport**     | 지정 포트 번호 또는 서비스는 IPv4 포트를 수신 하는 이름입니다.     | 필수 |
| **connectaddress** | 연결 하려는 IPv6 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **connectport**    | 포트 번호 또는 서비스에서 IPv6 포트를 지정 연결할 이름입니다. 하는 경우 **connectport** 지정 하지 않으면 기본값은 값 **listenport** 로컬 컴퓨터의 합니다.              |          |
| **listenaddress**  | 수신 하는 IPv4 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다.  |          |
| **protocol**       | 사용할 프로토콜을 지정 합니다.                                                                                                                                                                    |          |

## <a name="set-v6tov4"></a>집합 v6tov4

사용 하 여 만든 포트 프록시 서버에 있는 기존 항목의 매개 변수 값을 수정 합니다 **v6tov4 추가** 명령, 또는 maps 포트/주소 쌍 목록에 새 항목을 추가 합니다.

### <a name="syntax"></a>구문

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|--------------------|----------------------|----------|
| **listenport**     | 지정 포트 번호 또는 서비스에서 IPv6 포트를 수신 하는 이름입니다.      | 필수 |
| **connectaddress** | 에 연결 하는 데 IPv4 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |          |
| **connectport**    | 포트 번호 또는 서비스에서 IPv4 포트를 지정 연결할 이름입니다. 하는 경우 **connectport** 지정 하지 않으면 기본값은 값 **listenport** 로컬 컴퓨터의 합니다.              |          |
| **listenaddress**  | 수신 하는 IPv6 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다.  |          |
| **protocol**       | 사용할 프로토콜을 지정 합니다.                                                                                                                                                                    |          |

## <a name="set-v6tov6"></a>집합 v6tov6

사용 하 여 만든 포트 프록시 서버에 있는 기존 항목의 매개 변수 값을 수정 합니다 **v6tov6 추가** 명령, 또는 maps 포트/주소 쌍 목록에 새 항목을 추가 합니다.

### <a name="syntax"></a>구문

```PowerShell 
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|   |   |
|--------------------|-------------------------|----------|
| **listenport**     | 지정 포트 번호 또는 서비스에서 IPv6 포트를 수신 하는 이름입니다.   | 필수 |
| **connectaddress** | 연결 하려는 IPv6 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다.  |          |
| **connectport**    | 포트 번호 또는 서비스에서 IPv6 포트를 지정 연결할 이름입니다. 하는 경우 **connectport** 지정 하지 않으면 기본값은 값 **listenport** 로컬 컴퓨터의 합니다.               |          |
| **listenaddress**  | 수신 하는 IPv6 주소를 지정 합니다. 허용 되는 값에는 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름이 됩니다. 주소를 지정 하지 않으면 경우는 기본값은 로컬 컴퓨터입니다. |          |
| **protocol**       | 사용할 프로토콜을 지정 합니다.                                                                                                                                                                     |          |

## <a name="show-all"></a>모두 표시

V4tov4, v4tov6, v6tov4, 및 v6tov6에 대 한 포트/주소 쌍을 포함 하 여 모든 포트 프록시 매개 변수를 표시 합니다.

### <a name="syntax"></a>구문

`show all`


## <a name="show-v4tov4"></a>v4tov4 표시

V4tov4 포트 프록시 매개 변수를 표시합니다.

### <a name="syntax"></a>구문

`show v4tov4`

## <a name="show-v4tov6"></a>v4tov6 표시

V4tov6 포트 프록시 매개 변수를 표시합니다.

### <a name="syntax"></a>구문

`show v4tov6`

## <a name="show-v6tov4"></a>v6tov4 표시

V6tov4 포트 프록시 매개 변수를 표시합니다.

### <a name="syntax"></a>구문

`show v6tov4`


## <a name="show-v6tov6"></a>v6tov6 표시

V6tov6 포트 프록시 매개 변수를 표시합니다.

### <a name="syntax"></a>구문

`show v6tov6`

---
