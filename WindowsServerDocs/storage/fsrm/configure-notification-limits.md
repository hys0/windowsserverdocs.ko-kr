---
title: 알림 제한 구성
description: 이 문서에서는 다양 한 알림 유형에 시간 제한을 추가 하는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 32728fc9b19fca458b7ac4b86f3b550d9ff29490
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474170"
---
# <a name="configure-notification-limits"></a>알림 제한 구성

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

반복 해 서 할당량 임계값을 초과 하거나 권한이 없는 파일을 저장 하려고 할 때 누적 되는 알림 수를 줄이려면 파일 서버 리소스 관리자 다음 알림 유형에 시간 제한을 적용 합니다.

-   전자 메일
-   이벤트 로그
-   명령
-   보고서

각 제한은 동일한 문제에 대해 동일한 유형의 다른 구성 된 알림이 생성 되기까지 걸리는 기간을 지정 합니다.

기본 60 분 제한은 각 알림 유형에 대해 설정 되지만 이러한 제한을 변경할 수 있습니다. 이 제한은 할당량 임계값 또는 파일 차단 이벤트에 의해 생성 되는지에 관계 없이 지정 된 형식의 모든 알림에 적용 됩니다.

## <a name="to-specify-a-standard-notification-limit-for-each-notification-type"></a>각 알림 유형에 대 한 표준 알림 제한을 지정 하려면

1.  콘솔 트리에서 **파일 서버 리소스 관리자**를 마우스 오른쪽 단추로 클릭 하 고 **옵션 구성**을 클릭 합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.

2.  **알림 제한** 탭에서 표시 되는 각 알림 유형에 대해 분 단위로 값을 입력 합니다.

3.  **확인**을 클릭합니다.

> [!Note]
> 특정 할당량 또는 파일 화면에 대 한 알림과 관련 된 시간 제한을 사용자 지정 하려면 파일 서버 리소스 관리자 명령줄 도구 **Dirquota.exe** 및 **Filescrn.exe**를 사용 하거나 [파일 서버 리소스 관리자](https://technet.microsoft.com/itpro/powershell/windows/fileserverresourcemanager/fileserverresourcemanager) cmdlet을 사용할 수 있습니다.

## <a name="additional-references"></a>추가 참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)
-   [명령줄 도구](command-line-tools.md)