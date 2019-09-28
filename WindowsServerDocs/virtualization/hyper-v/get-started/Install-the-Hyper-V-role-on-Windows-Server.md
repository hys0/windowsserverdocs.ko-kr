---
title: Windows Server에 Hyper-v 역할 설치
description: 서버 관리자 또는 Windows PowerShell을 사용 하 여 Hyper-v를 설치 하기 위한 지침을 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8e871317-09d2-4314-a6ec-ced12b7aee89
author: KBDAzure
ms.author: kathydav
ms.date: 12/02/2016
ms.openlocfilehash: 2687a907852e2a81f03b147df1425cd01b34fb76
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392805"
---
# <a name="install-the-hyper-v-role-on-windows-server"></a>Windows Server에 Hyper-v 역할 설치

>적용 대상: Windows Server 2016, Windows Server 2019
  
가상 컴퓨터를 만들고 실행 하려면 windows PowerShell에서 서버 관리자 또는 **add-windowsfeature** cmdlet을 사용 하 여 windows Server에 hyper-v 역할을 설치 합니다. Windows 10에 대 한 참조 [설치에 Hyper-v Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)합니다.

Hyper-v에 대 한 자세한 내용은 [Hyper-v 기술 개요](../Hyper-V-Technology-Overview.md)를 참조 하세요. Windows Server 2019를 사용해 보려면 평가판 복사를 다운로드 하 여 설치 하면 됩니다. [평가 센터](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)를 참조 하세요.

Windows Server를 설치 하거나 Hyper-v 역할을 추가 하기 전에 다음을 확인 하십시오.
- 컴퓨터 하드웨어가 호환 됩니다. 자세한 내용은 windows server의 [시스템 요구 사항](../../../get-started/System-Requirements.md) 및 [Windows server의 hyper-v에 대 한 시스템 요구](../System-requirements-for-Hyper-V-on-Windows.md)사항을 참조 하세요.
- Hyper-v에서 요구 하는 것과 동일한 프로세서 기능을 사용 하는 타사 가상화 앱은 사용할 계획이 없습니다. 예를 들면 VMWare Workstation 및 VirtualBox가 있습니다. 이러한 다른 앱을 제거 하지 않고 Hyper-v를 설치할 수 있습니다. 그러나 Hyper-v 하이퍼바이저를 실행 하는 동안 가상 컴퓨터를 관리 하는 데이를 사용 하려고 하면 가상 컴퓨터가 시작 되지 않거나 불안정 실행 될 수 있습니다. 이러한 앱 중 하나를 사용 해야 하는 경우 Hyper-v 하이퍼바이저를 해제 하는 방법에 대 한 자세한 내용 및 지침은 [가상화 응용 프로그램이 hyper-v, Device Guard 및 Credential guard와 함께 작동 하지](https://support.microsoft.com/help/3204980/virtualization-applications-do-not-work-together-with-hyper-v-device-g)않음을 참조 하세요.

Hyper-v 관리자와 같은 관리 도구만 설치 하려면 hyper-v [관리자를 사용 하 여 hyper-v 호스트 원격 관리](../Manage/Remotely-manage-Hyper-V-hosts.md)를 참조 하세요.
  
## <a name="install-hyper-v-by-using-server-manager"></a>서버 관리자를 사용 하 여 Hyper-v 설치  
  
1. **서버 관리자**의 **관리** 메뉴에서 **역할 및 기능 추가**를 클릭합니다.  
  
2. **시작하기 전** 페이지에서 설치하려는 역할 및 기능의 대상 서버 및 네트워크 환경이 준비되어 있는지 확인합니다. **다음**을 클릭합니다.  
  
3. **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 선택하고 **다음**을 클릭합니다.  
  
4. **대상 서버 선택** 페이지에서 서버 풀의 서버를 선택하고 **다음**을 클릭합니다.  
  
5. 에 **서버 역할 선택** 페이지에서 선택 **Hyper-v**합니다.  
  
6. 가상 컴퓨터 만들기 및 관리를 사용 하는 도구를 추가 하려면 클릭 **기능 추가**합니다. 기능 페이지에서 클릭 **다음**합니다.  
  
7. 에 **가상 스위치 만들기** 페이지 **가상 컴퓨터 마이그레이션** 페이지 및 **기본 저장소** 페이지 적절 한 옵션을 선택 합니다.  
  
8. **설치 선택 확인** 페이지에서 **필요한 경우 자동으로 대상 서버 다시 시작**을 선택하고 **설치**를 클릭합니다.  
  
9. 설치가 완료 되 면 Hyper-v가 올바르게 설치 되었는지 확인 합니다. 열기는 **모든 서버** 서버 관리자에서 페이지를 Hyper-v가 설치 되어 있는 서버를 선택 합니다. 확인은 **역할 및 기능** 선택한 서버에 대 한 페이지에 바둑판식으로 배열입니다.  
  
## <a name="install-hyper-v-by-using-the-install-windowsfeature-cmdlet"></a>Install Add-windowsfeature cmdlet을 사용 하 여 Hyper-v 설치  
  
1. Windows 데스크톱에서 시작 단추를 클릭하고 **Windows PowerShell** 이름의 일부를 입력합니다.  
  
2. Windows PowerShell을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다.  
  
3. 원격으로 연결 된 서버에서 Hyper-v를 설치 하려면 다음 명령을 실행 하 고 대체 `<computer_name>` 서버 이름을 사용 합니다.  
  
    ```powershell
    Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart  
    ```  
  
    서버에 로컬로 연결 하는 경우 명령을 입력 하지 않고 `-ComputerName <computer_name>`합니다.  
  
4. 서버를 다시 시작한 후에는 Hyper-v 역할이 설치 되어 있는 것을 확인 하 고 다음 명령을 실행 하 여 설치 된 다른 역할 및 기능을 확인할 수 있습니다.  
  
    ```powershell
    Get-WindowsFeature -ComputerName <computer_name>  
    ```  
  
    서버에 로컬로 연결 하는 경우 명령을 입력 하지 않고 `-ComputerName <computer_name>`합니다.  
  
> [!NOTE]  
> Windows Server 2016의 Server Core 설치 옵션을 실행 하는 서버에이 역할을 설치 하 고 매개 변수 `-IncludeManagementTools`을 사용 하는 경우 Windows PowerShell 용 Hyper-v 모듈도 설치 됩니다. 원격으로 Server Core 설치에서 실행 되는 Hyper-v 호스트를 관리 하려면 다른 컴퓨터에서 Hyper-v 관리자의 GUI 관리 도구를 사용할 수 있습니다. 원격으로 연결 하는 방법에 대 한 지침은 [Hyper-v 관리자를 사용 하 여 hyper-v 호스트 원격 관리](../Manage/Remotely-manage-Hyper-V-hosts.md)를 참조 하세요.  
  
## <a name="see-also"></a>참조  
  
- [설치-Add-windowsfeature](https://docs.microsoft.com/powershell/module/Microsoft.Windows.ServerManager.Migration/Install-WindowsFeature)  
