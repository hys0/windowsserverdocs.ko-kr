---
title: 6 설치 단계 및 2-DC1 구성
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d66901a-c40b-474c-9948-f989f399cfea
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4f31c0e1d36ff458fb4807ab6856a56498f449ab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838184"
---
# <a name="step-6-install-and-configure-2-dc1"></a>6 설치 단계 및 2-DC1 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

2-DC1 다음 서비스를 제공 합니다.  
  
-   Corp2.corp.contoso.com Active Directory Domain Services (AD DS) 도메인에 대 한 도메인 컨트롤러입니다.  
  
-   Corp2.corp.contoso.com DNS 도메인에 대 한 DNS 서버입니다.  
  
2-DC1 구성 중 구성 됩니다.  
  
- 2-DC1에서 운영 체제를 설치 합니다.
  
- TCP/IP 속성을 구성합니다.

- 2-DC1을 도메인 컨트롤러 및 DNS 서버 구성

- CORP\User1에 그룹 정책 사용 권한 제공
  
- CORP2 컴퓨터 컴퓨터 인증서를 가져올 수 있도록 허용
  
- 강제로 DC1 사이의 2-DC1 복제
  
## <a name="install-the-operating-system-on-2-dc1"></a>2-DC1에서 운영 체제를 설치 합니다.  
첫째, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 설치 합니다.  
  
### <a name="to-install-the-operating-system-on-2-dc1"></a>2-DC1에서 운영 체제를 설치 하려면  
  
1.  Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012의 설치를 시작 합니다.  
  
2.  Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 (전체 설치) 및 로컬 관리자 계정의 강력한 암호를 지정 하 여 설치를 완료 하려면 지침을 따릅니다. 로컬 관리자 계정을 사용하여 로그온합니다.  
  
3.  인터넷에 연결 하는 네트워크에 2-DC1을 연결 하 고 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012에 대 한 최신 업데이트를 설치 하 고 인터넷에서 연결을 해제 하려면 Windows Update를 실행 합니다.  
  
4.  2-DC1 2 Corpnet 서브넷에 연결 합니다.  
  
## <a name="configure-tcpip-properties"></a>TCP/IP 속성을 구성합니다.  
고정 IP 주소를 사용 하 여 TCP/IP 프로토콜을 구성 합니다.  
  
### <a name="to-configure-tcpip-on-2-dc1"></a>2-DC1에 TCP/IP를 구성 하려면  
  
1.  서버 관리자 콘솔에서 클릭 **로컬 서버**를 선택한 다음는 **속성** 영역에서 다음을 **유선 이더넷 연결**, 링크를 클릭 합니다.  
  
2.  **네트워크 연결**에서 **유선 이더넷 연결**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **Internet Protocol Version 4(TCP/IPv4)** 를 클릭하고 **속성**을 클릭합니다.  
  
4.  **다음 IP 주소 사용**을 클릭합니다. **IP 주소**, 형식 **10.2.0.1**합니다. **서브넷 마스크**에 **255.255.255.0**을 입력합니다. **기본 게이트웨이**, 형식 **10.2.0.254**합니다. 클릭 **다음 DNS 서버 주소를 사용 하 여**의 **기본 설정 DNS 서버**, 유형 **10.2.0.1**, 및 **대체 DNS 서버**, 형식 **10.0.0.1**합니다.  
  
5.  **고급**을 클릭하고 **DNS** 탭을 클릭합니다.  
  
6.  **이 연결에 대 한 DNS 접미사**, 형식 **corp2.corp.contoso.com**를 클릭 하 고 **확인** 두 번입니다.  
  
7.  **인터넷 프로토콜 버전 6(TCP/IPv6)**, **속성**을 차례로 클릭합니다.  
  
8.  클릭 **다음 IPv6 주소를 사용 하 여**입니다. **IPv6 주소**, 형식 **2001:db8:2::1**합니다. **서브넷 접두사 길이**, 형식 **64**합니다. **기본 게이트웨이**, 형식 **2001:db8:2::fe**합니다. 클릭 **다음 DNS 서버 주소를 사용 하 여**의 **기본 설정 DNS 서버**, 유형 **2001:db8:2::1**, 및 **대체 DNS 서버**, 형식 **2001:db8:1::1**합니다.  
  
9. **고급**을 클릭하고 **DNS** 탭을 클릭합니다.  
  
10. **이 연결에 대 한 DNS 접미사**, 형식 **corp2.corp.contoso.com**를 클릭 하 고 **확인** 두 번입니다.  
  
11. 에 **유선 이더넷 연결 속성** 대화 상자, 클릭 **닫기**합니다.  
  
12. **네트워크 연결** 창을 닫습니다.  
  
13. 서버 관리자 콘솔에서의 **로컬 서버**를 **속성** 영역에서 다음을 **컴퓨터 이름**, 링크를 클릭 합니다.  
  
14. **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
15. 에 **컴퓨터 이름/도메인 변경** 대화 상자의 **컴퓨터 이름**, 유형 **2-DC1**를 클릭 하 고 **확인**합니다.  
  
