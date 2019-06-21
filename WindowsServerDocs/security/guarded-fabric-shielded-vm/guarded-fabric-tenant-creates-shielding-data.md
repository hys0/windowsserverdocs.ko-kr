---
title: 테 넌 트-보호 된 VM을 정의 하려면 실딩 데이터 만들기에 대 한 보호 된 Vm
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 49f4e84d-c1f7-45e5-9143-e7ebbb2ef052
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: 3c36eff8aabd1fa1c6456dce1d08ebe504102e8c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284163"
---
# <a name="shielded-vms-for-tenants---creating-shielding-data-to-define-a-shielded-vm"></a>테 넌 트-보호 된 VM을 정의 하려면 실딩 데이터 만들기에 대 한 보호 된 Vm

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

보호 데이터 파일(구축 데이터 파일 또는 PDK 파이라고도 함)은 테넌트 또는 VM 소유자가 관리자 암호, RDP 및 기타 ID 관련 인증서, 도메인 가입 증명서 등과 같은 중요한 VM 구성 정보를 보호하기 위해 만드는 암호화된 파일입니다. 이 항목에서는 보호 데이터 파일을 만드는 방법에 대 한 정보를 제공 합니다. 호스팅 서비스 공급자에 게 서 템플릿 디스크를 가져와 하거나에 설명 된 대로 템플릿 디스크 만들기 해야 파일을 만들려면 먼저 [테 넌 트-(선택 사항) 템플릿 디스크를 만들기에 대 한 보호 된 Vm](guarded-fabric-tenant-creates-template-disk.md)합니다.

목록 및 다이어그램 실딩 데이터 파일의 내용을 참조 하세요 [실딩 데이터는 무엇 이며 왜 필요?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)합니다.

> [!IMPORTANT]
> Windows Server 2016을 실행 하는 테 넌 트 컴퓨터에서이 섹션의 단계를 완료 해야 합니다. 해당 컴퓨터에는 보호 된 패브릭의 일부를 사용 해야 합니다. (즉, 해야 하지 하도록 HGS 클러스터를 사용 하 여).

실딩 데이터 파일을 작성 하기 위한 준비를 하려면 다음 단계를 수행 합니다.

