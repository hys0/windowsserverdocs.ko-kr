---
ms.assetid: ae241ed8-ef19-40a9-b2d5-80b8391551ff
title: "Active Directory Domain Services (수준을 100) 설치"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f76aa1e5200a9fc2f47a559c4a318aa619d31557
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-active-directory-domain-services-level-100"></a>Active Directory Domain Services (수준을 100) 설치

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server 2012에서 광고 DS 다음 방법 중 하나를 사용 하 여 설치 하는 방법을 설명 합니다.  
  
-   [Adprep.exe 실행 하 고 Active Directory 도메인 서비스 설치 자격 증명 요구 사항](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)  
  
-   [AD DS Windows PowerShell를 사용 하 여 설치](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PS)  
  
-   [광고 DS 서버 관리자를 사용 하 여 설치](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_GUI)  
  
-   [RODC 설치 준비 그래픽 사용자 인터페이스를 사용 하 여 수행](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_UIStaged)  
  
## <a name="BKMK_Creds"></a>Adprep.exe 실행 하 고 Active Directory 도메인 서비스 설치 자격 증명 요구 사항  
다음 자격 증명 Adprep.exe 실행 하 고 광고 DS 설치 해야 합니다.  
  
-   새 숲을 설치 하려면 컴퓨터에 대 한 현지 관리자 권한으로 로그온 해야 합니다.  
  
-   새 자녀 도메인 또는 새 도메인 트리를 설치 하려면 관리자 Enterprise 그룹의 회원으로 로그온 해야 합니다.  
  
-   기존 도메인에 추가 도메인 컨트롤러를 설치 하려면 관리자 도메인 그룹의 회원 이어야 합니다.  
  
    > [!NOTE]  
    > Adprep.exe 명령 별도로 실행 하지 않는 경우 기존 도메인 또는 숲 속의 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 설치 하는 Adprep 명령을 실행 하려면 자격 증명을 입력 하 라는 메시지가 표시 됩니다. 자격 증명 요구 사항은 다음과 같습니다.  
    >   
    > -   첫 번째 Windows Server 2012 도메인 컨트롤러의 숲 속의 기능을 소개 하 그룹 엔터프라이즈 관리자 스키마 관리자 그룹의 회원에 대해 자격 증명을 제공 해야 할 및 도메인 관리자 그룹 도메인에 있는 호스트 하는 스키마 마스터 합니다.  
    > -   도메인의 첫 번째 Windows Server 2012 도메인 컨트롤러를 소개 도메인 관리자 그룹의 회원에 대해 자격 증명을 제공 해야 합니다.  
    > -   첫 번째 읽기 전용 RODC (도메인 컨트롤러)는 숲 속의 기능을 소개 하 Enterprise 관리자 그룹의 회원에 대해 자격 증명을 제공 해야 합니다.  
    >   
    >     > [!NOTE]  
    >     > Windows Server 2008 또는 Windows Server 2008 R2 이미 adprep /rodcprep을 실행 하는 경우 Windows Server 2012에 대 한 다시 실행 필요는 없습니다.  
  
