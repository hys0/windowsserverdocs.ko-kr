---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: "Windows 시간 서비스"
description: 
author: shortpatti
ms.author: pashort
manager: brianlic
ms.date: 02/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c3c53db3839b5f33a87fe3789f2f7958f0bc42c2
ms.sourcegitcommit: 556361fe7c73c75d6cdc46a67dc88679fbe89c61
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="windows-time-service"></a>Windows 시간 서비스

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
 
  
## <a name="w2k3tr_times_intro"></a>Windows 시간이 서비스 기술 참조  
**이 가이드**  
  
* Windows 시간이 서비스 구성 정보를 찾을 수 있는 위치  
* Windows 시간 서비스 무엇 인가요?  
* 중요성 시간 프로토콜  
* Windows 시간 서비스의 작동 방식   
* Windows 서비스 도구 시간 및 설정  
  
> [!NOTE]  
> Windows Server 2003 및 Windows 2000 Server, 디렉터리 서비스 Active Directory 디렉터리 서비스를 이라고 합니다. Windows Server 2008 R2 및 Windows Server 2008 디렉터리 서비스 Active Directory Domain Services (AD DS) 라고 합니다. 이 항목의 나머지 부분 AD DS 의미 하지만 정보는도 Active Directory Domain Services Windows Server 2016에 적용 됩니다.  
  
라고도 W32Time Windows 시간 서비스의 날짜 및 시간 AD DS 도메인에서 실행 중인 모든 컴퓨터에 대 한 동기화 합니다. 시간 동기화가 제대로 작동 많은 Windows 서비스 및 온라인 비즈니스 응용 프로그램에 대 한 중요 합니다. Windows 시간 서비스 네트워크 시간 Protocol (NTP)를 사용 하 여 정확한 시간 값 또는 타임 스탬프 네트워크 리소스를 유효성 검사 액세스 요청에 할당 될 수 있도록 네트워크에서 컴퓨터 시계 동기화 하도록 합니다. 서비스 NTP 통합 및 시간 공급자, 더 안정적이 고 확장 가능 하도록 만들기 시간 서비스 enterprise 관리자를 합니다.  
  
