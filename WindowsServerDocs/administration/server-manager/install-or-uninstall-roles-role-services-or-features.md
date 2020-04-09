---
title: 역할, 역할 서비스 또는 기능 설치 또는 제거
description: 서버 관리자
ms.prod: windows-server
ms.technology: manage-server-manager
ms.topic: article
ms.assetid: 04f16d84-45c2-4771-84c1-1cc973d0ee02
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c270fbdacf5359af4e3150d61693470207f566b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851526"
---
# <a name="install-or-uninstall-roles-role-services-or-features"></a>역할, 역할 서비스 또는 기능 설치 또는 제거

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server의 서버 관리자 콘솔 및 Windows PowerShell cmdlet에 대 한 서버 관리자는 로컬 또는 원격 서버 또는 오프 라인 가상 하드 디스크 (Vhd)로 역할 및 기능 설치를 허용 합니다. 단일 원격 서버 또는 단일 역할 및 기능 추가 마법사 또는 Windows PowerShell 세션에서 여러 역할 및 기능을 설치할 수 있습니다.  
  
> [!IMPORTANT]  
> Windows Server 운영 체제의 최신 릴리스를 관리 하려면 서버 관리자를 사용할 수 없습니다. Windows server 2016를 실행 하는 서버에 역할, 역할 서비스 및 기능을 설치 하는 데 Windows Server 2012 R2 또는 Windows 8.1에서 실행 되는 서버 관리자를 사용할 수 없습니다.  
  
설치 또는 역할, 역할 서비스 및 기능을 제거 하려면 관리자 권한으로 서버에 로그온 해야 합니다. 대상 서버에서 관리자 권한이 없는 계정으로 로컬 컴퓨터에 로그온한 경우 **서버** 타일에서 대상 서버를 마우스 오른쪽 단추로 클릭한 후, **다음으로 관리**를 클릭하여 관리자 권한이 있는 계정을 적용합니다. 오프라인 VHD를 탑재하려는 서버는 서버 관리자에 추가되어 있어야 하며, 사용자는 해당 서버에 대한 관리자 권한이 있어야 합니다.  
  
