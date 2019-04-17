---
title: Always On VPN 기능 향상
description: Always On VPN은 과거의 Windows VPN 솔루션 보다 장점이 많습니다. 주요 개선 사항 통합, 보안, 연결, 네트워킹 컨트롤 및 호환성에서 Microsoft의 클라우드 중심, 모바일 중심 비전을 사용 하 여 Always On VPN을 맞춥니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d7844d93ac898316580123c82e08bb6f02d51a2b
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067338"
---
# Always On VPN 기능 향상

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

& #171; [ **이전:** Always On VPN 기능에 알아보기](../vpn-map-da.md)<br>
& #187; [ **다음:** Always On VPN 기술에 알아보기](always-on-vpn-technology-overview.md)

Always On VPN은 과거의 Windows VPN 솔루션 보다 장점이 많습니다. Always On VPN Microsoft의 클라우드 중심, 모바일 중심 비전을 사용 하 여 정렬 하는 다음 주요 개선 사항:

- **플랫폼 통합:** Always On VPN 향상된 된 Windows 운영 체제와 많은 고급 연결 시나리오에 대 한 강력한 플랫폼을 제공 하기 위해 타사 솔루션 통합을 했습니다.

- **보안:** Always On VPN에 VPN 연결을 사용할 수는 응용 프로그램, 트래픽 유형을 제한 하는 새, 고급 보안 기능 및 연결을 시작 하는 데 사용할 수 있는 인증 방법입니다. 연결 대부분의 경우 활성화 되 면에 연결을 보호 하는 것이 중요 합니다. 자세한 내용은 [VPN 인증 옵션](https://docs.microsoft.com/en-us/windows/security/identity-protection/vpn/vpn-authentication)을 참조 하세요.

- **VPN 연결:** VPN에 항상에 관계 없이 장치 터널 자동 트리거 기능도 제공합니다. VPN에 항상 하기 전에 사용자 또는 장치 인증을 통해 자동 연결을 실행 하는 기능 수 없습니다.  

- **네트워킹 제어:** Always On VPN 라우팅 정책 보다 세부적인 수준에서 지정 하는 관리자를 통해-개별 응용 프로그램 나타날 때까지 아래로-특별 한 원격 액세스 해야 하는 비즈니스 라인 (lob 기간 업무) 앱에 대 한 완벽 한입니다.  Always On VPN을 모두 인터넷 프로토콜 버전 4 (IPv4)과 완전히 호환 이기도 및 IPv6 (버전 6). DirectAccess, 달리 i p v 6에 특정 의존 하지 않습니다.

  >[!Note]
  >시작 하기 전에 VPN 서버에서 i p v 6를 사용 하도록 설정 해야 합니다. 그렇지 않으면 연결을 설정할 수 및 오류 메시지가 표시 됩니다.
  
- **구성 및 호환성:** Always On VPN 배포 하 고 Always On VPN에 다른 VPN 클라이언트 소프트웨어를 통해 여러 가지 이점을 제공 하는 여러 가지 방법으로 관리할 수 있습니다.

## 플랫폼 통합

Microsoft 도입 되었거나 Always On VPN에서 다음과 같은 통합 기능을 개선 합니다.

| 주요 개선 | 설명 |
| ---- | ---- |
| **[WIP(Windows Information Protection)](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip)** | WIP와 통합 트래픽이 VPN을 통과 하도록 허용 되는지 여부를 확인 하려면 네트워크 정책 적용을 수 있습니다. 사용자 프로필이 활성화 된 경우 WIP 정책이 적용 된 Always On VPN 연결을 자동으로 트리거됩니다. 또한 WIP를 사용 하면 필요는 없습니다 (원하지 않는 경우 고급 구성) VPN 프로필에서 AppTriggerList 및 TrafficFilterList 규칙을 지정할에 적용 되기 때문에 WIP 정책 및 응용 프로그램 목록을 자동으로 합니다. |
| **[비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-overview)** | Always On VPN 기본적으로 지원 Windows Hello for Business (인증서 기반 인증 모드)에서 환경을 제공 하기 위해 원활한 단일 로그온 컴퓨터에 모두 로그인 및 VPN에 연결 합니다. 따라서 비즈니스용 Windows Hello와 함께 항상 연결 사용 가능 VPN 연결에 대 한 보조 인증 없음 (사용자 자격 증명) 필요 합니다. |
| **[Microsoft Azure 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls)** | Always On VPN 클라이언트가 Azure 조건부 액세스 플랫폼 multi-factor authentication (MFA), 장치 준수 또는 둘의 조합을 적용을 통합할 수 있습니다. 조건부 액세스 정책을 준수, Azure Active Directory (Azure AD) VPN 게이트웨이를 인증 하는 사용할 수 있는 일시적인 (기본적으로 60 분) (IPsec) IP 보안 인증 인증서를 발급 합니다. 장치 준수 연결 준수 검사의 일부로 장치 상태 증명 상태를 포함할 수 있는 System Center Configuration Manager/Intune 준수 정책을 사용 합니다. |
| **Azure MFA** | Azure MFA에 대 한 원격 인증 전화-사용자 서비스 (RADIUS) 서비스 및 네트워크 정책 서버 (NPS) 확장 조합 되 면 VPN 인증 강력한 MFA를 사용할 수 있습니다. |
| **타사 VPN 플러그 인** | 사용 하 여 유니버설 Windows 플랫폼 (UWP), 타사 VPN 공급자 만들 수 Windows의 전체 범위에 대 한 단일 응용 프로그램 10 대의 디바이스. UWP 제공 커널 수준 드라이버 쓰기 관련 문제와 복잡성을 제거 장치 간에 보장 된 핵심 API 계층을 합니다. [Pulse Secure](https://www.microsoft.com/p/pulse-secure/9nblggh3b0bp), [F5 Access](https://www.microsoft.com/p/f5-access/9wzdncrdsfn0), [검사점 캡슐 VPN 확인](https://www.microsoft.com/p/check-point-capsule-vpn/9wzdncrdjxtj), [FortiClient](https://www.microsoft.com/p/forticlient/9wzdncrdh6mc), [SonicWall 모바일 연결](https://www.microsoft.com/p/sonicwall-mobile-connect/9wzdncrdsfkz)하 고 [GlobalProtect](https://www.microsoft.com/p/globalprotect/9nblggh6bzl3);에 대 한 Windows 10 UWP VPN 플러그 인 존재 하는 현재 흔히 다른 나타납니다 나중에 있습니다. |
---

## 보안

기본 보안 향상 다음 영역에 있습니다.

| 주요 개선 | 설명 |
| ---- | ---- |
| **트래픽 필터** | 트래픽 필터를 통해 회사 네트워크에 있는 트래픽이 허용 되었는지 여부를 결정 하는 클라이언트 쪽 정책 지정할 수 있습니다. 이렇게 하면에서 관리자 앱 또는 트래픽을에 제한을 적용할 수 VPN 인터페이스 IP 주소, 특정 원본 및 대상 포트 하는 사용을 제한 합니다. 두 가지 유형의 필터링 규칙을 사용할 수 있습니다.<ul><li>**앱 기반 규칙.** 앱 기반 방화벽 규칙은 이러한 앱에서 발생 하는 트래픽만 VPN 인터페이스 수 있도록 지정 된 응용 프로그램 목록에 기반 합니다.</li><li>**트래픽 기반 규칙.** 트래픽 기반 방화벽 규칙은 포트, 주소, 프로토콜 등 네트워크 요구 사항에 기반 합니다. 사용이 특정 조건에 맞는 트래픽에 대해서만 이러한 규칙 VPN 인터페이스 허용 됩니다.<p><p>_**참고.**_<br>장치에서 이러한 규칙 아웃 바운드 트래픽을에 적용 됩니다. 사용 하 여 트래픽 인바운드 트래픽을 차단 회사 네트워크에서 클라이언트를 필터링합니다. </li></ul> |
| **앱 별 VPN** | 앱 별 VPN는 앱 기반 트래픽 필터를 사용 하는 것과 유사 하지만 VPN 연결 VPN 클라이언트에서 모든 응용 프로그램 아니라 특정 응용 프로그램으로 제한 되는 앱 기반 트래픽 필터를 사용 하 여 응용 프로그램 트리거를 결합 하 여 멀리 이동 합니다. 기능을 앱이 시작 될 때 자동으로 시작 합니다. |
| **사용자 지정 된 IPsec 암호화 알고리즘에 대 한 지원** | Always On VPN 엄격한 정부 또는 조직의 보안 정책을 충족 하는 RSA과 타원 곡선 암호화 기반 암호화 알고리즘 사용자 지정 모두 지원 합니다. |
| **기본적으로 확장할 수 있는 인증 프로토콜 (EAP) 지원** | Always On VPN을 EAP 인증 워크플로의 일부로 다양 한 Microsoft 및 제 3 자 EAP 형식을 사용 하는 기본적으로 지원 합니다. EAP 다음 인증 형식에 따라 보안 인증을 제공 합니다.<ul><li>사용자 이름 및 암호</li><li>스마트 카드 (실제 및 가상)</li><li>사용자 인증서</li><li>비즈니스용 Windows Hello</li><li>EAP RADIUS 통합을 통해 MFA 지원</li></ul>응용 프로그램 공급 업체의 사용 가능한 옵션을 사용자 지정 자격 증명 유형 및 OTP 지원을 비롯 한 배열 있지만 제 3 자 UWP VPN 플러그 인 인증 방법을 제어 합니다. |
---

## VPN 연결

다음은 Always On VPN 연결의 주요 개선 사항입니다.

| 주요 개선 | 설명 |
| ---- | ---- |
| **항상 사용** | Always On은 활성 VPN 프로필이 자동으로 연결 하 고 계속 연결 되어 트리거가에 따라 하는 Windows 10 기능-즉, 사용자 로그인, 네트워크 상태 변경 또는 장치 화면을 활성화 합니다. Always On은 또한 통합 배터리 사용 시간을 최대화 하기 위해 연결 된 대기 상태 경험 합니다. |
| **응용 프로그램 트리거** | 지정된 된 응용 프로그램 집합의 실행 시 자동으로 연결 하려면 Windows 10에서 VPN 프로필을 구성할 수 있습니다. 데스크톱과 UWP 응용 프로그램 VPN 연결을 트리거하도록을 구성할 수 있습니다. |
| **이름 기반 트리거** | Always On VPN을 사용 하 여 특정 도메인 이름 쿼리에 VPN 연결을 트리거하도록 수 있도록 규칙을 정의할 수 있습니다. Windows 10 도메인 가입 및 도메인에 가입 된 컴퓨터에 대 한 트리거 이름 기반 지원 (이전에 컴퓨터만 미가입 된 지원 됨). |
| **신뢰할 수 있는 네트워크 검색** | Always On VPN 사용자 회사 경계 내에서 신뢰할 수 있는 네트워크에 연결 된 경우 VPN 연결 트리거되지 않습니다 수 있도록이 기능을 포함 합니다. 원활한 "필요할 때에 연결" 사용자 환경을 제공 하려면 앞에서 언급 한 트리거 방법 중 하나를 사용 하 여이 기능을 결합할 수 있습니다. |
| **[장치 터널](../vpn-device-tunnel-config.md)** | Always On VPN을 디바이스 또는 컴퓨터에 대 한 전용된 VPN 프로필을 만들 수가 있습니다. 달리 _사용자 터널_을 연결 하는 사용자가 디바이스 또는 컴퓨터에 로그온 한 후, _장치 터널_ VPN을 사용자 로그인 하기 전에 연결을 설정할 수 있습니다. 장치 터널와 사용자 터널 자신의 VPN 프로필을 사용 하 여 독립적으로 작동 이와 동시에 연결할 수 및 다른 인증 방법 및 다른 VPN 구성 설정을 적절 하 게 사용할 수 있습니다. |
---

## 네트워킹

다음은 항상 VPN에서 향상 된 네트워킹 기능입니다.

| 주요 개선 | 설명 |
| ---- | ---- |
| **IPv4 및 IPv6 이중 스택 지원** | Always On VPN 이중 스택 방식으로 IPv4 및 IPv6 사용이 기본적으로 지원 합니다. 에 특정 종속성 없이 하나의 프로토콜을 우선적 최대 IPv4/IPv6 응용 프로그램 호환성 네트워킹 요구 향후 IPv6 지원을 결합할 수 있습니다.<p>**_참고._** 시작 하기 전에 VPN 서버에서 i p v 6를 사용 하도록 설정 해야 합니다. 그렇지 않으면 연결을 설정할 수 및 오류 메시지가 표시 됩니다.|
| **응용 프로그램별 라우팅 정책** | 인터넷 및 인트라넷 트래픽 분리에 대 한 전역 VPN 연결 라우팅 정책을 정의 하는 것 외에도 것을 분할 터널의 사용을 제어 하거나 강제 터널 구성 응용 프로그램별 별로 라우팅 정책을 추가할 수 있습니다. 이 옵션은 앱은 VPN 터널을 통해 어떤 리소스와 상호 작용 하도록 허용 하는 보다 세부적으로 제어를 제공 합니다. |
| **제외 경로** | Always On VPN 특별히 트래픽이 해야만 VPN을 통과 하 고 실제 네트워크 인터페이스를 통과 하지 정의 하는 라우팅 동작을 제어 하는 제외 경로 지정 하는 기능을 지원 합니다.<p><p>_**참고 사항입니다.**_<br>-제외 경로 현재 작동 하므로 클라이언트와 동일한 서브넷 내 트래픽에 대 한 예를 들어 LinkLocal.<br>-분할 터널 설치에서 제외 경로 에서만 작동합니다. |
---

## 구성 및 호환성 

다음은 일부 Always On VPN 구성 및 호환성 향상입니다.

| 주요 개선 | 설명 |
| ---- | ---- |
| **타사 VPN 게이트웨이 호환성** | Always On VPN 클라이언트는 Microsoft 기반 VPN 게이트웨이 작동 하는 데 사용 하지 않아도 됩니다. IKEv2 프로토콜을 지원 하 여 클라이언트는이 산업 표준 터널링 형식을 지 원하는 타사 VPN 게이트웨이와 상호 운용성을 이용 합니다. Always On VPN 플랫폼 기능 및 혜택을 유지 하면서 사용자 지정 터널링 형식와 함께 UWP VPN 플러그 인을 사용 하 여 타사 VPN 게이트웨이와 상호 운용성을 얻을 수도 있습니다.<p><p>_**참고.**_<br>Always On VPN 및 IKEv2를 사용 하 여 장치 터널와의 호환성 구성을 켜고 게이트웨이 또는 제 3 자 백 엔드 기기 공급 업체에 문의 하십시오. |
| **산업 표준 IKEv2 VPN 프로토콜 지원** | 가장 널리 사용 되는 오늘날의 중 하나 산업 표준 터널링 프로토콜을 항상 VPN 클라이언트 IKEv2를 지원 합니다. 이 호환성 타사 VPN 게이트웨이와 상호 운용성이 극대화 됩니다. |
| **지원 되는 플랫폼** | 도메인에 가입 된 AAlways에서 VPN 지원, 미가입 (작업 그룹), 또는를 모두 엔터프라이즈에 대 한 허용 하 고 고유한 디바이스 (BYOD) 시나리오를 위해 Azure AD 가입 – 디바이스. 또한 Always On VPN은 모든 Windows 버전에서 사용할 수 있습니다. |
| **다양 한 관리 및 배포 메커니즘입니다.** | 많은 관리 및 배포 메커니즘을 사용 하 여 Windows PowerShell, System Center Configuration Manager, Intune (또는 제 3 자 모바일 장치 관리 [MDM] 도구)를 비롯 하 여 ( _VPN 프로필_이라고 함) VPN 설정을 관리 하 고 Windows 구성 디자이너 합니다. 이러한 옵션을 사용 하면 클라이언트 관리 도구에 관계 없이 항상 VPN의 구성을 간소화 합니다. |
| **표준화 된 VPN 프로필 정의** | Always On VPN 대부분의 관리 및 배포 도구를 사용 하는 표준 구성을 서식 제공 하는 표준 XML 프로필 (ProfileXML)를 사용 하 여 구성을 지원 합니다. |
---


## 다음 단계

- [고급 Always On VPN 기능 중 일부에 대해 알아보기](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 기술에 자세히 알아보기](always-on-vpn-technology-overview.md)

- [Always On VPN 배포 계획](deploy/always-on-vpn-deploy-deployment.md)



---
