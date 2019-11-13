---
ms.assetid: ''
title: 경계 지원으로 매우 정확한 시간
description: 이 문서에서는 매우 정확 하 고 안정적인 시스템 시간이 필요한 환경에서 W32Time (Windows 시간) 서비스에 대 한 지원 경계를 설명 합니다.
author: shortpatti
ms.author: dacuo
manager: dougkim
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 212b9c79bc2e43e966180b928c865a9053332c3f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405271"
---
# <a name="support-boundary-for-high-accuracy-time"></a>경계 지원으로 매우 정확한 시간

>적용 대상: Windows Server 2016 및 Windows 10 버전 1607 이상

이 문서에서는 매우 정확 하 고 안정적인 시스템 시간을 필요로 하는 환경에서 W32Time (Windows 시간 서비스)의 지원 경계를 설명 합니다.

## <a name="high-accuracy-support-for-windows-81-and-2012-r2-or-prior"></a>Windows 8.1 및 2012 R2 (또는 이전 버전)에 대 한 높은 정확도 지원

이전 버전의 Windows (Windows 10 1607 또는 Windows Server 2016 1607 이전 버전)에서는 매우 정확한 시간을 보장할 수 없습니다. 다음 시스템의 Windows 시간 서비스:

-   Kerberos 버전 5 인증 요구 사항을 충족 하기 위해 필요한 시간 정확도를 제공 했습니다.

-   공용 Active Directory 포리스트에 조인 된 Windows 클라이언트 및 서버에 대해 느슨하게 정확한 시간 제공

보다 엄격한 정확도 요구 사항은 이러한 운영 체제에서 Windows 시간 서비스의 디자인 사양을 벗어난 것 이며 지원 되지 않습니다.

## <a name="windows-10-and-windows-server-2016"></a>Windows 10 및 Windows Server 2016

Windows 10 및 Windows Server 2016의 시간 정확성이 크게 향상 되었고 이전 Windows 버전과의 모든 역방향 NTP 호환성을 유지 합니다. 올바른 운영 조건에서 Windows 10 또는 Windows Server 2016 이상 릴리스를 실행 하는 시스템은 1 초, 50ms (밀리초) 또는 1ms 정확도를 제공할 수 있습니다.

>[!IMPORTANT]
>**매우 정확한 시간 원본**<br>
>토폴로지의 결과 시간 정확도는 정확 하 고 안정적인 루트 (계층 1) 시간 원본을 사용 하는 경우에 매우 의존 합니다. 타사 공급 업체에서 판매 하는 windows 기반 및 Windows 기반이 아닌 windows 호환, NTP 시간 원본 하드웨어가 있습니다. 제품의 정확성에 대 한 공급 업체에 문의 하세요.

>[!IMPORTANT]
>**시간 정확도**<br>
>시간 정확성은 매우 정확한 신뢰할 수 있는 시간 원본에서 최종 장치로의 정확한 시간에 대 한 종단 간 배포를 수반 합니다. 네트워크 비대칭을 도입 하는 모든 항목은 실제 네트워크 장치나 대상 시스템의 높은 CPU 부하와 같은 정확도에 부정적인 영향을 줍니다.

## <a name="high-accuracy-requirements"></a>높은 정확도 요구 사항

이 문서의 나머지 부분에서는 해당 하는 높은 정확도 대상을 지원 하기 위해 충족 해야 하는 환경 요구 사항을 간략하게 설명 합니다.

### <a name="target-accuracy-1-second-1s"></a>대상 정확도: 1 초 (1 초)

매우 정확한 시간 원본과 비교할 때 특정 대상 컴퓨터에 대해 1의 정확도를 얻으려면 다음을 수행 합니다.

-   대상 시스템은 Windows 10, Windows Server 2016를 실행 해야 합니다.

-   대상 시스템은 시간 서버의 NTP 계층 구조에서 시간을 동기화 해야 하며, Windows 호환 NTP 시간 culminating 매우 정확 합니다.

-   위에서 언급 한 NTP 계층 구조의 모든 Windows 운영 체제는 [높은 정확도를 위한 시스템 구성](configuring-systems-for-high-accuracy.md) 설명서에 설명 된 대로 구성 해야 합니다.

-   대상과 원본 간의 누적 단방향 네트워크 대기 시간은 100ms를 초과 해서는 안 됩니다. 누적 네트워크 지연은 계층에서 대상으로 시작 하 여 원본에서 끝나는 NTP 클라이언트 서버 노드 쌍 사이에 개별 단방향 지연을 추가 하 여 측정 합니다. 자세한 내용은 높은 정확도 시간 동기화 문서를 참조 하세요.

### <a name="target-accuracy-50-milliseconds"></a>대상 정확도: 50 밀리초

**대상 정확도: 1 초** 섹션에서 설명 하는 모든 요구 사항은이 섹션에 설명 된 보다 엄격한 컨트롤이 있는 경우를 제외 하 고는 적용 됩니다.

특정 대상 시스템에 대해 50ms 정확도를 얻기 위한 추가 요구 사항은 다음과 같습니다.

-   대상 컴퓨터의 시간 원본 간에 네트워크 대기 시간이 5ms 이상 이어야 합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 계층 5 보다 높지 않아야 합니다.

    >[!Note]
    >명령줄에서 "w32tm/query/status"를 실행 하 여 계층를 확인 합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 네트워크 홉이 6 개 이내 여야 합니다.

-   모든 stratums의 1 일 평균 CPU 사용률이 90%를 초과 해서는 안 됩니다.

-   가상화 된 시스템의 경우 호스트의 1 일 평균 CPU 사용률이 90%를 초과 해서는 안 됩니다.

### <a name="target-accuracy-1-millisecond"></a>대상 정확도: 1 밀리초

**대상 정확도: 1 초** 및 **대상 정확도: 50 밀리초** 섹션에서 설명 하는 모든 요구 사항은이 섹션에 설명 된 보다 엄격한 컨트롤이 있는 경우를 제외 하 고는 적용 됩니다.

특정 대상 시스템에 대해 1 밀리초 정확도를 얻기 위한 추가 요구 사항은 다음과 같습니다.

-   대상 컴퓨터의 시간 원본 간에 0.1 밀리초 보다 더 나은 네트워크 대기 시간이 있어야 합니다.

-   대상 시스템은 매우 정확한 시간 원본에서 계층 5 보다 높지 않아야 합니다.

    >[!Note]
    >명령줄에서 ' w32tm/query/status '를 실행 하 여 계층를 확인 합니다.

-   대상 시스템은 항상 정확한 시간 원본에서 4 개 이하의 네트워크 홉에 있어야 합니다.

-   각 계층 평균 CPU 사용률은 80%를 초과 해서는 안 됩니다.

-   가상화 된 시스템의 경우 호스트의 1 일 평균 CPU 사용률이 80%를 초과 해서는 안 됩니다.