- [원격 데스크톱 연결에 대 한 인증서 가져오기](#obtain-a-certificate-for-remote-desktop-connection)
- [응답 파일 만들기](#create-an-answer-file)
- [볼륨 서명 카탈로그 파일 가져오기](#get-the-volume-signature-catalog-file)
- [신뢰할 수 있는 패브릭 선택](#select-trusted-fabrics)

다음 보호 데이터 파일을 만들 수 있습니다.

- [실딩 데이터 파일을 만들고 보호자를 추가 합니다.](#create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard)


## <a name="obtain-a-certificate-for-remote-desktop-connection"></a>원격 데스크톱 연결에 대 한 인증서 가져오기

올바른 끝점으로 연결 하는 테 넌 트 확인할 수 있도록 중요 한 것 이므로 테 넌 트, 원격 데스크톱 연결 또는 기타 원격 관리 도구를 사용 하 여 보호 된 Vm에 연결할 수만 (즉, 없는 "man-in-the-middle" 연결 차단).

원하는 서버에 연결 하는 확인 하는 하나 방법은 설치 및 연결을 초기화할 때를 표시 하도록 원격 데스크톱 서비스에 대 한 인증서를 구성 하는 것입니다. 서버에 연결할 클라이언트 컴퓨터는 지 여부를 신뢰 인증서 및 경고를 표시 하지 않는 경우를 확인 합니다. 일반적으로 연결 하는 클라이언트가 인증서를 신뢰 하도록 RDP 인증서는 테 넌 트의 PKI에서 발급 됩니다. 자세한 내용은 [원격 데스크톱 서비스의 인증서를 사용 하 여](https://technet.microsoft.com/library/dn781533.aspx) TechNet에서 확인할 수 있습니다.

<!-- The previous link comes from Windows 2012 R2 content, but as of Sept 2016, there isn't a more recent link that covers the same information. -->

> [!NOTE]
> 실딩 데이터 파일에 포함을 위한 RDP 인증서를 선택 하는 경우에 와일드 카드 인증서를 사용 해야 합니다. 실딩 데이터 파일을 하나 만드는 Vm 개수에 제한 없이 사용할 수 있습니다. 각 VM은 동일한 인증서를 공유 하기 때문에 와일드 카드 인증서를 하면 인증서를 VM의 호스트 이름에 관계 없이 유효한 됩니다.

아직 기관에서 인증서를 요청 하려면 준비를 만들면 자체 서명 된 인증서를 테 넌 트 컴퓨터에서 다음 Windows PowerShell 명령을 실행 하 여 보호 된 Vm 평가 하 고 없는 경우 (여기서 *contoso.com*  테 넌 트의 도메인):

``` powershell
$rdpCertificate = New-SelfSignedCertificate -DnsName '\*.contoso.com'
$password = ConvertTo-SecureString -AsPlainText 'Password1' -Force
Export-PfxCertificate -Cert $RdpCertificate -FilePath .\rdpCert.pfx -Password $password
```

## <a name="create-an-answer-file"></a>응답 파일 만들기

VMM에서 서명 된 템플릿 디스크는 일반화 되므로 테 넌 트는 프로 비전 프로세스 중 보호 된 Vm을 특수화 하는 응답 파일을 제공 해야 합니다. 응답 파일 (무인 파일)의 의도 한 역할에 대 한 VM을 구성할 수 있습니다-즉, 해당 Windows 기능을 설치, 이전 단계에서 만든 RDP 인증서 등록 작업을 수행할 수 다른 사용자 지정 합니다. 기본 관리자 암호 및 제품 키를 포함 하 여 Windows 설치 프로그램에서 필요한 정보를 제공할 수도 됩니다.

획득 및 사용에 대 한 자세한 합니다 **-New-shieldingdataanswerfile** 보호 된 Vm을 만들기 위한 응답 파일 (Unattend.xml 파일)를 생성 하는 함수 참조 [를 사용 하 여 응답 파일을 생성 합니다 새 ShieldingDataAnswerFile 함수](guarded-fabric-sample-unattend-xml-file.md)합니다. 함수를 사용 하는 다음과 같은 옵션을 반영 하는 응답 파일을 쉽게 생성할 수 있습니다.

- VM은 초기화 프로세스의 끝에 가입 된 도메인으로 고안 되었나요?
- 사용할 예정 볼륨 라이선스 또는 VM 당 특정 제품 키를?
- DHCP 또는 고정 IP를 사용 중 입니까?
- VM이 조직에 속해 있는지를 입증 하는 데 사용할 원격 데스크톱 프로토콜 (RDP) 인증서를 사용할 것인가?
- 초기화 후에 스크립트를 실행 하 시겠습니까?
- 추가 구성을 위한 Desired State Configuration (DSC) 서버를 사용 중 입니까?

응답 파일 보호 데이터 파일에 사용 되는 실딩 데이터 파일을 사용 하 여 만든 모든 VM에 사용 됩니다. 따라서 해야 VM 관련 정보를 응답 파일에 하드 코드 하지 마십시오. VMM에서 VM에 VM에서 변경 될 수 있는 특수화 값을 처리 하는 무인 파일 (아래 표 참조) 몇 가지 대체 문자열을 지원 합니다. 이러한;를 사용할 필요는 없습니다. 그러나 존재할 경우 VMM에 활용 하 고 걸립니다.

보호 된 Vm에 대 한 unattend.xml 파일을 만들 때 염두에 다음 제한 사항:

-   무인 파일은 구성 된 후 해제 중인 VM에서 결과 여야 합니다. 이 경우 보고 해야 하는 테 넌 트 VM 프로 비전을 완료 하 고 사용할 준비가 되었는지 알아야 VMM 것입니다. VMM이 해제 되었습니다 프로 비전 하는 동안 검색 되 면 VM에서 다시 전원이 자동으로 것입니다.

-   올바른 VM 및 구성 하는 중간자 개입 공격에 대 한 또 다른 컴퓨터에 연결 하는 확인을 위한 RDP 인증서를 구성 하는 것이 좋습니다.

-   구성 된 후 VM에 액세스할 수 있도록 RDP 및 해당 방화벽 규칙을 사용 하도록 설정 해야 합니다. RDP를 VM에 연결 해야 하므로 액세스 보호 된 Vm에 VMM 콘솔을 사용할 수 없습니다. Windows PowerShell 원격을 사용 하 여 시스템을 관리 하려는 경우에 WinRM을 사용 하는 너무를 확인 합니다.

-   보호 된 VM 무인 파일에서 지원 되는 유일한 대체 문자열을 다음과 같습니다.

| 대체 가능 요소 | 대체 문자열 |
|-----------|-----------|
| ComputerName        | @ComputerName@      |
| TimeZone            | @TimeZone@          |
| ProductKey          | @ProductKey@        |
| IPAddr4-1           | @IP4Addr-1@         |
| IPAddr6-1           | @IP6Addr-1@         |
| MACAddr-1           | @MACAddr-1@         |
| 접두사-1-1          | @Prefix-1-1@        |
| NextHop-1-1         | @NextHop-1-1@       |
| 접두사-1 ~ 2          | @Prefix-1-2@        |
| NextHop-1-2         | @NextHop-1-2@       |

대체 문자열을 사용할 경우 VM 프로비저닝 프로세스 중 문자열은 채워지지 하도록 반드시 합니다. 같은 문자열인 경우 @ProductKey@ 제공 하지 않으면 배포 시 종료 합니다 &lt;ProductKey&gt; 빈 무인 파일에 노드를 특수화 프로세스가 실패 하 고 VM에 연결할 수는 있습니다.

또한 VMM 고정 IP 주소 풀을 활용 하는 경우 테이블의 끝 쪽 네트워킹 관련 대체 문자열만 사용 됩니다 note 합니다. 호스팅 서비스 공급자는 이러한 대체 문자열은 필요한 경우 알릴 수 있어야 합니다. VMM 템플릿에서 고정 IP 주소에 대 한 자세한 내용은 VMM 문서에서 다음을 참조 하세요.

- [IP 주소 풀에 대 한 지침](https://technet.microsoft.com/system-center-docs/vmm/plan/plan-network#guidelines-for-ip-address-pools) 
- [VMM 패브릭에서 고정 IP 주소 풀 설정](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-network-static-address-pools)

마지막으로,이 것에 유의 해야 보호 된 VM 배포 프로세스를 OS 드라이브 암호화만 합니다. 하나 이상의 데이터 드라이브를 사용 하 여 보호 된 VM을 배포 하는 경우 것이 좋습니다는 무인 명령 또는 그룹 정책 설정을 자동으로 데이터 드라이브를 암호화 하려면 테 넌 트 도메인에 추가 합니다.

## <a name="get-the-volume-signature-catalog-file"></a>볼륨 서명 카탈로그 파일 가져오기

실딩 데이터 파일에는 테 넌 트를 트러스트 된 템플릿 디스크에 대 한 정보 포함 되어 있습니다. 테 넌 트의 디스크 서명에서 볼륨 서명 카탈로그 (VSC) 파일의 형태로 신뢰할 수 있는 템플릿 디스크를 획득합니다. 새 VM을 배포할 때 이러한 서명 후 유효성이 검사 됩니다. 실딩 데이터 파일의 서명이 일치 템플릿 디스크 (즉, 수정 되었거나 다른, 잠재적으로 악의적인 디스크를 사용 하 여 교환)에서 VM을 배포 하는 동안 프로 비전 프로세스는 실패 합니다.

> [!IMPORTANT]
> 디스크를 사용 하 여 손상 되지 VSC를 사용 하면 하는 동안에 처음에 디스크를 신뢰 하도록 테 넌 트 여전히 중요 합니다. 테 넌 트 이며 템플릿 디스크에서 제공 하는 호스팅 서비스 공급자를 테스트 템플릿 디스크를 사용 하 여 VM을 배포 하 고 디스크의 유효성을 검사 하려면 사용자 고유의 도구 (바이러스 백신, 취약점 스캐너 및 등)를 실행 하는 경우를 실제로 신뢰할 수 있는 상태입니다.

두 가지 방법으로 템플릿 디스크의 VSC를 가져오려고 합니다.

-  호스팅 서비스 공급자 (또는 테 넌 트, 테 넌 트를 VMM에 액세스할 수 있는 경우)는 VSC를 저장 하려면 VMM PowerShell cmdlet을 사용 하 고 테 넌 트에 제공 합니다. 설치 하 고는 호스팅 패브릭 VMM 환경을 관리 하도록 VMM 콘솔을 사용 하 여 모든 컴퓨터에서 수행할 수 있습니다. VSC를 저장 하는 PowerShell cmdlet은:

        $disk = Get-SCVirtualHardDisk -Name "templateDisk.vhdx"
    
        $vsc = Get-SCVolumeSignatureCatalog -VirtualHardDisk $disk
    
        $vsc.WriteToFile(".\templateDisk.vsc")

-  테 넌 트 템플릿 디스크 파일에 액세스할 수 있습니다. 이 테 넌 트 호스팅 서비스 공급자에 업로드 된 템플릿 디스크를 만드는 경우 또는 테 넌 트 호스팅 서비스 공급자의 템플릿 디스크를 다운로드할 수 있습니다 하는 경우 대/소문자를 수 있습니다. 이 경우 그림과에서 VMM 없이 테 넌 트 (보호 된 VM 도구 기능을 원격 서버 관리 도구의 일부 설치 됨)는 다음 cmdlet을 실행할 때:

        Save-VolumeSignatureCatalog -TemplateDiskPath templateDisk.vhdx -VolumeSignatureCatalogPath templateDisk.vsc

## <a name="select-trusted-fabrics"></a>신뢰할 수 있는 패브릭 선택

실딩 데이터 파일의 마지막 구성 요소 소유자 및 VM의 보호자와 관련이 있습니다. 보호자는 보호 된 VM과 보호 된 패브릭은 권한이 부여 된 실행의 소유자를 지정 하는 데 사용 됩니다.

보호 된 VM을 실행 하는 호스팅 패브릭을 인증 하려면 호스팅 서비스 공급자의 호스트 보호 서비스에서 보호 메타 데이터를 가져와야 합니다. 종종 호스팅 서비스 공급자가 관리 도구를 통해이 메타 데이터를 사용 하 여 제공 됩니다. 엔터프라이즈 시나리오에서 메타 데이터를 직접 가져옵니다에 대 한 직접 액세스를 해야 합니다.

사용자 또는 호스팅 서비스 공급자 수를 보호 메타 데이터를 가져올 HGS에서 다음 작업 중 하나를 수행 하 여:

-  다음 Windows PowerShell 명령을 실행 하거나 웹 사이트로 이동 하 고 표시 되는 XML 파일을 저장 하 여 HGS에서 직접 보호 메타 데이터를 가져옵니다.

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

-  VMM PowerShell cmdlet을 사용 하 여 VMM에서 보호 메타 데이터를 가져옵니다.

        $relecloudmetadata = Get-SCGuardianConfiguration

        $relecloudmetadata.InnerXml | Out-File .\RelecloudGuardian.xml -Encoding UTF8

<!-- Note that the VMM PowerShell cmdlets aren't Windows PowerShell, so "VMM PowerShell" is the correct terminology for them. -->

보호 된 Vm을 계속 하기 전에 실행 권한을 부여 하려는 각 보호 된 패브릭에 대해 가디언 메타 데이터 파일을 가져옵니다.

## <a name="create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard"></a>실딩 데이터 파일을 만들고 guardians 실딩 데이터 파일 마법사를 사용 하 여 추가

실딩 데이터 (PDK) 파일을 만들려면 보호 데이터 파일 마법사를 실행 합니다. 여기에서 RDP 인증서 추가, 무인 파일을 볼륨 서명 카탈로그 소유자 보호 됩니다 및 보호자를 다운로드 한 메타 데이터를 이전 단계에서 얻은 합니다.

1.  설치할 **원격 서버 관리 도구 &gt; 기능 관리 도구 &gt; 보호 된 VM 도구** 서버 관리자 또는 Windows PowerShell 명령을 사용 하 여 컴퓨터에서:

        Install-WindowsFeature RSAT-Shielded-VM-Tools

2.  시작 메뉴 또는 실행 파일을 실행 하 여 관리 도구 섹션에서 실딩 데이터 파일 마법사를 엽니다 **c:\\Windows\\System32\\ShieldingDataFileWizard.exe**합니다.

3.  첫 번째 페이지에서 실딩 데이터 파일의 위치와 파일 이름을 선택 하 고 두 번째 파일 선택 상자를 사용 합니다. 실딩 데이터를 사용 하 여 Vm을 소유 하는 엔터티를 만든 후 보호 데이터 파일을 이름을 일반적으로 (예를 들어, HR, IT 재무) (예, 파일 서버, 웹 서버 또는 다른 무인 파일에서 구성 항목)에 실행 중인 워크 로드 역할을 합니다. 로 설정 하는 라디오 단추를 둡니다 **실딩 데이터 보호 템플릿에 대 한**합니다.

    > [!NOTE]
    > 실딩 데이터 파일 마법사에서 아래 두 옵션을 알 수 있습니다.
    >- **보호 된 템플릿에 대 한 데이터를 보호합니다.**
    >- **기존 Vm 및 보호 되지 않은 템플릿에 대 한 데이터 보호**<br>
    > 첫 번째 옵션은 보호 된 템플릿에서 보호 된 Vm 새로 만들 때 사용 됩니다. 두 번째 옵션을 사용 하면 변환 기존 Vm에 만들거나 Vm 보호 되지 않은 템플릿에서 보호 된 경우에 사용할 수 있는 실딩 데이터를 만들 수 있습니다.

    ![실딩 데이터 파일 마법사, 파일 선택](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-01.png)

       또한 만든 Vm이 보호 데이터 파일을 사용 하 여 수 진정으로 보호 된 여부 "암호화 지원" 모드로 구성 된 선택 해야 합니다. 이러한 두 옵션에 대 한 자세한 내용은 참조 하세요. [보호 된 패브릭에서 실행할 수 있는 가상 컴퓨터의 형식은 무엇 인가요?](guarded-fabric-and-shielded-vms.md#what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run)합니다.

    > [!IMPORTANT]
    > 보호 된 Vm 및의 소유자를 정의 하는 대로 다음 단계를 주의 기울여야 패브릭에 보호 된 Vm에서 실행 하도록 권한이 부여 됩니다.<br>소유 **소유자 보호자** 뒷부분에서 기존 보호 된 VM을 변경 하는 데 필요한 **차폐** 를 **암호화 지원** 또는 그 반대로 합니다.
    
4.  이 단계의 목표는 두 가지가 있습니다.

    - 만들거나 나타내는 VM 소유자는 소유자 보호자를 선택 합니다.

    - 호스팅 공급자의에서 다운로드 한 가디언 가져오기 (또는 사용자 고유의) 이전 단계에서 호스트 보호 서비스

    기존 소유자 보호자를 지정 하려면 드롭다운 메뉴에서에서 적절 한 보호를 선택 합니다. 그대로 개인 키를 사용 하 여 로컬 컴퓨터에 설치 하는 guardians만이 목록에 표시 됩니다. 선택 하 여 사용자 고유의 소유자 보호자를 만들 수도 있습니다 **로컬 Guardians 관리** 아래에서 오른쪽 클릭 하 **만들기** 마법사를 완료 합니다.

    이전에 다운로드 한 보호 메타 데이터를 가져오는 다음으로 사용 하 여 다시 합니다 **소유자 및 보호자** 페이지입니다. 선택 **로컬 Guardians 관리** 오른쪽 아래 모퉁이에서. 사용 된 **가져오기** 보호 메타 데이터 파일을 가져오는 기능입니다. 클릭 **확인** 가져온 되거나 필요한 보호자를 모두 추가 되 면 합니다. 모범 사례로, 보호자 나타내는 호스팅 서비스 공급자 또는 기업 데이터 센터 후 이름을 합니다. 마지막으로는 보호 된 VM 실행 권한이 부여 된 데이터 센터를 나타내는 모든 보호자를 선택 합니다. 소유자 보호를 다시 선택할 필요가 없습니다. 클릭 **다음** 한 번 완료 합니다.

    ![보호 데이터 파일 마법사, 소유자 및 보호자](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-02.png)

5.  볼륨 ID 한정자 페이지에서 클릭 **추가** 실딩 데이터 파일에 서명 된 템플릿 디스크에 권한을 부여 합니다. VSC를 대화 상자에서를 선택 하면 해당 디스크의 이름, 버전 및 서명 하는 데 사용 된 인증서에 대 한 정보를 표시 됩니다. 권한을 부여 하려는 각 템플릿 디스크에 대해이 프로세스를 반복 합니다.

6.  에 **특수화 값** 페이지에서 **찾아보기** Vm을 특수화 하는 데 사용할 unattend.xml 파일을 선택 합니다.

    사용 된 **추가** 특수화 프로세스 중 필요한 PDK를 모든 파일을 추가 하려면 아래쪽 단추입니다. 예를 들어를 VM에 RDP 인증서를 설치 하는 무인 파일 (에 설명 된 대로 [-New-shieldingdataanswerfile 함수를 사용 하 여 응답 파일을 생성할](guarded-fabric-sample-unattend-xml-file.md)), RDPCert.pfx 파일에서 참조를 추가 해야 합니다 무인 파일. 여기에서 지정한 파일에서 자동으로 c: 복사할\\temp\\ 만들어지는 VM에 있습니다. 무인 파일에는 파일 경로에서 참조 하는 경우 해당 폴더의 수를 예상 해야 합니다.

7.  다음 페이지에서 선택 내용을 검토 한 다음 클릭 **생성**합니다.

8.  완료 된 후 마법사를 닫습니다.

## <a name="create-a-shielding-data-file-and-add-guardians-using-powershell"></a>실딩 데이터 파일을 만들고 PowerShell을 사용 하 여 보호자를 추가

실딩 데이터 파일 마법사 대신 실행할 수 있습니다 [새로 만들기-ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/new-shieldingdatafile?view=win10-ps) 실딩 데이터 파일을 만들려면.

모든 보호 데이터 파일에서 보호 된 패브릭에서 실행 되도록 보호 된 Vm에 권한을 부여 하는 올바른 소유자 및 보호 인증서를 사용 하 여 구성 해야 합니다.
모든 보호자를 실행 하 여 로컬로 설치 되어 있는지 확인할 수 있습니다 [Get HgsGuardian](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsguardian?view=win10-ps)합니다. 소유자의 보호자에 개인 키가 포함 하지만 데이터 센터에 대 한 보호자는 일반적으로 그렇지 않습니다.

소유자 보호자를 만들려는 경우 다음 명령을 실행 합니다.

```powershell
New-HgsGuardian -Name "Owner" -GenerateCertificates
```

이 명령은 "보호 된 VM의 로컬 인증서" 폴더 아래에 있는 로컬 컴퓨터의 인증서 저장소에 서명 및 암호화 인증서의 쌍을 만듭니다.
소유자 인증서 및 가상 컴퓨터를 unshield 이러한 있도록를 해당 개인 키를 사용 하도록 해야 인증서를 백업 및 도용 되지 않도록에서 보호 합니다.
소유자 인증서에 대 한 액세스를 사용 하 여 공격자 보호 된 가상 컴퓨터를 시작 하거나 보안 구성을 변경 하려면 사용할 수 있습니다.

다음 명령을 실행 하는 각 가상 컴퓨터 (에 기본 데이터 센터, 백업 데이터 센터, 등)를 실행 하려는 보호 된 패브릭에서 보호 정보를 가져오는 경우 [메타 데이터 파일에 보호 된 패브릭에서 검색 ](#select-trusted-fabrics).

```powershell
Import-HgsGuardian -Name 'EAST-US Datacenter' -Path '.\EastUSGuardian.xml'
```

> [!TIP]
> 자체 서명 된 인증서 또는 등록 된 인증서를 사용 하 여 HGS 만료 된 경우 사용 해야 합니다 `-AllowUntrustedRoot` 및/또는 `-AllowExpired` 보안 검사를 건너뛸 가져오기 HgsGuardian 명령으로 플래그 합니다.

또한 해야 [볼륨 서명 카탈로그를 가져올](#get-the-volume-signature-catalog-file) 이 보호 데이터 파일을 사용 하 여 사용 하려는 각 템플릿 디스크에 대 한와 [실딩 데이터 응답 파일](#create-an-answer-file) 운영 체제를 완료할 수 있도록 해당 특수화는 자동으로 작업 합니다.
마지막으로, VM 완벽 하 게 보호 하거나 vTPM-을 사용 하도록 설정 하려는 경우를 결정 합니다.
사용 하 여 `-Policy Shielded` 완벽 하 게 보호 된 VM에 대 한 또는 `-Policy EncryptionSupported` vTPM는 기본적인 콘솔 연결을 허용 하는 VM 및 PowerShell Direct를 사용 합니다.

모든 준비 되 면 보호 데이터 파일을 만들려면 다음 명령을 실행 합니다.

```powershell
$viq = New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\marketing-ws2016.vsc' -VersionRule Equals
New-ShieldingDataFile -ShieldingDataFilePath "C:\temp\Marketing-LBI.pdk" -Policy EncryptionSupported -Owner 'Owner' -Guardian 'EAST-US Datacenter' -VolumeIDQualifier $viq -AnswerFile 'C:\temp\marketing-ws2016-answerfile.xml'
```

위의 명령에 "Owner" (Get HgsGuardian에서 가져옴) 라는 보호 ' 미국 동부 데이터 센터 ' VM을 실행할 수 있지만 해당 설정을 변경 하지 하는 동안 나중에 VM의 보안 구성을 변경할 수 없게 됩니다.
둘 이상의 보호를 사용 하는 경우 별도 쉼표를 사용 하 여 보호자의 이름이 같은 `'EAST-US Datacenter', 'EMEA Datacenter'`합니다.
볼륨 ID 한정자의 정확한 버전의 템플릿 디스크 (같음) 또는 이후 버전 (GreaterThanOrEquals)도 신뢰할 수 있는지 여부를 지정 합니다.
디스크 이름 및 서명 인증서는 배포 시 고려해 버전 비교에 대 한 정확 하 게 일치 해야 합니다.
볼륨의 쉼표로 구분 된 목록 ID 한정자를 제공 하 여 둘 이상의 템플릿 디스크를 신뢰할 수 있는 여 `-VolumeIDQualifier` 매개 변수입니다.
마지막으로, 다른 경우 사용 하 여 VM 사용 하 여 응답 파일을와 함께 제공 해야 하는 파일의 `-OtherFile` 매개 변수 파일 경로 쉼표로 구분 된 목록에 제공 합니다.

Cmdlet 설명서를 참조 하십시오 [새로 만들기-ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-ShieldingDataFile?view=win10-ps) 및 [새로 만들기-VolumeIDQualifier](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-VolumeIDQualifier?view=win10-ps) 실딩 데이터 파일을 구성 하는 다른 방법에 대해 자세히 알아보려면 합니다.

## <a name="see-also"></a>참조

- [보호된 VM 배포](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
