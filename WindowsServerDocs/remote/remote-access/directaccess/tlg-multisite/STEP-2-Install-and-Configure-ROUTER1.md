---
title: 2 단계 ROUTER1 설치 및 구성
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc20b1a0-540d-4531-a176-50b87c071600
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 3cd73f1a5e2612f4551be1f16e49e9645c5e12c0
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308740"
---
# <a name="step-2-install-and-configure-router1"></a>2 단계 ROUTER1 설치 및 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 멀티 사이트 테스트 랩 가이드에서 라우터 컴퓨터는 Corpnet 및 Corpnet 서브넷 간에 IPv4 및 IPv6 브리지를 제공 하 고 IP-HTTPS 및 Teredo 트래픽에 대 한 라우터 역할을 합니다.  
  
- ROUTER1에 운영 체제 설치 
  
- TCP/IP 속성 구성 및 컴퓨터 이름 바꾸기  
  
- 방화벽 해제
  
- 라우팅 및 전달 구성
  
## <a name="install-the-operating-system-on-router1"></a>ROUTER1에 운영 체제 설치  
먼저 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 설치 합니다.  
  
### <a name="to-install-the-operating-system-on-router1"></a>ROUTER1에 운영 체제를 설치 하려면  
  
1.  Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 (전체 설치) 설치를 시작 합니다.  
  
2.  지침에 따라 설치를 완료하고 로컬 관리자 계정에 강력한 암호를 지정합니다. 로컬 관리자 계정을 사용하여 로그온합니다.  
  
3.  인터넷에 액세스할 수 있는 네트워크에 ROUTER1을 연결 하 고 Windows 업데이트를 실행 하 여 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012의 최신 업데이트를 설치한 다음 인터넷에서 연결을 끊습니다.  
  
4.  ROUTER1을 Corpnet 및 2 Corpnet 서브넷에 연결 합니다.  
  
## <a name="configure-tcpip-properties-and-rename-the-computer"></a>TCP/IP 속성 구성 및 컴퓨터 이름 바꾸기  
라우터에서 TCP/IP 설정을 구성 하 고 컴퓨터의 이름을 ROUTER1으로 바꿉니다.  
  
### <a name="to-configure-tcpip-properties-and-rename-the-computer"></a>TCP/IP 속성을 구성 하 고 컴퓨터의 이름을 바꾸려면  
  
1.  서버 관리자 콘솔에서 **로컬 서버**를 클릭 한 다음 **속성** 영역에서 **유선 이더넷 연결**옆에 있는 링크를 클릭 합니다.  
  
2.  **네트워크 연결** 창에서 Corpnet에 연결 된 네트워크 어댑터를 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 한 다음 **CORPNET**를 입력 하 고 enter 키를 누릅니다.  
  
3.  **Corpnet**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
4.  **Internet Protocol Version 4(TCP/IPv4)** 를 클릭하고 **속성**을 클릭합니다.  
  
5.  **다음 IP 주소 사용**을 클릭합니다. **IP 주소**에 **10.0.0.254**를 입력 합니다. **서브넷 마스크**에 **255.255.255.0**을 입력 한 다음 **확인**을 클릭 합니다.  
  
6.  **인터넷 프로토콜 버전 6(TCP/IPv6)** , **속성**을 차례로 클릭합니다.  
  
7.  **다음 IPv6 주소 사용을**클릭 합니다. **IPv6 주소**에 **2001: db8:1:: fe**를 입력 합니다. **서브넷 접두사 길이**에서 **64**를 입력 한 다음 **확인**을 클릭 합니다.  
  
8.  **Corpnet 속성** 대화 상자에서 **닫기**를 클릭 합니다.  
  
9. **네트워크 연결** 창에서 Corpnet에 연결 된 네트워크 어댑터를 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 한 다음 **2-CORPNET**를 입력 하 고 enter 키를 누릅니다.  
  
10. **Corpnet**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
11. **Internet Protocol Version 4(TCP/IPv4)** 를 클릭하고 **속성**을 클릭합니다.  
  
12. **다음 IP 주소 사용**을 클릭합니다. **IP 주소**에 **10.2.0.254**를 입력 합니다. **서브넷 마스크**에 **255.255.255.0**을 입력 한 다음 **확인**을 클릭 합니다.  
  
13. **인터넷 프로토콜 버전 6(TCP/IPv6)** , **속성**을 차례로 클릭합니다.  
  
