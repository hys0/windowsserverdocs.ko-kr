---
title: "대시보드 및 실행 창 색 구성표 변경"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2913e51-7979-4d48-a431-d2ec5f1042be
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f7079c9e59c44907fa203db48ce366c2b5a1102b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="change-the-color-scheme-of-the-dashboard-and-launchpad"></a>대시보드 및 실행 창 색 구성표 변경

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

대시보드의 색 구성표 변경 하 고 XML에 사용할 색을 정의 하 여 실행 패드 포맷.xml 파일 폴더의 서버에 및 레지스트리 항목이.xml 파일 이름을 지정 하 여 설치 파일을 합니다.  
  
## <a name="create-the-xml-file"></a>Xml 파일 만들기  
 다음 예제.xml 파일의 가능한 내용을 보여 줍니다.  
  
```xml  
<DashboardTheme xmlns="https://www.microsoft.com/HSBS/Dashboard/Branding/2010">  
  
  <!-- Hex color values overwriting default SKU theme colors -->  
  
    <SplashScreenBackgroundColor HexValue="FFFFFFFF"/>  
    <SplashScreenBorderColor HexValue="FF000000"/>  
    <MainHeaderBackgroundColor HexValue="FF414141"/>  
    <MainTabBackgroundColor HexValue="FFFFFFFF"/>  
    <MainTabFontColor HexValue="FF999999"/>  
    <MainTabHoverFontColor HexValue="FF0072BC"/>  
    <MainTabSelectedFontColor HexValue="FF0072BC"/>  
    <MainButtonPressedBackgroundColor HexValue="FF0072BC"/>  
    <MainButtonFontColor HexValue="FFFFFFFF"/>  
    <MainButtonBorderColor HexValue="FF6E6E6E"/>  
    <ScrollButtonBackgroundColor HexValue="FFF0F0F0"/>  
    <ScrollButtonArrowColor HexValue="FF999999"/>  
    <ScrollButtonHoverBackgroundColor HexValue="FF999999"/>  
    <ScrollButtonHoverArrowColor HexValue="FF6E6E6E"/>  
    <ScrollButtonSelectedBackgroundColor HexValue="FF6E6E6E"/>  
    <ScrollButtonSelectedArrowColor HexValue="FFFFFFFF"/>  
    <ScrollButtonDisabledBackgroundColor HexValue="FFF8F8F8"/>  
    <ScrollButtonDisabledArrowColor HexValue="FFCCCCCC"/>  
    <AlertTextBlockBackground HexValue="FFFFFFFF"/>  
    <AlertTextBlockFont HexValue="FF000000"/>  
    <FontColor HexValue="FF000000"/>  
    <SubTabBarBackgroundColor HexValue="FFFFFFFF"/>  
    <SubTabBackgroundColor HexValue="FFFFFFFF"/>  
    <SubTabSelectedBackgroundColor HexValue="FF414141"/>  
    <SubTabBorderColor HexValue="FF787878"/>  
    <SubTabFontColor HexValue="FF787878"/>  
    <SubTabHoverFontColor HexValue="FF0072BC"/>  
    <SubTabPressedFontColor HexValue="FFFFFFFF"/>  
    <ListViewColor HexValue="FFFFFFFF"/>  
    <PageBorderColor HexValue="FF999999"/>      
    <LaunchpadButtonHoverBorderColor HexValue="FF6BA0B4"/>  
    <LaunchpadButtonHoverBackgroundColor HexValue="FF41788F"/>  
    <ClientArrowColor HexValue="FFFFFFFF"/>  
    <ClientGlyphColor HexValue="FFFFFFFF"/>  
    <SplitterColor HexValue="FF83C6E2"/>  
    <HomePageBackColor     HexValue="FFFFFFFF"/>  
    <CategoryNotExpandedBackColor HexValue="FFFFB343"/>  
    <CategoryExpandedBackColor HexValue="FFF26522"/>  
    <CategoryNotExpandedForeColor HexValue="FF2A2A2A"/>  
    <CategoryExpandedForeColor HexValue="FFFFFFFF"/>  
    <HomePageTaskListForeColor    HexValue="FF2A2A2A"/>  
    <HomePageTaskListBackColor HexValue="FFEAEAEA"/>  
    <HomePageTaskListHoverForeColor      HexValue="FF2A2A2A"/>  
    <HomePageTaskListItemBorderColor     HexValue="FF999999"/>  
    <HomePageTaskListSelectedForeColor   HexValue="FFFFFFFF"/>  
    <HomePageTaskListSelectedBackColor   HexValue="FFF26522"/>  
    <HomePageTaskDetailStatusForeColor   HexValue="FFF26522"/>  
    <HomePageTaskDetailDescriptionForeColor     HexValue="FF2A2A2A"/>  
    <HomePageLinkForeColor HexValue="FF0072BC"/>  
    <HomePageLinkSelectedForeColor HexValue="FF0054A6"/>  
    <HomePageLinkHoverForeColor   HexValue="FF0072BC"/>  
    <PropertyFormForeColor HexValue="FF2A2A2A"/>  
    <PropertyFormTabHoverColor HexValue="FF0072BC"/>  
    <PropertyFormTabSelectedColor HexValue="FFFFFFFF"/>  
    <PropertyFormTabSelectedBackColor HexValue="FF414141"/>  
    <TaskPanelBackColor HexValue="FFFFFFFF"/>  
    <TaskPanelItemForeColor HexValue="FF2A2A2A"/>  
    <TaskPanelGroupTitleForeColor HexValue="FF2A2A2A"/>  
    <TaskPanelGroupTitleBackColor HexValue="FFCCCCCC"/>  
    <DashboardClientBackColor HexValue="FF004050"/>  
    <DashboardClientTitleColor HexValue="FFFFFFFF"/>  
    <DashboardClientOptionsForeColor HexValue="FFFFFFFF"/>  
    <DashboardClientOptionsItemForeColor HexValue="FF2A2A2A"/>  
    <DashboardClientHelpForeColor HexValue="FF0054A6"/>  
    <ClientSignInForeColor HexValue="FFFFFFFF"/>  
    <ClientSignInWaterMarkForeColor HexValue="FF999999"/>  
    <ClientSignInUserNameForeColor HexValue="FF2A2A2A"/>  
    <ClientSignInPassWordSpecificBackColor HexValue="FFCCCCCC"/>  
    <ClientSignInButtonBackColor HexValue="FF004050"/>  
    <ClientSignInPassWordForeColor HexValue="FF2A2A2A"/>  
    <LaunchPadBackColor HexValue="FF004050"/>  
    <LaunchPadPageTitleColor HexValue="FFFFFFFF"/>  
    <LaunchPadItemForeColor HexValue="FFFFFFFF"/>  
  <LaunchPadItemHoverColor HexValue="33FFFFFF"/>  
  <LaunchPadItemIconBackgroundColor HexValue="F2004050"/>  
</DashboardTheme >  
  
```  
  
