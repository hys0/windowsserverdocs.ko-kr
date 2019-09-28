---
title: 원격 데스크톱 서비스 아키텍처
description: RDS에 대한 아키텍처 다이어그램
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 02/10/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f73bb0a-ce98-48a4-9d9f-cf7438936ca1
author: lizap
manager: dongill
ms.openlocfilehash: 7cd46cadf5ed5424e50556ee0c91a80804108113
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404221"
---
# <a name="remote-desktop-services-architecture"></a>원격 데스크톱 서비스 아키텍처

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

다음은 최종 사용자를 위해 Windows 앱 및 데스크톱을 호스팅하는 원격 데스크톱 서비스를 구현하기 위한 다양한 구성입니다.

>[!NOTE]
> 아래 아키텍처 다이어그램은 Azure에서의 RDS 사용을 보여줍니다. 하지만 온-프레미스 및 기타 클라우드에 원격 데스크톱 서비스를 배포할 수 있습니다. 이러한 다이어그램은 주로 RDS 역할이 어떻게 배치되고 다른 서비스를 사용하는지를 설명하기 위한 것입니다.

## <a name="standard-rds-deployment-architectures"></a>표준 RDS 배포 아키텍처

원격 데스크톱 서비스에는 두 가지 표준 아키텍처가 있습니다.
-   기본 배포 – 여기에는 완전히 효과적인 RDS 환경을 만들기 위한 최소 서버 수가 포함됩니다.
-   고가용성 배포 – 여기에는 RDS 환경에 가장 높은 가동 시간을 보장하는 데 필요한 모든 구성 요소가 포함되어 있습니다.

### <a name="basic-deployment"></a>기본 배포

![기본 RDS 배포](./media/basic-rds.png)

### <a name="highly-available-deployment"></a>고가용성 배포

![고가용성 RDS 배포](./media/ha-rds.png)

## <a name="rds-architectures-with-unique-azure-paas-roles"></a>고유한 Azure PaaS 역할을 사용한 RDS 아키텍처

표준 RDS 배포 아키텍처가 대부분의 시나리오에 적합하지만, Azure는 계속해서 고객 가치를 높이는 자사 PaaS 솔루션에 투자하고 있습니다. 다음은 RDS를 사용한 통합 방법을 보여주는 일부 아키텍처입니다.

### <a name="rds-deployment-with-azure-ad-domain-services"></a>Azure AD Domain Services를 사용한 RDS 배포

위의 두 표준 아키텍처 다이어그램은 Windows Server VM에 배포된 기존 AD(Active Directory)를 기반으로 합니다. 그러나 기존 AD가 없고 Office365와 같은 서비스를 통한 Azure AD 테넌트만 있지만, 여전히 RDS를 활용하려는 경우 [Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview)를 사용하여 Azure AD 테넌트에 존재하는 것과 동일한 사용자를 사용하는 Azure IaaS 환경에서 완전 관리형 도메인을 만들 수 있습니다. 그러면 수동으로 사용자를 동기화하고 더 많은 가상 머신을 관리하는 복잡성이 제거됩니다. Azure AD Domain Services는 기본 배포 또는 고가용성 배포 중 하나로 작동할 수 있습니다.

![Azure AD 및 RDS 배포](./media/aadds-rds.png)

### <a name="rds-deployment-with-azure-ad-application-proxy"></a>Azure AD 애플리케이션 프록시를 사용한 RDS 배포

위의 두 표준 아키텍처 다이어그램은 RDS 시스템의 인터넷 접점 진입점으로 RD 웹/게이트웨이 서버를 사용합니다. 일부 환경에서는 관리자가 자체 서버를 경계에서 제거하고, 대신 역방향 프록시 기술을 통해 추가 보안을 제공하는 기술을 사용하는 것을 선호합니다. [Azure AD 애플리케이션 프록시](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) PaaS 역할이 이 시나리오에 적합합니다.

지원되는 구성과 이 설정을 만드는 방법은 [Azure AD 애플리케이션 프록시를 사용하여 원격 데스크톱을 게시하는](/azure/active-directory/application-proxy-publish-remote-desktop) 방법을 참조하세요.

![Azure AD 애플리케이션 프록시를 사용한 RDS](./media/aadappproxy-rds.png)
