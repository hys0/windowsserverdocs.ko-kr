---
title: MultiPoint 서비스 마이그레이션 계획 워크시트
description: Windows Server 2016에서 MultiPoint 서비스로 마이그레이션하는 데 도움이 되는 계획 워크시트를 제공 합니다.
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 864405bb-47ed-4c83-97a2-8df4c6e6f96b
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: c0d5976e70bcf8009cd98e54e973dd6f585d7208
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858906"
---
# <a name="planning-worksheet-for-multipoint-services-migration"></a>MultiPoint 서비스 마이그레이션 계획 워크시트

>적용 대상: Windows Server 2016

다음 목록 및 테이블을 사용 하 여 MultiPoint 서비스 마이그레이션 중 필요한 설정을 수집 합니다.

## <a name="source-server-settings"></a>원본 서버 설정

서버 설정에서 확인할 수 있습니다는 **홈** 다중 포인트 관리자 탭 합니다. 원본 서버에서 사용 중인 각 설정 옆에 있는 확인 표시를 배치 합니다.

- 하나의 계정 여러 세션을 허용 합니다.
- 이 컴퓨터와 원격으로 관리할 수 있도록 합니다.
- 이 컴퓨터의이 데스크톱의 모니터링을 허용 합니다.
- 항상 콘솔 모드에서 시작 합니다.
- 첫 번째 사용자 로그온 시 알림 개인 정보를 표시 하지 않습니다.
- 각 장치에 고유 IP를 할당 합니다.
- 이 컴퓨터에서 다중 포인트 대시보드 및 사용자 세션 간의 IM을 허용 합니다.
- 오케스트레이션 관리자와 다중 포인트 대시보드 사용자 세션을 허용 합니다.
- GPU 하드웨어 렌더링을 사용 하 여 스테이션을 허용 합니다.

## <a name="managed-servers-and-computers"></a>관리 되는 서버 및 컴퓨터

관리 되는 서버 및 컴퓨터의 이름을 기록 합니다. 이 정보를 확인할 수는 **홈** 다중 포인트 관리자 탭 합니다.

| 컴퓨터 | 컴퓨터 이름 |
|----------|---------------|
| 1        |               |
| 2        |               |
| 3        |               |
| 4        |               |
| 5        |               |
| 6        |               |
| 7        |               |
| 8        |               |
| 9        |               |
| 10       |               |


## <a name="stations"></a>스테이션

로컬 스테이션와 해당 설정을 기록 합니다. 이 정보를 확인할 수는 **스테이션** 다중 포인트 관리자 탭 합니다.

| #  | 스테이션 이름 | 자동 로그온 사용자 계정 | 사용 됩니다. |
|----|--------------|-------------------------|---------------------|
| 1  |              |                         |                     |
| 2  |              |                         |                     |
| 3  |              |                         |                     |
| 4  |              |                         |                     |
| 5  |              |                         |                     |
| 6  |              |                         |                     |
| 7  |              |                         |                     |
| 8  |              |                         |                     |
| 9  |              |                         |                     |
| 10 |              |                         |                     |

## <a name="administrators-and-multipoint-dashboard-users"></a>관리자와 사용자가 다중 포인트 대시보드

관리자와 다중 포인트 대시보드 사용자에 대 한 사용자 이름을 복사 합니다. 이 정보를 확인할 수는 **사용자** 다중 포인트 관리자 탭 합니다.

Administrators:

- 사용자 이름:
- 사용자 이름:
- 사용자 이름:
- 사용자 이름:
- 사용자 이름:
- 사용자 이름:

대시보드 사용자:

- 사용자 이름:
- 사용자 이름:
- 사용자 이름:
- 사용자 이름:
- 사용자 이름:

## <a name="vdi-template-and-virtual-desktops"></a>VDI 템플릿 및 가상 데스크톱

MultiPoint 서비스 배포에서 가상 데스크톱의 이름과 VDI 템플릿 정보를 기록 합니다. 이 정보를 확인할 수는 **가상 데스크톱** 다중 포인트 관리자 탭 합니다.

**VDI 템플릿 위치**: 

| # | 가상 데스크톱 이름입니다.      |
|---|---------------------------|
| 1 |                           |
| 2 |                           |
| 3 |                           |
| 4 |                           |
| 5 |                           |