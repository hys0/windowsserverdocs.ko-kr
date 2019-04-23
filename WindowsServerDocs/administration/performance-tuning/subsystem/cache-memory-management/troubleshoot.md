---
title: 캐시 및 메모리 관리자 성능 문제 해결
description: 캐시 및 Windows server 16 Memory Manager 성능 문제 해결
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 66c7e2a6b264a837c65df927b271fadd2672fa24
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835794"
---
# <a name="troubleshoot-cache-and-memory-manager-performance-issues"></a>캐시 및 메모리 관리자 성능 문제 해결

Windows Server 2012 이전의 두 가지 잠재적인 문제가 시스템 파일 캐시 사용 가능한 메모리가 특정 워크 로드에서 거의 고갈 된 때까지 발생 합니다. 때 느려지는 시스템에서이 경우 결과 서버 이러한 문제 중 하나가 연결 여부를 확인할 수 있습니다.


## <a name="counters-to-monitor"></a>모니터링 하는 카운터

-   메모리\\장기 평균 대기 캐시 수명 (초) &lt; 1800 초

-   메모리\\Available Mbytes 부족 합니다.

-   메모리\\시스템 캐시 상주 바이트

하는 경우 메모리\\Available Mbytes 이며 낮은 동시 메모리\\중요 한 부분 실제 메모리를 사용 하는 시스템 Cache Resident Bytes, 사용할 수 있습니다 [RAMMAP](https://technet.microsoft.com/sysinternals/ff700229.aspx) 어떤 캐시를 사용 하는 확인 하려면 에 대 한

## <a name="system-file-cache-contains-ntfs-metafile-data-structures"></a>시스템 파일 캐시 NTFS 메타 데이터 구조를 포함합니다.


이 문제는 다음 그림에 나와 있는 것 처럼 출력 RAMMAP active 메타 파일 페이지 매우 많은 수로 표시 됩니다. 이 문제 수 관찰 사용 중인 서버에서 수백만 개의 액세스 하는 파일을 사용 하 여 캐시에서 해제 되지 않을 NTFS 메타 데이터를 캐시에 있으므로 결과입니다.

![rammap 보기](../../media/perftune-guide-rammap.png)

문제는 하면 완화 될 데 *DynCache* 도구입니다. Windows Server 2012 이상, 아키텍처는 다시 설계 되었습니다 및이 문제가 더 이상 존재 해야 합니다.

## <a name="system-file-cache-contains-memory-mapped-files"></a>시스템 파일 캐시 메모리 매핑된 파일에 포함


이 문제는 매우 많은 RAMMAP 출력에 매핑된 파일 페이지를 활성으로 표시 됩니다. 일반적으로 서버에서 일부 응용 프로그램을 여는 중 많은 큰 파일을 사용 하 여 나타냅니다 [CreateFile](https://msdn.microsoft.com/library/windows/desktop/aa363858.aspx) 파일을 사용 하 여 API\_플래그\_임의\_액세스 플래그를 설정 합니다.

이 문제는 KB 문서에 자세히 설명 [2549369](https://support.microsoft.com/default.aspx?scid=kb;en-US;2549369)합니다. 파일\_플래그\_RANDOM\_액세스 플래그는 (Memory Manager는 메모리 부족 상태를 신호 하지)까지 최대한 오랫동안 메모리에 파일의 매핑된 뷰를 유지 하도록 캐시 관리자에 대 한 힌트입니다. 이 플래그는 동시에 파일 데이터의 프리페치를 사용 하지 않도록 설정 하려면 캐시 관리자에 지시 합니다.

이 이런 집합 조정을 향상 된 기능에서 Windows Server 2012 이상에서 작업 하 여 어느 정도 완화 되었습니다 하지만 파일을 사용 하지 않으면 기본적으로 응용 프로그램 공급 업체에서 해결 해야 할 자체 문제\_플래그\_임의\_액세스 합니다. 앱 공급 업체를 위한 대안 솔루션 파일에 액세스할 때 메모리 우선 순위를 사용할 수 있습니다. 사용 하 여 수행할 수 있습니다 합니다 [SetThreadInformation](https://msdn.microsoft.com/library/windows/desktop/hh448390.aspx) API. 메모리 우선 순위에 액세스할 수 있는 페이지는 작업 보다 적극적으로 집합에서 제거 됩니다.

캐시 관리자에서 추가 Windows Server 2016부터이 열 (캐시 관리자 여전히 적용이 FILE_FLAG_RANDOM_ACCESS 플래그 없이 다른 파일 처럼 처리 됩니다 있도록 트리밍 의사 결정을 수행할 때 FILE_FLAG_RANDOM_ACCESS를 무시 하 여 완화 파일 데이터의 프리페치를 사용 하지 않도록 설정 플래그)입니다. 많은 수의 파일이이 플래그를 사용 하 여 열고 실제로 무작위 방식에서으로 액세스 해야 하는 경우 시스템 캐시 블 로트가 발생을 여전히 발생할 수 있습니다. FILE_FLAG_RANDOM_ACCESS 응용 프로그램에서 사용 하지 않도록 것이 좋습니다.
