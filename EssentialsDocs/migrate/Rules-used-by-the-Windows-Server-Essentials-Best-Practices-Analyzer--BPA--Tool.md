---
title: "Windows Server Essentials 가장 좋은 방법은 분석기 (BPA) 도구에서 사용 규칙"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37e1dae7-586c-4dd7-bf83-7e14a9567c8f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c205bc8ff75bf64d4a13a7d799988c9d1ebe1a22
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="rules-used-by-the-windows-server-essentials-best-practices-analyzer-bpa-tool"></a>Windows Server Essentials 가장 좋은 방법은 분석기 (BPA) 도구에서 사용 규칙

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 문서에서의 Windows Server Essentials 최상의 관행 분석기 (BPA) 사용 규칙에 설명 합니다. BPA Windows Server Essentials 실행 하 고 문제를 설명 하 고 해결 하는 방법과 대 한 추천을 제공 하는 보고서를 제공 하는 서버를 검사 합니다. 권장 되는 Windows Server Essentials에 대 한 제품 지원 조직 개발 됩니다.  
  
## <a name="using-the-tool"></a>이 도구를 사용 하 여  
 Windows Server Essentials 2011, Windows 작은 Business Server 2011 필수 패키지 또는 Windows Home Server 2011, 설정 및 데이터 마이그레이션을 완료 한 후는 BPA 대상 서버에서 실행 하도록 Windows Server Essentials로 마이그레이션할 경우에 것이 표준 좋습니다. 언제 든 지 대시보드에서 도구를 실행할 수 있습니다.  
  
#### <a name="to-run-the--windows-server-essentials-bpa-on-the-server"></a>Windows Server Essentials BPA 서버에서 실행 하려면  
  
1.  관리자 권한으로 서버에에 로그인 하 고 대시보드 다음 엽니다.  
  
2.  클릭 하 고 대시보드에서 **디바이스** 탭 합니다.  
  
3.  에 **서버 작업** 창 클릭 **모범 사례 분석기**합니다.  
  
4.  각 BPA 메시지를 검토 하 고 필요한 경우 문제를 해결 하 고 지침을 따릅니다.  
  
## <a name="rules-used-by-the-best-practices-analyzer"></a>모범 사례 분석기 사용 규칙  
  
### <a name="disable-ip-filtering"></a>IP 필터링 사용 안 함  
 **문제:** IP 필터링 서버에 사용 중입니다. IP 필터링 사용 하지 않도록 설정 해야 합니다.  
  
 **영향을:** 네트워크 교통 IP 필터링을 사용 하는 경우 차단 될 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-disable-ip-filtering"></a>IP 필터링을 사용 하지 않도록 설정 하려면  
  
1.  서버에 regedit.exe 엽니다.  
  
2.  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters로 이동 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **EnableSecurityFilters**을 차례로 클릭 하 고 **수정**합니다.  
  
4.  에 **DWORD 편집 (32 비트) 값** 창 변경은 **값 데이터** 0 필드와 클릭 한 다음 **확인**합니다.  
  
5.  변경 내용을 적용을 서버를 다시 시작 합니다.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-set-to-start-automatically-by-default"></a>기본적으로 자동으로 시작 하도록 설정 해야 분산 트랜잭션이 Coordinator (MSDTC) 서비스  
 **문제:** MSDTC 서비스가 자동으로 시작 되도록 구성 되지 않은  
  
 **영향을:** MSDTC 서비스 수 자동으로 시작 되지 서버를 시작 합니다. 서비스를 중지 하는 경우 몇 가지 SQL Server 또는 COM 기능 실패할 수 있습니다. 결과적으로, Microsoft SQL Server 또는 COM 기능을 사용 하는 응용 프로그램 제대로 작동 하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-msdtc-service-to-start-automatically"></a>자동으로 시작 되도록 MSDTC 서비스 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Distributed Transaction Coordinator** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동 (시작 지연)**, 클릭 한 다음 **확인**합니다.  
  
