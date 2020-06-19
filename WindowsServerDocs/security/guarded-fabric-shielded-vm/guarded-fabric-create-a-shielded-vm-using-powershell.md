---
title: PowerShell을 사용 하 여 보호 된 VM 만들기
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: abc1a2af7353bd85e0ae7ac55debc36d63d1782f
ms.sourcegitcommit: fe89b8001ad664b3618708b013490de93501db05
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84942292"
---
# <a name="create-a-shielded-vm-using-powershell"></a>PowerShell을 사용 하 여 보호 된 VM 만들기

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

프로덕션 환경에서는 일반적으로 패브릭 관리자 (예: VMM)를 사용 하 여 보호 된 Vm을 배포 합니다. 그러나 아래에 설명 된 단계를 통해 패브릭 관리자 없이 전체 시나리오를 배포 하 고 유효성을 검사할 수 있습니다.

간단히 말해서 모든 컴퓨터에 템플릿 디스크, 보호 데이터 파일, 무인 설치 응답 파일 및 기타 보안 아티팩트를 만든 다음, 이러한 파일을 보호 된 호스트에 복사 하 고 보호 된 VM을 프로 비전 합니다.

## <a name="create-a-signed-template-disk"></a>서명된 템플릿 디스크 만들기

새 차폐 VM을 만들려면 먼저 서명 된 OS 볼륨 (또는 Linux의 부팅 및 루트 파티션)으로 미리 암호화 된 보호 된 VM 템플릿 디스크가 필요 합니다.
템플릿 디스크를 만드는 방법에 대 한 자세한 내용은 아래 링크를 참조 하세요.

- [Windows 템플릿 디스크 준비](guarded-fabric-create-a-shielded-vm-template.md)
- [Linux 템플릿 디스크 준비](guarded-fabric-create-a-linux-shielded-vm-template.md)

또한 보호 데이터 파일을 만들려면 디스크의 볼륨 서명 카탈로그 복사본이 필요 합니다.
이 파일을 저장 하려면 템플릿 디스크를 만든 컴퓨터에서 다음 명령을 실행 합니다.

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath "C:\temp\MyTemplateDisk.vhdx" -VolumeSignatureCatalogPath "C:\temp\MyTemplateDiskCatalog.vsc"
```

## <a name="download-guardian-metadata"></a>보호자 메타 데이터 다운로드

차폐 VM을 실행 하려는 각 가상화 패브릭에 대해 패브릭의 HGS 클러스터에 대 한 보호자 메타 데이터를 가져와야 합니다.
호스팅 공급자는이 정보를 제공할 수 있어야 합니다.

엔터프라이즈 환경에 있고 HGS 서버와 통신할 수 있는 경우 *Http:// \<HGSCLUSTERNAME\> /KeyProtection/service/metadata/2014-07/* 에서 보호자 메타 데이터를 사용할 수 있습니다 metadata.xml

## <a name="create-shielding-data-pdk-file"></a>보호 데이터 파일 (PDK) 만들기

보호 데이터는 테 넌 트 VM 소유자가 만들고 소유 하며, 패브릭 관리자 (예: 보호 된 VM의 관리자 암호)에서 보호 해야 하는 보호 된 Vm을 만드는 데 필요한 암호를 포함 합니다.
보호 데이터는 HGS 서버 및 테 넌 트만 암호를 해독할 수 있도록 암호화 됩니다.
테 넌 트/v m 소유자가 만든 후에는 결과 PDK 파일을 보호 된 패브릭에 복사 해야 합니다.
자세한 내용은 [보호 데이터 란 무엇 이며 필요한 이유는 무엇 인가요?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)를 참조 하세요.

또한 무인 설치 응답 파일 (Windows의 경우 unattend.xml는 Linux에 따라 다름)이 필요 합니다. 응답 파일에 포함할 내용에 대 한 지침은 [응답 파일 만들기](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file) 를 참조 하세요.

보호 된 Vm에 대 한 원격 서버 관리 도구가 설치 된 컴퓨터에서 다음 cmdlet을 실행 합니다.
Linux VM에 대 한 PDK를 만드는 경우 Windows Server 버전 1709 이상을 실행 하는 서버에서이 작업을 수행 해야 합니다.

 
```powershell
# Create owner certificate, don't lose this!
# The certificate is stored at Cert:\LocalMachine\Shielded VM Local Certificates
$Owner = New-HgsGuardian –Name 'Owner' –GenerateCertificates
 
