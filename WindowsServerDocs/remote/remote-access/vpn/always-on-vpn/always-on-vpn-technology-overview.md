---
title: VPN 기술 개요에서 항상
description: '이 페이지는 자세한 문서에 대 한 링크를 사용 하 여 Always On VPN 기술에 간략하게 설명 합니다. '
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 65a575b24ea3c70ad7eedd95fe287d955ccaeea6
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749681"
---
# <a name="always-on-vpn-technology-overview"></a>Always On VPN 기술 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** Always On VPN 향상 된 기능에 알아봅니다](always-on-vpn-enhancements.md)
- [**다음:** Always On VPN의 고급 기능에 대해 알아보기](deploy/always-on-vpn-adv-options.md)

이 배포에 대 한 있습니다 해야 Windows Server 2016을 실행 하는 새로운 원격 액세스 서버를 설치 뿐만 아니라 배포에 대 한 기존 인프라의 일부를 수정 합니다.

다음 그림에서는 Always On VPN을 배포 하는 데 필요한 인프라를 보여 줍니다.

![VPN 인프라 always On](../../../media/Always-On-Vpn/Ao-Vpn-Overview.jpg)

이 그림에 나와 있는 연결 프로세스는 다음 단계로 구성 됩니다.

1. Windows 10 VPN 클라이언트 공용 DNS 서버를 사용 하 여, VPN gateway의 IP 주소에 대 한 이름 확인 쿼리를 수행 합니다.

2. DNS에서 반환 하는 IP 주소를 사용 하 여, VPN 클라이언트가 VPN gateway에 연결 요청을 보냅니다.

3. VPN gateway는 전화 접속 사용자 서비스 RADIUS (Remote Authentication) 클라이언트로;도 구성 VPN RADIUS 클라이언트 연결 요청 처리를 위해 조직/회사 NPS 서버로 연결 요청을 보냅니다.

4. NPS 서버는 권한 부여 및 인증을 수행 하는 포함 하 여 연결 요청을 처리 하 고 연결 요청 허용 여부를 결정 합니다.

5. NPS 서버는 VPN gateway에 대 한 액세스 허용 또는 액세스 거부 응답을 전달합니다.

6. 연결 시작 되거나 종료 되는 VPN 서버는 NPS 서버에서 받은 응답에 기반 합니다.

위의 그림에 나와 있는 각 인프라 구성 요소에 대 한 자세한 내용은 다음 섹션을 참조 하세요.

>[!NOTE]
>이미 있는 경우 해당 네트워크에 배포 하는 이러한 기술 중 일부를이 배포를 위해 기술의 추가 구성을 수행 하려면이 배포 가이드의 지침을 사용할 수 있습니다.

## <a name="domain-name-system-dns"></a>DNS(Domain Name System)

내부 및 외부 도메인 이름 시스템 (DNS) 영역은 필요한 경우 내부 영역 외부 영역 (예: corp.contoso.com 및 contoso.com)의 하위 도메인 위임된 이라고 가정입니다.

에 대해 자세히 알아보세요 [도메인 이름 시스템 (DNS)](../../../../networking/dns/dns-top.md) 하거나 [핵심 네트워크 가이드](../../../../networking/core-network-guide/core-network-guide.md)합니다.

>[!NOTE]
>다른 DNS 스플릿 브레인 DNS (사용 하 여 동일한 도메인 이름을 내부 및 외부에서 별도 DNS 영역에서)와 같은 디자인 관련 되지 않은 내부 및 외부 도메인 (예: contoso.local과 contoso.com)을 사용할 수도 있습니다. 스플릿 브레인 DNS 배포에 대 한 자세한 내용은 참조 하십시오 [DNS Split-Brain 배포에 대 한 DNS 정책을 사용 하 여](../../../../networking/dns/deploy/split-brain-DNS-deployment.md)입니다.

## <a name="firewalls"></a>방화벽

방화벽이 제대로 작동 하려면 VPN 및 RADIUS 통신 하기 위해 필요한 트래픽을 허용 하는지 확인 합니다.

자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](../../../../networking/technologies/nps/nps-firewalls-configure.md)합니다.

## <a name="remote-access-as-a-ras-gateway-vpn-server"></a>RAS 게이트웨이 VPN 서버로 원격 액세스

Windows Server 2016에서 원격 액세스 서버 역할은 라우터 및 원격 액세스 서버를 모두 수행 하도록 설계 따라서 다양 한 기능을 지원합니다. 이 배포 가이드에 대 한 이러한 기능 중 일부만 필요: IKEv2 VPN 연결 및 LAN 라우팅에 대 한 지원.

