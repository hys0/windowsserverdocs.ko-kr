---
ms.assetid: e3d55565-ad45-4504-ad73-8103d1a92170
title: "새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 (수준을 200) 설치"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fc0eecc44bbc5f7459f22aceb5ebe41cd61948b6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-new-windows-server-2012-active-directory-child-or-tree-domain-level-200"></a>새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 (수준을 200) 설치

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 자녀와 밤나무 도메인 서버 관리자 또는 Windows PowerShell 사용 하 여 기존 Windows Server 2012 숲 프로그램을 추가 하는 방법에 설명 합니다.  
  
-   [자녀 및 밤나무 도메인 워크플로](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [자녀 및 밤나무 도메인 Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)  
  
-   [배포](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Deployment)  
  
## <a name="BKMK_Workflow"></a>자녀 및 밤나무 도메인 워크플로  
다음 그림 AD DS 역할을 이전에 설치 되어 있고 Active Directory 도메인 서비스 구성 마법사 서버 관리자를 사용 하 여 기존 숲 속의 새 도메인을 만들기 시작 때 Active Directory 도메인 서비스 구성 프로세스를 보여 줍니다.  
  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/adds_childtreedeploy_beta1.png)  
  
## <a name="BKMK_PS"></a>자녀 및 밤나무 도메인 Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수 (**굵게** 인수가 필요 합니다. *기울임꼴로 표시* 인수 Windows PowerShell 또는 광고 DS 구성 마법사를 사용 하 여 지정할 수 있습니다.)|  
|**설치 AddsDomain**|-SkipPreChecks<br /><br />***-NewDomainName***<br /><br />***-ParentDomainName***<br /><br />***-SafeModeAdministratorPassword***<br /><br />*-ADPrepCredential*<br /><br />-AllowDomainReinstall<br /><br />-확인<br /><br />*-CreateDNSDelegation*<br /><br />***자격 증명***<br /><br />*-데이터베이스 경로*<br /><br />*-DNSDelegationCredential*<br /><br />-NoDNSOnNetwork<br /><br />*-DomainMode*<br /><br />***-DomainType***<br /><br />힘<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />*-NewDomainNetBIOSName*<br /><br />*-NoGlobalCatalog*<br /><br />-NoNorebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-SiteName*<br /><br />-SkipAutoConfigureDNS<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-자격 증명** 인수는만 하면 하지에 현재 로그온 Enterprise 관리자 그룹의 회원으로 경우 필요 합니다. **-NewDomainNetBIOSName** DNS 도메인 이름 접두사에 따라 자동으로 생성 된 15 자의 이름 변경 하려는 경우 또는 이름을 초과 15 자 하는 경우의 인수가 필요 합니다.  
  
## <a name="BKMK_Deployment"></a>배포  
  
### <a name="deployment-configuration"></a>배포 구성  
다음 스크린샷 도메인 자녀를 추가 하기 위한 옵션을 보여 줍니다.  
  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDeployConfig.png)  
  
다음 스크린샷 밤나무 도메인 추가 하기 위한 옵션을 보여 줍니다.  
  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_TreeDeployConfig.png)  
  
서버 관리자 모든 도메인 컨트롤러 프로 모션으로 시작 되 고 **배포 구성** 페이지 합니다. 나머지 옵션과 필수 필드가 페이지에서 다음 페이지를 선택 하는 배포 작업에 따라 변경 됩니다.  
  
이 항목 두 번 별도 작업이 결합: 자녀 도메인 모션과 밤나무 도메인 프로 모션 합니다. 두 가지 작업이 것뿐입니다 만들기를 선택 도메인 유형이 합니다. 두 가지 작업이 간에 다른 단계를 모두 동일합니다.  
  
-   새 자녀 도메인 만들려면 클릭 **도메인 기존 숲에 추가** 선택 **자녀 도메인**합니다. 에 대 한 **부모 도메인 이름**를 입력 하거나 부모 도메인의 이름을 선택 합니다. 다음에 새는 도메인의 이름을 입력는 **새 도메인 이름** 상자 합니다. 제공 유효한, 단일 레이블 자녀 도메인 이름입니다. 이름은 DNS 도메인 이름 요구 사용 해야 합니다.  
  
-   기존 숲 내 밤나무 도메인 만들려면 클릭 **도메인 기존 숲에 추가** 선택 **트리 도메인**합니다. 이렇게의 이름을 입력 한 다음 새는 도메인의 이름을 입력 합니다. 제공 유효한, 정식 루트 도메인 이름입니다. 단일 레이블이 표시 될 수 없는 이름과 DNS 도메인 이름 요구 사항에 사용 해야 합니다.  
  
