---
title: Windows Server Essentials BPA(모범 사례 분석기) 도구에서 사용되는 규칙
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37e1dae7-586c-4dd7-bf83-7e14a9567c8f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5a737c777e1af25a59dc878fd0b3e99a6ee3ce24
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318808"
---
# <a name="rules-used-by-the-windows-server-essentials-best-practices-analyzer-bpa-tool"></a>Windows Server Essentials BPA(모범 사례 분석기) 도구에서 사용되는 규칙

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 문서에서는 Windows Server Essentials 모범 사례 분석기 (BPA)에서 사용 하는 규칙을 설명 합니다. BPA는 Windows Server Essentials를 실행 중인 서버를 검사 하 고 문제를 설명 하 고 문제 해결을 위한 권장 사항을 제공 하는 보고서를 제공 합니다. 권장 사항은 Windows Server Essentials에 대 한 제품 지원 조직에서 개발 됩니다.  
  
## <a name="using-the-tool"></a>도구 사용  
 마이그레이션 완료 후 대상 서버에서 BPA를 실행 하려면 windows Server 2011 Essentials, Windows Small Business Server 2011 Essentials 또는 Windows Home Server 2011에서 Windows Server Essentials로 마이그레이션하는 것이 표준 방법입니다. 설정 및 데이터. 언제든지 대시보드에서 도구를 실행할 수 있습니다.  
  
#### <a name="to-run-the--windows-server-essentials-bpa-on-the-server"></a>서버에서 Windows Server Essentials BPA를 실행 하려면  
  
1.  서버에 관리자로 로그온하고 대시보드를 엽니다.  
  
2.  대시보드에서 **장치** 탭을 클릭합니다.  
  
3.  **서버 작업** 창에서 **모범 사례 분석기**를 클릭합니다.  
  
4.  각 BPA 메시지를 검토하고 필요하면 지침에 따라 문제를 해결합니다.  
  
## <a name="rules-used-by-the-best-practices-analyzer"></a>모범 사례 분석기에서 사용되는 규칙  
  
### <a name="disable-ip-filtering"></a>IP 필터링 사용 안 함  
 **문제:** 서버에서 IP 필터링이 현재 사용 하도록 설정 되어 있습니다. IP 필터링을 사용하지 않도록 설정해야 합니다.  
  
 **영향:** IP 필터링을 사용 하는 경우 네트워크 트래픽이 차단 될 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-disable-ip-filtering"></a>IP 필터링을 사용하지 않도록 설정하려면  
  
1.  서버에서 regedit.exe를 엽니다.  
  
2.  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters로 이동합니다.  
  
3.  **EnableSecurityFilters**를 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
4.  **DWORD(32비트) 값 편집** 창에서 **값 데이터** 필드를 0으로 변경하고 **확인**을 클릭합니다.  
  
5.  변경 내용을 적용하려면 서버를 다시 시작합니다.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-set-to-start-automatically-by-default"></a>MSDTC(Distributed Transaction Coordinator) 서비스를 기본적으로 자동 시작되도록 설정해야 함  
 **문제:** MSDTC 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:** 서버를 시작할 때 MSDTC 서비스가 자동으로 시작 되지 않을 수 있습니다. 서비스를 중지하면 일부 SQL Server 또는 COM 함수가 실패할 수 있습니다. 따라서 Microsoft SQL Server 또는 COM 함수를 사용하는 애플리케이션이 제대로 작동하지 않을 수도 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-msdtc-service-to-start-automatically"></a>MSDTC 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Distributed Transaction Coordinator** 서비스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동(지연된 시작)** 으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-netlogon-service-should-be-configured-to-start-automatically-by-default"></a>Netlogon 서비스를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:** Netlogon 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:**  서버를 시작할 때 Netlogon 서비스가 자동으로 시작 되지 않을 수 있습니다. 서비스를 중지하면 서버가 사용자 및 서비스를 인증하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-netlogon-service-to-start-automatically"></a>Netlogon 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Netlogon** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-dns-client-service-should-be-configured-to-start-automatically-by-default"></a>DNS 클라이언트 서비스를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:**  DNS 클라이언트 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:**  서버를 시작할 때 DNS 클라이언트 서비스가 자동으로 시작 되지 않을 수 있습니다. 이 서비스를 중지하면 서버가 DNS 이름을 확인하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-dns-client-service-to-start-automatically"></a>DNS 클라이언트 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DNS 클라이언트** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-dns-server-service-should-be-configured-to-start-automatically-by-default"></a>DNS 서버 서비스를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:**  DNS 서버 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:**  서버를 시작할 때 DNS 서버 서비스가 자동으로 시작 되지 않을 수 있습니다. 이 서비스를 중지하면 DNS 업데이트가 발생하지 않습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-dns-server-service-to-start-automatically"></a>DNS 서버 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DNS 서버** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="active-directory-web-services-is-not-set-to-the-default-start-mode"></a>Active Directory 웹 서비스가 기본 시작 모드로 설정되어 있지 않음  
 **문제:**  Active Directory 웹 서비스는 기본 시작 모드인 자동으로 설정 되지 않습니다.  
  
 **영향:**  ADWS (Active Directory 웹 서비스)가 기본 시작 모드인 자동으로 설정 되어 있지 않습니다. 서버에서 ADWS를 중지하거나 사용하지 않도록 설정하면 Windows PowerShell용 Active Directory 모듈 또는 Active Directory 관리 센터와 같은 클라이언트 애플리케이션이 이 서버에서 실행 중인 디렉터리 서비스 인스턴스에 액세스하거나 관리할 수 없습니다. 자세한 내용은 Windows Server 기술 라이브러리의 [AD DS: Active Directory 웹 서비스](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx)의 새로운 기능을 참조 하십시오.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-active-directory-web-services-service-to-start-automatically"></a>Active Directory 웹 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Active Directory 웹 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-dhcp-client-service-should-be-configured-to-start-automatically-by-default"></a>DHCP 클라이언트 서비스를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:**  DHCP 클라이언트 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:**  서버를 시작할 때 DHCP 클라이언트 서비스가 자동으로 시작 되지 않습니다. 이 서비스를 중지하면 클라이언트 컴퓨터가 서버로부터 IP 주소를 받을 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-dhcp-client-service-to-start-automatically"></a>DHCP 클라이언트 서비스가 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DHCP 클라이언트** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-iis-admin-service-should-be-configured-to-start-automatically-by-default"></a>IIS Admin Service를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:** IIS Admin Service가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:** 서버를 시작할 때 IIS Admin Service가 자동으로 시작 되지 않습니다. 이 서비스를 중지하면 원격 웹 액세스와 같은 서버에서 실행 중인 웹 사이트에 액세스하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-iis-admin-service-to-start-automatically"></a>IIS Admin Service를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **IIS Admin Service**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-world-wide-web-publishing-service-should-be-configured-to-start-automatically-by-default"></a>World Wide Web Publishing 서비스를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:**  World Wide Web Publishing 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:**  서버를 시작할 때 World Wide Web 게시 서비스가 자동으로 시작 되지 않을 수 있습니다. 이 서비스를 중지하면 원격 웹 액세스와 같은 서버에서 실행 중인 웹 사이트에 액세스하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-world-wide-web-publishing-service-to-start-automatically"></a>World Wide Web Publishing 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **World Wide Web Publishing 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-remote-registry-service-should-be-configured-to-start-automatically-by-default"></a>원격 레지스트리 서비스를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:**  원격 레지스트리 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:** :  
  
 서버를 시작할 때 원격 레지스트리 서비스가 자동으로 시작되지 않을 수 있습니다. 이 서비스를 중지하면 일부 네트워크 작업을 원격으로 수행하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-remote-registry-service-to-start-automatically"></a>원격 레지스트리 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **원격 레지스트리** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-remote-desktop-gateway-service-should-be-configured-to-start-automatically-by-default"></a>원격 데스크톱 게이트웨이 서비스를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:**  원격 데스크톱 게이트웨이 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:**  이 서비스가 중지 되 면 사용자가 원격 웹 액세스를 사용 하 여 컴퓨터에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-remote-desktop-gateway-service-to-start-automatically"></a>원격 데스크톱 게이트웨이 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **원격 데스크톱 게이트웨이** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동(지연된 시작)** 으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-windows-time-service-should-be-configured-to-start-automatically-by-default"></a>Windows 시간 서비스를 기본적으로 자동 시작되도록 구성해야 함  
 **문제:**  Windows 시간 서비스가 자동으로 시작 되도록 구성 되어 있지 않습니다.  
  
 **영향:**  이 서비스를 중지 하면 데이터 및 시간 동기화를 사용할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-windows-time-service-to-start-automatically"></a>Windows 시간 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Windows 시간** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 탭에서 **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-should-be-started"></a>MSDTC(Distributed Transaction Coordinator) 서비스를 시작해야 함  
 **문제:**  서버에서 MSDTC 서비스가 실행 되 고 있지 않습니다.  
  
 **영향:**  이 서비스가 중지 되 면 일부 SQL Server 또는 COM 함수가 실패할 수 있습니다. 따라서 Microsoft SQL Server 또는 COM 함수를 사용하는 애플리케이션이 제대로 작동하지 않을 수도 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-distributed-transaction-coordinator-service"></a>Distributed Transaction Coordinator 서비스를 시작하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Distributed Transaction Coordinator** 서비스를 마우스 오른쪽 단추로 클릭하고 **시작**을 클릭합니다.  
  