IKEv2 VPN 터널링 프로토콜 주석 7296에 대 한 Internet Engineering Task Force 요청에 설명 된 경우 IKEv2의 주요 이점은 기본 네트워크 연결에서 중단을 허용 하는 경우 예를 들어 연결이 일시적으로 끊어진 경우 또는 사용자 클라이언트 컴퓨터 하나의 네트워크에서 다른 위치로 이동 하는 경우 IKEv2를 자동으로 복원 VPN 연결 네트워크 다시 연결이 되 면, 사용자 개입 없이 합니다.

RAS 게이트웨이 사용 하 여 VPN 연결을 통해 조직의 네트워크와 리소스에 대 한 원격 액세스를 사용 하 여 최종 사용자에 게 배포할 수 있습니다. Always On VPN 배포 원격 컴퓨터가 인터넷에 연결 되어 때마다 클라이언트와 조직 네트워크에 영구 연결을 유지 관리 합니다. RAS 게이트웨이 사용 하 여 만들고 수 있습니다도 다른 위치에 있는 두 서버 간에 사이트 간 VPN 연결을 같은 주 사무실 및 지점 간 네트워크 내에서 사용자는 외부 액세스할 수 있도록 네트워크 주소 변환 (NAT)를 사용 하 여 인터넷 등의 리소스입니다. 또한 RAS 게이트웨이 프로토콜 BGP (경계 게이트웨이), 원격 사무실 위치에 있어야 edge 게이트웨이에 BGP를 지 원하는 경우 동적 라우팅 서비스를 제공 하는 지원 합니다.

