---
title: 관리자가 아닌 사용자에 게 AD FS Powershell Commandlet 액세스 위임
description: 이 문서 descirbes 비-AD FS PowerShell cmdlt에 대 한 관리자 권한을 위임 하는 방법입니다.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: zhvolosh
ms.date: 01/31/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 265d22b045011e34192e56bdb970955b601cda56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883564"
---
# <a name="delegate-ad-fs-powershell-commandlet-access-to-non-admin-users"></a>관리자가 아닌 사용자에 게 AD FS Powershell Commandlet 액세스 위임 
PowerShell 통해 AD FS 관리 기본적으로 AD FS 관리자가 수행할 수만 있습니다. 많은 대규모 조직에서는이 되지 않을 수 있습니다 실행 가능한 운영 모델을 지원 센터 담당자와 같은 다른 가상 사용자를 처리할 때.  

사용 하 여 JEA Just Enough Administration (), 고객은 다른 직원 그룹에 특정 commandlet 이제 위임할 수 있습니다.  
AD FS 쿼리 지원 센터 직원이 계정 잠금 상태 및 사용자의 점검 되었습니다 되 면 AD FS의 계정 잠금 상태를 다시 설정 좋은 예가이 사용 사례에서 허용 됩니다. 이 경우 commandlet을 위임할 수는 다음과 같습니다. 
- `Get-ADFSAccountActivity`
- `Set-ADFSAccountActivity` 
- `Reset-ADFSAccountLockout` 

이 예제에서는이 문서의 나머지 부분에서 사용합니다. 그러나 또한 신뢰 당사자의 속성을 설정 및 해제이 조직 내에서 응용 프로그램 소유자에 게 전달에 대 한 위임을 허용 하도록 사용자 지정할 수 있습니다 하나입니다.  


##  <a name="create-the-required-groups-necessary-to-grant-users-permissions"></a>사용자 권한을 부여 하는 데 필요한 필요한 그룹을 만들려면 
1. 만들기는 [그룹 관리 서비스 계정](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)합니다. GMSA 계정 JEA 사용자가 다른 컴퓨터 또는 웹 서비스와 네트워크 리소스에 액세스 하도록 허용 됩니다. 도메인 내에서 모든 컴퓨터의 리소스에 대해 인증을 사용할 수 있는 도메인 id를 제공 합니다. GMSA 계정 설정에서 나중에 필요한 관리 권한이 부여 됩니다. 예를 들어 계정 이라고 **gMSAContoso**합니다. 
2. Active Directory 만들기 위임 된 명령에 권한을 부여 해야 하는 사용자와 그룹을 채울 수 있습니다. 이 예제에서는 지원 센터 담당자는 읽기, 업데이트 및 ADFS 잠금 상태를 다시 설정 권한이 부여 됩니다. 전체 예제를이 그룹 이라고 **JEAContoso**합니다. 

### <a name="install-the-gmsa-account-on-the-adfs-server"></a>GMSA 계정 ADFS 서버에 설치 합니다. 
ADFS 서버에 대 한 관리 권한이 있는 서비스 계정을 만듭니다. 이 수행할 수 있습니다 또는 long으로 원격으로 도메인 컨트롤러에서 AD RSAT 패키지를 설치 됩니다.  ADFS 서버와 동일한 포리스트에 서비스 계정을 만들어야 합니다. 팜의 구성 예제에서는 값을 수정 합니다. 

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

GMSA 계정 ADFS 서버에 설치 합니다.  이 팜의 모든 ADFS 노드에서 실행 해야 합니다. 
 
```powershell
Install-ADServiceAccount gMSAcontoso 
```

### <a name="grant-the-gmsa-account-admin-rights"></a>GMSA 계정 관리 권한 부여 
팜의 위임 된 관리를 사용 하는 경우 gMSA 계정 관리 권한 부여 관리자 액세스를 위임에 기존 그룹에 추가 하 여 합니다.  
 
팜의 위임 된 관리에 사용 하지 않는 경우 부여 gMSA 계정 관리자 권한으로 모든 ADFS 서버에서 로컬 관리 그룹을 만들어 합니다. 
 
 
### <a name="create-the-jea-role-file"></a>JEA 역할 파일 만들기 
 
메모장 파일에서 JEA 역할을 만듭니다. 제공 하는 역할을 만드는 지침 [JEA 역할 기능](https://docs.microsoft.com/powershell/jea/role-capabilities)합니다. 
 
이 예제에서 위임 commandlet은 `Reset-AdfsAccountLockout, Get-ADFSAccountActivity, and Set-ADFSAccountActivity`합니다. 

샘플 JEA 역할 ' 재설정 ADFSAccountLockout', ' Get-ADFSAccountActivity' 및 ' 설정-ADFSAccountActivity' commandlet에 대 한 액세스를 위임 합니다.

```powershell
@{
GUID = 'b35d3985-9063-4de5-81f8-241be1f56b52'
ModulesToImport = 'adfs'
VisibleCmdlets = 'Reset-AdfsAccountLockout', 'Get-ADFSAccountActivity', 'Set-ADFSAccountActivity'
}
```


### <a name="create-the-jea-session-configuration-file"></a>JEA 세션 구성 파일 만들기 
지침에 따라 만듭니다는 [JEA 세션 구성](https://docs.microsoft.com/powershell/jea/session-configurations) 파일입니다. 구성 파일에 액세스할 수 있는 기능 및 JEA 끝점을 사용할 수 있는 사용자를 결정 합니다. 

역할 기능은 역할 기능 파일의 일반 이름 (파일 이름 확장명 제외)에서 참조 됩니다. 여러 역할 기능 플랫 이름이 같은 시스템에서 사용할 경우 PowerShell 암시적 검색 순서를 사용 하 여 유효 역할 기능 파일을 선택 합니다. 동일한 이름 가진 모든 역할 기능 파일에 대 한 액세스를 부여 하지 않습니다. 

경로 사용 하 여 역할 기능 파일을 지정 하려면 사용 된 `RoleCapabilityFiles` 인수입니다. 하위 폴더를 포함 하는 유효한 Powershell 모듈에 대 한 JEA 찾습니다는 `RoleCapabilities` 하위 폴더를 위치 합니다 `RoleCapabilityFiles` 인수를 수정 해야 `RoleCapabilities`합니다. 

샘플 세션 구성 파일: 

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
 
에 가장 좋습니다 [세션 구성 파일 테스트](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Test-PSSessionConfigurationFile?view=powershell-5.1) 구문을 확인 하려면 텍스트 편집기를 사용 하는 올바른 pssc 파일을 수동으로 편집한 경우. 세션 구성 파일을이 테스트를 통과 하지 못하는 경우이 등록 되지 않았습니다 성공적으로 시스템에서.  
 
### <a name="install-the-jea-session-configuration-on-the-ad-fs-server"></a>JEA 세션 구성을 AD FS 서버에 설치 

AD FS 서버에서 JEA 세션 구성을 설치합니다 
 
```powershell
Register-PSSessionConfiguration -Path .\JEASessionConfig.pssc -name "AccountActivityAdministration" -force
``` 
## <a name="operational-instructions"></a>운영 지침 
설정한 후 로깅 및 감사 JEA 수 확인 하려면 올바른 사용자가 JEA 끝점에 액세스할 수 있습니다. 

명령을 사용 하 여 위임 합니다. 

```powershell
Enter-pssession -ComputerName server01.contoso.com -ConfigurationName "AccountActivityAdministration" -Credential <User Using JEA> 
Get-AdfsAccountActivity <User> 
```
