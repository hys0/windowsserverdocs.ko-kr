---
title: "브랜드 대시보드, 원격 Web Access 및 실행 창에 추가"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 04/10/2014
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 166262f8-b2a5-4b1c-a4a7-a141e1c54f10
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 02088b169e44cdcf87385425e1949232ffa408a6
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>브랜드 대시보드, 원격 Web Access 및 실행 창에 추가

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_Branding"></a>브랜드 대시보드, 원격 Web Access 및 실행 창에 추가  
 많은 브랜딩 추가의 항목을 추가 하 여 만들 수 있습니다. 아래를 Server\OEM의 운영 체제에 대 한 모든 브랜딩 항목이 있습니다.  
  
 모든 공동 브랜드 다음 로고 요구 사항을 충족 해야 합니다.  
  
-   Windows Server Essentials 로고 최소 너비가 있어야 **170 픽셀**, 올바른 가로 세로 비율에 맞게 **96DPI**합니다.  
  
#### <a name="to-add-branding-by-changing-the-registry"></a>브랜드 레지스트리를 변경 하 여 추가 하려면  
  
1.  서버에서 화면 오른쪽 위 모서리에 마우스를 이동 하 고 클릭 **검색**합니다.  
  
2.  검색 상자에 입력 **regedit**을 차례로 클릭 하 고 있는 **Regedit** 응용 프로그램입니다.  
  
3.  탐색 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**, 확장 **Windows Server**합니다. 하는 경우는 **OEM** 키가 없을 만드는 데 다음 단계를 완료 합니다.  
  
    1.  마우스 오른쪽 단추로 클릭 **Windows Server**, 클릭 **새로**을 차례로 클릭 하 고 **키**합니다.  
  
    2.  입력 **OEM** 키의 이름입니다.  
  
4.  (선택 사항) 로고에 대 한 항목을 만드는 로고 언어 버전을 구분 하기 위해 다른 키를 만들 수 있습니다. 예를 들어, 로고의 영어 및 독일어 버전을 사용 하는 경우는 en 만들 수 기능 키를 de de 키. 폴더와 동일한 폴더에 저장 되므로 로고 파일을 모두 인스턴스 로고 이미지 파일의 각 언어에 대 한 고유한 이름의 제공 해야 합니다. 예를 들어 DashboardLogo_en.png 및 DashboardLogo_de.png 파일을 만듭니다.  
  
5.  하거나 마우스 오른쪽 단추로 클릭 **OEM** 적절 한 언어 키를 마우스 오른쪽 단추로 클릭를 클릭 하거나 **새로**을 차례로 클릭 하 고 **문자열 값**합니다.  
  

6.  문자열의 이름을 입력 한 다음 ENTER 키를 누릅니다. 참조는 [문자열을 레지스트리 및 값](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings) 이름 및 데이터 추가적인 표 합니다.  

6.  문자열의 이름을 입력 한 다음 ENTER 키를 누릅니다. 참조는 [문자열을 레지스트리 및 값](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings) 이름 및 데이터 추가적인 표 합니다.  

  
7.  새 문자열을 마우스 오른쪽 단추로 클릭 한 다음 한 **수정**합니다.  
  
8.  테이블 관련 된 문자열이 이름 값을 입력 하 고 클릭 한 다음 **확인**합니다.  
  
9. 로고 이미지 또는 추가 링크에 대 한 항목을 만드는 경우 %programFiles%\Windows Server\Bin\OEM에 파일을 복사 합니다. OEM 디렉터리가 만듭니다.  
  
10. 고객은 서버 소유 후 원격 Web Access에 영향을 주는 변경 하는 경우 원격 Web Access 켭니다 해야 합니다. 다음을 수행 고객에 게 안내 합니다.  
  
    1.  대시보드에서 클릭 **설정**을 차례로 클릭 하 고는 **원하는 위치에 액세스** 탭 합니다.  
  
    2.  어디서 나 액세스 켜져 있으면 클릭 **구성**에 웹에 대 한 원격 액세스 확인란의 선택을 취소 합니다는 **선택 어디서 나 액세스 기능을 사용 하** 설정 어디서 나 액세스 마법사의 페이지 합니다.  
  
    3.  클릭 **구성**합니다.  
  
