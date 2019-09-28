---
title: 기존 원격 액세스(VPN) 배포에 DirectAccess 추가
description: 이 항목은 Windows Server 2016에 대 한 기존 원격 액세스 (VPN) 배포에 DirectAccess 추가 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5db01f7-1ae0-46f2-9be7-8d9e121446b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9266acfb38c65711d6d0b12e2b6223a8a4e91746
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388803"
---
# <a name="add-directaccess-to-an-existing-remote-access-vpn-deployment"></a>기존 원격 액세스(VPN) 배포에 DirectAccess 추가

>적용 대상: Windows Server(반기 채널), Windows Server 2016
  
## <a name="BKMK_OVER"></a>시나리오 설명  
이 시나리오에서는 VPN을 이미 설치 하 고 구성한 후 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 단일 컴퓨터가 권장 설정으로 DirectAccess 서버로 구성 됩니다. 부하 분산 된 클러스터, 멀티 사이트 배포 또는 2 단계 클라이언트 인증과 같은 엔터프라이즈 기능을 사용 하 여 DirectAccess를 구성 하려면이 항목에 설명 된 시나리오를 완료 하 여 단일 서버를 설정한 다음 엔터프라이즈를 설정 합니다. [엔터프라이즈에 원격 액세스 배포](../../ras/Deploy-Remote-Access-in-an-Enterprise.md)에 설명 된 시나리오입니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
단일 원격 액세스 서버를 설치하려면 몇 가지 계획 및 배포 단계가 필요합니다.  
  
### <a name="planning-steps"></a>계획 단계  
계획은 두 개의 단계로 나누어집니다.  
  
1.  **원격 액세스 인프라 계획**  
  
    이 단계에서는 원격 액세스 배포를 시작하기 전에 네트워크 인프라를 설치하는 데 필요한 계획에 대해 설명하며, 여기에는 네트워크 및 서버 토폴로지, 인증서, DNS(Domain Name System), Active Directory, GPO(그룹 정책 개체) 구성 및 DirectAccess 네트워크 위치 서버 계획이 포함됩니다.  
  
2.  **원격 액세스 배포 계획**  
  
    이 단계에서는 원격 액세스 배포를 준비하는 데 필요한 계획 단계에 대해 설명하며, 여기에는 원격 액세스 클라이언트 컴퓨터, 서버 및 클라이언트 인증 요구 사항 및 인프라 서버 계획이 포함됩니다.  
  
### <a name="deployment-steps"></a>배포 단계  
배포는 세 개의 단계로 나누어집니다.  
  
1.  **원격 액세스 인프라 구성**  
  
    이 단계에서는 네트워크 및 라우팅, 방화벽 설정(필요한 경우), 인증서, DNS 서버, Active Directory 및 GPO 설정, DirectAccess 네트워크 위치 서버 등을 구성합니다.  
  
2.  **원격 액세스 서버 설정 구성**  
  
    이 단계에서는 원격 액세스 클라이언트 컴퓨터, 원격 액세스 서버 및 인프라 서버를 구성합니다.  
  
3.  **배포 확인**  
  
    이 단계에서는 필요에 따라 배포가 작동하는지 확인합니다.  
  
## <a name="BKMK_APP"></a>실용적인 응용 프로그램  
단일 원격 액세스 서버를 배포하면 다음과 같은 이점이 있습니다.  
  
-   **간편한 액세스**  
  
    Windows 8 및 Windows 7을 실행 하는 관리 클라이언트 컴퓨터를 DirectAccess 클라이언트 컴퓨터로 구성할 수 있습니다. 이러한 클라이언트는 VPN 연결에 로그인할 필요 없이 인터넷에 있는 동안 언제든지 DirectAccess를 통해 내부 네트워크 리소스에 액세스할 수 있습니다. 이러한 운영 체제 중 하나를 실행하지 않는 클라이언트 컴퓨터는 VPN을 통해 내부 네트워크에 연결할 수 있습니다. DirectAccess와 VPN은 모두 동일한 콘솔에서 동일한 마법사 집합으로 관리됩니다.  
  