### <a name="the-netlogon-service-should-be-started"></a>Netlogon 서비스를 시작해야 함  
 **문제:**  서버에서 Netlogon 서비스가 실행 되 고 있지 않습니다.  
  
 **영향:**  이 서비스가 시작 되지 않은 경우 서버에서 사용자 및 서비스를 인증 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-netlogon-service"></a>Netlogon 서비스를 시작하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Netlogon** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="the-dns-client-service-should-be-started"></a>DNS 클라이언트 서비스를 시작해야 함  
 **문제:**  서버에서 DNS 클라이언트 서비스가 실행 되 고 있지 않습니다.  
  
 **영향:**  이 서비스가 시작 되지 않은 경우 서버에서 DNS 이름을 확인 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-dns-client-service"></a>DNS 클라이언트 서비스를 시작하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DNS 클라이언트** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="the-dns-server-service-should-be-started"></a>DNS 서버 서비스를 시작해야 함  
 **문제:**  서버에서 DNS 서버 서비스가 실행 되 고 있지 않습니다.  
  
 **영향:**  DNS 서버 서비스가 시작 되지 않으면 DNS 업데이트가 발생 하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-dns-server-service"></a>DNS 서버 서비스를 시작하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DNS 서버** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="active-directory-web-services-is-not-started"></a>Active Directory 웹 서비스를 시작하지 않음  
 **문제:**  Active Directory 웹 서비스가 시작 되지 않았습니다.  
  
 **영향:**  ADWS (Active Directory 웹 서비스)가 시작 되지 않았습니다. 서버에서 ADWS를 중지하거나 사용하지 않도록 설정하면 Windows PowerShell용 Active Directory 모듈 또는 Active Directory 관리 센터와 같은 클라이언트 애플리케이션이 이 서버에서 실행 중인 디렉터리 서비스 인스턴스에 액세스하거나 관리할 수 없습니다. 자세한 내용은 Windows Server 기술 라이브러리의 [AD DS: Active Directory 웹 서비스](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx)의 새로운 기능을 참조 하십시오.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-active-directory-web-services-service"></a>Active Directory 웹 서비스를 시작하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Active Directory 웹 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="the-dhcp-client-service-should-be-started"></a>DHCP 클라이언트 서비스를 시작해야 함  
 **문제:**  서버에서 DHCP 클라이언트 서비스가 실행 되 고 있지 않습니다.  
  
 **영향:**  이 서비스가 중지 되 면 클라이언트 컴퓨터가 서버에서 IP 주소를 받을 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-dhcp-client-service"></a>DHCP 클라이언트 서비스를 시작하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DHCP 클라이언트** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="the-iis-admin-service-should-be-started"></a>IIS Admin Service를 시작해야 함  
 **문제:**  서버에서 IIS Admin Service가 실행 되 고 있지 않습니다.  
  
 **영향:**  이 서비스가 중지 되 면 원격 웹 액세스 같은 서버에서 실행 중인 웹 사이트에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-iis-admin-service"></a>IIS Admin Service를 시작하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **IIS Admin Service**를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="the-world-wide-web-publishing-service-should-be-started"></a>World Wide Web Publishing 서비스를 시작해야 함  
 **문제:**  World Wide Web Publishing 서비스가 서버에서 실행 되 고 있지 않습니다.  
  
 **영향:**  이 서비스가 중지 되 면 원격 웹 액세스 같은 서버에서 실행 중인 웹 사이트에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-world-wide-web-publishing-service"></a>World Wide Web Publishing 서비스를 시작하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **World Wide Web Publishing 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="the-remote-desktop-gateway-service-should-be-started"></a>원격 데스크톱 게이트웨이 서비스를 시작해야 함  
 **문제:**  원격 데스크톱 게이트웨이 서비스가 서버에서 실행 되 고 있지 않습니다.  
  
 **영향:**  이 서비스가 중지 되 면 사용자가 원격 웹 액세스를 사용 하 여 컴퓨터에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-remote-desktop-gateway-service"></a>원격 데스크톱 게이트웨이 서비스를 시작 하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **원격 데스크톱 게이트웨이** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="the-windows-time-service-should-be-started"></a>Windows 시간 서비스를 시작해야 함  
 **문제:**  서버에서 Windows 시간 서비스가 실행 되 고 있지 않습니다.  
  
 **영향:**  이 서비스를 중지 하면 데이터 및 시간 동기화를 사용할 수 없게 됩니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-windows-time-service"></a>Windows 시간 서비스를 시작 하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Windows 시간** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.  
  
### <a name="the-distributed-transaction-coordinator-msdtc-service-logon-account-should-be-nt-authoritynetwork-service"></a>MSDTC(Distributed Transaction Coordinator) 서비스 로그온 계정은 NT AUTHORITY\Network Service여야 함  
 **문제:**  MSDTC (DTC(Distributed Transaction Coordinator)) 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동 하는 데 필요한 권한이 없을 수 있습니다. 따라서 SQL Server 또는 COM 함수를 사용 하는 응용 프로그램이 제대로 작동 하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-logon-account-for-the-service"></a>서비스에 대한 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Distributed Transaction Coordinator** 서비스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **계정 지정**을 선택하고 **NT AUTHORITY\Network Service**를 입력한 다음 **확인**을 클릭합니다.  
  
### <a name="the-netlogon-service-should-use-the-local-system-account-as-its-logon-account"></a>Netlogon 서비스는 로컬 시스템 계정을 로그온 계정으로 사용해야 함  
 **문제:**  Netlogon 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동 하는 데 필요한 권한이 없을 수 있습니다. 따라서 서버가 사용자 및 서비스를 인증하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-netlogon-service-logon-account"></a>Netlogon 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Netlogon** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **로컬 시스템 계정**을 선택합니다.  
  
### <a name="the-dns-client-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>DNS 클라이언트 서비스는 NT AUTHORITY\Network Service 계정을 로그온 계정으로 사용해야 함  
 **문제:**  DNS 클라이언트 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동 하는 데 필요한 권한이 없을 수 있습니다. 따라서 서버가 DNS 이름을 확인하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-dns-client-service-logon-account"></a>DNS 클라이언트 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DNS 클라이언트** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **계정 지정**을 선택하고 **NT AUTHORITY\Network Service**를 입력합니다.  
  
### <a name="the-dns-server-service-should-use-the-local-system-account-as-its-logon-account"></a>DNS 서버 서비스는 로컬 시스템 계정을 로그온 계정으로 사용 해야 합니다.  
 **문제:**  DNS 서버 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동 하는 데 필요한 권한이 없을 수 있습니다. 따라서 DNS 업데이트가 발생하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-dns-server-service-logon-account"></a>DNS 서버 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DNS 서버** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **로컬 시스템 계정**을 선택합니다.  
  
