---
title: 저장소 공간 다이렉트 배포
ms.prod: windows-server
manager: eldenc
ms.author: stevenek
ms.technology: storage-spaces
ms.topic: get-started-article
ms.assetid: 20fee213-8ba5-4cd3-87a6-e77359e82bc0
author: stevenek
ms.date: 06/07/2019
description: Windows Server의 스토리지 공간 다이렉트를 사용 하 여 하이퍼 수렴 형 인프라 또는 수렴 형 (세분화 된) 인프라가 있는 소프트웨어 정의 저장소를 배포 하는 단계별 지침을 참조 하세요.
ms.localizationpriority: medium
ms.openlocfilehash: 0ab96f737f7700e202c9d0382c06859c4ea84118
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402820"
---
# <a name="deploy-storage-spaces-direct"></a>저장소 공간 다이렉트 배포

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 [스토리지 공간 다이렉트](storage-spaces-direct-overview.md)을 배포 하는 단계별 지침을 제공 합니다.

> [!Tip]
> 하이퍼 수렴 형 인프라를 획득 하 고 싶으십니까? Microsoft는 배포 도구 및 절차를 포함 하 여, 파트너의 검증 된 하드웨어/소프트웨어 솔루션을 구입 하는 것이 좋습니다. 이러한 솔루션은 호환성 및 안정성을 보장 하기 위해 참조 아키텍처에 대해 설계, 조합 및 유효성 검사를 수행 하므로 신속 하 게 시작 하 고 실행할 수 있습니다. Windows Server 2019 솔루션은 [AZURE STACK HCI solutions 웹 사이트](https://azure.microsoft.com/overview/azure-stack/hci)를 참조 하세요. Windows Server 2016 솔루션에 대 한 자세한 내용은 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd)를 자세히 알아보세요.

> [!Tip]
> Microsoft Azure를 포함 하 여 Hyper-v 가상 컴퓨터를 사용 하 여 [하드웨어 없이 스토리지 공간 다이렉트를 평가할](storage-spaces-direct-in-vm.md)수 있습니다. 학습 목적으로 사용 하는 편리한 [Windows Server 신속한 랩 배포 스크립트](https://aka.ms/wslab)를 검토할 수도 있습니다.

## <a name="before-you-start"></a>시작하기 전 확인 사항

[스토리지 공간 다이렉트 하드웨어 요구 사항을](Storage-Spaces-Direct-Hardware-Requirements.md) 검토 하 고이 문서를 skim 하 여 일부 단계와 관련 된 전체 접근 방식 및 중요 정보를 숙지 합니다.

다음 정보를 수집 합니다.

- **배포 옵션입니다.** 스토리지 공간 다이렉트는 [하이퍼 수렴 형 및 수렴](storage-spaces-direct-overview.md#deployment-options)됨 (disaggregated 수 라고도 함)의 두 가지 배포 옵션을 지원 합니다. 사용자에 게 적합 한 것을 결정 하는 것은 각각의 이점에 익숙해져야 합니다. 아래 1-3 단계는 두 배포 옵션에 모두 적용 됩니다. 4 단계는 수렴 형 배포에만 필요 합니다.

- **서버 이름.** 컴퓨터, 파일, 경로 및 기타 리소스에 대 한 조직의 명명 정책에 대해 알아봅니다. 각각 고유한 이름을 가진 여러 서버를 프로 비전 해야 합니다.

- **도메인 이름입니다.** 도메인 명명 및 도메인 가입에 대 한 조직의 정책에 대해 알아봅니다.  서버를 도메인에 가입 시키고 도메인 이름을 지정 해야 합니다. 

- **RDMA 네트워킹.** RDMA 프로토콜에는 iWarp 및 RoCE의 두 가지 유형이 있습니다. 네트워크 어댑터에서 사용 하는 것을 확인 하 고 RoCE의 경우 버전 (v1 또는 v2)도 기록 합니다. RoCE의 경우 랙 상판 스위치의 모델도 확인 합니다.

- **VLAN ID입니다.** 서버에서 관리 OS 네트워크 어댑터에 사용할 VLAN ID (있는 경우)를 확인 합니다. 네트워크 관리자로부터 얻을 수 있습니다.

## <a name="step-1-deploy-windows-server"></a>1단계: Windows Server 배포

### <a name="step-11-install-the-operating-system"></a>1\.1 단계: 운영 체제 설치

첫 번째 단계는 클러스터에 있는 모든 서버에 Windows Server를 설치 하는 것입니다. 스토리지 공간 다이렉트 Windows Server 2016 Datacenter Edition이 필요 합니다. Server Core 설치 옵션을 사용 하거나 데스크톱 환경에서 서버를 사용할 수 있습니다.

설치 마법사를 사용 하 여 Windows Server를 설치 하는 경우 windows server 2012 r 2에서 사용할 수 있는 *전체* 설치 옵션에 해당 하 *는 Windows Server (server* Core 참조)와 *windows Server (데스크톱 환경 포함 서버)* 중에서 선택할 수 있습니다. 선택 하지 않으면 Server Core 설치 옵션을 사용할 수 있습니다. 자세한 내용은 [Windows Server 2016에 대 한 설치 옵션](../../get-started/Windows-Server-2016.md)을 참조 하세요.

### <a name="step-12-connect-to-the-servers"></a>1\.2 단계: 서버에 연결

이 가이드에서는 Server Core 설치 옵션을 중점적으로 설명 하 고 다음과 같은 별도의 관리 시스템에서 원격으로 배포/관리 합니다.

- 관리 중인 서버와 동일한 업데이트를 포함 하는 Windows Server 2016
- 관리 중인 서버에 대 한 네트워크 연결
- 동일한 도메인 또는 완전히 신뢰할 수 있는 도메인에 가입
- Hyper-V 및 장애 조치(failover) 클러스터링용 PowerShell 모듈 및 RSAT(원격 서버 관리 도구) RSAT 도구 및 PowerShell 모듈은 Windows Server에서 사용할 수 있으며 다른 기능을 설치 하지 않고도 설치할 수 있습니다. Windows 10 관리 PC에 [원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520) 를 설치할 수도 있습니다.

관리 시스템에서 장애 조치(failover) 클러스터 및 Hyper-V 관리 도구를 설치합니다. 서버 관리자에서 **역할 및 기능 추가** 마법사를 사용하여 이 작업을 수행할 수 있습니다. **기능** 페이지에서 **원격 서버 관리 도구**를 선택한 다음 설치할 도구를 선택합니다.

PS 세션을 입력하고 서버 이름 또는 연결하려는 노드의 IP 주소를 사용합니다. 이 명령을 실행 한 후 암호를 입력 하 라는 메시지가 표시 되 면 Windows를 설정할 때 지정한 관리자 암호를 입력 합니다.

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   이 작업을 두 번 이상 수행 해야 하는 경우 스크립트에서 보다 유용한 방식으로 동일한 작업을 수행 하는 예제는 다음과 같습니다.

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> 관리 시스템에서 원격으로 배포 하는 경우 *WinRM에서 요청을 처리할 수 없다는* 오류 메시지가 표시 될 수 있습니다. 이 문제를 해결 하려면 Windows PowerShell을 사용 하 여 각 서버를 관리 컴퓨터의 신뢰할 수 있는 호스트 목록에 추가 합니다.  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> 참고: 신뢰할 수 있는 호스트 목록은 `Server*`와 같은 와일드 카드를 지원 합니다.
>
> 신뢰할 수 있는 호스트 목록을 보려면 `Get-Item WSMAN:\Localhost\Client\TrustedHosts`를 입력 합니다.  
>   
> 목록을 비우려면 `Clear-Item WSMAN:\Localhost\Client\TrustedHost`를 입력 합니다.  

### <a name="step-13-join-the-domain-and-add-domain-accounts"></a>1\.3 단계: 도메인에 가입 하 고 도메인 계정 추가

지금까지 로컬 관리자 계정 (`<ComputerName>\Administrator`)으로 개별 서버를 구성 했습니다.

스토리지 공간 다이렉트를 관리 하려면 서버를 도메인에 가입 시키고 모든 서버에서 Administrators 그룹에 속한 Active Directory Domain Services 도메인 계정을 사용 해야 합니다.

관리 시스템에서 관리자 권한으로 PowerShell 콘솔을 엽니다. `Enter-PSSession`를 사용 하 여 각 서버에 연결 하 고 사용자 컴퓨터 이름, 도메인 이름 및 도메인 자격 증명을 대체 하 여 다음 cmdlet을 실행 합니다.

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

저장소 관리자 계정이 Domain Admins 그룹의 구성원이 아닌 경우 각 노드의 로컬 관리자 그룹에 저장소 관리자 계정을 추가 합니다. 또는 더 나은 저장소 관리자에 사용 하는 그룹을 추가 합니다. 다음 명령을 사용 하거나 Windows PowerShell 함수를 작성 하 여 수행할 수 있습니다. 자세한 내용은 [PowerShell을 사용 하 여 로컬 그룹에 도메인 사용자 추가](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx) 를 참조 하세요.

```
Net localgroup Administrators <Domain\Account> /add
```

### <a name="step-14-install-roles-and-features"></a>1\.4 단계: 역할 및 기능 설치

다음 단계는 모든 서버에 서버 역할을 설치 하는 것입니다. [Windows 관리 센터](../../manage/windows-admin-center/use/manage-servers.md), [서버 관리자](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)) 또는 PowerShell을 사용 하 여이 작업을 수행할 수 있습니다. 설치할 역할은 다음과 같습니다.

- 장애 조치(failover) 클러스터링
- Hyper-V
- 파일 서버 (수렴 형 배포와 같은 파일 공유를 호스트 하려는 경우)
- 데이터 센터 브리징(iWARP 네트워크 어댑터 대신 RoCEv2를 사용하는 경우)
- RSAT-클러스터링-PowerShell
- Hyper-V-PowerShell

PowerShell을 통해 설치 하려면 [add-windowsfeature](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature) cmdlet을 사용 합니다. 다음과 같이 단일 서버에서 사용할 수 있습니다.

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

클러스터의 모든 서버에서 명령을 동시에 실행 하려면이 작은 스크립트를 사용 하 여 스크립트의 시작 부분에 있는 변수 목록을 사용자 환경에 맞게 수정 합니다.

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"
$FeatureList = "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"

# This part runs the Install-WindowsFeature cmdlet on all servers in $ServerList, passing the list of features into the scriptblock with the "Using" scope modifier so you don't have to hard-code them here.
Invoke-Command ($ServerList) {
    Install-WindowsFeature -Name $Using:Featurelist
}
```

## <a name="step-2-configure-the-network"></a>2단계: 네트워크 구성

가상 컴퓨터 내 스토리지 공간 다이렉트을 배포 하는 경우이 섹션을 건너뜁니다.

스토리지 공간 다이렉트에는 클러스터의 서버 간에 고대역폭의 대기 시간이 짧은 네트워크가 필요 합니다. GbE 네트워킹은 10 개 이상 필요 하며 RDMA (원격 직접 메모리 액세스)를 사용 하는 것이 좋습니다. Windows Server 2016 로고가 있는 한 iWARP 또는 RoCE를 사용할 수 있지만 일반적으로 iWARP를 설정 하는 것이 더 쉽습니다.

> [!Important]
> 네트워킹 장비, 특히 RoCE v 2에 따라 랙 스위치의 일부 구성이 필요할 수 있습니다. 스토리지 공간 다이렉트의 안정성과 성능을 보장 하려면 올바른 스위치 구성이 중요 합니다.

Windows Server 2016에서는 Hyper-v 가상 스위치 내에 스위치 포함 팀 (집합)이 도입 되었습니다. 이렇게 하면 RDMA를 사용 하는 동안 모든 네트워크 트래픽에 동일한 실제 NIC 포트를 사용할 수 있으므로 필요한 실제 NIC 포트 수를 줄일 수 있습니다. 스위치 포함 팀은 스토리지 공간 다이렉트에 권장 됩니다.

스위치 또는 switchless 노드 상호 간의 상호 교환
- 전환 됨: 네트워크 스위치가 대역폭 및 네트워킹 유형을 처리 하도록 적절히 구성 되어 있어야 합니다. RoCE 프로토콜을 구현 하는 RDMA를 사용 하는 경우 네트워크 장치 및 스위치 구성이 훨씬 더 중요 합니다.
- Switchless: 직접 연결을 사용 하 여 노드를 상호 연결 하 여 스위치 사용을 방지할 수 있습니다. 모든 노드에서 클러스터의 다른 모든 노드에 직접 연결 해야 합니다.

스토리지 공간 다이렉트에 대 한 네트워킹을 설정 하는 지침은 [Windows Server 2016 수렴 형 NIC 및 게스트 RDMA 배포 가이드](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx)를 참조 하세요.

## <a name="step-3-configure-storage-spaces-direct"></a>3단계: 저장소 공간 다이렉트 구성

다음 단계는 구성 중인 서버와 동일한 버전의 관리 시스템에서 수행됩니다. 다음 단계는 PowerShell 세션을 사용 하 여 원격으로 실행 해서는 안 되며, 대신 관리 시스템의 로컬 PowerShell 세션에서 관리 권한을 사용 하 여 실행 해야 합니다.

### <a name="step-31-clean-drives"></a>3\.1 단계: 드라이브 청소

스토리지 공간 다이렉트를 사용 하도록 설정 하기 전에 드라이브가 비어 있는지 확인 합니다. 이전 파티션이나 기타 데이터는 없습니다. 컴퓨터 이름을 대체 하 여 다음 스크립트를 실행 하 여 모든 이전 파티션이나 기타 데이터를 제거 합니다.

> [!Warning]
> 이 스크립트는 운영 체제 부팅 드라이브가 아닌 다른 드라이브의 모든 데이터를 영구적으로 제거 합니다.

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"

Invoke-Command ($ServerList) {
    Update-StorageProviderCache
    Get-StoragePool | ? IsPrimordial -eq $false | Set-StoragePool -IsReadOnly:$false -ErrorAction SilentlyContinue
    Get-StoragePool | ? IsPrimordial -eq $false | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$false -ErrorAction SilentlyContinue
    Get-StoragePool | ? IsPrimordial -eq $false | Remove-StoragePool -Confirm:$false -ErrorAction SilentlyContinue
    Get-PhysicalDisk | Reset-PhysicalDisk -ErrorAction SilentlyContinue
    Get-Disk | ? Number -ne $null | ? IsBoot -ne $true | ? IsSystem -ne $true | ? PartitionStyle -ne RAW | % {
        $_ | Set-Disk -isoffline:$false
        $_ | Set-Disk -isreadonly:$false
        $_ | Clear-Disk -RemoveData -RemoveOEM -Confirm:$false
        $_ | Set-Disk -isreadonly:$true
        $_ | Set-Disk -isoffline:$true
    }
    Get-Disk | Where Number -Ne $Null | Where IsBoot -Ne $True | Where IsSystem -Ne $True | Where PartitionStyle -Eq RAW | Group -NoElement -Property FriendlyName
} | Sort -Property PsComputerName, Count
```

출력은 다음과 같이 표시 됩니다. 여기서 **Count** 는 각 서버의 각 모델에 대 한 드라이브 수입니다.

```
Count Name                          PSComputerName
----- ----                          --------------
4     ATA SSDSC2BA800G4n            Server01
10    ATA ST4000NM0033              Server01
4     ATA SSDSC2BA800G4n            Server02
10    ATA ST4000NM0033              Server02
4     ATA SSDSC2BA800G4n            Server03
10    ATA ST4000NM0033              Server03
4     ATA SSDSC2BA800G4n            Server04
10    ATA ST4000NM0033              Server04
```

### <a name="step-32-validate-the-cluster"></a>3\.2 단계: 클러스터 유효성 검사

이 단계에서는 클러스터 유효성 검사 도구를 실행 하 여 스토리지 공간 다이렉트를 사용 하 여 클러스터를 만들도록 서버 노드가 올바르게 구성 되어 있는지 확인 합니다. 클러스터를 만들기 전에 클러스터 유효성 검사 (`Test-Cluster`)를 실행 하면 구성이 장애 조치 (failover) 클러스터로 정상적으로 작동 하는 데 적합 한 것으로 표시 되는지 확인 하는 테스트를 실행 합니다. 아래 예제에서는 `-Include` 매개 변수를 사용한 다음 테스트의 특정 범주를 지정 합니다. 이렇게 하면 저장소 공간 다이렉트 관련 테스트가 유효성 검사에 포함됩니다.

다음 PowerShell 명령을 사용하여 저장소 공간 다이렉트 클러스터로 사용할 서버 집합의 유효성을 검사할 수 있습니다.

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### <a name="step-33-create-the-cluster"></a>3\.3 단계: 클러스터 만들기

이 단계에서는 다음 PowerShell cmdlet을 사용 하 여 이전 단계에서 클러스터 만들기에 대해 유효성을 검사 한 노드를 사용 하 여 클러스터를 만듭니다.

클러스터를 만들 때 "클러스터 된 역할을 만드는 동안 문제가 발생 하 여 시작 하지 못할 수 있습니다." 라는 경고가 표시 됩니다. 자세한 내용은 아래의 보고서 파일을 확인하십시오."라는 경고가 나타납니다. 이 경고를 안전 하 게 무시할 수 있습니다. 클러스터 쿼럼에 사용할 수 있는 디스크가 없기 때문에 나타나는 것입니다. 클러스터를 만든 후 파일 공유 감시 또는 클라우드 감시를 구성하는 것이 좋습니다.

> [!Note]
> 서버에서 고정 IP 주소를 사용하는 경우 다음 매개 변수를 추가하고 IP 주소 -StaticAddress &lt;X.X.X.X&gt;를 지정하여 고정 IP 주소를 반영하도록 다음 명령을 수정합니다.
> 다음 명령에서 ClusterName 자리 표시자는 고유하고 15자 이하인 netbios 이름으로 바꿔야 합니다.
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

클러스터를 만든 후 클러스터 이름에 대한 DNS 항목을 복제하는 데 약간의 시간이 걸릴 수 있습니다. 이 시간은 환경 및 DNS 복제 구성에 따라 달라집니다. 클러스터를 확인하지 못한 경우 대부분 클러스터 이름 대신 클러스터의 활성 구성원인 노드의 컴퓨터 이름을 사용하면 성공적으로 확인할 수 있습니다.

### <a name="step-34-configure-a-cluster-witness"></a>3\.4 단계: 클러스터 감시 구성

클러스터에 대해 미러링 모니터 서버를 구성 하는 것이 좋습니다. 따라서 서버가 3 대 이상인 클러스터는 두 서버에 장애가 발생 하거나 오프 라인 상태가 될 수 있습니다. 두 서버 배포에는 클러스터 미러링 모니터가 필요 합니다. 그렇지 않으면 오프 라인으로 전환 하는 서버에서 다른 서버를 사용할 수 없게 됩니다. 이러한 시스템에서는 파일 공유를 감시로 사용하거나 클라우드 감시를 사용할 수 있습니다. 

자세한 내용은 다음 항목을 참조하세요.

- [쿼럼 구성 및 관리](../../failover-clustering/manage-cluster-quorum.md)
- [장애 조치 (Failover) 클러스터용 클라우드 감시 배포](../../failover-clustering/deploy-cloud-witness.md)

### <a name="step-35-enable-storage-spaces-direct"></a>3\.5단계: 저장소 공간 다이렉트 사용

클러스터를 만든 후 `Enable-ClusterStorageSpacesDirect` PowerShell cmdlet을 사용 합니다 .이 cmdlet은 저장소 시스템을 스토리지 공간 다이렉트 모드로 전환 하 고 다음을 자동으로 수행 합니다.

-   **풀 만들기:** "S2D on Cluster1"과 같은 이름을 가진 대규모 단일 풀을 만듭니다.

-   **저장소 공간 다이렉트 캐시 구성:** 저장소 공간 다이렉트에 사용할 수 있는 미디어(드라이브) 유형이 2개 이상인 경우 가장 빠른 캐시 장치로 사용할 수 있습니다(대부분의 경우 읽기 및 쓰기).

-   **계층:** 두 계층을 기본 계층으로 만듭니다. 하나는 "Capacity"이고 다른 하나는 "Performance"입니다. Cmdlet은 장치를 분석한 후 장치 유형과 복원력을 조합하여 각 계층을 구성합니다.

관리 시스템에서 관리자 권한으로 PowerShell 명령 창을 열고 다음 명령을 시작합니다. 클러스터 이름은 이전 단계에서 만든 클러스터의 이름입니다. 이 명령을 노드 중 하나에서 로컬로 실행하면 -CimSession 매개 변수가 필요 없습니다.

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

위 명령을 통해 저장소 공간 다이렉트를 사용하려는 경우 클러스터 이름 대신 노드 이름을 사용할 수도 있습니다. 노드 이름을 사용하면 새로 만든 클러스터 이름에서 발생할 수 있는 DNS 복제 지연으로 인해 보다 안정적일 수 있습니다.

몇 분 후 이 명령이 완료되면 시스템이 볼륨을 만들 수 있도록 준비됩니다.

### <a name="step-36-create-volumes"></a>3\.6단계: 볼륨 만들기

`New-Volume` cmdlet은 가장 빠르고 가장 간단한 환경을 제공 하므로 사용 하는 것이 좋습니다. 이 단일 cmdlet은 가상 디스크를 자동으로 만들어서 분할 및 포맷하고, 이와 일치하는 이름으로 볼륨을 만들어 클러스터 공유 볼륨에 추가합니다. 이 모든 과정이 하나의 간편한 단계만으로 진행됩니다.

자세한 내용은 [저장소 공간 다이렉트에서 볼륨 만들기](create-volumes.md)를 참조하세요.

### <a name="step-37-optionally-enable-the-csv-cache"></a>3\.7 단계: CSV 캐시를 선택적으로 사용 하도록 설정

필요에 따라 CSV (클러스터 공유 볼륨) 캐시가 Windows cache manager에서 아직 캐시 되지 않은 읽기 작업의 쓰기 블록 수준 캐시로 시스템 메모리 (RAM)를 사용 하도록 설정할 수 있습니다. 이렇게 하면 Hyper-v와 같은 응용 프로그램의 성능을 향상 시킬 수 있습니다. CSV 캐시는 읽기 요청의 성능을 높일 수 있으며 스케일 아웃 파일 서버 시나리오에도 유용 합니다.

CSV 캐시를 사용 하도록 설정 하면 하이퍼 수렴 형 클러스터에서 Vm을 실행 하는 데 사용할 수 있는 메모리의 양이 줄어들기 때문에 Vhd에서 사용할 수 있는 메모리와 저장소 성능의 균형을 유지 해야 합니다.

CSV 캐시의 크기를 설정 하려면 저장소 클러스터에 대 한 관리자 권한이 있는 계정을 사용 하 여 관리 시스템에서 PowerShell 세션을 연 다음이 스크립트를 사용 하 여 `$ClusterName` 및 `$CSVCacheSize` 변수를 적절 하 게 변경 합니다 .이 예제에서는 서버당 2gb CSV 캐시를 설정 합니다.

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

자세한 내용은 [CSV 메모리 내 읽기 캐시 사용](csv-cache.md)을 참조 하세요.

### <a name="step-38-deploy-virtual-machines-for-hyper-converged-deployments"></a>3\.8 단계: 하이퍼 수렴 형 배포를 위한 가상 머신 배포

하이퍼 수렴 형 클러스터를 배포 하는 경우 마지막 단계는 스토리지 공간 다이렉트 클러스터에서 가상 컴퓨터를 프로 비전 하는 것입니다.

가상 컴퓨터의 파일은 장애 조치 (failover) 클러스터의 클러스터형 Vm과 마찬가지로 시스템 CSV 네임 스페이스 (예: c:\\ClusterStorage\\Volume1)에 저장 되어야 합니다.

기본 도구 또는 다른 도구를 사용 하 여 System Center Virtual Machine Manager와 같은 저장소 및 가상 컴퓨터를 관리할 수 있습니다.

## <a name="step-4-deploy-scale-out-file-server-for-converged-solutions"></a>4 단계: 수렴 형 솔루션에 대 한 스케일 아웃 파일 서버 배포

수렴 형 솔루션을 배포 하는 경우 다음 단계는 스케일 아웃 파일 서버 인스턴스를 만들고 일부 파일 공유를 설정 하는 것입니다. 하이퍼 수렴 형 클러스터를 배포 하는 경우 완료 되며이 섹션이 필요 하지 않습니다.

### <a name="step-41-create-the-scale-out-file-server-role"></a>4\.1 단계: 스케일 아웃 파일 서버 역할 만들기

파일 서버에 대 한 클러스터 서비스를 설정 하는 다음 단계에서는 클러스터 된 파일 서버 역할을 만듭니다 .이 역할은 지속적으로 사용 가능한 파일 공유가 호스트 되는 스케일 아웃 파일 서버 인스턴스를 만들 때 사용 됩니다.

#### <a name="to-create-a-scale-out-file-server-role-by-using-server-manager"></a>서버 관리자를 사용 하 여 스케일 아웃 파일 서버 역할을 만들려면

1. 장애 조치(Failover) 클러스터 관리자에서 클러스터를 선택 하 고 **역할**로 이동한 다음 **역할 구성**...을 클릭 합니다.<br>고가용성 마법사가 나타납니다.
2. **역할 선택** 페이지에서 **파일 서버**를 클릭 합니다.
3. **파일 서버 유형** 페이지에서 **응용 프로그램 데이터에 대 한 스케일 아웃 파일 서버**를 클릭 합니다.
4. **클라이언트 액세스 지점** 페이지에서 스케일 아웃 파일 서버의 이름을 입력 합니다.
5. 그림 1에 나와 있는 것 **처럼 역할로 이동 하 고** **상태** 열이 만든 클러스터 된 파일 서버 역할 옆의 **실행 중** 으로 표시 되는지 확인 하 여 역할이 성공적으로 설정 되었는지 확인 합니다.

   (media/Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016/SOFS_in_FCM.png "스케일 아웃 파일 서버를 표시 하 장애 조치(Failover) 클러스터 관리자") ![스케일 아웃 파일 서버를 보여 주는 장애 조치(Failover) 클러스터 관리자의 스크린샷]

    **그림 1** 실행 상태가 스케일 아웃 파일 서버를 표시 하 장애 조치(Failover) 클러스터 관리자

> [!NOTE]
>  클러스터 된 역할을 만든 후 몇 분 또는 그 이상에 대 한 파일 공유를 만들 수 없게 하는 네트워크 전파 지연이 발생할 수 있습니다.  
  
#### <a name="to-create-a-scale-out-file-server-role-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 스케일 아웃 파일 서버 역할을 만들려면

 파일 서버 클러스터에 연결 된 Windows PowerShell 세션에서 다음 명령을 입력 하 여 스케일 아웃 파일 서버 역할을 만들고, 클러스터 이름과 일치 하도록 *Fscluster* 를 변경 하 고, 스케일 아웃 파일 서버 역할에 부여할 이름과 일치 하도록 *SOFS* 합니다.

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  클러스터 된 역할을 만든 후 몇 분 또는 그 이상에 대 한 파일 공유를 만들 수 없게 하는 네트워크 전파 지연이 발생할 수 있습니다. SOFS 역할이 즉시 실패 하 고 시작 되지 않으면 클러스터의 컴퓨터 개체에 SOFS 역할에 대 한 컴퓨터 계정을 만들 수 있는 권한이 없기 때문일 수 있습니다. 이에 대 한 도움이 필요한 경우이 블로그 게시물을 참조 하세요. [스케일 아웃 파일 서버 역할은 이벤트 id 1205, 1069 및 1194로 시작 하지 못합니다](http://www.aidanfinn.com/?p=14142).

### <a name="step-42-create-file-shares"></a>4\.2 단계: 파일 공유 만들기

가상 디스크를 만들고 Csv에 추가한 후에는 가상 디스크당 CSV 당 하나의 파일 공유에서 파일 공유를 만들 수 있습니다. System Center Virtual Machine Manager (VMM)은 사용자에 대 한 권한을 처리 하기 때문에이 작업을 수행 하는 handiest입니다. 하지만 환경에 없는 경우 Windows PowerShell을 사용 하 여 배포를 부분적으로 자동화할 수 있습니다.

[Hyper-v 작업에 대 한 SMB 공유 구성](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) 에 포함 된 스크립트를 사용 합니다 .이 스크립트는 그룹 및 공유 만들기 프로세스를 부분적으로 자동화 합니다. Hyper-v 작업에 맞게 작성 되었으므로 다른 작업을 배포 하는 경우에는 공유를 만든 후 설정을 수정 하거나 추가 단계를 수행 해야 할 수 있습니다. 예를 들어 Microsoft SQL Server를 사용 하는 경우 SQL Server 서비스 계정에 공유 및 파일 시스템에 대 한 모든 권한을 부여 해야 합니다.

> [!NOTE]
>  System Center Virtual Machine Manager를 사용 하 여 공유를 만들지 않는 한 클러스터 노드를 추가할 때 그룹 멤버 자격을 업데이트 해야 합니다.

PowerShell 스크립트를 사용 하 여 파일 공유를 만들려면 다음을 수행 합니다.

1. [Hyper-v 작업에 대 한 SMB 공유 구성](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) 에 포함 된 스크립트를 파일 서버 클러스터의 노드 중 하나에 다운로드 합니다.
2. 관리 시스템에서 도메인 관리자 자격 증명을 사용 하 여 Windows PowerShell 세션을 열고 다음 스크립트를 사용 하 여 Hyper-v 컴퓨터 개체에 대 한 Active Directory 그룹을 만들고 해당 변수의 값을 개발

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. 저장소 노드 중 하나에서 관리자 자격 증명을 사용 하 여 Windows PowerShell 세션을 열고 다음 스크립트를 사용 하 여 각 CSV에 대 한 공유를 만들고 도메인 관리자 그룹 및 계산 클러스터에 대 한 공유에 대 한 관리 권한을 부여 합니다.

    ```PowerShell
    # Replace the values of these variables
    $StorageClusterName = "StorageSpacesDirect1"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $SOFSName = "SOFS"
    $SharePrefix = "Share"
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of the script itself
    CD $ScriptFolder
    Get-ClusterSharedVolume -Cluster $StorageClusterName | ForEach-Object
    {
        $ShareName = $SharePrefix + $_.SharedVolumeInfo.friendlyvolumename.trimstart("C:\ClusterStorage\Volume")
        Write-host "Creating share $ShareName on "$_.name "on Volume: " $_.SharedVolumeInfo.friendlyvolumename
        .\FileShareSetup.ps1 -HyperVClusterName $StorageClusterName -CSVVolumeNumber $_.SharedVolumeInfo.friendlyvolumename.trimstart("C:\ClusterStorage\Volume") -ScaleOutFSName $SOFSName -ShareName $ShareName -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName
    }
    ```

### <a name="step-43-enable-kerberos-constrained-delegation"></a>4\.3 단계 Kerberos 제한 된 위임 사용

저장소 클러스터 노드 중 하나에서 원격 시나리오 관리에 대해 Kerberos 제한 위임을 설정 하 고 실시간 마이그레이션 보안을 강화 하려면 [Hyper-v 작업에 대 한 SMB 공유 구성](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)에 포함 된 KCDSetup 스크립트를 사용 합니다. 스크립트에 대 한 간단한 래퍼는 다음과 같습니다.

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## <a name="next-steps"></a>다음 단계

클러스터 된 파일 서버를 배포한 후에는 실제 워크 로드를 가져오기 전에 가상 워크 로드를 사용 하 여 솔루션의 성능을 테스트 하는 것이 좋습니다. 이렇게 하면 솔루션이 제대로 수행 되 고 있는지 확인 하 고 작업의 복잡성을 추가 하기 전에 모든 느린 문제를 해결할 수 있습니다. 자세한 내용은 [가상 워크 로드를 사용 하 여 저장소 공간 성능 테스트](https://technet.microsoft.com/library/dn894707.aspx)를 참조 하세요.

## <a name="see-also"></a>참고 항목

-   [Windows Server 2016의 스토리지 공간 다이렉트](storage-spaces-direct-overview.md)
-   [스토리지 공간 다이렉트 캐시 이해](understand-the-cache.md)
-   [스토리지 공간 다이렉트에서 볼륨 계획](plan-volumes.md)
-   [저장소 공간 내결함성](storage-spaces-fault-tolerance.md)
-   [하드웨어 요구 사항 스토리지 공간 다이렉트](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [RDMA, or not to RDMA – that is the question(RDMA 선택 결정 문제)](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/)(TechNet 블로그)
