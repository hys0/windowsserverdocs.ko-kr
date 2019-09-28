---
title: RDS - Azure 서비스와 통합
description: RDS를 Azure 배포로 Azure를 RDS 배포로 통합하는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/18/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.openlocfilehash: ba53a16c75f205c329bf5e388cf52dd2bf40bb91
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387396"
---
# <a name="remote-desktop-services---integrating-with-azure-services"></a>원격 데스크톱 서비스 -  Azure 서비스와 통합

Windows Server 2016은 Microsoft Azure에서 제공하는 유연하고 확장 가능한 서비스로 원격 데스크톱 서비스를 통해 데스크톱과 앱의 강력한 보안 전달을 결합합니다. Azure 서비스로 RDS를 배포하여 온-프레미스 서버에 대한 인프라 유지 관리 비용을 절감하고, 고가용성을 보장하도록 Azure 서비스를 사용하여 안정성을 높이고, 다단계 인증을 사용하여 보안을 향상시키며, RDS의 리소스에 액세스하는 데 기존 ID를 사용하여 사용자의 환경을 개선할 수 있습니다.

다음 정보를 사용하여 Azure를 원격 데스크톱 배포로 통합합니다.

- [RDS를 통해 다단계 인증을 사용하는 방법 알아보기](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)
- [RDS 배포에 Azure AD Domain Services 통합](rds-azure-adds.md)
- [Azure AD 애플리케이션 프록시를 사용하여 원격 데스크톱 게시](/azure/active-directory/application-proxy-publish-remote-desktop)

이러한 서비스가 원격 데스크톱 배포의 아키텍처를 단순화하는 방법을 보려면 [고유한 Azure PaaS 역할을 사용한 RDS 아키텍처](desktop-hosting-logical-architecture.md#rds-architectures-with-unique-azure-paas-roles)를 확인하세요.