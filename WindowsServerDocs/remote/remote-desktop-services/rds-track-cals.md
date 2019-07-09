---
title: RDS CAL(원격 데스크톱 서비스 클라이언트 액세스 라이선스) 추적
description: RDS 배포에서 CAL을 추적하는 방법을 알아봅니다.
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
ms.openlocfilehash: a3b106a23660e1608231623bfd048669d97f9719
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63712009"
---
# <a name="track-your-remote-desktop-services-client-access-licenses-rds-cals"></a>RDS CAL(원격 데스크톱 서비스 클라이언트 액세스 라이선스) 추적

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

원격 데스크톱 라이선스 관리자 도구를 사용하면 원격 데스크톱 라이선스 서버에서 발급된 RDS 사용자 단위 CAL을 추적하는 보고서를 만들 수 있습니다.

> [!NOTE]
>  Azure AD Domain Services를 사용자 환경에서 사용하는 경우 원격 데스크톱 라이선스 관리자 도구는 사용자 단위 CAL을 가져오려고 작동하지 않습니다. 대신 로그온 이벤트, 연결 브로커를 통해 활성 원격 데스크톱 연결을 폴링하거나 사용자에게 적합한 다른 메커니즘을 통해 라이선스를 수동으로 추적해야 합니다. 

다음 단계를 사용하여 사용자 단위 CAL 보고서를 생성합니다.

1. 원격 데스크톱 라이선스 관리자에서 라이선스 서버를 마우스 오른쪽 단추로 클릭하고, **보고서 만들기**를 클릭한 다음, **사용자 단위 CAL 사용 현황**을 클릭합니다.
2. 보고서의 범위 설정 - 다음 중 하나를 선택합니다.
   - 전체 도메인 - 라이선스 서버가 멤버인 도메인입니다.
   - 조직 구성 단위 - 라이선스 서버가 멤버인 도메인 내 모든 OU입니다.
   - 전체 도메인 및 모든 트러스트된 도메인 - 다른 포리스트의 도메인을 포함할 수 있습니다. 이 옵션을 선택하면 보고서를 만드는 데 걸리는 시간이 늘어날 수 있습니다.

   사용자가 선택하는 항목이 AD DS에서 보고서를 생성할 RDS 사용자 단위 CAL 정보를 검색하는 사용자 계정을 결정합니다.
3. **보고서 만들기**를 클릭합니다. 보고서가 생성되고 보고서를 성공적으로 생성했음을 확인하는 메시지가 표시됩니다. **확인**을 클릭하여 메시지를 닫습니다.

사용자가 만든 보고서가 라이선스 서버에 대한 노드에 있는 보고서 섹션에 표시됩니다. 보고서는 다음과 같은 정보를 제공합니다.

- 보고서를 만든 날짜 및 시간
- 보고서의 범위(예: 도메인, OU = Sales 또는 모든 트러스트된 도메인)
- 라이선스 서버에 설치된 RDS 사용자 단위 CAL의 수
- 보고서의 범위에 한하여 특정 라이선스 서버에서 발급된 RDS 사용자 단위 CAL의 수

또한 컴퓨터의 폴더 위치에 CSV 파일로 보고서를 저장할 수 있습니다. 보고서를 저장하려면 저장할 보고서를 마우스 오른쪽 단추로 클릭하고, 다른 이름으로 저장을 클릭한 다음, 보고서를 저장할 위치와 파일 이름을 지정합니다.

만든 보고서는 원격 데스크톱 라이선스 관리자에서 라이선스 서버에 대한 노드에 있는 보고서 노드에 나열됩니다. 보고서가 더 이상 필요 없는 경우 삭제할 수 있습니다.
