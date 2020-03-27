---
title: 원격 액세스 Always On VPN 마이그레이션 계획
description: DirectAccess에서 Always On VPN으로 마이그레이션하려면 마이그레이션 단계를 결정 하기 위한 적절 한 계획이 필요 합니다 .이를 통해 전체 조직에 영향을 주기 전에 문제를 식별할 수 있습니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 05/29/2018
ms.openlocfilehash: 80a7a8b3ee13a9d9cc99b81ab917f6443147565f
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314947"
---
# <a name="plan-the-directaccess-to-always-on-vpn-migration"></a>DirectAccess-Always On VPN 마이그레이션 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

&#171;[ **이전:** Always On VPN 마이그레이션을 위한 DirectAccess 개요](da-always-on-migration-overview.md)<br>
&#187;[ **다음:** Always On VPN으로 마이그레이션하고 DirectAccess를 서비스 해제 합니다.](da-always-on-migration-deploy.md)


DirectAccess에서 Always On VPN으로 마이그레이션하려면 마이그레이션 단계를 결정 하기 위한 적절 한 계획이 필요 합니다 .이를 통해 전체 조직에 영향을 주기 전에 문제를 식별할 수 있습니다. 마이그레이션의 주된 목표는 사용자가 프로세스 전체에서 사무실에 대 한 원격 연결을 유지 관리 하는 것입니다. 순서를 벗어난 태스크를 수행 하는 경우에는 원격 사용자가 회사 리소스에 액세스할 수 없게 되는 경합 상태가 발생할 수 있습니다. 따라서 DirectAccess에서 Always On VPN으로의 계획 된 side-by-side 마이그레이션을 수행 하는 것이 좋습니다. 자세한 내용은 [ALWAYS ON VPN 마이그레이션 배포](da-always-on-migration-deploy.md) 섹션을 참조 하세요.

이 섹션에서는 마이그레이션, 표준 구성 고려 사항 및 Always On VPN 기능 향상을 위해 사용자를 분리 하는 이점에 대해 설명 합니다. 마이그레이션 계획 단계에는 다음이 포함 됩니다.

1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

## <a name="build-migration-rings"></a>빌드 마이그레이션 링
마이그레이션 링은 Always On VPN 클라이언트 마이그레이션 작업을 여러 단계로 나누는 데 사용 됩니다. 마지막 단계로 이동 하면 프로세스를 잘 테스트 하 고 일관 되 게 해야 합니다.

이 섹션에서는 사용자를 마이그레이션 단계로 구분 하는 한 가지 방법을 제공 하 고 해당 단계를 관리 합니다. 선택한 사용자 단계 분리 방법에 관계 없이 마이그레이션이 완료 되 면 관리를 용이 하 게 하기 위해 단일 VPN 사용자 그룹을 유지 관리 합니다.

>[!NOTE] 
>단어 _단계_ 는 이것이 긴 프로세스 임을 나타내는 것이 아닙니다. 각 단계를 며칠 또는 몇 달 동안 이동 하 든, 병렬 마이그레이션을 활용 하 고 단계별 접근 방법을 사용 하는 것이 좋습니다.

### <a name="benefits-of-dividing-the-migration-effort-into-multiple-phases"></a>마이그레이션 작업을 여러 단계로 나눌 경우의 이점

-   **대량 중단 방지.** 마이그레이션을 단계로 나누면 마이그레이션에 의해 생성 된 문제가 영향을 줄 수 있습니다.

-   **피드백에서 프로세스 또는 통신이 개선 되었습니다.** 사용자가 마이그레이션을 수행 하는 것을 알 수 없는 것이 가장 좋습니다. 그러나 환경이 최적이 아닌 경우 해당 사용의 피드백을 통해 계획을 개선 하 고 향후 문제를 방지할 수 있습니다.

### <a name="tips-for-building-your-migration-ring"></a>마이그레이션 링 빌드에 대 한 팁

