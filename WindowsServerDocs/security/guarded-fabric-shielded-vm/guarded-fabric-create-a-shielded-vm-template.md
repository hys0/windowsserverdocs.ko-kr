---
title: Windows 보호 된 VM 템플릿 디스크 만들기
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 9c8b84e8-1f5a-47a1-83ca-b1dbd801cb0b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/29/2019
ms.openlocfilehash: d9f07d2e6e93d4f8d198c2fc3b62c28c940bdefb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447513"
---
# <a name="create-a-windows-shielded-vm-template-disk"></a>Windows 보호 된 VM 템플릿 디스크 만들기

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

일반 Vm을 사용 하 여 VM 템플릿을 만들 수 (예를 들어, 한 [VM 템플릿을 Virtual Machine Manager (VMM)에서](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-library-add-vm-templates)) 쉽게 템플릿 디스크를 사용 하 여 패브릭에서 새 Vm을 배포 하는 테 넌 트 및 관리자에 대 한 합니다. 보호 된 Vm 보안이 중요 한 자산 이기 때문에 보호를 지 원하는 VM 템플릿을 만들려면 추가 단계가 있습니다. 이 항목에서는 VMM에서 보호 된 템플릿 디스크 및 VM 템플릿을 만드는 단계를 설명 합니다.

이 항목에서는 보호 된 Vm을 배포 하는 전체 과정에 얼마나 적합 한지 이해 하려면 [호스팅 서비스 공급자 구성 단계에 대 한 보호 된 호스트 및 차폐 Vm](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)합니다.

## <a name="prepare-an-operating-system-vhdx"></a>운영 체제 VHDX를 준비 합니다.

먼저 보호 된 템플릿 디스크 만들기 마법사를 통해 실행할 다음 OS 디스크를 준비 합니다. 이 디스크를 OS 디스크로 테 넌 트의 Vm에서 사용 됩니다. 이 디스크와 같은 Microsoft 데스크톱 이미지 서비스 관리자 (DISM)을 만들고 또는 수동으로 빈 VHDX 사용 하 여 VM을 설정 하 고 해당 디스크에 OS 설치에 모든 기존 도구를 사용할 수 있습니다. 디스크를 설정할 때 2 세대에 따라 다릅니다 및/또는 보호 된 Vm는 다음 요구 사항을 준수 해야 합니다. 

| VHDX에 대 한 요구 사항 | Reason |
|-----------|----|
|GUID 파티션 테이블 (GPT) 디스크 여야 합니다. | UEFI를 지 원하는 2 세대 가상 컴퓨터에 필요한|
|디스크 유형 이어야 합니다 **기본적인** 반대인 **동적**합니다. <br>참고: 이 "동적 확장" VHDX 기능이 아니라 Hyper-v에서 지 원하는 논리 디스크 형식을 가리킵니다. | BitLocker는 동적 디스크를 지원 하지 않습니다.|
|디스크에 두 개 이상의 파티션이 있습니다. 한 파티션에 Windows가 설치 된 드라이브를 포함 해야 합니다. 이 드라이브가 BitLocker 암호화 됩니다. 다른 파티션은 활성 파티션입니다, 부팅 로더를 포함 하 고 컴퓨터를 시작할 수 있도록 암호화 되지 않은 상태로 유지 됩니다.|BitLocker에 필요한|
|파일 시스템이 NTFS가 | BitLocker에 필요한|
|VHDX에 설치 된 운영 체제에는 다음 중 하나입니다.<br>Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 <br>- Windows 10, Windows 8.1, Windows 8| 2 세대 가상 컴퓨터 및 Microsoft 보안 부팅 템플릿을 지원 해야 합니다.|
|운영 체제에 일반화 된 (sysprep.exe 실행된) 해야 합니다. | 전문적으로 다루는 포함 템플릿을 프로 비전 특정 테 넌 트의 워크 로드에 대 한 Vm| 

> [!NOTE]
> VMM을 사용 하는 경우 복사 하지 마십시오 템플릿 디스크를 VMM 라이브러리로이 단계에서. 

## <a name="run-windows-update-on-the-template-operating-system"></a>템플릿 운영 체제에서 Windows Update를 실행 합니다.

템플릿 디스크에서 운영 체제에 모든 최신 Windows 업데이트가 설치 되어 있는지를 확인 합니다. 최근에 출시 된 업데이트는 종단 간 보호 프로세스의 안정성 향상-프로세스 템플릿 운영 체제가 완료가 실패할 수 있는 최신 상태가 아닙니다.

