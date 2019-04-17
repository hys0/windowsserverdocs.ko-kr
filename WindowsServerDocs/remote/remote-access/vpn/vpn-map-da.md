---
title: Always On VPN 기능
description: 이 항목에서는 Always On VPN 특징과 기능에 대해 알아봅니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.assetid: 8fe1c810-4599-4493-b4b8-73fa9aa18535
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 68d8561eb55b844a80c8b6a38d1255ad44457af6
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6066857"
---
# Always On VPN 기능 및 특성

>적용 대상: Windows Server \(Semi-Annual Channel\), Windows Server 2016, Windows 10

& #171;  [ **이전:** Windows에 대 한 VPN 배포에서 항상 서버 및 Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md)<br>
& #187; [ **다음:** 항상 VPN 향상 된 기능에 대 한 자세한](../vpn/always-on-vpn/always-on-vpn-enhancements.md)

이 항목에서는 Always On VPN 특징과 기능에 대해 알아봅니다.  하지만 다음 표에서 전체 목록이 아니며에서는 가장 일반적인 기능 및 원격 액세스 솔루션에서 사용 되는 기능 중 일부 포함지 않습니다. 

>[!TIP]
>현재 DirectAccess를 사용 하는 경우에 DirectAccess Always On VPN을 형성 마이그레이션을 수행 하기 전에 원격 액세스 요구 사항을 해결 하는 경우 확인을 신중 하 게 Always On VPN 기능을 조사 하는 것이 좋습니다.  

