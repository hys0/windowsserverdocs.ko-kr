---
title: 저장소 공간 다이렉트 배포
ms.prod: windows-server-threshold
manager: eldenc
ms.author: stevenek
ms.technology: storage-spaces
ms.topic: get-started-article
ms.assetid: 20fee213-8ba5-4cd3-87a6-e77359e82bc0
author: stevenek
ms.date: 8/16/2018
description: Windows Server에서 저장소 공간 다이렉트를 사용 하 여 소프트웨어 정의 저장소 하이퍼 수렴 형 인프라 또는 (세분화 라고도) 수렴 형된 인프라 배포에 대 한 단계별 지침입니다.
ms.localizationpriority: medium
ms.openlocfilehash: 55cfa0e066506d7174f9e5b1e61cc0aa290706d7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865414"
---
# <a name="deploy-storage-spaces-direct"></a>저장소 공간 다이렉트 배포

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 배포 하는 단계별 지침은 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)합니다.

> [!Tip]
> Hyper-Converged 인프라를 획득 하려고 하나요? 이러한 것이 좋습니다 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd) 파트너의 솔루션입니다. 이러한 설계, 조립 및 호환성 및 안정성 얻게 되므로 신속 하 게 실행 하기 위한이 참조 아키텍처에 대해 유효성을 검사 합니다.

