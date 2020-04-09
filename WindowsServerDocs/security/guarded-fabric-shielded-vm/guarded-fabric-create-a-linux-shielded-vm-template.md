---
title: Linux 차폐 VM 템플릿 디스크 만들기
ms.prod: windows-server
ms.topic: article
ms.assetid: d0e1d4fb-97fc-4389-9421-c869ba532944
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 1a6325a5d8e931f1e62c83ba4013d94760e39f86
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856796"
---
# <a name="create-a-linux-shielded-vm-template-disk"></a>Linux 차폐 VM 템플릿 디스크 만들기

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), 

이 항목에서는 하나 이상의 테 넌 트 Vm을 인스턴스화하는 데 사용할 수 있는 Linux 차폐 Vm의 템플릿 디스크를 준비 하는 방법에 대해 설명 합니다.

## <a name="prerequisites"></a>필수 조건

Linux 차폐 VM을 준비 하 고 테스트 하려면 다음 리소스를 사용할 수 있어야 합니다.

- Windows Server 버전 1709 이상을 실행 하는 가상화 capababilities을 갖춘 서버
- Hyper-v 관리자를 실행 하 여 실행 중인 VM의 콘솔에 연결할 수 있는 두 번째 컴퓨터 (Windows 10 또는 Windows Server 2016)
- 지원 되는 Linux 차폐 VM Os 중 하나에 대 한 ISO 이미지:
    - 4\.4 커널을 사용 하는 Ubuntu 16.04 LTS
    - Red Hat Enterprise Linux 7.3
    - SUSE Linux Enterprise Server 12 서비스 팩 2
- Lsvmtools 패키지 및 OS 업데이트를 다운로드 하기 위한 인터넷 액세스

> [!IMPORTANT]
> 이전 Linux Os의 최신 버전에는 보호 된 Vm으로 성공적으로 프로 비전 할 수 없도록 하는 알려진 TPM 드라이버 버그가 포함 될 수 있습니다.
> 수정 프로그램을 사용할 수 있을 때까지 템플릿이나 보호 된 Vm을 최신 릴리스로 업데이트 하지 않는 것이 좋습니다.
> 업데이트를 공용으로 설정 하면 위의 지원 되는 Os 목록이 업데이트 됩니다.

## <a name="prepare-a-linux-vm"></a>Linux VM 준비

보호 된 Vm은 보안 템플릿 디스크에서 생성 됩니다.
템플릿 디스크에는 배포 전에 핵심 OS 구성 요소가 수정 되지 않도록/boot 및/root 파티션의 디지털 서명을 포함 하 여 VM 및 메타 데이터에 대 한 운영 체제가 포함 됩니다.

템플릿 디스크를 만들려면 나중에 보호 되는 Vm에 대 한 기본 이미지로 준비할 일반 (보호 되지 않는) VM을 먼저 만들어야 합니다.
이 VM에 대해 설치 하는 소프트웨어와 구성 변경 내용은이 템플릿 디스크에서 만든 모든 보호 된 Vm에 적용 됩니다.
이러한 단계에서는 templatization에 대 한 Linux VM을 준비 하기 위한 최소 요구 사항을 안내 합니다.

> [!NOTE]
> Linux 디스크 암호화는 디스크가 분할 될 때 구성 됩니다.
> 즉, 보호 된 Linux VM 템플릿 디스크를 만들기 위해 dm을 사용 하 여 미리 암호화 된 새 VM을 만들어야 합니다.


1.  가상화 서버에서 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행 하 여 Hyper-v 및 호스트 보호자 지원 기능이 설치 되어 있는지 확인 합니다.

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2.  신뢰할 수 있는 원본에서 ISO 이미지를 다운로드 하 고 가상화 서버 또는 가상화 서버에 액세스할 수 있는 파일 공유에 저장 합니다.

