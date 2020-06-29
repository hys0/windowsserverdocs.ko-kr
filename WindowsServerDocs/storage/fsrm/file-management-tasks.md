---
title: 파일 관리 작업
description: 이 문서에서는 파일 관리 작업을 자동화 하는 프로세스를 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 402af4bd7c00bedfc3d01d43071af4fcd374d428
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474000"
---
# <a name="file-management-tasks"></a>파일 관리 작업

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 관리 작업은 서버에서 파일의 하위 집합을 찾고 간단한 명령을 적용 하는 프로세스를 자동화 합니다. 이러한 작업은 반복적인 비용을 줄이기 위해 정기적으로 수행 되도록 예약할 수 있습니다. 파일 관리 작업을 통해 처리 되는 파일은 다음 속성 중 하나를 통해 정의할 수 있습니다.

-   위치
-   분류 속성
-   만든 시간
-   수정 시간
-   마지막으로 액세스한 시간

파일 관리 작업은 파일에 적용 되는 모든 임박한 정책의 파일 소유자에 게 알리도록 구성 될 수도 있습니다.

> [!Note]
> 개별 파일 관리 작업은 독립 된 일정에 따라 실행 됩니다.

<br />
이 단원에 포함된 항목은 다음과 같습니다.

-   [파일 만료 작업 만들기](create-file-expiration-task.md)
-   [사용자 지정 파일 관리 작업 만들기](create-custom-file-management-task.md)

> [!Note]
> 전자 메일 알림과 특정 보고 기능을 설정 하려면 먼저 일반 파일 서버 리소스 관리자 옵션을 구성 해야 합니다.

## <a name="additional-references"></a>추가 참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


