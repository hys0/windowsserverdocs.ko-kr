---
title: "설정 하는 항목, 추가 기능, 빠른 상태를 추가 하 고 도움말 링크"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-entries-to-setup-add-ins-quick-status-and-help-links"></a>설정 하는 항목, 추가 기능, 빠른 상태를 추가 하 고 도움말 링크

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

작업을 추가할 수 있습니다는 **설치**, **추가 기능**, **빠른 상태** 일 목록을 만든 작업 대시보드의 홈페이지의 커뮤니티 링크 섹션으로 링크를 추가할 수 있습니다. 작업과 링크가 OEMHomePageContent.home 파일이 나 OEMHomePageContent.dll %ProgramFiles%\Windows Server\Bin\Addins\Home에에서 라는 리소스 포함 된 파일 이름을 XML 파일 배치 하 여 이러한 목록과 섹션에 추가 됩니다. 지역화 된 작업 및 추가 하는 링크의 텍스트를 포함된 리소스 파일을 사용할 수 있습니다. .Home 파일 작업 및 링크 XML 정의가 포함 되어 있습니다.  
  
## <a name="adding-tasks-to-the-setup-add-ins-quick-status-task-lists-and-adding-links-to-help-task"></a>작업 빠른 상태 작업 목록, 추가 기능 설치를 추가 하 고 도움이 작업에 대 한 링크를 추가  
 작업을 추가할 수는 **설치**, **추가 기능**, **빠른 상태** 작업에 대 한 링크 및 일 목록을 만든는 **하는 데 도움이** 정의 된 작업 및 XML를 사용 하 여 연결 하 여 작업 필요에 따라 포함된 리소스 파일을 만들고 서버에서 파일을 설치 합니다. 없이 리소스 파일 서버에 설치 되는 XML 파일 OEMHomePageContent.home 이름을 해야 합니다. XML 파일 및 리소스 파일을 설치 하는 조립 사용량을 OEMHomePageContent.dll 라는 있어야 하 고 Authenticode 로그인 되어 있어야 합니다.  
  
### <a name="define-the-tasks-and-links"></a>작업 및 링크 정의  
 메모장 등의 텍스트 편집기를 사용 하 여.home 파일을 만들 하거나 포함된 된 리소스 파일 작성 하는 경우 파일을 정의 하 Visual Studio 2010 이상를 사용할 수 있습니다. 다음 절차에 파일을 만들 Visual Studio 2010 이상을 사용 하는 방법을 보여 줍니다.  
  
##### <a name="to-define-the-tasks-and-links"></a>작업 및 링크를 정의 하  
  
1.  시작 메뉴에 프로그램을 마우스 오른쪽 단추로 선택 하 여 Visual Studio 2010 이상의 관리자 권한으로 엽니다 **관리자 권한으로 실행**합니다.  
  
2.  클릭 **파일**, 클릭 **새로**을 차례로 클릭 하 고 **프로젝트**합니다.  
  
3.  에 **템플릿** 창 클릭 **클래스 라이브러리**, 입력 **OEMHomePageContent** 에 **이름** 상자를 클릭 한 다음 한 **확인**합니다.  
  
4.  Class1.cs 파일을 삭제 합니다.  
  
5.  새 프로젝트 마우스 오른쪽 단추로 클릭, **추가**을 차례로 클릭 하 고 **새 항목**합니다.  
  
6.  에 **템플릿** 창 클릭 **XML 파일**, 입력 **OEMHomePageContent.home** 에 **이름** 상자를 클릭 한 다음 한 **추가**합니다.  
  
    > [!NOTE]
    >  리소스 파일 없이 XML 파일 설치 되 면 OEMHomePageContent.home 이름을 해야 합니다. 조립에 포함 되어 있는 경우을 받을 수 있습니다 이름은.home 확장명이으로 합니다.  
  
