---
title: Windows 관리 센터 SDK 사례 연구-제곱
description: Windows 관리 센터 SDK 사례 연구-제곱
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ab0a7bdcf2388ffc867763c04e183b7388fd13e9
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2052547"
---
# <a name="squared-up-extension"></a>위로 제곱된 확장

## <a name="bringing-scom-based-monitoring-server-dependency-visibility-and-external-data-insights-into-windows-admin-center"></a>SCOM 기반 모니터링, 서버 종속성 가시성 및 Windows 관리 센터에 외부 데이터 정보로 가져오기

제곱을 설립 비전 데이터 시각화를 사용 하 여 엔터프라이즈 IT 복잡성의 문제를 해결 하기 위해 사용 됩니다. Microsoft의 강력한 System Center Operations Manager 플랫폼으로 Microsoft의 Azure 로그 분석, 응용 프로그램 정보 및 시스템에서 추가 데이터 원본-와 통합을 기반으로 구축 제곱을 고유 경량, UI 전용 소프트웨어 서비스 관리자, 등과 같은 ServiceNow Splunk 더 많은-대규모 엔터프라이즈에 대 한 가시성 두 온-프레미스 인프라 및 응용 프로그램 estates 제공 하 고 하이브리드 클라우드 환경에 걸쳐 제 3 자 제품 가운데로 맞춥니다.

> <cite>"우리 했을 때 된 과도 하 게 활용 하 여 해당 기술 미리 보기 전체에서 Windows 관리 센터 및 막대 한 적중 이미, 정말 내리도록 지원 엔지니어가 사용해 구성 테스트에 쉽게 액세스 하 게 같은 문제를 해결 되었습니다 하 고이 기본 관리 하도록 계획 전체 릴리스를 방문한 후 콘솔입니다. 가능성을 제곱와 통합 하 고 한곳에서 모든 데이터를 표시 하는 기능을 항상 환영 합니다. "</cite>
>
> -David Acevedo I / S 전문가 NuStar 에너지 L.P.에 게

Windows 서버 및 IT 팀을 가져올 임무에 포트폴리오를 모두를 제곱 하 고 Microsoft에 의해 전달 되는 다양 한 응용 프로그램의 빠른, 현대, 웹의 정보를 제공 하는 사용자 인터페이스에서 최고 필요한, 제곱을 클라이언트 관리 수백, 다양 한 경우가 많습니다. 결과적으로, 팀을 제곱의 차세대 Windows 서버 관리에 이러한 동일한 값과 보안 주체를 표시 하는 Windows 관리 센터와 흥미로운 맞춤을 즉시 살펴보았습니다. 팀 장기 성능 데이터, 실시간 서버 종속성 인 사이트 및 응용 프로그램 컨텍스트를 제곱 하 여 표시 하 고 매끄러운, 실시간 데이터에서 제공 하는 서버 관리 기능 완벽 하 게 보완 것 라고 생각 하 특히 Windows 관리 센터입니다.

![위로 제곱된 확장](../../media/extend-case-study-squared-up/squared-up-1.png)

> <cite>"를 제곱는 대규모 서버 자산을 관리 하는 조직으로 / Windows 관리 센터의 통합은의 지역화 된 및 중앙 집중화 된 도구 및 되 고 등의 작업을 내에서 서버를 유지 관리 모드로 throw 할 완벽 한 결합 Windows 관리 센터는 귀하에 대 한 유용한 거의 wins "</cite>
>
> --키 프 Granson, Purdue 대학에서 가상화 시스템 관리자

Windows 관리 센터 내에서 해당 데이터를 원활 하 게 제시 하 려 할 때의 분명 한 비전을 갖춘 제곱 초기 개인 미리 보기 버전의 Windows 관리 센터 SDK와 협력 하 고 위로 간단 올바르게 문서화 하 고 유연한 발견 합니다.

Windows 관리 센터 SDK를 사용 하 여, 제곱 되었습니다 동적으로 관련 제곱 Up Windows 관리 센터 내의 보기 경험을 포함 하는 확장을 만들 수 있습니다. 등 특정 서버 또는 클러스터의 컨텍스트 내에서 위로 제곱 보기 자동으로 포함 된를 확장 된 표시를 제공 합니다. 보기에는 모두의 주요 성능 및 용량 메트릭 (예: CPU, 메모리 및 디스크), 기록 추세 스택 (클라우드 플랫폼 또는 데이터 센터 가상화), 예: SQL 데이터베이스 및 서비스 응용 프로그램 구성 요소를 호스트 및 클라우드 기반 로그 분석 및 ITSM 데이터입니다.

![위로 제곱된 확장](../../media/extend-case-study-squared-up/squared-up-2.png)

제곱 및 Windows 관리 센터는 현대 웹 아키텍처 및 디자인 시간적, 간단한 기술 통합 하 고 원활 하 게 사용자 환경을 모두가 사용 하도록 설정 하는 공유 합니다. 웹 기반 관리 점차는 norm 되 고로 서로 다른 시스템 간의 통합이이 메서드는 현대, 통합 관리 경험의 잠금을 해제 하는 키를 생각 합니다.

> <cite>"Windows 관리 센터도 표시 최첨단 현대 Windows 서버 관리 팀은 작업 중인 이러한 속도, 열정, 유연성 및 등 내에서 기본적으로 한다는 사실을와 매우 밀접 하 게 작동 하도록 해 뛰어난 경험을 받은 되므로 현대 개발 패러다임 할당이 수행을 갖추고 방법, 우리는 간결한, 민첩 한, 빠른 소프트웨어 개발 회사로 작동 번거로운. "</cite>
>
> -, 정방형: Richard Benwell에서 제품 설계자

이 자연 스러운 맞춤에서 개발 팀을 제곱의 Windows 관리 센터 환경 내에서 고유 하 게 제곱을 표시 하는 프로토타입 통합을 신속 하 게 진행 하 고 자신의 초기-사용자, 기술의 전달을 가져올 수 있는 수 클라이언트를 미리 보고 합니다. 고객의 반응을에서 즉시 지우기 이야기 충돌 했음을 했습니다.

> <cite>"이 환경의 넘는 3,500 서버 간에 해결 되지 않은 서비스를 사용해 다양 한 통합은 유지 관리의 주요 과제 중 하나는 가로의 관리 및 모니터링 도구 및 되도록 제곱 및 표시 하는 Windows 관리 센터-간의 통합 함께 단일 콘솔 –에 너무 많은 서로 다른 원본의 너무 많은 데이터는 귀하에 대 한 대규모. "</cite>
>
> -Martin Ehrnst, Intility A/S에서 Azure에 대 한 기술 책임자

해당 유형의 클라이언트로부터 제곱을 이미 열정와 톤의 유용한 새 기능 여전히 Windows 관리 센터로 되기를 제곱을 엄청나게 관심이이 통합 및 해당 클라이언트에 대 한 열 멋진 가능성의 미래 및 해당 true 이면 단일-창-의-유리 자신의 IT 운영 관리에 대 한로 여행 합니다.

위로 제곱 / Windows 관리 센터 통합 현재 베타; 중입니다. 액세스를 원하는 경우 하십시오 체크아웃 [제곱의 전용된 수정 페이지에서](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-wac&utm_medium=public-relations&utm_campaign=honolulu) 자세한 내용을 보려면 합니다. 조직에서 Microsoft System Center Operations Manager를 사용 하는 경우 제곱 높여서 (작동 하도록 확장 하기 위해 반드시) 아직 없는 경우 다음 얻을 수 있습니다 또한 손으로 완전 한 기능의 30 일 무료 평가판을 동일한 위치에서에서. 