## <a name="prepare-and-protect-the-vhdx-with-the-template-disk-wizard"></a>준비 하 고 템플릿 디스크 마법사를 사용 하 여 VHDX를 보호 합니다.

보호 된 Vm에서 템플릿 디스크를 사용 하려면 디스크 준비와 보호 된 템플릿 디스크 만들기 마법사를 사용 하 여 BitLocker로 암호화 합니다. 이 마법사는 디스크에 대 한 해시를 생성 하 고 볼륨 서명 카탈로그 (VSC)에 추가 합니다. VSC는 지정 하 고 테 넌 트에 대 한 배포 되는 디스크 없습니다 변경 하거나 테 넌 트를 신뢰할 수 없는 디스크를 사용 하 여 대체 되도록 프로 비전 프로세스 중에 사용 되는 인증서를 사용 하 여 서명 됩니다. 마지막으로 BitLocker에 설치 됩니다 디스크의 운영 체제 (이 아직 없는) 하는 경우 VM 프로 비전 중에 암호화에 대 한 디스크를 준비 하기.

> [!NOTE]
> 템플릿 디스크 마법사는 현재 위치를 지정 된 템플릿 디스크를 수정 합니다. 나중에 디스크를 업데이트 하려면 마법사를 실행 하기 전에 보호 되지 않는 VHDX의 복사본을 확인 하려는 경우. 템플릿 디스크 마법사를 사용 하 여 보호 된 디스크를 수정할 수 없습니다.

(보호 된 호스트 또는 VMM 서버가 필요 하지 않습니다)는 Windows Server 2016을 실행 하는 컴퓨터에서 다음 단계를 수행 합니다.

