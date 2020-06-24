---
title: 대시보드, 원격 웹 액세스 및 실행 패드에 브랜딩 추가
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 04/10/2014
ms.prod: windows-server
ms.topic: article
ms.assetid: 166262f8-b2a5-4b1c-a4a7-a141e1c54f10
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: fbe1c042c965a639ac860a7151d16e6548324d9e
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267514"
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>대시보드, 원격 웹 액세스 및 실행 패드에 브랜딩 추가

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a><a name="BKMK_Branding"></a>대시보드, 원격 웹 액세스 및 실행 패드에 브랜딩 추가  
 레지스트리에서 항목을 추가하여 여러 브랜딩을 추가할 수 있습니다. 운영 체제에 대한 레지스트리의 모든 브랜딩 항목은 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OEM 아래에 위치합니다.  
  
 모든 공동 브랜딩은 다음 특정 로고 요구 사항을 충족해야 합니다.  
  
-   Windows Server Essentials 로고의 최소 너비는 **170 픽셀**이어야 하며 올바른 가로 세로 비율을 **96 DPI**로 유지 해야 합니다.  
  
#### <a name="to-add-branding-by-changing-the-registry"></a>레지스트리를 변경하여 브랜딩을 추가하려면  
  
1.  서버에서 마우스를 화면 오른쪽 상단 구석으로 옮긴 후 **검색**을 클릭합니다.  
  
2.  검색 상자에 **regedit**를 입력하고 **Regedit** 애플리케이션을 클릭합니다.  
  
3.  탐색 창에서 **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server**를 차례로 확장합니다. **OEM** 키가 없으면 다음 단계를 수행하여 만듭니다.  
  
    1.  **Windows Server**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **키**를 클릭합니다.  
  
    2.  키 이름에 **OEM**을 입력합니다.  
  
4.  (옵션) 로고에 대한 항목을 만들 경우 여러 키를 만들어 로고의 언어 버전을 구분할 수 있습니다. 예를 들어 로고의 영어 버전과 독일어 버전을 모두 보유한 경우 en-us 키와 de-de 키를 만들 수 있습니다. 로고 파일은 모두 동일한 폴더에 저장되므로 각 언어별로 고유한 이름을 사용하여 로고 이미지 파일의 인스턴스를 제공해야 합니다. 예를 들어 DashboardLogo_en.png 및 DashboardLogo_de.png라는 파일을 만듭니다.  
  
5.  **OEM**을 마우스 오른쪽 단추로 클릭하거나 적절한 언어 키를 마우스 오른쪽 단추로 클릭하고, **새로 만들기**를 클릭한 다음 **문자열 값**을 클릭합니다.  
  

6.  문자열의 이름을 입력한 다음 Enter 키를 누릅니다. 문자열 이름 및 데이터 값은 [레지스트리 문자열 및 값](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings) 표를 참조하세요.  

6.  문자열의 이름을 입력한 다음 Enter 키를 누릅니다. 문자열 이름 및 데이터 값은 [레지스트리 문자열 및 값](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings) 표를 참조하세요.  

  
7.  새 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
8.  문자열 이름과 연결된 테이블에서 값을 입력한 다음 **확인**을 클릭합니다.  
  
9. 로고 이미지 또는 추가된 링크에 대한 항목을 만들 경우 파일을 %programFiles%\Windows Server\Bin\OEM에 복사합니다. OEM 디렉터리가 없으면 새로 만듭니다.  
  
10. 원격 웹 액세스에 영향을 미치는 변경을 수행한 경우에는 소비자가 서버에 대한 소유권을 받은 후 원격 웹 액세스를 켜야 합니다. 고객이 다음을 수행하도록 합니다.  
  
    1.  대시보드에서 **설정**을 클릭한 다음 **원격 액세스** 탭을 클릭합니다.  
  
    2.  원격 액세스가 켜져 있는 경우 **구성**을 클릭한 다음 원격 액세스 설정 마법사의 **사용할 원격 액세스 기능 선택** 페이지에서 원격 웹 액세스 확인란 선택을 취소합니다.  
  
    3.  **구성**을 클릭합니다.  
  
###  <a name="the-following-table-lists-the-location-where-registry-changes-affect-branding-the-string-name-and-the-data-value"></a><a name="BKMK_RegStrings"></a>다음 표에서는 레지스트리 변경 내용이 브랜딩, 문자열 이름 및 데이터 값에 영향을 주는 위치를 보여 줍니다.  
  
### <a name="registry-strings-and-values"></a>레지스트리 문자열 및 값  
  