###  <a name="BKMK_RegStrings"></a>다음 표에서 레지스트리 변경이 영향을 브랜드 위치, 문자열 이름 및 데이터 값 합니다.  
  
### <a name="registry-strings-and-values"></a>레지스트리 문자열 및 값  
  
|브랜드의 위치|설명|문자열 이름|데이터 값|  
|--------------------------|-----------------|-----------------|----------------|  
|대시보드 로고|대시보드에 로고 이미지를 추가합니다. 대시보드 로고.png 형식에 있어야 하며 38 픽셀 너비 350 픽셀 보다 큰 해야 합니다.<br /><br /> **중요:** 로고와 대시보드 cobrand, OPK DVD에서 제공 하 고 적절 한 공백 요구 사항을 준수 하는 동안 회사 로고 이미지를 추가 하는 작품 타일 편집 해야 합니다. 자세한 내용은 참조 예제 타일에 대 한는 제공 됩니다.|DashboardLogo|로고 이미지 파일 이름|  
|DashboardClientLogo|로고 이미지 대시보드 클라이언트 로그인 화면에 추가합니다.|DashboardClientLogo|로고 이미지 파일 이름|  
|웹 사이트 배경 그림|원격 Web Access 로그온 페이지에 표시 되는 배경 이미지를 변경 합니다. 일반적인 해상도 다음과 같이 표시 됩니다.<br /><br /> -1024 x 768 픽셀 해상도 정확 하 게 로그온 페이지를 채웁니다.<br /><br /> -800 x 600 픽셀 해상도 페이지에서 가운데 및 검은색 테두리를 표시 합니다.<br /><br /> -초과 1024 × 768 픽셀 표시 되지 않습니다 및 1280 x 720 픽셀 해상도 중심 합니다.|LogonBackground|배경 이미지 파일 이름|  
|제목 웹 사이트|Windows Server Essentials 제목 선택 하는 웹에 대 한 원격 액세스 사이트의 제목을 바꿉니다.|후 WebsiteName|새 웹에 대 한 원격 액세스 사이트 제목|  
|웹 사이트 로고|원격 Web Access 사이트에 기본 로고를 변경합니다. 로고 예상된 크기 32 픽셀입니다. 로고가 보다 더 크게 또는 더 작은 경우이 늘리거나 만든 이러한 크기에 맞게 축소|WebsiteLogo|로고 이미지 파일 이름|  
|추가 된 웹 사이트 로고|파트너 로고 원격 Web Access 사이트에 표시 되는 Microsoft 로고 바로 아래에 표시 됩니다. 로고 예상된 크기 200 픽셀 50 픽셀 너비입니다. 로고가 보다 큰 경우 것은 게 더 작은 원래 가로 세로 비율을 유지 하면서 적합 합니다. 로고가 보다 작으면 200 하 여 50 픽셀 공간 내 가운데 것인지 및 크기 지도 가로 세로 비율 변경 됩니다.|OEMLogo|로고 이미지 파일 이름|  

