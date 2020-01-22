---
title: Nano 서버 업데이트
description: " "
ms.prod: windows-server
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: d0ac67eed766f9b04121fc521557f906f644d42f
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947716"
---
# <a name="updating-nano-server"></a>Nano 서버 업데이트

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 

Nano 서버는 최신 상태로 유지할 수 있는 다양한 방법을 제공합니다. Windows Server의 다른 설치 옵션에 비해 Nano 서버는 Windows 10과 유사한 보다 능동적인 서비스 모델을 따릅니다. 이러한 주기적 릴리스를 **CBB(비즈니스용 현재 분기)** 릴리스라고 합니다. 이 방법은 더 빠르게 혁신하고 빠른 개발 수명 주기의 클라우드 빈도로 이동하려는 고객을 지원합니다. CBB에 대한 자세한 내용은 [Windows Server 블로그](https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/)를 참조하세요.

**이러한 CBB 릴리스 사이**에, Nano 서버는 일련의 *누적 업데이트*를 통해 최신 상태를 유지합니다. 예를 들어 Nano 서버의 첫 번째 누적 업데이트는 2016년 9월 26일 [KB4093120](https://support.microsoft.com/help/4093120/windows-10-update-kb4093120)으로 릴리스되었습니다. 이 누적 업데이트 및 이후의 누적 업데이트에서는 Nano 서버에서 이러한 업데이트를 설치하는 다양한 옵션을 제공합니다. 이 문서에서는 Nano 서버의 누적 업데이트를 받고 적용하는 방법을 설명하기 위한 예제로 KB3192366 업데이트를 사용합니다. 누적 업데이트 모델에 대한 자세한 내용은 [Microsoft 업데이트 블로그](https://blogs.technet.microsoft.com/mu/2016/10/25/patching-with-windows-server-2016/)를 참조하세요.

> [!NOTE]
> 미디어 또는 온라인 리포지토리에서 선택적 Nano 서버 패키지를 설치하는 경우에는 최근 보안 픽스가 포함되지 않습니다. 옵션 패키지와 기본 운영 체제 간의 버전 불일치를 방지하기 위해 옵션 패키지를 설치하는 즉시 최신 누적 업데이트를 설치한 **후** 서버를 다시 시작해야 합니다.

Windows Server 2016용 누적 업데이트의 경우: 2016년 9월 26일([KB3192366](https://support.microsoft.com/kb/3192366)), 먼저 Windows 10 버전 1607에 대한 최신 서비스 스택 업데이트를 설치해야 합니다. 필수 구성 요소로 2016년 8월 23일([KB3176936](https://support.microsoft.com/kb/3176936)) 아래의 옵션 중 대부분에는 .cab 업데이트 패키지가 포함된 .msu 파일이 필요합니다. 이러한 각 업데이트 패키지를 다운로드하려면 Microsoft 업데이트 카탈로그를 방문하세요.
- [https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3192366](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3192366)
- [https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3176936](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3176936)

Microsoft 업데이트 카탈로그에서 .msu 파일을 다운로드한 후 네트워크 공유 또는 C:\ServicingPackages와 같은 로컬 디렉터리에 저장합니다. 아래와 같이 .msu 파일을 쉽게 식별할 수 있도록 해당 KB 번호에 따라 이름을 변경할 수 있습니다. 그런 다음, EXPAND 유틸리티를 사용하여 .msu 파일에서 .cab 파일을 별도의 디렉터리에 추출하고 .cabs를 단일 폴더에 복사합니다.

```code
    mkdir C:\ServicingPackages_expanded
    mkdir C:\ServicingPackages_expanded\KB3176936
    mkdir C:\ServicingPackages_expanded\KB3192366
    Expand C:\ServicingPackages\KB3176936.msu -F:* C:\ServicingPackages_expanded\KB3176936
    Expand C:\ServicingPackages\KB3192366.msu -F:* C:\ServicingPackages_expanded\KB3192366
    mkdir C:\ServicingPackages_cabs
    copy C:\ServicingPackages_expanded\KB3176936\Windows10.0-KB3176936-x64.cab C:\ServicingPackages_cabs
    copy C:\ServicingPackages_expanded\KB3192366\Windows10.0-KB3192366-x64.cab C:\ServicingPackages_cabs
```

이제 추출된 .cab 파일을 사용하여 필요에 따라 몇 가지 방법으로 Nano 서버 이미지에 업데이트를 적용할 수 있습니다. 다음 옵션은 특별한 우선 순위 없이 표시됩니다. 환경에 가장 적합한 옵션을 사용하세요.

> [!NOTE]
> DISM 도구를 사용하여 Nano 서버를 서비스하는 경우 서비스 중인 Nano 서버의 버전과 동일하거나 최신 버전의 DISM을 사용해야 합니다. 이렇게 하려면 일치하는 버전의 Windows에서 DISM을 실행하거나 일치하는 버전의 [Windows ADK(Asssessment and Deployment Kit)](https://developer.microsoft.comwindows/hardware/windows-assessment-deployment-kit)를 설치하거나 Nano 서버 자체에서 DISM을 실행하세요.

## <a name="option-1-integrate-a-cumulative-update-into-a-new-image"></a>옵션 1: 새 이미지에 누적 업데이트 통합
새 Nano 서버 이미지를 만드는 경우 첫 번째 부팅에서 완전히 패치되도록 최신 누적 업데이트를 이미지에 직접 통합할 수 있습니다.

```powershell
New-NanoServerImage -ServicingPackagePath 'C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab', 'C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab' -<other parameters>
```

## <a name="option-2-integrate-a-cumulative-update-into-an-existing-image"></a>옵션 2: 기존 이미지에 누적 업데이트 통합
특정 Nano 서버 인스턴스를 만드는 기준으로 사용하는 기존 Nano 서버 이미지가 있는 경우 이미지를 사용하여 생성된 머신이 첫 번째 부팅 시 완전히 패치되도록 최신 누적 업데이트를 기존의 기준 이미지에 직접 통합할 수 있습니다.

```powershell
Edit-NanoServerImage -ServicingPackagePath 'C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab', 'C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab' -TargetPath .\NanoServer.wim
```

## <a name="option-3-apply-the-cumulative-update-to-an-existing-offline-vhd-or-vhdx"></a>옵션 3: 기존 오프라인 VHD 또는 VHDX에 누적 업데이트 적용
기존 가상 하드 디스크(VHD 또는 VHDX)가 있는 경우 DISM 도구를 사용하여 가상 하드 디스크에 업데이트를 적용할 수 있습니다. 디스크를 사용 중인 모든 VM을 종료하거나 가상 하드 디스크 파일을 분리하여 사용 중인 디스크가 없도록 해야 합니다.

- PowerShell 사용하기

   ```powershell
   Mount-WindowsImage -ImagePath .\NanoServer.vhdx -Path .\MountDir -Index 1
   Add-WindowsPackage -Path .\MountDir -PackagePath  C:\ServicingPackages_cabs
   Dismount-WindowsImage -Path .\MountDir -Save
   ```

- dism.exe 사용

   ```code
   dism.exe /Mount-Image /ImageFile:C:\NanoServer.vhdx /Index:1 /MountDir:C:\MountDir
   dism.exe /Image:C:\MountDir /Add-Package /PackagePath:C:\ServicingPackages_cabs
   dism.exe /Unmount-Image /MountDir:C:\MountDir /Commit
   ```

## <a name="option-4-apply-the-cumulative-update-to-a-running-nano-server"></a>옵션 4: 실행 중인 Nano 서버에 누적 업데이트 적용
실행 중인 Nano 서버 VM 또는 물리적 호스트가 있을 때 업데이트를 위한 .cab 파일을 다운로드한 경우 DISM 도구를 사용하여 운영 체제가 온라인 상태일 때 업데이트를 적용할 수 있습니다. .cab 파일을 Nano 서버에서 로컬로 또는 액세스 가능한 네트워크 위치로 복사해야 합니다. 서비스 스택 업데이트를 적용하는 경우 추가 업데이트를 적용하기 전에 서비스 스택 업데이트를 적용하고 서버를 다시 시작해야 합니다.

> [!NOTE]
> New-NanoServerImage cmdlet을 사용하여 Nano 서버 VHD 또는 VHDX 이미지를 만들고 가상 하드 디스크 파일에 대한 MaxSize를 지정하지 않은 경우에는 기본 크기인 4GB는 누적 업데이트를 적용하기에 너무 적습니다. 업데이트를 설치하기 전에 Hyper-V 관리자, 디스크 관리, PowerShell 또는 다른 도구를 사용하여 가상 하드 디스크 및 시스템 볼륨의 크기를 10GB 이상으로 확장하거나 DISM 도구에서 ScratchDir 매개 변수를 사용하여 임시 디렉터리를 최소 10GB의 여유 공간이 있는 볼륨으로 설정하세요.

```powershell
$s = New-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
Copy-Item -ToSession $s -Path C:\ServicingPackages_cabs -Destination C:\ServicingPackages_cabs -Recurse
Enter-PSSession $s
```

- PowerShell 사용하기

   ```powershell
   # Apply the servicing stack update first and then restart
   Add-WindowsPackage -Online -PackagePath C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab
   Restart-Computer; exit

   # After restarting, apply the cumulative update and then restart
   Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
   Add-WindowsPackage -Online -PackagePath C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab
   Restart-Computer; exit
   ```

- dism.exe 사용
   ```powershell
   # Apply the servicing stack update first and then restart
   dism.exe /Online /Add-Package /PackagePath:C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab
   
   # After the operation completes successfully and you are prompted to restart, it's safe to
   # press Ctrl+C to cancel the pipeline and return to the prompt
   Restart-Computer; exit

   # After restarting, apply the cumulative update and then restart
   Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
   dism.exe /Online /Add-Package /PackagePath:C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab
   Restart-Computer; exit
   ```

## <a name="option-5-download-and-install-the-cumulative-update-to-a-running-nano-server"></a>옵션 5: 실행 중인 Nano 서버에 누적 업데이트를 다운로드하고 설치

실행 중인 Nano 서버 VM 또는 물리적 호스트가 있는 경우 Windows 업데이트 WMI 공급자를 사용하면 운영 체제가 온라인 상태일 때 업데이트를 다운로드하고 설치할 수 있습니다. 이 방법을 사용하면 .msu 파일을 Microsoft 업데이트 카탈로그와 별도로 다운로드할 필요가 없습니다. WMI 공급자가 사용 가능한 모든 업데이트를 한 번에 검색하고 다운로드하고 설치합니다.

```powershell
Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
```

- 사용 가능한 업데이트 검색
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  
   $result = $ci | Invoke-CimMethod -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=0";OnlineScan=$true}
   $result.Updates
   ```

- 사용 가능한 업데이트 모두 설치
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   Invoke-CimMethod -InputObject $ci -MethodName ApplyApplicableUpdates
   Restart-Computer; exit
   ```

- 설치된 업데이트 목록 가져오기
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   $result = $ci | Invoke-CimMethod -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=1";OnlineScan=$true}
   $result.Updates
   ```
   
## <a name="additional-options"></a>추가 옵션
Nano 서버를 업데이트하는 다른 방법은 위의 옵션과 겹치거나 위의 옵션을 보완할 수 있습니다. 이러한 옵션에는 WSUS(Windows Server Update Services), System Center VMM(Virtual Machine Manager), 작업 스케줄러 또는 타사 솔루션을 사용하는 방법이 포함됩니다.
- 다음 레지스트리 키를 설정하여 [WSUS를 사용하도록 Windows 업데이트 구성](https://msdn.microsoft.com/library/dd939844(v=ws.10).aspx):
  - WUServer
  - WUStatusServer(일반적으로 WUServer와 동일한 값 사용)
  - UseWUServer
  - AUOptions
- [VMM에서 패브릭 업데이트 관리](https://technet.microsoft.com/library/gg675084(v=sc.12).aspx)
- [예약된 작업 등록](https://technet.microsoft.com/library/jj649811.aspx)