---
title: 테 넌 트 용 보호 된 vm-보호 된 VM을 정의 하는 보호 데이터 만들기
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 49f4e84d-c1f7-45e5-9143-e7ebbb2ef052
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: 1ae6f881e1bd4b9b317e5622f18958f25f692eec
ms.sourcegitcommit: de71970be7d81b95610a0977c12d456c3917c331
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71940800"
---
# <a name="shielded-vms-for-tenants---creating-shielding-data-to-define-a-shielded-vm"></a>테 넌 트 용 보호 된 vm-보호 된 VM을 정의 하는 보호 데이터 만들기

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

보호 데이터 파일(구축 데이터 파일 또는 PDK 파이라고도 함)은 테넌트 또는 VM 소유자가 관리자 암호, RDP 및 기타 ID 관련 인증서, 도메인 가입 증명서 등과 같은 중요한 VM 구성 정보를 보호하기 위해 만드는 암호화된 파일입니다. 이 항목에서는 보호 데이터 파일을 만드는 방법에 대 한 정보를 제공 합니다. 파일을 만들기 전에 호스팅 서비스 공급자에서 템플릿 디스크를 구하거 나 [테 넌 트 용으로 보호 된 vm-템플릿 디스크 만들기 (선택 사항)](guarded-fabric-tenant-creates-template-disk.md)에 설명 된 대로 템플릿 디스크를 만들어야 합니다.

보호 데이터 파일의 내용에 대 한 목록 및 다이어그램은 [보호 데이터 란 무엇 이며 필요한 이유는 무엇 인가요?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)를 참조 하세요.

> [!IMPORTANT]
> 이 섹션의 단계는 보호 된 패브릭 외부의 신뢰할 수 있는 별도의 컴퓨터에서 완료 해야 합니다. 일반적으로 VM 소유자 (테 넌 트)는 패브릭 관리자가 아닌 Vm에 대 한 보호 데이터를 만듭니다.

보호 데이터 파일을 만들 준비를 하려면 다음 단계를 수행 합니다.

