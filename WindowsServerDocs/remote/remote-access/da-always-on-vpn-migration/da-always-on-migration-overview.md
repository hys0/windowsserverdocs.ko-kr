---
title: 원격 액세스 Always On VPN 마이그레이션 개요
description: Always On VPN Windows Vpn 및 DirectAccess 및 Always On VPN에 directaccess에서로 마이그레이션하는 방법 간의 이전 차이 해결 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/29/2018
ms.openlocfilehash: 402d8ff72fe869572c9e6129cdf1aa7e755c354a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845984"
---
# <a name="overview-of-the-directaccess-to-always-on-vpn-migration"></a>DirectAccess-Always On VPN 마이그레이션 개요 

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

&#187;[ **다음:** Always On VPN 마이그레이션에 대 한 DirectAccess 계획](da-always-on-migration-planning.md)

Windows VPN 아키텍처의 이전 버전의 플랫폼 제한 하기가 어려웠습니다 DirectAccess를 사용 하면 사용자가 로그인 하기 전에 시작 하는 자동 연결 등 대체 하는 데 필요한 중요 한 기능을 제공 합니다. 그러나 Always On VPN, 이러한 제한 사항 중 대부분을 완화할 했거나이 DirectAccess의 기능을 넘어 VPN 기능을 확장 합니다. Always On VPN 주소 Windows Vpn 및 DirectAccess 사이의 차이 이전 제거 합니다.

DirectAccess –에 – Always On VPN 마이그레이션 프로세스는 네 가지 기본 구성 요소 및 높은 수준의 프로세스 구성 됩니다.


1.  **Always On VPN 마이그레이션을 계획 합니다.** 계획에 사용자 단계 분리 뿐만 아니라 인프라와 기능에 대 한 대상 클라이언트를 식별 하는 데 도움이 됩니다.

    1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

    2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

    3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

    4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

2.  **Side-by-side-VPN 인프라를 배포 합니다.** 배포에 포함 하려는 기능과 마이그레이션 단계에 확인 한 후 기존 DirectAccess 인프라와 함께 Always On VPN 인프라를 배포 합니다.  

3.  **클라이언트 인증서 및 구성을 배포 합니다.**  VPN 인프라 준비 되 면 만들고 클라이언트에 필요한 인증서를 게시 합니다. 클라이언트 인증서를 받은 경우 VPN_Profile.ps1 구성 스크립트를 배포 합니다. 또는 VPN 클라이언트를 구성 하려면 Intune을 사용할 수 있습니다. Microsoft System Center Configuration Manager 또는 Microsoft Intune을 사용 하 여 성공적인 VPN 구성 배포를 모니터링 합니다.

4.  **서비스 해제 및 제거 합니다.** DirectAccess 오프 모든 사용자를 마이그레이션한 후에 제대로 환경을 해제 합니다.

    1.  [!INCLUDE [remove-da-from-client-shortdesc-include](../includes/remove-da-from-client-shortdesc-include.md)]

    2.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]


## <a name="directaccess-deployment-scenario"></a>DirectAccess 배포 시나리오

이 배포 시나리오에서는이 가이드에서는 제공 된 마이그레이션에 대 한 시작 점으로 간단한 DirectAccess 배포 시나리오를 사용 합니다. Always On VPN을로 마이그레이션하기 전에이 배포 시나리오에 맞게 필요는 없지만 많은 조직에서는이 간단한 설치를 현재 DirectAccess 배포의 정확한 표현 합니다. 아래 표에이 설치에 대 한 기본 기능 목록을 제공합니다.

많은 DirectAccess 배포 시나리오와 옵션 존재 하므로 구현은 여기에 설명 된 것과에서 다를 수 있습니다. 그렇다면 가리킵니다 [DirectAccess 및 Always On VPN 간의 기능 매핑을](../vpn/vpn-map-da.md) Always On VPN 기능을 설정 하면 현재 추가 기능에 대 한 매핑을 확인 한 후 구성에 이러한 기능을 추가 합니다. 또한를 참조할 수 있습니다는 [Always On VPN 향상 된 기능](../vpn/always-on-vpn/always-on-vpn-enhancements.md) Always On VPN 배포 옵션을 추가 합니다.

>[!NOTE] 
>비도메인 가입 장치에 대 한 인증서 등록 등의 추가 고려 사항이 있습니다. 자세한 내용은 참조 하세요 [Always On VPN 배포에 대 한 Windows Server 및 Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)합니다.

### <a name="deployment-scenario-feature-list"></a>배포 시나리오 기능 목록

| DirectAccess 기능 | 일반적인 시나리오 |
|-----|----|
| 배포 시나리오                   | 클라이언트 액세스 및 원격 관리용으로 전체 DirectAccess 배포                                               |
| 네트워크 어댑터                      | 2                                                                                                              |
| 사용자 인증                   | Active Directory 자격 증명                                                                                   |
| 컴퓨터 인증서 사용             | 예                                                                                                            |
| 보안 그룹                       | 예                                                                                                            |
| 단일 DirectAccess 서버            | 예                                                                                                            |
| 네트워크 토폴로지                      | 네트워크 주소 변환 (NAT 경계 면 방화벽 뒤에 두 개의 네트워크 어댑터를 사용 하 여)                            |
| 액세스 모드                           | 가장자리 종료                                                                                                    |
| 터널링                             | 분할 터널                                                                                                   |
| 인증                        | 컴퓨터 인증서와 Kerberos (없습니다 KerbProxy)를 사용 하 여 표준 PKI (공개 키 인프라) 인증 |
| 프로토콜                             | HTTPS (IP-HTTPS)를 통한 IP                                                                                       |
| 네트워크 위치 서버 (NLS) 해제-상자 | 예                                                                                                            |

## <a name="always-on-vpn-deployment-scenario"></a>Always On VPN 배포 시나리오

이 배포 시나리오에서는 간단한 DirectAccess 환경을 DirectAccess 대체 솔루션에는 간단한 Always On VPN 환경으로 마이그레이션하는 방법에 집중 합니다. 다음 표에서이 간단한 솔루션에서 사용 하는 기능을 제공 합니다. Always On VPN 클라이언트에 향상 된 추가 기능에 대 한 정보를 자세한 [Always On VPN 향상](../vpn/always-on-vpn/always-on-vpn-enhancements.md)합니다.

### <a name="always-on-vpn-features-used-in-the-simple-environment"></a>간단한 환경에서 사용 되는 always On VPN 기능

| VPN 기능 | 배포 시나리오 구성 |
|-----|-----|
| 연결 형식 | 네이티브 Internet Key Exchange version 2 (IKEv2) |
| 네트워크 어댑터   | 2        |
| 사용자 인증  | Active Directory 자격 증명            |
| 컴퓨터 인증서 사용        | 예                          |
| 라우팅 | 분할 터널링 |
| 이름 확인 | 도메인 이름 정보 목록 및 도메인 이름 시스템 (DNS) 접미사 |
| 트리거 | Always on이 고 신뢰할 수 있는 네트워크 검색 |
| 인증  | 보호 된 확장할 수 있는 인증 프로토콜 전송 계층 보안 (PEAP-TLS) Trusted Platform Module-보호 된 사용자 인증서를 사용 하 여 |

## <a name="next-step"></a>다음 단계

[Always On VPN 마이그레이션에 대 한 DirectAccess 계획](da-always-on-migration-planning.md)합니다. 주된 목적은 마이그레이션 과정에서 office에 대 한 원격 연결을 유지 하기 위해 사용자입니다.

---