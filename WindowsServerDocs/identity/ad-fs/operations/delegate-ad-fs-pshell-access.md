---
title: 관리자가 아닌 사용자에 게 AD FS Powershell 기능을 위임 합니다.
description: 이 문서에서는 AD FS PowerShell cmdlts의 관리자가 아닌에 대 한 권한을 위임 하는 방법을 descirbes.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: zhvolosh
ms.date: 01/31/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 86bbb562e223fdf61dac3ce5646d97a57b2eba4c
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546310"
---
# <a name="delegate-ad-fs-powershell-commandlet-access-to-non-admin-users"></a>관리자가 아닌 사용자에 게 AD FS Powershell 기능을 위임 합니다. 
기본적으로 PowerShell을 통한 AD FS 관리는 AD FS 관리자만 수행할 수 있습니다. 많은 대기업의 경우 지원 센터 담당자와 같은 다른 가상 사용자를 처리할 때 실행 가능한 운영 모델이 아닐 수 있습니다.  

이제 충분 한 관리 (jea)를 사용 하 여 고객은 다양 한 직원 그룹에 특정 commandlet을 위임할 수 있습니다.  
이 사용 사례의 좋은 예로, 사용자가 점검 되었다는 된 후 AD FS에서 AD FS 계정 잠금 상태를 쿼리하고 계정 잠금 상태를 다시 설정할 수 있습니다. 이 경우 위임 해야 할 commandlet은 다음과 같습니다. 
- `Get-ADFSAccountActivity`
- `Set-ADFSAccountActivity` 
- `Reset-ADFSAccountLockout` 

이 문서의 나머지 부분에서이 예제를 사용 합니다. 그러나이를 사용자 지정 하 여 위임에서 신뢰 당사자의 속성을 설정 하 고이를 조직 내의 응용 프로그램 소유자에 게 전달할 수 있습니다.  


##  <a name="create-the-required-groups-necessary-to-grant-users-permissions"></a>사용자 권한을 부여 하는 데 필요한 필수 그룹 만들기 
1. [그룹 관리 서비스 계정을](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)만듭니다. GMSA 계정은 JEA 사용자가 다른 컴퓨터 또는 웹 서비스로 네트워크 리소스에 액세스할 수 있도록 하는 데 사용 됩니다. 도메인 내에 있는 모든 컴퓨터의 리소스에 대해 인증 하는 데 사용할 수 있는 도메인 id를 제공 합니다. GMSA 계정에는 나중에 설치 프로그램에서 필요한 관리 권한이 부여 됩니다. 이 예에서는 **gMSAContoso**계정을 호출 합니다. 
2. Active Directory 그룹 만들기는 위임 된 명령에 대 한 권한을 부여 받아야 하는 사용자로 채워질 수 있습니다. 이 예에서는 지원 센터 담당자에 게 ADFS 잠금 상태를 읽고, 업데이트 하 고, 다시 설정할 수 있는 권한이 부여 됩니다. 이 그룹은 예제 전체에서 **JEAContoso**로 참조 됩니다. 

### <a name="install-the-gmsa-account-on-the-adfs-server"></a>ADFS 서버에 gMSA 계정을 설치 합니다. 
ADFS 서버에 대 한 관리 권한이 있는 서비스 계정을 만듭니다. 이는 도메인 컨트롤러에서 수행 하거나 AD RSAT 패키지를 설치 하는 동안 원격으로 수행할 수 있습니다.  서비스 계정은 ADFS 서버와 동일한 포리스트에 만들어야 합니다. 팜 구성에 대 한 예제 값을 수정 합니다. 

```powershell
 # This command should only be run if this is the first time gMSA accounts are enabled in the forest 
Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))  
 
# Run this on every node that you want to have JEA configured on  
$adfsServer = Get-ADComputer server01.contoso.com  
 
# Run targeted at domain controller  
$serviceaccount = New-ADServiceAccount gMSAcontoso -DNSHostName <FQDN of the domain containing the KDS key> - PrincipalsAllowedToRetrieveManagedPassword $adfsServer –passthru 
 
# Run this on every node 
Add-ADComputerServiceAccount -Identity server01.contoso.com -ServiceAccount $ServiceAccount 
```

ADFS 서버에 gMSA 계정을 설치 합니다.  팜의 모든 ADFS 노드에서 실행 해야 합니다. 
 
```powershell
Install-ADServiceAccount gMSAcontoso 
```

### <a name="grant-the-gmsa-account-admin-rights"></a>GMSA 계정 관리자 권한 부여 
팜이 위임 된 관리를 사용 하는 경우 위임 된 관리 액세스 권한이 있는 기존 그룹에 gMSA 계정 관리자 권한을 추가 하 여 권한을 부여 합니다.  
 
