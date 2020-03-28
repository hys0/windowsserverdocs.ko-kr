---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows 시간 서비스에 대 한 기술 참조
description: ''
author: eross-msft
ms.author: lizross
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 6d6f203c43ccb764b3ccbfcabbf92f448920b41c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315042"
---
# <a name="windows-time-service"></a>Windows 시간 서비스

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 이상


**이 가이드의 내용**  
  
* Windows 시간 서비스 구성 정보를 찾을 수 있는 위치  
* Windows 시간 서비스란?  
* 시간 프로토콜의 중요도  
* Windows 시간 서비스 작동 방식   
* Windows 시간 서비스 도구 및 설정  
  
> [!NOTE]  
> Windows Server 2003 및 Microsoft Windows 2000 Server 디렉터리 서비스를 이름은 Active Directory 디렉터리 서비스입니다. Windows Server 2008 R2 및 Windows Server 2008에서 디렉터리 서비스의 이름은 AD DS(Active Directory Domain Services)입니다. 이 항목의 나머지 부분에서는 AD DS에 대해 설명하지만, 이 정보는 Windows Server 2016의 Active Directory Domain Services에도 적용됩니다.  
  
W32Time이라고도 하는 Windows 시간 서비스는 AD DS 도메인에서 실행 중인 모든 컴퓨터의 날짜와 시간을 동기화합니다. 시간 동기화는 많은 Windows 서비스 및 기간 업무 애플리케이션의 적절한 작동을 위해 매우 중요합니다. Windows 시간 서비스에서는 정확한 시계 값 또는 타임스탬프를 네트워크 유효성 검사 및 리소스 액세스 요청에 할당할 수 있도록 NTP(Network Time Protocol)를 사용하여 네트워크의 컴퓨터 시계를 동기화합니다. 서비스는 NTP 및 시간 공급자를 통합하여 엔터프라이즈 관리자에게 안정적이고 확장 가능한 시간 서비스를 제공합니다.
  
> [!IMPORTANT]  
> Windows Server 2016 이전에는 W32Time 서비스가 시간이 중요한 애플리케이션 요구 사항을 충족하도록 설계되지 않았습니다.  그러나 이제 Windows Server 2016으로 업데이트하면 도메인에서 1밀리초 정확도의 솔루션을 구현할 수 있습니다.  자세한 내용은 [Windows 2016 정확한 시간](accurate-time.md) 및 [경계 지원으로 정확도가 높은 환경을 위한 Windows 시간 서비스 구성](support-boundary.md)을 참조하세요.  
  
## <a name="where-to-find-windows-time-service-configuration-information"></a><a name="BKMK_Config"></a>Windows 시간 서비스 구성 정보를 찾을 수 있는 위치  
이 가이드에서는 Windows 시간 서비스 구성에 대해서는 설명하지 **않습니다**. Microsoft TechNet 및 Microsoft 기술 자료에는 Windows 시간 서비스를 구성하는 절차를 설명하는 여러 가지 항목이 있습니다. 구성 정보가 필요한 경우 다음 항목을 참조하여 적절한 정보를 찾을 수 있습니다.  
  