3.  Windows Server 버전 1709을 실행 하는 관리 컴퓨터에서 다음 명령을 실행 하 여 보호 된 VM 원격 서버 관리 도구를 설치 합니다.

    ```powershell
    Install-WindowsFeature RSAT-Shielded-VM-Tools
    ```

4.  관리 컴퓨터에서 **Hyper-v 관리자** 를 열고 가상화 서버에 연결 합니다.
    "서버에 연결 ..."을 클릭 하 여이 작업을 수행할 수 있습니다. 작업 창에서 또는 Hyper-v 관리자를 마우스 오른쪽 단추로 클릭 하 고 "서버에 연결 ..."을 선택 합니다. Hyper-v 서버에 대 한 DNS 이름을 제공 하 고 필요한 경우 연결 하는 데 필요한 자격 증명을 제공 합니다.

5.  Hyper-v 관리자를 사용 하 여 Linux VM이 인터넷에 액세스 하 여 업데이트를 받을 수 있도록 가상화 서버에서 [외부 스위치를 구성](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines) 합니다.

6.  그런 다음 Linux OS를 설치할 새 가상 머신을 만듭니다.
    작업 창에서 **새로 만들기** > **가상 컴퓨터** 를 클릭 하 여 마법사를 엽니다.
    VM에 대 한 친숙 한 이름 (예: "사전 템플릿 화 Linux")을 입력 하 고 **다음**을 클릭 합니다.

7.  마법사의 두 번째 페이지에서 **2 세대** 를 선택 하 여 VM이 UEFI 기반 펌웨어 프로필로 프로 비전 되도록 합니다.

8.  기본 설정에 따라 마법사의 나머지 단계를 완료 합니다.
    이 VM에 차이점 보관용 디스크를 사용 하지 마십시오. 보호 된 VM 템플릿 디스크는 차이점 보관용 디스크를 사용할 수 없습니다.
    마지막으로, OS를 설치할 수 있도록 이전에 다운로드 한 ISO 이미지를이 VM에 대 한 가상 DVD 드라이브에 연결 합니다.

9.  Hyper-v 관리자에서 새로 만든 VM을 선택 하 고 작업 창에서 **연결 ...** 을 클릭 하 여 vm의 가상 콘솔에 연결 합니다.
    표시 되는 창에서 **시작** 을 클릭 하 여 가상 머신을 설정 합니다.

10. 선택한 Linux 배포에 대 한 설치 프로세스를 진행 합니다.
    각 Linux 배포판에서 다른 설치 마법사를 사용 하는 동안 Linux 차폐 VM 템플릿 디스크가 될 Vm의 경우 다음 요구 사항을 충족 해야 합니다.

    - GPT (GUID 분할 Table) 레이아웃을 사용 하 여 디스크를 분할 해야 합니다.
    - 루트 파티션은 dm-로 암호화 되어야 합니다. 암호는 **암호** (모두 소문자)로 설정 해야 합니다. 이 암호는 임의로 제공 되며 차폐 VM이 프로 비전 되 면 파티션이 다시 암호화 됩니다.
    - 부팅 파티션은 **ext2** 파일 시스템을 사용 해야 합니다.

11. Linux OS가 완전히 부팅 되 고 로그인 한 후에는 linux 가상 커널 및 관련 Hyper-v integration services 패키지를 설치 하는 것이 좋습니다.
    또한 SSH 서버 또는 다른 원격 관리 도구를 설치 하 여 보호 된 VM에 액세스 하는 것이 좋습니다.

    Ubuntu에서 다음 명령을 실행 하 여 이러한 구성 요소를 설치 합니다.

    ```bash
    sudo apt-get install linux-virtual linux-tools-virtual linux-cloud-tools-virtual linux-image-extra-virtual openssh-server
    ```

    RHEL에서 다음 명령을 대신 실행 합니다.

    ```bash
    sudo yum install hyperv-daemons openssh-server
    sudo service sshd start
    ```

    SLES에서 다음 명령을 실행 합니다.

    ```bash
    sudo zypper install hyper-v
    sudo chkconfig hv_kvp_daemon on
    sudo systemctl enable sshd
    ```

