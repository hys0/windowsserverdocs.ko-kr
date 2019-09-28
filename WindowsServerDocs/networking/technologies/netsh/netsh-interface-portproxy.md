---
title: 인터페이스 portproxy Netsh 명령
description: Netsh interface portproxy 명령을 사용 하 여 IPv4 및 IPv6 네트워크와 응용 프로그램 간의 프록시로 작동 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: 6244213ea689f07230ce53288e52959972112037
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405505"
---
# <a name="netsh-interface-portproxy-commands"></a>Netsh 인터페이스 포트 프록시 명령

**Netsh interface portproxy** 명령을 사용 하 여 IPv4 및 IPv6 네트워크와 응용 프로그램 간의 프록시로 작동 합니다. 이러한 명령을 사용 하 여 다음과 같은 방법으로 프록시 서비스를 설정할 수 있습니다.

-   Ipv4로 구성 된 컴퓨터 및 응용 프로그램 메시지가 다른 IPv4 구성 컴퓨터 및 응용 프로그램으로 전송 되었습니다.

-   IPv6로 구성 된 컴퓨터 및 응용 프로그램에 전송 된 IPv4 구성 컴퓨터 및 응용 프로그램 메시지입니다.

-   IPv4로 구성 된 컴퓨터 및 응용 프로그램에 전송 된 IPv6 구성 컴퓨터 및 응용 프로그램 메시지입니다.

-   Ipv6로 구성 된 컴퓨터 및 응용 프로그램 메시지가 다른 IPv6 구성 컴퓨터 및 응용 프로그램으로 전송 됩니다.

이러한 명령을 사용 하 여 배치 파일 또는 스크립트를 작성할 때는 각 명령이 **netsh interface portproxy**로 시작 해야 합니다. 예를 들어 **delete v4tov6** 명령을 사용 하 여 서버에서 수신 대기 하는 ipv4 주소 목록에서 Portproxy 서버가 ipv4 포트와 주소를 삭제 하도록 지정 하는 경우 배치 파일이 나 스크립트는 다음 구문을 사용 해야 합니다.

