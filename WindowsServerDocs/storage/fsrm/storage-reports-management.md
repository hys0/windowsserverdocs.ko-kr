---
title: 스토리지 보고서 관리
description: 이 문서에서는 저장소 보고서를 생성, 예약 및 모니터링 하는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5bdcada1b445298c8743bdb39491726b594d0a66
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475480"
---
# <a name="storage-reports-management"></a>스토리지 보고서 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자 Microsoft<sup>®</sup> management CONSOLE (MMC) 스냅인의 **저장소 보고서 관리** 노드에서 다음 작업을 수행할 수 있습니다.

-   디스크 사용량의 추세를 식별할 수 있는 정기적인 저장소 보고서를 예약 합니다.
-   모니터는 모든 사용자 또는 선택한 사용자 그룹의 권한이 없는 파일을 저장 하려고 합니다.
-   저장소 보고서를 즉시 생성 합니다.

예를 들어, 다음을 수행할 수 있습니다.

-   매주 일요일 자정에 실행 되는 보고서를 예약 하 여 이전 2 일간 가장 최근에 액세스 한 파일을 포함 하는 목록을 생성 합니다. 이 정보를 사용 하 여 주말 동안 홈에서 연결 하는 사용자에 게 영향을 주지 않는 주말 저장소 활동 및 계획 서버 다운 시간을 모니터링할 수 있습니다.
-   언제 든 지 보고서를 실행 하 여 서버의 볼륨에 있는 모든 중복 파일을 식별 함으로써 데이터 손실 없이 디스크 공간을 신속 하 게 회수할 수 있습니다.
-   파일 그룹별 파일 보고서를 실행 하 여 저장소 리소스가 여러 파일 그룹에 걸쳐 분할 되는 방식 확인
-   소유자별 파일 보고서 보고서를 실행 하 여 개별 사용자가 공유 저장소 리소스를 사용 하는 방법을 분석 합니다.

이 단원에 포함된 항목은 다음과 같습니다.

-   [보고서 세트 예약](schedule-set-of-reports.md)
-   [주문형 보고서 생성](generate-reports-on-demand.md)

> [!Note]
> 전자 메일 알림과 특정 보고 기능을 설정 하려면 먼저 일반 파일 서버 리소스 관리자 옵션을 구성 해야 합니다.

## <a name="additional-references"></a>추가 참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


