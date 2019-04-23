---
title: 호스트 보호자 서비스 문제 해결
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 80ea38f4-4de6-4f85-8188-33a63bb1cf81
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7fe01039b47c36d940973fba97d25c401f5af8a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851374"
---
# <a name="troubleshooting-guarded-hosts"></a>보호 된 호스트의 문제 해결

> 적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

이 항목에서는 배포 또는 보호 된 패브릭에 보호 된 Hyper-v 호스트를 운영 하는 경우 발생 하는 일반적인 문제 해결 방법을 설명 합니다.
첫 번째 실행에 문제의 특성의 확실 하지 않은 경우는 [fabric 진단 보호](guarded-fabric-troubleshoot-diagnostics.md) 가능성 범위를 좁힐 하기 위해 Hyper-v 호스트에서 발생 합니다.

## <a name="guarded-host-feature"></a>호스트 기능 보호

Hyper-v 호스트를 사용 하 여 문제를 발생 하는 경우 먼저 확인 하는 합니다 **호스트 보호 Hyper-v 지원** 기능을 설치 합니다.
이 기능 없이 Hyper-v 호스트에 일부 중요 한 구성 설정이 누락 됩니다 및 증명 및 프로 비전을 전달할 수 있는 소프트웨어 보호 된 Vm입니다.

기능이 설치 되어 있는지를 확인 하려면 서버 관리자를 사용 하거나 관리자 권한 PowerShell 창에서 다음 명령을 실행:

```powershell
Get-WindowsFeature HostGuardian
```

기능이 설치 되지 않은 경우 다음 PowerShell 명령을 사용 하 여 설치 합니다.

```powershell
Install-WindowsFeature HostGuardian -Restart
```

## <a name="attestation-failures"></a>증명 오류