DNS 이름에 대 한 자세한 내용은 참조 [명명 컴퓨터에서 도메인, 사이트 및 Ou에 대 한 Active Directory 규칙](https://support.microsoft.com/kb/909264)합니다.  
  
서버 관리자 Active Directory 도메인 서비스 구성 묻는 도메인 자격 증명을 현재 자격 증명 도메인 없는 경우입니다. 클릭 **변경** 프로 모션 작업에 대 한 도메인 자격 증명을 제공 합니다.  
  
배포 구성 ADDSDeployment cmdlet 및 인수는 다음과 같습니다.  
  
```  
Install-AddsDomain  
-domaintype <{childdomain | treedomain}>  
-parentdomainname <string>  
-newdomainname <string>  
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_DCOptions_Child.gif)  
  
**도메인 컨트롤러 옵션** 페이지 새 도메인 컨트롤러에 대 한 도메인 컨트롤러 옵션을 지정 합니다. 가능한 도메인 컨트롤러 옵션이 포함 **DNS 서버** 및 **드**; 새 도메인의 첫 번째 도메인 컨트롤러 읽기 전용 도메인 컨트롤러를 구성할 수 없습니다.  
  
모든 도메인 컨트롤러 분산된 환경에서 사용 가능 하도록 DNS 및 GC 서비스를 제공 하는 것이 좋습니다. 기본적으로 GC은 항상 선택 하 고 현재 도메인 권한 시작 쿼리에 따라 해당 Dc에 이미 DNS 호스트 하는 경우 DNS 기본적으로 선택 됩니다. 또한 지정 해야는 **도메인 기능 수준**합니다. 기본 기능 수준을 Windows Server 2012와 다른 값 현재 숲 기능 수준 이상의 선택할 수 있습니다.  
  
**도메인 컨트롤러 옵션** 페이지도 논리 적절 한 Active Directory를 선택할 수 있습니다 **사이트 이름** 숲 구성에서 합니다. 기본적으로 가장 적은 서브넷 사이트 선택 됩니다. 사이트가 하나뿐인 경우 자동으로 선택 됩니다.  
  
> [!IMPORTANT]  
> 서버 Active Directory 서브넷에 속하지 않는 경우 둘 이상의 Active Directory 사이트가 아무 것도 선택 및 **다음** 단추는 목록에서 사이트를 선택할 때까지 사용할 수 없습니다.  
  
지정 된 **디렉터리 서비스 복원 모드 암호** 서버에 적용 암호 정책을 준수 해야 합니다. 항상 복잡 하 고 강력한 암호 또는 암호를 선택 합니다.  
  
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
> 한 값으로 제공 되는 경우에 이미 사이트 이름이 있어야는 **sitename** 인수 합니다. **설치-AddsDomainController** cmdlet 사이트의 이름을 생성 하지 않습니다. 사용할 수는 **새로운 adreplicationsite** cmdlet 새 사이트를 만들 수 있습니다.  
  
**설치 ADDSDomainController** cmdlet 인수 지정 되지 않은 경우 동일한 기본값 서버 관리자로 서을 따릅니다.  
  
**SafeModeAdministratorPassword** 특별 한 인수의 작업은 다음과 같습니다.  
  
-   하는 경우 *지정 하지* 를 인수로 cmdlet 묻는 메시지를 입력 하 고 마스크 암호를 확인 합니다. 기본 설정된 사용 cmdlet 대화식으로 실행 될 때입니다.  
  
    예를 들어, 새 자녀 도메인 Contoso.com 숲 속의 NorthAmerica 라는 만들고 입력 하 고 마스크 비밀 번호를 확인 하 라는 메시지가 표시 됩니다.  
  
    ```  
    Install-ADDSDomain "NewDomainName NorthAmerica "ParentDomainName Contoso.com "DomainType Child  
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
> 지우기 또는 애매 텍스트 암호를 저장 또는 제공 권장 하지 않습니다. 스크립트가이 명령을 실행 또는이 기사를 통해 모든 사용자 해당 도메인 컨트롤러의 DSRM 암호를 알고 있습니다.  애매 암호를 취소할 수 파일에 액세스할 수 있는 모든 사람이. 해당 정보를 DSRM 시작 DC에 로그온 하 고 자녀의 권한 광고 숲에서 가장 높은 수준의에 상승 도메인 컨트롤러 자체, 가장 결국 수 있습니다. 추가 단계를 사용 하 여 집합 **System.Security.Cryptography** 데이터는 것이 좋습니다 하지만 아니었습니다 텍스트 파일을 암호화 됩니다. 완전히 암호 저장을 방지 하는 것이 좋습니다.  
  
ADDSDeployment 모듈 자동으로 DNS 클라이언트 설정, 전달자 및 루트 힌트 구성을 건너뛰게 하는 추가 옵션을 제공 합니다. 이 없는 경우 구성할 수 서버 관리자를 사용 하는 경우 이 인수 도메인 컨트롤러 구성 전에 DNS 서버 서비스를 이미 설치한 경우에 중요 합니다.  
  
```  
-SkipAutoConfigureDNS  
  
```  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS 옵션과 DNS 위임 자격 증명  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDNSOptions.png)  
  
