---
title: Windows Server Essentials에서 원격 웹 액세스 연결 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3642575-b3ee-4488-b654-5bf9d3b8c935
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6db623308184c5be2968fa1d8991de2b48eef5b7
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318632"
---
# <a name="troubleshoot-remote-web-access-connectivity-in-windows-server-essentials"></a>Windows Server Essentials에서 원격 웹 액세스 연결 문제 해결
 
>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 일반적으로 Windows Server Essentials는 라우터가 UPnP 인증 디바이스이고 라우터에서 UPnP 설정이 사용되는 경우 광대역 라우터를 자동으로 구성할 수 있습니다.  
  
## <a name="possible-issues"></a>가능한 문제  
 원격 웹 액세스 연결에서 다음과 같은 문제가 발생할 수 있습니다.  
  
-   라우터가 켜지지 않거나 네트워크에 연결되지 않습니다.  
  
-   라우터에 대한 UPnP 설정이 꺼집니다.  
  
-   라우터가 UPnP 표준을 완벽하게 지원하지 않을 수 있습니다. Microsoft는 Windows 운영 체제에서 작동하는 라우터 목록을 유지 관리합니다. Windows Server Essentials와 호환되는 라우터(무선 라우터 포함) 목록을 보려면 [Windows 호환성 센터](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)를 참조하세요.  
  
## <a name="possible-fixes"></a>가능한 해결 방법  
 다음 작업을 통해 이러한 문제를 해결할 수 있습니다.  
  
- 라우터가 켜져 있고 제대로 작동하는지 확인합니다.  
  
- 서버가 직접 라우터에 연결되어 있거나 라우터에 연결된 스위치에 연결되어 있는지 확인합니다.  
  
- ISP(인터넷 서비스 공급자)에 연결하는 광대역 디바이스가 켜져 있고, 제대로 작동하며, 라우터가 광대역 디바이스에 연결되어 있는지 확인합니다.  
  
- 라우터에 대한 UPnP 설정을 켭니다. 라우터에 대한 구성 웹 페이지에 연결하여 UPnP 설정을 켭니다. 라우터에 로그온하는 방법 및 UPnP 설정을 켜는 방법에 대한 자세한 내용은 라우터 설명서를 참조하세요. UPnP 설정을 켠 후 원격 웹 액세스 켜기 마법사를 다시 실행 하 여 라우터를 구성 합니다.  
  
- 라우터가 UPnP 표준을 완벽하게 지원하지 않는 경우 자동으로 구성할 수 없습니다. 라우터를 수동으로 구성하거나 UPnP 표준을 지원하는 라우터를 구입해야 합니다.  
  
   라우터를 수동으로 구성하려면 다음 작업을 완료합니다.  
  
  - Windows Server Essentials 서버에 대한 IP 주소 예약을 만듭니다.  
  
     Windows Server Essentials에 필수 포트를 전달하도록 라우터를 수동으로 구성하기 전에 라우터에서 Windows Server Essentials를 실행하는 서버에 대한 DHCP(Dynamic Host Configuration Protocol) 예약을 설정해야 합니다. 이 단계는 포트를 전달할 IP 주소가 변경되지 않도록 합니다.  
  
     라우터에서 서버에 대 한 DHCP 예약을 수동으로 설정 하는 방법에 대 한 자세한 내용은 라우터에 대 한 제조업체 설명서를 참조 하세요.  
  
  - 라우터에서 다음 포트에 대해 포트 전달을 구성합니다.  
  
    |서비스 또는 프로토콜|포트|  
    |-------------------------|----------|  
    |HTTP|TCP 80|  
    |HTTPS|TCP 443|  
  
    라우터에서 포트 전달을 수동으로 설정 하는 방법에 대 한 자세한 내용은 제조업체의 설명서를 참조 하십시오.  
  
    일반적인 라우터 구성 페이지에는 다음과 유사한 표가 포함되어 있습니다.  
  
  > [!NOTE]
  >  이 표에서 Windows Server Essentials를 실행하는 컴퓨터의 IP 주소는 192.168.0.100입니다. 컴퓨터의 IP 주소를 확인하고 해당 IP 주소를 표에 있는 IP 주소로 대체해야 합니다.  
  
  |IP 주소|프로토콜(TCP/UDP)|일정|인바운드 필터|  
  |----------------|---------------------------|--------------|--------------------|  
  |192.168.0.100|TCP 80|항상|Allow All|  
  |192.168.0.100|TCP 443|항상|Allow All|  
  
   라우터를 수동으로 구성한 후 **시작** 페이지에서 **라우터 설정 건너뛰기** 옵션을 선택 하 여 원격 웹 액세스 켜기 마법사를 실행 합니다.  
  
- 라우터가 UPnP 표준을 완벽하게 지원하지 않는 경우 새 라우터를 구입합니다.  
  
> [!TIP]
>  라우터에 최신 BIOS 펌웨어가 설치되어 있는지 확인합니다. 라우터에 대한 구성 웹 페이지에서 라우터의 BIOS 펌웨어를 업데이트할 수 있는 경우가 많습니다. 자세한 내용은 라우터 설명서를 참조하세요. 라우터가 업데이트된 후 원격 액세스 설정 마법사를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
  
-   [원격 웹 액세스 사용](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [원격 웹 액세스 관리](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [원격 액세스 관리](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials 지원](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials 지원](../support/Support-Windows-Server-Essentials.md)

