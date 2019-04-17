---
title: "Oobe.xml 파일 로고 및 EULA 포함 하 여 만들기"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a7b3cc1-21bb-4344-8110-f5d5959b370d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f8f99a2051e114b3c890f1cdac23aebf58689980
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-the-oobexml-file-including-logo-and-eula"></a>Oobe.xml 파일 로고 및 EULA 포함 하 여 만들기

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

초기 구성 Oobe.xml 파일을 사용 하 여 자신의 최종 사용자 사용권 계약 EULA ()를 추가할 수 있습니다. Oobe.xml 초기 구성, Windows 시작 및 최종 사용자에 게 제공 하는 기타 페이지에 대 한 텍스트와 이미지를 제공 하는 데 사용 하는 파일입니다. 최종 사용자의 언어와 국가 또는 지역 선택한 항목에 따라 콘텐츠를 사용자 지정할 수 있는 여러 Oobe.xml 파일을 추가할 수 있습니다. 자세한 내용은 참조는 [Windows Assessment and Deployment Kit Windows 8에 대 한](https://go.microsoft.com/fwlink/?LinkId=248694) 설명서 합니다.  
  
 회사에 대 한 EULA Microsoft EULA 외에도 표시 됩니다. Microsoft EULA는 첫 번째 EULA 초기 구성 최종 사용자 환경 중 표시 될 고 EULA 표시 됩니다. 서버에서 EULA 어디서 나 배치할 수 있으며 Oobe.xml 파일의 위치를 지정 합니다.  
  
#### <a name="to-add-your-company-eula-and-logo"></a>회사 EULA 및 로고 추가 하려면  
  
1.  메모장과 같은 텍스트 편집기에 Oobe.xml 파일을 엽니다.  
  
2.  < Logopath\ >< 내 / logopath\ > 태그 절대 경로 로고 파일을 입력 합니다. 이 파일에는 절대 x입니다 32 비트 이동식 네트워크 그래픽 (.png) 파일이 있어야 합니다.  
  
3.  < Eulafilename\ >< 내 / eulafilename\ > 태그를 EULA 파일 절대 경로 입력 합니다. EULA 파일 서식 있는 텍스트 (.rtf) 파일 여야 합니다.  
  
4.  < Name\ >< 내 / name\ > 태그, 회사 이름을 입력 합니다.  
  
     다음 예제 Oobe.xml 파일에 태그를 보여 줍니다.  
  
    ```  
  
    <FirstExperience>  
       <oobe>  
          <oem>  
             <name>Fabrikam</name>  
             <logopath>c:\fabrikam\fabrikam.png</logopath>  
             <eulafilename>c:\fabrikam\fabrikam_eula.rtf</eulafilename>  
          </oem>  
       </oobe>  
    </FirstExperience>  
  
    ```  
  
5.  파일을 저장 합니다.  
  
6.  Oobe.xml 파일은 다음 위치 중 하나에 넣습니다.  
  
    |Oobe.xml 위치|위치를 결정 하는 조건|  
    |-----------------------|----------------------------------------|  
    |%windir%\system32\oobe\info\|서버 단일 국가/지역 및 언어 시스템에서 배송입니다.|  
    |< language\ > %windir%\system32\oobe\info\default\\|서버 단일 국가/지역 및 언어 시스템 여러 출시 됩니다.|  
    |%windir%\system32\oobe\info\\ < 국가/지역 > \ 및 %windir%\system32\oobe\info\\ < 국가/지역 > \\ < language\ > \|서버 개 이상의 국가/지역에 배송는 및 설정을 각 단일 언어는 국가/지역으로 사용자 지정 해야 합니다. 여기 < 국가/지역 >는 소수점 버전 국가 또는 지역 여기서 서버, 배포 되 고 < language\ >는 소수점 로캘 식별자 (LCID) 버전의 지리적 위치 식별자 (GeoID)의 합니다.|  
  
 흰색 텍스트와 다른 회사 로고를 사용 하는 경우 블루 배경으로 인해 설치 흐름에서 더 나은 표시 될 수 있습니다.  레지스트리 키와 값을 설정 하 여이 로고 필요에 따라 지정할 수 있습니다.  
  
#### <a name="to-specify-a-company-logo-by-setting-the-oem-registry-key"></a>OEM 레지스트리 키를 설정 하 여 회사 로고 지정 하려면  
  
1.  서버에서 화면 오른쪽 위 모서리에 마우스를 이동 하 고 클릭 **검색**합니다.  
  
2.  검색 상자에 입력 **regedit**, 다음 Regedit 응용 프로그램을 클릭 합니다.  
  
3.  탐색 창에서 이동 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**, 확장 **Windows Server**합니다. OEM 키가 없는 경우 다음과 같은 키를 만듭니다.  
  
    1.  마우스 오른쪽 단추로 클릭 **Windows Server**, 클릭 **새로**을 차례로 클릭 하 고 **키**합니다.  
  
    2.  키 이름 입력 **OEM**합니다.  
  
4.  (선택 사항) 로고에 대 한 항목을 만드는 로고 언어 버전을 구분 하기 위해 다른 키를 만들 수 있습니다. 예를 들어, 로고의 영어 및 독일어 버전을 사용 하는 경우는 en 만들 수 기능 키를 de de 키. 폴더와 동일한 폴더에 저장 되므로 로고 파일을 모두 인스턴스 로고 이미지 파일의 각 언어에 대 한 고유한 이름의 제공 해야 합니다. 예를 들어, LogoWithWhiteText_en.png 및 LogoWithWhiteText_de.png 이라고 하는 파일을 만들 수 있습니다.  
  
5.  하거나 마우스 오른쪽 단추로 클릭 **OEM** 적절 한 언어 키를 마우스 오른쪽 단추로 클릭를 클릭 하거나 **새로**을 차례로 클릭 하 고 **문자열 값**합니다.  
  
6.  LogoWithWhiteText 문자열을 입력 하 고 ENTER 키를 누릅니다.  
  
7.  새 문자열을 마우스 오른쪽 단추로 클릭 한 다음 한 **수정**합니다.  
  
8.  로고 이미지를 포함 하 여 경로 입력 한 다음 확인을 클릭 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [Windows Server Essentials ADK 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)