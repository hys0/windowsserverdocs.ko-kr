---
title: Azure AD Domain Services 및 원격 데스크톱 서비스
description: RDS 배포에 Azure AD Domain Services를 통합하는 방법을 알아봅니다.
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
ms.openlocfilehash: 511aee3ea5be7e5c70c75cbc4d1febe1ec58dd97
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871073"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>RDS 배포에 Azure AD Domain Services 통합

원격 데스크톱 서비스 배포에서 [Azure AD DS(Azure AD Domain Services)](/azure/active-directory-domain-services/active-directory-ds-overview)를 Windows Server Active Directory 대신 사용할 수 있습니다. Azure AD DS를 통해 기존 Azure AD ID를 클래식 Windows 워크로드에 사용할 수 있습니다.

Azure AD DS를 사용하여 다음을 수행할 수 있습니다. 
- 클라우드를 기반으로 한 조직에 대한 로컬 도메인을 사용하여 Azure 환경을 만듭니다. 
- 사이트 간 VPN 또는 ExpressRoute를 만들 필요 없이 온-프레미스 및 온라인 환경에 사용되는 동일한 ID로 격리된 Azure 환경을 만듭니다. 

원격 데스크톱 배포에 Azure AD DS를 통합하는 작업을 마치면 아키텍처는 다음과 같습니다.

![Azure AD DS와 함께 RDS를 보여주는 아키텍처 다이어그램](media/aadds-rds.png)

이 아키텍처를 다른 RDS 배포 시나리오와 비교하는 방법을 보려면 [원격 데스크톱 서비스 아키텍처](desktop-hosting-logical-architecture.md)를 확인하세요.

Azure AD DS를 더 잘 이해하려면 [Azure AD DS 개요](/azure/active-directory-domain-services/active-directory-ds-overview) 및 [사용자 사례에 적합한 Azure AD DS를 결정하는 방법](/azure/active-directory-domain-services/active-directory-ds-comparison)을 확인하세요.

다음 정보를 사용하여 RDS와 함께 Azure AD DS를 배포합니다.

## <a name="prerequisites"></a>필수 구성 요소

RDS 배포에서 사용할 Azure AD의 ID를 가져오기 전에 [사용자 ID에 대한 해시된 암호를 저장하도록 Azure AD를 구성](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync)합니다. 클라우드를 기반으로 하는 조직에서는 디렉터리에서 추가로 변경할 필요가 없지만, 온-프레미스 조직에서는 암호 해시를 동기화하여 Azure AD에 저장할 수 있도록 허용해야 하며, 이는 일부 조직에서는 허용되지 않을 수 있습니다. 사용자는 이 구성 변경을 수행한 후 암호를 다시 설정해야 합니다.

## <a name="deploy-azure-ad-ds-and-rds"></a>Azure AD DS 및 RDS 배포 
다음 단계를 사용하여 Azure AD DS 및 RDS를 배포합니다.

1. [Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started)를 사용하도록 설정합니다. 연결된 문서에서는 다음을 수행합니다.
   - 도메인 관리를 위한 적절한 Azure AD 그룹을 만드는 과정을 진행합니다.
   - 계정이 Azure AD DS와 작동할 수 있도록 사용자에게 암호를 변경하도록 해야 하는 경우 중요합니다.
   
2. RDS를 설정합니다. Azure 템플릿을 사용하거나 수동으로 RDS를 배포할 수 있습니다.
   - [기존 AD 템플릿](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)을 사용합니다. 다음을 사용자 지정해야 합니다.
   
     - **설정**
       - **리소스 그룹**: RDS 리소스를 만들려는 리소스 그룹을 사용합니다.
         > [!NOTE] 
         > 현재 이는 Azure 리소스 관리자 가상 네트워크가 존재하는 것과 동일한 리소스 그룹이어야 합니다.

       - **Dns 레이블 접두사**: 사용자가 RD 웹에 액세스하는 데 사용할 URL을 입력합니다.
       - **Ad 도메인 이름**: Azure AD 인스턴스의 전체 이름(예: “contoso.onmicrosoft.com” 또는 “contoso.com”)을 입력합니다.
       - **Ad Vnet 이름** 및 **Ad 서브넷 이름**: Azure 리소스 관리자 가상 네트워크를 만들 때 사용한 것과 동일한 값을 입력합니다. 이는 RDS 리소스를 연결할 서브넷입니다.
       - **관리자 사용자 이름** 및 **관리자 암호**: Azure AD에서 **AAD DC 관리자** 그룹의 멤버인 관리자에 대한 자격 증명을 입력합니다.
   
     - **템플릿**
        - **dnsServers**의 모든 속성 제거: Azure 빠른 시작 템플릿 페이지에서 **템플릿 편집**을 선택한 후 “dnsServers”를 검색하고 속성을 제거합니다. 

           예를 들어 **dnsServers** 속성을 제거하기 전에는 다음과 같습니다.
      
           ![dnsSettings 속성이 있는 Azure 빠른 시작 템플릿](media/rds-remove-dnssettings-before.png)

           또한 속성을 제거한 후의 같은 파일은 다음과 같습니다.

           ![dnsSettings 속성이 제거된 Azure 빠른 시작 템플릿](media/rds-remove-dnssettings-after.png)
   
   - [RDS를 수동으로 배포](rds-deploy-infrastructure.md)합니다. 

