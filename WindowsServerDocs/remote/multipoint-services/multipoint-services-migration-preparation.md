---
title: MultiPoint 서비스에 마이그레이션 준비
description: Windows Server 2016에서 MultiPoint 서비스를 마이그레이션하기 전에 수집 하는 정보를 설명 합니다.
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3060c531-98a2-4957-a02c-be273f25f493
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 9650ebcae7e6207a226617d401d892049405901f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824384"
---
# <a name="prepare-to-migrate-to-multipoint-services-in-windows-server-2016"></a>Windows Server 2016에서 MultiPoint 서비스에 마이그레이션 준비

>적용 대상: Windows Server 2016

다음 정보를 사용 하 여 이전 버전 Windows Server 2016의 Windows Server 2016 RTM을 실행 하는 대상 서버를 실행 하는 원본 서버에서 MultiPoint 서비스 역할 서비스를 마이그레이션해야 할 정보를 수집 합니다.

여기에 최소한 설치, 제거 또는 MultiPoint 서비스를 설정 하려면 원본 서버와 대상 서버에서 Administrators 그룹의 구성원 여야 합니다.

>[!NOTE]
> 여기의 단계는 데이터를 마이그레이션하는 사용자 폴더에 저장 또는 공유 폴더에 대 한 지침을 제공 하지 않습니다. 마이그레이션을 시작 하기 전에 사용자가 자신의 데이터를 다시 확인 합니다.

다중 포인트 관리자를 사용 하 여 마이그레이션에 필요한 정보를 검색 합니다. 다중 포인트 관리자를 사용 하려면 서버 관리자 권한이 필요 합니다.

MultiPoint 서버, 사용자 및 환경 설정을 기록해두십시오는 [마이그레이션 데이터 수집 워크시트](multipoint-services-migration-worksheet.md)합니다. 다음 단계를 사용 하 여 해당 정보를 수집 합니다.

## <a name="multipoint-server-settings-for-the-local-server"></a>로컬 서버에 대 한 다중 서버 설정
1. 다중 포인트 관리자를 시작 합니다.
2. 에 **홈** 탭 로컬 서버를 선택한 다음 클릭 **서버 설정을 편집 합니다.**
3. 데이터 워크시트에서의 설정을 기록 합니다.
4. 설정 창을 닫습니다.

## <a name="managed-servers-and-computers"></a>관리 되는 서버 및 컴퓨터

관리 되는 서버 및 컴퓨터의 이름을 찾을 수 있습니다는 **홈** 다중 포인트 관리자 탭 합니다.

## <a name="station-settings"></a>스테이션 설정
자동 로그온 또는 디스플레이 방향을 스테이션으로 구성 된 경우 해당 정보를 검색 하려면 다음 단계를 따르십시오. 그렇지 않으면이 단계를 건너뛸 수 있습니다.

스테이션 설정을 검색 합니다.

1. 이동 된 **스테이션** 다중 포인트 관리자 탭 합니다.
2. "예"를 가진 스테이션에서 찾기는 **자동 로그온** 열입니다.
3. 해당 스테이션을 선택한 다음 클릭 **스테이션 구성**합니다.
4. 자동 로그온에 사용 되는 사용자를 기록 합니다.

디스플레이 방향을 설정을 검색 하려면 보기는 **설정을 워크스테이션** 각 장치에 대 한 합니다.

## <a name="list-of-users"></a>사용자 목록
1. 클릭 된 **사용자** 다중 포인트 관리자 탭 합니다.
2. 레코드는 **관리자** 및 **MultiPoint 대시보드 사용자** accoutns 합니다.
3. 표준 사용자를 기록 합니다.

## <a name="vdi-template-location"></a>VDI 템플릿 위치
 이전에 설정한 경우 VDI 템플릿 기능, VDI 서식 파일의 위치를 기록 합니다. 원본 및 대상 서버는 동일한 네트워크에 있는 경우으로 다중 포인트 관리자를 사용 하 여 서식 파일을 가져올 수 있습니다.
 
## <a name="next-step"></a>다음 단계
준비가 이제 [MultiPoint Services로 마이그레이션](multipoint-services-migration-steps.md) RTM 버전의 Windows Server 2016 합니다.