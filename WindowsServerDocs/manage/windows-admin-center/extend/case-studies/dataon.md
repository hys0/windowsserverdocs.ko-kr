---
title: Windows Admin Center SDK 사례 연구-DataON
description: Windows Admin Center SDK 사례 연구-DataON
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 01/11/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 1adf538792763bf05a43d431d9751d275a6fcd04
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858224"
---
# <a name="dataon-must-extension"></a>DataON 확장을 해야 합니다.

## <a name="integrated-monitoring-and-management-for-microsoft-hyper-converged-infrastructure"></a>통합 모니터링 및 Microsoft 하이퍼 수렴 형 인프라에 대 한 관리

[DataON](http://www.dataonstorage.com/) 는 하이퍼 수렴 형 인프라 및 저장소 시스템의 Microsoft Windows Server 환경에 대 한 액세스에 최적화 된 업계 선도적인 공급자입니다. 개 650 엔터프라이즈 배포 및 저장소 공간 다이렉트 배포에 대해 120PB에 초점을 두어 설계 Microsoft 응용 프로그램, 가상화, 데이터 보호 및 하이브리드 클라우드 서비스를 제공 합니다.

[DataON의 해야](http://www.dataonstorage.com/must) Windows Admin Center 대 한 확장은 두 가지 보완 제품 통합 하드웨어 및 소프트웨어에 대 한 모니터링, 관리 및 엔드-투-엔드 한 정보를 함께 가져오는 고객에 게 제공할 수 있는 값의 소수 예제 통합된 된 환경에서 전체 클러스터.

> <cite>"독립 실행형 해야 표시 유형, 모니터링 및 관리 도구를 Windows Admin Center 내에서 작업을 사용 하도록 설정 합니다. 고객에 게 제공 해야 하는 확장된 기능에서 이익을 하며 조합 해야 하 고 Windows Admin Center 단일 콘솔에서 Windows Server 기반 인프라에 대 한 ultimate 관리 환경을 제공 합니다. "</cite>
>
> -Howard Lo, 바이스 판매 및 마케팅, DataON 사장

와 같은 기능을 제공 하 여 Windows Admin Center 기능을 확장 하는 확장 해야 합니다.
- **기록 데이터 보고** – IOPS, 대기 시간, 클러스터, 저장소 풀, 볼륨 및 노드에 대 한 처리량을 포함 하 여 시스템 성능 데이터의 실시간 및 월별 대시보드를 제공 합니다.
- **디스크 매핑** – 전체 노드의 일반 디스크 지도 제공 하는 노드의 각 장치 유형 및 구성 요소를 표시 해야 합니다. 디스크, 디스크 유형, 위치 및 각 드라이브의 디스크 상태 슬롯의 수를 보여 줍니다.
- **시스템 경고** – 하드웨어 오류, 구성 문제 및 리소스 채도 식별 하는 Windows 상태 서비스 오류가 발생 합니다. 또한 특정 위치, 오류 설명 및 복구 작업의 다중 수준 평가 제공합니다. 또한 디스크 또는 하드웨어 교체 해야 하는 경우 사용자에 게 알리는 타사 SNMP 트랩 모니터링을 활용할 수 있습니다.
- **SAN 같은 호출 홈 서비스** – 시스템 경고 메시지가 표시 되 면 관리자 수 자동 키 연락처로 전송 된 전자 메일 경고 합니다.

![DataON 확장](../../media/extend-case-study-dataon/dataon-1.png)
*DataON 해야 Windows Admin Center 대 한 확장에 대 한 디스크 매핑*

> <cite>"유용 Windows Admin Center DataON 해야와 같은 확장 방법을 원활 하 게 통합 됩니다와 같은 고 같은 콘솔 내에서 두 도구를 사용할 수 있도록 허용 합니다. Windows Admin Center DataON 함께 해야 실제로가 더 효율적으로 수 및 저장 팀 엄청난 시간입니다. 있게 전에 기대 했던 것 보다 훨씬 더 빠르게 관리자 작업을 수행 합니다. "</cite>
>
> -Matt Roper, 기술 지원 서비스, 체로키어 County (GA)의 진행자 학교 구역

![DataON 확장](../../media/extend-case-study-dataon/dataon-2.png)
*Windows Admin Center 대 한 DataON 해야 확장에서 알림 서비스*

> <cite>"해야 매우 중요 한 되었으며 큰 판매 시점을 했습니다. 우리에 게 Microsoft 하이퍼 수렴 형 인프라를 지 원하는 DataON의 약속을 보여 줍니다. 해당 S2D 어플라이언스를 사용 하 여 포함 해야 합니다는 실행 가능한 SAN 대신 저장소 공간 다이렉트를 사용 하 여 솔루션을 완료 항목입니다. " </cite>
>
> -Benjamin Clements, 사장 전략적 온라인 Systems, Inc.