```PowerShell
netsh interface portproxy delete v4tov6listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

사용 가능한 netsh interface portproxy 명령은 다음과 같습니다.

-   [v4tov4 추가](#add-v4tov4)

-   [v4tov6 추가](#add-v4tov6)

-   [v6tov4 추가](#add-v6tov4)

-   [v6tov6 추가](#add-v6tov6)

-   [v4tov4 삭제](#delete-v4tov4)

-   [v4tov6 삭제](#delete-v4tov6)

-   [v6tov6 삭제](#delete-v6tov6)

-   [reset](#reset)

-   [v4tov4 설정](#set-v4tov4)

-   [v4tov6 설정](#set-v4tov6)

-   [setv6tov4](#set-v6tov4)

-   [v6tov6 설정](#set-v6tov6)

-   [모두 표시](#show-all)

-   [v4tov4 표시](#show-v4tov4)

-   [v4tov6 표시](#show-v4tov6)

-   [v6tov4 표시](#show-v6tov4)

-   [v6tov6 표시](#show-v6tov6)


## <a name="add-v4tov4"></a>v4tov4 추가

Portproxy 서버는 특정 포트와 IPv4 주소로 전송 된 메시지를 수신 대기 하 고 포트 및 IPv4 주소를 매핑하여 별도의 TCP 연결을 설정한 후 받은 메시지를 보냅니다.

### <a name="syntax"></a>구문

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수


|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           수신 대기할 IPv4 포트 (포트 번호 또는 서비스 이름)를 지정 합니다.                                                            |
| **connectaddress** | 연결할 IPv4 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|  **connectport**   |       연결할 IPv4 포트 (포트 번호 또는 서비스 이름)를 지정 합니다. **Connectport** 를 지정 하지 않으면 기본값은 로컬 컴퓨터의 **listenport** 값입니다.        |
| **listenaddress**  | 수신 대기할 IPv4 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|    **프로토콜만**    |                                                                                  사용할 프로토콜을 지정 합니다.                                                                                   |

## <a name="add-v4tov6"></a>v4tov6 추가

Portproxy 서버는 특정 포트와 IPv4 주소로 전송 되는 메시지를 수신 대기 하 고 포트 및 IPv6 주소를 매핑하여 별도의 TCP 연결을 설정한 후 받은 메시지를 보냅니다.

### <a name="syntax"></a>구문

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           수신 대기할 IPv4 포트 (포트 번호 또는 서비스 이름)를 지정 합니다.                                                            |
| **connectaddress** | 연결할 IPv6 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|  **connectport**   |       연결할 IPv6 포트 (포트 번호 또는 서비스 이름)를 지정 합니다. **Connectport** 를 지정 하지 않으면 기본값은 로컬 컴퓨터의 **listenport** 값입니다.        |
| **listenaddress**  | 수신 대기할 IPv4 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다.  |
|    **프로토콜만**    |                                                                                  사용할 프로토콜을 지정 합니다.                                                                                   |

## <a name="add-v6tov4"></a>v6tov4 추가

Portproxy 서버는 특정 포트 및 IPv6 주소로 전송 된 메시지를 수신 대기 하 고 별도의 TCP 연결을 설정한 후 받은 메시지를 보낼 포트 및 IPv4 주소를 매핑합니다.

### <a name="syntax"></a>구문

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           수신할 포트 번호 또는 서비스 이름으로 IPv6 포트를 지정 합니다.                                                            |
| **connectaddress** | 연결할 IPv4 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|  **connectport**   |       연결할 IPv4 포트 (포트 번호 또는 서비스 이름)를 지정 합니다. **Connectport** 를 지정 하지 않으면 기본값은 로컬 컴퓨터의 **listenport** 값입니다.        |
| **listenaddress**  | 수신할 IPv6 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다.  |
|    **프로토콜만**    |                                                                                  사용할 프로토콜을 지정 합니다.                                                                                   |

## <a name="add-v6tov6"></a>v6tov6 추가

Portproxy 서버는 특정 포트 및 IPv6 주소로 전송 된 메시지를 수신 대기 하 고 별도의 TCP 연결을 설정한 후 받은 메시지를 보낼 포트 및 IPv6 주소를 매핑합니다.

### <a name="syntax"></a>구문

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           수신할 포트 번호 또는 서비스 이름으로 IPv6 포트를 지정 합니다.                                                            |
| **connectaddress** | 연결할 IPv6 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|  **connectport**   |       연결할 IPv6 포트 (포트 번호 또는 서비스 이름)를 지정 합니다. **Connectport** 를 지정 하지 않으면 기본값은 로컬 컴퓨터의 **listenport** 값입니다.        |
| **listenaddress**  | 수신할 IPv6 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다.  |
|    **프로토콜만**    |                                                                                  사용할 프로토콜을 지정 합니다.                                                                                   |

## <a name="delete-v4tov4"></a>v4tov4 삭제

Portproxy 서버는 서버에서 수신 대기 하는 IPv4 포트 및 주소 목록에서 IPv4 주소를 삭제 합니다.

### <a name="syntax"></a>구문

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    삭제할 IPv4 포트를 지정 합니다.                                    |
| **listenaddress** | 삭제할 IPv4 주소를 지정 합니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|   **프로토콜만**    |                                      사용할 프로토콜을 지정 합니다.                                      |

## <a name="delete-v4tov6"></a>v4tov6 삭제

Portproxy 서버는 서버에서 수신 대기 하는 IPv4 주소 목록에서 IPv4 포트 및 주소를 삭제 합니다.

### <a name="syntax"></a>구문

```PowerShell 
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    삭제할 IPv4 포트를 지정 합니다.                                    |
| **listenaddress** | 삭제할 IPv4 주소를 지정 합니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|   **프로토콜만**    |                                      사용할 프로토콜을 지정 합니다.                                      |

## <a name="delete-v6tov4"></a>v6tov4 삭제

Portproxy 서버는 서버가 수신 하는 IPv6 주소 목록에서 IPv6 포트 및 주소를 삭제 합니다.

### <a name="syntax"></a>구문

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    삭제할 IPv6 포트를 지정 합니다.                                    |
| **listenaddress** | 삭제할 IPv6 주소를 지정 합니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|   **프로토콜만**    |                                      사용할 프로토콜을 지정 합니다.                                      |

## <a name="delete-v6tov6"></a>v6tov6 삭제

Portproxy 서버는 서버가 수신 하는 IPv6 주소 목록에서 IPv6 주소를 삭제 합니다.

### <a name="syntax"></a>구문

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    삭제할 IPv6 포트를 지정 합니다.                                    |
| **listenaddress** | 삭제할 IPv6 주소를 지정 합니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|   **프로토콜만**    |                                      사용할 프로토콜을 지정 합니다.                                      |

## <a name="reset"></a>다시 설정

IPv6 구성 상태를 다시 설정 합니다.

### <a name="syntax"></a>구문

`reset`

## <a name="set-v4tov4"></a>v4tov4 설정

**Add v4tov4** 명령을 사용 하 여 만든 portproxy 서버에서 기존 항목의 매개 변수 값을 수정 하거나 포트/주소 쌍을 매핑하는 목록에 새 항목을 추가 합니다.