### <a name="active-directory-web-services-is-not-the-default-logon-account"></a>Active Directory 웹 서비스가 기본 로그온 계정이 아님  
 **문제:**  Active Directory 웹 서비스는 기본 로그온 계정이 아닙니다. 기본적으로 로그온 계정은 **로컬 시스템 계정**으로 설정됩니다.  
  
 **영향:**  ADWS (Active Directory 웹 서비스)가 시작 되지 않았습니다. 서버에서 ADWS를 중지하거나 사용하지 않도록 설정하면 Windows PowerShell용 Active Directory 모듈 또는 Active Directory 관리 센터와 같은 클라이언트 애플리케이션이 이 서버에서 실행 중인 디렉터리 서비스 인스턴스에 액세스하거나 관리할 수 없습니다. 자세한 내용은 Windows Server 기술 라이브러리의 [AD DS: Active Directory 웹 서비스](https://technet.microsoft.com/library/dd391908\(WS.10\).aspx) (https://technet.microsoft.com/library/dd391908(WS.10).aspx)의 새로운 기능을 참조 하십시오.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-active-directory-web-services-logon-account"></a>Active Directory 웹 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Active Directory 웹 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **시작 유형**을 **자동**으로 변경하고 **확인**을 클릭합니다.  
  
4.  Active Directory 웹 서비스 **속성**에서 **로그온** 탭을 클릭합니다.  
  
5.  **로컬 시스템 계정** 옵션을 선택하고 **확인**을 클릭합니다.  
  
### <a name="the-windows-update-service-should-use-the-local-system-account-as-its-logon-account"></a>Windows 업데이트 서비스는 로컬 시스템 계정을 로그온 계정으로 사용해야 함  
 **문제:**  자동 업데이트 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동 하는 데 필요한 권한이 없을 수 있습니다. 따라서 서버가 자동 업데이트를 받지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-windows-update-service-logon-account"></a>Windows 업데이트 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Windows 업데이트** 서비스를 마우스 오른쪽 단추로 클릭한 다음 속성을 클릭합니다.  
  
3.  **로그온** 탭에서 **로컬 시스템 계정**을 선택합니다.  
  
### <a name="the-dhcp-client-service-should-use-the-nt-authoritylocalservice-account-as-its-logon-account"></a>DHCP 클라이언트 서비스는 NT AUTHORITY\LocalService 계정을 로그온 계정으로 사용해야 함  
 **문제:**  DHCP 클라이언트 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동 하는 데 필요한 권한이 없을 수 있습니다. 따라서 클라이언트 컴퓨터가 서버로부터 IP 주소를 받지 못합니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-dhcp-client-service-logon-account"></a>DHCP 클라이언트 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **DHCP 클라이언트** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **계정 지정**을 선택하고 **NT AUTHORITY\Local Service**를 입력합니다.  
  
### <a name="the-iis-admin-service-should-use-the-local-system-account-as-its-logon-account"></a>IIS Admin Service는 로컬 시스템 계정을 로그온 계정으로 사용해야 함  
 **문제:**  IIS 관리 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동 하는 데 필요한 권한이 없을 수 있습니다. 따라서 원격 웹 액세스와 같은 서버에서 실행 중인 웹 사이트에 액세스하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-service-logon-account"></a>서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **IIS Admin Service**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **로컬 시스템 계정**을 선택합니다.  
  
### <a name="the-world-wide-web-publishing-service-should-use-the-local-system-account-as-its-logon-account"></a>World Wide Web Publishing 서비스는 로컬 시스템 계정을 로그온 계정으로 사용해야 함  
 **문제:**  World Wide Web Publishing 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동 하는 데 필요한 권한이 없을 수 있습니다. 따라서 원격 웹 액세스와 같은 서버에서 실행 중인 웹 사이트에 액세스하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-world-wide-web-publishing-service-logon-account"></a>World Wide Web Publishing 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **World Wide Web Publishing 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **로컬 시스템 계정**을 선택합니다.  
  
### <a name="the-remote-desktop-gateway-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>원격 데스크톱 게이트웨이 서비스는 NT AUTHORITY\Network Service 계정을 로그온 계정으로 사용해야 함  
 **문제:**  원격 데스크톱 게이트웨이 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동할 수 있는 적절 한 권한이 없을 수 있습니다. 따라서 사용자가 원격 웹 액세스를 사용하여 컴퓨터에 액세스하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-remote-desktop-gateway-service-logon-account"></a>원격 데스크톱 게이트웨이 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **원격 데스크톱 게이트웨이** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **계정 지정**을 선택하고 **NT AUTHORITY\Network Service**를 입력합니다.  
  
### <a name="the-windows-time-service-should-use-the-nt-authoritynetwork-service-account-as-its-logon-account"></a>Windows 시간 서비스는 NT AUTHORITY\Network Service 계정을 로그온 계정으로 사용해야 함  
 **문제:**  Windows 시간 서비스에 대 한 기본 로그온 계정이 변경 되었습니다.  
  
 **영향:**  서비스에 예상 대로 작동할 수 있는 적절 한 권한이 없을 수 있습니다. 따라서 날짜 및 시간 동기화를 사용하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-windows-time-service-logon-account"></a>Windows 시간 서비스 로그온 계정을 변경하려면  
  
1.  서버에서 services.msc를 엽니다.  
  
2.  **Windows 시간** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **로그온** 탭에서 **계정 지정**을 선택하고 **NT AUTHORITY\Local Service**를 입력합니다.  
  
### <a name="the-built-in-administrators-group-does-not-have-the-right-to-log-on-as-batch-job"></a>기본 제공 Administrators 그룹에 일괄 작업으로 로그온할 수 있는 권한이 없음  
 **문제:**  기본 제공 Administrators 그룹에 일괄 작업으로 로그온 할 수 있는 권한이 없습니다.  
  
 **영향:**  관리자가 경고를 생성 하 고 관리자가 로그온 하지 않을 때 실행 되도록 경고를 구성 하는 경우 오류 코드 2147943785이 발생 하 고 경고가 실패 합니다.  
  
 **해결 방법:**  기본 제공 Administrators 그룹에 일괄 작업으로 로그온 할 수 있는 권한을 부여 하는 방법에 대 한 자세한 내용은 [기본 제공 관리자 그룹에 일괄 작업](https://technet.microsoft.com/library/jj635076) 으로 로그온 권한을 부여 하는 방법 (https://technet.microsoft.com/library/jj635076)을 참조 하세요.  
  
### <a name="the-windows-firewall-is-turned-off"></a>Windows 방화벽이 꺼져 있음  
 **문제:**  Windows 방화벽이 꺼져 있습니다. 기본값은 켜기입니다.  
  
 **영향:**  방화벽 설정에 따라 Windows 방화벽은 일부 정보가 서버를 통과 하지 못하도록 차단 하 여 악의적인 활동 으로부터 서버와 네트워크를 보호 하는 데 도움이 될 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-turn-on-windows-firewall-on-the-server"></a>서버에서 Windows 방화벽을 켜려면  
  
1.  서버에서 제어판을 엽니다.  
  
2.  제어판에서 **시스템 및 보안**을 클릭한 다음 **Windows 방화벽**을 클릭합니다.  
  
3.  Windows 방화벽에서 **Windows 방화벽 켜기/끄기**를 클릭하고 **Windows 방화벽 사용** 옵션을 선택한 다음 **확인**을 클릭합니다.  
  
### <a name="the-internal-network-adapter-is-not-configured-to-register-ip-address-in-dns"></a>내부 네트워크 어댑터가 DNS에 IP 주소를 등록하도록 구성되어 있지 않음  
 **문제:**  내부 네트워크 어댑터가 DNS에 IP 주소를 등록 하도록 구성 되어 있지 않습니다.  
  
 **영향:**  내부 네트워크 어댑터의 IP 주소가 DNS에 등록 되어 있지 않은 경우 서버 컴퓨터 이름을 사용 하 여 서버에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  내부 네트워크 어댑터가 DNS에 등록 하도록 구성 되어 있는지 확인 합니다.  
  
### <a name="dns-the-values-for-the-dns-forwardingtimeout-and-recursiontimeout-registry-key-are-identical"></a>DNS: DNS ForwardingTimeout 및 RecursionTimeout 레지스트리 키의 값이 동일 합니다.  
 **문제:**  DNS ForwardingTimeout 레지스트리 키의 값은 RecursionTimeout 레지스트리 키의 값과 같을 수 없습니다.  
  
 **영향:**  이름으로 인터넷 리소스에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  RecursionTimeout 레지스트리 키의 값을 ForwardingTimeout 키의 값 보다 크게 설정 합니다 .이 키의 값은 레지스트리에 있는 HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\DNS\Parameters.에 있습니다.  
  
### <a name="the-forward-dns-zone-for-your-active-directory-domain-does-not-allow-secure-updates"></a>Active Directory 도메인에 대한 정방향 DNS 영역이 보안 업데이트를 허용하지 않음  
 **문제:**  보안 동적 업데이트만 허용 하도록 전방 조회 영역을 구성 해야 합니다.  
  
 **영향:**  보안 동적 업데이트를 사용 하도록 설정 하면 권한이 있는 사용자와 호스트만 레코드를 변경할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-forward-lookup-zone-for-your-active-directory-domain"></a>Active Directory 도메인에 대한 정방향 조회 영역을 구성하려면  
  
1.  서버에서 dnsmgmt.msc를 엽니다.  
  
2.  Active Directory 도메인에 대한 정방향 조회 영역을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **동적 업데이트** 드롭다운 목록에서 **보안된 항목만**을 선택하고 **확인**을 클릭합니다.  
  
### <a name="the-forward-dns-zone-does-not-allow-secure-updates"></a>정방향 DNS 영역이 보안 업데이트를 허용하지 않음  
 **문제:**  보안 동적 업데이트만 허용 하도록 _msdcs. * 영역에 대 한 전방 조회 영역을 구성 해야 합니다.  
  
 **영향:**  보안 동적 업데이트를 사용 하도록 설정 하면 권한이 있는 사용자와 호스트만 msdcs. * 영역의 레코드를 변경할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-allow-secure-updates-in-the-_msdcs-zone"></a>_msdcs 영역에서 보안 업데이트를 허용하려면  
  
1.  서버에서 dnsmgmt.msc를 엽니다.  
  
2.  _msdcs 영역에 대한 정방향 조회 영역을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **동적 업데이트** 드롭다운 목록에서 **보안된 항목만**을 선택하고 **확인**을 클릭합니다.  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer 보안 강화 구성이 사용되지 않음  
 **문제:**  Internet Explorer IE ESC (보안 강화 구성)는 현재 Administrators 그룹에 대해 사용 하도록 설정 되어 있지 않습니다.  
  
 **영향:**  관리자 그룹에 대해 Internet Explorer 보안 강화 구성이 사용 하도록 설정 되어 있지 않은 경우 웹 콘텐츠 및 응용 프로그램 스크립트를 통해 발생할 수 있는 악의적인 공격에 대 한 서버 및 Internet Explorer의 노출이 증가 합니다.  
  
 **해결 방법:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer 보안 강화 구성을 사용하도록 설정하려면  
  
1.  서버에서 **서버 관리자**를 열고 **로컬 서버**를 클릭합니다.  
  
2.  **속성** 창에서 **IE 보안 강화 구성**에 대한 설정을 **켜기**로 변경하고 **확인**을 클릭합니다.  
  
### <a name="internet-explorer-enhanced-security-configuration-is-not-enabled"></a>Internet Explorer 보안 강화 구성이 사용되지 않음  
 **문제:**  현재 IE ESC (Internet Explorer 보안 강화 구성)는 사용자 그룹에 대해 사용 하도록 설정 되어 있지 않습니다.  
  
 **영향:**  사용자 그룹에 대해 Internet Explorer 보안 강화 구성을 사용 하도록 설정 하지 않은 경우에는 웹 콘텐츠 및 응용 프로그램 스크립트를 통해 발생할 수 있는 악의적인 공격에 대 한 서버 및 Internet Explorer의 노출이 증가 합니다.  
  
 **해결 방법:**  
  
##### <a name="to-enable-internet-explorer-enhanced-security-configuration"></a>Internet Explorer 보안 강화 구성을 사용하도록 설정하려면  
  
1.  **서버 관리자**를 열고 **로컬 서버**를 클릭합니다.  
  
2.  **속성** 창에서 **IE 보안 강화 구성**에 대한 설정을 **켜기**로 변경하고 **확인**을 클릭합니다.  
  
### <a name="the-source-server-remains-in-active-directory-sites-and-services"></a>원본 서버가 Active Directory 사이트 및 서비스에 남아 있음  
 **문제:**  Windows Small Business Server를 실행 하는 원본 서버는 Active Directory 사이트와 서비스에 여전히 있습니다. 기본-사이트 이름입니다.  
  
 **영향:**  원본 서버가 Active Director 사이트 및 서비스에 남아 있으면 클라이언트 컴퓨터에서 연결 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  원본 서버의 수준을 내리고 도메인에서 제거한 후 Active Directory 사이트 및 서비스에서 원본 서버를 삭제 하 고 사용자 및 컴퓨터를 Active Directory 해야 합니다.  
  
### <a name="source-server-remains-in-sbscomputer-ou"></a>원본 서버가 SBSComputer OU에 남아 있음  
 **문제:**  Windows Small Business Server를 실행 하는 원본 서버가 Active Directory 사용자 및 컴퓨터에 여전히 있습니다.  
  
 **영향:**  원본 서버가 Active Director 사용자 및 컴퓨터에 남아 있으면 클라이언트 컴퓨터에서 연결 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  원본 서버의 수준을 내리고 도메인에서 제거한 후 Active Directory 사이트 및 서비스에서 원본 서버를 삭제 하 고 사용자 및 컴퓨터를 Active Directory 해야 합니다.  
  
### <a name="a-group-policy-is-missing"></a>그룹 정책이 없음  
 **문제:**  기본 도메인 정책 그룹 정책이 없습니다.  
  
 **영향:**  적절 한 도메인 기능을 위해서는 기본 도메인 정책이 필요 합니다.  
  
 **해결 방법:**  
  
##### <a name="to-restore-a-missing-group-policy"></a>누락된 그룹 정책을 복원하려면  
  
1.  서버에서 gpmc.msc를 엽니다.  
  
2.  그룹 정책 관리자에서 도메인 포리스트를 확장하고 콘솔 트리에서 **기본 도메인 정책** 그룹 정책 개체를 검색합니다.  
  
3.  정책이 트리에 표시되지 않는 경우 시스템 상태 백업에서 복원합니다.  
  
### <a name="no-dns-name-server-resource-records"></a>DNS 이름 서버 리소스 레코드가 없음  
 **문제:**  서버에 대 한 전방 조회 영역에 DNS NS (이름 서버) 리소스 레코드가 없습니다.  
  
 **영향:**  Active Directory 도메인의 전방 조회 영역에 DNS NS (이름 서버) 리소스 레코드가 없는 경우 사용자가 네트워크 또는 인터넷의 리소스에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-restore-missing-dns-name-server-resource-records"></a>누락된 DNS 이름 서버 리소스 레코드를 복원하려면  
  
1.  서버에서 dnsmgmt.msc를 엽니다.  
  
2.  DNS 관리자에서 Active Directory 도메인에 대한 정방향 조회 영역을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **이름 서버** 탭에서 설정이 올바른지 확인합니다.  
  
4.  필요에 따라 설정을 변경하고 **확인**을 클릭하여 설정을 저장합니다.  
  
### <a name="no-dns-name-server-records"></a>DNS 이름 서버 레코드가 없음  
 **문제:**  서버에 대 한 _msdcs 영역에 DNS NS (이름 서버) 리소스 레코드가 없습니다 (예: _msdcs. contoso.com).  
  
 **영향:**  Active Directory 도메인의 _msdcs 영역에 DNS NS (이름 서버) 리소스 레코드가 없는 경우 사용자가 네트워크 또는 인터넷의 리소스에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-restore-missing-dns-name-server-records"></a>누락된 DNS 이름 서버 레코드를 복원하려면  
  
1.  서버에서 dnsmgmt.msc를 엽니다.  
  
2.  DNS 관리자에서 _msdcs 영역에 대한 정방향 조회 영역을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **이름 서버** 탭에서 설정이 올바른지 확인합니다.  
  
4.  필요에 따라 설정을 변경하고 **확인**을 클릭하여 설정을 저장합니다.  
  
### <a name="no-dns-name-server-records"></a>DNS 이름 서버 레코드가 없음  
 **문제:**  위임 된 _msdcs 전방 조회 영역에 대 한 DNS NS (이름 서버) 리소스 레코드가 없습니다.  
  
 **영향:**  위임 된 _msdcs 전방 조회 영역에 대 한 DNS NS (이름 서버) 리소스 레코드가 없는 경우 DNS 서버 서비스는 도메인에 대 한 DNS 리소스 레코드를 확인할 수 없으며 시작 하지 못합니다.  
  
 **해결 방법:**  
  
##### <a name="to-reconfigure-missing-dns-name-server-records"></a>누락된 DNS 이름 서버 레코드를 구성하려면  
  
1.  서버에서 dnsmgmt.msc를 엽니다.  
  
2.  DNS 관리자에서 서버 이름을 확장하고 **정방향 조회 영역**을 확장합니다.  
  
3.  Active Directory 도메인에 대한 정방향 조회 영역(예: : contoso.local)을 클릭합니다.  
  
4.  위임된 _msdcs 영역이 회색 폴더로 나타납니다. _msdcs 영역을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **이름 서버** 탭에서 설정이 올바른지 확인합니다.  
  
6.  필요에 따라 설정을 변경하고 **확인**을 클릭하여 설정을 저장합니다.  
  
### <a name="authenticated-users-not-a-member-of-the-pre-windows-2000-compatible-access-group"></a>Authenticated Users가 Pre-Windows 2000 Compatible Access 그룹의 구성원이 아님  
 **문제:**  Authenticated Users 그룹이 Windows 이전 2000 호환 액세스 그룹의 구성원이 아닙니다.  
  
 **영향:**  기본 제공 인증 된 사용자 그룹이 Windows 이전 2000 호환 액세스 그룹의 멤버가 아닌 경우 네트워크 사용자는 "액세스가 거부 되었습니다." 오류가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-add-authenticated-users-to-the-pre-windows-2000-compatible-access-group"></a>Pre-Windows 2000 Compatible Access 그룹에 Authenticated Users를 추가하려면  
  
1.  서버에서 dsa.msc를 엽니다.  
  
2.  **Builtin** 폴더에서 **Pre-Windows 2000 Compatible Access**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **추가**를 클릭하고 **Authenticated Users**를 입력한 다음 **확인**을 두 번 클릭합니다.  
  
### <a name="dns-client-not-configured"></a>DNS 클라이언트가 구성되어 있지 않음  
 **문제:**  DNS 클라이언트가 서버의 내부 IP 주소만 가리키도록 구성 되어 있지 않습니다.  
  
 **영향:**  DNS 클라이언트가 서버의 내부 IP 주소만 가리키도록 구성 되지 않은 경우 DNS 이름 확인이 실패할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-dns-to-point-only-to-the-server-s-internal-ip-address"></a>서버 내부 IP 주소만 가리키도록 DNS를 구성 하려면  
  
1.  클라이언트 컴퓨터에서 네트워크 연결에 대한 **속성** 페이지를 엽니다.  
  
2.  DNS가 서버의 내부 IP 주소만 가리키도록 구성되어 있는지 확인합니다.  
  
### <a name="default-application-pool-value-changed"></a>기본 응용 프로그램 풀 값이 변경됨  
 **문제:**  DefaultAppPool 응용 프로그램 풀에 대 한 최대 작업자 프로세스 수가 기본값 1로 설정 되어 있지 않습니다.  
  
 **영향:**  사용자가 Windows Small Business Server 웹 기반 서비스에 연결 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-reset-maximum-worker-processes-for-the-default-application-pool"></a>기본 애플리케이션 풀에 대한 최대 작업자 프로세스를 다시 설정하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서 서버 이름을 확장하고 **응용 프로그램 풀**을 클릭합니다.  
  
3.  **응용 프로그램 풀**에서 **DefaultAppPool**을 마우스 오른쪽 단추로 클릭한 다음 **고급 설정**을 클릭합니다.  
  
4.  **고급 설정**에서 **최대 작업자 프로세스**의 값을 1로 변경하고 **확인**을 클릭합니다.  
  
5.  **고급 설정**을 닫고 **DefaultAppPool**을 마우스 오른쪽 단추로 클릭한 다음 응용 프로그램 풀을 중지했다가 다시 시작합니다.  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-account"></a>원격 웹 액세스에 대한 응용 프로그램 풀이 기본 계정을 사용하지 않음  
 **문제:**  RemoteAppPool 응용 프로그램 풀이 기본 계정을 사용 하 여 실행 되 고 있지 않습니다.  
  
 **영향:**  네트워크 사용자가 원격 웹 액세스 웹 사이트에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-reset-the-remote-application-pool-to-use-the-default-account"></a>기본 계정을 사용하도록 원격 애플리케이션 풀을 다시 설정하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서 서버 이름을 확장하고 **응용 프로그램 풀**을 클릭합니다.  
  
3.  **응용 프로그램 풀**에서 **RemoteAppPool**을 마우스 오른쪽 단추로 클릭한 다음 **고급 설정**을 클릭합니다.  
  
4.  **고급 설정**에서 **ID**를 **NetworkService**로 변경하고 **확인**을 클릭합니다.  
  
5.  **고급 설정**을 닫고 **RemoteAppPool**을 마우스 오른쪽 단추로 클릭한 다음 응용 프로그램 풀을 중지했다가 다시 시작합니다.  
  
### <a name="application-pool-for-remote-web-access-does-not-use-the-default-net-framework-version"></a>원격 웹 액세스에 대한 응용 프로그램 풀이 기본 .NET Framework 버전을 사용하지 않음  
 **문제:**  RemoteAppPool 응용 프로그램 풀이 기본 버전의 Microsoft .NET Framework에서 실행 되 고 있지 않습니다.  
  
 **영향:**  네트워크 사용자가 원격 웹 액세스 웹 사이트에 액세스 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-change-the-net-framework-version-used-by-the-remoteapppool"></a>RemoteAppPool에서 사용되는 .NET Framework 버전을 변경하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서 서버 이름을 확장하고 **응용 프로그램 풀**을 클릭합니다.  
  
3.  **응용 프로그램 풀**에서 **RemoteAppPool**을 마우스 오른쪽 단추로 클릭한 다음 **고급 설정**을 클릭합니다.  
  
4.  **고급 설정**에서 **.NET Framework 버전**을 v4.0으로 변경하고 **확인**을 클릭합니다.  
  
5.  **고급 설정**을 닫고 **RemoteAppPool**을 마우스 오른쪽 단추로 클릭한 다음 응용 프로그램 풀을 중지했다가 다시 시작합니다.  
  
### <a name="the-remoteaccesslog-file-is-larger-than-1-gb-in-size"></a>RemoteAccess.log 파일의 크기가 1GB보다 큼  
 **문제:**  액세스 로그 파일의 크기가 1gb를 초과 하면 시스템 드라이브에서 디스크 공간 부족 오류가 발생할 수 있습니다.  
  
 **영향:**  원격 액세스 로그 파일이 너무 크면 사용 가능한 공간 문제가 발생할 수 있습니다. c:  
  
 **해결 방법:**  서버를 백업한 후%ProgramData%\Microsoft\Windows Server\Logs\WebApps 폴더에 있는 Remoteaccess 파일을 삭제할 수 있습니다.  
  
### <a name="default-web-sites-log-directory-is-over-1-gb-in-size"></a>기본 웹 사이트의 로그 디렉터리 크기가 1GB를 초과함  
 **문제:**  기본 웹 사이트의 로그 폴더 크기가 1gb를 초과 하면 시스템 드라이브에서 디스크 공간 부족 오류가 발생할 수 있습니다.  
  
 **영향:**  기본 웹 사이트의 로그 폴더가 너무 크면 C 드라이브의 사용 가능한 공간 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  서버를 백업 하 고 기본 웹 사이트가 중지 된 상태에서 C:\inetpub\logs\LogFiles\W3SVC1 폴더에 있는 로그 파일을 삭제할 수 있습니다. 그런 다음 기본 웹 사이트를 시작합니다.  
  
### <a name="no-binding-for-ssl-on-all-ip-addresses"></a>모든 IP 주소에 SSL에 대한 바인딩이 없음  
 **문제:**  서버의 모든 IP 주소에 SSL(Secure Sockets Layer) (SSL)에 대 한 바인딩이 없습니다.  
  
 **영향:**  서버의 모든 IP 주소에 SSL이 바인딩되어 있지 않으면 사용자가 일부 웹 사이트를 사용할 수 없게 됩니다.  
  
 **해결 방법:**  
  
##### <a name="to-bind-ssl-to-all-ip-addresses-on-the-server"></a>서버의 모든 IP 주소에 SSL을 바인딩하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자의 **연결** 창에서 서버, **사이트**를 차례로 확장하고 **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭한 다음 **바인딩 편집**을 클릭합니다.  
  
3.  **사이트 바인딩**에서 **추가**를 클릭하고 다음 설정을 선택합니다.  
  
    -   **Https** = **형식**  
  
    -   **IP 주소** = **모두 할당 되지 않음**  
  
    -   **포트** = 443  
  
4.  SSL 인증서를 선택하고 **확인**을 클릭하여 변경 내용을 저장합니다.  
  
### <a name="no-binding-for-ssl-on-the-default-web-site"></a>기본 웹 사이트에 SSL에 대한 바인딩이 없음  
 **문제:**  기본 웹 사이트에는 SSL에 대 한 바인딩이 없습니다.  
  
 **영향:**  기본 웹 사이트에 SSL이 바인딩되어 있지 않으면 사용자가 일부 웹 사이트를 사용 하지 못할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-bind-ssl-to-the-default-website"></a>기본 웹 사이트에 SSL을 바인딩하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자의 **연결** 창에서 서버, **사이트**를 차례로 확장하고 **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭한 다음 **바인딩 편집**을 클릭합니다.  
  
3.  **사이트 바인딩**에서 **추가**를 클릭하고 다음 옵션을 선택합니다.  
  
    -   **Https** = **형식**  
  
    -   **IP 주소** = **모두 할당 되지 않음**  
  
    -   **포트** = 443  
  
    > [!NOTE]
    >  특정 IP 주소에 포트 443에 대한 HTTPS 바인딩이 있는 경우 해당 바인딩의 **IP 주소** 특성을 **모두 할당되지 않음**으로 변경합니다. IP 주소 127.0.0.1은 예외입니다. 127.0.0.1에 대한 바인딩은 변경하지 마세요.  
  
4.  SSL 인증서를 선택하고 **확인**을 클릭하여 변경 내용을 저장합니다.  
  
### <a name="a-certificate-expires-within-30-days"></a>인증서가 30일 내에 만료됨  
 **문제:**  서버 인증서는 30 일 이내에 만료 됩니다.  
  
 **영향:**  서버에서 만료 된 인증서를 사용할 수 없습니다. 인증서가 만료되면 사용자가 원격 액세스 기능을 사용하지 못할 수 있습니다.  
  
 **해결 방법:**  인증서가 만료 되지 않도록 하려면 신뢰할 수 있는 인증 기관으로 인증서를 갱신 합니다.  
  
### <a name="certificate-subject-does-not-match-the-name-configured-by-domain-name-wizard"></a>인증서 주체가 도메인 이름 마법사에서 구성된 이름과 일치하지 않음  
 **문제:**  인증서 주체가 도메인 이름 마법사에 의해 구성 된 이름과 일치 하지 않습니다.  
  
 **영향:**  인증서 주체가 도메인 이름 마법사에 의해 구성 된 이름과 일치 하지 않는 경우 일부 웹 사이트는 초기화 되지 않습니다. 다른 사이트는 "이 웹 사이트의 보안 인증서에 문제가 있습니다." 라는 오류를 표시 합니다.  
  
 **해결 방법:**  이 문제를 해결 하려면 원격 액세스 설정 마법사를 다시 실행 하 고 인증서에 올바른 도메인 이름을 제공 하거나 사용 하려는 도메인 이름과 일치 하는 새 인증서를 구입 합니다.  
  
### <a name="one-or-more-user-accounts-have-duplicate-cn-names"></a>하나 이상의 사용자 계정에 중복된 CN 이름이 있음  
 **문제:**  하나 이상의 사용자 계정에 중복 된 CN 이름 ({0})이 있습니다.  
  
 **영향:**  사용자 계정에 중복 된 CN 이름이 있는 경우 사용자가 네트워크에 로그온 하지 못할 수 있습니다. 또한 Active Directory에서 사용자를 검색할 경우 잘못된 값이 반환될 수 있습니다.  
  
 **해결 방법:**  이 문제를 해결 하려면: 네트워크 사용자 계정에 중복 된 "CN =" 이름이 없는지 확인 합니다. 이 작업을 더 쉽게 하려면 검토를 위해 Active Directory 내용을 텍스트 파일로 내보내는 것이 좋습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [LDIFDE를 사용 하 여 디렉터리 개체를 가져오기 및 내보내기 Active Directory (기술 자료 문서 237677)](https://support.microsoft.com/kb/237677) (https://support.microsoft.com/kb/237677)를 참조 하세요.  
  
### <a name="nt-backup-is-installed"></a>NT 백업이 설치되어 있음  
 **문제:**  서버에 Windows NT 백업 프로그램이 설치 되어 있습니다.  
  
 **영향:**   Windows Server Essentials는 Windows Server 백업을 사용 합니다. Windows NT Backup 프로그램도 설치되어 있으면 두 백업 프로그램 간에 충돌이 발생할 수 있습니다. 이 경우 Windows Server Backup 프로세스가 실패할 수 있습니다. 충돌로 인해 백업을 사용하여 서버를 복원하지 못할 수도 있습니다.  
  
 **해결 방법:** 이 문제를 해결 하려면 서버에서 NT 백업 프로그램을 제거 합니다.  
  
### <a name="iis-does-not-own-port-80-000080-or-port-443-0000443"></a>IIS에서 포트 80(0.0.0.0:80) 또는 포트 443(0.0.0.0:443)을 소유하고 있지 않음  
 **문제:**  인터넷 정보 서비스 (IIS)는 포트 80 (0.0.0.0:80) 또는 포트 443을 소유 하지 않습니다. 해당 포트가 현재 다른 애플리케이션에서 바인딩되어 있습니다.  
  
 **영향:**   Windows Server Essentials 웹 응용 프로그램에서는 사용자가 서비스를 사용할 수 있도록 포트 80 및 포트 443을 사용 해야 합니다. 다른 프로세스 또는 응용 프로그램에서 포트 80 또는 포트 443를 이미 사용 하 고 있는 경우에는 Windows Server Essentials 웹 응용 프로그램을 실행할 수 없습니다. 이 경우 사용자가 원격 웹 액세스 및 기타 애플리케이션을 사용할 수 없습니다.  
  
 **해결 방법:**  이 문제를 해결 하려면: 포트 80 또는 포트 443을 이미 사용 하 고 있는 응용 프로그램을 제거 하거나 해당 응용 프로그램을 다른 포트에 할당 합니다.  
  
### <a name="the-default-website-is-not-running"></a>기본 웹 사이트가 실행되고 있지 않음  
 **문제:**  Windows Server Essentials 환경에서 기본 웹 사이트가 실행 되 고 있지 않습니다.  
  
 **영향:**   Windows Server Essentials 웹 응용 프로그램을 사용 하려면 기본 웹 사이트를 사용 해야 합니다. 기본 웹 사이트가 실행되고 있지 않으면 사용자가 원격 웹 액세스 및 기타 애플리케이션을 사용할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-default-website"></a>기본 웹 사이트를 시작하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서 서버 이름을 확장하고 **사이트**를 클릭합니다.  
  
3.  **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭하고 **웹 사이트 관리**를 가리킨 다음 **시작**을 클릭합니다.  
  
### <a name="read-and-script-permissions-for-the-remote-virtual-directory-are-incorrect"></a>/Remote 가상 디렉터리에 대한 읽기 및 스크립트 권한이 잘못됨  
 **문제:**  읽기 및 스크립트 권한이/Remote 가상 디렉터리에 할당 되지 않았습니다.  
  
 **영향:**  /Remote 가상 디렉터리에 대 한 읽기 및 스크립트 권한이 잘못 된 경우 사용자가 원격 웹 액세스를 사용할 수 없습니다. 원격 웹 액세스를 사용 하 여 인터넷을 검색 하려고 하면 "HTTP 오류 403.1 사용할 수 없음" 오류가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-assign-read-and-script-permissions-to-the-remote-directory"></a>/Remote 디렉터리에 대한 읽기 및 스크립트 권한을 할당하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서 서버 이름을 확장하고 **사이트**를 클릭합니다.  
  
3.  **기본 웹 사이트**를 확장한 다음 **원격**을 확장합니다.  
  
4.  **기능 보기**에서 **처리기 매핑**을 두 번 클릭합니다.  
  
5.  **작업** 창에서 **기능 사용 권한 편집**을 클릭합니다.  
  
6.  **읽기** 및 **스크립트** 확인란을 선택하고 **확인**을 클릭합니다.  
  
### <a name="http-redirect-is-either-set-or-inherited-on-the-remote-virtual-directory"></a>/Remote 가상 디렉터리에 HTTP 리디렉션이 설정되어 있거나 상속됨  
 **문제:**  HTTP 리디렉션 특성이 예기치 않게 설정 되거나/Remote 가상 디렉터리에 상속 됩니다.  
  
 **영향:**  /Remote 가상 디렉터리에 HTTP 리디렉션 특성이 설정 되어 있으면 원격 웹 작업 공간이 제대로 작동 하지 않습니다.  
  
 **해결 방법:**  
  
##### <a name="to-remove-the-http-redirect-attribute"></a>HTTP 리디렉션 특성을 제거하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서 서버 이름을 확장하고 **사이트**를 클릭합니다.  
  
3.  **기본 웹 사이트**를 확장한 다음 **원격**을 확장합니다.  
  
4.  **기능 보기**에서 **HTTP 리디렉션**을 두 번 클릭합니다.  
  
5.  **요청을 이 대상으로 리디렉션** 확인란을 선택 취소하고 **작업** 창에서 **적용**을 클릭합니다.  
  
### <a name="a-host-name-exists-for-port-80-on-the-default-website"></a>기본 웹 사이트에 포트 80에 대한 호스트 이름이 있음  
 **문제:**  기본 웹 사이트에서 포트 80에 대 한 호스트 이름이 할당 됩니다.  
  
 **영향:**  기본 웹 사이트에서 포트 80에 대 한 호스트 이름이 할당 된 경우 일부 Windows Server Essentials 웹 응용 프로그램에 연결 하지 못할 수 있습니다. 호스트 이름은 필수가 아니며 이러한 상황에서 권장되지 않습니다.  
  
 **해결 방법:**  
  
##### <a name="to-clear-the-host-name-entry-for-port-80-on-the-default-website"></a>기본 웹 사이트에서 포트 80에 대한 호스트 이름 항목을 지우려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서 서버 이름을 확장하고 **사이트**를 클릭합니다.  
  
3.  **기능 보기**에서 **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭한 다음 **바인딩**을 클릭합니다.  
  
4.  **사이트 바인딩**에서 **포트 80에 대한 HTTP** 설정을 선택하고 **편집**을 클릭합니다.  
  
5.  **사이트 바인딩 편집**에서 **호스트 이름** 항목을 지우고 **확인**을 클릭합니다.  
  
### <a name="backup-does-not-succeed-because-of-a-hidden-partition"></a>숨겨진 파티션으로 인해 백업에 실패함  
 **문제:**  NTFS가 아닌 파티션은 Windows Server 백업 백업 하도록 예약 되어 있습니다.  
  
 **영향:**  Windows Server 백업는 NTFS로 포맷 된 파티션만 백업할 수 있습니다.  
  
 **해결 방법:**  NTFS가 아닌 파티션을 백업 하도록 Windows Server 백업 구성 하지 마십시오. 자세한 내용은 [Windows Server 2008 기반 컴퓨터에서 시스템 상태 백업이 실패할 때 이벤트 id 12290 및 16387이 기록 됨 (기술 자료 문서 968128)](https://support.microsoft.com/kb/968128) (https://support.microsoft.com/kb/968128)를 참조 하십시오.  
  
### <a name="the-most-recent-backup-did-not-succeed"></a>가장 최근의 백업이 실패함  
 **문제:**  가장 최근의 백업 시도가 성공적으로 완료 되지 않았습니다.  
  
 **영향:**  시스템의 백업 상태가 올바르지 않습니다.  
  
 **해결 방법:**  가장 최근의 백업 중에 발생 한 오류에 대 한 이벤트 로그 및 백업 로그를 검토 합니다.  
  
### <a name="the-startup-type-for-the-file-replication-service-is-not-set-to-automatic"></a>파일 복제 서비스의 시작 유형이 자동으로 설정되어 있지 않음  
 **문제:**  시작 유형이 기본값인 자동으로 설정 되어 있지 않으면 FRS (파일 복제 서비스)가 시작 되지 않을 수 있습니다.  
  
 **영향:**  파일 복제 서비스가 실행 되 고 있지 않으면 도메인 컨트롤러에서 해당 서비스의 보급을 중지할 수 있습니다. 이 경우 로그온 오류 및 그룹 정책 오류와 같은 다른 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-file-replication-service-for-automatic-startup"></a>파일 복제 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **파일 복제**를 두 번 클릭합니다.  
  
3.  **시작 유형**에 대해 **자동**을 선택하고 **적용**을 클릭합니다.  
  
### <a name="the-file-replication-service-is-not-running"></a>파일 복제 서비스가 실행되고 있지 않음  
 **문제:**  파일 복제 서비스가 실행 되 고 있지 않습니다.  
  
 **영향:**  파일 복제 서비스가 실행 되 고 있지 않으면 도메인 컨트롤러에서 해당 서비스의 보급을 중지할 수 있습니다. 이 동작으로 인해 로그온 오류 및 그룹 정책 오류와 같은 다른 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-file-replication-service"></a>파일 복제 서비스를 시작하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **파일 복제 서비스**를 두 번 클릭합니다.  
  
3.  **시작**을 클릭합니다.  
  
### <a name="the-logon-account-for-the-file-replication-service-is-not-set-to-use-the-local-system-account"></a>파일 복제 서비스에 대한 로그온 계정이 로컬 시스템 계정을 사용하도록 설정되어 있지 않음  
 **문제:**  파일 복제 서비스가 로컬 시스템 계정을 기본 로그온 계정으로 사용 하도록 구성 되어 있지 않습니다.  
  
 **영향:**  파일 복제 서비스가 로컬 시스템을 기본 로그온 계정으로 사용 하지 않는 경우 사용 권한 관련 오류가 발생할 수 있습니다. 이러한 오류는 다른 오류를 트리거할 수 있으며, 결국 도메인 컨트롤러가 해당 서비스의 알림을 중지하게 만들 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-local-system-as-the-default-logon-account-for-file-replication"></a>로컬 시스템을 파일 복제에 대한 기본 로그온 계정으로 구성하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **파일 복제**를 두 번 클릭합니다.  
  
3.  **서비스 속성** 페이지에서 **로그온** 탭을 클릭합니다.  
  
4.  **로컬 시스템 계정** 옵션을 선택하고 **적용**을 클릭합니다.  
  
5.  서비스를 다시 시작합니다.  
  
### <a name="the-startup-type-for-the-dfs-replication-service-is-not-set-to-automatic"></a>DFS 복제 서비스의 시작 유형이 자동으로 설정되어 있지 않음  
 **문제:**  시작 유형이 기본값인 자동으로 설정 되어 있지 않으면 DFS 복제 서비스가 시작 되지 않을 수 있습니다.  
  
 **영향:**  DFS 복제 서비스가 실행 되 고 있지 않으면 도메인 컨트롤러에서 해당 서비스의 보급을 중지할 수 있습니다. 이 경우 로그온 오류 및 그룹 정책 오류와 같은 다른 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-dfs-replication-service-for-automatic-startup"></a>DFS 복제 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **DFS 복제**를 두 번 클릭합니다.  
  
3.  **시작 유형**에 대해 **자동**을 선택하고 **적용**을 클릭합니다.  
  
### <a name="the-dfs-replication-service-is-not-running"></a>DFS 복제 서비스가 실행되고 있지 않음  
 **문제:**  DFS 복제 서비스가 현재 실행 되 고 있지 않습니다.  
  
 **영향:**  DFS 복제 서비스가 실행 되 고 있지 않으면 도메인 컨트롤러에서 해당 서비스의 보급을 중지할 수 있습니다. 이 동작으로 인해 로그온 오류 및 그룹 정책 오류와 같은 다른 문제가 발생할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-dfs-replication-service"></a>DFS 복제 서비스를 시작하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **DFS 복제**를 두 번 클릭합니다.  
  
3.  **시작**을 클릭합니다.  
  
### <a name="the-dfs-replication-service-is-not-is-not-set-to-use-the-local-system-account"></a>DFS 복제 서비스가 로컬 시스템 계정을 사용하도록 설정되어 있지 않음  
 **문제:**  DFS 복제 서비스가 로컬 시스템 계정을 기본 로그온 계정으로 사용 하도록 설정 되어 있지 않습니다.  
  
 **영향:**  DFS 복제 서비스에서 로컬 시스템을 기본 로그온 계정으로 사용 하지 않는 경우 사용 권한 관련 오류가 발생할 수 있습니다. 이러한 오류는 다른 오류를 트리거할 수 있으며, 결국 도메인 컨트롤러가 해당 서비스의 알림을 중지하게 만들 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-dfs-replication-to-use-local-system-as-the-default-logon-account"></a>로컬 시스템을 기본 로그온 계정으로 사용하도록 DFS 복제를 구성하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **DFS 복제**를 두 번 클릭합니다.  
  
3.  **서비스 속성** 페이지에서 **로그온** 탭을 클릭합니다.  
  
4.  **로컬 시스템 계정** 옵션을 선택하고 **적용**을 클릭합니다.  
  
5.  서비스를 다시 시작합니다.  
  
### <a name="the-windows-server-office-365-integration-service-is-not-set-to-use-the-local-system-account"></a>Windows Server Office 365 통합 서비스가 로컬 시스템 계정을 사용하도록 설정되어 있지 않음  
 **문제:**  Windows Server Office 365 통합 서비스가 로컬 시스템 계정을 기본 로그온 계정으로 사용 하도록 설정 되어 있지 않습니다.  
  
 **영향:**  Windows Server Office 365 Integration Service에서 로컬 시스템을 기본 로그온 계정으로 사용 하지 않는 경우 Office 365의 일부 기능이 제대로 작동 하지 않을 수 있습니다. 사용 권한 관련 오류가 발생할 수도 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-office-365-integration-service-to-use-local-system-as-the-default-logon-account"></a>로컬 시스템을 기본 로그온 계정으로 사용하도록 Office 365 통합 서비스를 구성하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **Windows Server Office 365 통합 서비스**를 두 번 클릭합니다.  
  
3.  **서비스 속성** 페이지에서 **로그온** 탭을 클릭합니다.  
  
4.  **로컬 시스템 계정** 옵션을 선택하고 **적용**을 클릭합니다.  
  
5.  서비스를 다시 시작합니다.  
  
### <a name="the-windows-server-office-365-integration-service-is-not-running"></a>Windows Server Office 365 통합 서비스가 실행되고 있지 않음  
 **문제:**  Windows Server Office 365 통합 서비스가 현재 실행 되 고 있지 않습니다.  
  
 **영향:**  Windows Server Office 365 Integration Service가 실행 되 고 있지 않은 경우에는 Office 365의 클라우드 기반 기능을 사용할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-start-the-windows-server-office-365-integration-service"></a>Windows Server Office 365 통합 서비스를 시작하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **Windows Server Office 365 통합 서비스**를 두 번 클릭합니다.  
  
3.  **시작**을 클릭합니다.  
  
### <a name="the-startup-type-for-the-windows-server-office-365-integration-service-is-not-set-to-automatic"></a>Windows Server Office 365 통합 서비스의 시작 유형이 자동으로 설정되어 있지 않음  
 **문제:**  시작 유형이 기본값인 자동으로 설정 되어 있지 않으면 Windows Server Office 365 통합 서비스가 시작 되지 않을 수 있습니다.  
  
 **영향:**  Windows Server Office 365 Integration Service가 실행 되 고 있지 않은 경우에는 Office 365의 클라우드 기반 기능을 사용할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-office-365-integration-service-for-automatic-startup"></a>Office 365 통합 서비스를 자동으로 시작되도록 구성하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **Windows Server Office 365 통합 서비스**를 두 번 클릭합니다.  
  
3.  **시작 유형**에 대해 **자동**을 선택하고 **적용**을 클릭합니다.  
  
### <a name="a-registry-value-is-missing-or-set-incorrectly"></a>레지스트리 값이 없거나 잘못 설정됨  
 **문제:**  HKEY_LOCAL_MACHINE \Software\Microsoft\Rpc\RpcProxy 아래에 있는 레지스트리 키가 잘못 된 값을 포함 하거나 존재 하지 않습니다.  
  
 **영향:**  RPCProxy 레지스트리 키가 잘못 설정 된 경우 다음과 유사한 오류 메시지가 표시 될 수 있습니다. "원격 데스크톱 게이트웨이 서버를 일시적으로 사용할 수 없기 때문에 컴퓨터에서 원격 컴퓨터에 연결할 수 없습니다. 나중에 다시 연결하거나 네트워크 관리자에게 문의하세요."  
  
 **해결 방법:**  
  
##### <a name="to-correct-the-registry-setting"></a>레지스트리 설정을 수정하려면  
  
1.  레지스트리 편집기를 엽니다.  
  
2.  다음 레지스트리 키로 이동합니다.  
  
     HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy  
  
3.  "웹 사이트" 라는 문자열에 기본 웹 사이트의 데이터 값이 있는지 확인 합니다.  
  
    -   데이터 값이 잘못된 경우 올바른 값을 사용하도록 문자열을 수정합니다.  
  
    -   문자열이 없으면 "웹 사이트" 라는 새 문자열을 만들고 데이터 값을 기본 웹 사이트로 설정 합니다.  
  
### <a name="the-startup-type-for-the-block-level-backup-engine-service-is-not-set-to-manual"></a>블록 수준 백업 엔진 서비스의 시작 유형이 수동으로 설정되어 있지 않음  
 **문제:**  블록 수준 백업 엔진 서비스에서 기본 시작 유형인 수동을 사용 하 고 있지 않습니다.  
  
 **영향:**  시작 유형이 수동으로 설정 되어 있지 않으면 블록 수준 백업 엔진 서비스가 시작 되지 않을 수 있습니다. 이 문제: Windows Server 백업 작업이 실패할 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-for-manual-startup"></a>블록 수준 백업 엔진 서비스를 수동으로 시작되도록 구성하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **블록 수준 백업 엔진 서비스**를 두 번 클릭합니다.  
  
3.  **시작 유형**에 대해 **수동**을 선택하고 **적용**을 클릭합니다.  
  
### <a name="the-logon-account-for-the-block-level-backup-engine-service-is-not-set-to-use-the-local-system-account"></a>블록 수준 백업 엔진 서비스에 대한 로그온 계정이 로컬 시스템 계정을 사용하도록 설정되어 있지 않음  
 **문제:**  블록 수준 백업 엔진 서비스가 로컬 시스템 계정을 기본 로그온 계정으로 사용 하도록 설정 되어 있지 않습니다.  
  
 **영향:**  블록 수준 백업 엔진 서비스가 로컬 시스템을 기본 로그온 계정으로 사용 하지 않는 경우 사용 권한 관련 오류가 발생할 수 있습니다. 이러한 오류로 인해 Windows Server Backup 작업이 성공적으로 완료되지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-the-block-level-backup-engine-service-to-use-local-system-as-the-default-logon-account"></a>로컬 시스템을 기본 로그온 계정으로 사용하도록 블록 수준 백업 엔진 서비스를 구성하려면  
  
1.  서비스 콘솔을 엽니다.  
  
2.  서비스 목록에서 **블록 수준 백업 엔진 서비스**를 두 번 클릭합니다.  
  
3.  **서비스 속성** 페이지에서 **로그온** 탭을 클릭합니다.  
  
4.  **로컬 시스템 계정** 옵션을 선택하고 **적용**을 클릭합니다.  
  
5.  서비스를 다시 시작합니다.  
  
### <a name="the-common-name-on-the-certificate-that-is-bound-to-the-wss-certificate-web-service-website-does-not-match-the-server-name"></a>WSS 인증서 웹 서비스 웹 사이트에 바인딩된 인증서의 일반 이름이 서버 이름과 일치하지 않음  
 **문제:**  유효 하지 않은 인증서는 IIS의 WSS 인증서 웹 서비스 웹 사이트에 바인딩되어 있습니다. 이 인증서의 일반 이름이 서버 이름과 일치하지 않습니다.  
  
 **영향:**  잘못 된 인증서를 WSS 인증서 웹 서비스 웹 사이트에 바인딩하는 경우 연결 마법사가 제대로 작동 하지 않을 수 있습니다.  
  
 **해결 방법:**  
  
##### <a name="to-configure-a-valid-certificate-for-the-wss-certificate-web-service"></a>WSS 인증서 웹 서비스에 대해 유효한 인증서를 구성하려면  
  
1.  서버에서 IIS(인터넷 정보 서비스) 관리자를 엽니다.  
  
2.  IIS 관리자에서 서버 이름을 확장하고 **사이트**를 클릭합니다.  
  
3.  **WSS 인증서 웹 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **바인딩 편집**을 클릭합니다.  
  
4.  **사이트 바인딩**에서 **HTTPS**를 클릭한 다음 **편집**을 클릭합니다.  
  
5.  **사이트 바인딩 편집**에서 **SSL 인증서**에 대해 서버와 동일한 이름을 가진 인증서를 선택합니다.  
  
6.  둘 이상의 인증서 항목에 서버와 동일한 이름이 있는 경우 **보기**를 클릭하여 유효한 인증서를 확인하고 해당 인증서를 선택합니다.  
  
### <a name="there-appears-to-be-a-problem-with-the-certificate-binding-for-the-remote-desktop-gateway-service"></a>원격 데스크톱 게이트웨이 서비스에 대한 인증서 바인딩에 문제가 있는 것 같음  
 **문제:**  원격 데스크톱 게이트웨이 서비스에 대 한 인증서가 잘못 바인딩되어 있는 것 같습니다.  
  
 **영향:**  원격 데스크톱 게이트웨이 서비스에 대 한 인증서가 올바르게 구성 되지 않은 경우 사용자는 원격 웹 액세스에 연결할 수 없습니다.  
  
 **해결 방법:**  
  
##### <a name="to-fix-the-binding-for-the-remote-desktop-gateway-service"></a>원격 데스크톱 게이트웨이 서비스에 대한 바인딩을 수정하려면  
  
-   관리자 권한으로 명령 프롬프트를 열고 다음 명령을 입력합니다.  
  
    ```  
    REG ADD HKLM\SYSTEM\CurrentControlSet\services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443  /v DefaultFlags /t REG_DWORD /d 1 /f  
    net stop tsgateway  
    net start tsgateway  
    ```  
  
     자세한 내용은 [Windows Server Essentials에서 원격 데스크톱 게이트웨이 서비스를 관리 하는 방법 (기술 자료 문서 2472211)](https://support.microsoft.com/kb/2472211) (https://support.microsoft.com/kb/2472211)을 참조 하세요.
