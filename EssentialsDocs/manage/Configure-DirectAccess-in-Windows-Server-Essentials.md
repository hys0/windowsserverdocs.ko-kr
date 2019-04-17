---
title: "Windows Server Essentials의 DirectAccess 구성"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>Windows Server Essentials의 DirectAccess 구성

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 항목 원활 하 게 네트워크에 연결할 사용자 조직의 인터넷 장착 원격 위치에서 (VPN) 가상 개인 네트워크 연결을 설정 하지 않고 모바일 직원이 수 있도록 Windows Server Essentials의 DirectAccess 구성에 대 한 단계별 지침을 제공 합니다. DirectAccess에서 Windows 8.1, Windows 8 및 Windows 7 컴퓨터 잦은 동일한 연결 환경을 내부 및 외부의 office를 제공할 수 있습니다.  
  
 Windows Server Essentials 도메인에 둘 이상의 Windows Server Essentials 서버 DirectAccess이 도메인 컨트롤러에서 구성 합니다.  
  
> [!NOTE]
>  이 항목은 Windows Server Essentials 서버가 도메인 컨트롤러 때 DirectAccess 구성에 대 한 지침을 제공 합니다. DirectAccess에서 도메인 멤버 구성 하려면 지침에 따라 Windows Server Essentials 서버 도메인 구성원이 경우 [기존 원격 액세스 (VPN) 배포 추가 DirectAccess](https://technet.microsoft.com/library/jj574220.aspx) 대신 합니다.  
  
## <a name="process-overview"></a>프로세스 개요  
 Windows Server Essentials의 DirectAccess를 구성 하려면 다음 단계를 완료 합니다.  
  
> [!IMPORTANT]
>  이 가이드는 절차를 사용 하 여 Windows Server Essentials의 DirectAccess 구성 전에 서버에서 VPN 설정 해야 합니다. 자세한 내용은 [관리 VPN](Manage-VPN-in-Windows-Server-Essentials.md)합니다.  
  
-   [1 단계: 서버 관리 도구 원격 액세스 추가](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)  
  
-   [2 단계:에서 고정 IP 주소를 서버 네트워크 어댑터 주소 변경](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)  
  
-   [네트워크 위치 서버에 대 한 인증서 및 DNS 레코드를 준비 하는 3 단계:](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)  
  
    -   [3a 단계: 웹 서버의 인증서 템플릿 인증 된 사용자에 게 전체 권한을 부여](#BKMK_GrantFullPermissions)  
  
    -   [3b 단계: 외부 네트워크에서 확인할 수 있는 일반적인 이름의 네트워크 위치 서버에 대 한 인증서 등록](#BKMK_EnrollaCertificate)  
  
    -   [3 단계: 새 호스트 DNS 서버에 추가 하 고 Windows Server Essentials 서버 주소 지도](#BKMK_MapNewHosttoServerAddress)  
  
-   [4 단계: DirectAccess 클라이언트 컴퓨터에 대 한 보안 그룹 만들기](#BKMK_AddSecurityGroup)  
  
-   [5 단계: 사용 및 DirectAccess 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)  
  
    -   [5a 단계: DirectAccess 원격 액세스 Management Console을 사용 하 여 사용](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
    -   [5b 단계: RRAS GPO (Windows Server Essentials에만 해당)에 잘못 된 IPv6Prefix 제거](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
    -   [5 단계: Windows 7 Enterprise DirectAccess 사용 하 여 실행 하는 클라이언트 컴퓨터를 사용 하도록 설정](#BKMK_Step4cWindows7Setup)  
  
    -   [D 5 단계: 네트워크 위치 서버 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
    -   [5e 단계: 레지스트리 키 때를 무시 캘리포니아 인증 된 IPsec 채널을 설정 추가](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
-   [6 단계: 이름 해상도 정책 테이블 설정을 DirectAccess 서버에 대 한 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)  
  
-   [7 단계: UDP 및 TCP 방화벽 규칙 Gpo DirectAccess 서버에 대 한 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)  
  
-   [8 단계: IP HTTPS 인터페이스를 듣기 시작 DNS64 구성을 변경합니다](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)  
  
-   [예약 WinNat 서비스에 대 한 포트 9 단계:](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)  
  
-   [10 단계: WinNat 서비스를 다시 시작](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)  
  
> [!NOTE]
>  [부록: Windows PowerShell를 사용 하 여 DirectAccess 설정](#BKMK_AppendixBPowerShellScript) DirectAccess 설정 하는 데 사용할 수 있는 Windows PowerShell 스크립트를 제공 합니다.  
  
##  <a name="BKMK_AddRAM"></a>1 단계: 서버 관리 도구 원격 액세스 추가  
  
#### <a name="to-add-remote-access-management-tools"></a>원격 액세스 관리 도구를 추가 하려면  
  
1.  서버에서 시작 페이지의 왼쪽된 아래 모서리에 있는 **서버 관리자** 아이콘 합니다.  
  
     Windows Server Essentials에서 검색 하 여 엽니다 서버 관리자에 대 한 해야 합니다. 시작 페이지에 입력 **서버 관리자**을 차례로 클릭 하 고 **서버 관리자** 검색 결과에서 합니다. 서버 관리자 시작 페이지에 고정 하 고 검색 결과에서 서버 관리자 단추로 클릭 하 고 클릭 **시작 화면에 고정**합니다.  
  
2.  경우에 **사용자 계정 컨트롤** 경고 메시지가 표시를 클릭 **예**합니다.  
  
3.  서버 관리자 대시보드에서 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다.  
  
4.  역할 추가 및 기능 마법사에서 다음을 수행 합니다.  
  
    1.  에 **설치 유형을** 페이지, 클릭 **역할 또는 기능 기반 설치**합니다.  
  
    2.  에 **서버 선택 페이지** (또는 **선택 대상 서버** Windows Server Essentials의 페이지)를 클릭 **서버 풀에서 서버를 선택**합니다.  
  
    3.  에 **기능** 페이지에서 확장 **원격 서버 관리 도구 (설치 됨)**, 확장 **원격 액세스 관리 도구 (설치 됨)**, 확장 **역할 관리 도구 (설치 됨)**, 확장 **원격 액세스 관리 도구**를 선택한 다음 **원격 액세스 GUI 및 명령줄 도구**합니다.  
  
    4.  마법사를 완료 하 고 지침을 따릅니다.  
  
##  <a name="BKMK_AddStaticIP"></a>2 단계:에서 고정 IP 주소를 서버 네트워크 어댑터 주소 변경  
 DirectAccess에서 고정 IP 주소와 어댑터가 필요합니다. 서버에서 로컬 네트워크 어댑터에 대 한 IP 주소를 변경 해야 합니다.  
  
#### <a name="to-add-a-static-ip-address"></a>고정 IP 주소를 추가 하려면  
  
1.  시작 페이지에 열고 **제어판**합니다.  
  
2.  클릭 **네트워크 및 인터넷**을 차례로 클릭 하 고 **네트워크 상태 및 작업 보기**합니다.  
  
3.  작업 창에서는 **네트워크 및 공유 센터**, 클릭 **어댑터 설정 변경**합니다.  
  
4.  로컬 네트워크 어댑터를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다.  
  
5.  에 **네트워킹** 탭을 클릭 **인터넷 프로토콜 버전 4 (TCP/IPv4)**을 차례로 클릭 하 고 **속성**합니다.  
  
6.  **일반** 탭을 클릭 **다음 IP 주소를 사용 하 여**를 선택한 다음 사용할 IP 주소를 입력 합니다.  
  
     기본값을 서브넷 마스크에 자동으로 표시 되는 **서브넷 마스크** 상자 합니다. 기본값, 하거나 사용 하려는 서브넷 마스크 값을 입력 합니다.  
  
7.  에 **기본 게이트웨이** 상자 기본 게이트웨이의 IP 주소를 입력 합니다.  
  
8.  에 **기본 설정 DNS 서버** 상자에 IP 주소 DNS 서버를 입력 합니다.  
  
    > [!NOTE]
    >  대신 루프백 네트워크 (예: 127.0.0.1) DHCP (예를 들어 192.168.X.X)가 네트워크 어댑터에 할당 된 IP 주소를 사용 합니다. 지정된 된 IP 주소를 확인 하려면 실행 **ipconfig** 명령 프롬프트에 있습니다.  
  
9. 에 **대체 DNS 서버** 상자에 있는 경우 대체 DNS 서버의 IP 주소를 입력 합니다.  
  
10. 클릭 **확인**을 차례로 클릭 하 고 **닫기**합니다.  
  
> [!IMPORTANT]
>  앞으로 포트 80 및 443 서버에 새로 고정 IP 주소를 라우터의 구성 있는지 확인 합니다.  
  
##  <a name="BKMK_DNS"></a>네트워크 위치 서버에 대 한 인증서 및 DNS 레코드를 준비 하는 3 단계:  
 인증서 및 DNS 레코드 네트워크 위치 서버에 대 한 준비를 다음 작업을 수행 합니다.  
  
-   [3a 단계: 웹 서버의 인증서 템플릿 인증 된 사용자에 게 전체 권한을 부여](#BKMK_GrantFullPermissions)  
  
-   [3b 단계: 외부 네트워크에서 확인할 수 있는 일반적인 이름의 네트워크 위치 서버에 대 한 인증서 등록](#BKMK_EnrollaCertificate)  
  
-   [3 단계: DNS 서버에서 새 호스트 추가 하 고 Windows Server Essentials 서버 주소에 매핑됩니다.](#BKMK_MapNewHosttoServerAddress)  
  
###  <a name="BKMK_GrantFullPermissions"></a>3a 단계: 웹 서버의 인증서 템플릿 인증 된 사용자에 게 전체 권한을 부여  
 첫 번째 작업 웹 서버의 인증서 템플릿 인증 기관에서 사용자를 인증 전체 권한을 부여 하는 것입니다.  
  
####  <a name="BKMK_ToGrantFullPermissions"></a>S 인증서 템플릿 웹 서버에 대 한 사용자가 인증 된 전체 사용 권한을 부여 하려면  
  
1.  에 **시작** 페이지를 열고 **인증 기관**합니다.  
  
2.  콘솔 트리에서 **인증 기관 (로컬)**, 확장 **< servername\ >-캐나다**를 마우스 오른쪽 단추로 클릭 **인증서 템플릿**, 클릭 한 다음 **관리**합니다.  
  
3.  **인증 기관 (로컬)**를 마우스 오른쪽 단추로 클릭 **웹 서버**을 차례로 클릭 하 고 **속성**합니다.  
  
4.  속성 웹 서버에서에서에 **보안** 탭을 클릭 **인증 된 사용자**선택 **모든 권한**, 클릭 한 다음 **확인**합니다.  
  
5.  다시 시작 **Active Directory 인증서 서비스**합니다. 제어판을 열고 **로컬 서비스 보고**합니다. 서비스의 목록에서 마우스 오른쪽 단추로 클릭 **Active Directory 인증서 서비스**을 차례로 클릭 하 고 **다시 시작**합니다.  
  
###  <a name="BKMK_EnrollaCertificate"></a>3b 단계: 외부 네트워크에서 확인할 수 있는 일반적인 이름의 네트워크 위치 서버에 대 한 인증서 등록  
 그런 다음, 외부 네트워크에서 확인할 수 있는 일반적인 이름의 네트워크 위치 서버에 대 한 인증서를 등록 합니다.  
  
####  <a name="BKMK_ToEnrollaCertificate"></a>네트워크 위치 서버에 대 한 인증서를 등록  
  
1.  에 **시작** 페이지를 열고 **mmc** (Microsoft Management Console)입니다.  
  
2.  경우에 **사용자 계정 컨트롤** 클릭 경고 메시지가 나타나면 **예**합니다.  
  
     Microsoft Management Console (MMC) 엽니다.  
  
3.  에 **파일** 메뉴를 클릭 **스냅인 추가/제거**합니다.  
  
4.  에 **원격 스냅인 추가 /** 상자를 클릭 **인증서**을 차례로 클릭 하 고 **추가**합니다.  
  
5.  에 **인증서 스냅인** 페이지, 클릭 **컴퓨터 계정**을 차례로 클릭 하 고 **다음**합니다.  
  
6.  에 **컴퓨터 선택** 페이지, 클릭 **로컬 컴퓨터**, 클릭 **완료**을 차례로 클릭 하 고 **확인**합니다.  
  
7.  콘솔 트리에서 **(로컬 컴퓨터) 인증서**, 확장 **개인**를 마우스 오른쪽 단추로 클릭 **인증서**를 선택한 다음 **모든 작업**, 클릭 **새 인증서를 요청**합니다.  
  
8.  인증서 등록이 마법사 나타나면 클릭 **다음**합니다.  
  
9. 에 **인증서 등록이 정책 선택** 페이지, 클릭 **다음**합니다.  
  
10. 에 **인증서를 요청** 페이지를 선택 하 고는 **웹 서버** 확인란을 선택한 다음 클릭 **자세한 정보는이 인증서 등록 해야**합니다.  
  
11. 에 **인증서 속성** 상자에 입력에 대해 다음 설정을 **주체 이름**:  
  
    1.  에 대 한 **종류**선택 **일반 이름**합니다.  
  
    2.  에 대 한 **값**네트워크 위치 서버 (예를 들어, DirectAccess-NLS.contoso.local)의 이름을 입력 하 고 클릭 한 다음 **추가**합니다.  
  
    3.  클릭 **확인**을 차례로 클릭 하 고 **등록**합니다.  
  
12. 인증서 등록이 완료 되 면 클릭 **완료**합니다.  
  
###  <a name="BKMK_MapNewHosttoServerAddress"></a>3 단계: 새 호스트 DNS 서버에 추가 하 고 Windows Server Essentials 서버 주소 지도  
 DNS 구성을 완료 새 호스트 DNS 서버에 추가 하 고 Windows Server Essentials 서버 주소 지도.  
  
####  <a name="BKMK_ToMapNewHosttoServerAddress"></a>Windows Server Essentials 서버 주소를 새 호스트 지도로  
  
1.  시작 화면 페이지에 DNS 관리자를 엽니다. 검색 DNS 관리자를 열려면 **dnsmgmt.msc**을 차례로 클릭 하 고 **dnsmgmt.msc** 검색 결과에서 합니다.  
  
2.  DNS 관리자 콘솔 트리에서 로컬 서버, **앞 조회 영역이**를 서버의 도메인 접미사 된 영역을 마우스 오른쪽 단추로 클릭 한 다음 **A 등의 AAAA 새 호스트**합니다.  
  
3.  이름 (예를 들어, DirectAccess NLS.contoso.local) 서버의 IP 주소 및 해당 (예를 들어 192.168.x.x) 서버 주소를 입력 합니다.  
  
4.  클릭 **호스트 추가**, 클릭 **확인**을 차례로 클릭 하 고 **완료**합니다.  
  
##  <a name="BKMK_AddSecurityGroup"></a>4 단계: DirectAccess 클라이언트 컴퓨터에 대 한 보안 그룹 만들기  
 그런 다음, DirectAccess 클라이언트 컴퓨터를 사용 하 여 보안 그룹을 만든 하 고 그룹에 컴퓨터 계정을 추가 합니다.  
  
#### <a name="to-add-a-security-group-for-client-computers-that-use-directaccess"></a>DirectAccess 사용 하는 클라이언트 컴퓨터에 대 한 보안 그룹을 추가 하려면  
  
1.  서버 관리자 대시보드에서 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 사용자와 컴퓨터**합니다.  
  
    > [!NOTE]
    >  표시 되지 않는 경우 **Active Directory 사용자와 컴퓨터** 에 **도구** 메뉴를 기능을 설치 해야 합니다. Active Directory 사용자 및 그룹을 설치 하려면 관리자 권한으로 다음 Windows PowerShell cmdlet 실행: `Install-WindowsFeature RSAT-ADDS-Tools`합니다. 자세한 내용은 참조 [설치 또는 제거 원격 서버 관리 도구 팩](https://technet.microsoft.com/library/cc730825.aspx)합니다.  
  
2.  콘솔 트리에서 확장 서버 마우스 오른쪽 단추로 클릭 하 고 **사용자**, 클릭 **새로**을 차례로 클릭 하 고 **그룹**합니다.  
  
3.  그룹 이름을 입력, 그룹 범위 및 그룹 종류 (보안 그룹을 만든)를 클릭 한 다음 **확인**합니다.  
  
 새로운 보안 그룹에 추가 되는 **사용자** 폴더 합니다.  
  
#### <a name="to-add-computer-accounts-to-the-security-group"></a>컴퓨터 계정 보안 그룹에 추가 하려면  
  
1.  서버 관리자 대시보드에서 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 사용자와 컴퓨터**합니다.  
  
2.  콘솔 트리에서 서버를 확장 한 다음 **사용자**합니다.  
  
3.  사용자 계정 및 서버에서 보안 그룹 목록에서 보안 그룹 DirectAccess를 위해 만든 마우스 단추로 클릭 한 다음 **속성**합니다.  
  
4.  에 **회원** 탭을 클릭 **추가**합니다.  
  
5.  대화 상자에서 이름 (;) 세미콜론 분리 그룹에 추가 하려면 컴퓨터 계정의 이름을 입력 합니다. 클릭 한 다음 **이름 확인**합니다.  
  
6.  컴퓨터 계정을 확인 한 후 클릭 **확인**합니다. 클릭 한 다음 **확인** 다시 합니다.  
  
> [!NOTE]
>  사용할 수도 있습니다는 **소속** 보안 그룹에 계정을 추가 하는 컴퓨터 계정 속성에서 탭 합니다.  
  
##  <a name="BKMK_EnableConfigureDA"></a>5 단계: 사용 및 DirectAccess 구성  
 을 사용 하도록 설정 및 Windows Server Essentials의 DirectAccess 구성 하려면 다음 단계를 완료 해야 합니다.  
  
-   [5a 단계: DirectAccess 원격 액세스 Management Console을 사용 하 여 사용](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
-   [5b 단계: RRAS GPO (Windows Server Essentials에만 해당)에 잘못 된 IPv6Prefix 제거](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
-   [5 단계: Windows 7 Enterprise DirectAccess 사용 하 여 실행 하는 클라이언트 컴퓨터를 사용 하도록 설정](#BKMK_Step4cWindows7Setup)  
  
-   [D 5 단계: 네트워크 위치 서버 구성](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
-   [5e 단계: 레지스트리 키 때를 무시 캘리포니아 인증 된 IPsec 채널을 설정 추가](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
###  <a name="BKMK_EnableDA"></a>5a 단계: DirectAccess 원격 액세스 Management Console을 사용 하 여 사용  
 이 섹션 Windows Server Essentials의 DirectAccess 수 있도록 단계별 지침을 제공 합니다. 하지 구성한 경우 VPN 서버의 아직,이 절차를 시작 하기 전에 수행 해야 합니다. 자세한 내용은 [관리 VPN](Manage-VPN-in-Windows-Server-Essentials.md)합니다.  
  
##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>DirectAccess 원격 액세스 Management Console을 사용 하 여 사용 하려면  
  
1.  시작 페이지에 열고 **원격 액세스 관리**합니다.  
  
2.  사용 DirectAccess 마법사에서 다음을 수행 합니다.  
  
    1.  리뷰 **DirectAccess 필수**를 클릭 하 고 **다음**합니다.  
  
    2.  에 **그룹 선택** 보안 그룹 DirectAccess 클라이언트에 대 한 이전에 만든 추가 탭 합니다. (보안 그룹 만들지 않은 경우 [4 단계: 컴퓨터 DirectAccess 클라이언트에 대 한 보안 그룹을 만든](#BKMK_AddSecurityGroup) 지침은.)  
  
    3.  에 **그룹 선택** 탭을 클릭 **모바일만 해당 컴퓨터에 대 한 사용 DirectAccess** 모바일 컴퓨터를 사용 하 여 DirectAccess 서버를 원격으로 액세스를 누른 사용 하려는 경우 **다음**합니다.  
  
    4.  **네트워크 토폴로지**토폴로지 서버를 선택한 다음 **다음**합니다.  
  
    5.  **DNS 접미사 검색 목록이**를 필요에 따라 추가 DNS 접미사 클라이언트 컴퓨터에 대 한 추가 클릭 한 다음 **다음**합니다.  
  
        > [!NOTE]
        >  기본적으로 활성화 DirectAccess 마법사 이미 DNS 접미사 현재 도메인에 대 한 추가 합니다. 그러나 필요한 경우 더 추가할 수 있습니다.  
  
    6.  적용 되 고 필요한 경우 수정 하는 그룹 정책 개체 (Gpo) 검토 합니다.  
  
    7.  클릭 **다음**을 차례로 클릭 하 고 **완료**합니다.  
  
    8.  고급 모드에서는 다음과 같은 Windows PowerShell 명령을 실행 하 여 원격 액세스 관리 서비스를 다시 시작 합니다.  
  
        ```powershell  
        Restart-Service RaMgmtSvc   
        ```  
  
###  <a name="BKMK_RemoveIPv6"></a>5b 단계: RRAS GPO (Windows Server Essentials에만 해당)에 잘못 된 IPv6Prefix 제거  
  이 섹션 Windows Server Essentials 실행 하는 서버에 적용 됩니다.  
  
 PowerShell을 관리자 권한으로 Windows를 열고 다음 명령을 실행 합니다.  
  
```powershell  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
```  
  
###  <a name="BKMK_Step4cWindows7Setup"></a>5 단계: Windows 7 Enterprise DirectAccess 사용 하 여 실행 하는 클라이언트 컴퓨터를 사용 하도록 설정  
 Windows 7 Enterprise를 실행 하는 클라이언트 컴퓨터를 사용 하는 경우 해당 컴퓨터에서 DirectAccess 사용 하도록 설정 하려면 다음 단계를 수행 합니다.  
  
##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>DirectAccess 사용 하 여 Windows 7 Enterprise 컴퓨터를 사용 하도록 설정 하려면  
  
1.  서버의 시작 페이지에 열고 **원격 액세스 관리**합니다.  
  
2.  원격 액세스 Management Console에서 클릭 **구성**합니다. 다음에 **설치 정보** 창, **2 단계**, 클릭 **편집**합니다.  
  
     원격 액세스 서버 설치 마법사를 엽니다.  
  
3.  에 **인증** 탭 합니다 (Windows Server Essentials 서버의 인증서를 선택할 수 있는) 신뢰할 수 있는 루트 인증서를 인증 기관 (캐나다) 인증서를 선택 합니다. 클릭 **DirectAccess 통해 연결 하기 위해 Windows 7 사용 클라이언트 컴퓨터**을 차례로 클릭 하 고 **다음**합니다.  
  
4.  마법사를 완료 하 고 지침을 따릅니다.  
  
> [!IMPORTANT]
>  Windows Server Essentials 서버 UR1 사전 설치 되어 제공 되지 않은 경우 통해 DirectAccess 연결 하는 Windows 7 Enterprise 컴퓨터에 대 한 알려진된 문제가 있습니다. 해당 환경에서 DirectAccess 연결을 사용 하려면 다음 단계를 수행 해야 합니다.  
>   
>  1.  설명에 핫픽스 설치 [Microsoft 기술 자료 문서 2796394](https://support.microsoft.com/kb/2796394) Windows Server Essentials 서버에 있습니다. 서버를 다시 시작 합니다.  
> 2.  다음에 설명 된 핫픽스 설치 [Microsoft 기술 자료 문서 2615847](https://support.microsoft.com/kb/2615847) 각 Windows 7 컴퓨터에서 합니다.  
>   
>      Windows Server Essentials에서이 문제가 해결 되었습니다.  
  
###  <a name="BKMK_NLS"></a>D 5 단계: 네트워크 위치 서버 구성  
 이 섹션에서 네트워크 위치 서버 구성 단계별 지침을 제공 합니다.  
  
> [!NOTE]
>  시작 하기 전에 < SystemDrive\ > \inetpub\wwwroot 폴더 내용 전체의 < SystemDrive\ > \Program Files\Windows Server\Bin\WebApps\Site\insideoutside 폴더에 복사 합니다. < SystemDrive\ > \Program Files\Windows Server\Bin\WebApps\Site\insideoutside 폴더로 < SystemDrive\ > \Program Files\Windows Server\Bin\WebApps\Site 폴더에서 default.aspx 파일을 복사도 합니다.  
  
##### <a name="to-configure-the-network-location-server"></a>네트워크 위치 서버 구성 하려면  
  
1.  시작 페이지에 열고 **원격 액세스 관리**합니다.  
  
2.  원격 액세스 Management Console에서 클릭 **구성**의 **원격 액세스 설치** 창에 자세히 설명 **3 단계**, 클릭 **편집**합니다.  
  
3.  원격 액세스 서버 설치 마법사에서에 **네트워크 위치 서버** 탭을 선택 하 고 **네트워크 위치 서버 원격 액세스 서버에 배포 될**, 다음 이전에 대해 발급 된 인증서를 선택 하 고 (에 [3 단계: 인증서 및 DNS 레코드 네트워크 위치 서버에 대 한 준비](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)).  
  
4.  마법사를 완료 하 고 클릭 한 다음 지침에 따라 **완료**합니다.  
  
###  <a name="BKMK_CA"></a>5e 단계: 레지스트리 키 때를 무시 캘리포니아 인증 된 IPsec 채널을 설정 추가  
 다음 단계 IPsec 채널을 설정할 때 캘리포니아 인증을 무시 하도록 서버 구성 하는 것입니다.  
  
##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>캘리포니아 인증 사용 하지 않으려면 레지스트리 키를 추가 하려면  
  
1.  시작 페이지에 열고 **regedit** (레지스트리 편집기).  
  
2.  레지스트리 편집기의 확장 **HKEY_LOCAL_MACHINE**, 확장 **시스템**, 확장 **CurrentControlSet**, 확장 **서비스**를 확장 하 고 **IKEEXT**합니다.  
  
3.  아래에서 **IKEEXT**를 마우스 오른쪽 단추로 클릭 **매개**, 클릭 **새로**, 클릭 한 다음 **(32 비트) 값 DWORD**합니다.  
  
4.  새로 추가 된 값을 이름 바꾸기 **ikeflags**합니다.  
  
5.  두 번 클릭 **ikeflags**설정는 **종류** 에 **16 진**, 값으로 설정 **8000**, 클릭 한 다음 **확인**합니다.  
  
> [!NOTE]
>  이 레지스트리 키를 추가 하려면 다음 Windows PowerShell 명령을 높은 모드에 사용할 수 있습니다.  
>   
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`  
  
##  <a name="BKMK_NRPT"></a>6 단계: 이름 해상도 정책 테이블 설정을 DirectAccess 서버에 대 한 구성  
 이 섹션 DirectAccess 클라이언트 gpo 내부 주소 (contoso.local 접미사는 예를 들어, 항목)에 대 한 이름 해상도 정책 테이블 (NPRT) 항목 편집 하기 위한 지침을 제공 하 고 IPHTTPS 인터페이스 주소를 설정 합니다.  
  
#### <a name="to-configure-name-resolution-policy-table-entries"></a>이름 해상도 정책 테이블 항목을 구성 하려면  
  
1.  시작 페이지에 열고 **그룹 정책 관리**합니다.  
  
2.  그룹 정책 관리 콘솔에서 기본 숲 및 도메인 클릭 마우스 오른쪽 단추로 클릭 **DirectAccess 클라이언트 설정**을 차례로 클릭 하 고 **편집**합니다.  
  
3.  클릭 **컴퓨터 구성**, 클릭 **정책**, 클릭 **Windows 설정**을 차례로 클릭 하 고 **이름 해결 정책**합니다. 사용자 DNS 접미사 동일 하 게 네임 있는 항목을 선택 하 고 클릭 한 다음 **규칙 편집**합니다.  
  
4.  클릭 하 고 **DirectAccess DNS 설정을** 탭 합니다. 다음 **이 규칙에 DirectAccess에 대 한 사용 하도록 설정 DNS 설정을**합니다. IP HTTPS 인터페이스 IPv6 주소 DNS 서버 목록에 추가 합니다.  
  
    > [!NOTE]
    >  다음 Windows PowerShell 명령을 IPv6 주소를 사용할 수 있습니다.  
    >   
    >  `(Get-NetIPInterface -InterfaceAlias IPHTTPSInterface | Get-NetIPAddress -PrefixLength 128)[1].IPAddress`  
  
##  <a name="BKMK_TCPUDP"></a>7 단계: UDP 및 TCP 방화벽 규칙 Gpo DirectAccess 서버에 대 한 구성  
 이 섹션 구성 UDP 및 TCP 방화벽 규칙 Gpo DirectAccess 서버에 대 한 단계별 지침을 제공 합니다.  
  
#### <a name="to-configure-firewall-rules"></a>방화벽 규칙 구성 하려면  
  
1.  시작 페이지에 열고 **그룹 정책 관리**합니다.  
  
2.  그룹 정책 관리 콘솔에서 기본 숲 및 도메인 클릭 마우스 오른쪽 단추로 클릭 **DirectAccess 서버 설정**을 차례로 클릭 하 고 **편집**합니다.  
  
3.  클릭 **컴퓨터 구성**, 클릭 **정책**, 클릭 **Windows 설정**, 클릭 **보안 설정**, 클릭 **고급 보안와 Windows 방화벽**, 다음 수준 클릭 **고급 보안와 Windows 방화벽**를 차례로 클릭 하 고 **돌아오는 규칙**합니다. 마우스 오른쪽 단추로 클릭 **도메인 이름 (TCP에서) 서버**을 차례로 클릭 하 고 **속성**합니다.  
  
4.  클릭는 **범위** 탭의는 **로컬 IP 주소** 목록에서 IP HTTPS 인터페이스 IPv6 주소를 추가 합니다.  
  
5.  반복 같은 절차 **도메인 이름 서버 (UDP에서)**합니다.  
  
##  <a name="BKMK_DNS64"></a>8 단계: IP HTTPS 인터페이스를 듣기 시작 DNS64 구성을 변경합니다  
 다음 Windows PowerShell 명령을 사용 하 여 IP HTTPS 인터페이스를 듣기 시작 DNS64 구성을 변경 해야 합니다.  
  
```powershell  
Set-NetDnsTransitionConfiguration  �AcceptInterface IPHTTPSInterface  
```  
  
##  <a name="BKMK_ExemptPort"></a>예약 WinNat 서비스에 대 한 포트 9 단계:  
 다음 Windows PowerShell 명령을 사용 하 여 WinNat 서비스에 대 한 포트 예약 합니다. Windows Server Essentials 서버 실제 IPv4 주소 "192.168.1.100을" 바꿉니다.  
  
```powershell  
Set-NetNatTransitionConfiguration  �IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
```  
  
> [!IMPORTANT]
>  포트 응용 프로그램와 충돌을 방지 하려면 WinNat 서비스에 대 한 예약 포트 범위 포트 6602 포함 되지 않습니다 해야 합니다.  
  
##  <a name="BKMK_WinNAT"></a>10 단계: WinNat 서비스를 다시 시작  
 다음 Windows PowerShell 명령을 실행 하 여 Windows NAT 드라이버 (WinNat) 서비스를 다시 시작 합니다.  
  
```powershell  
Restart-Service winnat  
```  
  
##  <a name="BKMK_AppendixBPowerShellScript"></a>부록: Windows PowerShell를 사용 하 여 DirectAccess 설정  
 이 섹션을 설정 하 고 Windows PowerShell를 사용 하 여 DirectAccess 구성 하는 방법을 설명 합니다.  
  
### <a name="preparation"></a>준비  
 DirectAccess에 대 한 서버 구성 시작 하기 전에 다음을 완료 해야 합니다.  
  
1.  절차에 따라 [3 단계: 인증서 및 DNS 레코드 네트워크 위치 서버에 대 한 준비](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS) 라는 인증서를 등록 **DirectAccess NLS.contoso.com** (여기서 **contoso.com** 실제 내부 도메인 이름으로 바뀝니다), 네트워크 위치 서버 (NLS)에 대 한 DNS 레코드를 추가 하 고 있습니다.  
  
2.  라는 보안 그룹 추가 **DirectAccessClients** Active Directory에 다음 DirectAccess 기능을 제공 하려는 클라이언트 컴퓨터를 추가 하 고 있습니다. 자세한 내용은 참조 [4 단계: 컴퓨터 DirectAccess 클라이언트에 대 한 보안 그룹을 만든](#BKMK_AddSecurityGroup)합니다.  
  
### <a name="commands"></a>명령  
  
> [!IMPORTANT]
>  Windows Server Essentials 불필요 한 IPv6 접두사 GPO 제거 필요가 없습니다. 다음 레이블이 코드 섹션 삭제: `# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`합니다.  
  
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
  
## <a name="see-also"></a>참조 하십시오  
  
-   [액세스를 어디서 나 관리](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
