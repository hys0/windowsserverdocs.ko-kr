---
title: DNS 클라이언트 문제 해결
description: 이 문서에서는 클라이언트 쪽에서 DNS 문제를 해결 하는 방법을 소개 합니다.
manager: dcscontentpm
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: ffc772bafa0027d516194b2741e7680065c0db4b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860066"
---
# <a name="troubleshooting-dns-clients"></a>DNS 클라이언트 문제 해결

이 문서에서는 DNS 클라이언트의 문제를 해결 하는 방법을 설명 합니다.

## <a name="check-ip-configuration"></a>IP 구성 확인

1. 클라이언트 컴퓨터에서 관리자 권한으로 명령 프롬프트 창을 엽니다.

2. 다음 명령을 실행합니다.

   ```cmd
   ipconfig /all
   ```

3. 클라이언트에 연결 되어 사용 되는 네트워크에 대 한 유효한 IP 주소, 서브넷 마스크 및 기본 게이트웨이가 있는지 확인 합니다.

4. 출력에 나열 된 DNS 서버를 확인 하 고 나열 된 IP 주소가 올바른지 확인 합니다.

5. 출력에서 연결별 DNS 접미사를 확인 하 고 올바른지 확인 합니다.

클라이언트에 유효한 TCP/IP 구성이 없는 경우 다음 방법 중 하나를 사용 합니다.

* 동적으로 구성 된 클라이언트의 경우 `ipconfig /renew` 명령을 사용 하 여 클라이언트가 DHCP 서버를 사용 하 여 IP 주소 구성을 갱신 하도록 수동으로 강제 합니다.

* 정적으로 구성 된 클라이언트의 경우 유효한 구성 설정을 사용 하도록 클라이언트 TCP/IP 속성을 수정 하거나 네트워크에 대 한 DNS 구성을 완료 합니다.

## <a name="check-network-connection"></a>네트워크 연결 확인

### <a name="ping-test"></a>Ping 테스트

클라이언트에서 기본 설정 DNS 서버에 IP 주소를 ping 하 여 기본 설정 (또는 대체) DNS 서버에 연결할 수 있는지 확인 합니다.

예를 들어 클라이언트가 10.0.0.1의 기본 설정 DNS 서버를 사용 하는 경우 명령 프롬프트에서 다음 명령을 실행 합니다.

```cmd
ping 10.0.0.1
```

구성 된 DNS 서버가 해당 IP 주소의 직접 ping에 응답 하지 않는 경우이는 문제의 원인이 클라이언트와 DNS 서버 간의 네트워크 연결 가능성을 나타냅니다. 이 경우 기본 TCP/IP 네트워크 문제 해결 단계를 수행 하 여 문제를 해결 합니다. Ping 명령이 작동 하려면 방화벽을 통해 ICMP 트래픽이 허용 되어야 합니다.

### <a name="dns-query-tests"></a>DNS 쿼리 테스트

Dns 클라이언트가 dns 서버 컴퓨터를 ping 할 수 있는 경우 다음 `nslookup` 명령을 사용 하 여 서버가 DNS 클라이언트에 응답할 수 있는지 여부를 테스트 하십시오. Nslookup은 클라이언트의 DNS 캐시를 사용 하지 않으므로 이름 확인은 클라이언트의 구성 된 DNS 서버를 사용 합니다.

#### <a name="test-a-client"></a>클라이언트 테스트

```cmd
nslookup <client>
```
  
예를 들어 클라이언트 컴퓨터의 이름이 **client1**인 경우 다음 명령을 실행 합니다.
  
```cmd
nslookup client1
```
  
성공적인 응답이 반환 되지 않으면 다음 명령을 실행 해 봅니다.
  
```cmd
nslookup <fqdn of client>
```
  
예를 들어 FQDN이 **client1.corp.contoso.com**인 경우 다음 명령을 실행 합니다.

```cmd
nslookup client1.corp.contoso.com.
```

> [!NOTE]
> 이 테스트를 실행할 때 후행 기간을 포함 해야 합니다.

Windows에서 FQDN을 찾았지만 짧은 이름을 찾을 수 없는 경우 NIC의 고급 TCP/IP 설정의 DNS 탭에서 DNS 접미사 구성을 확인 합니다. 자세한 내용은 [DNS 확인 구성](https://docs.microsoft.com/previous-versions/tn-archive/dd163570(v=technet.10)#configuring-dns-resolution)을 참조 하세요.

#### <a name="test-the-dns-server"></a>DNS 서버 테스트

```cmd
nslookup <DNS Server>
```

예를 들어 DNS 서버 이름이 DC1 인 경우 다음 명령을 실행 합니다.

```cmd
nslookup dc1
```
이전 테스트가 성공한 경우이 테스트도 성공 해야 합니다. 이 테스트에 실패 한 경우 DNS 서버에 대 한 연결을 확인 합니다.

#### <a name="test-the-failing-record"></a>실패 레코드 테스트

```cmd
nslookup <failed internal record>
```

예를 들어 실패 레코드가 **app1.corp.contoso.com**인 경우 다음 명령을 실행 합니다.

```cmd
nslookup app1.corp.contoso.com
```

#### <a name="test-a-public-internet-address"></a>공용 인터넷 주소 테스트

```cmd
nslookup <external name>
```

예를 들면 다음과 같습니다. 
```cmd
nslookup bing.com
```

이러한 테스트 중 네 가지 모두 성공 하면 `ipconfig /displaydns`를 실행 하 고 실패 한 이름에 대 한 출력을 확인 합니다. 실패 한 이름에 "이름이 없습니다."가 표시 되 면 DNS 서버에서 부정 응답이 반환 되었고 클라이언트에 캐시 되었습니다. 

이 문제를 해결 하려면 `ipconfig /flushdns`를 실행 하 여 캐시를 지웁니다.

## <a name="next-step"></a>다음 단계

이름 확인이 계속 실패 하는 경우에는 [DNS 서버 문제 해결](troubleshoot-dns-server.md) 섹션으로 이동 합니다.
