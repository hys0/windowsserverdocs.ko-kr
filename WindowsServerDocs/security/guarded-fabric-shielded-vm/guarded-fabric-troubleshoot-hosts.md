---
title: 호스트 보호자 서비스 문제 해결
ms.prod: windows-server
ms.topic: article
ms.assetid: 80ea38f4-4de6-4f85-8188-33a63bb1cf81
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: 86627f6013592c95f517d77fed6ac5f57eb139b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856396"
---
# <a name="troubleshooting-guarded-hosts"></a>보호 된 호스트 문제 해결

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

이 항목에서는 보호 된 패브릭에서 보호 된 Hyper-v 호스트를 배포 하거나 작동할 때 발생 하는 일반적인 문제에 대 한 해결 방법을 설명 합니다.
문제의 특성을 잘 모를 경우 먼저 Hyper-v 호스트에서 [보호 된 패브릭 진단을](guarded-fabric-troubleshoot-diagnostics.md) 실행 하 여 잠재적인 원인을 좁혀 보세요.

## <a name="guarded-host-feature"></a>보호 된 호스트 기능

Hyper-v 호스트에 문제가 발생 하는 경우 먼저 **호스트 보호자 Hyper-v 지원** 기능이 설치 되어 있는지 확인 합니다.
이 기능이 없으면 Hyper-v 호스트에는 증명을 전달 하 고 보호 된 Vm을 프로 비전 할 수 있는 중요 한 구성 설정 및 소프트웨어가 누락 됩니다.

기능이 설치 되어 있는지 확인 하려면 서버 관리자를 사용 하거나 관리자 권한 PowerShell 창에서 다음 명령을 실행 합니다.

```powershell
Get-WindowsFeature HostGuardian
```

기능이 설치 되지 않은 경우 다음 PowerShell 명령을 사용 하 여 설치 합니다.

```powershell
Install-WindowsFeature HostGuardian -Restart
```

## <a name="attestation-failures"></a>증명 실패

