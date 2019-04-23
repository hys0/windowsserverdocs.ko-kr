---
title: 설정, 추가 기능, 빠른 상태 및 도움말 링크에 항목 추가
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0a8f10d-fd85-4c8d-b9bb-176cb1db1f46
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6d3303f2c6d84932ad9d5dee8a547cd478447732
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864394"
---
# <a name="add-entries-to-setup-add-ins-quick-status-and-help-links"></a>설정, 추가 기능, 빠른 상태 및 도움말 링크에 항목 추가

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

**설정**, **추가 기능**, **빠른 상태** 작업 목록에 작업을 추가할 수 있으며 대시보드 홈 페이지의 커뮤니티 링크 섹션에 링크를 추가할 수 있습니다. 이름이 OEMHomePageContent.home 파일인 XML 파일 또는 이름이 OEMHomePageContent.dll인 내장 리소스 파일을 %ProgramFiles%\Windows Server\Bin\Addins\Home에 배치하여 작업과 링크가 이 목록과 섹션에 추가됩니다. 포함된 리소스 파일을 사용하여 추가한 작업과 링크의 텍스트를 지역화할 수 있습니다. .home 파일은 작업 및 링크의 XML 정의를 포함합니다.  
  
## <a name="adding-tasks-to-the-setup-add-ins-quick-status-task-lists-and-adding-links-to-help-task"></a>설정, 추가 기능, 빠른 상태 작업 목록에 작업 추가 및 도움말 작업에 링크 추가  
 XML을 사용하여 작업 및 링크를 정의하고, 선택적으로 포함 리소스 파일을 만들며, 서버에서 파일을 설치하여 **설정**, **추가 기능**, **빠른 상태** 작업 목록에 작업을 추가하고 **도움말** 목록에 링크를 추가할 수 있습니다. XML 파일을 리소스 파일 없이 서버에 설치하는 경우 파일 이름이 OEMHomePageContent.home이어야 합니다. XML 파일과 리소스 파일 설치하는 데 어셈블리를 사용하는 경우 이름이 OEMHomePageContent.dll이어야 하고 Authenticode 서명이 되어 있어야 합니다.  
  
### <a name="define-the-tasks-and-links"></a>작업 및 링크 정의  
 메모장과 같은 텍스트 편집기를 사용하여 .home 파일을 만들수 있습니다. 그렇지 않고 내장 리소스 파일을 만들 경우 Visual Studio 2010 이상을 사용하여 파일을 정의할 수 있습니다. 다음 절차는 Visio Studio 2010 이상을 사용하여 파일을 만드는 방법을 보여 줍니다.  
  
##### <a name="to-define-the-tasks-and-links"></a>작업 및 링크를 정의하려면  
  
1.  시작 메뉴에서 프로그램을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택하여 관리자로 Visual Studio 2010 이상을 엽니다.  
  
2.  **파일**, **새로 만들기**를 차례로 클릭한 다음 **프로젝트**를 클릭합니다.  
  
3.  **템플릿** 창에서 **클래스 라이브러리**를 클릭하고 **이름** 상자에 **OEMHomePageContent** 를 입력한 다음 **확인**을 클릭합니다.  
  
4.  Class1.cs 파일을 삭제합니다.  
  
5.  새 프로젝트를 마우스 오른쪽 단추로 클릭하고, **추가**를 클릭한 다음 **새 항목**을 클릭합니다.  
  
6.  **템플릿** 창에서 **XML 파일**을 클릭하고 **이름** 상자에 **OEMHomePageContent.home** 을 입력한 다음 **추가**를 클릭합니다.  
  
    > [!NOTE]
    >  XML 파일을 리소스 파일 없이 설치하는 경우 파일 이름이 OEMHomePageContent.home이어야 합니다. 어셈블리에 포함된 경우 확장자가 .home이면 어떤 이름을 설정해도 됩니다.  
  
