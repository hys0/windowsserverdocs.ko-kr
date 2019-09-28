---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows 시간 서비스에 대 한 기술 참조
description: W32Time 서비스는 광범위 한 구성이 필요 없는 컴퓨터에 대 한 네트워크 클록 동기화를 제공 합니다. W32Time 서비스는 Kerberos V5 인증을 성공적으로 수행 하는 데 필수적 이며, 따라서 AD DS 기반 인증을 수행 하는 데 필요 합니다.
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: c45ac44448326ec3a236a685387b7969d21aa607
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395664"
---
# <a name="windows-time-service-technical-reference"></a>Windows 시간 서비스에 대 한 기술 참조
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 이상

W32Time 서비스는 광범위 한 구성이 필요 없는 컴퓨터에 대 한 네트워크 클록 동기화를 제공 합니다. W32Time 서비스는 Kerberos V5 인증을 성공적으로 수행 하는 데 필수적 이며, 따라서 AD DS 기반 인증을 수행 하는 데 필요 합니다. 대부분의 보안 서비스를 비롯 한 모든 Kerberos 인식 응용 프로그램은 인증 요청에 참여 하는 컴퓨터 간의 시간 동기화에 의존 합니다. AD DS 도메인 컨트롤러에는 정확한 데이터 복제를 위해 동기화 된 클록도 있어야 합니다.

> [!NOTE]  
> Windows Server 2003 및 Microsoft Windows 2000 Server 디렉터리 서비스를 이름은 Active Directory 디렉터리 서비스입니다. Windows Server 2008 R2 및 Windows Server 2008에서 디렉터리 서비스의 이름은 Active Directory Domain Services (AD DS)입니다. 이 항목의 나머지 부분에서는 AD DS을 참조 하지만 Windows Server 2016의 Active Directory Domain Services에도 해당 정보를 적용할 수 있습니다.

W32Time 서비스는 **%Systemroot%\System32**에서 기본적으로 설치 되는 w32time 이라는 동적 연결 라이브러리에서 구현 됩니다. W32Time은 원래 Windows 2000 서버에서 네트워크에 대 한 클록을 요구 하는 Kerberos V5 인증 프로토콜의 사양을 지원 하기 위해 개발 되었습니다. Windows Server 2003부터 Windows Server 2000 운영 체제를 통한 네트워크 클록 동기화의 정확성이 향상 되었습니다. 또한 Windows Server 2003에서 W32Time은 시간 공급자를 사용 하 여 다양 한 하드웨어 장치 및 네트워크 시간 프로토콜을 지원 합니다.

원래는 Kerberos 인증에 대 한 클록 동기화를 제공 하도록 설계 되었지만 대부분의 현재 응용 프로그램에서는 타임 스탬프를 사용 하 여 트랜잭션 일관성을 유지 하 고 중요 한 이벤트의 시간을 기록 하며 비즈니스에 중요 한 시간을 구분 합니다. 내용을.  이러한 응용 프로그램은 Windows 시간 서비스에서 제공 하는 컴퓨터 간의 시간 동기화를 활용 합니다.

## <a name="importance-of-time-protocols"></a>시간 프로토콜의 중요도
시간 프로토콜은 두 컴퓨터 간에 통신 하 여 시간 정보를 교환 한 다음 해당 정보를 사용 하 여 시계를 동기화 합니다. 클라이언트는 Windows 시간 서비스 시간 프로토콜을 사용 하 여 서버에서 시간 정보를 요청 하 고 수신 된 정보에 따라 시계를 동기화 합니다.
  
