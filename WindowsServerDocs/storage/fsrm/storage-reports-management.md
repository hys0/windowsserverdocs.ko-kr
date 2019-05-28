---
title: 저장소 보고서 관리
description: 이 문서에서는 보고서를 생성, 예약, 모니터링하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 62215aa802e2509be5305aef53069ae9643562f1
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476095"
---
# <a name="storage-reports-management"></a>저장소 보고서 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자 MMC(Microsoft<sup>®</sup> Management Console) 스냅인의 **저장소 보고서 관리** 노드에서 다음과 같은 작업을 수행할 수 있습니다.

-   디스크 사용량의 추세를 파악할 수 있는 주기적 저장소 보고서를 예약합니다.
-   모든 사용자 또는 선택된 그룹의 사용자를 대상으로 허용되지 않은 파일의 저장 시도를 모니터링합니다.
-   즉시 저장소 보고서를 생성합니다.

예를 들어 다음 작업을 할 수 있습니다.

-   매주 일요일 자정에 지난 이틀간 가장 많이 사용된 파일의 목록을 생성하는 보고서가 실행되도록 예약합니다. 이 정보로 주말의 저장소 활동을 모니터링할 수 있으며, 주말에 집에서 연결하는 사용자에게 영향을 덜 주는 서버 중단 시간을 계획할 수 있습니다.
-   언제든 보고서를 실행하여 서버의 볼륨에서 중복된 파일을 파악할 수 있으므로, 데이터 손실 없이 신속하게 디스크 공간을 다시 확보할 수 있습니다.
-   파일 그룹별 파일 보고서를 실행하여 저장소 리소스가 다른 파일 그룹 사이에서 어떻게 분할되어 있는지 파악할 수 있습니다. 
-   소유자별 파일 보고서를 실행하여 개발 사용자가 공유 저장소 리소스를 어떻게 사용하는지 분석할 수 있습니다.

이 섹션에서는 다음 항목을 다룹니다.

-   [보고서 세트 예약](schedule-set-of-reports.md)
-   [주문형 보고서 생성](generate-reports-on-demand.md)

> [!Note]
> 전자 메일 알림과 특정 보고 기능을 설정하려면, 먼저 일반 파일 서버 리소스 관리자 옵션을 구성해야 합니다.

## <a name="see-also"></a>참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


