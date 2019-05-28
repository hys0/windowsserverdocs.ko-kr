---
title: 파일 차단 관리
description: 이 문서에서는 파일 차단을 만들고, 알림을 생성하고, 파일 차단 템플릿을 정의하고, 파일 차단 예외를 만드는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 05fcaf402347d16bf8c28528d402664ae5f99165
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476063"
---
# <a name="file-screening-management"></a>파일 차단 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자 MMC 스냅인의 **파일 차단 관리** 노드에서 다음과 같은 작업을 수행할 수 있습니다.

-   사용자가 저장할 수 있는 형식의 파일을 제어하기 위한 파일 차단을 만들고, 사용자가 허용되지 않은 파일을 저장하려고 시도하면 알림을 생성합니다.
-   조직 전체에서 사용할 수 있는 새 볼륨 또는 폴더에 적용할 수 있는 파일 차단 템플릿을 정의합니다.
-   파일 차단 규칙의 유연성을 확장하는 파일 차단 예외를 만듭니다.

예를 들어 다음 작업을 할 수 있습니다.

-   서버의 개인 폴더에 음악 파일이 저장되지 않도록 하고, 법적 권한 관리를 지원하거나 회사 정책을 준수하는 특정 형식의 미디어 파일 저장은 허용합니다. 동일한 시나리오에서 회사의 부사장에게 자신의 개인 폴더에 모든 형식의 파일을 저장할 수 있는 특별한 권한을 부여할 수 있습니다.
-   공유 폴더에 실행 파일이 저장될 때, 파일을 저장한 사용자와 파일의 정확한 위치에 대한 정보가 포함된 알림을 전자 메일로 알리는 차단 프로세스를 구현하여 예방 조치를 수행할 수 있도록 합니다.

이 섹션에서는 다음 항목을 다룹니다.

-   [차단을 위한 파일 그룹 정의](define-file-groups-for-screening.md)
-   [파일 화면 만들기](create-file-screen.md)
-   [파일 차단 예외 만들기](create-file-screen-exception.md)
-   [파일 차단 템플릿 만들기](create-file-screen-template.md)
-   [파일 차단 템플릿 속성 편집](edit-file-screen-template-properties.md)

> [!Note]
> 전자 메일 알림과 특정 보고 기능을 설정하려면, 먼저 일반 파일 서버 리소스 관리자 옵션을 구성해야 합니다.

## <a name="see-also"></a>참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


