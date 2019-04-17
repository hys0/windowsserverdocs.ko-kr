---
title: Domain Name System DNS)
description: 이 항목에서는 Windows Server 2016에는 dns 소개
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 23851d2d8015fc6ae9e0653e8a0843f8c4295162
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="domain-name-system-dns"></a>Domain Name System DNS)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

시스템 DNS (도메인 이름)은 산업 표준을 제품군의 TCP/IP을 구성 하는 프로토콜 중 하나 및 함께 DNS 클라이언트 및 DNS 서버 서비스를 제공 컴퓨터 이름을 TO-IP 주소 매핑 이름 해상도 컴퓨터 및 사용자에 게 합니다.  
  
> [!NOTE]  
> 이 항목에서는 뿐만 아니라 다음 DNS 콘텐츠를 사용할 수 있습니다.  
>   
> -   [DNS 클라이언트의 새로운 기능](What-s-New-in-DNS-Client.md)  
> -   [DNS 서버의 새로운 기능](What-s-New-in-DNS-Server.md)  
> -   [DNS 정책 시나리오 가이드](deploy/DNS-Policy-Scenario-Guide.md)  
> -   비디오: [Windows Server 2016: IPAM에서 DNS 관리](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)  
  
Windows Server 2016 DNS는 관리자 서버 또는 Windows PowerShell 명령을 사용 하 여 설치할 수 있는 서버 역할 합니다. 새 Active Directory 숲 및 도메인 설치 하는 경우 DNS은 자동으로 설치 된 Active Directory 숲 및 도메인에 대 한 전 세계 카탈로그 서버로.  
  
Active Directory Domain Services (AD DS) 사용 하는 도메인 컨트롤러 위치 메커니즘 DNS 합니다. 주 Active Directory 작업을 수행 하면 인증, 업데이트 하거나, 검색, 컴퓨터 사용 DNS 도메인 컨트롤러 Active Directory를 찾을 수 있습니다. 또한 도메인 컨트롤러 DNS 사용 하 여 서로 찾습니다.  
  
DNS 클라이언트 서비스는 Windows 운영 체제 모든 클라이언트 및 서버 버전에 포함 되어 및 운영 체제 설치 시 기본적으로 실행 합니다. TCP/IP 네트워크 연결이 DNS 서버를의 IP 주소와를 구성할 때 DNS 클라이언트 쿼리 DNS 서버 도메인 컨트롤러를 검색 하 고 컴퓨터 이름을 IP 주소를 확인 합니다. 예를 들어, Active Directory 도메인 네트워크 사용자 Active Directory 사용자 계정으로 로그인 할 때 DNS 클라이언트 서비스 쿼리 DNS 서버에 대 한 Active Directory 도메인 도메인 컨트롤러를 찾습니다. DNS 서버 쿼리에 응답 하지 않으면 클라이언트로 도메인 컨트롤러의 IP 주소를 제공, 클라이언트 도메인 컨트롤러에 연락 하 고 인증 프로세스를 시작할 수 있습니다.  
  
DNS 클라이언트와 Windows Server 2016 DNS 서버 서비스 tcp/ip 프로토콜에에서 포함 된 DNS 프로토콜을 사용 합니다. 다음 그림와 같이 DNS는 일부 응용 프로그램 계층 TCP/IP 참조 모델의입니다.  
  
![Tcp/ip DNS](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)  
  

