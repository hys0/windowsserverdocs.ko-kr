---
title: 이미지 배포 준비
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 681c6cad-7fde-494f-86a5-f4c7c15d23f9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 16411ab073e9417c52592aa9a6b13707dd461537
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838534"
---
# <a name="preparing-the-image-for-deployment"></a>이미지 배포 준비

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이미지를 준비하는 일반적인 도구는 sysprep.exe입니다. 이 도구를 실행하면 이미지를 포함한 서버가 다시 시작되었을 때 초기 구성이 실행되도록 이미지를 일반화하고 서버를 중지시킵니다. sysprep.exe를 실행하기 전에 이미지에 대한 모든 수정을 완료해야 합니다.  
  
> [!NOTE]
>  sysprep.exe를 실행하여 최대 3회까지 Windows 정품 인증을 재설정할 수 있습니다.  
  
#### <a name="to-prepare-the-image"></a>이미지를 준비하려면  
  
1.  추가한 SkipIC.txt를 삭제합니다.  
  
2.  관리자 권한으로 명령 프롬프트 창을 엽니다. **시작**을 클릭하고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 선택합니다.  
  
3.  다음 명령을 실행하여 레지스트리 키를 재설정함으로써 서버 호환이 중단되기 전에 사용자가 전체 유예 기간을 갖도록 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add HKLM\Software\Microsoft\ServerInfrastructureLicensing /v Rearm /t REG_DWORD /d 1 /f  
    ```  
  
4.  다음 명령을 실행하여 레지스트리 키를 디스플레이 키, 언어 페이지, 로캘 페이지 및 EULA 페이지에 추가합니다. 기본적으로 이러한 페이지는 초기 구성 중 표시되지 않습니다. 따라서 사전 설치한 박스를 다시 릴리스하는 경우 이 레지스트리 키를 추가해야 합니다. 하지만 DVD를 공개하는 경우 이러한 페이지가 WinPE 및 초기 구성 중에 표시되므로 이 키를 추가하지 말아야 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
5.  박스에 키가 사전 지정된 경우 초기 구성 키를 비활성화하세요. 키 페이지는 ShowPreinstallPages = true이고 KeyPreInstalled != true일 때만 표시됩니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v KeyPreInstalled /t REG_SZ /d true /f  
    ```  
  
6.  하드웨어 요구 사항 검사를 비활성화하려면 다음 명령을 실행하여 레지스트리 키를 추가하세요. 이것은 하드웨어 요구 사항을 충족하지 않는 사전 설치 박스에만 해당됩니다. DVD를 릴리스하는 경우 또는 박스가 하드웨어 요구 사항을 충족하는 경우 이 키를 추가하지 않는 것이 좋습니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
7.  (선택 사항) **%programdata%\Microsoft\Windows Server\Logs**에서 로그를 제거합니다.  
  
8.  다음 템플릿에 표시된 것처럼 sysprep을 위해 unattended xml 파일을 준비합니다.  
  
    ```  
    <unattend xmlns="urn:schemas-microsoft-com:unattend" xmlns:ms="urn:schemas-microsoft-com:asm.v3">  
  
      <settings pass="oobeSystem">  
        <component name="Microsoft-Windows-Shell-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" xmlns:wcm="https://schemas.microsoft.com/WMIConfig/2002/State" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
          <!-- Must have -->  
          <OOBE>  
             <HideEULAPage>true</HideEULAPage>  
          </OOBE>  
          <!-- Must have -->  
          <AutoLogon>   
            <Enabled>true</Enabled>   
            <Username>Administrator</Username>   
            <Domain>.</Domain>   
            <Password>   
              <!--You can set any password you like, but keep it consistent with password settings -->       
              <Value>Admin@123</Value>   
              <PlainText>true</PlainText>   
            </Password>   
          </AutoLogon>   
          <UserAccounts>   
           <AdministratorPassword>   
             <!--You can set any password you like, but keep it consistent with auto logon settings -->       
             <Value>Admin@123</Value>   
             <PlainText>true</PlainText>   
           </AdministratorPassword>   
          </UserAccounts>  
  
          <!-- Optional -->  
          <OEMInformation>  
             <HelpCustomized>true</HelpCustomized>  
             <Manufacturer>OEM name</Manufacturer>  
             <Model>model name</Model>  
             <SupportHours>hours</SupportHours>  
             <SupportPhone>123-456-7890</SupportPhone>  
             <SupportURL>http://www.contoso.com</SupportURL>  
          </OEMInformation>  
  
        </component>  
  
      </settings>  
  
      <settings pass="specialize">  
        <component name="Microsoft-Windows-Shell-Setup" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" processorArchitecture="amd64">  
          <!-- Must have -->  
          <ComputerName>Server</ComputerName>          
          <!-- Optional -->  
          <ProductKey>XXXXX-XXXXX-XXXXX-XXXXX-XXXXX</ProductKey>  
        </component>  
      </settings>  
    </unattend>  
    ```  
  
9. sysprep에 대한 다음 명령을 실행합니다.  
  
    ```  
    %systemroot%\system32\sysprep\sysprep.exe /generalize /OOBE /unattend:xxx.xml /Quit  
    ```  
  
    > [!IMPORTANT]
    >  unattend.xml을 sysprep의 매개 변수로 추가하지 않고 %systemdrive% 아래에 추가할 수도 있습니다. 파일을 c:\ 아래에 있는 경우 s 사용자 설정에 따라 적용 됩니다 있지만 sysprep의 매개 변수로 사용 하는 경우 해당 s 사용자 설정에 의해 적용 되지 됩니다. %systemdrive% 아래에 있는 unattend.xml은 서버가 다시 시작될 때마다 삭제됩니다. 따라서 %systemdrive% 아래에 unattend.xml을 만든 후에는 서버가 다시 시작되지 않도록 하세요.  
  
10. 다음 명령을 실행하여 레지스트리 키를 추가하고 Windows OOBE 키 페이지를 건너뜁니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedProductKey /t REG_DWORD /d 1 /f  
    ```  
  
11. 다음 명령을 실행하여 레지스트리 키를 추가하고 Windows 언어 선택 페이지를 건너뜁니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedLanguageSelection /t REG_DWORD /d 1 /f  
    ```  
  
    > [!IMPORTANT]
    >  마지막 2개의 단계를 수행하지 않으면 초기 구성 페이지로 인한 Windows OOBE 페이지가 표시되며 원격 관리 서버 시나리오가 깨지게 됩니다.  
  
12. sysprep 후 박스를 종료하면 이미지를 캡처하거나 서버를 다시 시작하여 클라이언트 컴퓨터에서 초기 구성을 계속할 수 있습니다.  
  
> [!IMPORTANT]
>  서버 복구 미디어를 만들려는 파트너는 다음 단계를 진행하기 전에 이미지를 캡처하고 복구 미디어를 만들어야 합니다.