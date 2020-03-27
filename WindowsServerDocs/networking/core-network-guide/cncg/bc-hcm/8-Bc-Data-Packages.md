---
title: 웹 및 파일 콘텐츠에 대해 콘텐츠 서버 데이터 패키지 만들기(선택 사항)
description: 이 가이드에서는 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 호스트 캐시 모드로 BranchCache를 배포 하는 방법 지침을 제공
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a02741b163aafe12c52bf0afb4c235aa9436347a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318443"
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>웹 및 파일 콘텐츠에 대해 콘텐츠 서버 데이터 패키지 만들기(선택 사항)

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 절차를 사용 하 여 웹 및 파일 서버에서 콘텐츠를 미리 해시 한 다음 호스트 캐시 서버에서 가져올 데이터 패키지를 만들 수 있습니다. 

없기 때문에 prehash 내용과 미리 로드 하는 데 필요한 호스트 캐시 서버에서이 절차는 선택 사항입니다. 콘텐츠를 미리 로드 하지 않는 경우 클라이언트가 WAN 연결을 통해 다운로드 하면 자동으로 호스트 캐시에 데이터가 추가 됩니다.

이 절차에서는 파일 서버와 웹 서버 모두에서 콘텐츠를 미리 해시 하는 방법에 대 한 지침을 제공 합니다. 이러한 유형의 콘텐츠 서버 중 하나가 없는 경우 해당 콘텐츠 서버 유형에 대 한 지침을 수행 하지 않아도 됩니다.

>[!IMPORTANT]
>이 절차를 수행 하기 전에 콘텐츠 서버에 BranchCache를 설치 하 고 구성 해야 합니다. 또한 콘텐츠 서버에서 서버 암호를 변경 하려는 경우 않은 하기 전에 이전\-콘텐츠 해시 – 서버 암호를 수정 합니다. 이전에 무효화\-해시를 생성 합니다.

이 절차를 수행하려면 Administrators 그룹의 멤버여야 합니다.

## <a name="to-create-content-server-data-packages"></a>콘텐츠 서버 데이터 패키지를 만들려면

1. 각 콘텐츠 서버에서 미리 해시 하 여 데이터 패키지에 추가 하려는 폴더 및 파일을 찾습니다. 이 절차의 뒷부분에서 데이터 패키지를 저장 하려는 폴더를 식별 하거나 만듭니다.

2. 서버 컴퓨터에서 관리자 권한으로 Windows PowerShell을 엽니다.

3. 보유 한 콘텐츠 서버 유형에 따라 다음 중 하나 또는 둘 다를 수행 합니다.

    > [!NOTE]
    > – Path 매개 변수의 값은 콘텐츠가 있는 폴더입니다. 아래 명령의 예제 값을 미리 해시 하 고 패키지에 추가 하려는 데이터가 포함 된 콘텐츠 서버의 유효한 폴더 위치로 바꾸어야 합니다.
  
    - 사전 해시 하려는 콘텐츠가 파일 서버에 있는 경우 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.

        ```  
        Publish-BCFileContent -Path D:\share -StageData
        ```  

    -   Prehash 할 콘텐츠가 웹 서버에 있는 경우 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.

        ```  
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```  

4. 각 콘텐츠 서버에서 다음 명령을 실행 하 여 데이터 패키지를 만듭니다. 예를 들어 값을 바꿉니다 \(d:\\temp\) 식별 되거나이 절차의 앞부분에서 만든 위치와-대상 매개 변수입니다.

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. 콘텐츠 서버에서 콘텐츠를 미리 로드 하려는 호스트 캐시 서버의 공유에 액세스 하 고 호스트 캐시 서버의 공유에 데이터 패키지를 복사 합니다.

이 가이드를 계속 하려면 참조 [호스트 캐시 서버 & #40; 옵션 & #41;에서 가져올 데이터 패키지](9-Bc-Import-Data.md)합니다.

