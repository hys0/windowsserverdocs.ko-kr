---
title: DNS(Domain Name System)
description: 이 항목에서는 Windows Server 2016의 DNS에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6ad3b66ff0b271c3b6f6134a96aaf6b5171bc7d4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406165"
---
# <a name="domain-name-system-dns"></a>DNS(Domain Name System)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

도메인 이름 시스템 (DNS) TCP/IP를 구성 하는 프로토콜의 산업 표준 프로토콜 중 하나 이며 DNS 클라이언트와 DNS 서버 함께 컴퓨터와 사용자에 게 컴퓨터 이름-IP 주소 매핑 이름 확인 서비스를 제공 합니다.  
  
> [!NOTE]  
> 이 항목 외에 다음과 같은 DNS 콘텐츠를 사용할 수 있습니다.  
>   
> -   [DNS 클라이언트의 새로운 기능](What-s-New-in-DNS-Client.md)  
> -   [DNS 서버의 새로운 기능](What-s-New-in-DNS-Server.md)  
> -   [DNS 정책 시나리오 가이드](deploy/DNS-Policy-Scenario-Guide.md)  
> -   비디오: [Windows Server 2016: IPAM에서 DNS 관리](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)  
  
Windows Server 2016에서 DNS는 서버 관리자 또는 Windows PowerShell 명령을 사용 하 여 설치할 수 있는 서버 역할입니다. 새 Active Directory 포리스트 및 도메인을 설치 하는 경우 DNS 자동으로 설치 됩니다 Active directory 포리스트 및 도메인에 대 한 글로벌 카탈로그 서버입니다.  
  
Active Directory 도메인 서비스 (AD DS) 도메인 컨트롤러 위치 메커니즘으로 DNS를 사용합니다. 주 Active Directory 작업을 수행할 때는 인증, 업데이트 또는 검색, 컴퓨터 DNS 사용 하 여 Active Directory 도메인 컨트롤러를 찾는 합니다. 또한 도메인 컨트롤러는 DNS를 사용 하 여 서로 찾을 수 있습니다.  
  
DNS 클라이언트 서비스 Windows 운영 체제의 모든 클라이언트 및 서버 버전에 포함 되어 있으며 운영 체제 설치 시 기본적으로 실행 됩니다. DNS 서버의 IP 주소와는 TCP/IP 네트워크 연결을 구성한 경우 DNS 클라이언트는 도메인 컨트롤러를 검색 하 고 컴퓨터 이름을 IP 주소로 확인 하도록 DNS 서버를 쿼리 합니다. 예를 들어, Active Directory 사용자 계정이 있는 네트워크 사용자가 Active Directory 도메인에 로그인 할 때 DNS 클라이언트 서비스는 DNS 서버를 Active Directory 도메인에 대 한 도메인 컨트롤러를 찾을 쿼리 합니다. DNS 서버 쿼리에 응답 하 고 클라이언트에 도메인 컨트롤러의 IP 주소를 제공 하는 경우 클라이언트는 도메인 컨트롤러에 연결 및 인증 프로세스를 시작할 수 있습니다.  
  
Windows Server 2016 DNS 서버 및 DNS 클라이언트 서비스는 tcp/ip 프로토콜에에서 포함 된 DNS 프로토콜을 사용 합니다. DNS는 TCP/IP 참조 모델의 응용 프로그램 계층의 일부는 다음 그림에 나와 있는 것 처럼입니다.  
  
![TCP/IP의 DNS](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)  
  

