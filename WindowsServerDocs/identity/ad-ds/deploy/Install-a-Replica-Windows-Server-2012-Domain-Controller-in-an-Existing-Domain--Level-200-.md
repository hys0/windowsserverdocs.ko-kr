---
ms.assetid: e6da5984-d99d-4c34-9c11-4a18cd413f06
title: "기존 도메인 (200 수준)의 복제 Windows Server 2012 도메인 컨트롤러 설치"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e3151a8beee2870ecc747a64241df9d562ad4cc2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-replica-windows-server-2012-domain-controller-in-an-existing-domain-level-200"></a>기존 도메인 (200 수준)의 복제 Windows Server 2012 도메인 컨트롤러 설치

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 기존 숲 또는 도메인 Windows Server 2012를 사용 하 여 서버 관리자 또는 Windows PowerShell로 업그레이드 하는 데 필요한 단계에 설명 합니다. 기존 도메인 Windows Server 2012를 실행 하는 도메인 컨트롤러를 추가 하는 방법을 설명 합니다.  
  
-   [복제본 워크플로 및 업그레이드](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [복제 Windows PowerShell 및 업그레이드](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)  
  
-   [배포](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Dep)  
  
## <a name="BKMK_Workflow"></a>복제본 워크플로 및 업그레이드  
다음 그림 AD DS 역할을 이전에 설치 되어 있고 Active Directory 도메인 서비스 구성 마법사 서버 관리자를 사용 하 여 기존 도메인에 새 도메인 컨트롤러를 만들기 시작 때 Active Directory 도메인 서비스 구성 프로세스를 보여 줍니다.  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/adds_forestupgrade.png)  
  
## <a name="BKMK_PS"></a>복제 Windows PowerShell 및 업그레이드  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수 (**굵게** 인수가 필요 합니다. *기울임꼴로 표시* 인수 Windows PowerShell 또는 광고 DS 구성 마법사를 사용 하 여 지정할 수 있습니다.)|  
|설치 AddsDomainController|-SkipPreChecks<br /><br />***-도메인 이름***<br /><br />*-SafeModeAdministratorPassword*<br /><br />*-SiteName*<br /><br />*-ADPrepCredential*<br /><br />-ApplicationPartitionsToReplicate<br /><br />*-AllowDomainControllerReinstall*<br /><br />-확인<br /><br />*-CreateDNSDelegation*<br /><br />***자격 증명***<br /><br />-CriticalReplicationOnly<br /><br />*-데이터베이스 경로*<br /><br />*-DNSDelegationCredential*<br /><br />힘<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />-NoDnsOnNetwork<br /><br />*-NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />-SiteName<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-UseExistingAccount*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-자격 증명** 인수는만 경우 하지 이미 로그온 (업그레이드 하는 경우 숲)는 엔터프라이즈 관리자 및 스키마 관리자 그룹 또는 도메인 관리자 그룹의 회원으로 (에 추가 하는 새 DC 기존 도메인) 하는 경우 필요 합니다.  
  
## <a name="BKMK_Dep"></a>배포  
  
### <a name="deployment-configuration"></a>배포 구성  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDeployConfig.png)  
  
서버 관리자 모든 도메인 컨트롤러 프로 모션으로 시작 되 고 **배포 구성** 페이지 합니다. 나머지 옵션과 필수 필드가 페이지에서 다음 페이지를 선택 하는 배포 작업에 따라 변경 됩니다.  
  
기존 숲 업그레이드 하거나 기존 도메인에 쓸 수 있는 도메인 컨트롤러 추가 클릭 **도메인 컨트롤러 기존 도메인에 추가** 클릭 **선택** 에 **도메인이이 도메인에 대 한 정보를 지정**합니다. 서버 관리자 묻는 유효한 자격 증명 필요 합니다.  
  
숲 업그레이드 자격 증명 그룹 구성원 엔터프라이즈 관리자와 스키마 관리자 그룹 Windows Server 2012에 포함 된 필요 합니다. Active Directory 도메인 서비스 구성 묻는 메시지가 나중에 적절 한 권한이 또는 그룹 구성원 현재 자격 증명 되어 있지 않습니다.  
  
자동 Adprep 과정이 기존 Windows Server 2012 도메인 도메인 컨트롤러에서 이전 버전의 Windows Server 실행 하는 도메인을 추가 하는 도메인 컨트롤러 차이 작동 합니다.  
  
배포 구성 ADDSDeployment cmdlet 및 인수는 다음과 같습니다.  
  
