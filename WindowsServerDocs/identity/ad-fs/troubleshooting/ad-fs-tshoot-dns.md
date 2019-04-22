---
title: AD FS 문제 해결-DNS 확인
description: 이 문서에서는의 AD FS DNS 측면을 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e0065feac4241b617b8b13c6867d5dc36634bd0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815904"
---
# <a name="ad-fs-troubleshooting---dns"></a>AD FS 문제 해결-DNS 
AD FS가 작동 하거나 응답 하지 확인 하려면 첫 번째 작업 중 하나는 DNS 이름 확인 합니다.  이러한 테스트는 AD FS 서버 또는 WAP 서버 네트워크에서 발견 되는 경우 확인 하기 위해 기본 테스트 합니다.  이러한 테스트는 내부 사용자에 대 한 AD FS 서버 (STS)를 확인 합니다.    외부 사용자를 위해 이러한 테스트는 WAP 서버를 확인 합니다.

이 문서의 나머지 부분에 명령줄 도구를 사용 하 여 일부 빠른 이름 확인 검사를 수행 하는 방법을 알아보겠습니다.

## <a name="ping-test"></a>Ping 테스트
제어 메시지 ICMP (Internet Protocol) 에코 요청 메시지를 전송 하 여 다른 TCP/IP 컴퓨터에 대 한 IP 수준 연결을 확인 합니다. 해당 에코 응답 메시지 수신의 왕복 시간이 함께 표시 됩니다.  자세한 내용은 [Ping](https://technet.microsoft.com/library/ff961503.aspx)합니다.


>[!NOTE]
>일부 조직에서는 해당 서버에서이 포트를 차단 하 발생할 수 있으므로 주의 해야는 **요청 시간이 초과** 응답 합니다.

### <a name="to-use-a-ping-test"></a>PING 테스트를 사용 하려면
1.  명령 프롬프트를 열으십시오
2. PING 입력 <name of adfs server> 를 합니다. 예:  PING sts.contoso.com
3. 서버에서 응답을 표시

![Ping](media/ad-fs-tshoot-dns/dns1.png)

## <a name="nslookup"></a>NSLookup
도메인 이름 시스템 (DNS) 인프라를 진단 하는 데 사용할 수 있는 정보를 표시 합니다.  자세한 내용은 [NSLookup](https://technet.microsoft.com/library/cc725991.aspx)합니다.

### <a name="to-use-a-nslookup"></a>NSLookup을 사용 하려면
1.  명령 프롬프트를 열으십시오
2. PING 입력 <name of adfs server> 를 합니다. 예: nslookup sts.contoso.com
3. 서버에 대 한 dns 정보를 표시 해야 ![NSLookup](media/ad-fs-tshoot-dns/dns2.png)

## <a name="tracert"></a>Tracert
경로 대상으로 보내는 제어 메시지 ICMP (Internet Protocol) 에코 요청 또는 ICMPv6 메시지 대상으로 증분 TTL (Live) 필드 값에 시간을 증가 시켜를 결정 합니다.   자세한 내용은 [Tracert](https://technet.microsoft.com/library/ff961507.aspx)합니다.


### <a name="to-use-tracert"></a>Tracert를 사용 하려면
1.  명령 프롬프트를 열으십시오
2. Tracert 입력 <name of adfs server> 를 합니다. 예: tracert sts.contoso.com
3. 서버에 도달 하는 데 사용 하는 대상 경로 표시 해야 ![Tracert](media/ad-fs-tshoot-dns/dns3.png)

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)