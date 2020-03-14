---
title: 호스트 보호자 서비스 관리
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: eecb002e-6ae5-4075-9a83-2bbcee2a891c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: 41912c90beacbb0c0c285ea4da8305c1afdf2a51
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322605"
---
# <a name="managing-the-host-guardian-service"></a>호스트 보호자 서비스 관리

> 적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

HGS (호스트 보호 서비스)는 보호 된 패브릭 솔루션의 핵심이입니다.
패브릭의 Hyper-v 호스트를 호스터 또는 엔터프라이즈에서 인식 하 고 신뢰할 수 있는 소프트웨어를 실행 하 고 보호 된 Vm을 시작 하는 데 사용 되는 키를 관리 하는 일을 담당 합니다.
테 넌 트가 보호 된 Vm을 호스트 하는 것을 신뢰 하기로 결정 하는 경우 호스트 보호자 서비스의 구성 및 관리에 해당 신뢰를 배치 합니다.
따라서 보호 된 패브릭의 보안, 가용성 및 안정성을 보장 하기 위해 호스트 보호자 서비스를 관리할 때 모범 사례를 따르는 것이 매우 중요 합니다.
다음 섹션의 지침에서는 HGS 관리자에 게 가장 일반적으로 작동 하는 문제를 다룹니다.

## <a name="limiting-admin-access-to-hgs"></a>관리자 액세스를 HGS로 제한
HGS의 보안을 중요 한 특성으로 인해 해당 관리자가 조직에서 항상 신뢰할 수 있는 구성원 인지 확인 하 고 패브릭 리소스 관리자와 분리 하는 것이 중요 합니다.
또한 HTTPS를 통한 WinRM과 같은 보안 통신 프로토콜을 사용 하 여 보안 워크스테이션에서 HGS를 관리 하는 것이 좋습니다.

### <a name="separation-of-duties"></a>의무 분리
HGS를 설정 하는 경우 HGS 용으로 격리 된 Active Directory 포리스트를 만들거나 HGS를 기존 트러스트 된 도메인에 조인할 수 있는 옵션이 제공 됩니다.
조직에서 관리자에 게 할당 하는 역할 뿐만 아니라 이러한 결정은 HGS의 트러스트 경계를 결정 합니다.
사용자가 hgs에 대 한 액세스 권한이 있는 사용자는 hgs에 영향을 줄 수 있는 기타 항목 (예: Active Directory)의 관리자로 직접 또는 간접적으로 보호 된 패브릭에 대 한 제어를 가집니다.
HGS 관리자는 보호 된 Vm을 실행할 수 있는 Hyper-v 호스트를 선택 하 고 보호 된 Vm을 시작 하는 데 필요한 인증서를 관리할 수 있습니다.
HGS에 대 한 액세스 권한이 있는 공격자 또는 악의적인 관리자는이 기능을 사용 하 여 손상 된 호스트에 게 보호 된 Vm을 실행 하 고 키 자료를 제거 하 여 서비스 거부 공격을 시작할 수 있는 권한을 부여할 수 있습니다.

이러한 위험을 방지 하려면 hgs의 관리자 (HGS가 가입 된 도메인 포함)와 Hyper-v 환경 간에 겹치는 부분을 제한 하 *는 것이 좋습니다.*
두 시스템에 대 한 액세스 권한이 있는 관리자가 없도록 하 여 공격자는 자신의 임무를 완료 하 여 HGS 정책을 변경 하기 위해 2 명의 사용자 로부터 서로 다른 2 개의 계정을 손상 해야 합니다.
즉, 두 Active Directory 환경의 도메인 및 엔터프라이즈 관리자는 동일한 사람이 아니어야 하며, HGS는 Hyper-v 호스트와 동일한 Active Directory 포리스트를 사용 해야 합니다.
자신에 게 더 많은 리소스에 대 한 액세스 권한을 부여할 수 있는 사람은 보안상 위험할 수 있습니다.