역할, 역할 서비스 및 기능을 기능에 대 한 자세한 내용은 참조 [역할, 역할 서비스 및 기능](https://go.microsoft.com/fwlink/p/?LinkId=239558)합니다.  
  
이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [역할 및 기능 추가 마법사를 사용 하 여 역할, 역할 서비스 및 기능 설치](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard)  
  
-   [Windows PowerShell cmdlet을 사용하여 역할, 역할 서비스 및 기능 설치](#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets)  
  
-   [역할 및 기능 제거 마법사를 사용 하 여 역할, 역할 서비스 및 기능 제거](#remove-roles-role-services-and-features-by-using-the-remove-roles-and-features-wizard)  
  
-   [Windows PowerShell cmdlet을 사용하여 역할, 역할 서비스 및 기능 제거](#remove-roles-role-services-and-features-by-using-windows-powershell-cmdlets)  
  
-   [Windows PowerShell 스크립트를 실행하여 여러 서버에 역할 및 기능 설치](#install-roles-and-features-on-multiple-servers-by-running-a-windows-powershell-script)  
  
-   [필요 시 .NET Framework 3.5 및 기타 기능 설치](#install-net-framework-35-and-other-features-on-demand)  
  
## <a name="install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard"></a>역할 및 기능 추가 마법사를 사용 하 여 역할, 역할 서비스 및 기능 설치  
역할 및 기능 추가 마법사의 단일 세션에서 로컬 서버, 서버 관리자에 추가 된 원격 서버 또는 오프 라인 VHD에서 역할, 역할 서비스 및 기능을 설치할 수 있습니다. 서버를 관리 하려면 서버 관리자를 추가 하는 방법에 대 한 자세한 내용은 참조 [서버 관리자에 서버 추가](add-servers-to-server-manager.md)합니다.  
  
> [!NOTE]  
> Windows Server 2016 또는 Windows 10에서 서버 관리자를 실행 하는 경우 역할 및 기능 추가 마법사를 사용 하 여 Windows Server 2016를 실행 하는 서버 및 오프 라인 Vhd에만 역할 및 기능을 설치할 수 있습니다.  
  
#### <a name="to-install-roles-and-features-by-using-the-add-roles-and-features-wizard"></a>역할 및 기능 추가 마법사를 사용 하 여 역할 및 기능을 설치 하려면  
  
1.  서버 관리자가 이미 열려 있으면 다음 단계로 이동합니다. 서버 관리자가 아직 열려 있지 않으면 다음 중 하나를 수행하여 엽니다.  
  
    -   Windows 바탕 화면에서 Windows 작업 표시줄의 **서버 관리자**를 클릭하여 서버 관리자를 시작합니다.  
  
    -   Windows **시작** 화면에서 **서버 관리자** 타일을 클릭 합니다.  
  
2.  **관리** 메뉴에서 **역할 및 기능 추가**를 클릭 합니다.  
  
3.  **시작하기 전** 페이지에서 설치하려는 역할 및 기능의 대상 서버 및 네트워크 환경이 준비되어 있는지 확인합니다. **다음**을 클릭합니다.  
  
4.  **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 선택하여 역할 또는 기능의 모든 부분을 단일 서버에 설치하거나, **원격 데스크톱 서비스 설치**를 선택하여 원격 데스크톱 서비스용 가상 컴퓨터 기반 데스크톱 인프라 또는 세션 기반 데스크톱 인프라를 설치합니다. **원격 데스크톱 서비스 설치** 옵션에서는 관리자가 필요에 따라 여러 서버에 원격 데스크톱 서비스 역할의 논리적 부분을 분산시킵니다. **다음**을 클릭합니다.  
  
5.  **대상 서버 선택** 페이지에서 서버 풀의 서버를 선택하거나 오프라인 VHD를 선택합니다. 오프라인 VHD를 대상 서버로 선택하려면 먼저 VHD가 탑재될 서버를 선택한 다음 VHD 파일을 선택합니다. 서버 풀에 서버를 추가 하는 방법에 대 한 정보를 참조 하십시오. [서버 관리자에 서버 추가](add-servers-to-server-manager.md)합니다. 대상 서버를 선택하고 나면 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    > 오프라인 VHD에 역할 및 기능을 설치하려면 대상 VHD가 다음의 요구 사항을 충족해야 합니다.  
    >   
    > -   Vhd를 실행 하는 서버 관리자의 버전과 일치 하는 Windows Server의 릴리스를 실행 되어야 합니다. 역할 [및 기능 추가 마법사를 사용 하 여 역할, 역할 서비스 및 기능 설치](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard)의 시작 부분에 있는 참고를 참조 하세요.  
    > -   VHD에는 두 개 이상의 시스템 볼륨 또는 파티션이 포함될 수 없습니다.  
    > -   VHD 파일이 저장된 네트워크 공유 폴더에서 VHD를 탑재하도록 선택한 서버의 컴퓨터(또는 로컬 시스템) 계정에 다음의 액세스 권한을 부여해야 합니다. 사용자 전용 계정 액세스 권한으로는 충분하지 않습니다. 공유는 **읽기** 및 **쓰기** 권한을 **Everyone** 그룹에 부여하여 VHD에 액세스하도록 할 수 있지만 보안상의 이유로 권장되지 않습니다.  
    >   
    >     -   **파일 공유** 대화 상자에서 **읽기/쓰기** 권한에 액세스  
    >     -   **모든 권한** 에 대 한 액세스는 **보안** 탭, 파일 또는 폴더 **속성** 대화 상자입니다.  
  
6.  역할을 선택하고 역할에 대한 역할 서비스(해당되는 경우)를 선택한 후 **다음**을 클릭하여 기능을 선택합니다.  
  
    계속할 때 역할 및 기능 추가 마법사가 대상 서버에서 충돌을 발견 하 여 선택 된 역할이 나 기능을 설치 또는 정상 작업에서 확인할 수 없게 되는 경우 자동으로 알립니다. 또한 선택한 역할이나 기능에 필요한 역할, 역할 서비스 또는 기능을 추가하라는 메시지도 표시됩니다.  
  
    또한 원격 서버 관리 도구를 실행하는 Windows 클라이언트 기반 컴퓨터 또는 다른 서버에서 역할을 원격으로 관리하려는 경우 역할에 대한 관리 도구 및 스냅인을 대상 서버에 설치하지 않도록 선택할 수 있습니다. 기본적으로 역할 및 기능 추가 마법사에서 관리 도구를 설치 하도록 선택 합니다.  
  
7.  **설치 선택 확인** 페이지에서 역할, 기능 및 서버에 대해 선택한 내용을 살펴봅니다. 설치할 준비가 되면 **설치**를 클릭합니다.  
  
    또한 Windows PowerShell을 사용한 무인된 설치에 사용할 수 있는 XML 기반 구성 파일을 선택 항목을 내보낼 수 있습니다. 이 역할 및 기능 추가 마법사 세션에서 지정한 구성을 내보내려면 **구성 설정 내보내기**를 클릭 한 다음 XML 파일을 편리한 위치에 저장 합니다.  
  
    **설치 선택 확인** 페이지의 **대체 원본 경로 지정** 명령을 사용하면 선택한 서버에 역할 및 기능을 설치하는 데 필요한 파일의 대체 원본 경로를 지정할 수 있습니다. Windows Server 2012 및 이후 버전의 Windows Server에서 [주문형 기능](https://go.microsoft.com/fwlink/p/?LinkID=241573) 의 양을 줄일 수 있습니다. 디스크 공간 원격 으로만 관리 되는 서버에서 역할 및 기능 파일을 제거 하 여 운영 체제에서 사용 합니다. `Uninstall-WindowsFeature -remove` cmdlet을 사용하여 서버에서 역할 및 기능 파일을 제거한 경우, 필요한 역할과 기능 파일이 저장되어 있는 대체 원본 경로 또는 공유를 지정하여 나중에 역할 및 기능을 서버에 설치할 수 있습니다. 원본 경로 또는 파일 공유에서 **읽기** 권한을 **Everyone** 그룹 (보안상의 이유로 권장 되지 않음) 또는 대상 서버의 컴퓨터 계정 (*도메인*\\*SERverNAME*$)에 부여 해야 합니다. 사용자 계정 액세스 권한을 부여 하는 것 만으로는 충분 하지 않습니다. 주문형 기능에 대한 자세한 내용은 [Windows Server 설치 옵션](https://go.microsoft.com/fwlink/p/?LinkId=241573)을 참조하세요.  
  
    실행 중인 실제 서버에서 역할, 역할 서비스 및 기능을 설치할 때 WIM 파일을 대체 기능 파일 원본으로 지정할 수 있습니다. WIM 파일의 원본 경로는 접두사로 **WIM**을 사용하고 접미사로 기능 파일이 있는 인덱스를 사용하여 **WIM:e:\sources\install.wim:4** 형식이어야 합니다. 그러나 사용할 수 없습니다 WIM 파일을 원본으로 직접; 오프 라인 VHD에 역할, 역할 서비스 및 기능 설치 해야 하거나 오프 라인 VHD를 탑재 하 고 소스 파일의 탑재 경로 또는 WIM 파일의 내용의 복사본을 포함 하는 폴더를 가리켜야 합니다.  
  
8.  **설치를 클릭 하면**설치 진행률, 결과 및 메시지 (예: 경고, 오류 또는 설치한 역할이 나 기능에 필요한 설치 후 구성 단계)가 설치 **진행률 페이지에** 표시 됩니다. Windows server 2012 이상 버전의 Windows Server에서는 설치가 진행 되는 동안 역할 및 기능 추가 마법사를 닫고 서버 관리자 콘솔 상단의 **알림** 영역에서 설치 결과 나 기타 메시지를 확인할 수 있습니다. 클릭 된 **알림을** 설치 또는 서버 관리자에서 수행 되는 기타 작업에 대 한 자세한 내용을 보려면 플래그 아이콘입니다.  
  
## <a name="install-roles-role-services-and-features-by-using-windows-powershell-cmdlets"></a>Windows PowerShell cmdlet을 사용하여 역할, 역할 서비스 및 기능 설치  
GUI 기반 역할 및 기능 추가 마법사와 유사 하 게 작동 하는 Windows PowerShell 용 서버 관리자 배포 cmdlet 및 역할 및 기능 제거 마법사는 중요 한 차이점이 있습니다. Windows PowerShell에서는 역할 및 기능 추가 마법사와 달리 역할에 대 한 관리 도구 및 스냅인이 기본적으로 포함 되어 있지 않습니다. 관리 도구를 역할 설치의 일부로 포함하려면 cmdlet에 `IncludeManagementTools` 매개 변수를 추가합니다. 를 설치 하는 역할 및 기능 Windows Server 2012 또는 이후 버전의 Server Core 설치 옵션을 실행 하는 서버의 경우에 역할의 관리 도구 설치를 추가할 수 있지만 GUI 기반 관리 도구 및 스냅인과 Windows Server의 Server Core 설치 옵션을 실행 하는 서버에 설치할 수 없습니다. 명령줄만 Server Core 설치 옵션에서 Windows PowerShell 관리 도구를 설치할 수 있습니다.  
  
#### <a name="to-install-roles-and-features-by-using-the-install-windowsfeature-cmdlet"></a>Install-WindowsFeature cmdlet을 사용하여 역할 및 기능을 설치하려면  
  
1. 다음 중 하나를 수행하여 관리자 권한으로 Windows PowerShell 세션을 엽니다.  
  
   > [!NOTE]  
   > 역할 및 기능 설치 하는 원격 서버에는, 관리자 권한으로 Windows PowerShell을 실행할 필요가 없습니다.  
  
   -   Windows 바탕 화면의 작업 표시줄에서 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.  
  
   -   Windows **시작** 화면에서 Windows PowerShell에 대 한 타일을 마우스 오른쪽 단추로 클릭 한 다음 앱 바에서 클릭 **관리자 권한으로 실행**합니다.  
  
2. **Get-WindowsFeature**를 입력한 다음 **Enter** 키를 누르면 로컬 서버에서 사용 가능하고 설치된 역할 및 기능 목록을 볼 수 있습니다. 로컬 컴퓨터가 서버가 아닌 경우 또는 원격 서버에 대 한 정보가 필요한 경우 Windows Server 2016를 실행 하는 원격 컴퓨터의 이름을 나타내는 *computer_name* **>** <em>computer_name</em> **<** 를 실행 합니다. Cmdlet의 결과는 역할 및 4 단계에서 cmdlet에 추가 기능 명령 이름이 포함 됩니다.  
  
   > [!NOTE]  
   > Windows PowerShell 3.0 이상 버전의 Windows PowerShell에는 서버 관리자 cmdlet 모듈을 모듈의 일부인 cmdlet을 실행 하기 전에 Windows PowerShell 세션으로 가져올 필요가 없습니다 있습니다. 모듈의 일부인 cmdlet을 처음으로 실행하면 모듈을 자동으로 가져옵니다. 또한 Windows PowerShell cmdlet도 아니고 cmdlet 사용 되는 기능 이름은 대/소문자를 구분 합니다.  
  
3. **Get-help Install-add-windowsfeature**를 입력 한 다음 **enter** 키를 눌러 `Install-WindowsFeature` cmdlet에 대 한 구문 및 허용 된 매개 변수를 확인 합니다.  
  
4. 다음을 입력 하 고 **enter**키를 누릅니다. 여기서 *feature_name* 는 설치 하려는 역할이 나 기능의 명령 이름 (2 단계에서 가져옴)을 나타내고 *computer_name* 는 역할 및 기능을 설치할 원격 컴퓨터를 나타냅니다. *feature_name*의 값이 여러 개인 경우에는 쉼표로 구분합니다. 역할 또는 기능 설치에 필요한 경우 `Restart` 매개 변수가 대상 서버를 자동으로 다시 시작합니다.  
  
   ```  
   Install-WindowsFeature -Name <feature_name> -computerName <computer_name> -Restart  
   ```  
  
   역할 및 기능을 오프라인 VHD에서 설치하려면 `computerName` 매개 변수와 `VHD` 매개 변수를 모두 추가합니다. `computerName` 매개 변수를 추가하지 않으면 cmdlet은 VHD에 액세스하기 위해 로컬 컴퓨터가 탑재되는 것으로 간주합니다. `computerName` 매개 변수에는 VHD를 탑재할 서버의 이름이 포함되며, `VHD` 매개 변수에는 지정된 서버에서의 VHD 파일 경로가 포함됩니다.  
  
   > [!NOTE]  
   > 추가 해야는 `computerName` 실행 하는 경우 cmdlet은 컴퓨터에서 하는 매개 변수는 Windows 클라이언트 운영 체제를 실행 합니다.  
   >   
   > 오프라인 VHD에 역할 및 기능을 설치하려면 대상 VHD가 다음의 요구 사항을 충족해야 합니다.  
   >   
   > -   Vhd를 실행 하는 서버 관리자의 버전과 일치 하는 Windows Server의 릴리스를 실행 되어야 합니다. 역할 [및 기능 추가 마법사를 사용 하 여 역할, 역할 서비스 및 기능 설치](#install-roles-role-services-and-features-by-using-the-add-roles-and-features-wizard)의 시작 부분에 있는 참고를 참조 하세요.  
   > -   VHD에는 두 개 이상의 시스템 볼륨 또는 파티션이 포함될 수 없습니다.  
   > -   VHD 파일이 저장된 네트워크 공유 폴더에서 VHD를 탑재하도록 선택한 서버의 컴퓨터(또는 로컬 시스템) 계정에 다음의 액세스 권한을 부여해야 합니다. 사용자 전용 계정 액세스 권한으로는 충분하지 않습니다. 공유는 **읽기** 및 **쓰기** 권한을 **Everyone** 그룹에 부여하여 VHD에 액세스하도록 할 수 있지만 보안상의 이유로 권장되지 않습니다.  
   >   
   >     -   **파일 공유** 대화 상자에서 **읽기/쓰기** 권한에 액세스  
   >     -   **모든 권한** 에 대 한 액세스는 **보안** 탭, 파일 또는 폴더 **속성** 대화 상자입니다.  
  
   ```  
   Install-WindowsFeature -Name <feature_name> -VHD <path> -computerName <computer_name> -Restart  
   ```  
  
   **예:** 다음 cmdlet은 ContosoDC1 원격 서버에 active directory 도메인 서비스 역할 및 그룹 정책 관리 기능을 설치 합니다. `IncludeManagementTools` 매개 변수를 사용하여 관리 도구와 스냅인을 추가하며 설치 시에 서버를 다시 시작해야 할 경우 대상 서버가 자동으로 다시 시작됩니다.  
  
   ```  
   Install-WindowsFeature -Name AD-Domain-Services,GPMC -computerName ContosoDC1 -IncludeManagementTools -Restart  
   ```  
  
5. 설치가 완료 되 면 열어 설치를 확인는 **모든 서버** 서버 관리자에서 역할 및 기능을 설치 된 서버를 선택 하 고 보는 페이지는 **역할 및 기능** 선택한 서버에 대 한 페이지에 바둑판식으로 배열입니다. 선택한 서버를 대상으로 하는 `Get-WindowsFeature` cmdlet (<*computer_name*>)을 실행 하 여 서버에 설치 된 역할 및 기능 목록을 볼 수도 있습니다.  
  
## <a name="remove-roles-role-services-and-features-by-using-the-remove-roles-and-features-wizard"></a>역할 및 기능 제거 마법사를 사용 하 여 역할, 역할 서비스 및 기능 제거  
역할, 역할 서비스 및 기능을 제거 하려면 관리자 권한으로 서버에 로그온 해야 합니다. 제거 대상 서버에 대해 관리자 권한이 없는 계정을 사용하여 로컬 컴퓨터에 로그온했으면 **서버** 타일에서 대상 서버를 마우스 오른쪽 단추로 클릭한 후 **다음으로 관리**를 클릭하여 관리자 권한을 가진 계정을 제공합니다. 오프라인 VHD를 탑재하려는 서버는 서버 관리자에 추가되어 있어야 하며, 사용자는 해당 서버에 대한 관리자 권한이 있어야 합니다.  
  
#### <a name="to-remove-roles-and-features-by-using-the-remove-roles-and-features-wizard"></a>역할 및 기능 제거 마법사를 사용 하 여 역할 및 기능을 제거 하려면  
  
1.  서버 관리자가 이미 열려 있으면 다음 단계로 이동합니다. 서버 관리자가 아직 열려 있지 않으면 다음 중 하나를 수행하여 엽니다.  
  
    -   Windows 바탕 화면에서 Windows 작업 표시줄의 **서버 관리자**를 클릭하여 서버 관리자를 시작합니다.  
  
    -   Windows **시작** 화면에서 **서버 관리자** 타일을 클릭합니다.  
  
2.  **관리** 메뉴에서 **역할 및 기능 제거**를 클릭합니다.  
  
3.  **시작하기 전** 페이지에서 역할 또는 기능을 서버에서 제거할 준비가 되었는지 확인합니다. **다음**을 클릭합니다.  
  
4.  **대상 서버 선택** 페이지에서 서버 풀의 서버를 선택 하거나 오프 라인 VHD를 선택 합니다. 오프라인 VHD를 선택하려면 먼저 VHD가 탑재될 서버를 선택한 다음 VHD 파일을 선택합니다.  
  
    > [!NOTE]  
    > VHD 파일이 저장된 네트워크 공유 폴더에서 VHD를 탑재하도록 선택한 서버의 컴퓨터(또는 로컬 시스템) 계정에 다음의 액세스 권한을 부여해야 합니다. 사용자 전용 계정 액세스 권한으로는 충분하지 않습니다. 공유는 **읽기** 및 **쓰기** 권한을 **Everyone** 그룹에 부여하여 VHD에 액세스하도록 할 수 있지만 보안상의 이유로 권장되지 않습니다.  
    >   
    > -   **파일 공유** 대화 상자에서 **읽기/쓰기** 권한에 액세스  
    > -   **보안** 탭, 파일 또는 폴더 **속성** 대화 상자에서 **모든 권한** 에 액세스  
  
    서버를 서버 풀에 추가 하는 방법에 대 한 자세한 내용은 [서버 관리자에 서버 추가](add-servers-to-server-manager.md)를 참조 하세요. 대상 서버를 선택하고 나면 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    > 역할 및 기능 제거 마법사를 사용 하 여 사용 중인 서버 관리자 버전을 지 원하는 Windows Server의 동일한 릴리스를 실행 하는 서버에서 역할 및 기능을 제거할 수 있습니다. Windows server 2012 R2, Windows Server 2012 또는 Windows 8에서 서버 관리자를 실행 하는 경우 Windows Server 2016를 실행 하는 서버에서 역할, 역할 서비스 또는 기능을 제거할 수 없습니다. 역할 및 기능 제거 마법사를 사용 하 여 Windows Server 2008 또는 Windows Server 2008 r 2를 실행 하는 서버에서 역할 및 기능을 제거할 수 없습니다.  
  
5.  역할을 선택하고 역할에 대한 역할 서비스(해당되는 경우)를 선택한 후 **다음**을 클릭하여 기능을 선택합니다.  
  
    계속할 때 역할 및 기능 제거 마법사는 제거 하려는 역할이 나 기능이 없으면 실행할 수 없는 역할, 역할 서비스 또는 기능을 제거 하 라는 메시지를 자동으로 표시 합니다.  
  
    또한 대상 서버에서 역할에 대 한 관리 도구 및 스냅인을 제거 하도록 선택할 수 있습니다. 기본적으로 역할 및 기능 제거 마법사에서 관리 도구를 선택 하 여 제거 합니다. 선택한 서버를 사용하여 다른 원격 서버의 역할을 관리할 계획이라면 관리 도구와 스냅인을 그대로 둘 수 있습니다.  
  
6.  **제거 선택 확인** 페이지에서 역할, 기능 및 서버에 대해 선택한 내용을 살펴봅니다. 역할이 나 기능을 제거할 준비가 되었으면 **제거**를 클릭 합니다.  
  
7.  **제거**를 클릭 하 고 나면 제거 진행률, 결과 및 메시지 (예: 경고, 오류 또는 대상 서버 다시 시작과 같은 제거 후 구성 단계)가 제거 **진행률** 페이지에 표시 됩니다. Windows server 2012 이상 버전의 Windows Server에서는 제거가 진행 중일 때 역할 및 기능 제거 마법사를 닫고 서버 관리자 콘솔 상단의 **알림** 영역에서 제거 결과 나 기타 메시지를 확인할 수 있습니다. 클릭 된 **알림을** 제거 또는 서버 관리자에서 수행 되는 기타 작업에 대 한 자세한 내용을 보려면 플래그 합니다.  
  
## <a name="remove-roles-role-services-and-features-by-using-windows-powershell-cmdlets"></a>Windows PowerShell cmdlet을 사용하여 역할, 역할 서비스 및 기능 제거  
Windows PowerShell 용 서버 관리자 배포 cmdlet은 GUI 기반 역할 및 기능 제거 마법사와 유사 하 게 작동 하지만 중요 한 차이점이 있습니다. Windows PowerShell에서는 역할 및 기능 제거 마법사와 달리 역할에 대 한 관리 도구 및 스냅인이 기본적으로 제거 되지 않습니다. 관리 도구를 역할 제거의 일부로 제거하려면 cmdlet에 `IncludeManagementTools` 매개 변수를 추가합니다. 역할 및 Windows Server 2012의 Server Core 설치 옵션 또는 이후 버전의 Windows Server,이 매개 변수 제거 명령줄 및 지정된 된 역할에 대 한 Windows PowerShell 관리 도구를 실행 하는 서버에서 기능 및 기능 제거 하는 경우입니다.  
  
#### <a name="to-remove-roles-and-features-by-using-the-uninstall-windowsfeature-cmdlet"></a>Uninstall-WindowsFeature cmdlet을 사용하여 역할 및 기능을 제거하려면  
  
1. 다음 중 하나를 수행하여 관리자 권한으로 Windows PowerShell 세션을 엽니다.  
  
   > [!NOTE]  
   > 역할 및 기능을 제거 하면 원격 서버에서 관리자 권한으로 Windows PowerShell을 실행할 필요가 없습니다.  
  
   -   Windows 바탕 화면의 작업 표시줄에서 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.  
  
   -   Windows **시작** 화면에서 windows PowerShell 타일을 마우스 오른쪽 단추로 클릭 한 다음 앱 바에서 **관리자 권한으로 실행**을 클릭 합니다.  
  
2. **Get-WindowsFeature**를 입력한 다음 **Enter** 키를 누르면 로컬 서버에서 사용 가능하고 설치된 역할 및 기능 목록을 볼 수 있습니다. 로컬 컴퓨터가 서버가 아닌 경우 또는 원격 서버에 대 한 정보가 필요한 경우 Windows Server 2016를 실행 하는 원격 컴퓨터의 이름을 나타내는 *computer_name* **>** <em>computer_name</em> **<** 를 실행 합니다. Cmdlet의 결과는 역할 및 4 단계에서 cmdlet에 추가 기능 명령 이름이 포함 됩니다.  
  
   > [!NOTE]  
   > Windows PowerShell 3.0 이상 버전의 Windows PowerShell에는 서버 관리자 cmdlet 모듈을 모듈의 일부인 cmdlet을 실행 하기 전에 Windows PowerShell 세션으로 가져올 필요가 없습니다 있습니다. 모듈의 일부인 cmdlet을 처음으로 실행하면 모듈을 자동으로 가져옵니다. 또한 Windows PowerShell cmdlet도 아니고 cmdlet 사용 되는 기능 이름은 대/소문자를 구분 합니다.  
  
3. **Get-help Uninstall**을 입력 하 고 **enter** 키를 눌러 `Uninstall-WindowsFeature` cmdlet에 대 한 구문 및 허용 된 매개 변수를 확인 합니다.  
  
4. 다음을 입력한 후 **Enter** 키를 누릅니다. 여기서 *feature_name*은 제거하려는 역할이나 기능의 명령 이름(2단계에서 확보)을 나타내며, *computer_name*은 역할이나 기능을 제거하려는 원격 컴퓨터를 나타냅니다. *feature_name*의 값이 여러 개인 경우에는 쉼표로 구분합니다. 역할 또는 기능 제거에서 필요한 경우 `Restart` 매개 변수가 대상 서버를 자동으로 다시 시작합니다.  
  
   ```  
   Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -Restart  
   ```  
  
   역할 및 기능을 오프라인 VHD에서 제거하려면 `computerName` 매개 변수와 `VHD` 매개 변수를 모두 추가합니다. `computerName` 매개 변수를 추가하지 않으면 cmdlet은 VHD에 액세스하기 위해 로컬 컴퓨터가 탑재되는 것으로 간주합니다. `computerName` 매개 변수에는 VHD를 탑재할 서버의 이름이 포함되며, `VHD` 매개 변수에는 지정된 서버에서의 VHD 파일 경로가 포함됩니다.  
  
   > [!NOTE]  
   > 추가 해야는 `computerName` 실행 하는 경우 cmdlet은 컴퓨터에서 하는 매개 변수는 Windows 클라이언트 운영 체제를 실행 합니다.  
   >   
   > VHD 파일이 저장된 네트워크 공유 폴더에서 VHD를 탑재하도록 선택한 서버의 컴퓨터(또는 로컬 시스템) 계정에 다음의 액세스 권한을 부여해야 합니다. 사용자 전용 계정 액세스 권한으로는 충분하지 않습니다. 공유는 **읽기** 및 **쓰기** 권한을 **Everyone** 그룹에 부여하여 VHD에 액세스하도록 할 수 있지만 보안상의 이유로 권장되지 않습니다.  
   >   
   > -   **파일 공유** 대화 상자에서 **읽기/쓰기** 권한에 액세스  
   > -   **모든 권한** 에 대 한 액세스는 **보안** 탭, 파일 또는 폴더 **속성** 대화 상자입니다.  
  
   ```  
   Uninstall-WindowsFeature -Name <feature_name> -VHD <path> -computerName <computer_name> -Restart  
   ```  
  
   **예:** 다음 cmdlet은 원격 서버 ContosoDC1에서 active directory 도메인 서비스 역할 및 그룹 정책 관리 기능을 제거 합니다. 관리 도구와 스냅인도 제거되며, 제거 시 서버를 다시 시작해야 할 경우 대상 서버가 자동으로 다시 시작됩니다.  
  
   ```  
   Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -computerName ContosoDC1 -IncludeManagementTools -Restart  
   ```  
  
5. 제거가 완료 되 면 확인을 열어서 역할 및 기능이 제거 됩니다는 **모든 서버** 서버 관리자에서 제거한 역할 및 기능을 서버를 선택 하 고 보는 페이지는 **역할 및 기능** 선택한 서버에 대 한 페이지에 바둑판식으로 배열입니다. 선택한 서버를 대상으로 하는 `Get-WindowsFeature` cmdlet (<*computer_name*>)을 실행 하 여 서버에 설치 된 역할 및 기능 목록을 볼 수도 있습니다.  
  
## <a name="install-roles-and-features-on-multiple-servers-by-running-a-windows-powershell-script"></a>Windows PowerShell 스크립트를 실행하여 여러 서버에 역할 및 기능 설치  
역할 및 기능 추가 마법사를 사용 하 여 단일 마법사 세션에서 두 개 이상의 대상 서버에 역할, 역할 서비스 및 기능을 설치할 수는 없지만, Windows PowerShell 스크립트를 사용 하 여 서버 관리자를 사용 하 여 관리 하는 여러 대상 서버에 역할, 역할 서비스 및 기능을 설치할 수 있습니다. 이 프로세스가 호출 될 때 일괄 배포를 수행 하는 데 사용 하는 스크립트는 역할 및 기능 추가 마법사를 사용 하 여 쉽게 만들 수 있는 XML 구성 파일을 가리키고 마법사를 통해 역할 및 기능 추가 마법사의 **설치 선택 확인** 페이지로 이동한 후 **구성 설정 내보내기** 를 클릭 하 여 쉽게 만들 수 있습니다.  
  
> [!IMPORTANT]  
> 스크립트에 지정 된 모든 대상 서버는 로컬 컴퓨터에서 실행 하는 서버 관리자의 버전과 일치 하는 Windows Server의 릴리스를 실행 되어야 합니다. 예를 들어, Windows 10에서 서버 관리자를 실행 하는 경우 Windows Server 2016를 실행 하는 서버에서 역할, 역할 서비스 및 기능 설치할 수 있습니다. GUI 기반 관리 도구 설치에 추가 되 면 설치 프로세스 전체 설치 옵션 (라고도 함: 실행 중인 서버 그래픽 셸, 전체 GUI 포함 서버)를 Windows Server의 Server Core 설치 옵션을 실행 하는 대상 서버를 자동으로 변환 합니다.  
>   
> 이 섹션에 제공 된 스크립트를 사용 하 여 일괄 배포를 수행 하는 방법의 한 예로 `Install-WindowsFeature` cmdlet 및 Windows PowerShell 스크립트입니다. 여러 서버에 일괄 배포를 수행할 수 있는 다른 스크립트와 방법도 있습니다. 역할 및 기능 배포 시 다른 스크립트를 제공하거나 검색하려면 [스크립트 센터 리포지토리](https://gallery.technet.microsoft.com/ScriptCenter)를 검색하세요.  
  
#### <a name="to-install-roles-and-features-on-multiple-servers"></a>여러 서버에 역할 및 기능을 설치하려면  
  
1.  아직 수행 하는 경우에 역할, 역할 서비스를 포함 하는 XML 구성 파일 및 여러 서버에 설치 하려는 기능을 만듭니다. 역할 및 기능 추가 마법사를 실행 하 고 원하는 역할, 역할 서비스 및 기능을 선택한 다음 마법사를 통해 **설치 선택 확인** 페이지로 이동한 후 **구성 설정 내보내기** 를 클릭 하 여이 구성 파일을 만들 수 있습니다. 구성 파일을 원하는 위치에 저장합니다. 마법사를 구성 파일을 만드는 데에만 실행할 경우에는 **설치**를 클릭하거나 마법사를 완료할 필요가 없습니다.  
  
2.  다음 중 하나를 수행하여 관리자 권한으로 Windows PowerShell 세션을 엽니다.  
  
    -   Windows 바탕 화면의 작업 표시줄에서 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.  
  
    -   Windows **시작** 화면에서 windows PowerShell 타일을 마우스 오른쪽 단추로 클릭 한 다음 앱 바에서 **관리자 권한으로 실행**을 클릭 합니다.  
  
3.  복사한 다음 스크립트는 Windows PowerShell 세션에 붙여 넣습니다.  
  
    ```  
    function Invoke-WindowsFeatureBatchDeployment {  
        param (  
            [parameter(mandatory)]  
            [string[]] $computerNames,  
            [parameter(mandatory)]  
            [string] $ConfigurationFilepath  
        )  
  
        # Deploy the features on multiple computers simultaneously.  
        $jobs = @()  
        foreach($computerName in $computerNames) {  
            $jobs += start-Job -Command {  
                Install-WindowsFeature -ConfigurationFilepath $using:ConfigurationFilepath -computerName $using:computerName -Restart  
            }   
        }  
  
        Receive-Job -Job $jobs -Wait | select-Object Success, RestartNeeded, exitCode, FeatureResult  
    }  
    ```  
  
    선택한 역할 및 기능에서 필요할 경우 대상 서버가 자동으로 다시 시작됩니다.  
  
4.  다음을 수행하여 기능을 실행합니다.  
  
    1.  대상 컴퓨터의 이름을 저장할 변수를 쉼표로 구분하여 만듭니다. 다음 예에서 변수 `$ServerNames`에는 대상 서버 *Contoso_01* 및 *Contoso_02*의 이름이 저장됩니다. **Enter** 키를 누릅니다.  
  
        ```  
        # Sample Invocation  
        $ServerNames = 'Contoso_01','Contoso_02'  
        Invoke-WindowsFeatureBatchDeployment -computerNames $ServerNames -ConfigurationFilepath C:\Users\sampleuser\Desktop\DeploymentConfigTemplate.xml  
        ```  
  
    2.  기능을 실행하려면 다음과 같이 입력한 다음 **Enter** 키를 누릅니다. 여기에서 `$ServerNames`는 이전 단계에서 만든 변수의 일례로, *C:\Users\Sampleuser\Desktop\DeploymentConfigTemplate.xml*은 1단계에서 만든 구성 파일의 경로를 나타내는 예입니다.  
  
        **-WindowsFeatureBatchDeployment-computerNames $ServerNames-ConfigurationFilepath C:\Users\Sampleuser\Desktop\DeploymentConfigTemplate.xml**  
  
5.  설치가 완료 되 면 열어 설치를 확인는 **모든 서버** 서버 관리자에서 역할 및 기능을 설치 된 서버를 선택 하 고 보는 페이지는 **역할 및 기능** 선택한 서버에 대 한 페이지에 바둑판식으로 배열입니다. 특정 서버를 대상으로 하는 `Get-WindowsFeature` cmdlet (`Get-WindowsFeature -computerName` <*computer_name*>)을 실행 하 여 서버에 설치 된 역할 및 기능 목록을 볼 수도 있습니다.  
  
## <a name="install-net-framework-35-and-other-features-on-demand"></a>필요 시 .NET Framework 3.5 및 기타 기능 설치  
Windows Server 2012 및 Windows 8부터 .NET Framework 3.5 (.NET Framework 2.0 및 .NET Framework 3.0 포함)의 기능 파일을 로컬 컴퓨터에서 기본적으로 사용할 수 없습니다. 파일이 제거되었습니다. 주문형 기능 구성에서 제거된 기능의 파일과 .NET Framework 3.5의 기능 파일은 Windows 업데이트를 통해 제공됩니다. 기본적으로 기능 파일을 Windows Server 2012 또는 이후 릴리스를 실행 하는 대상 서버에서 사용할 수 없는 경우 설치 프로세스 검색 누락 된 파일에 대 한 Windows Update에 연결 하 여 합니다. 역할 및 기능 추가 마법사 GUI 또는 명령줄을 사용 하 여 설치 하는 경우 설치 중에 그룹 정책 설정을 구성 하거나 대체 원본 경로를 지정 하 여 기본 동작을 재정의할 수 있습니다.  
  
다음 중 하나를 수행하여 .NET Framework 3.5를 설치할 수 있습니다.  
  
-   [Install-WindowsFeature cmdlet을 실행하여 .NET Framework 3.5를 설치하려면](#to-install-net-framework-35-by-running-the-install-windowsfeature-cmdlet)을 참조하여 `Source` 매개 변수를 추가하고 .NET Framework 3.5 기능 파일을 가져올 원본을 지정합니다. `Source` 매개 변수를 추가하지 않은 경우 설치 프로세스는 먼저 그룹 정책 설정으로 지정된 기능 파일의 경로가 있는지 확인한 다음, 해당 경로를 찾을 수 없으면 Windows 업데이트를 사용하여 누락된 기능 파일을 검색합니다.  
  
-   역할 및 기능 추가 마법사의 **설치 옵션 확인** 페이지에서 대체 원본 파일 위치를 지정 하려면 [역할 및 기능 추가 마법사](#to-install-net-framework-35-by-using-the-add-roles-and-features-wizard) 를 사용 하 여 .NET Framework 3.5을 설치 합니다.  
  
-   [DISM을 사용해 .NET Framework 3.5를 설치하려면](#to-install-net-framework-35-by-using-dism)을 참조하여 기본적으로 Windows 업데이트에서 파일을 가져오거나 설치 미디어의 원본 경로를 지정하여 가져옵니다.  
  
로컬 컴퓨터에서 기능 파일을 찾을 수 없는 경우 .NET Framework 3.5 또는 기타 기능에 대해[그룹 정책에 기능 파일의 대체 원본 구성](#configure-alternate-sources-for-feature-files-in-group-policy) .  
  
> [!IMPORTANT]  
> 원격 원본에서 기능 파일을 설치할 경우 원본 경로 또는 파일 공유에서 **읽기** 권한을 **Everyone** 그룹(보안상의 이유로 권장되지 않음) 또는 대상 서버의 컴퓨터(로컬 시스템) 계정에 부여해야 합니다. 사용자 계정 액세스 권한은 충분하지 않습니다.  
>   
> 작업 그룹에 속한 서버에서는 외부 공유에 대한 **읽기** 권한이 작업 그룹 서버의 컴퓨터 계정에 있더라도 외부 파일 공유에 액세스할 수 없습니다. 작업 그룹 서버에 사용되는 대체 원본 위치에는 로컬 작업 그룹 서버에 저장된 설치 미디어, Windows 업데이트 및 VHD 또는 WIM 파일이 포함됩니다.  
>   
> 실행 중인 실제 서버에서 역할, 역할 서비스 및 기능을 설치할 때 WIM 파일을 대체 기능 파일 원본으로 지정할 수 있습니다. WIM 파일의 원본 경로는 접두사로 **WIM**을 사용하고 접미사로 기능 파일이 있는 인덱스를 사용하여 **WIM:e:\sources\install.wim:4** 형식이어야 합니다. 그러나 사용할 수 없습니다 WIM 파일을 원본으로 직접; 오프 라인 VHD에 역할, 역할 서비스 및 기능 설치 해야 하거나 오프 라인 VHD를 탑재 하 고 소스 파일의 탑재 경로 또는 WIM 파일의 내용의 복사본을 포함 하는 폴더를 가리켜야 합니다.  
  
### <a name="to-install-net-framework-35-by-running-the-install-windowsfeature-cmdlet"></a>Install-WindowsFeature cmdlet을 실행해 .NET Framework 3.5를 설치하려면  
  
1.  다음 중 하나를 수행하여 관리자 권한으로 Windows PowerShell 세션을 엽니다.  
  
    > [!NOTE]  
    > 원격 서버에서 역할 및 기능을 설치 하는 경우 관리자 권한으로 Windows PowerShell을 실행할 필요가 없습니다.  
  
    -   Windows 바탕 화면의 작업 표시줄에서 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.  
  
    -   Windows **시작** 화면에서 windows PowerShell 타일을 마우스 오른쪽 단추로 클릭 한 다음 앱 바에서 **관리자 권한으로 실행**을 클릭 합니다.  
  
    -   Windows Server 2012 R2 또는 Windows Server 2012의 Server Core 설치 옵션을 실행 하는 서버에서 **PowerShell** 을 명령 프롬프트에 입력 한 다음 **enter**키를 누릅니다.  
  
2.  다음 명령을 입력 하 고 **enter**키를 누릅니다. 다음 예에서 원본 파일은 D 드라이브의 설치 미디어 내 side-by-side 저장소(**SxS**)에 있습니다.  
  
    ```  
    Install-WindowsFeature NET-Framework-Core -Source D:\Sources\SxS  
    ```  
  
    이 명령에서 누락된 기능 파일의 원본으로 Windows 업데이트를 사용하려는 경우 또는 그룹 정책을 사용해 기본 원본이 이미 구성되어 있는 경우에는 다른 원본을 지정하고자 하지 않는 한 `Source` 매개 변수를 추가할 필요가 없습니다.  
  
### <a name="to-install-net-framework-35-by-using-the-add-roles-and-features-wizard"></a>역할 및 기능 추가 마법사를 사용 하 여 .NET Framework 3.5를 설치 하려면  
  
1. 서버 관리자의 **관리** 메뉴에서 **역할 및 기능 추가**를 클릭 합니다.  
  
2. Windows Server 2016를 실행 하는 대상 서버를 선택 합니다.  
  
3. 역할 및 기능 추가 마법사의 **기능 선택** 페이지에서 **.NET Framework 3.5**을 선택 합니다.  
  
4. 로컬 컴퓨터가 그룹 정책 설정에서 이 작업을 수행할 수 있도록 허용된 경우 설치 프로세스는 Windows 업데이트를 사용해 누락된 기능 파일을 가져옵니다. 다음 단계로 이동할 필요 없이 **설치**를 클릭합니다.  
  
   그룹 정책 설정에서이 작업을 허용 하지 않거나 .NET Framework 3.5 기능 파일에 다른 원본을 사용 하려는 경우 마법사의 **설치 선택 확인** 페이지에서 **대체 원본 경로 지정**을 클릭 합니다.  
  
5. 설치 미디어의 side-by-side 저장소(**SxS**라고 함) 또는 WIM 파일의 경로를 제공합니다. 다음 예에서 설치 미디어는 D 드라이브에 있습니다.  
  
   **D:\Sources\SxS\\**  
  
   WIM 파일을 지정하려면 다음 예에 나와 있는 바와 같이 **WIM:** 접두사를 추가하고 WIM 파일에서 사용할 이미지의 인덱스를 접미사로 추가합니다.  
  
   **WIM:\\\\** <em>server_name</em> **\share\install.wim: 3**  
  
6. **확인**을 클릭한 다음 **설치**를 클릭합니다.  
  
### <a name="to-install-net-framework-35-by-using-dism"></a>DISM을 사용해 .NET Framework 3.5를 설치하려면  
  
1.  다음 중 하나를 수행하여 관리자 권한으로 Windows PowerShell 세션을 엽니다.  
  
    > [!NOTE]  
    > 원격 서버에서 역할 및 기능을 설치 하는 경우 관리자 권한으로 Windows PowerShell을 실행할 필요가 없습니다.  
  
    -   Windows 바탕 화면의 작업 표시줄에서 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.  
  
    -   Windows **시작** 화면에서 Windows PowerShell 타일을 마우스 오른쪽 단추로 클릭 한 다음 앱 바에서 클릭 **관리자 권한으로 실행**합니다.  
  
    -   Server Core 설치 옵션을 실행 하는 서버에서 **PowerShell** 을 명령 프롬프트에 입력 한 다음 **enter**키를 누릅니다.  
  
2.  다음 DISM 명령 중 하나를 사용합니다.  
  
    -   컴퓨터에서 Windows 업데이트에 액세스할 수 있거나 기본 원본 파일 위치가 이미 그룹 정책에 구성 되어 있는 경우 다음 명령을 실행 합니다.  
  
        ```  
        DISM /online /Enable-Feature /Featurename:NetFx3 /All  
        ```  
  
    -   컴퓨터에 설치 미디어에 대 한 액세스 권한이 있는 경우 다음과 유사한 명령을 실행 합니다. 다음 예에서 운영 체제 설치 미디어는 D 드라이브에 있습니다. `LimitAccess` 매개 변수로 인해 이 명령은 Windows 업데이트나 WSUS를 실행하는 서버에 연결하지 못합니다.  
  
        ```  
        DISM /online /Enable-Feature /Featurename:NetFx3 /All /LimitAccess /Source:d:\sources\sxs  
        ```  
  
    > [!NOTE]  
    > DISM 명령은 대/소문자를 구분합니다.  
  
### <a name="configure-alternate-sources-for-feature-files-in-group-policy"></a>그룹 정책에 기능 파일의 대체 원본 구성  
이 섹션에 설명된 그룹 정책 설정에서는 .NET Framework 3.5 파일 및 주문형 기능 구성의 일부로 제거된 기타 기능 파일에 대해 위임된 원본 위치를 지정합니다. **선택적 구성 요소 설치 및 구성 요소 복구를 위한 설정 지정** 정책 설정은 그룹 정책 관리 콘솔 또는 로컬 그룹 정책 편집기의 **컴퓨터 구성 \ 템플릿 \ 시스템** 폴더에 있습니다.  
  
> [!NOTE]  
> 로컬 컴퓨터의 그룹 정책 설정을 변경하려면 Administrators 그룹의 구성원이어야 합니다. 관리하려는 컴퓨터의 그룹 정책 설정이 도메인 수준에서 제어되는 경우 Domain Administrators 그룹의 구성원이어야 그룹 정책 설정을 변경할 수 있습니다.  
  
##### <a name="to-configure-a-default-alternate-source-path-in-group-policy"></a>그룹 정책에 기본 대체 원본 경로를 구성하려면  
  
1. 로컬 그룹 정책 편집기나 그룹 정책 관리 콘솔에서 다음 정책 설정을 엽니다.  
  
   **선택적 구성 요소 설치 및 구성 요소 복구를 위한 컴퓨터 구성 \ 시스템 \ 선택적 설정**  
  
2. 아직 설정 하지 않은 경우 정책 설정을 사용 하도록 설정 하려면 **사용** 을 설정 합니다.  
  
3. **옵션** 영역의 **대체 원본 파일 경로** 텍스트 상자에 공유 폴더 또는 WIM 파일의 정규화된 경로를 지정합니다. WIM 파일을 대체 원본 파일 위치로 지정하려면 **WIM:** 접두사를 경로에 추가하고 WIM 파일에서 사용할 이미지의 인덱스를 접미사로 추가합니다. 다음 예에 나온 값을 지정할 수 있습니다.  
  
   - 공유 폴더 경로: **\\\\** <em>server_name</em> **\share\\** <em>folder_name</em>  
  
   - WIM 파일의 경로 이며, **3** 은 기능 파일이 있는 이미지의 인덱스를 나타냅니다. **wim:\\\\** <em>server_name</em> **\share\install.wim: 3**  
  
4. 이 정책 설정에 따라 제어 되는 컴퓨터가 Windows 업데이트에서 누락 된 기능 파일을 검색 하지 않도록 하려면 **Windows 업데이트에서 페이로드를 다운로드 하지 않음**을 선택 합니다.  
  
5. 이 정책 설정에 따라 제어되는 컴퓨터는 일반적으로 WSUS를 통해 업데이트를 받습니다. 하지만 누락된 기능 파일을 WSUS가 아닌 Windows 업데이트를 통해 검색하려면 **WSUS(Windows Server Update Services) 대신 Windows 업데이트에 직접 연결하여 복구 콘텐츠를 다운로드**를 선택합니다.  
  
6. 이 정책 설정을 변경하면 **확인**을 클릭한 다음 그룹 정책 편집기를 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
[Windows Server 설치 옵션](https://go.microsoft.com/fwlink/p/?LinkId=241573)  
[Microsoft .NET Framework 3.5 배포 고려 사항](https://go.microsoft.com/fwlink/p/?LinkId=248869)  
[Windows 기능을 사용 하거나 사용 하지 않도록 설정 하는 방법](https://go.microsoft.com/fwlink/p/?LinkId=246552)  
  


