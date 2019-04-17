---
title: Azure AD 도메인 서비스 및 원격 데스크톱 서비스
description: RDS 배포에 Azure AD 도메인 서비스를 통합 하는 방법에 알아봅니다.
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
ms.openlocfilehash: e60cf70f1f91ad87046bedf024fe9afc459075b6
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1614520"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>RDS 배포와 함께 Azure AD 도메인 서비스 통합

Windows Server Active Directory를 대신 하 여 원격 데스크톱 서비스 배포에서 [Azure AD 도메인 서비스](/azure/active-directory-domain-services/active-directory-ds-overview) (Azure AD DS)를 사용할 수 있습니다. Azure AD DS 클래식 Windows 작업 부하를 사용 하 여 기존 Azure AD id를 사용할 수 있습니다.

Azure AD DS을 사용 하면 다음과 같은 작업을 수행할 수 있습니다. 
- 태어난에서-클라우드 조직에 대 한 로컬 도메인과 Azure 환경을 만듭니다. 
- 사이트 마다 VPN 또는 ExpressRoute 만들 필요 없이 온-프레미스 및 온라인 환경에 사용 되는 동일한 id를 가진 격리 된 Azure 환경을 만듭니다. 

확인이 끝나면 원격 데스크톱 배포에 Azure AD DS 통합 (영문)의 아키텍처는 다음과 같습니다.

![Azure AD DS와 RDS를 표시 하는 아키텍처 다이어그램](media/aadds-rds.png)

이 아키텍처 다른 RDS 배포 시나리오와 비교 하는 방법을 보려면, [원격 데스크톱 서비스 아키텍처](desktop-hosting-logical-architecture.md)를 체크아웃 합니다.

Azure AD DS를 자세하게 파악 하려면 [Azure AD DS 개요](/azure/active-directory-domain-services/active-directory-ds-overview) 및 [Azure AD DS 사용 사례에 적합 한지 결정 하는 방법](/azure/active-directory-domain-services/active-directory-ds-comparison)을 체크아웃 합니다.

다음 정보를 사용 하 여 rds.와 Azure AD DS를 배포 하려면

## <a name="prerequisites"></a>사전 요구 사항

전에 [사용자의 id에 대 한 해시 된 암호를 저장 하려면 Azure AD를 구성](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync)하는 RDS 배포에서 사용 하 여 Azure AD에서 id를 가져올 수 있습니다. 태어난에서-클라우드 조직에서는 해당 디렉터리;에 추가로 변경할 필요가 없습니다. 그러나 온-프레미스 조직에 동기화 하 고 일부 조직에서는 허용 되지 않을 수 있습니다는 Azure AD에 저장 된 암호 해시를 허용 해야 합니다. 사용자가이 구성을 변경한 후 자신의 암호를 다시 설정 해야 합니다.

## <a name="deploy-azure-ad-ds-and-rds"></a>Azure AD DS 및 RDS를 배포 합니다. 
다음 단계를 사용 하 여 Azure AD DS 및 rds.를 배포 하려면

1. [Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started)를 사용 하도록 설정 합니다. 연결 된 문서는 다음을 수행 하는 참고:
   - 적절 한 만드는 과정을 설명 도메인 관리를 위한 Azure AD 그룹입니다.
   - 강조 강제로 사용자가 자신의 계정 Azure AD DS 작업할 수 있도록 암호를 변경 하도록 할 수 있습니다.
   
2. Rds. 설정 Azure 서식 파일을 사용 하거나 RDS를 수동으로 배포 수 있습니다.
   - [기존 AD 서식 파일](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)을 사용 합니다. 다음을 사용자 지정할 수 있는지 확인 합니다.
   
      - **Settings**
         - **자원 그룹**: RDS 리소스 만들려는 자원 그룹을 사용 합니다.
         > [!NOTE] 
         > 이제이를 사용 해야 동일한 리소스 그룹 Azure 리소스 관리자 가상 네트워크 존재 하는 위치를 마우스 오른쪽 단추로 합니다.

         - **Dns 레이블 접두사**: URL을 입력 RD 웹 액세스를 사용 하 여 사용자가 원하는 합니다.
         - **Ad 도메인 이름**: Azure AD 인스턴스를 "contoso.onmicrosoft.com 형식" 또는 "contoso.com" 등의 전체 이름을 입력 합니다.
         - **Ad Vnet 이름** 및 **광고 서브넷 이름**: Azure 리소스 관리자 가상 네트워크를 만들 때 사용한 동일한 값을 입력 합니다. RDS 리소스에서 연결 하는 서브넷입니다.
         - **관리자의 사용자 이름** 및 **암호 관리**: Azure AD에 **AAD DC Administrators** 그룹의 구성원 인 관리자 사용자 자격 증명을 입력 합니다.
   
      - **서식 파일**
         - **DnsServers**의 속성을 모두 제거: Azure 빠른 시작 서식 파일 페이지에서 **서식 파일 편집** 를 선택한 후 "dnsServers"를 검색 하 고 속성을 제거 합니다. 

            **DnsServers** 속성 제거 하기 전에 예:
      
            ![DnsSettings 속성과 함께 azure 빠른 시작 서식 파일](media/rds-remove-dnssettings-before.png)

            그리고 동일한 파일의 속성을 제거한 후 합니다.

            ![제거 dnsSettings 속성과 함께 azure 빠른 시작 서식 파일](media/rds-remove-dnssettings-after.png)
   
   - [배포 RDS 수동으로](rds-deploy-infrastructure.md)합니다. 

