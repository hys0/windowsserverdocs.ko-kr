---
title: 원격 데스크톱 서비스 아키텍처
description: RDS에 대 한 아키텍처 다이어그램
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ba597318cdaf1d4659a72905eeb4e252c9020e49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887874"
---
# <a name="remote-desktop-services-architecture"></a>원격 데스크톱 서비스 아키텍처

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음은 Windows 앱을 호스트 하는 원격 데스크톱 서비스 및 최종 사용자에 대 한 데스크톱 배포에 대 한 다양 한 구성입니다.

>[!NOTE]
> 아래 아키텍처 다이어그램은 Azure에서 RDS를 사용 하 여 보여 줍니다. 그러나 온-프레미스 원격 데스크톱 서비스를 배포할 수 있습니다 및 기타 클라우드에 있습니다. 이러한 다이어그램은 RDS 역할에 함께 배치 됩니다 및 기타 서비스를 사용 하는 방법을 보여 주기 위해 주로 사용 됩니다.

## <a name="standard-rds-deployment-architectures"></a>표준 RDS 배포 아키텍처

원격 데스크톱 서비스에는 두 가지 표준 아키텍처에 있습니다.
-   기본 배포 –이 포함 된 완벽 하 게 효과적인 RDS 환경을 만들려면 서버의 최소 수
-   항상 사용 가능한 배포 – RDS 환경에 대 한 가장 높은 보장된 작동 하도록 하는 모든 필수 구성 요소가 포함

### <a name="basic-deployment"></a>기본 배포

![기본 RDS 배포](./media/basic-rds.png)

### <a name="highly-available-deployment"></a>항상 사용 가능한 배포

![항상 사용 가능한 RDS 배포](./media/ha-rds.png)

## <a name="rds-architectures-with-unique-azure-paas-roles"></a>고유한 Azure PaaS 역할을 사용 하 여 RDS 아키텍처

표준 RDS 배포 아키텍처에는 대부분의 시나리오에 맞춰, 하지만 Azure 고객 가치를 향상 자사 PaaS 솔루션에 투자를 계속 합니다. 다음은 rds.를 사용 하 여 통합 하는 방법을 보여 주는 일부 아키텍처

### <a name="rds-deployment-with-azure-ad-domain-services"></a>Azure AD Domain Services 사용 하 여 RDS 배포

위의 두 표준 아키텍처 다이어그램에는 기존 AD (Active Directory)는 Windows Server VM에 배포에 따라 달라 집니다. 그러나 기존 ad 및 Azure AD 테 넌 트를 하나만 없는 경우-예: office 365 서비스를 통해-RDS 활용 하려고 하지만 사용할 수 있습니다 [Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) 하 여 Azure IaaS에서 완전히 관리 되는 도메인을 만들려면 Azure AD 테 넌 트에 존재 하는 동일한 사용자를 사용 하는 환경입니다. 수동으로 사용자를 동기화 하 고 더 많은 가상 컴퓨터 관리의 복잡성을 제거 합니다. Azure AD Domain Services는 두 배포에서 작업할 수 있습니다: 기본 또는 고가용성입니다.

![Azure AD 및 RDS 배포](./media/aadds-rds.png)

### <a name="rds-deployment-with-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시를 사용 하 여 RDS 배포

위의 두 표준 아키텍처 다이어그램 RDS 체제로 인터넷 진입점으로 RD 웹/게이트웨이 서버를 사용합니다. 일부 환경에서는 관리자 하려는 경계에서 고유한 서버를 제거 하 고 기술도 역방향 프록시 기술을 통해 추가 보안을 제공 하는 대신 사용 합니다. 합니다 [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) PaaS 역할이이 시나리오를 사용 하 여 원활 하 게 적합 합니다.

지원 되는 구성과이 설치 프로그램을 만드는 방법에 대 한 참조 하는 방법 [Azure AD 응용 프로그램 프록시를 사용 하 여 원격 데스크톱 게시](/azure/active-directory/application-proxy-publish-remote-desktop)합니다.

![Azure AD 응용 프로그램 프록시를 사용 하 여 RDS](./media/aadappproxy-rds.png)
