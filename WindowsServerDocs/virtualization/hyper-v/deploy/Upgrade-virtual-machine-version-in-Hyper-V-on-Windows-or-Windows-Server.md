---
title: Windows 10 또는 Windows Server에서 Hyper-v의 가상 머신 버전 업그레이드
description: 가상 컴퓨터의 버전을 업그레이드 하는 방법에 대 한 지침 및 고려 사항 제공
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 897f2454-5aee-445c-a63e-f386f514a0f6
author: jasongerend
ms.author: jgerend
ms.date: 05/22/2019
ms.openlocfilehash: 96678dfab2a3d5b6f503d8ce9d00850a3c437b35
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392936"
---
# <a name="upgrade-virtual-machine-version-in-hyper-v-on-windows-10-or-windows-server"></a>Windows 10 또는 Windows Server에서 Hyper-v의 가상 머신 버전 업그레이드

>적용 대상: Windows 10, Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

구성 버전을 업그레이드 하 여 가상 머신에서 최신 Hyper-v 기능을 사용할 수 있도록 합니다. 다음을 수행할 때까지이 작업을 수행 하지 않습니다.

- Hyper-v 호스트를 최신 버전의 Windows 또는 Windows Server로 업그레이드 합니다.
- 클러스터 기능 수준을 업그레이드 합니다.
- 이전 버전의 Windows 또는 Windows Server를 실행 하는 Hyper-v 호스트로 가상 컴퓨터를 다시 이동할 필요가 없습니다.

자세한 내용은 [클러스터 운영 체제 롤링 업그레이드](../../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md) 및 [VMM에서 hyper-v 호스트 클러스터의 롤링 업그레이드 수행](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade)을 참조 하세요.

## <a name="step-1-check-the-virtual-machine-configuration-versions"></a>1단계: 가상 컴퓨터 구성 버전 확인

1. Windows 데스크톱에서 시작 단추를 클릭하고 **Windows PowerShell** 이름의 일부를 입력합니다.
2. Windows PowerShell을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다.
3. [GET VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm)cmdlet을 사용 합니다. 다음 명령을 실행 하 여 가상 컴퓨터의 버전을 가져옵니다.

```PowerShell
Get-VM * | Format-Table Name, Version
```

가상 컴퓨터를 선택 하 고 **요약** 탭에서 hyper-v 관리자의 구성 버전을 볼 수도 있습니다.

## <a name="step-2-upgrade-the-virtual-machine-configuration-version"></a>2단계: 가상 컴퓨터 구성 버전 업그레이드

1. Hyper-v 관리자에서 가상 컴퓨터를 종료 합니다.
2. 구성 버전 업그레이드 > 작업을 선택 합니다. 가상 컴퓨터에 대해이 옵션을 사용할 수 없는 경우 Hyper-v 호스트에서 지 원하는 가장 높은 구성 버전에 이미 있는 것입니다.

Windows PowerShell을 사용 하 여 가상 머신 구성 버전을 업그레이드 하려면 [업데이트-VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion) cmdlet을 사용 합니다. 다음 명령을 실행 합니다. 여기서 vmname은 가상 머신의 이름입니다.

```PowerShell
Update-VMVersion <vmname>
```

## <a name="supported-virtual-machine-configuration-versions"></a>지원 되는 가상 컴퓨터 구성 버전

