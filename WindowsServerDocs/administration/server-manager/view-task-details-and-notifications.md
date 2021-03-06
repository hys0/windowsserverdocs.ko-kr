---
title: 작업 세부 정보 및 알림 보기
description: 서버 관리자
ms.prod: windows-server
ms.technology: manage-server-manager
ms.topic: article
ms.assetid: 95117407-2dd3-4f9a-841f-4331be3544c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0047a9f2d4b6b66cec85b2746b1975af2ced3316
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851456"
---
# <a name="view-task-details-and-notifications"></a>작업 세부 정보 및 알림 보기

>적용 대상: Windows Server 2016

서버 관리자에서 Windows Server 2012 R2 또는 Windows Server 2012에서 역할 및 기능을 추가 하는 등의 관리 작업을 수행할 때 서비스, 서버 관리자 콘솔에 표시 되는 데이터 새로 고침 또는 서버의 사용자 지정 그룹을 만드는 시작 알림이 표시 됩니다에 **알림을** 서버 관리자 콘솔 헤더의 영역입니다. 알림 및 작업 **세부 정보** 대화 상자 (플래그 아이콘을 클릭 하 여 **알림** 메뉴에서 열 수 있음), 사용자 작업이 나 요청 상태 표시, 작업 실패 여부 표시, 작업 실패에 대 한 자세한 오류 메시지를 가리켜 문제를 해결 하는 데 도움을 줄 수 있습니다.

## <a name="the-notifications-area"></a>알림 영역
**알림을** 플래그 아이콘으로 표시 하면 서버 관리자 메뉴 모음에서 서버 관리자를 시작 하는 작업의 결과 표시 합니다. 알림 서버 관리자를 시작 하는 작업의 성공 또는 실패 되었는지 여부를 알려 줍니다. 볼 수 있는 알림이 있는 경우 플래그 아이콘 옆에 볼 수 있는 알림 수가 표시됩니다. 작업이 실패하면(작업을 수행하려는 일부 원격 서버에서는 작업을 수행할 수 없는 등 작업이 일부만 완료되거나 작업이 완료되었지만 경고가 있는 경우) **알림** 플래그가 빨간색으로 표시됩니다. 알림이 표시되는 작업은 다음과 같습니다.

-   수동으로 (알림을 고침이 실패 한 경우에 자동 새로 고침에 대 한 표시 됩니다)는 서버 관리자에 표시 된 데이터 새로 고침

-   서비스 시작 또는 중지

-   설치 또는 역할, 역할 서비스 및 기능 제거

-   BPA (모범 사례 분석기) 검사 시작

-   관리할 원격 서버 추가 (원격 서버에 대해 표시 되는 데이터를 연결 하거나 새로 고치지 못한 경우 알림이 표시 됨)

**알림** 메뉴의 항목에는 진행률 표시줄, 작업에 대한 간략한 설명, 작업의 대상 서버 이름(또는 대상 서버가 여러 대 선택된 경우 대상 서버 중 하나), 관련 컨트롤이나 대화 상자에 대한 링크(해당되는 경우) 및 **작업** 메뉴가 표시됩니다. **작업** 메뉴에는 활성 알림(마우스 커서가 놓인 알림)에 적용할 명령이 표시됩니다. 예를 들어 서비스를 중지한 경우 알림의 **작업** 메뉴에서 **다시 시작** 을 클릭하여 서비스를 다시 시작할 수 있습니다.

알림은 설치 하거나 역할, 역할 서비스 및 기능을 제거 하는 데 특히 유용 합니다. 예를 들어 원격 서버에서 기능 설치를 시작 하는 경우 설치가 진행 되는 동안 역할 및 기능 추가 마법사를 닫을 수 있지만 **알림** 목록에는 활성 작업이 유지 됩니다. **알림** 항목에는 설치에 대 한 진행률 표시줄이 표시 되며, 필요한 경우 **역할 및 기능 추가**마법사를 클릭 하 여 역할 및 기능 추가 마법사를 다시 열 수 있습니다. 이 목록의 항목은 설치 성공 여부를 알려주며, 기능 배포를 완료하는 데 있어 추가로 필요한 구성 단계가 있는지도 알려줍니다.

또한 알림은 서버 관리자의 작업 또는 프로세스 관련 문제를 해결 하는 데 중요 한 부분을 재생 합니다. **알림** 영역 및 **작업 세부 정보** 대화 상자의 메시지를 사용 하 여 실패 한 작업 또는 프로세스의 문제를 해결 하는 방법에 대 한 자세한 내용은 [서버 관리자 문제 해결 가이드](https://social.technet.microsoft.com/wiki/contents/articles/13443.windows-server-2012-server-manager-troubleshooting-guide-part-i-overview.aspx)를 참조 하세요.

**알림 목록에서** 더 이상 표시 하지 않을 알림을 삭제 하려면 해당 알림 위에 마우스 커서를 놓고 **작업 제거** (**X**)를 클릭 합니다.

## <a name="viewing-and-troubleshooting-tasks-by-using-task-details"></a>작업 세부 정보를 사용 하 여 작업 보기 및 문제 해결
**알림** 메뉴 하단의 작업 **세부 정보** 명령은 작업 **세부 정보** 대화 상자를 엽니다 .이 대화 상자에서는 작업 이벤트 (시작, 중지, 경고, 성공 또는 실패)에 대 한 전체 설명을 제공 합니다. **이벤트**, **서비스**및 **모범 사례 분석기** 타일과 같은 서버 관리자의 다른 목록 컨트롤과 같이 **작업 세부 정보** 대화 상자에 표시 되는 작업에 대해 실행할 쿼리를 필터링 하 고 만들 수 있습니다. 목록 컨트롤에서 쿼리를 필터링 하 고 만드는 방법에 대 한 자세한 내용은 [서버 관리자 타일에서 데이터 필터링, 정렬 및 쿼리](filter-sort-and-query-data-in-server-manager-tiles.md)를 참조 하세요.) 위쪽 창에서 **알림 메뉴에 표시 된 알림을 검토** 하 고 동일한 작업에 대해 생성 된 알림 수를 확인할 수 있습니다. 위쪽 창에서 알림을 선택 하면 아래쪽 창에 알림에 대 한 자세한 정보가 표시 됩니다.

하단 창은 실패한 작업과 관련하여 문제를 해결할 때 특히 유용합니다. 서버 관리자 서버 풀의 구성원 인 서버에 대 한 데이터에 연결할 수 없거나이 데이터를 가져올 수 없는 경우이 창의 항목에는 대상 서버와의 통신을 서버 관리자 방해 하는 기본 WinRM (Windows 원격 관리), 네트워킹 또는 보안 문제의 전체 텍스트를 비롯 한 자세한 메시지가 포함 되어 있는 경우가 많습니다.

## <a name="see-also"></a>관련 항목
[서버 관리자 타일의 데이터 필터링, 정렬 및 쿼리](filter-sort-and-query-data-in-server-manager-tiles.md)
[서버 관리자 문제 해결 가이드](https://social.technet.microsoft.com/wiki/contents/articles/13443.windows-server-2012-server-manager-troubleshooting-guide-part-i-overview.aspx)
