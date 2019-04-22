---
title: 로컬 사용자 계정 만들기
description: MultiPoint 서비스에서 사용자 계정에 대 한 thte 세 종류에 알아봅니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33321932-4266-4961-9924-2cb4620bfcb4
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: e2e5a6c79e6dcd603d19ca868df1d11fce2bf746
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823674"
---
# <a name="create-local-user-accounts"></a>로컬 사용자 계정 만들기
다중 포인트 관리자를 사용 하 여 세 가지 수준의 로컬 사용자 계정 만들 수 있습니다. 표준 사용자 계정. 관리자 권한, 제한 된 multiPoint 대시보드 사용자 및 전체 관리 사용자 계정입니다.  
  
MultiPoint 서버에서 로컬 사용자 계정을 만들려면 다음 절차를 따르십시오. 환경의 여러 MultiPoint 서버를 포함 하는 경우 사용자가 모든 서버에서 모든 스테이션에 로그온 할 수 있게 하려는 각 서버에서 로컬 사용자 계정을 만들려면 해야 합니다. 설치 프로그램에 몇 가지 제한 사항이 있습니다. 도메인 환경에서 해당 도메인 계정을 사용 하는 사용자를 시킬 수 있습니다. 옵션의 개요를 참조 하세요 [Windows MultiPoint 서비스 환경에 대 한 사용자 계정 계획](Plan-user-accounts-for-your-MultiPoint-services-environment.md)합니다.  
   
1.  관리자로 서버에 로그온 하 고 다중 포인트 관리자를 엽니다.  
  
2.  클릭 합니다 **사용자** 탭을 클릭 한 다음 **사용자 계정을 추가**합니다.  
  
    사용자 계정 추가 마법사가 열립니다.  
  
3.  새 사용자 계정에 대 한 계정 이름 및 암호를 입력 한 다음 클릭 **다음**합니다.  
  
4.  만들려는 사용자 계정의 유형을 선택 합니다.  
  
    -   **표준 사용자** -스테이션에 로그온 하 고 사용자 작업을 수행할 수 있지만 MultiPoint Server 대시보드를 다중 포인트 관리자에 액세스할 수 없는 및 시스템을 종료할 수 없습니다.  
  
    -   **MultiPoint 대시보드 사용자** -제한 된 관리 권한을 가집니다. 대시보드 사용자 대시보드를 엽니다를 업데이트 하 고 사용자에 게 시스템 로깅 또는 MultiPoint 서버 컴퓨터를 종료와 같이 작업을 수행할 수 있지만 사용자에 대 한 다중 포인트 관리자 없는 합니다.  
  
    -   **관리자에 게** MultiPoint Server에서 전체 관리 권한이 있습니다. 예를 들어, 관리자 수 다중 포인트 관리자를 실행, 추가 및 사용자를 삭제, 시스템 설정을 수정 및 드라이버를 업데이트 합니다.  
  
5.  클릭 **다음**, 클릭 하 고 **마침** 사용자 계정을 만들어야 합니다.