16. 컴퓨터를 다시 시작해야 한다는 메시지가 표시되면 **확인**을 클릭합니다.  
  
17. **시스템 속성** 대화 상자에서 **닫기**를 클릭합니다.  
  
18. 컴퓨터를 다시 시작할지 묻는 메시지가 표시되면 **지금 다시 시작**을 클릭합니다.  
  
19. 를 다시 시작 하면 로컬 관리자 계정을 사용 하 여 로그인 합니다.  
  
## <a name="configure-2-dc1-as-a-domain-controller-and-dns-server"></a>2-DC1을 도메인 컨트롤러 및 DNS 서버 구성  
Corp2.corp.contoso.com 도메인에 대 한 도메인 컨트롤러 및 corp2.corp.contoso.com DNS 도메인에 대 한 DNS 서버로 2-DC1을 구성 합니다.  
  
### <a name="to-configure-2-dc1-as-a-domain-controller-and-dns-server"></a>2-DC1 도메인 컨트롤러 및 DNS 서버를 구성 하려면  
  
1.  서버 관리자 콘솔에서에 **대시보드**, 클릭 **역할 및 기능 추가**합니다.  
  
2.  클릭 **다음** 하 여 서버 역할 선택 화면을 세 번  
  
3.  에 **서버 역할 선택** 페이지에서 선택 **Active Directory Domain Services**합니다. 클릭 **기능 추가** 메시지가 표시 되 고 클릭 **다음** 3 번입니다.  
  
4.  **설치 선택 확인** 페이지에서 **설치**를 클릭합니다.  
  
5.  설치가 성공적으로 완료 되 면 클릭 **이 서버를 도메인 컨트롤러로 승격**합니다.  
  
6.  Active Directory 도메인 서비스 구성 마법사에 **배포 구성** 페이지에서 **기존 포리스트에 새 도메인을 추가**합니다.  
  
7.  **부모 도메인 이름**, 형식 **corp.contoso.com**의 **새 도메인 이름**, 형식 **corp2**합니다.  
  
8.  아래에서 **이 작업을 수행 하는 자격 증명**, 클릭 **변경**합니다. 에 **Windows 보안** 대화 상자의 **사용자 이름**, 유형 **corp.contoso.com\Administrator**, 및 **암호**는 corp\ 입력 관리자 암호를 클릭 **확인**를 클릭 하 고 **다음**합니다.  
  
9. 에 **도메인 컨트롤러 옵션** 페이지에서 확인 합니다 **사이트 이름** 는 **두 번째-사이트**합니다. 아래 **디렉터리 서비스 복원 모드 (DSRM) 암호 입력**의 **암호** 하 고 **암호 확인**를 입력 한 강력한 암호를 두 번 클릭  **다음** 5 번입니다.  
  
10. 에 **필수 구성 요소 확인** 페이지에서 필수 구성 요소가 확인 되 면 클릭 **설치**합니다.  
  
11. 마법사가 Active Directory 및 DNS 서비스의 구성을 완료 될 때까지 기다린 다음 클릭 **닫기**합니다.  
  
12. 컴퓨터를 다시 시작한 후에 로그인 CORP2 도메인 관리자 계정을 사용 합니다.  
  
## <a name="provide-group-policy-permissions-to-corpuser1"></a>CORP\User1에 그룹 정책 사용 권한 제공  
CORP\User1 사용자를 만들고 corp2 그룹 정책 개체를 변경 하려면 전체 권한에 제공 하려면이 절차를 따르십시오.  
  
### <a name="to-provide-group-policy-permissions"></a>그룹 정책 사용 권한 제공  
  
1.  에 **시작** 화면에서 입력**gpmc.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  그룹 정책 관리 콘솔을 엽니다 **포리스트: corp.contoso.com/Domains/corp2.corp.contoso.com**합니다.  
  
3.  세부 정보 창에서 클릭 합니다 **위임** 탭 합니다. 에 **사용 권한** 드롭 다운 목록에서 클릭 **Gpo 링크**합니다.  
  
4.  클릭 **추가**, 및 새 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 클릭 **위치**합니다.  
  
5.  에 **위치** 대화 상자의 합니다 **위치** 트리를 클릭 **corp.contoso.com**, 클릭 **확인**합니다.  
  
6.  **선택할 개체 이름 입력** 형식 **User1**, 클릭 **확인**, 및를 **그룹 또는 사용자 추가** 대화 상자에서 클릭 **확인** .  
  
7.  트리에서 그룹 정책 관리 콘솔에서 클릭 **그룹 정책 개체**, 세부 정보 창 클릭 합니다 **위임** 탭 합니다.  
  
8.  클릭 **추가**, 및 새 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 클릭 **위치**합니다.  
  
9. 에 **위치** 대화 상자의 합니다 **위치** 트리를 클릭 **corp.contoso.com**, 클릭 **확인**합니다.  
  
