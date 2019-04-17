---
title: "할당량 관리"
description: "이 문서에서는 할당량을 만들고 관리하는 방법을 설명합니다."
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 60436f12e07b8a3f16312829d53a2885c98f30ed
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="quota-management"></a>할당량 관리

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자 MMC(Microsoft<sup>®</sup> Management Console) 스냅인의 **할당량 관리** 노드에서 다음과 같은 작업을 수행할 수 있습니다.

-   볼륨 또는 폴더에 허용되는 공간을 제한하는 할당량을 만들거나, 할당량 한계에 근접 또는 도달했을 때 알림을 생성합니다.
-   볼륨이나 폴더의 기존 하위 폴더와 나중에 생성될 모든 하위 폴더에 적용되는 할당량 자동 적용을 생성합니다.
-   조직 전체에서 사용할 수 있는 새 볼륨 또는 폴더에 쉽게 적용할 수 있는 할당량 템플릿을 정의합니다.

예를 들어 다음과 같이 할 수 있습니다.

-   사용자의 개인 서버 폴더에 200메가바이트(MB)의 제한을 설정하고, 180MB의 저장소를 초과했을 때 자신과 사용자에게 전자 메일 알림을 보냅니다.
-   그룹의 공유 폴더에 유연한 500MB 할당량을 설정합니다. 이 저장소 제한에 도달하는 경우, 불필요한 파일을 삭제하고 사전 설정된 500MB 할당량 정책을 준수할 수 있도록 저장소 할당량이 일시적으로 520MB까지 확장되었다는 알림이 전자 메일을 통해 그룹의 모든 사용자에게 제공됩니다.
-   임시 폴더가 2기가바이트(GB) 사용량에 도달하면 알림을 받지만, 서버의 서비스 실행에 필요하므로 폴더의 할당량을 제한하지는 않습니다.

이 섹션에는 다음 항목이 포함됩니다.

-   [할당량 만들기](create-quota.md)
-   [할당량 자동 적용 만들기](create-auto-apply-quota.md)
-   [할당량 템플릿 만들기](create-quota-template.md)
-   [할당량 템플릿 속성 편집](edit-quota-template-properties.md)
-   [자동 적용 할당량 속성 편집](edit-auto-apply-quota-properties.md)

> [!Note]
> 전자 메일 알림과 보고 기능을 설정하려면, 먼저 일반 파일 서버 리소스 관리자 옵션을 구성해야 합니다.

## <a name="see-also"></a>참고 항목

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


