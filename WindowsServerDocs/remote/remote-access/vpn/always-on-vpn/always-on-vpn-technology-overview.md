---
title: Always On VPN 기술 개요
description: '이 페이지에서는 자세한 문서에 대 한 링크를 사용 하 여 Always On VPN 기술에 대 한 간략 한 개요를 제공 합니다. '
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 31d0d5c12760fc627ce93972f4a70e85f61dd178
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371898"
---
# <a name="always-on-vpn-technology-overview"></a>Always On VPN 기술 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** Always On VPN 개선 사항에 대 한 자세한 정보](always-on-vpn-enhancements.md)
- [**다음:** Always On VPN의 고급 기능에 대 한 자세한 정보](deploy/always-on-vpn-adv-options.md)

이 배포의 경우 Windows Server 2016를 실행 하는 새 원격 액세스 서버를 설치 하 고 배포를 위해 기존 인프라의 일부를 수정 해야 합니다.

다음 그림에서는 Always On VPN을 배포 하는 데 필요한 인프라를 보여 줍니다.

![Always On VPN 인프라](../../../media/Always-On-Vpn/Ao-Vpn-Overview.jpg)

이 그림에 표시 된 연결 프로세스는 다음 단계로 구성 되어 있습니다.

1. Windows 10 VPN 클라이언트는 공용 DNS 서버를 사용 하 여 VPN 게이트웨이의 IP 주소에 대 한 이름 확인 쿼리를 수행 합니다.

2. VPN 클라이언트는 DNS에서 반환 된 IP 주소를 사용 하 여 VPN gateway에 연결 요청을 보냅니다.

3. VPN gateway는 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 클라이언트로도 구성 됩니다. VPN RADIUS 클라이언트는 연결 요청을 처리 하기 위해 조직/회사 NPS 서버에 연결 요청을 보냅니다.

4. NPS 서버는 권한 부여 및 인증 수행을 포함 하 여 연결 요청을 처리 하 고 연결 요청을 허용할지 또는 거부할지를 결정 합니다.

5. NPS 서버는 VPN gateway에 대 한 액세스 허용 또는 액세스 거부 응답을 전달 합니다.

6. VPN 서버가 NPS 서버에서 받은 응답에 따라 연결이 시작 되거나 종료 됩니다.

위의 그림에 나와 있는 각 인프라 구성 요소에 대 한 자세한 내용은 다음 섹션을 참조 하십시오.

>[!NOTE]
>이러한 기술 중 일부를 네트워크에 이미 배포한 경우이 배포 지침의 지침을 사용 하 여이 배포 목적으로 기술에 대 한 추가 구성을 수행할 수 있습니다.

## <a name="domain-name-system-dns"></a>DNS(Domain Name System)

내부 및 외부 DNS (Domain Name System) 영역이 모두 필요 합니다 .이는 내부 영역이 외부 영역 (예: corp.contoso.com 및 contoso.com)의 위임 된 하위 도메인 이라고 가정 합니다.

[DNS (Domain Name System)](../../../../networking/dns/dns-top.md) 또는 [핵심 네트워크 가이드](../../../../networking/core-network-guide/core-network-guide.md)에 대해 자세히 알아보세요.

>[!NOTE]
>분할 된 도메인 이름 (내부적으로는 별도의 DNS 영역에 있는 동일한 도메인 이름 사용) 또는 관련이 없는 내부 및 외부 도메인 (예: contoso. local 및 contoso.com)과 같은 다른 DNS 디자인도 가능 합니다. 분할에 대 한 DNS 배포에 대 한 자세한 내용은 [분할-두뇌 Dns 배포에 대 한 Dns 정책 사용](../../../../networking/dns/deploy/split-brain-DNS-deployment.md)을 참조 하세요.

## <a name="firewalls"></a>방화벽

