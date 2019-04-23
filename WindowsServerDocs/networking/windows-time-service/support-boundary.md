---
ms.assetid: ''
title: 경계 지원으로 매우 정확한 시간
description: 이 문서에서는 매우 정확 하 고 안정적인 시스템 시간을 필요로 하는 환경에서 Windows 시간 (W32Time) 서비스에 대 한 지원 경계를 설명 합니다.
author: shortpatti
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 991bf4502546771dae9f092c6d5732f96b1278ab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866274"
---
# <a name="support-boundary-for-high-accuracy-time"></a>경계 지원으로 매우 정확한 시간

>적용 대상: Windows Server 2016 및 Windows 10 버전 1607 이상

이 문서에서는 매우 정확 하 고 안정적인 시스템 시간을 필요로 하는 환경에서 Windows 시간 서비스 (w32time))에 대 한 지원 범위를 설명 합니다.

## <a name="high-accuracy-support-for-windows-81-and-2012-r2-or-prior"></a>Windows 8.1 및 2012 R2 (또는 이전)에 대 한 높은 정확도 지원

이전 버전의 Windows 10 1607 또는 Windows Server 2016 1607) (이전 Windows 매우 정확한 시간을 보장할 수 없습니다. 이러한 시스템에서 Windows 시간 서비스:

-   Kerberos 버전 5 인증 요구 사항을 충족 하는 데 필요한 시간 정확도 제공 합니다.

-   Windows 클라이언트 및 일반적인 Active Directory 포리스트에 가입 된 서버에 대해 느슨하게 정확한 시간 제공

더 엄격한 정확도 요구 사항 이러한 운영 체제에서 Windows 시간 서비스의 디자인 사양 외부 했으며 지원 되지 않습니다.

## <a name="windows-10-and-windows-server-2016"></a>Windows 10 및 Windows Server 2016

Windows 10 및 Windows Server 2016 시간 정확도 크게 향상 되었습니다, 이전 버전과 완전 NTP 이전 Windows 버전과 호환성을 유지 하면서 합니다. Windows 10 또는 Windows Server 2016 및 최신 버전을 실행 하는 시스템 작동 상태 오른쪽 아래에서 1, 두 번째 50ms (밀리초)을 제공할 수 있습니다 또는 1 밀리초 정확도입니다.

>[!IMPORTANT]
>**매우 정확한 시간 원본**<br>
>토폴로지의 결과 시간 정확도 정확 하 게 하 고 안정적인 루트 (계층 1)를 사용 하 여 하는 데 의존도 시간 원본. Windows 기반 및 비 Windows 기반된 항상 정확 하 고, Windows 호환 NTP 시간 원본 하드웨어 타사 공급 업체에서 판매 있습니다. 해당 제품의 정확성에 공급 업체에 문의 하십시오.

>[!IMPORTANT]
>**시간 정확도**<br>
>시간 정확도 엔드-투-엔드 분포 정확한 시간을 매우 정확 하 게 신뢰할 수 있는 시간 원본에서 최종 장치에 포함 됩니다. 정확도 예를 들어 실제 네트워크 장치 또는 높은 CPU 로드 대상 시스템에 부정적인 영향을 미칩니다 네트워크 비대칭을 소개 하는 아무 것도.

## <a name="high-accuracy-requirements"></a>높은 정확도 요구 사항

이 문서의 나머지 부분에 높은 정확도 해당 목표를 지원 하려면 충족 해야 하는 환경 요구 사항을 간략하게 설명 합니다.

### <a name="target-accuracy-1-second-1s"></a>대상 정확도: 1 초 (1)

1을 달성 하기 위해 특정 대상에 대 한 정확도 매우 정확한 시간 원본과 비교할 때 컴퓨터:

-   대상 시스템에는 Windows 10, Windows Server 2016 실행 해야 합니다.

-   시간 서버는 NTP 계층에서 시간을 동기화 해야 하는 대상 시스템을 매우 정확 하 고, Windows 호환 NTP 시간 원본에서 가장 중요 합니다.

-   위에서 언급 한 NTP 계층의 모든 Windows 운영 체제에 설명 된 대로 구성 해야 합니다 [높은 정확도 대 한 시스템 구성](configuring-systems-for-high-accuracy.md) 설명서.

-   원본 및 대상 간의 누적 단방향 네트워크 대기 시간이 100ms를 초과할 수 없습니다. 누적 네트워크 지연을 개별을 추가 하 여 측정 됩니다 대상을 사용 하 여 시작 및 종료 원본 계층의 NTP 클라이언트-서버 노드 쌍 간의 단방향 지연 합니다. 자세한 내용은 고정밀 시간 동기화 문서를 참조 하십시오.

### <a name="target-accuracy-50-milliseconds"></a>대상 정확도: 50 밀리초

모든 요구 사항 섹션에서 설명한 **대상 정확도: 1 두 번째** 더 엄격한 제어를이 섹션에 요약 되어 있는 제외 하 고 적용 합니다.

특정 대상 시스템에 대 한 50ms 정확도 달성 하기 위해 추가 요구 사항이 다음과 같습니다.

-   대상 컴퓨터는 해당 시간 원본 간의 네트워크 대기 시간이 5ms 보다 나은 있어야 합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 5 계층 보다 더 이상 이어야 합니다.

    >[!Note]
    >계층을 보려면 명령줄에서 "w32tm /query /status"를 실행 합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 6 개 이하의 네트워크 홉 내에 있어야 합니다.

-   모든 stratums의 하루 평균 CPU 사용률이 90%를 초과할 수 없습니다.

-   가상화 된 시스템에 대 한 호스트의 하루 평균 CPU 사용률이 90% 이내 여야 합니다.

### <a name="target-accuracy-1-millisecond"></a>대상 정확도: 1 밀리초

섹션에서 설명한 모든 요구 사항을 **대상 정확도: 1 초** 고 **정확도 대상: 50 밀리초** 더 엄격한 제어를이 섹션에 요약 되어 있는 제외 하 고 적용 합니다.

특정 대상 시스템에 대 한 1 ms 정확도 달성 하기 위해 추가 요구 사항이 다음과 같습니다.

-   대상 컴퓨터에 해당 시간 원본 간의 네트워크 대기 시간의 0.1 밀리초 보다 더 잘 있어야 합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 5 계층 보다 더 이상 이어야 합니다.

    >[!Note]
    >'W32tm /query /status' 계층을 보려면 명령줄에서 실행

-   대상 시스템은 매우 정확한 시간 원본에서 4 개 이하의 네트워크 홉 내에 있어야 합니다.

-   각 계층은 하루 평균 CPU 사용률이 80%를 초과할 수 없습니다.

-   하루 평균 CPU 사용률이 호스트의 가상화 된 시스템의 경우 80%를 초과 하지 해야 합니다.
