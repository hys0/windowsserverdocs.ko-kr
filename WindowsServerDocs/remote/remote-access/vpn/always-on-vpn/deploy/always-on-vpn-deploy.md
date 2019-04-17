---
title: Windows Server 및 Windows 10에 대한 Always On VPN 배포
description: Windows 10 클라이언트 컴퓨터에 대 한 Windows Server 2016 이상 원격 액세스 및 Always On VPN 프로필을 사용 하 여 원격 직원에 대 한 항상에서 가상 개인 네트워크 (VPN) 연결을 배포 하려면이 배포를 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cb60bdc6d6f3ff074f04827aa95c9e8e8abf35b
ms.sourcegitcommit: c435f91ef6f3ff5ffd2661291264b939d5ce4e2a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2018
ms.locfileid: "8981133"
---
# Windows Server 및 Windows 10에 대 한 always On VPN 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **이전:** 원격 액세스](../../../Remote-Access.md)<br>
& #187; [ **다음:** Always On VPN 기능 및 기능에 알아보기](../../vpn-map-da.md)


Always On VPN 원격 액세스 및 도메인에 가입 된 지원에 대 한 단일, 통합 솔루션, 미가입 (작업 그룹), 또는 개인적으로 장치를 소유 하 고 Azure AD – 가입 된 디바이스를 제공 합니다.  Always On VPN을 사용 하 여 연결 유형을 사용자 또는 디바이스만 될 필요가 없기 있지만 둘 다를 수 있습니다. 예를 들어 원격 장치 관리에 대 한 장치 인증을 사용 하 고 회사 내부 사이트 및 서비스에 연결에 대 한 사용자 인증을 사용 하도록 설정 수 있습니다.



## 사전 요구 사항

대부분의 경우에 기술이 Always On VPN 배포를 사용할 수 있는 배포 합니다. DC/DNS 서버 이외의 Always On VPN 배포 하는 NPS (반경) 서버, CA (인증 기관) 서버 및 원격 액세스 (라우팅/VPN) 서버에 필요합니다. 인프라를 설정 되 면 클라이언트를 등록 하 고 온-프레미스 여러 네트워크 변경을 통해 안전 하 게 하는 클라이언트를 연결 해야 합니다.

- Active Directory 도메인 인프라를 하나 이상의 도메인 이름 시스템 (DNS) 서버를 포함 합니다. 내부 및 외부 도메인 이름 시스템 (DNS) 영역에는 필요한 경우 내부 영역 외부 영역 (예를 들어 corp.contoso.com 및 contoso.com)의 하위 도메인 위임 된 것으로 가정 하는 합니다.
- Active Directory 기반 공개 키 인프라 (PKI) 및 Active Directory 인증서 서비스 (AD CS).
- 가상 또는 실제, 기존 또는 네트워크 정책 서버 (NPS)를 설치 하려면 새 서버입니다. 네트워크에서 NPS 서버 이미 있는 경우 새 서버를 추가 하는 대신 기존 NPS 서버 구성을 수정할 수 있습니다.
- IKEv2 VPN 연결 및 LAN 라우팅 지원 기능 중 일부 하위 집합을 사용 하 여 RAS 게이트웨이 VPN 서버 원격 액세스 합니다.
- 두 개의 방화벽을 포함 하는 경계 네트워크.  방화벽 제대로 작동 하려면 반경 및 VPN 통신에 필요한 트래픽을 허용 하는지 확인 합니다. 자세한 내용은 [항상에서 VPN 기술 개요](../always-on-vpn-technology-overview.md)를 참조 하세요.
- 물리적 서버 또는 원격 액세스 RAS 게이트웨이 VPN 서버로 설치 하려면 두 개의 실제 이더넷 네트워크 어댑터를 사용 하 여 경계 네트워크에 가상 컴퓨터 (VM). Vm은 호스트에 대 한 가상 LAN (VLAN) 필요합니다. 
- 멤버십 관리자 또는 이와 동등한에 최소 요구 사항입니다.
- 배포를 수행 하기 전에이 배포에 대 한 준비 되 게 하는이 가이드의 계획 섹션을 읽어 보세요.
- 각 사용 되는 기술에 대 한 디자인 및 배포 가이드를 검토 합니다. 이 가이드 서비스 및 조직의 네트워크에 필요한 구성 배포 시나리오 제공 하는지 여부를 확인할 수 있습니다. 자세한 내용은 [항상에서 VPN 기술 개요](../always-on-vpn-technology-overview.md)를 참조 하세요.
- Always On VPN 구성 CSP 공급 업체별 없기 때문에 배포 하기 위한 선택한 관리 플랫폼입니다.


