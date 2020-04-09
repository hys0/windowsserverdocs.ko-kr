---
title: 마이그레이션 MultiPoint 서비스에 대 한 단계
description: Windows Server 2016에서 MultiPoint 서비스로 마이그레이션하는 단계를 안내 합니다.
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 3ee77efa-7cc5-4ddf-aaff-b5634a717014
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: f2e293fafb8d6f5d84e9ea5a4ad8ef3b7fe2ba7d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858696"
---
# <a name="migrate-to--multipoint-services-in-windows-server-2016"></a>Windows Server 2016에서에서 MultiPoint Service로 마이그레이션

>적용 대상: Windows Server 2016

다음 단계와 Windows Server 2016에서 MultiPoint Service로 마이그레이션하는 마이그레이션 계획 워크시트에서 수집한 정보를 사용 합니다.

## <a name="transfer-server-settings"></a>전송 서버 설정
대상 서버에서 다중 포인트 관리자를 엽니다. 클릭 **서버 설정 편집**합니다. 마이그레이션 계획 워크시트에 따라 설정을 적용 합니다.

> [!NOTE]
> 대상 서버에서 디스크 보호를 사용 하도록 설정 해야 할 경우 MultiPoint 서비스를 구성한 후 될 때까지 기다립니다.

## <a name="transfer-station-settings"></a>전송 스테이션 설정
참여 하는 스테이션 하 고 매핑된 스테이션 설정을 적용 하기 전에 모든 대상 서버에 연결 되어 있는지 확인 합니다. 참여 하는 스테이션을 자동으로 검색 됩니다. 각 스테이션 화면 스테이션 사용자와 연결 된 USB 디바이스는 서버 매핑을 정의 하는 지침을 따릅니다. 마이그레이션 계획 워크시트에 설명 된 대로 기본 스테이션 설정을 적용 합니다.

## <a name="migrate-the-vdi-template"></a>VDI 템플릿이 마이그레이션

원본 서버에서 VDI 서식 파일을 가져오려면 먼저 다중 포인트 관리자를 사용 하 여 대상 서버에서 가상 데스크톱을 사용:

1. 이동 된 **가상 데스크톱** 다중 포인트 관리자 탭 합니다.
2. 클릭 **가상 데스크톱을 사용 하도록 설정**합니다. 서버는 Hyper-v 역할을 설치 하 고 다시 시작 됩니다.
3. 다중 포인트 관리자를 열고 다시 이동 **가상 데스크톱**합니다.
4. 클릭 **가상 데스크톱 템플릿 가져오기**합니다. 원본 서버에서 템플릿을 가져올 지침을 따릅니다.

> [!NOTE]
> 가상 데스크톱 템플릿을 가져오면 템플릿에 적용 하는 모든 사용자 지정 다시 설정 됩니다. 

## <a name="next-step"></a>다음 단계
[새 MultiPoint 서비스 배포의 유효성을 검사 합니다.](multipoint-services-post-migration-steps.md)