### <a name="syntax"></a>구문

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           수신 대기할 IPv4 포트 (포트 번호 또는 서비스 이름)를 지정 합니다.                                                            |
| **connectaddress** | 연결할 IPv4 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|  **connectport**   |       연결할 IPv4 포트 (포트 번호 또는 서비스 이름)를 지정 합니다. **Connectport** 를 지정 하지 않으면 기본값은 로컬 컴퓨터의 **listenport** 값입니다.        |
| **listenaddress**  | 수신 대기할 IPv4 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|    **프로토콜만**    |                                                                                  사용할 프로토콜을 지정 합니다.                                                                                   |

## <a name="set-v4tov6"></a>v4tov6 설정

**Add v4tov6** 명령을 사용 하 여 만든 portproxy 서버에서 기존 항목의 매개 변수 값을 수정 하거나 포트/주소 쌍을 매핑하는 목록에 새 항목을 추가 합니다.

### <a name="syntax"></a>구문

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           수신 대기할 IPv4 포트 (포트 번호 또는 서비스 이름)를 지정 합니다.                                                            |
| **connectaddress** | 연결할 IPv6 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|  **connectport**   |       연결할 IPv6 포트 (포트 번호 또는 서비스 이름)를 지정 합니다. **Connectport** 를 지정 하지 않으면 기본값은 로컬 컴퓨터의 **listenport** 값입니다.        |
| **listenaddress**  | 수신 대기할 IPv4 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다.  |
|    **프로토콜만**    |                                                                                  사용할 프로토콜을 지정 합니다.                                                                                   |

## <a name="set-v6tov4"></a>v6tov4 설정

**Add v6tov4** 명령을 사용 하 여 만든 portproxy 서버에서 기존 항목의 매개 변수 값을 수정 하거나 포트/주소 쌍을 매핑하는 목록에 새 항목을 추가 합니다.

### <a name="syntax"></a>구문

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           수신할 포트 번호 또는 서비스 이름으로 IPv6 포트를 지정 합니다.                                                            |
| **connectaddress** | 연결할 IPv4 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다. |
|  **connectport**   |       연결할 IPv4 포트 (포트 번호 또는 서비스 이름)를 지정 합니다. **Connectport** 를 지정 하지 않으면 기본값은 로컬 컴퓨터의 **listenport** 값입니다.        |
| **listenaddress**  | 수신할 IPv6 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다.  |
|    **프로토콜만**    |                                                                                  사용할 프로토콜을 지정 합니다.                                                                                   |

## <a name="set-v6tov6"></a>v6tov6 설정

**Add v6tov6** 명령을 사용 하 여 만든 portproxy 서버에서 기존 항목의 매개 변수 값을 수정 하거나 포트/주소 쌍을 매핑하는 목록에 새 항목을 추가 합니다.

### <a name="syntax"></a>구문

```PowerShell 
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>매개 변수

|                    |                                                                                                                                                                                                    |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                            수신할 포트 번호 또는 서비스 이름으로 IPv6 포트를 지정 합니다.                                                            |
| **connectaddress** | 연결할 IPv6 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소가 지정 되지 않은 경우 기본값은 로컬 컴퓨터입니다.  |
|  **connectport**   |        연결할 IPv6 포트 (포트 번호 또는 서비스 이름)를 지정 합니다. **Connectport** 를 지정 하지 않으면 기본값은 로컬 컴퓨터의 **listenport** 값입니다.        |
| **listenaddress**  | 수신할 IPv6 주소를 지정 합니다. 허용 되는 값은 IP 주소, 컴퓨터 NetBIOS 이름 또는 컴퓨터 DNS 이름입니다. 주소를 지정 하지 않으면 기본값은 로컬 컴퓨터입니다. |
|    **프로토콜만**    |                                                                                   사용할 프로토콜을 지정 합니다.                                                                                   |

## <a name="show-all"></a>모두 표시

V4tov4, v4tov6, v6tov4 및 v6tov6에 대 한 포트/주소 쌍을 포함 하 여 모든 portproxy 매개 변수를 표시 합니다.

### <a name="syntax"></a>구문

`show all`


## <a name="show-v4tov4"></a>v4tov4 표시

V4tov4 portproxy 매개 변수를 표시 합니다.

### <a name="syntax"></a>구문

`show v4tov4`

## <a name="show-v4tov6"></a>v4tov6 표시

V4tov6 portproxy 매개 변수를 표시 합니다.

### <a name="syntax"></a>구문

`show v4tov6`

## <a name="show-v6tov4"></a>v6tov4 표시

V6tov4 portproxy 매개 변수를 표시 합니다.

### <a name="syntax"></a>구문

`show v6tov4`


## <a name="show-v6tov6"></a>v6tov6 표시

V6tov6 portproxy 매개 변수를 표시 합니다.

### <a name="syntax"></a>구문

`show v6tov6`

---
