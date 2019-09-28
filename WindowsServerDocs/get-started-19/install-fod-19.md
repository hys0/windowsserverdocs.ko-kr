---
title: Server Core 앱 호환성 FOD(Feature on Demand)
description: Windows Server 주문형 기능을 설치하는 방법
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 9ba0303d1eebc2138db7c5f1428ce920b0cb8af0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360825"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>Server Core 앱 호환성 FOD(Feature on Demand)

> 적용 대상: Windows Server 2019, Windows Server 반기 채널

**Server Core 앱 호환성 FOD(Feature on Demand)** 는 Windows Server 2019 Server Core 설치 또는 Windows Server 반기 채널에 언제든지 추가할 수 있는 선택적 기능 패키지입니다.

FOD(Feature on Demand)에 대한 자세한 내용은 [주문형 기능](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)을 참조하세요.

## <a name="why-install-the-app-compatibility-fod"></a>앱 호환성 FOD를 설치하는 이유

Server Core의 주문형 기능인 앱 호환성은 Windows Server Desktop Experience 그래픽 환경을 추가하지 않고 Windows Server의 바이너리 및 패키지 하위 세트를 데스크톱 환경에 포함하여 Windows Server Core 설치 옵션의 앱 호환성을 크게 향상시킵니다. 이 선택적 패키지는 별도의 ISO 또는 Windows 업데이트에서 사용할 수 있지만 Windows Server Core 설치 및 이미지에만 추가할 수 있습니다.

앱 호환성 FOD가 제공하는 두 가지 주요 가치는 다음과 같습니다.

- 이미 시장에 있거나 조직에서 이미 개발하여 배포한 서버 애플리케이션에 대한 Server Core 호환성을 향상시킵니다.
- 심각한 문제 해결 및 디버깅 시나리오에 사용되는 소프트웨어 도구의 앱 호환성을 향상시키고 OS 구성 요소를 제공하는 데 도움을 줍니다.

Server Core 앱 호환성 FOD의 일부로 제공되는 운영 체제 구성 요소는 다음과 같습니다.

-   Microsoft Management Console(mmc.exe)

-   이벤트 뷰어(Eventvwr.msc)

-   성능 모니터(PerfMon.exe)

-   리소스 모니터(Resmon.exe)

-   디바이스 관리자(Devmgmt.msc)

-   파일 탐색기(Explorer.exe)

-   Windows PowerShell(Powershell_ISE.exe)

-   디스크 관리(Diskmgmt.msc)

-   장애 조치(failover) 클러스터 관리자(CluAdmin.msc)

    -   장애 조치(failover) 클러스터링 Windows Server 기능을 먼저 추가해야 합니다.

        -   관리자 권한으로 PowerShell 세션에서 다음을 수행합니다. 

            ```PowerShell
            Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools
            ```

        -   장애 조치(failover) 클러스터 관리자를 실행하려면 명령 프롬프트에 **cluadmin**을 입력합니다.

Windows Server, 버전 1903 이상을 실행하는 서버는 다음 구성 요소도 지원합니다(동일한 버전의 앱 호환성 FOD를 사용하는 경우).

- Hyper-V 관리자(virtmgmt.msc)
- 작업 스케줄러(taskschd.msc)

## <a name="installing-the-app-compatibility-fod"></a>앱 호환성 FOD 설치

앱 호환성 FOD는 Server Core에만 설치할 수 있습니다. 데스크톱 환경 포함 Windows Server의 Windows Server 설치에 Server Core 앱 호환성 FOD를 추가하려고 하지 마십시오. Windows Server 2019 Server Core 설치 또는 Windows Server 반기 채널 설치에 동일한 FOD 옵션 패키지 ISO를 사용할 수 있습니다.

1. 서버가 Windows 업데이트에 연결할 수 있으면, 관리자 권한으로 PowerShell 세션에서 다음 명령을 실행한 다음, 명령 실행이 완료되면 Windows Server를 다시 시작하기만 하면 됩니다.

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0
    ```

2. 서버가 Windows 업데이트에 연결할 수 없으면, Server FOD 선택적 패키지인 ISO를 다운로드하고 ISO를 로컬 네트워크의 공유 폴더에 복사합니다.

   - 볼륨 라이선스가 있는 경우 OS ISO 이미지 파일을 가져온 포털에서 Server FOD ISO 이미지 파일을 다운로드할 수 있습니다. [볼륨 라이선스 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx).
   - Server FOD ISO 이미지 파일은 구독자를 위한 [Visual Studio 포털](https://visualstudio.microsoft.com) 또는 [Microsoft 평가 센터](https://www.microsoft.com/evalcenter/evaluate-windows-server)에서도 사용할 수 있습니다.

3. 로컬 네트워크에 연결되어 있고 FOD를 추가하려는 Server Core 컴퓨터의 관리자 계정으로 로그인합니다.

4. **net use** 또는 다른 메서드를 사용하여 FOD ISO의 위치에 연결합니다.

5. FOD ISO를 원하는 로컬 폴더에 복사합니다.

6. 관리자 권한으로 PowerShell 세션에서 다음 명령을 사용하여 FOD ISO를 탑재합니다.

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

7. 다음 명령을 실행합니다.

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0 -Source <Mounted_Server_FOD_Drive> -LimitAccess
     ```

