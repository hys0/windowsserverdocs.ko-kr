---
title: 만들기 콘텐츠가 서버 데이터 패키지 파일 및 웹 콘텐츠 (선택 사항)
description: 이 가이드 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache 배포에 대해 설명
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8f814bbac5c74081259d8eef6deda79d914bfec7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>만들기 콘텐츠가 서버 데이터 패키지 파일 및 웹 콘텐츠 (선택 사항)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 절차 prehash 파일 및 웹 서버에 콘텐츠를 사용 하 고을 가져오려면 여 호스팅된 캐시 서버에 데이터 패키지를 만들 수 있습니다. 

이 절차 선택적 되므로 사용자 필요 하지 않은 prehash 및 미리 로드 콘텐츠를 호스트 캐시 서버에 합니다. 콘텐츠를 로드 하지 않는 경우 데이터는 자동으로 추가 호스트 캐시 클라이언트 WAN 연결을 통해 다운로드할 때.

이 절차 prehashing 콘텐츠 파일 서버 및 웹 서버에 대 한 지침을 제공 합니다. 하지 않은 경우 이러한 유형의 콘텐츠 서버 중 하나를 해당 콘텐츠 서버 유형에 대 한 지침을 수행 하려면 필요가 없습니다.

>[!IMPORTANT]
>이 절차를 수행 하기 전에 설치 하 고 콘텐츠 서버의 BranchCache 구성 해야 합니다. 또한 서버 시크릿 콘텐츠 서버에 변경 하려는 경우 이렇게 pre\ 해시 전에 콘텐츠 – 해시 previously\ 생성 무효화 서버 시크릿 수정 합니다.

이 절차를 수행 하려면 관리자가 그룹의 회원 이어야 합니다.

## <a name="to-create-content-server-data-packages"></a>서버를 만들려면 콘텐츠 데이터 패키지

1. 각 콘텐츠 서버의 prehash 데이터 패키지를 추가 하 고 파일과 폴더를 찾습니다. 사용자의 신원을 확인 하거나 나중에이 절차의 데이터 패키지를 저장 하려면 폴더를 만듭니다.

2. 서버 컴퓨터에서 Windows PowerShell을 관리자 권한으로 엽니다.

3. 해야 하는 서버 콘텐츠 종류에 따라 다음 중 하나 이상을 수행 합니다.

    > [!NOTE]
    > 값 – 경로 대 한 매개 콘텐츠 있는 폴더를입니다. 원하는 prehash 패키지를 추가 하는 데이터를 포함 하는 콘텐츠 서버의 올바른 폴더 위치를으로 명령 아래에 들어 값 바꿔야 합니다.
  
    - 파일 서버에 prehash 하려는 콘텐츠를 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

        ```  
        Publish-BCFileContent -Path D:\share -StageData
        ```  

    -   Prehash 하려는 콘텐츠를 웹 서버에 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

        ```  
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```  

4. 각 콘텐츠 서버에서 다음 명령을 실행 하 여 데이터 패키지를 만듭니다. 예제 값 \(D:\\temp\) 교체 식별 되거나 만든이 절차의 시작 부분에 있는 위치와 목적지 매개 – 합니다.

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. 콘텐츠 서버에서 공유 콘텐츠를 미리 로드할 하려는 여 호스팅된 캐시 서버에 액세스 하 고 공유 호스트 캐시 서버에 데이터 패키지를 복사 합니다.

이 가이드를 계속 참조 [캐시 호스트 서버 #40; 옵션 & #41; 데이터 패키지 가져오기 ](9-Bc-Import-Data.md).