Windows PowerShell 명령 및 원격 액세스 관리 콘솔 (MMC (Microsoft)를 사용 하 여 원격 액세스 서비스 (RAS) 게이트웨이 관리할 수 있습니다.

## <a name="network-policy-server-nps"></a>NPS(네트워크 정책 서버)

NPS 연결 요청 인증 및 권한 부여에 대 한 조직 전체의 네트워크 액세스 정책을 만들고 적용할 수 있습니다. 전화 접속 사용자 서비스 RADIUS (Remote Authentication) 서버와 NPS를 사용 하는 경우 NPS에서 RADIUS 클라이언트로 VPN 서버와 같은 네트워크 액세스 서버를 구성 합니다.

또한 NPS가 연결 요청에 권한을 부여하는 데 사용하는 네트워크 정책을 구성하고, NPS가 로컬 하드 디스크의 로그 파일이나 Microsoft SQL Server 데이터베이스에 계정 정보를 기록하도록 RADIUS 계정을 구성할 수 있습니다.

자세한 내용은 [네트워크 정책 (NPS 서버)](../../../../networking/technologies/nps/nps-top.md)합니다.

## <a name="active-directory-certificate-services"></a>Active Directory 인증서 서비스

CA (인증 기관) 서버를 Active Directory 인증서 서비스를 실행 하는 인증 기관입니다. VPN 구성에는 Active Directory 기반 PKI (공개 키 인프라)에 필요합니다.

조직에서는 사람, 장치 또는 서비스의 id는 해당 공개 키에 바인딩하여 보안을 강화 하기 위해 AD CS를 사용할 수 있습니다. AD CS에는 인증서 등록 및 해지 다양 한 확장 가능한 환경에서에서 관리할 수 있는 기능이 포함 되어 있습니다. 자세한 내용은 참조 [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx) 및 [공개 키 인프라 디자인 지침](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx)합니다.

배포를 완료 하는 동안 CA에서 다음 인증서 템플릿을 구성 합니다.

- 사용자 인증 인증서 템플릿

- VPN 서버 인증 인증서 템플릿

- NPS 서버 인증 인증서 템플릿

### <a name="certificate-templates"></a>인증서 템플릿

인증서 템플릿을 선택한 작업에 대 한 미리 구성 된 인증서를 발급할 수 있도록 하 여 인증 기관 (CA)를 관리 하는 작업을 크게 간소화할 수 있습니다. 인증서 템플릿 MMC 스냅인을 사용 하 여 다음 작업을 수행할 수 있습니다.

- 각 인증서 템플릿에 대 한 속성을 봅니다.

- 복사한 인증서 템플릿을 수정 합니다.

- 사용자 및 컴퓨터 템플릿을 읽을 수 및 인증서를 등록할 컨트롤입니다.

- 인증서 템플릿 관련 된 기타 관리 작업을 수행 합니다.

인증서 템플릿은 엔터프라이즈 인증 기관 (CA)의 필수적인 부분입니다. 인증서 등록, 사용 및 관리에 대 한 형식 및 규칙 집합이 environment에 대 한 인증서 정책의 중요 한 요소가 됩니다.

자세한 내용은 [인증서 템플릿](https://technet.microsoft.com/library/cc730705.aspx)합니다.

### <a name="digital-server-certificates"></a>디지털 서버 인증서

이 배포 가이드는 Active Directory 인증서 서비스 (AD CS)를 사용 하 여 등록 및 원격 액세스 및 NPS 인프라 서버에 인증서를 자동으로 등록 하는 지침을 제공 합니다. AD CS를 사용 하면 공개 키 인프라 (PKI)를 빌드 및 조직에 대 한 공개 키 암호화, 디지털 인증서 및 디지털 서명 기능을 제공할 수 있습니다.

네트워크에 있는 컴퓨터 간의 인증을 위해 디지털 서버 인증서를 사용 하는 경우 인증서를 제공 합니다.

1. 암호화를 통해 기밀을 유지 합니다.

2. 디지털 서명 통한 무결성입니다.

3. 컴퓨터 네트워크의 컴퓨터, 사용자 또는 장치 계정과 인증서 키를 연결 하 여 인증 합니다.

자세한 내용은 참조 하세요. [AD CS 단계별 가이드: 2 계층 PKI 계층 배포](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)합니다.

## <a name="active-directory-domain-services-ad-ds"></a>AD DS(Active Directory 도메인 서비스)

AD DS에서는 디렉터리 사용 응용 프로그램의 네트워크 리소스와 응용 프로그램별 데이터에 대한 정보를 저장하고 관리하는 분산 데이터베이스를 제공합니다. 관리자는 AD DS를 이용해 사용자, 컴퓨터 및 다른 장치와 같은 네트워크 요소를 계층적 포함 구조로 구성할 수 있습니다. 계층적 포함 구조에는 Active Directory 포리스트, 포리스트의 도메인 및 각 도메인의 OU(조직 구성 단위)가 포함되어 있습니다. AD DS를 실행하고 있는 서버를 도메인 컨트롤러라고 합니다.

AD DS 사용자 계정, 컴퓨터 계정 및 사용자 자격 증명을 인증 하 고 VPN 연결 요청에 대 한 권한 부여를 평가 하 여 인증 프로토콜 PEAP (Protected Extensible) 필요한 계정 속성을 포함 합니다. AD DS를 배포 하는 방법에 대 한 내용은 Windows Server 2016을 참조 하세요 [핵심 네트워크 가이드](../../../../networking/core-network-guide/Core-Network-Guide.md)합니다.

이 배포의 단계를 완료 하는 동안 도메인 컨트롤러에서 다음 항목을 구성 합니다.

- 컴퓨터 및 사용자에 대 한 그룹 정책에서 인증서 자동 등록을 사용 하도록 설정

- VPN 사용자 그룹 만들기

- VPN 서버 그룹 만들기

- NPS 서버 그룹 만들기

### <a name="active-directory-users-and-computers"></a>Active Directory 사용자 및 컴퓨터

Active Directory 사용자 및 컴퓨터는 컴퓨터, 사용자 또는 보안 그룹을 같은 실제 엔터티를 나타내는 계정을 포함 하는 AD DS의 구성 요소입니다. 보안 그룹은 관리자가 단일 단위로 관리할 수 있는 사용자 또는 컴퓨터 계정의 모음입니다. 특정 그룹에 속하는 사용자 및 컴퓨터 계정은 그룹 구성원 이라고 합니다.

사용자 계정 Active Directory 사용자 및 컴퓨터에 있지 않은 NPS-권한 부여 프로세스 중 계산 되는 전화 접속 속성을 **네트워크 액세스 권한** 사용자 계정의 속성 **컨트롤 NPS 네트워크 정책을 통해 액세스**합니다. 모든 사용자 계정에 대 한 기본 설정입니다. 그러나 일부 경우에이 설정은 사용자가 VPN을 사용 하 여 연결 하지 못하게 하는 다른 구성이 있을 수 있습니다. 이 가능성을 방지 하려면 사용자 계정 전화 접속 속성을 무시 하도록 NPS 서버를 구성할 수 있습니다.

자세한 내용은 [무시 사용자 계정 전화 접속 속성을 구성할 NPS](../../../../networking/technologies/nps/nps-np-configure.md#configure-nps-to-ignore-user-account-dial-in-properties)합니다.

### <a name="group-policy-management"></a>그룹 정책 관리

그룹 정책 관리 디렉터리 기반 변경 및 구성 설정 관리할을 수 사용자 및 컴퓨터, 보안 및 사용자 정보를 포함 합니다. 그룹 정책을 사용 하 여 사용자 및 컴퓨터 그룹에 대 한 구성을 정의 합니다.

그룹 정책을 사용 하 여 레지스트리 항목, 보안, 소프트웨어 설치, 스크립트, 폴더 리디렉션, 원격 설치 서비스 및 Internet Explorer 유지 관리에 대 한 설정을 지정할 수 있습니다. 사용자가 만든 그룹 정책 설정이 그룹 정책 개체 (GPO)에 포함 됩니다. Active Directory 시스템 컨테이너에 선택 된 GPO를 연결 하 여-사이트, 도메인 및 Ou-사용자 및 해당 Active Directory 컨테이너에는 컴퓨터에 GPO의 설정을 적용할 수 있습니다. 기업 내 그룹 정책 개체를 관리 하려면 그룹 정책 관리 편집기 Microsoft 관리 콘솔 (MMC)를 사용할 수 있습니다.

## <a name="windows-10-vpn-clients"></a>Windows 10 VPN 클라이언트

서버 구성 요소 외에도 VPN을 사용 하도록 구성 하는 클라이언트 컴퓨터에서 Windows 10 1 주년 업데이트 (버전 1607) 실행 되 고 있는지를 확인 합니다. Active Directory 도메인에 도메인에 가입 된 Windows 10 VPN 클라이언트가 있어야 합니다.


Windows 10 VPN 클라이언트는 고도로 구성 가능 하 고 다양 한 옵션을 제공 합니다. 표 1에는 이해를 돕기 위해이 시나리오에서는 특정 기능을이 배포를 참조 하는 VPN 기능 범주 및 특정 구성을 식별 합니다. 이 배포의 뒷부분에서 설명 된 VPNv2 CSP (구성 서비스 공급자)를 사용 하 여 이러한 기능에 대 한 개별 설정을 구성 합니다. 

표 1. VPN 기능 및이 배포에 설명 된 구성

| VPN 기능     |     배포 시나리오 구성         |
|-----------------|-----------------------------------------------|
| 연결 형식 |                 Native IKEv2                  |
|     라우팅     |                분할 터널링                |
| 이름 확인 |  도메인 이름 정보 목록 및 DNS 접미사  |
|   트리거    |    Always On이 고 신뢰할 수 있는 네트워크 검색    |
| 인증  | TPM-보호 된 사용자 인증서를 사용 하 여에 PEAP TLS |

>[!NOTE]
>PEAP-TLS 및 TPM은 "보호 된 확장할 수 있는 인증 프로토콜 사용 하 여 전송 계층 보안" 및 "신뢰할 수 있는 플랫폼 모듈을" 각각입니다.

### <a name="vpnv2-csp-nodes"></a>VPNv2 CSP 노드

이 배포에서는 ProfileXML VPNv2 CSP 노드를 사용 하 여 Windows 10 클라이언트 컴퓨터에 전달 되는 VPN 프로필을 만듭니다. 구성 서비스 공급자 (Csp)는 Windows 클라이언트; 내에서 다양 한 관리 기능을 노출 하는 인터페이스 개념적으로 Csp 그룹 정책 작동 원리 비슷하게 작동 합니다. 각 CSP에 개별 설정을 나타내는 구성 노드가 있습니다. 또한 그룹 정책 설정과 같은 레지스트리 키, 파일, 권한 및 등 CSP 설정을 연결할 수 있습니다. 그룹 정책 개체 (Gpo)를 구성 하 여 그룹 정책 관리 편집기를 사용 하는 방법을 마찬가지로 구성한 CSP 노드 예: Microsoft Intune 모바일 장치 관리 (MDM) 솔루션을 사용 하 여 합니다. Intune과 같은 MDM 제품에는 운영 체제에서 CSP를 구성 하는 친숙 한 구성 옵션을 제공 합니다.

![CSP 구성에 모바일 장치 관리](../../../media/Always-On-Vpn/Vpn-Mdm.jpg)

그러나 일부 CSP 노드에 같은 Intune 관리 콘솔 사용자 인터페이스 (UI)를 통해 직접 구성할 수 없습니다. 이러한 경우에는 Open Mobile Alliance Uniform Resource Identifier (OMA-URI) 설정을 구성 해야 수동으로. 최신 Apple, Android 및 Windows 장치에 지원 되는 범용 장치 관리 사양 OMA 장치 관리 프로토콜 (8.1(OMA-DM)를 사용 하 여 OMA Uri를 구성 합니다. 준수 하는 OMA-DM 사양,으로 MDM 제품 모두 동일한 방식으로 이러한 운영 체제 상호 작용 해야 합니다.

Windows 10에는 많은 Csp 제공 하지만,이 배포 VPNv2 CSP를 사용 하 여 VPN 클라이언트 구성에 중점을 둡니다. VPNv2 CSP는 고유한 CSP 노드를 통해 Windows 10에서 각 VPN 프로필 설정 구성할 수 있습니다. 노드인 호출도 VPNv2 CSP에 포함 *ProfileXML*, 모든 설정을 구성할 수 있는 하나의 노드에서만 보다는 개별적으로 합니다. ProfileXML에 대 한 자세한 내용은이 배포의 뒷부분에 나오는 "ProfileXML 개요" 섹션을 참조 하세요. 각 VPNv2 CSP 노드에 대 한 자세한 내용은 참조는 [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp)합니다.

## <a name="next-steps"></a>다음 단계

- [고급 Always On VPN 기능 중 일부에 대해 알아봅니다](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 배포 계획 시작](deploy/always-on-vpn-deploy-deployment.md)

## <a name="related-topics"></a>관련 항목

- [Microsoft Azure virtual machines에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines): 이 문서에서는 Microsoft Azure 가상 머신 환경 (인프라-as a service)에서 Microsoft 서버 소프트웨어를 실행 하는 것에 대 한 지원 정책을 설명 합니다.

- [원격 액세스](../../Remote-Access.md): 이 항목에서는 Windows Server 2016에서 원격 액세스 서버 역할의 개요를 제공합니다.

- [Windows 10 VPN에 대 한 기술 가이드](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): 이 가이드에서는 VPN 솔루션을 기업에서 Windows 10 클라이언트 및 배포를 구성 하는 방법에 대 한 결정은을 안내 합니다. 이 가이드는 VPNv2 구성 서비스 공급자 (CSP)를 참조 하 고 모바일 장치 관리 Windows 10 용 Microsoft Intune 및 VPN 프로필 템플릿을 사용 하 여 (MDM) 구성 지침을 제공 합니다.

- [핵심 네트워크 가이드](../../../../networking/core-network-guide/Core-Network-Guide.md): 이 가이드는 계획을 완벽 하 게 작동 하는 네트워크와 새 포리스트의 새 Active Directory 도메인에 필요한 핵심 구성 요소를 배포 하는 방법에 지침을 제공 합니다.

- [도메인 이름 시스템 (DNS)](../../../../networking/dns/dns-top.md): 이 항목에서는 도메인 이름 시스템 (DNS)의 개요를 제공합니다. Windows Server 2016에서 DNS는 서버 관리자 또는 Windows PowerShell 명령을 사용 하 여 설치할 수 있는 서버 역할입니다. 새 Active Directory 포리스트 및 도메인을 설치 하는 경우 DNS 자동으로 설치 됩니다 Active directory 포리스트 및 도메인에 대 한 글로벌 카탈로그 서버입니다.

- [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx): 이 문서는 Active Directory 인증서 서비스 (AD CS) Windows Server® 2012의 개요를 제공합니다. AD CS는 서버 역할로서 이를 이용하면 조직을 위해 PKI(공개 키 인프라)를 구축할 수 있고 공개 키 암호화, 디지털 인증서, 디지털 서명 기능을 제공할 수 있습니다.

- [공개 키 인프라 디자인 지침](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx):  이 wiki에 공개 키 인프라 (Pki) 디자인 지침을 제공 합니다. PKI 및 인증 기관 (CA) 계층 구조를 구성 하기 전에 조직의 보안 정책 및 인증서 cps ()를 인식 해야 합니다.

- [AD CS 단계별 가이드: 2 계층 PKI 계층 배포](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx): 이 단계별 가이드는 랩 환경에서 Active Directory® 인증서 서비스 (AD CS)의 기본 구성을 설정 하는 데 필요한 단계를 설명 합니다. Windows Server® 2008 R2의 AD CS 만들고 공개 키 기술을 적용 하는 소프트웨어 보안 시스템에 사용 되는 공개 키 인증서를 관리 하기 위한 사용자 지정 가능한 서비스를 제공 합니다.

- [네트워크 정책 서버 (NPS)](../../../../networking/technologies/nps/nps-top.md): 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버 개요를 제공합니다. 네트워크 정책 서버(NPS)를 사용하면 연결 요청 인증 및 권한 부여를 위해 조직 전체의 네트워크 액세스 정책을 생성하여 적용할 수 있습니다.
