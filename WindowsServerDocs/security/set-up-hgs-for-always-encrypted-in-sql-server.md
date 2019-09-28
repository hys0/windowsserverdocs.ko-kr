---
title: SQL Server에서 Always Encrypted에 대 한 호스트 보호자 서비스 설정
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/03/2018
ms.openlocfilehash: 5d1396f609a425adcd87a41d3469f3aa55774851
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402277"
---
# <a name="setting-up-the-host-guardian-service-for-always-encrypted-with-secure-enclaves-in-sql-server"></a>SQL Server에서 secure enclaves를 사용 하 여 Always Encrypted에 대 한 호스트 보호자 서비스 설정 

>적용 대상: Windows Server (반기 채널), Windows Server 2019 SQL Server 2019 preview
 
SQL Server 2019 preview의 [secure enclaves Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves) 는 데이터베이스에 저장 된 중요 한 데이터에 대해 기밀 계산을 수행할 수 있도록 설계 된 기능입니다. HGS (호스트 보호 서비스)는 Always Encrypted에 대해 구성 된 보안 enclave VBS (가상화 기반 보안) 메모리 enclave 경우 데이터를 안전 하 게 유지 하는 데 중요 한 역할을 합니다. VBS 메모리 enclave의 보안은 Windows 하이퍼바이저의 보안에 따라 다르며, SQL Server 호스트 하는 컴퓨터의 보안을 더욱 광범위 하 게 합니다. 

따라서 데이터베이스 클라이언트 응용 프로그램에서 Always Encrypted에 사용 되는 VBS memory enclave를 사용 하 여 중요 한 데이터에 대해 계산을 수행 하기 전에 응용 프로그램에서 신뢰할 수 있는 HGS를 사용 하 여 증명 해야 합니다. 증명은 enclave를 포함 하는 SQL Server를 호스트 하는 컴퓨터가 올바른 상태 이며 신뢰할 수 있는지를 증명 합니다. 이 항목의 나머지 부분에서는 단순히 호스트 컴퓨터로 SQL Server를 호스트 하는 컴퓨터를 참조 합니다.

응용 프로그램에서 다음과 같은 두 가지 방식으로 증명할 수 있습니다. 

- 호스트 키 증명은 알려진 신뢰할 수 있는 개인 키를 소유 하 고 있음을 증명 하 여 호스트에 권한을 부여 합니다. 사전 프로덕션 환경에는 호스트 키 증명 및 물리적 호스트 컴퓨터 또는 SQL Server를 실행 하는 2 세대 가상 머신이 권장 됩니다.
- TPM 증명은 하드웨어 측정의 유효성을 검사 하 여 호스트가 올바른 이진 파일 및 보안 정책만 실행 하는지 확인 합니다. 프로덕션 환경에는 TPM 증명 및 SQL Server를 실행 하는 실제 호스트 컴퓨터 (가상 컴퓨터가 아님)가 권장 됩니다.

호스트 보호자 서비스와이 서비스에서 측정할 수 있는 항목에 대 한 자세한 내용은 [보호 된 패브릭 및 보호 된 vm 개요](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)를 참조 하세요. 문서는 보호 된 Vm에 대해 이야기 하지만 동일한 보호, 아키텍처 및 모범 사례는 VBS enclaves를 사용 하 여 SQL Server Always Encrypted에 적용 됩니다. 

이 문서는 권장 구성에서 HGS를 설정 하는 데 도움이 됩니다. 

## <a name="prerequisites"></a>사전 요구 사항 

이 섹션에서는 HGS 및 호스트 컴퓨터에 대 한 필수 구성 요소를 다룹니다. 

### <a name="hgs-servers"></a>HGS 서버

