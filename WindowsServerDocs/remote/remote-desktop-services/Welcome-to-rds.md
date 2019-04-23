---
title: Windows Server 2016의에서 시작에 원격 데스크톱 서비스
description: 원격 데스크톱 서비스의 개요를 제공합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 02/22/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52b9e09f-39e0-41a9-9d3b-4d5f4eacf3e0
author: christianmontoya
manager: scottman
ms.localizationpriority: medium
ms.openlocfilehash: cd00f92254f9e55f83442f5e68e344e0aa7579a2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855504"
---
# <a name="welcome-to-remote-desktop-services"></a>원격 데스크톱 서비스 시작 

원격 데스크톱 서비스 (RDS)는 선택한 개별 가상화 된 응용 프로그램을 제공, 안전한 모바일 및 원격 데스크톱 액세스를 제공 하 고 최종 사용자에 게 제공을 포함 하 여 모든 최종 고객 요구에 대 한 가상화 솔루션을 빌드하기 위한 플랫폼을 클라우드에서 응용 프로그램과 데스크톱을 실행 하는 기능.

![원격 데스크톱 서비스 개요](.\media\rds-overview.png)

RDS 배포 유연성, 비용 효율성 및 확장성을 제공-다양 한 Windows Server 2016을 포함 하 여 온-프레미스 배포를 클라우드 배포에 대 한 Microsoft Azure 및 파트너의 강력한 배열에 대 한 배포 옵션을 통해 모든 배달 솔루션입니다.

환경 및 기본 설정에 따라 가상 데스크톱 인프라 (VDI) 또는 둘의 조합으로 세션 기반 가상화를 위해 RDS 솔루션을 설정할 수 있습니다.

- **세션 기반 가상화**: 사용자의 일상적인 작업을 구동 하는 비용 효율적인 다중 세션 환경을 제공 하기 위해 Windows Server의 계산 능력을 활용 합니다.
- **VDI**: 높은 성능, 응용 프로그램 호환성 및 사용자가 해당 Windows 데스크톱 환경 기대 하는 경험을 제공 하기 위해 Windows 클라이언트를 활용 합니다.

이러한 가상화 환경 내에서 사용자에 게 게시할의 유연성 강화 해야 합니다.

- **데스크톱**: 사용자에 게 다양 한 설치 및 관리 하는 응용 프로그램을 사용 하 여 전체 데스크톱 환경을 제공 합니다. 사용자가 자신의 기본 워크스테이션으로 이러한 컴퓨터에서 사용 하는 하거나는에서 들어오는 씬 클라이언트와 같은 MultiPoint 서비스에 적합 합니다.
- **RemoteApps**: 가상화 된 컴퓨터의 호스트/실행 중인 개별 응용 프로그램을 지정 하지만 로컬 응용 프로그램과 같은 사용자의 데스크톱에서 실행 하는 것 처럼 나타납니다. 앱 자체 작업 표시줄 항목 크기를 조정할 고의 모니터로 이동 될 수 있습니다. 작업 하 고 자신의 데스크톱을 사용자 지정 하도록 허용 하는 동안 안전 하 고 원격 환경의 주요 응용 프로그램 관리 및 배포에 적합 합니다.

여기서 비용 효율성은 중요 하 고 세션 기반 가상화 환경에서 전체 데스크톱을 배포 하는 이점을 확장 하려는 환경에서는 사용할 수 있습니다 [MultiPoint 서비스](../multipoint-services/multipoint-services.md) 최상의 가치를 제공 합니다. 

이러한 옵션 및 구성을 사용 하 여 데스크톱 및 원격, 보안 및 비용 효율적인 방식으로 사용자에 게 필요한 응용 프로그램을 배포할을 해야 합니다.

## <a name="next-steps"></a>다음 단계

RDS의 더 잘 이해 하 고도 사용자 환경의 배포를 시작할 수 있도록 다음 단계는 다음과 같습니다.
-   이해를 [지원 되는 구성](rds-supported-config.md) 다양 한 Windows 및 Windows Server 버전을 사용 하 여 RDS에 대 한
-   [계획 및 디자인](rds-plan-and-design.md) 고가용성 및 다단계 인증 등의 다양 한 요구 사항에 맞게 RDS 환경입니다.
-   검토 합니다 [원격 데스크톱 서비스 아키텍처 모델](desktop-hosting-logical-architecture.md) 원하는 환경에는 가장 적합 합니다.
-   시작할 [ARM에서 Azure Marketplace와 RDS 환경 배포](rds-in-azure.md)합니다.
