---
ms.assetid: e6da5984-d99d-4c34-9c11-4a18cd413f06
title: 기존 도메인에 복제 Windows Server 2012 도메인 컨트롤러 설치(수준 200)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 12068e5a062358463cf208f777144091e1de8257
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825206"
---
# <a name="install-a-replica-windows-server-2012-domain-controller-in-an-existing-domain-level-200"></a>기존 도메인에 복제 Windows Server 2012 도메인 컨트롤러 설치(수준 200)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 서버 관리자 또는 Windows PowerShell을 사용하여 기존 포리스트나 도메인을 Windows Server 2012로 업그레이드하는 데 필요한 단계를 설명하며, Windows Server 2012를 실행하는 도메인 컨트롤러를 기존 도메인에 추가하는 방법을 알아봅니다.  
  
-   [업그레이드 및 복제본 워크플로](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [업그레이드 및 복제본 Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)  
  
-   [배포](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Dep)  
  
## <a name="upgrade-and-replica-workflow"></a><a name="BKMK_Workflow"></a>업그레이드 및 복제본 워크플로  
다음 다이어그램에서는 이전에 AD DS 역할을 설치하고 서버 관리자를 사용하여 기존 도메인에서 새 도메인 컨트롤러를 만드는 Active Directory 도메인 서비스 구성 마법사를 시작한 경우의 Active Directory 도메인 서비스 구성 프로세스를 보여 줍니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/adds_forestupgrade.png)  
  
## <a name="upgrade-and-replica-windows-powershell"></a><a name="BKMK_PS"></a>업그레이드 및 복제본 Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수(**굵게** 표시된 인수는 필수 항목이며, *기울임꼴* 인수는 Windows PowerShell 또는 AD DS 구성 마법사를 사용하여 지정할 수 있음)|  
|Install-AddsDomainController|-SkipPreChecks<p>***-DomainName***<p>*-SafeModeAdministratorPassword*<p>*-SiteName*<p>*-ADPrepCredential*<p>-ApplicationPartitionsToReplicate<p>*-AllowDomainControllerReinstall*<p>-Confirm<p>*-CreateDNSDelegation*<p>***-Credential***<p>-CriticalReplicationOnly<p>*-DatabasePath*<p>*-DNSDelegationCredential*<p>-Force<p>*-InstallationMediaPath*<p>*-InstallDNS*<p>*-LogPath*<p>-MoveInfrastructureOperationMasterRoleIfNecessary<p>-NoDnsOnNetwork<p>*-NoGlobalCatalog*<p>-Norebootoncompletion<p>*-ReplicationSourceDC*<p>-SkipAutoConfigureDNS<p>-SiteName<p>*-SystemKey*<p>*-SYSVOLPath*<p>*-UseExistingAccount*<p>*-Whatif*|  
  
> [!NOTE]  
> **-credential** 인수는 현재 Enterprise Admins 및 Schema Admins 그룹의 구성원(포리스트를 업그레이드하는 경우) 또는 Domain Admins 그룹의 구성원(기존 도메인에 새 DC를 추가하는 경우)으로 로그인되어 있지 않은 경우에만 필요합니다.  
  
## <a name="deployment"></a><a name="BKMK_Dep"></a>배포가  
  
### <a name="deployment-configuration"></a>배포 구성  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDeployConfig.png)  
  
서버 관리자는 **배포 구성** 페이지에서 모든 도메인 컨트롤러 수준 올리기를 시작합니다. 선택한 배포 작업에 따라 이 페이지 및 다음 페이지에 표시되는 나머지 옵션 및 필수 필드가 바뀝니다.  
  
기존 포리스트를 업그레이드하거나 쓰기 가능한 도메인 컨트롤러를 기존 도메인에 추가하려면 클릭 **기존 도메인에 도메인 컨트롤러 추가** 를 클릭한 다음 **선택** 을 클릭하여 **이 작업에 대한 도메인 정보를 지정합니다**. 필요한 경우 서버 관리자에 유효한 자격 증명을 제공하라는 메시지가 표시됩니다.  
  