Windows 시간 서비스는 NTP를 사용 하 여 네트워크를 통해 시간을 동기화 합니다. NTP 시계를 동기화 하는 데 필요한 분야 알고리즘을 포함 하는 인터넷 시간 프로토콜입니다. NTP는 일부 버전의 Windows에서 사용 되는 SNTP (Simple Network Time Protocol) 보다 더 정확한 시간 프로토콜입니다. 그러나 W32Time은 Windows 2000와 같은 SNTP 기반 시간 서비스를 실행 하는 컴퓨터와 이전 버전과의 호환성을 지원 하기 위해 계속 해 서 SNTP를 지원 합니다.
<!-- maybe this should be its own topic under the Tech Ref section -->
## <a name="where-to-find-windows-time-service-configuration-related-information"></a>Windows 시간 서비스 구성 관련 정보를 찾을 수 있는 위치  
이 가이드에서는 Windows 시간 서비스를 구성 하는 방법에 대해서는 설명 **하지** 않습니다. Microsoft TechNet 및 Microsoft 기술 자료에는 Windows 시간 서비스를 구성 하는 절차를 설명 하는 여러 가지 항목이 있습니다. 구성 정보를 요구 하는 경우 다음 항목을 참조 하 여 적절 한 정보를 찾을 수 있습니다.  
<!-- should this be an if/then table -->
-   포리스트 루트 PDC (주 도메인 컨트롤러) 에뮬레이터에 대 한 Windows 시간 서비스를 구성 하려면 다음을 참조 하세요.  
  
    -   [포리스트 루트 도메인의 PDC 에뮬레이터에서 Windows 시간 서비스 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [포리스트에 대 한 시간 원본 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft 기술 자료 문서 816042, windows server 2008 R2, Windows Server 2008, Windows Server 2003 및 Windows를 실행 하는 컴퓨터의 구성 설정을 설명 하는 [Windows server에서 신뢰할 수 있는 시간 서버를 구성 하는 방법](https://go.microsoft.com/fwlink/?LinkID=60402) 서버 2003 R2.  
  
-   도메인 구성원 클라이언트나 서버 또는 포리스트 루트 PDC 에뮬레이터로 구성 되지 않은 도메인 컨트롤러에서 Windows 시간 서비스를 구성 하려면 [자동 도메인 시간 동기화를 위해 클라이언트 컴퓨터 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)을 참조 하세요.  
  
    > [!WARNING]  
    > 일부 응용 프로그램의 경우 컴퓨터의 정확도가 높은 시간 서비스를 필요로 할 수 있습니다. 이 경우 수동 시간 원본을 구성 하도록 선택할 수 있지만, Windows 시간 서비스는 매우 정확한 시간 원본으로 작동 하도록 설계 되지 않았습니다. Microsoft 기술 자료 문서 939322에 설명 된 대로 정확도가 뛰어난 시간 환경에 대 한 지원 제한이 있는지 확인 하 고, [높은 정확도 환경에 대해 Windows 시간 서비스를 구성 하는 지원 경계](support-boundary.md)를 확인 합니다.  
  
-   도메인 구성원이 아닌 작업 그룹 구성원으로 구성 된 Windows 기반 클라이언트 또는 서버 컴퓨터에서 Windows 시간 서비스를 구성 하려면 [선택한 클라이언트 컴퓨터의 수동 시간 원본 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29)을 참조 하세요.  
  
-   가상 환경을 실행 하는 호스트 컴퓨터에서 Windows 시간 서비스를 구성 하려면 Microsoft 기술 자료 문서 816042, [Windows server에서 신뢰할 수 있는 시간 서버를 구성 하는 방법](https://go.microsoft.com/fwlink/?LinkID=60402)을 참조 하십시오. 타사 가상화 제품을 사용 하는 경우 해당 제품에 대 한 공급 업체의 설명서를 참조 하세요.  
  
-   가상 컴퓨터에서 실행 되는 도메인 컨트롤러에서 Windows 시간 서비스를 구성 하려면 도메인 컨트롤러 역할을 하는 호스트 시스템과 게스트 운영 체제 간의 시간 동기화를 부분적으로 사용 하지 않도록 설정 하는 것이 좋습니다. 이를 통해 게스트 도메인 컨트롤러는 도메인 계층 구조에 대 한 시간을 동기화 할 수 있지만 저장 된 상태에서 복원 되는 경우에는 시간 오차를 갖지 않도록 보호할 수 있습니다. 자세한 내용은 Microsoft 기술 자료 문서 976924, Hyper-v 및 배포를 [사용 하 여 Windows Server 2008 기반 호스트 서버에서 실행 되는 가상화 된 도메인 컨트롤러에서 Windows 시간 서비스 이벤트 id 24, 29 및 38](https://go.microsoft.com/fwlink/?LinkID=192236) 를 참조 하세요. [ 가상화 된 도메인 컨트롤러에 대 한 고려 사항](https://go.microsoft.com/fwlink/?LinkID=192235)  
  
-   가상 컴퓨터에서 실행 중인 포리스트 루트 PDC 에뮬레이터 역할을 하는 도메인 컨트롤러에서 Windows 시간 서비스를 구성 하려면 [PDC에서 Windows 시간 서비스 구성에 설명 된 대로 물리적 컴퓨터에 대 한 동일한 지침을 따릅니다. 포리스트 루트 도메인의 에뮬레이터](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)입니다.  
  
-   가상 컴퓨터로를 실행 하는 구성원 서버에서 Windows 시간 서비스를 구성 하려면 [자동 도메인 시간 동기화를 위해 클라이언트 컴퓨터 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)에 설명 된 대로 도메인 시간 계층 구조를 사용 합니다.


> [!IMPORTANT]  
> Windows Server 2016 이전에는 W32Time 서비스가 시간이 중요 한 응용 프로그램 요구 사항을 충족 하도록 설계 되지 않았습니다.  그러나 이제 Windows Server 2016에 대 한 업데이트를 통해 도메인의 1ms 정확도에 대 한 솔루션을 구현할 수 있습니다.  에 대 한 자세한 내용은 [windows 2016 정확한 시간](accurate-time.md) 및 [지원 경계](support-boundary.md) (영문)를 참조 하세요.

## <a name="related-topics"></a>관련 항목
- [Windows 2016 정확한 시간](accurate-time.md)
- [Windows Server 2016에 대 한 시간 정확도 향상](windows-server-2016-improvements.md)  
- [Windows 시간 서비스의 작동 원리](How-the-Windows-Time-Service-Works.md)  
- [Windows 시간 서비스 도구 및 설정](Windows-Time-Service-Tools-and-Settings.md)  
- [높은 정확도 환경을 위한 Windows 시간 서비스를 구성 하는 경계 지원](support-boundary.md)
- [Microsoft 기술 자료 문서 902229](https://go.microsoft.com/fwlink/?LinkId=186066)