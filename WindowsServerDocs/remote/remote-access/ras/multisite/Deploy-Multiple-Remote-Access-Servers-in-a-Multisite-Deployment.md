---
title: 멀티 사이트 배포에서 여러 원격 액세스 서버 배포
description: 이 항목은 Windows Server 2016에서 멀티 사이트 배포에서 여러 원격 액세스 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac2f6015-50a5-4909-8f67-8565f9d332a2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4b9da54822c1b7610bbd7a095beeb305eb243bb1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314031"
---
# <a name="deploy-multiple-remote-access-servers-in-a-multisite-deployment"></a>멀티 사이트 배포에서 여러 원격 액세스 서버 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

 Windows Server 2016 및 Windows Server 2012 DirectAccess 및 원격 액세스 서비스 (RAS) VPN 단일 원격 액세스 역할로 결합 합니다. 원격 액세스는 다양한 엔터프라이즈 시나리오를 통해 배포될 수 있습니다. 이 개요에서는 멀티 사이트 구성에 원격 액세스 서버를 배포 하기 위한 엔터프라이즈 시나리오를 소개 합니다.  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>시나리오 설명  
멀티 사이트 배포에 두 개 이상의 원격 액세스 서버 또는 서버 클러스터 배포 되 고 다른 진입점을 한 위치에 나 지리적으로 분산 된 위치의 구성 합니다. 배포는 단일 위치에서 여러 진입점 서버 중복성을 위해 또는 기존 네트워크 아키텍처 원격 액세스 서버를 정렬할 수 있습니다. 원격 클라이언트 컴퓨터에 가장 가까운 수 있는 진입점을 사용 하 여 내부 네트워크 리소스에 연결할 수 리소스를 효율적으로 사용이 되도록 하는 지리적 위치에 따라 배포 합니다. 멀티 사이트 배포에서의 트래픽은 외부 전역 부하 분산 장치와 균등 하 게 분산 될 수 있습니다.  
  
멀티 사이트 배포는 Windows 10, Windows 8 또는 Windows 7을 실행 하는 클라이언트 컴퓨터를 지원 합니다. 사용자는 진입점을 수동으로 선택할 수 또는 자동으로 Windows 10 또는 Windows 8을 실행 하는 클라이언트 컴퓨터는 진입점을 식별 합니다. 자동 할당 다음 우선 순위 순서 대로 발생합니다.  
  
1.  사용자가 수동으로 선택할 수 있는 진입점을 사용 합니다.  
  
2.  배포 하는 경우에 외부 전역 부하 분산 장치에 의해 식별 되는 진입점을 사용 합니다.  
  
3.  자동 검색 메커니즘을 사용 하 여 클라이언트 컴퓨터에 의해 식별 된 가장 가까운 진입점을 사용 합니다.  
  
Windows 7을 실행 하는 클라이언트에 대 한 지원 각 진입점에 수동으로 활성화 해야 하 고 있는 진입점을 사용 하 여 이러한 클라이언트에 의해 선택이 지원 되지 않습니다.  
  
## <a name="prerequisites"></a>필수 조건  
이 시나리오의 배포를 시작하기 전에 다음 목록에서 중요한 요구 사항을 검토하세요.  
  
-   [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) 멀티 사이트 배포 하기 전에 배포 해야 합니다.  
  
-   Windows 7 클라이언트는 항상 특정 사이트에 연결 됩니다. 이러한 됩니다 (Windows 10, 8 또는 8.1 클라이언트)와 달리 클라이언트의 위치를 기준으로 가장 가까운 사이트에 연결할 수 있습니다.  
  
-   DirectAccess 관리 콘솔 또는 PowerShell cmdlet 외부에서 정책을 변경하는 것이 지원되지 않습니다.  
  
