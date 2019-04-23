---
ms.assetid: 66fa945e-598d-4f18-b603-97a39ce0d836
title: Windows Server 2012 Active Directory RODC(읽기 전용 도메인 컨트롤러) 설치(수준 200)
description: 이 항목에서는 준비된 RODC 계정을 만든 다음 RODC를 설치하는 동안 해당 계정에 서버를 연결하는 방법에 대해 설명합니다. 또한 준비된 설치를 수행하지 않고 RODC를 설치하는 방법도 알아봅니다.
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c8d34d7b35f3cd5209fd6096f69b16162229bc3a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863084"
---
# <a name="install-a-windows-server-2012-active-directory-read-only-domain-controller-rodc-level-200"></a>Windows Server 2012 Active Directory RODC(읽기 전용 도메인 컨트롤러) 설치(수준 200)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 준비된 RODC 계정을 만든 다음 RODC를 설치하는 동안 해당 계정에 서버를 연결하는 방법에 대해 설명합니다. 또한 준비된 설치를 수행하지 않고 RODC를 설치하는 방법도 알아봅니다.  
  
## <a name="stage-rodc-workflow"></a>RODC 준비 워크플로  
준비된 RODC(읽기 전용) 설치는 다음 두 가지 개별 단계로 진행됩니다.  
  
1.  비어 있는 컴퓨터 계정 준비  
  
2.  수준을 올리는 동안 이 계정에 RODC 연결  
  
다음 다이어그램에서는 Active Directory 관리 센터(Dsac.exe)를 사용하여 도메인에 비어 있는 RODC 컴퓨터 계정을 만드는 Active Directory Domain Services 읽기 전용 도메인 컨트롤러 준비 프로세스를 보여 줍니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stagedcreation.png)  
  
## <a name="BKMK_StagePS"></a>RODC 준비 Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수(**굵게** 표시된 인수는 필수 항목이며, *기울임꼴* 인수는 Windows PowerShell 또는 AD DS 구성 마법사를 사용하여 지정할 수 있음)|  
|Add-addsreadonlydomaincontrolleraccount|-SkipPreChecks<br /><br />***-DomainControllerAccountName***<br /><br />***-DomainName***<br /><br />***-SiteName***<br /><br />*-AllowPasswordReplicationAccountName*<br /><br />***-Credential***<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-DenyPasswordReplicationAccountName*<br /><br />*-NoGlobalCatalog*<br /><br />*-InstallDNS*<br /><br />-ReplicationSourceDC|  
  
> [!NOTE]  
> **-credential** 인수는 현재 Domain Admins 그룹의 구성원으로 로그온되어 있지 않은 경우에만 필요합니다.  
  
## <a name="attach-rodc-workflow"></a>RODC 연결 워크플로  
아래 다이어그램에서는 준비된 컴퓨터 계정에 연결하여 기존 도메인에 새 RODC를 만들기 위해 이미 AD DS 역할을 설치하고, RODC 계정을 준비했으며, 서버 관리자를 사용하여 **이 서버를 도메인 컨트롤러로 승격**을 시작한 Active Directory Domain Services 구성 프로세스를 보여 줍니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stageddeploy_beta1.png)  
  
## <a name="BKMK_AttachPS"></a>RODC Windows PowerShell 연결  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수(**굵게** 표시된 인수는 필수 항목이며, *기울임꼴* 인수는 Windows PowerShell 또는 AD DS 구성 마법사를 사용하여 지정할 수 있음)|  
|Install-AddsDomaincontroller|-SkipPreChecks<br /><br />***-DomainName***<br /><br />*-SafeModeAdministratorPassword*<br /><br />*-ApplicationPartitionsToReplicate*<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />-CriticalReplicationOnly<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />*-InstallationMediaPath*<br /><br />*-LogPath*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />***-UseExistingAccount***|  
  
> [!NOTE]  
> **-credential** 인수는 현재 Domain Admins 그룹의 구성원으로 로그온되어 있지 않은 경우에만 필요합니다.  
  
## <a name="staging"></a>준비  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_PreCreateRODC.png)  
  
Active Directory 관리 센터(**Dsac.exe**)를 열어 읽기 전용 도메인 컨트롤러 컴퓨터 계정의 준비 작업을 수행합니다. 탐색 창에서 도메인의 이름을 클릭합니다. 관리 목록에서 **도메인 컨트롤러**를 두 번 클릭합니다. 작업 창에서 **읽기 전용 도메인 컨트롤러 계정 미리 만들기**를 클릭합니다.  
  