## <a name="BKMK_PS"></a>AD DS Windows PowerShell를 사용 하 여 설치  
Windows Server 2012 부터는 AD DS Windows PowerShell를 사용 하 여 설치할 수 있습니다. Dcpromo.exe 일부 터 Windows Server 2012와 더 이상 사용이 있지만 dcpromo.exe 응답 파일을 사용 하 여 실행할 수 있습니다 (dcpromo /unattend:<answerfile> 또는 dcpromo /answer:<answerfile>). 계속 dcpromo.exe 응답 파일을 사용 하 여 실행 하는 기능 기존 자동화 시간이 자동화 dcpromo.exe에서 Windows PowerShell로 변환에 투자 리소스를 소유 하는 조직의 제공 합니다. For more information about running dcpromo.exe with an answer file, see [https://support.microsoft.com/kb/947034](https://support.microsoft.com/kb/947034).  
  
Windows PowerShell를 사용 하 여 광고 DS 제거에 대 한 자세한 내용은 참조 [Windows PowerShell를 사용 하 여 광고 DS 제거](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c#BKMK_RemovePS)합니다.  
  
역할을 추가 하면 Windows PowerShell를 사용 하 여 시작 합니다. 이 명령을 AD DS 서버 역할을 설치 및 광고 DS 및 광고 LDS 서버 관리 도구, Active Directory 사용자 컴퓨터 등 GUI 기반 도구와 같은 dcdia.exe 명령줄 도구를 포함 하 여 설치 합니다. 서버 관리 도구 Windows PowerShell를 사용 하면 기본적으로 설치 되지 않습니다. You need to specify **"IncludeManagementTools** to manage the local server or install [Remote Server Administration Tools](https://www.microsoft.com/download/details.aspx?id=28972) to manage a remote server.  
  
```  
Install-windowsfeature -name AD-Domain-Services -IncludeManagementTools  
<<Windows PowerShell cmdlet and arguments>>  
```  
  
다시 부팅 AD DS 설치가 완료 된 후 될 때까지 필요 없는 경우  
  
이 명령을 ADDSDeployment 모듈에 사용할 수 있는 cmdlet 보려면 다음 실행할 수 있습니다.  
  
```  
Get-Command -Module ADDSDeployment
```  
  
구문 및 cmdlet에 인수 지정할 수 있는의 목록을 보려면:  
  
```  
Get-Help <cmdlet name>  
```  
  
예를 들어 입력 읽기 전용 빈된 도메인 컨트롤러 (RODC) 계정을 만드는 데 필요한 인수를 보려면  
  
```  
Get-Help Add-ADDSReadOnlyDomainControllerAccount
```  
  
(옵션) 인수 대괄호에 표시 됩니다.  
  
또한 최신 도움말 예와 Windows PowerShell cmdlet에 대 한 개념을 다운로드할 수 있습니다. For more information, see [about_Updatable_Help](https://technet.microsoft.com/library/hh847735.aspx).  
  
원격 서버에 대해 Windows PowerShell cmdlet을 실행할 수 있습니다.  
  
-   Windows PowerShell에서 Invoke-Command ADDSDeployment cmdlet 사용 합니다. 예를 들어 설치 하려면 AD DS ConDC3 contoso.com 도메인에 있는 이라는 원격 서버에 입력 합니다.  
  
    ```  
    Invoke-Command { Install-ADDSDomainController -DomainName contoso.com -Credential (Get-Credential) } -ComputerName ConDC3  
    ```  
  
또는  
  
-   서버 관리자에서 원격 서버를 포함 하는 서버 그룹을 만듭니다. 원격 서버의 이름을 마우스 오른쪽 단추로 클릭 한 **Windows PowerShell**합니다.  
  
다음 섹션에서는 ADDSDeployment 모듈 cmdlet 광고 DS 설치를 실행 하는 방법에 설명 합니다.  
  
-   [ADDSDeployment cmdlet 인수](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)  
  
-   [Windows PowerShell 자격 증명 지정](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSCreds)  
  
-   [테스트 cmdlet 사용 하 여](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_TestCmdlets)  
  
-   [새 숲 루트 도메인 Windows PowerShell를 사용 하 여 설치](../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSForest)  
  
-   [Windows PowerShell를 사용 하 여 새 자녀 또는 밤나무 도메인 설치](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSDomain)  
  
-   [추가 (복제본) 도메인 컨트롤러 Windows PowerShell를 사용 하 여 설치](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSReplica)  
  
### <a name="BKMK_Params"></a>ADDSDeployment cmdlet 인수  
다음 표에서 인수 ADDSDeployment Windows powershell에서 cmdlet에 대 한 보여 줍니다. 굵게 인수가 필요 합니다. 다른 Windows powershell에서 라고 하는 경우 해당 하는 인수 dcpromo.exe에 대 한 괄호에 나열 됩니다.  
  
Windows PowerShell 스위치 $TRUE 또는 $FALSE 인수에 동의 합니다. 기본적으로 $TRUE는 인수 지정할 수 필요가 없습니다.  
  
기본값을 재정의 하려면 $False 값으로 인수를 지정할 수 있습니다. 예를 들어 때문에 **-installdns** 지정 되지 않은에 유일한 방법은 경우 숲 새로 설치에 대 한 자동 실행 *방지* DNS 설치 새 숲 설치할 때 사용 하는 다음과 같습니다.  
  
```  
-InstallDNS:$false  
```  
  
마찬가지로, 때문에 **"installdns** 도메인 컨트롤러 Windows Server DNS 호스트 하지 않는 한 환경에서 설치 하는 경우에 $False의 기본값이 서버를 지정 하려면 다음 인수 DNS 서버를 설치 하려면:  
  
```  
-InstallDNS:$true  
```  
  
|인수|설명|  
|------------|---------------|  
|**ADPrepCredential <PS Credential> ** **참고:** 첫 번째 Windows Server 2012 도메인 컨트롤러를 설치 하는 도메인의 또는 숲 및 자격 증명은 현재 사용자의 작업을 수행할 수 있는 충분 한 없는 경우 필요 합니다.|Specifies the account with Enterprise Admins and Schema Admins group membership that can prepare the forest, according to the rules of [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) and a PSCredential object.<br /><br />값을 지정 값은 **"자격 증명** 인수를 사용 합니다.|  
|AllowDomainControllerReinstall|계속이 쓸 수 있는 도메인 컨트롤러 다른 쓸 수 있는 도메인 컨트롤러 계정 이름이 같은 감지 되는 것도 불구 하 고 설치를 지정 합니다.<br /><br />사용 하 여 **$True** 는 계정을 다른 쓸 수 있는 도메인 컨트롤러에서 현재 사용 하지 않은 경우에 합니다.<br /><br />기본값은 **$False**합니다.<br /><br />이 인수 RODC에 대해 유효 합니다.|  
|AllowDomainReinstall|기존 도메인 다시 있는지 여부를 지정 합니다.<br /><br />기본값은 **$False**합니다.|  
|< 문자열 > AllowPasswordReplicationAccountName|사용자 계정, 그룹 계정 및이 RODC에 암호를 복제 수 컴퓨터 계정의 이름을 지정 합니다. 빈 문자열을 사용 하 여 "" 값 빈 유지 하려는 경우입니다. 기본적으로만 허용 RODC 암호 복제 그룹, 수 있으며 빈 원래 만들어집니다.<br /><br />문자열 배열 값을 제공 합니다. 예를 들어:<br /><br />코드-AllowPasswordReplicationAccountName "JSmith", "JSmithPC", "분기 사용자에 게"|  
|< 문자열 > ApplicationPartitionsToReplicate **참고:** UI에 해당 하는 옵션이 없습니다. IFM 또는 UI를 사용 하 여 설치 하는 경우 모든 응용 프로그램 파티션은 복제 됩니다.|응용 프로그램 파티션 복제할 지정 합니다. 이 인수 지정 하는 경우에 적용 되는 **-InstallationMediaPath** 설치 미디어 (IFM)에서 인수 합니다. 기본적으로 파티션을 복제 하는 모든 응용 프로그램 자신의 범위에 따라 합니다.<br /><br />문자열 배열 값을 제공 합니다. 예를 들어:<br /><br />코드-<br /><br />-ApplicationPartitionsToReplicate "partition1", "partition2", "partition3"|  
|확인|라는 메시지가 표시 되는 cmdlet 실행 하기 전에 확인을 위해 합니다.|  
|CreateDnsDelegation **참고:** 추가 ADDSReadOnlyDomainController cmdlet 실행 하는 경우이 인수 지정할 수 없습니다.|도메인 컨트롤러 함께 설치 하는 새 DNS 서버를 참조 하 여 DNS 위임 만들 수를 나타냅니다. 유효한 Active Directory "통합 된 DNS만 합니다. 온라인으로 액세스할 수 있는 Microsoft DNS 서버에만 위임 레코드를 만들 수 있습니다. 즉시 하위.com,.gov,.biz,.edu.nz.au 등 2 못 국가 코드 도메인 등 최상위 도메인에 있는 도메인 위임 레코드를 만들 수 없습니다.<br /><br />기본 설정의 환경에 따라 자동으로 계산 됩니다.|  
|**자격 증명 <PS Credential> ** **참고:** 현재 사용자의 자격 증명은 작업을 수행할 수 있는 충분 한 경우에 필요 합니다.|Specifies the domain account that can logon to the domain, according to the rules of [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) and a PSCredential object.<br /><br />지정 하지 않으면, 경우 현재 사용자의 자격 증명 사용 됩니다.|  
|CriticalReplicationOnly|광고 DS 설치 작업이 다시 부팅 되기 전에 중요 한 복제 수행 하 고 다음 계속 여부를 지정 합니다. 중요 하지 않은 복제 설치가 완료 되 고 컴퓨터가 다시 부팅 한 후 발생 합니다.<br /><br />이 인수를 사용 하 여 권장 하지 않습니다.<br /><br />이 UI (사용자 인터페이스)의이 옵션에 대 한 해당이 있습니다.|  
|데이터베이스 경로 <string>|완전히 적격 지정 비 "예를 들어 도메인 데이터베이스를 포함 하는 로컬 컴퓨터의 고정 된 디스크에 디렉터리에 명명 UNC 범용 규칙 () 경로 **C:\Windows\NTDS 합니다.**<br /><br />기본값은 **%SYSTEMROOT%\NTDS**합니다. **중요:** 볼륨 (ReFS) 복원 파일 시스템으로 포맷 AD DS 데이터베이스와 로그 파일을 저장할 수, ReFS에서 광고 DS 호스팅 특정 이점이, ReFS 데이터가 호스팅 복구의 정상적인 혜택 이외의 받게 됩니다.|  
|DelegatedAdministratorAccountName <string>|사용자 또는 설치 하 고 RODC 관리할 수 있는 그룹의 이름을 지정 합니다.<br /><br />기본적으로 도메인 관리자 그룹의 회원만 RODC 관리할 수 있습니다.|  
|< 문자열 > DenyPasswordReplicationAccountName|사용자 계정, 그룹 계정 및 암호를 가진를이 RODC을 복제할 컴퓨터 계정의 이름을 지정 합니다. 빈 문자열을 사용 하 여 "" 사용자 또는 컴퓨터의 자격 증명 복제 거부 하지 않으려는 경우입니다. 기본적으로 관리자, 서버 연산자, 백업 연산자, 계정 운영자 및 RODC 거부 암호 복제 그룹 거부 됩니다. 기본적으로 RODC 암호 복제 거부 그룹 인증 게시자, 도메인 관리자, Enterprise 관리자, Enterprise 도메인 컨트롤러, 엔터프라이즈 전용 도메인 컨트롤러, 그룹 정책 Creator 소유자, krbtgt 계정 및 포함 스키마 관리 합니다.<br /><br />문자열 배열 값을 제공 합니다. 예를 들어:<br /><br />코드-<br /><br />-DenyPasswordReplicationAccountName "RegionalAdmins", "AdminPCs"|  
|DnsDelegationCredential <PS Credential> **참고:** 추가 ADDSReadOnlyDomainController cmdlet 실행 하는 경우이 인수 지정할 수 없습니다.|Specifies the user name and password for creating DNS delegation, according to the rules of [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) and a PSCredential object.|  
|DomainMode <DomainMode> {w i n 2003 & #124; Win2008 & #124; Win2008R2 & #124; Win2012 & #124; Win2012R2}<br /><br />또는<br /><br />DomainMode <DomainMode> {2 & #124; 3 & #124; 4 & #124; 5 & #124; 6}|새 도메인 생성 하는 동안 도메인 기능 수준을 지정합니다.<br /><br />도메인 기능 수준을 숲 기능 수준 미만 될 수 없지만 높은 될 수 있습니다.<br /><br />기본값은 자동으로 계산 하 고 기존 숲 기능 수준 나에 대해 설정 값으로 설정 **-포리스트의**합니다.|  
|**도메인 이름**<br /><br />설치 ADDSForest 및 설치 ADDSDomainController cmdlet에 대 한 필요합니다.|추가 도메인 컨트롤러를 설치 하려는 도메인 FQDN 지정 합니다.|  
|**DomainNetbiosName <string>**<br /><br />15 자 FQDN 접두사 이름 넘으면 설치 ADDSForest 필요 합니다.|설치 ADDSForest와 함께 사용 합니다. 새 숲 루트 도메인 NetBIOS 이름이 지정 됩니다.|  
|DomainType <DomainType> {ChildDomain & #124; TreeDomain} 또는 {자녀 & #124; 밤나무}|만들려는 하는 도메인의 종류를 나타냅니다:의 기존 새 도메인 밤나무 포리스트의 기존 도메인 또는 새 숲 자녀 합니다.<br /><br />DomainType에 대 한 기본값은 ChildDomain입니다.|  
|힘|이 매개 지정 된 경우 경고 도메인 컨트롤러의 추가을 설치 일반적으로 표시 되는 표시 되지 않습니다 실행 완료 cmdlet 수 있도록 합니다. 이 매개 설치 스크립팅 때 포함 유용할 수 있습니다.|  
|포리스트의 <ForestMode> {w i n 2003 & #124; Win2008 & #124; Win2008R2 & #124; Win2012 & #124; Win2012R2}<br /><br />또는<br /><br />포리스트의 <ForestMode> {2 & #124; 3 & #124; 4 & #124; 5 & #124; 6}|새 숲 만들 때 숲 기능 수준을 지정 합니다.<br /><br />기본값은 Win2012 합니다.|  
|InstallationMediaPath|설치 미디어 새 도메인 컨트롤러를 설치 하는 데 사용 될 수 있는 위치를 나타냅니다.|  
|InstallDns|DNS 서버 서비스를 설치 및 구성 도메인 컨트롤러에 지정 합니다.<br /><br />새 숲에 대 한 기본값은 **$True** DNS 서버를 설치 하 고 있습니다.<br /><br />새 자녀 도메인 또는 도메인 밤나무, 부모 도메인 (또는 이렇게 도메인 트리) 이미 호스트 하 고 저장 DNS 이름을 도메인에 대 한 경우이 매개에 대 한 기본값은 $True 합니다.<br /><br />기존 도메인에 도메인 컨트롤러 설치에 대 한이 매개 지정 하지 않으면 하 고 현재 도메인 이미 섬에는이 매개에 대 한 기본값은 다음 도메인 DNS 이름을 저장 **$True**합니다. 그렇지 않으면 DNS 도메인 이름, Active Directory 외 호스트 기본값은 **$False** DNS 서버가 설치 되어 있습니다.|  
|LogPath <string>|예를 들어 도메인 로그 파일을 포함 하는 로컬 컴퓨터의 고정 된 디스크에 정식된, 비 UNC 경로 디렉터리를 지정 **C:\Windows\Logs**합니다.<br /><br />기본값은 **%SYSTEMROOT%\NTDS**합니다. **중요:** (ReFS) 복원 파일 시스템으로 포맷 데이터 볼륨 Active Directory 로그 파일 저장 하지 않습니다.|  
|MoveInfrastructureOperationMasterRoleIfNecessary|인프라 역할을 전송 마스터 작업 마스터 (단일 마스터 작업 라고도 유연한 또는 FSMO)를 만들 "경우 드 서버에 현재 호스트"는 도메인 컨트롤러를 확인 하려면 도메인 컨트롤러에 것인지 지정 드 서버를 만드는 것입니다. 이 매개 변수를 전송, 필요한 경우를 대비 만드는 도메인 컨트롤러 infrastructure 마스터 역할을 전송 지정 이 경우 지정는 **NoGlobalCatalog** 인프라 마스터 역할 현재 경우 계속 하려면 옵션입니다.|  
|**NewDomainName <string> ** **참고:** 설치 ADDSDomain에 대해서만 필요 합니다.|새 도메인에 대 한 단일 도메인 이름을 지정합니다.<br /><br />예를 들어 라는 새로운 자녀 도메인 만들려는 경우 **emea.corp.fabrikam.com**를 지정 해야 **emea** 이 인수 한 값으로 합니다.|  
|**NewDomainNetbiosName <string>**<br /><br />15 자 FQDN 접두사 이름 넘으면 설치 ADDSDomain 필요 합니다.|설치 ADDSDomain와 함께 사용 합니다. 새 도메인 NetBIOS 이름이 지정 됩니다. 기본값은 값에서 파생 **"NewDomainName**합니다.|  
|NoDnsOnNetwork|DNS 서비스 네트워크에서 사용할 수 없다는 지정 합니다. 이 매개 DNS 서버의 이름 확인을 위해 이름으로 네트워크 어댑터가 컴퓨터의 IP 설정을 구성 되지 않을 경우에 사용 됩니다. DNS 서버 이름 확인을 위해이 컴퓨터에 설치 됩니다 있는지를 나타냅니다. 그렇지 않은 경우 네트워크 어댑터의 IP 설정은 먼저 DNS 서버 주소를 구성 합니다.<br /><br />이 매개 (기본) 생략이 서버 컴퓨터에 네트워크 어댑터의 TCP/IP 클라이언트 설정 DNS 서버에 연결 하는 나타냅니다. 따라서이 매개 변수를 지정 하지 않는 경우 기본 설정 DNS 서버 주소 TCP/IP 설정을 클라이언트 먼저 구성 되어 있는지 확인 합니다.|  
|NoGlobalCatalog|도메인 컨트롤러 서버 드 원하지 않는 지정 합니다.<br /><br />Windows Server 2012를 실행 하는 도메인 컨트롤러 기본적으로 드도 설치 됩니다. 즉,이 자동으로 실행 계산을 않고도 지정 하지 않은 경우:<br /><br />코드-<br /><br />-NoGlobalCatalog|  
|NoRebootOnCompletion|지정 명령의 성공 여부에 상관 없이 완료 되 면 컴퓨터를 다시 시작 합니다. 기본적으로 컴퓨터를 다시 시작 됩니다. 서버를 다시 시작 되지 않도록 하려면 지정:<br /><br />코드-<br /><br />-NoRebootOnCompletion: $True<br /><br />이 UI (사용자 인터페이스)의이 옵션에 대 한 해당이 있습니다.|  
|**ParentDomainName <string> ** **참고:** 설치 ADDSDomain cmdlet에 대 한 필요 합니다.|기존 부모 도메인 FQDN 지정합니다. 이 인수를 사용 하 여 자녀가 도메인 또는 새 도메인 밤나무 설치 하면 됩니다.<br /><br />예를 들어 라는 새로운 자녀 도메인 만들려는 경우 **emea.corp.fabrikam.com**를 지정 해야 **corp.fabrikam.com** 이 인수 한 값으로 합니다.|  
|ReadOnlyReplica|읽기 전용 도메인 컨트롤러 (RODC)를 설치를 지정 합니다.|  
|ReplicationSourceDC <string>|도메인 정보를 복제 하는 파트너 도메인 컨트롤러의 FQDN 나타냅니다. 기본 계산 자동으로 됩니다.|  
|**SafeModeAdministratorPassword <securestring>**|디렉터리 서비스 복원 모드와 같은 안전 모드 유형의 또는 안전 모드에서 컴퓨터를 시작할 때 관리자 계정에 대 한 암호를 제공 합니다.<br /><br />기본값은 암호가 합니다. 암호를 입력 해야 합니다. 암호 읽기 호스트 assecurestring 또는 ConvertTo SecureString에서 제공 하는 System.Security.SecureString 형식으로 제공 합니다.<br /><br />SafeModeAdministratorPassword 인수 작업은 특수: 인수도 지정 되지 않은 경우, cmdlet 입력 하 고 마스크 암호를 확인 하 라는 메시지가 표시 됩니다. 기본 설정된 사용 cmdlet 대화식으로 실행 될 때입니다. 값, 없이 지정 cmdlet에 지정 된 다른 인수 cmdlet 확인 없이 마스크 암호를 입력 하 라는 메시지가 표시 되 합니다. Cmdlet 대화식으로 실행 될 때 기본 설정된 사용 아닙니다. 값으로 지정 값 보안 문자열 있어야 합니다. Cmdlet 대화식으로 실행 될 때 기본 설정된 사용 아닙니다. 예를 들어, 요청할 수 있습니다 수동으로 암호를 읽기 호스트 cmdlet 사용자에 게 보안 문자열 증명을 사용 하 여:-safemodeadministratorpassword (읽기 호스트-프롬프트 "암호:"-assecurestring) 제공할 수도 있습니다 보안 문자열 변환 일반 텍스트 변수와,이 좋습니다. -safemodeadministratorpassword (convertto securestring "password1 갖고 있어" asplaintext-강제로)|  
|**SiteName <string>**<br /><br />추가 addsreadonlydomaincontrolleraccount cmdlet에 대 한 필요합니다.|도메인 컨트롤러를 설치할 위치를 지정 합니다. 없이 **"sitename** 인수 실행할 때 **설치 ADDSForest** 만든 첫 번째 사이트는 첫 번째 사이트 이름 기본 합니다.<br /><br />인수로 제공 된 경우에 이미 사이트 이름이 있어야 **-sitename**합니다. Cmdlet 사이트를 만들지 됩니다.|  
|SkipAutoConfigureDNS|DNS 클라이언트 설정, 전달자 및 루트 힌트 자동으로 구성을 건너뜁니다. DNS 서버 서비스가 이미 설치 되었거나 함께 자동으로 설치 하는 경우이 인수에만 적용 됩니다 **-InstallDNS**합니다.|  
|SystemKey <string>|데이터를 복제 하는 미디어에 대 한 시스템 키를 지정 합니다.<br /><br />기본값은 **없음**합니다.<br /><br />데이터 형식 읽기 호스트 assecurestring 또는 ConvertTo SecureString 제공한에 있어야 합니다.|  
|SysvolPath <string>|예를 들어, 로컬 컴퓨터의 고정 된 디스크에 정식된, 비 UNC 경로 디렉터리를 지정 **C:\Windows\SYSVOL**합니다.<br /><br />기본값은 **%SYSTEMROOT%\SYSVOL**합니다. **중요:** SYSVOL (ReFS) 복원 파일 시스템으로 포맷 데이터 양에 저장할 수 없습니다.|  
|SkipPreChecks|설치를 시작 하기 전에 필수 검사를 실행 하지 않습니다. 이 설정을 사용 하는 것은 아닙니다.|  
|WhatIf|Cmdlet 자동으로 실행 하는 경우 표시 됩니다. Cmdlet 실행 되지 않습니다.|  
  
### <a name="BKMK_PSCreds"></a>Windows PowerShell 자격 증명 지정  
You can specify credentials without revealing them in plain text on screen by using [Get-credential](https://technet.microsoft.com/library/dd315327.aspx).  
  
특별 한-SafeModeAdministratorPassword 및 LocalAdministratorPassword 인수가 작업은 다음과 같습니다.  
  
-   인수도 지정 되지 않은 경우 cmdlet 입력 하 고 마스크 암호를 확인 하 라는 메시지가 표시 됩니다. 기본 설정된 사용 cmdlet 대화식으로 실행 될 때입니다.  
  
-   값으로 지정 값 보안 문자열 있어야 합니다. Cmdlet 대화식으로 실행 될 때 기본 설정된 사용 아닙니다.  
  
예를 들어, 요청할 수 있습니다 수동으로 암호를 사용 하 여는 **읽기 호스트** cmdlet에 대 한 보안 문자열 묻는  
  
```  
-SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString)
```  
  
> [!WARNING]  
> 이전 옵션 암호를 확인 하지 않는 주의 사용 하 여: 암호가 표시 되지 않습니다.  
  
또한이 것이 좋음 있지만 변환 일반 텍스트 변수와 보안 문자열을 제공할 수 있습니다.  
  
```  
-SafeModeAdministratorPassword (ConvertTo-SecureString "Password1" -AsPlainText -Force)
```  
  
> [!WARNING]  
> 하지 암호화 되지 않은 텍스트 암호를 저장 하거나 제공 하는 것이 좋습니다. 스크립트가이 명령을 실행 또는이 기사를 통해 모든 사용자 해당 도메인 컨트롤러의 DSRM 암호를 알고 있습니다. 해당 정보를 도메인 컨트롤러 자체 가장 하 고 자녀가 상승 Active Directory 숲에서 가장 높은 수준의에 수 있습니다.  
  
### <a name="BKMK_TestCmdlets"></a>테스트 cmdlet 사용 하 여  
각 ADDSDeployment cmdlet에는 해당 cmdlet 테스트 합니다. 테스트 cmdlet 실행 필수 검사만 설치 작동 합니다. 설치 설정이 없는 구성 됩니다. 각 테스트 cmdlet에 대 한 인수 해당 설치 cmdlet와 동일 하지만 **"SkipPreChecks** 를 테스트 cmdlet에 대 한 사용할 수 없습니다.  
  
|테스트 cmdlet|설명|  
|---------------|---------------|  
|테스트 ADDSForestInstallation|새 Active Directory 숲 설치 하기 위한 필수 실행 됩니다.|  
|테스트 ADDSDomainInstallation|새 도메인 Active Directory에 설치 하기 위한 필수 실행 됩니다.|  
|테스트 ADDSDomainControllerInstallation|도메인 컨트롤러 Active Directory에 설치 하기 위한 필수 실행 됩니다.|  
|테스트 ADDSReadOnlyDomainControllerAccountCreation|(RODC) 계정 읽기 전용 도메인 컨트롤러를 추가 하기 위한 필수 실행 됩니다.|  
  
### <a name="BKMK_PSForest"></a>새 숲 루트 도메인 Windows PowerShell를 사용 하 여 설치  
새 숲 설치 하기 위한 명령 구문을 다음과 같습니다. (옵션) 인수 대괄호 내에 나타납니다.  
  
```  
Install-ADDSForest [-SkipPreChecks] -DomainName <string> -SafeModeAdministratorPassword <SecureString> [-CreateDNSDelegation] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-DomainNetBIOSName <string>] [-ForestMode <ForestMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-InstallDNS] [-LogPath <string>] [-NoRebootOnCompletion] [-SkipAutoConfigureDNS] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
> [!NOTE]  
> DNS 도메인 이름 접두사에 따라 자동으로 생성 되는 15 자의 이름 변경 하려는 경우 또는 이름을 초과 15 자 하는 경우-DomainNetBIOSName 인수가 필요 합니다.  
  
예를 들어,를 설치 하 라는 corp.contoso.com 새 숲 고 안전 하 게 DSRM 암호를 입력 하 라는 메시지가 표시 될 입력 다음과 같습니다.  
  
```  
Install-ADDSForest -DomainName "corp.contoso.com"   
```  
  
> [!NOTE]  
> DNS 서버가 설치 ADDSForest 실행 될 때 기본적으로 설치 됩니다.  
  
디렉터리 서비스 복원 모드 암호 및 형식을 입력 하 라는 메시지가 corp.contoso.com 라는 새 숲 설치, DNS 위임 contoso.com 도메인에 있는 Windows Server 2008 R2 도메인 기능 수준을 설정 및 Windows Server 2008 숲 기능 수준을 설정, Active Directory 데이터베이스와 SYSVOL D:\ 드라이브에 설치, 로그 E:\ 드라이브에 파일을 설치 만들고 수 :  
  
```  
Install-ADDSForest -DomainName corp.contoso.com -CreateDNSDelegation -DomainMode Win2008 -ForestMode Win2008R2 -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  
  
### <a name="BKMK_PSDomain"></a>Windows PowerShell를 사용 하 여 새 자녀 또는 밤나무 도메인 설치  
새 도메인 설치 하기 위한 명령 구문을 다음과 같습니다. (옵션) 인수 대괄호 내에 나타납니다.  
  
```  
Install-ADDSDomain [-SkipPreChecks] -NewDomainName <string> -ParentDomainName <string> -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainReinstall] [-CreateDNSDelegation] [-Credential <PS Credential>] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [DomainType <DomainType> {Child Domain | TreeDomain} [-InstallDNS] [-LogPath <string>] [-NoGlobalCatalog] [-NewDomainNetBIOSName <string>] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-Systemkey <SecureString>] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
> [!NOTE]  
> **-자격 증명** 인수는만 하면 하지에 현재 로그온 Enterprise 관리자 그룹의 회원으로 경우 필요 합니다.  
>   
> **-NewDomainNetBIOSName** DNS 도메인 이름 접두사에 따라 자동으로 생성 된 15 자의 이름 변경 하려는 경우 또는 이름을 초과 15 자 하는 경우의 인수가 필요 합니다.  
  
예를 들어, child.corp.contoso.com 라는 새로운 자녀 도메인을 만드는 데 corp\EnterpriseAdmin1의 자격 증명을 사용 하려면 설치 DNS 서버, corp.contoso.com 도메인 DNS 위임 만들, Windows Server 2003로 도메인 기능 수준을 설정, 휴스턴 라고 하는 사이트에 도메인 컨트롤러 드 서버를 확인, DC1.corp.contoso.com 복제 원본 도메인 컨트롤러를 사용 하 여, Active Directory 데이터베이스와 SYSVOL D:\ 드라이브에 설치 E:\ 드라이브에 로그 파일을 설치 하 고 디렉터리 서비스 복원 모드 암호를 제공 하 고 입력 하 고 명령을 것인지 묻는 메시지가 나타나지 하 라는 메시지가 표시 됩니다.  
  
```  
Install-ADDSDomain -SafeModeAdministratorPassword -Credential (get-credential corp\EnterpriseAdmin1) -NewDomainName child -ParentDomainName corp.contoso.com -InstallDNS -CreateDNSDelegation -DomainMode Win2003 -ReplicationSourceDC DC1.corp.contoso.com -SiteName Houston -DatabasePath "d:\NTDS" "SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs" -Confirm:$False  
```  
  
### <a name="BKMK_PSReplica"></a>추가 (복제본) 도메인 컨트롤러 Windows PowerShell를 사용 하 여 설치  
추가 도메인 컨트롤러를 설치 하기 위한 명령 구문을 다음과 같습니다. (옵션) 인수 대괄호 내에 나타납니다.  
  
```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainControllerReinstall] [-ApplicationPartitionsToReplicate <string[]>] [-CreateDNSDelegation] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-NoGlobalCatalog] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
Corp.contoso.com 도메인에 있는 도메인 컨트롤러 및 DNS 서버를 설치 하 고 DSRM 암호를 입력 하 고 도메인 관리자 자격 증명을 입력 하 라는 메시지가:  
  
```  
Install-ADDSDomainController -Credential (Get-Credential CORP\Administrator) -DomainName "corp.contoso.com"
```  
  
컴퓨터가 이미 도메인 가입 하 고 도메인 관리자 그룹의 회원은을 사용할 수 있습니다.  
  
```  
Install-ADDSDomainController -DomainName "corp.contoso.com"  
```  
  
도메인 이름에 대 한 메시지가 표시 되도록 하려면 다음을 입력 합니다.  
  
```  
Install-ADDSDomainController -Credential (Get-Credential) -DomainName (Read-Host "Domain to promote into")
```  
  
다음 명령을를 사용 하 여 Contoso\EnterpriseAdmin1의 자격 증명 쓸 수 있는 도메인 컨트롤러 및 드 서버 보스턴 라고 하는 사이트의 설치, DNS 서버를 설치, DNS 위임 contoso.com 도메인 만들, c:\ADDS IFM 폴더에 저장 된 미디어에서 설치, Active Directory 데이터베이스와 SYSVOL D:\ 드라이브에 설치 로그 E:\ 드라이브에 파일을 설치 있는 서버 자동으로 다시 시작 광고 DS 설치를 완료 되 고 디렉터리 서비스 복원 모드 암호를 입력 하 라는 메시지가 표시 됩니다.  
  
```  
Install-ADDSDomainController -Credential (Get-Credential CONTOSO\EnterpriseAdmin1) -CreateDNSDelegation -DomainName corp.contoso.com -SiteName Boston -InstallationMediaPath "c:\ADDS IFM" -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  
  
### <a name="performing-a-staged-rodc-installation-using-windows-powershell"></a>Windows PowerShell 사용 준비 된 RODC 설치  
RODC 계정을 만드는 데 명령 구문을 다음과 같습니다. (옵션) 인수 대괄호 내에 나타납니다.  
  
```  
Add-ADDSReadOnlyDomainControllerAccount [-SkipPreChecks] -DomainControllerAccuntName <string> -DomainName <string> -SiteName <string> [-AllowPasswordReplicationAccountName <string []>] [-NoGlobalCatalog] [-Credential <PS Credential>] [-DelegatedAdministratorAccountName <string>] [-DenyPasswordReplicationAccountName <string []>] [-InstallDNS] [-ReplicationSourceDC <string>] [-Force] [-WhatIf] [-Confirm] [<Common Parameters>]  
```  
  
서버 RODC 계정에 연결 하는 명령 구문을 다음과 같습니다. (옵션) 인수 대괄호 내에 나타납니다.  
  
```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-ApplicationPartitionsToReplicate <string[]>] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-NoDNSOnNetwork] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-UseExistingAccount] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
예를 들어, RODC 계정을 만드는 데 RODC1 라는:  
  
```  
Add-ADDSReadOnlyDomainControllerAccount -DomainControllerAccountName RODC1 -DomainName corp.contoso.com -SiteName Boston DelegatedAdministratoraccountName PilarA  
```  
  
다음 RODC1 계정에 연결할 수 있는 서버의 뒤 다음 명령을 실행 합니다. 서버는 도메인에 가입 수 없습니다. 먼저 AD DS 서버 역할 및 관리 도구를 설치 합니다.  
  
```  
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```  
  
RODC 만드는 다음 명령 실행 합니다.  
  
```  
Install-ADDSDomainController -DomainName corp.contoso.com -SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString) -Credential (Get-Credential Corp\PilarA) -UseExistingAccount
```  
  
키를 눌러 **Y** 여부를 확인 하거나 포함는 **"확인** 인수 확인 메시지를 방지 합니다.  
  
## <a name="BKMK_GUI"></a>광고 DS 서버 관리자를 사용 하 여 설치  
AD DS 역할 추가 마법사 Active Directory 도메인 서비스 구성 마법사, Windows Server 2012에 새로운 시작 되는 이어서 서버 관리자에서 사용 하 여 Windows Server 2012에 설치할 수 있습니다. Active Directory 도메인 Services 설치 마법사 (dcpromo.exe)는 일부 터 Windows Server 2012에서 사용 되지 않습니다.  
  
다음 섹션을 설치 하 고 여러 서버의 AD DS 관리할 수 있도록 서버 풀 만드는 방법 및 광고 DS 설치 마법사를 사용 하는 방법을 설명 합니다.  
  
### <a name="BKMK_ServerPools"></a>서버 풀 만들기  
서버 관리자 서버 관리자 실행 하는 컴퓨터에서 액세스할 수 있는 되는 네트워크에서 다른 서버 풀 수 있습니다. 풀 되 면 원격 설치 AD DS 또는 가능한 내에서 서버 관리자 다른 구성 옵션에 대 한 이러한 서버 선택 합니다. 서버 관리자 자동으로 실행 하는 컴퓨터 풀 자체 합니다. For more information about server pools, see [Add Servers to Server Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
> [!NOTE]  
> 작업 그룹 서버 또는 반대의 서버 관리자를 사용 하는 도메인에 가입 컴퓨터를 관리 하기 위해 추가 구성 단계가 필요 합니다. For more information, see "Add and manage servers in workgroups" in [Add Servers to Server Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
### <a name="BKMK_installADDSGUI"></a>광고 DS 설치  
**관리자 자격 증명**  
  
광고 DS 설치 하기 위한 자격 증명 요구 사항을 선택 하는 배포 구성에 따라 다릅니다. 자세한 내용은 참조 [Adprep.exe 실행 하 고 Active Directory 도메인 서비스 설치 요구 사항이 자격 증명](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)합니다.  
  
다음 절차를 사용 하 여 광고 DS GUI 방법을 사용 하 여 설치 합니다. 로컬에서 또는 원격 단계를 수행할 수 있습니다. 이러한 단계 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [숲 서버 관리자와 함께 배포](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [복제 Windows Server 2012 도메인 컨트롤러에 기존 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  
  
-   [새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
  
-   [Windows Server 2012 Active Directory 읽기 전용 도메인 컨트롤러 & #40; 설치 RODC & #41; & #40; 200 수준 & #41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md)  
  
##### <a name="to-install-ad-ds-by-using-server-manager"></a>광고 DS 서버 관리자를 사용 하 여 설치  
  
1.  서버 관리자 클릭 **관리** 클릭 **역할 추가 및 기능** 역할 추가 마법사를 시작 합니다.  
  
2.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.  
  
3.  에 **설치 유형을 선택** 페이지, 클릭 **역할 또는 기능 기반 설치** 차례로 클릭 하 고 **다음**합니다.  
  
4.  에 **선택 대상 서버** 페이지, 클릭 **서버 풀에서 서버를 선택**, 광고 DS 설치를 클릭 한 다음 원하는 서버의 이름을 클릭 **다음**합니다.  
  
    원격 서버를 선택 하려면 서버 풀 만들기 및 원격 서버를 추가 합니다. For more information about creating server pools, see [Add Servers to Server Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
5.  에 **서버 역할을 선택** 페이지, 클릭 **Active Directory 도메인 서비스**에 다음의 **역할 추가 및 기능 마법사** 대화 상자에서 클릭 **기능 추가**, 클릭 한 다음 **다음**합니다.  
  
6.  에 **기능 선택** 페이지에서 설치를 클릭 모든 추가 기능을 선택 **다음**합니다.  
  
7.  에 **Active Directory 도메인 서비스** 페이지, 정보를 검토 한 다음 클릭 **다음**합니다.  
  
8.  에 **설치 선택을 확인** 페이지, 클릭 **설치**합니다.  
  
9. 에 **결과** 페이지에서 있는지 설치 되었는지 확인 한 클릭 **도메인 컨트롤러이 서버 홍보** Active Directory 도메인 서비스 구성 마법사를 시작 합니다.  
  
    ![광고 DS 설치](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_SMPromotes.gif)  
  
    > [!IMPORTANT]  
    > Active Directory 도메인 서비스 구성 마법사를 시작 하지 않고 역할 추가 마법사 이제 닫으면 서버 관리자의 작업을 클릭 하 여 다시 시작할 수 있습니다.  
  
    ![광고 DS 설치](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  
  
10. 에 **배포 구성** 페이지에서 다음 옵션 중 하나를 선택 합니다.  
  
    -   기존 도메인에 추가 도메인 컨트롤러를 설치 하는 경우 클릭 **도메인 컨트롤러 기존 도메인에 추가**하세요 (예를 들어 emea.corp.contoso.com)는 도메인의 이름을 입력 하거나 클릭 하 고 **선택... ** , 도메인 및 자격 증명을 선택할 수 (예를 들어 지정 도메인 관리자 그룹 구성원 계정을) 차례로 클릭 하 고 **다음**합니다.  
  
        > [!NOTE]  
        > 도메인 현재 사용자 자격의 이름과 컴퓨터가 도메인에 가입 하 고 로컬 설치 하는 경우에 기본적으로 제공 됩니다. AD DS 원격 서버를 설치 하는 경우 자격 증명을 디자인 하 여 지정 해야 합니다. 현재 사용자 자격 증명을 수행 하 여 설치 하는 데 충분 없는 경우 클릭 **변경... ** 다른 자격 증명을 지정할 수 있도록 합니다.  
  
        자세한 내용은 참조 [복제 Windows Server 2012 도메인 컨트롤러에 기존 도메인 & #40; 설치 200 수준 & #41; ](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
    -   새 자녀 도메인을 설치 하는 경우 클릭 **새 도메인 기존 숲에 추가**에 대 한 **도메인 유형을 선택**선택 **자녀 도메인**, 입력 하거나 부모 도메인 DNS 이름 (예: corp.contoso.com)의 이름을 검색, 새 자녀 도메인의 (예: emea), 타이핑 자격 증명을 사용 하 여 새 도메인 만들고 클릭 한 다음 상대 이름을 입력 **다음**합니다.  
  
        자세한 내용은 참조 [새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 & #40; 설치 200 수준 & #41; ](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
    -   도메인 트리를 새로 설치 하는 경우 클릭 **기존 숲에 추가 새 도메인**에 대 한 **도메인 유형을 선택**, 선택 **밤나무 도메인**루트 도메인 (예: corp.contoso.com)의 이름을 입력, 입력 자격 증명을 사용 하 여 새 도메인 만들고 클릭 한 다음 새 도메인 (예를 들어, fabrikam.com)의 DNS 이름을 입력 합니다 **다음**합니다.  
  
        자세한 내용은 참조 [새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 & #40; 설치 200 수준 & #41; ](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
    -   새 숲 설치 하는 경우 클릭 **새 숲 추가** 루트 도메인 (예: corp.contoso.com)의 이름을 입력 합니다.  
  
        자세한 내용은 참조 [는 새로운 Windows Server 2012 Active Directory 숲 & #40; 설치 200 수준 & #41; ](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
11. 에 **도메인 컨트롤러 옵션** 페이지에서 다음 옵션 중 하나를 선택 합니다.  
  
    -   새 숲 또는 도메인을 만드는 경우 도메인 및 숲 기능 수준을 클릭 **시스템 DNS (도메인 이름) 서버**DSRM 암호를 지정 하 고 클릭 한 다음 **다음**합니다.  
  
    -   기존 도메인 도메인 컨트롤러를 추가 하는 경우 클릭 **시스템 DNS (도메인 이름) 서버**, **글로벌 카탈로그 GC ()**, 또는 **읽기만 도메인 컨트롤러 (RODC)** 필요에 따라 사이트 이름을 선택 하 고 DSRM 암호를 입력 한 다음 **다음**합니다.  
  
    자세한 내용은 대 한이 페이지에 또는 옵션을 사용할 수 있는 다양 한 상황에서 사용할 수 없는 [도메인 컨트롤러 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)합니다.  
  
12. 에 **DNS 옵션** (나타나는 DNS 서버를 설치 하는 경우에) 페이지, 클릭 **업데이트 DNS 위임** 필요에 따라 합니다. 이렇게 하면 위임 DNS 레코드 부모 DNS 영역에 만들 수 있는 권한이 자격 증명을 제공 합니다.  
  
    부모 영역 호스트 하는 DNS 서버에 연결할 수 없는 경우는 **업데이트 DNS 위임** 옵션을 사용할 수 없습니다.  
  
    For more information about whether you need to update the DNS delegation, see [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx). 오류가 발생할를 확인 하 고 DNS 위임 업데이트 하려고 하면 [DNS 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)합니다.  
  
13. 에 **RODC 옵션** (에 표시 되는 RODC 설치 하는 경우에) 페이지에서 그룹이 나 RODC 관리를 허용 또는 거부 암호 복제 그룹에서 계정을 제거 하거나 및 클릭 한 다음에 계정을 추가 하는 사용자의 이름을 지정 **다음**합니다.  
  
    For more information, see [Password Replication Policy](https://technet.microsoft.com/library/cc730883(v=ws.10)).  
  
14. 에 **추가 옵션** 페이지에서 다음 옵션 중 하나를 선택 합니다.  
  
    -   새 도메인 만드는 경우 새 NetBIOS 이름을 입력 하거나는 도메인의 기본 NetBIOS 이름을 확인 하 고 클릭 한 다음 **다음**합니다.  
  
    -   기존 도메인 도메인 컨트롤러를 추가 하는 경우 복제 AD DS 설치에서 데이터 (또는 모든 도메인 컨트롤러를 선택 하 고 마법사 허용)를 하는 도메인 컨트롤러를 선택 합니다. 미디어에서 설치 하는 경우 클릭 **미디어 경로에서 설치** 입력 하 고 설치 원본 파일에 대 한 경로 확인 하 고, 클릭 한 다음 **다음**합니다.  
  
        사용할 수 없습니다 (IFM)는 도메인의 첫 번째 도메인 컨트롤러 설치 미디어를 설치 합니다. IFM 다른 운영 체제 버전에서 작동 하지 않습니다. 즉, IFM를 사용 하 여 Windows Server 2012를 실행 하는 추가 도메인 컨트롤러를 설치 하려면 만들어야 백업 미디어 Windows Server 2012 도메인 컨트롤러에서 합니다. For more information about IFM, see [Installing an Additional Domain Controller by Using IFM](https://technet.microsoft.com/library/cc816722(WS.10).aspx).  
  
15. 에 **경로** 페이지, Active Directory 데이터베이스, 로그 파일과 SYSVOL 폴더의 위치를 입력 (또는 기본 위치에 동의)을 클릭 하 고 **다음**합니다.  
  
    > [!IMPORTANT]  
    > (ReFS) 복원 파일 시스템으로 포맷 데이터 볼륨 Active Directory 데이터베이스, 로그 파일 또는 폴더 SYSVOL 저장 하지 않습니다.  
  
16. 에 **준비 옵션** 페이지 입력 자격 증명을 adprep 실행 하는 데 충분 합니다. 자세한 내용은 참조 [Adprep.exe 실행 하 고 Active Directory 도메인 서비스 설치 요구 사항이 자격 증명](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)합니다.  
  
17. 에 **리뷰 옵션** 페이지 선택 사항을 확인을 클릭 **스크립트 보기** 설정을를 Windows PowerShell 스크립트 내보내고 클릭 한 다음 원하는 경우 **다음**합니다.  
  
18. 에 **필수 확인** 페이지 완료 되 면 해당 필수 유효성 검사를 확인 하 고 클릭 한 다음 **설치**합니다.  
  
19. 에 **결과** 페이지에서 서버 성공적으로 도메인 컨트롤러도 구성 되어 있는지 확인 합니다. 서버 AD DS 설치를 완료 하려면 자동으로 다시 시작 됩니다.  
  
## <a name="BKMK_UIStaged"></a>RODC 설치 준비 그래픽 사용자 인터페이스를 사용 하 여 수행  
준비 된 RODC 설치 두 단계로 RODC 만들 수 있습니다. 첫 번째 단계 도메인 관리자 그룹의 회원 RODC 계정을 만듭니다. 2 단계 서버 RODC 계정에 연결 되어 있습니다. 도메인 관리자 그룹 또는 위임된 도메인 사용자 또는 그룹의 회원 한 2 단계를 수행할 수 있습니다.  
  
#### <a name="to-create-an-rodc-account-by-using-the-active-directory-management-tools"></a>Active Directory 관리 도구를 사용 하 여 RODC 계정 만들기  
  
1.  Active Directory 관리 센터 또는 Active Directory 사용자와 컴퓨터를 사용 하 여 RODC 계정을 만들 수 있습니다.  
  
    1.  클릭 **시작**, 클릭 **관리 도구**을 차례로 클릭 하 고 **Active Directory 관리 센터**합니다.  
  
    2.  탐색 창 (왼쪽된 창)의 도메인의 이름을 클릭 합니다.  
  
    3.  관리 목록 (가운데 창)를 클릭 하 고 **도메인 컨트롤러** OU 합니다.  
  
    4.  (오른쪽 창) 작업 창 클릭 **읽기 전용 도메인 컨트롤러 계정 만들기 미리**합니다.  
  
    또는  
  
    1.  클릭 **시작**, 클릭 **관리 도구**을 차례로 클릭 하 고 **Active Directory 사용자와 컴퓨터**합니다.  
  
    2.  하거나 마우스 오른쪽 단추로 클릭은 **도메인 컨트롤러** 조직 단위 하거나 클릭은 **도메인 컨트롤러** OU을 차례로 클릭 하 고 **알림**합니다.  
  
    3.  클릭 **미리 읽기 전용 도메인 컨트롤러 계정 만들기**합니다.  
  
2.  에 **Active Directory 도메인 Services 설치 마법사를 시작** 수정 기본은 복제 정책 PRP (암호)를 선택 하 고 싶은 경우 페이지 **사용 고급 모드 설치**를 차례로 클릭 하 고 **다음**합니다.  
  
3.  에 **네트워크 자격 증명** 페이지의 **설치를 사용 하 여 계정 자격 증명을 지정**, 클릭 **자격 증명에 현재 로그온 한** 키를 누르거나 **대체 자격**, 클릭 한 다음 **설정**합니다. 에 **Windows 보안** 대화 상자에 추가 도메인 컨트롤러를 설치할 수 있는 계정에 대 한 사용자 이름 및 암호를 제공 합니다. 추가 도메인 컨트롤러를 설치 하려면 관리자 Enterprise 그룹 또는 도메인 관리자 그룹의 회원 이어야 합니다. 자격 증명을 제공가 완료 되 면 클릭 **다음**합니다.  
  
4.  에 **컴퓨터 이름 지정** 페이지 RODC 수 있는 서버의 컴퓨터 이름을 입력 합니다.  
  
5.  에 **사이트 선택** 페이지를 목록에서 사이트를 선택 하거나 도메인 컨트롤러 마법사를 실행 하는 컴퓨터의 IP 주소에 해당 하는 사이트의 설치 옵션을 선택 하 고 클릭 한 다음 **다음**합니다.  
  
6.  에 **추가 도메인 컨트롤러 옵션** 페이지 다음과 같은 옵션을 선택 하 고 클릭 한 다음 **다음**:  
  
    -   **DNS 서버**: 도메인 컨트롤러 역할 시스템 DNS (도메인 이름) 서버를 할 수 있도록 기본적으로이 옵션을 선택 합니다. DNS 서버를 도메인 컨트롤러 하지 않으려면이 옵션을 선택 취소 합니다. 그러나 설치 하지 않는 DNS 서버 역할 RODC 및에 지점에만 도메인 컨트롤러, 지점에 사용자는 다양 한 영역 (네트워크) hub 사이트에 오프 라인 상태일 때 이름을 확인을 수행 수 없습니다.  
  
    -   **드**: 기본적으로이 옵션을 선택 합니다. 드 읽기 전용 파티션 도메인 컨트롤러에 추가 하 고 드 검색 기능을 사용 합니다. 도메인 컨트롤러 서버 드 하지 않으려면이 옵션을 선택 취소 합니다. 그러나 지사에서 드 서버를 설치 하지 않거나 유니버설 그룹 구성원 RODC 포함 된 사이트에 대 한 캐시를 사용 하는 경우 사용자는 지점에 허브 사이트 WAN 오프 라인 상태일 때 도메인에 로그인 할 수 되지 않습니다.  
  
    -   **읽기 전용 도메인 컨트롤러**합니다. RODC 계정을 만들 때이 옵션은 기본적으로 선택 하 고 지울 수는 없습니다.  
  
7.  선택한 경우는 **사용 고급 모드 설치** 확인란을는 **시작** 페이지의 **암호 복제 정책 지정** 페이지가 나타납니다. 기본적으로 계정 암호 없이 RODC에 복제 및 중요 한 보안 계정 (예: 도메인 관리자 그룹의 회원)의 개가 RODC 복제 암호만 거부 명시적으로 합니다.  
  
    정책에 다른 계정 추가를 클릭 **추가**, 클릭 한 다음 **이 RODC 복제 계정에 대 한 암호를 허용** 키를 누르거나 **계정에 대 한 암호에이 RODC 복제 거부** 및 계정을 선택 합니다.  
  
    완료 되 면 (또는 기본 설정을 적용 하려면)를 클릭 **다음**합니다.  
  
8.  에 **RODC 위임 설치 및 관리** 페이지에서 사용자 또는 서버 작성 중인 RODC 계정에 연결 하는 그룹의 이름을 입력 합니다. 하나의 보안 사용자의 이름을 입력할 수 있습니다.  
  
    특정 사용자 또는 그룹에 대 한 디렉터리를 검색 하려면 클릭 **설정**합니다. **사용자 또는 그룹 선택**그룹 또는 사용자의 이름을 입력 합니다. RODC 설치 및 그룹으로 관리에 위임 하는 것이 좋습니다.  
  
    사용자 또는 그룹이 또한는 로컬 관리자 권한 RODC에 설치 후 수 있습니다. 사용자 또는 그룹을 지정 하지 않으면 도메인 관리자 하나 또는 여러 개의 엔터프라이즈 관리자 그룹의 회원만 서버 계정에 연결할 수 없게 됩니다.  
  
    완료 되 면 클릭 **다음**합니다.  
  
9. 에 **요약** 페이지를 검토 하 여 선택 합니다. 클릭 **다시** 필요한 경우 어떤 선택 변경할 수 있습니다.  
  
    선택한 설정을 자동화 이후 AD DS 작업 하 고 클릭 사용할 수 있는 응답 파일에 저장 하려면 **내보내려면 설정**합니다. 응답 파일 이름을 입력 한 다음 **저장**합니다.  
  
    선택한 항목은 정확 하 게 클릭 **다음** RODC 계정을 만들 수 있습니다.  
  
10. 에 **Active Directory 도메인 Services 설치 마법사를 완료** 페이지, 클릭 **완료**합니다.  
  
RODC 계정을 만든 후 서버 RODC 설치를 완료 하는 계정에 첨부할 수 있습니다. 이 2 단계 RODC 찾을 수는 지점에 완료할 수 있습니다. 이 절차를 수행 하는 서버 도메인에 가입 하지 있어야 합니다. Windows Server 2012에서 부터는 역할 추가 마법사에서 서버 관리자를 사용 하면 서버 RODC 계정에 연결 합니다.  
  
#### <a name="to-attach-a-server-to-an-rodc-account-using-server-manager"></a>서버 RODC 서버 관리자를 사용 하 여 계정에 연결 하려면  
  
1.  로컬 관리자 권한으로 로그온 합니다.  
  
2.  서버 관리자 클릭 **역할 및 기능을 추가**합니다.  
  
3.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.  
  
4.  에 **설치 유형을 선택** 페이지, 클릭 **역할 또는 기능 기반 설치** 차례로 클릭 하 고 **다음**합니다.  
  
5.  에 **선택 대상 서버** 페이지, 클릭 **서버 풀에서 서버를 선택**, 광고 DS 설치를 클릭 한 다음 원하는 서버의 이름을 클릭 **다음**합니다.  
  
6.  에 **서버 역할 선택** 페이지, 클릭 **Active Directory 도메인 서비스**, 클릭 **기능 추가** 차례로 클릭 하 고 **다음**합니다.  
  
7.  에 **기능 선택** 페이지에서 설치를 클릭 하 고 있는 모든 추가 기능을 선택 **다음**합니다.  
  
8.  에 **Active Directory 도메인 서비스** 페이지, 정보를 검토 한 다음 클릭 **다음**합니다.  
  
9. 에 **설치 선택을 확인** 페이지, 클릭 **설치**합니다.  
  
10. 에 **결과** 페이지에서 확인할 **성공 설치**를 클릭 하 고 **도메인 컨트롤러이 서버 홍보** Active Directory 도메인 서비스 구성 마법사를 시작 합니다.  
  
    > [!IMPORTANT]  
    > Active Directory 도메인 서비스 구성 마법사를 시작 하지 않고 역할 추가 마법사 이제 닫으면 서버 관리자의 작업을 클릭 하 여 다시 시작할 수 있습니다.  
  
    (media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  
  
11. 에 **배포 구성** 페이지, 클릭 **도메인 컨트롤러 기존 도메인에 추가**도메인 (예를 들어 emea.contoso.com)의 이름을 입력 하 고 자격 증명 (예를 들어 지정 관리 하 고 설치 RODC 위임 하는 계정)를 클릭 한 다음 **다음**합니다.  
  
12. 에 **도메인 컨트롤러 옵션** 페이지, 클릭 **기존 RODC 계정을 사용 하 여**, 입력 및 디렉터리 서비스 복원 모드 암호를 확인 한 다음 **다음**합니다.  
  
13. 에 **추가 옵션** 미디어를 설치 하는 경우 페이지 클릭 **미디어 경로에서 설치** 입력 하 고 원본 설치 파일을 경로 확인, 복제 AD DS 설치에서 데이터 (또는 모든 도메인 컨트롤러를 선택 하 고 마법사 허용)를 하는 도메인 컨트롤러를 선택 차례로 클릭 하 고 **다음**합니다.  
  
14. 에 **경로** 페이지, Active Directory 데이터베이스, 로그 파일과 SYSVOL 폴더의 위치를 입력 하거나 기본 위치 적용 및 클릭 한 다음 **다음**합니다.  
  
15. 에 **리뷰 옵션** 페이지 선택 사항을 확인을 클릭 **스크립트 보기** 설정을를 Windows PowerShell 스크립트 내보내고 클릭 한 다음 **다음**합니다.  
  
16. 에 **필수 확인** 페이지 완료 되 면 해당 필수 유효성 검사를 확인 하 고 클릭 한 다음 **설치**합니다.  
  
    AD DS 설치를 완료 하려면 서버는 자동으로 다시 시작 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[도메인 컨트롤러 배포 문제 해결](Troubleshooting-Domain-Controller-Deployment.md)  
[새로운 Windows Server 2012 Active Directory 숲 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)  
[새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
[복제 Windows Server 2012 도메인 컨트롤러에 기존 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  
  



