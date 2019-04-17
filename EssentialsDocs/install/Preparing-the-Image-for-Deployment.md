---
title: "배포에 대 한 이미지를 준비 중"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="preparing-the-image-for-deployment"></a>배포에 대 한 이미지를 준비 중

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이미지를 준비 하는 일반적인 도구가 sysprep.exe입니다. 이 도구를 실행 이미지 일반화할 하 고 이미지를 포함 하는 서버를 다시 시작할 때 실행 초기 구성에서 서버를 종료 합니다. Sysprep.exe 실행 하기 전에 이미지를 모두 수정 작업을 완료 해야 합니다.  
  
> [!NOTE]
>  Windows 정품 인증에 최대 세 번 sysprep.exe을 사용 하 여 초기화할 수 있습니다.  
  
#### <a name="to-prepare-the-image"></a>이미지를 준비 하  
  
1.  추가 하는 SkipIC.txt 삭제 하나요?  
  
2.  관리자 권한 명령 프롬프트 창을 엽니다. 클릭 **시작**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**를 선택한 다음 **관리자 권한으로 실행**합니다.  
  
3.  사용자는 전체 유예 기간이 서버 정책을 준수 하지 않는 되기 전에 되도록 레지스트리 키를 다시 설정 하려면 다음 명령을 실행 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add HKLM\Software\Microsoft\ServerInfrastructureLicensing /v Rearm /t REG_DWORD /d 1 /f  
    ```  
  
4.  키를 언어 페이지, 로캘 페이지 및 EULA 페이지를 표시 레지스트리 키를 추가 하려면 다음 명령을 실행 합니다. 기본적으로 초기 구성 하는 동안 다음이 페이지 표시 되지 않습니다. 따라서 사전 설치 된 상자 해제 하는 경우이 레지스트리 키를 추가 해야 합니다. 그러나 DVD 해제 하는 경우 하지 추가 해야이 키를 WinPE 및 초기 구성 하는 동안 다음이 페이지 표시 됩니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
5.  확인란이 미리 키가 경우 초기 구성 키 페이지를 사용할 수 있습니다. 주요 페이지 표시만 ShowPreinstallPages 않게 및 KeyPreInstalled! 않게 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v KeyPreInstalled /t REG_SZ /d true /f  
    ```  
  
6.  하드웨어 요구 사항을 검사를 사용 하지 않도록 설정 하려면 레지스트리 키를 추가 하려면 다음 명령을 실행 합니다. 하드웨어 요구 사항을 충족 하지 않는 된 사용자 사전 설치 된 상자에 대해서만입니다. DVD를 배포 하거나, 사용자가 상자 하드웨어 요구 사항을 충족,이 키를 추가 하지 않는 것이 좋습니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
7.  (선택 사항) 아래에서 로그 제거 **%programdata%\Microsoft\Windows Server\Logs**합니다.  
  
8.  Sysprep 다음 템플릿을 같이 대 한 자동된 xml 파일을 준비 합니다.  
  
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
  
9. Sysprep에 대 한 다음 명령을 실행 합니다.  
  
    ```  
    %systemroot%\system32\sysprep\sysprep.exe /generalize /OOBE /unattend:xxx.xml /Quit  
    ```  
  
    > [!IMPORTANT]
    >  또한 sysprep 매개도 대신 캡처하에서 unattend.xml 추가할 수 있습니다. 아래에 파일이 c:\ 사용자 s 설정 적용 있지만 sysprep 매개도 사용 하는 경우 것 사용자 s 설정 적용 되지 않습니다. 서버를 다시 시작 될 때마다 unattend.xml 캡처하 아래에서 삭제 됩니다. 따라서 unattend.xml 캡처하 아래를 만든 후 서버를 다시 시작 하지 않으면 있는지 확인 합니다.  
  
10. 레지스트리 키 건너뛰고 Windows OOBE 키 페이지를 추가 하려면 다음 명령을 실행 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedProductKey /t REG_DWORD /d 1 /f  
    ```  
  
11. Windows 언어 페이지 선택 하지 않으려면 레지스트리 키를 추가 하려면 다음 명령을 실행 합니다.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedLanguageSelection /t REG_DWORD /d 1 /f  
    ```  
  
    > [!IMPORTANT]
    >  Windows OOBE 페이지 초기 구성 페이지 및 break 원격 관리 서버 시나리오는은 내놓는 아이디어는 의미 하거나 마지막 2 단계를 수행 해야 합니다.  
  
12. Sysprep 후 상자 종료, 이미지를 캡처할 또는 초기 구성 클라이언트 컴퓨터에서 계속 서버를 다시 시작 수 있습니다.  
  
> [!IMPORTANT]
>  파트너에 게 서버 복구 미디어를 만드는 계획 사진 촬영 하 고 단계로 진행 하기 전에 복구 미디어를 만드는 해야 합니다.