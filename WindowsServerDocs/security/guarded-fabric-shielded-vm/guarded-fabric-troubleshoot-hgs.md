---
title: 호스트 보호자 서비스 문제 해결
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 424b8090-0692-49a6-9dc4-3c0e77d74b80
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: 05888ce57b5b922fc330d9deab430d329fede69b
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222529"
---
# <a name="troubleshooting-the-host-guardian-service"></a>호스트 보호자 서비스 문제 해결

> 적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 배포 또는 보호 된 패브릭에서 호스트 보호자 서비스 (HGS) 서버를 운영 하는 경우 발생 하는 일반적인 문제 해결 방법을 설명 합니다.
첫 번째 실행에 문제의 특성의 확실 하지 않은 경우는 [fabric 진단 보호](guarded-fabric-troubleshoot-diagnostics.md) HGS 서버 및 잠재적을 줄이기 위해 Hyper-v 호스트에서 발생 합니다.

## <a name="certificates"></a>인증서

HGS 인증서가 필요한 몇 가지 운영 하기 위해 관리자 구성 암호화를 포함 하 여 및 자체는 HGS에서 관리 인증서 뿐 아니라 증명 인증서를 서명 합니다.
이러한 인증서를 잘못 구성 하는 경우 HGS 증명 또는 보호 된 Vm에 대 한 키 보호기를 잠금 해제 하려는 Hyper-v 호스트에서 요청을 처리할 수 없습니다.
다음 섹션에서 HGS에 구성 된 인증서와 관련 된 일반적인 문제를 설명 합니다.

### <a name="certificate-permissions"></a>인증서 권한

HGS는 암호화 및 서명 된 인증서 지 문으로 HGS에 추가 하는 인증서의 공용 및 개인 키에 액세스할 수 있어야 합니다.
관리 그룹에 특히 HGS 서비스를 실행 하는 서비스 계정 (gMSA) 키에 액세스 해야 합니다.
HGS에서 사용 하는 gMSA를 찾으려면 HGS 서버에서 관리자 권한 PowerShell 프롬프트에서 다음 명령을 실행:

```powershell
(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName
```

키가 저장 될 위치에 따라 달라 집니다 개인 키를 사용 하려면 gMSA 계정 액세스를 부여 하는 방법: 하드웨어 보안 모듈 (HSM) 또는 사용자 지정 타사 키 저장소 공급자를 사용 하 여 로컬 인증서 파일을 컴퓨터에 있습니다.

#### <a name="grant-access-to-software-backed-private-keys"></a>소프트웨어 백업 개인 키에 액세스 권한 부여

자체 서명 된 인증서 또는 되는 인증 기관에서 발급 한 인증서를 사용 하는 경우 **되지** 하드웨어 보안 모듈 또는 사용자 지정 키 저장소 공급자에 저장 권한을 변경할 수 있습니다는 개인 키를 수행 하 여는 다음 단계:

1. 열기 로컬 인증서 관리자 (certlm.msc)
2. 확장 **개인 > 인증서** 업데이트 하려는 서명 또는 암호화 인증서를 찾습니다.
3. 선택한 인증서를 마우스 오른쪽 단추로 클릭 **모든 작업 > 개인 키 관리**합니다.
4. 클릭 **추가** 하려면의 개인 키에 대 한 새 사용자 액세스를 부여 합니다.
5. 개체 선택에서 gMSA 계정 이름과 HGS 앞에 입력 한 다음 클릭 **확인**합니다.
6. GMSA를 갖도록 **읽기** 인증서에 액세스 합니다.
7. 클릭 **확인** 권한 창을 닫습니다.

