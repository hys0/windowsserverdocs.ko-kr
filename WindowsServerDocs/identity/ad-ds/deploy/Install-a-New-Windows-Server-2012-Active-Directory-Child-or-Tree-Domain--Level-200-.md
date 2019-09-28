---
ms.assetid: e3d55565-ad45-4504-ad73-8103d1a92170
title: 새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 설치(수준 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d0944377739f43ea5d9b8d0d9c94c13e9f18985f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390891"
---
# <a name="install-a-new-windows-server-2012-active-directory-child-or-tree-domain-level-200"></a>새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 설치(수준 200)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 서버 관리자 또는 Windows PowerShell을 사용하여 기존 Windows Server 2012 포리스트에 자식 및 트리 도메인을 추가하는 방법에 대해 설명합니다.  
  
-   [자식 및 트리 도메인 워크플로](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [자식 및 트리 도메인 Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)  
  
-   [배포](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Deployment)  
  
## <a name="BKMK_Workflow"></a>자식 및 트리 도메인 워크플로  
다음 다이어그램에서는 이전에 AD DS 역할을 설치하고 서버 관리자를 사용하여 기존 포리스트에서 새 도메인을 만드는 Active Directory 도메인 서비스 구성 마법사를 시작한 경우의 Active Directory 도메인 서비스 구성 프로세스를 보여 줍니다.  
  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/adds_childtreedeploy_beta1.png)  
  
## <a name="BKMK_PS"></a>자식 및 트리 도메인 Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수(**굵게** 표시된 인수는 필수 항목이며, *기울임꼴* 인수는 Windows PowerShell 또는 AD DS 구성 마법사를 사용하여 지정할 수 있음)|  
|**설치-AddsDomain**|-SkipPreChecks<br /><br />***-NewDomainName***<br /><br />***-ParentDomainName***<br /><br />***-SafeModeAdministratorPassword***<br /><br />*-ADPrepCredential*<br /><br />-AllowDomainReinstall<br /><br />-Confirm<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />-NoDNSOnNetwork<br /><br />*-DomainMode*<br /><br />***-DomainType***<br /><br />-Force<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />*-NewDomainNetBIOSName*<br /><br />*-NoGlobalCatalog*<br /><br />-NoNorebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-SiteName*<br /><br />-SkipAutoConfigureDNS<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-credential** 인수는 현재 Enterprise Admins 그룹의 구성원으로 로그인되어 있지 않은 경우에만 필요하고, **-NewDomainNetBIOSName** 인수는 DNS 도메인 이름 접두사에 따라 자동으로 생성된 15자 이름을 변경하려는 경우 또는 이름이 15자를 초과하는 경우에 필요합니다.  
  
## <a name="BKMK_Deployment"></a>배포가  
  
### <a name="deployment-configuration"></a>배포 구성  
다음 스크린샷에서는 자식 도메인을 추가하기 위한 옵션을 보여 줍니다.  
  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDeployConfig.png)  
  
다음 스크린샷에서는 트리 도메인을 추가하기 위한 옵션을 보여 줍니다.  
  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_TreeDeployConfig.png)  
  
서버 관리자는 **배포 구성** 페이지에서 모든 도메인 컨트롤러 수준 올리기를 시작합니다. 선택한 배포 작업에 따라 이 페이지 및 다음 페이지에 표시되는 나머지 옵션 및 필수 필드가 바뀝니다.  
  
이 항목에서는 두 개의 개별 작업인 자식 도메인 수준 올리기와 트리 도메인 수준 올리기를 통합합니다. 두 작업 간의 차이점은 만들려고 선택하는 도메인 유형뿐입니다. 다른 모든 단계는 두 작업 간에 동일합니다.  
  
-   새 자식 도메인을 만들려면 **기존 포리스트에 도메인 추가**를 선택한 다음 **자식 도메인**을 선택합니다. **부모 도메인 이름**에서 부모 도메인의 이름을 입력하거나 선택합니다. 그런 다음 **새 도메인 이름**에 새 도메인의 이름을 입력합니다. 단일 레이블로 구성된 유효한 자식 도메인 이름을 제공합니다. 이름은 DNS 도메인 이름 요구 사항을 사용해야 합니다.  
  
