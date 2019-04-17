---
title: Always On VPN 배포
description: 이 항목에서는 Always On VPN Windows Server 2016의 배포에 대 한 자세한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15c60f2986d3837c5c6e03f9e0a25c7e0a4e0cc0
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067329"
---
# Always On VPN 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #0171; [ **이전:** 항상에서 VPN 고급 기능에 알아보기](always-on-vpn-adv-options.md)<br>
& #0187; [ **다음:** 1 단계입니다. Always On VPN 배포 계획](always-on-vpn-deploy-planning.md)

이 섹션에서는 원격 도메인에 가입 된 Windows 10 클라이언트 컴퓨터에 대 한 Always On VPN 연결을 배포 하기 위한 워크플로에 대 한 알아봅니다. **조건부 액세스를 구성** 하는 VPN 사용자 리소스에 액세스 하는 방법을 세밀 하 게 하려면 [Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스](../../ad-ca-vpn-connectivity-windows10.md)를 참조 하세요. Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스에 대 한 자세한 내용은 [Azure Active Directory 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 참조 하세요. 


다음 다이어그램은 Always On VPN을 배포할 때 다양 한 시나리오에 대 한 워크플로 프로세스를 보여 줍니다. 

_이미지를 확대 하려면 클릭_합니다.

<a href="../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow.png" alt="Full-sized view of the Always On VPN deployment workflow" target="_blank">![섬네일](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)
</a> 

>[!IMPORTANT]
>이 배포에 대 한 요구 사항은 아니지만 인프라 서버, Active Directory 도메인 서비스, Active Directory 인증서 서비스 및 네트워크 정책 서버를 실행 하는 컴퓨터와 같은 Windows Server 2016을 실행 됩니다. 원격 액세스를 실행 하는 서버 및 인프라 서버에 대 한 이전 버전의 Windows Server, Windows Server 2012 r 2를 사용할 수 있습니다.

## [1단계. Always On VPN 배포 계획 수립](always-on-vpn-deploy-planning.md)

이 단계를 계획 하 고 Always On VPN 배포 준비를 시작 합니다. 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 사용 하 여 VPN 서버 계획 이라면 합니다. 후 적절 한 계획을 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.

## [2단계. Always On VPN 서버 인프라 구성](vpn-deploy-server-infrastructure.md)

이 단계에서 설치 및 VPN을 지 원하는 데 필요한 서버 측 구성 요소를 구성 합니다. 서버 쪽 구성 요소는 사용자, VPN 서버 및 NPS 서버에서 사용 되는 인증서를 배포할 PKI 구성 포함 됩니다.  RRAS IKEv2 연결 및 VPN 연결에 대 한 인증을 수행 하는 NPS 서버를 지원 하도록 구성할 수도 있습니다.

서버 인프라를 구성 하려면 다음 작업을 수행 해야 합니다.
- **Active Directory 도메인 서비스를 사용 하 여 구성 하는 서버의:** 컴퓨터 및 사용자 모두에 대 한 그룹 정책에서 인증서 자동 등록을 사용 하도록 설정 하 고, VPN 사용자 그룹, VPN 서버 그룹 및 NPS 서버 그룹 만들기 및 각 그룹에 구성원을 추가 합니다.
- **Active Directory 인증서 서버 CA에서:** 사용자 인증, VPN 서버 인증과 NPS 서버 인증 인증서 템플릿을 만듭니다.
- **도메인에 가입 된 Windows 10 클라이언트에:** 등록 하 고 사용자 인증서의 유효성을 검사 합니다.

## [3단계. Always On VPN에 대한 원격 액세스 서버 구성](vpn-deploy-ras.md)

이 단계에서 원격 액세스 VPN IKEv2 VPN 연결을 허용 하 고 다른 VPN 프로토콜에서 연결을 거부 승인 된 VPN 클라이언트를 연결 하는 데 발급의 IP 주소에 대 한 고정 IP 주소 풀 할당을 구성할 수 있습니다.

RAS를 구성 하려면 다음 작업을 수행 해야 합니다.
- 등록 하 고 VPN 서버 인증서의 유효성을 검사합니다
- 설치 및 원격 액세스 VPN 구성

## [4단계. NPS 서버 설치 및 구성](vpn-deploy-nps.md)

이 단계에서 Windows PowerShell 또는 서버 관리자 추가 역할 및 기능 마법사 중 하나를 사용 하 여 네트워크 정책 서버 (NPS)를 설치 합니다. 모든 인증, 권한 및 VPN 서버에서 받는 연결 요청에 대 한 계정 의무를 처리 하는 NPS 구성할 수도 있습니다.

NPS를 구성 하려면 다음 작업을 수행 해야 합니다.
- Active Directory에서 NPS 서버 등록
- RADIUS NPS 서버에 대 한 계정 구성
- RADIUS 클라이언트 NPS에서 VPN 서버를 추가 합니다.
- NPS에서 네트워크 정책 구성
- NPS 서버 인증서 자동 등록

## [5단계. DNS 및 방화벽 설정에 대 한 VPN에 항상 구성](vpn-deploy-dns-firewall.md)

DNS 및 방화벽 구성이 단계에서 설정 합니다. 원격 VPN 클라이언트에 연결할 때 사용 내부 클라이언트를 사용 하는 동일한 DNS 서버 이름을 내부 워크스테이션의 나머지 부분과 동일한 방식으로 확인할 수 있도록 합니다. 

## [6단계. Windows 10 클라이언트 Always On VPN 연결 구성](vpn-deploy-client-vpn-connections.md)

이 단계에서 VPN 연결을 사용 하 여 해당 인프라와 통신 하도록 Windows10 클라이언트 컴퓨터를 구성 합니다. Windows PowerShell, System Center Configuration Manager 및 Intune 등 Windows10 VPN 클라이언트를 구성 하려면 여러 가지 기술을 사용할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하는 XML VPN 프로필이 필요 합니다. 

## [7단계. (선택 사항) VPN 연결에 대 한 조건부 액세스 구성](../../ad-ca-vpn-connectivity-windows10.md) 
이 선택적 단계에서는 어떻게 권한이 부여 된 VPN을 미세 조정할 수 사용자 리소스에 액세스 합니다. VPN 연결에 대 한 조건부 액세스를 Azure AD 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 모든 Azure AD에 대 한 액세스 규칙을 만들 수 있는 정책 기반 평가 엔진 응용 프로그램을 연결 합니다. 자세한 내용은 [조건부 액세스 Azure Active Directory (Azure AD)를](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)참조 하세요.


## 다음 단계
1 [단계입니다. Always On VPN 배포 계획](always-on-vpn-deploy-planning.md): 사용 하 여 VPN 서버 계획 이라면 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 합니다. 후 적절 한 계획을 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다.  



---