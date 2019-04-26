---
title: Windows Server Essentials에서 DirectAccess 구성
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c959b6fc-c67e-46cd-a9cb-cee71a42fa4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cc336dcd2a5418aa79254108c941a02147112e8f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860684"
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>Windows Server Essentials에서 DirectAccess 구성

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 항목에서는 모바일 담당자가 원활 하 게 설정 하지 않고 인터넷 장치가 있는 원격 위치에서 s 조직 네트워크에 연결을 사용 하도록 설정 하려면 Windows Server Essentials에서 DirectAccess를 구성 하기 위한 단계별 지침을 가상 사설망 (VPN) 연결 합니다. DirectAccess가 Windows 8.1, Windows 8 및 Windows 7 컴퓨터에서 모바일 작업자에 게 내부 및 외부 같은 연결 경험을 제공할 수 있습니다.  
  
 Windows Server Essentials 도메인에 둘 이상의 Windows Server Essentials 서버에 DirectAccess이 도메인 컨트롤러에서 구성 합니다.  
  
> [!NOTE]
>  이 항목에서는 Windows Server Essentials 서버 도메인 컨트롤러인 경우 DirectAccess를 구성 하기 위한 지침을 제공 합니다. Windows Server Essentials 서버 도메인 멤버인 경우 도메인 구성원에서 DirectAccess를 구성 하는 지침을 따릅니다 [기존 원격 액세스 (VPN) 배포에 DirectAccess 추가](https://technet.microsoft.com/library/jj574220.aspx) 대신 합니다.  
  
## <a name="process-overview"></a>프로세스 개요  
 Windows Server Essentials에서 DirectAccess를 구성 하려면 다음 단계를 수행 합니다.  
  
> [!IMPORTANT]
>  이 가이드의 절차를 사용 하 여 Windows Server Essentials에서 DirectAccess를 구성 하려면 먼저 서버에서 VPN을 활성화 해야 합니다. 자세한 내용은 [VPN 관리](Manage-VPN-in-Windows-Server-Essentials.md)합니다.  
  
-   [1단계: 서버에 원격 액세스 관리 도구 추가](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)  
  
-   [2단계: 서버의 네트워크 어댑터 주소를 고정 IP 주소로 변경](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)  
  
-   [3 단계: 네트워크 위치 서버 인증서 및 DNS 레코드 준비](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)  
  
    -   [3a 단계: 인증서 템플릿의 웹 서버에 대 한 인증 된 사용자에 대 한 모든 권한을 부여합니다](#BKMK_GrantFullPermissions)  
  
    -   [3b단계: 외부 네트워크에서 확인할 수 없는 일반 이름의 네트워크 위치 서버용 인증서를 등록 합니다.](#BKMK_EnrollaCertificate)  
  
    -   [3c단계: DNS 서버에서 새 호스트를 추가 하 고 Windows Server Essentials 서버 주소에 매핑](#BKMK_MapNewHosttoServerAddress)  
  
-   [4 단계: DirectAccess 클라이언트 컴퓨터에 대 한 보안 그룹 만들기](#BKMK_AddSecurityGroup)  
  
-   [5단계: DirectAccess 설정 및 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)  
  
    -   [5a 단계: 원격 액세스 관리 콘솔을 사용 하 여 DirectAccess 설정](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
    -   [5b 단계: RRAS GPO (Windows Server Essentials에만 해당)에서 잘못 된 IPv6Prefix 제거](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
    -   [5c 단계: DirectAccess를 사용 하도록 Windows 7 Enterprise를 실행 하는 클라이언트 컴퓨터를 사용 하도록 설정](#BKMK_Step4cWindows7Setup)  
  
    -   [5d 단계: 네트워크 위치 서버 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
    -   [5e 단계: IPsec 채널을 설정한 경우 CA 인증을 무시 하는 레지스트리 키 추가](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
-   [6 단계: DirectAccess 서버에 대 한 이름 확인 정책 테이블 설정 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)  
  
-   [7 단계: DirectAccess 서버 Gpo에 대 한 TCP 및 UDP 방화벽 규칙 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)  
  
-   [8 단계: IP-HTTPS 인터페이스를 수신 대기 하도록 DNS64 구성 변경](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)  
  
-   [9 단계: WinNat 서비스용 포트 예약](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)  
  
-   [10 단계: WinNat 서비스 다시 시작](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)  
  
> [!NOTE]
>  [부록: Windows PowerShell을 사용 하 여 DirectAccess 설정](#BKMK_AppendixBPowerShellScript) DirectAccess 설정을 수행 하는 데 사용할 수 있는 Windows PowerShell 스크립트를 제공 합니다.  
  
##  <a name="BKMK_AddRAM"></a> 1 단계: 서버에 원격 액세스 관리 도구 추가  
  
#### <a name="to-add-remote-access-management-tools"></a>원격 액세스 관리 도구를 추가하려면  
  
1.  서버에서 시작 페이지 왼쪽 아래에 있는 **서버 관리자** 아이콘을 클릭합니다.  
  
     Windows Server Essentials에서 서버 관리자에 대 한 열을 검색 해야 합니다. 시작 페이지에서 **Server Manager**를 입력하고 검색 결과에서 **서버 관리자** 를 클릭합니다. 서버 관리자를 시작 페이지에 고정하려면 검색 결과에서 서버 관리자를 마우스 오른쪽 단추로 클릭하고 **시작 화면에 고정**을 클릭합니다.  
  
2.  **사용자 계정 컨트롤** 경고 메시지가 표시되는 경우 **예**를 클릭합니다.  
  
3.  서버 관리자 대시보드에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다.  
  
4.  역할 및 기능 추가 마법사에서 다음을 수행합니다.  
  
    1.  **설치 유형** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭합니다.  
  
    2.  에 **서버 선택 페이지** (또는 **대상 서버 선택** Windows Server Essentials에서 페이지)를 클릭 **서버 풀에서 서버 선택**.  
  
    3.  **기능** 페이지에서 **원격 서버 관리 도구(설치됨)**, **원격 액세스 관리 도구(설치됨)**, **역할 관리 도구(설치됨)**, **원격 액세스 관리 도구**를 차례로 확장한 다음 **원격 액세스 GUI 및 명령줄 도구**를 선택합니다.  
  
    4.  지시에 따라 마법사를 완료합니다.  
  
##  <a name="BKMK_AddStaticIP"></a> 2 단계: 서버의 네트워크 어댑터 주소를 고정 IP 주소로 변경  
 DirectAccess에는 고정 IP 주소를 사용하는 어댑터가 필요합니다. 서버에서 로컬 네트워크 어댑터의 IP 주소를 변경해야 합니다.  
  
#### <a name="to-add-a-static-ip-address"></a>고정 IP 주소를 추가하려면  
  
1.  시작 페이지에서 **제어판**을 엽니다.  
  
2.  **네트워크 및 인터넷**을 클릭한 다음 **네트워크 상태 및 작업 보기**를 클릭합니다.  
  
3.  **네트워크 및 공유 센터**의 작업창에서 **어댑터 설정 변경**을 클릭합니다.  
  
4.  로컬 네트워크 어댑터를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **네트워킹** 탭에서 **TCP/IPv4(인터넷 프로토콜 버전 4)** 를 클릭한 다음 **속성**을 클릭합니다.  
  
6.  **일반** 탭에서 **다음 IP 주소 사용**을 클릭한 다음 사용할 IP 주소를 입력합니다.  
  
     서브넷 마스크의 기본값이 **서브넷 마스크** 상자에 자동으로 표시됩니다. 기본값을 그대로 사용하거나 사용할 서브넷 마스크 값을 입력합니다.  
  
7.  **기본 게이트웨이** 상자에 기본 게이트웨이의 IP 주소를 입력합니다.  
  
8.  **기본 설정 DNS 서버** 상자에 DNS 서버의 IP 주소를 입력합니다.  
  
    > [!NOTE]
    >  루프백 네트워크(예: 127.0.0.1) 대신 DHCP(예, 192.168.X.X)에 의해 네트워크 어댑터에 할당된 IP 주소를 사용합니다. 할당된 IP 주소를 찾으려면 명령 프롬프트에서 **ipconfig** 를 실행합니다.  
  
9. **대체 DNS 서버** 상자에 대체 DNS 서버(있는 경우)의 IP 주소를 입력합니다.  
  
10. **확인**을 클릭하고 **닫기**를 클릭합니다.  
  
> [!IMPORTANT]
>  서버의 새 고정 IP 주소로 포트 80 및 443을 전달하도록 라우터를 구성해야 합니다.  
  
##  <a name="BKMK_DNS"></a> 3 단계: 네트워크 위치 서버에 대한 인증서 및 DNS 레코드 준비  
 네트워크 위치 서버에 대한 인증서 및 DNS 레코드를 준비하려면 다음 작업을 수행합니다.  
  
-   [3a 단계: 인증서 템플릿의 웹 서버에 대 한 인증 된 사용자에 대 한 모든 권한을 부여합니다](#BKMK_GrantFullPermissions)  
  
-   [3b단계: 외부 네트워크에서 확인할 수 없는 일반 이름의 네트워크 위치 서버용 인증서를 등록 합니다.](#BKMK_EnrollaCertificate)  
  
-   [3c단계: DNS 서버에서 새 호스트를 추가 하 고 Windows Server Essentials 서버 주소에 매핑하십시오.](#BKMK_MapNewHosttoServerAddress)  
  
###  <a name="BKMK_GrantFullPermissions"></a> 3a 단계: 인증서 템플릿의 웹 서버에 대 한 인증 된 사용자에 대 한 모든 권한을 부여합니다  
 먼저 인증 기관에서 웹 서버의 인증서 템플릿에 대 한 사용자를 인증에 대 한 모든 권한을 부여 하는 것입니다.  
  
####  <a name="BKMK_ToGrantFullPermissions"></a> S 인증서 템플릿을 웹 서버에 대 한 인증 된 사용자에 대 한 모든 권한을 부여 하려면  
  
1.  **시작** 페이지에서 **인증 기관**을 엽니다.  
  
2.  콘솔 트리에서 아래 **인증 기관 (로컬)** 를 확장 하 고 **< servername\>-CA**를 마우스 오른쪽 단추로 클릭 **인증서 템플릿**, 클릭 하 고 **관리할**합니다.  
  
3.  **인증 기관(로컬)** 에서 **웹 서버**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  웹 서버 속성의 **보안** 탭에서 **인증된 사용자**를 클릭하고 **모든 권한**을 선택한 다음 **확인**을 클릭합니다.  
  
5.  **Active Directory 인증서 서비스**를 다시 시작합니다. 제어판에서 **로컬 서비스 보기**를 엽니다. 서비스 목록에서 **Active Directory 인증서 서비스**를 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 클릭합니다.  
  
###  <a name="BKMK_EnrollaCertificate"></a> 3b 단계: 외부 네트워크에서 확인할 수 없는 일반 이름의 네트워크 위치 서버에 대한 인증서 등록  
 다음으로 외부 네트워크에서 확인할 수 없는 일반 이름의 네트워크 위치 서버에 대한 인증서를 등록합니다.  
  
####  <a name="BKMK_ToEnrollaCertificate"></a> 네트워크 위치 서버용 인증서를 등록 하려면  
  
1.  **시작** 페이지에서 **mmc**(Microsoft Management Console)를 엽니다.  
  
2.  **사용자 계정 컨트롤** 경고 메시지가 표시되는 경우 **예**를 클릭합니다.  
  
     MMC(Microsoft Management Console)가 열립니다.  
  
3.  **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
4.  **스냅인 추가/제거** 상자에서 **인증서**, **추가**를 차례로 클릭합니다.  
  
5.  **인증서 스냅인** 페이지에서 **컴퓨터 계정**을 클릭하고 **다음**을 클릭합니다.  
  
6.  **컴퓨터 선택** 페이지에서 **로컬 컴퓨터**를 클릭하고 **마침**을 클릭한 다음 **확인**을 클릭합니다.  
  
7.  콘솔 트리에서 **인증서(로컬 컴퓨터)**, **개인**을 차례로 확장하고 **인증서**를 마우스 오른쪽 단추로 클릭한 다음 **모든 작업**에서 **새 인증서 요청**을 클릭합니다.  
  
8.  인증서 등록 마법사가 나타나면 **다음**을 클릭합니다.  
  
9. **인증서 등록 정책 선택** 페이지에서 **다음**을 클릭합니다.  
  
10. **인증서 요청** 페이지에서 **웹 서버** 확인란을 선택하고 **이 인증서를 등록하려면 추가 정보가 필요합니다.** 를 클릭합니다.  
  
11. **인증서 속성** 상자에 **주체 이름**에 대한 다음 설정을 입력합니다.  
  
    1.  **유형**에 대해 **일반 이름**을 선택합니다.  
  
    2.  **값**에 네트워크 위치 서버의 이름(예: DirectAccess-NLS.contoso.local)을 입력하고 **추가**를 클릭합니다.  
  
    3.  **확인**, **등록**을 차례로 클릭합니다.  
  
12. 인증서 등록이 완료되면 **마침**을 클릭합니다.  
  
###  <a name="BKMK_MapNewHosttoServerAddress"></a> 3c 단계: DNS 서버에 새 호스트를 추가하여 Windows Server Essentials 서버 주소에 매핑  
 DNS 구성을 완료 하려면 DNS 서버에서 새 호스트를 추가 하 고 Windows Server Essentials 서버 주소에 매핑하십시오.  
  
####  <a name="BKMK_ToMapNewHosttoServerAddress"></a> Windows Server Essentials 서버 주소에 새 호스트를 매핑하려면  
  
1.  시작 페이지에서 DNS 관리자를 엽니다. DNS 관리자를 열려면 **dnsmgmt.msc**를 검색하고 결과에서 **dnsmgmt.msc** 를 클릭합니다.  
  
2.  DNS 관리자 콘솔 트리에서 로컬 서버를 확장 **정방향 조회 영역**s 서버 도메인 접미사가 있는 영역을 마우스 오른쪽 단추로 클릭 하 고 클릭 **새 호스트 (A 또는 AAAA)** 합니다.  
  
3.  서버의 이름과 IP 주소(예: DirectAccess-NLS.contoso.local) 및 해당 서버 주소(예: 192.168.x.x)를 입력합니다.  
  
4.  **호스트 추가**, **확인**, **완료**를 차례로 클릭합니다.  
  
##  <a name="BKMK_AddSecurityGroup"></a> 4 단계: DirectAccess 클라이언트 컴퓨터에 대한 보안 그룹 만들기  
 다음으로 DirectAccess 클라이언트 컴퓨터에 사용할 보안 그룹을 만들고 그룹에 컴퓨터 계정을 추가합니다.  
  
#### <a name="to-add-a-security-group-for-client-computers-that-use-directaccess"></a>DirectAccess를 사용하는 클라이언트 컴퓨터에 대한 보안 그룹을 추가하려면  
  
1.  서버 관리자 대시보드에서 **도구**, **Active Directory 사용자 및 컴퓨터**를 차례로 클릭합니다.  
  
    > [!NOTE]
    >  **도구** 메뉴에 **Active Directory 사용자 및 컴퓨터**가 표시되지 않으면 기능을 설치해야 합니다. Active Directory 사용자 및 그룹을 설치하려면 관리자 권한으로 다음 Windows PowerShell cmdlet을 실행합니다. `Install-WindowsFeature RSAT-ADDS-Tools` 자세한 내용은 [원격 서버 관리 도구 팩 설치 또는 제거](https://technet.microsoft.com/library/cc730825.aspx)를 참조하세요.  
  
2.  콘솔 트리에서 서버를 확장하고 **사용자**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기**, **그룹**을 차례로 클릭합니다.  
  
3.  그룹 이름, 그룹 범위 및 그룹 유형을 입력하고(보안 그룹 만들기) **확인**을 클릭합니다.  
  
 새 보안 그룹이 **사용자** 폴더에 추가됩니다.  
  
#### <a name="to-add-computer-accounts-to-the-security-group"></a>보안 그룹에 컴퓨터 계정을 추가하려면  
  
1.  서버 관리자 대시보드에서 **도구**, **Active Directory 사용자 및 컴퓨터**를 차례로 클릭합니다.  
  
2.  콘솔 트리에서 서버를 확장하고 **사용자**를 클릭합니다.  
  
3.  서버의 사용자 계정 및 보안 그룹 목록에서 DirectAccess에 대해 만든 보안 그룹을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
4.  **구성원** 탭에서 **추가**를 클릭합니다.  
  
5.  대화 상자에서 그룹에 추가할 컴퓨터 계정 이름을 세미콜론 (;)으로 구분하여 입력합니다. 그런 다음 **이름 확인**을 클릭합니다.  
  
6.  컴퓨터 계정의 유효성이 검사되고 나면 **확인**을 클릭합니다. 그런 다음 **확인**을 다시 클릭합니다.  
  
> [!NOTE]
>  컴퓨터 계정 속성에서 **소속 그룹** 탭을 사용하여 보안 그룹에 계정을 추가할 수도 있습니다.  
  
##  <a name="BKMK_EnableConfigureDA"></a> 5 단계: DirectAccess 설정 및 구성  
 사용 하도록 설정 하 고 Windows Server Essentials에서 DirectAccess를 구성 하려면 다음 단계를 완료 해야 합니다.  
  
-   [5a 단계: 원격 액세스 관리 콘솔을 사용 하 여 DirectAccess 설정](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
-   [5b 단계: RRAS GPO (Windows Server Essentials에만 해당)에서 잘못 된 IPv6Prefix 제거](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
-   [5c 단계: DirectAccess를 사용 하도록 Windows 7 Enterprise를 실행 하는 클라이언트 컴퓨터를 사용 하도록 설정](#BKMK_Step4cWindows7Setup)  
  
-   [5d 단계: 네트워크 위치 서버 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
-   [5e 단계: IPsec 채널을 설정한 경우 CA 인증을 무시 하는 레지스트리 키 추가](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
###  <a name="BKMK_EnableDA"></a> 5a 단계: 원격 액세스 관리 콘솔을 사용하여 DirectAccess 설정  
 이 섹션에서는 Windows Server Essentials에서 DirectAccess를 사용 하도록 설정 하려면 단계별 지침을 제공 합니다. 서버에서 아직 VPN을 구성하지 않았으면 이 절차를 시작하기 전에 VPN을 구성해야 합니다. 자세한 내용은 [VPN 관리](Manage-VPN-in-Windows-Server-Essentials.md)합니다.  
  
##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>원격 액세스 관리 콘솔을 사용하여 DirectAccess를 사용하도록 설정하려면  
  
1.  시작 페이지에서 **원격 액세스 관리**를 엽니다.  
  
2.  DirectAccess 사용 마법사에서 다음을 수행합니다.  
  
    1.  **DirectAccess 필수 구성 요소**를 검토하고 **다음**을 클릭합니다.  
  
    2.  **그룹 선택** 탭에서 DirectAccess 클라이언트에 대해 이전에 만든 보안 그룹을 추가합니다. (보안 그룹을 만들지 않은 경우 [4 단계: 컴퓨터가 DirectAccess 클라이언트에 대 한 보안 그룹 만들기](#BKMK_AddSecurityGroup) 지침은.)  
  
    3.  **그룹 선택** 탭에서 DirectAccess를 사용하여 서버에 원격으로 액세스하려는 경우 **이동 컴퓨터에만 DirectAccess 사용**을 클릭하고 **다음**을 클릭합니다.  
  
    4.  **네트워크 토폴로지**에서 서버의 토폴로지를 선택하고 **다음**을 클릭 합니다.  
  
    5.  **DNS 접미사 검색 목록**에서 필요한 경우 클라이언트 컴퓨터의 추가 DNS 접미사를 추가하고 **다음**을 클릭 합니다.  
  
        > [!NOTE]
        >  기본적으로 DirectAccess 사용 마법사에서 이미 현재 도메인의 DNS 접미사를 추가합니다. 그러나 필요한 경우 DNS 접미사를 더 추가할 수 있습니다.  
  
    6.  적용되는 GPO(그룹 정책 개체)를 검토하고 필요한 경우 수정합니다.  
  
    7.  **다음**을 클릭한 다음 **마침**을 클릭합니다.  
  
    8.  관리자 모드에서 다음 Windows PowerShell 명령을 실행하여 원격 액세스 관리 서비스를 다시 시작합니다.  
  
        ```powershell  
        Restart-Service RaMgmtSvc   
        ```  
  
###  <a name="BKMK_RemoveIPv6"></a> 5b 단계: RRAS GPO (Windows Server Essentials에만 해당)에서 잘못 된 IPv6Prefix 제거  
  이 섹션에서는 Windows Server Essentials를 실행 하는 서버에 적용 됩니다.  
  
 관리자 권한으로 Windows PowerShell을 열고 다음 명령을 실행합니다.  
  
```powershell  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
```  
  
###  <a name="BKMK_Step4cWindows7Setup"></a> 5c 단계: DirectAccess를 사용 하도록 Windows 7 Enterprise를 실행 하는 클라이언트 컴퓨터를 사용 하도록 설정  
 Windows 7 Enterprise를 실행 하는 클라이언트 컴퓨터에 있으면 해당 컴퓨터에서 DirectAccess를 사용 하도록 설정 하려면 다음 절차를 완료 합니다.  
  
##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>DirectAccess를 사용 하도록 Windows 7 Enterprise 컴퓨터를 사용 하도록 설정 하려면  
  
1.  S 서버 시작 페이지에서 엽니다 **원격 액세스 관리**합니다.  
  
2.  원격 액세스 관리 콘솔에서 **구성**을 클릭합니다. 그런 다음 **설정 세부 정보** 창의 **2단계**에서 **편집**을 클릭합니다.  
  
     원격 액세스 서버 설정 마법사가 열립니다.  
  
3.  에 **인증** 탭 (Windows Server Essentials 서버의 CA 인증서를 선택할 수 있습니다) 신뢰할 수 있는 루트 인증서로 사용할 수 있는 인증 기관 (CA) 인증서를 선택 합니다. **Windows 7 클라이언트 컴퓨터에서 DirectAccess를 통한 연결 사용**, **다음**을 차례로 클릭합니다.  
  
4.  지시에 따라 마법사를 완료합니다.  
  
> [!IMPORTANT]
>  Windows Server Essentials 서버 ur1이 미리 설치 되어 제공 되지 않은 경우 DirectAccess를 통해 연결 하는 Windows 7 Enterprise 컴퓨터의 알려진된 문제가 없습니다. 해당 환경에서 DirectAccess 연결을 사용하도록 설정하려면 다음 추가 단계를 수행해야 합니다.  
>   
>  1.  에 설명 된 핫픽스 [Microsoft 기술 자료 (KB) 문서 2796394](https://support.microsoft.com/kb/2796394) Windows Server Essentials 서버에 있습니다. 그런 다음 서버를 다시 시작합니다.  
> 2.  다음에 설명 된 핫픽스를 설치 [Microsoft 기술 자료 (KB) 문서 2615847](https://support.microsoft.com/kb/2615847) 각 Windows 7 컴퓨터에 있습니다.  
>   
>      이 문제는 Windows Server Essentials에서 해결 되었습니다.  
  
###  <a name="BKMK_NLS"></a> 5d 단계: 네트워크 위치 서버 구성  
 이 섹션에서는 네트워크 위치 서버 설정을 구성하는 단계별 지침을 제공합니다.  
  
> [!NOTE]
>  시작 하기 전에의 내용을 복사 합니다 < SystemDrive\>\inetpub\wwwroot 폴더는 < SystemDrive\>files\windows Server\Bin\WebApps\Site\insideoutside 폴더로 합니다. 또한 default.aspx 파일을 복사할 합니다 < SystemDrive\>files\windows Server\Bin\WebApps\Site 폴더는 < SystemDrive\>files\windows Server\Bin\WebApps\Site\insideoutside 폴더로 합니다.  
  
##### <a name="to-configure-the-network-location-server"></a>네트워크 위치 서버를 구성하려면  
  
1.  시작 페이지에서 **원격 액세스 관리**를 엽니다.  
  
2.  원격 액세스 관리 콘솔에서 **구성**을 클릭하고 **원격 액세스 설정** 세부 정보 창의 **3단계**에서 **편집**을 클릭합니다.  
  
3.  원격 액세스 서버 설치 마법사에서에 **네트워크 위치 서버** 탭을 선택 **원격 액세스 서버에 네트워크 위치 서버 배포**를 선택한 다음 있었던 인증서 이전에 발급 된 (에서 [3 단계: 네트워크 위치 서버 인증서 및 DNS 레코드 준비](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)).  
  
4.  지시에 따라 마법사를 완료하고 **마침**을 클릭합니다.  
  
###  <a name="BKMK_CA"></a> 5e 단계: IPsec 채널을 설정한 경우 CA 인증을 무시하는 레지스트리 키 추가  
 다음 단계에서는 IPsec 채널이 설정될 때 CA 인증을 무시하도록 서버를 구성합니다.  
  
##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>CA 인증을 무시하는 레지스트리 키를 추가하려면  
  
1.  시작 페이지에서 **regedit**(레지스트리 편집기)를 엽니다.  
  
2.  레지스트리 편집기에서 **HKEY_LOCAL_MACHINE**, **System**, **CurrentControlSet**, **Services**, **IKEEXT**를 차례로 확장합니다.  
  
3.  **IKEEXT**에서 **Parameters**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **DWORD(32비트) 값**을 차례로 클릭합니다.  
  
4.  새로 추가된 값의 이름을 **ikeflags**로 바꿉니다.  
  
5.  **ikeflags**를 두 번 클릭하고 **단위** 를 **16진수**로 설정한 다음 값을 **8000**으로 설정하고 **확인**을 클릭합니다.  
  
> [!NOTE]
>  관리자 모드에서 다음 Windows PowerShell 명령을 사용하여 이 레지스트리 키를 추가할 수 있습니다.  
>   
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`  
  
##  <a name="BKMK_NRPT"></a> 6 단계: DirectAccess 서버에 대한 이름 확인 정책 테이블 설정 구성  
 이 섹션에서는 DirectAccess 클라이언트 GPO의 내부 주소(예: contoso.local 접미사가 있는 항목)에 대한 NPRT(이름 확인 정책 테이블) 항목을 편집한 다음 IPHTTPS 인터페이스 주소를 설정하는 방법에 대한 지침을 제공합니다.  
  
#### <a name="to-configure-name-resolution-policy-table-entries"></a>이름 확인 정책 테이블 항목을 구성하려면  
  
1.  시작 페이지에서 **그룹 정책 관리**를 엽니다.  
  
2.  그룹 정책 관리 콘솔에서 기본 포리스트 및 도메인을 클릭하고 **DirectAccess 클라이언트 설정**을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **컴퓨터 구성**, **정책**, **Windows 설정**, **이름 확인 정책**을 차례로 클릭합니다. 네임스페이스가 DNS 접미사와 동일한 항목을 선택하고 **규칙 편집**을 클릭합니다.  
  
4.  **DirectAccess에 대한 DNS 설정** 탭을 클릭하고 **이 규칙에서 DirectAccess에 대한 DNS 설정 사용**을 선택합니다. DNS 서버 목록에 IP-HTTPS 인터페이스의 IPv6 주소를 추가합니다.  
  
    > [!NOTE]
    >  다음 Windows PowerShell 명령을 사용하여 IPv6 주소를 가져올 수 있습니다.  
    >   
    >  `(Get-NetIPInterface -InterfaceAlias IPHTTPSInterface | Get-NetIPAddress -PrefixLength 128)[1].IPAddress`  
  
##  <a name="BKMK_TCPUDP"></a> 7 단계: DirectAccess 서버 GPO에 대한 TCP 및 UDP 방화벽 규칙 구성  
 이 섹션에서는 DirectAccess 서버 GPO에 대한 TCP 및 UDP 방화벽 규칙을 구성하는 단계별 지침을 제공합니다.  
  
#### <a name="to-configure-firewall-rules"></a>방화벽 규칙을 구성하려면  
  
1.  시작 페이지에서 **그룹 정책 관리**를 엽니다.  
  
2.  그룹 정책 관리 콘솔에서 기본 포리스트 및 도메인을 클릭하고 **DirectAccess 서버 설정**을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **컴퓨터 구성**, **정책**, **Windows 설정**, **보안 설정**, **고급 보안이 포함된 Windows 방화벽**을 차례로 클릭하고 다음 수준 **고급 보안이 포함된 Windows 방화벽**, **인바운드 규칙**을 차례로 클릭합니다. **도메인 이름 서버(TCP-In)** 를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **범위** 탭을 클릭하고 **로컬 IP 주소** 목록에서 IP-HTTPS 인터페이스의 IPv6 주소를 추가합니다.  
  
5.  **도메인 이름 서버(UDP-In)** 에 대해 동일한 절차를 반복합니다.  
  
##  <a name="BKMK_DNS64"></a> 8 단계: IP-HTTPS 인터페이스를 수신 대기하도록 DNS64 구성 변경  
 다음 Windows PowerShell 명령을 사용하여 IP-HTTPS 인터페이스를 수신 대기하도록 DNS64 구성을 변경해야 합니다.  
  
```powershell  
Set-NetDnsTransitionConfiguration  �AcceptInterface IPHTTPSInterface  
```  
  
##  <a name="BKMK_ExemptPort"></a> 9 단계: WinNat 서비스용 포트 예약  
 다음 Windows PowerShell 명령을 사용하여 WinNat 서비스용 포트를 예약합니다. "192.168.1.100을"을 Windows Server Essentials 서버의 실제 IPv4 주소로 바꿉니다.  
  
```powershell  
Set-NetNatTransitionConfiguration  �IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
```  
  
> [!IMPORTANT]
>  응용 프로그램과의 포트 충돌을 방지하도록 WinNat 서비스용으로 예약하는 포트 범위에는 포트 6602가 포함됩니다.  
  
##  <a name="BKMK_WinNAT"></a> 10 단계: WinNat 서비스 다시 시작  
 다음 Windows PowerShell 명령을 실행하여 Windows NAT 드라이버(WinNat) 서비스를 다시 시작합니다.  
  
```powershell  
Restart-Service winnat  
```  
  
##  <a name="BKMK_AppendixBPowerShellScript"></a> 부록: Windows PowerShell을 사용하여 DirectAccess 설정  
 이 섹션에서는 Windows PowerShell을 사용하여 DirectAccess를 설정 및 구성하는 방법에 대해 설명합니다.  
  
### <a name="preparation"></a>준비  
 DirectAccess에 대해 서버를 구성하기 전에 다음을 완료해야 합니다.  
  
1.  절차에 따라 [3 단계: 네트워크 위치 서버 인증서 및 DNS 레코드를 준비](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS) 라는 인증서를 등록 하 **Directaccess-nls.contoso.com** (여기서 **contoso.com** 실제으로 바뀝니다 내부 도메인 이름) 및 (NLS)의 네트워크 위치 서버에 대 한 DNS 레코드를 추가 합니다.  
  
2.  Active Directory에 **DirectAccessClients** 라는 보안 그룹을 추가한 다음 DirectAccess 기능을 제공할 클라이언트 컴퓨터를 추가합니다. 자세한 내용은 참조 하세요. [4 단계: 컴퓨터가 DirectAccess 클라이언트에 대 한 보안 그룹 만들기](#BKMK_AddSecurityGroup)합니다.  
  
### <a name="commands"></a>명령  
  
> [!IMPORTANT]
>  Windows Server Essentials에서 불필요 한 IPv6 접두사 GPO를 제거할 필요가 없습니다. 다음 레이블이 있는 코드 섹션을 삭제합니다. `# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`.  
  
```powershell  
# Add Remote Access role if not installed yet  
$ra = Get-WindowsFeature RemoteAccess  
If ($ra.Installed -eq $FALSE) { Add-WindowsFeature RemoteAccess }  
  
# Server may need to restart if you installed RemoteAccess role in the above step  
  
# Set the internet domain name to access server, replace contoso.com below with your own domain name  
$InternetDomain = "www.contoso.com"  
#Set the SG name which you create for DA clients  
$DaSecurityGroup = "DirectAccessClients"  
#Set the internal domain name  
$InternalDomain = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().Name  
  
# Set static IP and DNS settings  
$NetConfig = Get-WmiObject Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true"  
$CurrentIP = $NetConfig.IPAddress[0]  
$SubnetMask = $NetConfig.IPSubnet | Where-Object{$_ -like "*.*.*.*"}  
$NetConfig.EnableStatic($CurrentIP, $SubnetMask)  
$NetConfig.SetGateways($NetConfig.DefaultIPGateway)  
$NetConfig.SetDNSServerSearchOrder($CurrentIP)  
  
# Get physical adapter name and the certificate for NLS server  
$Adapter = (Get-WmiObject -Class Win32_NetworkAdapter -Filter "NetEnabled=$true").NetConnectionId  
$Certs = dir cert:\LocalMachine\My  
$nlscert = $certs | Where-Object{$_.Subject -like "*CN=DirectAccess-NLS*"}  
  
# Add regkey to bypass CA cert for IPsec authentication  
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000  
  
# Install DirectAccess.   
Install-RemoteAccess -NoPrerequisite -DAInstallType FullInstall -InternetInterface $Adapter -InternalInterface $Adapter -ConnectToAddress $InternetDomain -nlscertificate $nlscert -force  
  
#Restart Remote Access Management service  
Restart-Service RaMgmtSvc  
  
# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO   
  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
  
# Enable client computers running Windows 7 to use DirectAccess  
$allcertsinroot = dir cert:\LocalMachine\root  
$rootcert = $allcertsinroot | Where-Object{$_.Subject -like "*-CAA*"}  
Set-DAServer  �IPSecRootCertificate $rootcert[0]  
Set  �DAClient  �OnlyRemoteComputers Disabled -Downlevel Enabled  
  
#Set the appropriate security group used for DA client computers. Replace the group name below with the one you created for DA clients  
Add-DAClient -SecurityGroupNameList $DaSecurityGroup   
Remove-DAClient -SecurityGroupNameList "Domain Computers"  
  
# Gather DNS64 IP address information  
$Remoteaccess = get-remoteaccess  
$IPinterface = get-netipinterface -InterfaceAlias IPHTTPSInterface | get-netipaddress -PrefixLength 128  
$DNS64IP=$IPInterface[1].IPaddress  
$Natconfig = Get-NetNatTransitionConfiguration  
  
# Configure TCP and UDP firewall rules for the DirectAccess server GPO  
$GpoName = 'GPO:'+$InternalDomain+'\DirectAccess Server Settings'  
Get-NetFirewallRule -PolicyStore $GpoName -Displayname "Domain Name Server (TCP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP  
Get-NetFirewallrule -PolicyStore $GpoName -Displayname "Domain Name Server (UDP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP  
  
# Configure the name resolution policy settings for the DirectAccess server, replace the DNS suffix below with the one in your domain  
$Suffix = '.' + $InternalDomain  
set-daclientdnsconfiguration -DNSsuffix $Suffix -DNSIPAddress $DNS64IP  
  
# Change the DNS64 configuration to listen to IP-HTTPS interface  
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface  
  
# Copy the necessary files to NLS site folder  
XCOPY 'C:\inetpub\wwwroot' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /E /Y  
XCOPY 'C:\Program Files\Windows Server\Bin\WebApps\Site\Default.aspx' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /Y  
  
# Reserve ports for the WinNat service  
Set-NetNatTransitionConfiguration  �IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
  
# Restart the WinNat service  
Restart-Service winnat  
```  
  
## <a name="see-also"></a>참조  
  
-   [원격 액세스 관리](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