포리스트를 업그레이드하려면 Windows Server 2012의 Enterprise Admins 그룹 구성원 자격과 Schema Admins 그룹 구성원 자격을 둘 다 포함하는 자격 증명이 있어야 합니다. 현재 자격 증명에 적절한 사용 권한이나 그룹 구성원이 없는 경우 나중에 Active Directory Domain Services 구성 마법사에 자격 증명을 제공하라는 메시지가 표시됩니다.  
  
기존 Windows Server 2012 도메인과 도메인 컨트롤러에서 이전 버전의 Windows Server를 실행하는 도메인에 도메인 컨트롤러를 추가하는 작업 간의 차이점은 자동 Adprep 프로세스뿐입니다.  
  
배포 구성 ADDSDeployment cmdlet 및 인수는 다음과 같습니다.  
  
```  
Install-AddsDomainController  
-domainname <string>  
-credential <pscredential>  
```  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeSelectDomain.png)  
  
특정 테스트는 각 페이지에서 수행되며, 일부 테스트는 나중에 개별 필수 구성 요소 확인으로 반복됩니다. 예를 들어 선택한 도메인이 최소 기능 수준을 충족하지 않으면 수준 올리기부터 필수 구성 요소 확인까지 모든 과정을 수행할 필요가 없습니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeFFLError.png)  
  
### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptions.png)  
  
**도메인 컨트롤러 옵션** 페이지에서는 새 도메인 컨트롤러에 대한 도메인 컨트롤러 기능을 지정합니다. 구성 가능한 도메인 컨트롤러 기능에는 **DNS 서버**, **글로벌 카탈로그** 및 **읽기 전용 도메인 컨트롤러**가 포함됩니다. 분산된 환경에서의 고가용성을 위해 모든 도메인 컨트롤러에서 DNS 및 GC 서비스를 제공하는 것이 좋습니다. GC는 항상 기본적으로 선택되며, DNS 서버는 현재 도메인에서 권한 시작 쿼리를 기반으로 해당 DC에 이미 있는 DNS를 호스트하는 경우 기본적으로 선택됩니다. **도메인 컨트롤러 옵션** 페이지에서는 포리스트 구성에서 적절한 Active Directory 논리 **사이트 이름** 을 선택할 수도 있습니다. 기본적으로 가장 정확한 서브넷을 포함한 사이트가 선택됩니다. 사이트가 1개만 있는 경우 자동으로 해당 사이트가 선택됩니다.  
  
> [!NOTE]  
> 서버가 어떠한 Active Directory 서브넷에도 속해 있지 않고 둘 이상의 Active Directory 사이트가 있는 경우에는 아무 항목도 선택되지 않습니다. 이 경우 목록에서 사이트를 선택해야 **다음** 단추를 사용할 수 있습니다.  
  
지정한 **디렉터리 서비스 복원 모드 암호** 는 서버에 적용되는 암호 정책을 준수해야 합니다. 항상 강력하고 복잡한 암호 또는 암호 문구를 선택하십시오.  
  
**도메인 컨트롤러 옵션** ADDSDeployment 인수는 다음과 같습니다.  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-sitename <string>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> **-sitename**에 대한 인수로 제공된 경우 사이트 이름이 이미 존재해야 합니다. **install-AddsDomainController** cmdlet은 사이트를 만들지 않습니다. **new-adreplicationsite** cmdlet을 사용하여 새 사이트를 만들 수 있습니다.  
  
**SafeModeAdministratorPassword** 인수의 작업은 특별합니다.  
  
