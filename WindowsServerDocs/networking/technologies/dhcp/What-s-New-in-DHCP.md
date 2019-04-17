---
title: DHCP의 새로운 기능
description: 이 항목에 대 한 Host Configuration DHCP (Dynamic Protocol) Windows Server 2016의 새로운 기능에 대 한 개요를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f67e5dfd8aefcf408a41f6fc919665419f0ff1c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-dhcp"></a>DHCP의 새로운 기능

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 DHCP Dynamic Host Configuration Protocol () 기능을 새로운 또는 변경 Windows Server 2016에서 설명 합니다.
  
DHCP는 인터넷 엔지니어링 작업 포스 (IETF) 표준 관리 부담와 같은 개인 인트라넷 IP\ 기반 네트워크 호스트 구성 복잡성 줄이기 하도록 설계 됩니다. DHCP 서버 서비스를 사용 하 여 DHCP 클라이언트에서 TCP/IP를 구성 하는 과정은 자동 합니다.

다음 섹션 dhcp 기능에서 새로운 기능과 변경에 대 한 정보를 제공합니다.

## <a name="dhcp-subnet-selection-options"></a>DHCP 서브넷 선택 옵션

이제 DHCP \(sub-option 5\) 118 및 82 옵션을 지원합니다. DHCP 프록시 클라이언트 프로그램과 릴레이 상담원에 대 한 특정 서브넷 및 IP 주소 범위 특정 및 범위 IP 주소를 요청할 수 있도록 이러한 옵션을 사용할 수 있습니다.

구성 된 가상 개인 네트워크 \(VPN\) 서버 Windows Server 2016 한 원격 액세스 서버 역할을 실행 하는 등 DHCP 옵션 118, DHCP 프록시 클라이언트를 사용 하는 경우에 VPN 서버의 VPN 클라이언트 특정 IP 주소 범위의 IP 주소 임대를 요청할 수 있습니다.

로컬 구성 된 82 sub\ 옵션 5, DHCP 옵션을 사용 하는 경우 릴레이 에이전트 DHCP 클라이언트 특정 IP 주소 범위의 IP 주소 임대를 요청할 수 있습니다.

자세한 내용은 참조 [DHCP 서브넷 선택 옵션](dhcp-subnet-options.md)합니다.

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>서버 DHCP에서 DNS 등록 오류에 대 한 새로운 로깅 이벤트

이제 DHCP 로깅 이벤트 서버 DNS 레코드 등록 DHCP에서 DNS 서버에 실패 하는 경우에 포함 되어 있습니다.

자세한 내용은 참조 [DNS 레코드 등록에 대 한 로그 이벤트 DHCP](dhcp-dns-events.md)합니다.

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP NAP Windows Server 2016에서에서 지원 되지 않는

네트워크 액세스 보호 \(NAP\) Windows Server 2012 r 2에 않으며 Windows Server 2016에 DHCP 서버 역할은 더 이상 지원 하지 NAP. 자세한 내용은 참조 [기능을 제거 하거나 Windows Server 2012 r 2에 사용 되지 않음](https://technet.microsoft.com/library/dn303411.aspx)합니다.  
  
NAP 지원 Windows Server 2008, DHCP 서버 역할을 도입 했습니다 및 Windows 10 및 Windows Server 2016 전에 Windows 클라이언트 및 서버 운영 체제에서 지원 됩니다. 다음 표에서 요약 NAP Windows server에서에 대 한 지원 합니다.  
  
|운영 체제|NAP 지원|  
|--------------------|---------------|  
| Windows Server 2008 |지원|  
| Windows Server 2008 R2 |지원|  
| Windows Server 2012 |지원|  
| Windows Server 2012 r 2 |지원|  
| Windows Server 2016|지원 되지 않음|  
  
DHCP를 지 원하는 NAP 운영 체제를 실행 NAP 배포에서 NAP DHCP 적용 방법에 대 한 NAP 집행 지점을 작동할 수 있습니다. DHCP NAP에 대 한 자세한 내용은 참조 [검사: DHCP 집행 디자인을 구현](https://technet.microsoft.com/library/dd314186.aspx)합니다.  
  
Windows Server 2016 DHCP 서버 NAP 정책을 적용 하지 않으면 및 DHCP 범위 NAP\ 사용할 수 없습니다. 도 NAP 클라이언트 있는 DHCP 클라이언트 컴퓨터 건강 \(SoH\) DHCP 요청에의 문의 전송 합니다. DHCP 서버 Windows Server 2016을 실행 중인 경우 없는 SoH 되기 전 까지는 하는 경우 이러한 요청 처리 됩니다. DHCP 서버 일반 DHCP 임대 클라이언트를 부여합니다. 

Windows Server 2016을 실행 하는 서버 RADIUS 프록시 인증 요청을 지 원하는 NAP 네트워크 정책 서버 \(NPS\) 전달 하는 경우, 해당 NAP 클라이언트 NAP\ 사용할 수 없는, 및 처리 오류 NAP NPS 평가 됩니다.
  
## <a name="see-also"></a>참조 하십시오  
  
-   [DHCP(Dynamic Host Configuration Protocol) DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