1. 만든 일반화 된 VHDX를 복사 [운영 체제 VHDX를 준비](#prepare-an-operating-system-vhdx) 서버에 아직 없는 경우.

2. 로컬에서 서버를 관리 하려면 다음을 설치 합니다 **보호 된 VM 도구** 에서 기능 **원격 서버 관리 도구** 서버의 합니다.

        Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
        
    가 설치 되어 있는 클라이언트 컴퓨터에서 서버를 관리할 수도 있습니다는 [Windows 10 원격 서버 관리 도구](https://www.microsoft.com/en-us/download/details.aspx?id=45520)합니다.

3. 구하거 나 VSC를 새 보호 된 Vm에 대 한 템플릿 디스크에 VHDX에 대 한 서명 인증서를 만듭니다. 이 인증서에 대 한 세부 정보는 보호 데이터 파일을 만들고 디스크를 신뢰 권한을 부여 하는 경우 테 넌 트에 표시 됩니다. 따라서 것이 중요 한 테 넌 트 상호 신뢰할 수 있는 인증 기관에서이 인증서를 가져와야 합니다. 호스팅 서비스 공급자 및 테 넌 트 둘 다 있는 엔터프라이즈 시나리오에서이 인증서를 발급 하 여 PKI에서 고려할 수 있습니다.

    테스트 환경을 설정 하는 자체 서명 된 인증서를 사용 하 여 템플릿 디스크를 준비 하려는 경우 다음과 비슷한 명령을 실행 합니다.

        New-SelfSignedCertificate -DnsName publisher.fabrikam.com

4. 시작 합니다 **템플릿 디스크 마법사** 에서 합니다 **관리 도구** 폴더를 입력 하 여 또는 시작 메뉴에서 **TemplateDiskWizard.exe** 명령 프롬프트에.

5. 에 **인증서** 페이지에서 **찾아보기** 인증서의 목록을 표시 합니다. 디스크 템플릿 준비를 사용 하 여 인증서를 선택 합니다. **확인**을 클릭하고 **다음**을 클릭합니다.

6. 가상 디스크 페이지에서 클릭 **찾아보기** 준비한 VHDX를 선택 하려면 클릭 **다음**합니다.

7. 서명 카탈로그 페이지의 친숙 한 제공할 **디스크 이름** 및 **버전입니다.** 이러한 필드는 준비 된 후 디스크를 식별 하는 데 도움이 되기 위해 존재 합니다.

    예를 들어 **디스크 이름** 입력할 수 있습니다 _WS2016_ 한 **버전**, _1.0.0.0_

8. 마법사의 설정 검토 페이지에서 선택 내용을 검토 합니다. 클릭 하면 **생성**, 마법사는 템플릿 디스크에서 BitLocker를 활성화, 디스크의 해시를 계산 및 VHDX 메타 데이터에 저장 된 볼륨 서명 카탈로그를 만듭니다.

    준비 프로세스를 탑재 하거나 템플릿 디스크를 이동 하기 전에 완료 될 때까지 기다립니다. 이 프로세스는 디스크의 크기에 따라 완료 하는 데 걸릴 수 있습니다.

    > [!IMPORTANT]
    > 템플릿 디스크 프로 비전 프로세스는 보안 보호 된 VM을 사용 하 여 사용할 수 있습니다.
    > 템플릿 디스크를 사용 하 여 일반 (차폐 되지 않은) VM을 부팅 하는 동안 중지 오류 (블루 스크린) 될 가능성이 있는 및 지원 되지 않습니다.

9. 에 **요약** 페이지에서 디스크 템플릿 VSC를 로그인에 사용 된 인증서에 대 한 정보 및 인증서 발급자가 표시 됩니다. **닫기**를 클릭하여 마법사를 종료합니다.

VMM을 사용 하는 경우 템플릿 디스크를 VMM에서 보호 된 VM 템플릿에 통합 하려면이 항목의 나머지 섹션의 단계를 수행 합니다. 

## <a name="copy-the-template-disk-to-the-vmm-library"></a>VMM 라이브러리에 템플릿 디스크를 복사 합니다.

템플릿 디스크를 만든 후 VMM을 사용 하면 호스트에서 다운로드 하 고 새 Vm을 프로 비전 할 때 디스크를 사용할 수 있도록 VMM 라이브러리 공유에 복사 해야 합니다. 다음 절차를 사용 하 여 VMM 라이브러리로 템플릿 디스크를 복사 하 여 라이브러리를 새로 고칩니다.

1. VMM 라이브러리 공유 폴더에 VHDX 파일을 복사 합니다. 기본 VMM 구성에 사용한 경우 템플릿 디스크를 복사  _\\ <vmmserver>\MSSCVMMLibrary\VHDs_합니다.

2. 라이브러리 서버를 새로 고칩니다. 엽니다는 **라이브러리** 작업 영역에서 확장 **라이브러리 서버**새로 고칠 라이브러리 서버를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새로 고침**합니다.

3. 다음으로, 템플릿 디스크에 설치 된 운영 체제에 대 한 정보를 사용 하 여 VMM을 제공 합니다.

    a. 라이브러리 서버의 새로 가져온된 템플릿 디스크를 찾을 합니다 **라이브러리** 작업 영역입니다.

    b. 디스크를 마우스 오른쪽 단추로 누른 **속성**합니다.

    c. 에 대 한 **운영 체제**목록을 확장 하 고 디스크에 설치 된 운영 체제를 선택 합니다. 운영 체제를 선택 하면 나타냅니다를 VMM에 VHDX 비어 있지 않음.

    d. 속성을 업데이트한 경우 **확인**을 클릭합니다.

디스크의 이름 옆의 작은 방패 아이콘으로 준비 된 템플릿 디스크를 보호 된 Vm에 대 한 디스크를 나타냅니다. 클릭할 수도 있습니다 마우스 오른쪽 단추로 열 머리글 및 설정/해제 합니다 **차폐** 일반 또는 보호 된 VM 배포에 대 한 디스크를 할지 나타내는 텍스트 표시에 열입니다.

![보호 된 vm 템플릿 디스크](../media/Guarded-Fabric-Shielded-VM/shielded-vm-template-disk.png)

## <a name="create-the-shielded-vm-template-in-vmm-using-the-prepared-template-disk"></a>준비 된 템플릿 디스크를 사용 하 여 VMM에서 보호 된 VM 템플릿 만들기

준비 된 템플릿 디스크를 VMM 라이브러리에 보호 된 Vm에 대 한 VM 템플릿을 만들 준비가 됩니다. 보호 된 Vm에 대 한 VM 템플릿을 점이 다를 뿐 기존 VM 템플릿을 통해 특정 설정은 고정 됩니다 (2 개의 VM, UEFI 및 보안 부팅 사용, 생성 및 등) 및 다른 사용자가 사용할 수 없습니다 (테 넌 트 사용자 지정 VM의 몇 가지 선택 속성 개로 제한 됨) . VM 템플릿을 만들려면 다음 단계를 수행 합니다.

1. 에 **라이브러리** 작업 영역에서 클릭 **VM 템플릿 만들기** 맨 위에 있는 홈 탭 합니다.

2. **원본 선택** 페이지에서 **라이브러리에 보관된 기존 VM 템플릿 또는 가상 하드 디스크 사용**을 클릭한 후 **찾아보기**를 클릭합니다.

3. 표시 되는 창에서 VMM 라이브러리에서 준비 된 템플릿 디스크를 선택 합니다. 디스크 준비를 보다 쉽게 식별 하려면 열 머리글을 마우스 오른쪽 단추로 클릭 하 고 사용 하도록 설정 합니다 **차폐** 열입니다. 클릭 **확인** 한 다음 **다음**합니다.

4. VM 템플릿 이름 및 선택적 설명을 지정 하 고 클릭 **다음**합니다.

5. 에 **하드웨어 구성** 페이지에서이 템플릿에서 만든 Vm의 용량을 지정 합니다. 사용 가능 하 고 VM 템플릿에서 구성 된 하나 이상의 NIC 인지 확인 합니다. 보호 된 VM에 연결할 테 넌 트에 대 한 유일한 방법은 원격 데스크톱 연결, Windows 원격 관리 또는 네트워킹 프로토콜을 통해 작동 하는 다른 미리 구성 된 원격 관리 도구를 통해.

    테 넌 트 네트워크에서 DHCP 서버를 실행 하는 대신 VMM에서 고정 IP 풀을 활용 하려는 경우이 구성은 테 넌 트가 경고 해야 합니다. 테 넌 트를 VMM에 대 한 무인 파일을 포함 하는 보호 데이터 파일을 제공 하는 경우 고정 IP 풀 정보에 대 한 특수 한 자리 표시자 값을 제공 해야 합니다. 테 넌 트 무인 파일에서 VMM 자리 표시자에 대 한 자세한 내용은 참조 하세요. [응답 파일을 만들고](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file)합니다. 

6. 에 **운영 체제 구성** 페이지에서 VMM 제품 키, 표준 시간대 및 컴퓨터 이름을 포함 하는 보호 된 Vm에 대 한 몇 가지 옵션을 표시만 됩니다. 실딩 데이터 파일을 통해 테 넌 트에서 관리자 암호 및 도메인 이름과 같은 일부 보안 정보를 지정 (합니다. PDK 파일)입니다. 

    > [!NOTE]
    > 이 페이지에서 제품 키를 지정 하려는 경우 템플릿 디스크의 운영 체제에 유효한 것을 확인 합니다. 잘못 된 제품 키를 사용 하는 경우 VM을 만드는 실패 합니다.

템플릿이 만들어진 후 테 넌 트 새 가상 컴퓨터를 만드는 데 사용할 수 있습니다. VM 템플릿을 테 넌 트 관리자 사용자 역할에 사용할 수 있는 리소스 중 하나 인지 확인 해야 합니다 (VMM에서 사용자 역할은는 **설정을** 작업 영역).

## <a name="prepare-and-protect-the-vhdx-using-powershell"></a>준비 하 고 PowerShell을 사용 하 여 VHDX를 보호 합니다.

템플릿 디스크 마법사를 실행 하는 대신, RSAT를 실행 하는 컴퓨터에 인증서 확인 하 고 템플릿 디스크를 복사 하 고 실행할 수 [보호 TemplateDisk](https://docs.microsoft.com/powershell/module/shieldedvmtemplate/protect-templatedisk?view=win10-ps
) 서명 프로세스를 시작 합니다.
다음 예제에서는 지정 된 이름 및 버전 정보를 _TemplateName_ 하 고 _버전_ 매개 변수입니다.
VHDX에 제공 하는 `-Path` 매개 변수는 업데이트 된 템플릿 디스크를 사용 하 여 덮어쓸 수, 명령을 실행 하기 전에 복사본을 확인 해야 합니다.

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Certificate $certificate -Path "WindowsServer2019-ShieldedTemplate.vhdx" -TemplateName "Windows Server 2019" -Version 1.0.0.0
```

템플릿 디스크에 Vm을 보호 하는 프로 비전 하는 데 사용할 준비가 되었습니다.
System Center Virtual Machine Manager VM을 배포 하려면를 사용 하는 경우 VMM 라이브러리에 VHDX를 이제 복사할 수 있습니다.

VHDX에서 볼륨 서명 카탈로그를 추출할 수도 있습니다.
이 파일은 사용 하 여 사용자 템플릿을 사용 하려는 VM 소유자에 게 서명 인증서, 디스크 이름 및 버전에 대 한 정보를 제공 합니다.
실딩 데이터 파일 마법사를 만들려면이 서명 인증서의 소유에서를 템플릿 작성자에 게 권한을 부여 하려면이 파일을 가져올 필요가 및 향후 템플릿 디스크에 있습니다.

볼륨 서명 카탈로그를 추출 하려면 PowerShell에서 다음 명령을 실행 합니다.

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```


## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [실딩 데이터 파일을 만들려면](guarded-fabric-tenant-creates-shielding-data.md)

## <a name="see-also"></a>참조

- [보호 된 호스트 및 차폐 Vm 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
