---
redirect_url: guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md
title: 테 넌 트 용 보호 된 VM-온-프레미스에서 새 차폐 VM 만들기 및 보호 된 패브릭으로 이동
ms.prod: windows-server
ms.topic: article
ms.assetid: 0ca1efa0-01f9-4b6f-87d4-c66db00d7d70
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c6753ae5d767f0c71b86fc47c1d8bf9971a2a5cc
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475530"
---
# <a name="shielded-vms-for-tenants---creating-a-new-shielded-vm-on-premises-and-moving-it-to-a-guarded-fabric"></a>테 넌 트 용 보호 된 VM-온-프레미스에서 새 차폐 VM 만들기 및 보호 된 패브릭으로 이동

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Hyper-v만 사용 하 여 보호 된 VM을 만드는 단계에 대해 설명 합니다. 즉, Virtual Machine Manager, 템플릿 디스크 또는 보호 데이터 파일을 사용 하지 않습니다. 이는 대부분의 공용 클라우드 호스팅 환경에서 일반적이 지 않은 시나리오 이지만, 보호 된 패브릭 또는 VM이 부서별 패브릭에서 공유 된 IT 인프라로 이동 되 고 마이그레이션 전에 암호화 되어야 하는 엔터프라이즈 시나리오에서 테스트 하는 경우에 유용할 수 있습니다.

이 항목이 보호 된 Vm을 배포 하는 전체 프로세스에 어떻게 부합 하는지 이해 하려면 [보호 된 호스트 및 보호 된 vm에 대 한 서비스 공급자 구성 단계 호스팅](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)을 참조 하세요.

## <a name="import-the-guardian-configuration-on-the-tenant-hyper-v-server"></a>테 넌 트 Hyper-v 서버에서 보호자 구성을 가져옵니다.

1.  절차를 시작 하기 전에 다음 역할 및 기능이 설치 된 Windows Server 2016를 실행 하는 Hyper-v 호스트에 있는지 확인 합니다.

    - 역할

        - Hyper-V

    - 기능

        - 원격 서버 관리 도구 \\ 기능 관리 도구 \\ 차폐 VM 도구

    > [!NOTE]
    > 여기에서 사용 된 호스트는 보호 된 패브릭의 *호스트가 아니어야 합니다* . 이는 보호 된 패브릭에 이동 하기 전에 Vm이 준비 되는 별도의 호스트입니다.

2.  이 컴퓨터에서 보호 된 VM을 실행 하려면 먼저 가상화 기반 보안이 사용 되 고 실행 중인지 확인 해야 합니다. 관리자 권한 Windows PowerShell 창에서 다음 명령을 실행 하 여 호스트 보호자 Hyper-v 지원 기능을 설치 합니다. 이렇게 하면 컴퓨터에서 보호 된 Vm을 실행할 수 있도록 필요한 모든 설정이 구성 됩니다.

        Install-WindowsFeature HostGuardian

3.  VM이 실행 되는 보호 된 패브릭에 대 한 보호자 메타 데이터를 획득 해야 합니다. 이 메타 데이터는 해당 패브릭에 보호 된 VM을 실행 하는 권한을 부여 하는 데 사용 됩니다. 이러한 정보를 얻는 방법은 호스팅 서비스 공급자나 엔터프라이즈 마다 다릅니다. 호스터 (또는 보호 된 패브릭 네트워크에 대 한 액세스 권한이 있는 경우)는 다음 Windows PowerShell 명령을 실행 하 여이 정보를 얻을 수 있습니다.

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

    위의 예에서 "hgs"는 HGS 클러스터의 분산 네트워크 이름이 고 "요새. local"은 HGS 도메인의 이름입니다.