방화벽에서 VPN 및 RADIUS 통신이 모두 제대로 작동 하는 데 필요한 트래픽을 허용 하는지 확인 합니다.

자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](../../../../networking/technologies/nps/nps-firewalls-configure.md)을 참조 하세요.

## <a name="remote-access-as-a-ras-gateway-vpn-server"></a>RAS 게이트웨이 VPN 서버로 원격 액세스

Windows Server 2016에서 원격 액세스 서버 역할은 라우터 및 원격 액세스 서버를 모두 수행 하도록 설계 되었습니다. 따라서 다양 한 기능의 배열을 지원 합니다. 이 배포 지침은 IKEv2 VPN 연결 및 LAN 라우팅에 대 한 지원의 작은 하위 집합만 필요 합니다.

IKEv2는 인터넷 엔지니어링 작업 Force Request for Comments 7296에 설명 된 VPN 터널링 프로토콜입니다. IKEv2의 주요 이점은 기본 네트워크 연결의 중단을 허용는 것입니다. 예를 들어 연결이 일시적으로 손실 되거나 사용자가 클라이언트 컴퓨터를 한 네트워크에서 다른 네트워크로 이동 하는 경우, IKEv2는 네트워크 연결이 다시 설정 될 때 자동으로 VPN 연결을 복원 합니다. 즉, 사용자 개입이 필요 하지 않습니다.

RAS Gateway를 사용 하 여 VPN 연결을 배포 하 여 최종 사용자에 게 조직의 네트워크 및 리소스에 대 한 원격 액세스를 제공할 수 있습니다. Always On VPN을 배포 하면 원격 컴퓨터가 인터넷에 연결 될 때마다 클라이언트와 조직 네트워크 간에 영구 연결을 유지 관리 합니다. RAS Gateway를 사용 하 여 기본 사무실과 지사 사이에서 서로 다른 위치에 있는 두 서버 간에 사이트 간 VPN 연결을 만들 수도 있으며, 네트워크 내의 사용자가 외부에 액세스할 수 있도록 NAT (Network Address Translation)를 사용할 수도 있습니다. 리소스 (예: 인터넷) 또한 RAS 게이트웨이는 원격 사무실 위치에 BGP를 지 원하는에 지 게이트웨이가 있는 경우 동적 라우팅 서비스를 제공 하는 BGP (Border Gateway Protocol)를 지원 합니다.

Windows PowerShell 명령 및 원격 액세스 MMC (Microsoft Management Console)를 사용 하 여 RAS (원격 액세스 서비스) 게이트웨이를 관리할 수 있습니다.

## <a name="network-policy-server-nps"></a>NPS(네트워크 정책 서버)

NPS를 사용 하면 연결 요청 인증 및 권한 부여에 대 한 조직 전체의 네트워크 액세스 정책을 만들고 적용할 수 있습니다. NPS를 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 서버로 사용 하는 경우 NPS에서 RADIUS 클라이언트로 VPN 서버와 같은 네트워크 액세스 서버를 구성 합니다.

또한 NPS가 연결 요청에 권한을 부여하는 데 사용하는 네트워크 정책을 구성하고, NPS가 로컬 하드 디스크의 로그 파일이나 Microsoft SQL Server 데이터베이스에 계정 정보를 기록하도록 RADIUS 계정을 구성할 수 있습니다.

자세한 내용은 [NPS (네트워크 정책 서버)](../../../../networking/technologies/nps/nps-top.md)를 참조 하세요.

## <a name="active-directory-certificate-services"></a>Active Directory 인증서 서비스

CA (인증 기관) 서버는 Active Directory 인증서 서비스를 실행 하는 인증 기관입니다. VPN 구성에는 Active Directory 기반 PKI (공개 키 인프라)가 필요 합니다.