### <a name="the-netlogon-service-should-be-configured-to-start-automatically-by-default"></a>기본적으로 자동으로 시작 되도록 Netlogon 서비스는 구성 해야  
 **문제:** Netlogon 서비스가 자동으로 시작 되도록 구성 되지 않았습니다.  
  
 **영향을:** Netlogon 서비스 수 자동으로 시작 되지 서버를 시작 합니다. 서비스를 중지 서버 사용자 및 서비스 인증할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-netlogon-service-to-start-automatically"></a>자동으로 시작 되도록 Netlogon 서비스 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Netlogon** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-dns-client-service-should-be-configured-to-start-automatically-by-default"></a>DNS 클라이언트 서비스는 기본적으로 자동으로 시작 되도록 구성 해야  
 **문제:** DNS 클라이언트 서비스가 자동으로 시작 되도록 구성 되지 않았습니다.  
  
 **영향을:** DNS 클라이언트 서비스 수 자동으로 시작 되지 서버를 시작 합니다. 이 서비스를 중지 서버 수 DNS 이름을 확인할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-dns-client-service-to-start-automatically"></a>DNS 클라이언트 서비스가 자동으로 시작 되도록 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **DNS 클라이언트** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-dns-server-service-should-be-configured-to-start-automatically-by-default"></a>DNS 서버가 서비스는 기본적으로 자동으로 시작 되도록 구성 해야  
 **문제:** DNS 서버 서비스가 자동으로 시작 되도록 구성 되지 않았습니다.  
  
 **영향을:** DNS 서버 서비스 수 자동으로 시작 되지 서버를 시작 합니다. 이 서비스를 중지 DNS 업데이트가 발생 하지 않습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-dns-server-service-to-start-automatically"></a>자동으로 시작 되도록 DNS 서버 서비스 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **DNS 서버** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="active-directory-web-services-is-not-set-to-the-default-start-mode"></a>Active Directory 웹 서비스 기본 모드를 시작 화면으로 설정 되지 않은  
 **문제:** Active Directory 웹 서비스 기본 시작 모드를 자동으로 설정 되지 않은 합니다.  
  
 **영향을:** Active Directory 웹 서비스 (ADWS) 기본 시작 모드를 자동으로 설정 되지 않은 합니다. 서버에서 ADWS를 중지 하거나 사용 하지 않도록 설정 하는 경우 Windows PowerShell 또는 Active Directory 관리 센터에 대 한 Active Directory 모듈 등 클라이언트 응용 프로그램에 액세스 하거나이 서버에서 실행 중인 디렉터리 서비스 인스턴스 관리할 수 없습니다. For more information, see [What's New in AD DS: Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in the Windows Server Technical Library.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-active-directory-web-services-service-to-start-automatically"></a>자동으로 시작 되도록 Active Directory 웹 서비스 서비스 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Active Directory 웹 서비스** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-dhcp-client-service-should-be-configured-to-start-automatically-by-default"></a>기본적으로 자동으로 시작 하도록 예약할 서비스는 구성 해야  
 **문제:** 자동으로 시작 하도록 예약할 서비스가 구성 되지 않았습니다.  
  
 **영향을:** DHCP 클라이언트 서비스는 자동으로 시작 되지 서버를 시작 합니다. 이 서비스를 중지 클라이언트 컴퓨터 서버에서 IP 주소를 받을 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-dhcp-client-service-to-start-automatically"></a>자동으로 시작 하도록 예약할 서비스 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **DHCP 클라이언트** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-iis-admin-service-should-be-configured-to-start-automatically-by-default"></a>기본적으로 자동으로 시작 되도록 IIS 관리자 서비스는 구성 해야  
 **문제:** IIS 관리자 서비스가 자동으로 시작 되도록 구성 되지 않았습니다.  
  
 **영향을:** IIS 관리 서비스는 자동으로 시작 되지 서버를 시작 합니다. 이 서비스를 중지 하는 경우 원격 Web Access와 같은 서버에서 실행 되는 웹 사이트에 액세스할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-iis-admin-service-to-start-automatically"></a>자동으로 시작 되도록 IIS 관리 서비스의 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭 **IIS 관리 서비스**을 차례로 클릭 하 고 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-world-wide-web-publishing-service-should-be-configured-to-start-automatically-by-default"></a>기본적으로 자동으로 시작 되도록 World Wide Web Publishing Service 구성 해야  
 **문제:** 자동으로 시작 되도록 World Wide Web Publishing Service 구성 되지 않았습니다.  
  
 **영향을:** World Wide Web Publishing Service 수 자동으로 시작 되지 서버를 시작 합니다. 이 서비스를 중지 하는 경우 원격 Web Access와 같은 서버에서 실행 되는 웹 사이트에 액세스할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-world-wide-web-publishing-service-to-start-automatically"></a>자동으로 시작 되도록 World Wide Web Publishing Service 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭 **World Wide Web Publishing Service**을 차례로 클릭 하 고 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-remote-registry-service-should-be-configured-to-start-automatically-by-default"></a>기본적으로 자동으로 시작 되도록 원격 레지스트리 서비스는 구성 해야  
 **문제:** 원격 레지스트리 서비스가 자동으로 시작 되도록 구성 되지 않았습니다.  
  
 **영향을:**  
  
 서버를 시작할 때 원격 레지스트리 서비스가 자동으로 시작 되지 않을 수 있습니다. 이 서비스를 중지 하는 경우 원격으로 일부 네트워크 작업을 수행할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-remote-registry-service-to-start-automatically"></a>자동으로 시작 되도록 원격 레지스트리 서비스 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **원격 레지스트리** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-remote-desktop-gateway-service-should-be-configured-to-start-automatically-by-default"></a>원격 데스크톱 게이트웨이의 서비스는 기본적으로 자동으로 시작 되도록 구성 해야  
 **문제:** 원격 데스크톱 게이트웨이의 서비스가 자동으로 시작 되도록 구성 되지 않았습니다.  
  
 **영향을:** 이 서비스를 중지 하는 경우 사용자가 못할 웹에 대 한 원격 액세스를 사용 하 여 컴퓨터에 액세스할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-remote-desktop-gateway-service-to-start-automatically"></a>원격 데스크톱 게이트웨이의 서비스를 자동으로 시작 하도록 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **원격 데스크톱 게이트웨이의** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동 (시작 지연)**, 클릭 한 다음 **확인**합니다.  
  
### <a name="the-windows-time-service-should-be-configured-to-start-automatically-by-default"></a>기본적으로 자동으로 시작 되도록 Windows 시간 서비스는 구성 해야  
 **문제:** Windows 시간 서비스가 자동으로 시작 되도록 구성 되지 않았습니다.  
  
 **영향을:** 데이터 및 시간 동기화 사용할 수 없는 경우이 서비스를 중지 합니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-windows-time-service-to-start-automatically"></a>자동으로 시작 되도록 Windows 시간 서비스 구성 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Windows 시간** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **일반** 탭에서 변경는 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-started"></a>분산 트랜잭션이 Coordinator (MSDTC) 서비스를 시작 합니다.  
 **문제:** MSDTC 서비스 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** 이 서비스를 중지 하는 경우 몇 가지 SQL Server 또는 COM 기능 실패할 수 있습니다. 결과적으로, Microsoft SQL Server 또는 COM 기능을 사용 하는 응용 프로그램 제대로 작동 하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-distributed-transaction-coordinator-service"></a>Distributed Transaction Coordinator 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Distributed Transaction Coordinator** 서비스를 마우스 클릭 한 다음 **시작**합니다.  
  
### <a name="the-netlogon-service-should-be-started"></a>Netlogon 서비스를 시작 합니다.  
 **문제:** Netlogon 서비스 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** 이 서비스를 시작 하지 않으면 사용자 및 서비스 서버 인증 되지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-netlogon-service"></a>Netlogon 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Netlogon** 서비스를 마우스 클릭 한 다음 **시작**합니다.  
  
### <a name="the-dns-client-service-should-be-started"></a>DNS 클라이언트 서비스를 시작 합니다.  
 **문제:** DNS 클라이언트 서비스 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** 이 서비스를 시작 하지 않으면 서버 못할 DNS 이름을 확인할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-dns-client-service"></a>DNS 클라이언트 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **DNS 클라이언트** 서비스를 마우스 클릭 한 다음 **시작**합니다.  
  
### <a name="the-dns-server-service-should-be-started"></a>DNS 서버 서비스를 시작 합니다.  
 **문제:** DNS 서버 서비스 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** DNS 서버 서비스를 시작 하지 않으면 DNS 업데이트가 발생 하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-dns-server-service"></a>DNS 서버 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **DNS 서버** 서비스를 마우스 클릭 한 다음 **시작**합니다.  
  
### <a name="active-directory-web-services-is-not-started"></a>Active Directory 웹 서비스를 시작 하지 않으면  
 **문제:** Active Directory 웹 서비스 시작 되지 않습니다.  
  
 **영향을:** Active Directory 웹 서비스 (ADWS)가 시작 되지 않습니다. 서버에서 ADWS를 중지 하거나 사용 하지 않도록 설정 하는 경우 Windows PowerShell 또는 Active Directory 관리 센터에 대 한 Active Directory 모듈 등 클라이언트 응용 프로그램에 액세스 하거나이 서버에서 실행 중인 디렉터리 서비스 인스턴스 관리할 수 없습니다. For more information, see [What's New in AD DS: Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in the Windows Server Technical Library.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-active-directory-web-services-service"></a>Active Directory 웹 서비스 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭 **Active Directory 웹 서비스**을 차례로 클릭 하 고 **시작**합니다.  
  
### <a name="the-dhcp-client-service-should-be-started"></a>DHCP 클라이언트 서비스를 시작 해야  
 **문제:** DHCP 클라이언트 서비스 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** 이 서비스를 중지 하는 경우 클라이언트 컴퓨터 서버에서 IP 주소를 받을 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-dhcp-client-service"></a>DHCP 클라이언트 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **DHCP 클라이언트** 서비스를 마우스 클릭 한 다음 **시작**합니다.  
  
### <a name="the-iis-admin-service-should-be-started"></a>IIS 관리 서비스를 시작 합니다.  
 **문제:** IIS 관리 서비스 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** 이 서비스를 중지 하는 경우 사용자 수 하지 원격 Web Access와 같은 서버에서 실행 되는 웹 사이트에 액세스할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-iis-admin-service"></a>IIS 관리 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭 **IIS 관리 서비스**을 차례로 클릭 하 고 **시작**합니다.  
  
### <a name="the-world-wide-web-publishing-service-should-be-started"></a>World Wide Web Publishing Service는 시작 합니다.  
 **문제:** World Wide Web Publishing Service 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** 이 서비스를 중지 하는 경우 사용자 수 하지 원격 Web Access와 같은 서버에서 실행 되는 웹 사이트에 액세스할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-world-wide-web-publishing-service"></a>World Wide Web Publishing Service를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭 **World Wide Web Publishing Service**을 차례로 클릭 하 고 **시작**합니다.  
  
### <a name="the-remote-desktop-gateway-service-should-be-started"></a>원격 데스크톱 게이트웨이의 서비스를 시작 합니다.  
 **문제:** 원격 데스크톱 게이트웨이의 서비스 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** 이 서비스를 중지 하는 경우 사용자가 못할 웹에 대 한 원격 액세스를 사용 하 여 컴퓨터에 액세스할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-remote-desktop-gateway-service"></a>원격 데스크톱 게이트웨이의 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **원격 데스크톱 게이트웨이의** 서비스를 마우스 클릭 한 다음 **시작**합니다.  
  
### <a name="the-windows-time-service-should-be-started"></a>Windows 시간 서비스를 시작 합니다.  
 **문제:** Windows 시간 서비스 서버에서 실행 되 고 있지 합니다.  
  
 **영향을:** 이 서비스를 중지 하는 경우 데이터와 시간 동기화 사용할 수 없게 됩니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-windows-time-service"></a>Windows 시간이 서비스를 시작 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Windows 시간** 서비스를 마우스 클릭 한 다음 **시작**합니다.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-logon-account-should-be-nt-authoritynetwork-service"></a>분산 트랜잭션이 Coordinator (MSDTC) 서비스 로그온 계정 NT AUTHORITY\Network 서비스 있어야 합니다.  
 **문제:** 분산 트랜잭션이 Coordinator (MSDTC) 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하는 데 필요한 사용 권한이 없을 수 있습니다. 결과적으로, SQL Server 또는 COM 기능을 사용 하는 응용 프로그램 제대로 작동 하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-logon-account-for-the-service"></a>서비스에 대 한 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Distributed Transaction Coordinator** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **이 계정**, 입력 **NT AUTHORITY\Network 서비스**, 클릭 한 다음 **확인**합니다.  
  
### <a name="the-netlogon-service-should-use-the-local-system-account-as-its-logon-account"></a>Netlogon 서비스가 로그온 계정으로 시스템 로컬 계정을 사용 해야  
 **문제:** Netlogon 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하는 데 필요한 사용 권한이 없을 수 있습니다. 결과적으로, 사용자 및 서비스 서버 인증 되지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-netlogon-service-logon-account"></a>Netlogon 서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Netlogon** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **시스템 로컬 계정**합니다.  
  
### <a name="the-dns-client-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>DNS 클라이언트 서비스 NT AUTHORITY\Network 서비스 계정을 로그온 계정으로 사용 해야  
 **문제:** DNS 클라이언트 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하는 데 필요한 사용 권한이 없을 수 있습니다. 결과적으로, 서버 DNS 이름을 확인할 수 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-dns-client-service-logon-account"></a>DNS 클라이언트 서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **DNS 클라이언트** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **이 계정**, 한 다음 입력 **NT AUTHORITY\Network 서비스**합니다.  
  
### <a name="the-dns-server-service-should-use-the-local-system-account-as-its-logon-account"></a>DNS 서버 서비스 로그온 계정으로 시스템 로컬 계정을 사용 해야  
 **문제:** DNS 서버 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하는 데 필요한 사용 권한이 없을 수 있습니다. 결과적으로, DNS 업데이트 하지 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-dns-server-service-logon-account"></a>DNS 서버 서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 열기  
  
2.  마우스 오른쪽 단추로 클릭는 **DNS 서버** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **시스템 로컬 계정**합니다.  
  
### <a name="active-directory-web-services-is-not-the-default-logon-account"></a>Active Directory 웹 서비스의 기본 로그온 계정을 아닙니다.  
 **문제:** Active Directory 웹 서비스의 기본 로그온 계정을 아닙니다. 기본적으로 로그온 계정을 설정 **시스템 로컬 계정**합니다.  
  
 **영향을:** Active Directory 웹 서비스 (ADWS)가 시작 되지 않습니다. 서버에서 ADWS를 중지 하거나 사용 하지 않도록 설정 하는 경우 Windows PowerShell 또는 Active Directory 관리 센터에 대 한 Active Directory 모듈 등 클라이언트 응용 프로그램에 액세스 하거나이 서버에서 실행 중인 디렉터리 서비스 인스턴스 관리할 수 없습니다. For more information, see [What's New in AD DS: Active Directory Web Services](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx) in the Windows Server Technical Library.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-active-directory-web-services-logon-account"></a>Active Directory 웹 서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭 **Active Directory 웹 서비스**을 차례로 클릭 하 고 **속성**합니다.  
  
3.  변경은 **시작 유형** 에 **자동**을 차례로 클릭 하 고 **확인**합니다.  
  
4.  Active Directory 웹 서비스의 **속성**, 클릭 하 고 **로그온** 탭 합니다.  
  
5.  선택는 **시스템 로컬 계정** 옵션을 클릭 한 다음 **확인**합니다.  
  
### <a name="the-windows-update-service-should-use-the-local-system-account-as-its-logon-account"></a>Windows 업데이트 서비스 로그온 계정으로 시스템 로컬 계정을 사용 해야  
 **문제:** 자동 업데이트 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하는 데 필요한 사용 권한이 없을 수 있습니다. 결과적으로, 서버 자동 업데이트를 받지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-windows-update-service-logon-account"></a>Windows 업데이트 서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Windows 업데이트** 서비스를 마우스 속성을 클릭 합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **시스템 로컬 계정**합니다.  
  
### <a name="the-dhcp-client-service-should-use-the-nt-authoritylocalservice-account-as-its-logon-account"></a>DHCP 클라이언트 서비스 NT AUTHORITY\LocalService 계정을 로그온 계정으로 사용 해야  
 **문제:** DHCP 클라이언트 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하는 데 필요한 사용 권한이 없을 수 있습니다. 따라서 클라이언트 컴퓨터 서버에서 IP 주소를 표시 되지 않습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-dhcp-client-service-logon-account"></a>DHCP 클라이언트 서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **DHCP 클라이언트** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **이 계정**, 한 다음 입력 **NT AUTHORITY\Local 서비스**합니다.  
  
### <a name="the-iis-admin-service-should-use-the-local-system-account-as-its-logon-account"></a>IIS 관리 서비스 로그온 계정으로 시스템 로컬 계정을 사용 해야  
 **문제:** IIS 관리 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 필요한 사용 권한이 없을 수 예상 대로 작동 하는 데 필요한는 합니다. 결과적으로, 원격 Web Access와 같은 서버에서 실행 되는 웹 사이트에 액세스할 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-service-logon-account"></a>서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭 **IIS 관리 서비스**을 차례로 클릭 하 고 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **시스템 로컬 계정**합니다.  
  
### <a name="the-world-wide-web-publishing-service-should-use-the-local-system-account-as-its-logon-account"></a>World Wide Web Publishing Service 로그온 계정으로 시스템 로컬 계정을 사용 해야  
 **문제:** World Wide Web Publishing Service에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하는 데 필요한 사용 권한이 없을 수 있습니다. 결과적으로, 원격 Web Access와 같은 서버에서 실행 되는 웹 사이트에 액세스할 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-world-wide-web-publishing-service-logon-account"></a>World Wide Web Publishing Service 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭 **World Wide Web Publishing Service**을 차례로 클릭 하 고 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **시스템 로컬 계정**합니다.  
  
### <a name="the-remote-desktop-gateway-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>원격 데스크톱 게이트웨이의 서비스 NT AUTHORITY\Network 서비스 계정을 로그온 계정으로 사용 해야  
 **문제:** 원격 데스크톱 게이트웨이의 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하도록 적절 한 권한이 없을 수 있습니다. 결과적으로, 사용자가 수 웹에 대 한 원격 액세스를 사용 하 여 컴퓨터에 액세스할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-remote-desktop-gateway-service-logon-account"></a>원격 데스크톱 게이트웨이의 서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **원격 데스크톱 게이트웨이의** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **이 계정**, 한 다음 입력 **NT AUTHORITY\Network 서비스**합니다.  
  
### <a name="the-windows-time-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Windows 시간 서비스 NT AUTHORITY\Network 서비스 계정을 로그온 계정으로 사용 해야  
 **문제:** Windows 시간 서비스에 대 한 기본 로그온 계정을 변경 됩니다.  
  
 **영향을:** 서비스 예상 대로 작동 하도록 적절 한 권한이 없을 수 있습니다. 결과적으로, 날짜 및 시간 동기화 수 사용할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-windows-time-service-logon-account"></a>Windows 시간 서비스 로그온 계정을 변경 하려면  
  
1.  서버에서 services.msc 엽니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **Windows 시간** 서비스를 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **로그온** 탭을 선택 하 고 **이 계정**, 한 다음 입력 **NT AUTHORITY\Local 서비스**합니다.  
  
### <a name="the-built-in-administrators-group-does-not-have-the-right-to-log-on-as-batch-job"></a>기본 제공 된 관리자가 그룹 배치 작업으로 로그온 수 있는 권한이 없는  
 **문제:** 기본 관리자가 그룹 일괄 작업으로 로그온 수 있는 권한이 없는 합니다.  
  
 **영향을:** 관리자 알림을 만들고 경고를 관리자가 하지 로그온 할 때 실행할 구성, 경고 2147943785에 오류 코드와 함께 실패 합니다.  
  
 **Resolution:**  For information about how to give the built-in Administrators group permission to log on as a batch job, see [Give the built-in Administrator group the right to log on as a batch job](https://technet.microsoft.com/library/jj635076) (https://technet.microsoft.com/library/jj635076).  
  
### <a name="the-windows-firewall-is-turned-off"></a>Windows 방화벽  
 **문제:** Windows 방화벽 꺼져 있습니다. 기본값 켜져 있습니다.  
  
 **영향을:** 방화벽 설정에 따라 Windows 방화벽 로부터 보호할 수 서버 및 네트워크 악성 활동 서버를 통해 전달에서 일부 정보를 차단 합니다.  
  
 **해결 방법:**  
  
##### <a name="to-turn-on-windows-firewall-on-the-server"></a>서버에서 Windows 방화벽을 켜려면  
  
1.  서버에서 제어판을 엽니다.  
  
2.  제어판에서 클릭 **시스템 및 보안**을 차례로 클릭 하 고 **Windows 방화벽**합니다.  
  
3.  Windows 방화벽을 클릭 **Windows 방화벽 설정 또는 해제**는 **Windows 방화벽** 옵션을 클릭 한 다음 **확인**합니다.  
  
### <a name="the-internal-network-adapter-is-not-configured-to-register-ip-address-in-dns"></a>IP 주소 DNS에 등록 하도록 내부 네트워크 어댑터 구성 되지 않은  
 **문제:** DNS에 IP 주소를 등록 하기 위해 내부 네트워크 어댑터가 구성 되지 않았습니다.  
  
 **영향을:** 내부 네트워크 어댑터의 IP 주소 dns에서 등록 되지 않은 경우 아닐 서버의 컴퓨터 이름을 사용 하 여 서버에 액세스할 수 있습니다.  
  
 **해결 방법:** 내부 네트워크 어댑터 DNS에 등록 하도록 구성 되어 있는지 확인 합니다.  
  
### <a name="dns-the-values-for-the-dns-forwardingtimeout-and-recursiontimeout-registry-key-are-identical"></a>DNS: DNS ForwardingTimeout 및 RecursionTimeout 레지스트리 키에 대 한 값 동일 있습니다.  
 **문제:** DNS ForwardingTimeout 레지스트리 키 값은 RecursionTimeout 레지스트리 키 값과 같은 수 없습니다.  
  
 **영향을:** 이름으로 인터넷 리소스에 액세스 하지 못할 수도 있습니다.  
  
 **해결 방법:** 레지스트리의 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters에 있는, ForwardingTimeout 키 값 보다 커야 RecursionTimeout 레지스트리 키에 대 한 값으로 설정 합니다.  
  
### <a name="the-forward-dns-zone-for-your-active-directory-domain-does-not-allow-secure-updates"></a>앞으로 DNS 영역에 대 한 Active Directory 도메인에는 보안 업데이트  
 **문제:** 앞으로 조회 영역이 보안 동적 업데이트를 받도록 구성 해야 합니다.  
  
 **영향을:** 권한이 있는 사용자만 보안 동적 업데이트 사용 시간과 호스트 레코드를 변경할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-forward-lookup-zone-for-your-active-directory-domain"></a>앞으로 조회 영역이 Active Directory 도메인에 대 한 구성 하려면  
  
1.  서버에서 dnsmgmt.msc 엽니다.  
  
2.  앞으로 조회 영역이 Active Directory 도메인에 대 한를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
3.  에 **동적 업데이트** 드롭다운 목록을 **만 보안**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-forward-dns-zone-does-not-allow-secure-updates"></a>DNS 영역 보안 허용 하지 않는 앞 업데이트  
 **문제:** 앞으로 조회 영역이 동적 업데이트만 수 있도록 _msdcs.* 영역에 대 한 구성 해야 합니다.  
  
 **영향을:** 권한이 있는 사용자만 보안 동적 업데이트 사용 시간과 호스트 msdcs.* 영역에 있는 레코드를 변경할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-allow-secure-updates-in-the-msdcs-zone"></a>_Msdcs 영역에서 보안 업데이트를 받도록  
  
1.  서버에서 dnsmgmt.msc 엽니다.  
  
2.  앞으로 조회 영역이 _msdcs 영역에 대 한를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
3.  에 **동적 업데이트** 드롭다운 목록을 **만 보안**을 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer 강화 된 보안 구성 되지 사용 하도록 설정  
 **문제:** Internet Explorer의 보안 강화 구성을 (IE ESC) 현재 관리자가 그룹에 대 한 사용 되지 않습니다.  
  
 **영향을:** 서버 및 Internet Explorer Internet Explorer의 보안 강화 구성을 관리자가 그룹에 대 한 사용 하지 않으면, 악의적인 공격 콘텐츠 거미줄 사이로 발생할 수 있는 및 응용 프로그램 스크립트에 노출 증가 했습니다.  
  
 **해결 방법:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer의 보안 강화 구성을 사용 하도록 설정 하려면  
  
1.  열린 **서버 관리자** 서버 및 클릭 **로컬 서버**합니다.  
  
2.  에 **속성** 창에 대 한 설정을 변경 **보안 구성 향상 된 IE** 에 **에**를 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer 강화 된 보안 구성 되지 사용 하도록 설정  
 **문제:** Internet Explorer의 보안 강화 구성을 (IE ESC) 현재의 사용자 그룹에 대 한 사용 되지 않습니다.  
  
 **영향을:** 서버 및 Internet Explorer의 사용자 그룹에 대 한 고급 보안 구성 Internet Explorer를 사용 하지 않으면, 악의적인 공격 콘텐츠 거미줄 사이로 발생할 수 있는 및 응용 프로그램 스크립트에 노출 증가 했습니다.  
  
 **해결 방법:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer의 보안 강화 구성을 사용 하도록 설정 하려면  
  
1.  열린 **서버 관리자**을 차례로 클릭 하 고 **로컬 서버**합니다.  
  
2.  에 **속성** 창에 대 한 설정을 변경 **보안 구성 향상 된 IE** 에 **에**를 차례로 클릭 하 고 **확인**합니다.  
  
### <a name="the-source-server-remains-in-active-directory-sites-and-services"></a>원본 서버 Active Directory 사이트 및 서비스에 남습니다.  
 **문제:** Small Business Server Windows를 실행 하는 원본 서버 Active Directory 사이트 및 서비스에서 여전히 존재 Default-First-Site-Name에에서 있습니다.  
  
 **영향을:** 클라이언트 컴퓨터 활성 디렉터 사이트 및 서비스에서 원본 서버 설정을 변경 하거나 경우 연결 문제가 발생할 수 있습니다: s 합니다.  
  
 **해결 방법:** 원본 서버 내리기, 된 도메인의 제거 한 다음 Active Directory 사이트 및 서비스와 Active Directory 사용자 및 컴퓨터 원본 서버를 삭제 해야 합니다.  
  
### <a name="source-server-remains-in-sbscomputer-ou"></a>원본 서버 SBSComputer OU에 유지 됩니다.  
 **문제:** Active Directory 사용자 및 컴퓨터 실행 하는 Small Business Server Windows 원본 서버 여전히 존재 합니다.  
  
 **영향을:** 클라이언트 컴퓨터 활성 디렉터 사용자 및 컴퓨터에서 원본 서버 설정을 변경 하거나 경우 연결 문제가 발생할 수 있습니다: s 합니다.  
  
 **해결 방법:** 원본 서버 내리기, 된 도메인의 제거 한 다음 Active Directory 사이트 및 서비스와 Active Directory 사용자 및 컴퓨터 원본 서버를 삭제 해야 합니다.  
  
### <a name="a-group-policy-is-missing"></a>그룹 정책을 누락 된  
 **문제:** 기본 도메인 정책 그룹 정책을 없습니다.  
  
 **영향을:** 기본 도메인 정책 적절 한 도메인 기능에 대 한 필요 합니다.  
  
 **해결 방법:**  
  
##### <a name="to-restore-a-missing-group-policy"></a>누락 된 그룹 정책 복원 하려면  
  
1.  서버에서 gpmc.msc 엽니다.  
  
2.  그룹 정책 관리자에서 도메인 숲 확장 하 고 콘솔 트리에서 검색는 **기본 도메인 정책** 그룹 정책 개체 합니다.  
  
3.  정책 트리에서 표시 되지 않으면 시스템 상태 백업에서 복원 합니다.  
  
### <a name="no-dns-name-server-resource-records"></a>없음 DNS 서버 리소스 기록 이름  
 **문제:** 서버에 대 한 앞으로 조회 영역에서 DNS 이름 (NS) 서버 리소스 레코드가 없는 합니다.  
  
 **영향을:** DNS 이름 (NS) 서버 리소스 레코드가 앞으로 조회 영역에 대 한 Active Directory 도메인에 없으면 사용자가 못할 리소스 네트워크 또는 인터넷에 액세스할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-restore-missing-dns-name-server-resource-records"></a>누락 복원 하려면 DNS 이름 서버 리소스 기록  
  
1.  서버에서 dnsmgmt.msc 엽니다.  
  
2.  DNS 관리자에 대 한 Active Directory 도메인 앞으로 조회 영역이 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **이름 서버** 탭을 설정이 올바른지 확인 합니다.  
  
4.  클릭 한 다음 하 고 필요한 변경을 수행 **확인** 설정을 저장 합니다.  
  
### <a name="no-dns-name-server-records"></a>이름 DNS 서버 레코드가 없습니다  
 **문제:** 레코드가 이름 DNS 서버 (NS) 리소스 서버에 대 한 _msdcs 영역에 (예: _msdcs.contoso.local).  
  
 **영향을:** DNS 이름 (NS) 서버 리소스 레코드가 _msdcs 영역에 대 한 Active Directory 도메인 없으면 사용자가 하지 수 리소스 네트워크 또는 인터넷에 액세스할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-restore-missing-dns-name-server-records"></a>기록 누락 DNS 이름을 서버를 복원 하려면  
  
1.  서버에서 dnsmgmt.msc 엽니다.  
  
2.  DNS 관리자 _msdcs 영역에 대 한 앞으로 조회 영역이 마우스 클릭 한 다음 **속성**합니다.  
  
3.  에 **이름 서버** 탭을 설정이 올바른지 확인 합니다.  
  
4.  클릭 한 다음 하 고 필요한 변경을 수행 **확인** 설정을 저장 합니다.  
  
### <a name="no-dns-name-server-records"></a>이름 DNS 서버 레코드가 없습니다  
 **문제:** 레코드가 이름 DNS 서버 (NS) 리소스 위임된 _msdcs 전달 조회 영역에 대 한 합니다.  
  
 **영향을:** DNS 서버 서비스 도메인에 대 한 리소스 DNS 레코드를 확인할 수 없는 DNS 이름 (NS) 서버 리소스 레코드가 위임된 _msdcs 전달 조회 영역에 대 한 없으면 및 시작 되지 것입니다.  
  
 **해결 방법:**  
  
##### <a name="to-reconfigure-missing-dns-name-server-records"></a>누락 DNS 이름을 서버를 다시 기록  
  
1.  서버에서 dnsmgmt.msc 엽니다.  
  
2.  DNS 관리자 서버 이름을 확장 한 다음 확장 **앞 조회 영역이**합니다.  
  
3.  클릭 Active Directory 도메인에 대 한 앞으로 조회 영역이 (예: contoso.local).  
  
4.  위임된 _msdcs 영역 폴더 회색된으로 표시 됩니다. _Msdcs 영역을 마우스 오른쪽 단추로 클릭 한 다음 한 **속성**합니다.  
  
5.  에 **이름 서버** 탭을 설정이 올바른지 확인 합니다.  
  
6.  클릭 한 다음 하 고 필요한 변경을 수행 **확인** 설정을 저장 합니다.  
  
### <a name="authenticated-users-not-a-member-of-the-pre-windows-2000-compatible-access-group"></a>인증 된 사용자가 windows 2000 호환 되는 액세스 그룹의 회원 하지  
 **문제:** 인증 된 사용자 그룹 windows 2000 호환 되는 액세스 그룹 구성원이 아닙니다.  
  
 **영향을:** 네트워크 사용자에 게 "액세스 거부" 오류 발생할 수 있는 기본 제공 되는 인증 된 사용자 그룹 windows 2000 호환 되는 액세스 그룹의 회원 없는 경우입니다.  
  
 **해결 방법:**  
  
##### <a name="to-add-authenticated-users-to-the-pre-windows-2000-compatible-access-group"></a>사용자가 인증 된 windows 2000 호환 되는 액세스 그룹에 추가 하려면  
  
1.  서버에서 dsa.msc 엽니다.  
  
2.  **내장** 폴더를 마우스 오른쪽 단추로 클릭 **windows 2000 호환 되는 액세스**을 차례로 클릭 하 고 **속성**합니다.  
  
3.  클릭 **추가**, 입력 **인증 된 사용자**을 차례로 클릭 하 고 **확인** 두 번 합니다.  
  
### <a name="dns-client-not-configured"></a>DNS 클라이언트 구성 되지 않음  
 **문제:** DNS 클라이언트는 서버 내부 IP 주소 가리키도록 구성 되지 않았습니다.  
  
 **영향을:** DNS 이름 확인 DNS 클라이언트는 서버 내부 IP 주소 가리키도록 하도록 구성 되어 있지,에 실패할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-dns-to-point-only-to-the-server-s-internal-ip-address"></a>DNS 서버 s 내부 IP 주소 가리키도록 구성 하려면  
  
1.  클라이언트 컴퓨터에서 엽니다는 **속성** 페이지에서 네트워크 연결.  
  
2.  DNS 서버 내부 IP 주소 가리키도록 구성 되어 있는지 확인 합니다.  
  
### <a name="default-application-pool-value-changed"></a>기본값 풀 응용 프로그램 변경  
 **문제:** DefaultAppPool 응용 프로그램 풀 최대 작업자 프로세스 수가 1 기본값으로 설정 되지 않은 합니다.  
  
 **영향을:** 사용자가 Windows Small Business Server 웹 기반 서비스에 연결할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-reset-maximum-worker-processes-for-the-default-application-pool"></a>기본 응용 프로그램 풀 최대 작업자 프로세스를 다시 설정 하려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자 서버 이름 확장 한 다음 클릭 **응용 프로그램 풀**합니다.  
  
3.  **응용 프로그램 풀**를 마우스 오른쪽 단추로 클릭 **DefaultAppPool**을 차례로 클릭 하 고 **고급 설정**합니다.  
  
4.  **고급 설정**, 변경에 대 한 값 **최대 작업자 프로세스** 1을 클릭 한 다음 **확인**합니다.  
  
5.  닫기 **고급 설정**를 마우스 오른쪽 단추로 클릭 **DefaultAppPool**, 다음 중지 하 고 응용 프로그램 풀 다시 시작 합니다.  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-account"></a>응용 프로그램 원격 Web Access 풀의 기본 계정 사용 하지 않는  
 **문제:** RemoteAppPool 응용 프로그램 풀 기본 계정을 사용 하 여 실행 되 고 있지 합니다.  
  
 **영향을:** 네트워크 사용자에 게 원격 Web Access 웹 사이트에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-reset-the-remote-application-pool-to-use-the-default-account"></a>기본 계정을 사용 하 여 원격 응용 프로그램 풀 초기화 하려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자 서버 이름 확장 한 다음 클릭 **응용 프로그램 풀**합니다.  
  
3.  **응용 프로그램 풀**를 마우스 오른쪽 단추로 클릭 **RemoteAppPool**을 차례로 클릭 하 고 **고급 설정**합니다.  
  
4.  **고급 설정**, 변경는 **신원을** 에 **NetworkService**을 차례로 클릭 하 고 **확인**합니다.  
  
5.  닫기 **고급 설정**를 마우스 오른쪽 단추로 클릭 **RemoteAppPool**, 다음 중지 하 고 응용 프로그램 풀 다시 시작 합니다.  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-net-framework-version"></a>응용 프로그램 원격 Web Access 풀 기본.NET Framework 버전을 사용 하지 않는  
 **문제:** RemoteAppPool 응용 프로그램 풀은 Microsoft.NET Framework의 기본 버전으로 실행 되 고 있지 합니다.  
  
 **영향을:** 네트워크 사용자에 게 원격 Web Access 웹 사이트에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-net-framework-version-used-by-the-remoteapppool"></a>.NET Framework 버전은 RemoteAppPool에서 사용 하는 변경 하려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자 서버 이름 확장 한 다음 클릭 **응용 프로그램 풀**합니다.  
  
3.  **응용 프로그램 풀**를 마우스 오른쪽 단추로 클릭 **RemoteAppPool**을 차례로 클릭 하 고 **고급 설정**합니다.  
  
4.  **고급 설정**, 변경는 **.NET Framework 버전** v 4.0을 클릭 한 다음 **확인**합니다.  
  
5.  닫기 **고급 설정**를 마우스 오른쪽 단추로 클릭 **RemoteAppPool**, 다음 중지 하 고 응용 프로그램 풀 다시 시작 합니다.  
  
### <a name="the-remoteaccesslog-file-is-larger-than-1-gb-in-size"></a>RemoteAccess.log 파일은 1GB의 크기 보다 크게  
 **문제:** Remoteaccess.log 파일의 크기 1GB 넘으면 시스템 드라이브에 부족 디스크 공간 오류가 발생할 수 있습니다.  
  
 **영향을:** Remoteaccess.log 파일이 너무 많은 경우 공간이 문제가 발생할 수 있습니다: c: 드라이브 s 합니다.  
  
 **해결 방법:** 서버 백업한 후 %ProgramData%\Microsoft\Windows Server\Logs\WebApps 폴더에 있는 Remoteaccess.log 파일을 삭제할 수 있습니다.  
  
### <a name="default-web-sites-log-directory-is-over-1-gb-in-size"></a>기본 웹 사이트의 로그 디렉터리 넘는 1GB의 크기는  
 **문제:** 기본 웹 사이트의 로그 폴더의 크기 1GB 넘으면 시스템 드라이브에 부족 디스크 공간 오류가 발생할 수 있습니다.  
  
 **영향을:** 기본 웹 사이트의 로그 폴더를 너무 많은 경우 공간이 문제가 발생할 수 있습니다: c: 드라이브 s  
  
 **해결 방법:** 서버를 백업 하 고 기본 웹 사이트를 중지 하는 동안 로그 C:\inetpub\logs\LogFiles\W3SVC1 폴더의 파일을 삭제할 수 있습니다. 기본 웹 사이트를 시작 합니다.  
  
### <a name="no-binding-for-ssl-on-all-ip-addresses"></a>없음 구속력 SSL에 대 한 모든 IP 주소에서  
 **문제:** 서버에 모든 IP 주소에서 없는 구속력에 대 한 소켓 SSL (Secure Layer)는 합니다.  
  
 **영향을:** 하지 SSL 서버에 모든 IP 주소에 바인딩된, 일부 웹 사이트 됩니다 사용자에 게 사용할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-bind-ssl-to-all-ip-addresses-on-the-server"></a>SSL 서버에 모든 IP 주소에 연결 하려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서에 **연결** 창 서버를 확장 **사이트**를 마우스 오른쪽 단추로 클릭 **기본 웹 사이트**을 차례로 클릭 하 고 **바인딩 편집**합니다.  
  
3.  **사이트 바인딩**, 클릭 **추가**, 한 후 다음 설정을 선택 합니다.  
  
    -   **입력** = **https**  
  
    -   **IP 주소** = **모두 지정 되지 않음**  
  
    -   **포트** 443 =  
  
4.  SSL 인증서를 선택한 다음 **확인** 변경 내용을 저장 합니다.  
  
### <a name="no-binding-for-ssl-on-the-default-web-site"></a>기본 웹 사이트에서 ssl 구속력 없음  
 **문제:** 는 기본 웹 사이트에서 ssl 구속력 없습니다.  
  
 **영향을:** SSL 기본 웹 사이트에 바인딩된 하지, 경우 일부 웹 사이트 하지 못할 사용자에 게 합니다.  
  
 **해결 방법:**  
  
##### <a name="to-bind-ssl-to-the-default-website"></a>기본 웹 SSL과 연결할  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서에 **연결** 창 서버를 확장 **사이트**를 마우스 오른쪽 단추로 클릭 **기본 웹 사이트**을 차례로 클릭 하 고 **바인딩 편집**합니다.  
  
3.  **사이트 바인딩**, 클릭 **추가**, 다음 옵션을 선택 하 고 있습니다.  
  
    -   **입력** = **https**  
  
    -   **IP 주소** = **모두 지정 되지 않음**  
  
    -   **포트** 443 =  
  
    > [!NOTE]
    >  특정 IP 주소에 대 한 포트 443 HTTPS 구속력 있는 경우 변경는 **IP 주소** 해당 구속력에 대 한 특성 **할당 되지 않은 모든**합니다. 이에 대 한 예외 127.0.0.1 IP 주소입니다. 구속력 127.0.0.1에 대 한 변경 되지 않습니다.  
  
4.  SSL 인증서를 선택한 다음 **확인** 변경 내용을 저장 합니다.  
  
### <a name="a-certificate-expires-within-30-days"></a>30 일 내에 만료 되는 인증서  
 **문제:** 서버 인증서 30 일 내에 만료 됩니다.  
  
 **영향을:** 서버 만료 된 인증서를 사용할 수 없습니다. 인증서가 만료 사용자가 수도 있습니다 어디서 나 액세스 기능을 사용할 수 없습니다.  
  
 **해결 방법:** 인증서 만료 되지 않도록 하려면 인증서에 신뢰할 수 있는 인증 기관과 함께 갱신 됩니다.  
  
### <a name="certificate-subject-does-not-match-the-name-configured-by-domain-name-wizard"></a>인증서 주제 도메인 이름 마법사에서 구성 된 이름 일치 하지 않는  
 **문제:** 인증서 도메인 이름 마법사가 구성 되어 있던 이름과 일치 하지 않습니다.  
  
 **영향을:** 일부 웹 사이트 인증서 도메인 이름 마법사가 구성 되어 있던 이름과 일치 하지 않는 경우 초기화 하지 것입니다. 다른 사이트 오류가 표시 됩니다 "이 웹이 사이트의 보안 인증서에 문제가입니다."  
  
 **해결 방법:** 이 문제를 해결 하려면:, 설정 어디서 나 액세스 마법사를 다시 실행 하 고, 인증서에 대 한 올바른 도메인 이름이 제공 하거나 사용 하려는 도메인 이름와 일치 하는 새 인증서를 구입 합니다.  
  
### <a name="one-or-more-user-accounts-have-duplicate-cn-names"></a>하나 이상의 사용자 계정이 있는 중복 CN 이름  
 **문제:** 하나 이상의 사용자 계정이 있는 중복 CN 이름: {0} 합니다.  
  
 **영향을:** 중복 CN 이름, 사용자 계정 경우 사용자가 하지 않을 수 네트워크에 로그인 할 수 있습니다. 또한 사용자에 대 한 Active directory 검색 잘못 된 값 반환할 수 있습니다.  
  
 **해결 방법:** 이 문제를 해결 하려면:, 네트워크 사용자 계정을 중복 없는 있는지 확인 "CN =" 이름입니다. 쉽게이 검토 하기 위해 텍스트 파일로 Active Directory 내용을 내보내기 하는 것이 좋습니다. For information about how to do this, see [Using LDIFDE to import and export directory objects to Active Directory (Knowledge Base article 237677)](https://support.microsoft.com/kb/237677) (https://support.microsoft.com/kb/237677).  
  
### <a name="nt-backup-is-installed"></a>NT 백업이 설치 되어 있습니다.  
 **문제:** 서버에 Windows NT 백업 프로그램이 설치 되어 있습니다.  
  
 **영향을:** Windows Server Essentials Windows Server 백업 하는 것입니다. Windows NT 백업 프로그램도 설치 된 경우 두 가지 백업 프로그램 간에 충돌 있을 수 있습니다. 이 실패 하는 Windows Server 백업 프로세스로 인해 발생할 수 있습니다. 충돌은 백업을 복원 서버를 사용 하 여 되지 않을 수 있습니다.  
  
 **해결 방법:** 이 문제를 해결 하려면:, 서버에서 NT 백업을 프로그램을 제거 합니다.  
  
### <a name="iis-does-not-own-port-80-000080-or-port-443-0000443"></a>포트 80 (0.0.0.0:80) 또는 포트 (0.0.0.0:443) 443 IIS 소유 하지 않는  
 **문제:** 포트 80 (0.0.0.0:80) 또는 포트 443 정보 IIS (인터넷 서비스)를 소유 하지 않습니다. 현재 이러한 포트 다른 응용 프로그램 연결 되어 있습니다.  
  
 **영향을:** Windows Server Essentials 웹 응용 프로그램 포트 80 사용 해야 하 고 사용자에 게 서비스를 사용할 수 있도록 443 포트 합니다. 다른 프로세스 또는 응용 프로그램은 이미 또는 사용 하 여 포트 80 포트 443, Windows Server Essentials 웹 응용 프로그램에서 실행할 수 없습니다. 이 문제가 발생 하는 경우 원격 Web Access 및 기타 응용 프로그램은 사용자에 게 사용할 수 없습니다.  
  
 **해결 방법:** 이 문제를 해결 하려면:, 이미 포트 80 또는 포트 443 사용 하 여 또는 다른 포트 하려면 해당 응용 프로그램을 지정 응용 프로그램을 제거 하거나 합니다.  
  
### <a name="the-default-website-is-not-running"></a>기본 웹 사이트를 실행 하지  
 **문제:** 웹 사이트 기본 Windows Server Essentials 환경에서 실행 되 고 있지 합니다.  
  
 **영향을:** Windows Server Essentials 웹 응용 프로그램 기본 웹 사이트를 사용 해야 합니다. 기본 웹 사이트를 실행 하지 않는 경우 원격 Web Access 및 기타 응용 프로그램은 사용자에 게 사용할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-default-website"></a>기본 웹 사이트를 시작 하려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자 서버 이름 확장 한 다음 클릭 **사이트**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **기본 웹 사이트**를 가리킨 **관리 웹 사이트**을 차례로 클릭 하 고 **시작**합니다.  
  
### <a name="read-and-script-permissions-for-the-remote-virtual-directory-are-incorrect"></a>잘못 된 /Remote 가상 디렉터리의 읽기 및 스크립트 권한을  
 **문제:** 읽기 및 스크립트 권한을 /Remote 가상 디렉터리에 할당 되지 않습니다.  
  
 **영향을:** /Remote 가상 디렉터리의 읽기 및 스크립트 권한을 올바르지 않은 경우 사용자가 웹에 대 한 원격 액세스를 사용할 수 없습니다. 웹에 대 한 원격 액세스 인터넷 검색 사용 하려고 할 때 "403.1 HTTP 오류 금 단의." 오류가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-assign-read-and-script-permissions-to-the-remote-directory"></a>읽기 및 스크립트 권한을 /Remote 디렉터리에 할당 하려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자 서버 이름 확장 한 다음 클릭 **사이트**합니다.  
  
3.  확장 **기본 웹 사이트**를 확장 한 다음 **원격**합니다.  
  
4.  **기능 보기**를 두 번 클릭 **처리기 매핑**합니다.  
  
5.  에 **작업** 창 클릭 **기능 사용 권한을 편집**합니다.  
  
6.  선택는 **읽기** 및 **스크립트** 확인란을 선택한 다음 클릭 **확인**합니다.  
  
### <a name="http-redirect-is-either-set-or-inherited-on-the-remote-virtual-directory"></a>HTTP 이동 설정 하거나 /Remote 디렉터리에 대해 상속 합니다.  
 **문제:** HTTP 이동 특성을 예기치 않게 설정 하거나 /Remote 디렉터리에 대해 상속 합니다.  
  
 **영향을:** 원격 웹 작업 HTTP 이동 특성을 /Remote 디렉터리에 대해 설정 제대로 작동 하지 않습니다.  
  
 **해결 방법:**  
  
##### <a name="to-remove-the-http-redirect-attribute"></a>HTTP 이동 특성을 제거 하려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자 서버 이름 확장 한 다음 클릭 **사이트**합니다.  
  
3.  확장 **기본 웹 사이트**를 확장 한 다음 **원격**합니다.  
  
4.  **기능 보기**를 두 번 클릭 **HTTP 이동**합니다.  
  
5.  지우기는 **요청이이 대상을 다시** 확인란을 선택한 다음 클릭 **적용** 에 **작업** 창 합니다.  
  
### <a name="a-host-name-exists-for-port-80-on-the-default-website"></a>호스트 이름이 포트 80 기본 웹 사이트에 있습니다  
 **문제:** 기본 웹 사이트에서 포트 80 호스트 이름이 지정 됩니다.  
  
 **영향을:** 일부 Windows Server Essentials 웹 응용 프로그램에 연결할 수 호스트 이름이 포트 80 기본 웹 사이트에 할당 되어 있으면 되지 않을 수 있습니다. 호스트 필요 하지 않은 이름과 이런 경우에서 권장 하지 않음  
  
 **해결 방법:**  
  
##### <a name="to-clear-the-host-name-entry-for-port-80-on-the-default-website"></a>기본 웹 사이트에서 포트 80 호스트 이름 항목을 지우려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자 서버 이름 확장 한 다음 클릭 **사이트**합니다.  
  
3.  **기능 보기**를 마우스 오른쪽 단추로 클릭 **기본 웹 사이트**을 차례로 클릭 하 고 **바인딩을**합니다.  
  
4.  **사이트 바인딩**는 **포트 80 http** 설정과 클릭 한 다음 **편집**합니다.  
  
5.  **편집 구속력**취소는 **호스트 이름** 항목과 클릭 **확인**합니다.  
  
### <a name="backup-does-not-succeed-because-of-a-hidden-partition"></a>숨겨진된 파티션 때문 백업이 실패  
 **문제:** NTFS가 아닌 파티션 Windows Server 백업에서 백업을 예정 된 합니다.  
  
 **영향을:** Windows Server 백업만 NTFS로 포맷 되어 파티션을을 백업할 수 있습니다.  
  
 **해결 방법:** NTFS가 아닌 파티션을 백업 Windows Server 백업 구성 되어 있지 않습니다. For more information, see [Event IDs 12290 and 16387 are logged when system state backup fails on a Windows Server 2008-based computer (Knowledge Base article 968128)](https://support.microsoft.com/kb/968128) (https://support.microsoft.com/kb/968128).  
  
### <a name="the-most-recent-backup-did-not-succeed"></a>가장 최근 백업이 하지 못했습니다.  
 **문제:** 최신 백업 시도 완료 되지 않았습니다.  
  
 **영향을:** 시스템에 대 한 백업 상태 잘못 되었습니다.  
  
 **해결 방법:** 이벤트 로그 및 가장 최근 백업 하는 동안 발생 한 오류에 대 한 로그를 백업 검토 합니다.  
  
### <a name="the-startup-type-for-the-file-replication-service-is-not-set-to-automatic"></a>시작 유형 파일 복제 서비스에 대 한 자동으로 설정 되지 않은  
 **문제:** 시작 유형 자동 기본값으로 설정 되지 않은 경우 복제 FRS 파일 서비스 () 시작 되지 않을 수 있습니다.  
  
 **영향을:** 파일 복제 서비스가 실행 하지 않는 경우 도메인 컨트롤러 서비스는 광고 중단 될 수 있습니다. 그룹 정책 오류 로그온 오류와 같은 다른 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-file-replication-service-for-automatic-startup"></a>자동으로 시작 되도록 파일 복제 서비스 구성 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **파일 복제**합니다.  
  
3.  에 대 한 **시작 유형**선택 **자동**을 차례로 클릭 하 고 **적용**합니다.  
  
### <a name="the-file-replication-service-is-not-running"></a>파일 복제 서비스가 실행 되 고 있지  
 **문제:** 파일 복제 서비스가 실행 되 고 있지 합니다.  
  
 **영향을:** 파일 복제 서비스가 실행 하지 않는 경우 도메인 컨트롤러 서비스는 광고 중단 될 수 있습니다. 이 문제가 로그온 오류와 그룹 정책 오류와 같은 다른 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-file-replication-service"></a>파일 복제 서비스를 시작 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **파일 복제 서비스**합니다.  
  
3.  클릭 **시작**합니다.  
  
### <a name="the-logon-account-for-the-file-replication-service-is-not-set-to-use-the-local-system-account"></a>파일 복제 서비스에 대 한 로그온 계정은 시스템 로컬 계정을 사용 하도록 설정 하지 않은  
 **문제:** 파일 복제 서비스 기본 로그온 계정으로 시스템 로컬 계정을 사용 하도록 구성 되지 않았습니다.  
  
 **영향을:** 파일 복제 서비스에서 기본 로그온 계정으로 로컬 시스템을 사용 하지 않으면 사용 권한을 관련 된 오류가 발생할 수 있습니다. 이러한 오류 다른 오류를 트리거하 수 있으며 서비스는 광고를 중지 하는 도메인 컨트롤러 결국 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-local-system-as-the-default-logon-account-for-file-replication"></a>로컬 시스템 파일 복제에 대 한 기본 로그온 계정을 구성 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **파일 복제**합니다.  
  
3.  에 **서비스 속성** 페이지, 클릭는 **로그온** 탭 합니다.  
  
4.  선택는 **시스템 로컬 계정** 옵션을 클릭 한 다음 **적용**합니다.  
  
5.  서비스를 다시 시작 합니다.  
  
### <a name="the-startup-type-for-the-dfs-replication-service-is-not-set-to-automatic"></a>시작 유형 Dfs 서비스에 대 한 자동으로 설정 되지 않은  
 **문제:** 시작 유형 자동 기본값으로 설정 되지 않은 경우 DFS 복제 서비스 시작 되지 않을 수 있습니다.  
  
 **영향을:** DFS 복제 서비스가 실행 하지 않는 경우 도메인 컨트롤러 서비스는 광고 중단 될 수 있습니다. 그룹 정책 오류 로그온 오류와 같은 다른 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-dfs-replication-service-for-automatic-startup"></a>자동으로 시작 되도록 DFS 복제 서비스 구성 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **DFS 복제**합니다.  
  
3.  에 대 한 **시작 유형**선택 **자동**을 차례로 클릭 하 고 **적용**합니다.  
  
### <a name="the-dfs-replication-service-is-not-running"></a>DFS 복제 서비스가 실행 되지 않으면  
 **문제:** DFS 복제 서비스에서 현재 실행 되지 않습니다.  
  
 **영향을:** DFS 복제 서비스가 실행 하지 않는 경우 도메인 컨트롤러 서비스는 광고 중단 될 수 있습니다. 이 문제가 로그온 오류와 그룹 정책 오류와 같은 다른 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-dfs-replication-service"></a>Dfs 서비스를 시작 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **DFS 복제**합니다.  
  
3.  클릭 **시작**합니다.  
  
### <a name="the-dfs-replication-service-is-not-is-not-set-to-use-the-local-system-account"></a>서비스가 DFS 복제 시스템 로컬 계정을 사용 하도록 설정 되지 않은  
 **문제:** DFS 복제 서비스는 기본 로그온 계정으로 시스템 로컬 계정을 사용 하도록 설정 하지 합니다.  
  
 **영향을:** DFS 복제 서비스에서 기본 로그온 계정으로 로컬 시스템을 사용 하지 않으면 사용 권한을 관련 된 오류가 발생할 수 있습니다. 이러한 오류 다른 오류를 트리거하 수 있으며 서비스는 광고를 중지 하는 도메인 컨트롤러 결국 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-dfs-replication-to-use-local-system-as-the-default-logon-account"></a>기본 로그온 계정으로 로컬 시스템을 사용 하 여 DFS 복제 구성 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **DFS 복제**합니다.  
  
3.  에 **서비스 속성** 페이지, 클릭는 **로그온** 탭 합니다.  
  
4.  선택는 **시스템 로컬 계정** 옵션을 클릭 한 다음 **적용**합니다.  
  
5.  서비스를 다시 시작 합니다.  
  
### <a name="the-windows-server-office-365-integration-service-is-not-set-to-use-the-local-system-account"></a>Windows Server Office 365 통합 서비스 시스템 로컬 계정을 사용 하도록 설정 하지는  
 **문제:** Windows Server Office 365 통합 서비스는 기본 로그온 계정으로 시스템 로컬 계정을 사용 하도록 설정 되지 않습니다.  
  
 **영향을:** Office 365의 일부 기능을 Windows Server Office 365 통합 서비스 기본 로그온 계정으로 로컬 시스템을 사용 하지 않는 제대로 작동 하지 않을 수 있습니다. 사용 권한와 관련 된 오류가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-office-365-integration-service-to-use-local-system-as-the-default-logon-account"></a>Office 365 통합 서비스 기본 로그온 계정으로 로컬 시스템을 사용 하도록 구성 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **Windows Server Office 365 통합 서비스**합니다.  
  
3.  에 **서비스 속성** 페이지, 클릭는 **로그온** 탭 합니다.  
  
4.  선택는 **시스템 로컬 계정** 옵션을 클릭 한 다음 **적용**합니다.  
  
5.  서비스를 다시 시작 합니다.  
  
### <a name="the-windows-server-office-365-integration-service-is-not-running"></a>Windows Server Office 365 통합 서비스가 실행 되 고 있지  
 **문제:** Windows Server Office 365 통합 서비스에서 현재 실행 되지 않습니다.  
  
 **영향을:** Windows Server Office 365 통합 서비스를 실행 하지 않는 경우 Office 365 클라우드 기반 기능을 사용할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-windows-server-office-365-integration-service"></a>Windows Server Office 365 통합 서비스를 시작 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **Windows Server Office 365 통합 서비스**합니다.  
  
3.  클릭 **시작**합니다.  
  
### <a name="the-startup-type-for-the-windows-server-office-365-integration-service-is-not-set-to-automatic"></a>Windows Server Office 365 통합 서비스에 대 한 시작 유형 자동으로 설정 되지 않은  
 **문제:** 시작 유형 자동 기본값으로 설정 되지 않은 경우 Windows Server Office 365 통합 서비스 시작 되지 않을 수 있습니다.  
  
 **영향을:** Windows Server Office 365 통합 서비스를 실행 하지 않는 경우 Office 365 클라우드 기반 기능을 사용할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-office-365-integration-service-for-automatic-startup"></a>자동으로 시작 되도록 Office 365 통합 서비스 구성 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **Windows Server Office 365 통합 서비스**합니다.  
  
3.  에 대 한 **시작 유형**선택 **자동**을 차례로 클릭 하 고 **적용**합니다.  
  
### <a name="a-registry-value-is-missing-or-set-incorrectly"></a>레지스트리 값 누락 되었거나 잘못 설정  
 **문제:** HKEY_LOCAL_MACHINE \Software\Microsoft\Rpc\RpcProxy 아래 레지스트리 키 또는 잘못 된 값 존재 하지 않습니다.  
  
 **영향을:** 다음과 같은 오류 메시지가 나타날 수입니다. 레지스트리 키가 올바르게 설정 하는 경우: "컴퓨터에서 원격 데스크톱 게이트웨이의 서버 일시적으로 사용할 수 없기 때문에 원격 컴퓨터에 연결할 수 없습니다. 나중에 다시 연결 시도 하거나 네트워크 관리자에 게 문의 하세요. "  
  
 **해결 방법:**  
  
##### <a name="to-correct-the-registry-setting"></a>레지스트리 설정이 수정 하려면  
  
1.  레지스트리 편집기 열기  
  
2.  다음 레지스트리 키로 이동 합니다.  
  
     찾아  
  
3.  "웹 사이트" 이라는 문자열 기본 웹 사이트 데이터 값 있는지 확인 합니다.  
  
    -   데이터 값 올바르지 않으면 올바르지 값을 사용 하 여 문자열을 수정 합니다.  
  
    -   문자열 존재 하지 않는 경우 "웹 사이트," 라는 새 문자열 만들고 데이터 값 웹 사이트 기본 설정입니다. "  
  
### <a name="the-startup-type-for-the-block-level-backup-engine-service-is-not-set-to-manual"></a>시작 유형 차단 수준을 백업을 엔진 서비스에 대 한 설명서를 설정 되지 않은  
 **문제:** 차단 수준을 백업을 엔진 서비스 기본 시작 유형 설명서에서 사용 하지 않는 합니다.  
  
 **영향을:** 시작 유형 수동으로 설정 되지 않은 경우 차단 수준을 백업을 엔진 서비스 시작 되지 않을 수 있습니다. 이 문제: Windows Server 백업 작업이 실패 하 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-for-manual-startup"></a>수동 시작 차단 수준을 백업을 엔진 서비스 구성 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **차단 수준을 백업을 엔진 서비스**합니다.  
  
3.  에 대 한 **시작 유형**선택 **수동**을 차례로 클릭 하 고 **적용**합니다.  
  
### <a name="the-logon-account-for-the-block-level-backup-engine-service-is-not-set-to-use-the-local-system-account"></a>차단 수준을 백업을 엔진 서비스에 대 한 로그온 계정은 시스템 로컬 계정을 사용 하도록 설정 하지 않은  
 **문제:** 차단 수준을 백업을 엔진 서비스는 기본 로그온 계정으로 시스템 로컬 계정을 사용 하도록 설정 하지 합니다.  
  
 **영향을:** 차단 수준을 백업을 엔진 서비스에서 기본 로그온 계정으로 로컬 시스템을 사용 하지 않으면 사용 권한을 관련 된 오류가 발생할 수 있습니다. 이러한 오류는 Windows Server 백업 작업을 성공적으로 완료 방지할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-to-use-local-system-as-the-default-logon-account"></a>기본 로그온 계정으로 로컬 시스템을 사용 하 여 차단 수준을 백업을 엔진 서비스 구성 하려면  
  
1.  서비스 console을 엽니다.  
  
2.  두 번 클릭 서비스의 목록에서 **차단 수준을 백업을 엔진 서비스**합니다.  
  
3.  에 **서비스 속성** 페이지, 클릭는 **로그온** 탭 합니다.  
  
4.  선택는 **시스템 로컬 계정** 옵션을 클릭 한 다음 **적용**합니다.  
  
5.  서비스를 다시 시작 합니다.  
  
### <a name="the-common-name-on-the-certificate-that-is-bound-to-the-wss-certificate-web-service-website-does-not-match-the-server-name"></a>WSS 인증서 웹 서비스 웹 사이트에 연결 된 인증서 일반적인 이름이 서버 이름 일치 하지 않는  
 **문제:** 인증서 유효 하지 않은 iis에서 WSS 인증서 웹 서비스 웹 사이트에 연결 됩니다. 이 인증서에는 일반적인 이름은 서버 이름을 일치 하지 않습니다.  
  
 **영향을:** 연결 마법사 인증서 유효 하지 않은 WSS 인증서 웹 서비스 웹 사이트에 연결한 경우 제대로 작동 하지 않습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-a-valid-certificate-for-the-wss-certificate-web-service"></a>유효한 인증서 WSS 인증서 웹 서비스에 대 한 구성 하려면  
  
1.  서버에서 정보가 IIS (인터넷 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자 서버 이름 확장 한 다음 클릭 **사이트**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **WSS 인증서 웹 서비스**을 차례로 클릭 하 고 **바인딩 편집**합니다.  
  
4.  **사이트 바인딩**, 클릭 **HTTPS**을 차례로 클릭 하 고 **편집**합니다.  
  
5.  **편집 구속력**에 대 한 **SSL 인증서**, 인증서 서버 이름이 같은 선택 합니다.  
  
6.  둘 이상의 인증서 항목 서버 이름이 같은 클릭 **보기** 인증서 올바른지 확인 한 다음 해당 인증서 합니다.  
  
### <a name="there-appears-to-be-a-problem-with-the-certificate-binding-for-the-remote-desktop-gateway-service"></a>문제가 원격 데스크톱 게이트웨이의 서비스에 대 한 인증서 구속력 있는 것으로 보입니다.  
 **문제:** 원격 데스크톱 게이트웨이의 서비스에 대 한 인증서 제대로 연결 것 같습니다.  
  
 **영향을:** 사용자가 웹에 대 한 원격 액세스에 연결할 수 없는 경우 원격 데스크톱 게이트웨이의 서비스에 대 한 인증서 올바르게 구성 되지 않았습니다.  
  
 **해결 방법:**  
  
##### <a name="to-fix-the-binding-for-the-remote-desktop-gateway-service"></a>원격 데스크톱 게이트웨이의 서비스에 대 한 구속력 문제를 해결 하려면  
  
-   관리자 권한으로 명령 프롬프트를 열고 뒤 다음 명령을 입력 합니다.  
  
    ```  
    REG ADD HKLM\SYSTEM\CurrentControlSet\services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443  /v DefaultFlags /t REG_DWORD /d 1 /f  
    net stop tsgateway  
    net start tsgateway  
    ```  
  
     For more information, see [How to Manage the Remote Desktop Gateway Service in Windows Server Essentials (Knowledge Base article 2472211)](https://support.microsoft.com/kb/2472211) (https://support.microsoft.com/kb/2472211).
