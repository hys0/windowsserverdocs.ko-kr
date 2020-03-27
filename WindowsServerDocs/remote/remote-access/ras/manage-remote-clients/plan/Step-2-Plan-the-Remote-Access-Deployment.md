---
title: 2 단계 원격 액세스 배포 계획
description: 이 항목은 Windows Server 2016에서 원격으로 DirectAccess 클라이언트 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc9f02b9-8ddd-4cae-b397-a832996144dd
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 39b6d0b924d4939361cb66109d049a6924e9be3e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314232"
---
# <a name="step-2-plan-the-remote-access-deployment"></a>2 단계 원격 액세스 배포 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

DirectAccess 클라이언트의 원격 관리를 위해 단일 원격 액세스 서버를 설정 하는 데 사용 하려는 인프라를 계획 한 후에는 원격 액세스 설치 마법사에서 사용할 설정을 계획할 준비가 됩니다.  
  
> [!NOTE]  
> 이러한 작업을 계속 하기 전에 [1 단계: 원격 액세스 인프라 계획](Step-1-Plan-the-Remote-Access-Infrastructure.md)을 참조 하세요.  
  
|작업|설명|  
|----|--------|  
|[클라이언트 배포 전략 계획](#plan-a-client-deployment-strategy)|DirectAccess 클라이언트로 구성될 관리 컴퓨터를 정합니다.|  
|[원격 액세스 서버 배포 전략 계획](#plan-a-remote-access-server-deployment-strategy)|원격 액세스 서버를 배포할 방법을 계획합니다.|  
|[인프라 서버의 구성 계획](#plan-the-infrastructure-servers-configurations)|DirectAccess 네트워크 위치 서버, DNS 서버 및 DirectAccess 관리 서버를 포함 하 여 원격 액세스 배포에서 인프라 서버를 계획 합니다.|  
  
## <a name="plan-a-client-deployment-strategy"></a>클라이언트 배포 전략 계획  
클라이언트 배포를 계획할 때 결정해야 하는 세 가지 사항이 있습니다.  
  
1.  DirectAccess는 모바일 컴퓨터에만 사용할 수 있나요? 아니면 지정 된 보안 그룹의 모든 컴퓨터에만 사용할 수 있나요?  
  
    Directaccess 클라이언트 설치 마법사에서 DirectAccess 클라이언트를 구성할 때 지정 된 보안 그룹의 모바일 컴퓨터만 DirectAccess를 사용 하 여 서버에 연결할 수 있도록 허용 하도록 선택할 수 있습니다. 액세스를 이동 컴퓨터로 제한하면 원격 액세스에서 DirectAccess 클라이언트 GPO가 지정된 보안 그룹의 이동 컴퓨터에만 적용되도록 WMI 필터를 자동으로 구성합니다. 이 설정을 사용하려면 원격 액세스 관리자에게 그룹 정책 WMI 필터를 만들거나 수정할 수 있는 권한이 있어야 합니다.  
  
2.  DirectAccess 클라이언트 컴퓨터가 어떤 보안 그룹에 포함되나요?  
  
    Directaccess 설정은 DirectAccess 클라이언트 GPO (그룹 정책 개체)에 포함 되어 있습니다. 이 GPO는 DirectAccess 클라이언트 설치 마법사에서 지정한 보안 그룹에 속한 컴퓨터에 적용됩니다. 지원 되는 모든 도메인에 포함 된 보안 그룹을 지정할 수 있습니다.
  
    원격 액세스를 구성 하기 전에 보안 그룹을 만들어야 합니다. 원격 액세스 배포를 완료 한 후 보안 그룹에 컴퓨터를 추가할 수 있습니다. 그러나 보안 그룹과 다른 도메인에 상주 하는 클라이언트 컴퓨터를 추가 하는 경우 해당 클라이언트에는 클라이언트 GPO가 적용 되지 않습니다. 예를 들어 도메인 A에 DirectAccess 클라이언트에 대 한 SG1을 만든 후 나중에 도메인 B의 클라이언트를이 그룹에 추가 하면 클라이언트 GPO가 도메인 B의 클라이언트에 적용 되지 않습니다.  
  
    이 문제를 방지 하려면 클라이언트 컴퓨터를 포함 하는 각 도메인에 대 한 새 클라이언트 보안 그룹을 만듭니다. 또는 새 보안 그룹을 만들지 않으려면 새 도메인의 새 GPO 이름으로 **Add-daclient** Windows PowerShell cmdlet을 실행 합니다.  
  
3.  DirectAccess 네트워크 연결 길잡이에 대해 구성 하는 설정은 무엇 인가요?  
  
    DirectAccess 네트워크 연결 길잡이는 클라이언트 컴퓨터에서 실행 되며 최종 사용자에 대 한 DirectAccess 연결에 대 한 추가 정보를 제공 합니다. DirectAccess 클라이언트 설치 마법사에서 다음을 구성할 수 있습니다.  
  
    -   **연결 검증 도구**  
  
        클라이언트에서 내부 네트워크 연결의 유효성을 검사하는 데 사용하는 기본 웹 검색이 만들어집니다. 기본 이름은 `https://directaccess-WebProbeHost.<domain_name>`입니다. DNS에 이름을 수동으로 등록해야 합니다. HTTP 또는 PING을 통해 다른 웹 주소를 사용 하는 다른 연결 검증 도구를 만들 수 있습니다. 각 연결 검증 도구에 대한 DNS 항목이 있어야 합니다.  
  
    -   **지원 센터 전자 메일 주소**  
  
        최종 사용자가 DirectAccess 연결 문제를 경험 하는 경우 원격 액세스 관리자에 게 문제를 해결할 수 있는 진단 정보가 포함 된 전자 메일을 보낼 수 있습니다.  
  
    -   **DirectAccess 연결 이름**  
  
        최종 사용자가 컴퓨터에서 DirectAccess 연결을 식별 하는 데 도움이 되는 DirectAccess 연결 이름을 지정할 수 있습니다.  
  
    -   **DirectAccess 클라이언트에서 로컬 이름 확인을 사용 하도록 허용**  
  
        클라이언트는 로컬에서 이름을 확인 하는 수단을 필요로 합니다. DirectAccess 클라이언트에서 로컬 이름 확인을 사용하도록 허용하면 최종 사용자가 로컬 DNS 서버를 사용하여 이름을 확인할 수 있습니다. 최종 사용자가 이름 확인을 위해 로컬 DNS 서버를 사용 하도록 선택 하는 경우 DirectAccess는 단일 레이블 이름에 대 한 확인 요청을 내부 회사 DNS 서버에 보내지 않습니다. 대신 로컬 이름 확인을 사용 합니다. 대신 LLMNR (링크-로컬 멀티 캐스트 이름 확인) 및 NetBios over TCP/IP 프로토콜을 사용 합니다.  
  
## <a name="plan-a-remote-access-server-deployment-strategy"></a>원격 액세스 서버 배포 전략 계획  
원격 액세스 서버 배포를 계획할 때 결정 해야 하는 사항은 다음과 같습니다.  
  
-   **네트워크 토폴로지**  
  
    원격 액세스 서버를 배포할 때는 다음 두 가지 토폴로지를 사용할 수 있습니다.  
  
    -   **두 어댑터**: 네트워크 어댑터 두 개를 사용 하면 인터넷에 직접 연결 된 네트워크 어댑터와 내부 네트워크에 연결 된 네트워크 어댑터를 사용 하 여 원격 액세스를 구성할 수 있습니다. 또는 방화벽이 나 라우터와 같은에 지 장치 뒤에 서버가 설치 됩니다. 이 구성에서는 네트워크 어댑터가 경계 네트워크에 연결 되 고 다른 하나는 내부 네트워크에 연결 됩니다.  
  
    -   **단일 네트워크 어댑터**:이 구성에서는 방화벽이 나 라우터와 같은에 지 장치 뒤에 원격 액세스 서버를 설치 합니다. 네트워크 어댑터는 내부 네트워크에 연결됩니다.  

-   **네트워크 어댑터**  
  
    원격 액세스 서버 설치 마법사는 원격 액세스 서버에 구성 된 네트워크 어댑터를 자동으로 검색 합니다. 올바른 어댑터를 선택해야 합니다.  
  
-   **IP-HTTPS 인증서**  
  
    원격 액세스 서버 설치 마법사가 IP-HTTPS 연결에 적합한 인증서를 자동으로 검색합니다. 선택한 인증서의 주체 이름이 ConnectTo 주소와 일치해야 합니다. 자체 서명 된 인증서를 사용 하는 경우 원격 액세스 서버에서 자동으로 만든 인증서를 사용 하도록 선택할 수 있습니다.  
  
-   **IPv6 접두사**  
  
    원격 액세스 서버 설치 마법사가 네트워크 어댑터에 배포된 IPv6을 검색하며, 내부 네트워크의 IPv6 접두사, DirectAccess 클라이언트 컴퓨터에 할당할 IPv6 접두사 및 VPN 클라이언트 컴퓨터에 할당할 IPv6 접두사를 자동으로 채웁니다. 자동으로 생성된 접두사가 기본 IPv6 또는 ISATAP 인프라에 올바르지 않은 경우 수동으로 변경해야 합니다.  
  
-   **인증**  
  
    다음 방법 중 하나를 선택 하 여 원격 액세스 서버에 대 한 DirectAccess 클라이언트를 인증할 수 있습니다.  
  
    -   **사용자 인증**: 사용자가 Active Directory 자격 증명으로 인증 하거나 2 단계 인증을 사용 하도록 설정할 수 있습니다.  
  
    -   **컴퓨터 인증**: 인증서를 사용 하도록 컴퓨터 인증을 구성할 수 있습니다. 또는 원격 액세스 서버는 인증서를 요구 하지 않고 Kerberos 인증에 대 한 프록시 역할을 할 수 있습니다. 
  
    -   **Windows 7 클라이언트** 기본적으로 Windows 7을 실행 하는 클라이언트 컴퓨터는 Windows Server 2012를 실행 하는 원격 액세스 배포에 연결할 수 없습니다. 조직에서 내부 리소스에 원격으로 액세스 해야 하는 Windows 7을 실행 하는 클라이언트가 있는 경우 연결 하도록 허용할 수 있습니다. 내부 리소스에 대한 액세스를 허용할 클라이언트 컴퓨터는 DirectAccess 클라이언트 설치 마법사에서 지정한 보안 그룹의 구성원이어야 합니다.  
  
        > [!NOTE]  
        > Windows 7을 실행 하는 클라이언트가 DirectAccess를 사용 하 여 연결 하도록 허용 하려면 컴퓨터 인증서 인증을 사용 해야 합니다.  
  
-   **VPN 구성**  
  
    원격 액세스를 구성 하기 전에 원격 클라이언트에 대 한 VPN 액세스를 제공할지 여부를 결정 합니다. DirectAccess 연결을 지원 하지 않는 조직의 클라이언트 컴퓨터가 있는 경우 (예: 관리 되지 않거나 DirectAccess가 지원 되지 않는 운영 체제를 실행 하는 경우) VPN 액세스를 제공 해야 합니다. 원격 액세스 서버 설치 마법사를 사용 하 여 IP 주소를 할당 하는 방법 (DHCP 또는 고정 주소 풀을 사용 하 여) 및 VPN 클라이언트를 인증 하는 방법 (Active Directory 또는 RADIUS 서버 사용)을 구성할 수 있습니다.  
  
## <a name="plan-the-infrastructure-servers-configurations"></a>인프라 서버의 구성 계획  
원격 액세스에는 세 가지 유형의 인프라 서버가 필요 합니다.  
  
-   **네트워크 위치 서버**  
  
-   **DNS 서버** 
  
-   **관리 서버** 
  
## <a name="see-also"></a>참고 항목  
  
-   [1 단계: 원격 액세스 인프라 계획](Step-1-Plan-the-Remote-Access-Infrastructure.md)  
  