12. Linux OS를 원하는 대로 구성 합니다.
    사용자가 설치 하는 모든 소프트웨어, 추가 하는 사용자 계정 및 시스템의 전체 구성 변경 사항은이 템플릿 디스크에서 만든 모든 이후 Vm에 적용 됩니다.
    암호 또는 불필요 한 패키지를 디스크에 저장 하지 않는 것이 좋습니다.

13. System Center Virtual Machine Manager를 사용 하 여 Vm을 배포 하려는 경우 vmm 게스트 에이전트를 설치 하 여 VM을 프로 비전 하는 동안 VMM에서 OS를 특수화할 수 있도록 합니다.
    특수화를 사용 하면 각 VM을 여러 사용자 및 SSH 키, 네트워킹 구성 및 사용자 지정 설치 단계로 안전 하 게 설정할 수 있습니다.
    Vmm 설명서에서 [vmm 게스트 에이전트를 다운로드 하 고 설치](https://docs.microsoft.com/system-center/vmm/vm-linux#install-the-vmm-guest-agent) 하는 방법에 대해 알아봅니다.

14. 그런 다음 [패키지 관리자에 Microsoft Linux 소프트웨어 리포지토리를 추가](../../administration/linux-package-repository-for-microsoft-software.md)합니다.

15. 패키지 관리자를 사용 하 여 Linux 차폐 VM 부팅 로더 shim, 프로 비전 구성 요소 및 디스크 준비 도구를 포함 하는 lsvmtools 패키지를 설치 합니다.

    ```bash
    # Ubuntu 16.04
    sudo apt-get install lsvmtools

    # SLES 12 SP2
    sudo zypper install lsvmtools

    # RHEL 7.3
    sudo yum install lsvmtools
    ```

14. Linux OS 사용자 지정이 완료 되 면 시스템에서 lsvmprep 설치 프로그램을 찾아 실행 합니다.
    
    ```bash
    # The path below may change based on the version of lsvmprep installed
    # Run "find /opt -name lsvmprep" to locate the lsvmprep executable
    sudo /opt/lsvmtools-1.0.0-x86-64/lsvmprep
    ```

15. VM을 종료 합니다.

16. VM의 검사점을 만든 경우 (Windows 10 자동 생성기 업데이트를 사용 하 여 Hyper-v에서 만든 자동 검사점 포함) 계속 하기 전에 삭제 해야 합니다.
    검사점은 템플릿 디스크 마법사에서 지원 되지 않는 차이점 보관용 디스크 (. .avhdx)를 만듭니다.
    
    검사점을 삭제 하려면 **Hyper-v 관리자**를 열고, VM을 선택 하 고, 검사점 창에서 가장 위쪽의 검사점을 마우스 오른쪽 단추로 클릭 한 다음 **검사점 하위 트리 삭제**를 클릭 합니다.

    ![Hyper-v 관리자에서 템플릿 VM에 대 한 모든 검사점 삭제](../media/Guarded-Fabric-Shielded-VM/delete-checkpoints-lsvm-template.png)

## <a name="protect-the-template-disk"></a>템플릿 디스크 보호

이전 섹션에서 준비한 VM은 Linux 차폐 VM 템플릿 디스크로 사용할 준비가 거의 완료 되었습니다.
마지막 단계는 루트 및 부팅 파티션의 현재 상태를 해시 하 고 디지털 서명 하는 템플릿 디스크 마법사를 통해 디스크를 실행 하는 것입니다.
해시 및 디지털 서명은 보호 된 VM을 프로 비전 하 여 템플릿 생성 및 배포 사이에 두 파티션이 무단으로 변경 되지 않도록 하는 경우에 확인 됩니다.

### <a name="obtain-a-certificate-to-sign-the-disk"></a>디스크에 서명할 인증서 가져오기

디스크 측정에 디지털 서명 하려면 템플릿 디스크 마법사를 실행 하는 컴퓨터에서 인증서를 얻어야 합니다.
인증서는 다음 요구 사항을 충족 해야 합니다.

Certificate 속성 | 필요한 값
---------------------|---------------
키 알고리즘 | RSA
최소 키 크기 | 2048비트
서명 알고리즘 | SHA256 (권장)
키 사용 | 디지털 서명

이 인증서에 대 한 세부 정보는 해당 보호 데이터 파일을 만들고 신뢰할 수 있는 디스크에 권한을 부여 하는 경우 테 넌 트에 표시 됩니다.
따라서 사용자 및 사용자의 테 넌 트가 상호 신뢰 하는 인증 기관에서이 인증서를 얻어야 합니다.
호스터 및 테 넌 트 인 엔터프라이즈 시나리오에서는 엔터프라이즈 인증 기관에서이 인증서를 발급 하는 것을 고려할 수 있습니다.
이 인증서를 소유 하는 모든 사용자가 인증 디스크와 동일한 방법으로 신뢰할 수 있는 새 템플릿 디스크를 만들 수 있으므로이 인증서를 신중 하 게 보호 합니다.

테스트 랩 환경에서 다음 PowerShell 명령을 사용 하 여 자체 서명 된 인증서를 만들 수 있습니다.

```powershell
New-SelfSignedCertificate -Subject "CN=Linux Shielded VM Template Disk Signing Certificate"
```

### <a name="process-the-disk-with-the-template-disk-wizard-cmdlet"></a>템플릿 디스크 마법사 cmdlet을 사용 하 여 디스크 처리

Windows Server, 버전 1709을 실행 하는 컴퓨터에 템플릿 디스크 및 인증서를 복사한 후 다음 명령을 실행 하 여 서명 프로세스를 시작 합니다.
`-Path` 매개 변수에 제공 하는 VHDX는 업데이트 된 템플릿 디스크로 덮어쓰여집니다. 따라서 명령을 실행 하기 전에 복사본을 만들어야 합니다.

> [!IMPORTANT]
> Windows Server 2016 또는 Windows 10에서 사용할 수 있는 원격 서버 관리 도구는 Linux 차폐 VM 템플릿 디스크를 준비 하는 데 사용할 수 없습니다.
> Windows Server, 버전 1709 및 Windows Server 2019에서 사용할 수 있는 원격 서버 관리 도구 [보호 템플릿 디스크](https://docs.microsoft.com/powershell/module/shieldedvmtemplate/protect-templatedisk?view=win10-ps) cmdlet만 사용 하 여 보호 된 Linux VM 템플릿 디스크를 준비할 수 있습니다.

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Path 'C:\temp\MyLinuxTemplate.vhdx' -TemplateName 'Ubuntu 16.04' -Version 1.0.0.0 -Certificate $certificate -ProtectedTemplateTargetDiskType PreprocessedLinux
```

이제 템플릿 디스크를 사용 하 여 Linux 차폐 Vm을 프로 비전 할 준비가 되었습니다.
System Center Virtual Machine Manager를 사용 하 여 VM을 배포 하는 경우 이제 VHDX를 VMM 라이브러리에 복사할 수 있습니다.

VHDX에서 볼륨 서명 카탈로그를 추출할 수도 있습니다.
이 파일은 템플릿을 사용 하려는 VM 소유자에 게 서명 인증서, 디스크 이름 및 버전에 대 한 정보를 제공 하는 데 사용 됩니다.
이 파일을 보호 데이터 파일 마법사에 추가 하 여 서명 인증서를 소유 하는 템플릿 작성자에 게이 및 향후의 템플릿 디스크를 만들 수 있는 권한을 부여 해야 합니다.

볼륨 서명 카탈로그를 추출 하려면 PowerShell에서 다음 명령을 실행 합니다.

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```
