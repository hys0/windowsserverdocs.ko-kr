---
title: MultiPoint 서비스-마이그레이션 후 작업
description: 유효성을 검사 하 여 MultiPoint 서비스 마이그레이션을 종료 하는 방법을 알아봅니다
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1497cae0-071e-467d-89b8-a7050815d7de
author: lizap
manager: dongill
ms.openlocfilehash: e3fa3c812355a14289ea4eeff3ab1e7e92e00d97
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863504"
---
# <a name="multipoint-services---post-migration-tasks"></a>MultiPoint 서비스-마이그레이션 후 작업

>적용 대상: Windows Server 2016

Windows Server 2016에서 MultiPoint Service를 마이그레이션한 후 마이그레이션을 확인 하 고 정리 단계를 수행 하려면 다음 정보를 사용 합니다.

## <a name="validate-the-migration-by-running-a-pilot-program"></a>파일럿 프로그램을 실행 하 여 마이그레이션 확인

프로덕션 환경에서 파일럿 프로젝트를 만들어 MultiPoint 서비스 마이그레이션을 확인할 수 있습니다. 프로덕션 배포가 예상 대로 작동 하는지 확인 하려면 마이그레이션된 역할 서비스를 배포 하기 전에 서버에서 파일럿 프로젝트를 실행 합니다. 느린 MultiPoint 서비스에 액세스 하는 사용자의 수를 늘리면 처음에는 연결의 수를 제한 하는 것이 좋습니다.

> [!NOTE] 
> 항상 마이그레이션을 테스트 하려면 테스트 계정을 사용 합니다. 계정 관리자 권한을 가진 계정을 사용 하 여 유효한 사용자에 대 한.

## <a name="retire-the-source-server"></a>원본 서버 사용 중지
마이그레이션의 유효성을 검사 한 후 종료 하거나 네트워크에서 원본 서버를 분리 합니다. 서버를 도메인에 가입 된 경우 제거 도메인에서이 연결을 끊기 전에 합니다.

