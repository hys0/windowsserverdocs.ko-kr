---
title: Always On VPN 고급 기능
description: 이 배포에 제공 된 배포 시나리오를 넘어 보안 및 VPN 연결의 가용성을 개선 하기 위해 다른 고급 VPN 기능을 추가할 수 있습니다.
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067433"
---
# Always On VPN의 고급 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **이전:** Always On VPN 기술에 알아보기](../always-on-vpn-technology-overview.md)<br>
& #187; [ **다음:** Always On VPN 배포 계획](always-on-vpn-deploy-planning.md)

제공 하는 배포 시나리오를 넘어 보안 및 VPN 연결의 가용성을 개선 하기 위해 다른 고급 VPN 기능을 추가할 수 있습니다. 예를 들어, 이러한 구성 요소 연결을 허용 하기 전에 연결 클라이언트 정상 인지 되도록 도와줍니다.


## 고가용성

다음은 고가용성을 위해 추가 옵션입니다.


|옵션  |설명  |
|---------|---------|
|서버에 대 한 복원 력 및 부하 분산     |높은 가용성 또는 지원 많은 수의 요청을 필요로 하는 환경에서는 늘릴 수 있습니다 성능 및 원격 액세스의 복원 력 네트워크 정책 서버 (NPS)를 실행 되며 원격을 사용 하도록 설정 하는 여러 서버 간에 균형을 사용 하 여 액세스 서버 클러스터링 합니다.<p>관련된 문서:<ul><li>[NPS 프록시 서버 부하 분산](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[클러스터에 원격 액세스 배포](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|지리적 사이트 복구     |IP 기반 지리적 위치에 대 한 전역 Traffic Manager Windows Server 2016에서 DNS와 함께 사용할 수 있습니다. 보다 강력한 지리적 부하 분산에 대 한 전역 서버 부하 분산 솔루션을 Microsoft Azure Traffic Manager 등을 사용할 수 있습니다.<p>관련된 문서:<ul><li>[Traffic Manager의 개요](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

---

## 고급 인증

다음은 인증에 대 한 추가 옵션입니다.


|옵션  |설명  |
|---------|---------|
|비즈니스용 Windows Hello     |Windows 10에서는 비즈니스용 Windows Hello가 PC 및 모바일 장치에서 암호를 강력한 2단계 인증으로 바꿉니다. 이 인증은 장치에 연결 되 고 생체 인식이 사용 하 여 사용자 자격 증명이 나 개인 식별 번호 (PIN) 새로운 유형의 구성 됩니다.<p>Windows 10 VPN 클라이언트를 비즈니스용 Windows Hello와 호환 됩니다. 제스처를 사용 하 여 사용자가 로그 후 VPN 연결 사용 하 여 Windows Hello 인증서 기반 인증에 대 한 비즈니스 인증서에 대 한 합니다.<p>관련된 문서:<ul><li>[비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>기술 사례 연구: [Windows 10에서에서 비즈니스용 Windows Hello 사용 하 여 원격 액세스 권한 부여](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure Multi-factor Authentication (MFA)     |Azure MFA가 클라우드 및 온-프레미스 Windows VPN 인증 메커니즘을 사용 하 여 통합할 수 있는 버전입니다.<p>이 메커니즘의 작동 방식에 대 한 자세한 내용은 [Azure Multi-factor Authentication 서버를 사용 하 여 RADIUS 통합 인증](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius)을 참조 하세요.         |

---

## 고급 VPN 기능

다음은 고급 기능에 대 한 추가 옵션입니다.


|옵션  |설명  |
|---------|---------|
|트래픽 필터링     |클라이언트에서 액세스할 수 있는 응용 프로그램 VPN 적용 해야 할 경우에 VPN 트래픽 필터를 사용할 수 있습니다.<p>자세한 내용은 [VPN 보안 기능](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features)을 참조 하세요.         |
|앱에서 트리거한 VPN     |특정 응용 프로그램이 나 유형의 응용 프로그램을 시작할 때 자동으로 연결 하는 VPN 프로필을 구성할 수 있습니다.<p>이 옵션 및 기타 트리거 옵션에 대 한 자세한 내용은 [VPN 자동 트리거된 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile)을 참조 하세요.         |
|VPN 조건부 액세스   |조건부 액세스 및 장치 준수 VPN에 연결 하기 전에 표준을 충족 하는 관리 되는 장치 필요할 수 있습니다. VPN 조건부 액세스에 대 한 고급 기능 중 하나를 통해 클라이언트 인증 인증서 'AAD 조건부 액세스의 OID의 ' 1.3.6.1.4.1.311.87'에 포함 된 VPN 연결으로만 제한할 수 있습니다.<p>VPN 연결을 제한 하려면 해야 합니다.<ol><li>NPS 서버에서 **네트워크 정책 서버** 스냅인을 엽니다.</li><li>**정책**을 확장 > **네트워크 정책**입니다.</li><li>네트워크 정책 **가상 개인 네트워크 (VPN) 연결** 을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</li><li>**설정** 탭을 선택 합니다.</li><li>**특정 공급 업체를** 선택 하 고 **추가**클릭 합니다.</li><li>**허용 됨-인증서-OID** 옵션을 선택한 다음 **추가**클릭 합니다.</li><li>특성 값으로 **1.3.6.1.4.1.311.87** AAD 조건부 액세스 OID 붙여넣고 후 **확인** 을 두 번 클릭 합니다.</li><li>그런 다음 **닫기** 하 고 **적용**을 클릭 합니다.<p>이제 VPN 클라이언트를 클라우드 일시적인 인증서 이외의 모든 인증서를 사용 하 여 연결 하려고 연결이 실패 합니다.</li></ol>조건부 액세스에 대 한 자세한 내용은 [VPN 및 조건부 액세스를](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)참조 하세요.   |

---


## 추가 보호 기능

**신뢰할 수 있는 플랫폼 모듈 (TPM) 키 증명**<p>
TPM 증명 된 키를 사용 하 여 사용자 인증서 내보내기 비, 해머링 방지 및 TPM에서 제공 하는 키의 격리 하 여 백업 더 높은 보안 보증을 제공 합니다.

Windows 10에서 TPM 키 증명에 대 한 자세한 내용은 [TPM 키 증명](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation)을 참조 하세요.

## 다음 단계
[Always On VPN 배포 계획 시작](always-on-vpn-deploy-planning.md): VPN 서버를 사용 하 여 계획 이라면 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 다음 작업을 수행 합니다. 후 적절 한 계획을 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.  

---

## 관련 항목
- [NPS 프록시 서버 부하 분산](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): 가상 사설망 (VPN) 서버 및 무선 액세스 지점과 같은 네트워크 액세스 서버는 원격 인증 전화-사용자 서비스 (RADIUS) 클라이언트 연결 요청을 만들고 RADIUS 보내 NPS 같은 서버. 경우에 따라 NPS 서버 나타날 수 너무 많은 연결 요청 한 번에 성능이 저하 또는 오버 로드 합니다.

- [Traffic Manager 개요](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview):이 항목의 Azure Traffic Manager, 서비스 끝점에 대 한 사용자 트래픽 배포를 제어할 수 있는 개요를 제공 합니다. 트래픽 관리자는 도메인 이름 시스템 (DNS)를 사용 하 여 트래픽을 라우팅 메서드와 끝점의 상태에 따라 가장 적합 한 끝점에 대 한 클라이언트 요청을 보냅니다. 

- [비즈니스용 Windows Hello](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification):이 항목에서는 클라우드 전용 배포 및 하이브리드 배포 등의 필수 구성 요소를 제공 합니다.  또한이 항목에서는 비즈니스용 Windows Hello에 대해 자주 묻는 질문을 나열합니다.

- [기술 사례 연구: 활성화 원격 액세스 Windows Hello와 함께 Windows 10에서 비즈니스용](https://msdn.microsoft.com/library/mt728163.aspx):이 기술 사례 연구에서는 Microsoft에서 비즈니스용 Windows Hello와 함께 원격 액세스를 구현 하는 방법을 알아봅니다.  비즈니스용 Windows Hello는 개인/공개 키 또는 암호를 벗어나는 조직 및 소비자 인증서 기반 인증 방법. 이 인증 형태는 암호를 대체할 수 고 침해, 도난을, 및 피싱 공격이 수 있는 키 쌍 자격 증명에 의존 합니다. 

- [Azure Multi-factor Authentication 서버를 사용 하 여 통합 RADIUS 인증](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius):이 항목에서는 Azure Multi-factor Authentication 서버를 사용 하 여 RADIUS 클라이언트 인증을 구성 하 고 추가 통해 안내 합니다. RADIUS는 표준 프로토콜 인증 요청을 수락 하 고 이러한 요청을 처리 합니다. Azure Multi-factor Authentication 서버 RADIUS 서버 역할을 수행할 수 있습니다. 

- [VPN 보안 기능](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features):이 항목에서는 지침을 제공 하면 VPN 보안 잠금 vpn의 경우 VPN 사용 하 여 Windows Information Protection (WIP) 통합 및 트래픽 필터 합니다. 

- [VPN 자동 트리거된 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile):이 항목에서는, 등의 앱 트리거 이름 기반 트리거 Always On VPN 자동 트리거된 프로필 옵션을 제공 합니다.

- [VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access):이 항목에서는 원격 클라이언트에 대 한 장치 준수 옵션을 제공 하기 위해 클라우드 기반 조건부 액세스 플랫폼의 개요를 제공 합니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다. 

- [TPM 키 증명](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation):이 항목에서는 신뢰할 수 있는 플랫폼 모듈 (TPM) 개요를 제공 하 고 TPM을 배포 하는 단계 키 증명 합니다. 또한 문제 해결 정보 및 문제 해결 단계를 찾을 수 있습니다. 

---