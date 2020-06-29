---
title: 할당량 관리
description: 이 문서에서는 할당량을 만들고 관리 하는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 1f2d584e7d3a0239e38dcadcf6415683d91a4bec
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474201"
---
# <a name="quota-management"></a>할당량 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자 Microsoft<sup>®</sup> Management CONSOLE (MMC) 스냅인의 **할당량 관리** 노드에서 다음 작업을 수행할 수 있습니다.

-   할당량을 만들어 볼륨이 나 폴더에 허용 되는 공간을 제한 하 고 할당량 한도에 도달 하거나 초과 하는 경우 알림을 생성 합니다.
-   볼륨 또는 폴더의 모든 기존 하위 폴더와 앞으로 생성 된 하위 폴더에 적용 되는 자동 적용 할당량을 생성 합니다.
-   새 볼륨 또는 폴더에 쉽게 적용 하 고 조직 전체에서 사용할 수 있는 할당량 템플릿을 정의 합니다.

예를 들어, 다음을 수행할 수 있습니다.

-   사용자에 게 전자 메일 알림이 전송 되 고 180 MB의 저장소가 초과 될 때 사용자에 게 전자 메일 알림이 전송 되는 200 메가바이트 (MB) 제한을 설정 합니다.
-   그룹의 공유 폴더에 유연한 500 MB 할당량을 설정 합니다. 이 저장소 제한에 도달 하면 사용자가 불필요 한 파일을 삭제 하 고 미리 설정 된 500 MB 할당량 정책을 준수할 수 있도록 저장소 할당량이 일시적으로 520 MB로 확장 되었다는 전자 메일로 그룹의 모든 사용자에 게 알립니다.
-   임시 폴더가 2gb의 사용량에 도달 하는 경우 알림을 받습니다. 서버에서 실행 되는 서비스에 필요 하기 때문에 해당 폴더의 할당량을 제한 하지 않습니다.

이 단원에 포함된 항목은 다음과 같습니다.

-   [할당량 만들기](create-quota.md)
-   [할당량 자동 적용 만들기](create-auto-apply-quota.md)
-   [할당량 템플릿 만들기](create-quota-template.md)
-   [할당량 템플릿 속성 편집](edit-quota-template-properties.md)
-   [할당량 자동 적용 속성 편집](edit-auto-apply-quota-properties.md)

> [!Note]
> 전자 메일 알림 및 보고 기능을 설정 하려면 먼저 일반 파일 서버 리소스 관리자 옵션을 구성 해야 합니다.

## <a name="additional-references"></a>추가 참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)


