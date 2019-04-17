---
title: Windows Server에서 DNS 서버의 새로운 기능
description: 이 항목에서는 Windows Server 2016 및 이후 버전에서 DNS 서버의 새로운 기능을 소개
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: c9cecb94-3cd5-4da7-9a3e-084148b8226b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3ddb8920c045f231dcf5286283d9895ef6ffff47
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-dns-server-in-windows-server"></a>Windows Server에서 DNS 서버의 새로운 기능

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 시스템 DNS (도메인 이름) 서버 기능을 새로운 또는 변경 Windows Server 2016에서 설명 합니다.  
  
Windows Server 2016에서 DNS 서버 다음과 같은 지역에서 향상 된 지원을 제공합니다.  
  
|기능|새로운 기능이 나 향상 된|설명|  
|-----------------|-------------------|---------------|  
|DNS 정책|새로운|DNS 서버가 DNS 쿼리에 응답 하는 방법을 지정 DNS 정책 구성할 수 있습니다. DNS 응답 클라이언트 IP 주소 (위치)에 따라 수 요일과 여러 매개 변수 시간 합니다. DNS 정책을 위치 인식 DNS, 교통 관리, 부하 분산, split-brain DNS 및 기타 시나리오 사용 합니다.|  
|응답 속도 (RRL)를 제한|새로운|DNS 서버에 응답 속도 제한 사용할 수 있습니다. 이 작업을 수행 하 여 가능성을 서비스 거부 공격이 DNS 클라이언트를 시작 하려면 DNS 서버를 사용 하 여 악성 시스템을 방지할 수 있습니다.|  
|DNS 기반 인증 명명 엔터티 (있는지)|새로운|(Transport Layer Security 인증) TLSA 레코드 도메인 이름에 대 한에서 인증서 있기 기대 어떤 캘리포니아 국립 DNS 클라이언트에 정보를 제공 하기 위해 사용할 수 있습니다. 이렇게 하면 남자 중간 공격 사람이 수 손상 된 웹 사이트 자체 가리키도록 DNS 캐시 하 고 다른 캘리포니아에서 발급 한 인증서를 제공 합니다.|  
|알 수 없는 기록 지원|새로운|알 수 없는 녹화 기능을 사용 하 여 Windows DNS 서버에서 명시적으로 지원 되지 않는 기록에 추가할 수 있습니다.|  
|IPv6 루트 힌트|새로운|기본 IPV6 루트 힌트 지원 IPV6 루트 서버를 사용 하 여 인터넷 이름을 확인 하는 데 사용할 수 있습니다.|  
|Windows PowerShell 지원|개선|새로운 Windows PowerShell cmdlet DNS 서버를 사용할 수 있습니다.|  
  
## <a name="dns-policies"></a>DNS 정책

지리적 위치를 기반으로 교통 관리, 날짜, 시간에 따라 지능형 DNS 응답에 대 한 DNS 정책을 사용 하 여 DNS 쿼리에 등에서 필터를 적용 split\ 두뇌 배포를 위해 구성 되어 DNS 서버 관리 수 있습니다. 다음과 같은 항목에는 이러한 기능에 대 한 자세한 내용을 제공합니다.

-   **응용 프로그램 부하 분산 합니다.** 다른 위치에서 응용 프로그램을 여러 개를 배포한 때 DNS 정책 동적으로 응용 프로그램에 대 한 교통량 로드 할당 다른 응용 프로그램이 인스턴스 간에 교통 부하 분산를 사용할 수 있습니다.

-   **Geo\ 위치 기반 교통 관리 합니다.** 클라이언트 가까운 리소스의 IP 주소를 제공 하는 클라이언트와, 연결을 시도 하는 클라이언트를 리소스 지리적 위치에 따라 DNS 클라이언트 쿼리가 응답할 기본 및 보조 DNS 서버를 허용 하도록 DNS 정책을 사용할 수 있습니다. 

-   **DNS 두뇌를 분할 됩니다.** Split\ 두뇌 DNS DNS 레코드 동일한 DNS 서버에서 다양 한 영역 범위도 분할 및 DNS 클라이언트 클라이언트는 내장형 또는 외장형 클라이언트 있는지 여부에 따라 응답을 받습니다. 독립 실행형 DNS 서버에 통합 된 Active Directory 영역에 대 한 또는 영역에 대 한 split\ 두뇌 DNS 구성할 수 있습니다.

