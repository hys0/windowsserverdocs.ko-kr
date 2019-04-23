---
title: 시스템 정보 데이터 원본
description: 새로운 기능에서 시스템 정보를 작성할 때 로컬로 수집 하 고 분석 하려면 기존 또는 새 데이터 원본을 지정할 수 있습니다. 이 항목에서는 새로운 기능을 등록할 때 선택할 수 있는 데이터 원본을 설명 합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 9b46db90787d24a173ffa472ec1ecb8eaffe054b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845414"
---
# <a name="system-insights-data-sources"></a>시스템 정보 데이터 원본

>적용 대상: Windows Server 2019

시스템 정보에는 확장 가능한 데이터 수집 기능이 도입 되었습니다. 새로운 기능을 작성할 때 로컬로 수집 하 고 분석 하려면 기존 또는 새 데이터 원본을 지정할 수 있습니다. 이 항목에서는 새로운 기능을 등록할 때 선택할 수 있는 데이터 원본을 설명 합니다.

## <a name="data-sources"></a>데이터 원본
새로운 기능을 작성할 때 각 기능에 대 한 특정 데이터 원본을 식별 해야 합니다. 지정 된 데이터 원본을 수집 되어 컴퓨터에서 직접 유지 및 세 가지 유형의 데이터 원본에서 선택할 수 있습니다.

- **성능 카운터**: 
    - 카운터 경로, 이름 및 인스턴스를 지정 하 고 시스템 Insights 이러한 성능 카운터에서 보고 된 관련 데이터를 수집 합니다. 

- **시스템 이벤트**:
    - 채널 이름 및 이벤트 ID를 지정 하 고 시스템 Insights는 횟수를 기록 해당 이벤트가 발생 합니다.

- **잘 알려진 시리즈**
    - 시스템 정보는 몇 가지 잘 정의 된 리소스에 대 한 컴퓨터에 몇 가지 기본 정보를 수집 합니다. 이러한 일련의 기본 기능을 사용 되지만 모든 사용자 지정 기능으로도 사용할 수 있습니다. 이러한 다음 정보를 수집 합니다.

        - **디스크**: 
            - *속성*: GUID
            - *데이터*: 크기
        - **볼륨**:
            - *속성*: UniqueId, DriveLetter, FileSystemLabel, Size
            - *데이터*: 사용된 된 크기
        - **네트워크 어댑터**:
            - *속성*: InterfaceGuid, InterfaceDescription, 속도
            - *데이터*: Bytes Received/sec에 보낸 바이트/초, Bytes Total/sec
        - **CPU**: 
            - *속성*:-
            - *데이터*: % 프로세서 시간

    - 잘 알려진 계열을 지정 하 고 시스템 Insights 해당 계열에서 수집한 데이터를 반환 합니다. 


## <a name="retention-timelines-and-collection-intervals"></a>보존 일정 및 수집 간격
위의 데이터 원본이 있는 다른 보존 타임 라인 및 컬렉션 간격입니다. 아래 표에서 각 데이터 원본 수집 되는 장기 방법 및 백업 주기 표시 됩니다.

| 데이터 원본 | 보존 시간 표시 막대 | 수집 간격 |
| --------------- | --------------- | ----------- |
| 성능 카운터 | 3 개월 | 15분 |
| 시스템 이벤트 | 3 개월 | 15분 |
| 잘 알려진 시리즈 | 1년 | 1시간 |


### <a name="aggregation-types"></a>집계 유형
각 계열에 집계 형식 연결 된 각 수집 간격에 대해 하나의 데이터 요소를 기록 하는 각 계열에 때문에 해당 합니다. 아래 표에서 데이터 원본 및 해당 집계 유형을 설명합니다.

>[!NOTE]
>성능 카운터에 대 한 몇 가지 다른 집계 형식에서 선택할 수 있습니다.

| 데이터 원본 | 집계 유형 |
| --------------- | --------------- |
| 성능 카운터 | Sum, average, max, min |
| 시스템 이벤트 | 개수 |
| 디스크 잘 알려진 시리즈 | 마지막 (가장 늦은 컬렉션 간격 값) |
| 볼륨 잘 알려진 시리즈 | 마지막 (가장 늦은 컬렉션 간격 값) |
| 잘 알려진 시리즈 CPU | 평균 |
| 네트워크의 잘 알려진 시리즈 | 평균 |

## <a name="data-footprint"></a>데이터 공간

시스템 Insights C 드라이브 (c:)의 모든 데이터를 로컬로 수집 합니다. 일반적으로 시스템 Insights 데이터 공간 속도가 빠릅니다. 유형 및 각 기능을 지정 하는 데이터 원본에 직접 다르며 각 데이터 형식에 대 한 저장소 사용량은 아래 테이블에 자세히 설명 합니다.

| 데이터 원본 | 최대 공간 |
| --------------- | --------------- |
| 성능 카운터 | 240 (KB) |
| 시스템 이벤트 | 200KB |
| 디스크 잘 알려진 시리즈 | 디스크당 200KB |
| 볼륨 잘 알려진 시리즈 | 볼륨당 300KB |
| 잘 알려진 시리즈 CPU | 100KB |
| 네트워크의 잘 알려진 시리즈 | 네트워크 어댑터 마다 300KB |

>[!NOTE]
>**기본 예측 기능에 대 한 최대 공간 대부분의 독립 실행형 컴퓨터에 대 한 10MB 미만 이어야 합니다.** 

## <a name="see-also"></a>참조
시스템 정보에 대 한 자세한 내용은 다음 리소스를 사용 합니다.

- [시스템 Insights 개요](overview.md)
- [이해 기능](understanding-capabilities.md)
- [관리 기능](managing-capabilities.md)
- [추가 및 기능 개발](adding-and-developing-capabilities.md)
- [System Insights FAQ](faq.md)
