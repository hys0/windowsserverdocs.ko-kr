---
title: 1 또는 2 세대 가상 컴퓨터를 Hyper-v에서 만들어야 하나요?
description: 부팅 메서드 같은 지원 되는 고려 사항 및 요구 사항에 맞는 세대를 선택할 수 있도록 다른 기능 차이 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02e31413-6140-4723-a8d6-46c7f667792d
author: KBDAzure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: e3c88ef5ee700bb3906746402bf6cc8916976800
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192771"
---
# <a name="should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v"></a>1 또는 2 세대 가상 컴퓨터를 Hyper-v에서 만들어야 하나요?

>적용 대상: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

> [!NOTE]
> Microsoft Azure, 1 세대 및 2 세대 Vm VHD 파일 형식으로 온-프레미스에서 Windows 가상 머신 (VM)를 그 어느 때 업로드할 계획 하 고 있는 경우 고정된 크기 디스크를 사용할 수 있습니다. 참조 [Azure에서 2 세대 Vm](https://docs.microsoft.com/azure/virtual-machines/windows/generation-2) Azure에서 지원 되는 2 세대 기능에 자세히 알아보려면 합니다. Windows VHD 또는 VHDX를 업로드 하는 방법은 참조 하세요 [Azure에 업로드할 Windows VHD 또는 VHDX 준비](https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image)합니다.

1 세대 또는 2 세대 가상 컴퓨터를 만드는 사용자가 선택한 설치 및 가상 컴퓨터를 배포 하는 데 사용할 부팅 메서드를 원하는 게스트 운영 체제에 따라 다릅니다. 다음 문 중 하나는 경우에 보안 부팅 등의 기능을 이용 하려면 2 세대 가상 컴퓨터를 만드는 것이 좋습니다.  

- VHD에서 부팅 하려면 없는 [UEFI 호환](https://technet.microsoft.com/library/hh824898.aspx)합니다.  
- 2 세대 가상 컴퓨터에서 실행 하려는 운영 체제를 지원 하지 않습니다.  
- 2 세대에 사용 하려는 부팅 방법을 지원 하지 않습니다.  

2 세대 가상 컴퓨터를 사용 하 여 사용할 수 있는 기능에 대 한 자세한 내용은 참조 하세요. [생성 및 게스트에서 Hyper-v 기능 호환성](../Hyper-V-feature-compatibility-by-generation-and-guest.md)합니다.

만든 후 가상 컴퓨터의 세대를 변경할 수 없습니다. 따라서는 하면 여기에서 고려 사항을 검토 뿐만 아니라 운영 체제, 부팅 방법 및 기능 생성을 선택 하기 전에 사용 하려는 선택 것이 좋습니다.  

## <a name="BKMK_OS"></a>지원 되는 게스트 운영 체제?

1 세대 가상 컴퓨터는 대부분의 게스트 운영 체제를 지원합니다. 2 세대 가상 컴퓨터는 가장 64 비트 버전의 Windows 및 Linux 및 FreeBSD 운영 체제의 최신 버전을 지원합니다. 다음 섹션에서는 사용 하 여 가상 컴퓨터의 세대 지원 설치 하려면 게스트 운영 체제를 확인 합니다.  

- [Windows 게스트 운영 체제 지원](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Windows)  

- [CentOS 및 Red Hat Enterprise Linux 게스트 운영 체제 지원](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_CentOS)  

- [Debian 게스트 운영 체제 지원](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Debian)  

- [FreeBSD 게스트 운영 체제 지원](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_FreeBSD)  

- [Oracle Linux 게스트 운영 체제 지원](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Oracle)  

- [SUSE 게스트 운영 체제 지원](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_SUSE)  

- [Ubuntu 게스트 운영 체제 지원](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Ubuntu)  

### <a name="BKMK_Windows"></a>Windows 게스트 운영 체제 지원

다음 표에서는 Windows 64 비트 버전으로 사용할 수 있습니다 게스트 운영 체제 1 세대 및 2 세대 가상 컴퓨터에 대해 보여 줍니다.  

|64 비트 버전의 Windows|1세대|2세대|  
|-------------------------------|----------------|----------------|  
| Windows Server 2019 |&#10004;|&#10004;|  
| Windows Server 2016 |&#10004;|&#10004;|  
| Windows Server 2012 R2 |&#10004;|&#10004;|  
| Windows Server 2012 |&#10004;|&#10004;|  
|Windows Server 2008 R2|&#10004;| &#10006;|  
|Windows Server 2008|&#10004;| &#10006;|  
|Windows 10|&#10004;|&#10004;|  
|Windows 8.1|&#10004;|&#10004;|  
|Windows 8|&#10004;|&#10004;|  
|Windows 7|&#10004;| &#10006;|

다음 표에서는 Windows 32 비트 버전으로 사용할 수 있습니다 게스트 운영 체제 1 세대 및 2 세대 가상 컴퓨터에 대해 보여 줍니다.

|32 비트 버전의 Windows|1세대|2세대|  
|-------------------------------|----------------|----------------|  
|Windows 10|&#10004;| &#10006;|  
|Windows 8.1|&#10004;| &#10006;|  
|Windows 8|&#10004;| &#10006;|  
|Windows 7|&#10004;| &#10006;|  

### <a name="BKMK_CentOS"></a>CentOS 및 Red Hat Enterprise Linux 게스트 운영 체제 지원

다음 표에서 Red Hat Enterprise Linux 버전 \(RHEL\) CentOS 1 세대 및 2 세대 가상 컴퓨터에 게스트 운영 체제로 사용할 수 없다.

|운영 체제 버전|1세대|2세대|  
|-----------------------------|----------------|----------------|  
|RHEL/CentOS 7.x 시리즈|&#10004;|&#10004;|  
|RHEL/CentOS 6.x 시리즈|&#10004;|&#10004;<br />**참고:** Windows Server 2016 이상만 지원 합니다.|  
|RHEL/CentOS 5.x 시리즈|&#10004;| &#10006;|  

자세한 내용은 참조 [CentOS 및 Red Hat Enterprise Linux Hyper-v에서 가상 컴퓨터](../Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)합니다.  

### <a name="BKMK_Debian"></a>Debian 게스트 운영 체제 지원  

다음 표에서 Debian의 버전 1 세대 및 2 세대 가상 컴퓨터에 대 한 게스트 운영 체제도 사용할 수 없다 보여 줍니다.

|운영 체제 버전|1세대|2세대|  
|-----------------------------|----------------|----------------|  
|Debian 7.x 시리즈|&#10004;| &#10006;|  
|Debian 8.x 시리즈|&#10004;|&#10004;|  

자세한 내용은 참조 [Hyper-v에서 가상 컴퓨터를 Debian](../Supported-Debian-virtual-machines-on-Hyper-V.md)합니다.  

### <a name="BKMK_FreeBSD"></a>FreeBSD 게스트 운영 체제 지원

다음 표에서 FreeBSD 버전 1 세대 및 2 세대 가상 컴퓨터에 대 한 게스트 운영 체제로 사용할 수 없다 보여 줍니다.  

|운영 체제 버전|1세대|2세대|  
|-----------------------------|----------------|----------------|  
|FreeBSD 10과 10.1|&#10004;| &#10006;|  
|FreeBSD 9.1 및 9.3|&#10004;| &#10006;|  
|FreeBSD 8.4|&#10004;| &#10006;|  

자세한 내용은 참조 [Hyper-v에 FreeBSD 가상 컴퓨터](../Supported-FreeBSD-virtual-machines-on-Hyper-V.md)합니다.  

### <a name="BKMK_Oracle"></a>Oracle Linux 게스트 운영 체제 지원  

다음 표에서 어떤 버전 Red Hat 호환 커널 시리즈의 1 세대 및 2 세대 가상 컴퓨터에 대 한 게스트 운영 체제로 사용 수 없다 보여 줍니다.  

|Red Hat 호환 커널 시리즈 버전|1세대|2세대|  
|---------------------------------------------|----------------|----------------|  
|Oracle Linux 7.x 시리즈|&#10004;|&#10004;|
|Oracle Linux 6.x 시리즈|&#10004;| &#10006;|  

다음 표에서 Unbreakable Enterprise Kernel의 버전 1 세대 및 2 세대 가상 컴퓨터에 대 한 게스트 운영 체제도 사용할 수 없다 보여 줍니다.

|Unbreakable Enterprise Kernel (UEK) 버전|1세대|2세대|  
|--------------------------------------------------|----------------|----------------|  
|Oracle Linux UEK R3 QU3|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU2|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU1|&#10004;| &#10006;|  

자세한 내용은 참조 [Oracle Linux 가상 컴퓨터에 Hyper-v](../Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)합니다.  

### <a name="BKMK_SUSE"></a>SUSE 게스트 운영 체제 지원

다음 표에서는 SUSE 버전 1 세대 및 2 세대 가상 컴퓨터에 대 한 게스트 운영 체제로 사용할 수 없다 보여 줍니다.

|운영 체제 버전|1세대|2세대|  
|-----------------------------|----------------|----------------|  
|SUSE Linux Enterprise Server 12 시리즈|&#10004;|&#10004;|  
|SUSE Linux Enterprise Server 11 시리즈|&#10004;| &#10006;|  
|12.3 SUSE 열기|&#10004;| &#10006;|  

자세한 내용은 참조 [Hyper-v에서 가상 컴퓨터 SUSE](../Supported-SUSE-virtual-machines-on-Hyper-V.md)합니다.  

### <a name="BKMK_Ubuntu"></a>Ubuntu 게스트 운영 체제 지원

다음 표에서 Ubuntu 버전으로 사용할 수 있습니다 게스트 운영 체제 1 세대 및 2 세대 가상 컴퓨터에 대해 보여 줍니다.

|운영 체제 버전|1세대|2세대|  
|-----------------------------|----------------|----------------|  
|Ubuntu 14.04 및 이후 버전|&#10004;|&#10004;|  
|Ubuntu 12.04|&#10004;| &#10006;|  

자세한 내용은 참조 [Ubuntu 가상 컴퓨터에 Hyper-v](../Supported-Ubuntu-virtual-machines-on-Hyper-V.md)합니다.  

## <a name="BKMK_Boot"></a>가상 컴퓨터를 부팅할 수는 방법

다음 표에서 메서드는 1 세대 및 2 세대 가상 컴퓨터에서 지원 되는 부팅을 보여 줍니다.  

|부팅 메서드|1세대|2세대|  
|---------------|----------------|----------------|  
|표준 네트워크 어댑터를 사용한 PXE 부팅| &#10006;|&#10004;|  
|레거시 네트워크 어댑터를 사용 하 여 PXE 부팅|&#10004;| &#10006;|  
|SCSI 가상 하드 디스크에서 부팅 (합니다. VHDX) 또는 가상 DVD (합니다. ISO)| &#10006;|&#10004;|  
|가상 하드 디스크를 IDE 컨트롤러에서 부팅 (합니다. VHD) 또는 가상 DVD (합니다. ISO)|&#10004;| &#10006;|  
|플로피에서 부팅 (합니다. VFD)|&#10004;| &#10006;|  

## <a name="BKMK_Advantages"></a>2 세대 가상 컴퓨터를 사용 하는 이점은 무엇입니까?

몇 가지 때 2 세대 가상 컴퓨터를 사용 하는 이점은 다음과 같습니다.  
- **보안 부팅** 부팅 로더는 권한 없는 펌웨어, 운영 체제 또는 UEFI 드라이버가 부팅 시에 실행 하지 않도록 하기 위해 UEFI 데이터베이스의 신뢰할 수 있는 기관에서 서명 확인 하는 기능은이 있습니다. 보안 부팅은 2세대 가상 컴퓨터에서 기본적으로 사용됩니다. 보안 부팅에서 지원 되지 않는 게스트 운영 체제를 실행 해야 할 경우 가상 컴퓨터를 만든 후 비활성화할 수 있습니다.  자세한 내용은 [보안 부팅](https://technet.microsoft.com/library/dn486875.aspx)을 참조하세요.  

    보안 부팅 2 세대 Linux 가상 컴퓨터에 가상 컴퓨터를 만들 때 UEFI CA 보안 부팅 서식 파일을 선택 해야 합니다.  

- **첫 번째 부팅 볼륨** 2 세대 가상 컴퓨터에 대 한 최대 부팅 볼륨은 64TB입니다. 지 원하는 최대 디스크 크기는 합니다. VHDX 합니다. 1 세대 가상 컴퓨터에 대 한 최대 부팅 볼륨이 2TB를 합니다. VHDX에 대 한 2040GB 하 고는 합니다. VHD입니다. 자세한 내용은 참조 [Hyper-v 가상 하드 디스크 형식 개요](https://technet.microsoft.com/library/hh831446.aspx)합니다.  

 2 세대 가상 컴퓨터와 가상 컴퓨터 부팅 및 설치 시간이 약간 향상을 확인할 수도 있습니다.

## <a name="BKMK_DeviceCompare"></a> 장치 지원의 차이점은 무엇입니까?

다음 표에서 1 세대 및 2 세대 가상 컴퓨터 간에 사용 가능한 장치를 비교 합니다.  

|1세대 장치|2세대 교체|2세대 개선|  
|-----------------------|----------------------------|-----------------------------|  
|IDE 컨트롤러|가상 SCSI 컨트롤러|.vhdx에서 부팅(최대 크기 64TB, 온라인 크기 조정 기능)|  
|IDE CD-ROM|가상 SCSI CD-ROM|SCSI 컨트롤러당 최대 64개의 SCSI DVD 장치 지원|  
|레거시 BIOS|UEFI 펌웨어|보안 부팅|  
|레거시 네트워크 어댑터|가상 네트워크 어댑터|IPv4 및 IPv6을 사용한 네트워크 부팅|  
|플로피 컨트롤러 및 DMA 컨트롤러|플로피 컨트롤러 지원 안 함|해당 사항 없음|  
|COM 포트용 UART(범용 비동기 수신기/송신기)|디버깅에 대한 선택적 UART|보다 빠르고 안정적|  
|i8042 키보드 컨트롤러|소프트웨어 기반 입력|에뮬레이션이 없으므로 더 적은 리소스를 사용하며, 게스트 운영 체제의 공격 취약점 감소|  
|PS/2 키보드|소프트웨어 기반 키보드|에뮬레이션이 없으므로 더 적은 리소스를 사용하며, 게스트 운영 체제의 공격 취약점 감소|  
|PS/2 마우스|소프트웨어 기반 마우스|에뮬레이션이 없으므로 더 적은 리소스를 사용하며, 게스트 운영 체제의 공격 취약점 감소|  
|S3 비디오|소프트웨어 기반 비디오|에뮬레이션이 없으므로 더 적은 리소스를 사용하며, 게스트 운영 체제의 공격 취약점 감소|  
|PCI 버스|더 이상 필요 없음|해당 사항 없음|  
|PIC(프로그램 가능 인터럽트 컨트롤러)|더 이상 필요 없음|해당 사항 없음|  
|PIT(프로그램 가능 간격 타이머)|더 이상 필요 없음|해당 사항 없음|  
|Super I/O 장치|더 이상 필요 없음|해당 사항 없음|  

## <a name="BKMK_More"></a> 2 세대 가상 컴퓨터에 대 한 자세한 정보

다음은 2 세대 virtual machines를 사용 하는 방법에 대 한 몇 가지 추가 팁입니다.

### <a name="attach-or-add-a-dvd-drive"></a>연결 또는 DVD 드라이브를 추가 합니다.

- 2 세대 가상 컴퓨터에 실제 CD 또는 DVD 드라이브를 연결할 수 없습니다. 2세대 가상 컴퓨터의 가상 DVD 드라이브는 ISO 이미지 파일만 지원합니다. Windows 환경의 ISO 이미지 파일을 만들려면 Oscdimg 명령줄 도구를 사용할 수 있습니다. 자세한 내용은 [Oscdimg 명령줄 옵션](https://msdn.microsoft.com/library/hh824847.aspx)참조하세요.
- NEW-VM Windows PowerShell cmdlet과 함께 새 가상 컴퓨터를 만들 때 2 세대 가상 컴퓨터 DVD 드라이브가 필요는 없습니다. 가상 컴퓨터에서 실행 되는 동안 DVD 드라이브를 추가할 수 있습니다.

### <a name="use-uefi-firmware"></a>UEFI 펌웨어를 사용 합니다.

- 보안 부팅 또는 UEFI 펌웨어는 실제 Hyper-v 호스트에 필요한 되지 않습니다. Hyper-v 가상 컴퓨터에 Hyper-v 호스트에는 무엇이 상관 없는 가상 펌웨어를 제공 합니다.
- 2 세대 가상 컴퓨터의 UEFI 펌웨어는 보안 부팅에 대 한 설치 모드를 지원 하지 않습니다.
- 2 세대 가상 컴퓨터에 UEFI 셸 또는 다른 UEFI 응용 프로그램을 실행 중인 지원 되지 않습니다. 타사 UEFI 셸 또는 UEFI 응용 프로그램을 사용하는 것은 소스에서 직접 컴파일된 경우 기술적으로 가능합니다. 이러한 응용 프로그램은 적절 하 게 디지털 서명이 없는 경우 가상 컴퓨터에 대 한 보안 부팅을 해제 해야 합니다.

### <a name="work-with-vhdx-files"></a>VHDX 파일 작업

- 가상 컴퓨터에서 실행 되는 동안 2 세대 가상 컴퓨터에 대 한 부팅 볼륨을 포함 하는 VHDX 파일의 크기를 조정할 수 있습니다.
- 지원 하지 않거나 1 세대와 2 세대 가상 컴퓨터를 부팅 가능한 VHDX 파일을 만드는 것이 좋습니다.  
- 가상 컴퓨터 세대는 가상 하드 디스크의 속성이 아니라 가상 컴퓨터의 속성입니다. 따라서 VHDX 파일이 1 세대 또는 2 세대 가상 컴퓨터에서 만들어진 경우 인식할 수 없습니다.  
- 세대 2 가상 컴퓨터의 IDE 컨트롤러 또는 1 세대 가상 컴퓨터의 SCSI 컨트롤러에 연결할 수를 사용 하 여 만든 VHDX 파일입니다. 그러나 부팅 가능한 VHDX 파일의 경우 1 세대 가상 컴퓨터 부팅 되지 않습니다.

### <a name="use-ipv6-instead-of-ipv4"></a>IPv4 대신 IPv6을 사용 합니다.

기본적으로 2세대 가상 컴퓨터는 IPv4를 사용합니다. IPv6를 대신 사용 하려면 실행 합니다 [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx) Windows PowerShell cmdlet. 예를 들어 다음 명령은 TestVM 이라는 가상 컴퓨터에 대 한 ipv6 기본 설정된 프로토콜을 설정:  

```powershell
Set-VMFirmware -VMName TestVM -IPProtocolPreference IPv6  
```  

## <a name="BKMK_Debug"></a>커널 디버깅에 대 한 COM 포트를 추가 합니다.

추가할 때까지 COM 포트를 2 세대 가상 컴퓨터에서 사용할 수 없습니다. Windows PowerShell 또는 Windows Management Instrumentation (WMI)를 사용 하 여이 수행할 수 있습니다. 이러한 단계는 Windows PowerShell을 사용 하 여 수행 하는 방법을 보여 줍니다.

COM 포트를 추가 합니다.  

1. 보안 부팅을 사용하지 않도록 설정합니다. 커널 디버깅 보안 부팅을 사용 하 여 호환 되지 않습니다. 가상 머신이 꺼짐 상태에 있는지 확인 한 다음 사용 합니다 [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx) cmdlet. 예를 들어 다음 명령은 TestVM 가상 컴퓨터에서 보안 부팅을 비활성화합니다.  

    ```powershell  
    Set-VMFirmware -Vmname TestVM -EnableSecureBoot Off  
    ```  

2. COM 포트를 추가 합니다. 사용 된 [Set-vmcomport](https://technet.microsoft.com/library/hh848616.aspx) cmdlet이 작업을 수행 합니다. 예를 들어 다음 명령은 로컬 컴퓨터에 명명 된 파이프, TestPipe에 연결 하도록 TestVM 가상 컴퓨터의 첫 번째 COM 포트를 구성 합니다.  

    ```powershell
    Set-VMComPort -VMName TestVM 1 \\.\pipe\TestPipe  
    ```  

> [!NOTE]  
> 구성 된 COM 포트는 Hyper-v 관리자에서 가상 컴퓨터의 설정에 표시 되지 않습니다.

## <a name="see-also"></a>관련 항목  

- [Linux 및 Hyper-v에 FreeBSD 가상 컴퓨터](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)
- [VMConnect 사용 하 여 Hyper-v 가상 머신에서 로컬 리소스 사용](../learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)
- [Windows Server 2016의 Hyper-v 확장성에 대 한 계획](Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)