```  
Install-AddsDomainController  
-domainname <string>  
-credential <pscredential>  
```  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeSelectDomain.png)  
  
나중에으로 이산 필수 검사 반복 중 일부는 각 페이지에서 특정 테스트를 수행 합니다. 예를 들어는 선택한 도메인 최소 기능 수준을 충족 하지 않는 경우 필요가 없습니다 알아보려면 필수 확인으로 통해 프로 모션:  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeFFLError.png)  
  
### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptions.png)  
  
**도메인 컨트롤러 옵션** 페이지 새 도메인 컨트롤러에 대 한 도메인 컨트롤러 기능을 지정 합니다. 가능한 도메인 컨트롤러 기능은 **DNS 서버**, **드**, 및 **읽기 전용 도메인 컨트롤러**합니다. 모든 도메인 컨트롤러 분산된 환경에서 사용 가능 하도록 DNS 및 GC 서비스를 제공 하는 것이 좋습니다. 기본적으로 GC은 항상 선택 하 고 현재 도메인 호스트 권한 시작 쿼리 기반 DNS 해당 Dc에 이미 있는 경우 DNS 서버 기본적으로 선택 됩니다. **도메인 컨트롤러 옵션** 페이지도 논리 적절 한 Active Directory를 선택할 수 있습니다 **사이트 이름** 숲 구성에서 합니다. 기본적으로 가장 적은 서브넷 사이트에서는 선택 합니다. 사이트가 하나뿐인 경우 자동으로 선택 합니다.  
  
> [!NOTE]  
> 서버 Active Directory 서브넷에 속하지 않는 경우 둘 이상의 Active Directory 사이트가 아무 것도 선택 및 **다음** 단추는 목록에서 사이트를 선택할 때까지 사용할 수 없습니다.  
  
지정 된 **디렉터리 서비스 복원 모드 암호** 서버에 적용 암호 정책을 준수 해야 합니다. 항상 복잡 하 고 강력한 암호 또는 암호를 선택 합니다.  
  
**도메인 컨트롤러 옵션** ADDSDeployment 인수는 다음과 같습니다.  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-sitename <string>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> 인수로 제공 된 경우에 이미 사이트 이름이 있어야 **-sitename**합니다. **설치-AddsDomainController** cmdlet 사이트를 생성 하지 않습니다. Cmdlet 사용할 수 **새로운 adreplicationsite** 새 사이트를 만들 수 있습니다.  
  
**SafeModeAdministratorPassword** 특별 한 인수의 작업은 다음과 같습니다.  
  
-   하는 경우 *지정 하지* 를 인수로 cmdlet 묻는 메시지를 입력 하 고 마스크 암호를 확인 합니다. 기본 설정된 사용 cmdlet 대화식으로 실행 될 때입니다.  
  
    예를 들어, 추가 도메인 컨트롤러에서를 treyresearch.net 도메인 만들고 수 하 라는 메시지가 표시 입력 하 고 마스크 비밀 번호를 확인 합니다.  
  
    ```  
    Install-ADDSDomainController "DomainName treyresearch.net "credential (get-credential)  
    ```  
  
-   지정 된 경우 *값*, 값 보안 문자열 여야 합니다. Cmdlet 대화식으로 실행 될 때 기본 설정된 사용 아닙니다.  
  
예를 들어, 요청할 수 있습니다 수동으로 암호를 사용 하 여는 **읽기 호스트** cmdlet에 대 한 보안 문자열 묻는:  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> 이전 옵션 암호를 확인 하지 않는 주의 사용 하 여: 암호가 표시 되지 않습니다.  
  
또한이 것이 좋음 있지만 변환 일반 텍스트 변수와 보안 문자열을 제공할 수 있습니다.  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
  
