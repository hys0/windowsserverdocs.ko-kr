---
title: 설정에 탭 추가
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aac6b7f3-9020-46c3-a83f-b81542300385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a37fd65b143e800a76bac9a77daa4b400426c805
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310160"
---
# <a name="add-a-tab-to-settings"></a>설정에 탭 추가

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

운영 체제의 설정 관리자에서 사용되는 코드 어셈블리를 만들어 설치함으로써 대시보드의 설정에 탭을 추가할 수 있습니다.  
  
## <a name="add-a-tab-to-settings"></a>설정에 탭 추가  
 다음 작업을 수행하여 설정에 탭을 추가할 수 있습니다.  
  
-   [어셈블리에 ISettingsData 인터페이스 구현 추가](Add-a-Tab-to-Settings.md#BKMK_ISettingsData).  
  
-   [Authenticode 서명으로 어셈블리에 서명합니다](Add-a-Tab-to-Settings.md#BKMK_SignAssembly).  
  
-   [어셈블리를 참조 컴퓨터에 설치](Add-a-Tab-to-Settings.md#BKMK_InstallAssembly).  
  
###  <a name="add-an-implementation-of-the-isettingsdata-interface-to-the-assembly"></a><a name="BKMK_ISettingsData"></a>어셈블리에 ISettingsData 인터페이스의 구현을 추가 합니다.  
 ISettingsData 인터페이스는 \Program Files\Windows Server\Bin에 위치한 AdminCommon.dll 어셈블리의 Microsoft.WindowsServerSolutions.Settings 네임스페이스에 포함되어 있습니다.  
  
##### <a name="to-add-the-isettingsdata-code-to-the-assembly"></a>어셈블리에 ISettingsData 코드를 추가하려면  
  
1.  **시작** 메뉴에서 프로그램을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택하여 관리자로 Visual Studio 2010을 엽니다.  
  
2.  **파일**, **새로 만들기**를 차례로 클릭한 다음 **프로젝트**를 클릭합니다.  
  
3.  **새 프로젝트** 대화 상자에서 **Visual C#** , **클래스 라이브러리**를 차례로 클릭하고, 솔루션 이름에 **DashboardSettingsPage**를 입력한 다음 **확인**을 클릭합니다.  
  
    > [!IMPORTANT]
    >  서버에 설치하는 어셈블리 이름은 DashboardSettingsPage.dll이어야 하며 이 dll 파일을 %ProgramFiles%\Windows Server\Bin\OEM으로 복사해야 합니다.  
  
4.  탭에서 사용할 컨트롤을 만듭니다. 이 예제에서 settings 컨트롤의 이름은 MySettingsControl로 지정 됩니다.  
  
5.  Class1.cs 파일의 이름을 바꿉니다. 예를 들면 MySettingTab.cs입니다.  
  
6.  AdminCommon.dll 파일에 참조를 추가합니다.  
  
7.  다음 Using 문을 추가합니다.  
  
    ```c#  
    using Microsoft.WindowsServerSolutions.Settings;  
    ```  
  
8.  네임스페이스 및 클래스 헤더를 다음 예에 맞게 변경합니다.  
  
    ```  
  
    namespace DashboardSettingsPage  
    {  
        public class MySettingTab : ISettingsData  
        {  
        }  
    }  
  
    ```  
  
9. 탭에 대해 만든 컨트롤의 인스턴스를 인스턴스화합니다. 예를 들어:  
  
    ```c#  
    private MySettingsControl tab;  
    ```  
  
10. 클래스의 생성자를 추가합니다. 다음 코드 예제에서는 생성자를 보여 줍니다.  
  
    ```  
  
    public MySettingTab()  
    {  
       tab = new MySettingsControl();  
    }  
    ```  
  
11. Commit 메서드를 추가합니다. 이 메서드는 설정 변경 사항을 전송합니다. 다음 코드 예제에서는 Commit 메서드를 보여 줍니다.  
  
    ```  
  
    void ISettingsData.Commit(bool dismissed)  
    {  
       // Implement the code that is required to submit your setting changes  
    }  
    ```  
  
12. TabControl 메서드를 추가 합니다 .이 메서드는 탭에 대 한 컨트롤을 식별 합니다. 다음 코드 예제에서는 TabControl 메서드를 보여 줍니다.  
  
    ```  
  
    System.Windows.Forms.Control ISettingsData.TabControl  
    {  
       get { return tab; }  
    }  
    ```  
  
13. 탭에 대 한 고유 식별자를 제공 하는 TabId 메서드를 추가 합니다. 다음 코드 예제에서는 TabId 메서드를 보여 줍니다.  
  
    ```  
  
    private Guid id = Guid.NewGuid();  
  
    Guid ISettingsData.TabId  
    {  
       get { return id; }  
    }  
    ```  
  
14. TabOrder 메서드를 추가 합니다 .이 메서드는 탭 순서를 반환 합니다. 다음 코드 예제에서는 TabOrder 메서드를 보여 줍니다.  
  
    ```  
  
    int ISettingsData.TabOrder  
    {  
       get { return 0; }  
    }  
    ```  
  
    > [!NOTE]
    >  탭 순서는 0부터 시작하는 숫자로 정의됩니다. 정의된 탭 순서에 따라 Microsoft 기본 제공 설정 탭이 먼저 표시되고 그 다음에 사용자의 탭이 표시됩니다. 예를 들어 3개의 설정 탭이 있는 경우 탭을 표시할 순서에 따라 탭 순서를 0, 1, 2로 지정합니다.  
  
15. 탭의 제목을 제공 하는 TabTitle 메서드를 추가 합니다. 다음 코드 예제에서는 TabTitle 메서드를 보여 줍니다.  
  
    ```  
  
    string ISettingsData.TabTitle  
    {  
      get { return "My Settings Tab"; }  
    }  
    ```  
  
    > [!NOTE]
    >  제목 텍스트는 지역화 요구 사항을 수용하도록 리소스 파일에서 가져올 수도 있습니다.  
  
16. 솔루션을 저장하고 빌드합니다.  
  
###  <a name="sign-the-assembly-with-an-authenticode-signature"></a><a name="BKMK_SignAssembly"></a>Authenticode 서명을 사용 하 여 어셈블리 서명  
 어셈블리를 운영 체제에서 사용할 수 있으려면 반드시 Authenticode 서명이 필요합니다. 어셈블리 서명에 대한 자세한 내용은 [Authenticode를 사용하여 코드 서명 및 확인](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)을 참조하세요.  
  
###  <a name="install-the-assembly-on-the-reference-computer"></a><a name="BKMK_InstallAssembly"></a>참조 컴퓨터에 어셈블리 설치  
 솔루션을 성공적으로 빌드한 후에는 참조 컴퓨터의 다음 폴더에 DashboardSettingsPage.dll 파일 복사본을 배치합니다.  
  
 **%Programfiles%\Windows Server\bin\oem 폴더가**  
  
## <a name="see-also"></a>관련 항목  
 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)