-   **필터링 합니다.** DNS 정책을를 제공 하는 조건에 따라 쿼리 필터 만드는 구성할 수 있습니다. DNS 정책에서 쿼리 필터를 사용 하 여 DNS 쿼리 및 DNS 쿼리에 보내는 DNS 클라이언트를 기반으로 사용자가 지정한 방식 응답 DNS 서버를 구성할 수 있습니다. 
-   **설명 합니다.** 연결 하려는 컴퓨터에 전송 하는 대신 non\ 존재 IP 주소를 악성 DNS 클라이언트 리디렉션합니다 DNS 정책을 사용할 수 있습니다.

-   **하루 중 시간 기반 전환 합니다.** DNS 정책을 사용 하 여 DNS 정책을 사용 하 여 하루 중 시간에 따라 다른 지리적 분산된 인스턴스 응용 프로그램의 응용 프로그램 교통 분산 수 있습니다. 
  
또한 정책을 사용 하 여 DNS Active Directory DNS 통합 된 영역 합니다.

자세한 내용은 참조는 [DNS 정책 시나리오 가이드](deploy/DNS-Policies-Overview.md)합니다.

## <a name="response-rate-limiting"></a>응답 속도 제한

서버 같은 클라이언트 표적화 몇 가지 요청을 받으면 DNS 클라이언트에 대 한 요청에 응답 하는 방법을 제어 하는 RRL 설정을 구성할 수 있습니다. 이 작업을 수행 하 여 DNS 서버를 사용 하 여 (Dos) 서비스 거부 공격이 보내는 사람 방지할 수 있습니다. 예를 들어 net 봇 요청 자가로 세 번째 컴퓨터의 IP 주소를 사용 하 여 DNS 서버에 요청을 보낼 수 있습니다. RRL를 않고도 DNS 서버 초과 세 번째 컴퓨터에서 모든 요청에 응답할 수 있습니다. RRL를 사용 하면 다음 설정을 구성할 수 있습니다.  
  
-   **초당 응답**합니다. 이것은 최대 시간 같은 응답을 클라이언트 1 초 이내 부여 됩니다.  
  
-   **초당 오류**합니다. 이것은 최대 시간 오류 응답 같은 클라이언트로 1 초 이내에 전송 됩니다.  
  
-   **창**합니다. 이 초 있는 클라이언트에 대 한 응답 중지 것입니다 너무 많이 요청을 만들 수 있습니다.  
  
-   **누수 속도**합니다. 이 얼마나 자주 DNS 서버가 응답 일시 중단 된 시간 동안 쿼리에 응답 합니다. 예를 들어 서버 10 초 동안 클라이언트에 대 한 응답을 중단 하 고 누수 속도가 5, 서버 여전히 쿼리 모든 5 전송에 대 한 쿼리에 응답 합니다. 합법적인 클라이언트가 DNS 서버가 응답 속도 제한 서브넷 나 FQDN에 적용 되 고 있는 경우에 응답 가져올 수 있습니다.  
  
-   **TC 속도**합니다. 이 클라이언트 응답 일시 중단 된 경우 TCP와 연결을 시도 하는 클라이언트를 사용 됩니다. 예를 들어 TC 속도가 3 하 고 서버를 일시 중지 클라이언트에 대 한 응답, 서버 받은 모든 3 쿼리 TCP 연결에 대 한 요청을 발표할 예정입니다. 클라이언트 응답 누수가 발생 하기 전에 tcp 연결 하는 옵션을 제공 하는 누수 속도 보다 낮은 TC 속도 값이 있는지 확인 합니다.  
  
-   **최대 응답**합니다. 최대 응답 응답 일시 중단 되는 동안 서버 클라이언트를 발표할 예정입니다.  
  
-   **화이트 목록 도메인**합니다. 도메인 RRL 설정에서 제외 될의 목록입니다.  
  
