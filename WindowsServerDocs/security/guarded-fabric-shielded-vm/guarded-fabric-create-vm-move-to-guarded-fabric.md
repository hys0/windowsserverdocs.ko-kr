---
redirect_url: guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md
title: 온-프레미스 VM 및 보호 된 패브릭 이동 테 넌 트-새 보호 된 Vm 보호
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 0ca1efa0-01f9-4b6f-87d4-c66db00d7d70
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: dd9b89f34a3b4af8bb98d2399a524790aa65de0e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447479"
---
# <a name="shielded-vms-for-tenants---creating-a-new-shielded-vm-on-premises-and-moving-it-to-a-guarded-fabric"></a>온-프레미스 VM 및 보호 된 패브릭 이동 테 넌 트-새 보호 된 Vm 보호

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019


<!-- NOTE THAT THIS FILE HAS A "redirect_url" LINE IN THE METADATA. EVENTUALLY WE WILL PROBABLY STRIP OUT THE DETAILED METADATA AND THE CONTENT BELOW, SO IT'S PURELY A REDIRECTED TOPIC. However, as of mid-November 2016, we're still deciding. -->



이 항목에서는 Hyper-v만;를 사용 하 여 보호 된 VM을 만드는 단계를 설명 합니다. 즉, Virtual Machine Manager, 템플릿 디스크 또는 보호 데이터 파일 없이 합니다. 대부분의 공용 클라우드 호스팅 환경에 대 한 일반적인 시나리오는 이지만 보호 된 패브릭을 테스트할 때 유용할 수 있습니다 또는 엔터프라이즈의 시나리오는 부서별 패브릭에서 VM을 이동 하는 위치 IT 인프라를 공유 하 고 마이그레이션 전에 암호화 해야 합니다.

이 항목에서는 보호 된 Vm을 배포 하는 전체 과정에 얼마나 적합 한지 이해 하려면 [호스팅 서비스 공급자 구성 단계에 대 한 보호 된 호스트 및 차폐 Vm](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)합니다.

## <a name="import-the-guardian-configuration-on-the-tenant-hyper-v-server"></a>테 넌 트 Hyper-v 서버에서 보호 구성을 가져옵니다.

1.  절차를 시작 하기 전에 다음 역할 및 기능 설치를 사용 하 여 Windows Server 2016을 실행 하는 Hyper-v 호스트에 있는지 확인 합니다.

    - 역할

        - Hyper-V

    - 기능

        - 원격 서버 관리 도구\\관리 도구 기능\\차폐 VM 도구

    > [!NOTE]
    > 여기에 호스트 해야 *되지* 보호 된 패브릭에서 호스트 되어야 합니다. 이것이 Vm 보호 된 패브릭을 이동 하기 전의 준비 되어 있는 별도 호스트입니다.

2.  이 컴퓨터에 보호 된 VM을 실행 하려면, 먼저 가상화 기반 보안이 활성화 되어 실행 되도록 해야 합니다. 호스트 보호 Hyper-v 지원 기능을 설치 하려면 관리자 권한 Windows PowerShell 창에서 다음 명령을 실행 합니다. 이렇게 보호 된 Vm을 실행 하려면 컴퓨터에 모든 필요한 설정이 구성 됩니다.

        Install-WindowsFeature HostGuardian

3.  VM이 실행 되는 보호 된 패브릭에 대 한 보호 메타 데이터를 획득 해야 합니다. 이 메타 데이터는 패브릭에서 보호 된 VM 실행 권한을 부여 하는 데 사용 됩니다. 이 정보를 가져오는 방법을 각 호스팅 서비스 공급자 또는 기업에 대 한 다른 됩니다. 다음 Windows PowerShell 명령을 실행 하 여 호스팅 서비스 공급자 (또는 보호 된 패브릭 네트워크에 액세스할 수 있으면 사용자)에이 정보를 얻을 수 있습니다.

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

    위의 예에서 "hgs" HGS 클러스터의 분산된 된 네트워크 이름이 며 "bastion.local" HGS 도메인의 이름입니다.

