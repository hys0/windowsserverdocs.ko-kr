---
title: 원격 액세스 Always On VPN 마이그레이션 개요
description: Always On VPN은 Windows Vpn과 DirectAccess 간의 이전 간격을 해결 하는 방법과 DirectAccess에서 Always On VPN으로 마이그레이션하는 방법에 대해 설명 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 05/29/2018
ms.openlocfilehash: bd4d0d4d3b165a4e89a00cd2975ace20687aed7d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314982"
---
# <a name="overview-of-the-directaccess-to-always-on-vpn-migration"></a>DirectAccess-Always On VPN 마이그레이션 개요 

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

&#187;[ **다음:** VPN 마이그레이션을 Always On DirectAccess 계획](da-always-on-migration-planning.md)

이전 버전의 Windows VPN 아키텍처에서 플랫폼 제한 사항은 사용자가 로그인 하기 전에 시작 된 자동 연결 등 DirectAccess를 교체 하는 데 필요한 중요 한 기능을 제공 하기 어려웠습니다. 그러나 Always On VPN은 이러한 제한 사항을 대부분 완화 하거나 DirectAccess 기능을 벗어나는 VPN 기능을 확장 했습니다. Always On VPN은 Windows Vpn과 DirectAccess 간의 이전 간격을 해결 합니다.

DirectAccess – Always On VPN 마이그레이션 프로세스는 4 가지 기본 구성 요소 및 상위 수준 프로세스로 구성 됩니다.


1.  **Always On VPN 마이그레이션을 계획 합니다.** 계획은 사용자 단계 분리를 위한 대상 클라이언트와 인프라 및 기능을 식별 하는 데 도움이 됩니다.

    1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

    2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

    3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

    4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

2.  **Side-by-side VPN 인프라를 배포 합니다.** 마이그레이션 단계와 배포에 포함 하려는 기능을 결정 한 후에는 Always On VPN 인프라를 기존 DirectAccess 인프라와 나란히 배포 합니다.  

3.  **인증서 및 구성을 클라이언트에 배포 합니다.**  VPN 인프라가 준비 되 면 필요한 인증서를 만들어 클라이언트에 게시 합니다. 클라이언트에서 인증서를 받은 경우 VPN_Profile. ps1 구성 스크립트를 배포 합니다. 또는 Intune을 사용 하 여 VPN 클라이언트를 구성할 수 있습니다. Microsoft Endpoint Configuration Manager 또는 Microsoft Intune를 사용 하 여 성공적인 VPN 구성 배포를 모니터링할 수 있습니다.

4.  **제거 및 서비스 해제.** 모든 사용자가 DirectAccess를 해제 한 후 환경을 적절 하 게 서비스 해제 합니다.

    1.  [!INCLUDE [remove-da-from-client-shortdesc-include](../includes/remove-da-from-client-shortdesc-include.md)]

    2.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]


## <a name="directaccess-deployment-scenario"></a>DirectAccess 배포 시나리오

이 배포 시나리오에서는 간단한 DirectAccess 배포 시나리오를이 가이드에서 제공 하는 마이그레이션의 시작 지점으로 사용 합니다. Always On VPN으로 마이그레이션하기 전에이 배포 시나리오와 일치 하지 않아도 되지만 대부분의 조직에서는이 간단한 설정이 현재 DirectAccess 배포를 정확 하 게 표현 합니다. 아래 표에서는이 설치 프로그램에 대 한 기본 기능 목록을 제공 합니다.

많은 DirectAccess 배포 시나리오와 옵션이 있으므로 구현이 여기에 설명 된 것과 다를 수 있습니다. 그렇다면 [DirectAccess와 ALWAYS ON vpn 간의 기능 매핑](../vpn/vpn-map-da.md) 을 참조 하 여 현재 추가 기능에 대 한 Always On vpn 기능 집합 매핑을 확인 한 후 해당 기능을 구성에 추가 합니다. 또한 [ALWAYS ON vpn 개선](../vpn/always-on-vpn/always-on-vpn-enhancements.md) 사항을 참조 하 여 Always On vpn 배포에 옵션을 추가할 수 있습니다.

>[!NOTE] 
>비도메인 가입 장치의 경우 인증서 등록과 같은 추가 고려 사항이 있습니다. 자세한 내용은 [Windows Server 및 windows 10에 대 한 ALWAYS ON VPN 배포](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)를 참조 하세요.

### <a name="deployment-scenario-feature-list"></a>배포 시나리오 기능 목록

| DirectAccess 기능 | 일반적인 시나리오 |
|-----|----|
| 배포 시나리오                   | 클라이언트 액세스 및 원격 관리용으로 전체 DirectAccess 배포                                               |
| 네트워크 어댑터                      | 2                                                                                                              |
| 사용자 인증                   | Active Directory 자격 증명                                                                                   |
| 컴퓨터 인증서 사용             | 예                                                                                                            |
| 보안 그룹                       | 예                                                                                                            |
| 단일 DirectAccess 서버            | 예                                                                                                            |
| 네트워크 토폴로지                      | 두 네트워크 어댑터를 사용 하는에 지 방화벽 뒤의 NAT (네트워크 주소 변환)                            |
| 액세스 모드                           | 끝에서 가장자리로                                                                                                    |
| 터널링                             | 분할 터널                                                                                                   |
| 인증                        | 컴퓨터 인증서를 사용 하는 표준 PKI (공개 키 인프라) 인증 및 Kerberos (KerbProxy가 아님) |
| 프로토콜                             | HTTPS를 통한 IP (ip-https)                                                                                       |
| 네트워크 위치 서버 (NLS) 오프 상자 | 예                                                                                                            |

## <a name="always-on-vpn-deployment-scenario"></a>Always On VPN 배포 시나리오

이 배포 시나리오에서는 간단한 DirectAccess 환경을 DirectAccess 교체 솔루션인 간단한 Always On VPN 환경으로 마이그레이션하는 데 중점을 둡니다. 다음 표에서는이 간단한 솔루션에서 사용 되는 기능을 제공 합니다. Always On VPN 클라이언트에 대 한 추가 개선 사항에 대 한 자세한 내용은 [vpn 개선 사항 Always On](../vpn/always-on-vpn/always-on-vpn-enhancements.md)을 참조 하세요.

### <a name="always-on-vpn-features-used-in-the-simple-environment"></a>단순 환경에서 사용 되는 Always On VPN 기능

| VPN 기능 | 배포 시나리오 구성 |
|-----|-----|
| 연결 형식 | IKEv2 (Native IKE(Internet Key Exchange) version 2) |
| 네트워크 어댑터   | 2        |
| 사용자 인증  | Active Directory 자격 증명            |
| 컴퓨터 인증서 사용        | 예                          |
| 라우팅 | 분할 터널링 |
| 이름 확인 | 도메인 이름 정보 목록 및 DNS (Domain Name System) 접미사 |
| 트리거 | Always on 및 신뢰할 수 있는 네트워크 검색 |
| 인증  | 신뢰할 수 있는 플랫폼 모듈-보호 된 사용자 인증서를 사용 하 여 PEAP (protected Extensible Authentication Protocol-Transport Layer Security) |

## <a name="next-step"></a>다음 단계

[DirectAccess를 Always On 하 여 VPN 마이그레이션을 계획](da-always-on-migration-planning.md)합니다. 마이그레이션의 주된 목표는 사용자가 프로세스 전체에서 사무실에 대 한 원격 연결을 유지 관리 하는 것입니다.

---