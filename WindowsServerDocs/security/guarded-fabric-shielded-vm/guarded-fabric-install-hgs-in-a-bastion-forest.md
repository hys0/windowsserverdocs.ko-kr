---
title: 기존 요새 포리스트에 HGS 설치
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5c503331893dbea65c99d79eb7444893d5f3b657
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403592"
---
# <a name="install-hgs-in-an-existing-bastion-forest"></a>기존 요새 포리스트에 HGS 설치 

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016


## <a name="join-the-hgs-server-to-the-existing-domain"></a>기존 도메인에 HGS 서버 조인

기존 요새 포리스트에서는 루트 도메인에 HGS를 추가 해야 합니다. 서버 관리자 또는 [컴퓨터 추가](https://go.microsoft.com/fwlink/?LinkId=821564) 를 사용 하 여 HGS 서버를 루트 도메인에 연결 합니다.

## <a name="add-the-hgs-server-role"></a>HGS 서버 역할 추가

관리자 권한 PowerShell 세션에서이 항목의 모든 명령을 실행 합니다.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

데이터 센터에 HGS 노드를 조인 하려는 보안 요새 포리스트가 있는 경우 다음 단계를 수행 합니다.
이러한 단계를 사용 하 여 동일한 도메인에 가입 된 두 개 이상의 독립 HGS 클러스터를 구성할 수도 있습니다.

## <a name="join-the-hgs-server-to-the-existing-domain"></a>기존 도메인에 HGS 서버 조인

서버 관리자 또는 [컴퓨터 추가](https://go.microsoft.com/fwlink/?LinkId=821564) 를 사용 하 여 HGS 서버를 원하는 도메인에 연결 합니다.

## <a name="prepare-active-directory-objects"></a>Active Directory 개체 준비

그룹 관리 서비스 계정 및 2 개의 보안 그룹을 만듭니다.
또한 HGS를 초기화 하는 계정에 도메인에서 컴퓨터 개체를 만들 수 있는 권한이 없는 경우 클러스터 개체를 미리 준비할 수 있습니다.

## <a name="group-managed-service-account"></a>그룹 관리 서비스 계정

GMSA (그룹 관리 서비스 계정)는 HGS에서 인증서를 검색 하 고 사용 하는 데 사용 하는 id입니다. [Uninstall-adserviceaccount](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adserviceaccount) 를 사용 하 여 gMSA를 만듭니다.
도메인의 첫 번째 gMSA 경우 키 배포 서비스 루트 키를 추가 해야 합니다.

각 HGS 노드는 gMSA 암호에 액세스할 수 있어야 합니다.
이를 구성 하는 가장 쉬운 방법은 모든 HGS 노드를 포함 하는 보안 그룹을 만들고 해당 보안 그룹에 gMSA 암호를 검색할 수 있는 액세스 권한을 부여 하는 것입니다.

새 그룹 멤버 자격을 가져오도록 보안 그룹에 추가한 후에 HGS 서버를 다시 부팅 해야 합니다.

```powershell
# Check if the KDS root key has been set up
if (-not (Get-KdsRootKey)) {
    # Adds a KDS root key effective immediately (ignores normal 10 hour waiting period)
    Add-KdsRootKey -EffectiveTime ((Get-Date).AddHours(-10))
}

# Create a security group for HGS nodes
$hgsNodes = New-ADGroup -Name 'HgsServers' -GroupScope DomainLocal -PassThru

# Add your HGS nodes to this group
# If your HGS server object is under an organizational unit, provide the full distinguished name instead of "HGS01"
Add-ADGroupMember -Identity $hgsNodes -Members "HGS01"

# Create the gMSA
New-ADServiceAccount -Name 'HGSgMSA' -DnsHostName 'HGSgMSA.yourdomain.com' -PrincipalsAllowedToRetrieveManagedPassword $hgsNodes
```

GMSA는 각 HGS 서버에서 보안 로그에 이벤트를 생성할 수 있는 권한이 필요 합니다.
그룹 정책를 사용 하 여 사용자 권한 할당을 구성 하는 경우 gMSA 계정에 HGS 서버에 대 한 [감사 이벤트 생성 권한이](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn221956%28v=ws.11%29) 부여 되어 있는지 확인 합니다.

> [!NOTE]
> 그룹 관리 서비스 계정은 Windows Server 2012 Active Directory 스키마부터 사용할 수 있습니다.
> 자세한 내용은 [그룹 관리 서비스 계정 요구 사항](https://technet.microsoft.com/library/jj128431.aspx)을 참조 하세요.

## <a name="jea-security-groups"></a>JEA 보안 그룹

HGS를 설정 하면 완전 한 로컬 관리자 권한이 없어도 관리자가 HGS를 관리할 수 있도록 [충분 한 관리 (JEA)](https://aka.ms/JEAdocs) PowerShell 끝점이 구성 됩니다.
HgsServer를 실행할 때 JEA를 사용 하 여 HGS를 관리할 필요는 없지만 여전히 구성 해야 합니다.
JEA 끝점의 구성은 HGS 관리자와 HGS 검토자를 포함 하는 2 개의 보안 그룹을 지정 하는 것으로 구성 됩니다.
관리자 그룹에 속한 사용자는 HGS에서 정책을 추가, 변경 또는 제거할 수 있습니다. 검토자는 현재 구성만 볼 수 있습니다.

Active Directory 관리 도구 또는 [new-adgroup](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adgroup)를 사용 하 여 이러한 jea 그룹에 대해 2 개의 보안 그룹을 만듭니다.

```powershell
New-ADGroup -Name 'HgsJeaReviewers' -GroupScope DomainLocal
New-ADGroup -Name 'HgsJeaAdmins' -GroupScope DomainLocal
```

## <a name="cluster-objects"></a>클러스터 개체

HGS를 설정 하는 데 사용 하는 계정에 도메인에 새 컴퓨터 개체를 만들 수 있는 권한이 없는 경우 클러스터 개체를 미리 준비 해야 합니다.
이러한 단계는 [Active Directory Domain Services의 클러스터 컴퓨터 개체 사전 준비](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx)에 설명 되어 있습니다.

첫 번째 HGS 노드를 설정 하려면 하나의 클러스터 이름 개체 (CNO)와 하나의 VCO (가상 컴퓨터 개체)를 만들어야 합니다.
CNO는 클러스터의 이름을 나타내며 주로 장애 조치 (Failover) 클러스터링에 의해 내부적으로 사용 됩니다.
VCO는 클러스터의 맨 위에 있고 DNS 서버에 등록 된 이름이 되는 HGS 서비스를 나타냅니다.

> [!IMPORTANT]
> `Initialize-HgsServer`를 실행 하는 사용자에 게는 Active Directory CNO 및 VCO 개체에 대 한 **모든 권한이** 필요 합니다.

CNO 및 VCO를 빠르게 사전 준비 하려면 Active Directory 관리자에 게 다음 PowerShell 명령을 실행 합니다.

```powershell
# Create the CNO
$cno = New-ADComputer -Name 'HgsCluster' -Description 'HGS CNO' -Enabled $false -Passthru

# Create the VCO
$vco = New-ADComputer -Name 'HgsService' -Description 'HGS VCO' -Passthru

# Give the CNO full control over the VCO
$vcoPath = Join-Path "AD:\" $vco.DistinguishedName
$acl = Get-Acl $vcoPath
$ace = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $cno.SID, "GenericAll", "Allow"
$acl.AddAccessRule($ace)
Set-Acl -Path $vcoPath -AclObject $acl

# Allow time for your new CNO and VCO to replicate to your other Domain Controllers before continuing
```

## <a name="security-baseline-exceptions"></a>보안 기준 예외

매우 잠긴 환경에 HGS를 배포 하는 경우 특정 그룹 정책 설정으로 인해 HGS가 정상적으로 작동 하지 않을 수 있습니다.
그룹 정책 개체에서 다음 설정을 확인 하 고 영향을 받는 경우 지침을 따릅니다.

### <a name="network-logon"></a>네트워크 로그온

**정책 경로:** 컴퓨터 구성 \ 로컬 정책 \ 보안 설정 \ 로컬 정책 \ 보안 설정

**정책 이름:** 네트워크에서이 컴퓨터 액세스 거부

**필요한 값:** 값이 모든 로컬 계정에 대 한 네트워크 로그온을 차단 하지 않는지 확인 합니다. 그러나 로컬 관리자 계정은 안전 하 게 차단할 수 있습니다.

**이유:** 장애 조치 (Failover) 클러스터링은 CLIUSR 이라는 비관리자 로컬 계정을 사용 하 여 클러스터 노드를 관리 합니다. 이 사용자에 대 한 네트워크 로그온을 차단 하면 클러스터가 올바르게 작동 하지 않습니다.

### <a name="kerberos-encryption"></a>Kerberos 암호화

**정책 경로:** 컴퓨터 구성 \ 보안 설정 \ 로컬 정책 \ 보안 옵션

**정책 이름:** 네트워크 보안: Kerberos에 허용 된 암호화 유형 구성

**작업**:이 정책을 구성 하는 경우이 정책에서 지원 되는 암호화 유형만 사용 하도록 GMSA 계정을 [uninstall-adserviceaccount](https://docs.microsoft.com/powershell/module/addsadministration/set-adserviceaccount?view=win10-ps) 로 업데이트 해야 합니다. 예를 들어 정책에서 AES128\_HMAC\_SHA1 및 AES256\_HMAC\_SHA1을 허용 하는 경우 `Set-ADServiceAccount -Identity HGSgMSA -KerberosEncryptionType AES128,AES256`를 실행 해야 합니다.



## <a name="next-steps"></a>다음 단계

- TPM 기반 증명을 설정 하는 다음 단계는 [기존 요새 포리스트에서 tpm 모드를 사용 하 여 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)를 참조 하세요.
- 호스트 키 증명을 설정 하는 다음 단계는 [기존 요새 포리스트에서 키 모드를 사용 하 여 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-key-mode-bastion.md)를 참조 하세요.
- 관리자 기반 증명을 설정 하는 다음 단계 (Windows Server 2019에서 사용 되지 않음)는 [기존 요새 포리스트에서 AD 모드를 사용 하 여 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-ad-mode-bastion.md)를 참조 하세요.

