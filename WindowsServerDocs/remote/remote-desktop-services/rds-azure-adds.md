---
title: Azure AD Domain Services 및 원격 데스크톱 서비스
description: RDS 배포에 Azure AD Domain Services를 통합 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/02/2017
ms.tgt_pltfrm: na
ms.topic: article
author: christianmontoya
ms.localizationpriority: medium
ms.openlocfilehash: 8b1baf642ffa3c8e8a0a2cfc70d2f49b58f208b3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446585"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>RDS 배포에 Azure AD Domain Services 통합

사용할 수 있습니다 [Azure AD Domain Services](/azure/active-directory-domain-services/active-directory-ds-overview) (Azure AD DS)에서 Windows Server Active Directory 대신 원격 데스크톱 서비스 배포 합니다. Azure AD DS를 사용 하면 클래식 Windows 워크 로드를 사용 하 여 기존 Azure AD id를 사용할 수 있습니다.

Azure AD DS를 사용 하 여 다음을 수행할 수 있습니다. 
- The-클라우드 조직에 대 한 로컬 도메인을 사용 하 여 Azure 환경을 만듭니다. 
- 사이트 간 VPN 또는 ExpressRoute를 만들 필요 없이 온-프레미스 및 온라인 환경에 대해 사용 되는 동일한 id를 사용 하 여 격리 된 Azure 환경을 만듭니다. 

원격 데스크톱 배포에 Azure AD DS 통합을 완료 하면 아키텍처 다음과 같이 표시 됩니다.

![Azure AD DS 사용 하 여 RDS를 보여 주는 아키텍처 다이어그램](media/aadds-rds.png)

이 아키텍처를 다른 RDS 배포 시나리오를 사용 하 여 비교 하는 방법을 보려면, 체크 아웃 [원격 데스크톱 서비스 아키텍처](desktop-hosting-logical-architecture.md)합니다.

Azure AD DS를 더 잘 이해을 가져오려면 체크 아웃 합니다 [Azure AD DS 개요](/azure/active-directory-domain-services/active-directory-ds-overview) 및 [Azure AD DS 사용 사례에 적합 한지 결정 하는 방법을](/azure/active-directory-domain-services/active-directory-ds-comparison)합니다.

다음 정보를 사용 하 여 rds.를 사용 하 여 Azure AD DS 배포

## <a name="prerequisites"></a>사전 요구 사항

RDS 배포에서 사용 하기 위해 Azure AD에서 id를 상태로 전환 하려면 먼저 [사용자 id에 대 한 해시 된 암호를 저장 하려면 Azure AD 구성](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync)합니다. The-클라우드 조직이 자신의 디렉터리에 추가로 변경할 필요가 없습니다. 그러나 온-프레미스 조직 암호 해시 동기화 되어 일부 조직에서는 허용 하지 않을 수 있는 Azure AD에 저장을 허용 해야 합니다. 사용자가이 구성을 변경한 후 암호를 다시 설정 해야 합니다.

## <a name="deploy-azure-ad-ds-and-rds"></a>Azure AD DS 및 RDS를 배포 합니다. 
다음 단계를 사용 하 여 Azure AD DS 및 rds. 배포

1. 사용 하도록 설정 [Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started)합니다. 연결 된 문서는 다음을 수행 하는 참고 합니다.
   - 적절 한 만들 안내 도메인 관리에 대 한 Azure AD 그룹입니다.
   - 강제로 사용자가 해당 계정을 Azure AD DS와 함께 작동할 수 있도록 암호를 변경 해야 하는 경우를 강조 표시 합니다.
   
2. Rds. 설정 Azure 템플릿을 사용 하거나 수동으로 RDS를 배포 합니다.
   - 사용 된 [기존 AD 템플릿](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)합니다. 다음을 사용자 지정할 수 있는지 확인 합니다.
   
     - **설정**
       - **리소스 그룹**: RDS 리소스를 만들려는 리소스 그룹을 사용 합니다.
         > [!NOTE] 
         > 지금 Azure resource manager 가상 네트워크의가 있는 동일한 리소스 그룹 이어야 합니다.

       - **Dns 레이블 접두사**: 입력 URL RD 웹 액세스를 사용 하는 사용자가 있습니다.
       - **Ad 도메인 이름**: Azure AD 인스턴스, 예: "contoso.onmicrosoft.com" 또는 "contoso.com"의 전체 이름을 입력 합니다.
       - **Ad Vnet-name** 하 고 **Ad 서브넷 이름**: Azure resource manager 가상 네트워크를 만들 때 사용한 동일한 값을 입력 합니다. RDS 리소스를 연결할 서브넷입니다.
       - **관리자 사용자 이름** 하 고 **관리자 암호**: 멤버인 관리 사용자에 대 한 자격 증명을 입력 합니다 **AAD DC Administrators** Azure AD의 그룹입니다.
   
     - **템플릿**
        - 모든 속성을 제거 **dnsServers**: 선택한 후 **템플릿 편집** Azure 빠른 시작 템플릿 페이지에서 "dnsServers"를 검색 하 고 속성을 제거 합니다. 

           제거 하기 전에 예를 들어 합니다 **dnsServers** 속성:
      
           ![DnsSettings 속성을 사용 하 여 azure 빠른 시작 템플릿](media/rds-remove-dnssettings-before.png)

           및 다음 속성을 제거한 후 같은 파일은:

           ![Azure 빠른 시작 템플릿과 dnsSettings 속성 제거](media/rds-remove-dnssettings-after.png)
   
   - [RDS를 수동으로 배포](rds-deploy-infrastructure.md)합니다. 

