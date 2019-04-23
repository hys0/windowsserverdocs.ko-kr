---
title: 2 단계 기본 DirectAccess 배포 계획
description: 이 항목은 시작 시작 마법사에 대 한 Windows Server 2016을 사용 하 여 단일 DirectAccess 서버 배포 가이드의 일부
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ddcb162-dd92-406c-acab-d3de7239c644
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8c21b7fa62246170caeb07cb5865c1ff311e0f09
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848754"
---
# <a name="step-2-plan-the-basic-directaccess-deployment"></a>2 단계 기본 DirectAccess 배포 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016

DirectAccess 인프라를 계획 한 후 기본 설정 사용 하 여 단일 서버에서 DirectAccess를 배포의 다음 단계에서는 시작 마법사에 대 한 설정을 계획 하는 것입니다.  
  
|태스크|설명|  
|----|--------|  
|클라이언트 배포 계획|기본적으로 시작 마법사 DirectAccess를 배포 모든 랩톱 및 노트북 컴퓨터가 도메인의 클라이언트 설정 GPO에 WMI 필터를 적용 하 여|  
|DirectAccess 서버 배포 계획|DirectAccess 서버를 배포할 방법을 계획합니다.|  
  
## <a name="bkmk_2_1_client"></a>클라이언트 배포 계획  
클라이언트 배포를 계획할 때 결정해야 하는 두 가지 사항이 있습니다.  
  
1.  DirectAccess를 이동 컴퓨터에서만 사용할 수 있나요, 아니면 모든 컴퓨터에서 사용할 수 있나요?  
  
    시작 마법사에서 DirectAccess 클라이언트를 구성할 때 DirectAccess를 사용 하 여 연결 된 지정 된 보안 그룹의 이동 컴퓨터 에서만 허용 하도록 선택할 수 있습니다. 모바일 컴퓨터에 대 한 액세스를 제한 하는 경우 DirectAccess는 자동으로 DirectAccess 클라이언트 GPO가 지정된 된 보안 그룹의 이동 컴퓨터에만 적용 되도록 WMI 필터를 구성 합니다. DirectAccess 관리자를 만들거나이 설정을 사용 하도록 설정 하려면 그룹 정책 WMI 필터 수정 권한이 필요 합니다.  
  
2.  DirectAccess 클라이언트 컴퓨터가 어떤 보안 그룹에 포함되나요?  
  
    DirectAccess 설정은 DirectAccess 클라이언트 GPO에 포함됩니다. 시작 마법사에서 지정 하는 보안 그룹의 일부인 컴퓨터에 적용 됩니다. 지원되는 모든 도메인에 보안 그룹이 포함되도록 지정할 수 있습니다. DirectAccess를 구성 하기 전에 보안 그룹을 만들어야 합니다. DirectAccess 배포를 완료 한 후 보안 그룹에 컴퓨터를 추가할 수 있지만 보안 그룹에 다른 도메인에 상주 하는 클라이언트 컴퓨터를 추가 하는 경우는 이러한 클라이언트에 클라이언트 GPO은 적용 되지 않습니다. 예를 들어 도메인 A에 DirectAccess 클라이언트에 대한 SG1을 만들고 나중에 도메인 B의 클라이언트를 이 그룹에 추가하는 경우 도메인 B의 클라이언트에는 클라이언트 GPO가 적용되지 않습니다. 이 문제를 방지하려면 클라이언트 컴퓨터가 포함된 각 도메인에 대한 새 클라이언트 보안 그룹을 만들어야 합니다. 또는 새 보안 그룹을 만들지 않으려면 새 도메인의 새 GPO 이름으로 Add-DAClient cmdlet을 실행합니다.  
  
## <a name="bkmk_2_2_server"></a>DirectAccess 서버 배포 계획  
DirectAccess 서버 배포를 계획할 때 결정할 수 있습니다.  
  
-   **네트워크 토폴로지** -두 가지 토폴로지가 있습니다 제공 하는 DirectAccess 서버를 배포 하는 경우:  
  
    -   **두 어댑터** -내부 네트워크에 연결 된 다른 및 두 개의 네트워크 어댑터, DirectAccess는 인터넷에 직접 연결 하는 하나의 네트워크 어댑터를 사용 하 여 구성할 수 있습니다. 또는 방화벽이나 라우터와 같은 에지 장치 뒤에 서버가 설치됩니다. 이 구성에서는 네트워크 어댑터가 경계 네트워크와 내부 네트워크에 각각 하나씩 연결됩니다.  
  
    -   **단일 네트워크 어댑터** -이 구성 된 DirectAccess 서버는 방화벽이 나 라우터와 같은 지 장치 뒤 설치 됩니다. 네트워크 어댑터는 내부 네트워크에 연결됩니다.  
  
-   **네트워크 어댑터** -DirectAccess 마법사는 DirectAccess 서버에 구성 된 네트워크 어댑터를 자동으로 검색 합니다. 올바른 어댑터에서 선택 되어 있는지 가능 합니다 **검토** 페이지입니다.  
  
-   **IP-HTTPS 인증서** -마법사 IP-HTTPS와 네트워크 위치 서버 (인증서가 없는) 하는 경우에 대 한 자체 서명 된 인증서를 자동으로 프로 비전 하 고 자동으로 사용 하도록이 배포에 필요한 PKI 이므로 Kerberos 프록시입니다. 또한 마법사에 IPv4 전용 환경에서의 프로토콜 변환에 NAT64 및 DNS64 수 있습니다. 마법사가 구성을 적용하고 나면 **닫기**를 클릭합니다.  
  
-   **Windows 7 클라이언트** -시작 마법사에서 Windows 7 클라이언트에 대 한 지원을 사용할 수 없습니다. 이 고급 설치 마법사에서 사용할 수 있습니다. 자세한 내용은 참조 하세요. [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다.  
  
-   **VPN 구성** -DirectAccess를 구성 하기 전에 원격 클라이언트에 대 한 VPN 액세스를 제공 하려는 경우를 결정 합니다. DirectAccess 연결을 지원 하지 않는 조직의 클라이언트 컴퓨터가 있는 경우 VPN 액세스를 제공 해야 (중 하나에 관리 되지 있거나, DirectAccess는 지원 되지 않습니다는 운영 체제를 실행). 시작 마법사는 DHCP를 사용 하 여 VPN IP 주소 할당을 구성 하 고 Active Directory를 사용 하 여 인증 하도록 VPN 클라이언트를 구성 합니다.  
  
-   **강제 터널링** -강제 터널링을 사용할 계획 이거나 나중에 추가할 수 있습니다, 경우에 사용 해야 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) 2 터널 구성을 배포 합니다. 보안 고려 사항으로 인해 단일 터널 구성에서 강제 터널링 지원 되지 않습니다.  
  
## <a name="BKMK_Links"></a>이전 단계  
  
-   [1단계: 기본 DirectAccess 인프라 계획](da-basic-plan-s1-infrastructure.md)  
  