14. **다음 IPv6 주소 사용을**클릭 합니다. **IPv6 주소**에 **2001: db8:2:: fe**를 입력 합니다. **서브넷 접두사 길이**에서 **64**를 입력 한 다음 **확인**을 클릭 합니다.  
  
15. **Corpnet 속성** 대화 상자에서 **닫기**를 클릭 합니다.  
  
16. **네트워크 연결** 창을 닫습니다.  
  
17. 서버 관리자 콘솔의 **로컬 서버**에 있는 **속성** 영역에서 **컴퓨터 이름**옆에 있는 링크를 클릭 합니다.  
  
18. **시스템 속성** 대화 상자의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.  
  
19. **컴퓨터 이름/도메인 변경** 대화 상자의 **컴퓨터 이름**에 **ROUTER1**을 입력 한 다음 **확인**을 클릭 합니다.  
  
20. 컴퓨터를 다시 시작해야 한다는 메시지가 표시되면 **확인**을 클릭합니다.  
  
21. **시스템 속성** 대화 상자에서 **닫기**를 클릭합니다.  
  
22. 컴퓨터를 다시 시작할지 묻는 메시지가 표시되면 **지금 다시 시작**을 클릭합니다.  
  
23. 컴퓨터가 다시 시작 되 면 로컬 관리자 계정으로 로그온 합니다.  
  
## <a name="turn-off-the-firewall"></a>방화벽 해제  
이 컴퓨터는 Corpnet 및 2 Corpnet 서브넷 간의 라우팅을 제공 하도록 구성 됩니다. 따라서 방화벽이 꺼져 있어야 합니다.  
  
### <a name="to-turn-off-the-firewall"></a>방화벽을 해제 하려면  
  
1.  **시작** 화면에서**wf**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  고급 보안이 포함 된 Windows 방화벽의 **동작** 창에서 **속성**을 클릭 합니다.  
  
3.  **고급 보안이 설정 된 Windows 방화벽** 대화 상자의 **도메인 프로필** 탭에 있는 **방화벽 상태**에서 **끄기**를 클릭 합니다.  
  
4.  **고급 보안이 설정 된 Windows 방화벽** 대화 상자의 **개인 프로필** 탭에 있는 **방화벽 상태**에서 **끄기**를 클릭 합니다.  
  
5.  **고급 보안이 설정 된 Windows 방화벽** 대화 상자의 **공용 프로필** 탭에 있는 **방화벽 상태**에서 **끄기**를 클릭 한 다음 **확인**을 클릭 합니다.  
  
6.  고급 보안이 설정된 Windows 방화벽을 닫습니다.  
  
## <a name="configure-routing-and-forwarding"></a>라우팅 및 전달 구성  
Corpnet 및 2 Corpnet 서브넷 간에 라우팅 및 전달 서비스를 제공 하려면 네트워크 인터페이스에서 전달을 사용 하도록 설정 하 고 서브넷 간에 고정 경로를 구성 해야 합니다.  
  
### <a name="to-configure-static-routes"></a>정적 경로를 구성 하려면  
  
1.  **시작** 화면에서**cmd.exe**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  다음 명령을 사용 하 여 두 네트워크 어댑터의 IPv4 및 IPv6 인터페이스 모두에서 전달을 사용 하도록 설정 합니다. 각 명령을 입력 한 후 ENTER 키를 누릅니다.  
  
    ```  
    netsh interface IPv4 set interface Corpnet forwarding=enabled  
    netsh interface IPv4 set interface 2-Corpnet forwarding=enabled  
    netsh interface IPv6 set interface Corpnet forwarding=enabled  
    netsh interface IPv6 set interface 2-Corpnet forwarding=enabled  
    ```  
  
3.  Corpnet 및 2 Corpnet 서브넷 간에 IP-HTTPS 라우팅을 사용 하도록 설정 합니다.  
  
    ```  
    netsh interface IPv6 add route 2001:db8:1:1000::/59 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:db8:2:2000::/59 2-Corpnet 2001:db8:2::20  
    ```  
  
4.  Corpnet 및 Corpnet 서브넷 간에 Teredo 라우팅을 사용 하도록 설정 합니다.  
  
    ```  
    netsh interface IPv6 add route 2001:0:836b:2::/64 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:0:836b:14::/64 2-Corpnet 2001:db8:2::20  
    ```  
  
5.  명령 프롬프트 창을 닫습니다.