4.  이후 절차에서 해야 하는 보호 키를 가져오는 다음 명령을 실행 합니다.

    에 대 한 &lt;경로&gt;&lt;Filename&gt;경로 대체 하 고 xml 파일 이름 파일, 예를 들어 이전 단계에서 저장 합니다. **C:\\temp\\GuardianKey.xml**

    에 대 한 &lt;GuardianName&gt;, 예를 들어, 호스팅 공급자 또는 엔터프라이즈 데이터 센터에 이름을 지정할 **HostingProvider1**합니다. 다음 절차에 대 한 이름을 기록 합니다.

    포함 **-AllowUntrustedRoot** HGS 서버에 자체 서명 된 인증서를 사용 하 여 설정 된 경우에 합니다. (이러한 인증서는 부분에서 HGS 키 보호 서비스입니다.)

        Import-HgsGuardian -Path '<Path><Filename>' -Name '<GuardianName>' -AllowUntrustedRoot

## <a name="create-a-new-shielded-virtual-machine-on-the-host"></a>호스트에서 새 보호 된 가상 머신 만들기

이 절차에서는 가상 컴퓨터를 Hyper-v 호스트에서 만들고 호스팅 공급자 또는 보호 된 호스트에서 실행할 수 있는 데이터 센터 관리자는 내보내기에 대 한 준비 합니다.

절차의 일부로, 두 가지 중요 한 요소를 포함 하는 키 보호기를 만듭니다.

-   **소유자**: 키 보호기를 있습니다 또는 가능성이, 인증서와 같은 보안 요소를 공유 하는 그룹에서 작업 하는 VM의 "소유자"로 식별 됩니다. 소유자 id 표시 된 대로 명령을 실행 하는 경우 자체 서명 된 인증서로 생성 된 인증서로 표시 됩니다. 필요에 따라 대신 PKI 인프라에서 지 원하는 인증서를 사용 하 여를 생략 합니다 **-AllowUntrustedRoot** 명령에 매개 변수입니다.