-   기존 포리스트 내에 새 트리 도메인을 만들려면 **기존 포리스트에 도메인 추가** 를 선택한 다음 **트리 도메인**을 선택합니다. 포리스트 루트 도메인의 이름을 입력한 다음 새 도메인의 이름을 입력합니다. 정규화된 유효한 루트 도메인 이름을 제공합니다. 이름은 단일 레이블로 구성된 이름일 수 없으며, DNS 도메인 이름 요구 사항을 사용해야 합니다.  
  
DNS 이름에 대한 자세한 내용은 [컴퓨터, 도메인, 사이트 및 OU에 대한 Active Directory의 명명 규칙](https://support.microsoft.com/kb/909264)을 참조하세요.  
  
현재 자격 증명이 도메인 범위에 속하지 않는 경우 서버 관리자 Active Directory 도메인 서비스 구성 마법사에 도메인 자격 증명을 제공하라는 메시지가 표시됩니다. **변경**을 클릭하여 수준 올리기 작업에 대한 도메인 자격 증명을 제공합니다.  
  
배포 구성 ADDSDeployment cmdlet 및 인수는 다음과 같습니다.  
  
```  
Install-AddsDomain  
-domaintype <{childdomain | treedomain}>  
-parentdomainname <string>  
-newdomainname <string>  
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_DCOptions_Child.gif)  
  
**도메인 컨트롤러 옵션** 페이지에서는 새 도메인 컨트롤러에 대한 도메인 컨트롤러 옵션을 지정합니다. 구성 가능한 도메인 컨트롤러 옵션에는 **DNS 서버** 및 **글로벌 카탈로그**가 포함됩니다. 읽기 전용 도메인 컨트롤러는 새 도메인의 첫 번째 도메인 컨트롤러로 구성할 수 없습니다.  
  
분산된 환경에서의 고가용성을 위해 모든 도메인 컨트롤러에서 DNS 및 GC 서비스를 제공하는 것이 좋습니다. GC는 항상 기본적으로 선택되며, DNS는 현재 도메인에서 권한 시작 쿼리를 기반으로 해당 DC에 이미 있는 DNS를 호스트하는 경우 기본적으로 선택됩니다. **도메인 기능 수준**도 지정해야 합니다. 기본 기능 수준은 Windows Server 2012이며 현재 포리스트 기능 수준보다 높거나 같은 다른 값을 선택할 수 있습니다.  
  
**도메인 컨트롤러 옵션** 페이지에서는 포리스트 구성에서 적절한 Active Directory 논리 **사이트 이름** 을 선택할 수도 있습니다. 기본적으로 가장 올바른 서브넷이 있는 사이트가 선택됩니다. 사이트가 1개만 있는 경우 자동으로 해당 사이트가 선택됩니다.  
  
> [!IMPORTANT]  
> 서버가 어떠한 Active Directory 서브넷에도 속해 있지 않고 둘 이상의 Active Directory 사이트가 있는 경우에는 아무 항목도 선택되지 않습니다. 이 경우 목록에서 사이트를 선택해야 **다음** 단추를 사용할 수 있습니다.  
  
지정한 **디렉터리 서비스 복원 모드 암호** 는 서버에 적용되는 암호 정책을 준수해야 합니다. 항상 강력하고 복잡한 암호 또는 암호 문구를 선택하십시오.  
  
**도메인 컨트롤러 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-Sitename <string>  
-SafeModeAdministratorPassword <secure string>  
-Credential <pscredential>  
```  
  
> [!IMPORTANT]  
> **sitename** 인수의 값으로 제공된 경우 사이트 이름이 이미 존재해야 합니다. **install-AddsDomainController** cmdlet은 사이트 이름을 만들지 않습니다. **new-adreplicationsite** cmdlet을 사용하여 새 사이트를 만들 수 있습니다.  
  
**Install-ADDSDomainController** cmdlet 인수는 서버 관리자와 동일한 기본값을 따릅니다(지정하지 않은 경우).  
  
**SafeModeAdministratorPassword** 인수의 작업은 특별합니다.  
  
-   인수로 *지정하지 않을 경우* cmdlet은 마스킹된 암호를 입력 및 확인하라는 메시지를 표시합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법입니다.  
  
    예를 들어 Contoso.com 포리스트에 NorthAmerica라는 새 자식 도메인을 만들고 마스킹된 암호를 입력하고 확인하라는 메시지를 표시하려면 다음 명령을 실행합니다.  
  
    ```  
    Install-ADDSDomain "NewDomainName NorthAmerica "ParentDomainName Contoso.com "DomainType Child  
    ```  
  
-   *값과 함께* 지정한 경우 값은 보안 문자열이어야 합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법이 아닙니다.  
  
예를 들어 **Read-Host** cmdlet을 사용하여 수동으로 암호를 물어 사용자에게 보안 문자열을 물을 수 있습니다.  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
  
```  
  
> [!WARNING]  
> 이전 옵션이 암호를 확인하지 않으므로 각별히 주의해야 합니다. 암호는 표시되지 않습니다.  
  
변환된 일반 텍스트 변수로 보안 문자열을 제공할 수도 있습니다(권장되지 않음).  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
  
```  
  
마지막으로 난독 처리된 암호를 파일에 저장한 다음 일반 텍스트 암호를 표시하지 않고 나중에 다시 사용할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> 일반 또는 난독 처리된 텍스트 암호는 제공하거나 저장하지 않는 것이 좋습니다. 스크립트에서 이 명령을 실행하는 사용자나 어깨 너머로 보고 있는 다른 사용자가 해당 도메인 컨트롤러의 DSRM 암호를 알게 될 수 있습니다.  파일에 액세스할 수 있는 모든 사람이 난독 처리된 암호를 반전시킬 수 있습니다. 이 정보를 알면 DSRM에서 시작된 DC에 로그온하여 도메인 컨트롤러 자체를 가장함으로써 AD 포리스트에서 가장 높은 수준으로 해당 권한을 상승시킬 수 있습니다. **System.Security.Cryptography**를 사용하여 텍스트 파일 데이터를 암호화하는 추가 단계를 수행하는 것이 좋지만 이러한 단계는 이 문서의 범위를 벗어납니다. 암호 저장을 완전히 피하는 것이 가장 좋습니다.  
  
ADDSDeployment 모듈에서는 DNS 클라이언트 설정, 전달자 및 루트 힌트의 자동 구성을 건너뛸 수 있는 추가 옵션을 제공합니다. 서버 관리자를 사용하는 경우에는 이를 구성할 수 없습니다. 이 인수는 도메인 컨트롤러를 구성하기 전에 DNS 서버 서비스를 이미 설치한 경우에만 적용됩니다.  
  
```  
-SkipAutoConfigureDNS  
  
```  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS 옵션 및 DNS 위임 자격 증명  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDNSOptions.png)  
  
