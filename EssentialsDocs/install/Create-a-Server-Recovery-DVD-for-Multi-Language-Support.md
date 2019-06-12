---
title: 다국어 지원을 위한 서버 복구 DVD 만들기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7da0f6c-9732-4784-9c28-7dad72c4071d
4author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e2bbc7bf7af71c671153bf7ba3356ddc08dcc38b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433635"
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>다국어 지원을 위한 서버 복구 DVD 만들기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_MLHeadedRecovery"></a> 로컬로 관리 되는 서버에서 서버 설치 및 다중 언어 지원 위한 서버 복구 DVD 만들기  
  
> [!NOTE]
>  에 설명 된 대로 다국어 Windows 이미지를 먼저 만들어야 합니다를 [연습: 다국어 Windows 이미지 만들기](https://technet.microsoft.com/library/jj126995) Windows Server Essentials 언어 팩을 install.wim에 추가 하기 전에 합니다.  
  
 설정은 Windows PE(Preinstallation Environment)와 초기 구성의 두 단계로 이루어집니다. 기본적으로 초기 구성의 언어 선택 페이지는 표시되지 않습니다.  
  
- OEM 원격 관리 설치나 OEM 사전 설치 시나리오의 경우 다음 명령을 사용하여 레지스트리 키를 추가해야 초기 구성에서 언어 선택 페이지가 표시됩니다.  
  
  ```  
  %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
  ```  
  
  > [!IMPORTANT]
  >  OEM은 랩에서 이미지를 만드는 경우 Windows PE 설치 단계 중에 **한국어** 를 언어로 선택해야 합니다.  
  
- ROK(Reseller Option Kit) 시나리오에서는 고객에게 DVD와 일부 하드웨어(해당되는 경우)가 제공됩니다. 고객은 Windows PE 설치 중 언어를 선택할 수 있고 언어 선택 페이지는 초기 구성 중 더 이상 표시되지 않습니다.  
  
  여러 언어가 포함된 단일 이중 계층 DVD를 제공하도록 선택할 수 있습니다.  
  
  이 섹션에서는 Windows 설치 프로그램에 언어 지원을 추가하는 방법에 대해 설명합니다. Windows PE 3.0을 사용자 지정하기 위한 기본 도구는 명령줄 도구인 DISM(배포 이미지 서비스 및 관리)입니다. 이 솔루션은 다음 시나리오를 가능하게 합니다.  
  
1.  다국어 설치 만들기  
  
2.  배포 가능 미디어 만들기  
  
### <a name="prerequisites"></a>사전 요구 사항  
 Windows 설치 프로그램에 다국어 지원을 추가하려면 다음이 필요합니다.  
  

-   사용자 지정 WinPE 이미지를 만드는 데 필요한 모든 도구 및 원본 파일을 제공하는 관리자 컴퓨터. 자세한 내용은 [Prepare the Technician Computer](Prepare-the-Technician-Computer.md)를 참조하세요.  

-   사용자 지정 WinPE 이미지를 만드는 데 필요한 모든 도구 및 원본 파일을 제공하는 관리자 컴퓨터. 자세한 내용은 [Prepare the Technician Computer](../install/Prepare-the-Technician-Computer.md)를 참조하세요.  

  
-   Windows Server Essentials DVD입니다.  
  
-   Windows Server Essentials 언어 팩 DVD입니다.  
  
###  <a name="BKMK_Steps"></a> 다중 언어 지원 추가  
 Windows 설치 프로그램에 다중 언어 지원을 추가 하려면 Windows Server 2012를 추가 하 여 Install.wim을 업데이트 하 고 Windows Server Essentials 언어 팩을 합니다.  
  
#### <a name="update-installwim"></a>Install.wim 업데이트  
 이 단계에서 추가한 Windows Server 2012 및 Windows Server Essentials 언어 팩을 Install.wim에 있습니다.  
  
> [!NOTE]
>  Windows Server 2012에 대 한 언어 팩 설치를 확인 합니다. 이렇게 하면 적절한 브랜딩을 가져오게 됩니다. Windows Server 2012 다국어 사용자 인터페이스 언어 팩을 사용할 [Microsoft.com](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx)합니다. 에 설명 된 대로 지침을 따르세요는 [연습: 다국어 Windows 이미지 만들기를 다국어](https://technet.microsoft.com/library/jj126995.aspx) 에서 다국어 Windows 이미지를 만들고 Windows Server Essentials 언어 팩을 install.wim에 추가 합니다.  
>   
>  Windows Server Essentials 언어 팩은 \Language 팩에서 언어 팩 미디어에서\\< CultureName\>합니다.  
  
> [!NOTE]
>  일부 언어 팩에 Windows Server 2012의 릴리스 전에 사용할 수 없음이 될 수 있습니다.  
  
###### <a name="to-add-language-packs-to-installwim"></a>Install.wim에 언어 팩을 추가 하려면  
  
1.  다음과 같이 Install.wim에 운영 체제 및 제품 언어 팩을 추가합니다(이 예에서는 프랑스어를 사용함).  
  
    ```  
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount  
    Mkdir c:\temp_Scratch  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab  
  
    ```  
  

2.  클라이언트 백업 복원 USB 제작 지원을 위한 언어별 파일을 플래시 드라이브에 설명 된 절차를 사용 하 여 추가 [다국어 클라이언트 복원 미디어 빌드](Build-Multi-Language-Client-Restore-Media.md)합니다.  

2.  클라이언트 백업 복원 USB 제작 지원을 위한 언어별 파일을 플래시 드라이브에 설명 된 절차를 사용 하 여 추가 [다국어 클라이언트 복원 미디어 빌드](../install/Build-Multi-Language-Client-Restore-Media.md)합니다.  

  
3.  `DISM /Gen-LangINI` 명령을 사용하여 추가 언어 지원이 반영되도록 느슨한 미디어에 Lang.ini 파일을 다시 만듭니다. 예를 들면 다음과 같습니다.  
  
    ```  
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution  
  
    ```  
  
4.  `DISM /unmount /commit` 명령을 사용하여 변경 내용을 이미지에 다시 저장합니다. 예를 들면 다음과 같습니다.  
  
    ```  
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit  
    ```  
  
## <a name="see-also"></a>관련 항목  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](../install/Additional-Customizations.md)   
 [배포용 이미지 준비](../install/Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](../install/Testing-the-Customer-Experience.md)

