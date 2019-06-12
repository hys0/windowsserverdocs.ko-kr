---
title: Server Core 앱 호환성 FOD(Feature on Demand)
description: 필요에 따라 Windows Server 기능을 설치 하는 방법
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 747258601aa05885d209aacde6947eb7b05e8121
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810797"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>Server Core 앱 호환성 FOD(Feature on Demand)

> 적용 대상: Windows Server 2019, Windows Server Semi-Annual Channel

**필요에 따라 Server Core 앱 호환성 기능** 은 언제 든 지 Windows Server 2019 Server Core 설치 또는 Windows Server 반기 채널에 추가할 수 있는 선택적 기능 패키지입니다.

기능에서 FOD (주문형)에 대 한 자세한 내용은 참조 하세요. [주문형 기능](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)합니다.

## <a name="why-install-the-app-compatibility-fod"></a>앱 호환성 FOD 설치 하는 이유?

응용 프로그램 호환성, Server Core에 대 한 주문형 기능을 추가 하지 않고 이진 파일 및 데스크톱 환경 포함 Windows Server에서 패키지의 하위 집합을 포함 하 여 Windows Server Core 설치 옵션의 응용 프로그램 호환성을 크게 개선 합니다 Windows Server Desktop Experience 그래픽 환경입니다. 이 선택적 패키지를 별도 ISO 또는 Windows Update에서 사용할 수 있지만 Windows Server Core 설치와 이미지에만 추가할 수 있습니다.

앱 호환성 FOD 제공 두 기본 값은:

- 이미 시장에 또는 이미 조직에서 개발 되어 배포는 서버 응용 프로그램에 대 한 Server Core의 호환성을 증가 합니다.
- OS 구성 요소 및 향상 된 응용 프로그램 호환성 문제 해결 및 디버깅 시나리오 예에 사용 되는 소프트웨어 도구를 제공 하는 데 유용 합니다.

Server Core 앱 호환성 FOD 부분을 포함 하는 대로 사용할 수 있는 운영 체제 구성 요소:

-   Microsoft Management Console (mmc.exe)

-   이벤트 뷰어 (Eventvwr.msc)

-   성능 모니터 (PerfMon.exe)

-   리소스 모니터 (Resmon.exe)

-   장치 관리자 (Devmgmt.msc)