| 기능 영역 | Always On VPN  |
| ---- | ---- |
| 회사 네트워크에 연결을 원활 하 게, 투명 합니다. | Always On VPN 응용 프로그램 시작 또는 네임 스페이스 확인 요청에 따라 자동 트리거를 지원 하도록 구성할 수 있습니다.<p><p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/AlwaysOn**<br>**VPNv2/ProfileName/AppTriggerList**<br>**VPNv2/ProfileName/DomainNameInformationList/AutoTrigger** |
| 회사 네트워크에 서명 되지 않은 사용자에 대 한 연결을 제공 하는 전용 인프라 터널을 사용 합니다. | VPN 프로필의 장치 터널 기능을 사용 하 여이 기능을 얻을 수 있습니다.<p><p>_**참고.**_<br>장치 터널 IKEv2를 사용 하 여 컴퓨터 인증서 인증을 사용 하 여 도메인에 가입 된 장치에만 구성할 수 있습니다.<p><p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/DeviceTunnel** |
| 회사 네트워크에 있는 관리 시스템에서 클라이언트 원격 연결을 허용 하도록 관리 아웃을 사용 합니다. | 내부 DNS 서비스 포함 VPN 인터페이스에 할당 된 IP 주소를 동적으로 등록 하도록 VPN 연결을 구성 하는과 결합 된 VPN 프로필의 장치 터널 기능을 사용 하 여이 기능을 얻을 수 있습니다.<p><p>_**참고.**_<br>장치 터널 프로필에 대 한 트래픽 필터를 설정 하면 장치 터널 (클라이언트에 회사 네트워크)에서 인바운드 트래픽의 거부 합니다.<p><p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/DeviceTunnel**<br>**VPNv2/ProfileName/RegisterDNS** |
| 방화벽 또는 프록시 서버 뒤에 클라이언트는 때를 대체 합니다. | VPN 프로필에서 자동 터널/프로토콜 형식을 사용 하 여 (IKEv2)에서 SSTP 돌아갈 구성할 수 있습니다.<p><p>_**참고.**_<br>사용자 터널 SSTP 및 IKEv2, 지원 및 장치 터널와 SSTP 대체에 대 한 지원 되지 않는 IKEv2를 지원 합니다.<p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/NativeProfile/NativeProtocolType** |
| 액세스 최종-에 지 모드를 지원 합니다. | Always On VPN VPN 게이트웨이 도달할 때까지 인증 및 암호화를 요구 하는 터널 정책을 사용 하 여 회사 리소스에 대 한 연결을 제공 합니다. 기본적으로 VPN 게이트웨이 최종-에 지 보안을 제공 하는 IKEv2 게이트웨이 역할도 터널 세션 종료 합니다. |
| 컴퓨터 인증서 인증을 지원 합니다. | IKEv2 프로토콜 유형 Always On VPN 플랫폼의 VPN 인증에 대 한 컴퓨터 또는 컴퓨터 인증서 사용이 지원 구체적으로 사용할 수 있습니다.<p><p>_**참고.**_<br>IKEv2 터널 장치에 대 한 지원 되는 유일한 프로토콜 이며 SSTP 대체에 대 한 지원 옵션이 없습니다. <p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/NativeProfile/인증/MachineMethod** |
| 보안 그룹을 사용 하 여 특정 클라이언트에 원격 액세스 기능을 제한할 수 있습니다. | Always On VPN RADIUS VPN 액세스 제어에 대 한 보안 그룹의 사용을 포함 하는 사용 하는 경우 세밀 한 인증을 지원 하도록 구성할 수 있습니다. |
| Edge 방화벽이 나 NAT 장치 뒤에서 서버에 대 한 지원 합니다. | Always On VPN 완전히 NAT 장치 또는 edge 방화벽 뒤에 있는 VPN 게이트웨이 사용을 지 원하는 IKEv2 및 SSTP와 같은 프로토콜을 사용 하는 기능을 제공 합니다.<p><p>_**참고.**_<br>사용자 터널 SSTP 및 IKEv2, 지원 및 장치 터널와 SSTP 대체에 대 한 지원 되지 않는 IKEv2를 지원 합니다. |
| 회사 네트워크에 연결 하면 인트라넷 연결을 확인할 수 있습니다. | 네트워크 인터페이스 및 네트워크 프로필에 할당 된 연결별 DNS 접미사의 평가 기반 및 신뢰할 수 있는 네트워크 검색 회사 네트워크 연결을 감지 하는 기능을 제공 합니다.<p><p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/TrustedNetworkDetection** |
| 네트워크 액세스 보호 (NAP)를 사용 하 여 규정을 준수 합니다. | Always On VPN 클라이언트는 MFA, 장치 준수 또는 둘의 조합 적용 하기 위한 Azure 조건부 액세스를 사용 하 여 통합할 수 있습니다. 조건부 액세스 정책을 준수, Azure AD 클라이언트 VPN 게이트웨이 인증을 사용할 수 있습니다 (기본적으로 60 분) 지속 시간이 짧은 IPsec 인증 인증서를 발급 합니다. 장치 준수는 장치 상태 증명 상태를 포함할 수 있는 System Center Configuration Manager/Intune 준수 정책 활용 합니다. 현재, Azure VPN 조건부 액세스 없음 형태의 시정 서비스 또는 격리 네트워크 접근 권한 값은 없지만 기존 NAP 솔루션에 가장 가까운 대체를 제공 합니다. 자세한 내용은 [VPN 및 조건부 액세스를](https://docs.microsoft.com/en-us/windows/security/identity-protection/vpn/vpn-conditional-access)참조 하세요.<p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/DeviceCompliance** |
| 정의 하는 관리 서버는 사용자 로그인 하기 전에 액세스할 수 있습니다. | 회사 네트워크의 어떤 관리 시스템을 통해 액세스할 수 있는지 제어 하는 트래픽 필터가 결합 된 VPN 프로필의 장치 터널 기능 (버전 1709-IKEv2만 사용 가능)를 사용 하 여 Always On VPN에서이 기능을 구현할 수는 장치 터널 합니다.<p><p>_**참고.**_<br>장치 터널 프로필에 대 한 트래픽 필터를 설정 하면 장치 터널 (클라이언트에 회사 네트워크)에서 인바운드 트래픽의 거부 합니다.<p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/DeviceTunnel**<br>**VPNv2/ProfileName/TrafficFilterList** |
---

## 추가 기능

이 섹션에서는 각 항목은 사용 사례 시나리오 또는 Always On VPN 기능을 향상 시켰습니다 자주 사용 되는 원격 액세스 기능-기능의 확장 나 이전 제한 제거 합니다.


| 기능 영역 | Always On VPN  |
| ---- | ---- |
| Enterprise Sku 요구 사항에 도메인에 가입 된 디바이스입니다. | 도메인에 가입 된 always On VPN 지원, 미가입 (작업 그룹), 또는 엔터프라이즈 및 BYOD 시나리오 모두 가능 하도록 Azure AD 가입 – 디바이스. Always On VPN 모든 Windows 버전에서 제공 되며 UWP VPN 플러그 인을 지원 통해 제 3 자에 사용할 수 있는 플랫폼 기능.<p><p>_**참고.**_<br>장치 터널 1709 이상 Windows 10 Enterprise 또는 Education 버전을 실행 하는 도메인에 가입 된 디바이스에만 구성할 수 있습니다. 장치 터널의 타사 컨트롤에 대 한 지원 되지 않습니다. |
| IPv4 및 IPv6 모두 지원 합니다. | VPN에 항상 사용자가 IPv4 및 IPv6 리소스 회사 네트워크에 액세스할 수 있습니다. Always On VPN 클라이언트는 특히 NAT64 또는 DNS64 번역 서비스를 제공 하기 위해 IPv6 또는 VPN 게이트웨이 필요에 따라 달라 지지 않습니다 하는 이중 스택 방법을 사용 합니다. |
| 2 단계 또는 OTP 인증을 지원 합니다. |Always On VPN 플랫폼에는 기본적으로 EAP 인증 워크플로의 일부로 다양 한 Microsoft 및 제 3 자 EAP 형식을 사용할 수 있도록 지원 합니다. 특히 always On VPN 스마트 카드 (실제 및 가상) 및 Windows Hello 비즈니스 인증서에 대 한 2 단계 인증 요구 사항을 충족 하기를 지원 합니다. 또한 Always On VPN EAP RADIUS 통합을 통해 MFA (지원 되지 않음 기본적으로, 타사 플러그 인에서 지원만)를 통해 OTP를 지원 합니다.<p><p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/NativeProfile/인증** |
| 여러 도메인 및 포리스트 지원 합니다. | Always On VPN 플랫폼 VPN 클라이언트를 함수에 가입 된 도메인에 필요 없기 때문에 Active Directory 도메인 서비스 (AD DS) 포리스트 또는 도메인 토폴로지 (또는 연결 된 기능/스키마 수준)에 없는 종속성을 갖습니다. 그룹 정책 것 이므로 클라이언트 구성 하는 동안 사용 되지 않는 때문에 VPN 프로필 설정을 정의 하는 종속성 되지 않습니다. Active Directory 인증 통합이 필요한 경우 EAP 인증 및 권한 부여 과정의 일환으로 RADIUS 통해 얻을 수 있습니다. |
| 두 분할 지원 하 고 강제 터널에 대 한 인터넷/인트라넷 트래픽 분리 합니다. | Always On VPN 기본적으로 분할 터널 및 강제 터널 (기본 운영 모드) 모두를 지 원하는 데 구성할 수 있습니다. Always On VPN 응용 프로그램별 라우팅 정책에 대 한 추가 세분성을 제공합니다.<p><p>_**참고.**_<br>사용자 터널만 지원합니다.<p><p>사용 하 여 정의 합니다.<p> **VPNv2/ProfileName/NativeProfile/RoutingPolicyType**<br>**VPNv2/ProfileName/TrafficFilterList/응용 프로그램/RoutingPolicyType** |
| 여러 프로토콜 지원 합니다. | Always On VPN Secure Sockets Layer를 IKEv2에서 대체 해야 하는 경우 기본적으로 SSTP 지원 하도록 구성할 수 있습니다.<p><p>_**참고.**_<br>사용자 터널 SSTP 및 IKEv2, 지원 및 장치 터널와 SSTP 대체에 대 한 지원 되지 않는 IKEv2를 지원 합니다.  |
| 회사 연결 상태를 제공 하기 위해 도우미를 연결 합니다. | Always On VPN는 기본 네트워크 연결 관리자와 완전히 통합 하 고 보기 모든 네트워크 인터페이스에서 연결 상태를 제공 합니다. Windows 10 크리에이터 스 업데이트 (버전 1703)의 출시로 인해, VPN 연결 상태 및 사용자 터널에 대 한 VPN 연결 제어를 사용 하 여 사용할 수 있습니다 (Windows 기본 제공 VPN 클라이언트)에 대해 네트워크 플라이 아웃을 통해도. |
| 짧은 이름, 정규화 된 도메인 이름 (FQDN) 및 DNS 접미사를 사용 하 여 회사 리소스의 이름 확인 합니다. | 기본적으로 always On VPN VPN 연결 및 짧은 이름, Fqdn, 또는 전체 DNS 네임 스페이스에 대 한 이름 확인 회사 리소스를 포함 하 여 IP 주소 할당 프로세스의 일환으로 하나 이상의 DNS 접미사를 정의할 수 있습니다. 또한 always On VPN 이름 확인 정책 테이블 네임 스페이스에 특정 해상도 세분성을 제공 하기 위해 사용을 지원 합니다.<p><p>_**참고.**_<br>이름 확인 정책 테이블을 사용 하는 경우에 shortname 해상도 방해가으로 전역 접미사를 사용 하지 마세요.<p><p>사용 하 여 정의 합니다.<br>**VPNv2/ProfileName/DnsSuffix**<br>**VPNv2/ProfileName/DomainNameInformationList** |
---



## 다음 단계

- [Always On VPN 향상 된 기능에 자세히 알아보기](always-on-vpn/always-on-vpn-enhancements.md)

- [고급 Always On VPN 기능 중 일부에 대해 알아보기](always-on-vpn/deploy/always-on-vpn-adv-options.md)

- [Always On VPN 기술에 자세히 알아보기](always-on-vpn/always-on-vpn-technology-overview.md)

- [Always On VPN 배포 계획](always-on-vpn/deploy/always-on-vpn-deploy-deployment.md)

---
