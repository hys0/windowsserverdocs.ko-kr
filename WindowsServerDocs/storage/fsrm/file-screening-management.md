---
title: 파일 차단 관리
description: 이 문서에서는 파일 차단을 만들고, 알림을 생성 하 고, 파일 차단 템플릿을 정의 하 고, 파일 차단 예외를 만드는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 43aed09aead02883f91c168e1cfaf6388aedfa85
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473980"
---
# <a name="file-screening-management"></a>파일 차단 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자 MMC 스냅인의 **파일 차단 관리** 노드에서 다음 작업을 수행할 수 있습니다.

-   사용자가 무단 파일을 저장 하려고 할 때 사용자가 저장할 수 있는 파일 형식을 제어 하 고 사용자가 알림을 생성할 수 있도록 파일 화면을 만듭니다.
-   새 볼륨 또는 폴더에 적용할 수 있고 조직 전체에서 사용할 수 있는 파일 차단 템플릿을 정의 합니다.
-   파일 차단 규칙의 유연성을 확장 하는 파일 차단 예외를 만듭니다.

예를 들어, 다음을 수행할 수 있습니다.

-   서버에 있는 개인 폴더에 음악 파일이 저장 되지 않도록 하 고, 법적 권한 관리를 지 원하는 특정 유형의 미디어 파일을 저장 하거나 회사 정책을 준수 하도록 허용할 수 있습니다. 이와 동일한 시나리오에서는 회사의 개인 폴더에 모든 형식의 파일을 저장할 수 있는 특별 한 권한을 부여할 수 있습니다.
-   파일을 저장 한 사용자 및 파일의 정확한 위치에 대 한 정보를 포함 하 여 실행 파일이 공유 폴더에 저장 되는 경우 전자 메일로 알리도록 차단 프로세스를 구현 하 여 적절 한 예비 단계를 수행할 수 있도록 합니다.

이 단원에 포함된 항목은 다음과 같습니다.

-   [차단을 위한 파일 그룹 정의](define-file-groups-for-screening.md)
-   [파일 화면 만들기](create-file-screen.md)
-   [파일 차단 예외 만들기](create-file-screen-exception.md)
-   [파일 차단 템플릿 만들기](create-file-screen-template.md)
-   [파일 차단 템플릿 속성 편집](edit-file-screen-template-properties.md)

> [!Note]
> 전자 메일 알림과 특정 보고 기능을 설정 하려면 먼저 일반 파일 서버 리소스 관리자 옵션을 구성 해야 합니다.

## <a name="additional-references"></a>추가 참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


