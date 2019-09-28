---
title: Windows 차폐 VM 템플릿 디스크 만들기
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 9c8b84e8-1f5a-47a1-83ca-b1dbd801cb0b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/29/2019
ms.openlocfilehash: 686fd2ed5969d191240bbd726f1d759e9974f08a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386684"
---
# <a name="create-a-windows-shielded-vm-template-disk"></a>Windows 차폐 VM 템플릿 디스크 만들기

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

일반 Vm과 마찬가지로 테 넌 트와 관리자가 템플릿 디스크를 사용 하 여 패브릭에 새 Vm을 쉽게 배포할 수 있도록 VM 템플릿 (예: [Virtual Machine Manager (VMM)의 vm 템플릿](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-library-add-vm-templates))을 만들 수 있습니다. 차폐 Vm은 보안에 민감한 자산 이므로 차폐를 지 원하는 VM 템플릿을 만들기 위한 추가 단계가 있습니다. 이 항목에서는 VMM에서 보호 된 템플릿 디스크 및 VM 템플릿을 만드는 단계에 대해 설명 합니다.

이 항목이 보호 된 Vm을 배포 하는 전체 프로세스에 어떻게 부합 하는지 이해 하려면 [보호 된 호스트 및 보호 된 vm에 대 한 서비스 공급자 구성 단계 호스팅](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)을 참조 하세요.

## <a name="prepare-an-operating-system-vhdx"></a>운영 체제 VHDX 준비

먼저 차폐 템플릿 디스크 만들기 마법사를 통해 실행 되는 OS 디스크를 준비 합니다. 이 디스크는 테 넌 트의 Vm에서 OS 디스크로 사용 됩니다. 기존 도구를 사용 하 여이 디스크를 만들 수 있습니다 (예: DISM (Microsoft Desktop Image Service Manager)). 또는 새 VHDX를 사용 하 여 VM을 수동으로 설정 하 고 해당 디스크에 OS를 설치 합니다. 디스크를 설정 하는 경우 2 세대 및/또는 차폐 Vm과 관련 된 다음 요구 사항을 준수 해야 합니다. 

| VHDX에 대 한 요구 사항 | Reason |
|-----------|----|
|GPT (GUID 파티션 테이블) 디스크 여야 합니다. | UEFI를 지원 하기 위해 2 세대 가상 컴퓨터에 필요|
|디스크 유형은 **동적**이 아닌 **기본** 이어야 합니다. <br>참고: 이는 Hyper-v에서 지 원하는 "동적 확장" VHDX 기능이 아니라 논리 디스크 유형을 나타냅니다. | BitLocker는 동적 디스크를 지원 하지 않습니다.|
|디스크에 파티션이 두 개 이상 있습니다. 한 파티션에는 Windows가 설치 된 드라이브가 포함 되어야 합니다. BitLocker가 암호화 하는 드라이브입니다. 다른 파티션은 부팅 로더를 포함 하 고 컴퓨터를 시작할 수 있도록 암호화 되지 않은 상태로 유지 되는 활성 파티션입니다.|BitLocker에 필요|
|파일 시스템이 NTFS입니다. | BitLocker에 필요|
|VHDX에 설치 된 운영 체제는 다음 중 하나입니다.<br>-Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 <br>-Windows 10, Windows 8.1, Windows 8| 2 세대 가상 컴퓨터 및 Microsoft 보안 부팅 템플릿을 지 원하는 데 필요 합니다.|
|운영 체제를 일반화 해야 합니다 (sysprep.exe 실행). | 템플릿 프로 비전에는 특정 테 넌 트의 작업에 대 한 특수화 Vm이 포함 됩니다.| 

> [!NOTE]
> VMM을 사용 하는 경우이 단계에서 VMM 라이브러리에 템플릿 디스크를 복사 하지 마십시오. 

## <a name="run-windows-update-on-the-template-operating-system"></a>템플릿 운영 체제에서 Windows 업데이트 실행

템플릿 디스크에서 운영 체제에 최신 Windows 업데이트가 설치 되어 있는지 확인 합니다. 최근 릴리스된 업데이트는 템플릿 운영 체제가 최신 상태가 아닌 경우 완료 되지 못할 수 있는 프로세스 인 종단 간 보호 프로세스의 안정성을 향상 시킵니다.

## <a name="prepare-and-protect-the-vhdx-with-the-template-disk-wizard"></a>템플릿 디스크 마법사를 사용 하 여 VHDX 준비 및 보호

