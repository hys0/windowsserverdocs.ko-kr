---
title: 만들 보호 된 Linux VM 템플릿 디스크
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d0e1d4fb-97fc-4389-9421-c869ba532944
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: e791d18e027e5e3e1c5b9c52659641ff588a96a2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858674"
---
# <a name="create-a-linux-shielded-vm-template-disk"></a>만들 보호 된 Linux VM 템플릿 디스크

> 적용 대상: Windows Server 2019, Windows Server (반기 채널) 

이 항목에서는 보호 된 Linux Vm에 하나 이상의 테 넌 트 Vm을 인스턴스화하는 데 사용할 수 있는 템플릿 디스크를 준비 하는 방법에 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

준비 및 테스트에 보호 된 Linux VM에서 다음 리소스를 제공 해야 합니다.

- Windows Server 버전 1709 이상을 실행 하는 가상화 capababilities 사용 하 여 서버
- 두 번째 컴퓨터 (Windows 10 또는 Windows Server 2016)는 실행 중인 VM의 콘솔에 연결 하려면 Hyper-v 관리자를 실행할 수 있는
- 지원 되는 Linux 중 하나에 대 한 ISO 이미지 차폐 VM Os:
    - 4.4 커널로 Ubuntu 16.04 LTS
    - Red Hat Enterprise Linux 7.3
    - SUSE Linux Enterprise Server 12 서비스 팩 2
- Lsvmtools 패키지 및 OS 업데이트를 다운로드 하려면 인터넷 액세스

> [!IMPORTANT]
> 보호 된 Vm을 최신 버전의 이전 Linux Os로 성공적으로 프로 비전 되지 것입니다 알려진된 TPM 드라이버 버그를 포함할 수 있습니다.
> 템플릿을 업데이트 하거나 보호 된 Vm을 최신 버전으로 사용할 수 있는 수정 될 때까지는 권장 되지 않습니다.
> 목록 위의 지원 되는 Os 업데이트를 공용으로 설정 하는 경우 업데이트 됩니다.

## <a name="prepare-a-linux-vm"></a>Linux VM 준비

보안 템플릿 디스크에서 보호 된 Vm은 만듭니다.
템플릿 디스크 VM에 대해 메타 데이터를 /boot 및 /root 파티션의 디지털 서명을 포함 하 여 핵심 OS 구성 요소를 배포 하기 전에 수정 되지 않습니다 있도록 운영 체제를 포함 합니다.

템플릿 디스크를 만들려면 먼저 향후 보호 된 Vm에 대 한 기본 이미지 준비를 하는 일반 (차폐 되지 않은) VM을 만들어야 합니다.
이 VM에 구성 변경 내용을 확인 하 고 설치 하는 소프트웨어는이 템플릿 디스크에서 생성 된 모든 보호 된 Vm에 적용 됩니다.
이러한 단계는 Linux VM templatization 준비 완전 최소 요구 사항을 안내 합니다.

> [!NOTE]
> Linux 디스크 암호화는 디스크 분할 되 면 구성 됩니다.
> 이 즉, Linux를 만들려면 dm 암호화를 사용 하 여 미리 암호화 된 새 VM을 만들어야 하는 VM 템플릿 디스크를 보호 합니다.


1.  가상화 서버에서 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행 하 여 Hyper-v 및 호스트 보호 Hyper-v 지원 기능 설치 되어 있는지 확인 합니다.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2.  신뢰할 수 있는 원본에서 ISO 이미지를 다운로드 하 고 가상화 서버에서 또는 가상화 서버에 액세스할 수 있는 파일 공유에 저장 합니다.

3.  Windows Server 버전 1709 실행 중인 관리 컴퓨터에 다음 명령을 실행 하 여 보호 된 VM 원격 서버 관리 도구를 설치 합니다.

    ```powershell
    Install-WindowsFeature RSAT-Shielded-VM-Tools
    ```

4.  오픈 **Hyper-v 관리자** 관리 컴퓨터에 가상화 서버에 연결 합니다.
    "Connect to Server..."를 클릭 하 여이 수행할 수 있습니다. 작업 창에서 또는에서 Hyper-v 관리자에서 클릭 하 고 선택 "서버에 연결..." Hyper-v 서버에 대 한 DNS 이름을 제공 하 고 하는 데 필요한 자격 증명에 연결 합니다.

5.  Hyper-v 관리자를 사용 하 여 [외부 스위치 구성](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines) Linux VM을 업데이트를 얻기 위해 인터넷에 액세스할 수 있도록 가상화 서버에서.

6.  다음으로 Linux OS를 설치 하려면 새 가상 머신을 만듭니다.
    작업 창에서 클릭 **새로 만들기** > **가상 머신** 마법사를 표시 합니다.
    "Pre-templatized Linux"와 같은 VM에 대 한 친숙 한 이름을 입력 하 고 클릭 **다음**합니다.

7.  마법사의 두 번째 페이지에서 선택 **2 세대** 는 VM이 UEFI 기반 펌웨어 프로필로 프로 비전 되도록 합니다.

