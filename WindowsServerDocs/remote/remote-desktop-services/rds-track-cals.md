---
title: 원격 데스크톱 서비스 클라이언트 액세스 라이선스 (RDS Cal)를 추적 합니다.
description: RDS 배포에 걸쳐 Cal을 추적 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80d82d30-3ad0-4a8c-9a9b-2773c47eee19
author: lizap
ms.author: elizapo
ms.date: 05/11/2017
manager: dongill
ms.openlocfilehash: ed7490b2b61eb516d43b280b67fcefaeedb3e225
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890624"
---
# <a name="track-your-remote-desktop-services-client-access-licenses-rds-cals"></a>원격 데스크톱 서비스 클라이언트 액세스 라이선스 (RDS Cal)를 추적 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 데스크톱 라이선스 관리자 도구는 RDS 사용자 Cal 원격 데스크톱 라이선스 서버에서 발급 된 추적 하는 보고서를 만드는 데 사용할 수 있습니다.

> [!NOTE]
>  Azure AD Domain Services를 사용자 환경에서 사용 하는 경우 원격 데스크톱 라이선스 관리자 도구는 사용자 단위 Cal을 가져오려고 작동 하지 않습니다. 대신, 로그온 이벤트, 연결 브로커 또는 적합 한 다른 메커니즘을 통해 폴링 활성 원격 데스크톱 연결을 통해 수동으로 라이선스 추적 해야 합니다. 

다음 단계를 사용 하 여 생성 된 사용자 Cal 보고서 마다:

1. 원격 데스크톱 라이선스 관리자에서 라이선스 서버를 마우스 오른쪽 단추로 클릭 합니다 **보고서 만들기**를 클릭 하 고 **당 사용자 CAL 사용 현황**합니다.
2. 보고서의 범위 설정-다음 중 하나를 선택 합니다.
   - 전체 도메인-라이선스 서버에서의 멤버입니다.
   - 조직 구성 단위-라이선스 서버 멤버인 도메인 내에서 모든 OU입니다.
   - 전체 도메인 및 모든 트러스트 된 도메인-다른 포리스트의 도메인을 포함할 수 있습니다. 이 옵션을 선택 하면 보고서를 만드는 데 걸리는 시간이 늘어날 수 있습니다.

   선택 해야 하는 보고서를 생성 하려면 RDS 사용자 단위 CAL 정보에 대 한 AD DS의 사용자 계정을 검색 됩니다 결정 합니다.
3. 클릭 **보고서를 만들**합니다. 보고서는 생성 및 보고서를 성공적으로 만들어졌는지 확인 하려면 메시지가 표시 됩니다. **확인** 을 클릭하여 메시지를 닫습니다.

사용자가 만든 보고서의 보고서 섹션 라이선스 서버에 대 한 노드 아래에 나타납니다. 보고서는 다음 정보를 제공 합니다.

- 보고서를 만든 날짜 및 시간
- 보고서의 범위 (예: 도메인, OU = Sales, 또는 모든 트러스트 된 도메인)
- RDS 사용자 Cal 라이선스 서버에 설치 된 수
- RDS 사용자 Cal 보고서의 범위를 특정 라이선스 서버에서 발급 된 수

또한 컴퓨터의 폴더 위치에 CSV 파일로 보고서를 저장할 수 있습니다. 보고서를 저장 하려면 보고서를 저장 하 고, 다른 이름으로 저장을 클릭 하 고, 보고서를 저장할 위치와 파일 이름을 지정 하려는 마우스 오른쪽 단추로 클릭 합니다.

만든 보고서는 보고서 노드에 원격 데스크톱 라이선스 관리자에서 라이선스 서버에 대 한 노드 아래에 나열 됩니다. 보고서가 더 이상 필요한 경우에이 삭제할 수 없습니다.
