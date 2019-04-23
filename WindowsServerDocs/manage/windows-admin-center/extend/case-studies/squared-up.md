---
title: Windows Admin Center SDK 사례 연구-제곱 합니다.
description: Windows Admin Center SDK 사례 연구-제곱 합니다.
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ab0a7bdcf2388ffc867763c04e183b7388fd13e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863944"
---
# <a name="squared-up-extension"></a>확장을 제곱합니다.

## <a name="bringing-scom-based-monitoring-server-dependency-visibility-and-external-data-insights-into-windows-admin-center"></a>SCOM 기반 모니터링, 서버 종속성 표시 유형 및 Windows Admin Center 대 한 외부 데이터 정보

제곱 등록 데이터 시각화를 사용 하 여 엔터프라이즈 IT 복잡성 문제를 해결 하는 데의 비전을 사용 하 여 설립 된 합니다. 제곱 등록의 고유 간단한 UI 전용 소프트웨어 기반 Microsoft의 강력한 System Center Operations Manager 플랫폼 뿐만 아니라 Microsoft의 Azure Log Analytics, Application Insights 및 시스템에서 추가 데이터 원본-통합 ServiceNow, Splunk 및 많은-온-프레미스 인프라 및 응용 프로그램 이상적인 대규모 엔터프라이즈에 대 한 가시성을 제공 하 고 하이브리드 클라우드 환경에서 타사 제품에 Service Manager 센터입니다.

> <cite>"에서는 했습니다 과도 하 게 활용 하 여 기술 미리 보기 동안 Windows Admin Center 엄청난 적중 이미 실제로 구성 실습에 쉽게 액세스 하는 엔지니어와 같은 문제를 해결할 수 있도록 지원 되었습니다 및 기본 관리를 확인 하려고 합니다. 전체 릴리스 도달할 되 면 콘솔입니다. 우리가 좋아하는 제곱 등록을 사용 하 여 통합을 한 곳에서 모든 데이터를 표시 하는 기능은 가능성. "</cite>
>
> -David Acevedo I / NuStar 에너지 L.P. S 전문가

Windows 서버를 둘 다를 제곱 하 고 Microsoft에서 제공 하는 포트폴리오를 제공 하려는 임무를 IT 팀에 다양 한 응용 프로그램을 빠르고 최신 웹 UI에서 정보를 제공 하는 가장 필요한, 제곱의 클라이언트를 관리 수백, 수천 경우가 많습니다. 결과적으로, 제곱 하에서 팀은 이러한 동일한 값 및 주체 차세대 Windows Server 관리를 제공 하는 Windows Admin Center 사용 하 여 흥미로운 맞춤 즉시 살펴보았습니다. 특히 팀 힘들게 장기 성능 데이터, 실시간 서버 종속성 정보 및 응용 프로그램 컨텍스트를 제곱 하 여 표시 되 고 세련 된 실시간 데이터에서 제공 하는 서버 관리 기능이 완벽 하 게 보완는 Windows Admin Center.

![확장을 제곱합니다.](../../media/extend-case-study-squared-up/squared-up-1.png)

> <cite>"제곱 하는 대규모 서버 자산을 관리 하는 조직으로 Windows Admin Center 통합은 지역화 및 중앙 집중식 도구 및 중 등에서 서버 유지 관리 모드로 바로 throw 할 완벽 한 결혼 / Windows Admin Center 우리 회사에 유용한 간단한 wins "</cite>
>
> --건너뛰기 Granson, Purdue 대학의 가상화 시스템 관리자

Windows Admin Center 내에서 해당 데이터를 원활 하 게 제공 하기 위해 필요에 대 한 명확한 비전과, 갖추었으므로 제곱 초기 비공개 미리 보기 버전의 Windows Admin Center SDK를 사용 하 여 작동 및 간단 하 고 잘 문서화 된 유연한 발견 합니다.

Windows Admin Center SDK를 사용 하 제곱 경우 동적으로 관련 제곱을 Windows Admin Center 내에서 보기 경험을 포함 하는 확장을 빌드할 수 예를 들어, 특정 서버 또는 클러스터의 컨텍스트 내에서 뷰를 제곱 자동으로 포함 됩니다에 확장된 가시성을 제공 합니다. 보기 포함 주요 성능 및 용량 메트릭 (예: CPU, 메모리 및 디스크)의 기록 추세 스택 (클라우드 플랫폼 또는 데이터 센터 가상화), SQL 데이터베이스 및 서비스와 같은 응용 프로그램 구성 요소를 호스팅 및 클라우드 기반 로그 분석 및 ITSM 데이터입니다.

![확장을 제곱합니다.](../../media/extend-case-study-squared-up/squared-up-2.png)

제곱 및 Windows Admin Center 최신 웹 아키텍처 및 디자인 서서히 정착, 간단한 기술 통합을와 서 원활한 사용자 환경을 사용 하도록 설정한는 공유 합니다. 점차 표준 되 고 웹 기반 관리를 사용 하 여 서로 다른 시스템 간의 통합이 메서드는 키 최신, 통합 관리 환경을 잠금을 해제 하는 것이 믿습니다.

> <cite>"Windows Admin Center 표시 최신 Windows Server 관리의 최첨단 하므로 팀에서 작업 중인 이러한 속도, 열정, 유연성 및 이러한 내 근본적으로 팩트와 매우 밀접 하 게 작업을 위한 뛰어난 환경과 되었습니다. 최신 개발 패러다임에 매우 적합 변경한 방식과, 린 (lean), 민첩 하 고 빠른 소프트웨어 개발 회사를 위한 노력 직접. "</cite>
>
> -Richard Benwell, 제품 아키텍트 제곱

이 자연 맞춤의 제곱 하에 개발 팀에서 Windows Admin Center 환경 내에서 고유 하 게 제곱을 표시 하는 프로토타입 통합을 신속 하 게 진행 하 고는 자신의-얼 기술 넘어갈 수 클라이언트를 미리 봅니다. 고객의 반응을에서 스토리 우승자 했음을 즉시 명확 했습니다.

> <cite>"3,500 개 서버 환경을 서비스는 다양 한 통합은 유지 관리의 핵심 과제 중 하나는 가로 관리 및 모니터링 도구 등의 제곱 및 제공-Windows Admin Center 간의 통합 함께 하나의 콘솔로 – 많이 서로 다른 원본에서 많은 양의 데이터가 우리 회사에 대규모입니다. "</cite>
>
> -Martin Ehrnst, Intility a/S에서 Azure에 대 한 기술 책임자

이러한 종류의 열정 제곱 클라이언트를 이미에서 및 유용한 새 기능이 여전히 많은 Windows Admin Center 제곱 하는 엄청나게 기대 멋진 가능성을 열어 줍니다 해당 클라이언트에 대 한이 통합의 미래에 대 한 및 true 단일-창-의-유리가 IT 운영 관리에 대 한 과정입니다.

제곱 하 / 통합 Windows Admin Center 현재 베타 버전입니다. 액세스를 원하는 경우 확인 하세요 [제곱의 전용된 페이지](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-wac&utm_medium=public-relations&utm_campaign=honolulu) 대 한 자세한 내용은 합니다. 조직에서 Microsoft System Center Operations Manager를 사용 하 고 제곱 등록 (이 확장 작업을 하는 데 필수적) 아직 없는 경우 다음 볼 수도 있습니다 손이 갖춘 30 일 무료 평가판을 동일한 위치에 있습니다. 