-   인수로 *지정하지 않을 경우* cmdlet은 마스킹된 암호를 입력 및 확인하라는 메시지를 표시합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법입니다.  
  
    예를 들어 treyresearch.net 도메인에 추가 도메인 컨트롤러를 만들고 마스킹된 암호를 입력하고 확인하라는 메시지를 표시하려면 다음 명령을 실행합니다.  
  
    ```  
    Install-ADDSDomainController "DomainName treyresearch.net "credential (get-credential)  
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
  
마지막으로 난독 처리된 암호를 파일에 저장한 다음 일반 텍스트 암호를 표시하지 않고 나중에 다시 사용할 수 있습니다. 예를 들면 다음과 같습니다.  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> 일반 또는 난독 처리된 텍스트 암호는 제공하거나 저장하지 않는 것이 좋습니다. 스크립트에서 이 명령을 실행하는 사용자나 어깨 너머로 보고 있는 다른 사용자가 해당 도메인 컨트롤러의 DSRM 암호를 알게 될 수 있습니다.  파일에 액세스할 수 있는 모든 사람이 난독 처리된 암호를 반전시킬 수 있습니다. 이 정보를 알면 DSRM에서 시작된 DC에 로그온하여 도메인 컨트롤러 자체를 가장함으로써 Active Directory 포리스트에서 가장 높은 수준으로 해당 권한을 상승시킬 수 있습니다. **System.Security.Cryptography**를 사용하여 텍스트 파일 데이터를 암호화하는 추가 단계를 수행하는 것이 좋지만 이러한 단계는 이 문서의 범위를 벗어납니다. 암호 저장을 완전히 피하는 것이 가장 좋습니다.  
  
ADDSDeployment cmdlet에서는 DNS 클라이언트 설정, 전달자 및 루트 힌트의 자동 구성을 건너뛸 수 있는 추가 옵션을 제공합니다. 서버 관리자를 사용할 때는 이 구성 옵션을 건너뛸 수 없습니다. 이 인수는 도메인 컨트롤러를 구성하기 전에 DNS 서버 역할을 설치한 경우에만 적용됩니다.  
  
```  
-SkipAutoConfigureDNS  
```  
  
**도메인 컨트롤러 옵션** 페이지에는 기존 도메인 컨트롤러에서 Windows Server 2003을 실행하는 경우 읽기 전용 도메인 컨트롤러를 만들 수 없다는 경고가 표시됩니다. 이는 예상된 동작이며 경고를 해제할 수 있습니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptionsError.png)  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS 옵션 및 DNS 위임 자격 증명  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDNSOptions.png)  
  
**DNS 옵션** 페이지에서는 **도메인 컨트롤러 옵션** 페이지에서 *DNS 서버* 옵션을 선택한 경우 및 DNS 위임이 허용되는 영역을 가리키는 경우 DNS 위임을 구성할 수 있습니다. **DNS Admins** 그룹의 구성원인 사용자의 대체 자격 증명을 제공해야 할 수도 있습니다.  
  
**DNS 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
DNS 위임을 업데이트해야 하는지 여부에 대한 자세한 내용은 [영역 위임 이해](https://technet.microsoft.com/library/cc771640.aspx)를 참조하세요.  
  
### <a name="additional-options"></a>추가 옵션  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeAdditionalOptions.png)  
  
**추가 옵션** 페이지에서는 도메인 컨트롤러 이름을 복제 원본으로 지정하는 구성 옵션을 제공하거나 원하는 도메인 컨트롤러를 복제 원본으로 사용할 수 있습니다.  
  
또한 IFM(미디어에서 설치) 옵션을 통해 백업된 미디어를 사용하여 도메인 컨트롤러를 설치하도록 선택할 수도 있습니다. **미디어에서 설치** 확인란을 선택하면 찾아보기 옵션이 제공되며 **확인** 을 클릭하여 제공된 경로가 유효한 미디어임을 확인해야 합니다. IFM 옵션에서 사용된 미디어는 기존의 다른 Windows Server 2012 컴퓨터의 Ntdsutil.exe나 Windows Server 백업으로만 만들어야 합니다. Windows Server 2008 R2나 이전 운영 체제를 사용하여 Windows Server 2012 도메인 컨트롤러용 미디어를 만들 수 없습니다. IFM의 변경 내용에 대한 자세한 내용은 [간소화된 관리 부록](../../ad-ds/deploy/Simplified-Administration-Appendix.md)을 참조하세요. SYSKEY로 보호된 미디어를 사용하는 경우 검증하는 동안 서버 관리자에는 이미지 암호를 제공하라는 메시지가 표시됩니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_NtdsutilIFM.png)  
  
**추가 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-syskey <secure string>  
```  
  
