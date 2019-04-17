---
title: "탭 하 고 설정 추가"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aac6b7f3-9020-46c3-a83f-b81542300385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9eaa1aa5a9c5e8d4c2e36f2000e0adecc83245d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-tab-to-settings"></a>탭 하 고 설정 추가

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

작성 및 운영 체제의 관리자는 설정에서 사용 되는 코드 조립 설치 하 여 대시보드에서 설정 탭을 추가할 수 있습니다.  
  
## <a name="add-a-tab-to-settings"></a>탭 하 고 설정 추가  
 다음과 같은 작업을 수행 하 여 설정을 탭을 추가 합니다.  
  
-   [하 여 조립 ISettingsData 인터페이스 구현을 추가](Add-a-Tab-to-Settings.md#BKMK_ISettingsData)합니다.  
  
-   [조립 Authenticode 서명으로 서명](Add-a-Tab-to-Settings.md#BKMK_SignAssembly)합니다.  
  
-   [참조 컴퓨터에 설치 하 여 조립](Add-a-Tab-to-Settings.md#BKMK_InstallAssembly)합니다.  
  
###  <a name="BKMK_ISettingsData"></a>ISettingsData 인터페이스 구현을 조립에 추가  
 ISettingsData 인터페이스 실행 \Program Files\Windows에 있는 AdminCommon.dll 조립의 Microsoft.WindowsServerSolutions.Settings 네임에 포함 되어 있습니다.  
  
##### <a name="to-add-the-isettingsdata-code-to-the-assembly"></a>ISettingsData 코드는 조립을 추가 하려면  
  
1.  프로그램에서 마우스 오른쪽 단추로 클릭 하 여 Visual Studio 2010 관리자 권한으로 엽니다는 **시작** 메뉴를 선택 하 고 **관리자 권한으로 실행**합니다.  
  
2.  클릭 **파일**, 클릭 **새로**을 차례로 클릭 하 고 **프로젝트**합니다.  
  
3.  에 **새 프로젝트** 대화 상자를 클릭 **C#**, 클릭 **클래스 라이브러리**, 입력 **DashboardSettingsPage** 솔루션을 및 클릭 이름에 대 한 **확인**합니다.  
  
    > [!IMPORTANT]
    >  서버에 설치 되어 있는 조립 DashboardSettingsPage.dll 이름 한 다음 dll %ProgramFiles%\Windows Server\Bin\OEM 복사 합니다.  
  
4.  탭에서 사용 하 고 싶은 컨트롤을 만듭니다. 이 이때 제어 하는 설정을 MySettingsControl 이름이입니다.  
  
5.  Class1.cs 파일을 이름을 바꿉니다. 예를 들어, MySettingTab.cs 합니다.  
  
6.  AdminCommon.dll 파일에 대 한 언급을 추가 합니다.  
  
7.  다음 추가 사용 하 여 문의:  
  
    ```c#  
    using Microsoft.WindowsServerSolutions.Settings;  
    ```  
  
8.  네임 및 이때에 맞게 클래스 헤더를 변경 합니다.  
  
    ```  
  
    namespace DashboardSettingsPage  
    {  
        public class MySettingTab : ISettingsData  
        {  
        }  
    }  
  
    ```  
  
9. 탭 하기 위해 만든 컨트롤의 인스턴스를 만들고 있습니다. 예를 들어:  
  
    ```c#  
    private MySettingsControl tab;  
    ```  
  
10. 클래스 생성자를 추가 합니다. 예제 생성자 보여 줍니다.  
  
    ```  
  
    public MySettingTab()  
    {  
       tab = new MySettingsControl();  
    }  
    ```  
  
11. 설정은 변경 내용을 전송 Commit 방법에 추가 합니다. 예제 취소할을 보여 줍니다.  
  
    ```  
  
    void ISettingsData.Commit(bool dismissed)  
    {  
       // Implement the code that is required to submit your setting changes  
    }  
    ```  
  
12. 탭에 대 한 컨트롤을 식별 TabControl 방법에 추가 합니다. 예제는 TabControl 방법을 보여 줍니다.  
  
    ```  
  
    System.Windows.Forms.Control ISettingsData.TabControl  
    {  
       get { return tab; }  
    }  
    ```  
  
13. 탭에 대 한 고유 식별자를 제공 하는 TabId 방법을 추가 합니다. 예제는 TabId 방법을 보여 줍니다.  
  
    ```  
  
    private Guid id = Guid.NewGuid();  
  
    Guid ISettingsData.TabId  
    {  
       get { return id; }  
    }  
    ```  
  
14. 탭의 순서를 반환 TabOrder 방법에 추가 합니다. 예제는 TabOrder 방법을 보여 줍니다.  
  
    ```  
  
    int ISettingsData.TabOrder  
    {  
       get { return 0; }  
    }  
    ```  
  
    > [!NOTE]
    >  탭 순서 숫자 0에서 시작 하 여 정의 됩니다. 처음 표시 되는 Microsoft의 기본 설정을 탭 하 고 탭 정의 있는에 따라 표시 됩니다. 예를 들어 세 개의 설정 탭을 사용 하는 경우 탭 순서 0, 1, 2 표시 되도록 탭 원하는 순서를 기반으로 지정 합니다.  
  
15. 탭의 제목 제공 TabTitle 방법에 추가 합니다. 예제는 TabTitle 방법을 보여 줍니다.  
  
    ```  
  
    string ISettingsData.TabTitle  
    {  
      get { return "My Settings Tab"; }  
    }  
    ```  
  
    > [!NOTE]
    >  제목 텍스트 지역화 요구에 맞게 리소스 파일에서 또한 가져올 수 있습니다.  
  
16. 저장 한 솔루션을 작성 합니다.  
  
###  <a name="BKMK_SignAssembly"></a>조립 Authenticode 서명으로 서명  
 운영 체제에 사용할 수 있도록는 조립 Authenticode 로그인을 해야 합니다. 로그인 하 여 조립에 대 한 자세한 내용은 참조 [Authenticode로 코드를 확인 하 고 서명](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)합니다.  
  
###  <a name="BKMK_InstallAssembly"></a>조립 참조 컴퓨터에 설치  
 성공적으로 솔루션을 작성 한 후 DashboardSettingsPage.dll 파일의 복사본을 참조 컴퓨터에 다음과 같은 폴더에 넣습니다.  
  
 **%Programfiles%\Windows Server\Bin\OEM**  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)