-   파일 탐색기 (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   디스크 관리 (Diskmgmt.msc)

-   장애 조치 클러스터 관리자 (CluAdmin.msc)

    -   먼저 Windows Server를 클러스터링 하는 장애 조치 기능이 필요합니다.

        -   관리자 권한 PowerShell 세션의 경우: 

            ```PowerShell
            Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools
            ```

        -   장애 조치 클러스터 관리자를 실행 하려면 입력 **cluadmin** 명령 프롬프트에서.

Windows Server를 실행 하는 서버 버전이 1903 이상 기능도 다음 구성 요소 (앱 호환성 FOD의 동일한 버전 사용) 하는 경우:

- Hyper-V Manager (virtmgmt.msc)
- 작업 스케줄러 (taskschd.msc)

## <a name="installing-the-app-compatibility-fod"></a>응용 프로그램 호환성 FOD 설치

앱 호환성 FOD Server Core에만 설치할 수 있습니다. Server Core 앱 호환성 FOD 데스크톱 환경 포함 Windows Server의 Windows Server 설치에 추가 하려고 하지 마세요. Windows Server 2019 Server Core 설치 또는 Windows Server 반기 채널 설치에 대 한 동일한 FOD 선택적 패키지 ISO를 사용할 수 있습니다.

1. 서버를 Windows 업데이트에 연결할 수 하면 모든 관리자 권한 PowerShell 세션에서 다음 명령을 실행 하 고 명령이 완료 된 후 실행 중인 Windows Server를 다시는:

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0
    ```

2. 서버를 Windows 업데이트에 연결할 수 없는 경우 대신 서버 FOD 선택적 패키지 ISO를 다운로드 하 고 ISO 로컬 네트워크의 공유 폴더에 복사:

   - 볼륨 라이선스가 있는 경우에 OS ISO 이미지 파일을 가져온 위치 하 고 같은 포털에서 서버 FOD ISO 이미지 파일을 다운로드할 수 있습니다. [볼륨 라이선스 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx)합니다.
   - Server FOD ISO 이미지 파일에서 제공 됩니다. 합니다 [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server) 또는 합니다 [Visual Studio 포털](https://visualstudio.microsoft.com) 구독자에 대 한 합니다.

3. 및에 해당 FOD 추가 하려는 로컬 네트워크에 연결 된 Server Core 컴퓨터에서 관리자 계정으로 로그인 합니다.

4. 사용 하 여 **사용 하 여 net**, 또는 해당 FOD ISO의 위치에 연결할 다른 방법입니다.

5. 선택한 로컬 폴더에는 해당 FOD ISO를 복사 합니다.

6. 관리자 권한 PowerShell 세션에서 다음 명령을 사용 하 여 해당 FOD ISO를 탑재 합니다.

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

7. 다음 명령을 실행합니다.

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0 -Source <Mounted_Server_FOD_Drive> -LimitAccess
     ```

8. 진행률 표시줄이 완료 되 면 운영 체제를 다시 시작 합니다.

   DISM 명령에 대 한 자세한 내용은 참조 하세요. [Windows PowerShell에서 DISM 사용](https://docs.microsoft.com/windows-hardware/manufacture/desktop/use-dism-in-windows-powershell-s14)

## <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>필요에 따라 (Server Core 앱 호환성 FOD 추가) 후 Server Core에 Internet Explorer 11을 추가 하려면

 >[!NOTE]  
   > Server Core 앱 호환성 FOD Internet Explorer 11을 추가 하기 위해 필요 하지만 Internet Explorer 11 Server Core 앱 호환성 FOD 추가 하지 않아도 됩니다.

1. 이미 추가 앱 호환성 FOD 있는 Server Core 컴퓨터에 ISO 로컬로 복사 Server FOD 선택적 패키지 관리자 권한으로 로그인 합니다.

2. 입력 하 여 PowerShell 시작 **powershell.exe** 명령 프롬프트에서.

3. 다음 명령을 사용 하 여 해당 FOD ISO를 탑재 합니다.

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

4. 다음 실행 명령을 사용 하는 `$package_path` Internet Explorer cab 파일의 경로 입력 하는 변수:

    ```PowerShell
    $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

    Add-WindowsPackage -Online -PackagePath $package_path
    ```

5. 진행률 표시줄이 완료 되 면 운영 체제를 다시 시작 합니다.

## <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>릴리스 정보 및 Server Core 앱 호환성 FOD 및 Internet Explorer 11 선택적 패키지에 대 한 제안

> [!IMPORTANT]
> FODs Windows 서버에 설치, 버전 1809 없습니다 상태로 유지 버전이 1903, Windows Server로 현재 위치 업그레이드 후에 업그레이드 후에 다시 설치 해야 합니다. 또는 업그레이드 하기 전에 새 Windows Server 설치 원본 FODs를 추가할 수 있습니다. 이렇게 하면 새 버전의 모든 FODs 있는지 업그레이드 완료 후 합니다. 자세한 내용은 참조는 [오프 라인 WIM Server Core 이미지에 기능 및 선택적 패키지를 추가](install-fod-19.md#add-capabilities)합니다.

- **중요:** 모든 문제, 고려 사항 또는 Server Core 앱 호환성 FOD 및 Internet Explorer 11 선택적 패키지의 설치 및 사용을 진행 하기 전에 지침에 대 한 Windows Server 2019 릴리스 정보를 읽습니다.

- 누적 업데이트를 설치 하려면 Windows Update를 사용 하 여 앱 호환성 FOD를 추가할 때 Server Core의 콘솔 환경을 사용 하 여 깜박임 발생 하는 것이 가능 합니다.  2018 년 12 월을 사용 하 여이 문제를 해결 하는 업데이트 합니다.  자세한 정보 및 해결 단계를 참조 하세요. [4481610 기술 자료 문서: Windows Server 2019 Server Core에서 Server Core 앱 호환성 FOD를 설치한 후 화면이 깜박인다](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core)합니다.

- 앱 호환성 FOD 및 서버를 재부팅을 설치한 후 콘솔 창 프레임 색상 명령을 다른 파란색 음영으로 변경 됩니다.

- 또한 Internet Explorer 11 선택적 패키지를 설치, 두 번 클릭 하 여 로컬로.htm 파일을 저장 하려는 경우 지원 되지 않습니다. 그러나 수 있습니다 **마우스 오른쪽 단추로 클릭** 선택한 **IE를 사용 하 여 엽니다**, 또는 Internet Explorer에서 직접 열 수 있습니다 **파일** -> **열기**.

- 향상을 위해 앱 호환성 FOD를 사용 하 여 Server Core의 응용 프로그램 호환성, IIS 관리 콘솔에 Server Core에 선택적 구성 요소로 추가 되었습니다.  그러나 먼저 IIS 관리 콘솔을 사용 하는 앱 호환성 FOD를 추가 하는 데 반드시 필요한 것입니다. IIS 관리 콘솔 앱 호환성 FOD 추가 하 여 Server Core에 사용할 수만 있는 Microsoft Management Console (mmc.exe)에 의존 합니다.  Powershell을 사용 하 여 [ **Install-windowsfeature** ](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) IIS 관리 콘솔을 추가 합니다.

- 으로 일반 지침을 서버에 앱 설치 핵심 (유무와 관계 없이 이러한 선택적 패키지) 해당 하는 경우 지점 자동 설치 옵션 및 지침을 사용 하는 데 필요한 경우가 있습니다. 
    
  - 예를 들어 SQL Server 2016 및 SQL Server 2017에 대 한 SQL Server Management Studio Server Core에 설치할 수 있습니다 및 앱 호환성 FOD 존재 하는 경우에 완벽 하 게 작동 합니다.  하세요 [명령 프롬프트에서 SQL Server 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017)합니다.
  - SQL Server Management Studio 원하지 않는 경우 다음이 아닌 경우 Server Core 앱 호환성 FOD를 설치 하는 데 필요한  하세요 [Server Core에 SQL Server 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017)합니다.

## <a name="a-idadd-capabilities-adding-capabilities-and-optional-packages-to-an-offline-wim-server-core-image"></a><a id="add-capabilities"> 추가 기능 및 선택적 패키지를 오프 라인 WIM Server Core 이미지

1. Windows Server 및 Server FOD ISO 이미지 파일을 Windows 컴퓨터에서 로컬 폴더로 다운로드 합니다.

   - 볼륨 라이선스가 있는 경우에서 Windows Server 및 Server FOD ISO 이미지 파일을 다운로드할 수 있습니다 합니다 [볼륨 라이선스 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx)합니다.
   - 장기 서비스 채널에서 릴리스를 서버 FOD ISO 이미지 파일을 사용할 수 있는 이기도 합니다 [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server) 또는 [Visual Studio 포털](https://visualstudio.microsoft.com) 구독자에 대 한 합니다.

2. 관리자 권한으로 PowerShell 세션을 열고 드라이브로 이미지 파일을 탑재 하려면 다음 명령을 사용 합니다.

   ```PowerShell
   Mount-DiskImage -ImagePath Path_To_ServerFOD_ISO
   Mount-DiskImage -ImagePath Path_To_Windows_Server_ISO
   ```

3. 복사는 Windows Server ISO 파일을 로컬 폴더의 콘텐츠 (예를 들어 *C:\SetupFiles\WindowsServer*).

4. 다음 명령을 사용 하 여 Install.wim 파일 내에서 수정 하려는 이미지 이름을 가져옵니다.<br>
사용 된 `$install_wim_path` ISO 파일의 \Sources 폴더 내에 있는 Install.wim 파일에 경로 입력 하는 변수입니다.

   ```PowerShell
   $install_wim_path = "C:\SetupFiles\WindowsServer\sources\install.wim"

   Get-WindowsImage -ImagePath $install_wim_path
   ```

5. 다음을 사용 하 여 새 폴더에 있는 Install.wim 파일을 탑재 명령을 사용 하 여 직접 샘플 변수 값을 대체 하 고 다시 사용 된 `$install_wim_path` 이전 명령에서 변수입니다.<br>

   - `$image_name` -탑재 하려는 이미지의 이름을 입력 합니다.
   - `$mount_folder variable` -Install.wim 파일의 내용에 액세스 하는 경우 사용할 폴더를 지정 합니다.

   ```PowerShell
   $image_name = "Windows Server Datacenter"
   $mount_folder = "c:\test\offline"

   Mount-WindowsImage -ImagePath $install_wim_path -Name $image_name -path $mount_folder
   ```

6. 다음 명령을 사용 하 여 사용자 고유의 샘플 변수 값 대체를 사용 하 여 탑재 된 Install.wim 이미지에 기능 및 패키지를 추가 합니다.<br>

   - `$capability_name` -이름을 지정 합니다 (이 예제의 경우 AppCompatibility 기능)에 설치 하는 기능입니다.
   - `$package_path` -(이 예제의 경우 Internet Explorer)에 설치 패키지의 경로를 지정 합니다.
   - `$fod_drive` -탑재 된 Server FOD 이미지의 드라이브 문자를 지정 합니다.

   ```PowerShell
   $capability_name = "ServerCore.AppCompatibility~~~~0.0.1.0"
   $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"
   $fod_drive = "d:\"

   Add-WindowsCapability -Path $mount_folder -Name $capability_name -Source $fod_drive -LimitAccess
   Add-WindowsPackage -Path $mount_folder -PackagePath $package_path
   ```

7. 분리 및 사용 하는 다음 명령을 사용 하 여 Install.wim 파일에 변경 내용을 커밋하는 `$mount_folder` 이전 명령에서 변수:

   ```PowerShell
   Dismount-WindowsImage -Path $mount_folder -Save
   ```

이제 Windows Server 설치 파일에 대 한 사용자가 만든 폴더에서 setup.exe를 실행 하 여 서버를 업그레이드할 수 있습니다 (이 예제에서: *C:\SetupFiles\WindowsServer*). 이 폴더는 이제 추가 기능 및 포함 된 선택적 패키지를 사용 하 여 Windows Server 설치 파일을 포함 합니다.