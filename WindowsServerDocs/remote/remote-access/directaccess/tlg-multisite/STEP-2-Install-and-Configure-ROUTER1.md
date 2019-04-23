---
title: 2 설치 단계 및 ROUTER1 구성
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
ms.assetid: dc20b1a0-540d-4531-a176-50b87c071600
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6a771b5eb8587d23bc67a7e7769264251afdb5bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838514"
---
# <a name="step-2-install-and-configure-router1"></a>2 설치 단계 및 ROUTER1 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 멀티 사이트 테스트 랩 가이드에서는 IP-HTTPS 및 Teredo 트래픽에 라우터 역할 및 라우터 컴퓨터가 Corpnet 및 2 Corpnet 서브넷에는 IPv4 및 IPv6 연결을 제공 합니다.  
  
- ROUTER1 운영 체제 설치 
  
- TCP/IP 속성을 구성 하 고 컴퓨터 이름 바꾸기  
  
- 방화벽을 해제
  
- 라우팅 및 전달을 구성 합니다.
  
## <a name="install-the-operating-system-on-router1"></a>ROUTER1 운영 체제 설치  
첫째, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 설치 합니다.  
  
### <a name="to-install-the-operating-system-on-router1"></a>ROUTER1에 운영 체제를 설치 하려면  
  
1.  Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 (전체 설치)의 설치를 시작 합니다.  
  
2.  지침에 따라 설치를 완료하고 로컬 관리자 계정에 강력한 암호를 지정합니다. 로컬 관리자 계정을 사용하여 로그온합니다.  
  
3.  ROUTER1 인터넷에 연결 하는 네트워크에 연결 하 고 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012에 대 한 최신 업데이트를 설치 하 고 인터넷에서 연결을 해제 하려면 Windows Update를 실행 합니다.  
  
4.  ROUTER1 Corpnet 및 2 Corpnet 서브넷에 연결 합니다.  
  
## <a name="configure-tcpip-properties-and-rename-the-computer"></a>TCP/IP 속성을 구성 하 고 컴퓨터 이름 바꾸기  
라우터에서 TCP/IP 설정을 구성 하 고 ROUTER1에 컴퓨터를 이름을 바꿉니다.  
  
### <a name="to-configure-tcpip-properties-and-rename-the-computer"></a>TCP/IP 속성을 구성 하는 컴퓨터의 이름을 바꾸려면  
  
1.  서버 관리자 콘솔에서 클릭 **로컬 서버**를 선택한 다음는 **속성** 영역에서 다음을 **유선 이더넷 연결**, 링크를 클릭 합니다.  
  
2.  에 **네트워크 연결** 창 Corpnet에 연결 된 네트워크 어댑터를 마우스 오른쪽 단추로 클릭, 클릭 **이름 바꾸기**, 형식 **Corpnet**, ENTER 키를 누릅니다.  
  
3.  마우스 오른쪽 단추로 클릭 **Corpnet**를 클릭 하 고 **속성**합니다.  
  
4.  **Internet Protocol Version 4(TCP/IPv4)** 를 클릭하고 **속성**을 클릭합니다.  
  
5.  **다음 IP 주소 사용**을 클릭합니다. **IP 주소**, 형식 **10.0.0.254**합니다. **서브넷 마스크**, 형식 **255.255.255.0**를 클릭 하 고 **확인**합니다.  
  
6.  **인터넷 프로토콜 버전 6(TCP/IPv6)**, **속성**을 차례로 클릭합니다.  
  
7.  클릭 **다음 IPv6 주소를 사용 하 여**입니다. **IPv6 주소**, 형식 **2001:db8:1::fe**합니다. **서브넷 접두사 길이**, 형식 **64**를 클릭 하 고 **확인**합니다.  
  
8.  에 **Corpnet 속성** 대화 상자 클릭 **닫기**합니다.  
  
9. 에 **네트워크 연결** 창 2 Corpnet에 연결 된 네트워크 어댑터를 마우스 오른쪽 단추로 클릭, 클릭 **이름 바꾸기**, 형식 **2 Corpnet**, ENTER 키를 누릅니다.  
  
10. 마우스 오른쪽 단추로 클릭 **2 Corpnet**를 클릭 하 고 **속성**합니다.  
  
11. **Internet Protocol Version 4(TCP/IPv4)** 를 클릭하고 **속성**을 클릭합니다.  
  
12. **다음 IP 주소 사용**을 클릭합니다. **IP 주소**, 형식 **10.2.0.254**합니다. **서브넷 마스크**, 형식 **255.255.255.0**를 클릭 하 고 **확인**합니다.  
  