**DNS 옵션** 페이지에서 위임을 위한 대체 DNS 관리자 자격 증명을 제공할 수 있습니다.  
  
기존 포리스트에 새 도메인을 설치하는 경우(**도메인 컨트롤러 옵션** 페이지에서 DNS 설치를 선택한 경우)에는 옵션을 구성할 수 없습니다. 위임이 자동으로 발생하며 취소할 수 없습니다. 필요한 경우 해당 구조를 업데이트할 권한이 있는 대체 DNS 관리 자격 증명을 제공할 수 있습니다.  
  
**DNS 옵션** ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
DNS 위임에 대한 자세한 내용은 [영역 위임 이해](https://technet.microsoft.com/library/cc771640.aspx)를 참조하세요.  
  
### <a name="additional-options"></a>추가 옵션  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildAdditionalOptions.png)  
  
**추가 옵션** 페이지에는 도메인의 NetBIOS 이름이 표시되며 이를 재정의할 수 있습니다. 기본적으로 NetBIOS 도메인 이름은 **배포 구성** 페이지에 제공된 정규화된 도메인 이름의 맨 왼쪽 레이블과 일치합니다. 예를 들어 corp.contoso.com의 정규화된 도메인 이름을 제공한 경우 기본 NetBIOS 도메인 이름은 CORP입니다.  
  
이름이 15자 이하이고 다른 NetBIOS 이름과 충돌하지 않으면 변경되지 않습니다. 반면, 다른 NetBIOS 이름과 충돌하면 이름에 숫자가 추가됩니다. 이름이 15자를 넘으면 마법사에서 잘린 고유 이름을 제안합니다. 두 경우 모두 마법사에서 WINS 조회 및 NetBIOS 브로드캐스트를 통해 해당 이름이 이미 사용 중이지 않은지 먼저 확인합니다.  
  
DNS 이름에 대한 자세한 내용은 [컴퓨터, 도메인, 사이트 및 OU에 대한 Active Directory의 명명 규칙](https://support.microsoft.com/kb/909264)을 참조하세요.  
  
**Install-AddsDomain** 인수는 서버 관리자와 동일한 기본값을 따릅니다(지정하지 않은 경우). **DomainNetBIOSName** 작업은 특별합니다.  
  
1.  **NewDomainNetBIOSName** 인수를 NetBIOS 도메인 이름과 함께 지정하지 않고 **DomainName** 인수의 단일 레이블 접두사 도메인 이름이 15자 이하인 경우 자동으로 생성된 이름으로 수준 올리기가 계속 진행됩니다.  
  
2.  **NewDomainNetBIOSName** 인수를 NetBIOS 도메인 이름과 함께 지정하지 않고 **DomainName** 인수의 단일 레이블 접두사 도메인 이름이 16자 이상인 경우 수준 올리기에 실패합니다.  
  
3.  **NewDomainNetBIOSName** 인수를 15자 이하의 NetBIOS 도메인 이름과 함께 지정한 경우 이 지정한 이름으로 수준 올리기가 계속 진행됩니다.  
  
4.  **NewDomainNetBIOSName** 인수를 16자 이상의 NetBIOS 도메인 이름과 함께 지정한 경우 수준 올리기에 실패합니다.  
  
**추가 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-newdomainnetbiosname <string>  
```  
  
### <a name="paths"></a>경로  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
**경로** 페이지에서 AD DS 데이터베이스, 데이터베이스 트랜잭션 로그 및 SYSVOL 공유의 기본 폴더 위치를 재정의할 수 있습니다. 기본 위치는 항상 %systemroot%의 하위 디렉터리입니다.  
  
**경로** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>옵션 검토 및 스크립트 보기  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildReviewOptions.png)  
  
**옵션 검토** 페이지에서 설치를 시작하기 전에 설정을 확인하고 이러한 설정이 요구 사항을 충족하는지도 확인할 수 있습니다. 이것이 서버 관리자를 사용할 때 설치를 중지할 수 있는 마지막 기회는 아닙니다. 구성을 계속하기 전에 설정을 확인하는 옵션일 뿐입니다.  
  
서버 관리자의 **옵션 검토** 페이지는 현재 ADDSDeployment 구성을 단일 Windows PowerShell 스크립트로 포함하는 유니코드 텍스트 파일을 만들 수 있도록 **스크립트 보기** 단추(선택 사항)도 제공합니다. 이 단추를 통해 서버 관리자 그래픽 인터페이스를 Windows PowerShell 배포 스튜디오로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용하여 옵션을 구성하고 구성을 내보낸 다음 마법사를 취소합니다.  이 프로세스를 통해 향후 수정을 위해 사용하거나 직접 사용하기 위한 유효하고 구문상으로 정확한 샘플이 만들어집니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomain `  
-NoGlobalCatalog:$false `  
-CreateDNSDelegation `  
-Credential (Get-Credential) `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainMode "Win2012" `  
-DomainType "ChildDomain" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-NewDomainName "research" `  
-NewDomainNetBIOSName "RESEARCH" `  
-ParentDomainName "corp.contoso.com" `  
-Norebootoncompletion:$false `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> 서버 관리자는 수준을 올릴 때 일반적으로 모든 인수의 값을 채우며 기본값에 의존하지 않습니다. 기본값은 향후 버전의 Windows 또는 서비스 팩 간에 변경될 수 있기 때문입니다. 단, **-safemodeadministratorpassword** 인수(스크립트에서 의도적으로 생략됨)는 예외입니다. 확인 프롬프트를 강제로 표시하려면 대화형으로 cmdlet을 실행할 때 이 값을 생략합니다.  
  
선택적 **Whatif** 인수를 **Install-ADDSForest** cmdlet과 함께 사용하여 구성 정보를 검토합니다. 이를 통해 cmdlet 인수의 명시적 및 암시적 값을 확인할 수 있습니다.  
  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildWhatIf.png)  
  
### <a name="prerequisites-check"></a>필수 구성 요소 확인  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildPrereqCheck.png)  
  
**필수 구성 요소 확인**은 AD DS 도메인 구성의 새로운 기능입니다. 이 새 단계에서는 서버 구성이 AD DS 도메인을 지원할 수 있는지 확인합니다.  
  
새 포리스트 루트 도메인을 설치할 때 서버 관리자 Active Directory 도메인 서비스 구성 마법사는 일련의 직렬화된 모듈식 테스트를 호출합니다. 이러한 테스트에서는 제안된 복구 옵션을 알려 줍니다. 필요한 만큼 여러 번 테스트를 실행할 수 있습니다. 모든 필수 구성 요소 테스트를 통과해야만 도메인 컨트롤러 프로세스를 계속 진행할 수 있습니다.  
  
**필수 구성 요소 확인**에서는 이전 운영 체제에 영향을 주는 보안 변경 내용과 같은 관련 정보도 제공합니다.  
  
특정 필수 구성 요소 검사에 대 한 자세한 내용은 참조 하십시오. [필수 구성 요소 확인](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)합니다.  
  
서버 관리자를 사용할 때는 **필수 구성 요소 확인** 을 무시할 수 없지만 AD DS 배포 cmdlet을 사용할 때는 다음 인수를 사용하여 프로세스를 건너뛸 수 있습니다.  
  
```  
-skipprechecks  
```  
  
> [!WARNING]  
> 필수 구성 요소 확인을 건너뛰면 도메인 컨트롤러 수준 올리기가 부분적으로 완료되거나 AD DS 포리스트가 손상될 수 있으므로 건너뛰지 않는 것이 좋습니다.  
  
**설치**를 클릭하여 도메인 컨트롤러 수준 올리기 프로세스를 시작합니다. 이때가 설치를 취소할 수 있는 마지막 기회입니다. 시작된 후에는 수준 올리기 프로세스를 취소할 수 없습니다. 수준 올리기가 끝나면 수준 올리기 결과에 상관없이 컴퓨터가 자동으로 다시 부팅됩니다.  
  
### <a name="installation"></a>설치  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildInstallation.png)  
  
**설치** 페이지가 표시되면 도메인 컨트롤러 구성이 시작되며 이는 중지하거나 취소할 수 없습니다. 세부 작업이 이 페이지에 표시되고 다음 로그에 기록됩니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment 모듈을 사용하여 새 Active Directory 도메인을 설치하려면 다음 cmdlet을 사용합니다.  
  
```  
Install-addsdomain  
```  
  
필수 및 선택적 인수는 [자식 및 트리 도메인 Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)을 참조하세요. **Install-addsdomain** cmdlet은 두 단계(필수 구성 요소 확인 및 설치)만 수행합니다. 아래 두 그림에는 최소 필수 인수인 **-domaintype**, **-newdomainname**, **-parentdomainname** 및 **-credential**을 사용한 설치 단계가 나와 있습니다. 서버 관리자와 마찬가지로 **Install-ADDSDomain**에서도 수준 올리기 후 서버가 자동으로 다시 부팅됨을 미리 알려 줍니다.  
  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomain.png)  
  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomainProgress.png)  
  
다시 부팅 프롬프트를 자동으로 허용하려면 임의의 ADDSDeployment Windows PowerShell cmdlet에서 **-force** 또는 **-confirm:$false** 인수를 사용합니다. 수준 올리기가 끝난 후 서버가 자동으로 다시 부팅되는 것을 방지하려면 **-norebootoncompletion** 인수를 사용합니다.  
  
> [!WARNING]  
> 다시 부팅을 무시하지 않는 것이 좋습니다. 도메인 컨트롤러가 올바르게 작동하려면 다시 부팅해야 합니다.  
  
### <a name="results"></a>결과  
![새 AD 자식 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**결과** 페이지에는 수준 올리기의 성공 또는 실패와 중요한 관리 정보가 표시됩니다. 10초 후 도메인 컨트롤러가 자동으로 다시 부팅됩니다.  
  