보호 된 Vm에서 템플릿 디스크를 사용 하려면 차폐 템플릿 디스크 만들기 마법사를 사용 하 여 BitLocker를 사용 하 여 디스크를 준비 하 고 암호화 해야 합니다. 이 마법사는 디스크에 대 한 해시를 생성 하 여 VSC (볼륨 서명 카탈로그)에 추가 합니다. VSC는 지정 하는 인증서를 사용 하 여 서명 되 고, 프로 비전 프로세스 중에 테 넌 트에 대해 배포 되는 디스크가 변경 되지 않았는지 확인 하거나 테 넌 트가 신뢰 하지 않는 디스크로 대체 되도록 하는 데 사용 됩니다. 마지막으로 VM을 프로 비전 하는 동안 디스크의 암호화를 준비 하기 위해 BitLocker가 디스크의 운영 체제에 설치 됩니다 (아직 없는 경우).

> [!NOTE]
> 템플릿 디스크 마법사는 현재 위치의 지정 된 템플릿 디스크를 수정 합니다. 마법사를 실행 하 여 나중에 디스크를 업데이트할 때까지 보호 되지 않는 VHDX의 복사본을 만들 수 있습니다. 템플릿 디스크 마법사를 사용 하 여 보호 된 디스크는 수정할 수 없습니다.

Windows Server 2016를 실행 하는 컴퓨터에서 다음 단계를 수행 합니다 (보호 된 호스트나 VMM 서버가 될 필요는 없음).