-   **화이트 목록 서브넷**합니다. 이것은 목록이 서브넷 RRL 설정에서 제외 될 수 있습니다.  
  
-   **화이트 목록 서버 인터페이스**합니다. DNS 서버 인터페이스 RRL 설정에서 제외 될의 목록입니다.  
  
## <a name="dane-support"></a>있는지 지원

있는지 지원을 사용할 수 있는 \ (RFC 6394 및 6698\) DNS 서버에은 도메인 이름에 대 한에서 발급 되어야 하는 인증서 됩니까 캘리포니아 호스트 무엇 DNS 클라이언트를 지정할 수 있습니다. 다른 사용자가 손상 DNS 캐시 있으며 DNS 이름을 자체 IP 주소를 가리킨 수 남자 중간 공격 형태의 수 없습니다.  
  
예를 들어 가정 호스트 SSL CA1 라는 유명 기관의 인증서를 사용 하 여 www.contoso.com에서 사용 하 여 안전한 웹 사이트를 합니다. 다른 사람이 다른, 하지 하므로-잘 알려지지, 인증서 기관 라는 c a 2에서에서 www.contoso.com에 대 한 인증서를 얻는 수 있습니다. 그런 다음 가짜 www.contoso.com 웹 사이트 호스트 엔터티 DNS 캐시 www.contoto.com 가짜 해당 사이트 가리키도록 클라이언트 또는 서버를 손상 시킬 수 있습니다. 최종 사용자 제시 인증서를 c a 2를에서 및 수 간단 하 게 승인 하 고 가짜 사이트에 연결 합니다. 있는지와 클라이언트 것 contoso.com TLSA 기록에 대 한 요청에 대 한 DNS 서버에 요청을 확인 하 고 www.contoso.com에 대 한 인증서가 CA1 하 여 문제에 알아봅니다. 인증서에서 다른 캘리포니아 표시, 연결 중단 됩니다.  
  
## <a name="unknown-record-support"></a>알 수 없는 기록 지원

"알 수 없는 기록" RDATA 서식을 DNS 서버를 알 수 없는 RR입니다. 알 수 없는 기록 (RFC 3597) 형식의 새로 추가 지원 바이너리 실시간 형태로 Windows DNS 서버 영역으로 지원 되지 않는 레코드 종류를 추가할 수 있습니다 의미 합니다. Windows 확인자 캐시 이미 알 수 없는 기록 종류를 처리 하는 기능입니다. Windows DNS 서버 알 수 없는 레코드에 대 한 특정 녹화 프로세스를 수행 하지는 하지만 보냅니다 응답에 다시 쿼리 것에 대해 수신 하는 경우 합니다.  
  
## <a name="ipv6-root-hints"></a>IPv6 루트 힌트

IPV6 루트 힌트 IANA에 의해 게시에 추가한 windows DNS 서버 합니다. 이제 internet 이름 쿼리 이름 해상도 수행 하기 위한 IPv6 루트 서버를 사용할 수 있습니다.

## <a name="windows-powershell-support"></a>Windows PowerShell 지원

Windows Server 2016에는 다음과 같은 새로운 Windows PowerShell cmdlet 및 매개 도입 합니다.
  
-   **추가 DnsServerRecursionScope**합니다. 이 cmdlet DNS 서버에서 새 재귀 범위를 만듭니다. DNS 쿼리에에서 사용할 수 있도록 전달자 목록이 지정 하려면 재귀 범위 DNS 정책에서 사용 됩니다.  
  
-   **제거 DnsServerRecursionScope**합니다. 이 cmdlet 기존 재귀 범위를 제거합니다.  
  
-   **설정 DnsServerRecursionScope**합니다. 이 cmdlet 기존 재귀 범위의 설정을 변경합니다.  
  
-   **Get DnsServerRecursionScope**합니다. 이 cmdlet 기존 재귀 범위에 대 한 정보를 검색합니다.  
  
-   **추가 DnsServerClientSubnet**합니다. 이 cmdlet 새 DNS 클라이언트 서브넷을 만듭니다. DNS 클라이언트의 위치를 식별 하 정책 DNS 서브넷 사용 됩니다.  
  