|브랜딩 위치|Description|문자열 이름|데이터 값|  
|--------------------------|-----------------|-----------------|----------------|  
|대시보드 로고|대시보드에 로고 이미지를 추가합니다. 대시보드 로고 형식은 .png여야 하며, 로고 크기는 350 x 38 픽셀 이하여야 합니다.<br /><br /> **중요:** 로고를 사용 하 여 대시보드를 공동 브랜드 하려면 OPK DVD에 제공 된 아트 워크 타일을 편집 하 고 적절 한 공백 요구 사항을 준수 하는 동안 이미지에 회사 로고를 추가 해야 합니다. 자세한 내용은 제공된 예제 구역을 참조하세요.|DashboardLogo|로고 이미지 파일의 이름입니다.|  
|DashboardClientLogo|대시보드 클라이언트 로그인 화면에 로고 이미지를 추가합니다.|DashboardClientLogo|로고 이미지 파일의 이름입니다.|  
|웹 사이트 배경 그림|원격 웹 액세스 로그온 페이지에 표시되는 배경 이미지를 변경합니다. 일반적인 해상도는 다음과 같이 나타납니다.<br /><br /> -1024x768 픽셀 해상도는 로그온 페이지를 정확 하 게 채웁니다.<br /><br /> -800x600 픽셀 해상도는 페이지 가운데에 맞춰지고 검정색 테두리가 표시 됩니다.<br /><br /> -1280x720 픽셀 해상도는 가운데에 맞춰지고 1024x768를 초과 하는 픽셀은 표시 되지 않습니다.|LogonBackground|배경 이미지 파일의 이름입니다.|  
|웹 사이트 제목|Windows Server Essentials에서 원격 웹 액세스 사이트의 제목을 선택한 제목으로 바꿉니다.|WebsiteName|새 원격 웹 액세스 사이트 제목입니다.|  
|웹 사이트 로고|원격 웹 액세스 사이트의 기본 로고를 변경합니다. 로고의 예상 크기는 32 x 32 픽셀입니다. 로고가 이 크기보다 작거나 큰 경우에는 이러한 치수에 맞게 늘리거나 줄입니다.|WebsiteLogo|로고 이미지 파일의 이름입니다.|  
|첨부한 웹 사이트 로고|파트너 로고는 원격 웹 액세스 사이트에 표시된 Microsoft 로고 바로 아래에 표시됩니다. 로고의 예상 크기는 200 x 50 픽셀입니다. 로고가 이 크기보다 큰 경우에는 원래 가로 세로 비율을 유지하면서 크기에 맞게 줄입니다. 로고가 이 크기보다 작은 경우에는 200 x 50 픽셀 영역 내에서 중심에 위치하며 크기나 가로 세로 비율 모두 변경되지 않습니다.|OEMLogo|로고 이미지 파일의 이름입니다.|  

| 웹 사이트 홈 페이지 및 로그온 페이지의 링크 | 원격 웹 액세스 사이트의 로그온 페이지 및 홈 페이지에 대 한 링크를 추가 합니다. 링크 정보가 포함된 .xml은 %programFiles%\Windows Server\Bin\OEM에 있어야 합니다. 다음 예에서는 .xml 파일의 형식을 보여 줍니다.<br /><br /> <OemLinks\><br /> <LogonLinks\><br /> <링크 이름 \= logonlinkname><br /> <텍스트 \> logonlinkdescription</text\><br /> <Url \> logonlinkurl</url\><br /> <아이콘 \> linkicon</아이콘\><br /> </Link\><br /> </로그온 링크\><br /> <HomepageLinks\><br /> <링크 이름 \= HomepageLinkName><br /> <텍스트 \> HomepageLinkDescription</text\><br /> <Url \> HomepageLinkURL</url\><br /> </Link\><br /> </HomepageLinks\><br /> </OemLinks 링크 \> | 링크 Xml | 요소 및 설명 목록은 [링크 xml 요소](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links) 표를 참조 하세요. |    

| 실행 패드 로고 | 실행 패드에 로고 이미지를 추가 합니다. 실행 패드 로고는 .png 형식 이어야 하며 64 픽셀 보다 커야 합니다. | LaunchpadLogo | 로고 이미지 파일의 이름 |  
  
###  <a name="the-following-table-lists-and-describes-the-linksxml-string-name-elements"></a><a name="BKMK_Links"></a>다음 표에서는 링크 Xml 문자열 이름 요소를 나열 하 고 설명 합니다.  
  
### <a name="linksxml-elements"></a>LinksXML 요소  
  
|LinksXML 요소|Description|  
|----------------------|-----------------|  
|**LogonLinks**|  
|LogonLinkName|로그온 링크 이름입니다.|  
|LogonLinkDescription|로그온 페이지 링크로 표시되는 텍스트입니다.|  
|LogonLinkURL|로그온 페이지 링크로 확인되는 URL입니다.|  
|LinkIcon|로그온 링크에 대한 아이콘 파일 이름입니다. 이 파일은 .xml 파일과 동일한 폴더 위치에 있어야 합니다. 링크 아이콘 이미지는 16 x 16 픽셀이어야 하며, .png 형식이어야 합니다. LinkIcon을 제공하지 않으면 기본 링크 아이콘 이미지가 사용됩니다.|  
|**HomepageLinks**|  
|HomepageLinkName|홈 페이지 링크 이름입니다.|  
|HomepageLinkDescription|홈 페이지 링크로 표시되는 텍스트입니다.|  
|HomepageLinkURL|홈 페이지 링크로 확인되는 URL입니다.|  
|HomepageLinkIcon|홈 페이지 링크에 대한 아이콘 파일 이름입니다. 이 파일은 .xml 파일과 동일한 폴더 위치에 있어야 합니다. HomepageLinkIcon 이미지는 16 x 16 픽셀이어야 하며, .png 형식이어야 합니다. HomepageLinkIcon을 제공하지 않으면 기본 홈 페이지 링크 아이콘 이미지가 사용됩니다.|  
  
## <a name="see-also"></a>참고 항목  

 [이미지 만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포를 위한 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

 [이미지 만들기 및 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포를 위한 이미지 준비](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