### <a name="using-just-enough-administration"></a>충분 한 관리 사용
HGS는 더 안전 하 게 관리할 수 있도록 기본 제공 되는 [충분 한 관리](https://aka.ms/JEAdocs) (jea) 역할만 제공 합니다.
JEA를 사용 하면 관리자가 아닌 사용자에 게 관리 작업을 위임할 수 있습니다. 즉, HGS 정책을 관리 하는 사용자는 실제로 전체 컴퓨터 또는 도메인의 관리자가 될 필요는 없습니다.
JEA는 사용자가 PowerShell 세션에서 실행할 수 있는 명령과 백그라운드 (각 사용자 세션 마다 고유)의 임시 로컬 계정을 사용 하 여 일반적으로 권한 상승이 필요한 명령을 실행 하는 방식으로 작동 합니다.

HGS는 미리 구성 된 2 개의 JEA 역할을 제공 합니다.
- 사용자가 보호 된 Vm을 실행할 새 호스트에 권한을 부여 하는 것을 포함 하 여 모든 HGS 정책을 관리할 수 있도록 하는 **Hgs 관리자** .
- 사용자만이 기존 정책을 감사할 수 있도록 허용 하는 **HGS 검토자** . HGS 구성을 변경할 수 없습니다.

JEA를 사용 하려면 먼저 새 표준 사용자를 만들어 HGS admins 또는 HGS 검토자 그룹의 구성원으로 설정 해야 합니다.
`Install-HgsServer`를 사용 하 여 HGS에 대 한 새 포리스트를 설정 하는 경우 이러한 그룹은 각각 "*servicename*Administrators" 및 "*servicename*검토자"로 이름이 지정 됩니다. 여기서 *servicename* 은 hgs 클러스터의 네트워크 이름입니다.
기존 도메인에 HGS를 조인한 경우 `Initialize-HgsServer`에서 지정한 그룹 이름을 참조 해야 합니다.

**HGS 관리자 및 검토자 역할에 대 한 표준 사용자 만들기**

```powershell
$hgsServiceName = (Get-ClusterResource HgsClusterResource | Get-ClusterParameter DnsName).Value
$adminGroup = $hgsServiceName + "Administrators"
$reviewerGroup = $hgsServiceName + "Reviewers"

New-ADUser -Name 'hgsadmin01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Admin Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $adminGroup -Members 'hgsadmin01'

New-ADUser -Name 'hgsreviewer01' -AccountPassword (Read-Host -AsSecureString -Prompt 'HGS Reviewer Password') -ChangePasswordAtLogon $false -Enabled $true
Add-ADGroupMember -Identity $reviewerGroup -Members 'hgsreviewer01'
```

**검토자 역할을 사용 하 여 정책 감사**

HGS에 네트워크로 연결 된 원격 컴퓨터에서 PowerShell에서 다음 명령을 실행 하 여 검토자 자격 증명으로 JEA 세션을 입력 합니다.
검토자 계정은 표준 사용자 일 뿐 이므로 일반 Windows PowerShell 원격, HGS에 대 한 원격 데스크톱 액세스 등에 사용할 수 없습니다.

```powershell
Enter-PSSession -ComputerName <hgsnode> -Credential '<hgsdomain>\hgsreviewer01' -ConfigurationName 'microsoft.windows.hgs'
```

그런 다음 `Get-Command` 세션에서 허용 되는 명령을 확인 하 고 허용 되는 명령을 실행 하 여 구성을 감사할 수 있습니다.
아래 예제에서는 HGS에서 사용 하도록 설정 된 정책을 확인 합니다.

```powershell
Get-Command

Get-HgsAttestationPolicy
```

JEA 세션에 대 한 작업이 완료 되 면 명령 `Exit-PSSession` 또는 해당 별칭 `exit`을 입력 합니다. 

**관리자 역할을 사용 하 여 HGS에 새 정책 추가**

실제로 정책을 변경 하려면 ' hgsAdministrators ' 그룹에 속하는 id를 사용 하 여 JEA 끝점에 연결 해야 합니다.
아래 예제에서는 새 코드 무결성 정책을 HGS에 복사 하 고 JEA를 사용 하 여 등록할 수 있는 방법을 보여 줍니다.
구문은 사용 되는 것과 다를 수 있습니다.
이는 전체 파일 시스템에 대 한 액세스 권한이 없는 것 처럼 JEA의 일부 제한 사항을 수용 하기 위한 것입니다.

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

## <a name="monitoring-hgs"></a>HGS 모니터링
### <a name="event-sources-and-forwarding"></a>이벤트 원본 및 전달
HGS의 이벤트는 Windows 이벤트 로그에 2 개 원본으로 표시 됩니다.
- **HostGuardianService-증명**
- **HostGuardianService-KeyProtection**

이벤트 뷰어를 열고 HostGuardianService 및 HostGuardianService-KeyProtection으로 이동 하 여 이러한 이벤트를 볼 수 있습니다.

많은 환경에서 이벤트를 보다 쉽게 분석 수 있도록 중앙 Windows 이벤트 수집기로 이벤트를 전달 하는 것이 좋습니다.
자세한 내용은 [Windows 이벤트 전달 설명서](https://msdn.microsoft.com/library/windows/desktop/bb427443.aspx)를 확인 하세요.

### <a name="using-system-center-operations-manager"></a>System Center Operations Manager 사용
또한 System Center 2016-Operations Manager를 사용 하 여 HGS 및 보호 된 호스트를 모니터링할 수 있습니다.
보호 된 패브릭 관리 팩에는 증명 및 HGS 서버를 통과 하지 못하는 호스트를 포함 하 여 데이터 센터 가동 중지 시간을 유발할 수 있는 일반적인 잘못 된 구성을 확인 하는 이벤트 모니터가 있습니다.

시작 하려면 [SCOM 2016을 설치 및 구성](https://technet.microsoft.com/system-center-docs/om/welcome-to-operations-manager) 하 고 [보호 된 패브릭 관리 팩을 다운로드](https://www.microsoft.com/download/details.aspx?id=52764)하세요.
포함 된 관리 팩 가이드에서는 관리 팩을 구성 하 고 해당 모니터의 범위를 이해 하는 방법을 설명 합니다.

## <a name="backing-up-and-restoring-hgs"></a>HGS 백업 및 복원
### <a name="disaster-recovery-planning"></a>재해 복구 계획
재해 복구 계획을 수립할 때 보호 된 패브릭에서 호스트 보호자 서비스의 고유한 요구 사항을 고려 하는 것이 중요 합니다.
일부 또는 모든 HGS 노드가 손실 되 면 사용자가 보호 된 Vm을 시작 하지 못하도록 하는 즉시 가용성 문제를 해결할 수 있습니다.
전체 HGS 클러스터가 손실 되는 시나리오에서는 hgs 클러스터를 복원 하 고 정상적인 작업을 다시 시작 하기 위해 수동으로 HGS 구성의 전체 백업을 수행 해야 합니다.
이 섹션에서는 이러한 시나리오를 준비 하는 데 필요한 단계에 대해 설명 합니다.

먼저 HGS가 백업 하는 데 중요 한 사항을 이해 하는 것이 중요 합니다.
HGS는 보호 된 Vm을 실행할 수 있는 권한이 있는 호스트를 결정 하는 데 도움이 되는 몇 가지 정보를 유지 합니다.
다음을 포함합니다.
1. Active Directory 증명을 사용 하는 경우 신뢰할 수 있는 호스트를 포함 하는 그룹에 대 한 보안 식별자를 Active Directory 합니다.
2. 사용자 환경에 있는 각 호스트의 고유한 TPM 식별자
3. 호스트의 각 고유 구성에 대 한 TPM 정책 하거나
4. 호스트에서 실행할 수 있는 소프트웨어를 결정 하는 코드 무결성 정책

이러한 증명 아티팩트를 얻으려면 호스팅 패브릭의 관리자와 조정 하 여 재해가 발생 한 후에이 정보를 다시 가져오는 것이 어려울 수 있습니다.

또한 HGS는 보호 된 VM을 시작 하는 데 필요한 정보 (키 보호기)를 암호화 하 고 서명 하는 데 사용 되는 2 개 이상의 인증서에 액세스 해야 합니다.
이러한 인증서는 잘 알려져 있으며 (보호 된 Vm의 소유자가 해당 Vm을 실행 하도록 패브릭에 권한을 부여 하는 데 사용 됨) 원활한 복구 환경을 위해 재해 후에 복원 해야 합니다.
재해 발생 후 동일한 인증서를 사용 하 여 HGS를 복원 하지 않아야 하는 경우 새 키에 대 한 정보를 해독할 수 있도록 각 VM을 업데이트 해야 합니다.
보안상의 이유로 vm 소유자만 이러한 새 키에 권한을 부여 하도록 VM 구성을 업데이트할 수 있습니다. 즉, 재해가 발생 한 후에 키를 복원 하지 못하면 각 VM 소유자가 vm을 다시 실행 하기 위한 조치를 취해야 합니다.

#### <a name="preparing-for-the-worst"></a>최악의 경우 준비
HGS의 완전 한 손실을 준비 하려면 다음 두 단계를 수행 해야 합니다.
1. HGS 증명 정책 백업
2. HGS 키 백업

이러한 단계를 모두 수행 하는 방법에 대 한 지침은 [HGS 백업](#backing-up-hgs) 섹션에서 제공 됩니다.

필요 하지는 않지만 Active Directory 도메인 또는 Active Directory 자체에서 HGS를 관리할 수 있는 권한이 있는 사용자 목록을 백업 하는 것이 좋습니다.

정보를 최신 상태로 유지 하 고 변조 또는 도난 방지를 위해 안전 하 게 저장 하려면 백업을 정기적으로 수행 해야 합니다.

HGS 노드의 전체 시스템 이미지를 백업 하거나 복원 하는 것은 **권장 되지 않습니다** .
전체 클러스터를 잃어버린 이벤트에서 모범 사례는 전체 서버 OS가 아닌 새 HGS 노드를 설정 하 고 HGS 상태만 복원 하는 것입니다.

#### <a name="recovering-from-the-loss-of-one-node"></a>한 노드의 손실에서 복구
HGS 클러스터에서 하나 이상의 노드 (일부 노드 제외)가 손실 된 경우 배포 가이드의 지침에 따라 [클러스터에 노드를 추가할](guarded-fabric-configure-additional-hgs-nodes.md) 수 있습니다.
증명 정책은 제공 된 암호를 사용 하 여 PFX 파일로 HGS에 제공 된 인증서와 마찬가지로 자동으로 동기화 됩니다.
지문을 사용 하 여 HGS에 추가 된 인증서 (내보낼 수 없는 및 하드웨어 지원 인증서, 일반적으로)의 경우 각 새 노드에 각 인증서의 개인 키에 대 한 액세스 권한이 있는지 확인 해야 합니다.

#### <a name="recovering-from-the-loss-of-the-entire-cluster"></a>전체 클러스터의 손실에서 복구
전체 HGS 클러스터가 중단 되 고 다시 온라인 상태로 전환할 수 없는 경우 백업에서 HGS를 복원 해야 합니다.
백업에서 HGS를 복원 하려면 먼저 [배포 가이드의 지침](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)에 따라 새 hgs 클러스터를 설정 해야 합니다.
호스트에서 이름 확인을 지원 하기 위해 복구 HGS 환경을 설정할 때 동일한 클러스터 이름을 사용 하는 것이 좋지만 필수는 아닙니다.
동일한 이름을 사용 하면 새 증명 및 키 보호 Url을 사용 하 여 호스트를 다시 구성 하지 않아도 됩니다.
개체를 Active Directory 도메인 백업 HGS로 복원한 경우 hgs 서버를 초기화 하기 전에 HGS 클러스터, 컴퓨터, 서비스 계정 및 JEA 그룹을 나타내는 개체를 제거 하는 것이 좋습니다.

첫 번째 HGS 노드 (예: 설치 및 초기화 됨)를 설정 했으면 [백업에서 HGS 복원](#restoring-hgs-from-a-backup) 의 절차에 따라 키 보호 인증서의 증명 정책 및 공개 절반을 복원 합니다.
인증서 공급자의 지침에 따라 인증서의 개인 키를 수동으로 복원 해야 합니다 (예: Windows에서 인증서 가져오기 또는 HSM 지원 인증서에 대 한 액세스 구성).
첫 번째 노드를 설정한 후 원하는 용량 및 복원 력에 도달할 때까지 [클러스터에 추가 노드](guarded-fabric-configure-additional-hgs-nodes.md) 를 계속 설치할 수 있습니다.

### <a name="backing-up-hgs"></a>HGS 백업
HGS 관리자는 정기적으로 HGS를 백업 해야 합니다.
전체 백업은 적절 한 보안을 유지 해야 하는 중요 한 키 자료를 포함 합니다.
신뢰할 수 없는 엔터티가 이러한 키에 대 한 액세스 권한을 얻는 경우 해당 자료를 사용 하 여 보호 된 Vm을 손상 시킬 수 있도록 악성 HGS 환경을 설정할 수 있습니다.

**증명 정책 백업** HGS 증명 정책을 백업 하려면 작동 하는 HGS 서버 노드에서 다음 명령을 실행 합니다.
암호를 제공 하 라는 메시지가 표시 됩니다.
이 암호는 인증서 지문 대신 PFX 파일을 사용 하 여 HGS에 추가 된 인증서를 암호화 하는 데 사용 됩니다.

```powershell
Export-HgsServerState -Path C:\temp\HGSBackup.xml
```

> [!NOTE]
> 관리자가 신뢰할 수 있는 증명을 사용 하는 경우 보호 된 호스트에 권한을 부여 하기 위해 HGS에서 사용 하는 보안 그룹의 멤버 자격을 별도로 백업 해야 합니다.
> HGS는 보안 그룹의 SID만 백업 합니다. 단, 해당 그룹 내의 멤버 자격은 백업 하지 않습니다.
> 재해가 발생 하는 동안 이러한 그룹이 손실 된 경우 그룹을 다시 만들고 보호 된 각 호스트를 다시 추가 해야 합니다.

**인증서 백업**

`Export-HgsServerState` 명령은 명령이 실행 될 때 HGS에 추가 된 PFX 기반 인증서를 백업 합니다.
지문을 사용 하 여 HGS에 인증서를 추가한 경우 (일반적으로 내보낼 수 없고 하드웨어 지원 인증서의 경우) 인증서에 대 한 개인 키를 수동으로 백업 해야 합니다.
HGS에 등록 되어 있고 수동으로 백업 해야 하는 인증서를 식별 하려면 작동 하는 모든 HGS 서버 노드에서 다음 PowerShell 명령을 실행 합니다.

```powershell
Get-HgsKeyProtectionCertificate | Where-Object { $_.CertificateData.GetType().Name -eq 'CertificateReference' } | Format-Table Thumbprint, @{ Label = 'Subject'; Expression = { $_.CertificateData.Certificate.Subject } }
```

나열 된 각 인증서에 대해 개인 키를 수동으로 백업 해야 합니다.
내보낼 수 없는 소프트웨어 기반 인증서를 사용 하는 경우 인증 기관에 문의 하 여 인증서의 백업이 있는지 확인 하거나 필요 시 다시 발급할 수 있습니다.
하드웨어 보안 모듈에 생성 및 저장 된 인증서의 경우 재해 복구 계획에 대 한 지침은 장치에 대 한 설명서를 참조 해야 합니다.

인증서 백업을 증명 정책 백업과 함께 안전한 위치에 저장 하 여 두 조각을 함께 복원할 수 있도록 해야 합니다.

**백업할 추가 구성**

백업 된 HGS 서버 상태에는 hgs 클러스터의 이름, Active Directory의 정보 또는 HGS Api와의 보안 통신에 사용 되는 SSL 인증서가 포함 되지 않습니다.
이러한 설정은 일관성을 위해 중요 하지만 재해 발생 후 HGS 클러스터를 다시 온라인 상태로 전환 하는 것은 중요 하지 않습니다.

HGS 서비스의 이름을 캡처하려면 `Get-HgsServer`를 실행 하 고 증명 및 키 보호 Url에서 플랫 이름을 확인 합니다.
예를 들어 증명 URL이 "<http://hgs.contoso.com/Attestation>" 인 경우 "hgs"는 HGS 서비스 이름입니다.

HGS에서 사용 하는 Active Directory 도메인은 다른 Active Directory 도메인과 같이 관리 해야 합니다.
재해 후에 HGS를 복원 하는 경우 현재 도메인에 있는 정확한 개체를 다시 만들 필요가 없습니다.
그러나 Active Directory를 백업 하 고 관리자가 신뢰할 수 있는 증명에서 사용 하는 보안 그룹의 멤버 자격 뿐만 아니라 보호 된 호스트에 대 한 권한을 부여 하는 데 사용 되는 경우에는 복구를 쉽게 수행할 수 있습니다.

HGS에 대해 구성 된 SSL 인증서의 지문을 확인 하려면 PowerShell에서 다음 명령을 실행 합니다.
그런 다음 인증서 공급자의 지침에 따라 SSL 인증서를 백업할 수 있습니다.

```powershell
Get-WebBinding -Protocol https | Select-Object certificateHash
```

### <a name="restoring-hgs-from-a-backup"></a>백업에서 HGS 복원
다음 단계에서는 백업에서 HGS 설정을 복원 하는 방법을 설명 합니다.
이러한 단계는 이미 실행 중인 HGS 인스턴스에 대 한 변경 내용을 실행 취소 하려고 하는 경우와 이전에는 완전히 손실 된 후 새로운 HGS 클러스터를 실행 하는 경우와 관련이 있습니다.

#### <a name="set-up-a-replacement-hgs-cluster"></a>대체 HGS 클러스터 설정
HGS를 복원 하려면 먼저 구성을 복원할 수 있는 초기화 된 HGS 클러스터가 있어야 합니다.
실수로 삭제 한 설정을 기존 (실행 중인) 클러스터로 단순히 가져오는 경우이 단계를 건너뛸 수 있습니다.
HGS의 전체 손실에서 복구 하는 경우 [배포 가이드의 지침](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)에 따라 하나 이상의 hgs 노드를 설치 하 고 초기화 해야 합니다.

특히 다음을 수행 해야 합니다.
1. [Hgs 도메인 설정](guarded-fabric-choose-where-to-install-hgs.md) 또는 기존 도메인에 hgs 조인
2. 기존 키 *또는* 임시 키 집합을 사용 하 여 [HGS 서버를 초기화](guarded-fabric-initialize-hgs.md) 합니다. HGS 백업 파일에서 실제 키를 가져온 후 [임시 키를 제거할](#renewing-or-replacing-keys) 수 있습니다.
3. 백업에서 [HGS 설정을 가져와서](#import-settings-from-a-backup) 신뢰할 수 있는 호스트 그룹, 코드 무결성 정책, tpm 기준 및 tpm 식별자 복원

> [!TIP]
> 새 HGS 클러스터는 백업 파일을 내보낸 HGS 인스턴스와 동일한 인증서, 서비스 이름 또는 도메인을 사용할 필요가 없습니다.

#### <a name="import-settings-from-a-backup"></a>백업에서 설정 가져오기

증명 정책, PFX 기반 인증서 및 비 PFX 인증서의 공개 키를 백업 파일에서 HGS 노드로 복원 하려면 초기화 된 HGS 서버 노드에서 다음 명령을 실행 합니다.
백업을 만들 때 지정한 암호를 입력 하 라는 메시지가 표시 됩니다.

```powershell
Import-HgsServerState -Path C:\Temp\HGSBackup.xml
```

관리자가 신뢰할 수 있는 증명 정책 또는 TPM으로 신뢰할 수 있는 증명 정책만 가져오려는 경우 `-ImportActiveDirectoryModeState` 또는 `-ImportTpmModeState` 플래그를 [HgsServerState](https://technet.microsoft.com/library/mt652168.aspx)으로 지정 하 여 수행할 수 있습니다.

`Import-HgsServerState`를 실행 하기 전에 Windows Server 2016에 대 한 최신 누적 업데이트가 설치 되어 있는지 확인 합니다.
실패 하면 가져오기 오류가 발생할 수 있습니다.

> [!NOTE]
> 이러한 정책이 이미 하나 이상 설치 되어 있는 기존 HGS 노드에서 정책을 복원 하는 경우 가져오기 명령에는 각 중복 정책에 대 한 오류가 표시 됩니다.
> 이는 예상 된 동작이 며 대부분의 경우 무시 해도 됩니다.

#### <a name="reinstall-private-keys-for-certificates"></a>인증서에 대 한 개인 키 다시 설치
지문을 사용 하 여 백업을 만든 HGS에서 사용 되는 인증서를 추가 하는 경우 해당 인증서의 공개 키만 백업 파일에 포함 됩니다.
즉, HGS가 Hyper-v 호스트에서 요청을 처리 하기 전에 이러한 각 인증서의 개인 키에 대 한 액세스를 수동으로 설치 및/또는 부여 해야 합니다.
해당 단계를 완료 하는 데 필요한 작업은 인증서가 원래 발급 된 방법에 따라 달라 집니다.
인증 기관에서 발급 한 소프트웨어 지원 인증서의 경우 CA에 문의 하 여 개인 키를 가져오고 해당 지침에 따라 **각** HGS 노드에 설치 해야 합니다.
마찬가지로 인증서가 하드웨어를 지 원하는 경우에는 하드웨어 보안 모듈 공급 업체의 설명서를 참조 하 여 각 HGS 노드에 필요한 드라이버를 설치 하 여 HSM에 연결 하 고 각 컴퓨터에 개인 키에 대 한 액세스 권한을 부여 해야 합니다.

미리 알림으로, 지문을 사용 하 여 HGS에 추가 된 인증서는 개인 키를 각 노드에 수동으로 복제 해야 합니다.
복원 된 HGS 클러스터에 추가 하는 각 추가 노드에서이 단계를 반복 해야 합니다.

#### <a name="review-imported-attestation-policies"></a>가져온 증명 정책 검토
백업에서 설정을 가져온 후에는 `Get-HgsAttestationPolicy`를 사용 하 여 가져온 모든 정책을 철저히 검토 하 여 보호 된 Vm을 실행 하기 위해 신뢰 하는 호스트만 성공적으로 입증할 수 있도록 하는 것이 좋습니다.
더 이상 보안 상태와 일치 하지 않는 정책을 찾으면 [해당 정책을 사용 하지 않도록 설정 하거나 제거할](#review-attestation-policies)수 있습니다.

#### <a name="run-diagnostics-to-check-system-state"></a>진단을 실행 하 여 시스템 상태 확인
HGS 노드의 상태를 설정 하 고 복원한 후에는 HGS 진단 도구를 실행 하 여 시스템의 상태를 확인 해야 합니다.
이렇게 하려면 구성을 복원한 HGS 노드에서 다음 명령을 실행 합니다.

```powershell
Get-HgsTrace -RunDiagnostics
```

"전체 결과"가 "통과"가 아니면 시스템 구성을 완료 하려면 추가 단계가 필요 합니다.
추가 정보에 대해 실패 한 하위 테스트에 보고 된 메시지를 확인 합니다.

## <a name="patching-hgs"></a>HGS 패치
최신 누적 업데이트를 설치 하면 호스트 보호자 서비스 노드를 최신 상태로 유지 하는 것이 중요 합니다. 새 HGS 노드를 설정 하는 경우 HGS 역할을 설치 하거나 구성 하기 전에 사용 가능한 업데이트를 설치 하는 것이 좋습니다.
이렇게 하면 새로운 기능이 나 변경 된 기능이 즉시 적용 됩니다.

보호 된 패브릭을 패치 하는 경우 **HGS를 업그레이드 하기 전에**먼저 *모든* hyper-v 호스트를 업그레이드 하는 것이 좋습니다.
Hyper-v 호스트가 필요한 정보를 제공 하도록 업데이트 된 *후* 에 HGS의 증명 정책에 대 한 변경 내용이 적용 되도록 하기 위한 것입니다.
업데이트에서 정책의 동작을 변경 하는 경우 패브릭을 중단 하지 않도록 자동으로 설정 되지 않습니다.
이러한 업데이트를 적용 하려면 다음 섹션의 지침에 따라 새로운 또는 변경 된 증명 정책을 활성화 해야 합니다.
Windows Server에 대 한 릴리스 정보 및 설치 하는 누적 업데이트를 읽고 정책 업데이트가 필요한 지 확인 하는 것이 좋습니다.

### <a name="updates-requiring-policy-activation"></a>정책 활성화가 필요한 업데이트
HGS 업데이트가 증명 정책의 동작을 도입 하거나 크게 변경 하는 경우 변경 된 정책을 활성화 하려면 추가 단계가 필요 합니다.
정책 변경 내용은 HGS 상태를 내보내고 가져온 후에만 적용 됩니다.
사용자 환경의 모든 호스트 및 모든 HGS 노드에 누적 업데이트를 적용 한 후에만 새 정책 또는 변경 된 정책을 활성화 해야 합니다.
모든 컴퓨터가 업데이트 되 면 모든 HGS 노드에서 다음 명령을 실행 하 여 업그레이드 프로세스를 트리거합니다.

```powershell
$password = Read-Host -AsSecureString -Prompt "Enter a temporary password"
Export-HgsServerState -Path .\temporaryExport.xml -Password $password
Import-HgsServerState -Path .\temporaryExport.xml -Password $password
```

새 정책이 도입 된 경우 기본적으로 사용 하지 않도록 설정 됩니다.
새 정책을 사용 하도록 설정 하려면 먼저 Microsoft 정책 목록 (' HGS_ '로 시작)에서 찾은 후 다음 명령을 사용 하 여 사용 하도록 설정 합니다.

```powershell
Get-HgsAttestationPolicy

Enable-HgsAttestationPolicy -Name <Hgs_NewPolicyName>
```

## <a name="managing-attestation-policies"></a>증명 정책 관리
HGS는 호스트가 "정상"으로 간주 되어 보호 된 Vm을 실행할 수 있도록 허용 하기 위해 충족 해야 하는 최소 요구 사항 집합을 정의 하는 몇 가지 증명 정책을 유지 관리 합니다.
이러한 정책 중 일부는 Microsoft에서 정의 되 고, 다른 일부는 사용자의 환경에서 허용 되는 코드 무결성 정책, TPM 기준 및 호스트를 정의 하는 데 추가 됩니다.
이러한 정책을 정기적으로 유지 관리 하 여 업데이트 하 고 교체할 때 호스트를 계속 증명 수 있는지 확인 하 고, 신뢰할 수 없는 호스트나 구성이 성공적으로 증명 차단 되었는지 확인 해야 합니다.

관리자가 신뢰할 수 있는 증명의 경우 호스트가 정상 상태 인지 확인 하는 정책 (신뢰할 수 있는 신뢰할 수 있는 보안 그룹의 멤버 자격)이 하나 뿐입니다.
TPM 증명은 더 복잡 하며, 시스템의 코드 및 구성을 측정 하는 다양 한 정책을 포함 하 여 시스템의 상태가 정상 인지 확인 합니다.

단일 HGS는 Active Directory 및 TPM 정책 모두를 사용 하 여 한 번에 구성할 수 있지만 서비스는 호스트가 증명을 시도할 때 구성 된 현재 모드의 정책만 확인 합니다.
HGS 서버의 모드를 확인 하려면 `Get-HgsServer`를 실행 합니다.

### <a name="default-policies"></a>기본 정책
TPM에서 신뢰할 수 있는 증명의 경우 HGS에 구성 된 몇 가지 기본 제공 정책이 있습니다.
이러한 정책 중 일부는 "잠김" 이며, 보안상의 이유로 사용 하지 않도록 설정할 수 없습니다.
아래 표에서는 각 기본 정책의 용도에 대해 설명 합니다.

정책 이름                    | 용도
-------------------------------|-----------------------------------------------------
Hgs_SecureBootEnabled          | 호스트에서 보안 부팅이 사용 하도록 설정 되어 있어야 합니다. 이는 시작 이진 파일 및 기타 UEFI 잠금 설정을 측정 하는 데 필요 합니다.
Hgs_UefiDebugDisabled          | 호스트에서 커널 디버거를 사용 하도록 설정 하지 않았는지 확인 합니다. 사용자 모드 디버거는 코드 무결성 정책에 의해 차단 됩니다.
Hgs_SecureBootSettings         | 호스트가 하나 이상의 (관리자 정의) TPM 기준선과 일치 하는지 확인 하는 부정 정책입니다.
Hgs_CiPolicy                   | 호스트가 관리자 정의 CI 정책 중 하나를 사용 하 고 있는지 확인 하는 부정 정책입니다.
Hgs_HypervisorEnforcedCiPolicy | 하이퍼바이저에서 코드 무결성 정책을 적용 해야 합니다. 이 정책을 사용 하지 않도록 설정 하면 커널 모드 코드 무결성 정책 공격 으로부터 보호를 weakens.
Hgs_FullBoot                   | 호스트를 절전 모드 또는 최대 절전 모드에서 다시 시작 하지 않았는지 확인 합니다. 이 정책을 통과 하려면 호스트를 올바르게 다시 시작 하거나 종료 해야 합니다.
Hgs_VsmIdkPresent              | 호스트에서 실행 되는 가상화 기반 보안이 필요 합니다. IDK는 호스트의 보안 메모리 공간으로 다시 전송 된 정보를 암호화 하는 데 필요한 키를 나타냅니다.
Hgs_PageFileEncryptionEnabled  | 호스트에서 암호화 해야 하는 탭이 필요 합니다. 이 정책을 사용 하지 않도록 설정 하면 테 넌 트 암호에 대해 암호화 되지 않은 페이지 파일을 검사할 경우 정보가 노출 될 수 있습니다.
Hgs_BitLockerEnabled           | Hyper-v 호스트에서 BitLocker를 사용 하도록 설정 해야 합니다. 이 정책은 성능상의 이유로 기본적으로 사용 하지 않도록 설정 되어 있으므로 사용 하지 않는 것이 좋습니다. 이 정책은 보호 된 Vm 자체의 암호화에 영향을 미치지 않습니다.
Hgs_IommuEnabled               | 직접 메모리 액세스 공격을 방지 하기 위해 호스트에 IOMMU 장치가 사용 되어야 합니다. 이 정책을 사용 하지 않도록 설정 하 고 IOMMU를 사용 하지 않는 호스트를 사용 하면 테 넌 트 VM 암호를 노출 하 여 메모리 공격을 직접
Hgs_NoHibernation              | Hyper-v 호스트에서 최대 절전 모드를 사용 하지 않도록 설정 해야 합니다. 이 정책을 사용 하지 않도록 설정 하면 호스트가 보호 된 VM 메모리를 암호화 되지 않은 최대 절전 모드 파일에 저장할 수 있습니다.
Hgs_NoDumps                    | Hyper-v 호스트에서 메모리 덤프를 사용 하지 않도록 설정 해야 합니다. 이 정책을 사용 하지 않도록 설정 하는 경우 보호 된 VM 메모리가 암호화 되지 않은 크래시 덤프 파일에 저장 되지 않도록 덤프 암호화를 구성 하는 것이 좋습니다.
Hgs_DumpEncryption             | Hyper-v 호스트에서 사용 하도록 설정 된 경우 HGS에서 신뢰 하는 암호화 키를 사용 하 여 암호화 하려면 메모리 덤프가 필요 합니다. 호스트에서 덤프가 사용 되지 않는 경우에는이 정책이 적용 되지 않습니다. 이 정책과 *Hgs\_nodumps* 모두 사용 하지 않도록 설정 된 경우 보호 된 VM 메모리를 암호화 되지 않은 덤프 파일에 저장할 수 있습니다.
Hgs_DumpEncryptionKey          | 메모리 덤프를 허용 하도록 구성 된 호스트가 HGS에 알려진 관리 정의 덤프 파일 암호화 키를 사용 하도록 하는 부정 정책입니다. 이 정책은 *Hgs\_암호화* 되지 않은 암호화를 사용 하지 않도록 설정한 경우에는 적용 되지 않습니다.

### <a name="authorizing-new-guarded-hosts"></a>새 보호 된 호스트 권한 부여
새 호스트가 보호 된 호스트가 될 수 있는 권한을 부여 하려면 (예: 증명 성공), HGS는 호스트를 신뢰 하 고 (TPM에서 신뢰할 수 있는 증명을 사용 하도록 구성 된 경우) 해당 소프트웨어에서 실행 되는 소프트웨어를 신뢰 해야 합니다.
새 호스트에 권한을 부여 하는 단계는 현재 HGS가 구성 된 증명 모드에 따라 다릅니다.
보호 된 패브릭에 대 한 증명 모드를 확인 하려면 모든 HGS 노드에서 `Get-HgsServer`를 실행 합니다.

#### <a name="software-configuration"></a>소프트웨어 구성
새 Hyper-v 호스트에서 Windows Server 2016 Datacenter edition이 설치 되어 있는지 확인 합니다.
Windows Server 2016 Standard는 보호 된 패브릭에서 보호 된 Vm을 실행할 수 없습니다.
호스트는 데스크톱 경험 또는 Server Core를 설치할 수 있습니다.

데스크톱 환경 및 Server Core가 설치 된 서버에서 Hyper-v 및 호스트 보호 Hyper-v 지원 서버 역할을 설치 해야 합니다.

```powershell
Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
```

#### <a name="admin-trusted-attestation"></a>관리자가 신뢰할 수 있는 증명
관리자가 신뢰할 수 있는 증명을 사용할 때 HGS에 새 호스트를 등록 하려면 먼저 해당 호스트를 가입 된 도메인의 보안 그룹에 추가 해야 합니다.
일반적으로 각 도메인에는 보호 된 호스트에 대 한 보안 그룹이 하나 있습니다.
해당 그룹을 HGS에 이미 등록 한 경우에는 호스트를 다시 시작 하 여 그룹 구성원 자격을 새로 고치는 작업만 수행 하면 됩니다.

다음 명령을 실행 하 여 HGS에서 신뢰 하는 보안 그룹을 확인할 수 있습니다.

```powershell
Get-HgsAttestationHostGroup
```

새 보안 그룹을 HGS에 등록 하려면 먼저 호스트의 도메인에 있는 그룹의 SID (보안 식별자)를 캡처하고 해당 SID를 HGS에 등록 합니다.

```powershell
Add-HgsAttestationHostGroup -Name "Contoso Guarded Hosts" -Identifier "S-1-5-21-3623811015-3361044348-30300820-1013"
```

호스트 도메인과 HGS 간에 트러스트를 설정 하는 방법에 대 한 지침은 배포 가이드에서 확인할 수 있습니다.

#### <a name="tpm-trusted-attestation"></a>TPM에서 신뢰할 수 있는 증명
HGS가 TPM 모드로 구성 된 경우 호스트는 "Hgs_" 접두사가 붙은 모든 잠긴 정책 및 "사용" 정책 뿐만 아니라 하나 이상의 TPM 기준, TPM 식별자 및 코드 무결성 정책을 전달 해야 합니다.
새 호스트를 추가할 때마다 새 TPM id를 HGS에 등록 해야 합니다.
호스트에서 동일한 소프트웨어를 실행 중이 고 (동일한 코드 무결성 정책이 적용 된 경우) TPM 기준이 사용자 환경의 다른 호스트인 경우에는 새 CI 정책 또는 기준을 추가할 필요가 없습니다.

**새 호스트에 대 한 TPM 식별자 추가** 새 호스트에서 다음 명령을 실행 하 여 TPM 식별자를 캡처합니다.
HGS에서 조회 하는 데 도움이 되는 호스트의 고유한 이름을 지정 해야 합니다.
호스트를 서비스 해제 하거나 HGS에서 보호 된 Vm을 실행 하지 않도록 하려면이 정보가 필요 합니다.

```powershell
(Get-PlatformIdentifier -Name "Host01").InnerXml | Out-File C:\temp\host01.xml -Encoding UTF8
```

이 파일을 HGS 서버에 복사한 후 다음 명령을 실행 하 여 HGS에 호스트를 등록 합니다.

```powershell
Add-HgsAttestationTpmHost -Name 'Host01' -Path C:\temp\host01.xml
```

**새 TPM 기준 추가** 새 호스트에서 사용자 환경에 대 한 새 하드웨어 또는 펌웨어 구성을 실행 하는 경우 새 TPM 기준을 사용 해야 할 수 있습니다.
이렇게 하려면 호스트에서 다음 명령을 실행 합니다.

```powershell
Get-HgsAttestationBaselinePolicy -Path 'C:\temp\hardwareConfig01.tcglog'
```

> [!NOTE]
> 호스트가 유효성 검사에 실패 하 고 성공적으로 증명 되지 않는다는 오류가 표시 되 면 걱정 하지 마세요.
> 이는 호스트가 보호 된 Vm을 실행할 수 있는지 확인 하기 위한 필수 구성 요소 확인 이며, 코드 무결성 정책 또는 기타 필수 설정이 아직 적용 되지 않았음을 의미 합니다.
> 오류 메시지를 읽고,이를 통해 권장 사항을 변경한 후 다시 시도 하십시오.
> 또는 명령에 `-SkipValidation` 플래그를 추가 하 여 유효성 검사를 건너뛸 수 있습니다.

TPM 기준을 HGS 서버에 복사한 후 다음 명령을 사용 하 여 등록 합니다.
이 종류의 Hyper-v 호스트에 대 한 하드웨어 및 펌웨어 구성을 이해 하는 데 도움이 되는 명명 규칙을 사용 하는 것이 좋습니다.

```powershell
Add-HgsAttestationTpmPolicy -Name 'HardwareConfig01' -Path 'C:\temp\hardwareConfig01.tcglog'
```

**새 코드 무결성 정책 추가** Hyper-v 호스트에서 실행 되는 코드 무결성 정책을 변경한 경우 해당 호스트가 성공적으로 증명 하려면 먼저 HGS에 새 정책을 등록 해야 합니다.
사용자 환경에서 신뢰할 수 있는 Hyper-v 컴퓨터의 마스터 이미지 역할을 하는 참조 호스트에서 `New-CIPolicy` 명령을 사용 하 여 새 CI 정책을 캡처합니다.
Hyper-v 호스트 CI 정책에는 **Filepublisher** 수준 및 **해시** 대체를 사용 하는 것이 좋습니다.
먼저 감사 모드에서 CI 정책을 만들어 모든 것이 예상 대로 작동 하는지 확인 해야 합니다.
시스템에서 샘플 작업의 유효성을 검사 한 후에는 정책을 적용 하 고 적용 된 버전을 HGS에 복사할 수 있습니다.
코드 무결성 정책 구성 옵션의 전체 목록은 [Device Guard 설명서](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies)를 참조 하세요.

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

정책을 만들어 테스트 하 고 적용 한 후에는 이진 파일 (.p7b)을 HGS 서버에 복사 하 고 정책을 등록 합니다.

```powershell
Add-HgsAttestationCiPolicy -Name 'WS2016-Hardware01' -Path 'C:\temp\ws2016-hardware01-ci.p7b'
```

**메모리 덤프 암호화 키 추가**

*Hgs\_NoDumps* 정책을 사용 하지 않도록 설정 하 고 *hgs\_암호화* 되지 않은 암호화 정책을 사용 하는 경우 보호 된 호스트는 덤프를 암호화 하는 동안 메모리 덤프 (크래시 덤프 포함)를 사용할 수 있습니다. 보호 된 호스트는 메모리 덤프를 사용할 수 없거나 HGS에 알려진 키를 사용 하 여 암호화 하는 경우에만 증명을 전달 합니다. 기본적으로 HGS에는 덤프 암호화 키가 구성 되어 있지 않습니다.

HGS에 덤프 암호화 키를 추가 하려면 `Add-HgsAttestationDumpPolicy` cmdlet을 사용 하 여 HGS에 덤프 암호화 키의 해시를 제공 합니다.
덤프 암호화를 사용 하 여 구성 된 Hyper-v 호스트에서 TPM 기준선을 캡처하면 해시가 tcglog에 포함 되 고 `Add-HgsAttestationDumpPolicy` cmdlet에 제공 될 수 있습니다.

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey01' -Path 'C:\temp\TpmBaselineWithDumpEncryptionKey.tcglog'
```

또는 해시에 대 한 문자열 표현을 cmdlet에 직접 제공할 수 있습니다.

```powershell
Add-HgsAttestationDumpPolicy -Name 'DumpEncryptionKey02' -PublicKeyHash '<paste your hash here>'
```

보호 된 패브릭에서 다른 키를 사용 하도록 선택 하는 경우 각 고유 덤프 암호화 키를 HGS에 추가 해야 합니다.
HGS에 알려지지 않은 키를 사용 하 여 메모리 덤프를 암호화 하는 호스트는 증명을 전달 하지 않습니다.

[호스트에서 덤프 암호화를 구성](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)하는 방법에 대 한 자세한 내용은 hyper-v 설명서를 참조 하십시오.

#### <a name="check-if-the-system-passed-attestation"></a>시스템이 증명을 통과 했는지 확인 합니다.
필요한 정보를 HGS에 등록 한 후 호스트가 증명을 전달 하는지 확인 해야 합니다.
새로 추가 된 Hyper-v 호스트에서 `Set-HgsClientConfiguration`를 실행 하 고 HGS 클러스터에 올바른 Url을 제공 합니다.
이러한 Url은 모든 HGS 노드에서 `Get-HgsServer`를 실행 하 여 가져올 수 있습니다.

```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'http://hgs.bastion.local/KeyProtection' -AttestationServerUrl 'http://hgs.bastion.local/Attestation'
```

결과 상태가 "IsHostGuarded: True"를 나타내지 않으면 구성 문제를 해결 해야 합니다.
증명에 실패 한 호스트에서 다음 명령을 실행 하 여 실패 한 증명을 해결 하는 데 도움이 될 수 있는 문제에 대 한 자세한 보고서를 가져옵니다.

```powershell
Get-HgsTrace -RunDiagnostics -Detailed
```

> [!IMPORTANT]
> Windows Server 2019 또는 Windows 10 버전 1809을 사용 중이 고 코드 무결성 정책을 사용 하는 경우 `Get-HgsTrace` **코드 무결성 정책 활성** 진단에 대 한 오류를 반환할 수 있습니다.
> 오류가 유일한 진단 인 경우에는이 결과를 무시 해도 안전 합니다.

### <a name="review-attestation-policies"></a>증명 정책 검토
HGS에 구성 된 정책의 현재 상태를 검토 하려면 모든 HGS 노드에서 다음 명령을 실행 합니다.

```powershell
# List all trusted security groups for admin-trusted attestation
Get-HgsAttestationHostGroup

# List all policies configured for TPM-trusted attestation
Get-HgsAttestationPolicy
```

더 이상 보안 요구 사항 (예: 안전 하지 않은 것으로 간주 되는 이전 코드 무결성 정책)을 충족 하지 않는 정책을 사용 하도록 설정한 경우 다음 명령에서 정책의 이름을 바꿔서 사용 하지 않도록 설정할 수 있습니다.

```powershell
Disable-HgsAttestationPolicy -Name 'PolicyName'
```

마찬가지로 `Enable-HgsAttestationPolicy`를 사용 하 여 정책을 다시 사용 하도록 설정할 수 있습니다.

더 이상 정책을 필요로 하지 않고 모든 HGS 노드에서 제거 하려는 경우 `Remove-HgsAttestationPolicy -Name 'PolicyName'`를 실행 하 여 정책을 영구적으로 삭제 합니다.

## <a name="changing-attestation-modes"></a>증명 모드 변경
관리자가 신뢰할 수 있는 증명을 사용 하 여 보호 된 패브릭을 시작한 경우 사용자 환경에 TPM 2.0 호환 호스트를 충분히 확보 하는 즉시 더 강력한 TPM 증명 모드로 업그레이드할 가능성이 높습니다.
전환할 준비가 되 면 관리자가 신뢰할 수 있는 증명을 사용 하 여 HGS를 계속 실행 하면서 HGS에서 모든 증명 아티팩트 (CI 정책, TPM 기준 및 TPM 식별자)를 미리 로드할 수 있습니다.
이렇게 하려면 [새 보호 된 호스트에 권한 부여](#authorizing-new-guarded-hosts) 섹션의 지침을 따르세요.

모든 정책을 HGS에 추가 하면 다음 단계는 호스트에서 가상 증명 시도를 실행 하 여 TPM 모드로 증명을 전달 하는지 확인 하는 것입니다.
이는 HGS의 현재 작동 상태에 영향을 주지 않습니다.
환경의 모든 호스트에 대 한 액세스 권한이 있는 컴퓨터 및 하나 이상의 HGS 노드에 대 한 액세스 권한이 있는 컴퓨터에서 아래 명령을 실행 해야 합니다.
방화벽이 나 기타 보안 정책에서이를 방지 하는 경우이 단계를 건너뛸 수 있습니다.
가능 하면 가상 증명을 실행 하 여 TPM 모드로 "전환" 하면 Vm 가동 중지 시간이 발생 하는지 여부를 확인 하는 것이 좋습니다. 

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

진단이 완료 되 면 출력 된 정보를 검토 하 여 TPM 모드의 증명에 오류가 발생 했는지 확인 합니다.
각 호스트에서 "통과"를 받을 때까지 진단을 다시 실행 한 다음, HGS를 TPM 모드로 변경 합니다.

**TPM 모드로 변경** 하는 작업은 완료 하는 데 1 초 밖에 걸리지 않습니다.
모든 HGS 노드에서 다음 명령을 실행 하 여 증명 모드를 업데이트 합니다.

```powershell
Set-HgsServer -TrustTpm
```

문제가 발생 하 여 Active Directory 모드로 다시 전환 해야 하는 경우 `Set-HgsServer -TrustActiveDirectory`를 실행 하 여이 작업을 수행할 수 있습니다.

모든 것이 예상 대로 작동 하는지 확인 한 후에는 모든 신뢰할 수 있는 Active Directory 호스트 그룹을 HGS에서 제거 하 고 HGS와 패브릭 도메인 간의 트러스트를 제거 해야 합니다.
Active Directory 신뢰를 그대로 유지 하는 경우 누군가가 트러스트를 다시 사용 하도록 설정 하 고 Active Directory 모드로 전환 하 여 보호 된 호스트에서 신뢰할 수 없는 코드가 실행 되지 않도록 할 수 있습니다.

## <a name="key-management"></a>키 관리
보호 된 패브릭 솔루션은 여러 공개/개인 키 쌍을 사용 하 여 솔루션에 있는 다양 한 구성 요소의 무결성을 확인 하 고 테 넌 트 암호를 암호화 합니다.
호스트 보호자 서비스는 보호 된 Vm을 시작 하는 데 사용 되는 키를 서명 및 암호화 하는 데 사용 되는 두 개 이상의 인증서 (공개 키 및 개인 키 포함)로 구성 됩니다.
이러한 키는 신중 하 게 관리 해야 합니다.
악의적 사용자가 개인 키를 획득 하는 경우 패브릭에서 실행 되는 모든 Vm을 보호 하거나 더 약한 증명 정책을 사용 하는 가짜 HGS 클러스터를 설정 하 여 현재 위치에서 사용 하는 보호를 우회할 수 있습니다.
재해 중에 개인 키를 손실 하 고 백업에서 찾을 수 없는 경우 새 키 쌍을 설정 하 고 각 VM이 새 인증서에 대 한 권한을 부여 하도록 키를 다시 지정 해야 합니다.

이 섹션에서는 기능 및 보안을 위해 키를 구성 하는 데 도움이 되는 일반적인 키 관리 항목에 대해 설명 합니다.

### <a name="adding-new-keys"></a>새 키 추가
HGS는 키 집합 하나를 사용 하 여 초기화 해야 하지만 둘 이상의 암호화 및 서명 키를 HGS에 추가할 수 있습니다.
HGS에 새 키를 추가 하는 가장 일반적인 두 가지 이유는 다음과 같습니다.
1. 테 넌 트가 자신의 개인 키를 하드웨어 보안 모듈에 복사 하 고 해당 키로 보호 된 Vm을 시작 하도록 권한을 부여 하는 "고유 키 가져오기" 시나리오를 지원 합니다.
2. 각 VM 구성이 새 키를 사용 하도록 업데이트 될 때까지 먼저 새 키를 추가 하 고 두 키 집합을 유지 하 여 HGS의 기존 키를 대체 합니다.

새 키를 추가 하는 프로세스는 사용 하는 인증서의 유형에 따라 달라 집니다.

**옵션 1: HSM에 저장 된 인증서 추가**

HGS 키를 보호 하는 데 권장 되는 방법은 HSM (하드웨어 보안 모듈)에서 만든 인증서를 사용 하는 것입니다.
Hsm을 사용 하 여 키 사용은 데이터 센터의 보안에 민감한 장치에 물리적으로 액세스할 수 있습니다.
각 HSM은 서로 다르며 인증서를 만들어 HGS에 등록 하는 고유한 프로세스를 포함 합니다.
아래 단계는 HSM 지원 인증서를 사용 하기 위한 대략적인 지침을 제공 하기 위한 것입니다.
정확한 단계와 기능에 대 한 자세한 내용은 HSM 공급 업체의 설명서를 참조 하세요.

1. 클러스터의 각 HGS 노드에 HSM 소프트웨어를 설치 합니다. 네트워크 또는 로컬 HSM 장치가 있는지 여부에 따라 컴퓨터에 키 저장소에 대 한 액세스 권한을 부여 하도록 HSM을 구성 해야 할 수 있습니다.
2. 암호화 및 서명에 **2048 비트 RSA 키** 를 사용 하 여 HSM에서 2 개의 인증서를 만듭니다.
    1. HSM에서 **데이터** 암호화 키 사용 속성을 사용 하 여 암호화 인증서 만들기
    2. HSM에서 **디지털 서명** 키 사용 속성을 사용 하 여 서명 인증서 만들기
3. HSM 공급 업체의 지침에 따라 각 HGS 노드의 로컬 인증서 저장소에 인증서를 설치 합니다.
4. HSM이 세분화 된 사용 권한을 사용 하 여 개인 키를 사용할 수 있는 특정 응용 프로그램 또는 사용자 권한을 부여 하는 경우, 인증서에 대 한 HGS 그룹 관리 서비스 계정 액세스 권한을 부여 해야 합니다. `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`를 실행 하 여 HGS gMSA 계정의 이름을 찾을 수 있습니다.
5. 다음 명령에서 지문을 인증서의 인증서로 바꿔서 HGS에 서명 및 암호화 인증서를 추가 합니다.

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA"
    ```

**옵션 2: 내보낼 수 없는 소프트웨어 인증서 추가**

회사 또는 공용 인증 기관에서 발급 한 소프트웨어 지원 인증서를 내보낼 수 없는 개인 키가 있는 경우 해당 지문을 사용 하 여 HGS에 인증서를 추가 해야 합니다.
1. 인증 기관의 지침에 따라 컴퓨터에 인증서를 설치 합니다.
2. HGS 그룹 관리 서비스 계정에 인증서의 개인 키에 대 한 읽기 액세스 권한을 부여 합니다. `(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName`를 실행 하 여 HGS gMSA 계정의 이름을 찾을 수 있습니다.
3. 다음 명령을 사용 하 여 인증서를 HGS에 등록 하 고 인증서의 지문 (서명 인증서에 대 한 *서명* *변경)을 대체* 합니다.

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899"
    ```

> [!IMPORTANT]
> 개인 키를 수동으로 설치 하 고 각 HGS 노드의 gMSA 계정에 대 한 읽기 권한을 부여 해야 합니다.
> HGS는 해당 지 문으로 등록 된 *모든* 인증서에 대 한 개인 키를 자동으로 복제할 수 없습니다.

**옵션 3: PFX 파일에 저장 된 인증서 추가**

PFX 파일 형식으로 저장 하 고 암호로 보호할 수 있는 내보내기 가능한 개인 키가 포함 된 소프트웨어 지원 인증서가 있는 경우 HGS는 자동으로 인증서를 관리할 수 있습니다.
PFX 파일을 사용 하 여 추가한 인증서는 HGS 클러스터의 모든 노드에 자동으로 복제 되 고, HGS는 개인 키에 대 한 액세스를 보호 합니다.
PFX 파일을 사용 하 여 새 인증서를 추가 하려면 모든 HGS 노드에서 다음 명령을 실행 합니다 (서명 인증서에 *서명* 하도록 *암호화* 변경).

```powershell
$certPassword = Read-Host -AsSecureString -Prompt "Provide the PFX file password"
Add-HgsKeyProtectionCertificate -CertificateType Encryption -CertificatePath "C:\temp\encryptionCert.pfx" -CertificatePassword $certPassword
```

**기본 인증서 식별 및 변경** HGS는 여러 서명 및 암호화 인증서를 지원할 수 있지만 하나의 쌍을 "기본" 인증서로 사용 합니다.
사용자가 해당 HGS 클러스터에 대 한 보호자 메타 데이터를 다운로드 하는 경우 사용 되는 인증서입니다.
현재 기본 인증서로 표시 된 인증서를 확인 하려면 다음 명령을 실행 합니다.

```powershell
Get-HgsKeyProtectionCertificate -IsPrimary $true
```

새 기본 암호화 또는 서명 인증서를 설정 하려면 원하는 인증서의 지문을 찾고 다음 명령을 사용 하 여 기본으로 표시 합니다.

```powershell
Get-HgsKeyProtectionCertificate
Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint "AABBCCDDEEFF00112233445566778899" -IsPrimary
Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint "99887766554433221100FFEEDDCCBBAA" -IsPrimary
```

### <a name="renewing-or-replacing-keys"></a>키 갱신 또는 바꾸기
HGS에서 사용 하는 인증서를 만들 때 인증서에는 인증 기관의 정책 및 요청 정보에 따라 만료 날짜가 할당 됩니다.
일반적으로 인증서의 유효성이 HTTP 통신 보안과 같은 중요 한 시나리오에서는 서비스 중단 또는 worrisome 오류 메시지를 방지 하기 위해 인증서가 만료 되기 전에 인증서를 갱신 해야 합니다.
HGS는 이러한 점에서 인증서를 사용 하지 않습니다.
HGS는 단순히 비대칭 키 쌍을 만들고 저장 하는 편리한 방법으로 인증서를 사용 합니다.
HGS의 만료 된 암호화 또는 서명 인증서는 보호 된 Vm에 대 한 보호의 약점 또는 손실을 나타내지는 않습니다.
또한 인증서 해지 검사는 HGS에 의해 수행 되지 않습니다.
HGS 인증서 또는 발급 기관의 인증서가 해지 된 경우 HGS의 인증서 사용에 영향을 주지 않습니다.

사용자가 개인 키를 도난당 했다고 판단 하는 이유가 있는 경우에만 HGS 인증서에 대해 걱정 해야 합니다.
이 경우에는 보호 된 Vm의 무결성이 위험에 노출 됩니다 .이 경우 HGS 암호화 및 서명 키 쌍의 사설 절반을 소유 하면 VM의 보호 보호를 제거 하거나 더 약한 증명 정책이 있는 가짜 HGS 서버를 강화할 수 있기 때문입니다.

이러한 상황에서 자신을 찾거나 규정 준수 표준에서 인증서 키를 정기적으로 새로 고쳐야 하는 경우 다음 단계에서는 HGS 서버에서 키를 변경 하는 프로세스를 간략하게 설명 합니다.
다음 지침은 HGS 클러스터에서 제공 하는 각 VM에 대 한 서비스 중단을 초래 하는 중요 한 정보를 나타냅니다.
서비스 중단을 최소화 하 고 테 넌 트 Vm의 보안을 보장 하려면 HGS 키를 적절 하 게 변경 해야 합니다.

HGS 노드에서 다음 단계를 수행 하 여 새 쌍의 암호화 및 서명 인증서를 등록 합니다.
새 키를 [추가](#adding-new-keys) 하는 방법에 대 한 자세한 내용은 HGS에 새 키를 추가 하는 방법을 참조 하세요.
1. HGS 서버에 대 한 암호화 및 서명 인증서의 새 쌍을 만듭니다. 하드웨어 보안 모듈에 생성 되는 것이 이상적입니다.
2. **HgsKeyProtectionCertificate** 를 사용 하 여 새 암호화 및 서명 인증서 등록

    ```powershell
    Add-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>
    Add-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>
    ```
3. 지문을 사용한 경우 개인 키를 설치 하 고 HGS gMSA 액세스를 키에 부여 하려면 클러스터의 각 노드로 이동 해야 합니다.
4. 새 인증서를 HGS의 기본 인증서로 설정

    ```powershell
    Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsPrimary
    Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsPrimary
    ```

이 시점에서, HGS 노드에서 얻은 메타 데이터로 만든 차폐 데이터는 새 인증서를 사용 하지만 기존 Vm은 계속 해 서 이전 인증서가 있기 때문에 계속 작동 합니다.
모든 기존 Vm이 새 키를 사용 하도록 하려면 각 VM에서 키 보호기를 업데이트 해야 합니다.
이는 VM 소유자 ("소유자" 보호자를 소유 하는 사람 또는 엔터티)가 관련 된 작업입니다.
보호 된 각 VM에 대해 다음 단계를 수행 합니다.
5. VM을 종료 합니다. 나머지 단계가 완료 될 때까지 VM을 다시 켤 수 없습니다. 그렇지 않으면 프로세스를 다시 시작 해야 합니다.
6. 현재 키 보호기를 파일에 저장 합니다. `Get-VMKeyProtector -VMName 'VM001' | Out-File '.\VM001.kp'`
7. VM 소유자에 게 KP 전송
8. 소유자가 HGS에서 업데이트 된 보호자 정보를 다운로드 하 고 로컬 시스템에서 가져옵니다.
9. 현재 KP를 메모리로 읽어 다음 명령을 실행 하 여 새 보호자에 게 KP에 대 한 액세스 권한을 부여 하 고 새 파일에 저장 합니다.

    ```powershell
    $kpraw = Get-Content -Path .\VM001.kp
    $kp = ConvertTo-HgsKeyProtector -Bytes $kpraw
    $newGuardian = Get-HgsGuardian -Name 'UpdatedHgsGuardian'
    $updatedKP = Grant-HgsKeyProtectorAccess -KeyProtector $kp -Guardian $newGuardian
    $updatedKP.RawData | Out-File .\updatedVM001.kp
    ```
10. 업데이트 된 KP를 다시 호스팅 패브릭에 복사
11. 원본 VM에 KP를 적용 합니다.

   ```powershell
   $updatedKP = Get-Content -Path .\updatedVM001.kp
   Set-VMKeyProtector -VMName VM001 -KeyProtector $updatedKP
   ```
12. 마지막으로 VM을 시작 하 고 성공적으로 실행 되는지 확인 합니다.

> [!NOTE]
> Vm 소유자가 vm에서 잘못 된 키 보호기를 설정 하 고 패브릭에서 VM을 실행할 수 있는 권한을 부여 하지 않는 경우 보호 된 VM을 시작할 수 없습니다.
> 마지막으로 알려진 좋은 키 보호기로 돌아가려면 `Set-VMKeyProtector -RestoreLastKnownGoodKeyProtector`를 실행 합니다.

새 보호자 키에 대 한 권한을 부여 하도록 모든 Vm을 업데이트 한 후에는 이전 키를 사용 하지 않도록 설정 하 고 제거할 수 있습니다.

13. `Get-HgsKeyProtectionCertificate -IsPrimary $false`에서 이전 인증서의 지문을 가져옵니다.

14. 다음 명령을 실행 하 여 각 인증서를 사용 하지 않도록 설정 합니다.  

   ```powershell
   Set-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint> -IsEnabled $false
   Set-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint> -IsEnabled $false
   ```

15. 인증서가 사용 하지 않도록 설정 된 상태에서 Vm을 시작할 수 있는지 확인 한 후 다음 명령을 실행 하 여 HGS에서 인증서를 제거 합니다.

   ```powershell
   Remove-HgsKeyProtectionCertificate -CertificateType Signing -Thumbprint <Thumbprint>`
   Remove-HgsKeyProtectionCertificate -CertificateType Encryption -Thumbprint <Thumbprint>`
   ```

> [!IMPORTANT]
> VM 백업은 이전 인증서를 사용 하 여 VM을 시작할 수 있도록 하는 이전 키 보호기 정보를 포함 합니다.
> 개인 키가 손상 된 것을 알고 있는 경우에는 VM 백업이 손상 될 수 있으며 적절 한 조치를 취할 수 있습니다.
> 백업 (vmcx)에서 VM 구성을 제거 하면 다음에 BitLocker 복구 암호를 사용 하 여 VM을 부팅 하는 데 필요한 비용으로 키 보호기가 제거 됩니다.

### <a name="key-replication-between-nodes"></a>노드 간 키 복제
HGS 클러스터의 모든 노드는 동일한 암호화, 서명 및 SSL 인증서 (구성 된 경우)를 사용 하 여 구성 해야 합니다.
이는 클러스터의 모든 노드에 대 한 Hyper-v 호스트의 요청이 성공적으로 처리 될 수 있도록 하기 위해 필요 합니다.

**PFX 기반 인증서를 사용 하 여 hgs 서버를 초기화 한 경우** hgs는 클러스터의 모든 노드에서 해당 인증서의 공개 키와 개인 키를 모두 자동으로 복제 합니다.
한 노드에 키를 추가 하기만 하면 됩니다.

**인증서 참조 또는 지문을 사용 하 여 hgs 서버를 초기화 한 경우** hgs는 인증서의 *공개* 키만 각 노드에 복제 합니다.
또한이 시나리오에서는 HGS가 모든 노드에서 개인 키에 대 한 액세스 권한을 자신에 게 부여할 수 없습니다.
따라서 다음 작업을 수행 해야 합니다.
1. 각 HGS 노드에 개인 키 설치
2. 각 노드에서 개인 키에 대 한 HGS 그룹 관리 서비스 계정 (gMSA) 액세스 권한을 부여 합니다. 이러한 작업은 작업 부담을 더 추가 하지만 HSM 지원 키와 내보낼 수 없는 개인 키가 있는 인증서에 필요 합니다.

**SSL 인증서** 는 어떠한 형식으로도 복제 되지 않습니다.
SSL 인증서를 갱신 하거나 바꾸도록 선택할 때마다 동일한 SSL 인증서를 사용 하 여 각 HGS 서버를 초기화 하 고 각 서버를 업데이트 하는 것은 사용자의 책임입니다.
SSL 인증서를 교체할 때 [HgsServer](https://technet.microsoft.com/library/mt652180.aspx) cmdlet을 사용 하 여이 작업을 수행 하는 것이 좋습니다.

## <a name="unconfiguring-hgs"></a>구성 취소 HGS

HGS 서버를 서비스 해제 하거나 크게 다시 구성 해야 하는 경우 [HgsServer](https://technet.microsoft.com/library/mt652176.aspx) 또는 [HgsServer](https://technet.microsoft.com/library/mt652182.aspx) cmdlet을 사용 하 여이 작업을 수행할 수 있습니다.

### <a name="clearing-the-hgs-configuration"></a>HGS 구성 지우기

HGS 클러스터에서 노드를 제거 하려면 [HgsServer](https://technet.microsoft.com/library/mt652176.aspx) cmdlet을 사용 합니다.
이 cmdlet은 실행 되는 서버에서 다음과 같이 변경 합니다.

- 증명 및 키 보호 서비스 등록 취소
- "Microsoft. w i n. w i n. w i n" JEA 관리 끝점을 제거
- HGS 장애 조치 (failover) 클러스터에서 로컬 컴퓨터를 제거 합니다.

서버가 클러스터의 마지막 HGS 노드인 경우 클러스터와 해당 분산 네트워크 이름 리소스도 제거 됩니다.

```powershell
# Removes the local computer from the HGS cluster
Clear-HgsServer
```

지우기 작업이 완료 된 후에는 [HgsServer](https://technet.microsoft.com/library/mt652185.aspx)를 사용 하 여 HGS 서버를 다시 초기화할 수 있습니다.
[HgsServer](https://technet.microsoft.com/library/mt652169.aspx) 를 사용 하 여 Active Directory Domain Services 도메인을 설정 하는 경우 해당 도메인은 지우기 작업 후 구성 및 작동 상태로 유지 됩니다.

### <a name="uninstalling-hgs"></a>HGS 제거

HGS 클러스터에서 노드를 제거 하 **고** 해당 노드에서 실행 중인 Active Directory 도메인 컨트롤러의 수준을 내리려면 [HgsServer](https://technet.microsoft.com/library/mt652182.aspx) cmdlet을 사용 합니다.
이 cmdlet은 실행 되는 서버에서 다음과 같이 변경 합니다.

- 증명 및 키 보호 서비스 등록 취소
- "Microsoft. w i n. w i n. w i n" JEA 관리 끝점을 제거
- HGS 장애 조치 (failover) 클러스터에서 로컬 컴퓨터를 제거 합니다.
- 구성 된 경우 Active Directory 도메인 컨트롤러의 수준을 내립니다.

서버가 클러스터의 마지막 HGS 노드인 경우에도 도메인, 장애 조치 (failover) 클러스터 및 클러스터의 분산 네트워크 이름 리소스가 제거 됩니다.

```powershell
# Removes the local computer from the HGS cluster and demotes the ADDC (restart required)
$newLocalAdminPassword = Read-Host -AsSecureString -Prompt "Enter a new password for the local administrator account"
Uninstall-HgsServer -LocalAdministratorPassword $newLocalAdminPassword -Restart
```

제거 작업이 완료 되 고 컴퓨터가 다시 시작 되 면 [HgsServer](https://technet.microsoft.com/library/mt652169.aspx) 를 사용 하 여 addc 및 hgs를 다시 설치 하거나 컴퓨터를 도메인에 가입 하 고 [HgsServer](https://technet.microsoft.com/library/mt652185.aspx)를 사용 하 여 해당 도메인의 HGS 서버를 초기화할 수 있습니다.

컴퓨터를 HGS 노드로 더 이상 사용 하지 않으려는 경우 Windows에서 역할을 제거할 수 있습니다.

```powershell
Uninstall-WindowsFeature HostGuardianServiceRole
```
