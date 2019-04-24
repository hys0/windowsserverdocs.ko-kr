---
title: 캐시 및 메모리 관리자 하위 시스템의 성능 튜닝
description: 캐시 및 메모리 관리자 하위 시스템의 성능 튜닝
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bbbd8ad17bfb735b148b7f9a53628ab4445f07c4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891434"
---
# <a name="performance-tuning-cache-and-memory-manager"></a>성능 튜닝 캐시 및 메모리 관리자

기본적으로 Windows는 디스크에서 읽거나 디스크에 쓴 파일 데이터를 캐시합니다. 즉, 읽기 작업은 실제 디스크가 아닌 시스템 파일 캐시라고 하는 시스템 메모리 영역의 파일 데이터를 읽습니다. 마찬가지로, 쓰기 작업은 디스크가 아닌 시스템 파일 캐시에 파일 데이터를 쓰며, 이 유형의 캐시를 나중 쓰기 캐시라고 합니다. 캐싱은 파일 개체 단위로 관리됩니다. 캐싱은 Windows가 실행되는 내내 작동하는 캐시 관리자의 지시에 따라 발생합니다.

시스템 파일 캐시의 파일 데이터는 운영 체제에서 결정한 간격으로 디스크에 기록됩니다. 플러시된 페이지는 시스템 캐시 작업 세트(FILE\_FLAG\_RANDOM\_ACCESS가 설정되고 파일 핸들이 종료되지 않은 경우) 또는 대기 목록에 남아 있으며, 이러한 부분이 사용 가능한 메모리가 됩니다.

데이터를 파일에 쓰는 것을 지연하고 캐시가 플러시될 때까지 캐시에 데이터를 보관하는 정책을 Lazy Writing이라고 하며, 확정된 시간 간격으로 캐시 관리자에 의해 트리거됩니다. 파일 데이터 블록이 플러시되는 시간은 데이터가 캐시에 저장되어 있었던 총 기간과 읽기 작업에서 데이터에 마지막으로 액세스한 이후 경과한 기간을 부분적으로 고려하여 결정됩니다. 이렇게 하면 자주 읽는 파일 데이터는 시스템 파일 캐시에 최대한 오래 남아 있습니다.

다음 그림은 이 파일 데이터 캐싱 프로세스를 보여줍니다.

![파일 데이터 캐싱](../../media/perftune-guide-file-data-caching.png)

이전 그림의 실선 화살표가 보여주듯이, 256KB 데이터 영역은 파일 읽기 작업 중에 캐시 관리자가 처음으로 요청할 때 시스템 주소 공간의 256KB 캐시 슬롯에 읽힙니다. 그러면 사용자 모드 프로세스에서는 이 슬롯의 데이터를 자체 주소 공간에 복사합니다. 이 프로세스는 데이터 액세스를 마치면 프로세스 주소 공간과 시스템 캐시 사이의 점선 화살표처럼 변경된 데이터를 시스템 캐시의 동일한 슬롯에 다시 기록합니다. 캐시 관리자는 특정 기간 동안 데이터가 필요 없을 것으로 판단하면 시스템 캐시와 디스크 사이의 점선 화살표처럼 변경된 데이터를 다시 디스크의 파일에 기록합니다.

**이 섹션의 내용:**

-   [캐시 및 메모리 관리자 잠재적인 성능 이슈](troubleshoot.md)

-   [Windows Server 2016의 캐시 및 메모리 관리자 개선 사항](improvements-in-2016.md)