팜이 위임 된 관리를 사용 하지 않는 경우 모든 ADFS 서버에서 로컬 관리 그룹으로 설정 하 여 gMSA 계정에 관리자 권한을 부여 합니다. 
 
 
### <a name="create-the-jea-role-file"></a>JEA 역할 파일 만들기 
 
AD FS 서버에서 메모장 파일에 JEA 역할을 만듭니다. 역할을 만드는 방법에 대 한 지침은 [Jea 역할 기능](https://docs.microsoft.com/powershell/jea/role-capabilities)에서 제공 됩니다. 
 
이 예 `Reset-AdfsAccountLockout, Get-ADFSAccountActivity, and Set-ADFSAccountActivity`에서는 commandlet을 위임할 수 있습니다. 

' ADFSAccountLockout ', ' ADFSAccountActivity ' 및 ' ADFSAccountActivity ' 명령에 대 한 액세스를 위임 하는 샘플 JEA 역할은 다음과 같습니다.

```powershell
@{
GUID = 'b35d3985-9063-4de5-81f8-241be1f56b52'
ModulesToImport = 'adfs'
VisibleCmdlets = 'Reset-AdfsAccountLockout', 'Get-ADFSAccountActivity', 'Set-ADFSAccountActivity'
}
```


### <a name="create-the-jea-session-configuration-file"></a>JEA 세션 구성 파일 만들기 
지침에 따라 [Jea 세션 구성](https://docs.microsoft.com/powershell/jea/session-configurations) 파일을 만듭니다. 구성 파일은 사용자가 JEA 끝점을 사용할 수 있는 사용자 및 액세스 권한이 있는 기능을 결정 합니다. 

역할 기능은 역할 기능 파일의 플랫 이름 (확장명이 없는 파일 이름)에서 참조 됩니다. 동일한 플랫 이름을 사용 하 여 시스템에서 여러 역할 기능을 사용할 수 있는 경우 PowerShell에서는 암시적 검색 순서를 사용 하 여 유효한 역할 기능 파일을 선택 합니다. 동일한 이름의 모든 역할 기능 파일에 대 한 액세스 권한은 제공 하지 않습니다. 

경로를 사용 하 여 역할 기능 파일을 지정 하려면 `RoleCapabilityFiles` 인수를 사용 합니다. 하위 폴더의 경우 jea는 `RoleCapabilities` 하위 폴더를 포함 하는 유효한 Powershell 모듈을 찾습니다 `RoleCapabilityFiles` `RoleCapabilities`. 여기서 인수는로 수정 해야 합니다. 

예제 세션 구성 파일: 

```powershell
@{
SchemaVersion = '2.0.0.0'
GUID = '54c8d41b-6425-46ac-a2eb-8c0184d9c6e6'
SessionType = 'RestrictedRemoteServer'
GroupManagedServiceAccount =  'CONTOSO\gMSAcontoso'
RoleDefinitions = @{ JEAcontoso = @{ RoleCapabilityFiles = 'C:\Program Files\WindowsPowershell\Modules\AccountActivityJEA\RoleCapabilities\JEAAccountActivityResetRole.psrc' } }
}
```

세션 구성 파일을 저장 합니다. 
 
구문이 올바른지 확인 하기 위해 텍스트 편집기를 사용 하 여 수동으로 .pssc 파일을 편집한 경우 [세션 구성 파일을 테스트](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Test-PSSessionConfigurationFile?view=powershell-5.1) 하는 것이 좋습니다. 세션 구성 파일에서이 테스트를 통과 하지 못하면 시스템에 성공적으로 등록 되지 않은 것입니다.  
 
### <a name="install-the-jea-session-configuration-on-the-ad-fs-server"></a>AD FS 서버에 JEA 세션 구성 설치 

AD FS 서버에 JEA 세션 구성 설치 
 
```powershell
Register-PSSessionConfiguration -Path .\JEASessionConfig.pssc -name "AccountActivityAdministration" -force
``` 
## <a name="operational-instructions"></a>작업 지침 
설정 된 후에는 JEA 로깅 및 감사를 사용 하 여 올바른 사용자에 게 JEA 끝점에 대 한 액세스 권한이 있는지 여부를 확인할 수 있습니다. 

위임 된 명령을 사용 하려면 다음을 수행 합니다. 

```powershell
Enter-pssession -ComputerName server01.contoso.com -ConfigurationName "AccountActivityAdministration" -Credential <User Using JEA> 
Get-AdfsAccountActivity <User> 


```
