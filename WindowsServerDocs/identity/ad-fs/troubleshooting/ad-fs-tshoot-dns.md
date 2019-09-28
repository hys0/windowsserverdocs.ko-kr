---
title: AD FS 문제 해결-DNS 확인
description: 이 문서에서는 AD FS의 DNS 측면 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7ffda6916bd91f1195ac0c289959becafff1d2c5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407207"
---
# <a name="ad-fs-troubleshooting---dns"></a>AD FS 문제 해결-DNS 
확인 해야 하는 첫 번째 항목 중 하나 (AD FS 작동 하지 않거나 응답 하지 않는 경우)는 DNS 이름 확인입니다.  이러한 테스트는 AD FS 서버 또는 WAP 서버를 네트워크에서 찾을 수 있는지 여부를 확인 하는 기본 테스트입니다.  내부 사용자의 경우 이러한 테스트는 AD FS 서버 (STS)로 확인 되어야 합니다.    외부 사용자의 경우 이러한 테스트는 WAP 서버를 확인 해야 합니다.

이 문서의 나머지 부분에서는 명령줄 도구를 사용 하 여 몇 가지 빠른 이름 확인 검사를 수행 하는 방법을 보여 줍니다.

## <a name="ping-test"></a>Ping 테스트
ICMP (Internet Control Message Protocol) 에코 요청 메시지를 전송 하 여 다른 TCP/IP 컴퓨터에 대 한 IP 수준 연결을 확인 합니다. 해당 에코 응답 메시지의 수신이 라운드트립 시간과 함께 표시 됩니다.  자세한 내용은 [Ping](https://technet.microsoft.com/library/ff961503.aspx)을 참조 하세요.


>[!NOTE]
>일부 조직에서는 서버에서이 포트를 차단 하 고 **요청 시간 초과** 응답을 받을 수 있습니다.

### <a name="to-use-a-ping-test"></a>PING 테스트를 사용 하려면
1.  명령 프롬프트 열기
2. PING <name of adfs server> a를 입력 합니다. 예:  PING sts.contoso.com
3. 서버에서 회신이 표시 되어야 합니다.

![Ping](media/ad-fs-tshoot-dns/dns1.png)

## <a name="nslookup"></a>NSLookup
도메인 이름 시스템 (DNS) 인프라를 진단 하는 데 사용할 수 있는 정보를 표시 합니다.  자세한 내용은 [NSLookup](https://technet.microsoft.com/library/cc725991.aspx)을 참조 하십시오.

### <a name="to-use-a-nslookup"></a>NSLookup을 사용 하려면
1.  명령 프롬프트 열기
2. PING <name of adfs server> a를 입력 합니다. 예: nslookup sts.contoso.com
3. 서버 ![NSLookup @ no__t-1에 대 한 dns 정보가 표시 되어야 합니다.

## <a name="tracert"></a>Tracert
경로 대상으로 보내는 제어 메시지 ICMP (Internet Protocol) 에코 요청 또는 ICMPv6 메시지 대상으로 증분 TTL (Live) 필드 값에 시간을 증가 시켜를 결정 합니다.   자세한 내용은 [Tracert](https://technet.microsoft.com/library/ff961507.aspx)를 참조 하세요.


### <a name="to-use-tracert"></a>Tracert를 사용 하려면
1.  명령 프롬프트 열기
2. Tracert <name of adfs server>을 입력 합니다. 예: tracert sts.contoso.com
3. 서버에 연결 하는 데 사용 되는 대상 경로가 표시 됩니다 ![Tracert @ no__t-1

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)