Active Directory 관리 센터에 대 한 자세한 내용은 참조 하세요. [고급 AD DS 관리를 사용 하 여 Active Directory 관리 센터 &#40;200 수준&#41; ](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md) 살펴보고 [Active Directory 관리 센터: Getting Started](https://technet.microsoft.com/library/dd560651(WS.10).aspx)합니다.  
  
읽기 전용 도메인 컨트롤러를 만들어 본 경험이 있다면 설치 마법사에 Windows Server 2008의 이전 Active Directory 사용자 및 컴퓨터 스냅인을 사용할 때 표시되는 것과 동일한 그래픽 인터페이스가 있으며, 오래된 dcpromo에서 사용하는 무인 파일 형식의 구성 내보내기가 포함된 동일한 코드를 사용하는 것을 알 수 있을 것입니다.  
  
Windows Server 2012에는 RODC 컴퓨터 계정을 준비하는 새로운 ADDSDeployment cmdlet이 도입되었지만 마법사에서는 이러한 작업에 이 cmdlet을 사용하지 않습니다. 다음 섹션에서는 정보를 서로 연결하여 보다 쉽게 이해할 수 있도록 상응하는 cmdlet 및 인수를 보여 줍니다.  
  
**읽기 전용 도메인 컨트롤러 계정 미리 만들기** Active Directory 관리 센터의 작업 창에서 링크 ADDSDeployment Windows PowerShell cmdlet과 같습니다.  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
### <a name="welcome"></a>시작  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_WelcomeStage1.png)  
  
**Active Directory Domain Services 설치 마법사 시작** 대화 상자에는 **고급 모드 설치 사용**이라는 옵션이 있습니다. 이 옵션을 선택하고 **다음**을 클릭하면 암호 복제 정책 옵션이 표시됩니다. 암호 복제 정책 옵션에 기본값을 사용하려면 이 옵션의 선택을 취소합니다(이 섹션의 뒷부분에 자세히 설명되어 있음).  
  
### <a name="network-credentials"></a>네트워크 자격 증명  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Creds.png)  
  
**네트워크 자격 증명** 대화 상자의 도메인 이름 옵션에는 기본적으로 Active Directory 관리 센터의 대상 도메인이 표시됩니다. 현재 자격 증명이 기본적으로 사용됩니다. 현재 자격 증명에 Domain Admins 그룹의 구성원 자격이 포함되지 않은 경우 **대체 자격 증명**을 클릭한 다음 **설정** 을 클릭하여 Domain Admins의 구성원인 사용자 이름 및 암호를 마법사에 제공합니다.  
  
상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-credential <pscredential>  
```  
  
준비 시스템은 Windows Server 2008 R2의 직접 포트이며, 새로운 Adprep 기능을 제공하지 않습니다. 준비된 RODC 계정을 배포하려면 자동 rodcprep 작업이 실행되도록 해당 도메인에 준비되지 않은 RODC를 먼저 배포하거나, 아니면 adprep.exe /rodcprep를 수동으로 먼저 실행해야 합니다.  
  
그러지 않으면 "이 "adprep /rodcprep"가 아직 실행되지 않았으므로 이 도메인에 읽기 전용 도메인 컨트롤러를 설치할 수 없습니다." 오류가 발생합니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepNotRunError.png)  
  
### <a name="specify-the-computer-name"></a>컴퓨터 이름 지정  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1CompName.png)  
  
**컴퓨터 이름을 지정** 대화 상자에는 존재하지 않는 도메인 컨트롤러의 단일 레이블 **컴퓨터 이름**을 입력해야 합니다. 프로 모션 작업을 준비 된 계정을 감지 하지 또는 구성 하 고 나중에이 계정에 연결 하는 도메인 컨트롤러에는 이름이 같은 있어야 합니다.  
  
상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-domaincontrolleraccountname <string>  
```  
  
### <a name="select-a-site"></a>사이트 선택  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Site.png)  
  
**사이트 선택** 대화 상자에는 현재 포리스트의 Active Directory 사이트 목록이 표시됩니다. 준비된 읽기 전용 도메인 컨트롤러 작업을 수행할 때 목록에서 단일 사이트를 선택해야 합니다. RODC에서는 이 정보를 사용하여 구성 파티션에 해당 NTDS 설정 개체를 만들고, 배포 후 처음 시작할 때 올바른 사이트에 자체적으로 가입합니다.  
  
상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-sitename <string>  
```  
  
### <a name="additional-domain-controller-options"></a>추가 도메인 컨트롤러 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DCOptions.png)  
  
**추가 도메인 컨트롤러 옵션** 대화 상자에서는 도메인 컨트롤러에 **DNS 서버** 및 **글로벌 카탈로그**역할을 포함하도록 지정할 수 있습니다. 읽기 전용 도메인 컨트롤러에서 DNS 및 GC 서비스를 제공하는 것이 좋으므로 둘 다 기본적으로 설치됩니다. RODC 역할의 한 가지 의도는 광역 네트워크를 사용할 수 없으며 해당 DNS 및 글로벌 카탈로그 서비스 없이는 지점의 컴퓨터에서 AD DS 리소스 및 기능을 사용할 수 없는 지점 시나리오입니다.  
  
**RODC(읽기 전용 도메인 컨트롤러)** 옵션은 미리 선택되며 사용하지 않도록 설정할 수 없습니다. 상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-installdns <string>  
-NoGlobalCatalog <{$true | $false}>  
  
```  
  
> [!NOTE]  
> 기본적으로는 **-NoGlobalCatalog** 값은 $false 인수가 지정 되지 않은 경우 도메인 컨트롤러가 글로벌 카탈로그 서버 수를 의미 합니다.  
  
### <a name="specify-the-password-replication-policy"></a>암호 복제 정책 지정  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRP.png)  
  
**암호 복제 정책 지정** 대화 상자에서는 이 읽기 전용 도메인 컨트롤러에서 암호를 캐시할 수 있는 계정의 기본 목록을 수정할 수 있습니다. **거부**로 구성된 목록의 계정 또는 목록에 없는 계정(암시적)은 해당 암호를 캐시하지 못합니다. RODC에서 암호를 캐시할 수 없으며 쓰기 가능한 도메인 컨트롤러에 연결 및 인증할 수 없는 계정은 Active Directory에서 제공하는 리소스 또는 기능에 액세스할 수 없습니다.  
  
> [!IMPORTANT]  
> 이 대화 상자는 마법사의 시작 화면에서 **고급 모드 설치 사용** 확인란을 선택한 경우에만 표시됩니다. 이 확인란의 선택을 취소하면 마법사에서 다음 기본 그룹 및 값을 사용합니다.  
>   
> -   Administrators - Deny  
> -   Server Operators - Deny  
> -   Backup Operators - Deny  
> -   Account Operators - Deny  
> -   Denied RODC Password Replication Group - Deny  
> -   Allowed RODC Password Replication Group - Allow  
  
상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRPAllow.png)  
  