> [!IMPORTANT]  
> Windows Server 2016 전에 W32Time 서비스 시간 응용 프로그램 요구를 충족 되도록 디자인 되지 않았습니다.  그러나 Windows Server 2016 업데이트 이제 수 있도록 1ms 위한 솔루션을 구현 도메인에 정확도 합니다.  See [Windows 2016 Accurate Time](accurate-time.md) and  [Support boundary to configure the Windows Time service for high-accuracy environments](https://go.microsoft.com/fwlink/?LinkID=179459) for more information.  
  
## <a name="BKMK_Config"></a>Windows 시간이 서비스 구성 정보를 찾을 수 있는 위치  
이 가이드는 **하지** Windows 시간 서비스 구성에 대해 설명 합니다. Windows 시간 서비스 구성 절차에 설명 수행 하는 여러 가지 주제 Microsoft technet 및 Microsoft 기술 자료 가지가 있습니다. 구성 정보를 필요로 하는 경우 다음 항목 해야 하는 데 도움이 적절 한 정보를 찾을 수 있습니다.  
  
-   Windows 시간 서비스 숲 루트 주 도메인 컨트롤러 (PDC) 에뮬레이터를 참조 하십시오.  
  
    -   [Windows 시간 서비스 숲 루트 도메인 PDC 에뮬레이터 구성](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [숲에 대 한 시간 소스 구성](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft 기술 자료 문서, 816042 [Windows Server에서 신뢰할 수 있는 시간 서버를 구성 하는 방법을](https://go.microsoft.com/fwlink/?LinkID=60402)를 설명 하는 Windows Server 2008 R2, Windows Server 2008, Windows Server 2003을 실행 하는 컴퓨터에 대 한 구성 설정 및 Windows Server 2003 R2입니다.  
  
-   Windows 시간 서비스 도메인 회원 클라이언트 또는 서버 또는 숲 루트 PDC 에뮬레이터로 구성 되어 있지 않으면도 도메인 컨트롤러에서 참조 하십시오 [시간 동기화 자동 도메인에 대 한 클라이언트 컴퓨터 구성](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)합니다.  
  
    > [!WARNING]  
    > 일부 응용 프로그램의 컴퓨터 높은 정확도 시간 서비스를 필요할 수 있습니다. 하는 경우 Windows 시간 서비스 매우 정확 하 게 시간 원본으로 작동 되도록 디자인 되지 않았습니다 수 있지만 수동 시간 소스 구성 하도록 선택할 수 있습니다. 939322, Microsoft 기술 자료 문서에서 설명한 대로 높은 정확도 시간 환경에 대 한 지원 제한을 알고 있는지 확인 [높은 정확도 환경에 대 한 Windows 시간 서비스를 구성 지원 경계](https://go.microsoft.com/fwlink/?LinkID=179459)합니다.  
  
-   모든 Windows 기반 클라이언트 또는 서버 컴퓨터에서 도메인 회원 대신 작업 그룹 구성원 볼 구성 되어 있는 Windows 시간 서비스 구성 하려면 [수동 시간 소스 선택한 클라이언트 컴퓨터에 대 한 구성](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29)합니다.  
  
-   Windows 시간 서비스 가상 환경 실행 되는 호스트 컴퓨터에서 참조 하십시오 Microsoft 기술 자료 문서, 816042 [Windows Server에서 신뢰할 수 있는 시간 서버를 구성 하는 방법을](https://go.microsoft.com/fwlink/?LinkID=60402)합니다. Microsoft가 아닌 타사 virtualization 제품을 사용 하는 경우 해당 제품에 대 한 공급 업체의 설명서를 참조 하 해야 합니다.  
  
-   가상 컴퓨터에서 실행 되는 도메인 컨트롤러에서 Windows 시간 서비스를 구성 하려면 사용자 부분적으로 간의 도메인 컨트롤러 역할 호스트 시스템과 게스트 운영 체제 시간 동기화를 비활성화할 수 좋습니다. 이 시간 도메인 계층을 동기화 게스트 도메인 컨트롤러를 사용 하면 하지만가 기울이기에서 저장 된 상태로 복원 되 면 한 번 수 없도록 보호 합니다. 자세한 내용은 참조 Microsoft 기술 자료 문서, 976924 [Windows 시간 서비스 이벤트 Id 24, 29 및 38 Hyper-v를 사용 하 여 Windows Server 2008 기반 호스트 서버에서 실행 되는 가상화 도메인 컨트롤러에서 수신](https://go.microsoft.com/fwlink/?LinkID=192236) 하 고 [가상화 도메인 컨트롤러에 대 한 배포 고려](https://go.microsoft.com/fwlink/?LinkID=192235)합니다.  
  
-   에 설명 된 대로 Windows 시간 서비스 또한 가상 컴퓨터에서 실행 되 고 숲 루트 PDC 에뮬레이터 역할을 하는 도메인 컨트롤러에서를 구성 하려면 실제 컴퓨터에 대 한 같은 지침에 따라 [Windows 시간 서비스 pdc 구성 숲 루트 도메인의 에뮬레이터](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)합니다.  
  
-   가상 컴퓨터와 실행 구성원 서버에서 시간 Windows 서비스를 구성 하 도메인 시간 계층에 설명 된 대로 사용 ([시간 동기화 자동 도메인에 대 한 클라이언트 컴퓨터 구성](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)합니다.  
  
## <a name="BKMK_WTS"></a>Windows 시간 서비스 무엇 인가요?  
Windows 시간 서비스 (W32Time) 광범위 하 게 구성에 대 한 필요 없이 컴퓨터에 대 한 네트워크 시계 동기화를 제공합니다.  
  
Windows 시간 서비스 Kerberos 5 버전 인증 성공적으로 작동 하 고, 따라서 광고 DS 기반 인증을 필수입니다. 대부분의 보안 서비스를 포함 하 여 모든 Kerberos 인식 응용 프로그램 시간 동기화 인증 요청에 참여 하는 컴퓨터 사이 의존 합니다. 또한 AD DS 도메인 컨트롤러 정확한 데이터 복제를 보장 하기 위해 시계 동기화가 있어야 합니다.  
  
Windows 시간 서비스 W32Time.dll 라는 동적 연결 라이브러리에 있는 구현 됩니다. W32Time.dll에서 기본적으로 설치 되 고 **%Systemroot%\System32** 운영 체제 설정 및 설치 하는 동안 폴더 합니다.  
  
W32Time.dll은 원래 Kerberos v 5 인증 프로토콜 시계 동기화 할 수 있는 네트워크에 필요한 설정을 지원 하기 위해 Windows 2000 Server에 대 한 개발 합니다. Windows Server 2003, 부터는 W32Time.dll 네트워크 시계 동기화의 정확도 향상된 Windows 2000 Server 운영 체제를 통해 제공 하 고, 또한 시간 공급자를 사용 하 여 다양 한 하드웨어 디바이스 및 네트워크 시간이 프로토콜을 지원 합니다. Kerberos 인증에 대 한 동기화 시계를 제공 하기 위해 설계 되었지만 처음, 현재 많은 응용 프로그램의 중요 한 이벤트 및 비즈니스에 중요 한 기타 시간 민감한 정보 시간을 기록해 트랜잭션 일관성을 유지 하려면 타임 스탬프를 사용 합니다. 이러한 응용 프로그램에서 동기화 Windows 시간 서비스에서 제공 하는 컴퓨터 간에 도움이 됩니다.  
  
## <a name="BKMK_TimeProtocols"></a>중요성 시간 프로토콜  
시간 프로토콜 교환 시간 정보 및 다음 해당 정보를 사용 하 여 자신의 시계 동기화 두 컴퓨터 통신할 수 있습니다. Windows 시간 서비스 시간 프로토콜을 사용 하는 클라이언트 서버에서 시간 정보를 요청 하 고 수신 하는 정보에 따라 해당 시계 동기화 합니다.  
  
Windows 시간 서비스 NTP를 사용 하 여 네트워크를 통해 시간을 동기화 하는 데 도움이 됩니다. NTP 시계 동기화 하는 데 필요한 분야 알고리즘을 포함 하는 인터넷 프로토콜 시간입니다. NTP은 더 정확 하 게 시간 프로토콜 보다는 네트워크 시간 (SNTP 프로토콜), Windows의 일부 버전에 사용 되는 그러나 W32Time SNTP Windows 2000 같은 시간 SNTP 기반 서비스를 실행 하는 컴퓨터 이전 버전과 호환성을 지원 하기 위해 계속 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[Windows 시간 서비스의 작동 방식](How-the-Windows-Time-Service-Works.md)  
[Windows 서비스 도구 시간 및 설정](Windows-Time-Service-Tools-and-Settings.md)  
[Microsoft 기술 자료 문서 902229](https://go.microsoft.com/fwlink/?LinkId=186066)