---
title: "공유 폴더를 사용자 지정"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: bcdd43183512bb225dd4afa916f2782c6eb79d7e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="customize-shared-folders"></a>공유 폴더를 사용자 지정

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

기본적으로 서버 폴더가 0 디스크에서 가장 큰 데이터 파티션에 만들어집니다. 파트너의 위치를 사용자 지정 하 고 다음 단계를 사용 하 여 추가 서버 폴더를 지정할 수 있습니다.  
  
1.  사용자 지정 파티션 구성을 사용 하 여 공장 이미지를 만들려면 하 고 sysprep 사용 하기 전에 새 저장소 레지스트리 키를 만듭니다. 하는 동안 초기 구성 (회사 간), 저장소 회사 간 작업 레지스트리 키가 있는지 확인합니다. 있는 경우 기본 서버 폴더 C:\ServerFolders 디렉터리에 만들어집니다.  
  
    #### <a name="to-create-a-new-storage-registry-key"></a>새 저장소 레지스트리 키를 만들려면  
  
    1.  서버에서 화면 오른쪽 위 모서리에 마우스를 이동 하 고 클릭 **검색**합니다.  
  
    2.  검색 상자에 입력 **regedit**을 차례로 클릭 하 고 있는 **Regedit** 응용 프로그램입니다.  
  
    3.  탐색 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 다음를 확장 하 고 **Microsoft**합니다.  
  
    4.  마우스 오른쪽 단추로 클릭 **Windows Server**, 클릭 **새로**을 차례로 클릭 하 고 **키**합니다.  
  
    5.  키 이름 **저장소**합니다.  
  
    6.  탐색 창에서 마우스 오른쪽 단추로 클릭 새 저장소 레지스트리 키를 클릭 **새로**을 차례로 클릭 하 고 **DWORD (32 비트) 값**합니다.  
  
    7.  이름을 지정 문자열 **CreateFoldersOnSystem**합니다.  
  
    8.  마우스 오른쪽 단추로 클릭 **CreateFoldersOnSystem**을 차례로 클릭 하 고 **수정**합니다. **문자열 편집** 대화 상자가 나타납니다.  
  
    9. 새이 키를 설정 **1**을 차례로 클릭 하 고 **확인**합니다.  
  
2.  PostIC.cmd 스크립트를 사용 하 여 다른 위치에 폴더 이동 하거나 추가 된 폴더를 만들 수 있습니다. 다음 예제 참조: [예제 1: 사용자 지정 폴더를 만들고 기본 폴더를 새 위치로 이동 PostIC.cmd에서 Windows PowerShell를 사용 하 여](Customize-Shared-Folders.md#BKMK_Example1)합니다.  
  
3.  Windows Server 솔루션 SDK를 사용 하 여 다른 위치에 폴더 이동 하거나 추가 된 폴더를 만들 수 있습니다. 다음 예제를 참조: [예제 2: Windows Server 솔루션 SDK를 사용 하 여 기존 폴더 이동을 사용자 지정 폴더를 만들고](Customize-Shared-Folders.md#BKMK_Example2)합니다.  
  
 필요에 따라 파트너 두면 데이터 폴더 C 드라이브에서 이렇게 하면 최종 사용자 또는 재판매인 데이터 드라이브에 데이터 폴더에서의 레이아웃 확인 합니다.  
  
###  <a name="BKMK_Example1"></a>기본 폴더를 새 위치로 이동 PostIC.cmd에서 Windows PowerShell를 사용 하 여을 사용자 지정 폴더를 만들고 예제 1:  
  
1.  설명한 대로 게시물 초기 구성 작업을 실행 하기 위한 PostIC.cmd 파일을 만들는 [게시물 초기 구성 작업을 실행을 위한 PostIC.cmd 파일 만들기](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) 섹션.  
  
2.  메모장을 사용 하 여 파일을 만듭니다 **customizefolders.ps1** C:\Windows\Setup\Scripts 폴더 및 다음과 같은 Windows PowerShell 붙여® 파일로 명령 (표시 지우기 동작에 따라 적절 한 줄).  
  
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
  
3.  다음 줄이이 스크립트를 실행할 PostIC.cmd 파일을 추가 합니다.  
  
    ```  
    REM Lower the execution policy  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy RemoteSigned"  
  
    REM Execute the folder customization script  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" -NoProfile -Noninteractive -command ". %windir%\setup\scripts\customizefolders.ps1;exit $LASTEXITCODE"  
    Set error_level=%ERRORLEVEL%  
  
    REM Restore the execution policy to deafult  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy Restricted"  
    Set ERRORLEVEL=%error_level%  
    ```  
  
###  <a name="BKMK_Example2"></a>2 예: 사용자 지정 폴더 만들기 및 Windows Server 솔루션 SDK를 사용 하 여 기존 폴더 이동  
 사용자가 만든 코드는 실행 컴파일 하 고 PostIC.cmd 파일에서 호출 하거나 수 직접 설치 된 추가 기능에서 이라고 합니다.  
  
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
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)