```  
  
마지막으로 애매 암호에 파일을 저장 하 고 나타나지 암호화 되지 않은 텍스트 암호 없이 나중에 다시 수 있습니다. 예를 들어:  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> 지우기 또는 애매 텍스트 암호를 저장 또는 제공 권장 하지 않습니다. 스크립트가이 명령을 실행 또는이 기사를 통해 모든 사용자 해당 도메인 컨트롤러의 DSRM 암호를 알고 있습니다.  애매 암호를 취소할 수 파일에 액세스할 수 있는 모든 사람이. 해당 정보를 DSRM 시작 DC에 로그온 하 고 자녀의 권한 Active Directory 숲에서 가장 높은 수준의에 상승 도메인 컨트롤러 자체, 가장 결국 수 있습니다. 추가 단계를 사용 하 여 집합 **System.Security.Cryptography** 데이터는 것이 좋습니다 하지만 아니었습니다 텍스트 파일을 암호화 됩니다. 완전히 암호 저장을 방지 하는 것이 좋습니다.  
  
ADDSDeployment cmdlet 자동으로 DNS 클라이언트 설정, 전달자 및 루트 힌트 구성을 건너뛰게 하는 추가 옵션을 제공 합니다. 서버 관리자를 사용 하는 경우이 구성 옵션을 건너뛸 수 없습니다. 이 인수 도메인 컨트롤러 구성 전에 DNS 서버 역할을 설치한 경우에 중요 합니다.  
  
```  
-SkipAutoConfigureDNS  
```  
  
**도메인 컨트롤러 옵션** 페이지 경고 기존 도메인 컨트롤러 Windows Server 2003을 실행 하는 경우에 읽기 도메인 컨트롤러를 만들 수는 없습니다. 이 정상적인 동작 한 경고를 해제할 수 있습니다.  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptionsError.png)  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS 옵션과 DNS 위임 자격 증명  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDNSOptions.png)  
  
**DNS 옵션** 페이지 선택한 경우 DNS 위임 구성할 수 있습니다의 **DNS 서버** 옵션에 *도메인 컨트롤러 옵션* 페이지 DNS 위임 수 있는 영역을 향하게 하는 경우 합니다. 구성원을 사용자의 암호 확인용 자격 증명을 제공 해야 할 수 있는 **DNS 관리자** 그룹 합니다.  
  
**DNS 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
For more information about whether you need to create a DNS delegation, see [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx).  
  
### <a name="additional-options"></a>추가 옵션  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeAdditionalOptions.png)  
  
**추가 옵션** 페이지 복제 원본으로 도메인 컨트롤러의 이름을 지정 구성 옵션을 제공 하거나 도메인 컨트롤러 복제 원본으로 사용할 수 있습니다.  
  
있습니다 하도록 선택할 수도 있는 도메인 컨트롤러를 사용 하 여 설치 미디어 (IFM) 옵션에서 설치를 사용 하 여 미디어를 백업 합니다. **설치 미디어에서** 확인란을 한 번 찾아보기 옵션을 선택 하 고 클릭 해야 제공 **확인** 제공된 경로 사용할 미디어 확인 하기 위해 합니다. IFM 옵션으로 사용 되는 미디어는 Windows Server 백업 또는 Ntdsutil.exe 컴퓨터에서 만든 다른 기존 Windows Server 2012만 사용 합니다. Windows Server 2012 도메인 컨트롤러에 대해 미디어를 만드는 Windows Server 2008 R2 또는 이전 운영 체제를 사용할 수 없습니다. 변경 IFM에 대 한 자세한 내용은 참조 [관리 부록 간체](../../ad-ds/deploy/Simplified-Administration-Appendix.md)합니다. 한 SYSKEY로 보호 된 미디어를 사용 하 여 확인 하는 동안 서버 관리자 이미지의 암호를 묻습니다.  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_NtdsutilIFM.png)  
  
**추가 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-syskey <secure string>  
```  
  
### <a name="paths"></a>경로  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
**경로** SYSVOL 공유 및 페이지 데이터베이스 트랜잭션 로그가 광고 DS 데이터베이스의 기본 폴더 위치를 무시할 수 있습니다. 기본 위치는 항상 하위 시스템 루트 %의입니다.  
  
Active Directory 경로 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>준비 옵션  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptions.png)  
  
**준비 옵션** 페이지에 표시 광고 DS 구성 스키마 (forestprep)를 확장 하 고 업데이트 하는 도메인 (도메인 준비)에 포함 됩니다.  만 수동으로 Adprep.exe 실행 하거나 이전 Windows Server 2012 도메인 컨트롤러 설치 여 숲 및 도메인 준비 되지 있는 경우이 페이지를 표시 합니다. 예를 들어, Active Directory 도메인 서비스 구성 마법사 표시 기존 Windows Server 2012 숲 루트 도메인에 새 도메인 컨트롤러를 추가한 경우이 페이지를 않습니다.  
  
스키마를 확장 하 고 업데이트 하는 도메인 클릭할 때 발생 하지 않으면 **다음**합니다. 이러한 이벤트 설치 단계 에서만 발생합니다. 이 페이지는 설치 나중에 발생 하는 행사에 대해 인식 간단 하 게 제공 됩니다.  
  
