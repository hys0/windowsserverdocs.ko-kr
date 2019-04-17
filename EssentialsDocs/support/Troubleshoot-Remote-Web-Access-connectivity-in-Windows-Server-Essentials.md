---
title: "Windows Server Essentials의 원격 Web Access 연결 문제 해결"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3642575-b3ee-4488-b654-5bf9d3b8c935
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: af4725fd3b1861c847434e3ed62c3da030689fb5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-remote-web-access-connectivity-in-windows-server-essentials"></a>Windows Server Essentials의 원격 Web Access 연결 문제 해결
 
>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.
  
 일반적으로, Windows Server Essentials 라우터가 장치와 라우터에 UPnP 설정을 사용 하는 경우 인증 UPnP 인 경우 광대역 라우터를 자동으로 구성할 수 있습니다.  
  
## <a name="possible-issues"></a>가능한 문제  
 원격 Web Access 연결 다음 문제가 발생할 수 있습니다.  
  
-   라우터가 켜져 있지 또는 네트워크에 연결 되지 않은 합니다.  
  
-   라우터 UPnP 설정이 꺼져 있습니다.  
  
-   라우터는 UPnP 표준 완벽 하 게 지원 되지 않을 수 있습니다. Microsoft는 Windows 운영 체제에서 작동 하는 라우터에 목록을 유지 관리 합니다. Windows Server Essentials와 호환 되는 무선 라우터 등 라우터의 목록을 보려면 방문 하는 [Windows 호환성 센터](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)합니다.  
  
## <a name="possible-fixes"></a>가능한 한 수정 사항  
 다음 작업 이러한 문제를 해결할 수 있습니다.  
  
-   라우터가 켜져 있는지 확인 하 고 제대로 작동 합니다.  
  
-   서버 라우터에 직접 연결 되어 있는지 스위치를 라우터에 연결에 연결 되어 있는지 확인 합니다.  
  
-   인터넷 서비스 공급자 (ISP)에 연결 하는 광대역 장치 설정 되어 있는지 확인에 제대로 작동 하 고 및 라우터 광대역 장치에 연결 되어 있습니다.  
  
-   라우터 UPnP 설정을 켭니다. UPnP 설정을 켭니다 라우터 구성 웹 페이지에 연결 합니다. 라우터 로그온 및 UPnP 설정을 사용 하는 방법에 대 한 정보를 라우터 설명서를 참조 하세요. UPnP 설정의 켠 후는 설정에서 원격 웹 액세스 마법사를 다시 실행 라우터 구성 합니다.  
  
-   라우터 완벽 하 게 UPnP 표준을 지원 하지 않는 경우 수 자동으로 구성할 수 없습니다. 수동으로 라우터를 구성 하거나 UPnP 표준을 지 원하는 라우터가 구입 해야 합니다.  
  
     사용자 라우터를 수동으로 구성 다음 작업을 수행 합니다.  
  
    -   Windows Server Essentials 서버에 대 한 예약을 된 IP 주소를 만듭니다.  
  
         Windows Server Essentials 필요한 포트 전달 라우터를 수동으로 구성 전에 DHCP(Dynamic Host Configuration Protocol) (DHCP) 예약을 라우터에 Windows Server Essentials 실행 하는 서버에 대 한 설정 해야 합니다. 이 이렇게 하면 된 IP 주소를 변경 하지 않는을 포트를 전달 됩니다.  
  
         수동으로 라우터에서 서버에 대 한 DHCP 예약을 설정 하는 방법에 대 한 내용은 라우터 제조업체의 설명서를 참조 하세요.  
  
    -   라우터에서 다음 포트에 대 한 포트 전달을 구성 합니다.  
  
        |서비스 또는 프로토콜|포트|  
        |-------------------------|----------|  
        |HTTP|80 TCP|  
        |HTTPS|443 TCP|  
  
     수동으로 라우터에서 포트 전달을 설정 하는 방법에 대 한 내용은 제조업체의 설명서를 참조 하세요.  
  
     일반적인 라우터 구성 페이지에는 다음과 같은 표 포함 되어 있습니다.  
  
    > [!NOTE]
    >  이 표에 Windows Server Essentials 실행 하는 컴퓨터의 IP 주소가 192.168.0.100 되었습니다. 컴퓨터의 IP 주소를 확인 하 고 해당 IP 주소 표에 나열 된 IP 주소를 대체 해야 합니다.  
  
    |IP 주소|프로토콜 (TCP/UDP)|일정|돌아오는 필터|  
    |----------------|---------------------------|--------------|--------------------|  
    |192.168.0.100|80 TCP|언제 든 지|모든 허용|  
    |192.168.0.100|443 TCP|언제 든 지|모든 허용|  
  
     수동으로 라우터를 구성 하 고 나면 설정에서 원격 웹 액세스 마법사를 실행 하도록 선택 하 고 **건너뛰기 라우터 설치** 옵션을 **시작** 페이지 합니다.  
  
-   라우터 UPnP 표준 완벽 하 게 지원 하지 않는 경우 새 라우터를 구입 합니다.  
  
> [!TIP]
>  라우터에서 BIOS 최신 펌웨어가 설치 되어 있는지 확인 합니다. 라우터 구성 웹 페이지에서 라우터 BIOS 펌웨어 종종 업데이트할 수 있습니다. 자세한 내용은 라우터 설명서를 참조 하세요. 라우터를 업데이트 한 후 설정 어디서 나 액세스 마법사 실행 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [사용 하 여 원격 웹 액세스](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [원격 Web Access 관리](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [액세스를 어디서 나 관리](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials 지원](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials 지원](../support/Support-Windows-Server-Essentials.md)