### <a name="delegation-of-rodc-installation-and-administration"></a>RODC 설치 및 관리 위임  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DelegateAdmin.png)  
  
**RODC 설치 및 관리 위임** 대화 상자에서는 RODC 컴퓨터 계정에 서버를 연결할 수 있는 사용자 또는 이러한 사용자가 포함된 그룹을 구성할 수 있습니다. **설정**을 클릭하여 사용자 또는 그룹에 대한 도메인을 찾아볼 수 있습니다. 이 대화 상자에 지정된 사용자 또는 그룹에는 RODC에 대한 로컬 관리 권한이 부여됩니다. 지정한 사용자 또는 지정된 된 그룹의 구성원 컴퓨터의 관리자 그룹과 동등한 권한으로 RODC에서 작업을 수행할 수 있습니다. Domain Admins 또는 도메인 기본 제공 Administrators 그룹의 구성원은 *아닙니다* .  
  
Domain Admins 그룹에 분기 관리자 구성원 자격을 부여하지 않고 지점 관리를 위임하려면 이 옵션을 사용합니다. RODC 관리를 위임하지 않아도 됩니다.  
  
상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
### <a name="summary"></a>요약  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Summary.png)  
  
**요약** 대화 상자에서는 설정을 확인할 수 있습니다. 마법사에서 준비된 계정을 만들기 전에 설치를 중지할 수 있는 마지막 기회입니다. 준비된 RODC 컴퓨터 계정을 만들 준비가 완료되었으면 **다음**을 클릭합니다.  **설정 내보내기** 를 클릭하여 응답 파일을 오래된 dcpromo 무인 파일 형식으로 저장합니다.  
  
### <a name="creation"></a>만들기  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1InstallProgress.png)  
  
**Active Directory Domain Services 설치 마법사**는 Active Directory에 준비된 읽기 전용 도메인 컨트롤러를 만듭니다. 이 작업을 시작한 후에는 취소할 수 없습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Complete.png)  
  
Windows PowerShell ADDSDeployment 모듈을 사용하여 읽기 전용 도메인 컨트롤러 컴퓨터 계정을 준비하려면 다음 cmdlet을 사용합니다.  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
필수 및 선택적 인수는 [RODC 준비 Windows PowerShell](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_StagePS)을 참조하세요.  
  
**Add-addsreadonlydomaincontrolleraccount** 는 두 단계(필수 구성 요소 확인 및 설치)로 구성된 하나의 작업만 수행하므로 다음 스크린샷에는 최소 필수 인수를 사용하는 설치 단계가 나와 있습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODC.png)  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODCValidating.png)  
  
RODC 준비 작업에서는 Active Directory에 RODC 컴퓨터 계정을 만듭니다. Active Directory 관리 센터에 **도메인 컨트롤러 유형**이 **비어 있는 도메인 컨트롤러 계정**으로 표시되어 있습니다. 이 도메인 컨트롤러 유형은 준비된 RODC 계정에서 서버를 읽기 전용 도메인 컨트롤러로 연결할 준비가 되었음을 나타냅니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Unoccupied.png)  
  
> [!IMPORTANT]  
> 더 이상 Active Directory 관리 센터에서 읽기 전용 도메인 컨트롤러 컴퓨터 계정에 서버를 연결할 필요가 없습니다. 서버 관리자와 Active Directory Domain Services 구성 마법사 또는 ADDSDeployment Windows PowerShell 모듈 cmdlet **Install-AddsDomainController**를 사용하여 새 RODC를 해당 준비된 계정에 연결할 수 있습니다. 이러한 단계는 RODC 컴퓨터 계정을 준비할 때 결정한 구성 옵션이 준비된 RODC 컴퓨터 계정에 포함되어 있다는 점을 제외하고는 기존 도메인에 새 쓰기 가능한 도메인 컨트롤러를 추가하는 것과 유사합니다.  
  
## <a name="attaching"></a>연결  
  
### <a name="deployment-configuration"></a>배포 구성  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
서버 관리자는 **배포 구성** 페이지에서 모든 도메인 컨트롤러 수준 올리기를 시작합니다. 선택한 배포 작업에 따라 이 페이지 및 다음 페이지에 표시되는 나머지 옵션 및 필수 필드가 바뀝니다.  
  
읽기 전용 도메인 컨트롤러를 기존 도메인에 추가하려면 클릭 **기존 도메인에 도메인 컨트롤러 추가**를 선택하고 **선택** 단추를 클릭하여 **이 작업에 대한 도메인 정보를 지정합니다**. 서버 관리자에서 올바른 자격 증명을 묻는 메시지를 자동으로 표시하거나, 아니면 **변경**을 클릭할 수 있습니다.  
  
RODC를 연결하려면 Windows Server 2012 Domain Admins 그룹의 구성원 자격이 필요합니다. 현재 자격 증명에 적절한 사용 권한이나 그룹 구성원이 없는 경우 나중에 Active Directory Domain Services 구성 마법사에 자격 증명을 제공하라는 메시지가 표시됩니다.  
  
**배포 구성** ADDSDeployment Windows PowerShell cmdlet 및 인수는 다음과 같습니다.  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2DCOptions.png)  
  
