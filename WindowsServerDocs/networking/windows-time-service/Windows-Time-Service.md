---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows 시간 서비스에 대 한 기술 참조
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 0b424e118980792d4b4db8ba365ad60cc5edc75c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815944"
---
# <a name="windows-time-service"></a>Windows 시간 서비스

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 이상


**이 가이드의**  
  
* Windows 시간 서비스 구성 정보를 찾을 수 있는 위치  
* Windows 시간 서비스 무엇입니까?  
* 시간 프로토콜의 중요성  
* Windows 시간 서비스 작동 방식   
* Windows 시간 서비스 도구 및 설정  
  
> [!NOTE]  
> Windows Server 2003 및 Microsoft Windows 2000 Server 디렉터리 서비스를 이름은 Active Directory 디렉터리 서비스입니다. Windows Server 2008 R2 및 Windows Server 2008 디렉터리 서비스의 이름은 Active Directory Domain Services (AD DS)입니다. 이 항목의 나머지 AD DS를 나타내지만 정보도 Windows Server 2016의 Active Directory Domain Services에 적용 됩니다.  
  
Windows 시간 서비스 W32Time 라고도 하며 AD DS 도메인에서 실행 하는 모든 컴퓨터에 대 한 시간과 날짜를 동기화 합니다. 시간 동기화는 여러 Windows 서비스 및 기간 업무 응용 프로그램의 올바른 작동에 중요 합니다. Windows 시간 서비스 (NTP (Network Time Protocol)를 사용 하 여 네트워크의 컴퓨터 시계를 동기화 하는 정확한 시간 값 또는 타임 스탬프를 네트워크 유효성 검사 및 리소스 액세스 요청에 할당할 수 있습니다. NTP를 통합 하는 서비스 및 엔터프라이즈 관리자에 대 한 확장 가능 하며 안정적인 시간 서비스를 만드는 시간 공급자입니다.
  
> [!IMPORTANT]  
> Windows Server 2016 이전 W32Time 서비스 시간에 민감한 응용 프로그램 요구 사항에 맞게 설계 되지 않았습니다.  그러나 Windows Server 2016에 대 한 업데이트 수 1ms에 대 한 솔루션을 구현 하려면 도메인의 정확도입니다.  참조 [Windows 2016 정확한 내용 시간](accurate-time.md) 하 고 [지원 정확도 높은 환경에 대 한 Windows 시간 서비스를 구성 하는 경계](support-boundary.md) 자세한 내용은 합니다.  
  
## <a name="BKMK_Config"></a>Windows 시간 서비스 구성 정보를 찾을 수 있는 위치  
이 가이드에서는 **되지** Windows 시간 서비스 구성에 대해 설명 합니다. Windows 시간 서비스를 구성 하는 절차를 설명 수행 하는 여러 가지 주제 Microsoft TechNet의 항목과 Microsoft 기술 자료에 있습니다. 구성 정보를 필요로 하는 경우 다음 항목에서는 적절 한 정보를 찾을 수 도움이 됩니다.  
  
-   포리스트 루트 주 도메인 컨트롤러 (PDC) 에뮬레이터에 대 한 Windows 시간 서비스를 구성 하려면 다음을 참조 하세요.  
  
    -   [포리스트 루트 도메인의 PDC 에뮬레이터에서 Windows 시간 서비스를 구성 합니다.](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [포리스트에 대 한 시간 원본 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft 기술 자료 문서, 816042 [Windows Server에서 신뢰할 수 있는 시간 서버를 구성 하는 방법을](https://go.microsoft.com/fwlink/?LinkID=60402), Windows Server 2008 R2, Windows Server 2008, Windows Server를 실행 하는 컴퓨터에 대 한 구성 설정을 설명 하는 2003 및 Windows Server 2003 R2.  
  
-   모든 도메인 구성원 클라이언트 또는 서버 또는 포리스트 루트 PDC 에뮬레이터 역할 구성 되지 않은 도메인 컨트롤러에서 Windows 시간 서비스를 구성 하려면 참조 [자동도메인시간동기화를위해클라이언트컴퓨터구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).  
  
    > [!WARNING]  
    > 일부 응용 프로그램에는 정확도 높은 시간 서비스 컴퓨터 필요할 수 있습니다. 하는 경우에 수동 시간 원본을 구성할 수 있지만 Windows 시간 서비스는 매우 정확한 시간 원본으로 작동 하도록 설계 되지 않았습니다는 주의를 선택할 수 있습니다. 인식 하 고 지원 제한 시간 정확도 높은 환경에서 Microsoft 기술 자료에 설명 된 대로 문서 939322, 참조에 대 한 확인 [지원 정확도 높은 환경에대한Windows시간서비스를구성하는경계](support-boundary.md).  
  
-   모든 Windows 기반 클라이언트 또는 서버 컴퓨터에서 참조 하는 도메인 멤버 대신 작업 그룹 구성원으로 구성 된 Windows 시간 서비스를 구성 하려면 [선택한 클라이언트 컴퓨터에 대 한 수동 시간 원본을 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29)합니다.  
  
-   가상 환경을 실행 하는 호스트 컴퓨터에서 Windows 시간 서비스를 구성 하려면 Microsoft 기술 자료 문서 816042를 참조 하세요 [Windows Server에서 신뢰할 수 있는 시간 서버를 구성 하는 방법을](https://go.microsoft.com/fwlink/?LinkID=60402)합니다. 타사 가상화 제품을 사용 하는 경우에 해당 제품에 대 한 공급 업체의 설명서를 참조 해야 합니다.  
  
-   가상 컴퓨터에서 실행 되는 도메인 컨트롤러에서 Windows 시간 서비스를 구성 하려면 부분적으로 도메인 컨트롤러 역할을 하는 호스트 시스템 및 게스트 운영 체제 간의 시간 동기화를 사용 하지 않는 것이 좋습니다. 이 도메인 계층 구조에 대 한 시간을 동기화 하도록 게스트 도메인 컨트롤러를 사용 하도록 설정 되지만 저장 된 상태에서 복원 된 경우를 지정 하 여 시간차가 못하도록 보호 합니다. 자세한 내용은 Microsoft 기술 자료 문서 976924를을 참조 하세요 [Windows 시간 서비스 이벤트 Id 24, 29 및 38 Hyper-v가 설치 된 Windows Server 2008 기반 호스트 서버에서 실행 되는 가상화 된 도메인 컨트롤러에 수신](https://go.microsoft.com/fwlink/?LinkID=192236) 및 [가상화 된 도메인 컨트롤러에 대 한 배포 고려 사항](https://go.microsoft.com/fwlink/?LinkID=192235)합니다.  
  
-   에 설명 된 대로 가상 컴퓨터 에서도 실행 되는 포리스트 루트 PDC 에뮬레이터 역할을 하는 도메인 컨트롤러에서 Windows 시간 서비스를 구성 하려면 물리적 컴퓨터에 대 한 동일한 지침에 따라 [에서 Windows 시간 서비스를 구성 합니다. 포리스트 루트 도메인의 PDC 에뮬레이터](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)합니다.  
  
-   에 설명 된 대로 가상 컴퓨터로 실행 하는 멤버 서버에서 Windows 시간 서비스를 구성 하려면 도메인 시간 계층 구조를 사용 ([자동 도메인 시간 동기화를 위해 클라이언트 컴퓨터 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)합니다.  
  
## <a name="BKMK_WTS"></a>Windows 시간 서비스 무엇입니까?  
Windows 시간 서비스 (w32time))는 광범위 한 구성이 필요 없이 컴퓨터에 대 한 네트워크 시계 동기화를 제공합니다.  
  
Kerberos 버전 5 인증 작업을 성공적으로 실행 하 고 따라서 AD DS 기반 인증으로 Windows 시간 서비스를 반드시 필요 합니다. 대부분의 보안 서비스를 비롯 한 모든 Kerberos 인식 응용 프로그램 인증 요청에 참여 하는 컴퓨터 간의 시간 동기화를 의존 합니다. 또한 AD DS 도메인 컨트롤러 정확한 데이터를 복제 하는 시계 동기화가 있어야 합니다.  
  
Windows 시간 서비스 W32Time.dll를 호출 하는 동적 링크 라이브러리에서 구현 됩니다. W32Time.dll은에서 기본적으로 설치 합니다 **%Systemroot%\System32** 운영 체제 설정 및 설치 하는 동안 폴더입니다.  
  
W32Time.dll 원래 사양을 지원 하도록 Windows 2000 Server에 대 한 동기화 하는 네트워크의 시계는 데 필요한 Kerberos V5 인증 프로토콜에 의해 개발 되었습니다. Windows Server 2003부터 제공 W32Time.dll Windows 2000 Server 운영 체제에서 네트워크 시계 동기화 정확도 크게 향상 하 고, 또한 시간을 사용 하 여 다양 한 하드웨어 장치 및 네트워크 시간 프로토콜을 지원 공급자입니다. 현재 많은 응용 프로그램 타임 스탬프를 사용 하 여 중요 한 이벤트 및 기타 업무상 중요 하며 시간을 기록할 트랜잭션 일관성을 유지 하려면 원래 Kerberos 인증에 대 한 클록 동기화를 제공 하도록 디자인 되었지만, 시간이 중요 한 정보입니다. 이러한 응용 프로그램이은 Windows 시간 서비스에서 제공 하는 컴퓨터 간의 시간 동기화에서 활용 합니다.  
  
## <a name="BKMK_TimeProtocols"></a>시간 프로토콜의 중요성  
시간 프로토콜 시간 정보를 교환 하 고 다음 정보를 사용 하 여 시계를 동기화 하려면 두 컴퓨터 간에 통신 합니다. Windows 시간 서비스 시간 프로토콜을 사용 하 여 클라이언트가 서버에서 시간 정보를 요청 하 고 수신 되는 정보를 기반으로 해당 클록을 동기화 합니다.  
  
Windows 시간 서비스 NTP를 사용 하 여 네트워크를 통해 시간을 동기화 하는 데 있습니다. NTP 시계를 동기화 하는 데 필요한 분야 알고리즘을 포함 하는 인터넷 시간 프로토콜입니다. NTP은 보다 정확한 시간 프로토콜 보다는 네트워크 시간 프로토콜 SNTP () Windows;의 일부 버전에 사용 되는 그러나 W32Time 계속 SNTP Windows 2000 같은 시간 대의 SNTP 기반 서비스를 실행 하는 컴퓨터를 사용 하 여 이전 버전과 호환성을 사용 하도록 지원 합니다.  
  
## <a name="see-also"></a>관련 항목  
[Windows 시간 서비스의 작동 원리](How-the-Windows-Time-Service-Works.md)  
[Windows 시간 서비스 도구 및 설정](Windows-Time-Service-Tools-and-Settings.md)  
[Microsoft 기술 자료 문서 902229](https://go.microsoft.com/fwlink/?LinkId=186066)