### <a name="paths"></a>경로  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
**경로** 페이지에서 AD DS 데이터베이스, 데이터베이스 트랜잭션 로그 및 SYSVOL 공유의 기본 폴더 위치를 재정의할 수 있습니다. 기본 위치는 항상 %systemroot%의 하위 디렉터리입니다.  
  
Active Directory 경로 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>준비 옵션  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptions.png)  
  
**준비 옵션** 페이지에서는 AD DS 구성에 스키마 확장(forestprep) 및 도메인 업데이트(domainprep)가 포함되어 있음을 알려 줍니다.  이 페이지는 이전 Windows Server 2012 도메인 컨트롤러 설치 또는 Adprep.exe 수동 실행에서 포리스트 및 도메인이 준비되지 않은 경우에만 표시됩니다. 예를 들어 기존 Windows Server 2012 포리스트 루트 도메인에 새 도메인 컨트롤러를 추가하는 경우에는 Active Directory Domain Services 구성 마법사에서 이 페이지를 표시하지 않습니다.  
  
**다음**을 클릭하면 스키마 확장 및 도메인 업데이트가 실행되지 않습니다. 이러한 이벤트는 설치 단계 중에만 발생합니다. 이 페이지는 설치 후반에서 발생할 이벤트를 알려 주는 역할만 합니다.  
  
또한 스키마를 확장하거나 도메인을 준비하려면 Schema Admin 및 Enterprise Admins 그룹의 구성원 자격이 필요하므로 이 페이지에서는 현재 사용자 자격 증명이 이러한 그룹의 구성원인지 확인합니다. 이 페이지에 현재 자격 증명의 권한이 부족하다는 메시지가 표시되면 **변경**을 클릭하여 적절한 사용자 자격 증명을 제공합니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptionsCreds.png)  
  
추가 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> 이전 버전의 Windows Server와 마찬가지로 Windows Server 2012를 실행하는 도메인 컨트롤러에 대한 자동화된 도메인 준비에서는 GPPREP를 실행하지 않습니다. 이전에 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 R2가 준비되지 않은 모든 도메인에 대해 **adprep.exe /gpprep** 를 수동으로 실행하세요. 업그레이드마다 실행하지 말고 도메인 기록에서 GPPrep를 한 번만 실행해야 합니다. Adprep.exe는 /gpprep를 자동으로 실행하지 않습니다. 자동으로 실행할 경우 SYSVOL 폴더의 모든 파일 및 폴더가 모든 도메인 컨트롤러에서 다시 복제될 수 있기 때문입니다.  
>   
> 자동 RODCPrep는 도메인에서 준비되지 않은 첫 번째 RODC의 수준을 올릴 때 실행됩니다. 쓰기 가능한 첫 번째 Windows Server 2012 도메인 컨트롤러의 수준을 올릴 때는 실행되지 않습니다. 또한 읽기 전용 도메인 컨트롤러를 배포하려는 경우에도 **adprep.exe /rodcprep** 를 수동으로 실행할 수 있습니다.  
  
### <a name="review-options-and-view-script"></a>옵션 검토 및 스크립트 보기  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeReviewOptions.png)  
  
