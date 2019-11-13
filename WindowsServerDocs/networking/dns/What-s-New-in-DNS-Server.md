---
title: Windows Server에서 제공 되는 DNS 서버의 새로운 기능
description: 이 항목에서는 Windows Server 2016 이상 버전에서 DNS 서버의 새 기능에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: c9cecb94-3cd5-4da7-9a3e-084148b8226b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: de502d7be023d12e3350063e467a60356b2472c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406234"
---
# <a name="whats-new-in-dns-server-in-windows-server"></a>Windows Server에서 제공 되는 DNS 서버의 새로운 기능

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016의 새롭거나 변경 되는 도메인 이름 시스템 (DNS) 서버 기능을 설명 합니다.  
  
Windows Server 2016에서 DNS 서버는 다음과 같은 영역에서 향상 된 지원을 제공합니다.  
  
|기능|새로운 기능 또는 향상된 기능|설명|  
|-----------------|-------------------|---------------|  
|DNS 정책|새로 만들기|DNS는 DNS 서버 DNS 쿼리에 응답 하는 방법을 지정 하는 정책을 구성할 수 있습니다. DNS 응답을 기반으로 클라이언트 IP 주소 (위치), 시간, 일 및 다른 여러 매개 변수입니다. DNS 정책을 위치 인식 DNS, 트래픽 관리, 부하 분산, 스플릿 브레인 DNS 및 기타 시나리오를 사용 합니다.|  
|응답 속도 (RRL)를 제한 합니다.|새로 만들기|DNS 서버에 대 한 응답 속도 제한 하는 것이 가능 합니다. 이 작업을 수행 하 여 DNS 서버를 사용 하 여 DNS 클라이언트에 서비스 공격 거부를 시작 하는 악의적인 시스템의 가능성을 방지할 수 있습니다.|  
|명명 된 엔터티 (있는지)의 DNS 기반 인증|새로 만들기|해당 상태에서 도메인 이름에 대 한 인증서를 기대 해야 어떤 CA DNS 클라이언트에 정보를 제공 하도록 TLSA (전송 계층 보안 인증) 레코드를 사용할 수 있습니다. 이렇게 하면 누군가가 자체 웹 사이트를 가리키도록 DNS 캐시를 손상 시키고 다른 CA에서 발급 한 인증서를 제공할 수 있는 메시지 가로채기 (man-in-the-middle) 공격을 방지할 수 있습니다.|  
|알 수 없는 레코드 지원|새로 만들기|알 수 없는 레코드 기능을 사용 하 여 Windows DNS 서버에 의해 명시적으로 지원 되지 않는 레코드를 추가할 수 있습니다.|  
|IPv6 루트 힌트|새로 만들기|루트 힌트 지원 IPV6 루트 서버를 사용 하 여 인터넷 이름 확인을 수행 하려면 기본 IPV6를 사용할 수 있습니다.|  
|Windows PowerShell 지원|향상된 기능|새 Windows PowerShell cmdlet은 DNS 서버에 사용할 수 있습니다.|  
  
## <a name="dns-policies"></a>DNS 정책

지리적 위치 기반 트래픽 관리에 DNS 정책을 사용 하 고, 시간을 기준으로 지능형 DNS 응답을 사용 하 여 분할\-두뇌 배포를 위해 구성 된 단일 DNS 서버를 관리 하 고, DNS 쿼리에 필터를 적용 하는 등의 기능을 수행할 수 있습니다. 다음 항목은 이러한 기능에 대 한 자세한 정보를 제공 합니다.

-   **응용 프로그램 부하 분산.** 응용 프로그램의 여러 인스턴스를 서로 다른 위치에 배포한 경우에는 DNS 정책을 사용 하 여 응용 프로그램에 대 한 트래픽 부하를 동적으로 할당 하는 여러 응용 프로그램 인스턴스 간의 트래픽 부하를 분산할 수 있습니다.

-   **지리적\-위치 기반 트래픽 관리.** DNS 정책을 사용 하 여 클라이언트와 클라이언트가 연결 하려고 하는 리소스의 지리적 위치에 따라 DNS 클라이언트 쿼리에 응답 하도록 기본 및 보조 DNS 서버를 허용 하 고, 클라이언트에 가장 가까운 IP 주소를 제공 합니다. 리소스나. 