13. **인터넷 프로토콜 버전 6(TCP/IPv6)**, **속성**을 차례로 클릭합니다.  
  
14. 클릭 **다음 IPv6 주소를 사용 하 여**입니다. **IPv6 주소**, 형식 **2001:db8:2::fe**합니다. **서브넷 접두사 길이**, 형식 **64**를 클릭 하 고 **확인**합니다.  
  
15. 에 **2 Corpnet 속성** 대화 상자 클릭 **닫기**합니다.  
  
16. **네트워크 연결** 창을 닫습니다.  
  
17. 서버 관리자 콘솔에서의 **로컬 서버**를 **속성** 영역에서 다음을 **컴퓨터 이름**, 링크를 클릭 합니다.  
  
18. **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
19. 에 **컴퓨터 이름/도메인 변경** 대화 상자의 **컴퓨터 이름**, 유형 **ROUTER1**를 클릭 하 고 **확인**합니다.  
  
20. 컴퓨터를 다시 시작해야 한다는 메시지가 표시되면 **확인**을 클릭합니다.  
  
21. **시스템 속성** 대화 상자에서 **닫기**를 클릭합니다.  
  
22. 컴퓨터를 다시 시작할지 묻는 메시지가 표시되면 **지금 다시 시작**을 클릭합니다.  
  
23. 컴퓨터를 다시 시작한 후 로컬 관리자 계정으로 로그온 합니다.  
  
## <a name="turn-off-the-firewall"></a>방화벽을 해제  
Corpnet 및 2 Corpnet 서브넷; 간의 라우팅을 제공 하기 위해서만이 컴퓨터는 구성 따라서 방화벽을 해제 해야 합니다.  
  
### <a name="to-turn-off-the-firewall"></a>방화벽을 해제 하려면  
  
1.  에 **시작** 화면에서 입력**wf.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  고급 보안이 포함 된 Windows 방화벽에서에 **작업** 창 클릭 **속성**합니다.  
  
3.  에 **Windows Firewall with Advanced Security** 대화 상자의 합니다 **도메인 프로필** 탭의 **방화벽 상태**, 클릭 **해제**합니다.  
  
4.  에 **Windows Firewall with Advanced Security** 대화 상자의 합니다 **개인 프로필** 탭의 **방화벽 상태**, 클릭 **해제**합니다.  
  
5.  에 **고급 보안이 포함 된 Windows 방화벽** 대화 상자의 합니다 **공개 프로필** 탭의 **방화벽 상태**, 클릭 **해제**, 차례로 클릭 **확인**합니다.  
  
6.  고급 보안이 포함 된 Windows 방화벽을 닫습니다.  
  
## <a name="configure-routing-and-forwarding"></a>라우팅 및 전달을 구성 합니다.  
라우팅 및 전달을 Corpnet 및 2 Corpnet 서브넷 간에 서비스를 제공 하려면 네트워크 인터페이스에서 전달을 사용 하도록 설정 하 고 서브넷 간의 고정 경로 구성 해야 합니다.  
  
### <a name="to-configure-static-routes"></a>고정 경로 구성 하려면  
  
1.  에 **시작** 화면에서 입력**cmd.exe**, 한 다음 ENTER를 누릅니다.  
  
2.  다음 명령을 사용 하 여 두 네트워크 어댑터의 IPv4와 IPv6 인터페이스에서 전달을 사용 하도록 설정 합니다. 각 명령을 입력 한 후 enter 키를 누릅니다.  
  
    ```  
    netsh interface IPv4 set interface Corpnet forwarding=enabled  
    netsh interface IPv4 set interface 2-Corpnet forwarding=enabled  
    netsh interface IPv6 set interface Corpnet forwarding=enabled  
    netsh interface IPv6 set interface 2-Corpnet forwarding=enabled  
    ```  
  
3.  IP-HTTPS Corpnet 및 2 Corpnet 서브넷 간 라우팅을 활성화 합니다.  
  
    ```  
    netsh interface IPv6 add route 2001:db8:1:1000::/59 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:db8:2:2000::/59 2-Corpnet 2001:db8:2::20  
    ```  
  
4.  Teredo Corpnet 및 2 Corpnet 서브넷 간 라우팅을 활성화 합니다.  
  
    ```  
    netsh interface IPv6 add route 2001:0:836b:2::/64 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:0:836b:14::/64 2-Corpnet 2001:db8:2::20  
    ```  
  
5.  명령 프롬프트 창을 닫습니다.
