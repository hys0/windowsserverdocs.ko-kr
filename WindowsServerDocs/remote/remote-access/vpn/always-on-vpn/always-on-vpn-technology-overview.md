---
title: Always On VPN 기술 개요
description: '이 페이지 provies 자세한 문서에 대 한 링크를 사용 하 여 Always On VPN 기술에 간략하게 설명 합니다. '
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: fd3f7c6ca8555e270aabf04bbee6800ed284080c
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031327"
---
# Always On VPN 기술 개요
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **이전:** Always On VPN 기능 향상에 알아보기](always-on-vpn-enhancements.md)<br>
& #187;  [ **다음:** Always On VPN의 고급 기능에 알아보기](deploy/always-on-vpn-adv-options.md)

이 배포에 대 한 하면 해야 Windows Server 2016을 실행 하는 새 원격 액세스 서버 설치 뿐 아니라 배포에 대 한 기존 인프라의 일부를 수정 합니다.

다음 그림에서는 Always On VPN 배포 하는 데 필요한 인프라를 보여 줍니다.

![Always On VPN 인프라](../../../media/Always-On-Vpn/Ao-Vpn-Overview.jpg)

이 그림에 표시 된 연결 프로세스에서 다음 단계를 구성 됩니다.

1. 공용 DNS 서버를 사용 하 여 Windows 10 VPN 클라이언트가 VPN 게이트웨이 IP 주소에 대 한 이름 확인 쿼리를 수행 합니다.

2. DNS에서 반환 된 IP 주소를 사용 하 여 VPN 클라이언트가 VPN 게이트웨이 연결 요청을 보냅니다.

3. VPN 게이트웨이 또한 원격 인증 전화 접속 사용자 서비스 \(RADIUS\)로 구성 되어 클라이언트; VPN RADIUS 클라이언트 연결 요청 처리에 대 한 조직/회사 NPS 서버에 연결 요청을 보냅니다.

4. NPS 서버 인증 및 인증을 수행 하는 연결 요청을 처리 하 고 연결 요청의 허용 여부를 결정 합니다.

5. NPS 서버에 대 한 액세스 허용 또는 액세스 거부 응답 VPN 게이트웨이 전달합니다.

6. 연결 시작 되거나 종료 VPN 서버 NPS 서버에서 받은 응답에 따라 합니다.

위 그림에 표시 된 각 인프라 구성 요소에 대 한 자세한 내용은 다음 섹션을 참조 하세요.

>[!NOTE]
>이미 있는 경우 네트워크에 배포 하는 이러한 기술을 중 일부를 배포 하 여 여기에 대 한 기술의 추가 구성을 수행 하려면이 배포 가이드의 지침을 사용할 수 있습니다.

## DNS(Domain Name System)

내부 및 외부 도메인 이름 시스템 (DNS) 영역에는 필요한 내부 영역이 외부 영역 (예를 들어 corp.contoso.com 및 contoso.com)의 위임 된 하위 도메인을 가정 합니다.

[시스템 DNS (도메인 이름)](../../../../networking/dns/dns-top.md) 또는 [핵심 네트워크 가이드](../../../../networking/core-network-guide/core-network-guide.md)에 대 한 자세한 정보를 알아봅니다.




>[!NOTE] 
>다른 DNS 스플릿 브레인 DNS (사용 하 여 동일한 도메인 이름을 내부 및 외부에서 별도 DNS 영역에)와 같은 디자인, 또는 관련 되지 않은 내부 및 외부 도메인 (예: contoso.local 및 contoso.com)을 사용할 수도 있습니다. 스플릿 브레인 DNS 배포에 대 한 자세한 내용은 [분할/브레인 DNS 배포에 DNS 정책 사용을](../../../../networking/dns/deploy/split-brain-DNS-deployment.md)참조 하세요.

## 방화벽

방화벽 제대로 작동 하도록 반경 및 VPN 통신에 필요한 트래픽을 허용 하는지 있는지 확인 합니다.

자세한 내용은 [RADIUS 트래픽에 대 한 방화벽 구성](../../../../networking/technologies/nps/nps-firewalls-configure.md)을 참조 하세요.

## RAS 게이트웨이 VPN 서버로 원격 액세스

Windows Server 2016 원격 액세스 서버 역할 라우터 및 원격 액세스 서버; 모두 수행 하도록 설계 되었습니다. 따라서 다양 한 기능을 지원합니다. 이 배포 가이드에 대 한 이러한 기능 중 일부만 필요한: IKEv2 VPN 연결 및 LAN 라우팅에 대 한 지원 합니다.

