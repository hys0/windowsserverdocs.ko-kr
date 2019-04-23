---
title: 캐시 및 메모리 관리자의 향상 된 기능
description: 캐시 및 Windows Server 2016의에서 메모리 관리자 개선
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bd15cfc0714d1992e6b15d716b6b96ce259786da
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868584"
---
# <a name="cache-and-memory-manager-improvements"></a>캐시 및 메모리 관리자의 향상 된 기능

이 항목에서는 캐시 관리자 및 Memory Manager 향상 된을 Windows Server 2012 및 2016에 설명합니다.

## <a name="cache-manager-improvements-in-windows-server-2016"></a>Windows Server 2016의 향상 된 캐시 관리자
캐시 관리자 true 비동기 캐시 읽기에 대 한 지원도 추가 했습니다.
비동기 캐시 된 읽기 의존 하는 경우에 잠재적으로 응용 프로그램의 성능을 개선할 수 있습니다이.  대부분의 기본 파일 시스템이 비동기 캐시 읽기에 대해 지원 되는 동안 종종 성능 같은 제한 사항이 있었습니다 인해 스레드 풀 및 파일 시스템의 내부 작업 큐의 처리와 관련 된 다양 한 디자인 선택 합니다.  커널 적절 한 지원을 통해 캐시 관리자는 이제 모든 스레드 풀 숨깁니다 및 작업 큐 관리 복잡성 하므로 처리에서 보다 효율적으로 비동기 파일 시스템에서 읽기 캐시 합니다. 캐시 관리자 집합이 하나의 컨트롤 datastructures (지원 되는 시스템 최대)의 각 VHD 중첩 수준 병렬 처리를 최대화 합니다.


## <a name="cache-manager-improvements-in-windows-server-2012"></a>Windows Server 2012의 향상 된 캐시 관리자
캐시 관리자 미리 읽기 논리 순차적 워크 로드를 새 API에 대 한 향상 된 기능 외에도 [CcSetReadAheadGranularityEx](https://msdn.microsoft.com/library/windows/hardware/hh406341.aspx) SMB와 같은 시스템 드라이버를 파일에서 해당 읽기 미리 매개 변수를 변경할 수 있도록 추가 되었습니다. 큰 단일 읽기 미리 요청을 전송 하는 대신 여러 소규모 미리 읽기 요청을 전송 하 여 원격 파일 시나리오에 대 한 더 나은 처리량을 허용 합니다. 프로그래밍 방식으로 커널 구성 요소를 파일 시스템 드라이버와 같은 파일 단위 별로 이러한 값을 구성할 수 있습니다.

## <a name="memory-manager-improvements-in-windows-server-2012"></a>Windows Server 2012의 향상 된 메모리 관리자
페이지 결합을 사용 하도록 설정 하면 많은 내용이 동일한 개인, 페이징할 수 있는 페이지는 서버의 메모리 사용량을 줄일 수 있습니다. 예를 들어, 동일한 메모리를 많이 사용 앱을 매우 반복 되는 데이터를 사용 하는 단일 앱의 여러 인스턴스를 실행 하는 서버에 결합 하는 페이지를 시도 하기에 적합 수 있습니다. 페이지 결합 사용의 단점은 CPU 사용량이 증가할된 것입니다.

다음은 결합 하는 페이지 그다지 많은 이점을 제공 가능성이 없는 서버 역할의 몇 가지 예:

-   파일 서버 (대부분의 메모리는 개인 및 따라서 하지 결합할 수 없는 파일 페이지에서 사용 됩니다.)

-   AWE 또는 큰 페이지 (대부분의 메모리는 페이징할 수 없는 있지만 개인)을 사용 하도록 구성 된 Microsoft SQL Server

결합 하는 페이지는 기본적으로 비활성화 되어 있지만 사용 하 여 사용할 수 있습니다 합니다 [사용 MMAgent](https://technet.microsoft.com/library/jj658954.aspx) Windows PowerShell cmdlet. 페이지를 결합 하는 Windows Server 2012에 추가 되었습니다.
