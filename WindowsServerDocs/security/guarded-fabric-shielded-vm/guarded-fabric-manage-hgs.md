---
title: 호스트 보호 서비스 관리
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: eecb002e-6ae5-4075-9a83-2bbcee2a891c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: dab27e71e42970507f321271edda90f6d161c691
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447397"
---
# <a name="managing-the-host-guardian-service"></a>호스트 보호 서비스 관리

> 적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

(HGS (호스트 보호 서비스)는 보호 된 패브릭 솔루션의 핵심입니다.
패브릭에서 Hyper-v 호스트 정상 호스팅 서비스 공급자 또는 엔터프라이즈 인지 확인 하 고 신뢰할 수 있는 소프트웨어를 실행 하 고 보호 된 Vm을 시작 하는 데 키를 관리 하기 위한 것입니다.
테 넌 트를 신뢰 하는 보호 된 Vm을 호스트 하 하기로 하는 경우 사용자의 구성과 호스트 보호자 서비스의 관리를 신뢰 하도록 배치할 수 있습니다.
따라서 보안, 가용성 및 보호 된 패브릭의 안정성을 보장 하는 호스트 보호자 서비스를 관리할 때 모범 사례를 따라야 하는 것이 반드시 합니다.
다음 섹션의 지침에는 HGS 관리자를 연결 하는 가장 일반적인 작동 문제를 해결 합니다.

## <a name="limiting-admin-access-to-hgs"></a>HGS에 대 한 관리자 액세스를 제한합니다.
가 특성으로 인해 보안 중요 한 HGS 해당 관리자가 조직의 신뢰할 수 있는 멤버를, 이상적으로 패브릭 리소스 관리자에서 분리를 확인 해야 합니다.
또한 HTTPS 통한 WinRM 등의 보안 통신 프로토콜을 사용 하 여 보안 워크스테이션에서 HGS만 관리 하는 것이 좋습니다.

### <a name="separation-of-duties"></a>의무 분리
HGS를 설정할 때 HGS에 대해서만 또는 HGS 기존, 신뢰할 수 있는 도메인에 가입 하려면 분리 된 Active Directory 포리스트를 만들기 위한 옵션도 제공 됩니다.
조직에서 관리자를 할당 하는 역할 뿐만 아니라이 의사 결정을 HGS에 대 한 신뢰 경계를 결정 합니다.
관리자로 서 직접 또는 간접적으로 HGS에서 영향을 줄 수 있는 다른 작업 (예: Active Directory)의 관리자로 서 HGS에 대 한 액세스를의 모든 사용자의 보호 된 패브릭에 대 한 제어 합니다.
HGS 관리자는 보호 된 Vm을 실행 하 고 보호 된 Vm을 시작 하는 데 필요한 인증서를 관리 권한이 있는 Hyper-v 호스트를 선택 합니다.
공격자 나 악의적인 관리자 HGS에 대 한 액세스 권한이 있는 사용자 손상 된 호스트를 보호 된 Vm 실행 키 자료 등을 제거 하 여 서비스 거부 공격을 시작할 권한을 부여 하려면이 power를 사용할 수 있습니다.

이러한 위험을 방지 하려면 *강력한* (HGS 가입 되어 있는 도메인 포함) HGS 관리자 간 중복을 제한 하는 것이 좋습니다. 및 Hyper-v 환경입니다.
두 시스템에 권한이 없는 한 관리자 함으로써 자신의 업무 HGS 정책을 변경 하는 데 2 개인의 2 다양 한 계정을 손상 해야 합니다.
이 문제는 또한 두 Active Directory 환경에 대 한 도메인 및 엔터프라이즈 관리자에는 동일한 사용자를 사용 해야 합니다. 또는 HGS를 사용 해야 동일한 Active Directory 포리스트에 Hyper-v 호스트를 의미 합니다.
보안 위험이 모든 사용자가 자체 자세한 리소스 액세스 권한을 부여할 수 있습니다.

### <a name="using-just-enough-administration"></a>Just Enough Administration을 사용 하 여
함께 제공 되는 HGS [Just Enough Administration](https://aka.ms/JEAdocs) (JEA) 역할을 더욱 안전 하 게 관리할 수 있도록 기본 제공 합니다.
HGS 정책을 관리 하는 사용자 실제로 전체 컴퓨터 또는 도메인 관리자가 아니어도 의미 하는 관리자가 아닌 사용자에 게 관리 작업을 위임할 수 있도록 하 여 JEA를 사용 하면 됩니다.
JEA는 사용자는 PowerShell 세션에서 실행할 수 있는 명령을 제한 되 고 백그라운드에서 고유한 각 사용자 세션에 대 한 임시 로컬 계정 사용 하 여 일반적으로 권한 상승 해야 하는 명령을 실행 하 여 작동 합니다.

HGS는 미리 구성 된 2 JEA 역할을 사용 하 여 제공 됩니다.
- **HGS 관리자** 보호 된 Vm을 실행 하려면 새 호스트를 권한 부여를 포함 하는 모든 HGS 정책을 관리 하려면 사용자 수 있습니다.
- **HGS 검토자** 만 있어 사용자가 기존 정책 감사 수 있는 권한입니다. HGS 구성에 변경 내용을 할 수 없습니다.

JEA를 사용 하려면 먼저 새 표준 사용자를 만들고 HGS 관리자 또는 HGS 검토자 그룹의 멤버인 있도록 해야 합니다.
사용 하는 경우 `Install-HgsServer` HGS에 대 한 새 포리스트를 설정 하려면 이러한 그룹 이름은 "*servicename*관리자" 및 "*servicename*검토자" 각각 여기서 *servicename*  HGS 클러스터의 네트워크 이름입니다.
에 지정 된 그룹 이름을 참조 해야 HGS를 기존 도메인에 가입 하는 경우 `Initialize-HgsServer`합니다.

**HGS 관리자 및 전문가 역할에 대 한 표준 사용자 만들기**

```powershell
$hgsServiceName = (Get-ClusterResource HgsClusterResource | Get-ClusterParameter DnsName).Value
$adminGroup = $hgsServiceName + "Administrators"
$reviewerGroup = $hgsServiceName + "Reviewers"

New-ADUser -Name 'hgsadmin01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Admin Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $adminGroup -Members 'hgsadmin01'

New-ADUser -Name 'hgsreviewer01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Reviewer Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $reviewerGroup -Members 'hgsreviewer01'
```

**검토자 역할을 사용 하 여 감사 정책**

HGS에 네트워크 연결 되어 있는 원격 컴퓨터에서 PowerShell 검토자 자격 증명을 사용 하 여 JEA 세션에서 다음 명령을 실행 합니다.
검토자 계정이 표준 사용자 뿐 이므로 사용할 수 없습니다 일반 Windows PowerShell 원격을 HGS 등의 원격 데스크톱 액세스에 대 한 두는 것이 반드시 합니다.

```powershell
Enter-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsreviewer01' -ConfigurationName 'microsoft.windows.hgs'
```

다음 명령을 사용 하 여 세션의 수를 확인할 수 있습니다 `Get-Command` 감사 구성에 허용 된 모든 명령을 실행 합니다.
에 아래 예제에서는 확인 HGS 정책을 사용할 수 있습니다.

```powershell
Get-Command

Get-HgsAttestationPolicy
```

명령을 입력 하 여 `Exit-PSSession` 또는 해당 별칭인 `exit`완료 되 면, JEA 세션을 사용 합니다. 

**HGS 관리자 역할을 사용 하 여 새 정책을 추가합니다**

정책을 실제로 변경 하려면 'hgsAdministrators' 그룹에 속하는 id 사용 하 여 JEA 끝점에 연결 해야 합니다.
에 아래 예제를 보여 줍니다 HGS 새 코드 무결성 정책을 복사할 JEA를 사용 하 여 등록 하는 방법입니다.
구문에 사용 되 다를 수 있습니다.
전체 파일 시스템에 액세스할 수 없는 경우 처럼 JEA에서 제한의 일부를 수용할 수 있도록 하기 위해서입니다.

```powershell
$cipolicy = Get-Item "C:\temp\cipolicy.p7b"
$session = New-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsadmin01' -ConfigurationName 'microsoft.windows.hgs'
Copy-Item -Path $cipolicy -Destination 'User:' -ToSession $session

# Now that the file is copied, we enter the interactive session to register it with HGS
Enter-PSSession -Session $session
Add-HgsAttestationCiPolicy -Name 'New CI Policy via JEA' -Path 'User:\cipolicy.p7b'

# Confirm it was added successfully
Get-HgsAttestationPolicy -PolicyType CiPolicy

# Finally, remove the PSSession since it is no longer needed
Exit-PSSession
Remove-PSSession -Session $session
```

## <a name="monitoring-hgs"></a>HGS를 모니터링합니다.
### <a name="event-sources-and-forwarding"></a>이벤트 원본 및 전달
HGS에서 이벤트에에서 표시 됩니다는 Windows 이벤트 로그 아래에 있는 두 소스:
- **HostGuardianService-Attestation**
- **HostGuardianService-KeyProtection**

이벤트 뷰어를 열고 Microsoft-Windows-HostGuardianService-증명 및 Microsoft Windows-HostGuardianService KeyProtection로 이동 하 여 이러한 이벤트를 볼 수 있습니다.

대규모 환경에서는 것이 좋습니다 이벤트 분석을 쉽게 수행할 수 있도록 중앙 Windows 이벤트 수집기에 이벤트를 전달 합니다.
자세한 내용은 체크 아웃 합니다 [설명서 Windows Event Forwarding](https://msdn.microsoft.com/library/windows/desktop/bb427443.aspx)합니다.

### <a name="using-system-center-operations-manager"></a>System Center Operations Manager를 사용 하 여
또한 System Center 2016-Operations Manager 모니터링 HGS 및 보호 된 호스트를 사용할 수 있습니다.
보호 된 패브릭 관리 팩에는 호스트 증명 및 오류 보고는 HGS 서버를 통과 하지 못한 것을 포함 하 여 데이터 센터 중단을 일으킬 수 있는 일반적인 구성 오류를 확인 하려면 이벤트 모니터입니다.

시작 하려면 [설치 및 구성 SCOM 2016](https://technet.microsoft.com/system-center-docs/om/welcome-to-operations-manager) 하 고 [보호 된 패브릭 관리 팩을 다운로드](https://www.microsoft.com/download/details.aspx?id=52764)합니다.
포함 된 관리 팩 가이드에는 구성 관리 팩의 모니터 범위를 파악 하는 방법을 설명 합니다.

## <a name="backing-up-and-restoring-hgs"></a>백업 및 복원 HGS
### <a name="disaster-recovery-planning"></a>재해 복구 계획
재해 복구 계획의 초안을 작성 하는 경우에 보호 된 패브릭에 호스트 보호자 서비스의 고유한 요구 사항을 고려해 야 합니다.
HGS 노드 중 일부나 전부를 잃어버린 경우, 사용자가 보호 된 Vm을 시작 하지 못하게 됩니다 하는 즉시 가용성 문제가 발생할 수 있습니다.
전체 HGS 클러스터를 잊은 경우 HGS 클러스터를 복원 하 고 일반 작업을 다시 시작 하려면 한편 HGS 구성의 전체 백업을 보유 해야 합니다.
이 섹션에서는 이러한 시나리오를 준비 하는 데 필요한 단계를 다룹니다.

먼저 HGS를 백업 하는 것이 중요 어떨까요을 이해 하는 것이 반드시 합니다.
HGS를 유지 하면서 여러 데 도움이 되는 정보의 부분 호스트 보호 된 Vm을 실행할 수를 결정 합니다.
다음을 포함합니다.
1. 포함 된 그룹에 대 한 active Directory 보안 식별자 (Active Directory 증명을 사용 하 여) 하는 경우 호스트를 신뢰할 수 있는
2. 사용자 환경에서 각 호스트에 대 한 고유 TPM 식별자
3. 호스트의 각 고유 구성에 대 한 TPM 정책 및
4. 호스트에서 실행 되도록 허용 되는 소프트웨어를 결정 하는 코드 무결성 정책입니다.

이러한 증명 아티팩트 잠재적으로 어려울 재해 후에 다시이 정보를 얻을 수를 가져오려면 호스팅 패브릭의 관리자와 조정을 해야 합니다.

또한 HGS는 2 개 이상의 인증서를 암호화 하 고 보호 된 VM (키 보호기)를 시작 하는 데 필요한 정보를 서명 하는 데 액세스를 해야 합니다.
이러한 인증서는 잘 알려진 (해당 Vm을 실행할 패브릭에 권한 부여 보호 된 Vm 소유자가 사용 함) 하 고 원활한 복구 환경을 재해 발생 후 복원 해야 합니다.
하면 복원 해서는 HGS에서 동일한 인증서를 사용 하 여 재해 발생 후, 각 VM 해당 정보를 해독 하 여 새 키 권한 부여를 업데이트 해야 합니다.
보안상의 이유로 VM 소유자만 이러한 새 키, 키를 다시 실행 하는 Vm을 가져오려고 조치를 취할 필요가 각 VM 소유자는 재해 발생 후 복원 의미 오류 권한을 부여 하는 VM 구성을 업데이트할 수 있습니다.

#### <a name="preparing-for-the-worst"></a>최악의 준비
완전히 손실 HGS 준비 하려면 가지 수행 해야 하는 2 단계
1. HGS 증명 정책을 백업합니다
2. HGS 키 백업

다음이 단계를 모두 수행 하는 방법에 대 한 지침이 제공 됩니다는 [HGS 백업](#backing-up-hgs) 섹션입니다.

또한 권장 되지만 없어도 해당 Active Directory 도메인에서 HGS 또는 Active Directory 자체를 관리할 권한이 있는 사용자 목록을를 백업 하는 것.

백업이 정보는 최신 상태이 고 변조 또는 도난 방지에 안전 하 게 저장 되도록 정기적으로 수행 해야 합니다.

것 **좋지** 를 백업 하거나 HGS 노드의 전체 시스템 이미지를 복원 하려고 합니다.
전체 클러스터를 분실 한 경우에 새로운 HGS 노드가 설정 및 전체 서버 OS 없습니다 HGS 상태만 복원 하는 것이 좋습니다.

#### <a name="recovering-from-the-loss-of-one-node"></a>하나의 노드가 손실 로부터 복구
HGS 클러스터에서 하나 이상의 노드 (하지만 모든 노드)를 분실 하면 단순히 [클러스터에 노드 추가](guarded-fabric-configure-additional-hgs-nodes.md) 배포 가이드의 지침에 따라 합니다.
제공 된 HGS를 PFX 파일로 암호와 함께 제공 되는 인증서로 증명 정책을 자동으로 동기화 됩니다.
인증서 지문을 사용 하 여 HGS에 추가 (내보낼 수 없는 및 하드웨어 인증서를 일반적으로 지원 되는), 각 새 노드에 각 인증서의 개인 키에 대 한 액세스를 확인 해야 합니다.

#### <a name="recovering-from-the-loss-of-the-entire-cluster"></a>전체 클러스터의 손실 로부터 복구
전체 HGS 클러스터 다운 하 고 다시 온라인 상태로 만들 수 없는 경우에 HGS 백업에서 복원 해야 합니다.
첫 번째 설정 당 새 HGS 클러스터는 HGS 백업에서 복원 합니다 [배포 가이드의 지침에](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)입니다.
이 좋지만 하지 않아도, 호스트에서 이름 확인을 지원 하기 위해 복구 HGS 환경을 설정 하는 경우 동일한 클러스터 이름을 사용 합니다.
동일한 이름을 사용 하 여 새 증명 및 키 보호 Url을 사용 하 여 호스트를 다시 구성 하지 않아도 됩니다.
HGS를 지 원하는 Active Directory 도메인에 개체를 복원한 경우 HGS 서버를 초기화 하기 전에 HGS 클러스터, 컴퓨터, 서비스 계정 및 JEA 그룹을 나타내는 개체를 제거 하는 것이 좋습니다.

첫 번째 HGS 노드 설정 (예:이 설치 되어 초기화), 아래의 절차를 수행 합니다 [백업에서 복원 HGS](#restoring-hgs-from-a-backup) 증명 정책 및 키 보호 공용 절반을 복원 하려면 인증서입니다.
인증서 공급자의 지침에 따라 수동으로 인증서에 대 한 개인 키를 복원 해야 합니다 (예: Windows에서 인증서를 가져올 또는 HSM 기반 인증서에 대 한 액세스를 구성).
첫 번째 노드를 설정한 후 계속 수 있습니다 [클러스터에 추가 노드 설치할](guarded-fabric-configure-additional-hgs-nodes.md) 까지 용량 및 원하는 복원 력에 도달 했습니다.

### <a name="backing-up-hgs"></a>HGS 백업
HGS 관리자 HGS를 정기적으로 백업 하는 일을 담당 해야 합니다.
전체 백업을 적절 하 게 보호 해야 하는 중요 한 키 자료를 포함 합니다.
신뢰할 수 없는 엔터티를 얻어 이러한 키에 대 한 액세스를 손상 시 키 지 목적으로 악성 HGS 환경을 설정 하는 자료는 보호 된 Vm를 사용할 수 있습니다.

**증명 정책을 백업** 다시 HGS 증명 정책 모든 작업 HGS 서버 노드에서 다음 명령을 실행 합니다.
암호를 입력 하 라는 메시지가 표시 됩니다.
이 암호 암호화 인증서 (인증서 지문) 대신 PFX 파일을 사용 하 여 HGS에 추가 됩니다.

```powershell
Export-HgsServerState -Path C:\temp\HGSBackup.xml
```

> [!NOTE]
> 관리자-신뢰할 수 있는 증명을 사용 하는 경우 별도로 HGS에서 보호 된 호스트를 권한 부여를 사용 하는 보안 그룹의 멤버를 백업 해야 합니다.
> HGS는 보안 그룹의 SID 하지 내에서 멤버 자격만 백업 합니다.
> 이러한 그룹은 재해 발생 시 손실, 이벤트 그룹을 다시 만들고 각 보호 된 호스트를 다시 추가 해야 합니다.

**인증서를 백업**

`Export-HgsServerState` PFX 기반 인증서 시 HGS에 추가 명령이 실행 되 고를 백업 하는 명령입니다.
HGS에 인증서를 추가 하는 경우 지문 (인증서를 내보낼 수 없는 및 하드웨어 지원에 대 한 일반)을 사용 하 여 해야 수동으로 인증서에 대 한 개인 키를 백업 합니다.
를 식별 하기 위해 인증서를 HGS에 등록 하 고 수동으로 백업 해야 모든 작업 HGS 서버 노드에서 다음 PowerShell 명령을 실행 합니다.

```powershell
Get-HgsKeyProtectionCertificate | Where-Object { $_.CertificateData.GetType().Name -eq 'CertificateReference' } | Format-Table Thumbprint, @{ Label = 'Subject'; Expression = { $_.CertificateData.Certificate.Subject } }
```

각 나열 된 인증서의 개인 키를 수동으로 백업 해야 합니다.
내보낼 수 있는 소프트웨어를 기반으로 인증서를 사용 하는 경우 이러한 인증서를 백업 및/또는 다시 실행 하십시오 주문형 수 있도록 인증 기관에 문의 해야 합니다.
만들고 하드웨어 보안 모듈에 저장 된 인증서에 대 한 재해 복구 계획에 대 한 지침에 대 한 장치에 대 한 설명서를 참조 하십시오.

두 부분을 함께 복원할 수 있도록 안전한 위치에 증명 정책 백업을 함께 인증서 백업을 저장 해야 합니다.

**백업에서 추가 구성**

백업 된 HGS 구성 서버 상태 정보 Active Directory에서 HGS 클러스터의 이름을 포함 되지 것입니다 또는 SSL 인증서 HGS Api를 사용 하 여 통신을 보호 하는 데 사용 합니다.
이러한 설정은 일관성을 위해 중요 하지만 재해 발생 후 다시 온라인 HGS 클러스터를 가져오려는 중요 하지 않습니다.

HGS 서비스의 이름을 캡처할 실행 `Get-HgsServer` 증명 및 키 보호 Url 플랫 이름을 확인 합니다.
예를 들어 증명 URL "<http://hgs.contoso.com/Attestation>", "hgs" HGS 서비스 이름입니다.

HGS에서 사용 하는 Active Directory 도메인은 다른 Active Directory 도메인과 같은 관리 되어야 합니다.
재해 발생 후 HGS를 복원할 때 없습니다 반드시 해야 현재 도메인에 있는 개체를 다시 만듭니다.
그러나이 경우 더 쉬워집니다 복구를 Active Directory를 백업 하 고 시스템 뿐만 아니라 관리자 신뢰할 수 있는 증명 하는 보호 된 호스트에 권한을 부여 하는 데 사용 된 보안 그룹의 멤버 자격을 관리할 수 있는 권한이 JEA 사용자의 목록을 유지 합니다.

HGS에 대해 구성 된 SSL 인증서의 지문을 식별 하려면 PowerShell에서 다음 명령을 실행 합니다.
그런 다음 인증서 공급자의 지침에 따라 해당 SSL 인증서를 백업할 수 있습니다.

```powershell
Get-WebBinding -Protocol https | Select-Object certificateHash
```

### <a name="restoring-hgs-from-a-backup"></a>HGS는 백업에서 복원
다음 단계를 HGS 설정을 백업에서 복원 하는 방법에 설명 합니다.
단계를 이미 실행 중인 HGS 인스턴스에 및 프로그램 이전과 완전히 손실 후 새로운 HGS 클러스터를 준비 하는 경우 변경한 내용을 실행 취소 하려는 경우 모두에 적용 됩니다.

#### <a name="set-up-a-replacement-hgs-cluster"></a>대체 HGS 클러스터 설정
HGS를 복원 하기 전에 초기화 HGS 클러스터가를 구성을 복원할 수 해야 합니다.
단순히 기존 (실행) 클러스터에 실수로 삭제 된 설정을 가져오려는 경우이 단계를 건너뛸 수 있습니다.
설치 하 여 하나 이상의 HGS 노드 다음에 초기화 해야 HGS 완전히 손실에서 복구 하는 경우는 [배포 가이드의 지침에](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)입니다.

특히를 해야 합니다.
1. [HGS 도메인 설정](guarded-fabric-choose-where-to-install-hgs.md) HGS 기존 도메인에 가입 하거나
2. [HGS 서버를 초기화할](guarded-fabric-initialize-hgs.md) 기존 키를 사용 하 여 *또는* 임시 키의 집합입니다. 할 수 있습니다 [임시 키를 제거](#renewing-or-replacing-keys) HGS에서 실제 키를 가져온 후 파일을 백업 합니다.
3. [HGS 설정 가져오기](#import-settings-from-a-backup) 신뢰할 수 있는 호스트 그룹, 코드 무결성 정책, TPM 기준 및 TPM 식별자를 복원 하려면 백업에서

> [!TIP]
> 새 HGS 클러스터는 동일한 인증서를 서비스 이름 또는 도메인을 사용 하 여 백업 파일을 내보낸 HGS 인스턴스로 필요가 없습니다.

#### <a name="import-settings-from-a-backup"></a>백업에서 설정을 가져오려면

증명을 복원 하려면 정책, 인증서 PFX 기반 및 백업 파일에서 HGS 노드로 비 PFX 인증서의 공개 키를 초기화 HGS 서버 노드에서 다음 명령을 실행 합니다.
백업을 만들 때 지정한 암호를 입력 하 라는 메시지가 표시 됩니다.

```powershell
Import-HgsServerState -Path C:\Temp\HGSBackup.xml
```

관리자-신뢰할 수 있는 증명 정책 또는 TPM 신뢰할 수 있는 증명 정책을 가져올 하려는 경우 있습니다 이렇게 지정 하는 `-ImportActiveDirectoryModeState` 또는 `-ImportTpmModeState` 하는 플래그 [가져오기 HgsServerState](https://technet.microsoft.com/library/mt652168.aspx).

실행 하기 전에 Windows Server 2016이 설치에 대 한 최신 누적 업데이트를 확인 `Import-HgsServerState`합니다.
이렇게 하지 않으면 가져오기 오류가 발생할 수 있습니다.

> [!NOTE]
> 설치 된 이러한 정책 중 하나 이상을 이미 있는 기존 HGS 노드에 대 한 정책을 복원 하는 경우 import 명령을 각 중복 된 정책에 대 한 오류가 표시 됩니다.
> 이 정상적인된 동작 및 대부분의 경우에서 안전 하 게 무시할 수 있습니다.

#### <a name="reinstall-private-keys-for-certificates"></a>인증서에 대 한 개인 키를 다시 설치
백업을 만든 HGS에서 사용 되는 인증서를 추가한 경우 지문을 사용 하 여 백업 파일에 해당 인증서의 공개 키만 포함 됩니다.
즉, 수동으로 설치 및/또는 HGS Hyper-v 호스트의 요청을 처리할 수 있습니다 각 해당 인증서의 개인 키에 대 한 액세스를 부여 해야 합니다.
해당 단계를 완료 하는 데 필요한 작업을 원래 인증서를 발행 하는 방법에 따라 달라 집니다.
소프트웨어 기반 인증서의 인증 기관에서 발급 한 경우 개인 키를 가져오고에 설치 하 여 CA에 게 문의 해야 합니다 **각** 해당 지침 당 HGS 노드.
마찬가지로, 인증서가 하드웨어 기반의 HSM을 연결 하 고 개인 키에 대 한 각 컴퓨터 액세스 권한을 부여 하려면 각 HGS 노드에 필요한 드라이버를 설치 하려면 하드웨어 보안 모듈 공급 업체의 설명서를 참조 해야 합니다.

참고로, 인증서 지문을 사용 하 여 HGS에 추가할 각 노드에 개인 키의 수동 복제 기능이 필요 합니다.
복원 된 HGS 클러스터를 추가한 각 추가 노드에 대해이 단계를 반복 해야 합니다.

#### <a name="review-imported-attestation-policies"></a>가져온된 증명 정책을 검토합니다
가져온 후 설정을 백업에서 것이 좋습니다 밀접 하 게 모두 사용 하 여 가져온된 정책 검토 `Get-HgsAttestationPolicy` 신뢰 보호 된 Vm을 실행 하는 호스트에만 성공적으로 증명할 수 있도록 합니다.
수 더 이상 보안 태세를 일치 하는 모든 정책이 있다면 [사용 하지 않도록 설정 하거나 제거](#review-attestation-policies)합니다.

#### <a name="run-diagnostics-to-check-system-state"></a>시스템 상태를 확인 하려면 진단 실행
설정 하 고 복원 HGS 노드의 상태를 완료 한 후에 시스템의 상태를 확인 하려면 HGS 진단 도구를 실행 해야 합니다.
이렇게 하려면 다음 명령을 실행 HGS 노드에서 구성을 복원 하는 위치:

```powershell
Get-HgsTrace -RunDiagnostics
```

"결과적" 없습니다 "Pass" 이면 시스템 구성을 완료 하려면 추가 단계가 필요 합니다.
자세한 내용은 실패 한 subtest(s)에서 보고 한 메시지를 확인 합니다.

## <a name="patching-hgs"></a>HGS 패치
호스트 보호자 서비스 노드를 확인 하는 경우 최신 누적 업데이트를 설치 하 여 최신 상태로 유지 하는 것이 반드시 합니다. 새로운 HGS 노드를 설정 하는 경우에 HGS 역할을 설치 또는 구성 하기 전에 사용 가능한 업데이트를 설치 하는 것이 좋습니다.
이렇게 하면 모든 새로운 또는 변경 된 기능 즉시 적용 됩니다.

보호 된 패브릭에 패치 하는 경우 것이 좋습니다는 처음 업그레이드할 *모든* Hyper-v 호스트 **HGS를 업그레이드 하기 전에**입니다.
HGS에서 증명 정책을 모든 변경 내용이 있는지 확인 하는 것이 *후* Hyper-v 호스트에 필요한 정보를 제공 하도록 업데이트 되었습니다.
업데이트 정책의 동작을 변경 하려는 경우 이러한가 자동으로 사용할 수 없습니다 패브릭에 중단 되지 않게 하려면.
이러한 업데이트는 새롭거나 변경 된 증명 정책을 활성화 하려면 다음 섹션의 지침에 따르는지 필요 합니다.
Windows Server 및 정책 업데이트를 필요한 경우 확인에 설치한 모든 누적 업데이트에 대 한 릴리스 정보를 읽을 수는 것이 좋습니다.

### <a name="updates-requiring-policy-activation"></a>정책 정품 인증을 요구 하는 업데이트
HGS에 대 한 업데이트 소개 또는 크게 증명 정책의 동작을 변경 하는 경우 변경된 된 정책을 활성화 하는 추가 단계가 필요 합니다.
정책 변경 내용은 내보내고 HGS 상태를 가져온 후만 시행 됩니다.
환경의 모든 호스트를 HGS 노드 모든 누적 업데이트를 적용 한 후에 새롭거나 변경 된 정책을 활성화 해야 합니다.
모든 컴퓨터를 업데이트 하면 업그레이드 프로세스를 트리거할 수 있는 HGS 노드에서 다음 명령을 실행 합니다.

```powershell
$password = Read-Host -AsSecureString -Prompt "Enter a temporary password"
Export-HgsServerState -Path .\temporaryExport.xml -Password $password
Import-HgsServerState -Path .\temporaryExport.xml -Password $password
```

새 정책을 도입을 기본적으로 비활성화 됩니다.
새 정책이 사용 하려면 먼저 Microsoft 정책 ('HGS_' 접두사로) 목록에서 찾습니다 하 고 다음 명령을 사용 하 여 사용 하도록 설정:

```powershell
Get-HgsAttestationPolicy

Enable-HgsAttestationPolicy -Name <Hgs_NewPolicyName>
```

## <a name="managing-attestation-policies"></a>증명 정책 관리
HGS는 호스트는 "정상" 것으로 간주 되어 보호 된 Vm을 실행 하도록 허용 하기 위해 충족 해야 하는 요구 사항의 최소 집합을 정의 하는 몇 가지 증명 정책을 유지 합니다.
Microsoft에서 정의 된 이러한 정책 중 일부를 다른 환경에서 허용 되는 코드 무결성 정책, TPM 기준 및 호스트를 정의 하 여 추가 됩니다.
이러한 정책의 정기적인 유지 관리는 호스트 계속 될 수 있습니다 증명 제대로 업데이트 및 교체 하 고 성공적으로 증명에서 모든 신뢰할 수 없는 호스트 또는 구성 되도록 차단 되도록 해야 합니다.

관리자-신뢰할 수 있는 증명에는 호스트를 정상 인지 여부를 결정 하는 하나의 정책만: 알려진, 신뢰할 수 있는 보안 그룹 멤버 자격.
TPM 증명 더 복잡 하 고 정상 인지 결정 하기 전에 시스템의 구성을 확인 하 고 코드를 측정 하는 다양 한 정책을 포함 합니다.

Active Directory와 TPM 정책을 사용 하 여 한 번에 하나의 HGS를 구성할 수 있지만 서비스에서는 호스트 증명 시도 하는 경우에 대해 구성 된 현재 모드에 대 한 정책을 확인 합니다.
HGS 서버 모드를 확인 하려면 실행 `Get-HgsServer`합니다.

### <a name="default-policies"></a>기본 정책
신뢰할 수 있는 TPM 증명에 대 한 몇 가지 기본 제공 정책을 HGS에 구성 되어 있습니다.
이러한 일부 정책을 "고정"-보안상의 이유로 비활성화할 없습니다 것을 의미 합니다.
아래 표에서 각 기본 정책의 용도 설명 합니다.

정책 이름                    | 용도
-------------------------------|-----------------------------------------------------
Hgs_SecureBootEnabled          | 보안 부팅이 사용 하도록 호스트에 필요 합니다. 이것이 시작 이진 파일 및 기타 UEFI 잠긴 설정을 측정 하는 데 필요한입니다.
Hgs_UefiDebugDisabled          | 호스트에 커널 디버거가 사용할 수 없는 것을 확인 합니다. 사용자 모드 디버거는 코드 무결성 정책을 사용 하 여 차단 됩니다.
Hgs_SecureBootSettings         | 음수 정책을 호스트 (관리자가 정의한) TPM 기준을 하나 이상 일치 합니다.
Hgs_CiPolicy                   | 호스트 되도록 음수 정책 관리자가 정의한 CI 정책 중 하나를 사용 합니다.
Hgs_HypervisorEnforcedCiPolicy | 하이퍼바이저에 의해 적용 될 코드 무결성 정책에 필요 합니다. 커널 모드 코드 무결성 정책 공격 하 여 보호를 해지고이 정책을 사용 하지 않도록 설정 합니다.
Hgs_FullBoot                   | 호스트 절전 또는 최대 절전 모드에서 다시 시작 되지 않은 확인 합니다. 호스트를 올바르게 다시 시작 되거나이 정책을 전달 하려면 종료 수 해야 합니다.
Hgs_VsmIdkPresent              | 호스트에서 실행 되 고 가상화 기반 보안에 필요 합니다. IDK 호스트의 보안 메모리 공간에 다시 전송 하는 정보를 암호화 하는 데 필요한 키를 나타냅니다.
Hgs_PageFileEncryptionEnabled  | 호스트에서 암호화할 사용량과 필요 합니다. 이 정책을 사용 하지 않으면 테 넌 트 암호는 암호화 되지 않은 페이지 파일이 검사 하는 경우 정보 노출 될 수 있습니다.
Hgs_BitLockerEnabled           | BitLocker가 Hyper-v 호스트에서 사용 하도록 설정 하려면 필요 합니다. 이 정책은 성능상의 이유로 기본적으로 비활성화 되 고 사용 하도록 권장 되지 않습니다. 이 정책은 보호 된 Vm 자체의 암호화에 관계가 없습니다.
Hgs_IommuEnabled               | 있어야 호스트 IOMMU 장치를 직접 메모리 액세스 공격을 방지 하는 데 사용에서 합니다. 이 정책을 사용 하지 않도록 설정 하 고 호스트를 사용 하 여 사용 하도록 설정 하는 IOMMU 없이 메모리 공격을 보내기 위해 테 넌 트 VM 암호를 노출할 수 있습니다.
Hgs_NoHibernation              | Hyper-v 호스트에서 사용 하지 않도록 설정할 최대 절전 모드에 필요 합니다. 이 정책을 사용 하지 않으면 보호 된 VM 메모리 암호화 되지 않은 최대 절전 모드 파일을 저장 하는 호스트를 허용할 수 있습니다.
Hgs_NoDumps                    | Hyper-v 호스트에서 사용할 수 없게 하려면 메모리 덤프에 필요 합니다. 이 정책을 사용 하는 경우 보호 된 VM 메모리 암호화 되지 않은 크래시 덤프 파일에 저장 되지 않도록 방지 하기 위해 덤프 암호화를 구성 하는 것이 좋습니다.
Hgs_DumpEncryption             | HGS에서 신뢰할 수 있는 암호화 키로 암호화 될 Hyper-v 호스트에서 사용 하도록 설정 하는 경우 메모리 덤프를 해야 합니다. 덤프는 호스트에서 사용할 수 없는 경우에이 정책이 적용 되지 않습니다. 하는 경우이 정책 및 *Hgs\_NoDumps* 모두 비활성화 되어 보호 된 VM 메모리 암호화 되지 않은 덤프 파일을 저장할 수 없습니다.
Hgs_DumpEncryptionKey          | 덤프는 HGS 알고 있는 관리자가 정의한 덤프 파일 암호화 키를 사용 하 여 메모리를 허용 하도록 구성 된 호스트 되도록 음수 정책입니다. 이 정책이 적용 되지 않습니다 *Hgs\_DumpEncryption* 을 사용할 수 없습니다.

### <a name="authorizing-new-guarded-hosts"></a>보호 된 호스트를 새 권한 부여
보호 된 호스트 될 새 호스트에 권한을 부여 하려면 (예: 증명할 성공적으로), HGS에서 호스트를 신뢰 해야 합니다 (TPM 신뢰할 수 있는 증명을 사용 하도록 구성) 하는 경우 및 소프트웨어가 실행 되 고 합니다.
새 호스트에 권한을 부여 하는 단계는 HGS이 현재 구성 된 증명 모드에 따라 다릅니다.
보호 된 패브릭에 대 한 증명 모드를 확인 하려면 실행 `Get-HgsServer` HGS 노드에 있습니다.

#### <a name="software-configuration"></a>소프트웨어 구성
새 Hyper-v 호스트에는 Windows Server 2016 Datacenter edition이 설치를 확인 합니다.
Windows Server 2016 Standard는 보호 된 패브릭에서 보호 된 Vm을 실행할 수 없습니다.
설치 된 데스크톱 경험 또는 Server Core 호스트일 수 있습니다.

데스크톱 환경 포함 서버 및 Server Core에서는 Hyper-v 및 호스트 보호 Hyper-v 지원 서버 역할을 설치 해야 합니다.

```powershell
Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
```

#### <a name="admin-trusted-attestation"></a>관리자-신뢰할 수 있는 증명
에 등록 하려면 새 호스트를 HGS 관리자 신뢰할 수 있는 증명을 사용 하는 경우 먼저 가입 된 도메인에서 보안 그룹에 호스트를 추가 해야 합니다.
일반적으로 각 도메인 보호 된 호스트에 대 한 하나 이상의 보안 그룹이 해야 합니다.
이미 해당 그룹 HGS를 사용 하 여 등록, 작업만 수행 해야 경우 해당 그룹 멤버 자격을 새로 고치려면 호스트를 다시 시작 합니다.

어떤 보안 그룹이 다음 명령을 실행 하 여 HGS에서 신뢰할 수를 확인할 수 있습니다.

```powershell
Get-HgsAttestationHostGroup
```

새 보안 그룹을 HGS에 등록 하려면 먼저 호스트의 도메인에 있는 그룹의 보안 식별자 (SID) 캡처하고 SID를 HGS에 등록 합니다.

```powershell
Add-HgsAttestationHostGroup -Name "Contoso Guarded Hosts" -Identifier "S-1-5-21-3623811015-3361044348-30300820-1013"
```

HGS 고 호스트 도메인 간의 트러스트를 설정 하는 방법에 대 한 지침 배포 가이드에서 사용할 수 있습니다.

#### <a name="tpm-trusted-attestation"></a>TPM 신뢰할 수 있는 증명
HGS가 TPM 모드로 구성 되 면 호스트는 잠긴 모든 정책과 접두사로 "Hgs_" 뿐만 아니라 하나 이상의 TPM 기준, TPM 식별자 및 코드 무결성 정책을 사용 하는 "enabled" 정책을 전달 해야 합니다.
새 호스트를 추가할 때마다 새 TPM 식별자를 HGS에 등록 해야 합니다.
으로 호스트는 동일한 소프트웨어를 실행 하는 (및 동일한 코드 무결성 정책 적용) 환경에서 다른 호스트로 TPM 기준 하지 해야 새 CI 정책 또는 기준을 추가 합니다.

**새 호스트의 TPM 식별자 추가** 새 호스트의 TPM 식별자를 캡처하려면 다음 명령을 실행 합니다.
HGS에서 조회 하는 데 도움이 되는 호스트에 대 한 고유한 이름을 지정 해야 합니다.
HGS에서 보호 된 Vm을 실행 하지 못하도록 하려면 호스트를 서비스 해제 하는 경우이 정보가 필요 합니다.

```powershell
(Get-PlatformIdentifier -Name "Host01").InnerXml | Out-File C:\temp\host01.xml -Encoding UTF8
```

HGS 서버에 호스트를 HGS에 등록 하려면 다음 명령을 실행 한 다음이 파일을 복사 합니다.

```powershell
Add-HgsAttestationTpmHost -Name 'Host01' -Path C:\temp\host01.xml
```

**새 TPM 기준을 추가** 새 TPM 기준을 사용 해야 새로운 하드웨어 또는 펌웨어 구성이 환경에 대 한 새 호스트로 실행 중인 경우.
이렇게 하려면 호스트에서 다음 명령을 실행 합니다.

```powershell
Get-HgsAttestationBaselinePolicy -Path 'C:\temp\hardwareConfig01.tcglog'
```

> [!NOTE]
> 호스트 유효성 검사에 실패 하 고는 성공적으로 입증 되었다는 오류가 표시를 하는 경우 걱정 하지 마십시오.
> 보호 된 Vm, 호스트에서 실행할 수 있도록 하는 필수 구성 요소 검사 이며 가능성이 없습니다 아직 적용 코드 무결성 정책 또는 설정 하는 데 필요한 다른 것을 의미 합니다.
> 오류 메시지를 읽을 하 한을 제안 하는 변경 후 다시 시도 합니다.
> 또는 추가 하 여이 시간에 유효성 검사를 건너뛸 수 있습니다는 `-SkipValidation` 명령에 대 한 플래그입니다.

TPM 기본 HGS 서버에 복사한 다음 명령을 사용 하 여 등록 합니다.
Hyper-v 호스트의이 클래스의 하드웨어 및 펌웨어 구성을 이해 하도록 도와주는 명명 규칙을 사용 하는 것이 좋습니다.

```powershell
Add-HgsAttestationTpmPolicy -Name 'HardwareConfig01' -Path 'C:\temp\hardwareConfig01.tcglog'
```

**새 코드 무결성 정책 추가** 해당 호스트 성공적으로 증명할 수 전에 HGS를 사용 하 여 새 정책을 등록 해야 Hyper-v 호스트에서 실행 되는 코드 무결성 정책으로 변경 된 경우.
환경에서 신뢰할 수 있는 Hyper-v 컴퓨터에 대 한 마스터 이미지와 역할을 하는 참조 호스트에서 사용 하 여 새 CI 정책을 캡처하는 `New-CIPolicy` 명령입니다.
사용 하 여 좋습니다 합니다 **FilePublisher** 수준 및 **해시** Hyper-v 호스트 CI 정책에 대 한 대체 (fallback) 합니다.
먼저 모든 항목이 예상 대로 작동 하는지 확인 하려면 감사 모드로 CI 정책을 만들어야 합니다.
시스템에는 샘플 워크 로드를 확인 한 후 정책을 적용할 수 있으며 HGS 적용된 버전을 복사할 수 있습니다.
코드 무결성 정책 구성 옵션의 전체 목록은 참조 합니다 [Device Guard 설명서](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies)합니다.

```powershell
# Capture a new CI policy with the FilePublisher primary level and Hash fallback and enable user mode code integrity protections
New-CIPolicy -FilePath 'C:\temp\ws2016-hardware01-ci.xml' -Level FilePublisher -Fallback Hash -UserPEs

# Apply the CI policy to the system
ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\ws2016-hardware01-ci.xml' -BinaryFilePath 'C:\temp\ws2016-hardware01-ci.p7b'
Copy-Item 'C:\temp\ws2016-hardware01-ci.p7b' 'C:\Windows\System32\CodeIntegrity\SIPolicy.p7b'
Restart-Computer

# Check the event log for any untrusted binaries and update the policy if necessary
# Consult the Device Guard documentation for more details

# Change the policy to be in enforced mode
Set-RuleOption -FilePath 'C:\temp\ws2016-hardare01-ci.xml' -Option 3 -Delete

# Apply the enforced CI policy on the system
ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\ws2016-hardware01-ci.xml' -BinaryFilePath 'C:\temp\ws2016-hardware01-ci.p7b'
Copy-Item 'C:\temp\ws2016-hardware01-ci.p7b' 'C:\Windows\System32\CodeIntegrity\SIPolicy.p7b'
Restart-Computer
```

정책을 만든 후 테스트 하 고 적용 HGS 서버에 이진 파일 (. p7b)를 복사 하 고 정책을 등록 합니다.

```powershell
Add-HgsAttestationCiPolicy -Name 'WS2016-Hardware01' -Path 'C:\temp\ws2016-hardware01-ci.p7b'
```

**메모리 덤프 암호화 키 추가**

경우는 *Hgs\_NoDumps* 정책은 사용 되지 않습니다 및 *Hgs\_DumpEncryption* 정책을 사용 하는, 보호 된 호스트 수에 크래시 덤프 등 메모리 덤프를 보유할 수 있는 이러한 덤프가 암호화으로 사용할 수 있습니다. 만 보호 된 호스트는 사용 하지 않도록 설정 하는 메모리 덤프를가 하거나 HGS에 알려진 키로 암호화 된 증명을 전달 합니다. 기본적으로 HGS에서 덤프 암호화 키 구성 됩니다.

HGS를 덤프 암호화 키를 추가 하려면 사용 된 `Add-HgsAttestationDumpPolicy` 덤프 암호화 키의 해시를 사용 하 여 HGS를 제공 하는 cmdlet입니다.
덤프 암호화를 사용 하 여 구성에서 Hyper-v 호스트에서 TPM 기준을 캡처하는 경우 해시는 tcglog에 포함 되 고이 제공할 수 있습니다 하는 `Add-HgsAttestationDumpPolicy` cmdlet.

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey01' -Path 'C:\temp\TpmBaselineWithDumpEncryptionKey.tcglog'
```

또는 cmdlet에 대 한 해시의 문자열 표현을 직접 제공할 수 있습니다.

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey02' -PublicKeyHash '<paste your hash here>'
```

에 보호 된 패브릭에서 서로 다른 키를 사용 하려는 경우 각 고유 덤프 암호화 키를 HGS에 추가 해야 합니다.
HGS를 알 수 없는 키를 사용 하 여 메모리 덤프를 암호화 하는 호스트는 증명을 전달 하지 않습니다.

에 대 한 자세한 내용은 Hyper-v 설명서를 참조 하세요 [호스트에서 암호화를 덤프 구성](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)합니다.

#### <a name="check-if-the-system-passed-attestation"></a>시스템 증명을 전달 하는 경우 확인
필요한 정보를 HGS에 등록 한 후 호스트가 증명을 전달 하는 경우를 확인 해야 합니다.
새로 추가한 Hyper-v 호스트에서 실행 `Set-HgsClientConfiguration` HGS 클러스터에 대 한 올바른 Url을 제공 합니다.
실행 하 여 이러한 Url을 가져올 수 있습니다 `Get-HgsServer` HGS 노드에 있습니다.

```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'http://hgs.bastion.local/KeyProtection' -AttestationServerUrl 'http://hgs.bastion.local/Attestation'
```

결과 상태를 나타내지 않는 경우 "IsHostGuarded: True "구성 문제를 해결 해야 합니다.
증명에 실패 한 호스트에서 실패 한 증명을 해결 하는 데 도움이 될 수 있는 문제에 대 한 자세한 보고서를 가져오려면 다음 명령을 실행 합니다.

```powershell
Get-HgsTrace -RunDiagnostics -Detailed
```

> [!IMPORTANT]
> Windows Server 2019 또는 Windows 10 버전 1809 사용 하는 코드 무결성 정책을 사용 하는 경우 `Get-HgsTrace` 에 대 한 오류를 반환할 수 있습니다 합니다 **코드 무결성 정책 Active** 진단 합니다.
> 이 결과 실패 한 진단 하는 것이 상태일 때에 안전 하 게 무시할 수 있습니다.

### <a name="review-attestation-policies"></a>증명 정책을 검토합니다
HGS에서 구성 된 정책은의 현재 상태를 검토 하려면 HGS 노드에서 다음 명령을 실행 합니다.

```powershell
# List all trusted security groups for admin-trusted attestation
Get-HgsAttestationHostGroup

# List all policies configured for TPM-trusted attestation
Get-HgsAttestationPolicy
```

더 이상 (예:는 이전 코드 무결성 정책을 안전 하지 않은 간주 되어 이제는) 보안 요구 사항을 충족 하는 정책을 사용할 수 있다면 다음 명령에서 정책의 이름을 대체 하 여 비활성화할 수 없습니다.

```powershell
Disable-HgsAttestationPolicy -Name 'PolicyName'
```

마찬가지로, 사용할 수 있습니다 `Enable-HgsAttestationPolicy` 정책을 다시 사용할 수 있도록 합니다.

정책 및 모든 HGS 노드에서 제거 하려는 더 이상 할 경우 실행 `Remove-HgsAttestationPolicy -Name 'PolicyName'` 정책을 영구적으로 삭제 하려면.

## <a name="changing-attestation-modes"></a>증명 모드를 변경합니다.
관리자-신뢰할 수 있는 증명을 사용 하 여 보호 된 패브릭에 시작한 경우 충분 한 TPM 2.0 호환 호스트 환경에 즉시 훨씬 더 강력한 TPM 증명 모드를 업그레이드 하려는 가능성이 높습니다.
전환할 준비가 로드할 수 있습니다 미리 HGS의 증명 아티팩트 (CI 정책, 기준 TPM 및 TPM 식별자)의 모든 HGS 관리자 신뢰할 수 있는 증명을 사용 하 여 실행을 계속 합니다.
이렇게 하려면 단순히의 지침에 따라 합니다 [새 보호 된 호스트를 권한 부여](#authorizing-new-guarded-hosts) 섹션입니다.

추가한 다음 모든 정책 HGS를, TPM 모드로 증명 전달는 하는지 확인 하기 위해 호스트에서 가상 증명 시도 실행 하는 다음 단계가입니다.
HGS의 현재 작동 상태는 영향을 주지 않습니다.
아래 명령은 환경과 HGS 노드가 하나 이상에서 호스트의 모든 항목에 대 한 액세스 권한이 있는 컴퓨터에서 실행 되어야 합니다.
방화벽 또는 기타 보안 정책과이 방지 하는 경우이 단계를 건너뛸 수 있습니다.
가능한 경우에 효과적으로 나타내므로 여부 "대칭 이동" TPM 모드로 가동 중지 시간이 발생 하면 Vm에 대 한 제공 하도록 가상 증명을 실행 하는 것이 좋습니다. 

```powershell
# Get information for each host in your environment
$hostNames = 'host01.contoso.com', 'host02.contoso.com', 'host03.contoso.com'
$credential = Get-Credential -Message 'Enter a credential with admin privileges on each host'
$targets = @()
$hostNames | ForEach-Object { $targets += New-HgsTraceTarget -Credential $credential -Role GuardedHost -HostName $_ }

$hgsCredential = Get-Credential -Message 'Enter an admin credential for HGS'
$targets += New-HgsTraceTarget -Credential $hgsCredential -Role HostGuardianService -HostName 'HGS01.bastion.local'

# Initiate the synthetic attestation attempt
Get-HgsTrace -RunDiagnostics -Target $targets -Diagnostic GuardedFabricTpmMode 
```

진단을 완료 후 모든 호스트 하는 경우 TPM 모드로 증명에서 실패 한 것을 결정 하 고 출력된 정보를 검토 합니다.
각 호스트에서 "전달"을 가져올 다음 HGS TPM 모드로 변경 하려면 계속 진행 될 때까지 진단 유틸리티를 다시 실행 합니다.

**TPM 모드로 변경** 완료 하려면 잠시 사용 합니다.
HGS 노드 증명 모드를 업데이트 하려면 다음 명령을 실행 합니다.

```powershell
Set-HgsServer -TrustTpm
```

Active Directory 모드로 다시 전환 해야 할 문제를 실행 하는 경우 하면 실행 하 여 `Set-HgsServer -TrustActiveDirectory`입니다.

모든 항목이 예상 대로 작동을 확인 한 후에 HGS에서 모든 신뢰할 수 있는 Active Directory 호스트 그룹을 제거 하 고 HGS 및 패브릭 도메인 간에 트러스트를 제거 해야 합니다.
Active Directory 트러스트 위치에 두면 트러스트를 다시 사용 하도록 설정 하 고 HGS 신뢰할 수 없는 코드가 확인 되지 않은 보호 된 호스트에서 실행 될 수 있는 Active Directory 모드로 전환할 경우 누군가가 위험이 있습니다.

## <a name="key-management"></a>키 관리
보호 된 패브릭 솔루션 솔루션의 다양 한 구성 요소의 무결성의 유효성을 검사 하 고 테 넌 트 암호를 암호화 하려면 여러 공개/개인 키 쌍을 사용 합니다.
호스트 보호 서비스 (사용 하 여 공용 및 개인 키), 서명 및 암호화 키 보호 된 Vm을 시작 하는 데 사용 되는 두 개 이상의 인증서를 사용 하 여 구성 됩니다.
해당 키를 신중 하 게 관리 되어야 합니다.
악의적 사용자가 개인 키를 획득, 패브릭에서 실행 되는 모든 Vm unshield 또는 위치에 배치 하는 보호 하지 않으려면 약한 증명 정책을 사용 하는 가짜 HGS 클러스터를 설정 하는 일을 할 됩니다.
개인 키 재해 발생 시 손실 되 고 해당 백업에서 찾을, 다시 새 인증서를 인증 하려면 키가 지정 된 각 VM을 새 키 쌍을 설정 해야 합니다.

이 섹션에서는 기능 및 보안 되므로 키를 구성할 수 있도록 일반 키 관리 다룹니다.

### <a name="adding-new-keys"></a>새 키를 추가합니다.
HGS 키 집합이 하나를 사용 하 여 초기화 되어야 합니다 하는 동안에 둘 이상의 암호화 및 서명 키 HGS 추가할 수 있습니다.
HGS를 새 키 추가 이유는 두 가지 가장 일반적인 원인은 다음과 같습니다.
1. 테 넌 트에 하드웨어 보안 모듈 자체 개인 키를 복사 하 고 해당 키가 보호 된 Vm을 시작 하려면 권한을 부여 "bring your own key" 시나리오를 지원 합니다.
2. 먼저 새 키를 추가 하 고 각 VM까지 키 집합을 모두 유지 하 여 HGS에 대 한 기존 키를 바꾸려면 구성 새 키를 사용 하도록 업데이트 되었습니다.

새 키를 추가 하는 프로세스를 사용 하는 인증서 종류에 따라 다릅니다.

**옵션 1: HSM에 저장 된 인증서를 추가 합니다.**

HGS 키 보호에 대 한 하드웨어 보안 모듈 (HSM)에서 만든 인증서를 사용 하는 것이 좋습니다.
Hsm 키 사용은 데이터 센터에서 보안과 관련 된 장치에 대 한 물리적 액세스와 관련이 있는지 확인 합니다.
각 HSM 다릅니다 있고 인증서를 만들고 HGS에 등록 하는 고유한 프로세스입니다.
다음 단계는 HSM을 사용 하기 위한 대략적인 지침 지원 인증서를 제공 하기 위해서입니다.
정확한 단계 및 기능을 위해 HSM 공급 업체의 설명서를 참조 하세요.

1. 클러스터의 각 HGS 노드에서 HSM 소프트웨어를 설치 합니다. 여부에 따라 네트워크 또는 로컬 HSM 장치에는 키 저장소에 대 한 컴퓨터 액세스 권한을 부여 하려면 HSM을 구성 해야 합니다.
2. 사용 하 여 HSM에서 2 개의 인증서를 만들 **2048 비트 RSA 키** 암호화 및 서명
    1. 암호화 인증서를 사용 하 여 만들기는 **데이터 암호화** usage 속성이 HSM에 키
    2. 사용 하 여 서명 인증서를 만들 합니다 **디지털 서명** usage 속성이 HSM에 키
3. HSM 공급 업체의 지침에 따라 각 HGS 노드의 로컬 인증서 저장소에 인증서를 설치 합니다.
4. HSM에서는 세분화 된 권한을 특정 응용 프로그램 또는 사용자가 개인 키를 사용 하는 권한을 부여 하는 경우 인증서에 HGS 그룹 관리 서비스 계정 액세스 권한을 부여 해야 합니다. 실행 하 여 HGS gMSA 계정의 이름을 찾을 수 있습니다. `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
5. 인증서의 다음 명령에서와 지문이 대체 하 여 HGS를 서명 및 암호화 인증서를 추가 합니다.

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA"
    ```

**옵션 2: 내보낼 수 없는 소프트웨어 인증서를 추가합니다.**

회사에서 발급 한 소프트웨어 기반 인증서 있는 경우 인증서의 지문을 사용 하 여 HGS를 추가 해야 내보낼 수 없는 개인 키가 있는 공용 인증 기관.
1. 기관의 지침에 따라 컴퓨터에 인증서를 설치 합니다.
2. HGS 그룹 관리 서비스 계정 읽기-액세스 인증서의 개인 키에 부여 합니다. 실행 하 여 HGS gMSA 계정의 이름을 찾을 수 있습니다. `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`
3. 다음 명령을 사용 하 고 인증서의 지문에서 대체 HGS를 사용 하 여 인증서를 등록 (변경 *암호화* 하 *서명* 서명 인증서에 대 한).

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    ```

> [!IMPORTANT]
> 수동으로 개인 키를 설치 하 고 각 HGS 노드에서 gMSA 계정에 대 한 읽기 액세스 권한을 부여 해야 합니다.
> HGS에 대 한 개인 키를 자동으로 복제할 수 없습니다 *모든* 인증서 지 문으로 등록 합니다.

**옵션 3: PFX 파일에 저장 된 인증서를 추가 합니다.**

소프트웨어 기반 인증서 PFX 파일 형식으로 저장 하 고 암호로 보호 될 수 있는 개인 키가 내보낼 수 있는 경우 HGS를 인증서를 자동으로 관리할 수 있습니다.
PFX 파일을 사용 하 여 추가 된 인증서는 HGS 클러스터의 모든 노드에 자동으로 복제 하 고 HGS 개인 키에 대 한 액세스를 보호 합니다.
PFX 파일을 사용 하 여 새 인증서를 추가 하려면 모든 HGS 노드에서 다음 명령을 실행 (변경할 *암호화* 하 *서명* 서명 인증서에 대 한).

```powershell
$certPassword = Read-Host -AsSecureString -Prompt "Provide the PFX file password"
Add-HgsKeyProtectionCertificate -CertificateType Encryption -CertificatePath "C:\temp\encryptionCert.pfx" -CertificatePassword $certPassword
```

**식별 및 기본 인증서 변경** HGS 서명 및 암호화 인증서가 여러 개를 지원할 수 있지만 한 쌍 해당 "기본" 인증서로 사용 합니다.
이들은 사용자는 HGS 클러스터에 대 한 보호 메타 데이터를 다운로드 하는 경우 사용할 인증서입니다.
인증서는 현재 기본 인증서로 표시 된를 확인 하려면 다음 명령을 실행 합니다.

```powershell
Get-HgsKeyProtectionCertificate -IsPrimary $true
```

새 기본 암호화 또는 서명 인증서를 설정 하려면 원하는 인증서의 지문의 찾을 하 고 다음 명령을 사용 하 여 기본으로 표시 합니다.

```powershell
Get-HgsKeyProtectionCertificate
Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899" -IsPrimary
Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA" -IsPrimary
```

### <a name="renewing-or-replacing-keys"></a>키를 바꾸거나 갱신
HGS에서 사용 된 인증서를 만들 때 인증 기관의 정책 및 요청 정보에 따라 만료 날짜가 인증서 할당 됩니다.
일반적으로 인증서의 유효성을 검사 HTTP 통신을 보호 하는 등 중요 한 시나리오에서 인증서 갱신 서비스 중단 또는 기술은 오류 메시지를 방지 하려면 만료 되기 전에 합니다.
HGS는 이런 의미에서 인증서를 사용 하지 않습니다.
HGS는 간단히 만들고 비대칭 키 쌍을 저장 하는 편리한 방법으로 인증서를 사용 해야 합니다.
만료 된 암호화 또는 HGS에서 서명 인증서를 나타내지 않습니다 취약 한 부분이 나 보호 된 Vm에 대 한 보호 손실 합니다.
또한 인증서 해지 확인 HGS에서 수행 되지 않습니다.
HGS 인증서 또는 발급 기관의 인증서가 해지 되 면 HGS'를 사용 하 여 인증서의 영향을 주지 않습니다.

에 인증서를 HGS에 걱정할 필요는 해당 개인 키에 있는지를 생각 하는 경우 도난 된 합니다.
이 경우 보호 된 Vm의 무결성 있기 위험이 HGS 암호화 및 서명 키 쌍의 개인 키 부분을 소유한 VM에서 보호 하는 보호를 제거 하거나 약한 증명 정책이 있는 가짜 HGS 서버를 구축 하기에 충분 합니다.

이러한 상황에 직면 하 게 규정 준수 표준을 인증서 키를 정기적으로 새로 고쳐야 하기 위해 필요한 경우 다음 단계를 간략하게 HGS 서버에서 키를 변경 하는 프로세스를 설명 합니다.
다음 지침을 HGS 클러스터에서 제공 하는 각 VM에 서비스가 중단 될 중요 한 작업을 나타내는 note 하십시오.
서비스 중단을 최소화 하 고 테 넌 트 Vm의 보안을 확보 하려면 HGS 키를 변경 하는 것에 대 한 적절 한 계획이 필요 합니다.

HGS 노드에 새 쌍을 암호화 및 서명 인증서를 등록 하려면 다음 단계를 수행 합니다.
섹션을 참조 하세요 [새 키를 추가](#adding-new-keys) 에 대 한 자세한 정보를 HGS에 새 키를 추가 하는 다양 한 방법입니다.
1. HGS 서버에 대 한 서명 인증서 및 암호화의 새로운 쌍을 만듭니다. 이상적으로 하드웨어 보안 모듈에서 이러한 생성 됩니다.
2. 새 암호화를 등록 하 고 사용 하 여 인증서 서명 **HgsKeyProtectionCertificate 추가**

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>
    ```
3. 지문을 사용 하는 경우 개인 키를 설치 하 고 키 HGS gMSA 액세스 권한을 부여 하려면 클러스터의 각 노드로 이동 해야 합니다.
4. HGS에서 새 인증서를 기본 인증서 확인

    ```powershell
    Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsPrimary
    Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsPrimary
    ```

이 시점에서 실딩 데이터 HGS 노드에서 가져온 메타 데이터를 사용 하 여 만든 경우 새 인증서를 사용할 되지만 기존 Vm은 계속 이전 인증서는 여전히 남아 있습니다 때문에 작동 합니다.
모든 기존 Vm에 새 키를 사용 하 여 작동을 보장 하려면 각 VM에서 키 보호기를 업데이트 해야 합니다.
이 포함 될 VM 소유자 (사용자 또는 "소유자" 보호를 소유한 엔터티)를 필요로 하는 작업.
각 보호 된 VM에 대해 다음 단계를 수행 합니다.
5. VM을 종료 합니다. VM은 프로세스를 다시 시작 해야 합니다. 그렇지 않으면 나머지 단계가 완료 될 때까지 다시 설정할 수 없습니다.
6. 현재 키 보호기를 파일로 저장 합니다. `Get-VMKeyProtector -VMName 'VM001' | Out-File '.\VM001.kp'`
7. VM 소유자에 게 양도 된 KP
8. HGS에서 업데이트 된 보호 정보 소유자 다운로드 있고 로컬 시스템에서 가져오기
9. 현재 KP 메모리로 읽어, KP, 새 보호 액세스 권한을 부여 하 고 다음 명령을 실행 하 여 새 파일에 저장 합니다.

    ```powershell
    $kpraw = Get-Content -Path .\VM001.kp
    $kp = ConvertTo-HgsKeyProtector -Bytes $kpraw
    $newGuardian = Get-HgsGuardian -Name 'UpdatedHgsGuardian'
    $updatedKP = Grant-HgsKeyProtectorAccess -KeyProtector $kp -Guardian $newGuardian
    $updatedKP.RawData | Out-File .\updatedVM001.kp
    ```
10. 업데이트 된 KP는 호스팅 패브릭 다시 복사
11. KP 원래 VM에 적용 됩니다.

   ```powershell
   $updatedKP = Get-Content -Path .\updatedVM001.kp
   Set-VMKeyProtector -VMName VM001 -KeyProtector $updatedKP
   ```
12. 마지막으로 VM을 시작 하 고 성공적으로 실행을 확인 합니다.

> [!NOTE]
> VM 소유자 VM에서 잘못 된 키 보호기를 설정 하 여 패브릭에서 VM 실행 권한을 부여 하지 않습니다 하는 경우 보호 된 VM을 시작 수 없습니다.
> 알려진된 마지막 좋은 키 보호기를 반환. `Set-VMKeyProtector -RestoreLastKnownGoodKeyProtector`

모든 Vm에 새 보호자 키 권한을 부여 하도록 업데이트 되었습니다, 되 면 사용 하지 않도록 설정 하 고 이전 키를 제거할 수 있습니다.

13. 이전 인증서의 지문이 가져오기 `Get-HgsKeyProtectionCertificate -IsPrimary $false`

14. 다음 명령을 실행 하 여 각 인증서를 사용 하지 않도록 설정 합니다.  

   ```powershell
   Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsEnabled $false
   Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsEnabled $false
   ```

15. Vm이 시작 수를 확인 한 후 사용 하지 않도록 설정, 인증서 HGS에서 인증서를 다음 명령을 실행 하 여 제거 합니다.

   ```powershell
   Remove-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>`
   Remove-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>`
   ```

> [!IMPORTANT]
> VM 백업에는 VM을 시작 하는 데 사용할 기존 인증서를 허용 하는 이전 키 보호기 정보가 포함 됩니다.
> 개인 키가 손상 된 인식 인 경우 VM 백업도 손상 될 수 있습니다 하 고 적절 한 조치를 가정해 야 합니다.
> 백업 (.vmcx)에서 VM 구성을 제거 하면 BitLocker 복구 암호를 사용 하 여 다음에 VM을 부팅 해야 하는 대신 키 보호기를 제거 됩니다.

### <a name="key-replication-between-nodes"></a>노드 간의 주요 복제
HGS 클러스터의 모든 노드에 구성 해야 서명 동일한 암호화를 사용 하 여 (구성) 하는 경우 SSL 인증서입니다.
이것은 Hyper-v 호스트 클러스터의 노드에 연락 성공적으로 처리 하는 해당 요청 수를 확인 하는 데 필요 합니다.

**PFX 기반 인증서를 사용 하 여 HGS 서버를 초기화 하는 경우** 다음 클러스터의 모든 노드 간에 HGS 해당 인증서의 공개 및 개인 키를 자동으로 복제 됩니다.
하나의 노드에 키를 추가 해야 합니다.

**인증서 참조를 사용 하 여 HGS 서버를 초기화 하는 경우** 지문, 다음 HGS만 복제 또는 합니다 *공용* 각 노드에 인증서의 키입니다.
HGS 자체를 부여할 수 없습니다. 또한이 시나리오의 모든 노드에서 개인 키에 액세스 합니다.
따라서 것 해야 합니다.
1. 각 HGS 노드에서 개인 키를 설치 합니다.
2. 하지만 HGS 그룹 관리 서비스 계정 (gMSA) 액세스 부여 각 노드에서 개인 키에 이러한 작업에는 추가 작업 부담을 추가 HSM 백업 키를 내보낼 수 없는 개인 키를 사용 하 여 인증서 필요 합니다.

**SSL 인증서** 어떤 형태로 든 복제 되지 않습니다.
것이 동일한 SSL 인증서를 사용 하 여 각 HGS 서버를 초기화 하 고 SSL 인증서를 바꾸거나 갱신 하려는 때마다 각 서버를 업데이트 해야 합니다.
SSL 인증서를 바꾸는 것이 좋습니다 사용 하 여 수행 하는 합니다 [집합 HgsServer](https://technet.microsoft.com/library/mt652180.aspx) cmdlet.

## <a name="unconfiguring-hgs"></a>HGS 구성 취소

서비스 해제 또는 크게 HGS 서버를 다시 구성 해야 할 경우 사용 하 여 수행할 수 있습니다 합니다 [Clear HgsServer](https://technet.microsoft.com/library/mt652176.aspx) 또는 [제거 HgsServer](https://technet.microsoft.com/library/mt652182.aspx) cmdlet.

### <a name="clearing-the-hgs-configuration"></a>HGS 구성 지우기

HGS 클러스터에서 노드를 제거 하려면 사용 합니다 [Clear HgsServer](https://technet.microsoft.com/library/mt652176.aspx) cmdlet.
이 cmdlet은 다음과 같이 변경 실행 되는 서버에서:

- 증명 및 키 보호 서비스를 등록 취소
- "Microsoft.windows.hgs" JEA 관리 끝점을 제거
- HGS 장애 조치 클러스터에서 로컬 컴퓨터를 제거합니다.

서버 클러스터의 마지막 HGS 노드를 클러스터 및 해당 하는 분산 네트워크 이름 리소스 또한 소멸 됩니다.

```powershell
# Removes the local computer from the HGS cluster
Clear-HgsServer
```

HGS 서버 지우기 작업이 완료 되 면 다시 초기화 될 수 있습니다 [Initialize HgsServer](https://technet.microsoft.com/library/mt652185.aspx)합니다.
사용 하는 경우 [설치 HgsServer](https://technet.microsoft.com/library/mt652169.aspx) 는 Active Directory Domain Services 도메인을 설정 하려면 해당 도메인 구성 및 운영 작업 후 유지 되는 선택을 취소 합니다.

### <a name="uninstalling-hgs"></a>HGS를 제거합니다.

HGS 클러스터에서 노드를 제거 하려는 경우 **및** 에서 실행 중인 Active Directory 도메인 컨트롤러 수준 내리기를 사용 합니다 [제거 HgsServer](https://technet.microsoft.com/library/mt652182.aspx) cmdlet.
이 cmdlet은 다음과 같이 변경 실행 되는 서버에서:

- 증명 및 키 보호 서비스를 등록 취소
- "Microsoft.windows.hgs" JEA 관리 끝점을 제거
- HGS 장애 조치 클러스터에서 로컬 컴퓨터를 제거합니다.
- 구성 된 경우 Active Directory 도메인 컨트롤러에서 강등

서버 클러스터의 마지막 HGS 노드 인 경우 도메인, 장애 조치 클러스터 및 클러스터의 분산 네트워크 이름 리소스 제거 됩니다.

```powershell
# Removes the local computer from the HGS cluster and demotes the ADDC (restart required)
$newLocalAdminPassword = Read-Host -AsSecureString -Prompt "Enter a new password for the local administrator account"
Uninstall-HgsServer -LocalAdministratorPassword $newLocalAdminPassword -Restart
```

제거 작업이 완료 된 후 컴퓨터를 다시 시작 다시 설치할 수 있습니다 ADDC 및 사용 하 여 HGS [설치 HgsServer](https://technet.microsoft.com/library/mt652169.aspx) 컴퓨터를 도메인에 가입 하 고 사용 하 여 해당 도메인에서 HGS 서버를 초기화 또는 [ 초기화 HgsServer](https://technet.microsoft.com/library/mt652185.aspx)합니다.

에서 더 이상 HGS 노드로 컴퓨터를 사용 하려는 경우에 Windows에서 역할을 제거할 수 없습니다.

```powershell
Uninstall-WindowsFeature HostGuardianServiceRole
```
