---
title: Always On VPN 기능 향상
description: Always On VPN 과거의 Windows VPN 솔루션을 통해 많은 장점이 있습니다. Microsoft의 클라우드 우선, 모바일 우선 비전을 사용 하 여 Always On VPN를 정렬 하는 통합 "," 보안 "," 연결 "," 네트워킹 제어 "및" 호환성의 주요 향상 기능입니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0b4dd78e0e88678d4570d408b3dcd472bddc88ba
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749671"
---
# <a name="always-on-vpn-enhancements"></a>Always On VPN 기능 향상

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

- [**이전:** Always On VPN 기능에 대해 알아보기](../vpn-map-da.md)
- [**다음:** Always On VPN 기술을 배우고합니다](always-on-vpn-technology-overview.md)

Always On VPN 과거의 Windows VPN 솔루션을 통해 많은 장점이 있습니다. Microsoft의 클라우드 우선, 모바일 우선 비전을 사용 하 여 Always On VPN를 정렬 하는 다음과 같은 주요 향상 기능:

- **플랫폼 통합:** Always On VPN에 향상 된 통합 Windows 운영 체제와 타사 솔루션 수많은 고급 연결 시나리오에 대해 강력한 플랫폼을 제공할 수 있습니다.

- **보안:** Always On VPN에서 새로운 고급 보안 기능이 있는 응용 프로그램 VPN 연결을 사용할 수, 트래픽 유형을 제한할는 인증 방법 수를 사용 하 여 연결을 시작 합니다. 연결이 활성 상태인 대부분의 경우에 연결을 보호 하는 것이 특히 유용 합니다. 자세한 내용은 참조 하세요. [VPN 인증 옵션](https://docs.microsoft.com/en-us/windows/security/identity-protection/vpn/vpn-authentication)합니다.

- **VPN 연결:** Always On VPN, 장치 터널 없이 자동 트리거 기능도 제공합니다. Always On VPN을 하기 전에 사용자 또는 장치 인증을 통해 자동 연결을 실행 하는 기능 수 없었습니다.  

- **네트워킹 제어 가능:** Always On VPN 관리자가 더 세부적인 수준에서 라우팅 정책을 지정할 수 있습니다-개별 응용 프로그램에 이르는-는 특별 한 원격 액세스를 필요로 하는 업무-(lob 기간 업무) 앱에 적합 합니다.  Always On VPN 인터넷 프로토콜 버전 4(ipv4)와 완전히 호환 이기도 및 버전 6(ipv6) 합니다. DirectAccess와 달리 IPv6에 특정 종속 되지 않습니다.

  >[!NOTE]
  >시작 하기 전에 VPN 서버에서 IPv6을 사용 하도록 설정 해야 합니다. 그렇지 않으면 연결을 설정할 수 없습니다 하 고 오류 메시지가 표시 됩니다.

- **구성과 호환성:** Always On VPN 배포 및 Always On VPN 다른 VPN 클라이언트 소프트웨어를 통해 여러 가지 이점을 제공 하는 여러 가지 방법으로 관리할 수 있습니다.

## <a name="platform-integration"></a>플랫폼 통합

Microsoft는 도입 했거나 Always On VPN의 다음 통합 기능 향상:


| 핵심 개선 사항   |  설명  |
|----------------|---|
| **[Windows Information Protection (WIP)](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip)** | WIP 사용 하 여 통합 네트워크 정책 적용을 트래픽이 VPN을 통해 이동할 허용 되는지 여부를 결정할 수 있습니다. 사용자 프로필 활성 상태 이며 WIP 정책을 적용 하는 경우 Always On VPN 연결을 자동으로 트리거됩니다. 또한 WIP를 사용 하는 경우 있습니다 이므로 (하지 않으려는 경우 고급 구성) VPN 프로필에 AppTriggerList 및 trafficfilterlist의 규칙을 개별적으로 지정할 필요가 없습니다 자동으로 적용 WIP 정책 및 응용 프로그램 목록입니다. |
|**[비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-overview)** |Always On VPN 고유 하 게 지원 Windows Hello for Business (인증서 기반 인증 모드)에서 컴퓨터에 모두 로그인 및 VPN 연결에 대 한는 원활한 single sign-on 환경을 제공 합니다. 따라서 보조 인증 (사용자 자격 증명) 없이 비즈니스 인증용 Windows Hello와 Always On 연결을 사용할 수 있도록 하 여 VPN 연결에 필요 합니다. |
| **[Microsoft Azure 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls)**  |Always On VPN 클라이언트는 multi-factor authentication (MFA), 장치 규정 준수 또는 둘의 조합을 적용할 Azure 조건부 액세스 플랫폼을 통합할 수 있습니다. 조건부 액세스 정책과 함께 준수 하는 경우 Azure Active Directory (Azure AD) VPN gateway에 대 한 인증에 사용할 수 있습니다 (기본적으로 60 분) 수명이 짧은 IPsec (IP 보안) 인증 인증서를 발급 합니다. 장치 규정 준수 연결 규정 준수 검사의 일부로 장치 상태 증명 상태를 포함할 수 있는 System Center Configuration Manager/Intune 준수 정책을 사용 합니다.|
|  **Azure MFA** |Azure MFA에 대 한 전화 접속 사용자 서비스 RADIUS (Remote Authentication) 서비스 및 네트워크 정책 (NPS 서버) 확장 함께 사용 하면 강력한 MFA VPN 인증에 사용할 수 있습니다. | **타사 VPN 플러그 인**  | 사용 하 여 Windows 플랫폼 (UWP (유니버설), 타사 VPN 공급자 만들면 전체 범위의 Windows에 대 한 단일 응용 프로그램을 10 개의 장치 됩니다. UWP 계층을 제공 보장된 core API, 장치에 걸쳐의 복잡성 및 커널 수준 드라이버 작성에 자주 연결 하는 문제를 제거 합니다. Windows 10 UWP VPN 플러그 인에 대해 존재 하는 현재 [Pulse Secure](https://www.microsoft.com/p/pulse-secure/9nblggh3b0bp)를 [F5 액세스](https://www.microsoft.com/p/f5-access/9wzdncrdsfn0)를 [검사점 캡슐 VPN](https://www.microsoft.com/p/check-point-capsule-vpn/9wzdncrdjxtj)를 [FortiClient](https://www.microsoft.com/p/forticlient/9wzdncrdh6mc), [ SonicWall Mobile Connect](https://www.microsoft.com/p/sonicwall-mobile-connect/9wzdncrdsfkz), 및 [GlobalProtect](https://www.microsoft.com/p/globalprotect/9nblggh6bzl3); 틀림 없이 다른 나타납니다 나중에 있습니다. |

## <a name="security"></a>보안

보안의 향상 된 주요 기능 영역은 다음과 같습니다.

| 핵심 개선 사항 | 설명  |
|---|---|
| **트래픽 필터** | 트래픽 필터를 통해 회사 네트워크에 허용 된 트래픽을 결정 하는 클라이언트 쪽 정책을 지정할 수 있습니다. 따라서에서 관리자 적용할 수 있습니다 앱 및 트래픽 제한을 VPN 인터페이스에 특정 원본, 대상 포트 및 IP 주소에 해당 사용을 제한 합니다. 사용 가능한 두 가지 유형의 필터링 규칙 같습니다.<ul><li>**앱 기반 규칙입니다.** 앱 기반 방화벽 규칙은 이러한 앱에서 생성 된 트래픽 에서만 VPN 인터페이스를 통해 이동할 수 있도록 지정 된 응용 프로그램 목록을 기반 합니다.</li><li>**트래픽 기반 규칙입니다.** 트래픽 기반 방화벽 규칙이 포트, 주소 및 프로토콜 등의 네트워크 요구 사항을 기반으로 합니다. 이러한 특정 조건과 일치 하는 트래픽에 대해서만 이러한 규칙은 VPN 인터페이스를 통해 이동 수를 사용 합니다.<p><p>***참고:***<br>이러한 규칙은 장치에서 아웃 바운드 트래픽의 에게만 적용 됩니다. 사용 하 여 트래픽의 인바운드 트래픽을 차단 회사 네트워크에서 클라이언트를 필터링합니다. </li></ul> |**앱 별 VPN**|앱 별 VPN 앱 기반 트래픽 필터를 사용 하는 것과 같습니다 되지만 시간을 미래의 시간 VPN 클라이언트의 모든 응용 프로그램 대신 특정 응용 프로그램에 VPN 연결 제한 됩니다 있도록 앱 기반 트래픽 필터를 사용 하 여 응용 프로그램을 결합 합니다. 기능 앱 시작 시에 자동으로 시작 합니다.|
|  **사용자 지정된 IPsec 암호화 알고리즘에 대 한 지원**   |  Always On VPN 엄격한 정부 또는 조직의 보안 정책을 충족 하기 위해 RSA와 elliptic curve cryptography 기반 사용자 지정 암호화 알고리즘의 사용을 지원 합니다.|
| **네이티브 Extensible Authentication Protocol (EAP) 지원** |Always On VPN 인증 워크플로의 일부로 다양 한 Microsoft 및 타사 EAP 종류를 사용할 수 있는 EAP를 고유 하 게 지원 합니다. EAP는 다음 인증 유형을 기반으로 하는 보안 인증을 제공 합니다.<ul><li>사용자 이름 및 암호</li><li>스마트 카드 (실제 및 가상)</li><li>사용자 인증서</li><li>비즈니스용 Windows Hello</li><li>EAP RADIUS 통합을 통해 MFA 지 원하</li></ul>응용 프로그램 공급 업체 사용할 수 있는 옵션을 사용자 지정 자격 증명 형식 및 OTP 지원을 포함 하 여 배열을 없지만 타사 UWP VPN 플러그 인 인증 방법을 제어 합니다.|

## <a name="vpn-connectivity"></a>VPN 연결

다음은 Always On VPN 연결의 향상 된 기본 기능입니다.

|  핵심 개선 사항  | 설명 |
|---|---|
|                    **Always On**                    |                                                                                          Always On은 자동으로 연결 하 여 트리거를 기반으로 연결 되어 현재 VPN 프로필을 사용 하도록 설정 하는 Windows 10 기능-즉, 사용자 로그인, 네트워크 상태 변경 또는 장치 화면을 활성화 합니다. Always On에 통합 되어 배터리 수명을 최대화 하기 위해 연결 된 대기 환경입니다.                                                                                           |
|             **응용 프로그램 트리거**              |                                                                                                                                          지정된 된 집합이 응용 프로그램의 시작 시 자동으로 연결 하려면 Windows 10에서 VPN 프로필을 구성할 수 있습니다. 데스크톱과 UWP 응용 프로그램 트리거 VPN 연결을 구성할 수 있습니다.                                                                                                                                          |
|              **트리거 이름 기반**              |                                                                                                            Always On VPN을 사용 하 여 특정 도메인 이름 쿼리 VPN 연결을 트리거하지 않도록 규칙을 정의할 수 있습니다. Windows 10 도메인 가입 및 비도메인 가입 컴퓨터에 대 한 트리거 이름 기반 이제 지원 (이전에 비도메인 가입 컴퓨터는 지원 된).                                                                                                            |
|            **신뢰할 수 있는 네트워크 검색**            |                                                                                    Always On VPN이이 기능을 사용자가 회사 경계 내에서 신뢰할 수 있는 네트워크에 연결 된 경우 VPN 연결 트리거되지가 포함 됩니다. "필요한 경우에 연결" 원활한 사용자 환경을 제공 하기 위해 앞에서 언급 한 트리거 방법 중 하나를 사용 하 여이 기능을 결합할 수 있습니다.                                                                                     |
| **[터널 장치](../vpn-device-tunnel-config.md)** | Always On VPN 장치 또는 컴퓨터에 대 한 전용된 VPN 프로필을 만들 수가 있습니다. 와 달리 *사용자 터널*에 연결 하는 사용자가 장치 또는 컴퓨터에 로그온 한 후 *장치 터널* VPN 사용자 로그인 하기 전에 연결을 설정할 수 있습니다. 터널 장치 및 사용자 터널의 VPN 프로필을 사용 하 여 독립적으로 작동할 동시에 연결할 수 있습니다 및 다른 인증 방법 및 다른 VPN 구성 설정을 적절 하 게 사용할 수입니다. |

## <a name="networking"></a>네트워킹

다음은 일부 Always On VPN의 향상 된 네트워킹 기능입니다.


|              핵심 개선 사항              |                                                                                                                                                                                                                설명                                                                                                                                                                                                                |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **IPv4 및 IPv6에 대 한 이중 스택 지원**  | Always On VPN는 기본적으로 이중 스택 접근 방식에서는 IPv4 및 IPv6 모두 사용을 지원합니다. 특정 종속성을 하나 프로토콜를 향후 IPv6 네트워킹 요구 사항 지원 함께 최대 IPv4/i p v 6 응용 프로그램 호환성에 대 한 허용 하는 합니다.<p>***참고:*** 시작 하기 전에 VPN 서버에서 IPv6을 사용 하도록 설정 해야 합니다. 그렇지 않으면 연결을 설정할 수 없습니다 하 고 오류 메시지가 표시 됩니다. |
| **응용 프로그램별 라우팅 정책** |                            인터넷 및 인트라넷 트래픽 분리에 대 한 전역 VPN 연결 라우팅 정책을 정의 하는 것 외에도 분할 터널의 사용을 제어 하거나 응용 프로그램 별로 터널 구성은 강제로 적용 하는 라우팅 정책을 추가 하는 것이 같습니다. 이 옵션은 보다 세부적인 제어는 앱 VPN 터널을 통해 리소스를 조작할 수를 제공 합니다.                             |
|           **제외 경로**            |                 Always On VPN 구체적으로 트래픽을 VPN만을 통과 하 고 실제 네트워크 인터페이스를 통해 이동 하지를 정의 하려면 라우팅 동작을 제어 하는 제외 경로 지정 하는 기능을 지원 합니다.<p><p>***참고:***<br>-제외 경로 현재 작동 클라이언트와 동일한 서브넷 내의 트래픽에 대 한 예를 들어 LinkLocal 합니다.<br>-제외 경로 분할 터널 설정에만 작동합니다.                  |

## <a name="configuration-and-compatibility"></a>구성 및 호환성 

다음은 일부 Always On VPN의 구성 및 호환성 개선 사항입니다.


|                 핵심 개선 사항                  |                                                                                                                                                                                                                                                                                                                       설명                                                                                                                                                                                                                                                                                                                       |
|--------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    **타사 VPN 게이트웨이 호환성**     | Always On VPN 클라이언트는 작동 하는 Microsoft 기반 VPN gateway 사용 하지 않아도 됩니다. 클라이언트는 IKEv2 프로토콜의 지원을 통해이 업계 표준 터널링 유형을 지 원하는 타사 VPN gateway와의 상호 운용성을 지원 합니다. 또한 Always On VPN 플랫폼 기능 및 혜택을 희생 하지 않고 사용자 지정 터널링 형식과 결합 UWP VPN 플러그 인을 사용 하 여 타사 VPN gateway와의 상호 운용성을 높일 수 있습니다.<p><p>***참고:***<br>게이트웨이 또는 제 3 자 백 엔드 어플라이언스 공급 업체 구성 및 Always On VPN 및 IKEv2를 사용 하 여 장치의 터널을 사용 하 여 호환성에 게 문의 하십시오. |
| **업계 표준 IKEv2 VPN 프로토콜 지원** |                                                                                                                                                                                                                              가장 널리 사용 되는 오늘 중 터널링의 업계 표준 프로토콜, Always On VPN 클라이언트는 IKEv2를 지원 합니다. 이 호환성 뿐만 아니라 타사 VPN gateway와의 상호 운용성을 최대화합니다.                                                                                                                                                                                                                               |
|               **플랫폼 지원**               |                                                                                                                                                                                                           도메인에 가입 된 AAlways On VPN 지원, 비도메인 가입 (작업 그룹) 또는 두 엔터프라이즈용 허용 bring 고유한 장치 (BYOD) 시나리오를 Azure AD-가입 된 장치입니다. 또한 Always On VPN은 모든 Windows 버전에서 사용할 수 있습니다.                                                                                                                                                                                                           |
| **다양 한 관리 및 배포 메커니즘입니다.** |                                                                                                                                 VPN 설정을 관리 하려면 다양 한 관리 및 배포 메커니즘을 사용할 수 있습니다 (호출을 *VPN 프로필*), Windows PowerShell, System Center Configuration Manager, Intune 또는 타사 모바일 장치 관리 (MDM) 도구를 비롯 하 여 및 Windows 구성 디자이너입니다. 이러한 옵션에 사용할 클라이언트 관리 도구에 관계 없이 Always On VPN 구성을 간소화 합니다.                                                                                                                                 |
|     **표준화 된 VPN 프로필 정의**      |                                                                                                                                                                                                                                  Always On VPN 대부분의 관리 및 배포 도구를 사용 하는 표준 구성 템플릿 형식이 제공 하는 표준 XML 프로필 (ProfileXML)를 사용 하 여 구성을 지원 합니다.                                                                                                                                                                                                                                   |

## <a name="next-steps"></a>다음 단계

- [고급 Always On VPN 기능 중 일부에 대해 알아봅니다](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 기술에 자세히 알아보기](always-on-vpn-technology-overview.md)

- [Always On VPN 배포 계획 시작](deploy/always-on-vpn-deploy-deployment.md)