**옵션 검토** 페이지에서 설치를 시작하기 전에 설정을 확인하고 이러한 설정이 요구 사항을 충족하는지도 확인할 수 있습니다. 서버 관리자를 사용하여 설치를 중지할 수 있는 마지막 기회는 아닙니다. 이 페이지에서는 단지 구성을 계속하기 전에 설정을 검토하고 확인합니다.  
  
서버 관리자의 **옵션 검토** 페이지는 현재 ADDSDeployment 구성을 단일 Windows PowerShell 스크립트로 포함하는 유니코드 텍스트 파일을 만들 수 있도록 **스크립트 보기** 단추(선택 사항)도 제공합니다. 이 단추를 통해 서버 관리자 그래픽 인터페이스를 Windows PowerShell 배포 스튜디오로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용하여 옵션을 구성하고 구성을 내보낸 다음 마법사를 취소합니다.  이 프로세스를 통해 향후 수정을 위해 사용하거나 직접 사용하기 위한 유효하고 구문상으로 정확한 샘플이 만들어집니다.  
  
예를 들면 다음과 같습니다.  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-CreateDNSDelegation `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainName "root.fabrikam.com" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> 서버 관리자는 수준을 올릴 때 일반적으로 모든 인수의 값을 채우며 기본값에 의존하지 않습니다. 기본값은 향후 버전의 Windows 또는 서비스 팩 간에 변경될 수 있기 때문입니다. 단, **-safemodeadministratorpassword** 인수는 예외입니다. 확인 프롬프트를 강제로 표시하려면 대화형으로 cmdlet을 실행할 때 이 값을 생략합니다.  
>   
> 선택적 **Whatif** 인수를 **Install-ADDSDomainController** cmdlet과 함께 사용하여 구성 정보를 검토합니다. 이를 통해 cmdlet 인수의 명시적 및 암시적 값을 확인할 수 있습니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSWhatIf.png)  
  
### <a name="prerequisites-check"></a>필수 구성 요소 확인  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrereqCheck.png)  
  
**필수 구성 요소 확인**은 AD DS 도메인 구성의 새로운 기능입니다. 이 새 단계에서는 도메인 및 포리스트가 새 Windows Server 2012 도메인 컨트롤러를 지원할 수 있는지 확인합니다.  
  
새 도메인 컨트롤러를 설치할 때 서버 관리자 Active Directory Domain Services 구성 마법사는 일련의 직렬화된 모듈식 테스트를 호출합니다. 이러한 테스트에서는 제안된 복구 옵션을 알려 줍니다. 필요한 만큼 여러 번 테스트를 실행할 수 있습니다. 모든 필수 구성 요소 테스트를 통과해야만 도메인 컨트롤러 프로세스를 계속 진행할 수 있습니다.  
  
**필수 구성 요소 확인**에서는 이전 운영 체제에 영향을 주는 보안 변경 내용과 같은 관련 정보도 제공합니다.  
  
특정 필수 구성 요소 확인에 대한 자세한 내용은 [필수 구성 요소 확인](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)을 참조하세요.  
  
서버 관리자를 사용할 때는 **필수 구성 요소 확인** 을 무시할 수 없지만 AD DS 배포 cmdlet을 사용할 때는 다음 인수를 사용하여 프로세스를 건너뛸 수 있습니다.  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> 필수 구성 요소 확인을 건너뛰면 도메인 컨트롤러 수준 올리기가 부분적으로 완료되거나 AD DS 포리스트가 손상될 수 있으므로 건너뛰지 않는 것이 좋습니다.  
  
**설치**를 클릭하여 도메인 컨트롤러 수준 올리기 프로세스를 시작합니다. 이때가 설치를 취소할 수 있는 마지막 기회입니다. 시작된 후에는 수준 올리기 프로세스를 취소할 수 없습니다. 수준 올리기가 끝나면 수준 올리기 결과에 상관없이 컴퓨터가 자동으로 다시 부팅됩니다. **필수 구성 요소 확인** 페이지에 프로세스 중에 발생한 문제와 이를 해결할 수 있는 지침이 표시됩니다.  
  
### <a name="installation"></a>설치  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeInstallProgress.png)  
  
**설치** 페이지가 표시되면 도메인 컨트롤러 구성이 시작되며 이는 중지하거나 취소할 수 없습니다. 세부 작업이 이 페이지에 표시되고 다음 로그에 기록됩니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
-   %systemroot%\debug\adprep\logs  
  
-   %systemroot%\debug\netsetup.log(서버가 작업 그룹에 속한 경우)  
  
ADDSDeployment 모듈을 사용하여 새 Active Directory 포리스트를 설치하려면 다음 cmdlet을 사용합니다.  
  
```  
Install-addsdomaincontroller  
```  
  
필수 및 선택적 인수는 [업그레이드 및 복제본 Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)을 참조하세요.  
  
**Install-AddsDomainController** cmdlet은 두 단계(필수 구성 요소 확인 및 설치)만 수행합니다. 아래 두 그림에는 최소 필수 인수인 **-domainname** 과 **-credential**을 사용한 설치 단계가 나와 있습니다. 기존 Windows Server 2003 포리스트에 첫 번째 Windows Server 2012 도메인 컨트롤러를 추가하는 작업의 일부로 Adprep 작업이 자동으로 수행됩니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSGetCred.png)  
  
서버 관리자와 마찬가지로 **Install-ADDSDomainController** 에서도 수준 올리기 후 서버가 자동으로 다시 부팅됨을 미리 알려 줍니다. 다시 부팅 프롬프트를 자동으로 허용하려면 임의의 ADDSDeployment Windows PowerShell cmdlet에서 **-force** 또는 **-confirm:$false** 인수를 사용합니다. 수준 올리기가 끝난 후 서버가 자동으로 다시 부팅되는 것을 방지하려면 **-norebootoncompletion** 인수를 사용합니다.  
  
> [!WARNING]  
> 다시 부팅을 무시하지 않는 것이 좋습니다. 도메인 컨트롤러가 올바르게 작동하려면 다시 부팅해야 합니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeConfirm.gif)  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeProgress.png)  
  
Windows PowerShell을 사용 하 여 도메인 컨트롤러를 원격으로 구성 하려면 **install-addsdomaincontroller** cmdlet을 **호출** 하는 cmdlet을 래핑합니다. *inside* 이 경우 중괄호를 사용해야 합니다.  
  
```  
invoke-command {install-addsdomaincontroller "domainname <domain> -credential (get-credential)} -computername <dc name>  
```  
  
예를 들면 다음과 같습니다.  
  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeExample.gif)  
  
> [!NOTE]  
> 설치 및 Adprep 프로세스 작동 방식에 대한 자세한 내용은 [도메인 컨트롤러 배포 문제 해결](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)을 참조하세요.  
  
### <a name="results"></a>결과  
![복제 데이터베이스를 설치 합니다.](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**결과** 페이지에는 수준 올리기의 성공 또는 실패와 중요한 관리 정보가 표시됩니다. 성공한 경우에는 10초 후 도메인 컨트롤러가 자동으로 다시 부팅됩니다.  
  
이전 버전의 Windows Server와 마찬가지로 Windows Server 2012를 실행하는 도메인 컨트롤러에 대한 자동화된 도메인 준비에서는 GPPREP를 실행하지 않습니다. 이전에 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 R2가 준비되지 않은 모든 도메인에 대해 **adprep.exe /gpprep** 를 수동으로 실행하세요. 업그레이드마다 실행하지 말고 도메인 기록에서 GPPrep를 한 번만 실행해야 합니다. Adprep.exe는 /gpprep를 자동으로 실행하지 않습니다. 자동으로 실행할 경우 SYSVOL 폴더의 모든 파일 및 폴더가 모든 도메인 컨트롤러에서 다시 복제될 수 있기 때문입니다.  
  

