---
title: 파일 관리 작업
description: 이 문서에서는 파일 관리 작업을 자동화하는 과정을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 257ee2955c4f521d14f01ec197fd45e5194eef02
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394095"
---
# <a name="file-management-tasks"></a>파일 관리 작업

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 관리 작업은 서버에서 파일의 하위 집합을 찾아 간단한 명령을 적용하는 과정을 자동화합니다. 이러한 작업은 반복 비용을 절감하기 위해 정기적으로 실행하도록 예약할 수 있습니다. 파일 관리 작업으로 처리되는 파일은 다음 중 어떤 속성으로도 정의할 수 있습니다.

-   위치
-   분류 속성
-   생성 시간
-   수정 시간
-   마지막 액세스 시간

파일 관리 작업은 파일 소유자에게 자신의 파일에 곧 적용되는 정책을 알리도록 구성될 수도 있습니다.

> [!Note]
> 개별 파일 관리 작업은 독립 일정으로 실행됩니다.

<br />
이 섹션에서는 다음 항목을 다룹니다.

-   [파일 만료 작업 만들기](create-file-expiration-task.md)
-   [사용자 지정 파일 관리 작업 만들기](create-custom-file-management-task.md)

> [!Note]
> 전자 메일 알림과 특정 보고 기능을 설정하려면, 먼저 일반 파일 서버 리소스 관리자 옵션을 구성해야 합니다.

## <a name="see-also"></a>참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