이 페이지도의 유효성을 검사 현재 사용자 자격 증명 스키마 관리자 및 Enterprise 관리자 그룹의 회원 있는 스키마 확장 하거나 도메인 준비 이러한 그룹의 회원 필요 합니다. 클릭 **변경** 페이지 알려 현재 자격 증명 충분 한 사용 권한을 제공 하지 않는 경우 사용자 자격 증명을 합니다.  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptionsCreds.png)  
  
추가 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> 서 이전 버전의 Windows Server, Windows Server 2012를 실행 하는 도메인 컨트롤러에 대 한 준비 자동화 된 도메인 실행 되지 않습니다 GPPREP. 실행 **adprep.exe /gpprep** 이전에 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 r 2에 대 한 준비 되지 된 모든 도메인에 대 한 수동으로 합니다. 모든 업그레이드를 하지는 도메인의 기록에 한 번만 GPPrep 실행 해야 합니다. 해당 작업 모든 도메인 컨트롤러에 다시 복제할 SYSVOL 폴더의 모든 파일 및 폴더를 시킬 수 있으므로 Adprep.exe /gpprep 자동으로 실행 되지 않습니다.  
>   
> 도메인의 첫 번째 없다고 준비 RODC 홍보 RODCPrep 자동 실행 됩니다. 첫 번째 쓰기 Windows Server 2012 도메인 컨트롤러 홍보 때 발생 하지 않습니다. 또한 수동으로 수 **adprep.exe /rodcprep** 읽기 전용 도메인 컨트롤러 배포를 계획 하는 경우입니다.  
  
### <a name="review-options-and-view-script"></a>스크립트 보기 및 리뷰 옵션  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeReviewOptions.png)  
  
**리뷰 옵션** 페이지를 설정을 확인 하 고 설치를 시작 하기 전에 사용자의 요구 사항을 충족 시키는 확인 수 있습니다. 마지막 기회를 서버 관리자를 사용 하 고 설치를 중단 되었습니다. 이 페이지 간단 하 게 검토 하 고 설정을 구성 계속 하기 전에 확인 수 있습니다.  
  
**리뷰 옵션** 서버 관리자의 페이지도 선택적 제공 **스크립트 보기** 단추를 현재 ADDSDeployment 구성을 하나의 Windows PowerShell 스크립트도 포함 유니코드 텍스트 파일을 만듭니다. 서버 관리자 그래픽 인터페이스 Windows PowerShell 배포 studio로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용 하 여 옵션 구성 구성, 내보내고 마법사 취소 합니다.  이 프로세스 추가 수정 또는 직접 사용에 대해 유효 하 고 구문이 샘플을 만듭니다.  
  
예를 들어:  
  
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
> 일반적으로 서버 관리자 모든 인수 및 (에 따라 수 향후 버전의 Windows 또는 서비스 팩 간에) 기본값에 의존 하지 않는 경우 값을 입력 합니다. 이 한 가지 예외는는 **-safemodeadministratorpassword** 인수 합니다. 강제로 프롬프트가 생략 값 cmdlet 대화식으로 실행 될 때  
>   
> 옵션을 사용 하 여 **Whatif** 인수의 **설치 ADDSDomainController** cmdlet 구성 정보를 검토 합니다. 이렇게 하면 cmdlet에 대 한 인수 명시적 및 암묵적인 값을 볼 수 있습니다.  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSWhatIf.png)  
  
### <a name="prerequisites-check"></a>필수 확인  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrereqCheck.png)  
  
**필수 확인** 광고 DS 도메인 구성의 새로운 기능입니다. 이 새로운 단계 도메인 및 숲은 새 Windows Server 2012 도메인 컨트롤러를 지원할 수를 확인 합니다.  
  
새 도메인 컨트롤러를 설치할 때는 서버 관리자 Active Directory 도메인 서비스 구성 마법사 호출 일련의 연속된 모듈식 테스트 합니다. 이러한 테스트 제안 된 복구 옵션을 알립니다. 필요에 따라 여러 번 테스트를 실행할 수 있습니다. 도메인 컨트롤러 프로세스 수 없는 모든 필수 테스트까지 계속 제공 전달 됩니다.  
  
**필수 확인** 이전 운영 체제에 영향을 주는 보안 변경와 같은 관련 정보를 표면 수도 있습니다.  
  
특정 필수 검사에 대 한 자세한 내용은 참조 [필수 검사](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)합니다.  
  
