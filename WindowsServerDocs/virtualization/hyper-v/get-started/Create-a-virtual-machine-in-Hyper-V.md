---
title: Hyper-v에서 가상 머신 만들기
description: Hyper-v 관리자 또는 Windows PowerShell을 사용 하 여 가상 컴퓨터를 만드는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: get-started-article
ms.assetid: 59297022-a898-456c-b299-d79cd5860238
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 703c3f739200fafa4934681c300a61d8039d660c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475660"
---
# <a name="create-a-virtual-machine-in-hyper-v"></a>Hyper-v에서 가상 머신 만들기

>적용 대상: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-V 관리자 및 Windows PowerShell을 사용하여 가상 머신을 만드는 방법과 Hyper-V 관리자에서 가상 머신을 만들 때 가질 수 있는 옵션에 대해 알아보세요.

## <a name="create-a-virtual-machine-by-using-hyper-v-manager"></a>Hyper-v 관리자를 사용하여 가상 머신 만들기

1.  **Hyper-v 관리자**를 엽니다.

2.  **작업** 창에서 클릭 **새로**를 클릭하고 **가상 머신**합니다.

3.  **새 가상 머신 마법사**, 클릭 **다음**합니다.

4.  각 페이지에서 가상 머신에 대한 적절한 선택 항목을 확인합니다. 자세한 내용은 [새 가상 머신 옵션 및 Hyper-v 관리자 기본값](#options-in-hyper-v-manager-new-virtual-machine-wizard) 항목의 뒷부분에 제공됩니다.

5.  선택 항목을 확인 한 후의 **요약** 페이지에서 클릭 **마침**합니다.

6.  Hyper-v 관리자에서 가상 머신을 마우스 오른쪽 단추로 클릭하고 선택 **연결**합니다.

7.  가상 컴퓨터 연결 창에서 **작업**  >  **시작**을 선택 합니다.

## <a name="create-a-virtual-machine-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 가상 머신 만들기

1. Windows 바탕 화면에서 시작 단추를 클릭 하 고 이름의 일부를 입력 **Windows PowerShell**합니다.

2. 마우스 오른쪽 단추로 클릭 **Windows PowerShell** 선택한 **관리자 권한으로 실행**합니다.

3. [Get-VMSwitch](https://technet.microsoft.com/library/hh848499.aspx)를 사용하여 가상 머신에서 사용할 가상 스위치의 이름을 가져옵니다.  예를 들면 다음과 같습니다.

   ```
   Get-VMSwitch  * | Format-Table Name
   ```

4. 사용 된 [NEW-VM](https://technet.microsoft.com/library/hh848537.aspx) 가상 머신을 만드는 cmdlet입니다.  다음 예를 참조하십시오.

   > [!NOTE]
   > 사용하여 이 가상 머신을 Windows Server 2012 r 2를 실행하는 Hyper-v 호스트를 이동될 수 있습니다-Version 매개 변수를  [NEW-VM](https://technet.microsoft.com/library/hh848537.aspx)를 5로 가상 머신 구성 버전을 설정합니다. Windows Server 2016에 대한 기본 가상 머신 구성 버전은 Windows Server 2012 R2 또는 이전 버전에서 지원 되지 않습니다. 가상 머신을 만든 후에 가상 머신 구성 버전을 변경할 수 없습니다. 자세한 내용은 [지원 되는 가상 머신 구성 버전](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#supported-virtual-machine-configuration-versions)을 참조하세요.

   - **기존 가상 하드 디스크** -기존 가상 하드 디스크를 사용하여 가상 머신을 만들려면 다음 명령을 사용할 수 있는,
     - **-이름** 사용자가 만드는 가상 머신에 대해 제공하는 이름입니다.
     - **-MemoryStartupBytes** 시작 시 가상 머신에 사용할 수 있는 메모리의 양입니다.
     - **-BootDevice** 디바이스 같은 네트워크 어댑터 (네트워크 어댑터) 또는 가상 하드 디스크 (VHD)이 시작 될 때로 부팅하는 가상 머신입니다.
     - **-VHDPath**의 경로 사용하려는 가상 머신 디스크입니다.
     - **경로** 가상 머신 구성 파일을 보관할 경로입니다.
     - **세대** 가상 머신 생성됩니다. VHD 및 VHDX에 대 한 2 세대에 1 세대를 사용 합니다. 참조 [Hyper-v에 1 또는 2세대 가상 머신을 만들어야 합니다.](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)
     - **-전환** 다른 가상 머신 또는 네트워크에 연결하는데 가상 머신에서 사용할 가상 스위치의 이름입니다. 참조 [Hyper-v 가상 컴퓨터에 대 한 가상 스위치를 만드는](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)합니다.

       ```
       New-VM -Name <Name> -MemoryStartupBytes <Memory> -BootDevice <BootDevice> -VHDPath <VHDPath> -Path <Path> -Generation <Generation> -Switch <SwitchName>
       ```

       예를 들면 다음과 같습니다.

       ```
       New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -VHDPath .\VMs\Win10.vhdx -Path .\VMData -Generation 2 -Switch ExternalSwitch
       ```

       이 4GB의 메모리와 Win10VM 이라는 2세대 가상 머신을 만듭니다. 현재 디렉터리에 VMs\Win10.vhdx 폴더에서 부팅 하 고 ExternalSwitch 라는 가상 스위치를 사용 합니다. 가상 머신 구성 파일은 VMData 폴더에 저장됩니다.

   - **새 가상 하드 디스크** -새 가상 하드 디스크로 가상 머신 만들기 위해서는 **-VHDPath** 매개 변수와 위의 예제 **-NewVHDPath**와 **-NewVHDSizeBytes** 매개 변수를 추가하세요. 예를 들면 다음과 같습니다.

     ```
     New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath .\VMs\Win10.vhdx -Path .\VMData -NewVHDSizeBytes 20GB -Generation 2 -Switch ExternalSwitch
     ```

   - **운영 체제 이미지를 부팅하는 새 가상 하드 디스크** -운영 체제 이미지를 부팅의 PowerShell 예제를 참조하는 새 가상 디스크를 사용하여 가상 머신을 만들려면 [Windows 10에서 hyper-v 가상 머신 연습 만들기](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_create_vm)를 참조하세요.

5. [START-VM](https://technet.microsoft.com/library/hh848589.aspx) cmdlet을 사용하여 가상 머신을 시작합니다. 다음 cmdlet을 실행하고 여기서 Name은 만든 가상 머신의 이름 키를 누릅니다.

   ```
   Start-VM -Name <Name>
   ```

   예를 들면 다음과 같습니다.

   ```
   Start-VM -Name Win10VM
   ```

6. 가상 머신 연결 (VMConnect) 사용하여 가상 머신에 연결합니다.

   ```
   VMConnect.exe
   ```

## <a name="options-in-hyper-v-manager-new-virtual-machine-wizard"></a>Hyper-v 관리자의 새 가상 머신 마법사에서 옵션
다음 표에서 각각에 대해 Hyper-v 관리자 및 기본값에는 가상 머신을 만들 때 선택할 수 있는 옵션을 나열합니다.

|페이지|Windows Server 2016 및 Windows 10에 대 한 기본값|기타 옵션|
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
|**이름 및 위치 지정**|새 가상 머신 이름:입니다.<p>위치:  **C:\ProgramData\Microsoft\Windows\Hyper-V\\**합니다.|또한 고유한 이름을 입력 하고 가상 머신에 대한 다른 위치를 선택합니다.<p>이 가상 머신 구성 파일을 저장합니다.|
|**세대 지정**|1세대|또한 2세대 가상 머신을 만들 수 있습니다. 자세한 내용은 [hyper-v에서 1 세대 또는 2 세대 가상 머신을 만들어야 하나요?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md) 를 참조 하세요.|
|**메모리 할당**|시작 메모리: 1024MB<p>동적 메모리: **선택 하지**|5902 MB로 32MB의 시작 메모리를 설정할 수 있습니다.<p>또한 동적 메모리를 사용할 수 있습니다. 자세한 내용은 참조 [Hyper-v 동적 메모리 개요](https://technet.microsoft.com/library/hh831766.aspx)합니다.|
|**네트워킹 구성**|연결되지 않음|기존 가상 스위치의 목록에서 사용하여 가상 머신에 대한 네트워크 연결을 선택할 수 있습니다. 참조 [Hyper-v 가상 컴퓨터에 대 한 가상 스위치를 만드는](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)합니다.|
|**가상 하드 디스크 연결**|가상 하드 디스크 만들기<p>이름: <*vmname*>.vhdx<p>**위치**: **C:\Users\Public\Documents\Hyper-V\Virtual 하드 디스크\\**<p>**크기**: 127GB|기존 가상 하드 디스크를 사용 하거나 기다렸다가 나중에 가상 하드 디스크를 연결 할 수도 있습니다.|
|**설치 옵션**|운영 체제를 나중에 설치|이러한 옵션의.iso 파일, 부팅 가능한 플로피 디스크 또는 네트워크 설치 서비스와 같은 배포 WDS (Windows 서비스)에서 설치할 수 있도록 가상 머신의 부팅 순서를 변경합니다.|
|**요약**|올바른지 확인할 수 있도록가 선택한 옵션을 표시 합니다.<p>-   Name<br />생성<br />메모리<br />-네트워크<br />하드 디스크<br />-운영 체제|**팁:** 요약 페이지에서 복사 하 고 전자 메일 또는 가상 컴퓨터를 추적할 수 있도록 다른 곳에 붙여 넣을 수 있습니다.|

## <a name="additional-references"></a>추가 참조

- [새 VM](https://technet.microsoft.com/library/hh848537.aspx)

- [지원 되는 가상 머신 구성 버전](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#supported-virtual-machine-configuration-versions)

-   [1세대 또는 2세대 가상 머신을 Hyper-V에서 만들어야 하나요?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)

-   [Hyper-v 가상 컴퓨터에 대 한 가상 스위치 만들기](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)