호스트가 호스트 보호자 서비스와 증명을 전달 하지 않으면 보호 된 Vm을 실행할 수 없습니다.
해당 호스트에 대 한 [get-hgsclientconfiguration](https://technet.microsoft.com/library/dn914500.aspx) 의 출력에는 해당 호스트가 증명에 실패 한 이유에 대 한 정보가 표시 됩니다.

다음 표에서는 **AttestationStatus** 필드에 나타날 수 있는 값과 해당 하는 경우 가능한 다음 단계에 대해 설명 합니다.

AttestationStatus         | 설명
--------------------------|------------
만료됨                   | 호스트가 이전에 증명을 통과 했지만 발급 된 상태 인증서가 만료 되었습니다. 호스트 및 HGS 시간이 동기화 되었는지 확인 합니다.
InsecureHostConfiguration | 호스트가 HGS에 구성 된 증명 정책을 준수 하지 않아 증명을 통과 하지 못했습니다. 자세한 내용은 AttestationSubStatus 테이블을 참조 하세요.
NotConfigured             | 호스트가 증명 및 키 보호를 위해 HGS를 사용 하도록 구성 되어 있지 않습니다. 대신 로컬 모드로 구성 됩니다. 이 호스트가 보호 된 패브릭에 있는 경우 [get-hgsclientconfiguration](https://technet.microsoft.com/library/dn914494.aspx) 를 사용 하 여 HGS 서버에 대 한 url을 제공 합니다.
통과                    | 호스트가 증명을 통과 했습니다.
TransientError            | 네트워킹, 서비스 또는 기타 임시 오류로 인해 마지막 증명 시도가 실패 했습니다. 마지막 작업을 다시 시도 합니다.
TpmError                  | 호스트에서 TPM 오류로 인해 마지막 증명 시도를 완료할 수 없습니다. 자세한 내용은 TPM 로그를 참조 하십시오.
UnauthorizedHost          | 보호 된 Vm을 실행할 수 있는 권한이 없어 호스트가 증명을 통과 하지 못했습니다. 호스트가 보호 된 Vm을 실행 하기 위해 HGS에서 신뢰 하는 보안 그룹에 속하는지 확인 합니다.
알 수 없음                   | 호스트가 아직 HGS를 증명 하려고 시도 하지 않았습니다.

**AttestationStatus** 가 **Insecurehostconfiguration**으로 보고 되는 경우 하나 이상의 이유가 **AttestationSubStatus** 필드에 채워집니다.
아래 표에서는 AttestationSubStatus의 가능한 값과 문제를 해결 하는 방법에 대 한 팁을 설명 합니다.

AttestationSubStatus       | 무엇을 의미 하 고 수행할 수 있습니다.
---------------------------|-------------------------------
BitLocker                  | 호스트의 OS 볼륨이 BitLocker로 암호화 되지 않았습니다. 이 문제를 해결 하려면 OS 볼륨에서 [bitlocker를 사용 하도록 설정](https://technet.microsoft.com/itpro/windows/keep-secure/bitlocker-basic-deployment) 하거나 [HGS에서 bitlocker 정책을 사용 하지 않도록](guarded-fabric-manage-hgs.md#review-attestation-policies)설정 합니다.
CodeIntegrityPolicy        | 호스트가 코드 무결성 정책을 사용 하도록 구성 되어 있지 않거나 HGS 서버에서 신뢰 하는 정책을 사용 하 고 있지 않습니다. 코드 무결성 정책이 구성 되어 있고, 호스트가 다시 시작 되었으며, 정책이 HGS 서버에 등록 되어 있는지 확인 합니다. 자세한 내용은 [코드 무결성 정책 만들기 및 적용](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#create-and-apply-a-code-integrity-policy)을 참조 하세요.
DumpsEnabled               | 호스트가 크래시 덤프 또는 라이브 메모리 덤프를 허용 하도록 구성 되어 있으며,이는 HGS 정책에서 허용 되지 않습니다. 이 문제를 해결 하려면 호스트에서 덤프를 사용 하지 않도록 설정 합니다.
암호화 되지 않은 암호화             | 호스트는 크래시 덤프 또는 라이브 메모리 덤프를 허용 하도록 구성 되지만 이러한 덤프는 암호화 하지 않습니다. 호스트에서 덤프를 사용 하지 않도록 설정 하거나 [덤프 암호화를 구성](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)합니다.
DumpEncryptionKey          | 호스트가 덤프를 허용 하 고 암호화 하도록 구성 되었지만 HGS에 알려진 인증서를 사용 하 여 암호화 하지 않습니다. 이 문제를 해결 하려면 호스트에서 [덤프 암호화 키를 업데이트](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption) 하거나 [키를 HGS에 등록](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts)합니다.
FullBoot                   | 호스트가 절전 모드 또는 최대 절전 모드에서 다시 시작 되었습니다. 완전 한 전체 부팅이 가능 하도록 호스트를 다시 시작 합니다.
HibernationEnabled         | 호스트는 최대 절전 모드 파일을 암호화 하지 않고 최대 절전 모드를 허용 하도록 구성 되어 있으며,이는 HGS 정책에서 허용 되지 않습니다. 최대 절전 모드를 해제 하 고 호스트를 다시 시작 하거나 [덤프 암호화를 구성](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)합니다.
HypervisorEnforcedCodeIntegrityPolicy | 호스트가 하이퍼바이저 적용 코드 무결성 정책을 사용 하도록 구성 되어 있지 않습니다. 하이퍼바이저에서 코드 무결성을 사용 하도록 설정 하 고 구성 하 고 적용 했는지 확인 합니다. 자세한 내용은 [Device Guard 배포 가이드](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies) 를 참조 하세요.
없거나                      | 호스트의 가상화 기반 보안 기능은 HGS 정책에서 요구 하는 대로 직접 메모리 액세스 공격 으로부터 보호 하기 위해 IOMMU 장치를 요구 하도록 구성 되어 있지 않습니다. 호스트에 IOMMU가 있는지 확인 하 고, 사용 하도록 설정 되어 있으며, 장치 가드가 VBS를 시작할 때 [DMA 보호를 요구 하도록 구성](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#enable-virtualization-based-security-vbs-and-device-guard) 되어 있는지 확인 합니다.
PagefileEncryption         | 호스트에서 페이지 파일 암호화를 사용할 수 없습니다. 이 문제를 해결 하려면 `fsutil behavior set encryptpagingfile 1`를 실행 하 여 페이지 파일 암호화를 사용 하도록 설정 합니다. 자세한 내용은 [fsutil behavior](https://technet.microsoft.com/library/cc785435.aspx)를 참조 하세요.
SecureBoot                 | 보안 부팅이이 호스트에서 사용 하도록 설정 되지 않았거나 Microsoft 보안 부팅 템플릿을 사용 하지 않습니다. Microsoft 보안 부팅 템플릿을 사용 하 여 [보안 부팅을 사용 하도록 설정](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/disabling-secure-boot#enable_secure_boot) 하면이 문제를 해결할 수 있습니다.
SecureBootSettings         | 이 호스트의 TPM 기준이 HGS에서 신뢰 하는 기준과 일치 하지 않습니다. 새 하드웨어나 소프트웨어를 설치 하 여 UEFI 시작 기관, .DBX 변수, 디버그 플래그 또는 사용자 지정 보안 부팅 정책을 변경 하는 경우 발생할 수 있습니다. 이 컴퓨터의 현재 하드웨어, 펌웨어 및 소프트웨어 구성을 신뢰 하는 경우 [새 TPM 기준선을 캡처하고](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#capture-the-tpm-baseline-for-each-unique-class-of-hardware) [HGS에 등록할](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts)수 있습니다.
TcgLogVerification         | TCG 로그 (TPM 기준)를 얻거나 확인할 수 없습니다. 이는 호스트의 펌웨어, TPM 또는 기타 하드웨어 구성 요소에 문제가 있음을 나타낼 수 있습니다. Windows를 부팅 하기 전에 PXE 부팅을 시도 하도록 호스트를 구성한 경우 오래 된 NBP (네트워크 부팅 프로그램) 에서도이 오류가 발생할 수 있습니다. PXE 부팅을 사용 하는 경우 모든 NBPs가 최신 상태 인지 확인 합니다.
VirtualSecureMode          | 가상화 기반 보안 기능이 호스트에서 실행 되 고 있지 않습니다. VBS를 사용 하도록 설정 하 고 시스템이 구성 된 [플랫폼 보안 기능](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#validate-enabled-device-guard-hardware-based-security-features)을 충족 하는지 확인 합니다. VBS 요구 사항에 대 한 자세한 내용은 [Device Guard 설명서](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide) 를 참조 하세요.

## <a name="modern-tls"></a>최신 TLS

그룹 정책을 배포 하거나 TLS 1.0을 사용 하지 못하도록 Hyper-v 호스트를 구성 하는 경우 보호 된 VM을 시작 하려고 할 때 "호스트 보호자 서비스 클라이언트가 호출 프로세스를 대신 하 여 키 보호기의 래핑을 해제 하지 못했습니다." 오류가 발생할 수 있습니다.
이는 지원 되는 TLS 버전을 HGS 서버와 협상할 때 시스템 기본 TLS 버전이 고려 되지 않는 .NET 4.6의 기본 동작 때문입니다.

이 동작을 해결 하려면 다음의 두 명령을 실행 하 여 .NET 앱에 대 한 시스템 기본 TLS 버전을 사용 하도록 .NET을 구성 합니다.

```cmd
reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SystemDefaultTlsVersions /t REG_DWORD /d 1 /f /reg:64
reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SystemDefaultTlsVersions /t REG_DWORD /d 1 /f /reg:32
```

> [!WARNING]
> 시스템 기본 TLS 버전 설정은 컴퓨터의 모든 .NET 앱에 영향을 줍니다. 프로덕션 컴퓨터에 배포 하기 전에 격리 된 환경에서 레지스트리 키를 테스트 해야 합니다.

.NET 4.6 및 TLS 1.0에 대 한 자세한 내용은 [tls 1.0 문제 해결, 두 번째 버전](https://docs.microsoft.com/security/solving-tls1-problem)을 참조 하세요.
