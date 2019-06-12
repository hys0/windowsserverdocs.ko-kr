---
title: PowerShell을 사용 하 여 보호 된 VM 만들기
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 0086edb7781a604cc90b9e76d34e5a3dc2725547
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447520"
---
# <a name="create-a-shielded-vm-using-powershell"></a>PowerShell을 사용 하 여 보호 된 VM 만들기

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

프로덕션 환경에서 보호 된 Vm을 배포 하 패브릭 관리자 (예: VMM)을 일반적으로 사용 됩니다. 그러나 아래 그림과 같이 배포 하 고 패브릭 관리자 없이 전체 시나리오의 유효성을 검사 할 수 있습니다.

간단히 말해 템플릿 디스크, 보호 데이터 파일, 무인된 설치 응답 파일 및 기타 보안 아티팩트 모든 컴퓨터에서 다음 보호 된 호스트에 다음이 파일을 복사 합니다. 만들고 보호 된 VM을 프로 비전 합니다.

## <a name="create-a-signed-template-disk"></a>서명 된 템플릿 디스크 만들기

새 보호 된 VM을 만들려면 먼저 해당 OS 볼륨 (또는 Linux에서 부팅 및 루트 파티션에) 로그인을 사용 하 여 미리 암호화 된 보호 된 VM 템플릿 디스크를 해야 합니다.
템플릿 디스크를 만드는 방법에 대 한 자세한 내용은 아래 링크를 따르세요.

- [Windows 템플릿 디스크를 준비](guarded-fabric-create-a-shielded-vm-template.md)
- [Linux 템플릿 디스크를 준비](guarded-fabric-create-a-linux-shielded-vm-template.md)

실딩 데이터 파일을 만들려면 디스크의 볼륨 서명 카탈로그의 복사본을 해야 합니다.
이 파일을 저장 하려면 다음 명령을 실행 컴퓨터에서 템플릿 디스크를 만들 위치:

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath "C:\temp\MyTemplateDisk.vhdx" -VolumeSignatureCatalogPath "C:\temp\MyTemplateDiskCatalog.vsc"
```

## <a name="download-guardian-metadata"></a>보호 메타 데이터 다운로드

각 보호 된 VM을 실행 하려는 가상화 패브릭의 보호 된 패브릭에 HGS 클러스터 메타 데이터를 가져오는 해야 합니다.
호스팅 공급자를이 정보를 제공할 수 있어야 합니다.

엔터프라이즈 환경에을 HGS 서버와 통신할 수 보호 메타 데이터에서 사용 가능한 인지 *http://\<HGSCLUSTERNAME\>/KeyProtection/service/metadata/2014-07/metadata.xml*

## <a name="create-shielding-data-pdk-file"></a>실딩 데이터 (PDK) 파일 만들기

실딩 데이터 만들어집니다 및 테 넌 트 VM 소유자가 소유 하 고 보호 된 VM의 관리자 암호와 같은 패브릭 관리자를 보호 해야 하는 보호 된 Vm을 만드는 데 필요한 암호를 포함 합니다.
실딩 데이터는 HGS 서버와 테 넌 트에만 해독할 수 있도록 암호화 됩니다.
테 넌 트/VM 소유자가 만들어지면 결과 PDK 파일 보호 된 패브릭에 복사 해야 합니다.
자세한 내용은 [실딩 데이터는 무엇 이며 왜 필요?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)합니다.

또한 무인된 설치 응답 파일을 해야 (Linux 용 Windows 위한 unattend.xml 다름). 참조 [응답 파일을 만들고](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file) 응답 파일에 포함할 항목에 대 한 지침에 대 한 합니다.

설치 하는 보호 된 Vm에 대 한 원격 서버 관리 도구를 사용 하는 컴퓨터에서 다음 cmdlet을 실행 합니다.
PDK Linux vm을 만들면이 Windows Server 버전 1709 이상을 실행 하는 서버에서 수행 해야 합니다.

 
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
    
## <a name="provision-shielded-vm-on-a-guarded-host"></a>보호 된 호스트에서 보호 된 VM을 프로 비전
보호 된 호스트 배포를 위한 준비를 하려면 템플릿 디스크 파일 (ServerOS.vhdx) 및 (contoso.pdk) PDK 파일을 복사 합니다.

보호 된 호스트 프로 비전 프로세스를 간소화 하기 위해 새 ShieldedVM cmdlet을 포함 하는 보호 된 패브릭 도구 PowerShell 모듈을 설치 합니다. 보호 된 호스트에 인터넷에 액세스할 수 있는 경우 다음 명령을 실행 합니다.

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

인터넷에 액세스 하 고 결과 모듈을 복사 하는 다른 컴퓨터에서 모듈을 다운로드할 수도 있습니다 `C:\Program Files\WindowsPowerShell\Modules` 보호 된 호스트에서.

```powershell
Save-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0 -Path C:\temp\
```

모듈이 설치 되 면 보호 된 VM을 프로 비전 할 준비가 되었습니다.

```powershell
New-ShieldedVM -Name 'MyShieldedVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait
```

템플릿 디스크를 Linux 기반 OS를 포함 하는 경우 포함 된 `-Linux` 명령을 실행할 때 플래그:

```powershell
New-ShieldedVM -Name 'MyLinuxVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait -Linux
```

사용 하 여 도움말 내용을 확인 `Get-Help New-ShieldedVM -Full` cmdlet에 전달할 수 있습니다 다른 옵션에 자세히 알아보려면 합니다.

VM 프로 비전 완료 되 면 지나면 사용할 준비가 됩니다 OS 별 특수화 단계에서 입력 됩니다.
(RDP, PowerShell, SSH 또는 기본 설정된 관리 도구 사용)이 실행 되 면 연결할 수 있도록 올바른 네트워크에 VM을 연결 해야 합니다.

## <a name="running-shielded-vms-on-a-hyper-v-cluster"></a>Hyper-v 클러스터에서 실행 되는 보호 된 Vm

보호 된 Vm (Windows 장애 조치 클러스터를 사용 하 여) 하는 클러스터 된 보호 된 호스트에 배포 하려는 경우 다음 cmdlet을 사용 하 여 항상 사용 가능한 보호 된 VM을 구성할 수 있습니다.

```powershell
Add-ClusterVirtualMachineRole -VMName 'MyShieldedVM' -Cluster <Hyper-V cluster name>
```

보호 된 VM 수 이제 실시간 마이그레이션할 수는 클러스터 내에서.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [배포를 보호 된 VMM을 사용 하 여](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)