-   **손쉬운 관리**  
  
    인터넷에 액세스할 수 있는 DirectAccess 클라이언트 컴퓨터는 회사 내부 네트워크에 없는 경우에도 원격 액세스 관리자가 DirectAccess를 통해 원격으로 관리할 수 있습니다. 회사 요구 사항을 충족하지 않는 클라이언트 컴퓨터를 관리 서버에서 자동으로 업데이트할 수 있습니다.  
  
## <a name="BKMK_NEW"></a>이 시나리오에 필요한 역할 및 기능  
다음 표에는 이 시나리오에 필요한 역할 및 기능이 나와 있습니다.  
  
|역할/기능|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|원격 액세스 역할|이 역할은 서버 관리자 콘솔이나 Windows PowerShell을 사용하여 설치 및 제거됩니다. 이 역할에는 DirectAccess(이전의 Windows Server 2008 R2 기능)와 라우팅 및 원격 액세스 서비스(이전의 NPAS(네트워크 정책 및 액세스 서비스) 서버 역할의 역할 서비스)가 포함되어 있습니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br /><br />1.  DirectAccess와 RRAS(라우팅 및 원격 액세스 서비스) VPN: 원격 액세스 관리 콘솔에서 관리됩니다.<br />2.  RRAS 라우팅: 라우팅 및 원격 액세스 콘솔에서 관리됩니다.<br /><br />원격 액세스 서버 역할은 다음과 같은 서버 기능에 종속됩니다.<br /><br />-인터넷 정보 서비스 (IIS) 웹 서버: 원격 액세스 서버에서 네트워크 위치 서버를 구성 하 고 기본 웹 프로브를 구성 하는 데 필요 합니다.<br />-Windows 내부 데이터베이스: 원격 액세스 서버의 로컬 계정에 사용됩니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치 됩니다.<br /><br />-기본적으로 원격 액세스 역할이 설치 될 때 원격 액세스 서버에 있습니다. 원격 관리 콘솔 사용자 인터페이스 및 Windows PowerShell cmdlet을 지원합니다.<br />-원격 액세스 서버 역할을 실행 하지 않는 서버에 선택적으로 설치 됩니다. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<br /><br />원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<br /><br />-원격 액세스 GUI<br />-Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />그룹 정책 관리 콘솔<br />RAS 연결 관리자 관리 키트 (CMAK)<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
  
## <a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  
  
**서버 요구 사항**  
  
-   Windows Server 2012에 대 한 하드웨어 요구 사항을 충족 하는 컴퓨터입니다.  
  
-   서버에는 네트워크 어댑터가 하나 이상 설치되어 있고, 사용하도록 설정되어 있어야 하며, 서버가 내부 네트워크에 연결되어 있어야 합니다. 두 개의 어댑터가 사용된 경우 하나의 어댑터는 내부 회사 네트워크에 연결되어야 하고 나머지 하나는 외부 네트워크(인터넷)에 연결되어야 합니다.  
  
-   Teredo가 IPv4-IPv6 전환 프로토콜로 필요한 경우 서버의 외부 어댑터에 연속된 두 개의 공용 IPv4 주소가 있어야 합니다. DirectAccess 사용 마법사는 연속된 두 개의 IP 주소가 있는 경우에도 Teredo를 사용하도록 설정하지 않습니다. 단일 IP 주소를 사용할 수 있는 경우 IP-HTTPS만 전환 프로토콜로 사용할 수 있습니다.  
  
-   도메인 컨트롤러가 하나 이상 있어야 합니다. 원격 액세스 서버와 DirectAccess 클라이언트가 도메인 구성원이어야 합니다.  
  
