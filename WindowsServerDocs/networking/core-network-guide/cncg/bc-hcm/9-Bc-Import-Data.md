---
title: (옵션) 호스트 캐시 서버에 데이터 패키지 가져오기
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e0bd8f12ab76c8e2bf03ba79ce46a4cbea2f4dc5
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>여 호스팅된에 데이터 패키지 가져오기 서버 \(Optional\) 캐시

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 절차를 데이터 패키지 가져오고 여 호스팅된 캐시 서버에 콘텐츠를 미리 로드할 사용할 수 있습니다.

이 절차 선택적 되므로 사용자 필요 하지 않은 prehash 및 미리 로드 콘텐츠를 호스트 캐시 서버에 합니다.

Pre\ 로드 콘텐츠가 아님을 할 경우 데이터 호스트 캐시를 자동으로 추가 됩니다 클라이언트 WAN 연결을 통해 다운로드 합니다.

이 절차를 수행 하려면 관리자가 그룹의 회원 있어야 합니다.

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>호스트 캐시 서버에 데이터 패키지를 가져오려면  

1. 서버 컴퓨터에서 Windows PowerShell을 관리자 권한으로 엽니다.

2. 값 교체 다음 명령을 입력-경로 매개 폴더 위치 데이터 패키지를 저장 한 다음 ENTER 키를 사용 합니다.

    ```  
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```  

3. 둘 이상의 호스트 캐시 서버 콘텐츠를 미리 로드할 하려는 경우 각 호스트 캐시 서버의이 절차를 수행 합니다.

이 가이드를 계속 참조 [구성 클라이언트 자동 호스트 캐시 검색 서비스 연결 지점에서](10-Bc-Client-By-Scp.md)합니다.
