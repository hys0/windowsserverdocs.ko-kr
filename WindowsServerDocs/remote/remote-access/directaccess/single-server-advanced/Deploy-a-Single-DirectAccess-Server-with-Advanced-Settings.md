---
title: 고급 설정을 사용하여 단일 DirectAccess 서버 배포
description: 이 항목은 고급 설정을 Windows Server 2016 용으로 단일 DirectAccess 서버 배포 가이드의 일부
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b211a9ca-1208-4e1f-a0fe-26a610936c30
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 260926e4818ef95db85d00af02a4fa87665ad709
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864654"
---
# <a name="deploy-a-single-directaccess-server-with-advanced-settings"></a>고급 설정을 사용하여 단일 DirectAccess 서버 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 단일 DirectAccess 서버를 사용 하 고 고급 설정을 사용 하 여 DirectAccess를 배포할 수 있는 DirectAccess 시나리오를 소개 합니다.  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>배포를 시작하기 전에 지원되지 않는 구성, 알려진 문제 및 사전 요구 사항 목록을 참조하세요.  
DirectAccess를 배포 하기 전에 필수 구성 요소 및 기타 정보를 검토 하려면 다음 항목을 사용할 수 있습니다.  
  
-   [DirectAccess 지원 되지 않는 구성](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [DirectAccess를 배포 하기 위한 필수 구성 요소](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="BKMK_OVER"></a>시나리오 설명  
이 시나리오에서는 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 단일 컴퓨터는 고급 설정 사용 하 여 DirectAccess 서버로 구성 됩니다.  
  
> [!NOTE]  
> 간단한 설정만으로 기본 배포를 구성하려면 [Deploy a Single DirectAccess Server Using the Getting Started Wizard](../../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)를 참조하세요. 간단한 시나리오에서는 DirectAccess가 CA(인증 기관) 또는 Active Directory 보안 그룹과 같은 인프라 설정 구성 없이 마법사를 사용하여 기본 설정으로 설치됩니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
고급 설정을 사용하여 단일 DirectAccess 서버를 설정하려면 몇 가지 계획 및 배포 단계를 완료해야 합니다.  
  
### <a name="prerequisites"></a>사전 요구 사항  
시작하기 전에 다음 요구 사항을 검토할 수 있습니다.  
  
-   모든 프로필에서 Windows 방화벽을 사용해야 합니다.  
  
-   DirectAccess 서버가 네트워크 위치 서버입니다.  
  
-   DirectAccess 서버를 설치하는 도메인의 모든 무선 컴퓨터에서 DirectAccess를 사용할 수 있습니다. DirectAccess를 배포하면 현재 도메인의 모든 모바일 컴퓨터에서 자동으로 사용하도록 설정됩니다.  
  
> [!IMPORTANT]  
> DirectAccess를 배포할 때 일부 기술 및 구성은 지원되지 않습니다.  
>   
> -   회사 네트워크의 ISATAP(Intra-Site Automatic Tunnel Addressing Protocol)는 지원되지 않습니다. ISATAP를 사용 중인 경우 이를 제거하고 기본 IPv6을 사용해야 합니다.  
  
### <a name="planning-steps"></a>계획 단계  
계획은 두 개의 단계로 나누어집니다.  
  
1.  **DirectAccess 인프라 계획**. 이 단계에서는 DirectAccess 배포를 시작하기 전에 네트워크 인프라를 설치하는 데 필요한 계획에 대해 설명하며, 네트워크 및 서버 토폴로지, 인증서 계획, DNS, Active Directory 및 GPO(그룹 정책 개체) 구성, DirectAccess 네트워크 위치 서버 계획이 포함됩니다.  
  
2.  **DirectAccess 배포 계획**. 이 단계에서는 DirectAccess 배포를 준비하는 데 필요한 계획 단계에 대해 설명하며, DirectAccess 클라이언트 컴퓨터, 서버 및 클라이언트 인증 요구 사항, VPN 설정, 인프라 서버, 관리 및 응용 프로그램 서버 계획이 포함됩니다.  
  
### <a name="deployment-steps"></a>배포 단계  
배포는 세 개의 단계로 나누어집니다.  
  
1.  **DirectAccess 인프라 구성**. 이 단계에는 네트워크 및 라우팅 구성, 필요한 경우 방화벽 설정 구성, 인증서, DNS 서버, Active Directory, GPO 설정 및 DirectAccess 네트워크 위치 서버 구성이 포함됩니다.  
  
2.  **DirectAccess 서버 설정 구성**. 이 단계에는 DirectAccess 클라이언트 컴퓨터, DirectAccess 서버, 인프라 서버, 관리 및 응용 프로그램 서버 구성을 위한 단계가 포함됩니다.  
  
3.  **배포 확인**. 이 단계에는 DirectAccess 배포를 확인하는 단계가 포함됩니다.  
  
자세한 배포 단계는 [Install and Configure Advanced DirectAccess](../../../remote-access/directaccess/single-server-advanced/Install-and-Configure-Advanced-DirectAccess.md)을 참조하세요.  
  
## <a name="BKMK_APP"></a>실제 응용 프로그램  
단일 DirectAccess 서버를 배포하면 다음과 같은 이점이 있습니다.  
  
-   **편리한 액세스**. Windows 10, Windows 8.1, Windows 8 및 Windows 7을 실행 하는 관리 되는 클라이언트 컴퓨터를 DirectAccess 클라이언트 컴퓨터로 구성할 수 있습니다. 이러한 클라이언트는 인터넷에 있는 동안 언제든지 VPN 연결에 로그인할 필요 없이 DirectAccess를 통해 내부 네트워크 리소스에 액세스할 수 있습니다. 이러한 운영 체제 중 하나가 실행되지 않는 클라이언트 컴퓨터는 VPN을 통해 내부 네트워크에 연결할 수 있습니다.  
  
-   **편리한 관리**. 인터넷에 있는 DirectAccess 클라이언트 컴퓨터가 내부 회사 네트워크에 없는 경우에도 원격 액세스 관리자가 DirectAccess를 통해 원격으로 관리할 수 있습니다. 회사 요구 사항을 충족하지 않는 클라이언트 컴퓨터를 관리 서버에서 자동으로 업데이트할 수 있습니다. DirectAccess와 VPN은 모두 동일한 콘솔에서 동일한 마법사 집합으로 관리됩니다. 또한 하나 이상의 DirectAccess 서버를 단일 원격 액세스 관리 콘솔에서 관리할 수 있습니다.  
  
## <a name="BKMK_NEW"></a>이 시나리오에 필요한 역할 및 기능  
다음 표에는 이 시나리오에 필요한 역할 및 기능이 나와 있습니다.  
  
|역할/기능|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|원격 액세스 역할|이 역할은 서버 관리자 콘솔이나 Windows PowerShell을 사용하여 설치 및 제거됩니다. 이 역할에는 DirectAccess와 RRAS(라우팅 및 원격 액세스 서비스)가 둘 다 포함됩니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br/><br/>1.  DirectAccess와 RRAS VPN입니다. DirectAccess 및 VPN 원격 액세스 관리 콘솔에서 함께 관리 됩니다.<br/>2.  RRAS 라우팅입니다. RRAS 라우팅 기능은 레거시 라우팅 및 원격 액세스 콘솔에서 관리 됩니다.<br /><br />원격 액세스 서버 역할은 다음과 같은 서버 역할/기능에 종속됩니다.<br/><br/> 인터넷 정보 서비스 (IIS) 웹 서버-이 기능은 네트워크 위치 서버가 DirectAccess 서버와 기본 웹 프로브를 구성 해야 합니다.<br/> -Windows 내부 데이터베이스입니다. DirectAccess 서버에서 로컬 계정 사용 합니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치 됩니다.<br /><br />-이 값은 원격 액세스 역할이 설치 되어 있고 원격 관리 콘솔 사용자 인터페이스 및 Windows PowerShell cmdlet을 지원 하는 경우 기본적으로 DirectAccess 서버에 설치 됩니다.<br />-선택적으로 설치할 수 없습니다 DirectAccess 서버 역할을 실행 하는 서버에서. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<br /><br />원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<br /><br />-원격 액세스 그래픽 사용자 인터페이스 (GUI)<br />-Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />그룹 정책 관리 콘솔<br />RAS 연결 관리자 관리 키트 (CMAK)<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
  
## <a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  
  
-   서버 요구 사항:  
  
    -   Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012에 대 한 하드웨어 요구 사항을 충족 하는 컴퓨터.  
  
    -   서버에는 네트워크 어댑터가 하나 이상 설치되어 있고, 사용하도록 설정되어 있어야 하며, 서버가 내부 네트워크에 연결되어 있어야 합니다. 두 개의 어댑터가 사용된 경우 하나의 어댑터는 내부 회사 네트워크에 연결되어야 하고 나머지 하나는 외부 네트워크(인터넷 또는 개인 네트워크)에 연결되어야 합니다.  
  
    -   Teredo가 IPv4-IPv6 전환 프로토콜로 필요한 경우 서버의 외부 어댑터에 연속된 두 개의 공용 IPv4 주소가 있어야 합니다. 단일 IP 주소를 사용할 수 있는 경우 IP-HTTPS만 전환 프로토콜로 사용할 수 있습니다.  
  
    -   도메인 컨트롤러가 하나 이상 있어야 합니다. DirectAccess 서버와 DirectAccess 클라이언트가 도메인 구성원이어야 합니다.  
  
    -   IP-HTTPS 또는 네트워크 위치 서버에 자체 서명된 인증서를 사용하지 않거나 클라이언트 IPsec 인증에 클라이언트 인증서를 사용하려면 CA(인증 기관)가 필요합니다. 또는 공용 CA에서 인증서를 요청할 수 있습니다.  
  
    -   네트워크 위치 서버가 DirectAccess 서버에 없는 경우에는 실행할 별도의 서버가 필요합니다.  
  
-   클라이언트 요구 사항:  
  
    -   Windows 10, Windows 8 또는 Windows 7 클라이언트 컴퓨터를 실행 되어야 합니다.  
  
        > [!NOTE]  
        > 운영 체제만 DirectAccess 클라이언트로 사용할 수 있습니다. Windows 10, Windows Server 2012 R2, Windows Server 2012, Windows 8 Enterprise, Windows 7 Enterprise 또는 Windows 7 Ultimate  
  
-   인프라 및 관리 서버 요구 사항:  
  
    -   DirectAccess 클라이언트 컴퓨터를 원격으로 관리하는 동안 클라이언트는 도메인 컨트롤러, 시스템 센터 구성 서버, 그리고 Windows와 바이러스 백신 업데이트 및 NAP(네트워크 액세스 보호) 클라이언트 준수 등 서비스의 HRA(상태 등록 기관) 서버 같은 관리 서버와 통신을 시작합니다. 필요한 서버는 원격 액세스 배포가 시작되기 전에 배포되어 있어야 합니다.  
  
    -   원격 액세스에서 클라이언트 NAP 준수가 필요한 경우, NPS 및 HRS 서버는 원격 액세스 배포가 시작되기 전에 배포되어 있어야 합니다.  
  
    -   VPN이 사용하도록 설정되어 있으면 고정 주소 풀이 사용되지 않는 경우 IP 주소를 VPN 클라이언트에 자동으로 할당하기 위해 DHCP 서버가 필요합니다.  
  
## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오에 필요한 요구 사항은 다음과 같이 다양합니다.  
  
-   서버 요구 사항:  
  
    -   DirectAccess 서버가 도메인 구성원이어야 합니다. 서버는 내부 네트워크의 경계면 또는 다른 장치의 경계면 방화벽 뒤에 배포될 수 있습니다.  
  
    -   DirectAccess 서버가 경계면 방화벽이나 NAT 장치 뒤에 있는 경우, 이 장치는 DirectAccess 서버와 트래픽을 주고받을 수 있도록 구성되어 있어야 합니다.  
  
    -   서버에 원격 액세스를 배포하는 사람에게는 서버에 대한 로컬 관리자 권한과 도메인 사용자 권한이 필요합니다. 또한 관리자에게는 DirectAccess 배포에 사용되는 GPO 사용 권한이 필요합니다. 이동 컴퓨터에만 DirectAccess를 배포하도록 제한하는 기능을 활용하려면 도메인 컨트롤러에서 WMI 필터를 만들 수 있는 권한이 필요합니다.  
  
-   원격 액세스 클라이언트 요구 사항:  
  
    -   DirectAccess 클라이언트가 도메인 구성원이어야 합니다. 클라이언트가 포함된 도메인은 DirectAccess 서버와 동일한 포리스트에 속하거나, 양방향 트러스트가 DirectAccess 서버 포리스트나 도메인과 함께 있을 수 있습니다.  
  
    -   Active Directory 보안 그룹은 DirectAccess 클라이언트로 구성될 컴퓨터를 포함하는 데 필요합니다. DirectAccess 클라이언트 설정을 구성할 때 보안 그룹이 지정되지 않은 경우 기본적으로 도메인 컴퓨터 보안 그룹의 모든 노트북 컴퓨터에 클라이언트 GPO가 적용됩니다.  
  
        > [!NOTE]  
        > DirectAccess 클라이언트 컴퓨터가 포함된 각 도메인에 대한 보안 그룹을 만드는 것이 좋습니다.  
  
        > [!IMPORTANT]  
        > DirectAccess 배포에서 Teredo를 활성화 하 고 Windows 7 클라이언트에 액세스할 수 있는지 확인 하려는 경우 클라이언트는 Windows 7 sp1으로 업그레이드 됩니다. Windows 7 RTM을 사용 하는 클라이언트는 Teredo를 통해 연결할 수 없습니다. 그러나 여전히 IP HTTPS를 통해 회사 네트워크에 연결할 수는 있습니다.  
  
## <a name="BKMK_LINKS"></a>참고 항목  
다음 표에는 추가 리소스에 대한 링크가 나와 있습니다.  
  
|콘텐츠 형식|참조|  
|--------|-------|  
|**배포**|[Windows Server의 DirectAccess 배포 경로](../../../remote-access/directaccess/DirectAccess-Deployment-Paths-in-Windows-Server.md)<br /><br />[시작된 마법사를 사용 하 여 단일 DirectAccess 서버 배포](../../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|  
|**도구 및 설정**|[원격 액세스 PowerShell cmdlet](https://technet.microsoft.com/library/hh918399.aspx)|  
|**커뮤니티 리소스**|[DirectAccess 서바이벌 가이드](https://social.technet.microsoft.com/wiki/contents/articles/23210.directaccess-survival-guide.aspx)<br /><br />[DirectAccess Wiki 항목](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**관련 기술**|[IPv6 작동 방법](https://technet.microsoft.com/library/cc781672(v=WS.10).aspx)|  
  