-   **두뇌 DNS를 분할 합니다.** 분할\-두뇌 DNS를 사용 하는 경우 DNS 레코드는 동일한 DNS 서버에서 다른 영역 범위로 분할 되 고, DNS 클라이언트는 내부 또는 외부 클라이언트 인지 여부에 따라 응답을 받습니다. 분할\-두뇌 DNS를 Active Directory 통합 영역에 대해 구성 하거나 독립 실행형 DNS 서버의 영역에 대해 구성할 수 있습니다.

-   **필터링.** 사용자가 제공 하는 조건을 기반으로 하는 쿼리 필터를 만들도록 DNS 정책을 구성할 수 있습니다. DNS 정책에서 쿼리 필터를 사용 하는 DNS 쿼리 및 DNS 쿼리를 보내는 DNS 클라이언트에 따라 사용자 지정 방식으로 응답 하도록 DNS 서버를 구성할 수 있습니다. 
-   **법률.** DNS 정책을 사용 하 여 악성 DNS 클라이언트를 연결 하려는 컴퓨터로 전달 하지 않고 존재\-하지 않는 IP 주소로 리디렉션할 수 있습니다.

-   **하루 기준 리디렉션 시간입니다.** DNS 정책을 사용 하 여 하루 중 시간을 기준으로 하는 DNS 정책을 사용 하 여 응용 프로그램의 여러 지리적으로 분산 된 인스턴스에 응용 프로그램 트래픽을 분산할 수 있습니다. 
  
Active Directory 통합 DNS에 대 한 DNS 정책을 사용할 수도 있습니다 영역입니다.

자세한 내용은 [DNS 정책 시나리오 가이드](deploy/DNS-Policies-Overview.md)를 참조 하세요.

## <a name="response-rate-limiting"></a>응답 속도 제한

서버에 동일한 클라이언트를 대상으로 하는 몇 개의 요청을 받으면 DNS 클라이언트에 대 한 요청에 응답 하는 방법을 제어 하려면 RRL 설정을 구성할 수 있습니다. 이 작업을 수행 하 여 DNS 서버를 사용 하 여 서비스 거부 (Dos) 공격을 보내는 사람이 방지할 수 있습니다. 예를 들어, net bot 요청자와 세 번째 컴퓨터의 IP 주소를 사용 하 여 DNS 서버에 요청을 보낼 수 있습니다. RRL, 없이 DNS 서버가 세 번째 컴퓨터의 폭주 모든 요청에 응답 합니다. RRL를 사용 하는 경우 다음 설정을 구성할 수 있습니다.  
  
-   **초당 응답**합니다. 이것이 같은 응답 1 초 이내에 클라이언트에 지정 될 최대 횟수입니다.  
  
-   **초당 오류**합니다. 이 1 초 이내에 동일한 클라이언트에 보낼 오류 응답은 최대 횟수입니다.  
  
-   **창**합니다. 클라이언트에 대 한 응답은 일시 중단 됩니다 너무 많은 요청이 수행 되는 경우 시간 (초) 수입니다.  
  
-   **누수 속도**합니다. 응답은 일시 중단 하는 동안 DNS 서버가 쿼리에 응답 하는 빈도입니다. 예를 들어, 서버를 10 초 동안 클라이언트에 대 한 응답을 일시 중단 하는 경우 누수 속도 5는 서버가 보낸 모든 5 개의 쿼리에 대 한 하나의 쿼리에 계속 응답 합니다. DNS 서버가 응답 속도 서브넷 또는 FQDN에 제한 적용 하는 경우에 응답을 받지 합법적인 클라이언트가 있습니다.  
  
-   **TC 속도**합니다. 이 클라이언트에 대 한 응답은 일시 중단 하는 경우 tcp 연결을 시도 하도록 클라이언트에 게 사용 됩니다. 예를 들어, TC 속도가 3, 서버 지정된 된 클라이언트에 대 한 응답을 일시 중단 하는 경우 서버 수신한 모든 3 쿼리 수에 대 한 TCP 연결에 대 한 요청을 실행 합니다. TC 속도 대 한 값 클라이언트 응답 누수가 발생 하기 전에 TCP를 통한 연결 옵션을 제공 하는 누수 속도 보다 낮은 인지 확인 합니다.  
  
-   **최대 응답**합니다. 응답은 일시 중단 하는 동안 서버에서 클라이언트에 발급할는 응답의 최대 수입니다.  
  
