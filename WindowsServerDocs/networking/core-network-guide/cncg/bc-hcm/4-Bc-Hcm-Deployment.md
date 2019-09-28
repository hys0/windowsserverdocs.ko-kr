---
title: BranchCache 호스트 캐시 모드 배포
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server
ms.suite: na
ms.technology: networking-bc
ms.topic: article
ms.assetid: c635fa48-d064-4b8b-9dce-9f26abfbcfa4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8734942e6d048df4be0107c67af7a2f741845e8b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406402"
---
# <a name="branchcache-hosted-cache-mode-deployment"></a>BranchCache 호스트 캐시 모드 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

BranchCache 호스트 캐시 모드 배포 프로세스를 안내 하는 자세한 절차 항목에 대 한 링크에 대 한이 항목을 사용할 수 있습니다.

BranchCache 호스트 캐시 모드를 배포 하려면 다음 단계를 수행 합니다.

- [서비스 연결 지점으로 BranchCache 기능을 설치 하 고 호스트 캐시 서버 구성](5-Bc-Feature-Scp.md)

- [호스트 캐시 &#40;이동 및 크기 조정 옵션&#41;](6-Bc-Move-Resize-Cache.md)

- [호스팅된 캐시 서버 &#40;에서 콘텐츠 사전 해시 및 미리 로드 옵션&#41;](7-Bc-Prehash-Preload.md)

- [서비스 연결 지점에의 한 클라이언트 자동 호스트 캐시 검색 구성](10-Bc-Client-By-Scp.md)

>[!NOTE]
>이 가이드의 절차에는 사례에 대 한 지침을 포함 하지 마십시오는 **사용자 계정 컨트롤** 를 계속 하려면 권한이 요청 대화 상자가 열립니다. 이 가이드의 절차를 수행 하는 사용자의 작업에 대 한 응답에서 대화 상자를 연 경우 클릭 하는 동안이 대화 상자가 열리면 **계속**합니다.

이 가이드를 계속 하려면 참조 [BranchCache 기능을 설치 하 고 서비스 연결 지점별 호스트 캐시 서버 구성](5-Bc-Feature-Scp.md)합니다.