**도메인 컨트롤러 옵션** 페이지에 도메인 컨트롤러 옵션은 새로운 도메인 컨트롤러에 대 한 표시 합니다. 이 페이지가 로드되면 Active Directory Domain Services 구성 마법사에서 기존 도메인 컨트롤러로 LDAP 쿼리를 보내 비어 있는 계정을 확인합니다. 현재 컴퓨터와 동일한 이름을 공유 하는 컴퓨터 계정의 비어 있는 도메인 컨트롤러를 찾을 경우 페이지 맨 위에 있는 마법사에 정보 메시지가 표시 됩니다. "**대상 서버의 이름과 일치 하는 미리 만든된 RODC 계정이 디렉터리에 있습니다. 이 기존 RODC 계정을 사용 하거나이 도메인 컨트롤러를 다시 설치 하도록 선택할**. " 마법사에서는 **기존 RODC 계정 사용**을 기본 구성으로 사용합니다.  
  
> [!IMPORTANT]  
> 도메인 컨트롤러에 물리적인 문제가 발생하여 정상적인 작동 상태로 되돌릴 수 없는 경우 **이 도메인 컨트롤러 다시 설치** 옵션을 사용할 수 있습니다. 이 저장 도메인 컨트롤러 컴퓨터 계정에 맡기고 대체 도메인 컨트롤러를 구성 하는 경우 시간 및 Active Directory에서 메타 데이터 개체입니다. *같은 이름*으로 새 컴퓨터를 설치하고 도메인의 도메인 컨트롤러로 수준을 올립니다. **이 도메인 컨트롤러를 다시 설치** 옵션은 Active Directory (메타 데이터 정리)에서 도메인 컨트롤러 개체의 메타 데이터를 제거 하는 경우에 사용할 수 없습니다.  
  
RODC 컴퓨터 계정에 서버를 연결할 때는 도메인 컨트롤러 옵션을 구성할 수 없습니다. 도메인 컨트롤러 옵션은 준비된 RODC 컴퓨터 계정을 만들 때 구성합니다.  
  
지정한 **디렉터리 서비스 복원 모드 암호** 는 서버에 적용되는 암호 정책을 준수해야 합니다. 항상 강력하고 복잡한 암호 또는 암호 문구를 선택하십시오.  
  
**도메인 컨트롤러 옵션** ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> **-sitename**에 대한 인수로 제공된 경우 사이트 이름이 이미 존재해야 합니다. **install-AddsDomainController** cmdlet은 사이트 이름을 만들지 않습니다. **new-adreplicationsite** cmdlet을 사용하여 새 사이트를 만들 수 있습니다.  
  
**Install-ADDSDomainController** 인수는 서버 관리자와 동일한 기본값을 따릅니다(지정하지 않은 경우).  
  
**SafeModeAdministratorPassword** 인수의 작업은 특별합니다.  
  
-   인수로 *지정하지 않을 경우* cmdlet은 마스킹된 암호를 입력 및 확인하라는 메시지를 표시합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법입니다.  
  
    예를 들어 corp.contoso.com에 새 RODC를 만들고 마스킹된 암호를 입력하고 확인하라는 메시지를 표시하려면 다음 명령을 실행합니다.  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
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
  
### <a name="additional-options"></a>추가 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2AdditionalOptions.png)  
  
**추가 옵션** 페이지에서는 도메인 컨트롤러 이름을 복제 원본으로 지정하는 구성 옵션을 제공하거나 원하는 도메인 컨트롤러를 복제 원본으로 사용할 수 있습니다.  
  
또한 IFM(미디어에서 설치) 옵션을 통해 백업된 미디어를 사용하여 도메인 컨트롤러를 설치하도록 선택할 수도 있습니다. **미디어에서 설치** 확인란을 선택하면 찾아보기 옵션이 제공되며 **확인** 을 클릭하여 제공된 경로가 유효한 미디어임을 확인해야 합니다. IFM 옵션에서 사용된 미디어는 기존의 다른 Windows Server 2012 컴퓨터의 Ntdsutil.exe나 Windows Server 백업으로만 만들어야 합니다. Windows Server 2008 R2나 이전 운영 체제를 사용하여 Windows Server 2012 도메인 컨트롤러용 미디어를 만들 수 없습니다. IFM의 변경 내용에 대한 자세한 내용은 [Ntdsutil.exe 미디어에서 설치 변경 내용](../../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)을 참조하세요. SYSKEY로 보호된 미디어를 사용하는 경우 검증하는 동안 서버 관리자에는 이미지 암호를 제공하라는 메시지가 표시됩니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_StagedIFM.png)  
  
**추가 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>경로  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Paths.png)  
  
**경로** 페이지에서 AD DS 데이터베이스, 데이터베이스 트랜잭션 로그 및 SYSVOL 공유의 기본 폴더 위치를 재정의할 수 있습니다. 기본 위치는 항상 %systemroot%의 하위 디렉터리입니다. **경로** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>옵션 검토 및 스크립트 보기  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2ReviewOptions.png)  
  
**옵션 검토** 페이지에서 설치를 시작하기 전에 설정을 확인하고 이러한 설정이 요구 사항을 충족하는지도 확인할 수 있습니다. 서버 관리자를 사용하여 설치를 중지할 수 있는 마지막 기회는 아닙니다. 이 페이지에서는 단지 구성을 계속하기 전에 설정을 검토하고 확인합니다. 서버 관리자의 **옵션 검토** 페이지는 현재 ADDSDeployment 구성을 단일 Windows PowerShell 스크립트로 포함하는 유니코드 텍스트 파일을 만들 수 있도록 **스크립트 보기** 단추(선택 사항)도 제공합니다. 이 단추를 통해 서버 관리자 그래픽 인터페이스를 Windows PowerShell 배포 스튜디오로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용하여 옵션을 구성하고 구성을 내보낸 다음 마법사를 취소합니다. 이 프로세스를 통해 향후 수정을 위해 사용하거나 직접 사용하기 위한 유효하고 구문상으로 정확한 샘플이 만들어집니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainName "corp.contoso.com" `  
-LogPath "C:\Windows\NTDS" `  
-SYSVOLPath "C:\Windows\SYSVOL" `  
-UseExistingAccount:$true `  
-Norebootoncompletion:$false  
-Force:$true  
  
