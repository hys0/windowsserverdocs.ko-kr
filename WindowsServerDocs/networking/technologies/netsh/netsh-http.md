---
title: Netsh 명령에 대 한 하이퍼텍스트 전송 프로토콜 (HTTP)
description: Netsh http를 사용 하 여 쿼리를 HTTP.sys 설정 및 매개 변수를 구성 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: daecc6a385d7aa2c02d1bea02eb0a585a9b33185
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881794"
---
# <a name="netsh-http-commands"></a>Netsh http 명령


사용 하 여 **netsh http** 를 쿼리하고 HTTP.sys 설정 및 매개 변수를 구성 합니다.  

>[!TIP]
>Windows PowerShell에서 Windows Server 2016 또는 Windows 10을 실행 하는 컴퓨터를 사용 하는 경우 입력 **netsh** Enter 키를 누릅니다. Netsh 프롬프트 **http** netsh http 프롬프트 Enter 키를 누릅니다.
>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh http\>

사용할 수 있는 netsh http 명령은 다음과 같습니다.

- [iplisten 추가](#add-iplisten)
- [sslcert 추가](#add-sslcert)
- [제한 시간 추가](#add-timeout)
- [urlacl 추가](#add-urlacl)
- [delete cache](#delete-cache)
- [delete iplisten](#delete-iplisten)
- [sslcert 삭제](#delete-sslcert)
- [삭제 시간 초과](#delete-timeout)
- [urlacl 삭제](#delete-urlacl)
- [flush logbuffer](#flush-logbuffer)
- [cachestate 표시](#show-cachestate)
- [iplisten 표시](#show-iplisten)
- [show servicestate](#show-servicestate)
- [sslcert 표시](#show-sslcert)
- [제한 시간을 표시](#show-timeout)
- [urlacl 표시](#show-urlacl)

## <a name="add-iplisten"></a>iplisten 추가

포트 번호를 제외 하 고 IP 수신 목록에 새 IP 주소를 추가 합니다.

**구문**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**매개 변수**
| | | |
|---|---|---|
| **ipaddress** | IP에 추가할 IPv4 또는 IPv6 주소를 수신 대기 목록입니다. IP 수신 대기 목록 HTTP 서비스를 바인딩하는 주소의 목록 범위를 지정 하는 데 사용 됩니다. "0.0.0.0"은 모든 IPv4 주소 및 ":" 모든 IPv6 주소를 의미 합니다. | 필수 |
---

**예**

다음은 네 가지는 **iplisten 추가** 명령입니다.

-   추가 iplisten ipaddress fe80::1 =
-   add iplisten ipaddress=1.1.1.1
-   추가 iplisten ipaddress = 0.0.0.0
-   추가 iplisten ipaddress =::

---

## <a name="add-sslcert"></a>sslcert 추가

새 SSL 서버 인증서를 바인딩 및 해당 IP 주소 및 포트에 대 한 클라이언트 인증서 정책을 추가 합니다.

**구문**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**매개 변수**

| | | |
|---|---|---|
| **ipport**                                   | IP 주소 및 바인딩에 대 한 포트를 지정합니다. 콜론 문자 (:) IP 주소 및 포트 번호 사이의 구분 기호로 사용 됩니다.                                              | 필수 |
| **certhash**                                 | 인증서의 SHA 해시를 지정합니다. 이 해시 20 바이트 및 16 진수 문자열로 지정 됩니다.                                                                          | 필수 |
| **appid**                                    | 소유 응용 프로그램을 식별 하는 GUID를 지정 합니다.                                                                                                                                   | 필수 |
| **certstorename**                            | 인증서 저장소 이름을 지정합니다. 기본값은 MY입니다. 인증서는 로컬 컴퓨터 컨텍스트에서 저장 되어야 합니다.                                                                   | 선택 사항 |
| **verifyclientcertrevocation**               | 켜기/끄기 클라이언트 인증서 해지 확인으로 설정 하면을 지정합니다.                                                                                                            | 선택 사항 |
| **verifyrevocationwithcachedclientcertonly** | 해지 확인을 위해 캐시 된 클라이언트 인증서만 사용 가능 여부를 지정 합니다.                                                                            | 선택 사항 |
| **usagecheck**                               | 사용량 확인 사용 되는지 여부를 지정 합니다. 기본 설정 됩니다.                                                                                                            | 선택 사항 |
| **revocationfreshnesstime**                  | 시간 간격 (초)는 업데이트 된 CRL (인증서 해지 목록)에 대 한 확인을 지정 합니다. 이 값이 0 이면 이전 항목이 만료 된 경우에 새 CRL은 업데이트 됩니다. | 선택 사항 |
| **urlretrievaltimeout**                      | 원격 URL에 대 한 인증서 해지 목록을 검색 하려면 시도 후 시간 제한 간격 (밀리초)을 지정 합니다.                                                       | 선택 사항 |
| **sslctlidentifier**                         | 신뢰할 수 있는 인증서 발급자 목록을 지정 합니다. 이 목록에는 컴퓨터에서 신뢰할 수 있는 인증서 발급자의 하위 집합일 수 있습니다.                                | 선택 사항 |
| **sslctlstorename**                          | LOCAL_MACHINE SslCtlIdentifier 저장 되는 위치에서 인증서 저장소 이름을 지정 합니다.                                                                                               | 선택 사항 |
| **dsmapperusage**                            | DS 매퍼 사용 되는지 여부를 지정 합니다. 기본값은 disabled입니다.                                                                                                                | 선택 사항 |
| **clientcertnegotiation**                    | 인증서의 협상 사용 되는지 여부를 지정 합니다. 기본값은 disabled입니다.                                                                                            | 선택 사항 |
---

**예**

다음은의 예는 **sslcert 추가** 명령입니다.

add sslcert ipport=1.1.1.1:443 certhash=0102030405060708090A0B0C0D0E0F1011121314 appid={00112233-4455-6677-8899- AABBCCDDEEFF}

---

## <a name="add-timeout"></a>제한 시간 추가

서비스에 전역 시간 제한을 추가합니다.

**구문** 

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**매개 변수**
| | |
|---|---|
| **timeouttype** | 설정에 대 한 시간 제한의 형식입니다.                                                                        |
| **value**       | 시간 제한 (초)의 값입니다. 추가 접두사 값을 16 진수 표기법의 경우 x입니다. |
---

**예**

다음은 두 가지 예는 **제한 시간을 추가** 명령입니다.

-   add timeout timeouttype=idleconnectiontimeout value=120
-   시간 제한 timeouttype 추가 headerwaittimeout 값 = 0x40 =

---

## <a name="add-urlacl"></a>urlacl 추가

Locator URL (Uniform Resource) 예약 항목을 추가합니다. 이 명령은 관리자가 아닌 사용자 및 계정에 대 한 URL을 예약합니다. 수신 및 대리자 매개 변수를 사용 하 여 NT 계정 이름을 사용 하 여 또는 SDDL 문자열을 사용 하 여 DACL은 지정할 수 있습니다.

**구문**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**매개 변수**
| | | |
|---|---|---|
| **url**       | 정규화 된 로케이터 URL (Uniform Resource)을 지정합니다.                                                                                    | 필수 |
| **user**      | 사용자 또는 사용자 그룹 이름을 지정합니다.                                                                                                            | 필수 |
| **listen**    | 다음 값 중 하나를 지정 합니다: 예: 사용자 등록 Url을 허용 합니다. 이것은 기본값입니다. 아니요: 등록 Url에서 사용자를 거부 합니다. | 선택 사항 |
| **delegate**  | 다음 값 중 하나를 지정 합니다: 예: Url을 더 위임할 사용자 허용: Url을 위임에서 사용자를 거부 합니다. 이것은 기본값입니다.   | 선택 사항 |
| **sddl**      | DACL을 나타내는 SDDL 문자열을 지정 합니다.                                                                                                | 선택 사항 |
---

**예**

다음은 네 가지는 **urlacl 추가** 명령입니다.

-   add urlacl =https://+:80/MyUri 사용자 = DOMAIN\\사용자
-   add urlacl url=https://www.contoso.com:80/MyUri user=DOMAIN\\user listen=yes
-   add urlacl =https://www.contoso.com:80/MyUri 사용자 = DOMAIN\\사용자 대리자 = 아니요
-   add urlacl =https://+:80/MyUri sddl =...

---

## <a name="delete-cache"></a>캐시를 삭제 합니다.

HTTP 서비스 커널 URI 캐시에서에서 모든 항목을 또는 지정된 된 항목을 삭제합니다.

**구문**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**매개 변수**
| | | |
|---|---|---|
| **url**       | 정규화 된 URL Uniform Resource Locator ()를 삭제 하려는 지정 합니다.                                        | 선택 사항 |
| **재귀** | Url 캐시 항목을 모두 제거 여부를 지정 합니다. **예**: 모든 항목을 제거할 **없습니다**: 모든 항목을 제거 하지 마세요 | 선택 사항 |
---

**예**

다음의 두 가지 예는 **캐시 삭제** 명령입니다.

-   delete cache url=https://www.contoso.com:80/myresource/ recursive=yes
-   캐시를 삭제 합니다.

---

## <a name="delete-iplisten"></a>iplisten 삭제

IP 수신 대기 목록에서 IP 주소를 삭제합니다. IP 수신 대기 목록 HTTP 서비스를 바인딩하는 주소의 목록 범위를 지정 하는 데 사용 됩니다.

**구문**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**매개 변수**
| | | |
|---|---|---|
| **ipaddress** | IP에서 삭제할 IPv4 또는 IPv6 주소를 수신 대기 목록입니다. IP 수신 대기 목록 HTTP 서비스를 바인딩하는 주소의 목록 범위를 지정 하는 데 사용 됩니다. "0.0.0.0"은 모든 IPv4 주소 및 ":" 모든 IPv6 주소를 의미 합니다. 여기에 포트 번호를 포함 되지 않습니다. | 필수 |
---


**예**

다음은 네 가지는 **iplisten 삭제** 명령입니다.

-   iplisten ipaddress 삭제 fe80::1 =
-   delete iplisten ipaddress=1.1.1.1
-   삭제 iplisten ipaddress = 0.0.0.0
-   삭제 iplisten ipaddress =::

---

## <a name="delete-sslcert"></a>sslcert 삭제


IP 주소 및 포트에 대 한 해당 클라이언트 인증서 정책 및 SSL 서버 인증서 바인딩을 삭제합니다.

**구문**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**매개 변수**
| | | |
|---|---|---|
| **ipport** | IPv4 또는 IPv6 주소와는 SSL 인증서 바인딩을 삭제 하는 포트를 지정 합니다. 콜론 문자 (:) IP 주소 및 포트 번호 사이의 구분 기호로 사용 됩니다. | 필수 |
---


**예**

다음은 세 가지는 **sslcert 삭제** 명령입니다.

- sslcert ipport 삭제 1.1.1.1:443 =
- sslcert ipport 삭제 = 0.0.0.0: 443
- sslcert ipport 삭제 [:] =: 443

---

## <a name="delete-timeout"></a>삭제 시간 초과

전역 시간 제한을 삭제 하 고 기본 값으로 되돌리려면 서비스를 사용 하면 키를 누릅니다.

**구문**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**매개 변수**
| | | |
|---|---|---|
| **timeouttype** | 제한 시간 설정의 형식을 지정합니다. | 필수 |
---


**예**

다음의 두 가지 예는 **삭제 시간 초과** 명령입니다.

-   삭제 시간 초과 timeouttype idleconnectiontimeout =
-   삭제 시간 초과 timeouttype headerwaittimeout =

---

## <a name="delete-urlacl"></a>urlacl 삭제

URL 예약을 삭제합니다.

**구문**

```powershell
delete urlacl [ url= ] URL
```

**매개 변수**
| | | |
|---|---|---|
| **url** | 정규화 된 URL Uniform Resource Locator ()를 삭제 하려는 지정 합니다. | 필수 |
---


**예**

다음은 두 가지 예는 **urlacl 삭제** 명령입니다.

-   delete urlacl url=https://+:80/MyUri
-   delete urlacl url=https://www.contoso.com:80/MyUri

---

## <a name="flush-logbuffer"></a>로그 플러시

로그 파일에 대 한 내부 버퍼를 플러시합니다.

**구문**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>cachestate 표시

목록에는 리소스 URI 및 관련된 속성 캐시 합니다. 이 명령은 모든 리소스 및 HTTP 응답 캐시에 캐시 하거나 단일 리소스 및 연결된 된 속성을 표시 하는 관련된 속성을 나열 합니다.

**구문**

```powershell
show cachestate [ [url= ] URL]
```

**매개 변수**
| | | |
|---|---|---|
| **url** | 표시 하려는 정규화 된 URL을 지정 합니다. 지정 하지 않으면 모든 Url을 표시 합니다. URL 등록된 Url 접두사를 수도 있습니다. | 선택 사항 |
---


**예**

다음은 두 가지 예는 **cachestate 표시** 명령:

-   cachestate url 표시 =https://www.contoso.com:80/myresource
-   cachestate 표시

---

## <a name="show-iplisten"></a>iplisten 표시

IP 수신 대기 목록에 모든 IP 주소를 표시합니다. IP 수신 대기 목록 HTTP 서비스를 바인딩하는 주소의 목록 범위를 지정 하는 데 사용 됩니다. "0.0.0.0"은 모든 IPv4 주소 및 ":" 모든 IPv6 주소를 의미 합니다.

**구문**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>servicestate 표시

HTTP 서비스의 스냅숏을 표시합니다.

**구문**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**매개 변수**
| | | |
|---|---|---|
| **보기**    | 서버 세션 또는 요청 큐를 기반으로 하는 HTTP 서비스 상태의 스냅숏을 볼 것인지 여부를 지정 합니다. | 선택 사항 |
| **Verbose** | 또한 속성 정보를 보여 주는 자세한 정보를 표시할지 여부를 지정 합니다.                               | 선택 사항 |
---

**예**

다음은 두 가지 예는 **servicestate 표시** 명령입니다.

-   표시 servicestate view = "세션"
-   표시 servicestate view = "requestq"

---

## <a name="show-sslcert"></a>sslcert 표시

서버 인증서 바인딩을 Secure Sockets Layer (SSL) 및 IP 주소 및 포트에 대 한 해당 클라이언트 인증서 정책을 표시합니다.

**구문**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**매개 변수**
| | | |
|---|---|---|
| **ipport** | IPv4 또는 IPv6 주소 및 포트를 SSL 인증서 바인딩 표시를 지정 합니다. 콜론 문자 (:) IP 주소 및 포트 번호 사이의 구분 기호로 사용 됩니다. Ipport를 지정 하지 않으면 모든 바인딩이 표시 됩니다. | 필수 |
---


**예**

다음은 5 가지는 **sslcert 표시** 명령입니다.

-   show sslcert ipport=[fe80::1]:443
-   sslcert 유사 표시 1.1.1.1:443 =
-   sslcert ipport 표시 = 0.0.0.0: 443
-   sslcert ipport 표시 [:] =: 443
-   sslcert 표시

---

## <a name="show-timeout"></a>제한 시간을 표시

HTTP 서비스의 시간 제한 값을 초 단위로 표시합니다.

**구문**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>urlacl 표시

표시 임의 액세스 제어는 지정된 된 예약 된 URL에 모든 예약 된 Url (Dacl)을 나열합니다.

**구문**

```powershell
show urlacl [ [url= ] URL]
```

**매개 변수**
| | | |
|---|---|---|
| **url** | 표시 하려는 정규화 된 URL을 지정 합니다. 지정 되지 경우 모든 Url을 표시 합니다. | 선택 사항 |
---


**예**

다음은 세 가지는 **urlacl 표시** 명령입니다.

-   show urlacl url=https://+:80/MyUri
-   show urlacl url=https://www.contoso.com:80/MyUri
-   urlacl 표시

---