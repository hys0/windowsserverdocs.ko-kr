---
title: 시작 마법사를 사용하여 단일 DirectAccess 서버 배포
description: 이 항목은 Windows Server 2016에 대 한 시작 마법사를 사용 하 여 단일 DirectAccess 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: eb0cf464-0668-40f8-8222-feb6bae6d3d5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 13b3fdea120a857cc0c8e890bba87c13823c3a38
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819566"
---
# <a name="deploy-a-single-directaccess-server-using-the-getting-started-wizard"></a>시작 마법사를 사용하여 단일 DirectAccess 서버 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 단일 DirectAccess 서버를 사용하며 몇 가지 간단한 단계로 DirectAccess를 배포할 수 있는 DirectAccess 시나리오를 소개합니다.  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>배포를 시작하기 전에 지원되지 않는 구성, 알려진 문제 및 사전 요구 사항 목록을 참조하세요.  
DirectAccess를 배포 하기 전에 다음 항목을 사용 하 여 필수 구성 요소 및 기타 정보를 검토할 수 있습니다.  
  
-   [DirectAccess에서 지원되지 않는 구성](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [DirectAccess를 배포하기 위한 필수 조건](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>시나리오 설명  
이 시나리오에서는 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 단일 컴퓨터가 몇 가지 간단한 마법사 단계에서 기본 설정을 사용 하 여 DirectAccess 서버로 구성 됩니다. CA (인증 기관) 또는 Active Directory 보안 그룹  
  
> [!NOTE]  
> 사용자 지정 설정으로 고급 배포를 구성하려는 경우 [Deploy a Single DirectAccess Server with Advanced Settings](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)를 참조합니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
기본 DirectAccess 서버를 설정 하려면 몇 가지 계획 및 배포 단계가 필요 합니다.  
  
### <a name="prerequisites"></a>필수 조건  
이 시나리오의 배포를 시작하기 전에 다음 목록에서 중요한 요구 사항을 검토하세요.  
  
-   모든 프로필에서 Windows 방화벽을 사용해야 합니다.  
  
-   이 시나리오는 클라이언트 컴퓨터에서 Windows 10, Windows 8.1 또는 Windows 8을 실행 하는 경우에만 지원 됩니다.  
  
-   회사 네트워크의 ISATAP는 지원되지 않습니다. ISATAP를 사용 중인 경우 이를 제거하고 기본 IPv6을 사용해야 합니다.  
  
-   공개 키 인프라가 필요하지 않습니다.  
  
-   2단계 인증 배포에는 지원되지 않습니다. 인증에 도메인 자격 증명이 필요합니다.  
  
-   현재 도메인의 모든 모바일 컴퓨터에 DirectAccess를 자동으로 배포합니다.  
  
-   인터넷 트래픽이 DirectAccess 터널을 통해 전달되지 않습니다. 강제 터널 구성이 지원되지 않습니다.  
  
-   DirectAccess 서버가 네트워크 위치 서버입니다.  
  
-   NAP(네트워크 액세스 보호)는 지원되지 않습니다.  
  
-   DirectAccess 관리 콘솔 또는 PowerShell cmdlet 외부에서 정책을 변경하는 것이 지원되지 않습니다.  
  
-   지금 또는 나중에 멀티 사이트를 배포 하려면 먼저 [고급 설정을 사용 하 여 단일 DirectAccess 서버를 배포](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다.  
  
### <a name="planning-steps"></a>계획 단계  
계획은 두 개의 단계로 나누어집니다.  
  
1.  DirectAccess 인프라 계획. 이 단계에서는 DirectAccess 배포를 시작하기 전에 네트워크 인프라를 설치하는 데 필요한 계획에 대해 설명하며, 네트워크, 서버 토폴로지 및 DirectAccess 네트워크 위치 서버 계획이 포함됩니다.  
  
2.  DirectAccess 배포 계획. 이 단계에서는 DirectAccess 배포를 준비하는 데 필요한 계획 단계에 대해 설명하며, DirectAccess 클라이언트 컴퓨터, 서버 및 클라이언트 인증 요구 사항, VPN 설정, 인프라 서버, 관리 및 응용 프로그램 서버 계획이 포함됩니다.  
  
자세한 계획 단계는 [고급 DirectAccess 배포 계획](../../../remote-access/directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md)을 참조 하세요.  
  
### <a name="deployment-steps"></a>배포 단계  
배포는 세 개의 단계로 나누어집니다.  
  
1.  DirectAccess 인프라 구성-이 단계에는 네트워크 및 라우팅 구성, 필요한 경우 방화벽 설정 구성, 인증서, DNS 서버, Active Directory 및 GPO 설정, DirectAccess 네트워크 위치 구성 등이 포함 됩니다. 서버인.  
  
2.  DirectAccess 서버 설정을 구성 하는 중입니다. 이 단계에는 DirectAccess 클라이언트 컴퓨터, DirectAccess 서버, 인프라 서버, 관리 및 응용 프로그램 서버 구성을 위한 단계가 포함됩니다.  
  
3.  배포를 확인 하는 중입니다. 이 단계에는 필요에 따라 배포가 작동 하는지 확인 하는 단계가 포함 되어 있습니다.  
  
자세한 배포 단계는 [Install and Configure Basic DirectAccess](../../../remote-access/directaccess/single-server-wizard/Install-and-Configure-Basic-DirectAccess.md)을 참조하세요.  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>실용적인 응용 프로그램  
단일 원격 액세스 서버를 배포하면 다음과 같은 이점이 있습니다.  
  
-   편리한 액세스. Windows 10, Windows 8.1, Windows 8 또는 Windows 7을 실행 하는 관리 클라이언트 컴퓨터를 DirectAccess 클라이언트로 구성할 수 있습니다. 이러한 클라이언트는 인터넷에 있는 동안 언제든지 VPN 연결에 로그인할 필요 없이 DirectAccess를 통해 내부 네트워크 리소스에 액세스할 수 있습니다. 이러한 운영 체제 중 하나를 실행하지 않는 클라이언트 컴퓨터는 기존 VPN 연결을 사용하여 내부 네트워크에 연결할 수 있습니다.  
  
-   관리 용이성. 인터넷에 있는 DirectAccess 클라이언트 컴퓨터가 내부 회사 네트워크에 없는 경우에도 원격 액세스 관리자가 DirectAccess를 통해 원격으로 관리할 수 있습니다. 회사 요구 사항을 충족하지 않는 클라이언트 컴퓨터를 관리 서버에서 자동으로 업데이트할 수 있습니다. DirectAccess와 VPN은 모두 동일한 콘솔에서 동일한 마법사 집합으로 관리됩니다. 또한 하나 이상의 원격 액세스 서버를 단일 원격 액세스 관리 콘솔에서 관리할 수 있습니다.  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>이 시나리오에 포함 된 역할 및 기능  
다음 표에는 시나리오에 필요한 역할 및 기능이 나와 있습니다.  
  
|역할/기능|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|원격 액세스 역할|이 역할은 서버 관리자 콘솔이나 Windows PowerShell을 사용하여 설치 및 제거됩니다. 이 역할에는 DirectAccess(이전의 Windows Server 2008 R2 기능)와 라우팅 및 원격 액세스 서비스(이전의 NPAS(네트워크 정책 및 액세스 서비스) 서버 역할의 역할 서비스)가 모두 포함되어 있습니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<p>1. DirectAccess 및 RRAS (라우팅 및 원격 액세스 서비스) VPN. DirectAccess와 VPN은 원격 액세스 관리 콘솔에서 함께 관리 됩니다.<br />2. RRAS 라우팅. RRAS 라우팅 기능은 레거시 라우팅 및 원격 액세스 콘솔에서 관리 됩니다.<p>원격 액세스 서버 역할은 다음과 같은 서버 역할/기능에 종속됩니다.<p>-인터넷 정보 서비스 (IIS) 웹 서버-이 기능은 원격 액세스 서버에서 네트워크 위치 서버를 구성 하 고 기본 웹 프로브를 구성 하는 데 필요 합니다.<br />-Windows 내부 데이터베이스 원격 액세스 서버의 로컬 계정에 사용됩니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치됩니다.<p>-원격 액세스 역할이 설치 될 때 원격 액세스 서버에 기본적으로 설치 되며, 원격 관리 콘솔 사용자 인터페이스 및 Windows PowerShell cmdlet을 지원 합니다.<br />-앱는 하지 원격 액세스 서버 역할을 실행 하는 서버에 필요에 따라 설치 수 있습니다. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<p>원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<p>-원격 액세스 GUI<br />-Windows PowerShell 용 원격 액세스 모듈<p>이 기능은 다음 요소에 종속됩니다.<p>그룹 정책 관리 콘솔<br />RAS 연결 관리자 관리 키트 (CMAK)<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  
  
-   서버 요구 사항:  
  
    -   Windows server 2016, Windows Server 2012 R2 또는 Windows Server 2012의 하드웨어 요구 사항을 충족 하는 컴퓨터입니다.  
  
    -   서버에는 네트워크 어댑터가 하나 이상 설치되어 있고, 사용하도록 설정되어 있어야 하며, 서버가 내부 네트워크에 연결되어 있어야 합니다. 두 개의 어댑터가 사용된 경우 하나의 어댑터는 내부 회사 네트워크에 연결되어야 하고 나머지 하나는 외부 네트워크(인터넷 또는 프라이빗 네트워크)에 연결되어야 합니다.  
  
    -   도메인 컨트롤러가 하나 이상 있어야 합니다. 원격 액세스 서버와 DirectAccess 클라이언트가 도메인 구성원이어야 합니다.  
  
-   클라이언트 요구 사항:  
  
    -   클라이언트 컴퓨터는 Windows 10, Windows 8.1 또는 Windows 8을 실행 해야 합니다.  
  
        > [!IMPORTANT]  
        > 일부 또는 모든 클라이언트 컴퓨터에서 Windows 7을 실행 하는 경우 고급 설치 마법사를 사용 해야 합니다. 이 문서에서 설명 하는 시작 설치 마법사는 Windows 7을 실행 하는 클라이언트 컴퓨터를 지원 하지 않습니다. DirectAccess에서 Windows 7 클라이언트를 사용 하는 방법에 대 한 지침은 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) 를 참조 하세요.  
  
        > [!NOTE]  
        > Windows 10 Enterprise, Windows 8.1 Enterprise, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 8 Enterprise, Windows Server 2008 R2, Windows 7 Enterprise 및 운영 체제만 DirectAccess 클라이언트로 사용할 수 있습니다. Windows 7 Ultimate  
  
-   인프라 및 관리 서버 요구 사항:  
  
    -   VPN을 사용하도록 설정되어 있는 경우 고정 IP 주소 풀이 구성되어 있지 않으면 VPN 클라이언트에 IP 주소를 자동으로 할당하도록 DHCP 서버를 배포해야 합니다.  
  
-   Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 SP2 또는 Windows Server 2008 r 2를 실행 하는 DNS 서버가 필요 합니다.  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오에 필요한 요구 사항은 다음과 같이 다양합니다.  
  
-   서버 요구 사항:  
  
    -   원격 액세스 서버가 도메인 구성원이어야 합니다. 서버는 내부 네트워크의 경계면 또는 다른 장치의 경계면 방화벽 뒤에 배포될 수 있습니다.  
  
    -   원격 액세스 서버가 경계면 방화벽이나 NAT 장치 뒤에 있는 경우, 이 장치는 원격 액세스 서버와 트래픽을 주고받을 수 있도록 구성되어 있어야 합니다.  
  
    -   서버에 원격 액세스를 배포하는 사람에게는 서버에 대한 로컬 관리자 권한과 도메인 사용자 권한이 필요합니다. 또한 관리자에게는 DirectAccess 배포에 사용되는 GPO 사용 권한이 필요합니다. 이동 컴퓨터에만 DirectAccess를 배포하도록 제한하는 기능을 활용하려면 도메인 컨트롤러에서 WMI 필터를 만들 수 있는 권한이 필요합니다.  
  
-   원격 액세스 클라이언트 요구 사항:  
  
    -   DirectAccess 클라이언트가 도메인 구성원이어야 합니다. 클라이언트가 포함된 도메인은 원격 액세스 서버와 동일한 포리스트에 속하거나 원격 액세스 서버 포리스트와 양방향 트러스트 관계가 있을 수 있습니다.  
  
    -   Active Directory 보안 그룹은 DirectAccess 클라이언트로 구성될 컴퓨터를 포함하는 데 필요합니다. DirectAccess 클라이언트 설정을 구성할 때 보안 그룹이 지정되지 않은 경우 기본적으로 도메인 컴퓨터 보안 그룹의 모든 노트북 컴퓨터에 클라이언트 GPO가 적용됩니다. Windows Server 2016, windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise 및 Windows 7 Ultimate와 같은 운영 체제만 DirectAccess 클라이언트로 사용할 수 있습니다.  
  
## <a name="see-also"></a><a name="BKMK_LINKS"></a>참고 항목  
다음 표에는 추가 리소스에 대한 링크가 나와 있습니다.  
  
|콘텐츠 유형|참조|  
|--------|-------|  
|**TechNet의 원격 액세스**|[원격 액세스 TechCenter](https://technet.microsoft.com/network/bb545655.aspx)|  
|**도구 및 설정**|[원격 액세스 PowerShell cmdlet](https://technet.microsoft.com/library/hh918399.aspx)|  
|**커뮤니티 리소스**|[DirectAccess Wiki 항목](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**관련 기술**|[IPv6 작동 방법](https://technet.microsoft.com/library/cc781672(v=WS.10).aspx)|  
  


