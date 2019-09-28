---
ms.assetid: 65ed5956-6140-4e06-8d99-8771553637d1
title: 도메인 컨트롤러 및 도메인 수준 내리기(수준 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 00f3851ce74a496bd530c8ea682ea312f8b06a0a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390924"
---
# <a name="demoting-domain-controllers-and-domains"></a>도메인 컨트롤러 및 도메인 수준 내리기

>적용 대상: Windows Server

이 항목에서는 서버 관리자 또는 Windows PowerShell을 사용하여 AD DS를 제거하는 방법에 대해 설명합니다.
  
## <a name="ad-ds-removal-workflow"></a>AD DS 제거 워크플로

![AD DS 제거 워크플로 차트](media/Demoting-Domain-Controllers-and-Domains--Level-200-/adds_demotedomainforest.png)  

> [!CAUTION]
> 도메인 컨트롤러로 수준을 올린 후 Dism.exe 또는 Windows PowerShell DISM 모듈을 사용하여 AD DS 역할을 제거하는 작업은 지원되지 않으며, 이 작업을 수행할 경우 서버가 정상적으로 부팅되지 않습니다.
>
> 서버 관리자 또는 Windows PowerShell용 ADDSDeployment 모듈과 달리 DISM은 AD DS 또는 해당 구성에 대한 내재된 지식이 없는 기본 서비스 시스템입니다. 서버가 더 이상 도메인 컨트롤러가 아닌 경우 외에는 Dism.exe 또는 Windows PowerShell DISM 모듈을 사용하여 AD DS 역할을 제거하지 마세요.

## <a name="demotion-and-role-removal-with-powershell"></a>PowerShell을 사용 하 여 수준 내리기 및 역할 제거

|||  
|-|-|  
|**ADDSDeployment 및 ServerManager Cmdlet**|인수(**굵게** 표시된 인수는 필수 항목이며, *기울임꼴* 인수는 Windows PowerShell 또는 AD DS 구성 마법사를 사용하여 지정할 수 있음)|  
|Uninstall-AddsDomainController|-SkipPreChecks<br /><br />*-LocalAdministratorPassword*<br /><br />-Confirm<br /><br />***-Credential***<br /><br />-DemoteOperationMasterRole<br /><br />*-DNSDelegationRemovalCredential*<br /><br />-Force<br /><br />*-ForceRemoval*<br /><br />*-IgnoreLastDCInDomainMismatch*<br /><br />*-IgnoreLastDNSServerForZone*<br /><br />*-LastDomainControllerInDomain*<br /><br />-Norebootoncompletion<br /><br />*-RemoveApplicationPartitions*<br /><br />*-RemoveDNSDelegation*<br /><br />-RetainDCMetadata|  
|Uninstall-WindowsFeature/Remove-WindowsFeature|***-Name***<br /><br />***-IncludeManagementTools***<br /><br />*-Restart*<br /><br />-Remove<br /><br />-Force<br /><br />-ComputerName<br /><br />-Credential<br /><br />-LogPath<br /><br />-Vhd|  
  
> [!NOTE]  
> **-credential** 인수는 Enterprise Admins 그룹(도메인의 마지막 DC 수준 내리기) 또는 Domain Admins 그룹(복제본 DC 수준 내리기)의 구성원으로 아직 로그온하지 않은 경우에만 필요하고, **-includemanagementtools** 인수는 모든 AD DS 관리 유틸리티를 제거하려는 경우에만 필요합니다.  
  
## <a name="demote"></a>수준 내리기  
  
### <a name="remove-roles-and-features"></a>역할 및 기능 제거

서버 관리자에서는 다음 두 가지 인터페이스에서 Active Directory 도메인 서비스 역할을 제거할 수 있습니다.  
  
* 기본 대시보드의 **관리** 메뉴에서 **역할 및 기능 제거**를 사용합니다.  

   ![서버 관리자-역할 및 기능 제거](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Manage.png)  

* 탐색 창에서 **AD DS** 또는 **모든 서버**를 클릭합니다. 아래의 **역할 및 기능** 섹션으로 스크롤합니다. **역할 및 기능** 목록에서 **Active Directory 도메인 서비스**를 마우스 오른쪽 단추로 클릭한 다음 **역할 또는 기능 제거**를 클릭합니다. 이 인터페이스에서는 **서버 선택** 페이지를 건너뜁니다.  

   ![서버 관리자-모든 서버-역할 및 기능 제거](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection.png)  

ServerManager **cmdlet을 제거 하면** 도메인 컨트롤러의 수준을 내릴 때까지 AD DS **역할이 제거 되지 않습니다.**
  
### <a name="server-selection"></a>서버 선택

![역할 및 기능 제거 마법사 대상 서버 선택](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection2.png)  

**서버 선택** 대화 상자에서는 이전에 풀에 추가한 서버 중 하나를 선택할 수 있습니다(액세스 가능한 경우). 서버 관리자를 실행하는 로컬 서버는 항상 자동으로 사용할 수 있습니다.  

### <a name="server-roles-and-features"></a>서버 역할 및 기능

![역할 및 기능 제거 마법사-제거할 역할 선택](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerRoles.png)  

도메인 컨트롤러의 수준을 내리려면 **Active Directory 도메인 서비스** 확인란의 선택을 취소합니다. 이때 서버가 현재 도메인 컨트롤러인 경우에는 AD DS 역할이 제거되지 않고 대신 수준 내리기를 제안하는 **유효성 검사 결과**로 전환됩니다. 그렇지 않으면 다른 역할 기능과 마찬가지로 이진 파일이 제거 됩니다.  

* 곧바로 도메인 컨트롤러의 수준을 다시 올리려는 경우에는 다른 AD DS 관련 역할 또는 기능(예: DNS, GPMC 또는 RSAT 도구)을 제거하지 마세요. 추가 역할 및 기능을 제거하면 역할을 다시 설치할 때 서버 관리자에서 이러한 기능을 재설치하므로 다시 수준을 올리는 데 시간이 오래 걸립니다.  
* 도메인 컨트롤러를 영구적으로 수준을 내리려는 경우에는 재량에 따라 불필요한 AD DS 역할 및 기능을 제거합니다. 그러려면 해당 역할 및 기능에 대한 확인란의 선택을 취소해야 합니다.  

   AD DS 관련 역할 및 기능의 전체 목록에는 다음이 포함됩니다.  
  
   * Windows PowerShell용 Active Directory 모듈 기능  
   * AD DS 및 AD LDS 도구 기능  
   * Active Directory 관리 센터 기능  
   * AD DS 스냅인 및 명령줄 도구 기능  
   * DNS 서버  
   * 그룹 정책 관리 콘솔  
  
상응하는 ADDSDeployment 및 ServerManager Windows PowerShell cmdlet은 다음과 같습니다.  
  
```
Uninstall-addsdomaincontroller  
Uninstall-windowsfeature  
```

![역할 및 기능 제거 마법사-확인 대화 상자](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_RemoveFeatures.png)  

![역할 및 기능 제거 마법사-유효성 검사](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demote.png)  

### <a name="credentials"></a>자격 증명

![Active Directory Domain Services 구성 마법사-자격 증명 선택](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Credentials.png)  

**자격 증명** 페이지에서 수준 내리기 옵션을 구성합니다. 다음 목록에서 수준 내리기를 수행하는 데 필요한 자격 증명을 제공합니다.  

* 추가 도메인 컨트롤러의 수준을 내리려면 Domain Admin 자격 증명이 필요합니다. **이 도메인 컨트롤러 강제 제거를** 선택 하면 Active Directory에서 도메인 컨트롤러 개체의 메타 데이터를 제거 하지 않고 도메인 컨트롤러의 수준을 내립니다.  

   > [!WARNING]  
   > 도메인 컨트롤러에서 다른 도메인 컨트롤러에 연결할 수 없고 해당 네트워크 문제를 해결할 *합리적인 방법이 없는* 경우가 아니면 이 옵션을 선택하지 마십시오. 강제로 수준을 내리면 포리스트에서 남아 있는 도메인 컨트롤러의 Active Directory에서 메타데이터가 분리되게 됩니다. 또한 암호나 새 사용자 계정과 같이 해당 도메인 컨트롤러에서 복제되지 않은 모든 변경 사항이 영구 손실됩니다. 분리된 메타데이터는 AD DS, Exchange, SQL 및 기타 소프트웨어와 관련한 Microsoft 고객 지원 사례의 상당 부분을 차지하는 근본 원인입니다.  
   >
   > 도메인 컨트롤러의 수준을 강제로 내리려면 바로 메타데이터 정리 작업을 수동으로 *수행해야 합니다*. 단계에 대 한 검토 [서버 메타 데이터 정리](https://technet.microsoft.com/library/cc816907(WS.10).aspx)합니다.  

   ![Active Directory Domain Services 구성 마법사-자격 증명 강제 제거](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ForceDemote.png)  
  
* 도메인에서 마지막 도메인 컨트롤러의 수준을 내리려면 이 작업은 도메인 자체를 제거(포리스트의 마지막 도메인일 경우 포리스트 자체가 제거됨)하므로 Enterprise Admins 그룹의 구성원이어야 합니다. 서버 관리자는 현재 도메인 컨트롤러가 도메인의 마지막 도메인 컨트롤러인지 여부를 알려줍니다. **도메인의 마지막 도메인 컨트롤러** 확인란을 선택하여 도메인 컨트롤러가 도메인의 마지막 도메인 컨트롤러인지 확인합니다.  

상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  

```
-credential <pscredential>  
-forceremoval <{ $true | false }>  
-lastdomaincontrollerindomain <{ $true | false }>  
```

### <a name="warnings"></a>경고

![Active Directory Domain Services 구성 마법사-자격 증명 FSMO 역할 영향](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Warnings.png)  

**경고** 페이지에서는 이 도메인 컨트롤러를 제거할 경우 가능한 결과를 알려 줍니다. 계속하려면 **제거 진행**을 선택해야 합니다.

> [!WARNING]  
> 이전에 **자격 증명** 페이지에 **이 도메인 컨트롤러 강제 제거**를 선택한 경우 **경고** 페이지에 이 도메인 컨트롤러에서 호스트하는 모든 FSMO(Flexible Single Master Operations)가 표시됩니다. 이 서버의 수준을 내리는 *즉시* 다른 도메인 컨트롤러의 역할을 점유 *해야* 합니다. FSMO 역할 점유에 대 한 자세한 내용은 참조 하십시오. [작업 마스터 역할 점유](https://technet.microsoft.com/library/cc816779(WS.10).aspx)합니다.

이 페이지에는 상응하는 ADDSDeployment Windows PowerShell 인수가 없습니다.

### <a name="removal-options"></a>제거 옵션

![Active Directory Domain Services 구성 마법사-자격 증명 DNS 및 응용 프로그램 파티션 제거](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ReviewOptions.png)  

이전에 **자격 증명** 페이지에서 선택한 **도메인의 마지막 도메인 컨트롤러**에 따라 **제거 옵션** 페이지가 표시됩니다. 이 페이지에서 추가 제거 옵션을 구성할 수 있습니다. **영역에 대 한 마지막 DNS 서버 무시**, **응용 프로그램 파티션 제거**및 **DNS 위임 제거** 를 선택 하 여 **다음** 단추를 사용 하도록 설정 합니다.

이러한 옵션은 이 도메인 컨트롤러에 적용되는 경우에만 표시됩니다. 예를 들어 이 서버에 대한 DNS 위임이 없는 경우에는 해당 확인란이 표시되지 않습니다.

**변경**을 클릭하여 대체 DNS 관리 자격 증명을 지정합니다. **파티션 보기**를 클릭하여 수준을 내리는 동안 마법사에서 제거하는 추가 파티션을 볼 수 있습니다. 기본적으로 추가 파티션은 도메인 DNS 및 포리스트 DNS 영역뿐입니다. 다른 모든 파티션은 Windows가 아닌 파티션입니다.

상응하는 ADDSDeployment cmdlet 인수는 다음과 같습니다.  

```
-ignorelastdnsserverforzone <{ $true | false }>  
-removeapplicationpartitions <{ $true | false }>  
-removednsdelegation <{ $true | false }>  
-dnsdelegationremovalcredential <pscredential>  
```

### <a name="new-administrator-password"></a>새 관리자 암호

![Active Directory Domain Services 구성 마법사-자격 증명 새 관리자 암호](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_NewAdminPwd.png)  

**새 관리자 암호** 페이지 수준 내리기를 완료 되 고 컴퓨터가 도메인 구성원 서버나 작업 그룹 컴퓨터에 기본 제공 로컬 컴퓨터의 관리자 계정에 대 한 암호를 제공 해야 합니다.

**Uninstall-addsdomaincontroller** cmdlet 및 인수는 서버 관리자와 동일한 기본값을 따릅니다(지정하지 않은 경우).

**LocalAdministratorPassword** 인수는 특별합니다.

* 인수로 *지정하지 않은* 경우 이 cmdlet은 마스킹된 암호를 입력 및 확인하라는 메시지를 표시합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법입니다.
* *값과 함께*지정한 경우 값은 보안 문자열이어야 합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법이 아닙니다.

예를 들어, 사용자에 게 보안 문자열을 입력 하 라는 메시지를 표시 하는 **읽기-호스트** cmdlet을 사용 하 여 암호를 수동으로 확인할 수 있습니다.

```
-localadministratorpassword (read-host -prompt "Password:" -assecurestring)
```

> [!WARNING]
> 위의 두 옵션은 암호를 확인 하지 않으므로 각별히 주의 해야 합니다. 암호는 표시 되지 않습니다.

변환된 일반 텍스트 변수로 보안 문자열을 제공할 수도 있습니다(권장되지 않음). 예를 들어 다음과 같은 가치를 제공해야 합니다.

```
-localadministratorpassword (convertto-securestring "Password1" -asplaintext -force)
```

> [!WARNING]
> 일반 텍스트 암호는 제공하거나 저장하지 않는 것이 좋습니다. 스크립트에서 이 명령을 실행하는 사용자나 어깨 너머로 보고 있는 다른 사용자가 해당 컴퓨터의 로컬 관리자 암호를 알게 될 수 있습니다. 이 정보를 알면 모든 데이터에 액세스할 수 있으며, 서버 자체를 가장할 수 있습니다.

### <a name="confirmation"></a>확인

![Active Directory Domain Services 구성 마법사-검토 옵션](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Confirmation.png)

**확인** 페이지에는 계획된 수준 내리기가 표시됩니다. 수준 내리기 구성 옵션은 이 페이지에 나열되지 않습니다. 이 페이지는 수준 내리기가 시작되기 전에 마법사에 표시되는 마지막 페이지입니다. 스크립트 보기 단추를 클릭하면 Windows PowerShell 수준 내리기 스크립트가 만들어집니다.

**수준 내리기**를 클릭하여 다음 AD DS 배포 cmdlet을 실행합니다.

```
Uninstall-DomainController
```

선택적 **Whatif** 인수를 **Uninstall-ADDSDomainController** 및 cmdlet과 함께 사용하여 구성 정보를 검토합니다. 이를 통해 cmdlet 인수의 명시적 및 암시적 값을 확인할 수 있습니다.

예를 들어 다음과 같은 가치를 제공해야 합니다.

![PowerShell 제거-Install-addsdomaincontroller 예제](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstall.png)

다시 시작할지 묻는 메시지가 표시될 때가 ADDSDeployment Windows PowerShell을 사용할 때 이 작업을 취소할 수 있는 마지막 기회입니다. 이 메시지를 무시하려면 **-force** 또는 **confirm:$false** 인수를 사용합니다.  

### <a name="demotion"></a>수준 내리기

![Active Directory Domain Services 구성 마법사-강등 중](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demotion.png)  

**수준 내리기** 페이지가 표시되면 도메인 컨트롤러 구성이 시작되며 이는 중지하거나 취소할 수 없습니다. 세부 작업이 이 페이지에 표시되고 다음 로그에 기록됩니다.  

* %systemroot%\debug\dcpromo.log
* %systemroot%\debug\dcpromoui.log

**Uninstall-AddsDomainController** 및 **Uninstall-WindowsFeature**는 각각 하나의 작업만 수행하므로 확인 단계에서 최소 필수 인수와 함께 여기에 표시됩니다. Enter 키를 누르면 취소할 수 없는 수준 내리기 프로세스가 시작되고 컴퓨터가 다시 시작됩니다.

![PowerShell 제거-Install-addsdomaincontroller 예제](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallConfirm.png)

![PowerShell Uninstall-Add-windowsfeature 예제](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallWindowsFeature.png)

다시 부팅 프롬프트를 자동으로 허용하려면 임의의 ADDSDeployment Windows PowerShell cmdlet에서 **-force** 또는 **-confirm:$false** 인수를 사용합니다. 수준 올리기가 끝난 후 서버가 자동으로 다시 부팅되는 것을 방지하려면 **-norebootoncompletion:$false** 인수를 사용합니다.

> [!WARNING]
> 다시 부팅을 무시하지 않는 것이 좋습니다. 구성원 서버가 올바르게 작동하려면 다시 부팅해야 합니다.

![PowerShell 제거-Install-addsdomaincontroller Force 예제](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallFinished.png)

다음 예제에서는 최소 필수 인수 **-forceremoval** 및 **-demoteoperationmasterrole**로 강제로 수준을 내립니다. 사용자가 Enterprise Admins 그룹의 구성원으로 로그온되었으므로 **-credential** 인수는 필요하지 않습니다.

![PowerShell 제거-Install-addsdomaincontroller 예제](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleForce.png)

다음은 최소 필수 인수인 **-lastdomaincontrollerindomain** 및 **-removeapplicationpartitions**를 사용하여 도메인의 마지막 도메인 컨트롤러를 제거하는 예제입니다.

![PowerShell Install-addsdomaincontroller-LastDomainControllerInDomain 예제](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleLastDC.png)

서버의 수준을 내리기 전에 AD DS 역할을 제거 하려고 하면 Windows PowerShell에서 오류를 차단 합니다.

![AD-도메인 서비스를 제거 하는 동안 제거 필수 조건 단계를 수행 하지 못했으며 제거를 계속할 수 없습니다. 1. 도메인 컨트롤러는 Active Directory 도메인 서비스 역할을 제거 하기 전에 강등 해야 합니다.](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallError.png)

> [!IMPORTANT]
> 서버의 수준을 내린 후 컴퓨터를 다시 시작해야 AD-Domain-Services 역할 파일을 제거할 수 있습니다.

### <a name="results"></a>결과

![AD DS를 제거한 후에도 로그 오프 하려고 합니다.](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_DemoteSignoff.png)

**결과** 페이지에는 수준 올리기의 성공 또는 실패와 중요한 관리 정보가 표시됩니다. 10초 후 도메인 컨트롤러가 자동으로 다시 부팅됩니다.
