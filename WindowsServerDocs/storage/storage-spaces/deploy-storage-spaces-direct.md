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
description: Windows Server의 저장소 공간 다이렉트를 사용 하 여 소프트웨어 정의 저장소 하이퍼 컨 버 지 드 인프라 또는 (세분화 라고도) 컨 버 지 드 인프라를 배포 하는 단계별 지침.
ms.localizationpriority: medium
ms.openlocfilehash: 55cfa0e066506d7174f9e5b1e61cc0aa290706d7
ms.sourcegitcommit: 65e4f760be73104e67847f77e834e7b5e065211b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "5429045"
---
# 저장소 공간 다이렉트 배포

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 [저장소 공간 다이렉트](storage-spaces-direct-overview.md)를 배포 하는 단계별 지침을 제공 합니다.

> [!Tip]
> 취득 Hyper-Converged 인프라를 찾고 계신가요? Microsoft은 파트너 로부터 이러한 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd) 솔루션을 권장합니다. 설계, 조립 되며 호환성 및 안정성 얻기 및 신속 하 게 실행 되도록 하는 참조 아키텍처에 대해 유효성이 검사 됩니다.

> [!Tip]
> [하드웨어 없이 저장소 공간 다이렉트를 평가](storage-spaces-direct-in-vm.md)하 여 Microsoft Azure에 포함 되는 Hyper-v 가상 컴퓨터를 사용할 수 있습니다. 간편 하 게 하는 [Windows Server 빠른 랩 배포 스크립트](https://aka.ms/wslab), 교육 목적을 위해 사용 하 여 검토할 수도 있습니다.

## 시작하기 전에

[저장소 공간 다이렉트 하드웨어 요구 사항](Storage-Spaces-Direct-Hardware-Requirements.md) 을 검토 하 고 전체 접근 방식 및 일부 단계와 관련 된 중요 정보를 잘 이해 하려면이 문서를 통해 키를 누릅니다.

다음 정보를 수집 합니다.

- **배포 옵션입니다.** 저장소 공간 다이렉트 지원 [두 가지 배포 옵션: 하이퍼 수렴 형 및 수렴 형](storage-spaces-direct-overview.md#deployment-options), 세분화 라고도 합니다. 적합 한 결정 하려면 각각의 장점 익숙해지도록 하세요. 단계 1 ~ 3 아래 두 배포 옵션에 적용 됩니다. 4 단계 수렴 형된 배포에만 필요 합니다.

- **서버 이름입니다.** 조직의 컴퓨터, 파일, 경로 및 기타 리소스에 대 한 명명 정책 개념을 익혀야 합니다. 각각 고유한 이름을 가진 여러 서버를 프로 비전 해야 합니다.

- **도메인 이름입니다.** 도메인 이름 지정 및 도메인에 가입 하는 것에 대 한 조직의 정책 개념을 익혀야 합니다.  있습니다 됩니다 수에 참여 서버를 도메인에 하 고 도메인 이름을 지정 해야 합니다. 

- **RDMA 네트워킹 합니다.** 두 가지 유형의 RDMA 프로토콜이 가지: iWarp 및 RoCE 합니다. 적합 한 네트워크 어댑터를 사용, 쓰고 RoCE, 또한 참고 버전 (v1 또는 v2). RoCE, 랙 위쪽 스위치의 모델을 note 수도 있습니다.

- **VLAN ID입니다.** 있는 경우 서버에서 관리 OS 네트워크 어댑터에 사용할 VLAN ID를 note 합니다. 네트워크 관리자로부터 얻을 수 있습니다.

## 1단계: Windows Server 배포

### 1.1 단계: 운영 체제를 설치 합니다.

첫 번째 단계는 클러스터에 있는 모든 서버에 Windows Server를 설치 합니다. 저장소 공간 다이렉트에 Windows Server 2016 Datacenter Edition이 필요합니다. 데스크톱 환경 포함 서버는 Server Core 설치 옵션을 사용할 수 있습니다.

설치 마법사를 사용 하 여 Windows Server를 설치 하면 선택할 수 있습니다 (Server Core 참조) 하는 *Windows Server* 및 *Windows Server (데스크톱 환경 포함 서버)* *전체* 설치 옵션에 해당 하는 Windows Server 2012 r 2에서 사용할 수 있습니다. 선택 하지 않으면 Server Core 설치 옵션을 얻을 수 있습니다. 자세한 내용은 [Windows Server 2016 설치 옵션을](../../get-started/Windows-Server-2016.md)참조 하세요.

### 1.2 단계: 서버에 연결

이 가이드는 Server Core 설치 옵션 및 이어야 하는 별도 관리 시스템에서 원격으로 배포/관리에 집중 합니다.

- 관리 서버와 동일한 업데이트를 사용 하 여 Windows Server 2016
- 네트워크 연결을 관리 하는 서버
- 동일한 도메인 또는 완전히 트러스트 된 도메인에 가입
- Hyper-V 및 장애 조치(failover) 클러스터링용 PowerShell 모듈 및 RSAT(원격 서버 관리 도구) RSAT 도구 및 PowerShell 모듈 Windows 서버에서 사용할 수 있으며 다른 기능을 설치 하지 않고도 설치할 수 있습니다. 또한 Windows 10 관리 PC에서 [원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520) 를 설치할 수 있습니다.

관리 시스템에서 장애 조치(failover) 클러스터 및 Hyper-V 관리 도구를 설치합니다. 서버 관리자에서 **역할 및 기능 추가** 마법사를 사용하여 이 작업을 수행할 수 있습니다. **기능** 페이지에서 **원격 서버 관리 도구**를 선택한 다음 설치할 도구를 선택합니다.

PS 세션을 입력하고 서버 이름 또는 연결하려는 노드의 IP 주소를 사용합니다. 수 Windows를 설정할 때 지정한 관리자 암호를 입력이 명령을 실행 하면 암호를 입력 합니다.

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   이 작업을 여러 번 수행 해야 하는 경우 스크립트에서 보다 유용한 방식에서 동일한 작업을 수행 하는의 예는 다음과 같습니다.

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> 관리 시스템에서 원격으로 구축 하는 경우 하면 오류가 발생할 수와 같은 *WinRM 요청을 처리할 수 없습니다.* 이 문제를 해결 하려면 관리 컴퓨터에서 신뢰할 수 있는 호스트 목록에 각 서버를 추가 하려면 Windows PowerShell을 사용 합니다.  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> 참고: 신뢰할 수 있는 호스트 목록에서 와일드 카드와 같은 `Server*`.
>
> 신뢰할 수 있는 호스트 목록에를 보려면 `Get-Item WSMAN:\Localhost\Client\TrustedHosts`.  
>   
> 비어 있는 목록에 입력 `Clear-Item WSMAN:\Localhost\Client\TrustedHost`.  

### 1.3 단계: 도메인에 가입 하 고 도메인 계정을 추가합니다

로컬 관리자 계정을 사용 하 여 개별 서버를 구성 했으므로 지금 `<ComputerName>\Administrator`.

저장소 공간 다이렉트를 관리 하려면 서버를 도메인에 가입 하 고 모든 서버의 관리자 그룹에 있는 Active Directory Domain Services 도메인 계정을 사용 해야 합니다.

관리 시스템에서 관리자 권한으로 PowerShell 콘솔을 엽니다. 사용 `Enter-PSSession` 각 서버에 연결 하 고 컴퓨터 이름, 도메인 이름 및 도메인 자격 증명을 대체 하는 다음 cmdlet을 실행 합니다.

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

저장소 관리자 계정에 Domain Admins 그룹의 구성원 없으면 저장소 관리자 계정에 각 노드에서-로컬 관리자 그룹에 추가 하거나 더 좋은 방법은 저장소 관리자가 사용 하 여 그룹을 추가 합니다. 다음 명령을 사용 하 여 (하거나 작성할 수 이렇게-자세한 내용은 [로컬 그룹에 도메인 사용자 추가를 사용 하 여 PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx) 참조 하는 Windows PowerShell 함수):

```
Net localgroup Administrators <Domain\Account> /add
```

### 1.4 단계: 역할 및 기능 설치

다음 단계는 모든 서버의 서버 역할을 설치 하는 것입니다. 이렇게 하려면 [Windows Admin Center](../../manage/windows-admin-center/use/manage-servers.md), [서버 관리자](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)를 사용 하 여), 또는 PowerShell 합니다. 역할을 설치 하는 다음과 같습니다.

- 장애 조치(failover) 클러스터링
- Hyper-V
- 파일 서버 (예: 수렴 형된 배포 모든 파일 공유를 호스팅합니다 경우)
- 데이터 센터 브리징(iWARP 네트워크 어댑터 대신 RoCEv2를 사용하는 경우)
- RSAT-클러스터링-PowerShell
- Hyper-V-PowerShell

PowerShell을 통해 설치 하려면 [설치 WindowsFeature](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature) cmdlet을 사용 합니다. 다음과 같은 단일 서버에서 사용할 수 있습니다.

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

한 번으로 클러스터의 모든 서버에서 명령을 실행 하려면이 약간 수정 환경에 맞게 스크립트의 시작 부분에는 변수 목록은 스크립트의를 사용 합니다.

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"
$FeatureList = "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"

# This part runs the Install-WindowsFeature cmdlet on all servers in $ServerList, passing the list of features into the scriptblock with the "Using" scope modifier so you don't have to hard-code them here.
Invoke-Command ($ServerList) {
    Install-WindowsFeature -Name $Using:Featurelist
}
```

## 2단계: 네트워크 구성

배포 하는 경우 저장소 공간 다이렉트 가상 컴퓨터 내에서이 섹션을 건너뜁니다.

저장소 공간 다이렉트는 높은 대역폭을 클러스터의 서버 간에 네트워킹 대기 시간이 필요 합니다. 최소 10 GbE 네트워킹에는 필수 이며 원격 직접 메모리 액세스 (RDMA)를 사용 하는 것이 좋습니다. Windows Server 2016 로고가 붙어 있다면 하지만 iWARP는 일반적으로 쉽게 설정할 수 있기만 iWARP 또는 RoCE 중 하나를 사용할 수 있습니다.

> [!Important]
> 네트워킹 장비에 따라 및 RoCE v2를 사용 하 여 특히 랙의 맨 위에 스위치의 몇 가지 구성을 필요할 수 있습니다. 올바른 스위치 구성은 저장소 공간 다이렉트의 안정성과 성능이 보장 되어야 합니다.

Windows Server 2016 스위치 포함 팀 (SET) 내의 Hyper-v 가상 스위치를 소개합니다. 이렇게 하면 똑같은 물리적 NIC 포트가 필요한 물리적 NIC 포트의 수를 줄여 RDMA를 사용 하는 동안 모든 네트워크 트래픽에 사용할 수 있습니다. 스위치 포함 팀은 저장소 공간 다이렉트에 권장 됩니다.

저장소 공간 다이렉트에 대 한 네트워킹을 설정 하는 지침, [Windows Server 2016 수렴 형 NIC 및 게스트 RDMA 배포 가이드를](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx)참조 하세요.

## 3단계: 저장소 공간 다이렉트 구성

다음 단계는 구성 중인 서버와 동일한 버전의 관리 시스템에서 수행됩니다. 다음 단계를 PowerShell 세션을 사용 하 여 원격으로 실행할 수 있지만 대신 로컬 PowerShell 세션에서 관리자 권한으로 관리 시스템에서 실행 해야 합니다.

### 3.1 단계: 정리 드라이브

저장소 공간 다이렉트를 사용 하기 전에 확인 드라이브가 빈: 없음 이전 파티션 또는 기타 데이터. 대체 하는 컴퓨터 이름이, 이전 모든 모든 파티션 또는 기타 데이터를 제거 하려면 다음 스크립트를 실행 합니다.

> [!Warning]
> 이 스크립트는 운영 체제 부팅 드라이브 이외의 모든 드라이브에 있는 모든 데이터를 영구적으로 제거 됩니다!

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

출력은 다음과 같이 표시, **개수** 는 각 서버에서 각 모델의 드라이브의 번호:

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

### 3.2 단계: 클러스터 확인

이 단계에서는 서버 노드가 저장소 공간 다이렉트를 사용 하 여 클러스터를 만들도록 올바르게 구성 되어 있는지 확인 하려면 클러스터 유효성 검사 도구를 실행 합니다. 때 유효성 검사를 클러스터 (`Test-Cluster`)는 장애 조치 클러스터로 성공적으로 작동 하도록 적절 한 구성을 나타나는지 확인 하는 테스트가 실행 클러스터를 만들기 전에 실행 합니다. 사용 하 여 바로 아래 예제는 `-Include` 매개 변수를 특정 테스트 범주가 지정 됩니다. 이렇게 하면 저장소 공간 다이렉트 관련 테스트가 유효성 검사에 포함됩니다.

다음 PowerShell 명령을 사용하여 저장소 공간 다이렉트 클러스터로 사용할 서버 집합의 유효성을 검사할 수 있습니다.

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### 3.3 단계: 클러스터 만들기

이 단계에서는 다음 PowerShell cmdlet을 사용 하 여 이전 단계에서 클러스터 만들기에 대 한 유효성을 검사 하는 노드를 사용 하 여 클러스터를 만듭니다.

클러스터를 만들 때 경고 상태를 받게-"문제가 발생 했습니다 클러스터 된 역할을 만드는 하지 못하도록 시작 하는 동안 합니다. 자세한 내용은 아래의 보고서 파일을 확인하십시오."라는 경고가 나타납니다. 이 경고는 무시해도 됩니다. 클러스터 쿼럼에 사용할 수 있는 디스크가 없기 때문에 나타나는 것입니다. 클러스터를 만든 후 파일 공유 감시 또는 클라우드 감시를 구성하는 것이 좋습니다.

> [!Note]
> 서버에서 고정 IP 주소를 사용하는 경우 다음 매개 변수를 추가하고 IP 주소 -StaticAddress &lt;X.X.X.X&gt;를 지정하여 고정 IP 주소를 반영하도록 다음 명령을 수정합니다.
> 다음 명령에서 ClusterName 자리 표시자는 고유하고 15자 이하인 netbios 이름으로 바꿔야 합니다.
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

클러스터를 만든 후 클러스터 이름에 대한 DNS 항목을 복제하는 데 약간의 시간이 걸릴 수 있습니다. 이 시간은 환경 및 DNS 복제 구성에 따라 달라집니다. 클러스터를 확인하지 못한 경우 대부분 클러스터 이름 대신 클러스터의 활성 구성원인 노드의 컴퓨터 이름을 사용하면 성공적으로 확인할 수 있습니다.

### 3.4 단계: 클러스터 감시를 구성 합니다.

세 개 이상의 서버를 사용 하 여 클러스터에 두 명의 서버 실패 또는 오프 라인 상태 대응할 수 있도록 클러스터에 대 한 감시를 구성 하는 것이 좋습니다. 그렇지 않은 경우 두 서버를 오프 라인으로 전환 하면도 사용할 수 없게 만드는 다른, 두 서버 배포에는 클러스터 감시가 필요 합니다. 이러한 시스템에서는 파일 공유를 감시로 사용하거나 클라우드 감시를 사용할 수 있습니다. 

자세한 내용은 다음 항목을 참조하세요.

- [쿼럼 구성 및 관리](../../failover-clustering/manage-cluster-quorum.md)
- [장애 조치 클러스터용 클라우드 감시 배포](../../failover-clustering/deploy-cloud-witness.md)

### 3.5단계: 저장소 공간 다이렉트 사용

클러스터를 만든 후 사용 하 여는 `Enable-ClusterStorageSpacesDirect` PowerShell cmdlet 저장소 시스템이 저장소 공간 다이렉트 모드로 전환 하 고 다음 작업이 자동으로 수행 됩니다.

-   **풀 만들기:** "S2D on Cluster1"과 같은 이름을 가진 대규모 단일 풀을 만듭니다.

-   **저장소 공간 다이렉트 캐시 구성:** 저장소 공간 다이렉트에 사용할 수 있는 미디어(드라이브) 유형이 2개 이상인 경우 가장 빠른 캐시 장치로 사용할 수 있습니다(대부분의 경우 읽기 및 쓰기).

-   **계층:** 기본 계층으로 두 계층을 만듭니다. 하나는 "Capacity"이고 다른 하나는 "Performance"입니다. Cmdlet은 장치를 분석한 후 장치 유형과 복원력을 조합하여 각 계층을 구성합니다.

관리 시스템에서 관리자 권한으로 PowerShell 명령 창을 열고 다음 명령을 시작합니다. 클러스터 이름은 이전 단계에서 만든 클러스터의 이름입니다. 이 명령을 노드 중 하나에서 로컬로 실행하면 -CimSession 매개 변수가 필요 없습니다.

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

위 명령을 통해 저장소 공간 다이렉트를 사용하려는 경우 클러스터 이름 대신 노드 이름을 사용할 수도 있습니다. 노드 이름을 사용하면 새로 만든 클러스터 이름에서 발생할 수 있는 DNS 복제 지연으로 인해 보다 안정적일 수 있습니다.

몇 분 후 이 명령이 완료되면 시스템이 볼륨을 만들 수 있도록 준비됩니다.

### 3.6단계: 볼륨 만들기

사용 하는 것이 좋습니다 합니다 `New-Volume` cmdlet으로 가장 빠르고 간단한 환경을 제공 합니다. 이 단일 cmdlet은 가상 디스크를 자동으로 만들어서 분할 및 포맷하고, 이와 일치하는 이름으로 볼륨을 만들어 클러스터 공유 볼륨에 추가합니다. 이 모든 과정이 하나의 간편한 단계만으로 진행됩니다.

자세한 내용은 [저장소 공간 다이렉트에서 볼륨 만들기](create-volumes.md)를 참조하세요.

### 3.7 단계: CSV 캐시를 선택적으로 사용 하도록 설정

클러스터 공유 볼륨 (CSV) 캐시 시스템 메모리 (RAM)를 사용 하 여 Windows 캐시 관리자가 이미 캐시 되지 읽기 작업의 쓰기 블록 수준 캐시를 활성화할 수 있습니다. Hyper-v 같은 응용 프로그램에 대 한 성능을 향상할 수 있습니다. CSV 캐시 읽기 요청 성능을 높일 수 및 스케일 아웃 파일 서버 시나리오에도 유용 합니다.

CSV 캐시를 사용 하면 Vhd를 사용할 수 있는 메모리를 사용 하 여 저장소 성능을 균형을 유지 해야 하므로 하이퍼 수렴 형 클러스터에서 Vm을 실행할 수 있는 메모리 양을 줄입니다.

CSV 캐시의 크기를 설정 하려면 저장소 클러스터에 대 한 관리자 권한이 있는 계정으로 관리 시스템에서 PowerShell 세션을 열고 다음을 변경 하는이 스크립트를 사용 하 여 `$ClusterName` 및 `$CSVCacheSize` 변수를 적절 하 게 (설정 하는이 예제는 2 GB CSV 캐시 서버당):

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

자세한 정보는 [CSV 메모리 내 읽기 캐시를 사용 하 여](csv-cache.md)참조 하세요.

### 3.8 단계: 하이퍼 수렴 형 배포에 대 한 가상 컴퓨터 배포

하이퍼 수렴 형 클러스터를 배포 하는 경우 마지막 단계는 저장소 공간 다이렉트 클러스터에서 가상 컴퓨터를 프로 비전입니다.

가상 컴퓨터의 파일은 장애 조치(failover) 클러스터의 클러스터형 VM과 마찬가지로 시스템 CSV 네임스페이스에 저장되어야 합니다(예: c:\\ClusterStorage\\Volume1).

저장소 및 가상 컴퓨터, System Center 가상 컴퓨터 Manager 같은 관리 도구 상자에서 또는 다른 도구를 사용할 수 있습니다.

## 4 단계: 컨 버 지 드 솔루션에 대 한 스케일 아웃 파일 서버 배포

수렴 형된 솔루션을 배포 하는 경우 다음 단계 스케일 아웃 파일 서버 인스턴스를 만들고 일부 파일 공유를 설정 하는 것입니다. 완료 하 고이 필요 하지 않습니다-하이퍼 수렴 형 클러스터를 배포 하는 경우 섹션.

### 4.1 단계: 스케일 아웃 파일 서버 역할 만들기

파일 서버 클러스터 서비스 설정의 다음 단계로 지속적으로 사용할 수 있는 파일 공유 호스팅되는 스케일 아웃 파일 서버 인스턴스를 만들 때 클러스터 된 파일 서버 역할을 만드는 것입니다.

#### 서버 관리자를 사용 하 여 스케일 아웃 파일 서버 역할을 만들려면

1.  장애 조치 클러스터 관리자에서 클러스터를 선택 하 고, **역할**을 이동, **역할 구성...** 를 클릭 합니다.<br>고가용성 마법사가 나타납니다.
2.  **역할 선택** 페이지에서 **파일 서버**를 클릭 합니다.
3.  **파일 서버 유형** 페이지에서 **응용 프로그램 데이터에 대 한 스케일 아웃 파일 서버**를 클릭 합니다.
4.  **클라이언트 액세스 지점** 페이지에서 스케일 아웃 파일 서버에 대 한 이름을 입력 합니다.
5.  그림 1에 표시 된 대로 역할 된 **역할** 을 이동 하 여 설치를 완료 하 고 만든 **상태** 열의 표시 되는지 **실행** 클러스터 된 파일 서버 역할 옆에 있는 확인을 확인 합니다.

    ![스크린샷 장애 조치 클러스터 관리자의 스케일 아웃 파일 서버를 표시 합니다.](media\Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016\SOFS_in_FCM.png "Failover Cluster Manager showing the Scale-Out File Server")

     **그림 1** 장애 조치 클러스터 관리자를 실행 상태를 사용 하 여 스케일 아웃 파일 서버를 표시 합니다.

> [!NOTE]
>  클러스터 된 역할을 만든 후 있을 일부 네트워크 몇 분 동안 또는 잠재적으로 더 긴 것에 파일 공유를 만들지 못하게 방지할 수 있는 전파 지연 합니다.  
  
#### Windows PowerShell을 사용 하 여 스케일 아웃 파일 서버 역할을 만들려면

 파일 서버 클러스터에 연결 된 Windows PowerShell 세션에서 제공 하려면 클러스터의 이름과 일치 시키기 위해 *FSCLUSTER* 및 *SOFS* 이름과 일치 하도록 변경 하 여 스케일 아웃 파일 서버 역할을 만들려면 다음 명령을 입력 합니다 스케일 아웃 파일 서버 역할:

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  클러스터 된 역할을 만든 후 있을 일부 네트워크 몇 분 동안 또는 잠재적으로 더 긴 것에 파일 공유를 만들지 못하게 방지할 수 있는 전파 지연 합니다. SOFS 역할 즉시 실패 시작 되지 않는 경우 클러스터의 컴퓨터 개체 SOFS 역할에 대 한 컴퓨터 계정을 만들 수 있는 권한이 없는 때문일 수 있습니다. 도움말, 해당 참조를 사용 하 여이 블로그 게시물: [스케일 아웃 파일 서버 역할에 실패 To 시작 With 이벤트 Id 1205, 1069, 및 1194](http://www.aidanfinn.com/?p=14142)합니다.

### 4.2 단계: 파일 공유를 만들려면

가상 디스크를 만들고 Csv에 추가 했습니다, 되 면 바로에서 파일 공유를 만드는 가상 디스크 당 CSV 당 하나의 파일을 공유 합니다. System Center 가상 Machine Manager (VMM) 환경에서 없는, 경우 배포를 자동화 부분적으로 Windows PowerShell을 사용 하지만,에 대 한 권한 처리 때문에이 작업을 수행 하는 편리한 방법 때문일 수 있습니다.

부분적으로 그룹 및 공유를 만드는 프로세스를 자동화 하는 [Hyper-v 워크 로드에 대 한 SMB 공유 구성](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) 스크립트에 포함 된 스크립트를 사용 합니다. Hyper-v 워크 로드에 대 한 쓰여질 하므로 다른 워크 로드를 배포 하는 경우 설정을 수정 하거나 공유를 만든 후에 추가 단계를 수행 합니다. 예를 들어 Microsoft SQL Server를 사용 하는 경우 SQL Server 서비스 계정 받아야 공유 및 파일 시스템에 전체 제어 합니다.

> [!NOTE]
>  System Center 가상 컴퓨터 Manager를 사용 하 여 공유 위치를 만드는 경우가 아니면 클러스터 노드를 추가할 때 그룹 구성원을 업데이트 해야 합니다.

PowerShell 스크립트를 사용 하 여 파일 공유를 만들려면 다음을 수행 합니다.

1. 파일 서버 클러스터 노드 중 하나를 [Hyper-v 워크 로드에 대 한 SMB 공유 구성](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a) 포함 된 스크립트를 다운로드 합니다.
2. 관리 시스템에서 도메인 관리자 자격 증명을 사용 하 여 Windows PowerShell 세션을 열고 다음 스크립트를 사용 하 여 만들 Hyper-v 컴퓨터 개체에 대 한 Active Directory 그룹에 적절 하 게 변수에 대 한 값을 변경 합니다 환경:

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. 저장소 노드 중 하나에서 관리자 자격 증명으로 Windows PowerShell 세션을 열고, 다음 스크립트를 사용 하 여 각 CSV에 대 한 공유를 만들고 Domain Admins 그룹 및 계산 클러스터에는 공유에 대 한 관리 권한을 부여 합니다.

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

### 4.3 단계를 사용 하도록 설정 Kerberos 제한 위임

Kerberos 제한 위임 원격 시나리오 관리 및 저장소 클러스터 노드 중 하나에서 실시간 마이그레이션 보안 강화를 설정 하려면 [Hyper-v 워크 로드에 대 한 SMB 공유 구성](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)에 포함 된 KCDSetup.ps1 스크립트를 사용 합니다. 스크립트에 대 한 약간의 래퍼는 다음과 같습니다.

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## 다음 단계

클러스터 된 파일 서버를 배포한 후 모든 실제 워크 로드를 표시 하기 전에 가상 워크 로드를 사용 하 여 솔루션의 성능을 테스트 하는 것이 좋습니다. 이렇게 하면 솔루션 제대로 수행 하 고 있는지 확인 하 고 복잡 한 워크 로드를 추가 하기 전에 모든 느린 문제를 파악 합니다. 자세한 내용은 [테스트 저장소 공간 성능 사용 하 여 가상 워크 로드](https://technet.microsoft.com/library/dn894707.aspx)를 참조 하세요.

## 참고 항목

-   [Windows Server 2016의 저장소 공간 다이렉트](storage-spaces-direct-overview.md)
-   [저장소 공간 다이렉트에서 캐시 이해](understand-the-cache.md)
-   [저장소 공간 다이렉트에서 볼륨 계획](plan-volumes.md)
-   [저장소 공간 내결함성](storage-spaces-fault-tolerance.md)
-   [저장소 공간 다이렉트 하드웨어 요구 사항](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [RDMA, or not to RDMA – that is the question(RDMA 선택 결정 문제)](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/)(TechNet 블로그)
