---
title: 파일 서버 리소스 관리자 문제 해결
description: 이 문서에서는 파일 서버 리소스 관리자를 사용할 때 일반적인 문제를 해결하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 0f30bcfd07f28ecd3fa1618e4f5d89b7a0b4d14f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403090"
---
# <a name="troubleshooting-file-server-resource-manager"></a>파일 서버 리소스 관리자 문제 해결

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

이 섹션에서는 파일 서버 리소스 관리자를 사용할 때 발생할 수 있는 일반적인 문제를 나열합니다.

> [!Note]
> 좋은 문제 해결 방법은 파일 서버 리소스 관리자에서 생성한 이벤트 로그를 확인하는 것입니다. 파일 서버 리소스 관리자에 대한 모든 이벤트 로그 항목은 소스 **SRMSVC**의 **응용 프로그램** 이벤트 로그에서 찾을 수 있습니다.

## <a name="i-am-not-receiving-e-mail-notifications"></a>전자 메일 알림을 받지 못합니다.

-   **원인**: 전자 메일 옵션이 구성 되지 않았거나 잘못 구성 되었습니다.

-   **해결 방법**: **전자 메일 알림** 탭의 **파일 서버 리소스 관리자 옵션** 대화 상자에서 SMTP 서버와 기본 전자 메일 받는 사람을 지정 하 고 유효한 지 확인 합니다. 정보가 올바르고 알림을 보내는 데 사용되는 SMTP 서버가 제대로 작동하는지 확인하기 위해 테스트 전자 메일을 보냅니다. 자세한 내용은 [전자 메일 알림 구성](configure-email-notifications.md)을 참조하세요.


## <a name="i-am-only-receiving-one-e-mail-notification-even-though-the-event-that-triggered-that-notification-happened-several-times-in-a-row"></a>이벤트가 알림 발생을 여러 번 트리거해도 하나의 전자 메일 알림만 받습니다.

-   **원인**: 사용자가 차단 된 파일을 저장 하기 위해 여러 번 시도 하거나 할당량 임계값을 초과 하는 파일을 저장 하는 경우 해당 파일 차단 또는 할당량 이벤트에 대해 구성 된 전자 메일 알림이 있는 경우 60 분 동안 관리자에 게 하나의 전자 메일만 전송 됩니다.  기본. 이는 관리자의 전자 메일 계정이 중복된 메시지가 넘치는 것을 방지합니다.

-   **해결 방법**: **알림 제한** 탭의 **파일 서버 리소스 관리자 옵션** 대화 상자에서 전자 메일, 이벤트 로그, 명령 및 보고서와 같은 각 알림 유형에 대 한 시간 제한을 설정할 수 있습니다. 각 제한은 동일한 문제에 대한 같은 유형의 다른 알림이 생성되기 전의 기간을 지정합니다. 자세한 내용은 [알림 제한 구성](configure-notification-limits.md)을 참조하세요.


## <a name="my-storage-reports-keep-failing-and-little-or-no-information-is-available-in-the-event-log-regarding-the-source-of-the-failure"></a>저장소에 계속 오류가 발생하고 오류의 원인에 관련된 정보가 이벤트 로그에 너무 적거나 없습니다.

-   **원인**: 보고서가 저장 되는 볼륨이 손상 되었을 수 있습니다.
-   **해결 방법**: 볼륨에서 **chkdsk** 를 실행 하 고 보고서를 다시 생성 하십시오.

## <a name="my-file-screening-audit-reports-do-not-contain-any-information"></a>파일 차단 감사 보고서에 아무 정보가 없습니다.

-   **원인**: 다음 중 하나 이상이 원인일 수 있습니다.
    -   감사 데이터베이스가 파일 차단 활동을 기록하도록 구성되지 않았습니다.
    -   감사 데이터베이스가 비어 있습니다. 즉, 기록된 파일 차단 활동이 없습니다.
    -   파일 차단 감사 파일 보고서에 매개 변수가 감사 데이터베이스에서 데이터를 선택하지 않습니다.
    
-   **해결 방법**: 파일 **화면 감사** 탭의 **파일 서버 리소스 관리자 옵션** 대화 상자에서 **감사 데이터베이스의 파일 차단 작업 기록** 확인란이 선택 되어 있는지 확인 합니다.
    -   파일 차단 활동 기록에 대한 자세한 내용은 [파일 차단 감사 구성](configure-file-screen-audit.md)을 참조하세요.
    -   파일 차단 감사 파일 보고서에 대한 기본 매개 변수를 구성하려면 [저장소 보고서 구성](configure-storage-reports.md)을 참조하세요.
    -   예약된 보고서 작업이나 주문형 보고서에 대한 보고서 매개 변수를 편집하려면 [저장소 보고서 관리](storage-reports-management.md)를 참조하세요.

## <a name="the-used-and-available-values-for-some-of-the-quotas-i-have-created-do-not-correspond-to-the-actual-limit-setting"></a>제가 만든 일부 할당량의 "사용된" 값과 "사용 가능한" 값이 실제 "제한" 설정과 일치하지 않습니다.

-   **원인**: 중첩 된 할당량이 있을 수 있습니다 .이 경우 하위 폴더의 할당량은 부모 폴더의 할당량에서 더 제한적인 제한을 가집니다. 예를 들어, 상위 폴더에 100메가바이트(MB)의 할당량 제한이 적용되어 있고 각 하위 폴더에 별도로 200MB의 할당량이 적용되어 있는 경우입니다. 상위 폴더에 총 50MB(하위 폴더에 저장된 데이터의 합계)의 데이터가 저장되어 있다면, 각 하위 폴더는 50MB의 사용 가능 공간만 나열하게 됩니다.

-   **해결 방법**: **할당량 관리**에서 **할당량**을 클릭 합니다. **결과** 창에서 문제를 해결하려는 할당량 항목을 선택합니다. **작업** 창에서 **폴더에 영향을 주는 할당량 보기**를 클릭한 다음 상위 폴더에 적용되는 할당량을 확인합니다. 이렇게 하면 선택한 할당량보다 더 적은 저장소 제한 설정을 가진 상위 폴더 할당량을 파악할 수 있습니다.

