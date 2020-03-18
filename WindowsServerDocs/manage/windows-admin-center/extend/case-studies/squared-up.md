---
title: Windows 관리 센터 SDK 사례 연구-제곱
description: Windows 관리 센터 SDK 사례 연구-제곱
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 620d3d9f4b5c3638d49fe9141e83ebdcb9eb245c
ms.sourcegitcommit: 5197a87e659589bcc8d2a32069803ae736b02892
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429307"
---
# <a name="squared-up-extension"></a>제곱 위쪽 확장

## <a name="bringing-scom-based-monitoring-server-dependency-visibility-and-external-data-insights-into-windows-admin-center"></a>Windows 관리 센터에 SCOM 기반 모니터링, 서버 종속성 표시 유형 및 외부 데이터 정보 가져오기

제곱은 기업의 IT 복잡성 문제를 해결 하는 데 도움이 되는 데이터 시각화를 사용 하는 비전과 설립 되었습니다. Microsoft의 Microsoft 고유의 Azure Log Analytics, Application Insights 및 시스템에서 추가 데이터 원본과 통합 하는 것 뿐만 아니라 Microsoft의 강력한 System Center Operations Manager 플랫폼을 기반으로 하는 다양 한 경량 UI 전용 소프트웨어 Service Manager를 ServiceNow, Splunk 등의 타사 제품으로 확장 하 여 온-프레미스 및 하이브리드 클라우드 환경에서 대규모 엔터프라이즈 인프라 및 응용 프로그램 자산에 대 한 가시성을 제공 합니다.

> <cite>"Microsoft는 기술 미리 보기 전체에서 Windows 관리 센터를 많이 활용 하 고 있으며, microsoft는 엔지니어 들이 구성 랩에 쉽게 액세스 하는 것과 같은 문제를 해결 하는 데 도움을 주므로 기본 관리를 위해 노력 하 고 있습니다. 콘솔에서 전체 릴리스가 적중 되 면 모든 데이터를 한 장소에 통합 하는 것과 비교할 수 있는 가능성을 좋아합니다. "</cite>
>
> --David Acevedo, NuStar Energy L.P.의 I/S 전문가

제곱의 클라이언트는 수백, 수천, 수천 개의 Windows 서버 및 해당 서버에서 제공 하는 다양 한 응용 프로그램 포트폴리오를 관리 하 고, Microsoft의 핵심 및 Microsoft 모두는 IT 팀이 필요한 정보를 제공 하는 가장 빠른 최신 웹 UI를 제공 합니다. 결과적으로, 팀은 그와 동일한 값과 보안 주체를 차세대 Windows Server 관리에 제공 하는 Windows 관리 센터의 흥미로운 맞춤을 즉시 살펴보았습니다. 특히, 팀은 장기적인 성능 데이터, 제곱으로 표시 되는 실시간 서버 종속성 정보 및 응용 프로그램 컨텍스트는에서 제공 하는 슬림 하 고 실시간 데이터 및 서버 관리 기능을 완벽 하 게 보완 합니다. Windows 관리 센터.

![제곱 위쪽 확장](../../media/extend-case-study-squared-up/squared-up-1.png)

> <cite>"대규모 서버 공간을 관리 하는 조직에서는 Windows 관리 센터 내에서 Windows 관리 센터 내에서 Windows 관리 센터 내에서 서버를 유지 관리 모드로 바로 실행할 수 있는 것과 같은 작업을 수행 하는 것과 같은 중요 한 위쪽/Windows 관리 센터 통합 기능을 결혼.</cite>
>
> -– 건너뛰기 Granson, Purdue 대학의 가상화 시스템 관리자

Windows 관리 센터 내에서 데이터를 원활 하 게 제공 하고자 하는 명확한 비전을 제공 하 고, Windows 관리 센터 SDK의 초기 비공개 미리 보기 버전을 사용 하 여 작업을 수행 하 고, 잘 설명 하 고 유연 하 게 찾을 수 있습니다.

Windows 관리 센터 SDK를 사용 하 여 Windows 관리 센터 환경 내에서 관련 된 제곱 된 보기를 동적으로 포함 하는 확장을 빌드할 수 있습니다. 예를 들어 특정 서버 또는 클러스터의 컨텍스트 내에서 제곱 위쪽 보기는 제공 된 확장 표시에 자동으로 포함 됩니다. 보기에는 주요 성능 및 용량 메트릭 (예: CPU, 메모리 및 디스크), 호스팅 스택 (클라우드 플랫폼 또는 데이터 센터 가상화), SQL database 및 서비스와 같은 응용 프로그램 구성 요소, 클라우드 기반 log analytics 등의 기록 추세를 포함 합니다. 및 ITSM 데이터.

![제곱 위쪽 확장](../../media/extend-case-study-squared-up/squared-up-2.png)

제곱 위쪽 및 Windows 관리 센터는 간단한 기술 통합과 원활한 사용자 환경을 모두 사용 하는 최신 웹 아키텍처와 디자인 ethos을 공유 합니다. 웹 기반 관리를 사용 하는 것이 점점 점점 보편화 되 고 있으며,이는 서로 다른 시스템 간의 통합이 통합 된 최신 관리 환경을 잠금 해제 하는 데 중요 하다 고 생각 합니다.

> <cite>"Windows 관리 센터를 최신 Windows Server 관리의 최첨단으로 볼 수 있으므로, 팀과 긴밀 하 게 협력 하 고 이러한 속도, 관심, 유연성 및 이러한 근본적으로 작업 하는 것이 좋습니다. 최신 개발 패러다임은 간단 하 고 민첩 하 고 신속 하 게 진행 하는 소프트웨어 개발 회사, 작업을 수행 하는 방식에 잘 맞습니다.</cite>
>
> --Richard 교차곱 웰, 제품 설계자 (제곱)

이 자연 스런 연계를 통해 개발 팀은 처음에는 Windows 관리 센터 환경 내에서 기본적으로 제곱 하는 프로토타입 통합을 신속 하 게 진행 하 고 자신의 초기 도입자, 기술 클라이언트를 미리 봅니다. 고객의 반응부터 스토리가 적용 되었다는 것을 즉시 알 수 있었습니다.

> <cite>"전체 3500 서버 환경에서 처리 중인 서비스를 유지 관리 하는 데 있어 중요 한 문제 중 하나는 다양 한 관리 및 모니터링 도구를 통합 하는 것입니다. 따라서 Windows 관리 센터와 여러 개의 서로 다른 소스에서 단일 콘솔로 많은 데이터를 함께 사용할 수 있습니다. "</cite>
>
> --Martin Ehrnst, Intility A/S의 Azure에 대 한 기술 리드

이러한 종류의 관심는 이미 Windows 관리 센터에 제공 되는 것과 같은 다양 한 새로운 기능을 갖춘 클라이언트에서 사용 하는 것이 가능 하며,이 통합의 미래와 클라이언트 및 해당 클라이언트에 대 한 놀라운 가능성이까지 대폭. IT 운영 관리를 위한 진정한 단일 창으로 전환 합니다.

제곱 Up/Windows 관리 센터 통합은 현재 베타 버전입니다. 액세스 하려는 경우 자세한 내용을 보려면 [제곱의 전용 페이지](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-wac&utm_medium=public-relations&utm_campaign=honolulu) 를 확인 하세요. 조직에서 Microsoft System Center Operations Manager를 사용 하 고 아직 제곱 하지 않은 경우 (확장이 작동 하는 데 필요 함) 동일한 위치에서 완전 한 기능을 갖춘 30 일 무료 평가판을 활용할 수도 있습니다. 