7.  OEMHomePageContent.home 파일에 다음 XML 코드를 추가합니다.  
  
    ```  
  
    <Tasks version=?2.0? xmlns=?https://schemas.microsoft.com/WindowsServerSolutions/2010/01/Dashboard>  
       <SetupMyServerTasks>  
          <Task name="MyTask"  
             description="MyTaskDescription"  
             id="GUID">  
                  <Action   
                  name=?MyAction1Name?   
                  image=?IconForAction1?  
                  type=?TaskType?  
                  exelocation=?ActionExeLocation? />  
                  <Action   
                  name=?MyAction2Name?   
                  image=?IconForAction2?  
                  type=?TaskType?  
                  exelocation=?ActionExeLocation? />  
                   ¦  
           </Task>  
                   ¦  
        </SetupMyServerTasks>  
    <MailServiceTasks>  
         <!-- Same schema as in œSetupMyServerTasks? but the tasks are shown in œConnect to Email Service? category. -->  
    </MailServiceTasks>  
    <LineOfBusinessTasks>  
         <!-- Same schema as in œSetupMyServerTasks? but the tasks are shown in œAdd-ins? category. -->  
  
    <GetQuickStatusTasks>  
          <Task name="MyQuickStatusTask1"  
             description="MyQuickStatusTask1Desc   "  
             id="GUID"  
             assembly="AssemblyName of quick status query implementation"  
             class="ClassName of quick status query implementation"           
             replaceid="GUID"/>  
               <!--  Same schema as Actions in œSetupMyServerTasks? -->   
             </Task>  
    </GetQuickStatusTasks>  
       <Links>  
          <Link  
             ID=?GUID?  
             Title="Displayed text of the link"  
             Description="A very short description"  
             ShellExecPath="Path to the application or URL"/>  
       </Links>  
    </Tasks>  
    ```  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
    |attribute|설명|  
    |---------------|-----------------|  
    |Name (Task)|목록에서 작업에 대해 표시되는 이름입니다. 포함 리소스 파일을 만들 경우 이 특성 값이 문자열 리소스가 됩니다.|  
    |description (Task)|작업에 대한 설명입니다. 포함 리소스 파일을 만들 경우 이 특성 값이 문자열 리소스가 됩니다.|  
    |id (Task)|작업의 식별자입니다. 이 식별자는 GUID여야 합니다. **exe** 작업에 대해 새 GUID를 만들지만 **글로벌** 작업의 경우 하위 탭의 작업 창에서 작업을 정의할 때 만든 GUID를 사용합니다. GUID 만들기에 대 한 자세한 내용은 참조 하세요. [Guid 만들기 (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098)합니다.|  
    |이미지|이 필드를 무시합니다.|  
    |Name (Action)|작업 이름을 표시합니다.|  
    |Type (Action)|작업 유형을 설명합니다. 작업은 **전역** 작업, **exe** 또는 URL 작업 중 하나가 될 수 있습니다. **전역** 작업은 하위 탭의 작업 창에서 작업을 정의할 때 만든 것과 동일한 전역 작업입니다. 하위 탭의 두 작업 창과 홈페이지의 시작 작업 또는 일반 작업 목록에 사용할 수 있는 전역 작업을 만드는 방법에 대 한 자세한 내용은 지원 클래스를 참조 하십시오 œCreating? œHow에: 하위 탭 만들기 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)합니다. **exe** 작업은 시작 작업 또는 일반 작업 목록에서 응용 프로그램을 실행하는 데 사용할 수 있습니다.|  
    |exelocation|작업과 관련된 응용 프로그램 경로입니다. 이 특성은 **exe** 작업에 대해서만 사용됩니다.|  
    |replaceid|이 작업으로 바꿀 작업의 식별자입니다.|  
    |어셈블리(assembly)|빠른 상태 쿼리를 구현할 클래스를 제공하는 어셈블리의 어셈블리 이름입니다. 어셈블리 Program files\ windows server\bin에 위치 해야\\합니다.|  
    |class|클래스의 이름은 빠른 상태 쿼리를 구현합니다. 클래스는 **ITaskStatusQuery** 인터페이스를 구현해야 합니다.|  
    |Title (link)|링크에 대해 표시되는 텍스트입니다. 포함 리소스 파일을 만들 경우 이 특성 값이 문자열 리소스가 됩니다.|  
    |Description (link)|링크 대상에 대한 설명입니다. 포함 리소스 파일을 만들 경우 이 특성 값이 문자열 리소스가 됩니다.|  
    |ShellExecPath|응용 프로그램 또는 URL 경로입니다.<br /><br /> **참고:** 환경 변수는 ShellExecPath 특성에서 지원됩니다.|  
  
     다음 코드 예제에서는 응용 프로그램에 대한 링크를 정의하는 방법을 보여 줍니다.  
  
    ```  
    <Links>  
       <Link Title="Calc" Description="Launches Calc" ShellExecPath="%windir%\system32\calc.exe" />  
    </Links>  
    ```  
  
     다음 코드 예제에서는 웹 페이지에 대한 링크를 정의하는 방법을 보여 줍니다.  
  
    ```  
    <Links>  
       <Link Title="Browser" Description="Open browser" ShellExecPath="http://www.adventureworks.com/" />  
    </Links>  
    ```  
  