- [원격 데스크톱 연결에 대 한 인증서 가져오기](#optional-obtain-a-certificate-for-remote-desktop-connection)
- [응답 파일 만들기](#create-an-answer-file)
- [볼륨 서명 카탈로그 파일 가져오기](#get-the-volume-signature-catalog-file)
- [신뢰할 수 있는 패브릭 선택](#select-trusted-fabrics)

그런 다음 보호 데이터 파일을 만들 수 있습니다.

- [보호 데이터 파일을 만들고 보호자 추가](#create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard)

## <a name="optional-obtain-a-certificate-for-remote-desktop-connection"></a>필드 원격 데스크톱 연결에 대 한 인증서 가져오기

테 넌 트는 원격 데스크톱 연결 또는 다른 원격 관리 도구를 사용 하 여 보호 된 Vm에만 연결할 수 있으므로 테 넌 트가 올바른 끝점에 연결 하 고 있는지 확인할 수 있는지 확인 하는 것이 중요 합니다. 즉, "사용자의 중간에는 사람이 없습니다." 연결 가로채기).

원하는 서버에 연결 하는 것을 확인 하는 한 가지 방법은 연결을 시작할 때 제공 되는 원격 데스크톱 서비스에 대 한 인증서를 설치 하 고 구성 하는 것입니다. 서버에 연결 하는 클라이언트 컴퓨터는 인증서를 신뢰 하는지 여부를 확인 하 고 그렇지 않은 경우 경고를 표시 합니다. 일반적으로 연결 클라이언트가 인증서를 신뢰 하도록 하려면 테 넌 트의 PKI에서 RDP 인증서가 발급 됩니다. [원격 데스크톱 서비스에서 인증서를 사용 하](https://technet.microsoft.com/library/dn781533.aspx) 는 방법에 대 한 자세한 내용은 TechNet에서 찾을 수 있습니다.

 사용자 지정 RDP 인증서를 가져와야 하는지 여부를 결정 하려면 다음을 고려 하십시오.

- 랩 환경에서 보호 된 Vm만 테스트 하는 경우에는 사용자 지정 RDP 인증서가 필요 **하지 않습니다** .
- VM이 Active Directory 도메인에 가입 하도록 구성 된 경우 일반적으로 컴퓨터 인증서는 조직의 인증 기관에서 자동으로 발급 되며 RDP 연결 중에 컴퓨터를 식별 하는 데 사용 됩니다. 사용자 지정 RDP 인증서가 필요 **하지 않습니다** .
- VM이 도메인에 가입 되어 있지 않지만 원격 데스크톱을 사용 하는 경우 올바른 컴퓨터에 연결 하 고 있는지 확인 하려면 사용자 지정 RDP 인증서를 사용 하는 방법을 **고려해** 야 합니다.

> [!TIP]
> 보호 데이터 파일에 포함할 RDP 인증서를 선택할 때는 와일드 카드 인증서를 사용 해야 합니다. 하나의 보호 데이터 파일을 사용 하 여 Vm을 무제한으로 만들 수 있습니다. 각 VM은 동일한 인증서를 공유 하므로 와일드 카드 인증서는 VM의 호스트 이름에 관계 없이 인증서가 유효한 지 확인 합니다.

## <a name="create-an-answer-file"></a>응답 파일 만들기

VMM에서 서명 된 템플릿 디스크는 일반화 되므로 프로 비전 프로세스 중에 보호 된 Vm을 특수화 하려면 테 넌 트가 응답 파일을 제공 해야 합니다. 응답 파일 (무인 파일 이라고 함)은 의도 한 역할에 대 한 VM을 구성할 수 있습니다. 즉, Windows 기능을 설치 하 고, 이전 단계에서 만든 RDP 인증서를 등록 하 고, 다른 사용자 지정 작업을 수행할 수 있습니다. 또한 기본 관리자의 암호 및 제품 키를 비롯 하 여 Windows 설치 프로그램에 필요한 정보를 제공 합니다.

**ShieldingDataAnswerFile** 함수를 가져오고 사용 하 여 보호 된 vm을 만들기 위한 응답 파일 (unattend.xml 파일)을 생성 하는 방법에 대 한 자세한 내용은 [ShieldingDataAnswerFile 함수를 사용 하 여 응답 파일 생성](guarded-fabric-sample-unattend-xml-file.md)을 참조 하세요. 함수를 사용 하면 다음과 같은 선택 사항을 반영 하는 응답 파일을 보다 쉽게 생성할 수 있습니다.

- VM이 초기화 프로세스가 끝날 때 도메인에 가입 되어 있나요?
- VM 당 볼륨 라이선스 또는 특정 제품 키를 사용 하 시겠습니까?
- DHCP 또는 고정 IP를 사용 하 고 있습니까?
- VM이 조직에 속해 있음을 증명 하는 데 사용 되는 사용자 지정 원격 데스크톱 프로토콜 (RDP) 인증서를 사용 하나요?
- 초기화가 끝날 때 스크립트를 실행 하 시겠습니까?

보호 데이터 파일에 사용 되는 응답 파일은 해당 보호 데이터 파일을 사용 하 여 만든 모든 VM에서 사용 됩니다. 따라서 VM 관련 정보를 응답 파일에 하드 코딩 하지 않도록 해야 합니다. VMM은 무인 파일에서 일부 대체 문자열 (아래 표 참조)을 지원 하 여 VM에서 VM으로 변경 될 수 있는 특수화 값을 처리 합니다. 이러한 항목은 사용할 필요가 없습니다. 그러나 존재 하는 경우 VMM은이를 활용 합니다.

차폐 Vm에 대 한 unattend.xml 파일을 만드는 경우 다음 제한 사항에 유의 하세요.

- VMM을 사용 하 여 데이터 센터를 관리 하는 경우 무인 파일은 구성 된 후에 VM을 해제 해야 합니다. 이는 VMM이 VM에서 프로 비전을 완료 하 고 사용할 준비가 된 테 넌 트에 보고 해야 하는 시기를 알 수 있도록 하기 위한 것입니다. VMM은 프로 비전 중에 해제 된 것을 감지 하면 VM을 자동으로 다시 켭니다.

- 구성 된 후 VM에 액세스할 수 있도록 RDP와 해당 방화벽 규칙을 사용 하도록 설정 해야 합니다. VMM 콘솔을 사용 하 여 보호 된 Vm에 액세스할 수 없으므로 VM에 연결 하는 데 RDP가 필요 합니다. Windows PowerShell 원격을 사용 하 여 시스템을 관리 하려는 경우에는 WinRM도 사용 하도록 설정 해야 합니다.

- 보호 된 VM 무인 파일에서 지원 되는 대체 문자열은 다음과 같습니다.

    | 대체 가능 요소 | 대체 문자열 |
    |-----------|-----------|
    | ComputerName        | @ComputerName@      |
    | 표준            | @TimeZone@          |
    | ProductKey          | @ProductKey@        |
    | IPAddr4-1           | @IP4Addr-1@         |
    | IPAddr6-1           | @IP6Addr-1@         |
    | MACAddr-1           | @MACAddr-1@         |
    | 접두사-1-1          | @Prefix-1-1@        |
    | NextHop-1-1         | @NextHop-1-1@       |
    | 접두사-1-2          | @Prefix-1-2@        |
    | NextHop-1-2         | @NextHop-1-2@       |

    NIC가 둘 이상 있는 경우 첫 번째 숫자를 증가 시켜 IP 구성에 대 한 대체 문자열을 여러 개 추가할 수 있습니다. 예를 들어 2 개의 Nic에 대 한 IPv4 주소, 서브넷 및 게이트웨이를 설정 하려면 다음 대체 문자열을 사용 합니다.

    | 대체 문자열 | 예제 대체 |
    |---------------------|----------------------|
    | @IP4Addr-1@         | 192.168.1.10         |
    | @MACAddr-1@         | 이더넷             |
    | @Prefix-1-1@        | 192.168.1.0/24       |
    | @NextHop-1-1@       | 192.168.1.254        |
    | @IP4Addr-2@         | 10.0.20.30           |
    | @MACAddr-2@         | 이더넷 2           |
    | @Prefix-2-1@        | 10.0.20.0/24         |
    | @NextHop-2-1@       | 10.0.20.1            |

대체 문자열을 사용 하는 경우 VM 프로 비전 프로세스 중에 문자열이 채워지는지 확인 하는 것이 중요 합니다. @ProductKey@과 같은 문자열이 배포 시 제공 되지 않는 경우 무인 파일에 &lt;ProductKey&gt; 노드를 비워 두면 특수화 프로세스가 실패 하 고 VM에 연결할 수 없게 됩니다.

또한 테이블의 끝 부분을 향하는 네트워킹 관련 대체 문자열은 VMM 고정 IP 주소 풀을 활용 하는 경우에만 사용 됩니다. 호스팅 서비스 공급자는 이러한 대체 문자열이 필요한 지 여부를 알려줄 수 있어야 합니다. VMM 템플릿의 고정 IP 주소에 대 한 자세한 내용은 VMM 설명서에서 다음 항목을 참조 하십시오.

- [IP 주소 풀에 대 한 지침](https://technet.microsoft.com/system-center-docs/vmm/plan/plan-network#guidelines-for-ip-address-pools)
- [VMM 패브릭에서 고정 IP 주소 풀 설정](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-network-static-address-pools)

마지막으로, 보호 된 VM 배포 프로세스는 OS 드라이브만 암호화 한다는 점에 유의 해야 합니다. 하나 이상의 데이터 드라이브를 사용 하 여 보호 된 VM을 배포 하는 경우 테 넌 트 도메인의 무인 명령 또는 그룹 정책 설정을 추가 하 여 데이터 드라이브를 자동으로 암호화 하는 것이 좋습니다.

## <a name="get-the-volume-signature-catalog-file"></a>볼륨 서명 카탈로그 파일 가져오기

또한 보호 데이터 파일은 테 넌 트가 신뢰 하는 템플릿 디스크에 대 한 정보를 포함 합니다. 테 넌 트는 VSC (볼륨 서명 카탈로그) 파일 형식으로 신뢰할 수 있는 템플릿 디스크의 디스크 서명을 가져옵니다. 그러면 새 VM이 배포 될 때 이러한 서명의 유효성이 검사 됩니다. 보호 데이터 파일의 어떤 서명도 VM과 함께 배포 하려는 템플릿 디스크와 일치 하지 않는 경우 (즉, 다른 잠재적으로 악성 디스크로 수정 또는 교환 된 경우) 프로 비전 프로세스가 실패 합니다.

> [!IMPORTANT]
> VSC는 디스크가 변조 되지 않았는지 확인 하는 동안 테 넌 트가 먼저 디스크를 신뢰 하는 것이 중요 합니다. 테 넌 트이 고 템플릿 디스크가 호스터에 의해 제공 되는 경우 해당 템플릿 디스크를 사용 하 여 테스트 VM을 배포 하 고 사용자 고유의 도구 (바이러스 백신, 취약성 스캐너 등)를 실행 하 여 디스크의 유효성을 검사 하는 것이 실제로 신뢰할 수 있는 상태 인지 확인 합니다.

템플릿 디스크의 VSC를 가져오는 방법에는 두 가지가 있습니다.

1. 호스터 (또는 테 넌 트에 VMM에 대 한 액세스 권한이 있는 경우)는 VMM PowerShell cmdlet을 사용 하 여 VSC를 저장 하 고 테 넌 트에 제공 합니다. 이는 VMM 콘솔이 설치 되어 있고 호스팅 패브릭의 VMM 환경을 관리 하도록 구성 된 모든 컴퓨터에서 수행할 수 있습니다. VSC를 저장 하는 PowerShell cmdlet은 다음과 같습니다.

    ```powershell
    $disk = Get-SCVirtualHardDisk -Name "templateDisk.vhdx"

    $vsc = Get-SCVolumeSignatureCatalog -VirtualHardDisk $disk

    $vsc.WriteToFile(".\templateDisk.vsc")
    ```

2. 테 넌 트는 템플릿 디스크 파일에 액세스할 수 있습니다. 이는 테 넌 트가 호스팅 서비스 공급자에 업로드할 템플릿 디스크를 만드는 경우 또는 테 넌 트가 호스터의 템플릿 디스크를 다운로드할 수 있는 경우에 발생할 수 있습니다. 이 경우 그림에서 VMM을 사용 하지 않으면 테 넌 트는 다음 cmdlet을 실행 합니다 (차폐 VM 도구 기능과 함께 설치 됨, 원격 서버 관리 도구의 일부).

    ```powershell
    Save-VolumeSignatureCatalog -TemplateDiskPath templateDisk.vhdx -VolumeSignatureCatalogPath templateDisk.vsc
    ```

## <a name="select-trusted-fabrics"></a>신뢰할 수 있는 패브릭 선택

보호 데이터 파일의 마지막 구성 요소는 VM의 소유자 및 보호자와 관련이 있습니다. 보호자는 보호 된 VM의 소유자와이를 실행할 수 있는 보호 된 패브릭 모두를 지정 하는 데 사용 됩니다.

호스팅 패브릭에서 보호 된 VM을 실행할 수 있도록 권한을 부여 하려면 호스팅 서비스 공급자의 호스트 보호자 서비스에서 보호자 메타 데이터를 가져와야 합니다. 호스트 서비스 공급자는 관리 도구를 통해이 메타 데이터를 제공 하는 경우가 많습니다. 엔터프라이즈 시나리오에서 직접 액세스 하 여 메타 데이터를 직접 가져올 수 있습니다.

사용자 또는 호스팅 서비스 공급자는 다음 작업 중 하나를 수행 하 여 HGS에서 보호자 메타 데이터를 가져올 수 있습니다.

- 다음 Windows PowerShell 명령을 실행 하거나 웹 사이트를 검색 하 고 표시 되는 XML 파일을 저장 하 여 HGS에서 직접 보호자 메타 데이터를 가져옵니다.

    ```powershell
    Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml
    ```

- Vmm PowerShell cmdlet을 사용 하 여 VMM에서 보호자 메타 데이터를 가져옵니다.

    ```powershell
    $relecloudmetadata = Get-SCGuardianConfiguration
    $relecloudmetadata.InnerXml | Out-File .\RelecloudGuardian.xml -Encoding UTF8
    ```

계속 하기 전에 보호 된 Vm에 대 한 권한을 부여 하려는 보호 된 각 패브릭에 대해 보호자 메타 데이터 파일을 가져옵니다.

## <a name="create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard"></a>보호 데이터 파일을 만들고 보호 데이터 파일 마법사를 사용 하 여 보호자 추가

보호 데이터 파일 마법사를 실행 하 여 PDK (보호 데이터) 파일을 만듭니다. 여기서는 이전 단계에서 가져온 RDP 인증서, 무인 파일, 볼륨 서명 카탈로그, 소유자 보호자 및 다운로드 된 보호자 메타 데이터를 추가 합니다.

1. 서버 관리자 또는 다음 Windows PowerShell 명령을 사용 하 여 컴퓨터에 **보호 된 VM 도구 &gt; 원격 서버 관리 도구 &gt; 기능 관리 도구** 를 설치 합니다.

    ```powershell
    Install-WindowsFeature RSAT-Shielded-VM-Tools
    ```

2. 시작 메뉴의 관리자 도구 섹션에서 보호 데이터 파일 마법사를 열거나 다음 실행 파일을 실행 하 여 **C:\\Windows\\System32\\ShieldingDataFileWizard**를 실행 합니다.

3. 첫 번째 페이지에서 두 번째 파일 선택 상자를 사용 하 여 보호 데이터 파일의 위치 및 파일 이름을 선택 합니다. 일반적으로 보호 데이터 (예: HR, IT, 재무) 및 실행 중인 작업 역할 (예: 파일 서버, 웹 서버 또는 무인 파일에 의해 구성 된 모든 항목)을 사용 하 여 만든 Vm을 소유한 엔터티 뒤에 보호 데이터 파일의 이름을 표시 합니다. **보호 된 템플릿에 대 한 보호 데이터**로 설정 된 라디오 단추를 그대로 둡니다.

    > [!NOTE]
    > 보호 데이터 파일 마법사에서 다음과 같은 두 가지 옵션을 확인할 수 있습니다.
    >- **차폐 템플릿에 대 한 보호 데이터**
    >- **기존 Vm 및 차폐가 아닌 템플릿에 대 한 보호 데이터**<br>
    > 첫 번째 옵션은 차폐 템플릿에서 새 보호 된 Vm을 만들 때 사용 됩니다. 두 번째 옵션을 사용 하면 기존 Vm을 변환 하거나 차폐가 아닌 템플릿에서 보호 된 Vm을 만들 때만 사용할 수 있는 보호 데이터를 만들 수 있습니다.

    ![보호 데이터 파일 마법사, 파일 선택](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-01.png)

    또한이 보호 데이터 파일을 사용 하 여 만든 Vm을 "암호화 지원" 모드에서 실제로 보호 하거나 구성할 지 여부를 선택 해야 합니다. 이러한 두 옵션에 대 한 자세한 내용은 [보호 된 패브릭에서 실행할 수 있는 가상 컴퓨터의 종류는 무엇 인가요?](guarded-fabric-and-shielded-vms.md#what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run)를 참조 하세요.

    > [!IMPORTANT]
    > 보호 된 Vm의 소유자를 정의 하 고 보호 된 Vm을 실행할 수 있는 패브릭을 정의 하는 다음 단계를 주의 해 서 기울여야 합니다.<br>나중에 기존 보호 된 VM을 **차폐** 에서 **지원 되는 암호화** 로 변경 하거나 그 반대로 변경 하려면 **소유자 보호자** 의 소유가 필요 합니다.

4. 이 단계의 목표는 2 배입니다.

    - VM 소유자로 사용자를 나타내는 소유자 보호자를 만들거나 선택 합니다.

    - 이전 단계에서 호스팅 공급자의 호스트 보호자 서비스에서 다운로드 한 보호자를 가져옵니다.

    기존 소유자 보호자를 지정 하려면 드롭다운 메뉴에서 적절 한 보호자를 선택 합니다. 개인 키가 그대로 유지 되 고 로컬 컴퓨터에 설치 된 보호자만이 목록에 표시 됩니다. 오른쪽 아래 모서리에서 **로컬 보호자 관리** 를 선택 하 고 마법사 **만들기** 및 완료를 클릭 하 여 소유자 보호를 직접 만들 수도 있습니다.

    이제 **소유자 및 보호자** 페이지를 사용 하 여 이전에 다운로드 한 보호자 메타 데이터를 가져옵니다. 오른쪽 아래 모서리에서 **로컬 보호자 관리** 를 선택 합니다. **가져오기** 기능을 사용 하 여 보호자 메타 데이터 파일을 가져옵니다. 필요한 모든 보호자를 가져오거나 추가 했으면 **확인을** 클릭 합니다. 호스트 서비스 공급자 또는 엔터프라이즈 데이터 센터의 이름을 보호 하는 것이 가장 좋은 방법입니다. 마지막으로, 보호 된 VM이 실행 되도록 허가 된 데이터 센터를 나타내는 모든 보호자를 선택 합니다. 소유자 보호자를 다시 선택할 필요는 없습니다. 완료 되 면 **다음** 을 클릭 합니다.

    ![보호 데이터 파일 마법사, 소유자 및 보호자](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-02.png)

5. 볼륨 ID 한정자 페이지에서 **추가** 를 클릭 하 여 보호 데이터 파일에서 서명 된 템플릿 디스크에 권한을 부여 합니다. 대화 상자에서 VSC를 선택 하면 해당 디스크의 이름, 버전 및 해당 디스크에 서명 하는 데 사용 된 인증서에 대 한 정보가 표시 됩니다. 권한을 부여 하려는 각 템플릿 디스크에 대해이 프로세스를 반복 합니다.

6. **특수화 값** 페이지에서 **찾아보기** 를 클릭 하 여 vm을 특수화 하는 데 사용 되는 unattend.xml 파일을 선택 합니다.

    아래쪽의 **추가** 단추를 사용 하 여 특수화 프로세스 중에 필요한 PDK에 추가 파일을 추가 합니다. 예를 들어 무인 파일이 VM에 RDP 인증서를 설치 하는 경우 ( [ShieldingDataAnswerFile 함수를 사용 하 여 응답 파일 생성](guarded-fabric-sample-unattend-xml-file.md)에 설명 된 대로) RDP 인증서 PFX 파일 및 RDPCertificateConfig 스크립트를 여기에 추가 해야 합니다. 여기에서 지정 하는 모든 파일은 생성 된 VM에서 C:\\임시\\에 자동으로 복사 됩니다. 무인 파일은 경로를 기준으로 파일을 참조할 때 해당 폴더에 있을 것으로 간주 해야 합니다.

7. 다음 페이지에서 선택 항목을 검토 하 고 **생성**을 클릭 합니다.

8. 완료 되 면 마법사를 닫습니다.

## <a name="create-a-shielding-data-file-and-add-guardians-using-powershell"></a>PowerShell을 사용 하 여 보호 데이터 파일을 만들고 보호자 추가

보호 데이터 파일 마법사 대신 [ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/new-shieldingdatafile?view=win10-ps) 를 실행 하 여 보호 데이터 파일을 만들 수 있습니다.

보호 된 패브릭에서 실행 되도록 보호 된 Vm에 대 한 권한을 부여 하려면 모든 보호 데이터 파일을 올바른 소유자 및 보호자 인증서로 구성 해야 합니다.
[HgsGuardian](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsguardian?view=win10-ps)를 실행 하 여 로컬에 보호 된 보호자가 있는지 확인할 수 있습니다. 소유자 보호자는 개인 키를 보유 하 고 있으며, 데이터 센터에 대 한 보호자는 일반적으로 그렇지 않습니다.

소유자 보호자를 만들어야 하는 경우 다음 명령을 실행 합니다.

```powershell
New-HgsGuardian -Name "Owner" -GenerateCertificates
```

이 명령은 로컬 컴퓨터의 인증서 저장소에 있는 "차폐 VM Local Certificate" 폴더에 서명 및 암호화 인증서 쌍을 만듭니다.
가상 컴퓨터를 보호 하려면 소유자 인증서와 해당 개인 키가 필요 하므로 이러한 인증서가 도난 으로부터 백업 되 고 보호 되도록 해야 합니다.
소유자 인증서에 액세스할 수 있는 공격자는이 인증서를 사용 하 여 보호 된 가상 컴퓨터를 시작 하거나 보안 구성을 변경할 수 있습니다.

가상 컴퓨터 (기본 데이터 센터, 백업 데이터 센터 등)를 실행 하려는 보호 된 패브릭에서 보호자 정보를 가져와야 하는 경우 [보호 된 패브릭에서 검색 된 각 메타 데이터 파일](#select-trusted-fabrics)에 대해 다음 명령을 실행 합니다.

```powershell
Import-HgsGuardian -Name 'EAST-US Datacenter' -Path '.\EastUSGuardian.xml'
```

> [!TIP]
> 자체 서명 된 인증서를 사용 했거나 HGS에 등록 된 인증서가 만료 된 경우 HgsGuardian 명령을 사용 하 여 `-AllowUntrustedRoot` 및/또는 `-AllowExpired` 플래그를 사용 하 여 보안 검사를 무시 해야 할 수 있습니다.

또한이 보호 데이터 파일 및 [보호 데이터 응답 파일](#create-an-answer-file) 에서 사용 하려는 각 템플릿 디스크에 대 한 [볼륨 서명 카탈로그를 가져와야](#get-the-volume-signature-catalog-file) 운영 체제에서 해당 특수화 작업을 자동으로 완료할 수 있습니다.
마지막으로 VM을 완전히 차폐 또는 vTPM 사용으로 설정할지 결정 합니다.
기본 콘솔 연결과 PowerShell Direct를 허용 하는 vTPM 사용 VM에 대해 완전히 보호 된 VM 또는 `-Policy EncryptionSupported`에 대 한 `-Policy Shielded`를 사용 합니다.

모든 것이 준비 되 면 다음 명령을 실행 하 여 보호 데이터 파일을 만듭니다.

```powershell
$viq = New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\marketing-ws2016.vsc' -VersionRule Equals
New-ShieldingDataFile -ShieldingDataFilePath "C:\temp\Marketing-LBI.pdk" -Policy EncryptionSupported -Owner 'Owner' -Guardian 'EAST-US Datacenter' -VolumeIDQualifier $viq -AnswerFile 'C:\temp\marketing-ws2016-answerfile.xml'
```

> [!TIP]
> 사용자 지정 RDP 인증서, SSH 키 또는 보호 데이터 파일에 포함 되어야 하는 기타 파일을 사용 하는 경우에는 `-OtherFile` 매개 변수를 사용 하 여 포함 해야 합니다. 쉼표로 구분 된 파일 경로 목록 (예:)을 제공할 수 있습니다 `-OtherFile "C:\source\myRDPCert.pfx", "C:\source\RDPCertificateConfig.ps1"`

위의 명령에서 "Owner" (HgsGuardian에서 가져옴) 라는 보호자는 나중에 VM의 보안 구성을 변경할 수 있으며, ' 미국 동부 데이터 센터 '는 VM을 실행할 수 있지만 설정을 변경할 수는 없습니다.
둘 이상의 보호자를 사용 하는 경우 보호자의 이름을 `'EAST-US Datacenter', 'EMEA Datacenter'`와 같이 쉼표로 구분 합니다.
볼륨 ID 한정자는 템플릿 디스크 또는 이후 버전 (GreaterThanOrEquals)의 정확한 버전 (Equals)만 신뢰 하는지 여부를 지정 합니다.
배포 시 고려 되는 버전 비교의 경우 디스크 이름 및 서명 인증서가 정확 하 게 일치 해야 합니다.
`-VolumeIDQualifier` 매개 변수에 볼륨 ID 한정자의 쉼표로 구분 된 목록을 제공 하 여 둘 이상의 템플릿 디스크를 신뢰할 수 있습니다.
마지막으로, VM과 응답 파일을 함께 제공 해야 하는 다른 파일이 있는 경우 `-OtherFile` 매개 변수를 사용 하 여 쉼표로 구분 된 파일 경로 목록을 제공 합니다.

보호 데이터 파일을 구성 하는 다른 방법에 대 한 자세한 내용은 [ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-ShieldingDataFile?view=win10-ps) 및 [VolumeIDQualifier](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-VolumeIDQualifier?view=win10-ps) 에 대 한 cmdlet 설명서를 참조 하세요.

## <a name="see-also"></a>참고 항목

- [보호된 VM 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