1. [운영 체제 VHDX](#prepare-an-operating-system-vhdx) 를 서버에 준비 (아직 없는 경우) 하 여 만든 일반화 된 vhdx를 복사 합니다.

2. 서버를 로컬로 관리 하려면 서버에 **원격 서버 관리 도구** 에서 **보호 된 VM 도구** 기능을 설치 합니다.

        Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
        
    [Windows 10 원격 서버 관리 도구](https://www.microsoft.com/en-us/download/details.aspx?id=45520)가 설치 된 클라이언트 컴퓨터에서 서버를 관리할 수도 있습니다.

3. 새 보호 된 Vm의 템플릿 디스크가 될 VHDX에 대 한 VSC를 서명할 인증서를 가져오거나 만듭니다. 이 인증서에 대 한 세부 정보는 해당 보호 데이터 파일을 만들고 신뢰할 수 있는 디스크에 권한을 부여 하는 경우 테 넌 트에 표시 됩니다. 따라서 사용자 및 사용자의 테 넌 트가 상호 신뢰 하는 인증 기관에서이 인증서를 얻어야 합니다. 호스터 및 테 넌 트 인 엔터프라이즈 시나리오에서는 PKI에서이 인증서를 발급 하는 것을 고려할 수 있습니다.

    테스트 환경을 설정 하 고 자체 서명 된 인증서를 사용 하 여 템플릿 디스크를 준비 하려는 경우 다음과 유사한 명령을 실행 합니다.

        New-SelfSignedCertificate -DnsName publisher.fabrikam.com

4. 시작 메뉴의 **관리 도구** 폴더에서 **템플릿 디스크 마법사** 를 시작 하거나 명령 프롬프트에 템플릿 **disk마법사나 .Exe** 를 입력 하 여 템플릿 디스크 마법사를 시작 합니다.

5. **인증서** 페이지에서 **찾아보기** 를 클릭 하 여 인증서 목록을 표시 합니다. 디스크 템플릿을 준비 하는 데 사용할 인증서를 선택 합니다. **확인**을 클릭하고 **다음**을 클릭합니다.

6. 가상 디스크 페이지에서 **찾아보기** 를 클릭 하 여 준비한 VHDX를 선택 하 고 **다음**을 클릭 합니다.

7. 서명 카탈로그 페이지에서 **디스크 이름** 및 버전을 제공 **합니다.** 이러한 필드는 준비 된 후 디스크를 식별 하는 데 도움이 되는 정보를 제공 합니다.

    예를 들어 **디스크 이름** 에 대해 _WS2016_ 를 입력 하 고 **버전**, _1.0.0.0_ 을 입력할 수 있습니다.

8. 마법사의 설정 검토 페이지에서 선택 사항을 검토 합니다. **생성**을 클릭 하면 마법사가 템플릿 디스크에서 BitLocker를 사용 하도록 설정 하 고, 디스크의 해시를 계산 하 고, VHDX 메타 데이터에 저장 되는 볼륨 서명 카탈로그를 만듭니다.

    준비 프로세스가 완료 될 때까지 기다렸다가 템플릿 디스크를 탑재 하거나 이동 하려고 합니다. 디스크 크기에 따라이 프로세스를 완료 하는 데 다소 시간이 걸릴 수 있습니다.

    > [!IMPORTANT]
    > 템플릿 디스크는 보호 된 보호 VM 프로 비전 프로세스 에서만 사용할 수 있습니다.
    > 템플릿 디스크를 사용 하 여 일반 (보호 되지 않는) VM을 부팅 하려고 하면 중지 오류 (파란색 화면)가 발생할 수 있으며,이는 지원 되지 않습니다.

9. **요약** 페이지에서 디스크 템플릿, VSC에 서명 하는 데 사용 되는 인증서 및 인증서 발급자에 대 한 정보가 표시 됩니다. **닫기**를 클릭하여 마법사를 종료합니다.

VMM을 사용 하는 경우이 항목의 나머지 섹션에 나오는 단계를 수행 하 여 VMM의 보호 된 VM 템플릿에 템플릿 디스크를 통합 합니다. 

## <a name="copy-the-template-disk-to-the-vmm-library"></a>VMM 라이브러리에 템플릿 디스크 복사

VMM을 사용 하는 경우 템플릿 디스크를 만든 후 VMM 라이브러리 공유에 복사 하 여 새 Vm을 프로 비전 할 때 호스트에서 디스크를 다운로드 하 고 사용할 수 있도록 해야 합니다. 다음 절차를 사용 하 여 템플릿 디스크를 VMM 라이브러리에 복사 하 고 라이브러리를 새로 고칩니다.

1. VHDX 파일을 VMM 라이브러리 공유 폴더에 복사 합니다. 기본 VMM 구성을 사용한 경우 템플릿 디스크를 _\\ @ no__t-2\MSSCVMMLibrary\VHDs_로 복사 합니다.

2. 라이브러리 서버를 새로 고칩니다. **라이브러리** 작업 영역을 열고 **라이브러리 서버**를 확장 하 고 새로 고칠 라이브러리 서버를 마우스 오른쪽 단추로 클릭 한 다음 **새로 고침**을 클릭 합니다.

3. 그런 다음 VMM에 템플릿 디스크에 설치 된 운영 체제에 대 한 정보를 제공 합니다.

    a. **라이브러리 작업 영역의** 라이브러리 서버에서 새로 가져온 템플릿 디스크를 찾습니다.

    b. 디스크를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.

    c. **운영 체제**의 경우 목록을 확장 하 고 디스크에 설치 된 운영 체제를 선택 합니다. 운영 체제를 선택 하는 것은 VMM에 VHDX가 비어 있지 않음을 나타냅니다.

    d. 속성을 업데이트한 경우 **확인**을 클릭합니다.

디스크 이름 옆의 작은 방패 아이콘은 디스크를 보호 된 Vm의 준비 된 템플릿 디스크로 나타냅니다. 열 머리글을 마우스 오른쪽 단추로 클릭 하 고 **차폐** 열을 설정/해제 하 여 디스크가 일반 또는 차폐 VM 배포용으로 사용 되는지 여부를 나타내는 텍스트 표현을 볼 수도 있습니다.

![보호 된 vm 템플릿 디스크](../media/Guarded-Fabric-Shielded-VM/shielded-vm-template-disk.png)

## <a name="create-the-shielded-vm-template-in-vmm-using-the-prepared-template-disk"></a>준비 된 템플릿 디스크를 사용 하 여 VMM에서 보호 된 VM 템플릿 만들기

VMM 라이브러리에 준비 된 템플릿 디스크가 있으면 보호 된 Vm에 대 한 VM 템플릿을 만들 준비가 된 것입니다. 보호 된 Vm에 대 한 VM 템플릿은 특정 설정 (2 세대 VM, UEFI 및 보안 부팅 사용 등)이 고정 되 고 다른 일부는 사용할 수 없게 된다는 점에서 기존 VM 템플릿과 약간 다릅니다. 테 넌 트 사용자 지정은 몇 가지 VM 속성을 선택 하는 것으로 제한 됩니다. . VM 템플릿을 만들려면 다음 단계를 수행 합니다.

1. **라이브러리** 작업 영역의 맨 위에 있는 홈 탭에서 **VM 템플릿 만들기** 를 클릭 합니다.

2. **원본 선택** 페이지에서 **라이브러리에 보관된 기존 VM 템플릿 또는 가상 하드 디스크 사용**을 클릭한 후 **찾아보기**를 클릭합니다.

3. 표시 되는 창에서 VMM 라이브러리의 준비 된 템플릿 디스크를 선택 합니다. 준비 된 디스크를 더 쉽게 식별 하려면 열 머리글을 마우스 오른쪽 단추로 클릭 하 고 **차폐** 열을 사용 하도록 설정 합니다. **확인** 을 클릭 한 후 **다음**을 클릭 합니다.

4. VM 템플릿 이름과 설명 (선택 사항)을 지정 하 고 **다음**을 클릭 합니다.

5. **하드웨어 구성** 페이지에서이 템플릿에서 만든 vm의 기능을 지정 합니다. VM 템플릿에서 하나 이상의 NIC를 사용할 수 있고 구성 했는지 확인 합니다. 테 넌 트가 보호 된 VM에 연결 하는 유일한 방법은 원격 데스크톱 연결, Windows 원격 관리 또는 네트워킹 프로토콜을 통해 작동 하는 미리 구성 된 다른 원격 관리 도구를 사용 하는 것입니다.

    테 넌 트 네트워크에서 DHCP 서버를 실행 하는 대신 VMM에서 고정 IP 풀을 활용 하도록 선택 하는 경우 테 넌 트에이 구성에 대 한 경고를 표시 해야 합니다. 테 넌 트가 VMM의 무인 파일을 포함 하는 보호 데이터 파일을 제공 하는 경우 고정 IP 풀 정보에 대 한 특수 한 자리 표시자 값을 제공 해야 합니다. 테 넌 트 무인 파일의 VMM 자리 표시자에 대 한 자세한 내용은 [응답 파일 만들기](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file)를 참조 하세요. 

6. **운영 체제 구성** 페이지에서 VMM은 제품 키, 표준 시간대 및 컴퓨터 이름을 포함 하 여 보호 된 vm에 대 한 몇 가지 옵션만 표시 합니다. 관리자 암호 및 도메인 이름과 같은 일부 보안 정보는 보호 데이터 파일 ()을 통해 테 넌 트에서 지정 합니다. PDK 파일). 

    > [!NOTE]
    > 이 페이지에서 제품 키를 지정 하도록 선택 하는 경우 템플릿 디스크의 운영 체제에 유효한 지 확인 합니다. 잘못 된 제품 키를 사용 하는 경우 VM 만들기가 실패 합니다.

템플릿을 만든 후 테 넌 트는이 템플릿을 사용 하 여 새 가상 컴퓨터를 만들 수 있습니다. VM 템플릿이 테넌트 관리자 사용자 역할에서 사용할 수 있는 리소스 중 하나 인지 확인 해야 합니다. VMM에서는 사용자 역할이 **설정** 작업 영역에 있습니다.

## <a name="prepare-and-protect-the-vhdx-using-powershell"></a>PowerShell을 사용 하 여 VHDX 준비 및 보호

템플릿 디스크 마법사를 실행 하는 대신 RSAT를 실행 하는 컴퓨터에 템플릿 디스크 및 인증서를 복사 하 고 [Protect-템플릿 디스크 @ no__t-1을 실행 하 여 서명 프로세스를 시작할 수 있습니다.
다음 예에서는 _TemplateName_ 및 _version_ 매개 변수에서 지정한 이름 및 버전 정보를 사용 합니다.
@No__t-0 매개 변수에 제공한 VHDX는 업데이트 된 템플릿 디스크로 덮어쓰여집니다. 따라서 명령을 실행 하기 전에 복사본을 만들어야 합니다.

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Certificate $certificate -Path "WindowsServer2019-ShieldedTemplate.vhdx" -TemplateName "Windows Server 2019" -Version 1.0.0.0
```

이제 템플릿 디스크를 사용 하 여 보호 된 Vm을 프로 비전 할 준비가 되었습니다.
System Center Virtual Machine Manager를 사용 하 여 VM을 배포 하는 경우 이제 VHDX를 VMM 라이브러리에 복사할 수 있습니다.

VHDX에서 볼륨 서명 카탈로그를 추출할 수도 있습니다.
이 파일은 템플릿을 사용 하려는 VM 소유자에 게 서명 인증서, 디스크 이름 및 버전에 대 한 정보를 제공 하는 데 사용 됩니다.
이 파일을 보호 데이터 파일 마법사에 추가 하 여 서명 인증서를 소유 하는 템플릿 작성자에 게이 및 향후의 템플릿 디스크를 만들 수 있는 권한을 부여 해야 합니다.

볼륨 서명 카탈로그를 추출 하려면 PowerShell에서 다음 명령을 실행 합니다.

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```


## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [보호 데이터 파일 만들기](guarded-fabric-tenant-creates-shielding-data.md)

## <a name="see-also"></a>참조

- [보호 된 호스트 및 보호 된 Vm에 대 한 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
