---
title: 캐시 및 메모리 관리자의 향상 된 기능
description: Windows Server 2016의 캐시 및 메모리 관리자 개선 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: pavel; atales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: ef3658ab0f035435f6140c1dfa585de78537d37a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851646"
---
# <a name="cache-and-memory-manager-improvements"></a>캐시 및 메모리 관리자의 향상 된 기능

이 항목에서는 Windows Server 2012 및 2016의 캐시 관리자 및 메모리 관리자 개선 사항에 대해 설명 합니다.

## <a name="cache-manager-improvements-in-windows-server-2016"></a>Windows Server 2016의 캐시 관리자 개선 사항
또한 캐시 관리자는 진정한 비동기 캐시 된 읽기에 대 한 지원을 추가 했습니다.
이렇게 하면 비동기 캐시 된 읽기에 크게 의존 하는 응용 프로그램의 성능이 향상 될 수 있습니다.  대부분의 기본 제공 파일 시스템는 잠시 동안 비동기 캐시 읽기를 지원 하지만 스레드 풀 및 파일 시스템의 내부 작업 큐 처리와 관련 된 다양 한 디자인 선택으로 인해 성능 제한이 있었습니다.  커널에서 적절 한 지원을 통해 캐시 관리자는 이제 파일 시스템에서 모든 스레드 풀 및 작업 큐 관리의 복잡성을 숨기고 비동기 캐시 된 읽기를 처리 하는 것이 더 효율적입니다. 캐시 관리자에는 병렬 처리를 최대화 하기 위해 각 (시스템 지원 최대) VHD 중첩 수준에 대 한 제어 데이터 구조 집합이 하나 있습니다.


## <a name="cache-manager-improvements-in-windows-server-2012"></a>Windows Server 2012의 캐시 관리자 개선 사항
순차적 워크 로드에 대 한 미리 읽기 논리에 대 한 캐시 관리자의 향상 된 기능 외에도 새 API [CcSetReadAheadGranularityEx](https://msdn.microsoft.com/library/windows/hardware/hh406341.aspx) 가 추가 되어 SMB와 같은 파일 시스템 드라이버를 통해 미리 읽기 매개 변수를 변경할 수 있습니다. 이를 통해 미리 읽은 단일 요청을 전송 하는 대신 작은 크기의 미리 읽기 요청을 여러 개 전송 하 여 원격 파일 시나리오에 대 한 처리량을 향상 시킬 수 있습니다. 파일 시스템 드라이버와 같은 커널 구성 요소만 파일 별로 이러한 값을 프로그래밍 방식으로 구성할 수 있습니다.

## <a name="memory-manager-improvements-in-windows-server-2012"></a>Windows Server 2012의 메모리 관리자 개선 사항
페이지 결합을 사용 하면 동일한 내용이 포함 된 페이징할 수 있는 여러 페이지가 있는 서버에서 메모리 사용량을 줄일 수 있습니다. 예를 들어 메모리를 많이 사용 하는 동일한 앱의 여러 인스턴스 또는 매우 반복적인 데이터를 사용 하는 단일 앱을 실행 하는 서버는 페이지 결합을 시도 하는 것이 좋을 수 있습니다. 페이지 결합을 사용 하는 경우의 단점은 CPU 사용량이 증가 한다는 것입니다.

다음은 페이지를 결합 하 여 많은 이점을 제공할 가능성이 없는 서버 역할의 몇 가지 예입니다.

-   파일 서버 (대부분의 메모리는 전용이 지 않으므로 결합할 수 없는 파일 페이지에서 사용 됨)

-   AWE 또는 큰 페이지를 사용 하도록 구성 된 Microsoft SQL Server (대부분의 메모리는 개인 이지만 페이징할 수 없음)

페이지 조합은 기본적으로 사용 하지 않도록 설정 되어 있지만 [Enable MMAgent](https://technet.microsoft.com/library/jj658954.aspx) Windows PowerShell cmdlet을 사용 하 여 사용 하도록 설정할 수 있습니다. 페이지 조합은 Windows Server 2012에 추가 되었습니다.
