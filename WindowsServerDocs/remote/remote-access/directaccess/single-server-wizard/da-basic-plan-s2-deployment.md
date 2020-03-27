---
title: 2 단계 기본 DirectAccess 배포 계획
description: 이 항목은 Windows Server 2016에 대 한 시작 마법사를 사용 하 여 단일 DirectAccess 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ddcb162-dd92-406c-acab-d3de7239c644
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2d9480b3f021fcf1086ca8001997a1c7c1b56456
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308912"
---
# <a name="step-2-plan-the-basic-directaccess-deployment"></a>2 단계 기본 DirectAccess 배포 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

DirectAccess 인프라를 계획 한 후 기본 설정을 사용 하 여 단일 서버에 DirectAccess를 배포 하는 다음 단계는 시작 마법사에 대 한 설정을 계획 하는 것입니다.  
  
|작업|설명|  
|----|--------|  
|클라이언트 배포 계획|기본적으로 시작 마법사는 클라이언트 설정 GPO에 WMI 필터를 적용 하 여 도메인의 모든 랩톱 및 노트북 컴퓨터에 DirectAccess를 배포 합니다.|  
|DirectAccess 서버 배포 계획|DirectAccess 서버를 배포할 방법을 계획합니다.|  
  
## <a name="planning-for-client-deployment"></a><a name="bkmk_2_1_client"></a>클라이언트 배포 계획  
클라이언트 배포를 계획할 때 결정해야 하는 두 가지 사항이 있습니다.  
  
1.  DirectAccess를 이동 컴퓨터에서만 사용할 수 있나요, 아니면 모든 컴퓨터에서 사용할 수 있나요?  
  
    시작 마법사에서 DirectAccess 클라이언트를 구성할 때 지정 된 보안 그룹의 모바일 컴퓨터만 DirectAccess를 사용 하 여 연결할 수 있도록 허용 하도록 선택할 수 있습니다. 모바일 컴퓨터에 대 한 액세스를 제한 하는 경우 DirectAccess 클라이언트 GPO가 지정 된 보안 그룹의 모바일 컴퓨터에만 적용 되도록 DirectAccess에서 자동으로 WMI 필터를 구성 합니다. DirectAccess 관리자가이 설정을 사용 하도록 설정 하려면 그룹 정책 WMI 필터를 만들거나 수정할 수 있는 권한이 있어야 합니다.  
  
2.  DirectAccess 클라이언트 컴퓨터가 어떤 보안 그룹에 포함되나요?  
  
    DirectAccess 설정은 DirectAccess 클라이언트 GPO에 포함됩니다. 이 GPO는 시작 마법사에서 지정한 보안 그룹의 일부인 컴퓨터에 적용 됩니다. 지원되는 모든 도메인에 보안 그룹이 포함되도록 지정할 수 있습니다. DirectAccess를 구성 하기 전에 보안 그룹을 만들어야 합니다. DirectAccess 배포를 완료 한 후 보안 그룹에 컴퓨터를 추가할 수 있지만, 다른 도메인에 있는 클라이언트 컴퓨터를 보안 그룹에 추가 하는 경우 해당 클라이언트에는 클라이언트 GPO가 적용 되지 않습니다. 예를 들어 도메인 A에 DirectAccess 클라이언트에 대한 SG1을 만들고 나중에 도메인 B의 클라이언트를 이 그룹에 추가하는 경우 도메인 B의 클라이언트에는 클라이언트 GPO가 적용되지 않습니다. 이 문제를 방지하려면 클라이언트 컴퓨터가 포함된 각 도메인에 대한 새 클라이언트 보안 그룹을 만들어야 합니다. 또는 새 보안 그룹을 만들지 않으려면 새 도메인의 새 GPO 이름으로 Add-DAClient cmdlet을 실행합니다.  
  
## <a name="planning-for-directaccess-server-deployment"></a><a name="bkmk_2_2_server"></a>DirectAccess 서버 배포 계획  
DirectAccess 서버 배포를 계획할 때 결정 해야 할 몇 가지 사항이 있습니다.  
  
-   **네트워크 토폴로지** -DirectAccess 서버를 배포할 때 두 가지 토폴로지를 사용할 수 있습니다.  
  
    -   두 **개의 어댑터** -두 개의 네트워크 어댑터를 사용 하 여 DirectAccess는 인터넷에 직접 연결 된 네트워크 어댑터 하나를 사용 하 여 구성할 수 있으며 다른 네트워크 어댑터는 내부 네트워크에 연결 됩니다. 또는 방화벽이나 라우터와 같은 에지 디바이스 뒤에 서버가 설치됩니다. 이 구성에서는 네트워크 어댑터가 경계 네트워크와 내부 네트워크에 각각 하나씩 연결됩니다.  
  
    -   **단일 네트워크 어댑터** -이 구성에서는 방화벽이 나 라우터와 같은에 지 장치 뒤에 DirectAccess 서버가 설치 됩니다. 네트워크 어댑터는 내부 네트워크에 연결됩니다.  
  
-   **네트워크 어댑터** -directaccess 마법사는 directaccess 서버에 구성 된 네트워크 어댑터를 자동으로 검색 합니다. **검토** 페이지에서 올바른 어댑터를 선택 했는지 확인할 수 있습니다.  
  
-   **Ip-https 인증서** -이 배포에는 PKI가 필요 하지 않으므로 마법사는 Ip-https 및 네트워크 위치 서버 (인증서가 없는 경우)에 대해 자체 서명 된 인증서를 자동으로 프로 비전 하 고 Kerberos 프록시를 자동으로 사용 하도록 설정 합니다. 또한 마법사는 IPv4 전용 환경에서 프로토콜 변환에 대해 NAT64 및 DNS64를 사용 하도록 설정 합니다. 마법사가 구성을 적용하고 나면 **닫기**를 클릭합니다.  
  
-   **Windows 7 클라이언트** -시작 마법사에서 windows 7 클라이언트에 대 한 지원을 사용 하도록 설정할 수 없습니다. 이는 고급 설치 마법사에서 사용 하도록 설정할 수 있습니다. 자세한 내용은 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)를 참조 하세요.  
  
-   **Vpn 구성** -DirectAccess를 구성 하기 전에 원격 클라이언트에 대 한 VPN 액세스를 제공할지 여부를 결정 합니다. DirectAccess 연결을 지원 하지 않는 조직의 클라이언트 컴퓨터가 있는 경우 (관리 되지 않거나 DirectAccess가 지원 되지 않는 운영 체제를 실행 하기 때문에) VPN 액세스를 제공 해야 합니다. 시작 마법사는 DHCP를 사용 하 여 VPN IP 주소 할당을 구성 하 고 Active Directory를 사용 하 여 VPN 클라이언트를 인증 하도록 구성 합니다.  
  
-   **강제 터널링** -강제 터널링을 사용할 예정 이거나 나중에 추가할 수 있는 경우 [고급 설정으로 단일 DirectAccess 서버 배포](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) 를 사용 하 여 두 개의 터널 구성을 배포 해야 합니다. 보안을 고려 하 여 단일 터널 구성의 강제 터널링은 지원 되지 않습니다.  
  
## <a name="previous-step"></a><a name="BKMK_Links"></a>이전 단계  
  
-   [1 단계: 기본 DirectAccess 인프라 계획](da-basic-plan-s1-infrastructure.md)  
  


