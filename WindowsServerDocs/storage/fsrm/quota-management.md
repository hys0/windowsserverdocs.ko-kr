---
title: 할당량 관리
description: 이 문서에서는 할당량을 만들고 관리하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 6effaf7c2d197c08b4930e09c3ada96462b17d6f
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476189"
---
# <a name="quota-management"></a>할당량 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자 MMC(Microsoft<sup>®</sup> Management Console) 스냅인의 **할당량 관리** 노드에서 다음과 같은 작업을 수행할 수 있습니다.

-   볼륨 또는 폴더에 허용되는 공간을 제한하는 할당량을 만들거나, 할당량 한계에 근접 또는 도달했을 때 알림을 생성합니다.
-   볼륨이나 폴더의 기존 하위 폴더와 나중에 생성될 모든 하위 폴더에 적용되는 할당량 자동 적용을 생성합니다.
-   조직 전체에서 사용할 수 있는 새 볼륨 또는 폴더에 쉽게 적용할 수 있는 할당량 템플릿을 정의합니다.

예를 들어 다음 작업을 할 수 있습니다.

-   저장소의 180 MB 초과 했을 때 하 고 사용자에 게 보낼 전자 메일 알림을 사용 하 여 사용자의 개인 서버 폴더에 200 mb (메가바이트) 한계를 설정 합니다.
-   그룹의 공유 폴더에서 유연성 있는 500MB 할당량을 설정 합니다. 이 저장소 용량 한도 도달 하면 모든 사용자 그룹에 저장소 할당량이 일시적으로 확장 된 520mb 불필요 한 파일을 삭제 하 고 미리 설정 된 500MB 할당량 정책을 준수할 수 있도록 전자 메일로 알림이 표시 됩니다.
-   임시 폴더가 2기가바이트(GB) 사용량에 도달하면 알림을 받지만, 서버의 서비스 실행에 필요하므로 폴더의 할당량을 제한하지는 않습니다.

이 섹션에서는 다음 항목을 다룹니다.

-   [할당량 만들기](create-quota.md)
-   [할당량 자동 적용 만들기](create-auto-apply-quota.md)
-   [할당량 템플릿 만들기](create-quota-template.md)
-   [할당량 템플릿 속성 편집](edit-quota-template-properties.md)
-   [할당량 자동 적용 속성 편집](edit-auto-apply-quota-properties.md)

> [!Note]
> 전자 메일 알림과 보고 기능을 설정하려면, 먼저 일반 파일 서버 리소스 관리자 옵션을 구성해야 합니다.

## <a name="see-also"></a>참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


