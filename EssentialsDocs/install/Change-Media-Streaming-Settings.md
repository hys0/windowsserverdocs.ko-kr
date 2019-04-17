---
title: "미디어 스트리밍 설정 변경"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dec690d2-f80c-4b09-99d6-3bba41331972
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d34d60e792fcda4d71a4509fe3d1b95fc6e74d0e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="change-media-streaming-settings"></a>미디어 스트리밍 설정 변경

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

여러 옵션은 설정 스트리밍 미디어 변경할 수 있습니다. 다음 옵션을 사용할 수 있습니다.  
  
-   [추가 기능을 스트리밍 원격 미디어 숨기기](Change-Media-Streaming-Settings.md#BKMK_DisableRemote)  
  
-   [미디어 라이브러리 이름 설정](Change-Media-Streaming-Settings.md#BKMK_LibraryName)  
  
-   [스트리밍 동영상 품질 설정](Change-Media-Streaming-Settings.md#BKMK_StreamingQuality)  
  
-   [프로그래밍 방식으로 사용 하거나 스트리밍 미디어 사용 안 함](Change-Media-Streaming-Settings.md#BKMK_Program)  
  
##  <a name="BKMK_DisableRemote"></a>추가 기능을 스트리밍 원격 미디어 숨기기  
 원격 미디어 레지스트리에 항목을 추가 하 여 추가 기능을 스트리밍 숨길 수 있습니다.  
  
#### <a name="to-hide-the-remote-media-streaming-add-in"></a>추가 기능을 스트리밍 원격 미디어 숨기려면  
  
1.  서버에서 화면 오른쪽 위 모서리에 마우스를 이동 하 고 클릭 **검색**합니다.  
  
2.  에 **검색** 상자에 입력 **regedit**, 클릭 한 다음는 **Regedit** 응용 프로그램입니다.  
  
3.  왼쪽된 창에서 다음 레지스트리 항목이 활성화 된 나타날 때까지 아래로 확장:  
  
     **Server\RemoteAccess\DisabledAddIns**  
  
4.  마우스 오른쪽 단추로 클릭 **DisabledAddIns**, 가리킨 **새로**을 차례로 클릭 하 고 **DWORD 값**합니다.  
  
5.  새 값을 입력 **497796c6-9cc7-43be-aa26-4e6b5695370d**는 원격 추가 기능에 스트리밍 미디어에 대 한 식별자 누른 다음 **Enter**합니다.  
  
6.  값을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **수정**합니다.  
  
7.  입력 **1** 값 데이터 및 클릭 **확인**합니다.  
  
##  <a name="BKMK_LibraryName"></a>미디어 라이브러리 이름 설정  
 미디어 라이브러리의 이름을 설정 하는 Windows Server 솔루션 SDK의 클래스를 사용할 수 있습니다. 미디어 라이브러리의 이름을 설정 하려면 사용할 수 있습니다는 **SetMediaLibraryName** 의 방법으로는 **MediaStreamingManager** 클래스은 **Microsoft.WindowsServerSolutions.MediaStreaming** 네임 합니다. 미디어 라이브러리의 이름을 설정 하는 방법은 다음과 같습니다.  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
string mediaLibraryName = Guid.NewGuid().ToString("B");   
mediaStreamingManager.SetMediaLibraryName(mediaLibraryName);  
  
```  
  
 자세한 내용은 참조 [Windows Server 솔루션 SDK](https://go.microsoft.com/fwlink/?LinkID=248648)합니다.  
  
##  <a name="BKMK_StreamingQuality"></a>스트리밍 동영상 품질 설정  
 스트리밍 품질을 얻는 WinSAT CPU 점수 로컬 폴더를 만들고.xml WinSAT 점수 정보가 포함 된 파일을 설치 하 여 video를 설정 합니다. WinSAT 점수 정보가 포함 된.xml 파일이 설치 된 경우 초기 구성 실행 하기 전에 사용자 인터페이스 설정 비디오 품질에 대 한 고객에 게 표시 되지 것입니다. 자세한 내용은 참조 [서버에 WinSAT 점수 설정](Set-the-WinSAT-Score-on-the-Server.md)합니다.  
  
##  <a name="BKMK_Program"></a>프로그래밍 방식으로 사용 하거나 스트리밍 미디어 사용 안 함  
 프로그래밍 방식으로 사용 하거나 스트리밍 미디어를 사용 하지 않도록 설정 하는 Windows Server 솔루션 SDK에 사용할 수 있습니다. 를 사용 하거나 스트리밍 미디어를 사용 하지 않도록 설정 하려면 사용할 수 있습니다는 **SetMediaStreamingEnabled** 의 방법으로는 **MediaStreamingManager** 클래스은 **Microsoft.WindowsServerSolutions.MediaStreaming** 네임 합니다. 예제 스트리밍 미디어를 사용 하도록 설정 하는 방법을 보여 줍니다.  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(true);  
  
```  
  
 예제 스트리밍 미디어를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(false);  
```  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)