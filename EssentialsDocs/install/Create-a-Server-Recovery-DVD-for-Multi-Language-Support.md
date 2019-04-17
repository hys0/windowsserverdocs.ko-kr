---
title: "다국어 지원 서버 복구 DVD 만들기"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: ac547f97b48e4cd0ebf87e0935cadc2c539b4d0b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>다국어 지원 서버 복구 DVD 만들기

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_MLHeadedRecovery"></a>로컬에서 관리 되는 서버에 서버 설정 및 여러 언어를 지원 서버 복구 DVD 만들기  
  
> [!NOTE]
>  먼저 만들어야 다국어 Windows 이미지에 설명 된 대로 [연습: 다국어 Windows 이미지를 만들려면](https://technet.microsoft.com/library/jj126995) Windows Server Essentials langauage 팩 install.wim을 추가 하기 전에 합니다.  
  
 설치 중 두 단계는: Windows 사전 설치 환경 (Windows PE) 및 초기 구성 합니다. 기본적으로 초기 구성에서 언어 선택 페이지 표시 되지 않습니다.  
  
-   원격으로 관리 OEM 설치 또는 OEM 사전 설치 시나리오에 대 한는 레지스트리 키 다음 사용 하 여 명령 초기 구성에서 언어 선택 페이지 표시에 추가 해야 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
    > [!IMPORTANT]
    >  선택 해야 Oem 랩에서 이미지를 만든 경우 **영어** 언어로 설정의 Windows PE 단계입니다.  
  
-   재판매인 키트 ROK (옵션) 시나리오에 대 한 고객 DVD를 하 고, 일부 하드웨어를 받습니다. 초기 구성 하는 동안 더 이상 표시 되는 언어 선택 페이지 하 고 고객이 Windows PE 설치 하는 동안 언어를 선택 해야 합니다.  
  
 여러 언어 포함 된 단일 듀얼 계층 DVD 제공 하도록 선택할 수 있습니다.  
  
 Windows 설치 언어 지원을 추가 하는 방법을 설명 합니다. Windows PE 3.0 사용자 지정 하기 위한 기본 도구 배포 이미지 서비스 및 관리 DISM (), 명령줄 도구입니다. 이 솔루션을 사용 하면 다음 시나리오는 다음과 같습니다.  
  
1.  다국어 설치 만들기  
  
2.  배포 미디어 만들기  
  
### <a name="prerequisites"></a>필수  
 다국어 지원을 Windows 설치를 추가 하려면 다음이 필요 합니다.  
  

-   도구 및 사용자 지정 된 WinPE 이미지를 만들려면에 제공 하는 관리자 컴퓨터 합니다. 자세한 내용은 참조 [관리자 컴퓨터 준비](Prepare-the-Technician-Computer.md)합니다.  

-   도구 및 사용자 지정 된 WinPE 이미지를 만들려면에 제공 하는 관리자 컴퓨터 합니다. 자세한 내용은 참조 [관리자 컴퓨터 준비](../install/Prepare-the-Technician-Computer.md)합니다.  

  
-   Windows Server Essentials DVD 합니다.  
  
-   Windows Server Essentials 언어 팩 DVD 합니다.  
  
###  <a name="BKMK_Steps"></a>여러 언어 지원을 추가합니다.  
 Windows 설치 여러 언어 지원을 추가 하는 Windows Server 2012를 추가 하 여 Install.wim 업데이트 및 Windows Server Essentials 언어 팩 것을 합니다.  
  
#### <a name="update-installwim"></a>Install.wim 업데이트  
 이 단계에서 추가할 Windows Server 2012와 Windows Server Essentials 언어 팩 Install.wim에 됩니다.  
  
> [!NOTE]
>  Windows Server 2012 용 언어 팩을 설치할 수 있는지 확인 합니다. 이 적절 한 브랜드을 얻을 수 있도록 보장 합니다. Windows Server 2012 다국어 사용자 인터페이스 언어 팩을 사용할 수 있는 [Microsoft.com](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx)합니다. 에 설명 된 대로 지침에 따라는 [연습: 다국어를 만드는 방법에 대해 Windows 이미지 만들기 다국어](https://technet.microsoft.com/library/jj126995.aspx) Windows Server Essentials 언어 팩을 추가 하기 전에 다국어 Windows 이미지를 만드는 방법에 대해 Install.wim 합니다.  
>   
>  Windows Server Essentials 언어 팩 \Language Packs\\ < CultureName\ >에 언어 팩 미디어에서 사용할 수 있습니다.  
  
> [!NOTE]
>  Windows Server 2012 릴리스 전 사용할 수 없는 언어 팩이 없는 수 있습니다.  
  
###### <a name="to-add-language-packs-to-installwim"></a>언어 팩 Install.wim에 추가 하려면  
  
1.  언어 팩이 운영 체제 및 제품 Install.wim에 추가 하려면 (프랑스어 사용 하 여이 예제) 다음과 같이 합니다.  
  
    ```  
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount  
    Mkdir c:\temp_Scratch  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab  
  
    ```  
  

2.  플래시 드라이브를에 설명 된 절차를 사용 하 여 특정 파일 클라이언트 백업을 복원 USB 만들기를 지 원하는 언어를 추가 [다국어 클라이언트 복원 미디어 빌드](Build-Multi-Language-Client-Restore-Media.md)합니다.  

2.  플래시 드라이브를에 설명 된 절차를 사용 하 여 특정 파일 클라이언트 백업을 복원 USB 만들기를 지 원하는 언어를 추가 [다국어 클라이언트 복원 미디어 빌드](../install/Build-Multi-Language-Client-Restore-Media.md)합니다.  

  
3.  다시 추가 언어 지원을 사용 하 여 반영 헐 미디어에서 Lang.ini 파일은 `DISM /Gen-LangINI`명령,:  
  
    ```  
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution  
  
    ```  
  
4.  사용 하 여 이미지로 다시 변경 내용을 저장는 `DISM /unmount /commit`명령을 예를 들어 다음과 같습니다.  
  
    ```  
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit  
    ```  
  
## <a name="see-also"></a>참조 하십시오  

 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)

 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)