| 홈페이지 웹 사이트 및 로그온 페이지의 링크를 | 로그온 페이지 및 원격 Web Access 사이트의 홈페이지에 대 한 링크를 추가 합니다. 링크 정보가 포함 된.xml %programFiles%\Windows Server\Bin\OEM에 있어야 합니다. 다음 예제.xml 파일의 형식이 보여 줍니다.<br /><br /> < OemLinks\ ><br /> < LogonLinks\ ><br /> < Name\ 연결 LogonLinkName = ><br /> LogonLinkDescription < Text\ > < / Text\ ><br /> LogonLinkURL < Url\ > < / Url\ ><br /> LinkIcon < Icon\ > < / Icon\ ><br /> < / Link\ ><br /> < / LogonLinks\ ><br /> < HomepageLinks\ ><br /> < Name\ 연결 HomepageLinkName = ><br /> HomepageLinkDescription < Text\ > < / Text\ ><br /> HomepageLinkURL < Url\ > < / Url\ ><br /> < / Link\ ><br /> < / HomepageLinks\ ><br /> < / OemLinks\ > | LinksXML | 참조는 [LinksXML 요소](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links) 요소 및 설명 목록에 대 한 표. |  

| 홈페이지 웹 사이트 및 로그온 페이지의 링크를 | 로그온 페이지 및 원격 Web Access 사이트의 홈페이지에 대 한 링크를 추가 합니다. 링크 정보가 포함 된.xml %programFiles%\Windows Server\Bin\OEM에 있어야 합니다. 다음 예제.xml 파일의 형식이 보여 줍니다.<br /><br /> < OemLinks\ ><br /> < LogonLinks\ ><br /> < Name\ 연결 LogonLinkName = ><br /> LogonLinkDescription < Text\ > < / Text\ ><br /> LogonLinkURL < Url\ > < / Url\ ><br /> LinkIcon < Icon\ > < / Icon\ ><br /> < / Link\ ><br /> < / LogonLinks\ ><br /> < HomepageLinks\ ><br /> < Name\ 연결 HomepageLinkName = ><br /> HomepageLinkDescription < Text\ > < / Text\ ><br /> HomepageLinkURL < Url\ > < / Url\ ><br /> < / Link\ ><br /> < / HomepageLinks\ ><br /> < / OemLinks\ > | LinksXML | 참조는 [LinksXML 요소](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links) 요소 및 설명 목록에 대 한 표. |  

| 실행 패드 로고 | 로고 이미지에서 실행 창에 추가합니다. 실행 패드 로고.png 형식 및 반드시 64 픽셀 하지 높이나 있어야 합니다. | LaunchpadLogo | 로고 이미지 파일의 이름을 |  
  
###  <a name="BKMK_Links"></a>다음 표에서 목록과 LinksXML 문자열 이름 요소에 설명 합니다.  
  
### <a name="linksxml-elements"></a>LinksXML 요소  
  
|LinksXML 요소|설명|  
|----------------------|-----------------|  
|**LogonLinks**|  
|LogonLinkName|로그온 연결 이름입니다.|  
|LogonLinkDescription|로그온 페이지 링크로 표시 되는 텍스트입니다.|  
|LogonLinkURL|Url을 로그온 페이지 링크를 확인 합니다.|  
|LinkIcon|아이콘 파일 로그온 링크에 대 한의 이름입니다. 이 파일.xml 파일와 동일한 폴더 위치에 있어야 합니다. 링크 아이콘 이미지 16 x 16 픽셀 해야 하며.png 포맷 해야 합니다. 한 LinkIcon 제공 하지 않는 경우 기본 링크 아이콘 이미지 사용 됩니다.|  
|**HomepageLinks**|  
|HomepageLinkName|홈페이지 연결 이름입니다.|  
|HomepageLinkDescription|홈페이지 링크로 표시 되는 텍스트입니다.|  
|HomepageLinkURL|URL을 홈페이지 링크를 확인 합니다.|  
|HomepageLinkIcon|아이콘 파일 홈페이지 링크에 대 한의 이름입니다. 이 파일.xml 파일와 동일한 폴더 위치에 있어야 합니다. HomepageLinkIcon 이미지 16 x 16 픽셀 해야 하며.png 포맷 해야 합니다. 한 HomepageLinkIcon 제공 하지 않는 경우 기본 홈페이지 링크 아이콘 이미지 사용 됩니다.|  
  
## <a name="see-also"></a>참조 하십시오  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

