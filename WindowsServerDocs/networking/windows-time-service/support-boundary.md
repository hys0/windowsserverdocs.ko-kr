---
title: 정확한 시간을 위한 경계 지원
description: 이 문서에서는 매우 정확하고 안정적인 시스템 시간을 필요로 하는 환경에서 Windows 시간(W32Time) 서비스의 지원 경계를 설명합니다.
author: dcuomo
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: f6df2a07fa7af2b5912c368393bdab39ccc5ced3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861636"
---
# <a name="support-boundary-for-high-accuracy-time"></a>정확한 시간을 위한 경계 지원

>적용 대상: Windows Server 2016 및 Windows 10 버전 1607 이상

이 문서에서는 매우 정확하고 안정적인 시스템 시간을 필요로 하는 환경에서 Windows 시간 서비스(W32Time)의 지원 경계를 설명합니다.

## <a name="high-accuracy-support-for-windows-81-and-2012-r2-or-prior"></a>Windows 8.1 및 2012 R2(또는 이전 버전)에 대한 높은 정확도 지원

이전 버전의 Windows(Windows 10 1607 또는 Windows Server 2016 1607 이전 버전)에서는 매우 정확한 시간을 보장할 수 없습니다. 다음 시스템의 Windows 시간 서비스:

-   Kerberos 버전 5 인증 요구 사항을 충족하기 위해 필요한 시간 정확도를 제공했습니다.

-   일반적인 Active Directory 포리스트에 조인된 Windows 클라이언트 및 서버에 대해 정확도가 낮은 시간을 제공했습니다.

보다 엄격한 정확도 요구 사항은 이러한 운영 체제에서 Windows 시간 서비스의 디자인 사양을 벗어난 것이며 지원되지 않습니다.

## <a name="windows-10-and-windows-server-2016"></a>Windows 10 및 Windows Server 2016

이전 Windows 버전과 완전 역방향 NTP 호환성을 유지하면서 Windows 10 및 Windows Server 2016에서 시간 정확도가 크게 향상되었습니다. 올바른 운영 조건에서 Windows 10 또는 Windows Server 2016 이상 릴리스를 실행하는 시스템은 1초, 50ms(밀리초) 또는 1ms 정확도를 제공할 수 있습니다.

>[!IMPORTANT]
>**매우 정확한 시간 원본**<br>
>토폴로지의 결과 시간 정확도는 정확하고 안정적인 루트(계층 1) 시간 원본을 사용하는 것에 매우 의존합니다. 타사 공급 업체에서 판매하는 Windows 기반 및 Windows 기반이 아닌 매우 정확한 Windows 호환 NTP 시간 원본 하드웨어가 있습니다. 제품의 정확성에 대해 공급 업체에 문의하세요.

>[!IMPORTANT]
>**시간 정확도**<br>
>시간 정확도는 매우 정확한 신뢰할 수 있는 시간 원본에서 최종 디바이스로의 정확한 시간에 대한 엔드투엔드 배포를 수반합니다. 네트워크 비대칭을 도입하는 모든 항목은 실제 네트워크 디바이스나 대상 시스템의 높은 CPU 부하와 같은 정확도에 부정적인 영향을 줍니다.

## <a name="high-accuracy-requirements"></a>높은 정확도 요구 사항

이 문서의 나머지 부분에서는 해당하는 높은 정확도 대상을 지원하기 위해 충족해야 하는 환경 요구 사항을 간략하게 설명합니다.

### <a name="target-accuracy-1-second-1s"></a>대상 정확도: 1초(1s)

매우 정확한 시간 원본과 비교할 때 특정 대상 머신에 대해 1s의 정확도를 얻으려면:

-   대상 시스템은 Windows 10, Windows Server 2016을 실행해야 합니다.

-   대상 시스템은 시간 서버의 NTP 계층 구조에서 시간을 동기화해야 하며, Windows 호환 NTP 시간 원본이 매우 정확해야 합니다.

-   위에서 언급한 NTP 계층 구조의 모든 Windows 운영 체제는 [높은 정확성을 위한 시스템 구성](configuring-systems-for-high-accuracy.md) 설명서에 설명된 대로 구성되어야 합니다.

-   대상과 원본 간의 누적 단방향 네트워크 대기 시간은 100ms를 초과해서는 안 됩니다. 누적 네트워크 지연은 계층에서 대상으로 시작하여 원본에서 끝나는 NTP 클라이언트 서버 노드의 쌍 사이에 개별 단방향 지연을 추가하여 측정됩니다. 자세한 내용은 높은 정확도 시간 동기화 문서를 참조하세요.

### <a name="target-accuracy-50-milliseconds"></a>대상 정확도: 50밀리초

이 섹션에서 설명된 보다 엄격한 컨트롤을 제외하고 섹션 **대상 정확도: 1초**에서 설명하는 모든 요구 사항이 적용됩니다.

특정 대상 시스템에 대해 50ms 정확도를 얻기 위한 추가 요구 사항은 다음과 같습니다.

-   대상 컴퓨터는 시간 원본 간에 네트워크 대기 시간이 5ms 이상이어야 합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 계층 5보다 높지 않아야 합니다.

    >[!Note]
    >명령줄에서 "w32tm /query /status"를 실행하여 계층을 확인합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 네트워크 홉이 6개 이내여야 합니다.

-   모든 계층의 1일 평균 CPU 사용률이 90%를 초과해서는 안 됩니다.

-   가상화된 시스템의 경우 호스트의 1일 평균 CPU 사용률이 90%를 초과해서는 안 됩니다.

### <a name="target-accuracy-1-millisecond"></a>대상 정확도: 1밀리초

이 섹션에서 설명된 보다 엄격한 컨트롤을 제외하고 섹션 **대상 정확도: 1초** 및 **대상 정확도: 50초**에서 설명하는 모든 요구 사항이 적용됩니다.

특정 대상 시스템에 대해 1ms 정확도를 얻기 위한 추가 요구 사항은 다음과 같습니다.

-   대상 컴퓨터는 시간 원본 간에 네트워크 대기 시간이 0.1ms 이상이어야 합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 계층 5보다 높지 않아야 합니다.

    >[!Note]
    >명령줄에서 `w32tm /query /status'를 실행하여 계층을 확인합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 네트워크 홉이 4개 이내여야 합니다.

-   각 계층에서 1일 평균 CPU 사용률이 80%를 초과해서는 안 됩니다.

-   가상화된 시스템의 경우 호스트의 1일 평균 CPU 사용률이 80%를 초과해서는 안 됩니다.