조직에서는 사람, 디바이스 또는 서비스의 id는 해당 공개 키에 바인딩하여 보안을 강화 하기 위해 AD CS를 사용할 수 있습니다. AD CS에는 인증서 등록 및 해지 다양 한 확장 가능한 환경에서에서 관리할 수 있는 기능이 포함 되어 있습니다. 자세한 내용은 참조 [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx) 및 [공개 키 인프라 디자인 지침](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx)합니다.

배포를 완료 하는 동안 CA에서 다음 인증서 템플릿을 구성 합니다.

- 사용자 인증 인증서 템플릿

- VPN 서버 인증 인증서 템플릿

- NPS 서버 인증 인증서 템플릿

### <a name="certificate-templates"></a>인증서 템플릿

인증서 템플릿은 선택한 작업에 대해 미리 구성 된 인증서를 발급할 수 있도록 하 여 CA (인증 기관)를 관리 하는 작업을 크게 간소화할 수 있습니다. 인증서 템플릿 MMC 스냅인을 사용 하 여 다음 작업을 수행할 수 있습니다.

- 각 인증서 템플릿에 대 한 속성을 봅니다.

- 인증서 템플릿을 복사 하 고 수정 합니다.

- 템플릿을 읽고 인증서를 등록할 수 있는 사용자와 컴퓨터를 제어 합니다.

- 인증서 템플릿과 관련 된 기타 관리 작업을 수행 합니다.

인증서 템플릿은 엔터프라이즈 CA (인증 기관)의 필수적인 부분입니다. 환경에 대 한 인증서 정책의 중요 한 요소 이며, 인증서 등록, 사용 및 관리에 대 한 규칙 및 형식의 집합입니다.