> [!IMPORTANT]
>  위 예제에서 나와 있는 순서 대로 xml 요소 지정 되어야 합니다.  
  
> [!NOTE]
>  모든 값 HexValue 특성는 색에 대 한 값 16 진 예입니다. 사용 하려는 모든 16 진 색 값을 입력할 수 있습니다.  
  
 메모장 또는 Visual Studio 2010을 사용 하 여 사용자 지정 하려면 분야에 대 한 태그를 포함 하 여.xml 파일을 만듭니다. 파일 모든 이름을 지정할 수 있습니다 하지만.xml 확장명이 여야 합니다. 대시보드 및 실행 패드 사용자 지정할 수 있는 영역에 대 한 참고 [변경할 수 있는 영역을 대시보드 및 실행 패드](Change-the-Color-Scheme-of-the-Dashboard-and-Launchpad.md#BKMK_Dashboard)합니다.  
  
#### <a name="to-install-the-xml-file"></a>.Xml 파일을 설치 하려면  
  
1.  서버에서 화면 오른쪽 위 모서리에 마우스를 이동 하 고 클릭 **검색**합니다.  
  
2.  검색 상자에 입력 **regedit**을 차례로 클릭 하 고 있는 **Regedit** 응용 프로그램입니다.  
  
3.  왼쪽된 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**, 확장 **Windows Server**합니다. 하는 경우는 **OEM** 키가 없는, 새로 만드시겠습니까 다음 단계를 완료 해야 합니다.  
  
    1.  마우스 오른쪽 단추로 클릭 **Windows Server**를 가리킨 **새로**을 차례로 클릭 하 고 **키**합니다.  
  
    2.  입력 **OEM** 키의 이름입니다.  
  
4.  마우스 오른쪽 단추로 클릭 **OEM**, 가리킨 **새로**을 차례로 클릭 하 고 **문자열 값**합니다.  
  
5.  Enter **CustomColorScheme** 문자열을 차례로 누르기의 이름으로 **Enter**합니다.  
  
6.  마우스 오른쪽 단추로 클릭 **CustomColorScheme** 오른쪽 단추로 클릭 하거나 길게 누른 **수정**합니다.  
  
7.  해당 파일의 이름을 입력 한 다음 누르고 **확인**합니다.  
  
8.  %ProgramFiles%\Windows Server\Bin\OEM에 파일을 복사 합니다. OEM 디렉터리가 만듭니다.  
  
##  <a name="BKMK_Dashboard"></a>변경할 수 있는 영역을 대시보드 및 실행 패드  
 이 섹션 대시보드 및 실행 패드 영역 사용자 지정할 수 있는 몇 가지 포함 되어 있습니다.  
  
### <a name="examples"></a>예제  
  
####  <a name="BKMK_Figure1"></a>대시보드 그림 1: 로그인 페이지  
 ![Windows Server Essentials 대시보드](media/SBS8_ADK_Dashboard_Signin_RC.png "SBS8_ADK_Dashboard_Signin_RC")  
  
####  <a name="BKMK_Figure2"></a>그림 2: 실행 패드  
 ![Windows SBS 실행 패드 로그인 & #45,에](media/SBS8_ADK_LaunchpadSignin2.png "SBS8_ADK_LaunchpadSignin2")  
  
####  <a name="BKMK_Figure3"></a>실행 패드 로그인 페이지 그림 3:  
 ![Windows Server Essentials 실행 패드](media/SBS8_ADK_Launchpad_Signin_RC.png "SBS8_ADK_Launchpad_Signin_RC")  
  
####  <a name="BKMK_Figure4"></a>대시보드 그림 4: 텍스트  
 ![Windows Server Essentials 탐색 창](media/SBS8_ADK_Navigation_RC.png "SBS8_ADK_Navigation_RC")  
  
####  <a name="BKMK_Figure5"></a>탭 테두리 그림 5:  
 ![Windows SBS 대시보드 하위 탭 테두리](media/SBS8_ADK_DashboardSubtabborder.png "SBS8_ADK_DashboardSubtabborder")  
  
####  <a name="BKMK_Figure6"></a>작업 창 그림 6:  
 ![Windows SBS 대시보드 작업 창을](media/SBS8_ADK_DashboardTaskPane.png "SBS8_ADK_DashboardTaskPane")  
  
####  <a name="BKMK_Figure9"></a>7a 그림: 제품 시작 화면  
 ![Windows Server Essentials 시작 화면](media/SBS8_ADK_productspalshscreen_RC.png "SBS8_ADK_productspalshscreen_RC")  
  
#### <a name="figure-7b-home-page"></a>그림 7b: 홈페이지  
 ![Windows Server Essentials 홈페이지](media/SBS8_ADK_Dashboard_HomePage_RC.png "SBS8_ADK_Dashboard_HomePage_RC")  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)