# Import the HGS guardian for each fabric you want to run your shielded VM
$Guardian = Import-HgsGuardian -Path C:\HGSGuardian.xml -Name 'TestFabric'
 
# Create the PDK file
# The "Policy" parameter describes whether the admin can see the VM's console or not
# Use "EncryptionSupported" if you are testing out shielded VMs and want to debug any issues during the specialization process
New-ShieldingDataFile -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Owner $Owner –Guardian $guardian –VolumeIDQualifier (New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\MyTemplateDiskCatalog.vsc' -VersionRule Equals) -WindowsUnattendFile 'C:\unattend.xml' -Policy Shielded
```
    
## <a name="provision-shielded-vm-on-a-guarded-host"></a>보호 된 호스트에서 보호 된 VM 프로 비전
Windows Server 2016를 실행 하는 호스트에서 프로 비전 작업의 신호 완료를 위해 VM을 종료 하는 작업을 모니터링 하 고 프로 비전이 실패 한 경우 Hyper-v 이벤트 로그에서 오류 정보를 확인할 수 있습니다.

새 보호 된 VM을 만들기 전에 매번 새 템플릿 디스크를 만들 수도 있습니다.

배포 준비를 위해 템플릿 디스크 파일 (ServerOS .vhdx) 및 PDK 파일 (contoso. pdk)을 보호 된 호스트로 복사 합니다.

보호 된 호스트에서 프로 비전 프로세스를 간소화 하는 ShieldedVM cmdlet이 포함 된 보호 된 패브릭 도구 PowerShell 모듈을 설치 합니다. 보호 된 호스트에서 인터넷에 액세스할 수 있는 경우 다음 명령을 실행 합니다.

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

인터넷에 액세스할 수 있는 다른 컴퓨터에 모듈을 다운로드 하 여 `C:\Program Files\WindowsPowerShell\Modules` 보호 된 호스트의 결과 모듈을에 복사할 수도 있습니다.

```powershell
Save-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0 -Path C:\temp\
```

모듈이 설치 되 면 보호 된 VM을 프로 비전 할 준비가 된 것입니다.

```powershell
New-ShieldedVM -Name 'MyShieldedVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait
```

보호 데이터 응답 파일에 특수화 값이 포함 된 경우 ShieldedVM에 대체 값을 제공할 수 있습니다. 이 예제에서 응답 파일은 고정 IPv4 주소에 대 한 자리 표시자 값으로 구성 됩니다.

```powershell
$specializationValues = @{
    "@IP4Addr-1@" = "192.168.1.10/24"
    "@MacAddr-1@" = "Ethernet"
    "@Prefix-1-1@" = "24"
    "@NextHop-1-1@" = "192.168.1.254"
}
New-ShieldedVM -Name 'MyStaticIPVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -SpecializationValues $specializationValues -Wait

```

템플릿 디스크에 Linux 기반 OS가 포함 된 경우 `-Linux` 명령을 실행할 때 플래그를 포함 합니다.

```powershell
New-ShieldedVM -Name 'MyLinuxVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait -Linux
```

`Get-Help New-ShieldedVM -Full`Cmdlet에 전달할 수 있는 다른 옵션에 대 한 자세한 내용은를 사용 하 여 도움말 콘텐츠를 확인 하세요.

VM이 프로 비전을 완료 하면 OS 특정 특수화 단계가 시작 되 고 그 후에 사용할 준비가 됩니다.
VM이 실행 되 고 있는 경우 (RDP, PowerShell, SSH 또는 선호 하는 관리 도구를 사용 하 여) 해당 네트워크에 연결할 수 있도록 VM을 유효한 네트워크에 연결 해야 합니다.

## <a name="running-shielded-vms-on-a-hyper-v-cluster"></a>Hyper-v 클러스터에서 보호 된 Vm 실행

Windows 장애 조치 (Failover) 클러스터를 사용 하 여 클러스터 된 보호 된 호스트에 보호 된 Vm을 배포 하려는 경우 다음 cmdlet을 사용 하 여 보호 된 VM을 항상 사용 가능 하도록 구성할 수 있습니다.

```powershell
Add-ClusterVirtualMachineRole -VMName 'MyShieldedVM' -Cluster <Hyper-V cluster name>
```

이제 보호 된 VM을 클러스터 내에서 실시간 마이그레이션할 수 있습니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [VMM을 사용 하 여 차폐 배포](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)