PowerShell cmdlet [VMHostSupportedVersion](https://docs.microsoft.com/powershell/module/hyper-v/get-vmhostsupportedversion) 를 실행 하 여 hyper-v 호스트가 지 원하는 가상 컴퓨터 구성 버전을 확인 합니다. 가상 컴퓨터를 만들 때 기본 구성 버전으로 만들어집니다. 기본값을 보려면 다음 명령을 실행 합니다.

```PowerShell
Get-VMHostSupportedVersion -Default
```

이전 버전의 Windows를 실행 하는 Hyper-v 호스트로 이동할 수 있는 가상 컴퓨터를 만들어야 하는 경우-version 매개 변수와 함께 [새 VM](https://docs.microsoft.com/powershell/module/hyper-v/new-vm) cmdlet을 사용 합니다. 예를 들어 Windows Server 2012 r 2를 실행 하는 Hyper-v 호스트로 이동할 수 있는 가상 머신을 만들려면 다음 명령을 실행 합니다. 이 명령은 구성 버전 5.0을 사용 하 여 이름이 "WindowsCV5" 인 가상 컴퓨터를 만듭니다.

```PowerShell
New-VM -Name "WindowsCV5" -Version 5.0
```

>[!NOTE]
>이전 버전의 Windows를 실행 하는 Hyper-v 호스트에 대해 만들어진 가상 컴퓨터를 가져오거나 백업에서 복원할 수 있습니다. Vm의 구성 버전이 아래 표에 있는 Hyper-v 호스트 OS에 대해 지원 되는 것으로 표시 되지 않는 경우 vm을 시작 하기 전에 vm 구성 버전을 업데이트 해야 합니다.

### <a name="supported-vm-configuration-versions-for-long-term-servicing-hosts"></a>장기 서비스 호스트에 대해 지원 되는 VM 구성 버전

다음 표에는 장기 서비스 버전의 Windows를 실행 하는 호스트에서 지원 되는 VM 구성 버전이 나와 있습니다.

| Hyper-v 호스트 Windows 버전 | 9.1 | 9.0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
| --- |---|---|---|---|---|---|---|---|---|---|
|Windows Server 2019|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise LTSC 2019|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2016 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2015 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|
|Windows Server 2012 R2|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|
|Windows 8.1|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|

### <a name="supported-vm-configuration-versions-for-semi-annual-channel-hosts"></a>반기 채널 호스트에 대해 지원 되는 VM 구성 버전

다음 표에는 현재 지원 되는 Windows의 반기 채널 버전을 실행 하는 호스트에 대 한 VM 구성 버전이 나와 있습니다. Windows의 반기 채널 버전에 대 한 자세한 내용을 보려면 [Windows Server](../../../get-started-19/servicing-channels-19.md) 및 [windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview#servicing-channels) 에 대 한 다음 페이지를 방문 하세요.

| Hyper-v 호스트 Windows 버전 | 9.1 | 9.0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
| --- |---|---|---|---|---|---|---|---|---|---|
| Windows 10 5 월 2019 업데이트 (버전 1903) |&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;| &#10004;|
| Windows Server, 버전 1903 |&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;| &#10004;|
|Windows Server, 버전 1809|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 10 월 2018 업데이트 (버전 1809)|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server, 버전 1803|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 4 월 2018 업데이트 (버전 1803)|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10의 작성자 업데이트 (버전 1709)|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 크리에이터 스 업데이트 (버전 1703)|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 기념일 업데이트 (버전 1607)|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|

## <a name="why-should-i-upgrade-the-virtual-machine-configuration-version"></a>가상 컴퓨터 구성 버전을 업그레이드 해야 하는 이유는 무엇 인가요?

Windows Server 2019, Windows Server 2016 또는 Windows 10에서 Hyper-v를 실행 하는 컴퓨터로 가상 컴퓨터를 이동 하거나 가져오는 경우 가상 컴퓨터의 구성이 자동으로 업데이트 되지 않습니다. 즉, 이전 버전의 Windows 또는 Windows Server를 실행 하는 Hyper-v 호스트에 가상 컴퓨터를 다시 이동할 수 있습니다. 그러나이는 구성 버전을 수동으로 업데이트할 때까지 새 가상 컴퓨터 기능 중 일부를 사용할 수 없음을 의미 하기도 합니다. 업그레이드 한 후에는 가상 머신 구성 버전을 다운 그레이드할 수 없습니다.

가상 머신 구성 버전은 가상 머신의 구성, 저장 된 상태 및 스냅숏 파일과 Hyper-v 버전의 호환성을 나타냅니다. 구성 버전을 업데이트 하는 경우 가상 머신 구성 및 검사점 파일을 저장 하는 데 사용 되는 파일 구조를 변경 합니다. 또한 구성 버전을 해당 Hyper-v 호스트에서 지 원하는 최신 버전으로 업데이트 합니다. 업그레이드 된 가상 컴퓨터는 가상 컴퓨터 구성 데이터 읽기 및 쓰기의 효율성을 높이기 위해 설계된 새 구성 파일 형식을 사용합니다. 또한 업그레이드는 저장소 오류 발생 시 데이터 손상 가능성을 줄입니다.

다음 표에는 새 가상 컴퓨터 또는 업그레이드 된 가상 컴퓨터에 사용 되는 각 파일 형식에 대 한 설명, 파일 이름 확장명 및 기본 위치가 나와 있습니다.

 |가상 컴퓨터 파일 형식 | 설명|
 |---|---|
|Configuration |이진 파일 형식으로 저장 된 가상 컴퓨터 구성 정보입니다. <br /> 파일 이름 확장명:. vmcx <br /> 기본 위치: C:\ProgramData\Microsoft\Windows\Hyper-V\가상 컴퓨터|
 |런타임 상태|이진 파일 형식으로 저장 된 가상 컴퓨터 런타임 상태 정보입니다. <br />파일 이름 확장명:. vmrs 및 vmrs <br />기본 위치: C:\ProgramData\Microsoft\Windows\Hyper-V\가상 컴퓨터|
|가상 하드 디스크|가상 컴퓨터의 가상 하드 디스크를 저장 합니다. <br /> 파일 이름 확장명: .vhd 또는 .vhdx <br />기본 위치: 하드 디스크 C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual|
 |자동 가상 하드 디스크 |가상 컴퓨터 검사점에 사용 되는 차이점 보관용 디스크 파일입니다. <br /> 파일 이름 확장명:. .avhdx <br /> 기본 위치: 하드 디스크 C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual|
 |검사점|검사점은 여러 검사점 파일에 저장됩니다. 각 검사점은 구성 파일 및 런타임 상태 파일을 만듭니다. <br /> 파일 이름 확장명:. vmrs 및 vmrs <br />기본 위치: C:\ProgramData\Microsoft\Windows\Snapshots|

## <a name="what-happens-if-i-dont-upgrade-the-virtual-machine-configuration-version"></a>가상 머신 구성 버전을 업그레이드 하지 않으면 어떻게 되나요?

이전 버전의 Hyper-v를 사용 하 여 만든 가상 컴퓨터가 있는 경우 구성 버전을 업데이트할 때까지 최신 호스트 OS에서 사용할 수 있는 일부 기능이 해당 가상 컴퓨터에서 작동 하지 않을 수 있습니다.

일반적으로 가상화 호스트를 최신 버전의 Windows로 성공적으로 업그레이드 하 고 롤백할 필요가 없다고 확신 하는 경우 구성 버전을 업데이트 하는 것이 좋습니다. [클러스터 OS 롤링 업그레이드](https://docs.microsoft.com/windows-server/failover-clustering/Cluster-Operating-System-Rolling-Upgrade) 기능을 사용 하는 경우 일반적으로 클러스터 기능 수준을 업데이트 한 후에이 기능을 사용 합니다. 이러한 방식으로 새로운 기능과 내부 변경 및 최적화를 활용 하는 것이 좋습니다.

>[!NOTE]
>VM 구성 버전이 업데이트 되 면 업데이트 된 구성 버전을 지원 하지 않는 호스트에서 VM을 시작할 수 없습니다.

다음 표에서는 일부 Hyper-v 기능을 사용 하는 데 필요한 최소 가상 머신 구성 버전을 보여 줍니다.

|기능|최소 VM 구성 버전|
|---|---|
|메모리 핫 추가/제거|6.2|
|Linux VM에 대한 보안 부팅|6.2|
|프로덕션 검사점|6.2|
|PowerShell Direct |6.2|
|가상 컴퓨터 그룹화|6.2|
|vTPM(가상 신뢰할 수 있는 플랫폼 모듈)|7.0|
|가상 컴퓨터 다중 큐 (VMMQ)|7.1|
|XSAVE 지원|8.0|
|키 저장소 드라이브|8.0|
|게스트 가상화 기반 보안 지원 (VBS)|8.0|
|중첩 된 가상화|8.0|
|가상 프로세서 수|8.0|
|대량 메모리 Vm|8.0|
|가상 장치의 기본 최대 수를 장치당 64 (예: 네트워킹 및 할당 된 장치)로 늘립니다.|8.3|
|Perfmon의 추가 프로세서 기능 허용|9.0|
|[핵심 스케줄러](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler) 를 사용 하 여 호스트에서 실행 중인 vm에 대 한 [동시 다중 스레딩](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#background) 구성 자동으로 노출|9.0|
|최대 절전 모드 지원|9.0|

이러한 기능에 대 한 자세한 내용은 [Windows Server에서 제공 되는 hyper-v의 새로운](../What-s-new-in-Hyper-V-on-Windows.md)기능을 참조 하세요.