-   **허용 목록을 도메인**합니다. RRL 설정에서 제외할 도메인의 목록입니다.  
  
-   **허용 목록을 서브넷**합니다. RRL 설정에서 제외할 서브넷의 목록입니다.  
  
-   **허용 목록을 서버 인터페이스**합니다. RRL 설정에서 제외할 DNS 서버 인터페이스의 목록입니다.  
  
## <a name="dane-support"></a>있는지 지원

있는지 support \(RFC 6394 및 6698\)를 사용 하 여 dns 서버에 호스트 된 도메인 이름에 대해 인증서를 발급할 CA를 DNS 클라이언트에 지정할 수 있습니다. 이 방지 중간자 개입 공격을 다른 사용자가 DNS 캐시를 손상 시키고 DNS 이름을 자신의 IP 주소를 가리킬 수 있습니다.  
  
예를 들어 www.contoso.com에서 c a 1 이라는 잘 알려진 기관에서 인증서를 사용 하 여 SSL을 사용 하는 보안 웹 사이트 호스트 한다고 가정 합니다. 사용자는 다른, not 하므로-잘 알려지지, 인증서 기관을 라는 c a 2에서에서 www.contoso.com에 대 한 인증서를 가져올 수 중일 수 있습니다. 그런 다음 가짜 www.contoso.com 웹 사이트를 호스트 하는 엔터티 클라이언트 또는 서버의 www.contoto.com 가짜 사이트를 가리키도록 DNS 캐시를 손상 시킬 수 있습니다. 최종 사용자 c, a 2에서 인증서를 제공 됩니다 수 단순히 승인 및 가짜 사이트에 연결 합니다. 있는지와 클라이언트는 contoso.com TLSA 레코드에 대 한 요청에 대 한 DNS 서버에 요청을 수행 하 고 www.contoso.com에 대 한 인증서가 c a 1 별 문제에 알아봅니다. 다른 CA에서 인증서와 함께 표시 하는 경우에 연결이 중단 되었습니다.  
  
## <a name="unknown-record-support"></a>알 수 없는 레코드 지원

"알 수 없는 레코드" RDATA 형식의 DNS 서버에 알려지지 않은 한 RR입니다. 알 수 없는 레코드 (RFC 3597) 형식에 대해 새로 추가 된 지원 Windows DNS 서버 영역 이진 실시간 형식으로 지원 되지 않는 레코드 종류를 추가할 수 있습니다 의미 합니다. Windows에 이미 캐싱 확인자입니다. 알 수 없는 레코드 종류를 처리 하는 기능입니다. Windows DNS 서버 알 수 없는 레코드에 대 한 특정 레코드 처리를 수행 하지 않습니다 하지만 됩니다 보냅니다 응답에 다시 것에 대 한 쿼리가 수신 하는 경우.  
  
## <a name="ipv6-root-hints"></a>IPv6 루트 힌트

IPV6 루트 힌트를 IANA에서 게시에 추가한 windows DNS 서버입니다. 이제 인터넷 이름 쿼리 이름 확인을 수행 하기 위한 IPv6 루트 서버를 사용할 수 있습니다.

## <a name="windows-powershell-support"></a>Windows PowerShell 지원

다음 새 Windows PowerShell cmdlet 및 매개 변수는 Windows Server 2016에서 도입 되었습니다.
  
-   **추가 DnsServerRecursionScope**합니다. 이 cmdlet에는 DNS 서버에서 새 재귀 범위를 만듭니다. 재귀 범위는 DNS 정책에서 DNS 쿼리 하는 데 사용 되는 전달자 목록을 지정 하는 데 사용 됩니다.  
  
-   **제거 DnsServerRecursionScope**합니다. 이 cmdlet는 기존 재귀 범위를 제거합니다.  
  
-   **집합 DnsServerRecursionScope**합니다. 이 cmdlet는 기존 재귀 범위의 설정을 변경합니다.  
  
-   **Get DnsServerRecursionScope**합니다. 이 cmdlet는 기존 재귀 범위에 대 한 정보를 검색합니다.  
  
-   **추가 DnsServerClientSubnet**합니다. 이 cmdlet는 새 DNS 클라이언트 서브넷을 만듭니다. 서브넷은 DNS 정책에 의해 DNS 클라이언트의 위치를 식별 하는 데 사용 됩니다.  
  