IKEv2 VPN 터널링 프로토콜에 대 한 설명을 7296 Internet Engineering Task Force\ 요청에 설명 된입니다. IKEv2의 기본 장점은에서 내부 네트워크 연결 중단을가 것입니다. 예를 들어 연결이 일시적으로 중단 또는 사용자가 다른 네트워크의 클라이언트 컴퓨터를 이동 하는 경우 IKEv2 자동으로 복원 VPN 연결 네트워크 연결을 다시 설정할 때-사용자 개입 없이 모든 합니다.

RAS 게이트웨이 사용 하 여 조직의 네트워크 및 리소스에 대 한 원격 액세스를 사용 하 여 최종 사용자에 게 제공 하기 위해 VPN 연결을 배포할 수 있습니다. Always On VPN 배포 원격 컴퓨터가 인터넷에 연결 되어 될 때마다 클라이언트와 회사 네트워크 간에 영구 연결 유지 관리 합니다. RAS 게이트웨이 사용 하 여 있습니다 또한 서로 다른 위치에 두 서버 간에 사이트 간 VPN 연결을와 같은 기본 사무실와 지점 간의 만들고 사용할 수 있는 네트워크 주소 변환 \(NAT\) 네트워크 내부 사용자가 외부 액세스할 수 있도록 인터넷 등의 리소스입니다. 또한, RAS 게이트웨이 게이트웨이 BGP (프로토콜), 원격 사무실 위치 BGP 지 edge 게이트웨이 있을 때 동적 라우팅 서비스를 제공 하는 지원 합니다.

Windows PowerShell 명령 및 원격 액세스 Microsoft 관리 콘솔 (MMC)를 사용 하 여 원격 액세스 서비스 (RAS) 게이트웨이 관리할 수 있습니다.



## NPS(네트워크 정책 서버)

NPS 만들고 연결 요청 인증 및 권한 부여를 위해 조직 전체의 네트워크 액세스 정책을 적용할 수 있습니다. NPS를 사용 하 여 원격 인증 전화 접속 사용자 서비스 (RADIUS 서버로)에서 NPS RADIUS 클라이언트와 VPN 서버와 같은 네트워크 액세스 서버를 구성할 수 있습니다.

또한 NPS 연결 요청에 권한을 부여 하는 데 사용 하는 네트워크 정책 구성과 NPS 계정 정보를 로그 파일을 Microsoft SQL Server 데이터베이스 또는 로컬 하드 디스크에 기록 되도록 RADIUS 계정을 구성할 수 있습니다.

자세한 내용은 [네트워크 정책 서버 (NPS)를](../../../../networking/technologies/nps/nps-top.md)참조 하세요.


## Active Directory 인증서 서비스

CA (인증 기관) 서버는 Active Directory 인증서 서비스를 실행 하는 인증 기관입니다. VPN 구성에는 Active Directory 기반 공개 키 인프라 (PKI) 필요합니다.

조직은은 사용자, 장치 또는 서비스의 id에 해당 하는 공개 키를 결합 하 여 보안 강화를 위해 AD CS를 사용할 수 있습니다. AD CS 인증서 등록 및 다양 한 고가용성 환경에서에서 해지를 관리할 수 있는 기능이 포함 됩니다. 자세한 내용은 [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx) 및 [공개 키 인프라 디자인 지침](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx)을 참조 하세요.

배포를 완료 하는 동안 CA에 다음 인증서 템플릿 구성 합니다.

-   사용자 인증 인증서 템플릿

-   VPN 서버 인증 인증서 템플릿

-   NPS 서버 인증 인증서 템플릿

### 인증서 템플릿

인증서 템플릿 선택 된 작업에 대 한 미리 구성 된 인증서를 발급할 수 있도록 하 여 인증 기관 (CA) 관리 작업을 크게 간소화할 수 있습니다. 인증서 템플릿 MMC 스냅인을 사용 하면 다음 작업을 수행할 수 있습니다.

-   각 인증서 템플릿에 대 한 속성을 확인 합니다.

-   복사 및 인증서 템플릿을 수정 합니다.

-   있는 사용자를 제어 하 고 컴퓨터를 템플릿 읽고 인증서를 등록할 수 있습니다.

-   인증서 템플릿과 관련 된 다른 관리 작업을 수행 합니다.