10. **선택할 개체 이름 입력** 형식을 **User1**, 클릭 **확인**합니다.  
  
11. 트리에서 그룹 정책 관리 콘솔에서 클릭 **WMI 필터**, 세부 정보 창 클릭 합니다 **위임** 탭 합니다.  
  
12. 클릭 **추가**, 및 새 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 클릭 **위치**합니다.  
  
13. 에 **위치** 대화 상자의 합니다 **위치** 트리를 클릭 **corp.contoso.com**, 클릭 **확인**합니다.  
  
14. **선택할 개체 이름 입력** 형식을 **User1**, 클릭 **확인**합니다. 에 **그룹 또는 사용자 추가** 대화 상자에서 확인 **사용 권한** 로 설정 됩니다 **모든 권한**를 클릭 하 고 **확인**.  
  
15. 그룹 정책 관리 콘솔을 닫습니다.  
  
## <a name="allow-corp2-computers-to-obtain-computer-certificates"></a>CORP2 컴퓨터 컴퓨터 인증서를 가져올 수 있도록 허용 

CORP2 도메인에서 컴퓨터 APP1의 인증 기관에서 컴퓨터 인증서를 가져와야 합니다. APP1에서이 절차를 수행 합니다.  
  
### <a name="to-allow-corp2-computers-to-automatically-obtain-computer-certificates"></a>컴퓨터 인증서를 자동으로 가져오려고 CORP2 컴퓨터 수 있도록  
  
1.  APP1에서 클릭 **시작**, 형식 **certtmpl.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  에 **인증서 템플릿 콘솔**, 가운데 창에서 두 번 클릭 **Client-server Authentication**합니다.  
  
3.  에 **Client-server Authentication 속성** 대화 상자에서 클릭 합니다 **보안** 탭.  
  
4.  클릭 **추가**, 및에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 클릭 **위치**합니다.  
  
5.  에 **위치** 대화 상자의 **위치**를 확장 하 고 **corp.contoso.com**, 클릭 **corp2.corp.contoso.com**, 클릭하고 **확인**합니다.  
  
6.  **선택할 개체 이름을 입력 하십시오**, 형식 **Domain Admins; 도메인 컴퓨터** 을 클릭 한 다음 **확인**합니다.  
  
7.  에 **Client-server Authentication 속성** 대화 상자의 **그룹 또는 사용자 이름**, 클릭 **Domain Admins (CORP2\Domain Admins)**, 및  **Domain Admins의 권한**를 **허용** 열을 선택 **작성** 하 고 **등록**.  
  
8.  **그룹 또는 사용자 이름**, 클릭 **도메인 컴퓨터 (CORP2\Domain 컴퓨터)**, 및 **도메인 컴퓨터에 대 한 권한을**를 **허용**열을 선택 **등록** 하 고 **자동 등록**를 클릭 하 고 **확인**합니다.  
  
9. 인증서 템플릿 콘솔을 닫습니다.  
  
## <a name="replication"></a>강제로 DC1 사이의 2-DC1 복제  
2-EDGE1에 대 한 인증서를 등록 하려면 먼저 2-DC1 DC1에서 설정의 복제를 하도록 해야 합니다. DC1에서이 작업을 수행 해야 합니다.  
  
### <a name="to-force-replication"></a>복제  
  
1.  Dc1 **시작**를 클릭 하 고 **Active Directory 사이트 및 서비스**합니다.  
  
2.  Active Directory 사이트 및 서비스 콘솔 트리에서 **사이트 간 전송**를 클릭 하 고 **IP**입니다.  
  
3.  세부 정보 창에서 두 번 클릭 **DEFAULTIPSITELINK**합니다.  
  
4.  에 **DEFAULTIPSITELINK 속성** 대화 상자의 **비용**, 형식 **1**의 **복제 마다**, 형식 **15**를 클릭 하 고 **확인**합니다. 15 분 동안 복제가 완료 될 때까지 기다립니다.  
  
5.  콘솔 트리에서 이제 복제를 강제 적용 하려면 확장 **Sites\Default-첫 번째-사이트-name\Servers\DC1\NTDS 설정을**, 세부 정보 창에서 마우스 오른쪽 단추로 클릭 **<automatically generated>**, 클릭  **지금 복제**, 한 후 합니다 **지금 복제** 대화 상자, 클릭 **확인**합니다.  
  
6.  복제를 성공적으로 완료 되었는지 확인 하려면 다음을 수행 합니다.  
  
    1.  에 **시작** 화면에서 입력**cmd.exe**, 한 다음 ENTER를 누릅니다.  
  
    2.  다음 명령을 입력한 후 Enter 키를 누릅니다.  
  
        ```  
        repadmin /syncall /e /A /P /d /q  
        ```  
  
    3.  오류 없이 모든 파티션에 동기화 되는지 확인 합니다. 그러지 않으면 계속 진행 하기 전에 보고 된 오류가 없는 될 때까지 다음 명령을 다시 실행 합니다.  
  
7.  명령 프롬프트 창을 닫습니다.  
  


