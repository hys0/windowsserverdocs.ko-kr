---
title: 원격 액세스 관리
description: 이 항목에서는 Windows Server 2016에서 원격 액세스를 관리 하는 방법을 설명 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1459819a-b1b6-4800-8770-4a85d02c7a2b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3b2c251f99be455ec11e3ea3ef25ca14c8399de2
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282974"
---
# <a name="manage-remote-access"></a>원격 액세스 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

DirectAccess 원격 클라이언트 관리 배포 시나리오에서는 인터넷을 통해 클라이언트를 유지 관리하는 데 DirectAccess를 사용합니다. 이 섹션에서는 단계, 역할, 기능 및 추가 리소스에 대한 링크를 포함한 시나리오에 대해 설명합니다.  
  
Windows Server 2016 및 Windows Server 2012 DirectAccess 및 라우팅 및 원격 액세스 서비스 (RRAS) VPN 단일 원격 액세스 역할로 결합합니다.   
  
> [!NOTE]  
> 이 항목 외에도 다음과 같은 원격 액세스 관리 항목을 사용할 수 있습니다.  
>   
> -   [원격 액세스 모니터링 및 계정 사용](monitoring-and-accounting/Use-Remote-Access-Monitoring-and-Accounting.md)  
> -   [DirectAccess 클라이언트 원격 관리](manage-remote-clients/Manage-DirectAccess-Clients-Remotely.md)  
  
## <a name="BKMK_OVER"></a>시나리오 설명  
DirectAccess 클라이언트 컴퓨터는 사용자가 컴퓨터에 로그인했는지 여부에 관계없이 인터넷에 연결될 때마다 인트라넷에 연결됩니다. 따라서 인트라넷 리소스로 관리할 수 있으며 그룹 정책 변경, 운영 체제 업데이트, 맬웨어 방지 업데이트 및 기타 조직 구성 변경을 통해 최신 상태로 유지할 수 있습니다.  
  
일부 경우에는 인트라넷 서버 또는 컴퓨터에서 DirectAccess 클라이언트에 대한 연결을 시작해야 합니다. 예를 들어 지원 기술자는 원격 데스크톱 연결을 사용하여 원격 DirectAccess 클라이언트에 연결하고 이 클라이언트의 문제를 해결할 수 있습니다. 이 시나리오를 사용하면 기존의 원격 액세스 솔루션은 사용자 연결용으로 그대로 유지하면서 DirectAccess는 원격 관리용으로 사용할 수 있습니다.  
  
DirectAccess는 DirectAccess 클라이언트의 원격 관리를 지 원하는 구성을 제공 합니다. 클라이언트 컴퓨터의 원격 관리에 필요한 정책만 만들어지도록 제한하는 배포 마법사 옵션을 사용할 수 있습니다.  
  
> [!NOTE]  
> 이러한 배포에서는 강제 터널링, NAP(네트워크 액세스 보호) 통합 및 2단계 인증과 같은 사용자 수준 구성 옵션을 사용할 수 없습니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
DirectAccess 원격 클라이언트 관리 배포 시나리오는 다음과 같은 계획 및 구성 단계로 구성됩니다.  
  
### <a name="plan-the-deployment"></a>배포 계획  
이 시나리오를 계획하는 데 필요한 컴퓨터 및 네트워크 요구 사항은 다음의 몇 가지에 불과합니다. 해당 기능은 아래와 같습니다.  
  
-   **네트워크 및 서버 토폴로지**: DirectAccess를 사용하면 원격 액세스 서버를 인트라넷의 경계면 또는 NAT(네트워크 주소 변환) 장치나 방화벽의 뒤에 배치할 수 있습니다.  
  
-   **DirectAccess 네트워크 위치 서버**: 네트워크 위치 서버는 DirectAccess 클라이언트가 내부 네트워크에 있는지 확인하는 데 사용됩니다. 네트워크 위치 서버는 DirectAccess 서버 또는 다른 서버에 설치할 수 있습니다.  
  
-   **DirectAccess 클라이언트**: DirectAccess 클라이언트로 구성될 관리 컴퓨터를 정합니다.  
  
### <a name="configure-the-deployment"></a>배포 구성  
배포 구성은 여러 단계로 이루어져 있습니다. 이러한 개체는 다음과 같습니다.  
  
