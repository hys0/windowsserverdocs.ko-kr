---
title: "Windows Server Essentials를 설치 하기 전에"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d0893bd-e2b7-4494-9537-02b1cbbcd57a
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e7eb1b7bed780b41f1a87589add4ab015f41624a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="before-you-install-windows-server-essentials"></a>Windows Server Essentials를 설치 하기 전에

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_BeforeYouBegin"></a>Windows Server Essentials의 설치를 시작 하기 전에 다음과 같은 작업을 수행 합니다.  

-   **컴퓨터가 최소 하드웨어 요구 사항을 충족 하는지 확인**합니다. 추가 하드웨어가 필요 확인 하 고 확인 하 여 하드웨어에 대 한 드라이버 Windows Server Essentials에서 지원 되는 포함 됩니다. 자세한 내용은 참조 [Windows Server Essentials의 시스템 요구 사항에 대 한](../get-started/system-requirements.md)합니다.   

  
    > [!IMPORTANT]
    >  Windows Server Essentials 기존 컴퓨터에 설치 하기 전에 포맷 완벽 하 게 하 고 기존 컴퓨터의 하드 디스크 다음 다시 하는 것이 좋습니다. 포맷을 하 고 하드 디스크 파티션 설정을 다시 하드 디스크에 파티션 숨겨진된 남아 있는 가능성을 제거할 수 있습니다.  
  
-   **네트워크 준비** Windows Server Essentials를 설치 하 여 네트워크를 준비 하 고 다음을 수행 합니다.  
    
  
    -   **운영 체제 클라이언트 컴퓨터를 업그레이드** Windows Server Essentials 지원 다음 운영 체제: Windows 8, Windows 7, Windows 10 및 OS X 사자 Macintosh 큰 합니다. 이 운영 체제 기능이 필요한 보안, 안정성, 성능 및 로컬 네트워크에 대 한 기능을 제공합니다.  
  
    -   **라우터 구성** 라우터 다음과 같은 구성 되어 있는지 확인 합니다.  
  
        -   라우터에서 UPnP 프레임 워크 활성화 됩니다.  
  
        -   Lan DHCP Dynamic Host Configuration Protocol () 서버 서비스 사용 하도록 설정 하거나 사용 하지 않도록 설정 될 수 있습니다.  Windows Server Essentials 서버 및 라우터 DHCP 실행 하지 설치할 수 있도록 보장? 라우터에서 DHCP를 사용 DHCP 사용 하지 않습니다 서버에 설치 하는 동안.  
  
        -   외부 인터페이스 인터넷 서비스 공급자 (ISP)에서 제공 하 여 라우터의 IP 주소를 해야 합니다. IP 주소 동적으로 isp, DHCP 서버 서비스에서 할당 될 수 있는 하거나 고정 IP 주소를 라우터의 관리 콘솔을 사용 하 여 수동으로 구성 해야 합니다.  
  
        -   사용자 이름 및 암호를 (이더넷상의), 지점 간 프로토콜 라고도 인터넷 연결에 필요한 경우 장치에서 UPnP framework를 지원 하는 경우 라우터에서 이러한 설정은 구성 됩니다.  
  
        -   라우터 LAN와 인터넷에 연결 되어 하 고, 켜져 제대로 작동 합니다.  
  
     라우터 UPnP framework를 지원 하지 않는 경우 또는 설치 시 라우터를 구성할 수 없거나 직접 구성 해야 설정을 사용 하 여 네트워크에 대 한 합니다. 다음 포트 열기 되며 대상 서버의 IP 주소를 전달 있는지 확인 합니다.  
  
    |포트 번호|응용 프로그램|  
    |-----------------|-----------------|  
    |포트 80|HTTP 웹 교통량|  
    |포트 443|HTTPS 웹 교통량|  
  

-   **Windows Server Essentials 릴리스 문서 읽기**합니다. 릴리스 설명서 중요 하며 제대로 설치 및 Windows Server Essentials 구성 될 수 있는 최신 정보를 포함 합니다. 참조를 보거나 인쇄 릴리스 설명서 [Windows에 대 한 설명서 릴리스 Server Essentials](../get-started/release-notes.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)

