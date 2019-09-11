---
title: Always On VPN 기능 향상
description: Always On VPN은 과거의 Windows VPN 솔루션에 비해 많은 이점을 제공 합니다. 통합, 보안, 연결, 네트워킹 제어 및 호환성의 주요 개선 사항은 Microsoft의 클라우드 우선, 모바일 우선 비전을 사용 하 여 VPN Always On 맞춥니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 65bf9f732e28e5974a3880c7d07ab7262de18144
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871385"
---
# <a name="always-on-vpn-enhancements"></a>Always On VPN 기능 향상

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

- [**선행** Always On VPN 기능에 대해 알아보기](../vpn-map-da.md)
- [**그런** Always On VPN 기술에 대해 알아보기](always-on-vpn-technology-overview.md)

Always On VPN은 과거의 Windows VPN 솔루션에 비해 많은 이점을 제공 합니다. 다음과 같은 주요 향상 된 기능은 Microsoft의 클라우드 우선, 모바일 우선 비전을 사용 하 여 VPN Always On 맞춥니다.

- **플랫폼 통합:** Always On VPN은 Windows 운영 체제 및 타사 솔루션과의 통합이 향상 되어 수많은 고급 연결 시나리오를 위한 강력한 플랫폼을 제공 합니다.

- **보안** Always On VPN은 트래픽 유형, VPN 연결을 사용할 수 있는 응용 프로그램, 연결을 시작 하는 데 사용할 수 있는 인증 방법을 제한 하는 새로운 고급 보안 기능을 제공 합니다. 연결이 대부분 활성 상태인 경우 연결을 보호 하는 것이 특히 중요 합니다. 자세한 내용은 [VPN authentication options](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-authentication)를 참조 하세요.

- **VPN 연결:** 장치 터널을 사용 하거나 사용 하지 않는 Always On VPN은 자동 트리거 기능을 제공 합니다. VPN을 Always On 하기 전에 사용자 또는 장치 인증을 통해 자동 연결을 트리거할 수 없습니다.  

- **네트워킹 제어:** Always On VPN을 사용 하면 관리자는 개별 응용 프로그램에 대해서도 보다 세분화 된 수준으로 라우팅 정책을 지정할 수 있습니다 .이는 특별 한 원격 액세스가 필요한 LOB (기간 업무) 앱에 적합 합니다.  또한 Always On VPN은 IPv4 (인터넷 프로토콜 버전 4) 및 버전 6 (IPv6) 모두와 완전히 호환 됩니다. DirectAccess와 달리 IPv6에 대 한 특정 종속성은 없습니다.

  >[!NOTE]
  >시작 하기 전에 VPN 서버에서 i p v 6를 사용 하도록 설정 해야 합니다. 그렇지 않으면 연결을 설정할 수 없으며 오류 메시지가 표시 됩니다.

- **구성 및 호환성:** Always On VPN은 여러 가지 방법으로 배포 하 고 관리할 수 있습니다 .이를 통해 Always On VPN은 다른 VPN 클라이언트 소프트웨어에 비해 여러 가지 이점을 제공 합니다.

## <a name="platform-integration"></a>플랫폼 통합

Microsoft는 Always On VPN에서 다음과 같은 통합 기능을 도입 하거나 향상 시켰습니다.


