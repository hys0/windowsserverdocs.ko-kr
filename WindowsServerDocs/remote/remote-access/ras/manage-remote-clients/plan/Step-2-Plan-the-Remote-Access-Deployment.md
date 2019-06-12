---
title: 2 단계 원격 액세스 배포 계획
description: 이 항목은 가이드 Windows Server 2016에서 원격으로 관리 DirectAccess 클라이언트의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc9f02b9-8ddd-4cae-b397-a832996144dd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7aec08a19759c98150cf7518643f634947c5133d
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66805002"
---
# <a name="step-2-plan-the-remote-access-deployment"></a>2 단계 원격 액세스 배포 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016

DirectAccess 클라이언트의 원격 관리를 위해 단일 원격 액세스 서버를 설정 하는 데는 인프라에 대 한 계획, 원격 액세스 설치 마법사를 사용 하는 설정을 계획 준비가 되었습니다.  
  
> [!NOTE]  
> 이러한 작업을 계속 하기 전에 참조 [1 단계: 원격 액세스 인프라 계획](Step-1-Plan-the-Remote-Access-Infrastructure.md)합니다.  
  
|태스크|설명|  
|----|--------|  
|[클라이언트 배포 전략 계획](#plan-a-client-deployment-strategy)|DirectAccess 클라이언트로 구성될 관리 컴퓨터를 정합니다.|  
|[원격 액세스 서버 배포 전략 계획](#plan-a-remote-access-server-deployment-strategy)|원격 액세스 서버를 배포할 방법을 계획합니다.|  
|[인프라 서버 구성을 계획 합니다.](#plan-the-infrastructure-servers-configurations)|DirectAccess 네트워크 위치 서버, DNS 서버 및 DirectAccess 관리 서버를 포함 하 여 원격 액세스 배포에서 인프라 서버를 계획 합니다.|  
  
## <a name="plan-a-client-deployment-strategy"></a>클라이언트 배포 전략 계획  
클라이언트 배포를 계획할 때 결정해야 하는 세 가지 사항이 있습니다.  
  
1.  DirectAccess만을 사용할 수 모바일 컴퓨터에, 또는 지정 된 보안 그룹의 모든 컴퓨터에 있습니까?  
  
    DirectAccess 클라이언트 설치 마법사에서 DirectAccess 클라이언트를 구성한 경우 이동 컴퓨터 에서만 DirectAccess를 사용 하 여 서버에 연결할 지정 된 보안 그룹에서 허용 하도록 선택할 수 있습니다. 액세스를 이동 컴퓨터로 제한하면 원격 액세스에서 DirectAccess 클라이언트 GPO가 지정된 보안 그룹의 이동 컴퓨터에만 적용되도록 WMI 필터를 자동으로 구성합니다. 이 설정을 사용하려면 원격 액세스 관리자에게 그룹 정책 WMI 필터를 만들거나 수정할 수 있는 권한이 있어야 합니다.  
  
2.  DirectAccess 클라이언트 컴퓨터가 어떤 보안 그룹에 포함되나요?  
  
    DirectAccess 설정은 DirectAccess 클라이언트 그룹 정책 개체 (GPO)에 포함 됩니다. 이 GPO는 DirectAccess 클라이언트 설치 마법사에서 지정한 보안 그룹에 속한 컴퓨터에 적용됩니다. 모든 지원 되는 도메인에 포함 된 보안 그룹을 지정할 수 있습니다.
  
    원격 액세스를 구성 하기 전에 보안 그룹을 만드는 해야 합니다. 원격 액세스 배포를 완료 한 후 보안 그룹에 컴퓨터를 추가할 수 있습니다. 그러나 보안 그룹과 다른 도메인에 상주 하는 클라이언트 컴퓨터를 추가 하는 경우 클라이언트 GPO는 여러 클라이언트에 적용 되지 않습니다. 예를 들어, DirectAccess 클라이언트에 대 한 SG1 도메인 A에서 만든 경우 나중에 추가한 클라이언트 도메인 B에서이 그룹에 클라이언트 GPO는 적용할 수 없습니다 2. 도메인에 있는 클라이언트  
  
    이 문제를 방지 하려면 클라이언트 컴퓨터가 포함 된 각 도메인에 대 한 새 클라이언트 보안 그룹을 만듭니다. 새 보안 그룹을 만들 하지 않을 경우 또는 실행 합니다 **Add-daclient** 새 도메인에 대 한 새 GPO의 이름 사용 하 여 Windows PowerShell cmdlet.  
  
3.  DirectAccess 네트워크 연결 길잡이 대 한 구성 설정을 있습니다?  
  
    DirectAccess 네트워크 연결 길잡이 클라이언트 컴퓨터에서 실행 되 고 최종 사용자에 게 DirectAccess 연결에 대 한 추가 정보를 제공 합니다. DirectAccess 클라이언트 설치 마법사에서 다음을 구성할 수 있습니다.  
  
    -   **연결 검증 도구**  
  
        클라이언트에서 내부 네트워크 연결의 유효성을 검사하는 데 사용하는 기본 웹 검색이 만들어집니다. 기본 이름은 `https://directaccess-WebProbeHost.<domain_name>`입니다. DNS에 이름을 수동으로 등록해야 합니다. HTTP 또는 PING을 통해 다른 웹 주소를 사용 하는 다른 연결 검증 도구를 만들 수 있습니다. 각 연결 검증 도구에 대한 DNS 항목이 있어야 합니다.  
  
    -   **기술 지원팀 전자 메일 주소 도움말**  
  
        최종 사용자에 게 DirectAccess 연결 문제가 발생 하는 경우 문제를 해결할 수 있는 원격 액세스 관리자에 게 진단 정보가 포함 된 메일을 보낼 수 있습니다.  
  
    -   **DirectAccess 연결 이름**  
  
        최종 사용자가 자신의 컴퓨터에서 DirectAccess 연결을 식별 하는 데 DirectAccess 연결 이름을 지정할 수 있습니다.  
  
    -   **DirectAccess 클라이언트가 로컬 이름 확인을 사용 하도록 허용**  
  
        클라이언트는 이름을 로컬로 확인할 주의 해야 합니다. DirectAccess 클라이언트에서 로컬 이름 확인을 사용하도록 허용하면 최종 사용자가 로컬 DNS 서버를 사용하여 이름을 확인할 수 있습니다. 최종 사용자를 이름 확인을 위해 로컬 DNS 서버를 사용 하도록 선택 하는 경우 DirectAccess 단일 레이블 이름에 대 한 확인 요청을 내부 회사 DNS 서버에 보내지 않습니다. 로컬 이름 확인 대신 사용 (링크-로컬 멀티 캐스트 이름 확인 LLMNR () 및 NetBios over TCP/IP 프로토콜 사용)가 있습니다.  
  
## <a name="plan-a-remote-access-server-deployment-strategy"></a>원격 액세스 서버 배포 전략 계획  
원격 액세스 서버를 배포할 계획인 경우을 해야 하는 결정은 다음과 같습니다.  
  
-   **네트워크 토폴로지**  
  
    두 가지 토폴로지가 있습니다 사용할 수 있는 원격 액세스 서버를 배포 하는 경우:  
  
    -   **두 어댑터**: 두 개의 네트워크 어댑터를 사용 하 여 인터넷에 직접 연결 된 하나의 네트워크 어댑터를 사용 하 여 원격 액세스를 구성할 수 있습니다 하 고 내부 네트워크에 연결 합니다. 또는 방화벽이 나 라우터와 같은 지 장치를 뒤에 서버가 설치 되는 또는 합니다. 이 구성 하나의 네트워크 어댑터를 경계 네트워크에 연결 됩니다 하 고 내부 네트워크에 연결 됩니다 다른 키를 누릅니다.  
  
    -   **단일 네트워크 어댑터**: 이 구성 된 원격 액세스 서버는 방화벽이 나 라우터와 같은 지 장치를 뒤에 설치 됩니다. 네트워크 어댑터는 내부 네트워크에 연결됩니다.  

-   **네트워크 어댑터**  
  
    원격 액세스 서버 설치 마법사는 자동으로 원격 액세스 서버에 구성 된 네트워크 어댑터를 검색 합니다. 올바른 어댑터를 선택해야 합니다.  
  
-   **IP-HTTPS 인증서**  
  
    원격 액세스 서버 설치 마법사가 IP-HTTPS 연결에 적합한 인증서를 자동으로 검색합니다. 선택한 인증서의 주체 이름이 ConnectTo 주소와 일치해야 합니다. 자체 서명 된 인증서를 사용 하는 경우에 원격 액세스 서버에 의해 자동으로 만들어지는 인증서를 사용 하도록 선택할 수 있습니다.  
  
-   **IPv6 접두사**  
  
    원격 액세스 서버 설치 마법사가 네트워크 어댑터에 배포된 IPv6을 검색하며, 내부 네트워크의 IPv6 접두사, DirectAccess 클라이언트 컴퓨터에 할당할 IPv6 접두사 및 VPN 클라이언트 컴퓨터에 할당할 IPv6 접두사를 자동으로 채웁니다. 자동으로 생성된 접두사가 기본 IPv6 또는 ISATAP 인프라에 올바르지 않은 경우 수동으로 변경해야 합니다.  
  
-   **인증**  
  
    원격 액세스 서버에 DirectAccess 클라이언트를 인증 하기 위해 다음 방법 중 하나를 선택할 수 있습니다.  
  
    -   **사용자 인증**: 사용자가 Active Directory 자격 증명 또는 2단계 인증을 통해 인증을 받도록 설정할 수 있습니다.  
  
    -   **컴퓨터 인증**: 컴퓨터 인증 인증서를 사용 하도록 구성할 수 있습니다. 또는 원격 액세스 서버 인증서를 요구 하지 않고 Kerberos 인증에 대 한 프록시로 작동할 수 있습니다. 
  
    -   **Windows 7 클라이언트** 기본적으로 Windows 7을 실행 하는 클라이언트 컴퓨터는 Windows Server 2012를 실행 하는 원격 액세스 배포에 연결할 수 없습니다. 내부 리소스에 대 한 원격 액세스를 필요로 하는 조직에서 Windows 7을 실행 하는 클라이언트를 사용 하는 경우 연결 하도록 허용할 수 있습니다. 내부 리소스에 대한 액세스를 허용할 클라이언트 컴퓨터는 DirectAccess 클라이언트 설치 마법사에서 지정한 보안 그룹의 구성원이어야 합니다.  
  
        > [!NOTE]  
        > DirectAccess를 사용 하 여 연결 하려면 Windows 7을 실행 하는 클라이언트를 허용 하려면 컴퓨터 인증서 인증을 사용 해야 합니다.  
  
-   **VPN 구성**  
  
    원격 액세스를 구성 하기 전에 원격 클라이언트에 대 한 VPN 액세스를 제공 하려는 경우를 결정 합니다. DirectAccess 연결을 지원 하지 않는 조직의 클라이언트 컴퓨터가 있는 경우 VPN 액세스를 제공 해야 합니다 (예를 들어 관리 되지 또는 DirectAccess 지원 되지 않습니다 운영 체제를 실행). 원격 액세스 서버 설치 마법사를 사용 하면 (DHCP를 사용 하 여 또는 고정 주소 풀에서) IP 주소를 할당 하는 방법 및 (사용 하 여 Active Directory 또는 RADIUS 서버) VPN 클라이언트 인증 방법을 구성할 수 있습니다.  
  
## <a name="plan-the-infrastructure-servers-configurations"></a>인프라 서버 구성을 계획 합니다.  
원격 액세스에는 세 가지 유형의 인프라 서버가 필요합니다.  
  
-   **네트워크 위치 서버**  
  
-   **DNS 서버** 
  
-   **관리 서버** 
  
## <a name="see-also"></a>참조  
  
-   [1단계: 원격 액세스 인프라 계획](Step-1-Plan-the-Remote-Access-Infrastructure.md)  
  