-   포리스트 루트 PDC(주 도메인 컨트롤러) 에뮬레이터에 대한 Windows 시간 서비스를 구성하려면 다음을 참조하세요.  
  
    -   [포리스트 루트 도메인의 PDC 에뮬레이터에서 Windows 시간 서비스 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [포리스트에 대한 시간 소스 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft 기술 자료 문서 816042, [Windows Server에서 신뢰할 수 있는 시간 서버를 구성하는 방법](https://go.microsoft.com/fwlink/?LinkID=60402), Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 및 Windows Server 2003 R2를 실행하는 컴퓨터의 구성 설정에 대해 설명합니다.  
  
-   도메인 구성원 클라이언트나 서버 또는 포리스트 루트 PDC 에뮬레이터로 구성되지 않은 도메인 컨트롤러에서 Windows 시간 서비스를 구성하려면 [자동 도메인 시간 동기화를 위해 클라이언트 컴퓨터 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)을 참조하세요.  
  
    > [!WARNING]  
    > 일부 애플리케이션은 높은 정확도의 시간 서비스가 컴퓨터에 필요할 수 있습니다. 이 경우 수동 시간 소스를 구성하도록 선택할 수 있지만 Windows 시간 서비스는 매우 정확한 시간 소스로 작동하도록 설계되지 않았습니다. Microsoft 기술 자료 문서 939322, [정확도가 높은 환경에 맞게 Windows 시간 서비스를 구성할 수 있는 지원 범위](support-boundary.md)에 설명된 대로 정확도가 뛰어난 시간 환경에 대한 지원 제한 사항을 알고 있어야 합니다.  
  
-   도메인 구성원이 아닌 작업 그룹 구성원으로 구성된 Windows 기반 클라이언트 또는 서버 컴퓨터에서 Windows 시간 서비스를 구성하려면 [선택한 클라이언트 컴퓨터의 수동 시간 소스 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29)을 참조하세요.  
  
-   가상 환경을 실행하는 호스트 컴퓨터에서 Windows 시간 서비스를 구성하려면 Microsoft 기술 자료 문서 816042, [Windows Server에서 권한을 보유한 시간 서버를 구성하는 방법](https://go.microsoft.com/fwlink/?LinkID=60402)을 참조하세요. 타사 가상화 제품을 사용하는 경우 해당 제품에 대한 공급 업체의 설명서를 참조하세요.  
  
-   가상 머신에서 실행되는 도메인 컨트롤러에서 Windows 시간 서비스를 구성하려면 도메인 컨트롤러 역할을 하는 호스트 시스템과 게스트 운영 체제 간의 시간 동기화를 부분적으로 사용하지 않도록 설정하는 것이 좋습니다. 이를 통해 게스트 도메인 컨트롤러는 도메인 계층 구조에 대한 시간을 동기화할 수 있지만 저장된 상태에서 복원되는 경우에는 시간 오차를 갖지 않도록 보호할 수 있습니다. 자세한 내용은 Microsoft 기술 자료 문서 976924, [Hyper-V를 사용하여 Windows Server 2008 기반 호스트 서버에서 실행되는 가상화된 도메인 컨트롤러에서 Windows 시간 서비스 이벤트 ID 24, 29 및 38을 수신](https://go.microsoft.com/fwlink/?LinkID=192236) 및 [가상화된 도메인 컨트롤러에 대한 배포 고려 사항](https://go.microsoft.com/fwlink/?LinkID=192235)을 참조하세요.  
  
-   가상 컴퓨터에서 실행되는 포리스트 루트 PDC 에뮬레이터 역할을 하는 도메인 컨트롤러에서 Windows 시간 서비스를 구성하려면 [포리스트 루트 도메인의 PDC 에뮬레이터에서 Windows 시간 서비스 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)에 설명된 대로 물리적 컴퓨터에 대한 동일한 지침을 따릅니다.  
  
-   가상 컴퓨터로 실행하는 구성원 서버에서 Windows 시간 서비스를 구성하려면 ([자동 도메인 시간 동기화를 사용하도록 클라이언트 컴퓨터 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)에 설명된 대로 도메인 시간 계층 구조를 사용합니다.  
  
## <a name="what-is-the-windows-time-service"></a><a name="BKMK_WTS"></a>Windows 시간 서비스란?  
Windows 시간 서비스(W32Time)는 광범위한 구성 없이도 컴퓨터에 대한 네트워크 시계 동기화를 제공합니다.  
  
Windows 시간 서비스는 Kerberos 버전 5 인증을 성공적으로 수행하고 AD DS 기반 인증을 수행하는 데 필수적입니다. 대부분의 보안 서비스를 비롯한 모든 Kerberos 인식 애플리케이션은 인증 요청에 참여하는 컴퓨터 간의 시간 동기화에 의존합니다. AD DS 도메인 컨트롤러에는 정확한 데이터 복제를 위해 동기화된 시계도 있어야 합니다.  
  
Windows 시간 서비스는 W32Time.dll이라는 동적 링크 라이브러리에서 구현됩니다. W32Time.dll은 기본적으로 운영 체제 설정 및 설치 중에 **%Systemroot%\System32** 폴더에 설치됩니다.  
  
W32Time.dll은 원래 네트워크의 시계를 동기화해야 하는 Kerberos V5 인증 프로토콜에 의한 사양을 지원하기 위해 Windows 2000 서버용으로 개발되었습니다. Windows Server 2003부터 W32Time.dll은 Windows 2000 서버 운영 체제를 통한 네트워크 시계 동기화의 향상된 정확도를 제공하고, 시간 공급자를 통해 다양한 하드웨어 디바이스 및 네트워크 시간 프로토콜을 지원했습니다. 원래는 Kerberos 인증에 대한 시계 동기화를 제공하도록 설계되었지만 대부분의 현재 애플리케이션은 트랜잭션 일관성을 보장하고, 중요한 이벤트의 시간 및 업무상 중요하고 시간이 중요한 정보를 기록하기 위해 타임스탬프를 사용합니다. 이러한 애플리케이션은 Windows 시간 서비스에서 제공하는 컴퓨터 간의 시간 동기화를 활용합니다.  
  
## <a name="importance-of-time-protocols"></a><a name="BKMK_TimeProtocols"></a>시간 프로토콜의 중요도  
시간 프로토콜은 두 컴퓨터 간에 통신하여 시간 정보를 교환한 다음, 해당 정보를 사용하여 시계를 동기화합니다. 클라이언트는 Windows 시간 서비스 시간 프로토콜을 사용하여 서버에서 시간 정보를 요청하고 수신된 정보에 따라 시계를 동기화합니다.  
  
Windows 시간 서비스는 NTP를 사용하여 네트워크를 통해 시간을 동기화하는 데 도움이 됩니다. NTP 시계를 동기화 하는 데 필요한 분야 알고리즘을 포함 하는 인터넷 시간 프로토콜입니다. NTP는 일부 버전의 Windows에서 사용되는 SNTP(Simple Network Time Protocol)보다 정확한 시간 프로토콜입니다. 그러나 W32Time은 Windows 2000과 같은 SNTP 기반 시간 서비스를 실행하는 컴퓨터와 이전 버전과의 호환성을 지원하기 위해 계속해서 SNTP를 지원합니다.  
  
## <a name="see-also"></a>참고 항목  
[Windows 시간 서비스의 작동 방식](How-the-Windows-Time-Service-Works.md)  
[Windows 시간 서비스 도구 및 설정](Windows-Time-Service-Tools-and-Settings.md)  
[Microsoft 기술 자료 문서 902229](https://go.microsoft.com/fwlink/?LinkId=186066)