**DNS 옵션** 페이지 위임 대체 DNS 관리자 자격 증명을 제공할 수 있습니다.  
  
DNS 설치에서 선택한 위치에 기존 숲-새 도메인 설치할 때의 **도메인 컨트롤러 옵션** 페이지-옵션; 구성 수 없는 위임 완전히 하 고 자동으로 정품 인증 됩니다. 해당 구조 업데이트에 대 한 권한을 대체 DNS 관리 자격 증명을 제공 하는 옵션이 있습니다.  
  
**DNS 옵션** ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
DNS 위임에 대 한 자세한 내용은 참조 [이해 영역 위임](https://technet.microsoft.com/library/cc771640.aspx)합니다.  
  
### <a name="additional-options"></a>추가 옵션  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildAdditionalOptions.png)  
  
**추가 옵션** 페이지 표시 되는 도메인의 NetBIOS 이름 및 재정의 수 있습니다. 기본적으로 NetBIOS 도메인 이름 일치 제공 정식된 도메인 이름의 왼쪽 맨 레이블을 **배포 구성** 페이지 합니다. 예를 들어 corp.contoso.com 정식된 도메인 이름을 제공한 경우 기본 NetBIOS 도메인 이름은 CORP.  
  
이름이 15 자 충돌 하지 않는 다른 NetBIOS 이름의 유효 하지 변경 합니다. NetBIOS 다른 이름으로 충돌 하 않도록 숫자 이름에 추가 됩니다. 이름이 15 자 경우 마법사 고유한, 잘림 제안을 제공 합니다. 두 경우 모두 마법사 먼저의 유효성을 검사 이름이 없는 통해 WINS 조회 사용에서 및 NetBIOS 브로드캐스트 됩니다.  
  
DNS 이름에 대 한 자세한 내용은 참조 [명명 컴퓨터에서 도메인, 사이트 및 Ou에 대 한 Active Directory 규칙](https://support.microsoft.com/kb/909264)합니다.  
  
**설치 AddsDomain** 인수 지정 되지 않은 경우 동일한 기본값 서버 관리자로 서을 따릅니다. **DomainNetBIOSName** 특별 한 작업은 다음과 같습니다.  
  
1.  하는 경우는 **NewDomainNetBIOSName** 인수 NetBIOS 도메인 이름와의 단일 레이블 접두사 도메인 이름 지정 하지 않으면는 **도메인 이름** 인수가 15 자 이하로 다음 프로 모션 계속 자동으로 생성 된 이름입니다.  
  
2.  하는 경우는 **NewDomainNetBIOSName** 인수 NetBIOS 도메인 이름와의 단일 레이블 접두사 도메인 이름 지정 하지 않으면는 **도메인 이름** 인수는 16 자로 이상 프로 모션 실패 합니다.  
  
3.  하는 경우는 **NewDomainNetBIOSName** 인수 15 자 이하로 NetBIOS 도메인 이름으로 지정 프로 모션 지정 된 이름이 계속 합니다.  
  
4.  하는 경우는 **NewDomainNetBIOSName** 인수 16 자로의 NetBIOS 도메인 이름 또는 기타를 지정 프로 모션 실패 합니다.  
  
**추가 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-newdomainnetbiosname <string>  
```  
  
### <a name="paths"></a>경로  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
**경로** 페이지 AD DS 데이터베이스, 데이터 기본 트랜잭션 로그가 및 SYSVOL 공유에서 기본 폴더 위치를 무시할 수 있습니다. 기본 위치는 항상 하위 시스템 루트 %의입니다.  
  
**경로** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>스크립트 보기 및 리뷰 옵션  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildReviewOptions.png)  
  
**리뷰 옵션** 페이지를 설정을 확인 하 고 설치를 시작 하기 전에 사용자의 요구 사항에 맞는지 확인 수 있습니다. 설치 관리자 서버를 사용할 때 중지 마지막 기회 않습니다. 이 옵션은 구성 계속 하기 전에 설정을 확인 하는 옵션 간단 하 게  
  
**리뷰 옵션** 서버 관리자의 페이지도 선택적 제공 **스크립트 보기** 단추를 현재 ADDSDeployment 구성을 하나의 Windows PowerShell 스크립트도 포함 유니코드 텍스트 파일을 만듭니다. 서버 관리자 그래픽 인터페이스 Windows PowerShell 배포 studio로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용 하 여 옵션 구성 구성, 내보내고 마법사 취소 합니다.  이 프로세스 추가 수정 또는 직접 사용에 대해 유효 하 고 구문이 샘플을 만듭니다. 예를 들어:  
  
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
> 일반적으로 서버 관리자 모든 인수 및 (에 따라 수 향후 버전의 Windows 또는 서비스 팩 간에) 기본값에 의존 하지 않는 경우 값을 입력 합니다. 이 한 가지 예외는는 **-safemodeadministratorpassword** 인수 (스크립트에서 의도적으로 생략은). 확인 메시지가 되도록 값을 생략 cmdlet 대화식으로 실행 될 때 합니다.  
  
옵션을 사용 하 여 **Whatif** 인수의 **설치 ADDSForest** cmdlet 구성 정보를 검토 합니다. 이렇게 하면 cmdlet에 대 한 인수 명시적 및 암묵적인 값을 볼 수 있습니다.  
  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildWhatIf.png)  
  
### <a name="prerequisites-check"></a>필수 확인  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildPrereqCheck.png)  
  
**필수 확인** 광고 DS 도메인 구성의 새로운 기능입니다. 이 새로운 단계 서버 구성 새 광고 DS 도메인을 지원할 수 확인 합니다.  
  
새 숲 루트 도메인을 설치할 때는 서버 관리자 Active Directory 도메인 서비스 구성 마법사 호출 일련의 연속된 모듈식 테스트 합니다. 이러한 테스트 제안 된 복구 옵션을 알립니다. 필요에 따라 여러 번 테스트를 실행할 수 있습니다. 도메인 컨트롤러 프로세스 수 없는 모든 필수 테스트까지 계속 제공 전달 됩니다.  
  
**필수 확인** 이전 운영 체제에 영향을 주는 보안 변경와 같은 관련 정보를 표면 수도 있습니다.  
  
에 대 한 자세한 내용은 특정 필수 검사를 [필수 검사](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)합니다.  
  
무시할 수 없는 **필수 확인** 때 되는데 서버 관리자를 사용 하 여 건너뛸 수 프로세스 AD DS 배포 cmdlet 인수를 사용 하 여 사용 하는 경우:  
  
```  
-skipprechecks  
```  
  
> [!WARNING]  
> Microsoft 부분 도메인 컨트롤러 프로 모션 발생할 수 있는 되거나 손상 AD DS 숲 필수 검사를 건너뛰는 것이 수 없게 됩니다.  
  
클릭 **설치** 도메인 컨트롤러 프로 모션 프로세스를 시작 합니다. 설치를 취소 하 마지막 기회입니다. 시작 된 후 프로 모션 프로세스를 취소할 수 없습니다. 컴퓨터가 끝 프로 모션 결과 관계 없이 프로 모션에 자동으로 재부팅 됩니다.  
  
### <a name="installation"></a>설치  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildInstallation.png)  
  
때는 **설치** 페이지에 표시, 도메인 컨트롤러 구성 시작 되 고 하거나 수 없는 중단 취소 합니다. 자세한 작업이이 페이지에 표시 되며, 로그에 기록 합니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment 모듈을 사용 하 여 새 Active Directory 도메인을 설치 하려면 다음 cmdlet 사용:  
  
```  
Install-addsdomain  
```  
  
참조 [자녀와 밤나무 도메인 Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS) 인수 필수 및 선택 사항에 대 한 합니다. **설치 addsdomain** cmdlet (필수 확인 하 고 설치) 2 단계에 있습니다. 아래 두 그림 표시 설치 단계와의 최소는 인수 **-domaintype**, **-newdomainname**, **-parentdomainname**, 및 **-자격 증명**합니다. 참고 방법을 지난번 처럼 서버 관리자 **설치 ADDSDomain** 프로 모션 서버 자동으로 부팅 하 게 알려줍니다.  
  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomain.png)  
  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomainProgress.png)  
  
다시 부팅 메시지를 자동으로 동의를 사용 하 여는 **-강제로** 또는 **-확인: $false** 인수 모든 ADDSDeployment Windows PowerShell cmdlet 사용 합니다. 서버 끝 프로 모션에 자동으로 다시 부팅 되지 않도록 하려면 사용는 **-norebootoncompletion** 인수 합니다.  
  
> [!WARNING]  
> 다시 부팅 재정의 권장 하지 않습니다. 제대로 작동 하려면 다시 부팅 해야 도메인 컨트롤러  
  
### <a name="results"></a>결과  
![새 광고 자녀 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**결과** 프로 모션 및 관리 중요 한 정보가의 성공 여부 페이지에 표시 됩니다. 도메인 컨트롤러 10 초 후 자동으로 다시 부팅 됩니다.  
  