4.  이후 절차에서 필요한 보호자 키를 가져오려면 다음 명령을 실행 합니다.

    &lt;경로 &gt; &lt; 파일 이름에 대해 &gt; 이전 단계에서 저장 한 XML 파일의 경로와 파일 이름을 바꿉니다 (예: **C: \\ temp \\GuardianKey.xml**

    GuardianName에 대해 &lt; &gt; 호스팅 공급자 또는 엔터프라이즈 데이터 센터의 이름을 지정 합니다 (예: **HostingProvider1**). 다음 절차의 이름을 기록 합니다.

    HGS 서버가 자체 서명 된 인증서로 설정 된 경우 **에만-allowunroot root** 를 포함 합니다. (이러한 인증서는 HGS의 키 보호 서비스의 일부입니다.)

        Import-HgsGuardian -Path '<Path><Filename>' -Name '<GuardianName>' -AllowUntrustedRoot

## <a name="create-a-new-shielded-virtual-machine-on-the-host"></a>호스트에서 새 차폐 가상 컴퓨터 만들기

이 절차에서는 Hyper-v 호스트에서 가상 컴퓨터를 만들고, 보호 된 호스트에서 실행할 수 있는 호스팅 공급자 또는 데이터 센터 관리자에 게 내보낼 수 있도록 준비 합니다.

절차의 일부로 다음과 같은 두 가지 중요 한 요소를 포함 하는 키 보호기를 만듭니다.

-   **소유자**: 키 보호기에서 사용 하는 그룹은 인증서와 같은 보안 요소를 공유 하는 VM의 "소유자"로 식별 됩니다. 소유자로 서의 id는 인증서로 표시 되며, 표시 된 대로 명령을 실행 하는 경우 자체 서명 된 인증서로 생성 됩니다. 필요에 따라 PKI 인프라에서 지원 되는 인증서를 대신 사용 하 고 명령에서 **-allowunroot** 매개 변수를 생략할 수 있습니다.

-   **보호자**: 키 보호기 에서도, 호스팅 공급자 또는 엔터프라이즈 데이터 센터 (HGS 및 보호 된 호스트를 실행 하는)는 "보호자"로 식별 됩니다. 보호자는 이전 절차에서 가져온 보호자 키로 표시 되며,이는 [테 넌 트 hyper-v 서버에서 보호자 구성을 가져옵니다](#import-the-guardian-configuration-on-the-tenant-hyper-v-server).

보호 데이터 파일의 요소인 키 보호기를 보여 주는 예시의 경우 [보호 데이터는 무엇 이며 필요한 이유는 무엇 인가요?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)를 참조 하세요.

1. 테 넌 트 Hyper-v 호스트에서 새 2 세대 가상 머신을 만들려면 다음 명령을 실행 합니다.

   ShieldedVMname의 경우 &lt; &gt; VM의 이름을 지정 합니다 (예: **ShieldVM1** ).

   VHDPath의 경우 &lt; &gt; VM의 VHDX를 저장할 위치를 지정 합니다 (예: **C: \\ vm \\ ShieldVM1 \\ ShieldVM1** ).

   NnGB의 경우 &lt; &gt; VHDX의 크기 (예: **60gb** )를 지정 합니다.

       New-VM -Generation 2 -Name "<ShieldedVMname>" -NewVHDPath <VHDPath>.vhdx -NewVHDSizeBytes <nnGB>

2. VM에 지원 되는 운영 체제 (Windows Server 2012 이상, Windows 8 클라이언트 이상)를 설치 하 고 원격 데스크톱 연결 및 해당 방화벽 규칙을 사용 하도록 설정 합니다. VM의 IP 주소 및/또는 DNS 이름을 기록 합니다. 원격으로 연결 하는 데 필요 합니다.

3. RDP를 사용 하 여 VM에 원격으로 연결 하 고 RDP 및 방화벽이 올바르게 구성 되어 있는지 확인 합니다. 보호 프로세스의 일부로 Hyper-v를 통해 가상 컴퓨터에 대 한 콘솔 액세스를 사용할 수 없게 되므로 네트워크를 통해 시스템을 원격으로 관리할 수 있는지 확인 하는 것이 중요 합니다.

4. 새 키 보호기를 만들려면 (이 섹션의 앞부분에서 설명) 다음 명령을 실행 합니다.

   GuardianName의 경우 &lt; &gt; 이전 절차에서 지정한 이름 (예: **HostingProvider1** )을 사용 합니다.

   자체 서명 된 인증서를 허용 하는 **-allowunroot** 를 포함 합니다.

       $Guardian = Get-HgsGuardian -Name '<GuardianName>'

       $Owner = New-HgsGuardian -Name 'Owner' -GenerateCertificates

       $KP = New-HgsKeyProtector -Owner $Owner -Guardian $Guardian -AllowUntrustedRoot

   보호 된 VM을 실행할 수 있는 두 개 이상의 데이터 센터 (예: 재해 복구 사이트 및 공용 클라우드 공급자)에 대 한 보호자의 목록을 원하는 경우 **보호자 매개 변수에** 보호자 목록을 제공할 수 있습니다. 자세한 내용은 [HgsKeyProtector] (을 참조 하세요 https://docs.microsoft.com/powershell/module/hgsclient/new-hgskeyprotector?view=win10-ps .

5. 키 보호기를 사용 하 여 vTPM을 사용 하도록 설정 하려면 다음 명령을 실행 합니다. ShieldedVMname의 경우 &lt; &gt; 이전 단계에서 사용 된 것과 동일한 VM 이름을 사용 합니다.

       $VMName="<ShieldedVMname>"

       Stop-VM -Name $VMName -Force

       Set-VMKeyProtector -VMName $VMName -KeyProtector $KP.RawData

       Set-VMSecurityPolicy -VMName $VMName -Shielded $true

       Enable-VMTPM -VMName $VMName

6. VM을 시작 하 여 키 보호기가 로컬 소유자 인증서로 작동 하는지 확인 하려면 다음 명령을 실행 합니다.

       Start-VM -Name $VMName

7. Hyper-v 콘솔에서 VM이 시작 되었는지 확인 합니다.

8. RDP를 사용 하 여 VM에 원격으로 연결 하 고 보호 된 VM에 연결 된 모든 Vhdx의 모든 파티션에서 BitLocker를 사용 하도록 설정 합니다.

   > [!IMPORTANT]
   > 다음 단계로 진행 하기 전에 BitLocker 암호화를 사용 하도록 설정한 모든 파티션에서 BitLocker 암호화가 완료 될 때까지 기다립니다.

9. 보호 된 패브릭에 이동할 준비가 되 면 VM을 종료 합니다.

10. 테 넌 트 Hyper-v 서버에서 원하는 도구 (Windows PowerShell 또는 Hyper-v 관리자)를 사용 하 여 VM을 내보냅니다. 그런 다음 호스팅 공급자 또는 기업 데이터 센터에 의해 유지 관리 되는 보호 된 호스트로 복사할 파일을 정렬 합니다.

11. **호스팅 공급자 또는 기업 데이터 센터의 경우**:

    Hyper-v 관리자 또는 Windows PowerShell을 사용 하 여 보호 된 VM을 가져옵니다. Vm을 시작 하려면 vm 소유자에서 vm 구성 파일을 가져와야 합니다. 이는 키 보호기와 VM의 가상 TPM이 구성 파일에 저장 되기 때문입니다. VM이 보호 된 패브릭에서 실행 되도록 구성 된 경우 성공적으로 시작할 수 있어야 합니다.

## <a name="additional-references"></a>추가 참조

- [보호 된 호스트 및 보호 된 Vm에 대 한 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
