---
title: DHCP의 새로운 기능
description: 이 항목에 대 한 동적 호스트 구성 프로토콜 (DHCP) Windows Server 2016의 새로운 기능의 개요를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73cc5134f7af5063c912ad578fa7d660b3194aa1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840234"
---
# <a name="whats-new-in-dhcp"></a>DHCP의 새로운 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016의 새롭거나 변경 되는 동적 호스트 구성 프로토콜 (DHCP) 기능을 설명 합니다.
  
DHCP는 호스트는 TCP/IP를 구성할 때 복잡성 및 관리 부담을 줄이도록 설계 된는 Task Force IETF (Internet Engineering) 표준\-사설 인트라넷과 같은 네트워크에 기반 합니다. DHCP 서버 서비스를 사용하면 DHCP 클라이언트에서 TCP/IP를 구성하는 프로세스가 자동으로 수행됩니다.

다음 섹션에서는 dhcp 기능에 새로운 기능과 변경 사항에 대 한 정보를 제공합니다.

## <a name="dhcp-subnet-selection-options"></a>DHCP 서브넷 선택 옵션

DHCP는 이제 옵션 118 및 82 \(하위 5 옵션\)합니다. DHCP 프록시 클라이언트와 릴레이 에이전트에서 특정 IP 주소 범위와 범위를 특정 서브넷을 IP 주소를 요청할 수 있도록 이러한 옵션을 사용할 수 있습니다.


82 DHCP 옵션을 사용 하 여 구성 된 DHCP 릴레이 에이전트를 사용 하는 경우 하위\-5 옵션 릴레이 에이전트는 특정 IP 주소 범위에서 DHCP 클라이언트에 대 한 IP 주소 임대를 요청할 수 있습니다.

자세한 내용은 [DHCP 서브넷 선택 옵션](dhcp-subnet-options.md)합니다.

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>새 DHCP 서버에서 DNS 등록 오류에 대 한 이벤트 로깅

이제 DHCP는 DHCP 서버 DNS 레코드 등록 DNS 서버에서 실패 하는 상황에 대 한 로깅 이벤트를 포함 합니다.

자세한 내용은 [DHCP DNS 레코드 등록에 대 한 이벤트 로깅](dhcp-dns-events.md)합니다.

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>Windows Server 2016에서에서 DHCP NAP 지원 되지 않습니다.

네트워크 액세스 보호 \(NAP\) Windows Server 2012 R2에서 사용 되지 않습니다 및 DHCP 서버 역할 Windows Server 2016에서 더 이상 지원 NAP입니다. 자세한 내용은 참조 [기능 제거 또는 Windows Server 2012 r 2에서 사용 되지 않는](https://technet.microsoft.com/library/dn303411.aspx)합니다.  
  
Nap은 DHCP 서버 역할 Windows Server 2008에 도입 되었으며 Windows 10 및 Windows Server 2016 이전의 Windows 클라이언트 및 서버 운영 체제에서 지원 됩니다. 다음 표에서 Windows Server의 NAP에 대 한 지원을 요약 합니다.  
  
|운영 체제|NAP 지원|  
|--------------------|---------------|  
| Windows Server 2008 |지원됨|  
| Windows Server 2008 R2 |지원됨|  
| Windows Server 2012 |지원됨|  
| Windows Server 2012 R2 |지원됨|  
| Windows Server 2016|지원되지 않음|  
  
NAP 배포의 경우 NAP을 지 원하는 운영 체제를 실행 하는 DHCP 서버는 NAP DHCP 적용 방법에 대 한 NAP 적용 지점을 작동할 수 있습니다. DHCP NAP에서에 대 한 자세한 내용은 참조 하세요. [검사 목록: DHCP 적용 디자인 구현](https://technet.microsoft.com/library/dd314186.aspx)합니다.  
  
Windows Server 2016에서 DHCP 서버 NAP 정책을 적용 하지 않습니다 및 DHCP 범위 NAP을 사용할 수 없습니다.\-사용 하도록 설정 합니다. NAP 클라이언트도 있는 DHCP 클라이언트 컴퓨터 상태 문을 보낼 \(SoH\) 에 DHCP 요청 합니다. DHCP 서버에서 Windows Server 2016을 실행 하는 경우 이러한 요청이 없는 SoH가 처럼 처리 됩니다. DHCP 서버는 일반 DHCP 임대를 클라이언트에 부여합니다. 

Windows Server 2016을 실행 하는 서버에 RADIUS 프록시는 네트워크 정책 서버에 인증 요청을 전달 하는 경우 \(NPS\) 지 원하는 NAP, 이러한 NAP 클라이언트가 아닌 NAP으로 NPS를 통해 평가 되는\-다양 하 고 NAP 처리가 실패 합니다.
  
## <a name="see-also"></a>참조  
  
-   [동적 호스트 구성 프로토콜 (DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