8.  기본 설정에 따라 마법사의 나머지 단계를 완료 합니다.
    이 VM을에 차이점 보관용 디스크를 사용 하지 마세요 보호 된 VM 템플릿 디스크는 차이점 보관용 디스크를 사용할 수 없습니다.
    마지막으로 이전에 다운로드 한 가상 DVD 드라이브에이 VM의 OS를 설치할 수 있도록 ISO 이미지에 연결 합니다.

9.  Hyper-v 관리자에서 새로 만든 VM을 선택 하 고 클릭 **연결 하는 중...**  VM의 가상 콘솔을 연결할 작업 창에서.
    표시 되는 창에서 클릭 **시작** 를 가상 컴퓨터를 켭니다.

10. 선택한 Linux 배포에 대 한 설치 프로세스를 진행 합니다.
    각 Linux 배포는 다른 설치 마법사를 사용 하는 동안에 Linux 될 Vm 차폐 VM 템플릿 디스크에 대 한 다음 요구 사항은 충족 되어야 합니다.

    - 충분 테이블 (GPT (GUID) 레이아웃을 사용 하 여 디스크를 분할 해야 합니다.
    - 루트 파티션에 dm 암호화를 사용 하 여 암호화 되어야 합니다. 암호 설정 해야 **암호** (모두 소문자). 이 암호는 임의 수 및 파티션 보호 된 VM을 프로 비전 될 때 다시 암호화 합니다.
    - 부팅 파티션을 사용 해야 합니다 **ext2** 파일 시스템

11. Linux OS가 부팅 완벽 하 게 로그인 하 고 linux 가상 커널 및 연결 된 Hyper-v integration services 패키지를 설치 하는 것이 좋습니다.
    또한 SSH 서버 또는 보호 되 면 VM에 액세스 하려면 다른 원격 관리 도구를 설치 해야 합니다.

    Ubuntu에서 이러한 구성 요소를 설치 하려면 다음 명령을 실행 합니다.

    ```bash
    sudo apt-get install linux-virtual linux-tools-virtual linux-cloud-tools-virtual linux-image-extra-virtual openssh-server
    ```

    RHEL에서 다음 명령을 대신 실행 합니다.

    ```bash
    sudo yum install hyperv-daemons openssh-server
    sudo service sshd start
    ```

    및 SLES에서 다음 명령을 실행 합니다.

    ```bash
    sudo zypper install hyper-v
    sudo chkconfig hv_kvp_daemon on
    sudo systemctl enable sshd
    ```

12. 필요에 따라 Linux OS를 구성 합니다.
    모든 소프트웨어를 설치 하기에 추가한 사용자 계정 및 시스템 전반에 걸쳐 구성 변경 하면이 템플릿 디스크에서 생성 된 이후 모든 Vm에 적용 됩니다.
    디스크에 모든 암호 또는 불필요 한 패키지를 저장 하지 마십시오.

13. System Center Virtual Machine Manager 사용 하 여 Vm을 배포 하려는 경우 VM 프로 비전 하는 동안 OS를 특수화 하는 VMM을 사용 하도록 설정 하려면 VMM 게스트 에이전트를 설치 합니다.
    특수화에는 각 VM을 다른 사용자와 SSH 키, 네트워킹 구성 및 사용자 지정 설치 단계를 사용 하 여 안전 하 게 설정할 수 있습니다.
    에 대해 알아봅니다 하는 방법 [받아서 VMM 게스트 에이전트를 설치](https://docs.microsoft.com/system-center/vmm/vm-linux#install-the-vmm-guest-agent) VMM 설명서에서.

14. 그런 다음, [패키지 관리자에 게 Microsoft Linux 소프트웨어 리포지토리에서 추가](../../administration/linux-package-repository-for-microsoft-software.md)합니다.

15. Linux를 포함 하는 lsvmtools 패키지 설치 구성 요소 및 디스크 준비 도구를 프로 비전 되는 VM 부팅 로더 shim 보호 된 패키지 관리자를 사용 합니다.

    ```bash
    # Ubuntu 16.04
    sudo apt-get install lsvmtools

    # SLES 12 SP2
    sudo zypper install lsvmtools

    # RHEL 7.3
    sudo yum install lsvmtools
    ```

14. 완료 되 면 시스템에서 lsvmprep 설치 프로그램을 찾을 Linux OS 사용자 지정 및 실행 합니다.
    
    ```bash
    # The path below may change based on the version of lsvmprep installed
    # Run "find /opt -name lsvmprep" to locate the lsvmprep executable
    sudo /opt/lsvmtools-1.0.0-x86-64/lsvmprep
    ```

15. VM을 종료 합니다.

16. Windows 10 Fall Creators Update 사용 하 여 Hyper-v에서 생성 하는 자동 검사점 등 VM의 검사점을 진행 하려면 계속 하기 전에 삭제 해야 합니다.
    검사점은 템플릿 디스크 마법사가 지원 되지 않는 차이점 보관용 디스크 (.avhdx)를 만듭니다.
    
    검사점을 삭제 하려면 엽니다 **Hyper-v 관리자**VM을 선택, 검사점 창의 맨 위에 있는 검사점을 마우스 오른쪽 단추로 클릭 차례로 클릭 **검사점 하위 트리 삭제**합니다.

    ![Hyper-v 관리자에서 템플릿 VM에 대 한 모든 검사점 삭제](../media/Guarded-Fabric-Shielded-VM/delete-checkpoints-lsvm-template.png)

## <a name="protect-the-template-disk"></a>템플릿 디스크를 보호 합니다.

이전 섹션에서 준비한 VM 보호 된 VM 템플릿 디스크를 Linux로 사용할 준비가 거의 되었습니다.
마지막 단계를 해시 하 고 루트 및 부팅 파티션의 현재 상태에 디지털 서명 템플릿 디스크 마법사를 통해 디스크를 실행 하는 것입니다.
보호 된 VM 템플릿 만들기 및 배포 사이 두 개의 파티션에 무단된 변경 된 내용이 있는지 확인 하는 프로 비전 될 때 디지털 서명을 확인 하 고 해시 확인 됩니다.

### <a name="obtain-a-certificate-to-sign-the-disk"></a>디스크를 서명 하려면 인증서 가져오기

디스크 측정을 디지털 서명 하기 위해 템플릿 디스크 마법사를 실행할 컴퓨터의 인증서를 가져올 해야 합니다.
인증서에는 다음 요구 사항을 충족 해야 합니다.

인증서 속성 | 필요한 값
---------------------|---------------
키 알고리즘 | RSA
최소 키 크기 | 2048 비트
서명 알고리즘 | SHA256 (권장)
키 사용 | 디지털 서명

이 인증서에 대 한 세부 정보는 보호 데이터 파일을 만들고 디스크를 신뢰 권한을 부여 하는 경우 테 넌 트에 표시 됩니다.
따라서 것이 중요 한 테 넌 트 상호 신뢰할 수 있는 인증 기관에서이 인증서를 가져와야 합니다.
호스팅 서비스 공급자 및 테 넌 트 둘 다 있는 엔터프라이즈 시나리오에서이 인증서를 엔터프라이즈 인증 기관에서 발급 하는 것을 고려할 수 있습니다.
이 인증서를 신중 하 게 보호, 새 템플릿 디스크를 인증 디스크와 동일 하 게 신뢰 하는이 인증서를 소유한 모든 사용자가 만들 수 있습니다.

테스트 랩 환경에서 다음 PowerShell 명령을 사용 하 여 자체 서명 된 인증서를 만들 수 있습니다.

```powershell
New-SelfSignedCertificate -Subject "CN=Linux Shielded VM Template Disk Signing Certificate"
```

### <a name="process-the-disk-with-the-template-disk-wizard-cmdlet"></a>프로세스 템플릿 디스크 마법사 cmdlet 사용 하 여 디스크

Windows Server 버전 1709 실행 하는 컴퓨터에 인증서 확인 하 고 템플릿 디스크를 복사한 서명 프로세스를 시작 하려면 다음 명령을 실행 합니다.
VHDX에 제공 하는 `-Path` 매개 변수는 업데이트 된 템플릿 디스크를 사용 하 여 덮어쓸 수, 명령을 실행 하기 전에 복사본을 확인 해야 합니다.

> [!IMPORTANT]
> 보호 된 Linux를 준비 하려면 Windows Server 2016 또는 Windows 10에서 사용할 수 있는 원격 서버 관리 도구를 사용할 수 없습니다 VM 템플릿 디스크.
> 만 사용 합니다 [보호 TemplateDisk](https://docs.microsoft.com/powershell/module/shieldedvmtemplate/protect-templatedisk?view=win10-ps) Linux를 준비 하려면 Windows Server, 버전 1709 또는 Windows Server 2019에서 사용할 수 있는 원격 서버 관리 도구에서 사용할 수 있는 cmdlet 차폐 VM 템플릿 디스크.

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Path 'C:\temp\MyLinuxTemplate.vhdx' -TemplateName 'Ubuntu 16.04' -Version 1.0.0.0 -Certificate $certificate -ProtectedTemplateTargetDiskType PreprocessedLinux
```

템플릿 디스크에 보호 된 Linux Vm 프로 비전 하는 데 사용할 준비가 되었습니다.
System Center Virtual Machine Manager VM을 배포 하려면를 사용 하는 경우 VMM 라이브러리에 VHDX를 이제 복사할 수 있습니다.

VHDX에서 볼륨 서명 카탈로그를 추출할 수도 있습니다.
이 파일은 사용 하 여 사용자 템플릿을 사용 하려는 VM 소유자에 게 서명 인증서, 디스크 이름 및 버전에 대 한 정보를 제공 합니다.
실딩 데이터 파일 마법사를 만들려면이 서명 인증서의 소유에서를 템플릿 작성자에 게 권한을 부여 하려면이 파일을 가져올 필요가 및 향후 템플릿 디스크에 있습니다.

볼륨 서명 카탈로그를 추출 하려면 PowerShell에서 다음 명령을 실행 합니다.

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```
