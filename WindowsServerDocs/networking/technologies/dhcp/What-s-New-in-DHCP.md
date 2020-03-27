---
title: DHCP의 새로운 기능
description: 이 항목에서는 Windows Server 2016에서 DHCP (Dynamic Host Configuration Protocol)의 새로운 기능에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 58d849fa1003148b034cc426817b97d3a70d4421
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312691"
---
# <a name="whats-new-in-dhcp"></a>DHCP의 새로운 기능

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016의 새롭거나 변경 되는 동적 호스트 구성 프로토콜 (DHCP) 기능을 설명 합니다.
  
DHCP는 개인 인트라넷과 같은 TCP/IP\-기반 네트워크에서 호스트를 구성 하는 작업의 복잡성 및 관리 부담을 줄이도록 설계 된 IETF (Internet 공학적 작업 Force) 표준입니다. DHCP 서버 서비스를 사용하면 DHCP 클라이언트에서 TCP/IP를 구성하는 프로세스가 자동으로 수행됩니다.

다음 섹션에서는 DHCP의 새로운 기능 및 기능에 대 한 정보를 제공 합니다.

## <a name="dhcp-subnet-selection-options"></a>DHCP 서브넷 선택 옵션

이제 DHCP는 옵션 118 및 82 \(하위 옵션 5\)를 지원 합니다. 이러한 옵션을 사용 하 여 DHCP 프록시 클라이언트 및 릴레이 에이전트가 특정 서브넷에 대 한 IP 주소와 특정 IP 주소 범위 및 범위를 요청할 수 있습니다.


DHCP 옵션 82, sub\-옵션 5로 구성 된 DHCP 릴레이 에이전트를 사용 하는 경우 릴레이 에이전트는 특정 IP 주소 범위에서 DHCP 클라이언트에 대 한 IP 주소 임대를 요청할 수 있습니다.

자세한 내용은 [DHCP Subnet Selection Options](dhcp-subnet-options.md)을 참조 하세요.

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>DHCP 서버의 DNS 등록 오류에 대 한 새 로깅 이벤트

이제 DHCP는 DNS 서버에서 DHCP 서버 DNS 레코드 등록이 실패 하는 상황에 대 한 로깅 이벤트를 포함 합니다.

자세한 내용은 [DNS 레코드 등록을 위한 DHCP 로깅 이벤트](dhcp-dns-events.md)를 참조 하세요.

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP NAP는 Windows Server 2016에서 지원 되지 않습니다.

NAP\) \(네트워크 액세스 보호는 Windows Server 2012 r 2에서 더 이상 사용 되지 않으며, Windows Server 2016에서는 DHCP 서버 역할이 더 이상 NAP를 지원 하지 않습니다. 자세한 내용은 참조 [기능 제거 또는 Windows Server 2012 r 2에서 사용 되지 않는](https://technet.microsoft.com/library/dn303411.aspx)합니다.  
  
NAP 지원은 windows Server 2008를 사용 하는 DHCP 서버 역할에 도입 되었으며 windows 10 및 Windows Server 2016 이전 버전의 Windows 클라이언트 및 서버 운영 체제에서 지원 됩니다. 다음 표에서 Windows Server의 NAP에 대 한 지원을 요약 합니다.  
  
|운영 체제|NAP 지원|  
|--------------------|---------------|  
| Windows Server 2008 |지원됨|  
| Windows Server 2008 R2 |지원됨|  
| Windows Server 2012 |지원됨|  
| Windows Server 2012 R2 |지원됨|  
| Windows Server 2016|지원되지 않음|  
  
NAP 배포의 경우 NAP을 지 원하는 운영 체제를 실행 하는 DHCP 서버는 NAP DHCP 적용 방법에 대 한 NAP 적용 지점을 작동할 수 있습니다. DHCP nap에서에 대 한 자세한 내용은 참조 [검사 목록: DHCP 적용 디자인 구현](https://technet.microsoft.com/library/dd314186.aspx)합니다.  
  
Windows Server 2016에서는 DHCP 서버가 NAP 정책을 적용 하지 않으며 DHCP 범위는 NAP\-사용 하도록 설정할 수 없습니다. NAP 클라이언트 이기도 한 DHCP 클라이언트 컴퓨터는 DHCP 요청을 사용 하 여 SoH\) \(상태 설명을 보냅니다. DHCP 서버에서 Windows Server 2016를 실행 하는 경우 이러한 요청은 SoH가 없는 것 처럼 처리 됩니다. DHCP 서버는 클라이언트에 정상적인 DHCP 임대를 부여 합니다. 

Windows Server 2016를 실행 하는 서버가 NAP를 지 원하는 NPS\) \(네트워크 정책 서버에 대 한 인증 요청을 전달 하는 RADIUS 프록시 인 경우 이러한 NAP 클라이언트는 nap가 아닌\-사용할 수 있고 NAP 처리가 실패 하는 경우 NPS에 의해 평가 됩니다.
  
## <a name="see-also"></a>참고 항목  
  
-   [DHCP(Dynamic Host Configuration Protocol)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

