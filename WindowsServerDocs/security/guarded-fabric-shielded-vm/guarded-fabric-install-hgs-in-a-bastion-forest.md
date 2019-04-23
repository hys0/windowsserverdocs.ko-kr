---
title: 기존 배스 천 포리스트의 HGS를 설치 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 147610d9dcb36dfedab3aca11ee1a64731715519
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842224"
---
# <a name="install-hgs-in-an-existing-bastion-forest"></a>기존 배스 천 포리스트의 HGS를 설치 합니다. 

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019


## <a name="join-the-hgs-server-to-the-existing-domain"></a>HGS 서버를 기존 도메인에 가입

기존 배스 천 포리스트의 HGS 루트 도메인에 추가 되어야 합니다. 서버 관리자를 사용 하거나 [Add-computer](https://go.microsoft.com/fwlink/?LinkId=821564) HGS 서버를 루트 도메인에 가입 하 합니다.

## <a name="add-the-hgs-server-role"></a>HGS 서버 역할 추가

관리자 권한 PowerShell 세션에서이 항목의 모든 명령을 실행 합니다.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

데이터 센터에 보안 배스 천 포리스트 HGS 노드 가입 하려는 경우 다음이 단계를 수행 합니다.
또한 동일한 도메인에 가입 된 2 개 이상의 독립 HGS 클러스터를 구성할 수 다음이 단계를 사용할 수 있습니다.

## <a name="join-the-hgs-server-to-the-existing-domain"></a>HGS 서버를 기존 도메인에 가입

서버 관리자를 사용 하거나 [Add-computer](https://go.microsoft.com/fwlink/?LinkId=821564) HGS 서버를 원하는 도메인에 가입 하 합니다.

## <a name="prepare-active-directory-objects"></a>Active Directory 개체를 준비 합니다.

그룹 관리 서비스 계정 및 2 개의 보안 그룹을 만듭니다.
준비할 수 있습니다도 미리 클러스터 개체가 사용 하 여 HGS를 초기화 하는 계정에 도메인의 컴퓨터 개체를 만들 수 있는 권한이 없는 경우.

## <a name="group-managed-service-account"></a>그룹 관리 서비스 계정

그룹 관리 서비스 계정 (gMSA)는 HGS에서 해당 인증서를 사용 하 여 검색을 사용 하는 id입니다. 사용 하 여 [New-adserviceaccount](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adserviceaccount) gMSA를 만들려고 합니다.
도메인의 첫 번째 gMSA 인 경우 키 배포 서비스 루트 키를 추가 해야 합니다.

HGS 노드마다 gMSA 암호에 액세스할 수 있도록 허용 하려면 할 수 있습니다.
이 구성 하는 가장 쉬운 방법은 모든 HGS 노드가 포함 된 보안 그룹을 만들 때 및 gMSA 암호 검색에 대 한 해당 보안 그룹 액세스 권한을 부여 합니다.

HGS 서버에 가져와서 새 그룹 멤버 자격을 확인 하는 보안 그룹에 추가한 후 다시 부팅 해야 합니다.

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

GMSA 각 HGS 서버에서 보안 로그에 이벤트를 생성할 수 있는 권한이 필요 합니다.
그룹 정책을 사용 하 여 사용자 권한 할당을 구성 하는 경우 gMSA 계정 부여 되어 있음을 확인 합니다 [감사 이벤트 권한 생성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn221956%28v=ws.11%29) HGS 서버.

> [!NOTE]
> 그룹 관리 서비스 계정은 Windows Server 2012 Active Directory 스키마를 사용 하 여부터 사용할 수 있습니다.
> 자세한 내용은 [그룹 관리 서비스 계정 요구 사항](https://technet.microsoft.com/library/jj128431.aspx)합니다.

## <a name="jea-security-groups"></a>JEA 보안 그룹

HGS를 설정 하는 경우는 [관리 JEA (Just Enough)](https://aka.ms/JEAdocs) PowerShell 끝점 관리자를 통해 전체 로컬 관리자 권한이 필요 없이 HGS 관리를 허용 하도록 구성 되어 있습니다.
JEA를 사용 하 여 HGS를 관리할 필요가 없습니다 있지만 여전히 구성 해야 HgsServer 초기화를 실행 하는 경우.
JEA 끝점의 구성을 지정 하 고 HGS 관리자 HGS 검토자를 포함 하는 2 개의 보안 그룹 이루어져 있습니다.
관리 그룹에 속한 사용자 수를 추가, 변경 또는 HGS;에서 정책을 제거합니다 검토자가 현재 구성을 보기만 할 수 있습니다.

Active Directory 관리 도구를 사용 하 여 이러한 JEA 그룹에 대 한 2 개의 보안 그룹 만들기 또는 [New-adgroup](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adgroup)합니다.

```powershell
New-ADGroup -Name 'HgsJeaReviewers' -GroupScope DomainLocal
New-ADGroup -Name 'HgsJeaAdmins' -GroupScope DomainLocal
```

## <a name="cluster-objects"></a>클러스터 개체

HGS를 설정 하는 데 사용할 계정에 도메인에 새 컴퓨터 개체를 만들 수 있는 권한이 없으면 클러스터 개체를 사전 준비 해야 합니다.
이러한 단계에 설명 되어 [Active Directory Domain Services에서 Prestage Cluster Computer Objects](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx)합니다.

첫 번째 HGS 노드를 설정 하려면 하나의 클러스터 이름 개체 (CNO)를 만들고 한 가상 컴퓨터 개체 (VCO) 해야 합니다.
CNO는 클러스터의 이름을 나타내는 이며, 장애 조치 클러스터링에서 내부적으로 주로 사용 됩니다.
VCO 클러스터 위에 있는 HGS를 나타내며 DNS 서버에 등록 된 이름이 됩니다.

> [!IMPORTANT]
> 사용자가 실행 됩니다 `Initialize-HgsServer` 필요 **전면적인** Active Directory에서 CNO와 VCO 개체에 대해 합니다.

신속 하 게 CNO 고 VCO를 사전 준비를 하려면 다음 PowerShell 명령을 실행 하는 Active Directory 관리자에

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

항상 잠긴된 환경으로 HGS를 배포 하는 경우 특정 그룹 정책 설정을 HGS가 제대로 작동 하지 못할 수 있습니다.
다음 설정에 대 한 그룹 정책 개체를 확인 하 고는 영향을 받는 경우 지침을 따르세요.

### <a name="network-logon"></a>네트워크 로그온

**정책 경로:** 컴퓨터 구성 설정 \ 보안 설정 \ 로컬 정책 \ 사용자 권한 할당

**정책 이름:** 네트워크에서 이 컴퓨터 액세스 거부

**필요한 값:** 값은 모든 로컬 계정에 대 한 네트워크 로그온을 차단 하지 않습니다 확인 합니다. 그러나 로컬 관리자 계정을 안전 하 게 차단할 수 있습니다.

**원인:** 장애 조치 클러스터링 클러스터 노드를 관리할 수 CLIUSR 호출 관리자가 아닌 로컬 계정에 의존 합니다. 이 사용자에 대 한 네트워크 로그온을 차단는 클러스터에서 제대로 작동 하지 것입니다.

### <a name="kerberos-encryption"></a>Kerberos 암호화

**정책 경로:** 컴퓨터 구성\Windows 설정\보안 설정\로컬 정책\보안 옵션

**정책 이름:** 네트워크 보안: Kerberos에 허용 된 암호화 유형 구성

**작업**: 이 정책이 구성 되어 있는 gMSA 계정을 업데이트 해야 합니다 [Set-adserviceaccount](https://docs.microsoft.com/powershell/module/addsadministration/set-adserviceaccount?view=win10-ps) 이 정책에만 지원 되는 암호화 형식을 사용 합니다. 예를 들어 정책 AES128만을 허용 한다면\_HMAC\_고 AES256 SHA1\_HMAC\_실행 해야 SHA1 `Set-ADServiceAccount -Identity HGSgMSA -KerberosEncryptionType AES128,AES256`합니다.



## <a name="next-steps"></a>다음 단계

- TPM 기반 증명을 설정 하려면 다음 단계를 참조 하세요 [TPM 모드를 사용 하 여 기존 배스 천 포리스트의 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)합니다.
- 호스트 키 증명을 설정 하려면 다음 단계를 참조 하세요 [키 모드를 사용 하 여 기존 배스 천 포리스트의 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-key-mode-bastion.md)합니다.
- 다음 관리자 기반 증명 (Windows Server 2019에 사용 되지 않음)를 설정 하는 방법 참조 [기존 배스 천 포리스트의 AD 모드를 사용 하 여 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-ad-mode-bastion.md)합니다.