8.  작업 또는 링크를 나타내는 특성 값을 변경합니다.  
  
9. **솔루션 탐색기**에서 **OEMHomePageContent.home**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  **속성** 창의 **빌드 작업**에서 **포함 리소스**를 선택합니다.  
  
10. OEMHomePageContent.home 파일을 저장합니다.  
  
 빠른 상태 쿼리 구현 방법은 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)의 문서와 샘플을 참조하세요.  
  
#### <a name="change-the-status-of-a-setupadd-ins-task"></a>설정/추가 기능 작업 상태 변경  
 설정 및 추가 기능에 열거된 작업은 완료된 상태(추가 기능으로 구성됨) 및 완료되지 않은 상태(추가 기능으로 구성되지 않음)로 토글할 수 있습니다.  
  
 새 작업과 연결된 응용 프로그램을 정의할 때는 Microsoft.WindowsServerSolutions.Administration.ObjectModel.TaskStatusHelper 네임스페이스의 SetTaskStatus 메서드를 사용하여 작업 상태를 변경할 수 있습니다. 이 메서드는 Windows Server Solutions에 포함되어 있기는 하지만 SDK에 설명되어 있지는 않습니다. 예를 들어 TaskStatus.Complete 열거 값(SetTaskStatus(id, TaskStatus.Complete))을 사용해 SetTaskStatus 메서드를 호출하여 확인 표시를 회색에서 녹색으로 변경할 수 있습니다. 여기서 **id**는 작업의 식별자입니다. 사용할 수 있는 열거 값은 TaskStatus.Complete, TaskStatus.Incomplete 또는 TaskStatus.Hidden입니다.  
  
##### <a name="replace-tasks"></a>작업 대체  
 작업 정의의 replaceid 특성에 작업에 대한 GUID를 추가하여 시작 작업 또는 일반 작업 목록에 미리 정의된 작업을 바꿀 수 있습니다. 다음 표에는 대시보드에서 바꿀 수 있는 작업과 해당 식별자가 나열되어 있습니다.  
  
|작업 이름|Identifier|  
|---------------|----------------|  
|다른 Microsoft 제품에 대한 업데이트 가져오기|8412D35A-13EE-4112-AE0B-F7DBC83EA83D|  
|서버 백업 설정|F68B3F3F-19DE-499D-9ACB-4BB41B8FF420|  
|원격 액세스 설정|8991302D-676A-4A7C-B244-D1E08AE0EFEA|  
|전자 메일 경고 알림 설정|DE6F2B36-F19C-4FAF-998B-9772300E3530|  
|사용자 계정 추가|6D5B5D5F-2EC7-4B1F-9580-4DB084B278B1|  
|서버 폴더 추가|03F1F438-D94E-439B-A9F7-0C817C37D625|  
|원격 액세스 - 빠른 상태|6093B462-1F04-4212-8804-9BC823070FAD|  
|서버 백업 - 빠른 상태|156947D8-21DC-45FE-A9A8-2F80AE304191|  
|서버 폴더 - 빠른 상태|C657E8AB-AC1F-4AA1-8E80-5AF6BB27C314|  
|활성 사용자 계정 - 빠른 상태|68BCB125-CE8F-467F-B65B-56AD45A614B5|  
|전자 메일 경고 알림 - 빠른 상태|75AB06E7-A679-4D62-A5EC-65362FE4F9DB|  
|컴퓨터 - 빠른 상태|7966A974-D52D-4F5D-B37F-05C1B73CEEF3|  
  