| 주요 개선 사항   |  설명  |
|----------------|---|
| **[WIP (Windows Information Protection)](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip)** | WIP와 통합 하면 네트워크 정책 적용을 통해 트래픽이 VPN을 통과할 수 있는지 여부를 확인할 수 있습니다. 사용자 프로필이 활성 상태이 고 WIP 정책이 적용 된 경우 Always On VPN이 자동으로 트리거되어 연결 합니다. 또한 WIP를 사용 하는 경우에는 WIP 정책 및 응용 프로그램 목록이 자동으로 적용 되기 때문에 추가 고급 구성을 사용 하지 않는 한, 추가 고급 구성을 사용 하지 않는 한, AppTriggerList 및 Trafficfilterlist의 규칙을 VPN 프로필에 별도로 지정할 필요가 없습니다. |
|**[비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-overview)** |Always On VPN은 기본적으로 Windows Hello for Business (인증서 기반 인증 모드)를 지원 하 여 컴퓨터에 로그인 하 고 VPN에 연결 하는 데 원활한 Single Sign-On 환경을 제공 합니다. 따라서 VPN 연결에는 보조 인증 (사용자 자격 증명)이 필요 하지 않으므로 비즈니스용 Windows Hello 인증에 Always On 연결을 사용할 수 있습니다. |
| **[조건부 액세스 Microsoft Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls)**  |Always On VPN 클라이언트는 Azure 조건부 액세스 플랫폼과 통합 하 여 MFA (다단계 인증), 장치 준수 또는 둘의 조합을 적용할 수 있습니다. 조건부 액세스 정책을 준수 하는 경우 Azure Active Directory (Azure AD)에서 VPN gateway에 인증 하는 데 사용할 수 있는 단기 (기본적으로 60 분)의 IPsec (IP 보안) 인증 인증서를 발급 합니다. 장치 준수는 연결 준수 확인의 일부로 장치 상태 증명 상태를 포함할 수 있는 System Center Configuration Manager/Intune 준수 정책을 사용 합니다.|
|  **Azure MFA** |Azure MFA에 대 한 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 서비스와 NPS (네트워크 정책 서버) 확장을 결합 하면 VPN 인증에서 강력한 MFA를 사용할 수 있습니다. | **타사 VPN 플러그 인**  | UWP (유니버설 Windows 플랫폼)를 사용 하 여 타사 VPN 공급자는 전체 범위의 Windows 10 장치에 대 한 단일 응용 프로그램을 만들 수 있습니다. UWP는 장치 간에 보장 된 핵심 API 계층을 제공 하 여 커널 수준 드라이버 작성과 관련 된 복잡 한 문제 및 문제를 제거 합니다. 현재 [Pulse Secure](https://www.microsoft.com/p/pulse-secure/9nblggh3b0bp), [F5 Access](https://www.microsoft.com/p/f5-access/9wzdncrdsfn0), [Check Point 캡슐 Vpn](https://www.microsoft.com/p/check-point-capsule-vpn/9wzdncrdjxtj), [FortiClient](https://www.microsoft.com/p/forticlient/9wzdncrdh6mc), [SonicWall Mobile CONNECT](https://www.microsoft.com/p/sonicwall-mobile-connect/9wzdncrdsfkz)및 [globalprotect](https://www.microsoft.com/p/globalprotect/9nblggh6bzl3)에 대 한 Windows 10 UWP VPN 플러그 인이 있습니다. 잘 모르겠으면 나중에 다른 사람이 표시 될 것입니다. |

## <a name="security"></a>보안

보안의 주요 개선 사항은 다음 영역에 있습니다.

| 주요 개선 사항 | 설명  |
|---|---|
| **트래픽 필터** | 트래픽 필터를 통해 회사 네트워크에 허용 되는 트래픽을 결정 하는 클라이언트 쪽 정책을 지정할 수 있습니다. 이러한 방식으로 관리자는 VPN 인터페이스에 앱 또는 트래픽 제한을 적용 하 여 특정 원본, 대상 포트 및 IP 주소에 대 한 사용을 제한할 수 있습니다. 사용할 수 있는 필터링 규칙에는 다음 두 가지 유형이 있습니다.<ul><li>**앱 기반 규칙.** 앱 기반 방화벽 규칙은 지정 된 응용 프로그램 목록을 기반으로 하므로 이러한 앱에서 발생 하는 트래픽만 VPN 인터페이스를 통과할 수 있습니다.</li><li>**트래픽 기반 규칙.** 트래픽 기반 방화벽 규칙은 포트, 주소 및 프로토콜과 같은 네트워크 요구 사항을 기반으로 합니다. 이러한 특정 조건과 일치 하는 트래픽만 VPN 인터페이스를 통과할 수 있도록 이러한 규칙을 사용 합니다.<p><p>***참고:***<br>이러한 규칙은 장치에서 아웃 바운드 된 트래픽에만 적용 됩니다. 트래픽 필터를 사용 하면 회사 네트워크에서 클라이언트로 들어오는 인바운드 트래픽을 차단할 수 있습니다. </li></ul> |**앱 별 VPN**|앱 별 VPN은 응용 프로그램 기반 트래픽 필터를 사용 하는 것과 유사 하지만, vpn 연결을 VPN 클라이언트의 모든 응용 프로그램과 대조 하 여 특정 응용 프로그램으로 제한 하도록 응용 프로그램 트리거를 앱 기반 트래픽 필터와 결합 하는 것이 더 멀리 떨어져 있습니다. 이 기능은 앱이 시작 될 때 자동으로 시작 됩니다.|
|  **사용자 지정 된 IPsec 암호화 알고리즘에 대 한 지원**   |  Always On VPN은 엄격한 정부 또는 조직 보안 정책을 충족 하기 위해 RSA 및 타원 curve 암호화 기반 사용자 지정 암호화 알고리즘을 모두 사용할 수 있도록 지원 합니다.|
| **네이티브 EAP (Extensible Authentication Protocol) 지원** |Always On VPN은 인증 워크플로의 일부로 다양 한 Microsoft 및 타사 EAP 종류 집합을 사용할 수 있는 EAP를 기본적으로 지원 합니다. EAP는 다음 인증 유형을 기반으로 보안 인증을 제공 합니다.<ul><li>사용자 이름 및 암호</li><li>스마트 카드 (실제 및 가상 모두)</li><li>사용자 인증서</li><li>비즈니스용 Windows Hello</li><li>EAP RADIUS 통합 방식으로 MFA 지원</li></ul>응용 프로그램 공급 업체는 사용자 지정 자격 증명 유형 및 OTP 지원을 비롯 하 여 사용 가능한 옵션의 배열을 포함 하지만 타사 UWP VPN 플러그 인 인증 방법을 제어 합니다.|

## <a name="vpn-connectivity"></a>VPN 연결

다음은 Always On VPN 연결의 주요 향상 기능입니다.

|  주요 개선 사항  | 설명 |
|---|---|
|                    **Always On**                    |                                                                                          Always On은 활성 VPN 프로필이 자동으로 연결 될 수 있도록 하는 Windows 10 기능이 며, 사용자 로그인, 네트워크 상태 변경 또는 장치 화면이 활성 상태 인지에 따라 연결 된 상태를 유지 합니다. 또한 Always On은 배터리 수명을 최대화 하기 위해 연결 된 대기 환경에 통합 되어 있습니다.                                                                                           |
|             **트리거하는 응용 프로그램**              |                                                                                                                                          지정 된 응용 프로그램 집합을 시작할 때 자동으로 연결할 수 있도록 Windows 10에서 VPN 프로필을 구성할 수 있습니다. VPN 연결을 트리거하기 위해 데스크톱 및 UWP 응용 프로그램을 모두 구성할 수 있습니다.                                                                                                                                          |
|              **이름 기반 트리거**              |                                                                                                            Always On VPN을 사용 하면 특정 도메인 이름 쿼리가 VPN 연결을 트리거하기 위해 규칙을 정의할 수 있습니다. 이제 Windows 10은 도메인에 가입 된 컴퓨터와 연결 되지 않은 컴퓨터에 대 한 이름 기반 트리거를 지원 합니다 (이전에는 도메인에 가입 된 컴퓨터만 지원 됨).                                                                                                            |
|            **신뢰할 수 있는 네트워크 검색**            |                                                                                    Always On VPN은 사용자가 회사 경계 내에서 신뢰할 수 있는 네트워크에 연결 된 경우 VPN 연결이 트리거되지 않도록이 기능을 포함 합니다. 이 기능을 앞에서 설명한 것과 함께 사용 하 여 원활한 "필요한 경우에만 연결" 사용자 환경을 제공할 수 있습니다.                                                                                     |
| **[장치 터널](../vpn-device-tunnel-config.md)** | Always On VPN은 장치 또는 컴퓨터에 대 한 전용 VPN 프로필을 만드는 기능을 제공 합니다. 사용자가 장치 또는 컴퓨터에 로그온 한 후에 연결 하는 *사용자 터널*과 달리 *장치 터널* 을 통해 VPN은 사용자 로그인 전에 연결을 설정할 수 있습니다. 장치 터널 및 사용자 터널은 모두 VPN 프로필과 독립적으로 작동 하 고 동시에 연결 될 수 있으며, 다른 인증 방법 및 기타 VPN 구성 설정을 적절 하 게 사용할 수 있습니다. |

## <a name="networking"></a>네트워킹

다음은 Always On VPN의 네트워킹 개선 사항 중 일부입니다.


|              주요 개선 사항              |                                                                                                                                                                                                                설명                                                                                                                                                                                                                |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **IPv4 및 IPv6에 대 한 이중 스택 지원**  | Always On VPN은 기본적으로 이중 스택 방식에서 IPv4 및 i p v 6의 사용을 지원 합니다. 다른 프로토콜에 대 한 특정 종속성이 없습니다 .이를 통해 IPv4/IPv6 응용 프로그램 호환성을 이후 IPv6 네트워킹 요구 사항에 대 한 지원과 함께 사용할 수 있습니다.<p>***참고:*** 시작 하기 전에 VPN 서버에서 i p v 6를 사용 하도록 설정 해야 합니다. 그렇지 않으면 연결을 설정할 수 없으며 오류 메시지가 표시 됩니다. |
| **응용 프로그램별 라우팅 정책** |                            인터넷 및 인트라넷 트래픽 분리를 위한 글로벌 VPN 연결 라우팅 정책을 정의 하는 것 외에도 라우팅 정책을 추가 하 여 분할 터널의 사용을 제어 하거나 응용 프로그램 별로 터널 구성을 강제 적용할 수 있습니다. 이 옵션은 VPN 터널을 통해 리소스와 상호 작용할 수 있는 앱을 보다 세부적으로 제어할 수 있도록 합니다.                             |
|           **제외 경로**            |                 Always On VPN은 VPN만 통과 해야 하는 트래픽을 정의 하기 위해 특별히 라우팅 동작을 제어 하는 제외 경로를 지정 하는 기능을 지원 하며, 실제 네트워크 인터페이스를 통해 이동 하지 않습니다.<p><p>***참고:***<br>-제외 경로는 현재 클라이언트와 동일한 서브넷 내에 있는 트래픽에 대해 작동 합니다 (예: LinkLocal).<br>-제외 경로는 분할 터널 설정 에서만 작동 합니다.                  |

## <a name="configuration-and-compatibility"></a>구성 및 호환성 

다음은 Always On VPN의 구성 및 호환성 향상 기능 중 일부입니다.


|                 주요 개선 사항                  |                                                                                                                                                                                                                                                                                                                       설명                                                                                                                                                                                                                                                                                                                       |
|--------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    **타사 VPN gateway 호환성**     | Always On VPN 클라이언트는 Microsoft 기반 VPN gateway를 사용 하 여 작동 하지 않아도 됩니다. 클라이언트는 IKEv2 프로토콜을 지원 하기 때문에이 업계 표준 터널링 유형을 지 원하는 타사 VPN 게이트웨이와의 상호 운용성을 용이 하 게 합니다. 또한 Always On VPN 플랫폼 기능과 이점에 영향을 주지 않고 사용자 지정 터널링 유형과 결합 된 UWP VPN 플러그 인을 사용 하 여 타사 VPN 게이트웨이와의 상호 운용성을 달성할 수 있습니다.<p><p>***참고:***<br>I k e v 2를 사용 하 여 게이트웨이 또는 타사 백 엔드 어플라이언스 공급 업체와 Always On VPN 및 장치 터널의 호환성을 참조 하세요. |
| **업계 표준 IKEv2 VPN 프로토콜 지원** |                                                                                                                                                                                                                              Always On VPN 클라이언트는 현재 가장 널리 사용 되는 업계 표준 터널링 프로토콜인 IKEv2를 지원 합니다. 이 호환성은 타사 VPN 게이트웨이와의 상호 운용성을 극대화 합니다.                                                                                                                                                                                                                               |
|               **플랫폼 지원**               |                                                                                                                                                                                                           AAlways On VPN은 도메인 가입, 비도메인 조인 (작업 그룹) 또는 Azure AD 조인 장치를 지원 하 여 두 기업은 모두 허용 하 고 BYOD (사용자 장치) 시나리오를 가져옵니다. 또한 Always On VPN은 모든 Windows 버전에서 사용할 수 있습니다.                                                                                                                                                                                                           |
| **다양 한 관리 및 배포 메커니즘** |                                                                                                                                 다양 한 관리 및 배포 메커니즘을 사용 하 여 Windows PowerShell, System Center Configuration Manager, Intune 또는 타사 MDM (모바일 장치 관리) 도구 및 Windows를 포함 한 VPN 설정 ( *vpn 프로필*이라고 함)을 관리할 수 있습니다. 구성 디자이너. 이러한 옵션을 사용 하면 사용 하는 클라이언트 관리 도구에 관계 없이 Always On VPN의 구성이 간단해 집니다.                                                                                                                                 |
|     **표준화 된 VPN 프로필 정의**      |                                                                                                                                                                                                                                  Always On VPN은 프로 파일링 및 배포 도구 집합 대부분에서 사용 하는 표준 구성 템플릿 형식을 제공 하는 프로 파일링 (표준 XML 프로필)을 사용 하 여 구성을 지원 합니다.                                                                                                                                                                                                                                   |

## <a name="next-steps"></a>다음 단계

- [몇 가지 고급 Always On VPN 기능에 대해 알아봅니다.](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 기술에 대 한 자세한 정보](always-on-vpn-technology-overview.md)

- [Always On VPN 배포 계획 시작](deploy/always-on-vpn-deploy-deployment.md)