-   DirectAccess 사용 마법사는 IP-HTTPS와 네트워크 위치 서버에 대한 인증서를 요구합니다. SSTP VPN에서 인증서를 이미 사용하는 경우 해당 인증서가 IP-HTTPS에 다시 사용됩니다. SSTP VPN이 구성되지 않은 경우 IP-HTTPS용 인증서를 구성하거나 자동으로 만들어진 자체 서명된 인증서를 사용할 수 있습니다. 네트워크 위치 서버의 경우 인증서를 구성하거나 자동으로 만들어진 자체 서명된 인증서를 사용할 수 있습니다.  
  
**클라이언트 요구 사항**  
  
-   클라이언트 컴퓨터는 Windows 8 또는 Windows 7을 실행 해야 합니다.  
  
    > [!NOTE]  
    > DirectAccess 클라이언트로 사용할 수 있는 운영 체제는 Windows Server 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise 및 Windows 7 Ultimate  
  
**인프라 및 관리 서버 요구 사항**  
  
-   DirectAccess 클라이언트 컴퓨터를 원격으로 관리하는 동안 클라이언트는 도메인 컨트롤러, 시스템 센터 구성 서버, 그리고 Windows와 바이러스 백신 업데이트 및 NAP(네트워크 액세스 보호) 클라이언트 준수 등 서비스의 HRA(상태 등록 기관) 서버 같은 관리 서버와 통신을 시작합니다. 필요한 서버는 원격 액세스 배포를 시작하기 전에 배포되어 있어야 합니다.  
  
-   원격 액세스에서 클라이언트 NAP 규정 준수를 요구하는 경우 원격 액세스 배포를 시작하기 전에 NPS(네트워크 정책 서버) 및 HRS를 배포해야 합니다.  
  
-   Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 s p 2를 실행 하는 DNS 서버가 필요 합니다.  
  
## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오의 소프트웨어 요구 사항은 다음과 같습니다.  
  
**서버 요구 사항**  
  
-   원격 액세스 서버가 도메인 구성원이어야 합니다. 서버는 내부 네트워크의 경계면 또는 다른 장치의 경계면 방화벽 뒤에 배포될 수 있습니다.  
  
-   원격 액세스 서버가 경계면 방화벽이나 NAT(네트워크 주소 변환) 장치 뒤에 있는 경우, 이 장치는 원격 액세스 서버와 트래픽을 주고받을 수 있도록 구성되어 있어야 합니다.  
  
-   서버에 원격 액세스를 배포하는 사람에게는 서버에 대한 로컬 관리자 권한과 도메인 사용자 권한이 필요합니다. 또한 관리자에게는 DirectAccess 배포에 사용되는 GPO 사용 권한이 필요합니다. 이동 컴퓨터에만 DirectAccess를 배포하도록 제한하는 기능을 활용하려면 도메인 컨트롤러에서 WMI 필터를 만들 수 있는 권한이 필요합니다.  
  
**원격 액세스 클라이언트 요구 사항**  
  
-   DirectAccess 클라이언트가 도메인 구성원이어야 합니다. 클라이언트가 포함된 도메인은 원격 액세스 서버와 동일한 포리스트에 속하거나, 원격 액세스 서버 포리스트 또는 도메인과 양방향 트러스트 관계를 유지할 수 있습니다.  
  
-   Active Directory 보안 그룹은 DirectAccess 클라이언트로 구성될 컴퓨터를 포함하는 데 필요합니다. DirectAccess 클라이언트 설정을 구성할 때 보안 그룹이 지정되지 않은 경우 기본적으로 Domain Computers 보안 그룹의 모든 DirectAccess 사용 랩톱 컴퓨터에 클라이언트 GPO가 적용됩니다. DirectAccess 클라이언트로 사용할 수 있는 운영 체제는  Windows Server 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise 및 Windows 7 Ultimate  
  
    > [!NOTE]  
    > DirectAccess 클라이언트로 구성할 컴퓨터가 포함된 각 도메인에 대해 보안 그룹을 만드는 것이 좋습니다.  
  

  

