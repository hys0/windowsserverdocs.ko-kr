---
title: 호스트 보호자 서비스 문제 해결
ms.prod: windows-server
ms.topic: article
ms.assetid: 424b8090-0692-49a6-9dc4-3c0e77d74b80
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: 4cbbb41b965a44b6c81b58adc94990bb4d6af046
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856406"
---
# <a name="troubleshooting-the-host-guardian-service"></a>호스트 보호자 서비스 문제 해결

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

이 항목에서는 보호 된 패브릭에서 HGS (호스트 보호 서비스) 서버를 배포 하거나 작동할 때 발생 하는 일반적인 문제에 대 한 해결 방법을 설명 합니다.
문제의 특성을 잘 모를 경우 먼저 HGS 서버 및 Hyper-v 호스트에서 보호 된 [패브릭 진단을](guarded-fabric-troubleshoot-diagnostics.md) 실행 하 여 잠재적인 원인을 좁혀 보세요.

## <a name="certificates"></a>인증서

HGS는 관리 구성 된 암호화 및 서명 인증서 뿐만 아니라 HGS 자체에서 관리 하는 증명 인증서를 포함 하 여 작동 하기 위해 여러 인증서가 필요 합니다.
이러한 인증서가 잘못 구성 된 경우 HGS는 보호 된 Vm에 대 한 키 보호기를 증명 하거나 잠금 해제 하려는 Hyper-v 호스트의 요청을 처리할 수 없습니다.
다음 섹션에서는 HGS에 구성 된 인증서와 관련 된 일반적인 문제를 다룹니다.

### <a name="certificate-permissions"></a>인증서 사용 권한

HGS는 인증서 지문을 사용 하 여 HGS에 추가 된 암호화 및 서명 인증서의 공개 키 및 개인 키에 모두 액세스할 수 있어야 합니다.
특히, HGS 서비스를 실행 하는 gMSA (그룹 관리 서비스 계정)는 키에 대 한 액세스 권한이 필요 합니다.
HGS에서 사용 하는 gMSA를 찾으려면 HGS 서버의 관리자 권한 PowerShell 프롬프트에서 다음 명령을 실행 합니다.

```powershell
(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName
```

GMSA 계정에 개인 키를 사용할 수 있는 액세스 권한을 부여 하는 방법은 키가 저장 되는 위치에 따라 달라 집니다. 컴퓨터는 로컬 인증서 파일, HSM (하드웨어 보안 모듈) 또는 사용자 지정 타사 키 저장소 공급자를 사용 합니다.

#### <a name="grant-access-to-software-backed-private-keys"></a>소프트웨어 지원 개인 키에 대 한 액세스 권한 부여

하드웨어 보안 모듈이 나 사용자 지정 키 저장소 공급자에 저장 **되지** 않은 인증 기관에서 발급 한 인증서 또는 자체 서명 된 인증서를 사용 하는 경우 다음 단계를 수행 하 여 개인 키 사용 권한을 변경할 수 있습니다.

1. 로컬 인증서 관리자 (인증서 관리자)를 엽니다.
2. **개인 > 인증서** 를 확장 하 고 업데이트 하려는 서명 또는 암호화 인증서를 찾습니다.
3. 인증서를 마우스 오른쪽 단추로 클릭 하 고 **모든 작업 >** 선택 하 여 개인 키를 관리 합니다.
4. **추가** 를 클릭 하 여 새 사용자에 게 certiciate의 개인 키에 대 한 액세스 권한을 부여 합니다.
5. 개체 선택에서 앞서 찾은 HGS의 gMSA 계정 이름을 입력 하 고 **확인**을 클릭 합니다.
6. GMSA에 인증서에 대 한 **읽기** 권한이 있는지 확인 합니다.
7. **확인** 을 클릭 하 여 사용 권한 창을 닫습니다.

