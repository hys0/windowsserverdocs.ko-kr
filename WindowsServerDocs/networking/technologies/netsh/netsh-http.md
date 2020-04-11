---
title: HTTP(Hypertext Transfer Protocol)용 Netsh 명령
description: netsh http를 사용하여 HTTP.sys 설정 및 매개 변수를 쿼리하고 구성합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
manager: dougkim
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 81053e71040d2a0cd125af9fb7f3802dfd535781
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853756"
---
# <a name="netsh-http-commands"></a>Netsh http 명령


**netsh http**를 사용하여 HTTP.sys 설정 및 매개 변수를 쿼리하고 구성합니다.  

>[!TIP]
>Windows Server 2016 또는 Windows 10을 실행하는 컴퓨터에서 Windows PowerShell을 사용하는 경우 **netsh**를 입력하고 Enter 키를 누릅니다. netsh 프롬프트에서 **http**를 입력하고 Enter 키를 눌러 netsh http 프롬프트를 가져옵니다.
>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh http\>

사용 가능한 netsh http 명령은 다음과 같습니다.

- [add iplisten](#add-iplisten)
- [add sslcert](#add-sslcert)
- [add timeout](#add-timeout)
- [add urlacl](#add-urlacl)
- [delete cache](#delete-cache)
- [delete iplisten](#delete-iplisten)
- [delete sslcert](#delete-sslcert)
- [delete timeout](#delete-timeout)
- [delete urlacl](#delete-urlacl)
- [flush logbuffer](#flush-logbuffer)
- [show cachestate](#show-cachestate)
- [show iplisten](#show-iplisten)
- [show servicestate](#show-servicestate)
- [show sslcert](#show-sslcert)
- [show timeout](#show-timeout)
- [show urlacl](#show-urlacl)

## <a name="add-iplisten"></a>add iplisten

포트 번호를 제외하고 IP 수신 대기 목록에 새 IP 주소를 추가합니다.

**구문**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**매개 변수**

|               |                                                                                                                                                                                                                          |          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipaddress** | IP 수신 대기 목록에 추가할 IPv4 또는 IPv6 주소입니다. IP 수신 대기 목록은 HTTP 서비스가 바인딩되는 주소 목록의 범위를 결정하는 데 사용됩니다. "0.0.0.0"은 IPv4 주소를 의미하고 "::"은 IPv6 주소를 의미합니다. | 필수 |

---

**예제**

다음은 **add iplisten** 명령의 네 가지 예입니다.

-   add iplisten ipaddress=fe80::1
-   add iplisten ipaddress=1.1.1.1
-   add iplisten ipaddress=0.0.0.0
-   add iplisten ipaddress=::

---

## <a name="add-sslcert"></a>add sslcert

IP 주소 및 포트에 대한 새 SSL 서버 인증서 바인딩과 해당 클라이언트 인증서 정책을 추가합니다.

**구문**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**매개 변수**


|                                              |                                                                                                                                                                                          |          |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|                  **ipport**                  |                       바인딩의 IP 주소 및 포트를 지정합니다. 콜론 문자(:)는 IP 주소와 포트 번호 사이의 구분 기호로 사용됩니다.                        | 필수 |
|                 **certhash**                 |                                     인증서의 SHA 해시를 지정합니다. 이 해시는 20바이트 길이이며 16진수 문자열로 지정됩니다.                                      | 필수 |
|                  **appid**                   |                                                                  소유 애플리케이션을 식별하는 GUID를 지정합니다.                                                                  | 필수 |
|              **certstorename**               |                                  인증서의 저장소 이름을 지정합니다. 기본값은 MY입니다. 인증서는 로컬 머신 컨텍스트에 저장해야 합니다.                                  | 선택 |
|        **verifyclientcertrevocation**        |                                                      클라이언트 인증서의 해지 확인을 설정/해제하도록 지정합니다.                                                       | 선택 |
| **verifyrevocationwithcachedclientcertonly** |                                      해지 확인에 캐시된 클라이언트 인증서만 사용하도록 설정할 것인지 아니면 사용하지 않을 것인지 지정합니다.                                       | 선택 |
|                **usagecheck**                |                                                      사용량 확인의 사용 여부를 지정합니다. 기본값은 사용입니다.                                                       | 선택 |
|         **revocationfreshnesstime**          | 업데이트된 CRL(인증서 해지 목록)을 확인하는 간격(초)을 지정합니다. 이 값이 0이면 이전 CRL이 만료된 경우에만 새 CRL이 업데이트됩니다. | 선택 |
|           **urlretrievaltimeout**            |                            여기서 지정한 제한 시간 간격(밀리초)이 지나면 원격 URL의 인증서 해지 목록을 검색하려고 시도합니다.                            | 선택 |
|             **sslctlidentifier**             |                신뢰할 수 있는 인증서 발급자 목록을 지정합니다. 이 목록은 컴퓨터에서 신뢰할 수 있는 인증서 발급자의 하위 세트일 수 있습니다.                 | 선택 |
|             **sslctlstorename**              |                                                SslCtlIdentifier가 저장된 LOCAL_MACHINE 아래의 인증서 저장소 이름을 지정합니다.                                                | 선택 |
|              **dsmapperusage**               |                                                        DS 매퍼의 사용 여부를 지정합니다. 기본값은 사용 안 함입니다.                                                         | 선택 |
|          **clientcertnegotiation**           |                                              인증서 협상의 사용 여부를 지정합니다. 기본값은 사용 안 함입니다.                                               | 선택 |

---

**예제**

다음은 **add sslcert** 명령의 예입니다.

add sslcert ipport=1.1.1.1:443 certhash=0102030405060708090A0B0C0D0E0F1011121314 appid={00112233-4455-6677-8899- AABBCCDDEEFF}

---

## <a name="add-timeout"></a>add timeout

서비스에 글로벌 시간 제한을 추가합니다.

**구문** 

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**매개 변수**

|                 |                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------|
| **timeouttype** |                                    설정의 시간 제한 유형입니다.                                     |
|    **value**    | 제한 시간 갑(초)입니다. 이 값이 16진수 표기법이면 접두사 0x를 추가합니다. |

---

**예제**

다음은 **add timeout** 명령의 두 가지 예입니다.

-   add timeout timeouttype=idleconnectiontimeout value=120
-   add timeout timeouttype=headerwaittimeout value=0x40

---

## <a name="add-urlacl"></a>add urlacl

URL(Uniform Resource Locator) 예약 항목을 추가합니다. 이 명령은 관리자가 아닌 사용자 및 계정의 URL을 예약합니다. DACL은 수신 및 대리자 매개 변수를 사용하는 NT 계정 이름 또는 SDDL 문자열을 사용하여 지정할 수 있습니다.

**구문**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**매개 변수**

|              |                                                                                                                                                  |          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|   **url**    |                                          정규화된 URL(Uniform Resource Locator)을 지정합니다.                                           | 필수 |
|   **user**   |                                                      사용자 또는 사용자 그룹 이름을 지정합니다.                                                       | 필수 |
|  **listen**  | 다음 값 중 하나를 지정합니다. 예: 사용자가 URL을 등록할 수 있도록 허용합니다. 기본값입니다. 아니요: 사용자가 URL을 등록할 수 없습니다. | 선택 |
| **delegate** |  다음 값 중 하나를 지정합니다. 예: 사용자가 URL을 위임할 수 있도록 허용합니다. 아니요: 사용자가 URL을 위임할 수 없습니다. 기본값입니다.  | 선택 |
|   **sddl**   |                                                DACL을 설명하는 SDDL 문자열을 지정합니다.                                                 | 선택 |

---

**예제**

다음은 **add urlacl** 명령의 네 가지 예입니다.

- add urlacl url=https://+:80/MyUri user=DOMAIN\\ user
- add urlacl url=<https://www.contoso.com:80/MyUri> user=DOMAIN\\user listen=yes
- add urlacl url=<https://www.contoso.com:80/MyUri> user=DOMAIN\\user delegate=no
- add urlacl url=https://+:80/MyUri sddl=...

---

## <a name="delete-cache"></a>delete cache

HTTP 서비스 커널 URI 캐시에서 모든 항목 또는 지정된 항목을 삭제합니다.

**구문**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**매개 변수**

|               |                                                                                                                              |          |
|---------------|------------------------------------------------------------------------------------------------------------------------------|----------|
|    **url**    |                    삭제할 정규화된 URL(Uniform Resource Locator)을 지정합니다.                     | 선택 |
| **recursive** | url 캐시 아래의 모든 항목을 제거할지 여부를 지정합니다. **예**: 모든 항목 제거 **아니요**: 모든 항목을 제거하지 않음 | 선택 |

---

**예제**

다음은 **delete cache** 명령의 두 가지 예입니다.

- delete cache url=<https://www.contoso.com:80/myresource/> recursive=yes
- delete cache

---

## <a name="delete-iplisten"></a>delete iplisten

IP 수신 대기 목록에서 IP 주소를 삭제합니다. IP 수신 대기 목록은 HTTP 서비스가 바인딩되는 주소 목록의 범위를 결정하는 데 사용됩니다.

**구문**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**매개 변수**

|               |                                                                                                                                                                                                                                                                     |          |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipaddress** | IP 수신 대기 목록에서 삭제할 IPv4 또는 IPv6 주소입니다. IP 수신 대기 목록은 HTTP 서비스가 바인딩되는 주소 목록의 범위를 결정하는 데 사용됩니다. "0.0.0.0"은 IPv4 주소를 의미하고 "::"은 IPv6 주소를 의미합니다. 포트 번호는 포함되지 않습니다. | 필수 |

---


**예제**

다음은 **delete iplisten** 명령의 네 가지 예입니다.

-   delete iplisten ipaddress=fe80::1
-   delete iplisten ipaddress=1.1.1.1
-   delete iplisten ipaddress=0.0.0.0
-   delete iplisten ipaddress=::

---

## <a name="delete-sslcert"></a>delete sslcert


IP 주소 및 포트에 대한 SSL 서버 인증서 바인딩과 해당 클라이언트 인증서 정책을 삭제합니다.

**구문**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**매개 변수**

|            |                                                                                                                                                                                          |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | SSL 인증서 바인딩을 삭제할 IPv4 또는 IPv6 주소와 포트를 지정합니다. 콜론 문자(:)는 IP 주소와 포트 번호 사이의 구분 기호로 사용됩니다. | 필수 |

---


**예제**

다음은 **delete sslcert** 명령의 세 가지 예입니다.

- delete sslcert ipport=1.1.1.1:443
- delete sslcert ipport=0.0.0.0:443
- delete sslcert ipport=[::]:443

---

## <a name="delete-timeout"></a>delete timeout

글로벌 시간 제한을 삭제하고 서비스를 기본값으로 되돌립니다.

**구문**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**매개 변수**

|                 |                                        |          |
|-----------------|----------------------------------------|----------|
| **timeouttype** | 시간 제한 설정의 유형을 지정합니다. | 필수 |

---


**예제**

다음은 **delete timeout** 명령의 두 가지 예입니다.

-   delete timeout timeouttype=idleconnectiontimeout
-   delete timeout timeouttype=headerwaittimeout

---

## <a name="delete-urlacl"></a>delete urlacl

URL 예약을 삭제합니다.

**구문**

```powershell
delete urlacl [ url= ] URL
```

**매개 변수**

|         |                                                                                       |          |
|---------|---------------------------------------------------------------------------------------|----------|
| **url** | 삭제할 정규화된 URL(Uniform Resource Locator)을 지정합니다. | 필수 |

---


**예제**

다음은 **delete urlacl** 명령의 두 가지 예입니다.

- delete urlacl url=https://+:80/MyUri
- delete urlacl url=<https://www.contoso.com:80/MyUri>

---

## <a name="flush-logbuffer"></a>flush logbuffer

로그 파일의 내부 버퍼를 플러시합니다.

**구문**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>show cachestate

캐시된 URI 리소스 및 관련 속성을 나열합니다. 이 명령은 HTTP 응답 캐시에 캐시된 모든 리소스 및 관련 속성을 나열하거나 단일 리소스 및 관련 속성을 표시합니다.

**구문**

```powershell
show cachestate [ [url= ] URL]
```

**매개 변수**

|         |                                                                                                                                                    |          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **url** | 표시하려는 정규화된 URL을 지정합니다. 지정하지 않으면 모든 URL이 표시됩니다. URL은 등록된 URL의 접두사일 수도 있습니다. | 선택 |

---


**예제**

다음은 **show cachestate** 명령의 두 가지 예입니다.

- show cachestate url=<https://www.contoso.com:80/myresource>
- show cachestate

---

## <a name="show-iplisten"></a>show iplisten

IP 수신 대기 목록에 있는 모든 IP 주소를 표시합니다. IP 수신 대기 목록은 HTTP 서비스가 바인딩되는 주소 목록의 범위를 결정하는 데 사용됩니다. "0.0.0.0"은 IPv4 주소를 의미하고 "::"은 IPv6 주소를 의미합니다.

**구문**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>show servicestate

HTTP 서비스의 스냅샷을 표시합니다.

**구문**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**매개 변수**

|             |                                                                                                                      |          |
|-------------|----------------------------------------------------------------------------------------------------------------------|----------|
|  **보기**   | 서버 세션 또는 요청 큐를 기반으로 HTTP 서비스 상태 스냅샷을 표시할 것인지 여부를 지정합니다. | 선택 |
| **Verbose** |                속성 정보까지 표시하는 자세한 정보를 표시할지 여부를 지정합니다.                | 선택 |

---

**예제**

다음은 **show servicestate** 명령의 두 가지 예입니다.

-   show servicestate view="session"
-   show servicestate view="requestq"

---

## <a name="show-sslcert"></a>show sslcert

IP 주소 및 포트에 대한 SSL(Secure Sockets Layer) 서버 인증서 바인딩과 해당 클라이언트 인증서 정책을 표시합니다.

**구문**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**매개 변수**

|            |                                                                                                                                                                                                                                                |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | SSL 인증서 바인딩을 표시할 IPv4 또는 IPv6 주소와 포트를 지정합니다. 콜론 문자(:)는 IP 주소와 포트 번호 사이의 구분 기호로 사용됩니다. ipport를 지정하지 않으면 모든 바인딩이 표시됩니다. | 필수 |

---


**예제**

다음은 **show sslcert** 명령의 다섯 가지 예입니다.

-   show sslcert ipport=[fe80::1]:443
-   show sslcert ipport=1.1.1.1:443
-   show sslcert ipport=0.0.0.0:443
-   show sslcert ipport=[::]:443
-   show sslcert

---

## <a name="show-timeout"></a>show timeout

HTTP 서비스의 시간 제한 값(초)을 표시합니다.

**구문**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>show urlacl

지정된 예약 URL 또는 모든 예약 URL의 DACL(임의 액세스 제어 목록)을 표시합니다.

**구문**

```powershell
show urlacl [ [url= ] URL]
```

**매개 변수**

|         |                                                                                                |          |
|---------|------------------------------------------------------------------------------------------------|----------|
| **url** | 표시하려는 정규화된 URL을 지정합니다. 지정하지 않으면 모든 URL이 표시됩니다. | 선택 |

---


**예제**

다음은 **show urlacl** 명령의 세 가지 예입니다.

- show urlacl url=https://+:80/MyUri
- show urlacl url=<https://www.contoso.com:80/MyUri>
- show urlacl

---