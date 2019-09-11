---
title: Windows 관리 센터 SDK 사례 연구-DataON
description: Windows 관리 센터 SDK 사례 연구-DataON
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 01/11/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 12de939aa451ba75b4bafed85cd57bdd8280bc81
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70864942"
---
# <a name="dataon-must-extension"></a>DataON이 확장 되어야 합니다.

## <a name="integrated-monitoring-and-management-for-microsoft-hyper-converged-infrastructure"></a>Microsoft 하이퍼 수렴 형 인프라에 대 한 통합 모니터링 및 관리

[Dataon](http://www.dataonstorage.com/) 은 Microsoft Windows Server 환경에 최적화 된 하이퍼 수렴 형 인프라 및 저장소 시스템의 업계 최고의 공급자입니다. Microsoft 응용 프로그램, 가상화, 데이터 보호 및 하이브리드 클라우드 서비스를 제공 하는 것에만 중점을 두었습니다. 650 엔터프라이즈 배포를 초과 하 고 스토리지 공간 다이렉트 배포를 120PB 이상 사용 합니다.

Windows 관리 센터에 대 한 [Dataon의](http://www.dataonstorage.com/must) 경우 확장 프로그램은 두 가지 보완 제품을 통합 하 여 고객에 게 제공 하 고, 모니터링 및 관리를 제공 하 고, 하드웨어 및 소프트웨어에 대 한 완벽 한 통찰력을 제공 합니다. 통합 환경의 전체 클러스터

> <cite>"우리는 독립 실행형으로 표시, 모니터링 및 관리 도구를 사용 하 여 Windows 관리 센터 내에서 작업을 수행 하도록 설정 했습니다. 고객은에서 제공 해야 하는 확장 된 기능을 활용 하 고, windows 관리 센터를 단일 콘솔에서 조합 하 여 Windows Server 기반 인프라를 위한 최고의 관리 환경을 제공 합니다. "</cite>
>
> --Howard로, 판매 및 마케팅 부사장, DataON

는 다음과 같은 기능을 제공 하 여 Windows 관리 센터의 기능을 확장 해야 합니다.
- **기록 데이터 보고** – 클러스터의 IOPS, 대기 시간, 처리량, 저장소 풀, 볼륨 및 노드를 포함 하 여 시스템 성능 데이터의 실시간 및 월간 대시보드를 제공 합니다.
- **디스크 매핑** – 전체 노드에 대 한 명확한 디스크 맵을 제공 하 여 각 노드의 장치 유형 및 구성 요소를 표시 해야 합니다. 디스크 수, 디스크 유형, 각 드라이브의 위치 및 슬롯 및 디스크 상태를 표시 합니다.
- **시스템 경고** – Windows 상태 관리 서비스 오류를 활용 하 여 하드웨어 오류, 구성 문제 및 리소스 포화를 식별 합니다. 또한 특정 위치, 오류 설명 및 복구 작업에 대 한 다중 수준 평가를 제공 합니다. 또한 디스크 또는 하드웨어를 교체 해야 하는 경우 타사 SNMP 모니터링 트랩을 활용 하 여 사용자에 게 경고할 수 있습니다.
- **SAN과 유사한 호출 홈 서비스** – 시스템 경고에 의해 관리자가 키 연락처에 자동 전자 메일 알림을 보낼 수 있습니다.

![*Windows 관리 센터의 경우 dataon에서 확장 디스크 매핑의* dataon 확장이 필요 합니다.](../../media/extend-case-study-dataon/dataon-1.png)


> <cite>"동일한 콘솔 내에서 두 도구를 모두 사용할 수 있도록 Windows 관리 센터에서 DataON 같은 확장을 허용 하는 것이 좋습니다. Windows 관리 센터와 DataON을 함께 사용 하면 더 효율적이 고 팀에 많은 시간을 절감할 수 있습니다. 이를 통해 관리자 작업을 이전 보다 훨씬 더 빠르게 달성할 수 있습니다. "</cite>
>
> --Matt Roper, 기술 지원 서비스의 촉진 자, 체로키어 군 (GA) School 학구

![](../../media/extend-case-study-dataon/dataon-2.png)
*Windows 관리 센터에 대 한 확장 프로그램의 dataon 확장 경고 서비스*

> <cite>"는 매우 중요 하며 큰 판매 지점 이었습니다. Microsoft는 Microsoft 하이퍼 수렴 형 인프라를 지원 하기 위해 DataON의 약정을 보여 주었습니다. 을 (를) 사용 하는 것은 사용 가능한 SAN 교체로 스토리지 공간 다이렉트 솔루션을 완료 하는 것입니다.</cite>
>
> --Benjamin Clements, 부사장, 전략적 온라인 시스템, i n c.