Server Core에서 HGS를 실행 하는 경우 또는 서버를 원격으로 관리 하는 경우에는 로컬 인증서 관리자를 사용 하 여 개인 키를 관리할 수 없습니다.
대신 PowerShell에서 사용 권한을 관리 하는 데 사용할 수 있는 [보호 된 패브릭 도구 powershell 모듈](https://www.powershellgallery.com/packages/GuardedFabricTools) 을 다운로드 해야 합니다.

1. Server Core 컴퓨터에서 관리자 권한으로 PowerShell 콘솔을 열거나, HGS에 대 한 로컬 관리자 권한이 있는 계정으로 PowerShell 원격을 사용 합니다.
2. 다음 명령을 실행 하 여 보호 된 패브릭 도구 PowerShell 모듈을 설치 하 고 gMSA 계정에 개인 키에 대 한 액세스 권한을 부여 합니다.

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

#### <a name="grant-access-to-hsm-or-custom-provider-backed-private-keys"></a>HSM 또는 사용자 지정 공급자 지원 개인 키에 대 한 액세스 권한 부여

인증서의 개인 키가 HSM (하드웨어 보안 모듈) 또는 사용자 지정 KSP (키 저장소 공급자)에 의해 지원 되는 경우 사용 권한 모델은 특정 소프트웨어 공급 업체에 따라 다릅니다.
최상의 결과를 위해 특정 장치/소프트웨어에 대해 개인 키 권한이 처리 되는 방법에 대 한 자세한 내용은 공급 업체의 설명서 또는 지원 사이트를 참조 하십시오.
모든 경우에서 HGS가 사용 하는 gMSA에는 서명 및 암호화 작업을 수행할 수 있도록 암호화, 서명 및 통신 인증서 개인 키에 대 한 *읽기* 권한이 필요 합니다.

일부 하드웨어 보안 모듈은 특정 사용자 계정에 개인 키에 대 한 액세스 권한을 부여 하는 것을 지원 하지 않습니다. 대신, 컴퓨터 계정에서 특정 키 집합의 모든 키에 액세스할 수 있도록 허용 합니다.
이러한 장치의 경우 일반적으로 컴퓨터에 키에 대 한 액세스 권한을 부여 하는 데 충분 하며, HGS는 해당 연결을 활용할 수 있습니다.

**Hsm 팁**

다음은 Microsoft 및 해당 파트너의 경험을 기반으로 하는 HGS에서 HSM 지원 키를 성공적으로 사용 하는 데 도움이 되는 권장 구성 옵션입니다.
이러한 팁은 사용자 편의를 위해 제공 되며, 읽을 때 정확 하지 않을 수도 있고 HSM 제조업체에서 보증 수도 없습니다.
추가 질문이 있는 경우 HSM 제조업체에 특정 장치와 관련 된 정확한 정보를 문의 하세요.

HSM 브랜드/시리즈      | 제안
----------------------|-------------
Gemalto       | 인증서 요청 파일의 키 사용 속성이 0xa0로 설정 되었는지 확인 하 여 서명 및 암호화에 인증서를 사용할 수 있도록 합니다. 또한 로컬 인증서 관리자 도구를 사용 하 여 gMSA 계정에 개인 키에 대 한 *읽기* 액세스 권한을 부여 해야 합니다 (위의 단계 참조).
nCipher nShield        | 각 HGS 노드가 서명 및 암호화 키를 포함 하는 보안 영역에 액세스할 수 있도록 합니다. 로컬 인증서 관리자를 사용 하 여 개인 키에 대 한 *읽기* 액세스 권한을 gMSA에 추가로 부여 해야 할 수도 있습니다 (위 단계 참조).
Utimaco CryptoServers | 인증서 요청 파일의 키 사용 속성이 0x13로 설정 되었는지 확인 하 여 암호화, 암호 해독 및 서명에 인증서를 사용할 수 있도록 합니다.

### <a name="certificate-requests"></a>인증서 요청

인증 기관을 사용 하 여 PKI (공개 키 인프라) 환경에서 인증서를 발급 하는 경우 인증서 요청에 해당 키의 HGS 사용에 대 한 최소 요구 사항이 포함 되어 있는지 확인 해야 합니다.

**서명 인증서**

CSR 속성 | 필수 값
-------------|---------------
알고리즘    | RSA
키 크기     | 최소 2048 비트
키 사용    | 서명/서명/DigitalSignature

**암호화 인증서**

CSR 속성 | 필수 값
-------------|---------------
알고리즘    | RSA
키 크기     | 최소 2048 비트
키 사용    | 암호화/암호화/데이터 암호화

**Active Directory 인증서 서비스 템플릿**

인증서를 만드는 ADCS (Active Directory 인증서 서비스) 인증서 템플릿을 사용 하는 경우 다음 설정의 템플릿을 사용 하는 것이 좋습니다.

ADCS Template 속성 | 필수 값
-----------------------|---------------
공급자 범주      | 키 저장소 공급자
알고리즘 이름         | RSA
최소 키 크기       | 2048
용도                | 서명 및 암호화
키 사용 확장    | 디지털 서명, 키 암호화, 데이터 암호화 ("사용자 데이터의 암호화 허용")


### <a name="time-drift"></a>시간 드리프트

서버의 시간이 보호 된 패브릭의 다른 HGS 노드 또는 Hyper-v 호스트와 매우 데이터베이스가 드리프트 경우 증명 서명자 인증서의 유효성을 검사 하는 동안 문제가 발생할 수 있습니다.
증명 서명자 인증서는 HGS의 백그라운드에서 만들어지고 갱신 되며 증명 서비스에서 보호 된 호스트에 발급 된 상태 인증서에 서명 하는 데 사용 됩니다.

증명 서명자 인증서를 새로 고치려면 관리자 권한 PowerShell 프롬프트에서 다음 명령을 실행 합니다.

```powershell
Start-ScheduledTask -TaskPath \Microsoft\Windows\HGSServer -TaskName 
AttestationSignerCertRenewalTask
```

또는 **작업 스케줄러** (taskschd)를 열고 **작업 스케줄러 라이브러리 > Microsoft > Windows > HGSServer** 로 이동한 다음 **AttestationSignerCertRenewalTask**이라는 작업을 실행 하 여 예약 된 작업을 수동으로 실행할 수 있습니다.

## <a name="switching-attestation-modes"></a>증명 모드 전환

[HgsServer](https://technet.microsoft.com/library/mt652180.aspx) cmdlet을 사용 하 여 HGS를 TPM 모드에서 Active Directory 모드로 전환 하거나 그 반대로 전환 하는 경우, hgs 클러스터의 모든 노드가 새 증명 모드 적용을 시작 하는 데 최대 10 분이 소요 될 수 있습니다.
이는 정상적인 동작입니다.
모든 호스트가 새 증명 모드를 사용 하 여 성공적으로 증명 확인할 때까지 이전 증명 모드에서 호스트를 허용 하는 정책을 제거 하지 않는 것이 좋습니다.

**TPM에서 AD 모드로 전환할 때 발생 하는 알려진 문제**

TPM 모드에서 HGS 클러스터를 초기화 하 고 나중에 Active Directory 모드로 전환 하는 경우 HGS 클러스터의 다른 노드가 새 증명 모드로 전환 되지 않도록 하는 알려진 문제가 있습니다.
모든 HGS 서버가 올바른 증명 모드를 적용 하 고 있는지 확인 하려면 HGS 클러스터의 **각 노드에서** `Set-HgsServer -TrustActiveDirectory`를 실행 합니다.
TPM 모드에서 AD 모드로 전환 하 *고* 클러스터가 원래 ad 모드에서 설정 된 경우에는이 문제가 적용 되지 않습니다.

[HgsServer](https://technet.microsoft.com/library/mt652162.aspx)를 실행 하 여 HGS 서버의 증명 모드를 확인할 수 있습니다.

## <a name="memory-dump-encryption-policies"></a>메모리 덤프 암호화 정책

메모리 덤프 암호화 정책을 구성 하 고 기본 HGS 덤프 정책 (Hgs\_NoDumps, Hgs\_덤프 암호화 및 Hgs\_DumpEncryptionKey) 또는 덤프 정책 cmdlet (HgsAttestationDumpPolicy)이 표시 되지 않는 경우 최신 누적 업데이트가 설치 되지 않은 것일 수 있습니다.
이 문제를 해결 하려면 [HGS 서버](guarded-fabric-manage-hgs.md#patching-hgs) 를 최신 누적 Windows 업데이트로 업데이트 하 고 [새 증명 정책을 활성화](guarded-fabric-manage-hgs.md#updates-requiring-policy-activation)합니다.
새 증명 정책을 활성화 하기 전에 Hyper-v 호스트를 동일한 누적 업데이트로 업데이트 해야 합니다. 새로운 암호화 기능이 설치 되지 않은 호스트는 HGS 정책이 활성화 되 면 증명에 실패할 가능성이 높습니다.

## <a name="endorsement-key-certificate-error-messages"></a>인증 키 인증서 오류 메시지

[HgsAttestationTpmHost](https://docs.microsoft.com/powershell/module/hgsattestation/add-hgsattestationtpmhost) cmdlet을 사용 하 여 호스트를 등록 하는 경우 제공 된 플랫폼 식별자 파일에서 두 개의 TPM 식별자 (인증 키 인증서 (EKcert) 및 공용 인증 키 (EKpub))를 추출 합니다.
EKcert는 tpm의 제조업체를 식별 하 여 TPM이 일반 공급 체인을 통해 인증 되 고 제조 되었다는 보증을 제공 합니다.
EKpub는 특정 TPM을 고유 하 게 식별 하 고, HGS가 보호 된 Vm을 실행할 수 있는 호스트 액세스 권한을 부여 하는 데 사용 하는 측정값 중 하나입니다.

두 조건 중 하나에 해당 하는 경우 TPM 호스트를 등록할 때 다음과 같은 오류가 표시 됩니다.
1. 플랫폼 식별자 파일에 인증 키 인증서가 포함 되어 **있지** 않습니다.
2. 플랫폼 식별자 파일에 인증 키 인증서가 포함 되어 있지만 해당 인증서를 시스템에서 **신뢰할 수 없습니다** .

특정 TPM 제조업체의 TPM에 EKcerts 포함 되지 않습니다.
TPM을 사용 하는 것으로 의심 되는 경우 사용자의 tpm에 EKcert이 없어야 하 고 `-Force` 플래그를 사용 하 여 수동으로 HGS에 호스트를 등록 해야 하는지 확인 합니다.
TPM에 EKcert가 있어야 하지만 플랫폼 식별자 파일에서 찾을 수 없는 경우 호스트에서 [식별자](https://docs.microsoft.com/powershell/module/platformidentifier/get-platformidentifier) 를 실행할 때 관리자 (승격) PowerShell 콘솔을 사용 하 고 있는지 확인 합니다.

EKcert를 신뢰할 수 없다는 오류를 받은 경우 각 HGS 서버에 [신뢰할 수 있는 tpm 루트 인증서 패키지를 설치](guarded-fabric-install-trusted-tpm-root-certificates.md) 하 고 tpm 공급 업체의 루트 인증서가 로컬 컴퓨터의 신뢰할 수 있는 **tpm\_rootca.cer** 저장소에 있는지 확인 합니다. 해당 하는 모든 중간 인증서를 로컬 컴퓨터의 **IntermediateCA tpm\_** 저장소에도 설치 해야 합니다.
루트 및 중간 인증서를 설치한 후 `Add-HgsAttestationTpmHost` 성공적으로 실행할 수 있어야 합니다.
