---
title: 호스트 캐시 서버에서 데이터 패키지 가져오기(선택 사항)
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 440ef1e04143cba09213ffea634aa9d4fea51dab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888004"
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>호스트 캐시 서버에서 데이터 패키지 가져오기 \(옵션\)

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

데이터 패키지를 가져오고 호스트 캐시 서버에서 콘텐츠를 미리 로드 하려면이 절차를 사용할 수 있습니다.

없기 때문에 prehash 내용과 미리 로드 하는 데 필요한 호스트 캐시 서버에서이 절차는 선택 사항입니다.

이전 되지 않으면\-콘텐츠 데이터는 호스트 캐시에 자동으로 추가 클라이언트가 WAN 연결을 통해 다운로드 하는 대로 로드 합니다.

이 절차를 수행 하려면 Administrators 그룹의 구성원 이어야 합니다.

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>데이터를 가져오려면 호스트 캐시 서버에서 패키지를  

1. 서버 컴퓨터에서 관리자 권한으로 Windows PowerShell을 엽니다.

2. 값 경로로 바꿔서 다음 명령을 입력에 대 한 폴더 위치에 데이터 패키지를 저장 한 다음 ENTER 키를-Path 매개 변수입니다.

    ```  
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```  

3. 콘텐츠를 미리 로드 하려면 둘 이상의 호스트 캐시 서버를 설정한 경우 각 호스트 캐시 서버에서이 절차를 수행 합니다.

이 가이드를 계속 하려면 참조 [클라이언트 자동 호스트 캐시 검색 구성 서비스 연결 지점에](10-Bc-Client-By-Scp.md)합니다.