1.  **인프라 구성**: DNS 설정을 구성하고, 필요한 경우 서버 및 클라이언트 컴퓨터를 도메인에 가입시키며, Active Directory 보안 그룹을 구성합니다.  
  
    이 배포 시나리오에서 GPO(그룹 정책 개체)는 원격 액세스에 의해 자동으로 생성됩니다. 고급 인증서 GPO 옵션에 대해서 [고급 원격 액세스 배포](assetId:///3475e527-541f-4a34-b940-18d481ac59f6)합니다.  
  
2.  **원격 액세스 서버 및 네트워크 설정 구성**: 네트워크 어댑터, IP 주소 및 라우팅을 구성합니다.  
  
3.  **인증서 설정 구성**: 이 배포 시나리오에서는 시작 마법사 고급 인증서 인프라 구성 하지 않아도 되므로 자체 서명 된 인증서를 만듭니다.  
  
4.  **네트워크 위치 서버 구성**:  이 시나리오에서는 네트워크 위치 서버가 원격 액세스 서버에 설치됩니다.  
  
5.  **DirectAccess 관리 서버 계획**: 관리자는 인터넷을 사용하여 회사 네트워크 외부에 있는 DirectAccess 클라이언트 컴퓨터를 원격으로 관리할 수 있습니다. 관리 서버에는 원격 클라이언트 관리 중 사용되는 컴퓨터(예: 업데이트 서버)가 포함됩니다.  
  
6.  **원격 액세스 서버 구성**: 원격 액세스 역할을 설치하고 DirectAccess 시작 마법사를 실행하여 DirectAccess를 구성합니다.  
  
7.  **배포 확인**: 클라이언트를 테스트하여 DirectAccess로 내부 네트워크 및 인터넷에 연결할 수 있는지 확인합니다.  
  
## <a name="BKMK_APP"></a>실제 응용 프로그램  
DirectAccess 클라이언트를 관리하기 위해 단일 원격 액세스 서버를 배포하면 다음과 같은 이점이 있습니다.  
  
-   **편리한 액세스**: Windows 8 또는 Windows 7을 실행 하는 컴퓨터를 DirectAccess 클라이언트 컴퓨터로 구성할 수 있습니다 하는 클라이언트를 관리 합니다. 이러한 클라이언트는 VPN 연결에 로그인할 필요 없이 인터넷에 연결되어 있는 동안 언제든지 DirectAccess를 통해 내부 네트워크 리소스에 액세스할 수 있습니다. 이러한 운영 체제 중 하나가 실행되지 않는 클라이언트 컴퓨터는 VPN을 통해 내부 네트워크에 연결할 수 있습니다. DirectAccess와 VPN은 모두 동일한 콘솔에서 동일한 마법사 집합으로 관리됩니다.  
  
-   **편리한 관리**: 인터넷에 연결된 DirectAccess 클라이언트 컴퓨터는 회사 내부 네트워크에 없는 경우에도 원격 액세스 관리자가 DirectAccess를 사용하여 원격으로 관리할 수 있습니다. 회사 요구 사항을 충족하지 않는 클라이언트 컴퓨터를 관리 서버에서 자동으로 업데이트할 수 있습니다. 또한 하나 이상의 원격 액세스 서버를 단일 원격 액세스 관리 콘솔에서 관리할 수 있습니다.  
  
## <a name="BKMK_NEW"></a>역할과이 시나리오에 포함 된 기능  
다음 표에는 시나리오에 필요한 역할 및 기능이 나와 있습니다.  
  
|역할 또는 기능|이 시나리오를 지원하는 방법|  
|----------|-----------------|  
|*원격 액세스 역할*|이 역할은 서버 관리자 콘솔이나 Windows PowerShell을 사용하여 설치 및 제거됩니다. 이 역할에는 DirectAccess(이전의 Windows Server 2008 R2 기능)와 라우팅 및 원격 액세스 서비스(이전의 NPAS(네트워크 정책 및 액세스 서비스) 서버 역할의 역할 서비스)가 포함되어 있습니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br /><br />1.  DirectAccess와 RRAS(라우팅 및 원격 액세스 서비스) VPN: DirectAccess와 VPN은 원격 액세스 관리 콘솔에서 관리됩니다.<br />2.  RRAS: 기능은 라우팅 및 원격 액세스 콘솔에서 관리됩니다.<br /><br />원격 액세스 서버 역할은 다음과 같은 기능에 종속됩니다.<br /><br />웹 서버 (IIS): 네트워크 위치 서버와 기본 웹 프로브를 구성해야 합니다.<br />-Windows 내부 데이터베이스: 원격 액세스 서버의 로컬 계정에 사용됩니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치 됩니다.<br /><br />-기본적으로는 원격 액세스 서버에 원격 액세스 역할이 설치 되어 있고 원격 관리 콘솔 사용자 인터페이스를 지원 합니다.<br />서버에 대 한 옵션으로는 원격 액세스 서버 역할을 실행 되지 않습니다. 이 경우 원격 액세스 서버의 원격 관리에 사용됩니다.<br /><br />이 기능은 다음과 같은 항목으로 구성되어 있습니다.<br /><br />-원격 액세스 GUI 및 명령줄 도구<br />-Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />그룹 정책 관리 콘솔<br />RAS 연결 관리자 관리 키트 (CMAK)<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
  
## <a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  
  
### <a name="server-requirements"></a>서버 요구 사항  
  
-   Windows Server 2016의 하드웨어 요구 사항을 충족 하는 컴퓨터. 자세한 내용은 Windows Server 2016을 참조 하세요 [시스템 요구 사항](https://technet.microsoft.com/windows-server-docs/get-started/system-requirements-and-installation)합니다.  
  
-   서버에는 네트워크 어댑터가 하나 이상 설치되어 있고, 사용하도록 설정되어 있어야 합니다. 회사 내부 네트워크에 어댑터가 하나만 연결되어 있어야 하고, 외부 네트워크(인터넷)에도 어댑터가 하나만 연결되어 있어야 합니다.  
  
-   Teredo가 IPv6에서 IPv4로의 변환 프로토콜로 필요한 경우 서버의 외부 어댑터에는 연속된 두 개의 공용 IPv4 주소가 있어야 합니다. 단일 네트워크 어댑터를 사용할 수 있는 경우에는 IP-HTTPS만 변환 프로토콜로 사용할 수 있습니다.  
  
-   도메인 컨트롤러가 하나 이상 있어야 합니다. 원격 액세스 서버와 DirectAccess 클라이언트가 도메인 구성원이어야 합니다.  
  
-   IP-HTTPS 또는 네트워크 위치 서버에 자체 서명된 인증서를 사용하지 않거나 클라이언트 IPsec 인증에 클라이언트 인증서를 사용하려면 서버에 인증 기관이 필요합니다.  
  
### <a name="client-requirements"></a>클라이언트 요구 사항  
  
-   Windows 10 또는 Windows 8 또는 Windows 7 클라이언트 컴퓨터를 실행 되어야 합니다.  
  
### <a name="infrastructure-and-management-server-requirements"></a>인프라 및 관리 서버 요구 사항  
  
-   DirectAccess 클라이언트 컴퓨터의 원격 관리 하는 동안 클라이언트는 도메인 컨트롤러, 시스템 센터 구성 서버 및 HRA(상태 등록 기관) 서버 같은 관리 서버와의 통신을 시작합니다. 이러한 서버는 Windows와 바이러스 백신 업데이트 및 NAP(네트워크 액세스 보호) 클라이언트 준수를 포함하는 서비스를 제공합니다. 원격 액세스 배포를 시작하기 전에 필요한 서버를 배포해야 합니다.  
  
-   Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 SP2를 실행 하는 DNS 서버가 필요 합니다.  
  
## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오의 소프트웨어 요구 사항은 다음과 같습니다.  
  
### <a name="server-requirements"></a>서버 요구 사항  
  
-   원격 액세스 서버가 도메인 구성원이어야 합니다. 서버는 내부 네트워크의 경계면 또는 다른 장치의 경계면 방화벽 뒤에 배포될 수 있습니다.  
  
-   원격 액세스 서버가 경계면 방화벽이나 NAT 장치 뒤에 있는 경우, 이 장치는 원격 액세스 서버와 트래픽을 주고받을 수 있도록 구성되어 있어야 합니다.  
  
-   원격 액세스 서버를 배포하는 관리자에게는 서버에 대한 로컬 관리자 권한과 도메인 사용자 권한이 필요합니다. 또한 관리자에게는 DirectAccess 배포에 사용되는 GPO에 대한 사용 권한이 필요합니다. 모바일 컴퓨터로만 DirectAccess 배포를 제한하는 기능을 활용하려면 도메인 컨트롤러에서 WMI 필터를 만들 수 있는 Domain Admins 권한이 필요합니다.  
  
-   네트워크 위치 서버가 원격 액세스 서버에 없는 경우에는 실행할 별도의 서버가 필요합니다.  
  
### <a name="remote-access-client-requirements"></a>원격 액세스 클라이언트 요구 사항  
  
-   DirectAccess 클라이언트가 도메인 구성원이어야 합니다. 클라이언트가 포함된 도메인은 원격 액세스 서버와 동일한 포리스트에 속하거나, 원격 액세스 서버 포리스트 또는 도메인과 양방향 트러스트 관계를 유지할 수 있습니다.  
  
-   Active Directory 보안 그룹은 DirectAccess 클라이언트로 구성될 컴퓨터를 포함하는 데 필요합니다. 컴퓨터가 DirectAccess 클라이언트를 포함하는 둘 이상의 보안 그룹에 포함되어 있으면 안 됩니다. 클라이언트가 여러 그룹에 포함되어 있으면 클라이언트에 대한 이름 확인 요청이 올바르게 작동되지 않습니다.  
  