- 1-3 서버에서 HGS를 실행 합니다. 

  > [!NOTE]
  > 테스트 또는 프리 프로덕션 환경에는 1 개의 HGS 서버만 필요 합니다.

  이러한 서버는 보안 enclaves Always Encrypted를 사용 하 여 SQL Server 인스턴스를 실행할 수 있는 컴퓨터를 제어 하므로 신중 하 게 보호 해야 합니다. 
  여러 관리자가 HGS 클러스터를 관리 하 고 나머지 인프라 또는 별도의 가상화 패브릭 또는 Azure 구독에서 격리 된 물리적 하드웨어에서 HGS를 실행 하는 것이 좋습니다.

  - Windows Server 2019 Standard 또는 Datacenter edition
  - Cpu 2 개
  - 8GB RAM
  - 100GB 저장소

  [LTSC (장기 서비스 채널)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) 또는 [반기 채널](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)중 하나를 사용할 수 있습니다. 
  Windows Server Insider Preview를 등록 하 고 다운로드 하려면 [Windows 참가자 프로그램 시작](https://insider.windows.com/for-business-getting-started-server/)을 참조 하세요.

- 호스트 보호자 서비스에서 만든 새 Active Directory 포리스트의 이름을 선택 합니다. 
  HGS는 기존 회사 도메인에 가입 되지 않아야 하 고 별도의 관리자가 관리 해야 합니다.   

- 에서 호스트 보호 서비스 노드의 인바운드 HTTP (TCP 80) 또는 HTTPS (TCP 443) 트래픽을 허용 하는 방화벽 및 라우팅 규칙: 

  - SQL Server를 실행 하는 컴퓨터
  - 데이터베이스 쿼리를 실행 하 고 secure enclaves와 Always Encrypted를 사용 하는 데이터베이스 클라이언트 응용 프로그램 (예: 웹 서버)을 실행 하는 컴퓨터입니다. 

### <a name="sql-server-host-machines"></a>호스트 컴퓨터 SQL Server

- SQL Server 인스턴스는 다음 요구 사항을 충족 하는 컴퓨터에서 실행 해야 합니다.

  - Windows: 
    - Windows 10 Enterprise, 버전 1809  
    - Windows Server 2019 Datacenter (반기 채널), 버전 1809
    - Windows Server 2019 Datacenter
  - 프로덕션을 위한 물리적 컴퓨터 또는 테스트용 2 세대 가상 컴퓨터 (Azure는 2 세대 Vm을 지원 하지 않음)
  - [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017)에 나열 된 일반 요구 사항   

  [LTSC (장기 서비스 채널)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) 또는 [반기 채널](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)중 하나를 사용할 수 있습니다. 
  Windows Server Insider Preview를 등록 하 고 다운로드 하려면 [Windows 참가자 프로그램 시작](https://insider.windows.com/for-business-getting-started-server/)을 참조 하세요.

- 선택한 증명 모드와 관련 된 요구 사항:
  - **Tpm 모드** 는 가장 강력한 증명 모드 이며, tpm (신뢰할 수 있는 플랫폼 모듈)을 사용 하 여 호스트 컴퓨터가 사용자의 데이터 센터에 알려진 지 (각 TPM의 고유 ID 사용), 신뢰할 수 있는 하드웨어 및 펌웨어를 실행 하는 것을 암호화 합니다. 구성 (TPM 기준 사용) 및 신뢰할 수 있는 커널 및 사용자 모드 코드 실행 (Windows Defender 응용 프로그램 제어 사용) TPM 모드를 사용 하려면 다음 하드웨어가 필요 합니다. 
    - TPM 2.0 모듈이 설치 되 고 사용 하도록 설정 됨 
    - Microsoft 보안 부팅 정책으로 보안 부팅 사용 (타사 보안 부팅 CA 정책 또는 사용자 지정 정책 사용 안 함)
    - 직접 메모리 액세스 공격을 방지 하는 IOMMU (Intel VT-d 또는 AMD) 

  - **호스트 키 모드** 는 비대칭 키 쌍 (SSH 키와 매우 유사)을 사용 하 여 SQL Server 실행 하려는 호스트 컴퓨터를 식별 하 고 권한을 부여 합니다. 이 모드는 설정 하기 쉬우며 특정 하드웨어 요구 사항은 없지만 호스트 컴퓨터에서 실행 되는 소프트웨어나 펌웨어는 확인 하지 않습니다.  

TPM이 호환 되는지 확인 하려면 secure enclaves를 사용 하 여 Always Encrypted를 사용 하 SQL Server를 실행 하려는 호스트 컴퓨터에서 다음 명령을 실행 합니다. TPM 증명을 사용 하려면 지원 되는 SpecVersions 목록에 "2.0"가 표시 되어야 합니다.

```powershell
Get-CimInstance -ClassName Win32_Tpm -Namespace root/cimv2/Security/MicrosoftTpm 
```

## <a name="set-up-the-first-hgs-node"></a>첫 번째 HGS 노드 설정 

호스트 보호자 서비스는 3 개 노드 클러스터를 사용 하 여 항상 사용 가능한 구성으로 작동 합니다. 다른 노드를 추가 하기 전에 노드를 완전히 설정 하는 것이 좋습니다. 

관리자 권한 PowerShell 세션에서 다음 명령을 모두 실행 합니다.

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. [!INCLUDE [Install HGS by default](../../includes/install-hgs-default.md)] 

3. [!INCLUDE [Determine a DNN](../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

   Secure enclaves를 사용 하는 Always Encrypted 경우, SQL Server를 실행 하는 호스트 컴퓨터와 데이터베이스 클라이언트 응용 프로그램을 실행 하는 컴퓨터는 모두 HGS에 연결 해야 하지만,이 경우에는 호스트 컴퓨터에만 증명이 필요 합니다.

4. 컴퓨터가 다시 부팅 되 면 HGS가 설치 되 고 서버가 Active Directory 구성 된 도메인 컨트롤러가 됩니다. 
   Active Directory 구성 중에는 로컬 컴퓨터 관리자 계정이 Domain Admins 그룹에 추가 되 고이 그룹의 구성원만 도메인 컨트롤러에 로그인 할 수 있습니다.
   도메인 관리자 계정 (예: administrator@bastion.local 또는 요새. local\administrator)을 사용 하 여 로그인 하거나 로그인을 위한 다른 도메인 관리자 계정을 만든 다음 증명 서비스를 구성 합니다.
   TPM 또는 호스트 키 증명을 선택 하 고 해당 명령을 실행 해야 합니다. 
   HgsServiceName에 대해 선택한 DNN를 지정 합니다.

   TPM 모드의 경우:

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustTpm
   ```

   호스트 키 모드의 경우:

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey 
   ```

5. SQL Server를 실행 하는 호스트 컴퓨터가 회사 DNS 서버에서 새 HGS 도메인 컨트롤러로 전달자를 설정 하 여 새 HGS 도메인 구성원의 DNS 이름을 확인할 수 있는지 확인 합니다. Windows Server DNS를 사용 하는 경우 조직의 DNS 서버에 있는 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행 하 여 조건부 전달자를 설정할 수 있습니다. 사용자 환경에 필요한 대로 아래의 Windows PowerShell 구문에서 이름 및 주소를 대체 합니다. 더 많은 HGS 노드를 추가한 후이 명령을 다시 실행 하 여 마스터 서버로 추가 합니다.

   ```powershell
   Add-DnsServerConditionalForwarderZone -Name <HGS domain name> -ReplicationScope "Forest" -MasterServers <IP addresses of HGS servers>
   ```

## <a name="set-up-additional-hgs-nodes-for-production-deployments"></a>프로덕션 배포를 위한 추가 HGS 노드 설정

클러스터에 노드를 추가 하려면 관리자 권한 PowerShell 세션에서 다음 명령을 실행 합니다. 

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. HGS 도메인 이름을 확인할 수 있도록 기본 HGS 서버를 가리키도록 DNS 클라이언트 확인자를 설정 합니다. 데스크톱 환경에서 서버를 사용 하는 경우 네트워크 및 공유 센터에서이 작업을 수행할 수 있습니다. Server Core에서 **sconfig .exe** 도구, 옵션 8 또는 **설정-dnsclientserveraddress** 를 사용 하 여 DNS 주소를 설정할 수 있습니다. 

3. 다음에는이 서버를 도메인 컨트롤러로 승격 합니다. 이 작업을 완료 하려면 도메인 관리자 자격 증명이 필요 하며 명령을 실행 한 후 디렉터리 서비스 복구 모드 암호를 입력 하 라는 메시지가 표시 됩니다. 

   ```powershell
   $HgsDomainName = 'bastion.local' 
   $HgsDomainCredential = Get-Credential 
 
   Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $HgsDomainCredential -Restart 
   ```

4. [!INCLUDE [Initialize HGS](../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="configure-hgs-for-https"></a>HTTPS에 대 한 HGS 구성 

기본적으로, HGS 서버를 초기화할 때 HTTP 전용 통신을 위한 IIS 웹 사이트가 구성 됩니다.

> [!NOTE]
> 메시지 가로채기 (man-in-the-middle) 공격을 방지 하기 위해 잘 알려진 신뢰할 수 있는 HGS 서버 인증서를 사용 하 여 HTTPS를 구성 해야 하므로 프로덕션 배포에 적합 합니다.

[!INCLUDE [Configure HTTPS](../../includes/configure-hgs-for-https.md)] 

> [!NOTE]
> Secure enclaves를 사용 하는 Always Encrypted SQL Server를 실행 하는 두 호스트 컴퓨터에서 SSL 인증서를 신뢰할 수 있어야 하며, 데이터베이스 클라이언트 응용 프로그램을 실행 하는 컴퓨터에서 HGS에 연결 해야 합니다. 

## <a name="collect-attestation-info-from-the-host-machines"></a>호스트 컴퓨터에서 증명 정보 수집

HGS가 설정 되 면 호스트 컴퓨터의 증명 정보를 사용 하 여 구성 해야 Always Encrypted 및 VBS secure enclaves를 사용 하 여 기밀 계산을 수행할 수 있도록 권한이 부여 되어야 하는 컴퓨터를 알 수 있습니다. 이러한 단계는 사용 하는 증명 모드에 따라 달라 집니다. 

### <a name="collect-tpm-attestation-artifacts"></a>TPM 증명 아티팩트 수집 

TPM 모드를 사용 하는 경우 각 호스트 컴퓨터의 관리자 권한 PowerShell 세션에서 다음 명령을 실행 하 여 증명에 대 한 지원을 설치 하 고 호스트 보호자 서비스에 등록 하는 데 필요한 정보를 수집 합니다. 

1. 호스트 컴퓨터에 HGS 클라이언트를 설치 하려면 보호 된 호스트 기능을 설치 합니다. 그러면 Hyper-v도 설치 됩니다. 
   이 컴퓨터에서 Vm을 실행 하지는 않지만 v m enclaves를 격리 하는 가상화 기반 보안 기능을 사용 하도록 설정 하려면 하이퍼바이저가 필요 합니다.

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Hyper-v 설치를 완료 하 라는 메시지가 표시 되 면 컴퓨터를 다시 시작 합니다. 
3. 코드 무결성 정책을 작성 하 여 시스템에서 실행할 수 있는 소프트웨어를 제한 합니다. 
   모든 Windows Defender 응용 프로그램 제어 정책으로 충분 합니다. 
   서버에서 Microsoft 소프트웨어를 실행 하는 경우 다음 명령을 실행 하 여 정책을 신속 하 게 만들 수 있습니다. 
   정책은 감사 모드에 있습니다. 즉, 권한 없는 코드에 대 한 이벤트를 기록 하지만 실행을 유지 하지는 않습니다.  

   ```powershell
   mkdir C:\artifacts
   Copy-Item C:\Windows\Schemas\CodeIntegrity\ExamplePolicies\AllowMicrosoft.xml C:\artifacts\AllowMicrosoft-Audit.xml 
   Set-RuleOption -FilePath C:\artifacts\AllowMicrosoft-Audit.xml -Option 3 
   ConvertFrom-CIPolicy -XmlFilePath C:\artifacts\AllowMicrosoft-Audit.xml -BinaryFilePath C:\artifacts\AllowMicrosoft-Audit.bin 
   Copy-Item C:\artifacts\AllowMicrosoft-Audit.bin C:\Windows\System32\CodeIntegrity\SIPolicy.p7b 
   Restart-Computer 
   ```

   Windows Defender 응용 프로그램 제어에는 다양 한 보안 postures를 다루는 다양 한 기능이 있습니다. 
   타사 소프트웨어를 허용 하거나 기본 정책을 사용자 지정 해야 하는 경우 [Windows Defender 응용 프로그램 제어 배포 가이드를 참조](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)하세요.   


4. 다음 명령을 사용 하 여 가상화 기반 보안이 컴퓨터에서 실행 되 고 있는지 확인 합니다. 
   DeviceGuardSecurityServicesRunning 필드에 "HypervisorEnforcedCodeIntegrity"가 나열 되어 있으면 VBS가 실행 되 고 있는 것을 알 수 있습니다. 
   실행 되 고 있지 않으면 [Device Guard 준비 도구](https://www.microsoft.com/download/details.aspx?id=53337) 를 다운로드 하 고 "DG_Readiness-hvci"를 실행 하 여 사용 하도록 설정 합니다.  
   
   ```powershell
   Get-ComputerInfo -Property DeviceGuard* 
   ```

5. TPM 식별자 및 기준 수집:

   ```powershell 
   (Get-PlatformIdentifier -Name $env:computername).Save("C:\artifacts\TpmID-$env:computername.xml") 
   Get-HgsAttestationBaselinePolicy -SkipValidation -Path "C:\artifacts\TpmBaseline-$env:computername.tcglog" 
   ```
   
6. Xml, tcglog 및 bin 파일을 C:\filea의 HGS 서버에 복사 합니다.
7. HGS 서버에 추가 하는 첫 번째 TPM 호스트인 경우 각 HGS 서버에 신뢰할 수 있는 TPM 루트 인증서를 설치 해야 합니다. 
   [HGS 설명서의 지침](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-install-trusted-tpm-root-certificates) 에 따라이 단계를 완료 합니다.
8. HGS 서버에서이 호스트가 증명을 전달 하도록 권한을 부여 합니다. 
   아래 스크립트는 HGS 서버에서 3 개의 파일이 C:\temp에 복사 되었고 서버의 컴퓨터 이름이 "서버 a" 라고 가정 합니다. 
   사용자 환경에 맞게 경로 및 이름을 조정 합니다. 

   ```powershell
   Add-HgsAttestationTpmHost -Name ServerA -Path C:\temp\TpmID-ServerA.xml 
   Add-HgsAttestationTpmPolicy -Name ServerA-Baseline -Path C:\temp\TpmBaseline-ServerA.tcglog 
   Add-HgsAttestationCiPolicy -Name AllowMicrosoft-Audit -Path C:\temp\AllowMicrosoft-Audit.bin 
   ```

9. 이제 첫 번째 서버에서 증명할 준비가 되었습니다! 
   호스트 컴퓨터에서 다음 명령을 실행 하 여 증명할 위치를 지시 합니다. (일반적으로 hgs 클러스터의 DNS 이름 변경, hgs 도메인 이름과 함께 사용 하는 hgs 서비스 이름 사용). 
   호스트에 연결할 수 없음 오류가 발생 하는 경우에는 HGS 서버의 DNS 이름을 확인 하 고 ping 할 수 있는지 확인 합니다. 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl https://hgs.bastion.local/Attestation -KeyProtectionServerUrl https://hgs.bastion.local/KeyProtection/ 
   ```

10. 위의 명령 결과는 AttestationStatus = 전달 됨을 표시 해야 합니다. 그렇지 않은 경우 오류를 해결 하는 방법에 대 한 지침은 [증명 오류](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts#attestation-failures) 를 참조 하세요.   
11. 각 호스트 컴퓨터에 대해 1-10 단계를 반복 합니다. 
    동일한 하드웨어를 사용 하는 경우 모든 컴퓨터에 대 한 새 기준 또는 CI 정책을 캡처하지 않아도 됩니다. 
    첫 번째 서버의 기준은 동일 하 게 구성 된 모든 컴퓨터를 포함 하며, Microsoft 소프트웨어가 컴퓨터의 유일한 소프트웨어 이면 CI 정책을 여러 컴퓨터에서 다시 사용할 수 있습니다.

### <a name="collecting-host-keys"></a>호스트 키 수집 

> [!NOTE] 
> 호스트 키 증명은 테스트 환경 에서만 사용 하는 것이 좋습니다. TPM 증명은 SQL Server에서 중요 한 데이터를 처리 하는 것이 신뢰할 수 있는 코드를 실행 하 고 컴퓨터에 권장 되는 보안 설정을 구성 하는 가장 강력한 보증을 제공 합니다. 

호스트 키 증명 모드에서 HGS를 설정 하도록 선택한 경우 각 호스트 컴퓨터에서 키를 생성 하 여 수집 하 고 호스트 보호자 서비스에 등록 해야 합니다. 

1. 호스트 컴퓨터에 HGS 클라이언트를 설치 하려면 보호 된 호스트 기능을 설치 합니다. 그러면 Hyper-v도 설치 됩니다. 
   이 컴퓨터에서 Vm을 실행 하지는 않지만 Always Encrypted 쿼리를 실행 하는 VBS enclaves를 격리 하는 가상화 기반 보안 기능을 사용 하도록 설정 하려면 하이퍼바이저가 필요 합니다. 

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Hyper-v 설치를 완료 하 라는 메시지가 표시 되 면 컴퓨터를 다시 시작 합니다.
3. 고유한 호스트 키를 생성 하 고 결과 공개 키를 파일로 내보냅니다. 

   ```powershell
   Set-HgsClientHostKey 
   mkdir C:\artifacts 
   Get-HgsClientHostKey -Path C:\artifacts\$env:computername.cer 
   ```
   
   또는 고유한 인증서를 사용 하려는 경우 지문을 지정할 수 있습니다. 
   이는 여러 컴퓨터에서 인증서를 공유 하거나 TPM 또는 HSM에 바인딩된 인증서를 사용 하려는 경우에 유용할 수 있습니다. 다음은 TPM 바인딩된 인증서를 만드는 예제입니다 (개인 키를 도난당 하 고 다른 컴퓨터에서 사용 하 고 TPM 1.2만 필요).

   ```powershell
   $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
   Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
   ```

4. 호스트 보호 서비스에 호스트 키를 복사 합니다. 
5. 사용자 환경에 관련 된 이름 및 경로를 사용 하 여 모든 HGS 노드에 호스트 키를 등록 합니다. 

   ```powershell
   Add-HgsAttestationHostKey -Name 'ServerA' -Path C:\temp\ServerA.cer 
   ``` 

6. 이제 첫 번째 서버에서 증명할 준비가 되었습니다! 
   호스트 컴퓨터에서 다음 명령을 실행 하 여 증명할 위치를 지시 합니다. (일반적으로 hgs 클러스터의 DNS 이름 변경, hgs 도메인 이름과 함께 사용 하는 hgs 서비스 이름 사용). 
   호스트에 연결할 수 없음 오류가 발생 하는 경우에는 HGS 서버의 DNS 이름을 확인 하 고 ping 할 수 있는지 확인 합니다.    

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://hgs.bastion.local/Attestation -KeyProtectionServerUrl http://hgs.bastion.local/KeyProtection/  
   ```

7. 위의 명령 결과는 AttestationStatus = 전달 됨을 표시 해야 합니다. 
   호스트에 연결할 수 없음 오류가 발생 하는 경우 호스트 컴퓨터가 HGS와 통신할 수 없음을 의미 합니다. 
   호스트 컴퓨터와 HGS 서버 간에 DNS 확인을 설정 하 고 서버를 ping 할 수 있는지 확인 합니다. 
   UnauthorizedHost 오류는 공개 키가 HGS 서버에 등록 되지 않았음을 나타냅니다.-4 단계와 5 단계를 반복 하 여 오류를 해결 합니다. 
   다른 모든 작업이 실패 하는 경우 HgsClientHostKey를 실행 하 고 3-6 단계를 반복 합니다.   

8. VBS enclaves를 사용 하 여 SQL Server Always Encrypted를 실행 하는 각 서버에 대해 1-7 단계를 반복 합니다.     


