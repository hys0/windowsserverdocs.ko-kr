---
title: 원격 액세스 Always On VPN 마이그레이션 계획
description: DirectAccess에서 Always On VPN로 적절 한 계획이 필요 마이그레이션 단계에 확인 하는 조직 전체 영향을 미치기 전에 문제를 식별 하는 데 도움이 됩니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/29/2018
ms.openlocfilehash: 494dc7916b505991c22b07bec738c2300d660ec1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835674"
---
# <a name="plan-the-directaccess-to-always-on-vpn-migration"></a>DirectAccess-Always On VPN 마이그레이션 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

&#171;[ **이전:** Always On VPN 마이그레이션 DirectAccess 개요](da-always-on-migration-overview.md)<br>
&#187;[ **다음:** Always On VPN 마이그레이션하고 DirectAccess를 서비스 해제](da-always-on-migration-deploy.md)


DirectAccess에서 Always On VPN로 적절 한 계획이 필요 마이그레이션 단계에 확인 하는 조직 전체 영향을 미치기 전에 문제를 식별 하는 데 도움이 됩니다. 주된 목적은 마이그레이션 과정에서 office에 대 한 원격 연결을 유지 하기 위해 사용자입니다. 잘못 된 작업을 수행 하는 경우 회사 리소스에 액세스할 수 없으므로 사용 하 여 원격 사용자를 그대로 두고 경합 상태가 발생할 수 있습니다. 따라서 Always On VPN에 DirectAccess에서 계획 된, side-by-side-마이그레이션을 수행 것이 좋습니다. 자세한 내용은 참조는 [Always On VPN 마이그레이션 배포](da-always-on-migration-deploy.md) 섹션입니다.

마이그레이션, 표준 구성 고려 사항 및 Always On VPN의 향상 된 기능에 대 한 사용자가 분리의 이점을 설명 합니다. 마이그레이션 계획 단계에는 다음이 포함 됩니다.

1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)] 

3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)] 

4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

## <a name="build-migration-rings"></a>마이그레이션 링 빌드
마이그레이션 링은 여러 단계로 Always On VPN 클라이언트 마이그레이션 작업을 나누는 데 사용 됩니다. 마지막 단계에는 시간별 프로세스 테스트 및 일치 해야 합니다.

이 섹션에서는 마이그레이션 단계를 사용자를 분리 한 후 이러한 단계를 관리 하는 한 가지 방법을 제공 합니다. 선택한 사용자 단계 분리 방법에 관계 없이 관리 간소화 하기 위해 단일 VPN 사용자 그룹 마이그레이션이 완료 되 면 유지 관리 합니다.

>[!NOTE] 
>단어 _단계_ 긴 프로세스 임을 나타내려면이 아닙니다. 며칠 또는 몇 달의 각 단계를 이동 하는지 여부를 side-by-side-마이그레이션 활용 단계적된 접근을 사용 하는 것이 좋습니다.

### <a name="benefits-of-dividing-the-migration-effort-into-multiple-phases"></a>마이그레이션 작업을 여러 단계로 분할의 이점

-   **대용량 중단 보호 합니다.** 마이그레이션을 단계로 나누어 마이그레이션 생성 문제를 영향을 줄 수는 사용자 수가 훨씬 작습니다.

-   **프로세스 또는 통신 피드백에서 향상 되었습니다.** 이상적으로 사용자도 알지 못해 마이그레이션이 발생 했습니다. 하지만, 경험 최적이 아닌 경우에 해당 사용에서 피드백 계획을 개선 하 고 나중에 문제를 방지 하려면 영업 기회 수 있습니다.

### <a name="tips-for-building-your-migration-ring"></a>마이그레이션 링을 만들기 위한 팁

-   **원격 사용자를 식별 합니다.** 두 개의 버킷으로 사용자를 구분 하 여 시작: 자주 사무실 및 그렇지 않은 사용자도 제공 하는 사람입니다. 마이그레이션 프로세스는 두 그룹에 대해 동일 하지만 것 보다 더 자주 연결 하는 사용자에 대 한 업데이트를 수신 하 여 원격 클라이언트가 오래 걸리기 때문입니다. 이상적으로 각 마이그레이션 단계는 각 버킷은에서 멤버를 포함 해야 합니다.

-  **사용자가 우선 순위를 지정 합니다.** 리더십 및 다른 강력한 사용자는 일반적으로 마지막 사용자 간에 마이그레이션됩니다. 하지만 사용자에 우선 순위를 지정 하는 경우 해당 클라이언트 컴퓨터의 마이그레이션 실패 한다면 비즈니스 생산성 영향을 고려 합니다. 예를 들어 1-3의 등급을 설치한 경우 1 의미를 사용 하 여 직원이 작업을 즉시 작업 중단 없이 즉 3 없게만 내부 기간 업무 (LOB) 앱을 원격으로 사용 하는 비즈니스 분석가 되도록 1 인 반면 클라우드를 사용 하 여 영업 직원  앱 3 것입니다.

-   **여러 단계에서 각 부서 또는 비즈니스 단위를 마이그레이션하십시오.** 동시에 전체 부서를 마이그레이션하지 않은 것이 좋습니다. 문제가 발생 해야 하는 경우 원하지 않는 전체 부서에 대 한 원격 작업을 방해 하 합니다. 대신, 두 개 이상의 단계에서 각 부서 또는 비즈니스 단위를 마이그레이션하십시오.

-   **사용자 수를 점차적으로 늘립니다.** 가장 일반적인 마이그레이션 시나리오는 IT 조직의 단기 멤버를 사용 하 여 시작 하 고 뒤에 리더십과 다른 강력한 사용자는 비즈니스 사용자에 게 이동 합니다. 각 마이그레이션 단계에는 점진적으로 더 많은 사람들이 일반적으로 포함 됩니다. 예를 들어, 첫 번째 단계는 10 명의 사용자가 포함 될 수 있습니다 및 마지막 그룹 5,000 명의 사용자가 포함 될 수 있습니다. 배포를 간소화 하려면 단일 VPN 사용자 보안 그룹을 만들고 도착 하면 해당 단계에 사용자를 추가 합니다. 이러한 방식으로 끝나는 나중에 멤버 추가할 수 있는 단일 VPN 사용자 그룹입니다.

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../includes/always-on-vpn-standard-config-considerations-include.md)]


## <a name="next-step"></a>다음 단계

|하려는 경우...  |다음을 참조 하는 중...  |
|---------|---------|
|Always On VPN으로 마이그레이션 시작     |[Always On VPN 마이그레이션하고 DirectAccess를 서비스 해제](da-always-on-migration-deploy.md)합니다. DirectAccess에서 Always On VPN로 마이그레이션 발생 순서가 마이그레이션 단계를 수행 하는 경합을 최소화 하는 데 도움이 되는 클라이언트를 마이그레이션할 특정 프로세스에 필요 합니다.         |
|Always On VPN 및 DirectAccess의 기능에 대해 알아보기    |[기능 비교의 Always On VPN 및 DirectAccess](../vpn/vpn-map-da.md)합니다. Windows VPN 아키텍처의 이전 버전의 플랫폼 제한 하기가 어려웠습니다 (예: 사용자가 로그인 하기 전에 시작 자동 연결) DirectAccess를 대체 하는 데 필요한 중요 한 기능을 제공 합니다. 그러나 Always On VPN, 이러한 제한 사항 중 대부분을 완화할 했거나이 DirectAccess의 기능을 넘어 VPN 기능을 확장 합니다.         |



---