-   공개 키 인프라를 배포해야 합니다.  
  
    자세한 내용은 다음을 참조하십시오. [테스트 랩 가이드 미니 모듈: Windows Server 2012에 대한 기본 PKI](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   회사 네트워크에 IPv6 사용 가능 해야 합니다. ISATAP를 사용 중인 경우 이를 제거하고 기본 IPv6을 사용해야 합니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
멀티 사이트 배포 시나리오는 여러를 단계가 포함 되어 있습니다.  
  
1. [고급 설정으로 단일 DirectAccess 서버 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다. 멀티 사이트 배포를 설정 하기 전에 고급 설정으로 단일 원격 액세스 서버를 배포 해야 합니다.  
  
2. [멀티 사이트 배포를 계획](plan/Plan-a-Multisite-Deployment.md)합니다. 단일 서버에서 멀티 사이트 배포 다양 한 추가 계획을 작성 하 단계는 Active Directory 보안 그룹, 그룹 정책 개체 (Gpo), DNS 및 클라이언트 설정에 대 한 계획 및 멀티 사이트 필수 구성 요소를 준수를 포함 하 여 필요 합니다.  
  
3. [멀티 사이트 배포를 구성](configure/Configure-a-Multisite-Deployment.md)합니다. 다양 한 구성 단계를 준비 하는 Active Directory 인프라, 멀티 사이트 배포로 진입점으로 여러 원격 액세스 서버 추가 등의 기존 원격 액세스 서버의 구성을 포함 하 여 구성 됩니다.  
  
4. [멀티 사이트 배포의 문제를 해결](troubleshoot/Troubleshoot-a-Multisite-Deployment.md)합니다. 이 문제 해결 섹션에서는 여러 원격 액세스 멀티 사이트 배포에서를 배포할 때 발생할 수 있는 가장 일반적인 오류를 설명 합니다.
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>실용적인 응용 프로그램  
멀티 사이트 배포는 다음을 제공합니다.  
  
-   향상 된 성능 A 멀티 사이트 배포 하 고 가장 적합 한 가장 가까운 진입점을 사용 하 여 연결 하려면 원격 액세스를 사용 하 여 내부 리소스에 액세스 하는 컴퓨터 클라이언트를 수 있습니다. 클라이언트에서 내부 리소스를 효율적으로 액세스 하 고 DirectAccess를 통해 라우트된 인터넷 요청 클라이언트의 속도 향상 됩니다. 진입점에서 트래픽은 외부 전역 부하 분산 장치를 사용 분산할 수 있습니다.  
  
-   용이성의 관리 멀티 관리자가 원격 액세스 배포 간소화 된 아키텍처를 제공 하는 Active Directory 사이트 배포를 맞출 수 있습니다. 공유 설정은 항목 지점 서버 또는 클러스터에서 쉽게 설정할 수 있습니다. 원격 액세스 설정에는 배포 또는 원격 서버 관리 도구 (RSAT)를 사용 하 여 원격 서버에서 관리할 수 있습니다. 또한 단일 원격 액세스 관리 콘솔에서 전체 멀티 사이트 배포를 모니터링할 수 있습니다.  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>이 시나리오에 포함 된 역할 및 기능  
다음 표에서 역할과이 시나리오에서 사용 되는 기능을 나열 합니다.  
  
|역할/기능|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|원격 액세스 역할|이 역할은 서버 관리자 콘솔을 사용하여 설치 및 제거됩니다. 이 역할에는 DirectAccess(이전의 Windows Server 2008 R2 기능)와 라우팅 및 원격 액세스 서비스(이전의 NPAS(네트워크 정책 및 액세스 서비스) 서버 역할의 역할 서비스)가 모두 포함되어 있습니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br /><br />-DirectAccess 및 라우팅 및 원격 액세스 서비스 (RRAS) VPN-DirectAccess 및 VPN 원격 액세스 관리 콘솔에서 함께 관리 됩니다.<br />RRAS 라우팅 RRAS 라우팅 기능은 레거시 라우팅 및 원격 액세스 콘솔에서 관리 됩니다.<br /><br />종속성은 다음과 같습니다.<br /><br />인터넷 정보 서비스 (IIS) 웹 서버-이 기능은 네트워크 위치 서버와 기본 웹 프로브를 구성 해야 합니다.<br />Windows 로컬 계정에 원격 액세스 서버에 대 한 내부 Database-Used 합니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치됩니다.<br /><br />-이 값은 원격 액세스 역할이 설치 되어 있고 원격 관리 콘솔 사용자 인터페이스를 지 원하는 때 기본적으로 원격 액세스 서버에 설치 됩니다.<br />-앱는 하지 원격 액세스 서버 역할을 실행 하는 서버에 필요에 따라 설치 수 있습니다. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<br /><br />원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<br /><br />-원격 액세스 GUI 및 명령줄 도구<br />-Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />그룹 정책 관리 콘솔<br />RAS 연결 관리자 관리 키트 (CMAK)<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  
  
-   멀티 사이트 배포에 수집 하 원격 액세스 컴퓨터 두 개 이상 있습니다.   
  
-   시나리오를 테스트 하려면 하나 이상의 Windows 8을 실행 하 고 DirectAccess 클라이언트로 구성 된 컴퓨터가 필요 합니다. Windows 7을 실행 하는 클라이언트에 대 한 시나리오를 테스트 하려면 적어도 하나의 컴퓨터에서 Windows 7을 실행 해야 합니다.  
  
-   항목 지점 서버에 걸쳐 부하 분산 트래픽에, 타사 외부 전역 부하 분산 장치는 필요 합니다.  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오의 소프트웨어 요구 사항은 다음과 같습니다.  
  
-   단일 서버 배포에 필요한 소프트웨어 요구 사항.  
  
-   단일 서버에 대 한 소프트웨어 요구 사항 외에 다양 한 multisite-특정 요구 사항  
  
    -   IPsec 인증 요구 사항-에 IPsec 컴퓨터 인증서 인증을 사용 하 여 DirectAccess 멀티 사이트 배포를 배포 해야 합니다. 원격 액세스 서버를 Kerberos 프록시로 사용 하 여 IPsec 인증을 수행 하는 옵션을 사용할 수 없습니다. 내부 CA는 IPsec 인증서를 배포 해야 합니다.  
  
    -   IP-HTTPS 및 네트워크 위치 서버 요구 사항-인증서 IP-HTTPS와 네트워크 위치 서버에 필요한 CA에서 발급 되어야 합니다. 자동으로 발급 되 고 원격 액세스 서버에서 자체 서명 인증서를 사용 하는 옵션이 지원 되지 않습니다. 내부 CA에서 또는 타사 외부 CA에서 인증서를 발급할 수 있습니다.  
  
    -   Active Directory 요구 사항-하나 이상의 Active Directory 사이트가 필요 합니다. 원격 액세스 서버 사이트에 있어야 합니다. 업데이트 시간을 단축 것이 좋습니다 각 사이트에는 쓰기 가능한 도메인 컨트롤러는 경우에이 옵션은 필수입니다.  
  
    -   보안 그룹 요구 사항-요구 사항은 다음과 같습니다.  
  
        -   단일 보안 그룹은 모든 도메인에서 모든 Windows 8 클라이언트 컴퓨터에 필요 합니다. 각 도메인에 대 한 이러한 클라이언트의 고유 보안 그룹을 만드는 것이 좋습니다.  
  
        -   Windows 7 컴퓨터를 포함 하는 고유한 보안 그룹 각 진입점을 Windows 7 클라이언트를 지원 하도록 구성 되어야 합니다. 각 도메인에서 각 진입점에 대 한 고유한 보안 그룹을 보유 하는 것이 좋습니다.  
  
        -   컴퓨터가 DirectAccess 클라이언트를 포함하는 둘 이상의 보안 그룹에 포함되어 있으면 안 됩니다. 클라이언트가 여러 그룹에 포함되어 있으면 클라이언트에 대한 이름 확인 요청이 올바르게 작동되지 않습니다.  
  
    -   GPO 요구 사항-Gpo 원격 액세스를 구성 하기 전에 수동으로 만든 또는 원격 액세스 배포 하는 동안 자동으로 만들 수 있습니다. 요구 사항은 다음과 같습니다.  
  
        -   고유한 클라이언트 GPO가 각 도메인에 대해 필요 합니다.  
  
        -   서버 GPO는 진입점의 위치를 가리키는 도메인에 있는 각 진입점에 대 한 필요 합니다. 따라서 여러 진입점을 동일한 도메인에 있는 경우 여러 서버 도메인에서 Gpo (각 진입점에 대해 하나씩) 됩니다.  
  
        -   고유한 Windows 7 클라이언트 GPO가 각 도메인에 대 한 Windows 7 클라이언트 지원에 대해 활성화 된 각 진입점에 대 한 필요 합니다.  
  
## <a name="known-issues"></a><a name="KnownIssues"></a>알려진 문제  
다음은 알려진 문제는 멀티 사이트 시나리오를 구성 하는 경우:  
  
-   **동일한 IPv4 서브넷에 여러 진입점**합니다. 동일한 IPv4 서브넷에 여러 진입점을 추가 IP 주소 충돌 메시지 고 DNS64 주소 진입점에 대 한 예상 대로 구성 되지 않습니다. I p v 6은 회사 네트워크에서 서버의 내부 인터페이스에 배포 되지 않은 경우이 문제가 발생 합니다. 이 문제를 방지 모든 현재 및 미래의 원격 액세스 서버에서 다음 Windows PowerShell 명령을 실행 합니다.  
  
    ```  
    Set-NetIPInterface -InterfaceAlias <InternalInterfaceName> -AddressFamily IPv6 -DadTransmits 0  
    ```  
  
-   원격 액세스 서버에 연결 하는 DirectAccess 클라이언트에 대 한 지정 된 공용 주소 접미사를 NRPT에 포함 되어 있으면, DirectAccess 예상 대로 작동 하지 않을 수 있습니다. NRPT에 공개 이름에 대 한 예외가 있는지 확인 합니다. 멀티 사이트 배포에서는 모든 진입점의 공개 이름에 대 한 예외를 추가 되어야 합니다. 있는 경우 강제 터널링 사용 하도록 설정 되어 이러한 예외는 자동으로 추가 됩니다. 강제 터널링을 사용할 수 없는 경우 제거 됩니다.  
  
-   Windows PowerShell cmdlet을 사용 하는 경우 **비활성화 DAMultiSite**, WhatIf 및 Confirm 매개 변수는 아무런 영향이 및 멀티 사이트를 사용할 수 없게 됩니다 및 Windows 7 Gpo 제거 됩니다.  
  
-   Windows 7 클라이언트 DCA 멀티 사이트 배포에서 사용 하 여 Windows 8로 업그레이드 되는 네트워크 연결 길잡이가 작동 하지 않습니다. 다음 Windows PowerShell cmdlet을 사용 하 여 Windows 7 Gpo를 수정 하 여 클라이언트를 업그레이드 하기 전에이 문제를 해결할 수 있습니다.  
  
    ```  
    Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
    Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
    ```  
  
    클라이언트로 이미 업그레이드 하는 경우 클라이언트 컴퓨터의 Windows 8 보안 그룹으로 전환 합니다.  
  
-   Windows PowerShell cmdlet을 사용 하 여 도메인 컨트롤러 설정을 수정 하는 경우 **Set-daentrypointdc**, ComputerName 매개 변수 지정 마지막 아닌 다른 진입점에서 원격 액세스 서버에 추가 됩니다 멀티 사이트 배포에서는 지정 된 서버 정책 새로 고칠 때까지 업데이트 되지 것입니다 나타내는 경고가 표시 됩니다. 업데이트 되지 않은 실제 서버를 사용 하 여 볼 수는 **구성 상태** 에 **대시보드** 의 **원격 액세스 관리 콘솔**합니다. 이 문제가 되지 것입니다 모든 기능을 실행할 수 있습니다 **gpupdate /force** 구성 상태를 즉시 업데이트 하도록 업데이트 되지 않았습니다 하는 서버에서.  
  
-   IPv4 전용 회사 네트워크에서는 내부 변경 멀티 사이트 배포 되는 경우 네트워크 IPv6 접두사도 변경의 DNS64 주소 하지만 d n s 64 서비스에 대 한 DNS 쿼리를 허용 하는 방화벽 규칙에 주소를 업데이트 하지 않습니다. 이 문제를 해결 하려면 내부 네트워크 IPv6 접두사를 변경한 후 다음 Windows PowerShell 명령을 실행 합니다.  
  
    ```  
    $dns64Address = (Get-DAClientDnsConfiguration).NrptEntry | ?{ $_.DirectAccessDnsServers -match ':3333::1' } | Select-Object -First 1 -ExpandProperty DirectAccessDnsServers  
  
    $serverGpoName = (Get-RemoteAccess).ServerGpoName  
  
    $serverGpoDc = (Get-DAEntryPointDC).DomainControllerName  
  
    $gpoSession = Open-NetGPO -PolicyStore $serverGpoName -DomainController $serverGpoDc  
  
    Get-NetFirewallRule -GPOSession $gpoSession | ? {$_.Name -in @('0FDEEC95-1EA6-4042-8BA6-6EF5336DE91A', '24FD98AA-178E-4B01-9220-D0DADA9C8503')} |  Set-NetFirewallRule -LocalAddress $dns64Address  
  
    Save-NetGPO -GPOSession $gpoSession  
    ```  
  
-   기존 ISATAP 인프라가 ISATAP 호스트 된 진입점을 제거 하는 경우에 있는 DirectAccess가 배포 된 경우 DNS64 서비스의 IPv6 주소는 모든 DNS 접미사에 NRPT의 DNS 서버 주소에서 제거 됩니다.  
  
    이 문제를 해결 하려면는 **인프라 서버 설정** 마법사는 **DNS** 페이지 수정 된 DNS 접미사를 제거 하 고 다시 추가 올바른 DNS 서버 주소를 클릭 하 여 **검색** 에 **DNS 서버 주소** 대화 상자입니다.  
  