8. 진행률 표시줄이 완료되 면 운영 체제를 다시 시작합니다.

   DISM 명령에 대한 자세한 내용은 [Windows PowerShell에서 DISM 사용](https://docs.microsoft.com/windows-hardware/manufacture/desktop/use-dism-in-windows-powershell-s14)을 참조하세요.

## <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>Server Core에 Internet Explorer 11을 선택적으로 추가하려면(Server Core 앱 호환성 FOD를 추가한 후)

 >[!NOTE]  
   > Server Core 앱 호환성 FOD는 Internet Explorer 11을 추가하는 데 필요하지만 Internet Explorer 11에는 Server Core 앱 호환성 FOD를 추가할 필요가 없습니다.

1. 앱 호환성 FOD가 이미 추가되고 서버 FOD 선택적 패키지 ISO가 로컬로 복사된 Server Core 컴퓨터에 관리자로 로그인합니다.

2. 명령 프롬프트에 **powershell.exe**를 입력하여 PowerShell을 시작합니다.

3. 다음 명령을 사용하여 FOD ISO를 탑재합니다.

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

4. `$package_path` 변수를 사용하여 Internet Explorer cab 파일의 경로를 입력하여 다음 명령을 실행합니다.

    ```PowerShell
    $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

    Add-WindowsPackage -Online -PackagePath $package_path
    ```

5. 진행률 표시줄이 완료되 면 운영 체제를 다시 시작합니다.

## <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>Server Core 앱 호환성 FOD 및 Internet Explorer 11 선택적 패키지에 대한 제안 및 릴리스 정보

> [!IMPORTANT]
> Windows Server, 버전 1809에 설치된 FOD는 Windows Server, 버전 1903으로 전체 업그레이드된 후에 그대로 유지되지 않기 때문에, 업그레이드 후에 다시 설치해야 합니다. 또는 업그레이드 전에 FOD를 새 Windows Server 설치 원본에 추가할 수 있습니다. 이렇게 하면 업그레이드가 완료된 후 FOD의 새 버전이 존재합니다. 자세한 내용은 [오프라인 WIM Server Core 이미지에 기능 및 선택적 패키지 추가](install-fod-19.md#add-capabilities)를 참조하세요.

- **중요:** Server Core 앱 호환성 FOD 및 Internet Explorer 11 선택적 패키지의 설치를 진행하고 사용하기 전에 Windows Server 2019 릴리스 정보에서 문제점, 고려 사항 또는 지침을 읽어보세요.

- Windows 업데이트를 사용하여 누적 업데이트를 설치한 후, 앱 호환성 FOD를 추가할 때 Server Core 콘솔 환경이 깜박일 수 있습니다.  이 문제는 2018년 12월 업데이트로 해결됩니다.  자세한 정보 및 해결 단계는 [기술 자료 문서 4481610: Windows Server 2019 Server Core에 Server Core 앱 호환성 FOD를 설치한 후 화면 깜박임](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core)을 참조하세요.

- 앱 호환성 FOD를 설치하고 서버를 재부팅하면 명령 콘솔 창 프레임 색상이 다른 파란색 음영으로 변경됩니다.

- Internet Explorer 11 선택적 패키지도 설치하는 경우, 로컬에 저장된 .htm 파일을 두 번 클릭하여 여는 것이 지원되지 않습니다. 하지만 **마우스 오른쪽 단추를 클릭**하고 **Internet Explorer에서 열기**를 선택하거나 Internet Explorer **파일** -> **열기**에서 직접 열 수 있습니다.

- 앱 호환성 FOD와 Server Core의 앱 호환성을 향상시키기 위해, IIS 관리 콘솔이 Server Core에 선택적 구성 요소로 추가되었습니다.  단, IIS 관리 콘솔을 사용하려면 먼저 앱 호환성 FOD를 추가해야 합니다. IIS 관리 콘솔은 Microsoft Management Console(mmc.exe)을 사용하며, 이것은 앱 호환성 FOD가 추가된 Server Core에서만 사용할 수 있습니다.  Powershell [**Install-WindowsFeature**](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps)를 사용하면 IIS 관리 콘솔을 추가할 수 있습니다.

- 일반적인 지침의 일환으로, Server Core에 앱을 설치할 때(이 선택적 패키지의 유무에 관계 없이) 자동 설치 옵션과 지침을 사용해야 하는 경우가 있습니다. 
    
  - 예를 들어 SQL Server 2016 및 SQL Server 2017용 SQL Server Management Studio는 Server Core에 설치될 수 있으며 앱 호환성 FOD가 있을 때 완전하게 작동합니다.  [명령 프롬프트에서 SQL Server 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017)를 참조하세요.
  - SQL Server Management Studio를 사용하지 않으려면 Server Core 앱 호환성 FOD를 설치할 필요가 없습니다.  [Server Core에 SQL Server 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017)를 참조하세요.

## <a name="a-idadd-capabilities-adding-capabilities-and-optional-packages-to-an-offline-wim-server-core-image"></a><a id="add-capabilities"> 오프라인 WIM Server Core 이미지에 기능 및 선택적 패키지 추가

1. Windows Server 및 Server FOD ISO 이미지 파일을 Windows 컴퓨터의 로컬 폴더로 다운로드합니다.

   - 볼륨 라이선스가 있으면 [볼륨 라이선스 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx)에서 Windows Server와 Server FOD ISO 이미지 파일을 다운로드할 수 있습니다.
   - Server FOD ISO 이미지 파일은 구독자를 위한 [Visual Studio 포털](https://visualstudio.microsoft.com) 또는 [Microsoft 평가 센터](https://www.microsoft.com/evalcenter/evaluate-windows-server)의 장기 서비스 채널 릴리스에서도 사용할 수 있습니다.

2. PowerShell 세션을 관리자로 연 다음, 다음 명령을 사용하여 이미지 파일을 드라이브로 탑재합니다.

   ```PowerShell
   Mount-DiskImage -ImagePath Path_To_ServerFOD_ISO
   Mount-DiskImage -ImagePath Path_To_Windows_Server_ISO
   ```

3. Windows Server ISO 파일의 내용을 로컬 폴더(예: *C:\SetupFiles\WindowsServer*)에 복사합니다.

4. 다음 명령을 사용하여 Install.wim 파일에서 수정할 이미지 이름을 가져옵니다.<br>
`$install_wim_path` 변수를 사용하여 ISO 파일의 \Sources 폴더에 있는 Install.wim 파일의 경로를 입력합니다.

   ```PowerShell
   $install_wim_path = "C:\SetupFiles\WindowsServer\sources\install.wim"

   Get-WindowsImage -ImagePath $install_wim_path
   ```

5. 다음 명령을 사용하여 샘플 변수 값을 실제 값으로 바꾸고 이전 명령의 `$install_wim_path` 변수를 다시 사용하여 Install.wim 파일을 새 폴더에 탑재합니다.<br>

   - `$image_name` - 탑재할 이미지의 이름을 입력합니다.
   - `$mount_folder variable` - Install.wim 파일의 내용에 액세스할 때 사용할 폴더를 지정합니다.

   ```PowerShell
   $image_name = "Windows Server Datacenter"
   $mount_folder = "c:\test\offline"

   Mount-WindowsImage -ImagePath $install_wim_path -Name $image_name -path $mount_folder
   ```

6. 다음 명령을 사용하고 샘플 변수 값을 실제 값으로 바꿔서 탑재된 Install.wim 이미지에 원하는 기능과 패키지를 추가합니다.<br>

   - `$capability_name` - 설치할 기능의 이름을 지정합니다(이 예제의 경우 AppCompatibility 기능).
   - `$package_path` - 설치할 패키지의 경로를 지정합니다(이 예제의 경우 Internet Explorer).
   - `$fod_drive` - 탑재된 서버 FOD 이미지의 드라이브 문자를 지정합니다.

   ```PowerShell
   $capability_name = "ServerCore.AppCompatibility~~~~0.0.1.0"
   $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"
   $fod_drive = "d:\"

   Add-WindowsCapability -Path $mount_folder -Name $capability_name -Source $fod_drive -LimitAccess
   Add-WindowsPackage -Path $mount_folder -PackagePath $package_path
   ```

7. 이전 명령의 `$mount_folder` 변수를 사용하는 다음 명령을 사용하여 Install.wim 파일의 변경 사항을 분리하고 커밋합니다.

   ```PowerShell
   Dismount-WindowsImage -Path $mount_folder -Save
   ```

이제 Windows Server 설치 파일용으로 만든 폴더에서 setup.exe를 실행하여 서버를 업그레이드할 수 있습니다(이 예제의 경우: *C:\SetupFiles\WindowsServer*). 이제 이 폴더에 추가 기능 및 선택적 패키지가 포함된 Windows Server 설치 파일이 들어 있습니다.