##### <a name="optional-create-the-resource-file"></a>(옵션) 리소스 파일 만들기  
 시작 작업, 일반 작업 및 커뮤니티 링크를 추가 하는 작업에서 텍스트를 지역화 하려면 만들어야.home 파일을 포함 하는 어셈블리 및. 텍스트 문자열을 정의 하는.home.resx 파일.  
  
###### <a name="to-create-the-resource-file"></a>리소스 파일을 만들려면  
  
1.  작업에 대해 만든 프로젝트를 마우스 오른쪽 단추로 클릭하고, **추가**를 클릭한 다음 **새 항목**을 클릭합니다.  
  
2.  **템플릿** 창에서 **리소스 파일**을 클릭하고 **이름** 상자에 **OEMHomePageContent.home.resx**를 입력한 다음 **추가**를 클릭합니다.  
  
    > [!NOTE]
    >  리소스 파일 확장명이 .home.resx인 경우 어떤 이름도 지정할 수 있습니다.  
  
3.  추가한 작업 또는 링크 각각에 대해 OEMHomePageContent.home 파일에 정의된 작업 및 링크 요소와 일치하는 문자열과 값을 OEMHomePageContent.home.resx 파일에 추가해야 합니다. 다음 코드 예제에서는 리소스 파일에 대해 구조화된 Tasks.xml 파일의 예를 보여 줍니다.  
  
    ```  
  
    <Tasks version=?2.0? xmlns=?https://schemas.microsoft.com/WindowsServerSolutions/2010/01/Dashboard>  
       <SetupMyServerTasks>  
          <Task name="MyTask"  
             description="MyDescription"  
             id="GUID">  
             <Action  
             name="MyActionname"  
             image="IconForAction"  
             type="TaskType"  
             exelocation="ActionExeLocation" />  
          </Task>  
       </SetupMyServerTasks>  
    </Tasks>  
  
    ```  
  
    > [!NOTE]
    >  지역화에 사용되는 특성의 식별자에는 공백이 포함될 수 없습니다.  
  
4.  적절한 값이 포함된 .resx 파일에 MyTask, MyTaskDescription, MyActionName 및 IconForAction 리소스 이름을 추가합니다.  
  
5.  OEMHomePageContent.home.resx 파일을 저장하고 솔루션을 빌드합니다.  
  
#####  <a name="BKMK_SignAssembly"></a> Authenticode 서명으로 어셈블리 서명  
 어셈블리를 운영 체제에서 사용할 수 있으려면 반드시 Authenticode 서명이 필요합니다. 어셈블리 서명에 대한 자세한 내용은 [Authenticode를 사용하여 코드 서명 및 확인](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)을 참조하세요.  
  
##### <a name="install-the-task-files"></a>작업 파일 설치  
 .home 및 .home.resx 파일을 만들고 나면 서버에서 파일을 설치해야 합니다.  
  
###### <a name="to-install-the-task-files"></a>작업 파일을 설치하려면  
  
1.  솔루션이 오류 없이 빌드되는지 확인합니다.  
  
2.  포함 리소스 파일을 만들지 않은 경우 OEMHomePageContent.home 파일을 서버의 **%ProgramFiles%\Windows Server\Bin\Addins\Home** 에 복사합니다. 포함 리소스 파일을 만든 경우 OEMHomePageContent.dll 파일을 서버의 **%ProgramFiles%\Windows Server\Bin\Addins\Home**에 복사합니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)