-   **제거 DnsServerClientSubnet**합니다. 이 cmdlet 기존 DNS 클라이언트 서브넷 제거합니다.  
  
-   **설정 DnsServerClientSubnet**합니다. 이 cmdlet 기존 DNS 클라이언트 서브넷 설정을 변경합니다.  
  
-   **Get DnsServerClientSubnet**합니다. 이 cmdlet 기존 DNS 클라이언트 서브넷에 대 한 정보를 검색합니다.  
  
-   **추가 DnsServerQueryResolutionPolicy**합니다. 이 cmdlet 새 DNS 쿼리에 해결 정책을 만듭니다. DNS 쿼리에 해상도 정책 지정 하는 데는 방법을, 쿼리에 대 한 답변을에 따라 다른 기준을 또는 합니다.  
  
-   **제거 DnsServerQueryResolutionPolicy**합니다. 이 cmdlet 기존 DNS 정책을 제거합니다.  
  
-   **설정 DnsServerQueryResolutionPolicy**합니다. 이 cmdlet 기존 DNS 정책 설정을 변경합니다.  
  
-   **Get DnsServerQueryResolutionPolicy**합니다. 이 cmdlet 기존 DNS 정책에 대 한 정보를 검색합니다.  
  
-   **사용 DnsServerPolicy**합니다. 이 cmdlet 기존 DNS 정책 수 있습니다.  
  
-   **사용 안 함 DnsServerPolicy**합니다. 이 cmdlet 기존 DNS 정책 해제합니다.  
  
-   **추가 DnsServerZoneTransferPolicy**합니다. 이 cmdlet 새 DNS 서버 영역 전송 정책을 만듭니다. DNS 영역 전송 정책 거부 또는 다른 조건에 따라 영역 전송 무시 여부를 지정 합니다.  
  
-   **제거 DnsServerZoneTransferPolicy**합니다. 이 cmdlet 기존 DNS 서버 영역 전송 정책 제거합니다.  
  
-   **설정 DnsServerZoneTransferPolicy**합니다. 이 cmdlet 기존 DNS 서버 영역 전송 정책의 설정을 변경합니다.  
  
-   **Get DnsServerResponseRateLimiting**합니다. 이 cmdlet RRL 설정을 검색합니다.  
  
-   **설정 DnsServerResponseRateLimiting**합니다. 이 cmdlet RRL settigns를 변경합니다.  
  
-   **추가 DnsServerResponseRateLimitingExceptionlist**합니다. 이 cmdlet DNS 서버에서 RRL 예외 목록을 만듭니다.  
  
-   **Get DnsServerResponseRateLimitingExceptionlist**합니다. 이 cmdlet RRL excception 목록을 검색합니다.  
  
-   **제거 DnsServerResponseRateLimitingExceptionlist**합니다. 이 cmdlet 기존 RRL 예외 목록을 제거합니다.  
  
-   **설정 DnsServerResponseRateLimitingExceptionlist**합니다. 이 cmdlet RRL 예외 목록을 변경 됩니다.  
  
-   **추가 DnsServerResourceRecord**합니다. 이 cmdlet 알 수 없는 기록 형식을 지원 하도록 업데이트 되었습니다.  
  
-   **Get DnsServerResourceRecord**합니다. 이 cmdlet 알 수 없는 기록 형식을 지원 하도록 업데이트 되었습니다.  
  
-   **제거 DnsServerResourceRecord**합니다. 이 cmdlet 알 수 없는 기록 형식을 지원 하도록 업데이트 되었습니다.  
  
-   **설정 DnsServerResourceRecord**합니다. 이 cmdlet 알 수 없는 기록 형식을 지원 하도록 업데이트 되었습니다.

자세한 내용은 다음과 같은 Windows Server 2016 Windows PowerShell 명령 참조 항목을 참조 합니다.

- [Dns 서버 모듈](https://technet.microsoft.com/itpro/powershell/windows/dns-server/index)
- [DnsClient 모듈](https://technet.microsoft.com/itpro/powershell/windows/dns-client/index)

## <a name="see-also"></a>참조 하십시오  
  
-   [DNS 클라이언트의 새로운 기능](What-s-New-in-DNS-Client.md)  
  

  