-   **제거 DnsServerClientSubnet**합니다. 이 cmdlet는 기존 DNS 클라이언트 서브넷을 제거합니다.  
  
-   **집합 DnsServerClientSubnet**합니다. 이 cmdlet는 기존 DNS 클라이언트 서브넷의 설정을 변경합니다.  
  
-   **Get DnsServerClientSubnet**합니다. 이 cmdlet는 기존 DNS 클라이언트 서브넷에 대 한 정보를 검색합니다.  
  
-   **추가 DnsServerQueryResolutionPolicy**합니다. 이 cmdlet는 새 DNS 쿼리 해결 정책을 만듭니다. DNS 쿼리 해결 정책 지정 하는 데 사용 됩니다 방법, 또는 다양 한 조건에 따라 쿼리 응답을 하는 경우.  
  
-   **제거 DnsServerQueryResolutionPolicy**합니다. 이 cmdlet는 기존 DNS 정책을 제거합니다.  
  
-   **집합 DnsServerQueryResolutionPolicy**합니다. 이 cmdlet는 기존 DNS 정책의 설정을 변경합니다.  
  
-   **Get DnsServerQueryResolutionPolicy**합니다. 이 cmdlet는 기존 DNS 정책에 대 한 정보를 검색 합니다.  
  
-   **Enable DnsServerPolicy**합니다. 이 cmdlet을 사용 하도록 기존 DNS 정책을 설정 합니다.  
  
-   **사용 안 함 DnsServerPolicy**합니다. 이 cmdlet은 기존 DNS 정책을 해제 합니다.  
  
-   **추가 DnsServerZoneTransferPolicy**합니다. 이 cmdlet는 새 DNS 서버 영역 전송 정책을 만듭니다. DNS 영역 전송 정책을를 거부 하거나 서로 다른 기준에 따라 영역 전송을 무시 여부를 지정 합니다.  
  
-   **제거 DnsServerZoneTransferPolicy**합니다. 이 cmdlet는 기존 DNS 서버 영역 전송 정책을 제거합니다.  
  
-   **집합 DnsServerZoneTransferPolicy**합니다. 이 cmdlet의 기존 DNS 서버 영역 전송 정책 설정을 변경합니다.  
  
-   **Get DnsServerResponseRateLimiting**합니다. 이 cmdlet는 RRL 설정을 검색합니다.  
  
-   **집합 DnsServerResponseRateLimiting**합니다. 이 cmdlet는 RRL 하려는 변경합니다.  
  
-   **추가 DnsServerResponseRateLimitingExceptionlist**합니다. 이 cmdlet에는 DNS 서버에서 RRL 예외 목록을 만듭니다.  
  
-   **Get DnsServerResponseRateLimitingExceptionlist**합니다. 이 cmdlet은 RRL excception 목록을 검색 합니다.  
  
-   **제거 DnsServerResponseRateLimitingExceptionlist**합니다. 이 cmdlet는 기존 RRL 예외 목록을 제거합니다.  
  
-   **집합 DnsServerResponseRateLimitingExceptionlist**합니다. 이 cmdlet는 RRL 예외 목록을 변경합니다.  
  
-   **추가 DnsServerResourceRecord**합니다. 이 cmdlet은 알 수 없는 레코드 형식을 지원 하도록 업데이트 되었습니다.  
  
-   **Get DnsServerResourceRecord**합니다. 이 cmdlet은 알 수 없는 레코드 형식을 지원 하도록 업데이트 되었습니다.  
  
-   **제거 DnsServerResourceRecord**합니다. 이 cmdlet은 알 수 없는 레코드 형식을 지원 하도록 업데이트 되었습니다.  
  
-   **집합 DnsServerResourceRecord**합니다. 이 cmdlet은 알 수 없는 레코드 형식을 지원 하도록 업데이트 되었고

자세한 내용은 다음 Windows Server 2016 Windows PowerShell 명령 참조 항목을 참조 하세요.

- [DnsServer 모듈](https://docs.microsoft.com/powershell/module/dnsserver/?view=win10-ps)
- [DnsClient 모듈](https://docs.microsoft.com/powershell/module/dnsclient/?view=win10-ps)

## <a name="see-also"></a>참고 항목  
  
-   [DNS 클라이언트의 새로운 기능](What-s-New-in-DNS-Client.md)  
  

  