-   **보호자**: 또한 키 보호기를에 호스팅 공급자 또는 기업 데이터 센터 (HGS 및 보호 된 호스트를 실행)으로 식별 됩니다 "보호 합니다." 가디언 이전 절차에서 가져온 보호자 키가 나타내는 [테 넌 트 Hyper-v 서버에서 보호 구성을 가져오려면](#import-the-guardian-configuration-on-the-tenant-hyper-v-server)합니다.

실딩 데이터 파일의 요소는 키 보호기를 보여 주는 예시를 참조 하세요. [실딩 데이터는 무엇 이며 왜 필요?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)합니다.

1. 테 넌 트 Hyper-v 호스트에 새로운 2 세대 가상 컴퓨터를 만들려면 다음 명령을 실행 합니다.

   에 대 한 &lt;ShieldedVMname&gt;, 예를 들어 VM의 이름을 지정 합니다. **ShieldVM1**
    
   에 대 한 &lt;VHDPath&gt;, 예를 들어 VM의 VHDX를 저장할 위치를 지정 합니다. **C:\\VMs\\ShieldVM1\\ShieldVM1.vhdx**
    
   에 대 한 &lt;nnGB&gt;, 예를 들어, VHDX의 크기를 지정 합니다. **60GB**

       New-VM -Generation 2 -Name "<ShieldedVMname>" -NewVHDPath <VHDPath>.vhdx -NewVHDSizeBytes <nnGB>

2. 지원 되는 운영 체제를 설치 (Windows Server 2012 이상, Windows 8 클라이언트 이상) VM에 원격 데스크톱 연결 및 해당 방화벽 규칙을 사용 하도록 설정 합니다. VM의 IP 주소 및/또는 DNS 이름을; 기록 원격으로 연결 하도록 해야 합니다.

3. RDP를 사용 하 여 원격으로 VM에 연결 하 고 RDP 및 방화벽을 올바르게 구성 되어 있는지 확인 하십시오. 보호 프로세스의 일부로, Hyper-v를 통해 가상 컴퓨터에 대 한 콘솔 액세스를 사용할 수 있으므로 네트워크를 통해 시스템을 원격으로 관리할 수 있도록 합니다.

4. (이 섹션의 시작 부분에서 설명) 새 키 보호기를 만들려면 다음 명령을 실행 합니다.

   에 대 한 &lt;GuardianName&gt;, 예를 들어, 이전 절차에서 지정한 이름을 사용 합니다. **HostingProvider1**

   포함 **-AllowUntrustedRoot** 자체 서명 된 인증서에 대 한 허용 하도록 합니다.

       $Guardian = Get-HgsGuardian -Name '<GuardianName>'

       $Owner = New-HgsGuardian -Name 'Owner' -GenerateCertificates

       $KP = New-HgsKeyProtector -Owner $Owner -Guardian $Guardian -AllowUntrustedRoot

   하려는 경우 둘 이상의 데이터 센터에 대 한 보호 된 VM (예: 재해 복구 사이트 및 공용 클라우드 공급자)를 실행할 수 있도록에 대 한 보호자의 목록을 제공할 수 있습니다 합니다 **-보호** 매개 변수입니다. 자세한 내용은 [새로 만들기-HgsKeyProtector]을 참조 하세요. (https://docs.microsoft.com/powershell/module/hgsclient/new-hgskeyprotector?view=win10-ps합니다.

5. 키 보호기를 사용 하 여 vTPM을 사용 하도록 설정 하려면 다음 명령을 실행 합니다. 에 대 한 &lt;ShieldedVMname&gt;, 이전 단계에서 사용한 동일한 VM 이름을 사용 합니다.

       $VMName="<ShieldedVMname>"

       Stop-VM -Name $VMName -Force

       Set-VMKeyProtector -VMName $VMName -KeyProtector $KP.RawData

       Set-VMSecurityPolicy -VMName $VMName -Shielded $true

       Enable-VMTPM -VMName $VMName

6. 키 보호기 소유자 로컬 인증서를 사용 하 여 작동 하는지 확인 하려면 VM을 시작 하려면 다음 명령을 실행 합니다.

       Start-VM -Name $VMName

7. VM에서 Hyper-v 콘솔에서 시작 되었는지 확인 합니다.

8. RDP를 사용 하 여 원격으로 VM에 연결 하 고 보호 된 VM에 연결 된 모든 Vhdx에서 모든 파티션에 대해 BitLocker를 사용 하도록 설정 합니다.

   > [!IMPORTANT]
   > 다음 단계를 계속 하기 전에 BitLocker 암호화를 사용할 수 있는 모든 파티션에 대해 완료 될 때까지 기다립니다.

9. 보호 된 패브릭 이동할 준비가 되 면 VM을 종료 합니다.

10. 테 넌 트 Hyper-v 서버에서 VM (Windows PowerShell 또는 Hyper-v 관리자) 사용자가 선택한 도구를 사용 하 여 내보냅니다. 그런 다음 호스팅 공급자 또는 엔터프라이즈 데이터 센터에서 유지 관리 하는 보호 된 호스트에 복사할 파일에 대 한 정렬 합니다.

11. **호스팅 공급자 또는 기업 데이터 센터를 위한**:

    Hyper-v 관리자 또는 Windows PowerShell을 사용 하 여 보호 된 VM을 가져옵니다. VM을 시작 하기 위해 VM 소유자 로부터 VM 구성 파일을 가져와야 합니다. 즉, 키 보호기와 VM의 가상 TPM 구성 파일에 저장 됩니다. VM를 보호 된 패브릭에서 실행 되도록 구성 된 경우이 성공적으로 시작할 수 있어야 합니다.

## <a name="see-also"></a>참조

- [보호 된 호스트 및 차폐 Vm 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
