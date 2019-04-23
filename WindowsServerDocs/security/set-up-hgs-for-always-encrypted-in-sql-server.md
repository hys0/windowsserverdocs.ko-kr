---
title: SQL Server의 Always Encrypted에 대 한 호스트 보호 서비스 설정
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/03/2018
ms.openlocfilehash: 2f800dfa01077287f8200dd8abea0be899776683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866694"
---
# <a name="setting-up-the-host-guardian-service-for-always-encrypted-with-secure-enclaves-in-sql-server"></a>SQL Server에서 보안 enclaves를 사용 하 여 Always Encrypted에 대 한 호스트 보호 서비스 설정 

>적용 대상: Windows Server (반기 채널), Windows Server 2019 SQL Server 2019 미리 보기
 
[상시 암호화와 보안 enclaves](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves) SQL Server 2019 미리 보기에서는 데이터베이스에 저장 된 중요 한 데이터 기밀 계산 작업을 사용 하도록 설정 하기 위한 기능입니다. (HGS (호스트 보호 서비스)는 Always Encrypted에 대해 구성 된 보안 enclave 가상화 기반 보안 (VBS)이 메모리 enclave 때 데이터를 안전 하 게 유지 하는 중요 한 역할을 재생 합니다. VBS 메모리 enclave의 보안 Windows 하이퍼바이저의 보안 및 보다 광범위 하 게 SQL Server를 호스팅하는 컴퓨터의 보안에 따라 달라 집니다. 

따라서 Always Encrypted에 대 한 중요 한 데이터에서 계산을 수행 하는 데 사용 하 여 VBS 메모리 enclave 데이터베이스 클라이언트 응용 프로그램을 허용 하기 전에 응용 프로그램을 신뢰할 수 있는 HGS 증명 해야 합니다. Enclave를 포함 하 고 올바른 상태에는 신뢰할 수 있는 SQL Server를 호스팅하는 컴퓨터를 입증 합니다. 이 항목의 나머지 부분을 간단히 호스트 컴퓨터와 SQL Server를 호스팅하는 컴퓨터를 지칭 합니다.

두 가지 증명 응용 프로그램에 대 한 상호 배타적인 방법이: 

- 호스트를 인증 하는 호스트 키 증명 알려져 있고 신뢰할 수 있는 개인 키를 소유 증명 하는 것입니다. 호스트 키 증명 및 물리적 호스트 컴퓨터 또는 SQL Server를 실행 하는 2 세대 가상 컴퓨터는 사전 프로덕션 환경에 대 한 것이 좋습니다.
- TPM 증명 올바른 이진 파일 및 보안 정책을 호스트에서 실행 되도록 하려면 하드웨어 측정의 유효성을 검사 합니다. TPM 증명 및 SQL Server를 실행 하는 물리적 호스트 컴퓨터 (가상 머신 아님)는 프로덕션 환경에 권장 됩니다.

호스트 보호 서비스 및 수 측정값에 대 한 자세한 내용은 참조 하세요. [보호 패브릭 및 차폐 Vm 개요](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)합니다. 문서를 보호 된 Vm에 대 한 이야기 하지만 동일한 보호, 아키텍처 및 모범 사례에 적용할 SQL Server Always Encrypted enclaves VBS를 사용 하 여 note 합니다. 

이 문서에서는 권장 되는 구성에서 HGS를 설정 하는 데 도움이 됩니다. 

## <a name="prerequisites"></a>사전 요구 사항 

이 섹션에서는 HGS 및 호스트 컴퓨터에 대 한 필수 구성 요소에 설명 합니다. 

### <a name="hgs-servers"></a>HGS 서버

- 1 ~ 3 서버가 HGS를 실행 합니다. 

  >[!NOTE]
  >하나의 HGS 서버 테스트 또는 프로덕션 전 환경에 필요합니다.

  이러한 서버는 컴퓨터 보안 enclaves를 사용 하 여 상시 암호화를 사용 하 여 SQL Server 인스턴스를 실행할 수 있습니다 제어 하므로 신중 하 게 보호 되어야 합니다. 
  다른 관리자 HGS 클러스터를 관리 하 고 Azure 구독 또는 별도 가상화 패브릭 또는 인프라의 나머지 부분에서 격리 된 물리적 하드웨어에서 HGS를 실행 하는 것이 좋습니다.

  - Windows Server 2019 Standard 또는 Datacenter edition
  - 2 개 Cpu
  - 8GB RAM
  - 100 GB 저장소

  하나를 사용 합니다 [장기 서비스 채널 LTSC ()](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) 또는 [반기 채널](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)합니다. 
  참조를 등록 하 고 Windows Server Insider Preview를 다운로드 [Windows 참가자 프로그램 시작](https://insider.windows.com/for-business-getting-started-server/)합니다.

- 호스트 보호자 서비스에 의해 만들어진 새 Active Directory 포리스트에 대 한 이름을 선택 합니다. 
  HGS는 기존 회사 도메인에 가입 되지 않아야 하 고 관리 하는 별도 관리자가 있어야 합니다.   

- 방화벽 및에서 호스트 보호자 서비스 노드에서 인바운드 HTTP (TCP 80) 또는 HTTPS (TCP 443) 트래픽을 허용 하는 라우팅 규칙: 

  - SQL Server를 실행 하는 컴퓨터
  - Database 클라이언트 응용 프로그램 (예: 웹 서버) 데이터베이스 쿼리를 실행 하 고 안전한 enclaves를 사용 하 여 상시 암호화를 사용 하는 실행 중인 컴퓨터입니다. 

### <a name="sql-server-host-machines"></a>SQL Server 호스트 컴퓨터

- SQL Server 인스턴스는 다음 요구 사항을 충족 하는 컴퓨터에서 실행 해야 합니다.

  - Windows: 
    - Windows 10 Enterprise 버전 1809  
    - Windows Server 2019 Datacenter (반기 채널) 버전 1809
    - Windows Server 2019 Datacenter
  - 프로덕션 환경 또는 테스트 (Azure에서 2 세대 Vm을 지원 하지 않음을 참고)에 대 한 2 세대 가상 컴퓨터에 대 한 물리적 컴퓨터
  - 에 나열 된 일반 요구 사항 [Hardware and Software Requirements for Installing SQL](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017)합니다.   

  하나를 사용 합니다 [장기 서비스 채널 LTSC ()](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) 또는 [반기 채널](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)합니다. 
  참조를 등록 하 고 Windows Server Insider Preview를 다운로드 [Windows 참가자 프로그램 시작](https://insider.windows.com/for-business-getting-started-server/)합니다.

- 선택한 증명 모드를 특정 요구 사항:
  - **TPM 모드** 가장 강력한 증명 모드 이며 신뢰할 수 있는 플랫폼 모듈 (TPM)를 사용 하 여 암호화 된 데이터 센터 (각 TPM에서 고유 ID 사용)를 신뢰할 수 있는 하드웨어 및 펌웨어를 실행 하 여 호스트 컴퓨터 정상 인지 유효성을 검사 하는 (사용 하 여 TPM 기준)를 구성 하 고 신뢰할 수 있는 커널 및 (Windows Defender 응용 프로그램 제어를 사용 하 여) 사용자 모드 코드를 실행 합니다. 다음 하드웨어 TPM 모드를 사용 해야 합니다. 
    - TPM 2.0 모듈을 설치 및 사용 
    - 보안 부팅 Microsoft 보안 부팅 정책을 사용 하 여 사용 하도록 설정 (타사 파티 보안 부팅 CA 정책 또는 모든 사용자 지정 정책을 사용 수행)
    - IOMMU (Intel vt-d 또는 IOV AMD) 직접 메모리 액세스 공격을 방지 하기 위해 

  - **호스트 키 모드** 흡사 SSH 키는 비대칭 키 쌍을 사용 하 여를 식별 하 여 SQL Server를 실행 하려면 호스트 컴퓨터에 권한을 부여 합니다. 이 모드는 쉽게 설정할 수 및 특정 하드웨어 요구 사항이 없지만 소프트웨어 또는 호스트 컴퓨터에서 실행 하는 펌웨어를 확인 하지 않습니다.  

호환 TPM 인지를 확인 하려면 다음 명령을 실행 호스트 컴퓨터에서 보안 enclaves를 사용 하 여 상시 암호화를 사용 하 여 SQL Server를 실행 하려는 경우. "2.0" TPM 증명을 사용 하 여에 대 한 지원 되는 SpecVersions 목록에 나타나야 합니다.

```powershell
Get-CimInstance -ClassName Win32_Tpm -Namespace root/cimv2/Security/MicrosoftTpm 
```

## <a name="set-up-the-first-hgs-node"></a>첫 번째 HGS 노드 설정 

호스트 보호 서비스는 3 노드 클러스터를 사용 하 여 항상 사용 가능한 구성에서 작동 합니다. 설정 하는 하나의 노드가 완전히 다른 노드를 추가 하기 전에 것이 좋습니다. 

관리자 권한 PowerShell 세션에서 다음 명령을 모두를 실행 합니다.

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. [!INCLUDE [Install HGS by default](../../includes/install-hgs-default.md)] 

3. [!INCLUDE [Determine a DNN](../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

   보안 enclaves를 사용 하 여 Always Encrypted에 대해 컴퓨터 및 SQL Server을 실행 하는 호스트 컴퓨터 둘 다에 문의 해야 HGS를 호스트 컴퓨터만 증명 필요 하지만 database 클라이언트 응용 프로그램을 실행 합니다.

4. 컴퓨터 다시 부팅 한 후 HGS를 설치 하 고 서버에서 구성 된 Active Directory를 사용 하 여 도메인 컨트롤러도 됩니다. 
   Active Directory를 구성 하는 동안 로컬 컴퓨터 관리자 계정이 Domain Admins 그룹에 추가 되 고이 그룹의 구성원만이 도메인 컨트롤러에 로그인 할 수 있습니다.
   도메인 관리자 계정을 사용 하 여 로그인 (예를 들어 administrator@bastion.local 또는 bastion.local\administrator)에 대 한 다른 도메인 관리자 계정을 만들거나 로그인 하 고 다음 증명 서비스를 구성 합니다.
   호스트 또는 TPM 키 증명을 선택 하 고 해당 명령을 실행 해야 합니다. 
   선택한 DNN HgsServiceName를 지정 합니다.

   TPM 모드의 경우:
   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustTpm
   ```

   호스트 키 모드:
   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey 
   ```

5. SQL Server를 실행 하는 호스트 컴퓨터 전달자 회사 DNS 서버에서 새 HGS 도메인 컨트롤러를 설정 하 여 새 HGS 도메인 구성원의 DNS 이름을 확인할 수 있는지 확인 합니다. Windows Server DNS를 사용 하는 경우 조직에서 DNS 서버에서 관리자 권한 PowerShell 콘솔에서 다음 명령을 실행 하 여 조건부 전달자를 설정할 수 있습니다. 이름 및 사용자 환경에 대 한 필요에 따라 아래 Windows PowerShell 구문에서 주소를 대체 합니다. HGS 노드를 추가한 후 다시 마스터 서버를 추가 하려면이 명령을 실행 합니다.

   ```powershell
   Add-DnsServerConditionalForwarderZone -Name <HGS domain name> -ReplicationScope "Forest" -MasterServers <IP addresses of HGS servers>
   ```

## <a name="set-up-additional-hgs-nodes-for-production-deployments"></a>프로덕션 배포에 대 한 추가 HGS 노드 설정

클러스터에 노드를 추가 하려면 관리자 권한 PowerShell 세션에서 다음 명령을 실행 합니다. 

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. HGS 도메인 이름을 확인할 수 있도록 주 HGS 서버를 가리키도록 DNS 클라이언트 확인자를 설정 합니다. 데스크톱 환경 포함 서버를 사용 하는 경우 네트워크 및 공유 센터에이 수행할 수 있습니다. Server core에서 사용할 수 있습니다 합니다 **sconfig.exe** 도구, 8, 옵션 또는 **Set-dnsclientserveraddress** DNS 주소를 설정 합니다. 

3. 다음으로,이 서버를 도메인 컨트롤러로 승격 하려는 됩니다. 이 작업을 완료 하려면 도메인 관리자 자격 증명이 필요 하 고 명령을 실행 한 후 디렉터리 서비스 복구 모드 암호를 입력 하 라는 메시지가 표시 됩니다. 

   ```powershell
   $HgsDomainName = 'bastion.local' 
   $HgsDomainCredential = Get-Credential 
 
   Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $HgsDomainCredential -Restart 
   ```

4. [!INCLUDE [Initialize HGS](../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="configure-hgs-for-https"></a>HTTPS에 대 한 HGS 구성 

HGS 서버를 초기화 하는 경우 기본적으로 HTTP 전용 통신을 위해 IIS 웹 사이트를 구성 합니다 것입니다.

>[!NOTE]
>잘 알려져 있고 신뢰할 수 있는 HGS 서버 인증서를 사용 하 여 HTTPS를 구성 하는 중간자 개입 공격을 방지 하는 데 필요한 및 프로덕션 배포에 따라서 것이 좋습니다.

[!INCLUDE [Configure HTTPS](../../includes/configure-hgs-for-https.md)] 

>[!NOTE]
>보안 enclaves를 사용 하 여 Always Encrypted에 대해 SSL 인증서를 SQL Server를 실행 하는 두 호스트 컴퓨터에서 신뢰할 수 하며 database 클라이언트 응용 프로그램을 실행 하는 컴퓨터를 HGS에 문의 해야 합니다. 

## <a name="collect-attestation-info-from-the-host-machines"></a>호스트 컴퓨터의 증명 정보를 수집 합니다.

HGS 설정 되 면 보안 enclaves 상시 암호화 및 VBS를 사용 하 여 기밀 계산을 수행 하는 컴퓨터에 권한이 부여 되어야 알 수 있도록 호스트 컴퓨터에서 증명 정보를 사용 하 여 구성 해야 합니다. 다음이 단계를 사용 하는 증명 모드에 따라 다릅니다. 

### <a name="collect-tpm-attestation-artifacts"></a>TPM 증명 아티팩트를 수집 합니다. 

TPM 모드를 사용 하는 경우 증명에 대 한 지원을 설치 하 고 호스트 보호 서비스를 사용 하 여 등록 해야 하는 정보를 수집 하도록 각 호스트 컴퓨터에서 관리자 권한 PowerShell 세션에서 다음 명령을 실행 합니다. 

1. 호스트 컴퓨터에서 HGS 클라이언트를 설치 하려면 Hyper-v를 설치할 수도 보호 된 호스트 기능을 설치 합니다. 
   있습니다 하지을 실행 하는 Vm이이 컴퓨터에 있지만 하이퍼바이저 VBS enclaves를 격리 하는 가상화 기반 보안 기능을 사용 하도록 설정 하려면 필요 합니다.

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Hyper-v의 설치를 완료 하 라는 메시지가 나타나면 컴퓨터를 다시 시작 합니다. 
3. 시스템에서 실행 가능한 소프트웨어를 제한 하는 코드 무결성 정책을 구성 합니다. 
   모든 Windows Defender 응용 프로그램 제어 정책을 부족 합니다. 
   서버에서 Microsoft 소프트웨어를 한만 실행 하는 경우 다음 명령을를 정책의 신속 하 게 만듭니다. 
   정책이 감사 모드, 즉 무단된 코드에 대 한 이벤트를 기록 하는 않지만 실행에서 유지 되지 것입니다 됩니다.  

   ```powershell
   mkdir C:\artifacts
   Copy-Item C:\Windows\Schemas\CodeIntegrity\ExamplePolicies\AllowMicrosoft.xml C:\artifacts\AllowMicrosoft-Audit.xml 
   Set-RuleOption -FilePath C:\artifacts\AllowMicrosoft-Audit.xml -Option 3 
   ConvertFrom-CIPolicy -XmlFilePath C:\artifacts\AllowMicrosoft-Audit.xml -BinaryFilePath C:\artifacts\AllowMicrosoft-Audit.bin 
   Copy-Item C:\artifacts\AllowMicrosoft-Audit.bin C:\Windows\System32\CodeIntegrity\SIPolicy.p7b 
   Restart-Computer 
   ```

   Windows Defender 응용 프로그램 제어에 다양 한 보안 postures에 맞게 다양 한 기능이 있습니다. 
   타사 소프트웨어를 허용 하거나 se 기본 정책을 사용자 지정 하는 경우는 [Windows Defender 응용 프로그램 제어 배포 가이드](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)합니다.   


4. 가상화 기반 보안 다음 명령 사용 하 여 컴퓨터에서 실행 되 고 있는지 확인 합니다. 
   DeviceGuardSecurityServicesRunning 필드에 "HypervisorEnforcedCodeIntegrity"에 나열 된 VBS 실행 되 고 있는지 알 수 있습니다. 
   실행 하지 않는 경우 다운로드 합니다 [장치 가드 준비 도구](https://www.microsoft.com/download/details.aspx?id=53337) 실행 및 "DG_Readiness.ps1--HVCI를 사용 하도록 설정" 사용 하도록 설정 합니다.  
   
   ```powershell
   Get-ComputerInfo -Property DeviceGuard* 
   ```
5. TPM 식별자 및 기준 수집 합니다.

   ```powershell 
   (Get-PlatformIdentifier -Name $env:computername).Save("C:\artifacts\TpmID-$env:computername.xml") 
   Get-HgsAttestationBaselinePolicy -SkipValidation -Path "C:\artifacts\TpmBaseline-$env:computername.tcglog" 
   ```
   
6. Xml, tcglog, 및 bin 파일 C:\artifacts에서 HGS 서버에 복사 합니다.
7. 첫 번째 TPM 호스트는 HGS 서버를 추가 하는 경우 각 HGS 서버에 신뢰할 수 있는 TPM 루트 인증서를 설치 해야 합니다. 
   수행 합니다 [HGS 설명서에 대 한 지침](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-install-trusted-tpm-root-certificates) 이 단계를 완료 합니다.
8. HGS 서버에서이 호스트에서 증명을 전달 권한을 부여 합니다. 
   아래의 스크립트 HGS 서버에서 파일 세 개를 C:\temp로 복사 된 서버의 컴퓨터 이름 "ServerA" 임을 가정 합니다. 
   경로 이름을 사용자 환경에 맞게 조정 합니다. 

   ```powershell
   Add-HgsAttestationTpmHost -Name ServerA -Path C:\temp\TpmID-ServerA.xml 
   Add-HgsAttestationTpmPolicy -Name ServerA-Baseline -Path C:\temp\TpmBaseline-ServerA.tcglog 
   Add-HgsAttestationCiPolicy -Name AllowMicrosoft-Audit -Path C:\temp\AllowMicrosoft-Audit.bin 
   ```
9. 첫 번째 서버 증명할 준비가 되었습니다! 
   호스트 컴퓨터에서 (HGS 클러스터의 DNS 이름을 일반적으로 사용할지 HGS 도메인 이름과 결합 된 HGS 서비스 이름 변경)를 증명할 수 있는 위치를 확인 하려면 다음 명령을 실행 합니다. 
   HostUnreachable 오류가 발생 하는 경우 해결 하 고 DNS 이름을 HGS 서버를 ping 할 수 있습니다를 확인 합니다. 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl https://hgs.bastion.local/Attestation -KeyProtectionServerUrl https://hgs.bastion.local/KeyProtection/ 
   ```

10. 위의 명령의 결과 표시 해야 해당 AttestationStatus = 성공 합니다. 그렇지 않은 경우 [증명 오류](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts#attestation-failures) 오류를 해결 하는 방법에 대 한 지침에 대 한 합니다.   
11. 각 호스트 컴퓨터에 대해 1 ~ 10 단계를 반복 합니다. 
    동일한 하드웨어를 사용 하는 경우 새 기준 또는 모든 컴퓨터에 대 한 CI 정책 캡처 해야 하지 않습니다. 
    첫 번째 서버에서 초기에 동일 하 게 구성 된 모든 컴퓨터에 다룰 및 CI 정책을 다시 사용할 수 있습니다 여러 컴퓨터에서 Microsoft 소프트웨어는 컴퓨터에만 소프트웨어 하기만 합니다.

### <a name="collecting-host-keys"></a>호스트 키를 수집합니다. 

>[!NOTE] 
>호스트 키 증명만 테스트 환경에서 사용 하기 위해 권장 됩니다. TPM 증명 SQL Server에서 중요 한 데이터를 처리 하는 VBS enclaves 신뢰할 수 있는 코드를 실행 하는 컴퓨터는 권장 되는 보안 설정을 사용 하 여 구성 됩니다 가장 강력한 보증을 제공 합니다. 

호스트 키 증명 모드에서 HGS 설정 하기로 하 생성 각 호스트 컴퓨터에서 키를 수집 하 고 호스트 보호 서비스에 등록 해야 합니다. 

1. 호스트 컴퓨터에 설치 된 HGS 클라이언트를 가져오려면 Hyper-v도 설치 하는 보호 된 호스트 기능을 설치 합니다. 
   있습니다 하지을 실행 하는 Vm이이 컴퓨터에 있지만 하이퍼바이저 Always Encrypted 쿼리를 실행 하는 VBS enclaves를 격리 하는 가상화 기반 보안 기능을 사용 하도록 설정 하려면 필요 합니다. 

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Hyper-v의 설치를 완료 하 라는 메시지가 나타나면 컴퓨터를 다시 시작 합니다.
3. 고유한 호스트 키를 생성 하 고 파일로 결과 공개 키를 내보냅니다. 

   ```powershell
   Set-HgsClientHostKey 
   mkdir C:\artifacts 
   Get-HgsClientHostKey -Path C:\artifacts\$env:computername.cer 
   ```
   
   또는 사용자 고유의 인증서를 사용 하려는 경우 지문을 지정할 수 있습니다. 
   이 여러 컴퓨터에 인증서를 공유 하거나 TPM 또는 HSM에 바인딩된 인증서를 사용 하려는 경우에 유용할 수 있습니다. TPM 바인딩된 인증서 (개인 키를 도난당 하 고 다른 컴퓨터에서 사용할 수 없도록 방지 및 TPM 1.2만 필요)을 만드는 예제는 다음과 같습니다.

   ```powershell
   $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
   Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
   ```

4. 호스트 보호자 서비스를 호스트 키를 복사 합니다. 
5. 사용자 환경에 관련 된 이름 및 경로 사용 하 여 HGS 노드를 사용 하 여 호스트 키를 등록 합니다. 

   ```powershell
   Add-HgsAttestationHostKey -Name 'ServerA' -Path C:\temp\ServerA.cer 
   ``` 

6. 첫 번째 서버 증명할 준비가 되었습니다! 
   호스트 컴퓨터에서 (HGS 클러스터의 DNS 이름을 일반적으로 사용할지 HGS 도메인 이름과 결합 된 HGS 서비스 이름 변경)를 증명할 수 있는 위치를 확인 하려면 다음 명령을 실행 합니다. 
   HostUnreachable 오류가 발생 하는 경우 해결 하 고 DNS 이름을 HGS 서버를 ping 할 수 있습니다를 확인 합니다.    

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://hgs.bastion.local/Attestation -KeyProtectionServerUrl http://hgs.bastion.local/KeyProtection/  
   ```

7. 위의 명령의 결과 표시 해야 해당 AttestationStatus = 성공 합니다. 
   HostUnreachable 오류가 발생할 경우 즉, 호스트 컴퓨터 HGS와 통신할 수 없습니다. 
   DNS 확인 호스트 컴퓨터와 HGS 서버 간에 설정 되 고 서버를 ping 할 수 있는지 확인 합니다. 
   UnauthorizedHost 오류 HGS 서버 –이 오류를 해결 하려면 4, 5 단계를 반복으로 공개 키 등록 되지 않은 것을 나타냅니다. 
   모든 작업이 실패 하면 Clear HgsClientHostKey를 실행 하 고 3 ~ 6 단계를 반복 합니다.   

8. SQL Server Always Encrypted enclaves VBS를 사용 하 여 실행 하는 각 서버에 대해 1-7 단계를 반복 합니다.     


