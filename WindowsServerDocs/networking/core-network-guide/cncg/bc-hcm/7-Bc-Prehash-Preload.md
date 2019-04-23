---
title: 호스트 캐시 서버에서 콘텐츠 Prehash 및 미리 로드(선택 사항)
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b60a1f24b8988d6e394df0faf678467021e0c882
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839394"
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>Prehash 및 호스트 캐시 서버에서 콘텐츠를 미리 로드 \(옵션\)

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

콘텐츠 서버에서 콘텐츠를 prehash 데이터 패키지에 콘텐츠를 추가 하 고 다음 호스트 캐시 서버에서 콘텐츠를 미리 로드 하려면이 단원의 절차를 사용할 수 있습니다. 

없기 때문에 prehash 내용과 미리 로드 하는 데 필요한 호스트 캐시 서버에서이 절차는 선택적입니다. 

콘텐츠를 로드 하지 않는 경우 데이터는 호스트 캐시에 자동으로 추가 클라이언트가 WAN 연결을 통해 다운로드 하는 대로 합니다.

>[!IMPORTANT]
>이러한 절차 전체적으로 선택 사항 이지만, 호스트 캐시 서버에 prehash 내용과 미리 로드 하려는 경우 필요 두 절차를 수행 합니다. 합니다.

- [웹 콘텐츠 서버 데이터 패키지를 만들고 파일 콘텐츠 &#40;선택 사항&#41;](8-Bc-Data-Packages.md)
  
- [호스트 캐시 서버에서 데이터 패키지 가져오기 &#40;선택 사항&#41;](9-Bc-Import-Data.md)

이 가이드를 계속 하려면 참조 [웹 및 파일 콘텐츠 & #40; 옵션 & #41;에 대 한 콘텐츠 서버 데이터 패키지 만들기](8-Bc-Data-Packages.md)합니다.