자세한 내용은 [인증서 템플릿](https://technet.microsoft.com/library/cc730705.aspx)을 참조 하세요.

### <a name="digital-server-certificates"></a>디지털 서버 인증서

이 배포 지침은 Active Directory 인증서 서비스 (AD CS)를 사용 하 여 원격 액세스 및 NPS 인프라 서버에 인증서를 등록 하 고 자동으로 등록 하는 방법에 대 한 지침을 제공 합니다. AD CS를 사용 하면 공개 키 인프라 (PKI)를 빌드 및 조직에 대 한 공개 키 암호화, 디지털 인증서 및 디지털 서명 기능을 제공할 수 있습니다.

네트워크에 있는 컴퓨터 간의 인증을 위해 디지털 서버 인증서를 사용 하는 경우 인증서를 제공 합니다.

1. 암호화를 통해 기밀을 유지 합니다.

2. 디지털 서명 통한 무결성입니다.

3. 인증서 키를 컴퓨터 네트워크의 컴퓨터, 사용자 또는 장치 계정에 연결 하 여 인증 합니다.

자세한 내용은 [AD CS 단계별 가이드: 2 계층 PKI 계층 배포](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)를 참조 하세요.

## <a name="active-directory-domain-services-ad-ds"></a>AD DS(Active Directory 도메인 서비스)

AD DS에서는 디렉터리 사용 애플리케이션의 네트워크 리소스와 애플리케이션별 데이터에 대한 정보를 저장하고 관리하는 분산 데이터베이스를 제공합니다. 관리자는 AD DS를 이용해 사용자, 컴퓨터 및 다른 디바이스와 같은 네트워크 요소를 계층적 포함 구조로 구성할 수 있습니다. 계층적 포함 구조에는 Active Directory 포리스트, 포리스트의 도메인 및 각 도메인의 OU(조직 구성 단위)가 포함되어 있습니다. AD DS를 실행하고 있는 서버를 도메인 컨트롤러라고 합니다.

AD DS에는 사용자 자격 증명을 인증 하 고 VPN 연결 요청에 대 한 권한 부여를 평가 하기 위해 PEAP (Protected Extensible Authentication Protocol)에 필요한 사용자 계정, 컴퓨터 계정 및 계정 속성이 포함 되어 있습니다. AD DS를 배포 하는 방법에 대 한 자세한 내용은 Windows Server 2016 [Core 네트워크 가이드](../../../../networking/core-network-guide/Core-Network-Guide.md)를 참조 하세요.

이 배포의 단계를 완료 하는 동안 도메인 컨트롤러에서 다음 항목을 구성 합니다.

- 컴퓨터 및 사용자에 대해 그룹 정책에서 인증서 자동 등록 사용

- VPN 사용자 그룹 만들기

- VPN Servers 그룹 만들기

- NPS 서버 그룹 만들기

### <a name="active-directory-users-and-computers"></a>Active Directory 사용자 및 컴퓨터

Active Directory 사용자 및 컴퓨터는 컴퓨터, 사용자 또는 보안 그룹을 같은 실제 엔터티를 나타내는 계정을 포함 하는 AD DS의 구성 요소입니다. 보안 그룹은 관리자가 단일 단위로 관리할 수 있는 사용자 또는 컴퓨터 계정의 모음입니다. 특정 그룹에 속하는 사용자 및 컴퓨터 계정을 그룹 구성원 이라고 합니다.

Active Directory 사용자 및 컴퓨터의 사용자 계정에는 nps **네트워크 정책을 통해 액세스를 제어**하도록 사용자 계정의 **네트워크 액세스 권한** 속성이 설정 되지 않은 경우 권한 부여 프로세스 중 nps에서 평가 하는 전화 접속 속성이 있습니다. 모든 사용자 계정에 대 한 기본 설정입니다. 그러나 경우에 따라이 설정에는 사용자가 VPN을 사용 하 여 연결 하지 못하도록 차단 하는 다른 구성이 있을 수 있습니다. 이러한 가능성을 방지 하기 위해 사용자 계정 전화 접속 속성을 무시 하도록 NPS 서버를 구성할 수 있습니다.

자세한 내용은 [사용자 계정 전화 접속을 무시 하도록 NPS 구성 속성](../../../../networking/technologies/nps/nps-np-configure.md#configure-nps-to-ignore-user-account-dial-in-properties)을 참조 하세요.

### <a name="group-policy-management"></a>그룹 정책 관리

그룹 정책 관리를 통해 보안 및 사용자 정보를 포함 하 여 사용자 및 컴퓨터 설정의 디렉터리 기반 변경 및 구성 관리를 수행할 수 있습니다. 그룹 정책를 사용 하 여 사용자 및 컴퓨터 그룹의 구성을 정의 합니다.

그룹 정책를 사용 하 여 레지스트리 항목, 보안, 소프트웨어 설치, 스크립트, 폴더 리디렉션, 원격 설치 서비스 및 Internet Explorer 유지 관리에 대 한 설정을 지정할 수 있습니다. 만든 그룹 정책 설정은 GPO (그룹 정책 개체)에 포함 되어 있습니다. Active Directory 시스템 컨테이너에 선택 된 GPO를 연결 하 여-사이트, 도메인 및 Ou-사용자 및 해당 Active Directory 컨테이너에는 컴퓨터에 GPO의 설정을 적용할 수 있습니다. 엔터프라이즈에서 그룹 정책 개체를 관리 하려면 그룹 정책 관리 편집기 MMC (Microsoft Management Console)를 사용할 수 있습니다.

## <a name="windows-10-vpn-clients"></a>Windows 10 VPN 클라이언트

서버 구성 요소 외에도 VPN을 사용 하도록 구성 하는 클라이언트 컴퓨터가 Windows 10 기념일 업데이트 (버전 1607)를 실행 하 고 있는지 확인 합니다. Windows 10 VPN 클라이언트는 도메인에 가입 되어 있어야 Active Directory 도메인에 가입 되어 있어야 합니다.


Windows 10 VPN 클라이언트는 매우 쉽게 구성할 수 있으며 다양 한 옵션을 제공 합니다. 이 시나리오에서 사용 하는 특정 기능을 보다 잘 설명 하기 위해 표 1은이 배포에서 참조 하는 VPN 기능 범주 및 특정 구성을 식별 합니다. 이 배포의 뒷부분에 설명 된 VPNv2 CSP (구성 서비스 공급자)를 사용 하 여 이러한 기능에 대 한 개별 설정을 구성 합니다. 

테이블 1. 이 배포에 설명 되어 있는 VPN 기능 및 구성

| VPN 기능     |     배포 시나리오 구성         |
|-----------------|-----------------------------------------------|
| 연결 형식 |                 기본 IKEv2                  |
|     라우팅     |                분할 터널링                |
| 이름 확인 |  도메인 이름 정보 목록 및 DNS 접미사  |
|   트리거    |    Always On 및 신뢰할 수 있는 네트워크 검색    |
| 인증  | PEAP-TPM-보호 된 사용자 인증서 |

>[!NOTE]
>PEAP-TLS 및 TPM은 각각 "전송 계층 보안을 사용 하는 보호 가능한 인증 프로토콜" 및 "신뢰할 수 있는 플랫폼 모듈"입니다.

### <a name="vpnv2-csp-nodes"></a>VPNv2 CSP 노드

이 배포에서는 ProfileXML VPNv2 CSP 노드를 사용 하 여 Windows 10 클라이언트 컴퓨터에 배달 되는 VPN 프로필을 만듭니다. Csp (구성 서비스 공급자)는 Windows 클라이언트 내에서 다양 한 관리 기능을 노출 하는 인터페이스입니다. 개념적으로, Csp는 그룹 정책 작동 하는 방식과 유사 하 게 작동 합니다. 각 CSP에는 개별 설정을 나타내는 구성 노드가 있습니다. 또한 그룹 정책 설정 처럼 CSP 설정을 레지스트리 키, 파일, 사용 권한 등에 연결할 수 있습니다. 그룹 정책 관리 편집기를 사용 하 여 Gpo (그룹 정책 개체)를 구성 하는 방법과 마찬가지로 Microsoft Intune와 같은 MDM (모바일 장치 관리) 솔루션을 사용 하 여 CSP 노드를 구성 합니다. Intune과 같은 MDM 제품은 운영 체제에서 CSP를 구성 하는 사용자에 게 친숙 한 구성 옵션을 제공 합니다.

![CSP 구성에 대 한 모바일 장치 관리](../../../media/Always-On-Vpn/Vpn-Mdm.jpg)

그러나 Intune 관리 콘솔과 같은 UI (사용자 인터페이스)를 통해 일부 CSP 노드를 직접 구성할 수는 없습니다. 이러한 경우에는 OMA-URI (Open Mobile 동맹 Uniform Resource Identifier) 설정을 수동으로 구성 해야 합니다. 대부분의 최신 Apple, Android 및 Windows 장치에서 지 원하는 범용 장치 관리 사양의 oma-uri (oma 장치 관리 프로토콜)를 사용 하 여 OMA-URI를 구성 합니다. OMA DM 사양을 준수 한다면 모든 MDM 제품은 동일한 방식으로 이러한 운영 체제와 상호 작용 해야 합니다.

Windows 10에서는 많은 Csp를 제공 하지만이 배포에서는 VPNv2 CSP를 사용 하 여 VPN 클라이언트를 구성 하는 방법을 중점적으로 설명 합니다. VPNv2 CSP를 사용 하면 고유한 CSP 노드를 통해 Windows 10에서 각 VPN 프로필 설정을 구성할 수 있습니다. VPNv2 CSP에도 포함 되어 있습니다 .이 노드 *를 사용*하면 모든 설정을 개별적이 아닌 하나의 노드에 구성할 수 있습니다. 프로 파일링에 대 한 자세한 내용은이 배포 뒷부분의 "프로 파일링 개요" 섹션을 참조 하세요. 각 VPNv2 CSP 노드에 대 한 자세한 내용은 [VPNV2 csp](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

- [몇 가지 고급 Always On VPN 기능에 대해 알아봅니다.](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 배포 계획 시작](deploy/always-on-vpn-deploy-deployment.md)

## <a name="related-topics"></a>관련 항목

- [Microsoft Azure 가상 컴퓨터에 대 한 microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines):이 문서에서는 Microsoft Azure 가상 컴퓨터 환경에서 microsoft 서버 소프트웨어를 실행 하는 데 필요한 지원 정책 (infrastructure as a service)에 대해 설명 합니다.

- [원격 액세스](../../Remote-Access.md):이 항목에서는 Windows server 2016의 원격 액세스 서버 역할에 대 한 개요를 제공 합니다.

- [Windows 10 Vpn 기술 가이드](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide):이 가이드에서는 엔터프라이즈 vpn 솔루션의 windows 10 클라이언트에 대해 결정 하는 사항 및 배포를 구성 하는 방법을 안내 합니다. 이 가이드에서는 VPNv2 CSP (구성 서비스 공급자)를 참조 하 고 Microsoft Intune 및 Windows 10 용 VPN 프로필 템플릿을 사용 하 여 MDM (모바일 장치 관리) 구성 지침을 제공 합니다.

- [핵심 네트워크 가이드](../../../../networking/core-network-guide/Core-Network-Guide.md):이 가이드에서는 완벽 하 게 작동 하는 네트워크와 새 포리스트의 새 Active Directory 도메인에 필요한 핵심 구성 요소를 계획 하 고 배포 하는 방법에 대 한 지침을 제공 합니다.

- [Dns (Domain Name System)](../../../../networking/dns/dns-top.md):이 항목에서는 Dns (도메인 이름 시스템)의 개요를 제공 합니다. Windows Server 2016에서 DNS는 서버 관리자 또는 Windows PowerShell 명령을 사용 하 여 설치할 수 있는 서버 역할입니다. 새 Active Directory 포리스트 및 도메인을 설치 하는 경우 DNS 자동으로 설치 됩니다 Active directory 포리스트 및 도메인에 대 한 글로벌 카탈로그 서버입니다.

- [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx):이 문서에서는 Windows Server® 2012에 있는 Active Directory 인증서 서비스 (AD CS)의 개요를 제공 합니다. AD CS는 서버 역할로서 이를 이용하면 조직을 위해 PKI(공개 키 인프라)를 구축할 수 있고 공개 키 암호화, 디지털 인증서, 디지털 서명 기능을 제공할 수 있습니다.

- [공개 키 인프라 디자인 지침](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx):이 Wiki는 Pki (공개 키 인프라) 디자인에 대 한 지침을 제공 합니다. PKI 및 CA (인증 기관) 계층 구조를 구성 하기 전에 조직의 보안 정책 및 CPS (인증서 약관)를 알고 있어야 합니다.

- [AD cs 단계별 가이드: 2 단계 PKI 계층 구조 배포](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx):이 단계별 가이드에서는 랩 환경에서 ad CS (Active Directory® 인증서 서비스)의 기본 구성을 설정 하는 데 필요한 단계에 대해 설명 합니다. Windows Server® 2008 r 2의 AD CS는 공개 키 기술을 사용 하는 소프트웨어 보안 시스템에서 사용 되는 공개 키 인증서를 만들고 관리 하기 위한 사용자 지정 가능한 서비스를 제공 합니다.

- [NPS (네트워크 정책 서버)](../../../../networking/technologies/nps/nps-top.md):이 항목에서는 Windows Server 2016의 네트워크 정책 서버에 대 한 개요를 제공 합니다. 네트워크 정책 서버(NPS)를 사용하면 연결 요청 인증 및 권한 부여를 위해 조직 전체의 네트워크 액세스 정책을 생성하여 적용할 수 있습니다.