인증서 템플릿은 엔터프라이즈 인증 기관 (CA)의 핵심입니다. 이들은 인증서 정책 규칙 및 인증서 등록, 사용 및 관리에 대 한 형식을 집합이 환경에 대 한 중요 한 요소입니다.

자세한 내용은 [인증서 템플릿을](https://technet.microsoft.com/library/cc730705.aspx)참조 하세요.

### 디지털 서버 인증서

이 배포 가이드 Active Directory 인증서 서비스 (AD CS)를 사용 하 여 등록 하 고 원격 액세스 및 NPS 인프라 서버에 인증서를 자동으로 등록에 대 한 지침을 제공 합니다. AD CS 공개 키 인프라 (PKI) 빌드 및 조직에 대 한 공개 키 암호화, 디지털 인증서 및 디지털 서명 기능을 제공할 수 있습니다.

디지털 서버 인증서를 사용 하 여 네트워크의 컴퓨터 간 인증을 위해 인증서를 제공 합니다.

1.  암호화를 통해 기밀성입니다.

2.  디지털 서명을 통해 무결성 합니다.

3.  컴퓨터 네트워크에서 컴퓨터, 사용자 또는 장치 계정을 사용 하 여 인증서 키를 연결 하 여 인증 합니다.

자세한 내용은 참조 [AD CS 단계별 가이드: 두 개의 계층 PKI 계층 구조 배포](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)합니다.

## AD DS(Active Directory 도메인 서비스)

AD DS에 저장 하 고 디렉터리 기반 응용 프로그램에서 네트워크 리소스와 응용 프로그램 관련 데이터에 대 한 정보를 관리 하는 분산된 데이터베이스를 제공 합니다. 관리자가 사용자, 컴퓨터 및 기타 디바이스와 같은 네트워크 요소 계층적 포함 구조로 구성할 AD DS를 사용할 수 있습니다. 계층적 포함 구조는 각 도메인에서 Active Directory 포리스트를 도메인 포리스트 및 Ou (조직 단위)에 포함 됩니다. AD DS를 실행 하는 서버는 도메인 컨트롤러를 라고 합니다.

AD DS 사용자 계정, 컴퓨터 계정 및 사용자 자격 증명을 인증 하 고 VPN 연결 요청에 대 한 인증을 평가 하 여 보호 된 확장할 수 있는 인증 프로토콜 (PEAP) 필요한 계정 속성이 포함 되어 있습니다. AD DS 배포 하는 방법에 대 한 내용은 Windows Server 2016 [핵심 네트워크 가이드](../../../../networking/core-network-guide/Core-Network-Guide.md)를 참조 하세요.



이 배포의 단계를 완료 하는 동안 도메인 컨트롤러에서 다음 항목을 구성 합니다.

-   컴퓨터 및 사용자에 대 한 그룹 정책에서 인증서 자동 등록을 사용 하도록 설정

-   VPN 사용자 그룹 만들기

-   VPN 서버 그룹 만들기

-   NPS 서버 그룹 만들기

### Active Directory 사용자 및 컴퓨터

Active Directory 사용자 및 컴퓨터 보안 그룹, 컴퓨터 및 등에 등의 실제 엔터티를 나타내는 계정을 포함 하는 AD DS의 구성 요소입니다. 보안 그룹의 관리자는 하나의 단위로 관리할 수 있는 사용자 또는 컴퓨터 계정 모음입니다. 특정 그룹에 속하는 사용자 및 컴퓨터 계정은 그룹 구성원으로 참조 됩니다.

Active Directory 사용자 및 컴퓨터의 사용자 계정에 NPS-인증 과정을 평가 하는 전화 접속 속성이 **NPS 네트워크 정책을 통해 액세스 제어로 설정 되어 사용자 계정의 **네트워크 액세스 권한** 속성 **. 모든 사용자 계정에 대 한 기본 설정입니다. 그러나 경우에 따라이 설정이 사용자가 VPN을 사용 하 여 연결을 차단 하는 다른 구성을 가질 수 합니다. 이 문제를 방지 하려면 사용자 계정 전화 접속 속성을 무시 하도록 NPS 서버를 구성할 수 있습니다.

자세한 내용은 [구성 NPS 무시 사용자 계정 전화 접속 속성을](../../../../networking/technologies/nps/nps-np-configure.md#configure-nps-to-ignore-user-account-dial-in-properties)참조 하세요.



### 그룹 정책 관리

그룹 정책 관리를 디렉터리 기반 변경 및 구성 관리를, 보안 및 사용자 정보를 포함 하 여 사용자 및 컴퓨터 설정 수 있습니다. 그룹 정책을 사용 하 여 사용자 및 컴퓨터 그룹에 대 한 구성을 정의 합니다.

그룹 정책을 사용 하 여 레지스트리 항목, 보안, 소프트웨어 설치, 스크립트, 폴더 리디렉션, 원격 설치 서비스 및 Internet Explorer 유지 관리에 대 한 설정을 지정할 수 있습니다. 사용자가 만든 그룹 정책 설정은 그룹 정책 개체 (GPO)에 포함 됩니다. 선택한 Active Directory 시스템 컨테이너를 사용 하 여 GPO를 연결 하 여-사이트, 도메인 및 Ou의 사용자와 그 Active Directory 컨테이너의 컴퓨터에 GPO의 설정을 적용할 수 있습니다. 기업 전체에서 그룹 정책 개체를 관리 하려면 그룹 정책 관리 편집기 Microsoft Management Console (MMC)를 사용할 수 있습니다.


## Windows 10 VPN 클라이언트

서버 구성 요소와 함께 VPN을 사용 하도록 구성 된 클라이언트 컴퓨터에서 windows 10 1 주년 업데이트 (version1607) 실행 되 고 있는지 확인 합니다. Windows 10 VPN 클라이언트는 Active Directory 도메인에 도메인에 가입 된 이어야 합니다.


Windows 10 VPN 클라이언트 매우 구성 가능 하며 많은 옵션을 제공 합니다. 이해를 돕기 위해이 시나리오는 특정 기능, 표 1이이 배포를 참조 하는 VPN 기능 범주 및 특정 구성을 식별 합니다. 이 배포의 뒷부분에 나오는 VPNv2 구성 서비스 공급자 (CSP)를 사용 하 여 이러한 기능에 대 한 개별 설정을 구성 합니다. 

표 1. VPN 기능 및이 배포에서 설명 하는 구성

| **VPN 기능** | **배포 시나리오 구성**         |
|-----------------|-----------------------------------------------|
| 연결 형식 | 기본 IKEv2                                  |
| 라우팅         | 분할 터널링                               |
| 이름 확인 | 도메인 이름 정보 목록 및 DNS 접미사   |
| 트리거      | 항상 설정 및 신뢰할 수 있는 네트워크 검색       |
| Authentication  | TPM 보호 된 사용자 인증서를 사용 하 여 PEAP TLS |
---

>[!NOTE] 
>PEAP-TLS 및 TPM은 "보호 확장할 수 있는 인증 프로토콜 사용 하 여 전송 계층 보안" 및 "신뢰할 수 있는 플랫폼 모듈," 각각입니다.

### VPNv2 CSP 노드

이 배포에서는 windows 10 클라이언트 컴퓨터에 전달 되는 VPN 프로필을 만들 ProfileXML VPNv2 CSP 노드를 사용 합니다. 구성 서비스 공급자 (Csp)는 Windows 클라이언트에 다양 한 관리 기능을 노출 하는 인터페이스 개념적으로 Csp 그룹 정책 작동 방식 비슷하게 작동 합니다. 각 CSP는 개별 설정을 나타내는 구성 노드가 있습니다. 또한 그룹 정책 설정, 같은 CSP 설정 레지스트리 키, 파일, 권한을 연결할 수 있습니다. 그룹 정책 개체 (Gpo)를 구성 하려면 그룹 정책 관리 편집기를 사용 하는 방법을 마찬가지로 구성한 CSP 노드 Microsoft Intune과 같은 모바일 장치 관리 (MDM) 솔루션을 사용 하 여 합니다. Intune 같은 MDM 제품은 운영 체제에서 CSP를 구성 하는 친숙 한 구성 옵션을 제공 합니다.

![CSP 구성에 모바일 장치 관리](../../../media/Always-On-Vpn/Vpn-Mdm.jpg)

그러나 일부 같은 Intune 관리 콘솔 사용자 인터페이스 (UI)을 통해 직접 CSP 노드를 구성할 수 없습니다. 이러한 경우 Open Mobile Alliance Uniform Resource Identifier (OMA-URI) 설정을 구성 해야 수동으로 합니다. 대부분의 최신 Apple, Android 및 Windows 장치에 지원 되는 유니버설 디바이스 관리 사양 OMA 장치 관리 프로토콜 (OMA-DM)를 사용 하 여 OMA Uri를 구성 합니다. OMA DM 사양을 준수,으로 모든 MDM 제품 동일한 방식으로 이러한 운영 체제 상호 작용 해야 합니다.

Windows 10은 많은 Csp를 제공 하지만이 배포 VPNv2 CSP를 사용 하 여 VPN 클라이언트를 구성 하에 중점을 둡니다. VPNv2 CSP 고유한 CSP 노드를 통해 windows 10의 각 VPN 프로필 설정의 구성을 수 있습니다. *ProfileXML*, 모든 설정을 구성할 수 있는 라는 노드에 VPNv2 CSP에도 포함 한 노드에 개별적이 아니라 합니다. ProfileXML에 대 한 자세한 내용은이 배포의 뒷부분에 나오는 "ProfileXML 개요" 섹션을 참조 하세요. 각 VPNv2 CSP 노드에 대 한 자세한 [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp)참조 하세요.



## 다음 단계

- [Always On VPN 고급 기능 중 일부에 대해 알아보기](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 배포 계획](deploy/always-on-vpn-deploy-deployment.md)


---

## 관련 항목
- [Microsoft Azure 가상 컴퓨터에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines): Microsoft Azure 가상 컴퓨터 (인프라도-서비스) 환경에서 Microsoft 서버 소프트웨어를 실행 하기 위한 지원 정책에 설명 합니다.

- [원격 액세스](../../Remote-Access.md):이 항목에서는 Windows Server 2016에서 원격 액세스 서버 역할의 개요를 제공 합니다.

- [Windows 10 VPN 기술 가이드](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide):이 가이드를 엔터프라이즈 VPN 솔루션 및 배포를 구성 하는 방법에 대 한 Windows 10 클라이언트 결정할 단계별로 안내 메시지를 표시 합니다. 이 가이드는 VPNv2 CSP(구성 서비스 공급자)를 참조하고 Microsoft Intune 및 Windows 10용 VPN 프로필 템플릿을 사용하는 MDM(모바일 장치 관리) 구성 지침을 제공합니다.

- [핵심 네트워크 가이드](../../../../networking/core-network-guide/Core-Network-Guide.md):이 가이드 계획 하 고 완벽 하 게 작동 네트워크 및 새 포리스트에서 새 Active Directory 도메인에 필요한 핵심 구성 요소를 배포 하는 방법에 대해 설명 합니다.

- [시스템 DNS (도메인 이름)](../../../../networking/dns/dns-top.md):이 항목에서는 도메인 이름 시스템 (DNS)의 개요를 제공 합니다. Windows Server 2016에서 DNS는 서버 관리자 또는 Windows PowerShell 명령을 사용 하 여 설치할 수 있는 서버 역할입니다. 새 Active Directory 포리스트 및 도메인을 설치 하는 경우 DNS가 자동으로 설치 Active directory 포리스트 및 도메인에 대 한 글로벌 카탈로그 서버. 

- [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx):이 문서에서는 Active Directory 인증서 서비스 (AD CS) Windows Server® 2012에 대 한 개요를 제공 합니다. AD CS 하면 공개 키 인프라 (PKI) 빌드를 조직에 대 한 공개 키 암호화, 디지털 인증서 및 디지털 서명 기능을 제공 하는 서버 역할입니다.

- [공개 키 인프라 디자인 지침](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx):이 wiki 공개 키 인프라 (Pki) 디자인 지침을 제공 합니다. PKI 및 인증 기관 (CA) 계층 구조를 구성 하기 전에 조직의 보안 정책 및 인증서 사용 약관 (CPS) 알고 있어야 합니다.

- [AD CS 단계별 가이드: 두 개의 계층 PKI 계층 구조 배포](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx):이 단계별 가이드 랩 환경에서 Active Directory® 인증서 서비스 (AD CS)의 기본 구성을 설정 하는 데 필요한 단계에 설명 합니다. Windows Server® 2008 r 2의 AD CS 만들고 공개 키 기술이 적용 된 소프트웨어 보안 시스템에서 사용 되는 공개 키 인증서를 관리 하기 위한 사용자 지정 가능한 서비스를 제공 합니다.

- [네트워크 정책 서버 (NPS)](../../../../networking/technologies/nps/nps-top.md):이 항목에서는 Windows Server 2016의 네트워크 정책 서버의 개요를 제공 합니다. 네트워크 정책 서버(NPS)를 사용하면 연결 요청 인증 및 권한 부여를 위해 조직 전체의 네트워크 액세스 정책을 생성하여 적용할 수 있습니다. 

---