>[!IMPORTANT]
>이 배포에 대 한 요구 사항은 아니지만 인프라 서버, Active Directory 도메인 서비스, Active Directory 인증서 서비스 및 네트워크 정책 서버를 실행 하는 컴퓨터와 같은 Windows Server 2016을 실행 됩니다. 원격 액세스를 실행 하는 서버 및 인프라 서버에 대 한 이전 버전의 Windows Server 2012 r 2와 같은 Windows Server를 사용할 수 있습니다.
>
>가상 컴퓨터에 원격 액세스 배포 하려고 하지 마십시오 Microsoft azure에서 \(VM\) 합니다. 원격 액세스를 사용 하 여 Microsoft Azure에서 지원 되지 않는 원격 액세스 VPN과 DirectAccess를 포함 합니다. 자세한 내용은 [Microsoft Azure 가상 컴퓨터에 대 한 지원 Microsoft 서버 소프트웨어](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)를 참조 하세요.


## <a name="bkmk_about"></a>이 배포에 대 한

제공 된 지침으로 단일 테 넌 트 VPN RAS 게이트웨이 중간 to\ 사이트 VPN 연결에 대 한 Windows 10을 실행 하는 원격 클라이언트 컴퓨터에 대 한, 아래에 설명 된 시나리오 중 하나를 사용 하 여 원격 액세스 배포를 안내 합니다. 배포에 대 한 기존 인프라의 일부를 수정 하기 위한 지침을 찾을 수도 있습니다. 또한이 배포 전체에서 VPN 연결 프로세스, 구성 하는 서버, ProfileXML VPNv2 CSP 노드 및 Always On VPN 배포를 다른 기술에 대 한 자세한 수 있도록 링크를 찾을 있습니다.

**Always On VPN 배포 시나리오:**

1. Always On VPN 배포만 합니다.
2. Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스 Always On VPN 배포 합니다.


자세한 내용 및 워크플로 제시 하는 시나리오의 [배포 Always On VPN](always-on-vpn-deploy-deployment.md)을 참조 하세요.


## <a name="bkmk_not"></a>이 배포에서 제공 되지 않는 기능

이 배포에 대 한 지침을 제공 하지 않습니다.

- Active Directory 도메인 서비스 \(AD DS\) 합니다.
- Active Directory 인증서 서비스는 공개 키 인프라 및 \(AD CS\) \(PKI\) 합니다.
- 동적 호스트 구성 프로토콜 \(DHCP\) 합니다. 
- 이더넷 케이블이, 방화벽, 스위치 및 허브 같은 하드웨어를 네트워크입니다.
- Always On VPN 연결을 통해 원격 사용자가 액세스할 수 있는 응용 프로그램 및 파일 서버와 같은 추가 네트워크 리소스
- 인터넷 연결 또는 Azure AD를 사용 하 여 인터넷 연결에 대 한 조건부 액세스 합니다. 세부 정보를 [Azure Active Directory에 액세스 하는 조건부](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 참조 하세요.




## 다음 단계

- [Always On VPN 기능에 대해 자세히 알아보기](../../vpn-map-da.md)

- [Always On VPN 기능 향상에 자세히 알아보기](../always-on-vpn-enhancements.md)

- [Always On VPN 고급 기능 중 일부에 대해 알아보기](always-on-vpn-adv-options.md)

- [Always On VPN 기술에 자세히 알아보기](../always-on-vpn-technology-overview.md)

- [Always On VPN 배포 계획](always-on-vpn-deploy-deployment.md)


---