-   **원격 사용자를 식별 합니다.** 사용자를 두 개의 버킷으로 분리 하는 것으로 시작 합니다. 즉, 사무실에 자주 들어온 사람 및 그렇지 않은 경우입니다. 마이그레이션 프로세스는 두 그룹에 대해 동일 하지만 원격 클라이언트에서 더 자주 연결 하는 것 보다 더 오래 걸릴 수 있습니다. 각 마이그레이션 단계에는 각 버킷의 구성원이 포함 되어야 합니다.

-  **사용자 우선 순위 지정.** 리더십 및 기타 높은 영향의 사용자는 일반적으로 마이그레이션된 마지막 사용자 중에 있습니다. 그러나 사용자의 우선 순위를 정하는 경우 클라이언트 컴퓨터의 마이그레이션이 실패할 경우 비즈니스 생산성 영향을 고려해 야 합니다. 예를 들어 등급이 1 ~ 3 인 경우 1은 직원이 작업을 수행할 수 없고, 3은 즉각적인 작업이 중단 되지 않는다는 것을 의미 하 고, 내부 LOB (기간 업무) 응용 프로그램을 원격으로 사용 하는 비즈니스 분석가는 1이 고, 클라우드를 사용 하는 영업 사원은 앱은 3입니다.

-   **여러 단계로 각 부서 또는 비즈니스 단위를 마이그레이션합니다.** 전체 부서를 동시에 마이그레이션하지 않는 것이 좋습니다. 문제가 발생 해야 하는 경우 전체 부서에 대 한 원격 작업을 방해 하지 않도록 합니다. 대신 두 단계 이상에서 각 부서 또는 비즈니스 단위를 마이그레이션합니다.

-   **사용자 수를 점차적으로 늘립니다.** 가장 일반적인 마이그레이션 시나리오는 IT 조직의 구성원으로 시작한 후 비즈니스 사용자로 이동 하 고 그 다음에는 리더십 및 기타 높은 영향을 주는 사용자로 이동 합니다. 일반적으로 각 마이그레이션 단계에는 점점 더 많은 사람들이 포함 됩니다. 예를 들어 첫 번째 단계에는 10 명의 사용자가 포함 될 수 있으며 최종 그룹에는 5000 명의 사용자가 포함 될 수 있습니다. 배포를 간소화 하려면 단일 VPN 사용자 보안 그룹을 만들고 해당 단계가 도착할 때 사용자를 추가 합니다. 이러한 방식으로 나중에 구성원을 추가할 수 있는 단일 VPN 사용자 그룹이 생성 됩니다.

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../includes/always-on-vpn-standard-config-considerations-include.md)]


## <a name="next-step"></a>다음 단계

|원하는 경우  |다음을 참조 하세요.  |
|---------|---------|
|Always On VPN으로 마이그레이션 시작     |[ALWAYS ON VPN으로 마이그레이션하고 DirectAccess를 서비스](da-always-on-migration-deploy.md)해제 합니다. DirectAccess에서 Always On VPN으로 마이그레이션하려면 클라이언트를 마이그레이션하기 위한 특정 프로세스가 필요 하며,이를 통해 마이그레이션 단계를 수행 하는 동안 발생 하는 경합 상태를 최소화 하는 데 도움이 됩니다.         |
|Always On VPN 및 DirectAccess의 기능에 대해 알아봅니다.    |[ALWAYS ON VPN 및 DirectAccess의 기능 비교](../vpn/vpn-map-da.md) 이전 버전의 Windows VPN 아키텍처에서 플랫폼 제한은 DirectAccess를 대체 하는 데 필요한 중요 한 기능 (예: 사용자가 로그인 하기 전에 시작 된 자동 연결)을 제공 하기 어렵게 만들었습니다. 그러나 Always On VPN은 이러한 제한 사항을 대부분 완화 하거나 DirectAccess 기능을 벗어나는 VPN 기능을 확장 했습니다.         |



---