Server Core에서 HGS를 실행 하는 서버를 원격으로 관리 하는 경우 로컬 인증서 관리자를 사용 하 여 개인 키를 관리할 수 없습니다.
다운로드 해야 하는 대신 합니다 [보호 된 패브릭 도구 PowerShell 모듈](https://www.powershellgallery.com/packages/GuardedFabricTools) PowerShell에서 사용 권한을 관리할 수 있는 합니다.

1. Server Core 컴퓨터에서 관리자 권한 PowerShell 콘솔을 열거나 HGS에서 로컬 관리자 권한이 있는 계정으로 PowerShell Remoting을 사용 합니다.
2. 보호 된 패브릭 도구 PowerShell 모듈을 설치 하 고 개인 키에 대 한 gMSA 계정 액세스 권한을 부여 하려면 다음 명령을 실행 합니다.

```powershell
$certificateThumbprint = '<ENTER CERTIFICATE THUMBPRINT HERE>'

# Install the Guarded Fabric Tools module, if necessary
Install-Module -Name GuardedFabricTools -Repository PSGallery

# Import the module into the current session
Import-Module -Name GuardedFabricTools

# Get the certificate object
$cert = Get-Item "Cert:\LocalMachine\My\$certificateThumbprint"

# Get the gMSA account name
$gMSA = (Get-IISAppPool -Name KeyProtection).ProcessModel.UserName

# Grant the gMSA read access to the certificate
$cert.Acl = $cert.Acl | Add-AccessRule $gMSA Read Allow
```

#### <a name="grant-access-to-hsm-or-custom-provider-backed-private-keys"></a>HSM 또는 사용자 지정 공급자 기반 개인 키에 액세스 권한 부여

인증서의 개인 키 하드웨어 보안 모듈 (HSM) 또는 사용자 지정 키 저장소 공급자 KSP ()를 지 원하는, 하는 경우 권한 모델 특정 소프트웨어 공급 업체에 따라 달라 집니다.
최상의 결과 공급 업체의 설명서를 참조 하거나 특정 장치/소프트웨어에 대 한 사용 권한 처리 방법 개인 키에 대 한 정보에 대 한 사이트를 지원 합니다.

일부 하드웨어 보안 모듈에서 특정 사용자 계정에 액세스 권한을 부여는 개인 키를 지원 하지 않습니다. 대신, 특정 키 집합의 모든 키에 대 한 컴퓨터 계정 액세스를 수 있습니다.
이러한 장치에 대 한 키 컴퓨터 액세스 권한을 부여 하려면 일반적으로 부족 및 HGS 해당 연결을 활용할 수 있게 됩니다.

**Hsm에 대 한 팁**

다음은 도움이 성공적으로 사용 하 여 HSM 백업 키 Microsoft 및 해당 파트너의 환경을 기반으로 하는 HGS를 사용 하 여 제안 된 구성 옵션입니다.
이러한 팁 편의 위해 제공 되 고 읽기 시 올바른 것으로 보장 되지 않습니다는는 HSM 제조업체에서 인증 됩니다.
추가 질문이 있는 경우 특정 장치에 대 한 정확한 정보에 대 한 HSM 제조업체에 문의 합니다.

HSM 브랜드/시리즈      | 제안
----------------------|-------------
Gemalto SafeNet       | 인증서 요청 파일에서 키 사용량 속성은 설정 확인 0xa0, 서명 및 암호화에 사용할 인증서를 허용 합니다. GMSA 계정에 부여 해야 뿐만 *읽을* 로컬 인증서 관리자 도구를 사용 하 여 개인 키에 대 한 액세스 (위의 단계 참조).
nCipher nShield        | HGS 노드마다 서명 및 암호화 키가 포함 된 보안 권역에 대 한 액세스 권한이 있는지 확인 합니다. GMSA 관련 사용 권한을 구성할 필요가 없습니다.
Utimaco CryptoServers | 인증서 요청 파일의 키 사용 속성이 설정 확인 0x13, 암호화, 해독 및 서명에 사용할 인증서를 허용 합니다.

### <a name="certificate-requests"></a>인증서 요청

인증 기관 PKI (공개 키 인프라) 환경에서 인증서를 발급할지를 사용 하는 경우에 인증서 요청에 해당 키의 HGS의 사용량에 대 한 최소 요구 사항을 확인 해야 합니다.

**서명 인증서**

CSR 속성 | 필수 값
-------------|---------------
알고리즘    | RSA
키 크기     | 2048 비트 이상
키 사용    | Signature/Sign/DigitalSignature

**암호화 인증서**

CSR 속성 | 필수 값
-------------|---------------
알고리즘    | RSA
키 크기     | 2048 비트 이상
키 사용    | 암호화/암호화/DataEncipherment

**Active Directory 인증서 서비스 템플릿**

Active Directory 인증서 서비스 (ADCS) 인증서 템플릿 만들기를 사용 하는 경우 것이 좋습니다 인증서 템플릿을 다음 설정을 사용 하 여 사용 합니다.

ADCS Template 속성 | 필수 값
-----------------------|---------------
공급자 범주      | 키 저장소 공급자
알고리즘 이름         | RSA
최소 키 크기       | 2048
용도                | 서명 및 암호화
키 사용 확장    | 디지털 서명, 키 암호화, 데이터 암호화 ("허용 암호화의 사용자 데이터")


### <a name="time-drift"></a>시간 드리프트

다른 HGS 노드 또는 보호 된 패브릭에 Hyper-v 호스트에서 서버의 시간이 크게 드리프트를 하는 경우 증명 서명자 인증서 유효성 검사를 사용 하 여 문제를 발생할 수 있습니다.
증명 서명자 인증서 생성 되어 백그라운드에서 HGS에서 갱신는 보호 된 호스트에 증명 서비스에서 발급 하는 상태 인증서에 서명 하는 데 사용 됩니다.

증명 서명자 인증서를 새로 고치려면 관리자 권한 PowerShell 프롬프트에서 다음 명령을 실행 합니다.

```powershell
Start-ScheduledTask -TaskPath \Microsoft\Windows\HGSServer -TaskName 
AttestationSignerCertRenewalTask
```

또는 수동으로 실행할 수 있습니다 예약 형된 작업을 열어 **작업 스케줄러** (taskschd.msc)로 이동 **작업 Scheduler 라이브러리 > Microsoft > Windows > HGSServer** 및 실행 합니다 명명 된 작업 **AttestationSignerCertRenewalTask**합니다.

## <a name="switching-attestation-modes"></a>증명 모드를 전환합니다.

Active Directory 모드로 또는 그 반대로 사용 하 여 TPM 모드에서 HGS를 전환 합니다 [집합 HgsServer](https://technet.microsoft.com/library/mt652180.aspx) cmdlet, 새 증명 모드를 적용 하려면 HGS 클러스터의 모든 노드에 대해 10 분 정도 걸릴 수 있습니다.
이 정상적인 동작입니다.
성공적으로 새 증명 모드를 사용 하 여 모든 호스트는 증명 있는지 확인 하기 전에 이전 증명 모드에서 호스트를 허용 하는 정책을 제거 하지 않는 것이 좋습니다.

**TPM에서 AD 모드로 전환 하는 경우의 알려진된 문제**

Active Directory 모드로 TPM 모드 및 이후 스위치에서 HGS 클러스터를 초기화 하는 경우에 HGS 클러스터의 다른 노드에서 새 증명 모드를 전환 하지 못하게 하는 알려진된 문제가 있습니다.
실행을 보장 하기 위해 모든 HGS 서버 올바른 증명 모드를 적용 하 고 있으며 `Set-HgsServer -TrustActiveDirectory` **노드마다** HGS 클러스터.
AD 모드로 TPM 모드에서 전환 하는 경우이 문제가 적용 되지 않습니다 *및* AD 모드로 클러스터 된 원래 설정 합니다.

HGS 서버 증명 모드를 실행 하 여 확인할 수 있습니다 [Get HgsServer](https://technet.microsoft.com/library/mt652162.aspx)합니다.

## <a name="memory-dump-encryption-policies"></a>메모리 덤프 암호화 정책

기본 HGS 정책을 덤프 메모리 덤프 암호화 정책을 구성 하려는 경우에 표시 되지 않으면 (Hgs\_NoDumps, Hgs\_DumpEncryption 및 Hgs\_DumpEncryptionKey) 또는 덤프 정책 cmdlet ( Add-HgsAttestationDumpPolicy), 최신 누적 업데이트가 설치 되어 있는 것입니다.
이 문제를 해결 하려면 [HGS 서버를 업데이트](guarded-fabric-manage-hgs.md#patching-hgs) 누적 최신 Windows 업데이트를 하 고 [새 증명 정책 활성화](guarded-fabric-manage-hgs.md#updates-requiring-policy-activation)합니다.
새 덤프 암호화 기능 설치 되지 않은 호스트 증명 실패할 가능성이 높습니다 HGS 정책이 활성화 되 면 대로 새 증명 정책을 활성화 하기 전에 동일한 누적 업데이트 하기 위해 Hyper-v 호스트를 업데이트 해야 합니다.

## <a name="endorsement-key-certificate-error-messages"></a>인증 키 인증서 오류 메시지

사용 하 여 호스트를 등록 하는 경우는 [추가 HgsAttestationTpmHost](https://docs.microsoft.com/powershell/module/hgsattestation/add-hgsattestationtpmhost) cmdlet 두 TPM 식별자는 제공 된 플랫폼 식별자 파일에서 추출 된: 인증 키 인증서 (EKcert) 및 공용 인증 키 (EKpub).
EKcert는 TPM 인증 및 일반 공급 체인을 통해 제조 임을 보증을 제공 하는 TPM 제조업체를 식별 합니다.
고유 하 게 EKpub는 해당 특정 TPM을 식별 하 고 HGS가 사용 하 여 호스트 보호 된 Vm 실행에 대 한 액세스 권한을 부여 하는 측정값 중 하나입니다.

두 조건 중 하나에 해당할 경우 TPM 호스트를 등록 하는 경우는 오류가 발생 합니다.
1. 플랫폼 식별자 파일 **하지 않습니다** 인증 키 인증서를 포함 합니다.
2. 플랫폼 식별자 파일의 인증 키 인증서를 포함 하지만 해당 인증서가 **신뢰할 수 없는** 시스템에서

특정 TPM 제조업체의 Tpm에서 되도록 EKcerts 포함 되지 않습니다.
에 Tpm 해야 하지 ekcert를 사용 하는 TPM의 경우 이것이 것 같으면 oem에 게 확인을 `-Force` HGS를 사용 하 여 호스트를 수동으로 등록 하는 플래그입니다.
TPM EKcert 있어야 하지만 플랫폼 식별자 파일에 없는 경우 관리자 (권한 높은 권한) PowerShell 콘솔을 실행 하는 경우 사용 하기 [Get PlatformIdentifier](https://docs.microsoft.com/powershell/module/platformidentifier/get-platformidentifier) 호스트 합니다.

EKcert에 신뢰할 수 없는 오류를 받은 경우 했는지 [신뢰할 수 있는 TPM 루트 인증서 패키지 설치](guarded-fabric-install-trusted-tpm-root-certificates.md) TPM 공급 업체에 대 한 루트 인증서가 로컬 컴퓨터 에에서있는각HGS서버에서 **TrustedTPM\_RootCA** 저장 합니다. 적용 가능한 모든 중간 인증서에 설치 해야 합니다 **TrustedTPM\_IntermediateCA** 로컬 컴퓨터에 저장 합니다.
루트 및 중간 인증서를 설치한 후 실행할 수 있어야 `Add-HgsAttestationTpmHost` 성공적으로 합니다.