무시할 수 없는 **필수 확인** 때 되는데 서버 관리자를 사용 하 여 건너뛸 수 프로세스 AD DS 배포 cmdlet 인수를 사용 하 여 사용 하는 경우:  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> Microsoft 부분 도메인 컨트롤러 프로 모션 발생할 수 있는 되거나 손상 AD DS 숲 필수 검사를 건너뛰는 것이 수 없게 됩니다.  
  
클릭 **설치** 도메인 컨트롤러 프로 모션 프로세스를 시작 합니다. 설치를 취소 하 마지막 기회입니다. 시작 된 후 프로 모션 프로세스를 취소할 수 없습니다. 컴퓨터가 끝 프로 모션 결과 관계 없이 프로 모션에 자동으로 재부팅 됩니다. **필수 확인** 페이지 프로세스와 문제를 해결 하기 위한 지침 하는 동안 발생 한 문제에 표시 됩니다.  
  
### <a name="installation"></a>설치  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeInstallProgress.png)  
  
때는 **설치** 페이지에 표시, 도메인 컨트롤러 구성 시작 되 고 하거나 수 없는 중단 취소 합니다. 자세한 작업이이 페이지에 표시 되며, 로그에 기록 합니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
-   %systemroot%\debug\adprep\logs  
  
-   %systemroot%\debug\netsetup.log (서버 작업 그룹 경우)  
  
ADDSDeployment 모듈을 사용 하 여 새 Active Directory 숲을 설치 하려면 다음 cmdlet 사용:  
  
```  
Install-addsdomaincontroller  
```  
  
참조 [업그레이드와 Windows PowerShell 복제본](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS) 인수 필수 및 선택 사항에 대 한 합니다.  
  
**설치 AddsDomainController** cmdlet (필수 확인 하 고 설치) 2 단계에 있습니다. 아래 두 그림 표시 설치 단계와의 최소는 인수 **-도메인 이름** 및 **-자격 증명**합니다. 어떻게 Adprep 작업을 자동으로 정품 인증을 기존 Windows Server 2003 숲 첫 번째 Windows Server 2012 도메인 컨트롤러 추가의 일부로 note 다음과 같습니다.  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSGetCred.png)  
  
참고 방법을 지난번 처럼 서버 관리자 **설치 ADDSDomainController** 프로 모션 서버 자동으로 부팅 하 게 알려줍니다. 다시 부팅 메시지를 자동으로 동의를 사용 하 여는 **-강제로** 또는 **-확인: $false** 인수 모든 ADDSDeployment Windows PowerShell cmdlet 사용 합니다. 서버 끝 프로 모션에 자동으로 다시 부팅 되지 않도록 하려면 사용는 **-norebootoncompletion** 인수 합니다.  
  
> [!WARNING]  
> 다시 부팅 재정의 것이 좋습니다. 도메인 컨트롤러 제대로 작동 하려면 다시 부팅 해야 합니다.  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeConfirm.gif)  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeProgress.png)  
  
배치를 Windows PowerShell를 사용 하 여 원격 도메인 컨트롤러를 구성 하 고 **설치 adddomaincontroller** cmdlet *내* 의 **호출 명령** cmdlet 합니다. 이 경우 기호와 사용 해야 합니다.  
  
```  
invoke-command {install-addsdomaincontroller "domainname <domain> -credential (get-credential)} -computername <dc name>  
```  
  
예를 들어:  
  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeExample.gif)  
  
> [!NOTE]  
> 설치 및 Adprep 프로세스가 작동 방식에 대 한 자세한 내용은 참조는 [문제 해결 도메인 컨트롤러 배포](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)합니다.  
  
### <a name="results"></a>결과  
![복제본 설치](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**결과** 프로 모션 및 관리 중요 한 정보가의 성공 여부 페이지에 표시 됩니다. 성공 하면 도메인 컨트롤러 10 초 후 자동으로 다시 부팅 됩니다.  
  
이전 버전의 Windows Server와 마찬가지로 Windows server 2012를 실행 하는 도메인 컨트롤러에 대 한 자동화 된 도메인 준비 GPPREP 실행 되지 않습니다. 실행 **adprep.exe /gpprep** 이전에 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 r 2에 대 한 준비 되지 된 모든 도메인에 대 한 수동으로 합니다. 모든 업그레이드를 하지는 도메인의 기록에 한 번만 GPPrep 실행 해야 합니다. 해당 작업 모든 도메인 컨트롤러에 다시 복제할 SYSVOL 폴더의 모든 파일 및 폴더를 시킬 수 있으므로 Adprep.exe /gpprep 자동으로 실행 되지 않습니다.  
  

