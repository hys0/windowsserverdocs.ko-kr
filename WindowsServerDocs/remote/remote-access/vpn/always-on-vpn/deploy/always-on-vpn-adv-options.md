---
title: Always On VPN 고급 기능
description: 이 배포에 제공 된 배포 시나리오에서 초과 보안 및 VPN 연결의 가용성을 개선 하기 위해 기타 고급 VPN 기능을 추가할 수 있습니다.
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: a544ac3c1a121874170a2fc78a34bd401b8bebe1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885084"
---
# <a name="advanced-features-of-always-on-vpn"></a>Always On VPN의 고급 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**이전:** Always On VPN 기술을 배우고합니다](../always-on-vpn-technology-overview.md)<br>
&#187;[ **다음:** Always On VPN 배포 계획 시작](always-on-vpn-deploy-planning.md)

제공 된 배포 시나리오를 넘어 보안 및 VPN 연결의 가용성을 개선 하기 위해 기타 고급 VPN 기능을 추가할 수 있습니다. 예를 들어, 이러한 구성 요소를 사용 하는 연결을 허용 하기 전에 연결 하는 클라이언트가 정상 인지 확인 수 있습니다.


## <a name="high-availability"></a>고가용성

다음은 고가용성을 위한 추가 옵션입니다.


|옵션  |설명  |
|---------|---------|
|서버 복원 력 및 부하 분산     |높은 가용성 또는 지원을 많은 수의 요청을 필요로 하는 환경에서는 늘리려면 성능 및 원격 액세스의 복원 력을 서버 NPS (네트워크 정책)를 실행 하 고 원격을 사용 하도록 설정 하는 여러 서버 간에 부하 분산을 사용 하 여 액세스 서버를 클러스터링 합니다.<p>관련된 문서:<ul><li>[NPS 프록시 서버 부하 분산](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[클러스터에 원격 액세스 배포](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|지리적 사이트 복구     |IP 기반 지리적 위치에 대 한 Windows Server 2016에서 DNS를 사용 하 여 Global Traffic Manager를 사용할 수 있습니다. 더 강력한 지리적 부하 분산에 대 한 Microsoft Azure Traffic Manager와 같은 전역 서버 부하 분산 솔루션을 사용할 수 있습니다.<p>관련된 문서:<ul><li>[Traffic Manager 개요](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

---

## <a name="advanced-authentication"></a>고급 인증

다음은 인증에 대 한 추가 옵션입니다.


|옵션  |설명  |
|---------|---------|
|비즈니스용 Windows Hello     |Windows 10에서는 비즈니스용 Windows Hello가 PC 및 모바일 디바이스에서 암호를 강력한 2단계 인증으로 바꿉니다. 이 인증의 새로운 유형의 장치에 연결 되 고 사용 하는 생체 인식 하는 사용자 자격 증명이 나 개인 식별 번호 (PIN)으로 구성 됩니다.<p>Windows 10 VPN 클라이언트는 Windows Hello와 호환 됩니다. 사용자 제스처도 로그인 한 후 VPN 연결에 사용 된 Windows Hello 인증서 기반 인증을 위해 비즈니스 인증서에 대 한 합니다.<p>관련된 문서:<ul><li>[비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>기술 사례 연구: [Windows 10에서에서 비즈니스용 Windows Hello 사용 하 여 원격 액세스를 사용 하도록 설정](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure MFA (다단계 인증)     |Azure MFA가 클라우드 및 온-프레미스 Windows VPN 인증 메커니즘을 사용 하 여 통합할 수 있는 버전입니다.<p>이 메커니즘 작동 방법에 대 한 자세한 내용은 참조 하세요. [Azure Multi-factor Authentication 서버와 RADIUS 인증 통합](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius)합니다.         |

---

## <a name="advanced-vpn-features"></a>고급 VPN 기능

다음은 고급 기능에 대 한 추가 옵션입니다.


|옵션  |설명  |
|---------|---------|
|트래픽 필터링     |클라이언트에서 액세스할 수 있는 응용 프로그램 VPN 적용 해야 할 경우에 VPN 트래픽 필터를 사용할 수 있습니다.<p>자세한 내용은 [VPN 보안 기능](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features)합니다.         |
|앱 트리거 VPN     |특정 응용 프로그램 또는 응용 프로그램의 종류를 시작 하는 경우 자동으로 연결 하려면 VPN 프로필을 구성할 수 있습니다.<p>이 및 다른 트리거 옵션에 대 한 자세한 내용은 참조 하세요. [VPN 프로필 자동 트리거 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile)합니다.         |
|VPN 조건부 액세스   |조건부 액세스 및 장치 규정 준수 표준에 맞도록 VPN에 연결 하기 전에 관리 되는 장치를 요구할 수 있습니다. 조건부 액세스를 위한 고급 기능 중 하나를 통해 클라이언트 인증 인증서는 'AAD 조건부 액세스 ' OID ' 1.3.6.1.4.1.311.87의 '를 포함 하는 위치만 VPN 연결을 제한할 수 있습니다.<p>VPN 연결을 제한 해야 합니다.<ol><li>NPS 서버에서 엽니다는 **네트워크 정책 서버** 스냅인입니다.</li><li>확장 **정책을** > **네트워크 정책을**합니다.</li><li>마우스 오른쪽 단추로 클릭 합니다 **가상 개인 네트워크 (VPN) 연결** 네트워크 정책 및 선택 **속성**합니다.</li><li>선택 된 **설정을** 탭 합니다.</li><li>선택 **공급 업체 특정** 누릅니다 **추가**합니다.</li><li>선택 된 **허용-인증서-OID** 옵션을 클릭 **추가**합니다.</li><li>AAD 조건부 액세스의 OID를 붙여 넣습니다 **1.3.6.1.4.1.311.87** 클릭 한 다음 확인 하 고 특성 값으로 **확인** 두 번입니다.</li><li>클릭 **닫습니다** 차례로 **적용**합니다.<p>이제 VPN 클라이언트는 수명이 짧은 클라우드 인증서 이외의 인증서를 사용 하 여 연결할 때 연결이 실패 합니다.</li></ol>조건부 액세스에 대 한 자세한 내용은 참조 하세요. [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)합니다.   |

---


## <a name="additional-protection"></a>추가 보호

**신뢰할 수 있는 플랫폼 모듈 (TPM) 키 증명**<p>
TPM 증명 된 키를 사용 하 여 사용자 인증서를 내보내기 아닌, 앤티 만들던 및 TPM에서 제공 하는 키의 격리 하 여 백업 하는 더 높은 보안 보증을 제공 합니다.

Windows 10에서 TPM 키 증명에 대 한 자세한 내용은 참조 하세요. [TPM 키 증명](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation)합니다.

## <a name="next-step"></a>다음 단계
[Always On VPN 배포 계획 시작](always-on-vpn-deploy-planning.md): VPN 서버를 사용 하 여 계획 하는 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 다음 작업을 수행 합니다. 적절 한 계획 한 후에 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.  

---

## <a name="related-topics"></a>관련 항목
- [NPS 프록시 서버 부하 분산](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): 가상 사설망 (VPN) 서버 및 무선 액세스 지점과 같은 네트워크 액세스 서버는 원격 인증 전화 접속 사용자 서비스 (RADIUS) 클라이언트 연결 요청을 만들고 NPS와 같은 RADIUS 서버 보냅니다. 일부 경우에는 NPS 서버 요청을 받을 수 너무 많은 연결 한 번에 성능 저하 또는 오버 로드.

- [Traffic Manager 개요](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview): 이 항목의 Azure Traffic Manager 서비스 끝점에 대 한 사용자 트래픽의 배포를 제어할 수 있는 개요를 제공 합니다. Traffic Manager 도메인 이름 시스템 (DNS)를 사용 하 여 트래픽 라우팅 메서드 및 끝점의 상태에 따라 가장 적합 한 끝점으로 클라이언트 요청을 보냅니다. 

- [비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification): 이 항목에서는 클라우드 전용 배포 및 하이브리드 배포와 같은 필수 구성 요소를 제공합니다.  또한이 항목에 대 한 Windows Hello 비즈니스에 대 한 질문과 대답을 나열합니다.

- [기술 사례 연구: Windows 10에서에서 비즈니스용 Windows Hello 사용 하 여 원격 액세스를 사용 하도록 설정 하면](https://msdn.microsoft.com/library/mt728163.aspx): 이 기술 사례 연구에서는 Microsoft 비즈니스용 Windows Hello와 원격 액세스를 구현 하는 방법을 알아봅니다.  Windows Hello for Business는 개인/공개 키 또는 암호 수준을 넘어서는 조직과 소비자에 대 한 인증서 기반 인증 방법. 이 형태의 인증 암호를 대신할 수 및 위반, 도난 및 피싱에 강한 키 쌍 자격 증명에 의존 합니다. 

- [Azure Multi-factor Authentication 서버와 RADIUS 인증 통합](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): 이 항목에서는 안내 추가 하 고 Azure Multi-factor Authentication 서버를 사용 하 여 RADIUS 클라이언트 인증을 구성 합니다. RADIUS는 인증 요청을 받고 해당 요청을 처리하는 표준 프로토콜입니다. Azure Multi-factor Authentication 서버를 RADIUS 서버로 작동할 수 있습니다. 

- [VPN 보안 기능](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features): 이 항목에서는 잠금 VPN, VPN 및 트래픽 필터를 사용 하 여 Windows 정보 보호 (WIP) 통합에 대 한 VPN 보안 지침을 제공합니다. 

- [VPN 프로필 자동 트리거 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile): 이 항목에서는 앱 트리거, 트리거 이름 기반 및 Always On 등의 VPN 프로필 자동 트리거 옵션을 제공 합니다.

- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이 항목에서는 원격 클라이언트에 대 한 장치 준수 옵션을 제공 하기 위해 클라우드 기반 조건부 액세스 플랫폼의 개요를 제공 합니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다. 

- [TPM 키 증명](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation): 이 항목에서는 모듈 TPM (Trusted Platform) 및 단계는 TPM 키 증명을 배포 하는 개요를 제공 합니다. 또한 문제를 해결 하는 단계 및 문제 해결 정보를 찾을 수 있습니다. 

---