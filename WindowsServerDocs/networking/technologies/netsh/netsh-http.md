---
title: 하이퍼텍스트 전송 프로토콜 (HTTP)에 대 한 Netsh 명령
description: Netsh http를 사용 하 여 HTTP.SYS 설정 및 매개 변수를 쿼리하고 구성 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7b9032eb05128532c8bf90a0db2f685b4435e6eb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401873"
---
# <a name="netsh-http-commands"></a>Netsh http 명령


**Netsh http** 를 사용 하 여 http.sys 설정 및 매개 변수를 쿼리하고 구성 합니다.  

>[!TIP]
>Windows Server 2016 또는 Windows 10을 실행 하는 컴퓨터에서 Windows PowerShell을 사용 하는 경우 **netsh** 를 입력 하 고 enter 키를 누릅니다. Netsh 프롬프트에서 **http** 를 입력 하 고 enter 키를 눌러 netsh http 프롬프트를 가져옵니다.
>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh http\>

사용 가능한 netsh http 명령은 다음과 같습니다.

- [iplisten 추가](#add-iplisten)
- [sslcert 추가](#add-sslcert)
- [시간 제한 추가](#add-timeout)
- [urlacl 추가](#add-urlacl)
- [캐시 삭제](#delete-cache)
- [iplisten 삭제](#delete-iplisten)
- [sslcert 삭제](#delete-sslcert)
- [삭제 제한 시간](#delete-timeout)
- [urlacl 삭제](#delete-urlacl)
- [logbuffer 플러시](#flush-logbuffer)
- [cachestate 표시](#show-cachestate)
- [iplisten 표시](#show-iplisten)
- [servicestate 표시](#show-servicestate)
- [sslcert 표시](#show-sslcert)
- [시간 제한 표시](#show-timeout)
- [urlacl 표시](#show-urlacl)

## <a name="add-iplisten"></a>iplisten 추가

포트 번호를 제외 하 고 IP 수신 대기 목록에 새 IP 주소를 추가 합니다.

**구문**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**매개 변수**

|               |                                                                                                                                                                                                                          |          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **\** | IP 수신 대기 목록에 추가할 IPv4 또는 IPv6 주소입니다. IP 수신 대기 목록을 사용 하 여 HTTP 서비스가 바인딩되는 주소 목록의 범위를 결정 합니다. "0.0.0.0"은 모든 IPv4 주소를 의미 하 고 "::"은 IPv6 주소를 의미 합니다. | 필수 |

---

**예제**

**Iplisten 추가** 명령의 네 가지 예는 다음과 같습니다.

-   add iplisten ipaddress = fe80:: 1
-   add iplisten ipaddress = 1.1.1.1
-   iplisten ipaddress = 0.0.0.0 추가
-   add iplisten ipaddress =::

---

## <a name="add-sslcert"></a>sslcert 추가

IP 주소 및 포트에 대 한 새 SSL 서버 인증서 바인딩과 해당 클라이언트 인증서 정책을 추가 합니다.

**구문**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**매개 변수**


|                                              |                                                                                                                                                                                          |          |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|                  **ipport**                  |                       바인딩에 대 한 IP 주소 및 포트를 지정 합니다. 콜론 문자 (:) 는 IP 주소와 포트 번호 사이에 구분 기호로 사용 됩니다.                        | 필수 |
|                 **문으로**                 |                                     인증서의 SHA 해시를 지정 합니다. 이 해시는 20 바이트 길이 이며 16 진수 문자열로 지정 됩니다.                                      | 필수 |
|                  **appid**                   |                                                                  소유 응용 프로그램을 식별 하는 GUID를 지정 합니다.                                                                  | 필수 |
|              **certstorename**               |                                  인증서의 저장소 이름을 지정 합니다. 기본값은 MY입니다. 인증서는 로컬 컴퓨터 컨텍스트에 저장 해야 합니다.                                  | 선택 사항 |
|        **verifyclient>tre**        |                                                      클라이언트 인증서 해지 확인을 설정/해제 하도록 지정 합니다.                                                       | 선택 사항 |
| **verifyrevocationwithcachedclientcertonly** |                                      해지 확인을 위해 캐시 된 클라이언트 인증서를 사용 하도록 설정할지 여부를 지정 합니다.                                       | 선택 사항 |
|                **usagecheck**                |                                                      사용 확인이 사용 되는지 여부를 지정 합니다. 기본값은 사용입니다.                                                       | 선택 사항 |
|         **revocationfreshnesstime**          | 업데이트 된 CRL (인증서 해지 목록)을 확인 하는 시간 간격 (초)을 지정 합니다. 이 값이 0 이면 이전 CRL이 만료 된 경우에만 새 CRL이 업데이트 됩니다. | 선택 사항 |
|           **urlretrievaltimeout**            |                            원격 URL에 대 한 인증서 해지 목록을 검색 한 후의 제한 시간 간격 (밀리초)을 지정 합니다.                            | 선택 사항 |
|             **sslctlidentifier**             |                신뢰할 수 있는 인증서 발급자 목록을 지정 합니다. 이 목록은 컴퓨터에서 신뢰할 수 있는 인증서 발급자의 하위 집합일 수 있습니다.                 | 선택 사항 |
|             **sslctlstorename**              |                                                SslCtlIdentifier가 저장 된 LOCAL_MACHINE 아래의 인증서 저장소 이름을 지정 합니다.                                                | 선택 사항 |
|              **dsmapperusage**               |                                                        DS 매퍼 사용 여부를 지정 합니다. 기본값은 사용 안 함입니다.                                                         | 선택 사항 |
|          **clientcertnegotiation**           |                                              인증서 협상이 사용 되는지 여부를 지정 합니다. 기본값은 사용 안 함입니다.                                               | 선택 사항 |

---

**예제**

**Sslcert 추가** 명령의 예는 다음과 같습니다.

add sslcert ipport = 1.1.1.1:443 certhash = 0102030405060708090A0B0C0D0E0F1011121314 appid = {00112233-4455-6677-8899}

---

## <a name="add-timeout"></a>시간 제한 추가

서비스에 전역 시간 제한을 추가 합니다.

**구문** 

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**매개 변수**

|                 |                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------|
| **timeouttype** |                                    설정에 대 한 시간 제한 유형입니다.                                     |
|    **value**    | 제한 시간 (초)의 값입니다. 값이 16 진수 표기법 인 경우 접두사 0x를 추가 합니다. |

---

**예제**

다음은 **제한 시간 추가** 명령의 두 가지 예입니다.

-   add timeout timeouttype = idleconnectiontimeout value = 120
-   add timeout timeouttype = headerwaittimeout 값 = 0x40

---

## <a name="add-urlacl"></a>urlacl 추가

URL (Uniform Resource Locator) 예약 항목을 추가 합니다. 이 명령은 비관리자 사용자 및 계정에 대 한 URL을 예약 합니다. DACL은 수신 및 대리자 매개 변수를 사용 하는 NT 계정 이름 또는 SDDL 문자열을 사용 하 여 지정할 수 있습니다.

**구문**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**매개 변수**

|              |                                                                                                                                                  |          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|   **url**    |                                          정규화 된 URL (Uniform Resource Locator)을 지정 합니다.                                           | 필수 |
|   **user**   |                                                      사용자 또는 사용자 그룹 이름을 지정 합니다.                                                       | 필수 |
|  **들**  | 다음 값 중 하나를 지정 합니다. 예: 사용자가 Url을 등록할 수 있도록 허용 합니다. 기본값입니다. 아니요: 사용자가 Url을 등록 하지 못하도록 합니다. | 선택 사항 |
| **대리자나** |  다음 값 중 하나를 지정 합니다. 예: 사용자가 Url을 위임할 수 있도록 허용 아니요: 사용자가 Url을 위임 하지 못하도록 합니다. 기본값입니다.  | 선택 사항 |
|   **sddl**   |                                                DACL을 설명 하는 SDDL 문자열을 지정 합니다.                                                 | 선택 사항 |

---

**예제**

다음은 **urlacl 추가** 명령의 네 가지 예입니다.

- add urlacl url =https://+:80/MyUri user = DOMAIN\\user
- add urlacl url =<https://www.contoso.com:80/MyUri> user = DOMAIN\\사용자 수신 = 예
- add urlacl url =<https://www.contoso.com:80/MyUri> user = DOMAIN\\사용자 대리자 = 아니요
- add urlacl url =https://+:80/MyUri sddl = ...

---

## <a name="delete-cache"></a>캐시 삭제

HTTP 서비스 커널 URI 캐시에서 모든 항목 또는 지정 된 항목을 삭제 합니다.

**구문**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**매개 변수**

|               |                                                                                                                              |          |
|---------------|------------------------------------------------------------------------------------------------------------------------------|----------|
|    **url**    |                    삭제할 정규화 된 URL (Uniform Resource Locator)을 지정 합니다.                     | 선택 사항 |
| **재귀** | Url 캐시 아래의 모든 항목을 제거할지 여부를 지정 합니다. **예**: 모든 항목 제거 **아니요**: 모든 항목을 제거 하지 않습니다. | 선택 사항 |

---

**예제**

다음은 **캐시 삭제** 명령의 두 가지 예입니다.

- 캐시 삭제 url =<https://www.contoso.com:80/myresource/> recursive = 예
- 캐시 삭제

---

## <a name="delete-iplisten"></a>iplisten 삭제

Ip 수신 대기 목록에서 IP 주소를 삭제 합니다. IP 수신 대기 목록을 사용 하 여 HTTP 서비스가 바인딩되는 주소 목록의 범위를 결정 합니다.

**구문**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**매개 변수**

|               |                                                                                                                                                                                                                                                                     |          |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **\** | IP 수신 대기 목록에서 삭제할 IPv4 또는 IPv6 주소입니다. IP 수신 대기 목록을 사용 하 여 HTTP 서비스가 바인딩되는 주소 목록의 범위를 결정 합니다. "0.0.0.0"은 모든 IPv4 주소를 의미 하 고 "::"은 IPv6 주소를 의미 합니다. 포트 번호는 포함 되지 않습니다. | 필수 |

---


**예제**

다음은 **delete iplisten** 명령의 네 가지 예입니다.

-   delete iplisten ipaddress = fe80:: 1
-   delete iplisten ipaddress = 1.1.1.1
-   delete iplisten ipaddress = 0.0.0.0
-   delete iplisten ipaddress =::

---

## <a name="delete-sslcert"></a>sslcert 삭제


IP 주소 및 포트에 대 한 SSL 서버 인증서 바인딩과 해당 클라이언트 인증서 정책을 삭제 합니다.

**구문**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**매개 변수**

|            |                                                                                                                                                                                          |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | SSL 인증서 바인딩이 삭제 될 IPv4 또는 IPv6 주소 및 포트를 지정 합니다. 콜론 문자 (:) 는 IP 주소와 포트 번호 사이에 구분 기호로 사용 됩니다. | 필수 |

---


**예제**

다음은 **delete sslcert** 명령에 대 한 세 가지 예입니다.

- delete sslcert ipport = 1.1.1.1:443
- delete sslcert ipport = 0.0.0.0:443
- delete sslcert ipport = [::]: 443

---

## <a name="delete-timeout"></a>삭제 제한 시간

전역 시간 제한을 삭제 하 고 서비스를 기본값으로 되돌립니다.

**구문**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**매개 변수**

|                 |                                        |          |
|-----------------|----------------------------------------|----------|
| **timeouttype** | 제한 시간 설정의 유형을 지정 합니다. | 필수 |

---


**예제**

다음은 **delete timeout** 명령의 두 가지 예입니다.

-   delete timeout timeouttype = idleconnectiontimeout
-   delete timeout timeouttype = headerwaittimeout

---

## <a name="delete-urlacl"></a>urlacl 삭제

URL 예약을 삭제 합니다.

**구문**

```powershell
delete urlacl [ url= ] URL
```

**매개 변수**

|         |                                                                                       |          |
|---------|---------------------------------------------------------------------------------------|----------|
| **url** | 삭제할 정규화 된 URL (Uniform Resource Locator)을 지정 합니다. | 필수 |

---


**예제**

다음은 **urlacl 삭제** 명령의 두 가지 예입니다.

- urlacl url 삭제 =https://+:80/MyUri
- urlacl url 삭제 =<https://www.contoso.com:80/MyUri>

---

## <a name="flush-logbuffer"></a>logbuffer 플러시

로그에 대 한 내부 버퍼를 플러시합니다.

**구문**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>cachestate 표시

캐시 된 URI 리소스 및 관련 속성을 나열 합니다. 이 명령은 HTTP 응답 캐시에 캐시 된 모든 리소스 및 연결 된 속성을 나열 하거나 단일 리소스 및 관련 속성을 표시 합니다.

**구문**

```powershell
show cachestate [ [url= ] URL]
```

**매개 변수**

|         |                                                                                                                                                    |          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **url** | 표시 하려는 정규화 된 URL을 지정 합니다. 지정 하지 않으면 모든 Url을 표시 합니다. URL은 등록 된 Url에 대 한 접두사 일 수도 있습니다. | 선택 사항 |

---


**예제**

다음은 **cachestate** 명령의 두 가지 예입니다.

- cachestate url =<https://www.contoso.com:80/myresource> 표시
- cachestate 표시

---

## <a name="show-iplisten"></a>iplisten 표시

IP 수신 대기 목록에서 모든 IP 주소를 표시 합니다. IP 수신 대기 목록을 사용 하 여 HTTP 서비스가 바인딩되는 주소 목록의 범위를 결정 합니다. "0.0.0.0"은 모든 IPv4 주소를 의미 하 고 "::"은 IPv6 주소를 의미 합니다.

**구문**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>servicestate 표시

HTTP 서비스의 스냅숏을 표시 합니다.

**구문**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**매개 변수**

|             |                                                                                                                      |          |
|-------------|----------------------------------------------------------------------------------------------------------------------|----------|
|  **보기**   | 서버 세션이 나 요청 큐를 기반으로 HTTP 서비스 상태의 스냅숏을 볼 지 여부를 지정 합니다. | 선택 사항 |
| **구문** |                속성 정보를 표시 하는 자세한 정보를 표시할지 여부를 지정 합니다.                | 선택 사항 |

---

**예제**

다음은 **servicestate 명령 표시** 의 두 가지 예입니다.

-   servicestate view = "session" 표시
-   servicestate view = "requestq" 표시

---

## <a name="show-sslcert"></a>sslcert 표시

IP 주소 및 포트에 대 한 SSL(Secure Sockets Layer) (SSL) 서버 인증서 바인딩과 해당 클라이언트 인증서 정책을 표시 합니다.

**구문**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**매개 변수**

|            |                                                                                                                                                                                                                                                |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | SSL 인증서 바인딩이 표시 되는 IPv4 또는 IPv6 주소 및 포트를 지정 합니다. 콜론 문자 (:) 는 IP 주소와 포트 번호 사이에 구분 기호로 사용 됩니다. Ipport를 지정 하지 않으면 모든 바인딩이 표시 됩니다. | 필수 |

---


**예제**

다음은 **sslcert 표시** 명령의 5 가지 예입니다.

-   show sslcert ipport = [fe80:: 1]: 443
-   show sslcert ipport = 1.1.1.1:443
-   show sslcert ipport = 0.0.0.0:443
-   show sslcert ipport = [::]: 443
-   sslcert 표시

---

## <a name="show-timeout"></a>시간 제한 표시

HTTP 서비스의 시간 제한 값 (초)을 표시 합니다.

**구문**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>urlacl 표시

지정 된 예약 된 URL 또는 모든 예약 된 url의 Dacl (임의 액세스 제어 목록)을 표시 합니다.

**구문**

```powershell
show urlacl [ [url= ] URL]
```

**매개 변수**

|         |                                                                                                |          |
|---------|------------------------------------------------------------------------------------------------|----------|
| **url** | 표시 하려는 정규화 된 URL을 지정 합니다. 지정한 경우 모든 Url을 표시 합니다. | 선택 사항 |

---


**예제**

다음은 **urlacl 표시** 명령의 세 가지 예입니다.

- urlacl url 표시 =https://+:80/MyUri
- urlacl url 표시 =<https://www.contoso.com:80/MyUri>
- urlacl 표시

---