7.  다음 XML 코드 OEMHomePageContent.home 파일을 추가 합니다.  
  
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
  
     위치:  
  
    |특성|설명|  
    |---------------|-----------------|  
    |이름 (작업)|목록에서 해당 작업 표시 되는 이름입니다. 이 특성 값 리소스 포함 된 파일을 만든 경우 문자열 리소스 수 있습니다.|  
    |설명 (작업)|작업을 설명 합니다. 이 특성 값 리소스 포함 된 파일을 만든 경우 문자열 리소스 수 있습니다.|  
    |Id (작업)|작업의 식별자입니다. 이 식별자 GUID 해야 합니다. 에 대 한 새로운 GUID 만들는 **exe** 작업을에 대해서는 **전 세계** 하위 탭의 작업 창에 대 한 작업을 정의한 때 만든 GUID 사용 작업을 합니다. GUID 만들기에 대 한 자세한 내용은 참조 [Guid 만들기 (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098)합니다.|  
    |이미지|이 필드 무시 됩니다.|  
    |이름 (동작)|작업의 이름을 표시합니다.|  
    |(동작) 유형|작업의 종류에 설명 합니다. 작업 중 하나를 수 있는:- **글로벌** 작업을 **exe**, 또는 url 작업입니다. A **글로벌** 작업이 만든 하위 탭에서 작업 창에 대 한 작업을 정의 하는 경우 동일한 글로벌 작업이 있습니다. 모두 작업 창 하위 탭의 및 하기 시작 또는 일반적인 작업 목록이 홈페이지에 사용할 수 있는 전 세계 작업을 만드는 대 한 자세한 내용은 참조 œCreating 지원 클래스? œHow에: 재 탭을 만드는? 중 고 [Windows Server 솔루션 SDK](https://go.microsoft.com/fwlink/?LinkID=248648)합니다. **exe** 일반적인 작업을 나열 또는 응용 프로그램을 실행할 시작 작업에서 작업을 사용할 수 있습니다.|  
    |exelocation|경로 작업와 연결 된 응용 프로그램입니다. 이 특성만에 사용 되는 **exe** 작업입니다.|  
    |replaceid|이 작업을 대체 하는 작업의 식별자입니다.|  
    |조립|제공 클래스 빠른 상태 쿼리를 구현 하는 조립의 AssemblyName 합니다. 프로그램 폴더 windows server\bin\\에 해야 합니다.|  
    |클래스|이름 클래스의 빠른 상태 쿼리를 구현합니다. 클래스 구현 해야 **ITaskStatusQuery** 인터페이스 합니다.|  
    |제목 (링크)|링크에 표시 되는 텍스트입니다. 이 특성 값 리소스 포함 된 파일을 만든 경우 문자열 리소스 수 있습니다.|  
    |설명 (연결)|링크 대상에 대 한 설명입니다. 이 특성 값 리소스 포함 된 파일을 만든 경우 문자열 리소스 수 있습니다.|  
    |ShellExecPath|경로 응용 프로그램이 나 URL입니다.<br /><br /> **참고:** 환경 변수 ShellExecPath 특성에서 지원 됩니다.|  
  
     예제 응용 프로그램에 대 한 링크를 정의 하는 방법을 보여 줍니다.  
  
    ```  
    <Links>  
       <Link Title="Calc" Description="Launches Calc" ShellExecPath="%windir%\system32\calc.exe" />  
    </Links>  
    ```  
  
     예제 웹 페이지에 대 한 링크를 정의 하는 방법을 보여 줍니다.  
  
    ```  
    <Links>  
       <Link Title="Browser" Description="Open browser" ShellExecPath="http://www.adventureworks.com/" />  
    </Links>  
    ```  
  
8.  작업 또는 링크를 대표 하 속성 값을 변경 합니다.  
  
9. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **OEMHomePageContent.home**을 차례로 클릭 하 고 **속성**합니다.  에 **속성** 창에서 **빌드 작업**선택 **포함 리소스**합니다.  
  
10. OEMHomePageContent.home 파일을 저장 합니다.  
  
 문서와의 샘플을 참조 하십시오, 빠른 상태 쿼리를 구현 하는 방법에 대 한는 [Windows Server 솔루션 SDK](https://go.microsoft.com/fwlink/?LinkID=248648)합니다.  
  
#### <a name="change-the-status-of-a-setupadd-ins-task"></a>추가 기능 설치/작업의 상태를 변경 합니다.  
 설치 및 추가 기능에 나와 있는 작업의 상태에서 전환할 수 완료 (Add-ins에 대 한 구성) (Add-ins에 대해 구성 되지 않았습니다)를 완료 되지 합니다.  
  
 새 작업과 관련 된 응용 프로그램을 정의 하는 경우 Microsoft.WindowsServerSolutions.Administration.ObjectModel.TaskStatusHelper 네임 스페이스 (, 포함 되어 있지만 Windows Server 솔루션 SDK에 하지 설명)의 SetTaskStatus 방법을 사용할 수 있습니다 작업의 상태를 변경할 수 있습니다. 예를 들어,에서 변경할 수 있습니다 확인 표시가 그레이 녹색 TaskStatus.Complete 열거형 값으로 SetTaskStatus 메서드를 호출 하 여 (SetTaskStatus (id TaskStatus.Complete), 여기서 **id** 작업의 식별자). 사용할 수 있는 열거형 값은 TaskStatus.Complete, TaskStatus.Incomplete, 또는 TaskStatus.Hidden 합니다.  
  
##### <a name="replace-tasks"></a>작업 바꾸기  
 작업에 대 한 GUID 작업 정의 replaceid 특성을 추가 하 여 시작 작업 또는 일반적인 작업 목록에 미리 정의 된 작업 바꿀 수 있습니다. 다음 표에서 작업과 대시보드에 대체할 수 있는 해당 식별자 다음과 같습니다.  
  
|작업 이름|식별자|  
|---------------|----------------|  
|기타 Microsoft 제품에 대 한 업데이트 가져오기|8412D35A-13EE-4112-AE0B-F7DBC83EA83D|  
|서버 백업 설정|F68B3F3F-19DE-499D-9ACB-4BB41B8FF420|  
|어디서 나 액세스를 설정|8991302D-676A-4A7C-B244-D1E08AE0EFEA|  
|메일 알림 설정|DE6F2B36-F19C-4FAF-998B-9772300E3530|  
|사용자 계정 추가|6D5B5D5F-2EC7-4B1F-9580-4DB084B278B1|  
|서버 폴더 추가|03F1F438-D94E-439B-A9F7-0C817C37D625|  
|어디서 나 액세스-빠른 상태|6093B462-1F04-4212-8804-9BC823070FAD|  
|서버 백업-빠른 상태|156947D8-21DC-45FE-A9A8-2F80AE304191|  
|서버 폴더-빠른 상태|C657E8AB-AC1F-4AA1-8E80-5AF6BB27C314|  
|현재 사용자 계정이-빠른 상태|68BCB125-CE8F-467F-B65B-56AD45A614B5|  
|빠른 상태 경고 알림-메일|75AB06E7-A679-4D62-A5EC-65362FE4F9DB|  
|컴퓨터에서 빠른 상태|7966A974-D52D-4F5D-B37F-05C1B73CEEF3|  
  
##### <a name="optional-create-the-resource-file"></a>(선택 사항) 만들기 리소스 파일  
 .Home 파일이 들어 있는 조립 만들어야 하기 시작, 일반적인 작업을 작업과 커뮤니티 링크를 추가 하는 작업에 있는 텍스트 지역화 하려는 경우와. 텍스트 문자열을 정의 하 home.resx 파일.  
  
###### <a name="to-create-the-resource-file"></a>리소스 파일을 만들려면  
  
1.  작업에 대해 생성 하는 프로젝트를 마우스 오른쪽 단추로 클릭, **추가**을 차례로 클릭 하 고 **새 항목**합니다.  
  
2.  에 **템플릿** 창 클릭 **리소스 파일**, 입력 **OEMHomePageContent.home.resx** 에 **이름** 상자를 클릭 한 다음 한 **추가**합니다.  
  
    > [!NOTE]
    >  리소스 파일 이름을 지정할 수 있습니다 모든을 한. home.resx 확장 합니다.  
  
3.  각 작업이 나 추가 하는 링크에 대 한 문자열 및 값 OEMHomePageContent.home 파일에 정의 된 작업 및 링크 요소와 일치 하는 OEMHomePageContent.home.resx 파일에 추가 해야 합니다. 예제는 리소스 파일에 대 한 구성 되어 Tasks.xml 파일의 예 보여 줍니다.  
  
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
    >  지역화에 사용 되는 특성 식별자 공간을 사용할 수 없습니다.  
  
4.  MyTask, MyTaskDescription, MyActionName, 및 IconForAction 리소스 이름 적절 한 값으로.resx 파일에 추가 합니다.  
  
5.  OEMHomePageContent.home.resx 파일을 저장 한 다음 솔루션을 작성 합니다.  
  
#####  <a name="BKMK_SignAssembly"></a>조립 Authenticode 서명으로 서명  
 운영 체제에 사용할 수 있도록는 조립 Authenticode 로그인을 해야 합니다. 로그인 하 여 조립에 대 한 자세한 내용은 참조 [Authenticode로 코드를 확인 하 고 서명](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)합니다.  
  
##### <a name="install-the-task-files"></a>작업 파일을 설치  
 .home 만든 다음 및. home.resx 파일을 설치 해야 하는 서버에 있습니다.  
  
###### <a name="to-install-the-task-files"></a>작업 파일을 설치 하려면  
  
1.  빌드 솔루션 오류가 있는지 확인 합니다.  
  
2.  포함된 된 리소스 파일을 만들지 않은 경우 OEMHomePageContent.home 파일을 복사 **%ProgramFiles%\Windows Server\Bin\Addins\Home** 서버에 있습니다. 포함된 된 리소스 파일을 만든 경우 OEMHomePageContent.dll 파일을 복사 **%ProgramFiles%\Windows Server\Bin\Addins\Home** 서버에 있습니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)