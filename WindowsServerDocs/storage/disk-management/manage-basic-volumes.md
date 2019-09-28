---
title: 기본 볼륨 관리
description: 이 문서에서는 기본 볼륨을 관리하는 방법을 설명합니다.
ms.date: 10/12/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 2eee5820891c108475c58c9ad024cd7c00391e43
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385921"
---
# <a name="manage-basic-volumes"></a>기본 볼륨 관리

> **적용 대상:** Windows 10, Windows 8.1, Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기본 디스크는 주 파티션, 확장 파티션 또는 논리 드라이브를 포함한 실제 디스크입니다. 기본 디스크의 파티션 및 논리 드라이브는 기본 볼륨이라고도 합니다. 기본 디스크에서는 기본 볼륨만 만들 수 있습니다.

기존 기본 파티션 및 논리 드라이브를 동일한 디스크의 할당되지 않은 인접 공간으로 확장하여 더 많은 공간을 추가할 수 있습니다. 기본 볼륨을 확장하려면 NTFS 파일 시스템으로 포맷되어야 합니다. 확장된 파티션에 포함된 인접한 사용 가능한 공간 내에 논리 드라이브를 확장할 수 있습니다. 확장 파티션의 사용 가능한 공간을 초과하여 논리 드라이브를 확장한 경우 확장 파티션은 인접한 할당되지 않은 공간 다음에 위치하는 한 확장되어 논리 드라이브를 포함합니다.

## <a name="see-also"></a>참고 항목

-   [탑재 지점 폴더 경로를 드라이브에 할당](assign-a-mount-point-folder-path-to-a-drive.md)
-   [기본 볼륨 확장](extend-a-basic-volume.md)
-   [기본 볼륨 축소](shrink-a-basic-volume.md)