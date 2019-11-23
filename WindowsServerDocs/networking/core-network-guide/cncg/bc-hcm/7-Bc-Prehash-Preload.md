---
title: 호스트 캐시 서버에서 콘텐츠 Prehash 및 미리 로드(선택 사항)
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fe206576278b09e4a360c7bb27f5ff076af97be7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356249"
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>호스트 캐시 서버에서 콘텐츠 사전 해시 및 미리 로드 \(선택\)

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 섹션의 절차를 사용 하 여 콘텐츠 서버에서 콘텐츠를 미리 해시 하 고, 데이터 패키지에 콘텐츠를 추가 하 고, 호스트 캐시 서버에서 콘텐츠를 미리 로드할 수 있습니다. 

없기 때문에 prehash 내용과 미리 로드 하는 데 필요한 호스트 캐시 서버에서이 절차는 선택적입니다. 

콘텐츠를 미리 로드 하지 않는 경우 클라이언트가 WAN 연결을 통해 다운로드 하면 자동으로 호스트 캐시에 데이터가 추가 됩니다.

>[!IMPORTANT]
>이러한 절차는 모두 선택적 이지만 호스트 캐시 서버에서 콘텐츠를 미리 로드 하 고 미리 로드 하는 경우에는 두 절차를 모두 수행 해야 합니다.

- [웹 및 파일 콘텐츠에 &#40;대 한 콘텐츠 서버 데이터 패키지 만들기 옵션&#41;](8-Bc-Data-Packages.md)
  
- [호스트 캐시 서버 &#40;에서 데이터 패키지 가져오기 옵션&#41;](9-Bc-Import-Data.md)

이 가이드를 계속 하려면 참조 [웹 및 파일 콘텐츠 & #40; 옵션 & #41;에 대 한 콘텐츠 서버 데이터 패키지 만들기](8-Bc-Data-Packages.md)합니다.