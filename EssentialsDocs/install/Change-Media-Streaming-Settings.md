---
title: 미디어 스트리밍 설정 변경
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823404"
---
# <a name="change-media-streaming-settings"></a>미디어 스트리밍 설정 변경

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

미디어 스트리밍 설정을 변경하는 데 사용할 수 있는 여러 옵션이 있습니다. 사용할 수 있는 옵션은 다음과 같습니다.  
  
-   [원격 미디어 스트리밍 추가 기능을 숨기려면](Change-Media-Streaming-Settings.md#BKMK_DisableRemote)  
  
-   [미디어 라이브러리 이름 설정](Change-Media-Streaming-Settings.md#BKMK_LibraryName)  
  
-   [비디오 스트리밍 품질 설정](Change-Media-Streaming-Settings.md#BKMK_StreamingQuality)  
  
-   [프로그래밍 방식으로 사용 하도록 설정 하거나 미디어 스트리밍을 사용 하지 않도록 설정](Change-Media-Streaming-Settings.md#BKMK_Program)  
  
##  <a name="BKMK_DisableRemote"></a> 원격 미디어 스트리밍 추가 기능을 숨기려면  
 레지스트리에 항목을 추가하여 원격 미디어 스트리밍을 숨길 수 있습니다.  
  
#### <a name="to-hide-the-remote-media-streaming-add-in"></a>원격 미디어 스트리밍 추가 기능을 숨기려면  
  
1.  서버에서 마우스를 화면 오른쪽 상단 구석으로 옮긴 후 **검색**을 클릭합니다.  
  
2.  **검색** 상자에 **regedit**를 입력하고 **Regedit** 응용 프로그램을 클릭합니다.  
  
3.  왼쪽 창에서 다음 레지스트리 항목을 아래로 확장하세요.  
  
     **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\RemoteAccess\DisabledAddIns**  
  
4.  **DisabledAddIns**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **DWORD 값**을 클릭합니다.  
  
5.  새로운 값으로 원격 미디어 스트리밍 추가 기능 식별자인 **497796c6-9cc7-43be-aa26-4e6b5695370d**를 입력한 다음 **Enter**키를 누릅니다.  
  
6.  값을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
7.  값 데이터로 **1**을 입력한 다음 **확인**을 클릭합니다.  
  
##  <a name="BKMK_LibraryName"></a> 미디어 라이브러리 이름 설정  
 Windows Server Solutions SDK의 클래스를 사용하면 미디어 라이브러리의 이름을 설정할 수 있습니다. 미디어 라이브러리의 이름을 설정하려면 **Microsoft.WindowsServerSolutions.MediaStreaming** 네임스페이스에 있는 **MediaStreamingManager** 클래스의 **SetMediaLibraryName** 메서드를 사용하면 됩니다. 다음 예제에서는 미디어 라이브러리 이름을 설정하는 방법을 보여 줍니다.  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
string mediaLibraryName = Guid.NewGuid().ToString("B");   
mediaStreamingManager.SetMediaLibraryName(mediaLibraryName);  
  
```  
  
 자세한 내용은 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)를 참조하세요.  
  
##  <a name="BKMK_StreamingQuality"></a> 비디오 스트리밍 품질 설정  
 WinSAT CPU 점수를 얻은 다음 WinSAT 점수 정보가 포함된 .xml 파일을 만들고 설치하여 비디오 스트리밍 품질을 설정합니다. 초기 구성이 실행되기 전에 WinSAT 점수 정보가 포함된 .xml 파일을 설치하면 비디오 품질 설정을 위한 사용자 인터페이스가 나타나지 않습니다. 자세한 내용은 [Set the WinSAT Score on the Server](Set-the-WinSAT-Score-on-the-Server.md)를 참조하세요.  
  
##  <a name="BKMK_Program"></a> 프로그래밍 방식으로 사용 하도록 설정 하거나 미디어 스트리밍을 사용 하지 않도록 설정  
 Windows Server Solutions SDK의 클래스를 사용하면 프로그래밍 방식으로 미디어 스트리밍의 사용 여부를 설정할 수 있습니다. 미디어 스트리밍의 사용 여부를 설정하려면 **Microsoft.WindowsServerSolutions.MediaStreaming** 네임스페이스에 있는 **MediaStreamingManager** 클래스의 **SetMediaStreamingEnabled** 메서드를 사용하면 됩니다. 다음 코드 예제에서는 미디어 스트리밍을 사용하도록 설정하는 방법을 보여 줍니다.  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(true);  
  
```  
  
 다음 코드 예제에서는 미디어 스트리밍을 사용하지 않도록 설정하는 방법을 보여 줍니다.  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(false);  
```  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)