```  
  
> [!NOTE]  
> 서버 관리자는 수준을 올릴 때 일반적으로 모든 인수의 값을 채우며 기본값에 의존하지 않습니다. 기본값은 향후 버전의 Windows 또는 서비스 팩 간에 변경될 수 있기 때문입니다. 단, **-safemodeadministratorpassword** 인수는 예외입니다. 확인 프롬프트를 강제로 표시하려면 대화형으로 cmdlet을 실행할 때 이 값을 생략합니다.  
  
선택적 **Whatif** 인수를 **Install-ADDSDomainController** cmdlet과 함께 사용하여 구성 정보를 검토합니다. 이를 통해 cmdlet 인수의 명시적 및 암시적 값을 확인할 수 있습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2WhatIf.png)  
  
### <a name="prerequisites-check"></a>필수 구성 요소 확인  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2PrereqCheck.png)  
  
**필수 구성 요소 확인**은 AD DS 도메인 구성의 새로운 기능입니다. 이 새 단계에서는 서버 구성이 새 AD DS 포리스트를 지원할 수 있는지 확인합니다.  
  
새 포리스트 루트 도메인을 설치할 때 서버 관리자 Active Directory 도메인 서비스 구성 마법사는 일련의 직렬화된 모듈식 테스트를 호출합니다. 이러한 테스트에서는 제안된 복구 옵션을 알려 줍니다. 필요한 만큼 여러 번 테스트를 실행할 수 있습니다. 모든 필수 구성 요소 테스트가 통과할 때까지 도메인 컨트롤러 설치 프로세스를 계속할 수 없습니다.  
  
**필수 구성 요소 확인**에서는 이전 운영 체제에 영향을 주는 보안 변경 내용과 같은 관련 정보도 제공합니다. 필수 구성 요소 검사에 대 한 자세한 내용은 참조 [필수 구성 요소 확인](../../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)합니다.  
  
서버 관리자를 사용할 때는 **필수 구성 요소 확인** 을 무시할 수 없지만 AD DS 배포 cmdlet을 사용할 때는 다음 인수를 사용하여 프로세스를 건너뛸 수 있습니다.  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> 필수 구성 요소 확인을 건너뛰면 도메인 컨트롤러 수준 올리기가 부분적으로 완료되거나 AD DS 포리스트가 손상될 수 있으므로 건너뛰지 않는 것이 좋습니다.  
  
**설치**를 클릭하여 도메인 컨트롤러 수준 올리기 프로세스를 시작합니다. 이때가 설치를 취소할 수 있는 마지막 기회입니다. 시작된 후에는 수준 올리기 프로세스를 취소할 수 없습니다. 수준 올리기가 끝나면 수준 올리기 결과에 상관없이 컴퓨터가 자동으로 다시 부팅됩니다.  
  
### <a name="installation"></a>설치  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Installation.png)  
  
설치 페이지가 표시되면 도메인 컨트롤러 구성이 시작되며 이는 중지하거나 취소할 수 없습니다. 세부 작업이 이 페이지에 표시되고 다음 로그에 기록됩니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment 모듈을 사용하여 새 Active Directory 포리스트를 설치하려면 다음 cmdlet을 사용합니다.  
  
```  
Install-addsdomaincontroller  
  
