---
title: Prehash 및 미리 로드 콘텐츠를 호스트 캐시 서버 (선택 사항)
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0e7ffaac4e427222d5539195ecef91768f61c4a3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>Prehash 및에 호스팅된 콘텐츠를 미리 로드할 서버 \(Optional\) 캐시

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 섹션의 콘텐츠 서버에 콘텐츠를 prehash 데이터 패키지에 내용을 추가 하 고 다음 여 호스팅된 캐시 서버에 콘텐츠를 미리 로드 하는 절차를 사용할 수 있습니다. 

이 절차는 선택적 필요는 prehash 및 미리 로드 콘텐츠를 호스트 캐시 서버의 하기 때문입니다. 

콘텐츠를 로드 하지 않는 경우 데이터는 자동으로 추가 호스트 캐시 클라이언트 WAN 연결을 통해 다운로드할 때.

>[!IMPORTANT]
>이 절차 집합적으로 선택 사항 이지만, 여 호스팅된 캐시 서버에 콘텐츠를 미리 로드 하 고 prehash 하려는 경우 필요한는 모두 절차를 수행 합니다.

- [#40, 웹 및 파일 내용에 대 한 콘텐츠 서버 데이터 패키지 만들 옵션 & #41;](8-Bc-Data-Packages.md)
  
- [가져오기 데이터 패키지 호스트 캐시 서버 및 #40; 옵션 & #41;](9-Bc-Import-Data.md)

이 가이드를 계속 참조 [웹 및 파일 콘텐츠 & #40; 옵션 & #41;에 대 한 콘텐츠 서버 데이터 패키지 만들기 ](8-Bc-Data-Packages.md).