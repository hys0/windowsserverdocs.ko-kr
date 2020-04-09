---
title: Windows Server Essentials를 설치하기 전에
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 8d0893bd-e2b7-4494-9537-02b1cbbcd57a
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 08f39acccef390cbc5cfa10d0743b05f6914327c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817356"
---
# <a name="before-you-install-windows-server-essentials"></a>Windows Server Essentials를 설치하기 전에

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="before-you-begin-your-installation-of--windows-server-essentials-perform-the-following-tasks"></a><a name="BKMK_BeforeYouBegin"></a>Windows Server Essentials 설치를 시작 하기 전에 다음 작업을 수행 합니다.  

-   **컴퓨터가 최소 하드웨어 요구 사항을 충족하는지 확인합니다**. 여기에는 추가 하드웨어가 필요한 지 확인 하 고 하드웨어 드라이버가 Windows Server Essentials에서 지원 되는지 확인 하는 작업이 포함 됩니다. 자세한 내용은 [Windows Server Essentials의 시스템 요구 사항](../get-started/system-requirements.md)을 참조 하세요.   

> [!IMPORTANT]
> 기존 컴퓨터에 Windows Server Essentials를 설치 하기 전에 기존 컴퓨터의 하드 디스크를 전체 포맷 한 후 다시 분할 하는 것이 좋습니다. 하드 디스크를 포맷하고 다시 분할하면 하드 디스크에 숨겨진 파티션이 남아 있을 가능성이 없어집니다.  

- **네트워크 준비** Windows Server Essentials를 설치 하기 위해 네트워크를 준비 하려면 다음을 수행 합니다.  


  - **클라이언트 컴퓨터에서 운영 체제 업그레이드**  Windows Server Essentials는 Windows 8, Windows 7, Windows 10 및 Macintosh OS X 사자 이상의 운영 체제를 지원 합니다. 이러한 운영 체제는 로컬 네트워크에 필요한 보안 기능, 안정성, 성능 및 기능을 제공합니다.  

  - **라우터 구성** 라우터가 다음과 같이 구성되어 있는지 확인합니다.  

    -   라우터에서 UPnP 프레임워크가 사용됩니다.  

    -   LAN에 대한 DHCP(Dynamic Host Configuration Protocol) 서버 서비스를 사용하거나 사용하지 않도록 설정할 수 있습니다.  Windows Server Essentials에서 DHCP가 서버와 라우터에서 모두 실행 되 고 있지 않은지 확인 합니다. 라우터에서 DHCP를 사용 하는 경우 설치 하는 동안 DHCP가 서버에서 사용 되지 않습니다.  

    -   라우터의 외부 인터페이스에 대한 IP 주소가 있으며 이 주소는 ISP(인터넷 서비스 공급자)에서 제공합니다. IP 주소는 ISP의 DHCP 서버 서비스에서 동적으로 할당될 수 있습니다. 아니면 라우터 관리 콘솔을 사용하여 수동으로 정적 IP 주소를 구성해야 합니다.  

    -   인터넷에 연결하는 데 사용자 이름과 암호 및 PPPoE(Point-to-Point Protocol over Ethernet)가 필요한 경우 라우터가 UPnP 프레임워크를 지원하는 경우에도 라우터에서 이러한 설정이 구성됩니다.  

    -   라우터가 LAN 및 인터넷에 연결되어 있으며, 켜져 있고, 제대로 작동하고 있습니다.  

    라우터가 UPnP 프레임워크를 지원하지 않는 경우 또는 설치 도중 라우터를 구성할 수 없는 경우 네트워크 설정을 사용하여 수동으로 라우터를 구성해야 합니다. 다음 포트가 열려 있으며 대상 서버의 IP 주소로 보내지는지 확인하세요.  

  |포트 번호|응용 프로그램|  
  |-----------------|-----------------|  
  |포트 80|HTTP 웹 트래픽|  
  |포트 443|HTTPS 웹 트래픽|  


- **Windows Server Essentials 릴리스 설명서를 참조**하세요. 릴리스 문서에는 Windows Server Essentials를 올바르게 설치 하 고 구성 하는 데 중요 한 최신 정보가 포함 되어 있습니다. 릴리스 문서를 보거나 인쇄 하려면 [Windows Server Essentials에 대 한 릴리스 설명서](../get-started/release-notes.md)를 참조 하세요.  

## <a name="see-also"></a>참고 항목  

-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)