```  
  
필수 및 선택적 인수는 [RODC 연결 Windows PowerShell](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_AttachPS)을 참조하세요.  
  
**Install-addsdomaincontroller** cmdlet은 두 단계(필수 구성 요소 확인 및 설치)만 수행합니다. 아래 두 그림에는 최소 필수 인수인 **-domainname**, **-useexistingaccount**및 **-credential**을 사용한 설치 단계가 나와 있습니다. 서버 관리자와 마찬가지로 **Install-ADDSDomainController** 에서도 수준 올리기 후 서버가 자동으로 다시 부팅됨을 미리 알려 줍니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2.png)  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2Complete.png)  
  
다시 부팅 프롬프트를 자동으로 허용하려면 임의의 ADDSDeployment Windows PowerShell cmdlet에서 **-force** 또는 **-confirm:$false** 인수를 사용합니다. 수준 올리기가 끝난 후 서버가 자동으로 다시 부팅되는 것을 방지하려면 **-norebootoncompletion** 인수를 사용합니다.  
  
> [!WARNING]  
> 다시 부팅을 무시하지 않는 것이 좋습니다. 도메인 컨트롤러가 올바르게 작동하려면 다시 부팅해야 합니다.  
  
### <a name="results"></a>결과  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**결과** 페이지에는 수준 올리기의 성공 또는 실패와 중요한 관리 정보가 표시됩니다. 10초 후 도메인 컨트롤러가 자동으로 다시 부팅됩니다.  
  
## <a name="rodc-without-staging-workflow"></a>준비 없는 RODC 워크플로  
다음 다이어그램에서는 이전에 AD DS 역할을 설치하고 서버 관리자를 사용하여 기존 Windows Server 2012 도메인에서 준비되지 않은 새 읽기 전용 도메인 컨트롤러를 만드는 Active Directory 도메인 서비스 구성 마법사를 시작한 경우의 Active Directory 도메인 서비스 구성 프로세스를 보여 줍니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_rodcdeploy.png)  
  
## <a name="rodc-without-staging-windows-powershell"></a>준비 없는 RODC Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수(**굵게** 표시된 인수는 필수 항목이며, *기울임꼴* 인수는 Windows PowerShell 또는 AD DS 구성 마법사를 사용하여 지정할 수 있음)|  
|Install-AddsDomainController|-SkipPreChecks<br /><br />***-DomainName***<br /><br />*-SafeModeAdministratorPassword*<br /><br />***-SiteName***<br /><br />*-ApplicationPartitionsToReplicate*<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />*-CriticalReplicationOnly*<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />-DNSOnNetwork<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />*-NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-AllowPasswordReplicationAccountName*<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-DenyPasswordReplicationAccountName*<br /><br />***-ReadOnlyReplica***|  
  
> [!NOTE]  
> **-credential** 인수는 현재 Domain Admins 그룹의 구성원으로 로그온되어 있지 않은 경우에만 필요합니다.  
  
## <a name="rodc-without-staging-deployment"></a>준비 없는 RODC 배포  
  
### <a name="deployment-configuration"></a>배포 구성  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
서버 관리자는 **배포 구성** 페이지에서 모든 도메인 컨트롤러 수준 올리기를 시작합니다. 선택한 배포 작업에 따라 이 페이지 및 다음 페이지에 표시되는 나머지 옵션 및 필수 필드가 바뀝니다.  
  
준비되지 않은 읽기 전용 도메인 컨트롤러를 기존 Windows Server 2012 도메인에 추가하려면 클릭 **기존 도메인에 도메인 컨트롤러 추가**를 선택하고 **선택** 단추를 클릭하여 **이 작업에 대한 도메인 정보를 지정합니다**. 서버 관리자에서 올바른 자격 증명을 묻는 메시지를 자동으로 표시하거나, 아니면 **변경**을 클릭할 수 있습니다.  
  
RODC를 연결하려면 Windows Server 2012 Domain Admins 그룹의 구성원 자격이 필요합니다. 현재 자격 증명에 적절한 사용 권한이나 그룹 구성원이 없는 경우 나중에 Active Directory Domain Services 구성 마법사에 자격 증명을 제공하라는 메시지가 표시됩니다.  
  
**배포 구성** ADDSDeployment Windows PowerShell cmdlet 및 인수는 다음과 같습니다.  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDCOptions.png)  
  
**도메인 컨트롤러 옵션** 페이지에서는 새 도메인 컨트롤러에 대한 도메인 컨트롤러 기능을 지정합니다. 구성 가능한 도메인 컨트롤러 기능에는 **DNS 서버**, **글로벌 카탈로그** 및 **읽기 전용 도메인 컨트롤러**가 포함됩니다. 분산된 환경에서의 고가용성을 위해 모든 도메인 컨트롤러에서 DNS 및 GC 서비스를 제공하는 것이 좋습니다. GC는 항상 기본적으로 선택되며, DNS 서버는 현재 도메인에서 권한 시작 쿼리를 기반으로 해당 DC에 이미 있는 DNS를 호스트하는 경우 기본적으로 선택됩니다.  
  
**도메인 컨트롤러 옵션** 페이지에서는 포리스트 구성에서 적절한 Active Directory 논리 **사이트 이름** 을 선택할 수도 있습니다. 기본적으로 가장 정확한 서브넷을 포함한 사이트가 선택됩니다. 사이트가 1개 있는 경우 자동으로 그 사이트가 선택됩니다.  
  
> [!IMPORTANT]  
> 서버가 어떠한 Active Directory 서브넷에도 속해 있지 않고 둘 이상의 Active Directory 사이트가 있는 경우에는 아무 항목도 선택되지 않습니다. 이 경우 목록에서 사이트를 선택해야 **다음** 단추를 사용할 수 있습니다.  
  
지정한 **디렉터리 서비스 복원 모드 암호** 는 서버에 적용되는 암호 정책을 준수해야 합니다. 항상 강력하고 복잡한 암호를 선택해야 하며 가급적 암호 문구를 선택하는 것이 좋습니다. **도메인 컨트롤러 옵션** ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> **-sitename**에 대한 인수로 제공된 경우 사이트 이름이 이미 존재해야 합니다. **install-AddsDomainController** cmdlet은 사이트 이름을 만들지 않습니다. **new-adreplicationsite** cmdlet을 사용하여 새 사이트를 만들 수 있습니다.  
  
**Install-ADDSDomainController** 인수는 서버 관리자와 동일한 기본값을 따릅니다(지정하지 않은 경우).  
  
**SafeModeAdministratorPassword** 인수의 작업은 특별합니다.  
  
-   인수로 *지정하지 않을 경우* cmdlet은 마스킹된 암호를 입력 및 확인하라는 메시지를 표시합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법입니다.  
  
    예를 들어 corp.contoso.com에 새 RODC를 만들고 마스킹된 암호를 입력하고 확인하라는 메시지를 표시하려면 다음 명령을 실행합니다.  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
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
  
### <a name="rodc-options"></a>RODC 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCOptions.png)  
  
**RODC 옵션** 페이지에서는 다음 설정을 수정할 수 있습니다.  
  
-   위임된 관리자 계정  
  
-   암호를 RODC에 복제할 수 있는 계정  
  
-   암호를 RODC에 복제할 수 없는 계정  
  
위임된 관리자 계정은 RODC에 대한 로컬 관리 권한을 가집니다. 이러한 사용자는 로컬 컴퓨터의 관리자 그룹에 해당 하는 권한으로 작동할 수 있습니다.  Domain Admins 또는 도메인 기본 제공관리자그룹의 구성원은 아닙니다 이 옵션은 도메인 관리 권한을 정지하지 않고도 지점 관리를 위임하는 데 유용합니다. 관리 위임을 별도로 구성하지 않아도 됩니다.  
  
상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
RODC에서 암호를 캐시할 수 없으며 쓰기 가능한 도메인 컨트롤러에 연결 및 인증할 수 없는 계정은 Active Directory에서 제공하는 리소스 또는 기능에 액세스할 수 없습니다.  
  
> [!IMPORTANT]  
> 수정하지 않을 경우 기본 그룹 및 설정이 사용됩니다.  
>   
> -   Administrators - Deny  
> -   Server Operators - Deny  
> -   Backup Operators - Deny  
> -   Account Operators - Deny  
> -   Denied RODC Password Replication Group - Deny  
> -   Allowed RODC Password Replication Group - Allow  
  
상응하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_SelectDelAdmin.png)  
  
### <a name="additional-options"></a>추가 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCAdditionalOptions.png)  
  
**추가 옵션** 페이지에서는 도메인 컨트롤러 이름을 복제 원본으로 지정하는 구성 옵션을 제공하거나 원하는 도메인 컨트롤러를 복제 원본으로 사용할 수 있습니다.  
  
또한 IFM(미디어에서 설치) 옵션을 통해 백업된 미디어를 사용하여 도메인 컨트롤러를 설치하도록 선택할 수도 있습니다. **미디어에서 설치** 확인란을 선택하면 찾아보기 옵션이 제공되며 **확인** 을 클릭하여 제공된 경로가 유효한 미디어임을 확인해야 합니다. IFM 옵션에서 사용된 미디어는 기존의 다른 Windows Server 2012 컴퓨터의 Ntdsutil.exe나 Windows Server 백업으로만 만들어야 합니다. Windows Server 2008 R2나 이전 운영 체제를 사용하여 Windows Server 2012 도메인 컨트롤러용 미디어를 만들 수 없습니다.  부록에서는 IFM의 변경 내용에 자세한 정보를 제공합니다. SYSKEY로 보호된 미디어를 사용하는 경우 검증하는 동안 서버 관리자에는 이미지 암호를 제공하라는 메시지가 표시됩니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSIFM.png)  
  
추가 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>경로  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPaths.png)  
  
**경로** 페이지에서 AD DS 데이터베이스, 데이터베이스 트랜잭션 로그 및 SYSVOL 공유의 기본 폴더 위치를 재정의할 수 있습니다. 기본 위치는 항상 %systemroot%의 하위 디렉터리입니다. **경로** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>준비 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepOptions.png)  
  
**준비 옵션** 페이지에서는 AD DS 구성에 스키마 확장(forestprep) 및 도메인 업데이트(domainprep)가 포함되어 있음을 알려 줍니다. 이 페이지는 이전 Windows Server 2012 도메인 컨트롤러 설치 또는 Adprep.exe 수동 실행에서 포리스트 또는 도메인이 준비되지 않은 경우에만 표시됩니다. 예를 들어 기존 Windows Server 2012 포리스트 루트 도메인에 새 복제본 도메인 컨트롤러를 추가하는 경우에는 Active Directory 도메인 서비스 구성 마법사에서 이 페이지를 표시하지 않습니다.  
  
**다음**을 클릭하면 스키마 확장 및 도메인 업데이트가 실행되지 않습니다. 이러한 이벤트는 설치 단계 중에만 발생합니다. 이 페이지는 설치 후반에서 발생할 이벤트를 알려 주는 역할만 합니다.  
  
또한 스키마를 확장하거나 도메인을 준비하려면 Schema Admin 및 Enterprise Admins 그룹의 구성원 자격이 필요하므로 이 페이지에서는 현재 사용자 자격 증명이 이러한 그룹의 구성원인지 확인합니다. 이 페이지에 현재 자격 증명의 권한이 부족하다는 메시지가 표시되면 **변경**을 클릭하여 적절한 사용자 자격 증명을 제공합니다.  
  
추가 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> 이전 버전의 Windows Server와 마찬가지로 Windows Server 2012의 자동화된 도메인 준비에서는 GPPREP를 실행하지 않습니다. 이전에 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 R2가 준비되지 않은 모든 도메인에 대해 **adprep.exe /gpprep** 를 수동으로 실행하세요. 업그레이드마다 실행하지 말고 도메인 기록에서 GPPrep를 한 번만 실행해야 합니다. Adprep.exe는 /gpprep를 자동으로 실행하지 않습니다. 자동으로 실행할 경우 SYSVOL 폴더의 모든 파일 및 폴더가 모든 도메인 컨트롤러에서 다시 복제될 수 있기 때문입니다.  
>   
> 자동 RODCPrep는 도메인에서 준비되지 않은 첫 번째 RODC의 수준을 올릴 때 실행됩니다. 쓰기 가능한 첫 번째 Windows Server 2012 도메인 컨트롤러의 수준을 올릴 때는 실행되지 않습니다. 또한 읽기 전용 도메인 컨트롤러를 배포하려는 경우에도 **adprep.exe /rodcprep** 를 수동으로 실행할 수 있습니다.  
  
### <a name="review-options-and-view-script"></a>옵션 검토 및 스크립트 보기  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCReviewOptions.png)  
  
**옵션 검토** 페이지에서 설치를 시작하기 전에 설정을 확인하고 이러한 설정이 요구 사항을 충족하는지도 확인할 수 있습니다. 서버 관리자를 사용하여 설치를 중지할 수 있는 마지막 기회는 아닙니다. 이 페이지에서는 단지 구성을 계속하기 전에 설정을 검토하고 확인합니다.  
  
서버 관리자의 **옵션 검토** 페이지는 현재 ADDSDeployment 구성을 단일 Windows PowerShell 스크립트로 포함하는 유니코드 텍스트 파일을 만들 수 있도록 **스크립트 보기** 단추(선택 사항)도 제공합니다. 이 단추를 통해 서버 관리자 그래픽 인터페이스를 Windows PowerShell 배포 스튜디오로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용하여 옵션을 구성하고 구성을 내보낸 다음 마법사를 취소합니다. 이 프로세스를 통해 향후 수정을 위해 사용하거나 직접 사용하기 위한 유효하고 구문상으로 정확한 샘플이 만들어집니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-AllowPasswordReplicationAccountName @("CORP\Allowed RODC Password Replication Group", "CORP\Chicago RODC Admins", "CORP\Chicago RODC Users and Computers") `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DelegatedAdministratorAccountName "CORP\Chicago RODC Admins" `  
-DenyPasswordReplicationAccountName @("BUILTIN\Administrators", "BUILTIN\Server Operators", "BUILTIN\Backup Operators", "BUILTIN\Account Operators", "CORP\Denied RODC Password Replication Group") `  
-DomainName "corp.contoso.com" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-ReadOnlyReplica:$true `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> 서버 관리자는 수준을 올릴 때 일반적으로 모든 인수의 값을 채우며 기본값에 의존하지 않습니다. 기본값은 향후 버전의 Windows 또는 서비스 팩 간에 변경될 수 있기 때문입니다. 단, **-safemodeadministratorpassword** 인수는 예외입니다. 확인 프롬프트를 강제로 표시하려면 대화형으로 cmdlet을 실행할 때 이 값을 생략합니다.  
  
선택적 Whatif 인수를 Install-ADDSDomainController cmdlet과 함께 사용하여 구성 정보를 검토합니다. 이를 통해 cmdlet 인수의 명시적 및 암시적 값을 확인할 수 있습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCWhatIf.png)  
  
### <a name="prerequisites-check"></a>필수 구성 요소 확인  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrereqCheck.png)  
  
**필수 구성 요소 확인**은 AD DS 도메인 구성의 새로운 기능입니다. 이 새 단계에서는 서버 구성이 새 AD DS 포리스트를 지원할 수 있는지 확인합니다.  
  
새 포리스트 루트 도메인을 설치할 때 서버 관리자 Active Directory 도메인 서비스 구성 마법사는 일련의 직렬화된 모듈식 테스트를 호출합니다. 이러한 테스트에서는 제안된 복구 옵션을 알려 줍니다. 필요한 만큼 여러 번 테스트를 실행할 수 있습니다. 모든 필수 구성 요소 테스트를 통과해야만 도메인 컨트롤러 프로세스를 계속 진행할 수 있습니다.  
  
**필수 구성 요소 확인**에서는 이전 운영 체제에 영향을 주는 보안 변경 내용과 같은 관련 정보도 제공합니다.  
  
서버 관리자를 사용할 때는 **필수 구성 요소 확인** 을 무시할 수 없지만 AD DS 배포 cmdlet을 사용할 때는 다음 인수를 사용하여 프로세스를 건너뛸 수 있습니다.  
  
```  
-skipprechecks  
  
