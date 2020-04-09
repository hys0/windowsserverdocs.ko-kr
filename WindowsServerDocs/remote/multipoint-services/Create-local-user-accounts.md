---
title: 로컬 사용자 계정 만들기
description: MultiPoint 서비스의 세 가지 종류의 사용자 계정 알아보기
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 33321932-4266-4961-9924-2cb4620bfcb4
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: b07c88e4961544f5854f6e9d829b8d4b97adf7e8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859766"
---
# <a name="create-local-user-accounts"></a>로컬 사용자 계정 만들기
다중 포인트 관리자 (표준 사용자 계정)를 사용 하 여에서 세 가지 수준의 로컬 사용자 계정을 만들 수 있습니다. 관리 권한이 제한 된 MultiPoint 대시보드 사용자 및 전체 관리 사용자 계정.  
  
다음 절차를 사용 하 여 MultiPoint server에서 로컬 사용자 계정을 만들 수 있습니다. 환경에 다중 MultiPoint 서버가 포함 되어 있는 경우 사용자가 임의의 서버에 있는 모든 스테이션에 로그온 할 수 있도록 하려면 각 서버에서 로컬 사용자 계정을 만들어야 합니다. 이 설치에는 몇 가지 제한 사항이 있습니다. 도메인 환경에서는 사용자가 도메인 계정을 사용 하도록 할 수도 있습니다. 옵션에 대 한 개요는 [Windows MultiPoint 서비스 환경에 대 한 사용자 계정 계획](Plan-user-accounts-for-your-MultiPoint-services-environment.md)을 참조 하세요.  
   
1.  관리자 권한으로 서버에 로그온 하 여 다중 포인트 관리자를 엽니다.  
  
2.  **사용자** 탭을 클릭 한 다음 **사용자 계정 추가**를 클릭 합니다.  
  
    사용자 계정 추가 마법사가 열립니다.  
  
3.  새 사용자 계정에 대 한 계정 이름 및 암호를 입력 하 고 **다음**을 클릭 합니다.  
  
4.  만들려는 사용자 계정 유형 선택:  
  
    -   **표준 사용자** -스테이션에 로그온 하 여 사용자 작업을 수행할 수는 있지만 multipoint 관리자 또는 Multipoint Server 대시보드에 대 한 액세스 권한은 없으며 시스템을 종료할 수 없습니다.  
  
    -   **MultiPoint 대시보드 사용자** 에 게는 제한 된 관리 권한이 있습니다. 대시보드 사용자는 대시보드를 열고 사용자를 시스템에서 로그 오프 하거나 MultiPoint Server 컴퓨터를 종료 하는 등의 작업을 수행할 수 있지만 사용자는 MultiPoint 관리자에 액세스할 수 없습니다.  
  
    -   **관리자** 에는 MultiPoint Server에 대 한 모든 관리 권한이 있습니다. 예를 들어 관리자가 MultiPoint 관리자를 실행 하 고, 사용자를 추가 및 삭제 하 고, 시스템 설정을 수정 하 고, 드라이버를 업데이트할 수 있습니다.  
  
5.  **다음**을 클릭 한 다음 **마침** 을 클릭 하 여 사용자 계정을 만듭니다.