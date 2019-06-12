---
title: 공유 폴더 사용자 지정
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47bc4986-14eb-4a29-9930-83a25704a3a0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d8f52cbe76204bb00cb15c3093f69daf3d8abb6e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433529"
---
# <a name="customize-shared-folders"></a>공유 폴더 사용자 지정

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

기본적으로 서버 폴더는 디스크 0의 가장 큰 데이터 파티션에 생성됩니다. 파트너는 다음 단계에 따라 위치를 사용자 지정하고 추가 서버 폴더를 지정할 수 있습니다.  
  
1. 사용자 지정 파티션 구성을 사용하여 출하 시 이미지를 만든 다음 sysprep을 사용하기 전에 새 저장소 레지스트리 키를 만듭니다. IC(초기 구성) 동안 저장소 IC 작업에서 이 레지스트리 키를 확인합니다. 레지스트리 키가 있는 경우 기본 서버 폴더가 C:\ServerFolders 디렉터리에 만들어집니다.  
  
   #### <a name="to-create-a-new-storage-registry-key"></a>새 저장소 레지스트리 키를 만들려면  
  
   1.  서버에서 마우스를 화면 오른쪽 상단 구석으로 옮긴 후 **검색**을 클릭합니다.  
  
   2.  검색 상자에 **regedit**를 입력하고 **Regedit** 응용 프로그램을 클릭합니다.  
  
   3.  탐색 창에서 **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**를 차례로 확장합니다.  
  
   4.  **Windows Server**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **키**를 클릭합니다.  
  
   5.  키 이름을 **Storage**로 지정합니다.  
  
   6.  탐색 창에서 새 저장소 레지스트리 키를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **DWORD(32비트) 값**을 클릭합니다.  
  
   7.  문자열 이름을 **CreateFoldersOnSystem**으로 지정합니다.  
  
   8.  **CreateFoldersOnSystem**을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다. **문자열 편집** 대화 상자가 나타납니다.  
  
   9. 이 새 키 값을 **1**로 설정한 다음 **확인**을 클릭합니다.  
  
2. PostIC.cmd 스크립트를 사용하여 폴더를 다른 위치로 이동하거나 추가 폴더를 만듭니다. 다음 예제를 참조하십시오. [예제 1: 사용자 지정 폴더를 만들고 기본 폴더는 Windows PowerShell을 사용 하 여 PostIC.cmd에서 새 위치로 이동](Customize-Shared-Folders.md#BKMK_Example1)합니다.  
  
3. Windows Server 솔루션 SDK를 사용하여 폴더를 다른 위치로 이동하거나 추가 폴더를 만듭니다. 다음 예제를 참조하십시오. [예제 2: 사용자 지정 폴더를 만들고 Windows Server 솔루션 SDK를 사용 하 여 기존 폴더를 이동](Customize-Shared-Folders.md#BKMK_Example2)합니다.  
  
   선택적으로 파트너는 C 드라이브에 데이터 폴더를 남겨둘 수 있습니다. 이렇게 하면 최종 사용자 또는 대리점이 데이터 드라이브에서 데이터 폴더의 레이아웃을 확인할 수 있습니다.  
  
###  <a name="BKMK_Example1"></a> 예제 1: Windows PowerShell을 사용하여 PostIC.cmd에서 사용자 지정 폴더를 만들고 기본 폴더를 새 위치로 이동합니다.  
  
1.  [초기 구성 후 작업 실행을 위해 PostIC.cmd 파일 만들기](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) 섹션의 세부 정보에 따라 초기 구성 후 작업 실행을 위해 PostIC.cmd 파일을 만듭니다.  
  
2.  메모장을 사용하여 C:\Windows\Setup\Scripts 폴더에 **customizefolders.ps1**이라는 파일을 만든 후 다음 Windows PowerShell® 명령을 파일에 붙여 넣습니다(원하는 동작에 따라 적절한 줄을 표시 해제).  
  
    ```  
    # Move the Documents folder to D:\ServerFolders  
    #Get-WssFolder -name Documents| Move-WssFolder - NewDrive D:\ -Force  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    # Move all folders to D:\ServerFolders  
    #foreach( $folder in Get-WssFolder )  
    #{  
    #    Move-WssFolder $folder -NewDrive D:\ -Force  
    #}  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    # Create a custom folder named Custom Folder  
    #Add-WssFolder -Name CustomFolder -Path D:\ServerFolders\CustomFolder -Description "Custom Folder"  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    exit 0  
    ```  
  
3.  PostIC.cmd 파일에 다음 줄을 추가하여 이 스크립트를 실행합니다.  
  
    ```  
    REM Lower the execution policy  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy RemoteSigned"  
  
    REM Execute the folder customization script  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" -NoProfile -Noninteractive -command ". %windir%\setup\scripts\customizefolders.ps1;exit $LASTEXITCODE"  
    Set error_level=%ERRORLEVEL%  
  
    REM Restore the execution policy to default  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy Restricted"  
    Set ERRORLEVEL=%error_level%  
    ```  
  
###  <a name="BKMK_Example2"></a> 예제 2: Windows Server 솔루션 SDK를 사용하여 사용자 지정 폴더를 만들고 기존 폴더를 이동합니다.  
 만든 코드는 실행 파일로 컴파일하여 PostIC.cmd 파일에서 호출하거나 설치된 추가 기능에서 직접 호출할 수 있습니다.  
  
```  
static void Main(string[] args)  
{  
 StorageManager storageManager = new StorageManager();  
 //Connect to the StorageManager  
 storageManager.Connect();  
  
 //Move the Documents folder to D:\ServerFolders  
 Folder targetFolder = storageManager.Folders.First(folder => folder.Name == "Documents");  
  
 MoveFolderRequest moveRequest = targetFolder.GetMoveRequest(@"D:\");  
 moveRequest.MoveFolder();  
  
 //Verify operation was successful, if so print result  
 if (moveRequest.Status == OperationStatus.Succeeded)  
 {  
  Console.WriteLine("Folder {0} now located at {1}", targetFolder.Name, targetFolder.Path);  
 }  
  
 string newFolderName = "New Custom Folder";  
 string newFolderLocation = @"C:\ServerFolders\New Custom Folder";  
  
 //Create add request based with specific name and location  
 CreateFolderRequest request = storageManager.GetCreateFolderRequest(newFolderName, newFolderLocation);  
  
 //Give Guest user read only permission to folder  
 request.PermissionsByName.Add(new NamePermission("Guest", Permission.ReadOnly));  
  
 //Create the new folders  
 request.CreateFolder();  
  
 //Verify operation was successful, if so print result  
 if( request.Status == OperationStatus.Succeeded)  
 {  
  Folder newFolder = storageManager.Folders.First(folder => folder.Path == newFolderLocation);  
  
  Console.WriteLine("Folder {0} created at {1}", newFolder.Name, newFolder.Path);  
 }  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)