> [!Tip]
> Hyper-v 가상 컴퓨터를 포함 하 여 Microsoft Azure에 사용할 수 있습니다 [하드웨어 없이 저장소 공간 다이렉트를 평가](storage-spaces-direct-in-vm.md)합니다. 유용한 검토할 수도 있습니다 [Windows Server 빠른 랩 배포 스크립트](https://aka.ms/wslab), 학습 용도로 사용 합니다.

## <a name="before-you-start"></a>시작하기 전 주의 사항

검토 합니다 [저장소 공간 다이렉트 하드웨어 요구 사항](Storage-Spaces-Direct-Hardware-Requirements.md) 일부 단계와 관련 된 중요 한 참고 사항 고 전체 접근 방식을 사용 하 여 잘 이해 하려면이 문서를 가볍게 보고 및 합니다.

다음 정보를 수집 합니다.

- **배포 옵션입니다.** 저장소 공간 다이렉트 지원 [두 가지 배포 옵션: 수렴 형 및 하이퍼 수렴 형](storage-spaces-direct-overview.md#deployment-options), 세분화 라고도 합니다. 적합 한 것을 결정 하려면 각 응용 프로그램의 장점을 숙지 해야 합니다. 단계 1-3 아래 배포 옵션을 모두 적용 됩니다. 4 단계는 수렴 형된 배포만 필요 합니다.

- **서버 이름입니다.** 컴퓨터, 파일, 경로 및 기타 리소스에 대 한 조직의 명명 정책 개념을 익혀야 합니다. 각 고유한 이름을 사용 하 여 여러 서버를 프로 비전 해야 합니다.

- **도메인 이름입니다.** 도메인 이름 지정 및 도메인 가입에 대 한 조직의 정책을 개념을 익혀야 합니다.  있습니다 수 가입 될 서버를 도메인에 도메인 이름을 지정 해야 하며 

- **RDMA 네트워킹입니다.** 두 가지 유형의 RDMA 프로토콜이 가지: iWarp 및 RoCE. 어떤 네트워크 어댑터 사용을 경우 RoCE를 참고 ((v1 또는 v2) 버전도 있습니다. RoCE를-top-of-rack 스위치의 모델을 note도 합니다.

- **VLAN ID.** 있는 경우 서버에서 운영 체제 관리 네트워크 어댑터에 사용할 VLAN ID를 note 합니다. 네트워크 관리자로부터 얻을 수 있습니다.

## <a name="step-1-deploy-windows-server"></a>1단계: Windows Server 배포

### <a name="step-11-install-the-operating-system"></a>1.1 단계: 운영 체제 설치

먼저는 Windows 서버 클러스터 포함에서 될 모든 서버에 설치 하는 것입니다. 저장소 공간 다이렉트는 Windows Server 2016 Datacenter Edition 필요합니다. 데스크톱 환경 포함 서버를 Server Core 설치 옵션을 사용할 수 있습니다.

설치 마법사를 사용 하 여 Windows Server를 설치할 때 선택할 수 있습니다 *Windows Server* (Server Core 참조) 및 *Windows Server (데스크톱 환경 포함 서버)* 에 해당 하는 *전체* 설치 옵션 Windows Server 2012 R2에서 사용할 수 있습니다. 선택 하지 않으면 Server Core 설치 옵션을 얻게 됩니다. 자세한 내용은 [Windows Server 2016의 설치 옵션에 대 한](../../get-started/Windows-Server-2016.md)합니다.

### <a name="step-12-connect-to-the-servers"></a>1.2 단계: 서버에 연결

이 가이드에서는 Server Core 설치 옵션 및 이어야 하는 별도 관리 시스템에서 원격으로 배포/관리 중점을 둡니다.

- 관리 서버와 동일한 업데이트를 사용 하 여 Windows Server 2016
- 관리 하는 서버에 대 한 네트워크 연결
- 동일한 도메인 또는 완전히 트러스트 된 도메인에 가입
- Hyper-V 및 장애 조치(failover) 클러스터링용 PowerShell 모듈 및 RSAT(원격 서버 관리 도구) RSAT 도구 및 PowerShell 모듈 Windows Server에서 사용할 수 있으며 다른 기능을 설치 하지 않고도 설치할 수 있습니다. 설치할 수도 있습니다는 [원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520) 를 Windows 10 PC 관리 합니다.

관리 시스템에서 장애 조치(failover) 클러스터 및 Hyper-V 관리 도구를 설치합니다. 서버 관리자에서 **역할 및 기능 추가** 마법사를 사용하여 이 작업을 수행할 수 있습니다. **기능** 페이지에서 **원격 서버 관리 도구**를 선택한 다음 설치할 도구를 선택합니다.

PS 세션을 입력하고 서버 이름 또는 연결하려는 노드의 IP 주소를 사용합니다. 수 Windows를 설정할 때 지정한 관리자 암호 입력이 명령을 실행 하면 암호를 입력 합니다.

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   이 작업을 두 번 이상 수행 해야 하는 경우 스크립트에서 보다 유용한 방식에서 동일한 작업을 수행 하는 예는 다음과 같습니다.

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> 관리 시스템에서 원격으로 배포 하는 경우 다음과 같은 오류가 발생할 수 있습니다 *WinRM 요청을 처리할 수 없습니다.* 이 문제를 해결 하려면 관리 컴퓨터에 신뢰할 수 있는 호스트 목록에 각 서버를 추가 하려면 Windows PowerShell을 사용 합니다.  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> 참고: 신뢰할 수 있는 호스트 목록에서 와일드 카드를 같은 `Server*`합니다.
>
> 신뢰할 수 있는 호스트 목록에서 보려는 입력 `Get-Item WSMAN:\Localhost\Client\TrustedHosts`합니다.  
>   
> 입력 목록 비어 `Clear-Item WSMAN:\Localhost\Client\TrustedHost`합니다.  

### <a name="step-13-join-the-domain-and-add-domain-accounts"></a>1.3 단계: 도메인에 가입 하 고 도메인 계정 추가

로컬 관리자 계정을 사용 하 여 개별 서버를 구성 했으므로 지금 `<ComputerName>\Administrator`합니다.

저장소 공간 다이렉트를 관리 하려면 서버를 도메인에 가입 하 여 모든 서버에서 Administrators 그룹에 있는 Active Directory Domain Services 도메인 계정을 사용 해야 합니다.

관리 시스템에서 관리자 권한으로 PowerShell 콘솔을 엽니다. 사용 하 여 `Enter-PSSession` 각 서버에 연결 하 고 고유한 컴퓨터 이름, 도메인 이름 및 도메인 자격 증명을 대체 하 여 다음 cmdlet을 실행 합니다.

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

저장소 관리자 계정이 Domain Admins 그룹의 멤버인 되지 않으면, 저장소 관리자 계정-각 노드에서 로컬 관리자 그룹에 추가 또는 더 나아가 저장소 관리자를 사용 하는 그룹을 추가 합니다. 다음 명령을 사용할 수 있습니다 (이렇게 하려면 참조는 Windows PowerShell 함수를 작성 하거나 [로컬 그룹에 도메인 사용자를 추가 하려면 PowerShell을 사용 하 여](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx) 자세한):

```
Net localgroup Administrators <Domain\Account> /add
```

### <a name="step-14-install-roles-and-features"></a>1.4 단계: 역할 및 기능 설치

다음 단계는 모든 서버의 서버 역할을 설치 하는 것입니다. 사용 하 여이 수행할 수 있습니다 [Windows Admin Center](../../manage/windows-admin-center/use/manage-servers.md)를 [서버 관리자](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md))에서 또는 PowerShell입니다. 역할 설치는 다음과 같습니다.

- 장애 조치(failover) 클러스터링
- Hyper-V
- 파일 서버 (예: 수렴 형된 배포를 모든 파일 공유를 호스트 하려는) 하는 경우
- 데이터 센터 브리징(iWARP 네트워크 어댑터 대신 RoCEv2를 사용하는 경우)
- RSAT-클러스터링-PowerShell
- Hyper-V-PowerShell

PowerShell을 통해 설치 하려면 사용 합니다 [Install-windowsfeature](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature) cmdlet. 다음과 같은 단일 서버에 사용할 수 있습니다.

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

한 번으로 클러스터의 모든 서버에서 명령을 실행 하려면이 약간의 스크립트를 환경에 맞게 스크립트의 시작 부분에서 변수 목록이 수정를 사용 합니다.

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

저장소 공간 다이렉트 가상 컴퓨터 내에서 배포 하는, 하는 경우이 섹션을 건너뜁니다.

저장소 공간 다이렉트는 높은 대역폭, 지연율이 낮은 클러스터의 서버 간 네트워킹 필요 합니다. 최소 10 GbE 네트워킹 필수 항목이 며 원격 직접 메모리 액세스 (RDMA)를 사용 하는 것이 좋습니다. Windows Server 2016 로고를 갖지만 iWARP는 일반적으로 쉽게 설정할 수 있다면 iWARP 또는 RoCE 중 하나를 사용할 수 있습니다.

> [!Important]
> 네트워킹 장비에 따라 및 RoCE v2를 사용 하 여 특히-top-of-rack 스위치의 몇 가지 구성이 필요할 수 있습니다. 올바른 스위치 구성은 저장소 공간 다이렉트의 안정성 및 성능을 확인 해야 합니다.

Windows Server 2016에서는 스위치 포함 된 팀 (SET) 내에서 Hyper-v 가상 스위치를 소개합니다. 따라서 동일한 물리적 NIC 포트가 필요한 물리적 NIC 포트의 수를 줄이면 RDMA를 사용 하는 동안 모든 네트워크 트래픽에 사용할 수 있습니다. 저장소 공간 다이렉트에 대 한 스위치 포함 팀 것이 좋습니다.

저장소 공간 다이렉트에 대 한 네트워킹을 설정 하는 지침은 참조 하세요 [Windows Server 2016 수렴 된 NIC 및 게스트 RDMA 배포 가이드](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx)합니다.

## <a name="step-3-configure-storage-spaces-direct"></a>3단계: 저장소 공간 다이렉트 구성

다음 단계는 구성 중인 서버와 동일한 버전의 관리 시스템에서 수행됩니다. 다음 단계를 야 원격 PowerShell 세션을 사용 하 여 실행 하지만 로컬 PowerShell 세션에서 관리자 권한으로 관리 시스템에서 대신 실행 합니다.

### <a name="step-31-clean-drives"></a>3.1 단계: 드라이브 청소

저장소 공간 다이렉트를 사용 하기 전에 비어 있는 드라이브 확인: 이전 파티션이 없는 또는 기타 데이터. 이전 모든 파티션 또는 기타 데이터를 제거 하 여 컴퓨터 이름을 대체 하 여 다음 스크립트를 실행 합니다.

> [!Warning]
> 이 스크립트는 운영 체제 부팅 드라이브 이외의 모든 드라이브의 모든 데이터가 영구적으로 제거 됩니다!

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

출력은 다음과 유사 합니다 위치 **개수** 각 서버에서 각 모델의 드라이브입니다.

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

### <a name="step-32-validate-the-cluster"></a>3.2 단계: 클러스터 유효성 검사

이 단계에서는 서버 노드가 저장소 공간 다이렉트를 사용 하 여 클러스터를 만들려면 올바르게 구성 되었는지 확인 하려면 클러스터 유효성 검사 도구를 실행할 수 있습니다. 경우 클러스터 유효성 검사 (`Test-Cluster`)가 구성을 성공적으로 장애 조치 클러스터로 작동 하는 데 적합 표시 되는지 확인 하는 테스트를 실행할 클러스터를 만들기 전에 실행 합니다. 사용 하 여 바로 위의 예에서 `-Include` 매개 변수를 특정 테스트 범주가 지정 됩니다. 이렇게 하면 저장소 공간 다이렉트 관련 테스트가 유효성 검사에 포함됩니다.

다음 PowerShell 명령을 사용하여 저장소 공간 다이렉트 클러스터로 사용할 서버 집합의 유효성을 검사할 수 있습니다.

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### <a name="step-33-create-the-cluster"></a>3.3 단계: 클러스터 만들기

이 단계에서는 다음 PowerShell cmdlet을 사용 하 여 이전 단계에서 클러스터 만들기에 대 한 유효성을 검사 해야 하는 노드를 사용 하 여 클러스터를 만들어야 합니다.

클러스터를 만들 때 상태는 경고를 받게-"문제가 있었습니다는 클러스터 된 역할을 만들 수 있어 시작 하는 동안. 자세한 내용은 아래의 보고서 파일을 확인하십시오."라는 경고가 나타납니다. 이 경고를 안전 하 게 무시할 수 있습니다. 클러스터 쿼럼에 사용할 수 있는 디스크가 없기 때문에 나타나는 것입니다. 클러스터를 만든 후 파일 공유 감시 또는 클라우드 감시를 구성하는 것이 좋습니다.

> [!Note]
> 서버에서 고정 IP 주소를 사용하는 경우 다음 매개 변수를 추가하고 IP 주소 -StaticAddress &lt;X.X.X.X&gt;를 지정하여 고정 IP 주소를 반영하도록 다음 명령을 수정합니다.
> 다음 명령에서 ClusterName 자리 표시자는 고유하고 15자 이하인 netbios 이름으로 바꿔야 합니다.
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

클러스터를 만든 후 클러스터 이름에 대한 DNS 항목을 복제하는 데 약간의 시간이 걸릴 수 있습니다. 이 시간은 환경 및 DNS 복제 구성에 따라 달라집니다. 클러스터를 확인하지 못한 경우 대부분 클러스터 이름 대신 클러스터의 활성 구성원인 노드의 컴퓨터 이름을 사용하면 성공적으로 확인할 수 있습니다.

### <a name="step-34-configure-a-cluster-witness"></a>3.4 단계: 클러스터 감시 구성

3 개 이상의 서버를 사용 하 여 클러스터에 두 서버가 실패 하거나 오프 라인 견딜 수 있도록 클러스터에 대 한 미러링 모니터 서버를 구성 하는 것이 좋습니다. 클러스터 감시 두 서버 배포에서는 그렇지 않은 경우 서버 중 하나의 오프 라인으로 전환 하면 다른도 사용할 수 없습니다. 이러한 시스템에서는 파일 공유를 감시로 사용하거나 클라우드 감시를 사용할 수 있습니다. 

자세한 내용은 다음 항목을 참조하세요.

- [구성 및 쿼럼 관리](../../failover-clustering/manage-cluster-quorum.md)
- [장애 조치 클러스터에 대 한 클라우드 감시 배포](../../failover-clustering/deploy-cloud-witness.md)

### <a name="step-35-enable-storage-spaces-direct"></a>3.5 단계: 저장소 공간 다이렉트 사용

클러스터를 만든 후 사용 된 `Enable-ClusterStorageSpacesDirect` 저장소 시스템이 저장소 공간 다이렉트 모드로 설정 되며 자동으로 다음을 수행 하는 PowerShell cmdlet:

-   **풀을 만듭니다.** "S2D에서 Cluster1" 같은 이름을 가진 대규모 단일 풀을 만듭니다.

-   **저장소 공간 다이렉트 캐시를 구성합니다.** 형식이 없는 경우 둘 이상의 미디어 (드라이브) 저장소 공간 다이렉트에 사용할 수 있는, 수 있도록 가장 빠른 캐시 장치로 (읽기 및 쓰기 대부분의 경우)

-   **계층:** 기본 계층으로 두 계층을 만듭니다. 하나는 "Capacity"이고 다른 하나는 "Performance"입니다. Cmdlet은 장치를 분석한 후 장치 유형과 복원력을 조합하여 각 계층을 구성합니다.

관리 시스템에서 관리자 권한으로 PowerShell 명령 창을 열고 다음 명령을 시작합니다. 클러스터 이름은 이전 단계에서 만든 클러스터의 이름입니다. 이 명령을 노드 중 하나에서 로컬로 실행하면 -CimSession 매개 변수가 필요 없습니다.

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

위 명령을 통해 저장소 공간 다이렉트를 사용하려는 경우 클러스터 이름 대신 노드 이름을 사용할 수도 있습니다. 노드 이름을 사용하면 새로 만든 클러스터 이름에서 발생할 수 있는 DNS 복제 지연으로 인해 보다 안정적일 수 있습니다.

몇 분 후 이 명령이 완료되면 시스템이 볼륨을 만들 수 있도록 준비됩니다.

### <a name="step-36-create-volumes"></a>3.6 단계: 볼륨 만들기

사용 하는 것이 좋습니다는 `New-Volume` cmdlet으로 가장 빠르고 가장 간단한 환경을 제공 합니다. 이 단일 cmdlet은 가상 디스크를 자동으로 만들어서 분할 및 포맷하고, 이와 일치하는 이름으로 볼륨을 만들어 클러스터 공유 볼륨에 추가합니다. 이 모든 과정이 하나의 간편한 단계만으로 진행됩니다.

자세한 내용은 [저장소 공간 다이렉트에서 볼륨 만들기](create-volumes.md)를 참조하세요.

### <a name="step-37-optionally-enable-the-csv-cache"></a>3.7 단계: 필요에 따라 CSV 캐시를 사용 하도록 설정

필요에 따라 시스템 메모리 (RAM)를 사용 하 여 이미 Windows 캐시 관리자가 캐시 되지 않은 읽기 작업의 쓰기 블록 수준 캐시를 클러스터 공유 볼륨 (CSV) 캐시를 사용할 수 있습니다. Hyper-v와 같은 응용 프로그램의 성능을 향상 시킬 수 있습니다이 있습니다. CSV 캐시 읽기 요청의 성능을 높일 수 있습니다 및 스케일 아웃 파일 서버 시나리오에도 유용 합니다.

CSV 캐시를 사용 하도록 설정 하면 Vhd를 사용할 수 있는 메모리를 사용 하 여 저장소 성능을 균형을 유지 해야 하므로 하이퍼 수렴 형 클러스터에서 Vm을 실행할 수 있는 메모리의 양을 줄일 수 있습니다.

CSV 캐시의 크기를 설정 하려면 관리 시스템에서 PowerShell 세션을 저장소 클러스터에 대 한 관리자 권한이 있는 계정으로 열고 사용 하 여이 스크립트를 변경 합니다 `$ClusterName` 및 `$CSVCacheSize` 변수 (이 적절 한 대로 예제 설정 서버당 2 GB CSV 캐시).

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

자세한 내용은 참조 하세요. [읽기 캐시를 CSV에 메모리를 사용 하 여](csv-cache.md)입니다.

### <a name="step-38-deploy-virtual-machines-for-hyper-converged-deployments"></a>3.8 단계 하이퍼 수렴 형 배포에 대 한 가상 컴퓨터 배포

하이퍼 수렴 형 클러스터에 배포 하는 경우 저장소 공간 다이렉트 클러스터에서 가상 머신을 프로 비전 하는 마지막 단계가입니다.

가상 머신의 파일 시스템 CSV 네임 스페이스에 저장 되어야 합니다 (예: c:\\ClusterStorage\\Volume1) 장애 조치 클러스터에서 클러스터 된 Vm과 마찬가지로 합니다.

저장소 및 가상 컴퓨터, System Center Virtual Machine Manager 같은 관리 도구 또는 기타 도구를 사용할 수 있습니다.

## <a name="step-4-deploy-scale-out-file-server-for-converged-solutions"></a>4단계: 수렴 형된 솔루션에 대 한 스케일 아웃 파일 서버 배포

수렴 형된 솔루션을 구축 하는 경우 스케일 아웃 파일 서버 인스턴스를 만들고 일부 파일 공유를 설정 하는 다음 단계가입니다. 이 과정을 완료 하 고 필요 하지 않습니다 하는 하이퍼 수렴 형 클러스터를 배포 하는 경우 섹션입니다.

### <a name="step-41-create-the-scale-out-file-server-role"></a>4.1 단계: 스케일 아웃 파일 서버 역할 만들기

파일 서버의 클러스터 서비스 설정에서 다음 단계는 지속적으로 사용 가능한 파일 공유에 호스트 되는 스케일 아웃 파일 서버 인스턴스를 만들 때 클러스터 된 파일 서버 역할을 만드는 것입니다.

#### <a name="to-create-a-scale-out-file-server-role-by-using-server-manager"></a>서버 관리자를 사용 하 여 스케일 아웃 파일 서버 역할을 만들려면

1.  장애 조치 클러스터 관리자에서 클러스터를 선택로 이동 **역할**를 클릭 하 고 **역할 구성...** .<br>고가용성 마법사에 표시 됩니다.
2.  에 **역할 선택** 페이지에서 클릭 **파일 서버**합니다.
3.  에 **파일 서버 유형** 페이지에서 클릭 **응용 프로그램 데이터용 스케일 아웃 파일 서버**합니다.
4.  에 **클라이언트 액세스 지점** 페이지에서 스케일 아웃 파일 서버에 대 한 이름을 입력 합니다.
5.  역할이로 이동 하 여 성공적으로 설정 되었는지 확인 **역할** 지 확인 하는 및를 **상태** 열에 표시 **실행** 만든 클러스터 된 파일 서버 역할 옆에 있는 그림 1 에서처럼.

    ![스크린 샷 장애 조치 클러스터 관리자의 스케일 아웃 파일 서버를 보여 주는](media\Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016\SOFS_in_FCM.png "스케일 아웃 파일 서버 장애 조치 클러스터 관리자")

     **그림 1** 실행 상태를 사용 하 여 스케일 아웃 파일 서버를 보여 주는 장애 조치 클러스터 관리자

> [!NOTE]
>  클러스터 된 역할을 만든 후 있을 일부 네트워크 전파 지연을 몇 분 이상 동안 잠재적으로 파일 공유를 만들지 못하게 방지할 수 있는.  
  
#### <a name="to-create-a-scale-out-file-server-role-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 스케일 아웃 파일 서버 역할을 만들려면

 파일 서버 클러스터에 연결 되어 있는 Windows PowerShell 세션에서 다음 명령을 입력 합니다 변경 스케일 아웃 파일 서버 역할을 만들 *FSCLUSTER* 클러스터의 이름과 일치 하도록 및 *SOFS* 스케일 아웃 파일 서버 역할을 부여 하려는 이름과 일치 하도록 합니다.

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  클러스터 된 역할을 만든 후 있을 일부 네트워크 전파 지연을 몇 분 이상 동안 잠재적으로 파일 공유를 만들지 못하게 방지할 수 있는. 즉시 실패 하 고 시작 되지 않습니다 하는 SOFS 역할을 하는 경우 클러스터의 컴퓨터 개체 SOFS 역할에 대 한 컴퓨터 계정을 만들 수 있는 권한이 없는 때문일 수 있습니다. 에 대 한 데 도움이 되는 참조를 사용 하 여이 블로그 게시물: [스케일 아웃 파일 서버 역할에 오류가 발생 1205, 1069, 및 1194 이벤트 Id 사용 하 여 시작](http://www.aidanfinn.com/?p=14142)합니다.

### <a name="step-42-create-file-shares"></a>4.2 단계: 파일 공유 만들기

후 가상 디스크를 만들고 Csv에 추가 했을 것이 하나의 파일 공유를 CSV 당 가상 디스크당 있으며에서 파일 공유를 만들 시간입니다. System Center Virtual Machine Manager (VMM) 환경의 없는, 하는 경우 부분적으로 배포를 자동화 하려면 Windows PowerShell을 사용할 수 있습니다,에 대 한 권한을 처리 하므로이 작업을 수행 하는 편리한 방법은 때문일 수 있습니다.

에 포함 된 스크립트를 사용 합니다 [Hyper-v 워크 로드에 대 한 SMB 공유 구성을](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) 부분적으로 그룹 및 공유를 만드는 과정을 자동화 하는 스크립트입니다. Hyper-v 워크 로드에 대해 작성 하므로 다른 워크 로드를 배포 하는 경우 설정을 수정 하 여 공유를 만든 후 추가 단계를 수행 합니다. 예를 들어 Microsoft SQL Server를 사용 하는 경우 SQL Server 서비스 계정을 부여 되어야 합니다 공유 및 파일 시스템에 대 한 모든 권한.

> [!NOTE]
>  System Center Virtual Machine Manager 사용 하 여 공유 위치를 만드는 경우가 아니면 클러스터 노드를 추가 하면 그룹 구성원 자격을 업데이트 해야 합니다.

PowerShell 스크립트를 사용 하 여 파일 공유를 만들려면 다음을 수행 합니다.

1. 에 포함 된 스크립트를 다운로드 [Hyper-v 워크 로드에 대 한 SMB 공유 구성을](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) 파일 서버 클러스터의 노드 중 하나에 있습니다.
2. 관리 시스템에서 도메인 관리자 자격 증명을 사용 하 여 Windows PowerShell 세션을 열고 다음 변수를 적절 한 값을 변경 Hyper-v 컴퓨터 개체에 대 한 Active Directory 그룹을 만들려면 다음 스크립트를 사용 하면 환경:

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. 저장소 노드 중 하나에서 관리자 자격 증명을 사용 하 여 Windows PowerShell 세션을 열고 다음 스크립트를 사용 하 여 공유를 만들고 각 CSV에 대 한 Domain Admins 그룹 및 계산 클러스터에 공유에 대 한 관리 권한을 부여할 합니다.

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

### <a name="step-43-enable-kerberos-constrained-delegation"></a>4.3 단계를 사용 하도록 설정 하는 Kerberos 제한 위임

에 포함 된 KCDSetup.ps1 스크립트를 사용 하 여 원격 시나리오 관리 및 저장소 클러스터 노드 중 하나에서 실시간 마이그레이션 보안을 강화에 대 한 Kerberos 제한 위임을 설정 하려면 [Hyper-v워크로드에대한SMB공유구성](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a). 스크립트에 대 한 간단한 래퍼는 다음과 같습니다.

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## <a name="next-steps"></a>다음 단계

클러스터 된 파일 서버를 배포한 후 모든 실제 작업 상태로 만들기 전에 가상 워크 로드를 사용 하 여 솔루션의 성능을 테스트 하는 것이 좋습니다. 이렇게 하면 솔루션 제대로 수행 되 고 있는지 확인 하 고 복잡 한 워크 로드를 추가 하기 전에 느린 문제를 해결 합니다. 자세한 내용은 참조 하세요. [테스트 저장소 공간 성능을 사용 하 여 가상 워크 로드](https://technet.microsoft.com/library/dn894707.aspx)합니다.

## <a name="see-also"></a>참조

-   [Windows Server 2016의에서 저장소 공간 다이렉트](storage-spaces-direct-overview.md)
-   [저장소 공간 다이렉트 캐시 이해](understand-the-cache.md)
-   [저장소 공간 다이렉트 볼륨 계획](plan-volumes.md)
-   [저장소 공간 내결함성](storage-spaces-fault-tolerance.md)
-   [저장소 공간 다이렉트 하드웨어 요구 사항](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [RDMA, or not to RDMA – that is the question(RDMA 선택 결정 문제)](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/)(TechNet 블로그)