호스트의 호스트 보호자 서비스를 사용 하 여 증명을 통과 하지 못한 경우 보호 된 Vm을 실행할 수 없게 됩니다 것입니다.
출력 [Get-hgsclientconfiguration](https://technet.microsoft.com/library/dn914500.aspx) 해당 호스트에 정보가 표시 됩니다 호스트 하는 증명에 실패 한 이유는 방법에 대 한 합니다.

아래 테이블에 나타날 수 있는 값에 설명 합니다 **AttestationStatus** 필드 및 해당 하는 경우 잠재적인 다음 단계의 합니다.

AttestationStatus         | 설명
--------------------------|------------
만료됨                   | 호스트가 증명을 이전에 전달 하지만 발급 된 상태 인증서가 만료 되었습니다. 호스트 및 HGS 시간 동기화 되었는지 확인 합니다.
InsecureHostConfiguration | 호스트는 HGS에 구성 된 증명 정책을 준수 하지 않은 증명을 통과 하지 못했습니다. 자세한 내용은 AttestationSubStatus 표를 참조 하십시오.
NotConfigured             | 호스트는 HGS 증명 및 키 보호에 대 한 사용 하도록 구성 되지 않았습니다. 대신 로컬 모드에 대해 구성 된 것입니다. 사용 하 여이 호스트에 있는 경우 보호 된 패브릭 [집합 HgsClientConfiguration](https://technet.microsoft.com/library/dn914494.aspx) HGS 서버에 대 한 Url을 사용 하 여 제공 합니다.
전달                    | 호스트가 증명을 전달 합니다.
TransientError            | 마지막 증명 시도 네트워킹, 서비스 또는 다른 임시 오류로 인해 실패 했습니다. 마지막 작업을 다시 시도 합니다.
TpmError                  | 호스트는 TPM 오류로 인해 마지막 증명 시도 완료 하지 못했습니다. 자세한 내용은 TPM 로그를 참조 하십시오.
UnauthorizedHost          | 보호 된 Vm을 실행할 수 있는 권한이 없습니다 했습니다 때문에 호스트가 증명을 통과 하지 못했습니다. 호스트가 HGS 보호 된 Vm을 실행 하 여 신뢰할 수 있는 보안 그룹에 속하는지 확인 합니다.
알 수 없음                   | 호스트를 HGS 증명 하는 아직 시도 하지 않은 합니다.


때 **AttestationStatus** 으로 보고 됩니다 **InsecureHostConfiguration**에 하나 이상의 이유가 채워집니다 합니다 **AttestationSubStatus** 필드입니다.
아래 표에서 AttestationSubStatus 및 문제를 해결 하는 방법에 대 한 팁에 대 한 가능한 값에 설명 합니다.

AttestationSubStatus       | 의미와 수행할 작업
---------------------------|-------------------------------
BitLocker                  | 호스트의 OS 볼륨 BitLocker로 암호화 되지 않습니다. 이 해결 하려면 [BitLocker 사용](https://technet.microsoft.com/itpro/windows/keep-secure/bitlocker-basic-deployment) OS 볼륨에서 또는 [HGS에서 BitLocker 정책을 사용 하지 않도록](guarded-fabric-manage-hgs.md#review-attestation-policies)합니다.
CodeIntegrityPolicy        | 호스트 코드 무결성 정책을 사용 하도록 구성 되어 있지 않거나 HGS 서버에서 신뢰할 수 있는 정책을 사용 하지 않는 합니다. 코드 무결성 정책을 구성한 경우, 호스트를 다시 시작 하 고 정책에 등록 된 HGS 서버 확인 합니다. 자세한 내용은 [만들기 및 코드 무결성 정책 적용](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#create-and-apply-a-code-integrity-policy)합니다.
DumpsEnabled               | HGS 정책에 의해 허용 되지 않는 크래시 덤프를 허용 하거나 메모리 덤프를 실시간으로 호스트 구성 됩니다. 이 해결 하려면 호스트에서 덤프를 사용 하지 않도록 설정 합니다.
DumpEncryption             | 호스트는 크래시 덤프를 허용 하도록 구성 되어 또는 라이브 메모리 덤프는 덤프 암호화 하지 않습니다. 호스트에서 덤프를 사용 하지 않도록 설정 중 하나 또는 [덤프 암호화를 구성](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)합니다.
DumpEncryptionKey          | 호스트 허용 덤프 암호화를 구성 되어 있지만 증명을 암호화 하는 데 HGS에 알려진 인증서를 사용 하지 않습니다. 이 해결 하려면 [덤프 암호화 키를 업데이트](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption) 호스트에서 또는 [HGS 키 등록](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts)합니다.
FullBoot                   | 호스트 절전 또는 최대 절전 모드에서 다시 시작 합니다. 정리 및 전체 부팅 수 있도록 호스트를 다시 시작 합니다.
HibernationEnabled         | 호스트는 HGS 정책에 의해 허용 되지 않는 최대 절전 모드 파일을 암호화 하지 않고 최대 절전 모드를 허용 하도록 구성 됩니다. 최대 절전 모드를 사용 하지 않도록 설정 하 고 호스트를 다시 시작 하거나 [덤프 암호화를 구성](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)합니다.
HypervisorEnforcedCodeIntegrityPolicy | 호스트는 하이퍼바이저 적용 코드 무결성 정책을 사용 하도록 구성 되지 않았습니다. 코드 무결성은 사용 하도록 설정, 구성 및 하이퍼바이저에 의해 적용 되는 확인 합니다. 참조 된 [Device Guard 배포 가이드](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies) 자세한 내용은 합니다.
Iommu                      | 호스트의 가상화 기반 보안 기능 HGS 정책에서 필요에 따라 직접 메모리 액세스 공격 으로부터 보호 하기 위한 IOMMU 장치를 요구 하도록 구성 되지 않습니다. 호스트에서 IOMMU를 사용 하는 Device Guard는 확인 [DMA 보호를 요구 하도록 구성 된](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#enable-virtualization-based-security-vbs-and-device-guard) VBS를 시작할 때입니다.
PagefileEncryption         | 호스트 페이지 파일 암호화가 사용 되지 않습니다. 이 해결 하려면 실행 `fsutil behavior set encryptpagingfile 1` 페이지 파일 암호화를 사용 하도록 설정 합니다. 자세한 내용은 [fsutil 동작](https://technet.microsoft.com/library/cc785435.aspx)합니다.
SecureBoot                 | 보안 부팅 여부이 호스트에서 해제 하거나 사용 하는 Microsoft 보안 부팅 템플릿. [보안 부팅을 사용 하도록 설정](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/disabling-secure-boot#enable_secure_boot) 이 문제를 해결 하려면 Microsoft 보안 부팅 템플릿을 사용 하 여 합니다.
SecureBootSettings         | 이 호스트에서 TPM 기준 HGS가 신뢰할 수 있는 일치 하지 않습니다. 이 경우 UEFI 시작 기관, DBX, 디버그 플래그를 변수나 사용자 지정 보안 부팅 정책 새로운 하드웨어 또는 소프트웨어를 설치 하 여 변경 되 면 발생할 수 있습니다. 현재 설치 된 하드웨어, 펌웨어 및 소프트웨어 구성을이 컴퓨터의 신뢰할 수 있는 경우 있습니다 [새 TPM 초기 계획을 캡처한](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#capture-the-tpm-baseline-for-each-unique-class-of-hardware) 및 [HGS에 등록](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts)합니다.
TcgLogVerification         | TCG 로그 (TPM 기준)를 얻거나 확인할 수 없습니다. 이 호스트의 펌웨어, TPM 또는 다른 하드웨어 구성 요소를 사용 하 여 문제를 나타낼 수 있습니다. 호스트를 Windows 부팅 하기 전에 PXE 부팅을 시도 하도록 구성 하는 경우 오래 된 네트워크 부팅 프로그램 (NBP)에이 오류가 발생할 수 있습니다. PXE 부팅을 사용 하는 경우 모든 Nbp는 최신 상태를 확인 합니다.
VirtualSecureMode          | 호스트의 가상화 기반 보안 기능을 실행 하지 않습니다. VBS 사용 하도록 설정 하 고 시스템 구성 된 충족 [플랫폼 보안 기능](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#validate-enabled-device-guard-hardware-based-security-features)합니다. 참조 된 [Device Guard 설명서](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide) VBS 요구 사항에 대 한 자세한 내용은 합니다.
