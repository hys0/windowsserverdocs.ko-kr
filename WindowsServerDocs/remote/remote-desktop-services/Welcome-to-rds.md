---
title: Windows Server 2016에서 원격 데스크톱 서비스 시작
description: 원격 데스크톱 서비스의 개요를 제공합니다.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 46a04905d5247ae940ca900297171d1112cf936b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404202"
---
# <a name="welcome-to-remote-desktop-services"></a>원격 데스크톱 서비스 시작 

RDS(원격 데스크톱 서비스)는 개별 가상화 애플리케이션 제공, 안전한 모바일 및 원격 데스크톱 액세스 제공, 최종 사용자에게 클라우드에서 애플리케이션 및 데스크톱을 실행할 수 있는 기능 제공 등 모든 최종 고객의 요구에 맞는 가상화 솔루션을 빌드하는 데 필요한 플랫폼입니다.

![원격 데스크톱 서비스 개요](./media/rds-overview.png)

RDS는 온-프레미스 배포를 위한 Windows Server 2016, 클라우드 배포를 위한 Microsoft Azure 및 강력한 파트너 솔루션 배열을 비롯한 다양한 배포 옵션을 통해 배포 유연성, 비용 효율성 및 확장성을 제공합니다.

환경 및 기본 설정에 따라 세션 기반 가상화를 위한 RDS 솔루션을 VDI(가상 데스크톱 인프라)로 설정하거나 다음 두 가지 기능을 함께 설정할 수 있습니다.

- **세션 기반 가상화**: Windows Server의 컴퓨팅 능력을 활용하여 사용자의 일상적인 워크로드를 구동하기 위한 비용 효율적인 다중 세션 환경을 제공합니다.
- **VDI**: Windows 클라이언트를 활용하여 사용자들이 Windows 데스크톱 환경에서 기대하게 되는 고성능, 앱 호환성 및 친숙함을 제공합니다.

이러한 가상화 환경에서 사용자에게 게시하는 내용에 대한 추가적인 유연성을 제공합니다.

- **데스크톱**: 사용자에게 설치 및 관리하는 다양한 애플리케이션으로 전체 데스크톱 환경을 제공합니다. 이러한 컴퓨터를 기본 워크스테이션으로 사용하거나 MultiPoint Services와 같이 씬 클라이언트의 사용자에게 이상적입니다.
- **RemoteApps**: 가상화된 머신에서 호스팅/실행되지만 로컬 애플리케이션처럼 사용자의 데스크톱에서 실행되는 것처럼 표시되는 개별 애플리케이션을 지정합니다. 앱에는 자체 작업 표시줄 항목이 있으며 크기 조정이 가능하고 모니터 간에 이동할 수 있습니다. 사용자가 자신의 데스크톱에서 작업하고 사용자 지정할 수 있도록 하는 동시에 안전한 원격 환경에서 주요 애플리케이션을 배포하고 관리하는 데 이상적입니다.

비용 효율성이 중요하고 세션 기반 가상화 환경에 전체 데스크톱을 배포하여 이점을 확장하려는 환경의 경우 [MultiPoint Services](../multipoint-services/multipoint-services.md)를 사용하여 최상의 가치를 제공할 수 있습니다. 

이러한 옵션과 구성을 통해 사용자에게 필요한 데스크톱과 애플리케이션을 원격, 보안 및 비용 효율적인 방식으로 유연하게 배포할 수 있습니다.

## <a name="next-steps"></a>다음 단계

다음은 RDS를 더 잘 이해하고 사용자 자신의 환경 배포를 시작하는 데 도움이 되는 몇 가지 단계입니다.
-   다양한 Windows 및 Windows Server 버전을 사용하는 RDS에 대해 [지원되는 구성](rds-supported-config.md)을 이해합니다.
-   고가용성 및 다중 요인 인증과 같은 다양한 요구 사항을 수용할 수 있는 RDS 환경을 [계획 및 설계](rds-plan-and-design.md)합니다.
-   원하는 환경에 가장 적합한 [원격 데스크톱 서비스 아키텍처 모델](desktop-hosting-logical-architecture.md)을 검토합니다.
-   [ARM 및 Azure Marketplace를 사용하여 RDS 환경 배포](rds-in-azure.md)를 시작합니다.
