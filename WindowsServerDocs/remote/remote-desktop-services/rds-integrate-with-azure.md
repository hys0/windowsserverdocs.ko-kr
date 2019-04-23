---
title: RDS-Azure 서비스와 통합
description: RDS 배포에 Azure 배포 및 Azure에 RDS를 통합 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/18/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.openlocfilehash: e582612496591356ed96b34522333d0e8bf34093
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879604"
---
# <a name="remote-desktop-services---integrating-with-azure-services"></a>원격 데스크톱 서비스-Azure 서비스와 통합

Windows Server 2016 데스크톱 및 Microsoft Azure에서 제공 하는 유연 하 고 확장 가능한 서비스를 사용 하 여 원격 데스크톱 서비스를 통해 앱의 강력한 보안 배달을 결합 합니다. 온-프레미스 서버에 대 한 인프라 유지 관리 비용을 줄이고, 높은 가용성을 보장 하려면 multi-factor Authentication을 사용 하 여 보안을 향상 시킬 Azure 서비스를 사용 하 여 안정성을 높이 데 Azure 서비스를 사용 하 여 RDS를 배포 하 고 개선 프로그램 rds.의 리소스에 액세스 하려면 기존 id를 사용 하 여 사용자 환경

다음 정보를 사용 하 여 Azure 원격 데스크톱 배포를 통합 하려고 합니다.

- [RDS를 사용 하 여 multi-factor Authentication을 사용 하는 방법 알아보기](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)
- [RDS 배포를 사용 하 여 Azure AD Domain Services 통합](rds-azure-adds.md)
- [Azure AD 응용 프로그램 프록시를 사용 하 여 원격 데스크톱 게시](/azure/active-directory/application-proxy-publish-remote-desktop)

이러한 서비스에 원격 데스크톱 배포의 아키텍처를 단순화 하는 방법을 보려면, 체크 아웃 [고유한 Azure PaaS 역할을 사용 하 여 RDS 아키텍처](desktop-hosting-logical-architecture.md#rds-architectures-with-unique-azure-paas-roles)합니다.