```  
  
**설치**를 클릭하여 도메인 컨트롤러 수준 올리기 프로세스를 시작합니다. 이때가 설치를 취소할 수 있는 마지막 기회입니다. 시작된 후에는 수준 올리기 프로세스를 취소할 수 없습니다. 수준 올리기가 끝나면 수준 올리기 결과에 상관없이 컴퓨터가 자동으로 다시 부팅됩니다.  
  
### <a name="installation"></a>설치  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCInstallation.png)  
  
**설치** 페이지가 표시되면 도메인 컨트롤러 구성이 시작되며 이는 중지하거나 취소할 수 없습니다. 세부 작업이 이 페이지에 표시되고 다음 로그에 기록됩니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment 모듈을 사용하여 새 Active Directory 포리스트를 설치하려면 다음 cmdlet을 사용합니다.  
  
```  
Install-addsdomaincontroller  
  
```  
  
필수 및 선택적 인수는 이 섹션의 첫 부분에 있는 **ADDSDeployment Cmdlet** 표를 참조하세요.  
  
**Install-addsdomaincontroller** cmdlet은 두 단계(필수 구성 요소 확인 및 설치)만 수행합니다. 아래 두 그림에는 최소 필수 인수인 **-domainname**, **-readonlyreplica**, **-sitename** 및 **-credential**을 사용한 설치 단계가 나와 있습니다. 서버 관리자와 마찬가지로 **Install-ADDSDomainController** 에서도 수준 올리기 후 서버가 자동으로 다시 부팅됨을 미리 알려 줍니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODC.png)  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODCProgress.png)  
  
다시 부팅 프롬프트를 자동으로 허용하려면 임의의 ADDSDeployment Windows PowerShell cmdlet에서 **-force** 또는 **-confirm:$false** 인수를 사용합니다. 수준 올리기가 끝난 후 서버가 자동으로 다시 부팅되는 것을 방지하려면 **-norebootoncompletion** 인수를 사용합니다.  
  
> [!WARNING]  
> 다시 부팅을 무시하지 않는 것이 좋습니다. 도메인 컨트롤러가 올바르게 작동하려면 다시 부팅해야 합니다. 도메인 컨트롤러에서 로그오프한 경우 다시 시작할 때까지 대화형으로 다시 로그온할 수 없습니다.  
  
### <a name="results"></a>결과  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCSignoff.png)  
  
**결과** 페이지에는 수준 올리기의 성공 또는 실패와 중요한 관리 정보가 표시됩니다. 10초 후 도메인 컨트롤러가 자동으로 다시 부팅됩니다.  
  

