---
ms.assetid: ae241ed8-ef19-40a9-b2d5-80b8391551ff
title: Active Directory 도메인 서비스 설치(수준 100)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5934e4a709ab00048168cb30976aab06fd5c5374
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825246"
---
# <a name="install-active-directory-domain-services-level-100"></a>Active Directory 도메인 서비스 설치(수준 100)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 다음 방법 중 하나를 사용 하 여 Windows Server 2012의 AD DS를 설치 하는 방법에 설명 합니다.  

-   [Adprep.exe를 실행 하 고 Active Directory Domain Services를 설치 하기 위한 자격 증명 요구 사항](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)  

-   [Windows PowerShell을 사용 하 여 AD DS 설치](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PS)  

-   [서버 관리자를 사용 하 여 AD DS 설치](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_GUI)  

-   [그래픽 사용자 인터페이스를 사용 하 여 단계적 RODC 설치 수행](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_UIStaged)  

## <a name="credential-requirements-to-run-adprepexe-and-install-active-directory-domain-services"></a><a name="BKMK_Creds"></a>Adprep.exe를 실행 하 고 Active Directory Domain Services를 설치 하기 위한 자격 증명 요구 사항  
Adprep.exe를 실행하고 AD DS를 설치하려면 다음과 같은 자격 증명이 필요합니다.  

-   새 포리스트를 설치하려면 컴퓨터의 로컬 관리자로 로그온해야 합니다.  

-   새 자식 도메인이나 새 도메인 트리를 설치하려면 Enterprise Admins 그룹의 구성원으로 로그인해야 합니다.  

-   기존 도메인에서 추가 도메인 컨트롤러를 설치하려면 Domain Admins 그룹 구성원이어야 합니다.  

    > [!NOTE]  
    > Adprep.exe 명령을 별도로 실행 하지 않으면 기존 도메인 또는 포리스트에 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 설치 하는 경우 Adprep 명령을 실행 하는 자격 증명을 제공 해야 합니다. 자격 증명 요구 사항은 다음과 같습니다.  
    >   
    > -   포리스트의 첫 번째 Windows Server 2012 도메인 컨트롤러를 도입 Enterprise Admins 그룹, Schema Admins 그룹의 구성원에 대 한 자격 증명을 제공 해야 하 고 Domain Admins 그룹의 도메인에서 호스팅하는 스키마 마스터입니다.  
    > -   도메인의 첫 번째 Windows Server 2012 도메인 컨트롤러를 도입 하려면 Domain Admins 그룹의 구성원에 대 한 자격 증명을 제공 해야 합니다.  
    > -   포리스트에서 첫 번째 RODC(읽기 전용 도메인 컨트롤러)를 설치하려면 Enterprise Admins 그룹 구성원에 대한 자격 증명을 제공해야 합니다.  
    >   
    >     > [!NOTE]  
    >     > Windows Server 2008 또는 Windows Server 2008 r 2에서 이미 adprep /rodcprep을 실행 하는 경우 Windows Server 2012에 대 한 다시 실행할 필요가 없습니다.  

## <a name="installing-ad-ds-by-using-windows-powershell"></a><a name="BKMK_PS"></a>Windows PowerShell을 사용 하 여 AD DS 설치  
Windows Server 2012 부터는 Windows PowerShell을 사용 하 여 AD DS를 설치할 수 있습니다. Windows Server 2012 부터는 Dcpromo.exe가 사용 되지 않지만 응답 파일을 사용 하 여 dcpromo.exe를 실행할 수 있습니다 (dcpromo /unattend:<answerfile> 또는 dcpromo /answer:<answerfile>). 응답 파일을 통해 계속해서 dcpromo.exe를 실행하는 기능은 기존의 자동화에 리소스를 투자한 조직에게 자동화를 dcpromo.exe에서 Windows PowerShell로 변환할 수 있는 시간을 제공해 줍니다. 응답 파일을 사용 하 여 dcpromo.exe를 실행 하는 방법에 대 한 자세한 내용은 [https://support.microsoft.com/kb/947034](https://support.microsoft.com/kb/947034)를 참조 하세요.  

Windows PowerShell을 사용하여 AD DS를 제거하는 방법에 대한 자세한 내용은 [Windows PowerShell을 사용하여 AD DS 제거](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c#BKMK_RemovePS)를 참조하십시오.  

Windows PowerShell을 사용하여 역할을 추가하는 작업부터 시작합니다. 이 명령은 AD DS 서버 역할을 설치하고 Active Directory 사용자 및 컴퓨터와 같은 GUI 기반 도구와 dcdia.exe와 같은 명령줄 도구를 비롯하여 AD DS 및 AD LDS 서버 관리 도구를 설치합니다. Windows PowerShell을 사용할 경우에는 기본적으로 서버 관리 도구가 설치되지 않습니다. 지정 해야 **"IncludeManagementTools** 을 로컬 서버를 관리 하거나 설치 [원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=28972) 원격 서버를 관리 합니다.  

```  
Install-windowsfeature -name AD-Domain-Services -IncludeManagementTools  
<<Windows PowerShell cmdlet and arguments>>  
```  

AD DS 설치가 완료될 때까지 재부팅하지 않아도 됩니다.  

그런 다음 이 명령을 실행하여 ADDSDeployment 모듈에서 사용 가능한 cmdlet을 확인할 수 있습니다.  

```  
Get-Command -Module ADDSDeployment
```  

cmdlet 및 구문에 지정할 수 있는 인수 목록을 보려면  

```  
Get-Help <cmdlet name>  
```  

예를 들어 비어 있는 RODC(읽기 전용 도메인 컨트롤러) 계정을 만드는 인수를 보려면 다음을 입력합니다.  

```  
Get-Help Add-ADDSReadOnlyDomainControllerAccount
```  

옵션 인수는 대괄호 안에 표시됩니다.  

Windows PowerShell cmdlet에 대한 최신 도움말 예제 및 개념을 다운로드할 수도 있습니다. 자세한 내용은 [about_Updatable_Help](https://technet.microsoft.com/library/hh847735.aspx)를 참조하세요.  

원격 서버에 대해 Windows PowerShell cmdlet을 실행할 수 있습니다.  

-   Windows PowerShell에서 ADDSDeployment cmdlet과 함께 Invoke 명령을 사용 합니다. 예를 들어 contoso.com 도메인에서 ConDC3라는 원격 서버에 AD DS를 설치하려면 다음을 입력합니다.  

    ```  
    Invoke-Command { Install-ADDSDomainController -DomainName contoso.com -Credential (Get-Credential) } -ComputerName ConDC3  
    ```  

-또는-  

-   서버 관리자에서 원격 서버를 포함하는 서버 그룹을 만듭니다. 원격 서버의 이름을 마우스 오른쪽 단추로 클릭하고 **Windows PowerShell**을 클릭합니다.  

다음 섹션에서는 ADDSDeployment 모듈 cmdlet을 실행하여 AD DS를 설치하는 방법에 대해 설명합니다.  

-   [ADDSDeployment cmdlet 인수](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)  

-   [Windows PowerShell 자격 증명 지정](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSCreds)  

-   [테스트 cmdlet 사용](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_TestCmdlets)  

-   [Windows PowerShell을 사용 하 여 새 포리스트 루트 도메인 설치](../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSForest)  

-   [Windows PowerShell을 사용 하 여 새 자식 또는 트리 도메인 설치](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSDomain)  

-   [Windows PowerShell을 사용 하 여 추가 (복제본) 도메인 컨트롤러 설치](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSReplica)  

### <a name="addsdeployment-cmdlet-arguments"></a><a name="BKMK_Params"></a>ADDSDeployment cmdlet 인수  
다음 표에는 Windows PowerShell의 ADDSDeployment cmdlet에 대한 인수가 정리되어 있습니다. 굵은 글꼴로 표시된 인수가 필요합니다. dcpromo.exe에 대한 동등한 인수가 Windows PowerShell에서 다른 이름으로 지정된 경우 이 인수는 괄호 안에 나열됩니다.  

Windows PowerShell 스위치에서는 $TRUE 또는 $FALSE 인수를 사용할 수 있습니다. 기본적으로 $TRUE 되는 인수는 지정할 필요가 없습니다.  

기본값을 재정의하려면 인수를 $False 값으로 지정하면 됩니다. 예를 들어 때문에 **-installdns** 것을 지정 하지 않으면 하는 유일한 방법은 하는 경우 새 포리스트 설치에 대 한 자동으로 실행 *방지* 사용 하는 새 포리스트 설치 시 DNS 설치:  

```  
-InstallDNS:$false  
```  

마찬가지로, 때문에 **"installdns** 기본값이 $False의 Windows Server DNS를 호스트 하지 않는 환경에서 도메인 컨트롤러를 설치 하는 경우 서버, DNS 서버를 설치 하려면 다음 인수를 지정 해야 합니다.  

```  
-InstallDNS:$true  
```  


|                                                                                                                 인수                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ADPrepCredential <PS Credential>** **Note:** 도메인 이나 포리스트에 첫 번째 Windows Server 2012 도메인 컨트롤러를 설치 하 고 현재 사용자의 자격 증명에 작업을 수행할 수 있는 권한이 없는 경우에 필요 합니다. |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    규칙에 따라 포리스트를 준비할 수 있는 Enterprise Admins 및 Schema Admins 그룹 구성원으로 계정을 지정 [Get-credential](https://technet.microsoft.com/library/dd315327.aspx) 및 PSCredential 개체입니다.<p>없는 값을 지정 하는 경우의 값은 **"자격 증명** 인수를 사용 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                                                      AllowDomainControllerReinstall                                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    동일한 이름을 가진 또 다른 쓰기 가능한 도메인 컨트롤러 계정이 감지된 경우에도 쓰기 가능한 이 도메인 컨트롤러 설치를 계속할지 여부를 지정합니다.<p>사용 하 여 **$True** 계정이 현재 다른 쓰기 가능한 도메인 컨트롤러에 의해 사용 되지 경우에 있습니다.<p>기본값은 **$False**합니다.<p>이 인수는 RODC에는 사용할 수 없습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                                                           AllowDomainReinstall                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        기존 도메인을 다시 만들지 여부를 지정합니다.<p>기본값은 **$False**합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                                                                                             AllowPasswordReplicationAccountName <string []>                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         해당 암호를 이 RODC로 복제할 수 있는 컴퓨터 계정, 그룹 계정 및 사용자 계정의 이름을 지정합니다. 이 값을 비워 두려면 빈 문자열 ""을 사용합니다. 기본적으로 Allowed RODC Password Replication Group만 허용되며 이 그룹은 원래 빈 상태로 만들어집니다.<p>값을 문자열 배열로 제공합니다. 예를 들면 다음과 같습니다.<p>-AllowPasswordReplicationAccountName "JSmith", "JSmithPC", "지점 사용자 가" 코드                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                      < String > ApplicationPartitionsToReplicate **참고:** UI에 해당 하는 옵션이 없습니다. UI나 IFM을 사용하여 설치하는 경우 모든 응용 프로그램 파티션이 복제됩니다.                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    복제할 응용 프로그램 디렉터리 파티션을 지정합니다. 이 인수에 지정 하는 경우에 적용 되는 **-InstallationMediaPath** (ifm 미디어) 미디어에서 설치에 대 한 인수입니다. 기본적으로 모든 응용 프로그램 파티션은 고유 범위를 바탕으로 복제됩니다.<p>값을 문자열 배열로 제공합니다. 예를 들면 다음과 같습니다.<p>코드-<p>-ApplicationPartitionsToReplicate "파티션 1", "파티션 2", "파티션 3"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|                                                                                                                 Confirm                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        cmdlet을 실행하기 전에 확인 메시지가 표시됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                         CreateDnsDelegation **참고:** Add-addsreadonlydomaincontroller cmdlet을 실행 하는 경우에이 인수를 지정할 수 없습니다.                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                   도메인 컨트롤러와 함께 설치하고 있는 새 DNS 서버를 참조하는 DNS 위임을 만들지 여부를 나타냅니다. 유효한 Active Directory "통합 된 DNS만 합니다. 위임 레코드는 온라인 상태이고 액세스 가능한 Microsoft DNS 서버에서만 만들 수 있습니다. .com, gov, .biz, .edu와 같은 최상위 수준 도메인이나 .nz 및 .au와 같은 두 글자 국가 코드 도메인에 바로 종속된 도메인에 대해서는 위임 레코드를 만들 수 없습니다.<p>기본값은 환경에 따라 자동으로 계산됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                 **자격 증명 <PS Credential>** **참고:** 현재 사용자의 자격 증명에 작업을 수행할 수 있는 권한이 없는 경우에만 필요 합니다.                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                규칙에 따라 도메인에 로그온 할 수 있는 도메인 계정을 지정 [Get-credential](https://technet.microsoft.com/library/dd315327.aspx) 및 PSCredential 개체입니다.<p>값을 지정하지 않으면 현재 사용자의 자격 증명이 사용됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                                         CriticalReplicationOnly                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         AD DS 설치 작업을 다시 부팅 하기 전에 중요 한 복제를 수행 하 고 계속 합니다 있는지 여부를 지정 합니다. 중요하지 않은 복제는 설치가 완료되고 컴퓨터가 재부팅된 후에 수행됩니다.<p>이 인수는 사용하지 않는 것이 좋습니다.<p>UI(사용자 인터페이스)에 이 옵션과 동등한 옵션이 없습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                          DatabasePath <string>                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                      지정 된 정규화 된 비 "예를 들어 도메인 데이터베이스를 포함 하는 로컬 컴퓨터의 고정된 디스크에 있는 디렉터리에 대 한 범용 명명 규칙 (UNC) 경로 **C:\Windows\NTDS 합니다.**<p>기본값은 **%SYSTEMROOT%\NTDS**합니다. **중요:** (ReFS) 복원 파일 시스템으로 포맷 된 볼륨에 AD DS 데이터베이스 및 로그 파일을 저장할 수 있습니다, ReFS에서 AD DS를 호스팅하기 위한 특정 이점은, ReFS에서 데이터를 호스팅하기 위한 get 이외의 복구의 일반적인 이점입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                                                                DelegatedAdministratorAccountName <string>                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                RODC를 설치하고 관리할 수 있는 사용자 또는 그룹의 이름을 지정합니다.<p>기본적으로 Domain Admins 그룹의 구성원만 RODC를 관리할 수 있습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                              DenyPasswordReplicationAccountName <string []>                                                                                              |                                                                                                                                                                                                                                                                                                           해당 암호가 이 RODC로 복제되지 않는 컴퓨터 계정, 그룹 계정 및 사용자 계정의 이름을 지정합니다. 사용자나 컴퓨터의 자격 증명 복제를 거부하지 않으려면 빈 문자열 ""을 사용합니다. 기본적으로 Administrators, Server Operators, Backup Operators, Account Operators 및 Denied RODC Password Replication Group이 거부됩니다. 기본적으로 Denied RODC Password Replication Group에는 Cert Publishers, Domain Admins, Enterprise Admins, Enterprise Domain Controllers, Enterprise Read-Only Domain Controllers, Group Policy Creator Owners, krbtgt 계정 및 Schema Admins가 포함됩니다.<p>값을 문자열 배열로 제공합니다. 예를 들면 다음과 같습니다.<p>코드-<p>-DenyPasswordReplicationAccountName "RegionalAdmins", "AdminPCs"                                                                                                                                                                                                                                                                                                            |
|                                               DnsDelegationCredential <PS Credential> **참고:** add-addsreadonlydomaincontroller cmdlet을 실행할 때이 인수를 지정할 수 없습니다.                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      사용자 이름 및 규칙에 따라 DNS 위임 만들기에 대 한 암호 지정 [Get-credential](https://technet.microsoft.com/library/dd315327.aspx) 및 PSCredential 개체입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                        DomainMode <DomainMode> {w i n 2003 & #124; Win2008 & #124; Win2008R2 & #124; W i n 2012 & #124; Win2012R2}<p>또는<p>DomainMode <DomainMode> {2 & #124; 3 & #124; 4 & #124; 5 & #124; 6}                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             새 도메인을 만드는 동안 도메인 기능 수준을 지정합니다.<p>도메인 기능 수준은 포리스트 기능 수준보다 낮은 값으로 설정할 수 없으며, 포리스트 기능 수준보다 높은 값으로 설정할 수는 있습니다.<p>기본값은 자동으로 계산되며 **-ForestMode**에 대해 설정된 값이나 기존의 포리스트 기능 수준으로 설정됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|                                                                   **DomainName**<p>Install-ADDSForest 및 Install-ADDSDomainController cmdlet에 필요합니다.                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     추가 도메인 컨트롤러를 설치할 도메인의 FQDN을 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                       **DomainNetbiosName <string>**<p>FQDN 접두사 이름이 15자보다 긴 경우 Install-ADDSForest에 필요합니다.                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           Install-ADDSForest와 함께 사용합니다. 새 포리스트 루트 도메인에 NetBIOS 이름을 할당합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                              DomainType <DomainType> {ChildDomain & #124; TreeDomain} 또는 {자식 & #124; 트리}                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  만들려는 도메인의 유형, 즉 새 포리스트, 기존 포리스트의 새 도메인 트리 또는 기존 도메인의 자식 도메인을 나타냅니다.<p>DomainType의 기본값은 ChildDomain입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                                                  Force                                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             이 매개 변수가 지정된 경우 도메인을 추가 및 설치하는 동안 일반적으로 나타날 수 있는 모든 경고가 표시되지 않아 cmdlet에서 해당 실행을 완료할 수 있습니다. 이 매개 변수는 설치 스크립팅 시 포함하면 유용할 수 있습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                        ForestMode <ForestMode> {w i n 2003 & #124; Win2008 & #124; Win2008R2 & #124; W i n 2012 & #124; Win2012R2}<p>또는<p>ForestMode <ForestMode> {2 & #124; 3 & #124; 4 & #124; 5 & #124; 6}                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              새 포리스트를 만들 때 포리스트 기능 수준을 지정합니다.<p>기본값은 Win2012입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                                          InstallationMediaPath                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 새 도메인 컨트롤러를 설치하는 데 사용될 설치 미디어의 위치를 나타냅니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                                                                                                                InstallDns                                                                                                                |                                                                                                                                                                                                                                                                                                                      도메인 컨트롤러에 DNS 서버 서비스를 설치 및 구성할지 여부를 지정합니다.<p>새 포리스트의 경우 기본값은 **$True**이며, DNS 서버가 설치됩니다.<p>새 자식 도메인 또는 도메인 트리의 경우, 부모 도메인(또는 도메인 트리에 대한 포리스트 루트 도메인)이 이미 도메인에 대한 DNS 이름을 호스트하고 저장한 경우 이 매개 변수의 기본값은 $True입니다.<p>기존 도메인에 도메인 컨트롤러 설치에 대 한이 매개 변수가 지정 하지 않으면 및 현재 도메인에서 이미 호스트 하 고 기본적으로이 매개 변수는 다음에 도메인에 대 한 DNS 이름을 저장 **$True**합니다. 그렇지 않고 DNS 도메인 이름이 Active Directory 외부에서 호스트된 경우에는 기본값이 **$False**이며 DNS 서버가 설치되지 않습니다.                                                                                                                                                                                                                                                                                                                      |
|                                                                                                             LogPath <string>                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            도메인 로그 파일을 포함하는 로컬 컴퓨터의 고정 디스크에 있는 디렉터리에 대한 UNC(범용 명명 규칙)가 아닌 정규화된 경로를 지정합니다(예: **C:\Windows\Logs**).<p>기본값은 **%SYSTEMROOT%\NTDS**합니다. **중요:** (ReFS) 복원 파일 시스템으로 포맷 된 데이터 볼륨에 Active Directory 로그 파일을 저장 하지 않습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                             MoveInfrastructureOperationMasterRoleIfNecessary                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                  만들고 있는 경우 "현재 글로벌 카탈로그 서버에서 호스트 하는 경우"에 도메인 컨트롤러를 확인 하려면 도메인 컨트롤러에 인프라 마스터 작업 마스터 역할 (라고도 신축 단일 마스터 작업 또는 FSMO)를 전송할지 여부를 지정 글로벌 카탈로그 서버를 만들고 있다고 합니다. 전송이 필요한 경우 만들고 있는 도메인 컨트롤러에 인프라 마스터 역할을 전송하려면 이 매개 변수를 지정합니다. 이 경우 인프라 마스터 역할을 현재 그대로 남겨두려면 **NoGlobalCatalog** 옵션을 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                **Newdomainname <string>** **Note:** 설치-addsdomain에만 필요 합니다.                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           새 도메인의 단일 도메인 이름을 지정합니다.<p>예를 들어 라는 새 자식 도메인을 만들려는 경우 **emea.corp. fabrikam.com**, 를 지정 해야 **emea** 이 인수의 값으로.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                      **NewDomainNetbiosName <string>**<p>FQDN 접두사 이름이 15자보다 긴 경우 Install-ADDSDomain에 필요합니다.                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Install-ADDSDomain과 함께 사용합니다. 새 도메인에 NetBIOS 이름을 할당합니다. 기본값은 값에서 파생 된 **"NewDomainName**합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                                              NoDnsOnNetwork                                                                                                              |                                                                                                                                                                                                                                                                                                                                    네트워크에서 DNS 서비스를 사용할 수 없음을 지정합니다. 이 매개 변수는 이 컴퓨터의 네트워크 어댑터에 대한 IP 설정에서 이름 확인이 DNS 서버 이름으로 구성되어 있지 않은 경우에만 사용됩니다. 이름 확인을 위해 이 컴퓨터에 DNS 서버가 설치됨을 나타냅니다. 그렇지 않으면 먼저 네트워크 어댑터의 IP 설정을 DNS 서버의 주소로 구성해야 합니다.<p>이 매개 변수를 생략하면(기본값) DNS 서버를 연결하는 데 있어 이 서버 컴퓨터의 네트워크 어댑터에 대한 TCP/IP 클라이언트 설정이 사용됨을 나타냅니다. 따라서 이 매개 변수를 지정하지 않은 경우 먼저 TCP/IP 클라이언트 설정을 기본 설정 DNS 서버 주소로 구성해야 합니다.                                                                                                                                                                                                                                                                                                                                     |
|                                                                                                             NoGlobalCatalog                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   도메인 컨트롤러를 글로벌 카탈로그 서버로 설정하지 않음을 지정합니다.<p>Windows Server 2012를 실행 하는 도메인 컨트롤러는 글로벌 카탈로그와 기본적으로 설치 됩니다. 즉, 다음 항목을 별도로 지정하지 않은 경우 계산 없이 자동으로 실행됩니다.<p>코드-<p>-NoGlobalCatalog                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|                                                                                                           NoRebootOnCompletion                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     성공 여부와 상관없이, 명령 완료 시 컴퓨터를 다시 시작할지 여부를 지정합니다. 기본적으로 컴퓨터가 다시 시작됩니다. 서버를 다시 시작하지 않으려면 다음을 지정합니다.<p>코드-<p>-NoRebootOnCompletion: $True<p>UI(사용자 인터페이스)에 이 옵션과 동등한 옵션이 없습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                              **Parentdomainname <string>** **Note:** Install-addsdomain cmdlet에 필요 합니다.                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 기존 부모 도메인의 FQDN을 지정합니다. 자식 도메인이나 새 도메인 트리를 설치할 때 이 인수를 사용합니다.<p>예를 들어 이름이 **emea.corp.fabrikam.com**인 새 자식 도메인을 만들려면 이 인수 값으로 **corp.fabrikam.com**을 지정해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                                             ReadOnlyReplica                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   RODC(읽기 전용 도메인 컨트롤러)를 설치할지 여부를 지정합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                       ReplicationSourceDC <string>                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              도메인 정보를 복제할 파트너 도메인 컨트롤러의 FQDN을 나타냅니다. 기본값은 자동으로 계산됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                                                                                             **Jemode관리자 암호 <securestring>**                                                                                             | 안전 모드나 안전 모드의 변형(예: 디렉터리 서비스 복원 모드)으로 컴퓨터를 시작할 때 사용할 관리자 계정의 암호를 제공합니다.<p>기본값은 빈 암호입니다. 암호를 제공해야 합니다. 암호는 read-host -assecurestring 또는 ConvertTo-SecureString에서 제공된 것과 같은 System.Security.SecureString 형식으로 제공되어야 합니다.<p>SafeModeAdministratorPassword 인수 작업은 특별합니다. 인수로 지정하지 않을 경우 cmdlet은 마스킹된 암호를 입력 및 확인하라는 메시지를 표시합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법입니다. 값 없이 지정하고 cmdlet에 다른 인수가 지정되지 않은 경우 cmdlet은 확인 없이 마스킹된 암호를 입력하라는 메시지를 표시합니다. cmdlet를 대화형으로 실행할 경우 기본 설정된 사용법이 아닙니다. 값과 함께 지정한 경우 이 값은 보안 문자열이어야 합니다. cmdlet를 대화형으로 실행할 경우 기본 설정된 사용법이 아닙니다. 예를 들어 Read-Host cmdlet을 사용하여 수동으로 암호를 물어 사용자에게 보안 문자열을 물을 수 있습니다. -safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring) 또한 보안 문자열을 변환된 일반 텍스트 변수로 제공할 수도 있습니다(권장되지 않음). -safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force) |
|                                                                     **SiteName <string>**<p>Add-addsreadonlydomaincontrolleraccount cmdlet에 필요합니다.                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  도메인 컨트롤러를 설치할 사이트를 지정합니다. 없는 **"sitename** 인수를 실행할 때 **Install-addsforest** 만든 첫 번째 사이트 사용자가 기본 첫 번째-사이트 이름.<p>**-sitename**에 대한 인수로 제공된 경우 사이트 이름이 이미 존재해야 합니다. cmdlet은 사이트를 만들지 않습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                           SkipAutoConfigureDNS                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           DNS 클라이언트 설정, 전달자 및 루트 힌트의 자동 구성을 건너뜁니다. DNS 서버 서비스가 이미 설치 되었거나 함께 자동으로 설치 하는 경우이 인수에만 적용 됩니다 **-InstallDNS**합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                                            SystemKey <string>                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            복제할 데이터가 있는 미디어의 시스템 키를 지정합니다.<p>기본값은 **none**입니다.<p>데이터 형식은 read-host -assecurestring 또는 ConvertTo-SecureString에서 제공된 형식이어야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                                           SysvolPath <string>                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     로컬 컴퓨터의 고정 디스크에 있는 디렉터리에 대한 UNC(범용 명명 규칙)가 아닌 정규화된 경로를 지정합니다(예: **C:\Windows\SYSVOL**).<p>기본값은 **%SYSTEMROOT%\SYSVOL**합니다. **중요:** SYSVOL (ReFS) 복원 파일 시스템으로 포맷 된 데이터 볼륨에 저장할 수 없습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                                                                              SkipPreChecks                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              설치를 시작하기 전에 필수 구성 요소 확인을 실행하지 않습니다. 이 설정은 사용하지 않는 것이 좋습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                                                                                                                  Whatif                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   cmdlet이 실행될 경우 결과 동작을 표시합니다. cmdlet이 실행되지 않습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### <a name="specifying-windows-powershell-credentials"></a><a name="BKMK_PSCreds"></a>Windows PowerShell 자격 증명 지정  
사용 하 여 화면에 일반 텍스트로 노출 하지 않고 자격 증명을 지정할 수 있습니다 [get-credential](https://technet.microsoft.com/library/dd315327.aspx)합니다.  

SafeModeAdministratorPassword 및 LocalAdministratorPassword 인수 작업은 특별합니다.  

-   인수로 지정하지 않을 경우 cmdlet은 마스킹된 암호를 입력 및 확인하라는 메시지를 표시합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법입니다.  

-   값과 함께 지정한 경우 값은 보안 문자열이어야 합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법이 아닙니다.  

예를 들어 **Read-Host** cmdlet을 사용하여 수동으로 암호를 물어 사용자에게 보안 문자열을 물을 수 있습니다.  

```  
-SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString)
```  

> [!WARNING]  
> 이전 옵션이 암호를 확인하지 않으므로 각별히 주의해야 합니다. 암호는 표시되지 않습니다.  

변환된 일반 텍스트 변수로 보안 문자열을 제공할 수도 있습니다(권장되지 않음).  

```  
-SafeModeAdministratorPassword (ConvertTo-SecureString "Password1" -AsPlainText -Force)
```  

> [!WARNING]  
> 일반 텍스트 암호는 제공하거나 저장하지 않는 것이 좋습니다. 스크립트에서 이 명령을 실행하는 사용자나 어깨 너머로 보고 있는 다른 사용자가 해당 도메인 컨트롤러의 DSRM 암호를 알게 될 수 있습니다. 이 암호를 알게 된 사용자는 도메인 컨트롤러 자체를 가장하여 자신의 권한을 Active Directory 포리스트에서 가장 높은 수준으로 상승시킬 수 있습니다.  

### <a name="using-test-cmdlets"></a><a name="BKMK_TestCmdlets"></a>테스트 cmdlet 사용  
ADDSDeployment cmdlet마다 해당 테스트 cmdlet이 있습니다. cmdlet은 설치 작업 시 필수 구성 요소 확인만 실행합니다. 설치 설정은 구성하지 않습니다. 각 테스트 cmdlet에 대 한 인수는 해당 설치 cmdlet의 경우와 동일 하지만 **"SkipPreChecks** 테스트 cmdlet을 사용할 수 있습니다.  

|테스트 cmdlet|설명|  
|---------------|---------------|  
|Test-ADDSForestInstallation|새 Active Directory 포리스트 설치 관련 필수 구성 요소를 실행합니다.|  
|Test-ADDSDomainInstallation|Active Directory에 새 도메인 설치하는 것과 관련된 필수 구성 요소를 실행합니다.|  
|Test-ADDSDomainControllerInstallation|Active Directory에 도메인 컨트롤러를 설치하는 것과 관련된 필수 구성 요소를 실행합니다.|  
|Test-ADDSReadOnlyDomainControllerAccountCreation|RODC(읽기 전용 도메인 컨트롤러) 계정 추가 관련 필수 구성 요소를 실행합니다.|  

### <a name="installing-a-new-forest-root-domain-using-windows-powershell"></a><a name="BKMK_PSForest"></a>Windows PowerShell을 사용 하 여 새 포리스트 루트 도메인 설치  
새 포리스트 설치를 위한 명령 구문은 다음과 같습니다. 옵션 인수는 대괄호 안에 표시됩니다.  

```  
Install-ADDSForest [-SkipPreChecks] -DomainName <string> -SafeModeAdministratorPassword <SecureString> [-CreateDNSDelegation] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-DomainNetBIOSName <string>] [-ForestMode <ForestMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-InstallDNS] [-LogPath <string>] [-NoRebootOnCompletion] [-SkipAutoConfigureDNS] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  

> [!NOTE]  
> DNS 도메인 이름 접두사를 바탕으로 자동으로 생성된 15자 이름을 변경하기를 원하거나 이름이 15자를 초과하는 경우 -DomainNetBIOSName 인수가 필요합니다.  

예를 들어 이름이 corp.contoso.com인 새 포리스트를 설치하고 DSRM 암호를 제공하라는 메시지를 안전하게 표시하려면 다음을 입력합니다.  

```  
Install-ADDSForest -DomainName "corp.contoso.com"   
```  

> [!NOTE]  
> DNS 서버는 Install-ADDSForest 실행 시 기본적으로 설치됩니다.  

이름이 corp.contoso.com인 새 포리스트를 설치하고 contoso.com 도메인에서 DNS 위임을 만들고 도메인 기능 수준을 Windows Server 2008 R2로 올린 다음 포리스트 기능 수준을 Windows Server 2008로 올리고 D:\ 드라이브에 Active Directory 데이터베이스 및 SYSVOL을 설치하고 E:\ 드라이브에 로그 파일을 설치한 후 디렉터리 서비스 복원 모드 암호를 제공하라는 메시지를 표시하려면 다음을 입력합니다.  

```  
Install-ADDSForest -DomainName corp.contoso.com -CreateDNSDelegation -DomainMode Win2008 -ForestMode Win2008R2 -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  

### <a name="installing-a-new-child-or-tree-domain-using-windows-powershell"></a><a name="BKMK_PSDomain"></a>Windows PowerShell을 사용 하 여 새 자식 또는 트리 도메인 설치  
새 도메인 설치를 위한 명령 구문은 다음과 같습니다. 옵션 인수는 대괄호 안에 표시됩니다.  

```  
Install-ADDSDomain [-SkipPreChecks] -NewDomainName <string> -ParentDomainName <string> -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainReinstall] [-CreateDNSDelegation] [-Credential <PS Credential>] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [DomainType <DomainType> {Child Domain | TreeDomain} [-InstallDNS] [-LogPath <string>] [-NoGlobalCatalog] [-NewDomainNetBIOSName <string>] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-Systemkey <SecureString>] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  

> [!NOTE]  
> 현재 Enterprise Admins 그룹의 구성원으로 로그온하지 않은 경우에만 **-credential** 인수가 필요합니다.  
>   
> DNS 도메인 이름 접두사를 바탕으로 자동으로 생성된 15자 이름을 변경하기를 원하거나 이름이 15자를 초과하는 경우 **-NewDomainNetBIOSName** 인수가 필요합니다.  

예를 들어 corp\EnterpriseAdmin1 자격 증명을 사용하여 이름이 child.corp.contoso.com인 새 자식 도메인을 만들고 DNS 서버를 설치하고 corp.contoso.com 도메인에서 DNS 위임을 만들고 도메인 기능 수준을 Windows Server 2003으로 설정한 후 이름이 Houston인 사이트에서 도메인 컨트롤러를 글로벌 카탈로그 서버로 설정하고 복제 원본 도메인 컨트롤러로 DC1.corp.contoso.com을 사용하고 D:\ 드라이브에 Active Directory 데이터베이스 및 SYSVOL을 설치하고 E:\ 드라이브에 로그 파일을 설치한 후 명령을 확인하라는 메시지가 아닌 디렉터리 서비스 복원 모드 암호를 제공하라는 메시지를 표시하려면 다음을 입력합니다.  

```  
Install-ADDSDomain -SafeModeAdministratorPassword -Credential (get-credential corp\EnterpriseAdmin1) -NewDomainName child -ParentDomainName corp.contoso.com -InstallDNS -CreateDNSDelegation -DomainMode Win2003 -ReplicationSourceDC DC1.corp.contoso.com -SiteName Houston -DatabasePath "d:\NTDS" "SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs" -Confirm:$False  
```  

### <a name="installing-an-additional-replica-domain-controller-using-windows-powershell"></a><a name="BKMK_PSReplica"></a>Windows PowerShell을 사용 하 여 추가 (복제본) 도메인 컨트롤러 설치  
추가 도메인 설치를 위한 명령 구문은 다음과 같습니다. 옵션 인수는 대괄호 안에 표시됩니다.  

```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainControllerReinstall] [-ApplicationPartitionsToReplicate <string[]>] [-CreateDNSDelegation] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-NoGlobalCatalog] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  

corp.contoso.com 도메인에 도메인 컨트롤러 및 DNS 서버를 설치하고 도메인의 Administrator 자격 증명 및 DSRM 암호를 제공하라는 메시지를 표시하려면 다음을 입력합니다.  

```  
Install-ADDSDomainController -Credential (Get-Credential CORP\Administrator) -DomainName "corp.contoso.com"
```  

컴퓨터가 이미 도메인에 가입되어 있고 사용자가 Domain Admins 그룹의 구성원인 경우 다음을 사용할 수 있습니다.  

```  
Install-ADDSDomainController -DomainName "corp.contoso.com"  
```  

도메인 이름을 입력하라는 메시지를 표시하려면 다음을 입력합니다.  

```  
Install-ADDSDomainController -Credential (Get-Credential) -DomainName (Read-Host "Domain to promote into")
```  

다음 명령은 Contoso\EnterpriseAdmin1 자격 증명을 사용하여 Boston이라는 사이트에 쓰기 가능한 도메인 컨트롤러 및 글로벌 카탈로그 서버를 설치하고 DNS 서버를 설치하며 contoso.com 도메인에서 DNS 위임을 만들고 c:\ADDS IFM 폴더에 저장된 미디어에서 설치하며 D:\ 드라이브에 Active Directory 데이터베이스 및 SYSVOL을 설치하고 E:\ 드라이브에 로그 파일을 설치하며 AD DS 설치 완료 후 서버를 자동으로 다시 시작하게 하고 디렉터리 서비스 복원 모드 암호를 제공하라는 메시지를 표시합니다.  

```  
Install-ADDSDomainController -Credential (Get-Credential CONTOSO\EnterpriseAdmin1) -CreateDNSDelegation -DomainName corp.contoso.com -SiteName Boston -InstallationMediaPath "c:\ADDS IFM" -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  

### <a name="performing-a-staged-rodc-installation-using-windows-powershell"></a>Windows PowerShell을 사용하여 단계적 RODC 설치 수행  
RODC 계정을 만들기 위한 명령 구문은 다음과 같습니다. 옵션 인수는 대괄호 안에 표시됩니다.  

```  
Add-ADDSReadOnlyDomainControllerAccount [-SkipPreChecks] -DomainControllerAccuntName <string> -DomainName <string> -SiteName <string> [-AllowPasswordReplicationAccountName <string []>] [-NoGlobalCatalog] [-Credential <PS Credential>] [-DelegatedAdministratorAccountName <string>] [-DenyPasswordReplicationAccountName <string []>] [-InstallDNS] [-ReplicationSourceDC <string>] [-Force] [-WhatIf] [-Confirm] [<Common Parameters>]  
```  

RODC 계정에 서버를 연결하기 위한 명령 구문은 다음과 같습니다. 옵션 인수는 대괄호 안에 표시됩니다.  

```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-ApplicationPartitionsToReplicate <string[]>] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-NoDNSOnNetwork] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-UseExistingAccount] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  

예를 들어 이름이 RODC1인 RODC 계정을 만듭니다.  

```  
Add-ADDSReadOnlyDomainControllerAccount -DomainControllerAccountName RODC1 -DomainName corp.contoso.com -SiteName Boston DelegatedAdministratoraccountName PilarA  
```  

그런 다음 RODC1 계정에 연결할 서버에서 다음 명령을 실행합니다. 서버는 도메인에 가입시킬 수 없습니다. 먼저, AD DS 서버 역할 및 관리 도구를 설치합니다.  

```  
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```  

그런 다음 다음 명령을 실행하여 RODC를 만듭니다.  

```  
Install-ADDSDomainController -DomainName corp.contoso.com -SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString) -Credential (Get-Credential Corp\PilarA) -UseExistingAccount
```  

키를 눌러 **Y** 확인 하거나 포함 하는 **"확인** 확인 프롬프트를 방지 하기 위해 인수입니다.  

## <a name="installing-ad-ds-by-using-server-manager"></a><a name="BKMK_GUI"></a>서버 관리자를 사용 하 여 AD DS 설치  
서버 관리자에서 Windows Server 2012의 새로운 기능인는 Active Directory 도메인 서비스 구성 마법사, 다음 역할 추가 마법사를 사용 하 여 Windows Server 2012에서 AD DS는 설치할 수 있습니다. Active Directory 도메인 서비스 설치 마법사 (dcpromo.exe)는 Windows Server 2012부터 사용 되지 않습니다.  

다음 섹션에서는 여러 서버에서 AD DS를 설치 및 관리하기 위해 서버 풀을 만드는 방법 및 마법사를 사용하여 AD DS를 설치하는 방법에 대해 설명합니다.  

### <a name="creating-server-pools"></a><a name="BKMK_ServerPools"></a>서버 풀 만들기  
서버 관리자는 서버 관리자를 실행하는 컴퓨터에서 이 관리자에 액세스할 수 있는 동안 네트워크에서 다른 서버를 풀링할 수 있습니다. 풀링하고 나면 서버 관리자 내 사용 가능한 다른 구성 옵션이나 AD DS의 원격 설치를 위해 이 서버를 선택할 수 있습니다. 서버 관리자를 실행하는 컴퓨터는 스스로 자동으로 풀링됩니다. 서버 풀에 대 한 자세한 내용은 참조 [서버 관리자에 서버 추가](https://technet.microsoft.com/library/hh831453.aspx)합니다.  

> [!NOTE]  
> 작업 그룹 서버에서 서버 관리자를 사용하여 도메인 가입 컴퓨터를 관리하거나 그 반대로 하려면 추가 구성 단계가 필요합니다. 자세한 내용은 참조 하십시오. "추가 작업 그룹에서 서버를 관리 하 고"에서 [서버 관리자에 서버 추가](https://technet.microsoft.com/library/hh831453.aspx)합니다.  

### <a name="installing-ad-ds"></a><a name="BKMK_installADDSGUI"></a>AD DS 설치  
**관리 자격 증명**  

AD DS를 설치하는 데 필요한 자격 증명 요구 사항은 선택한 배포 구성에 따라 다릅니다. 자세한 내용은 [Adprep.exe를 실행하고 Active Directory Domain Services를 설치하는 데 필요한 자격 증명 요구 사항](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)을 참조하십시오.  

다음 절차에 따라 GUI 방법을 사용하여 AD DS를 설치합니다. 이 단계는 로컬로 또는 원격으로 수행할 수 있습니다. 이 단계에 대한 자세한 내용은 다음 항목을 참조하십시오.  

-   [서버 관리자를 사용 하 여 포리스트 배포](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  

-   [기존 도메인 &#40;수준 200에 복제 Windows Server 2012 도메인 컨트롤러를 설치 합니다.&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  

-   [새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 &#40;수준 200 설치&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  

-   [Windows Server 2012 Active Directory 읽기 전용 도메인 컨트롤러 &#40;RODC&#41; &#40;수준 200 설치&#41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md)  

##### <a name="to-install-ad-ds-by-using-server-manager"></a>서버 관리자를 사용하여 AD DS를 설치하려면  

1.  서버 관리자에서 클릭 **관리** 클릭 **역할 및 기능 추가** 역할 추가 마법사를 시작 합니다.  

2.  **시작하기 전에** 페이지에서 **다음**을 클릭합니다.  

3.  **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭한 후 **다음**을 클릭합니다.  

4.  **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭하고 AD DS를 설치할 서버의 이름을 클릭한 후에 **다음**을 클릭합니다.  

    원격 서버를 선택하려면 먼저 서버 풀을 만든 다음 원격 서버를 이 풀에 추가합니다. 서버 풀을 만드는 방법에 대 한 자세한 내용은 참조 [서버 관리자에 서버 추가](https://technet.microsoft.com/library/hh831453.aspx)합니다.  

5.  **서버 역할 선택** 페이지에서 **Active Directory 도메인 서비스**를 클릭하고 **역할 및 기능 추가 마법사** 대화 상자에서 **기능 추가**를 클릭한 후 **다음**을 클릭합니다.  

6.  에 **기능 선택** 페이지에서 설치 하려는 추가 기능 선택 **다음**합니다.  

7.  에 **Active Directory 도메인 서비스** 페이지, 정보를 검토 한 다음 클릭 **다음**합니다.  

8.  **설치 선택 확인** 페이지에서 **설치**를 클릭합니다.  

9. **결과** 페이지에서 [설치 완료]가 표시되는지 확인하고 **이 서버를 도메인 컨트롤러로 승격**을 클릭하여 Active Directory 도메인 서비스 구성 마법사를 시작합니다.  

    ![AD DS 설치](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_SMPromotes.gif)  

    > [!IMPORTANT]  
    > 이 시점에서 Active Directory 도메인 서비스 구성 마법사를 시작하지 않고 역할 추가 마법사를 닫은 경우 서버 관리자에서 [작업]을 클릭하여 이 마법사를 다시 시작할 수 있습니다.  

    ![AD DS 설치](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  

10. 에 **배포 구성** 페이지에서 다음 옵션 중 하나를 선택 합니다.  

    -   기존 도메인에 추가 도메인 컨트롤러를 설치 하는 경우 클릭 **도메인 컨트롤러를 기존 도메인에 추가**, 고 (예를 들어 emea.corp.contoso.com) 도메인의 이름을 입력 하거나 줄임표 **선택...** 도메인과 자격 증명을 선택할 수 (예를 들어, Domain Admins 그룹의 구성원 인 계정 지정)을 클릭 한 다음 **다음**합니다.  

        > [!NOTE]  
        > 컴퓨터가 도메인에 가입되어 있고 로컬 설치를 수행하는 경우에만 기본적으로 도메인 이름 및 현재 사용자의 자격 증명이 제공됩니다. 원격 서버에 AD DS를 설치하는 경우에는 설계상 자격 증명을 지정해야 합니다. 현재 사용자 자격 증명에 설치를 수행 하는 데 충분 하지도 경우 **변경...** 다른 자격 증명을 지정 합니다.  

        자세한 내용은 참조 [기존 도메인 & #40;에 복제 Windows Server 2012 도메인 컨트롤러를 설치 합니다. 200 수준 & #41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)합니다.  

    -   새 자식 도메인을 설치 하는 경우 클릭 **를 기존 포리스트에 새 도메인을 추가**, 에 대 한 **도메인 유형 선택**, 선택, **자식 도메인**, 입력 또는 부모 도메인 DNS 이름 (예: corp.contoso.com)의 이름을 찾고, 새 자식 도메인 (예: emea)을 사용 하 여 새 도메인 만들기를 클릭 한 다음에 자격 증명을 입력의 상대 이름을 입력 **다음**합니다.  

        자세한 내용은 참조 [는 새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 및 #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)합니다.  

    -   새 도메인 트리를 설치 하는 경우 클릭 **를 기존 포리스트에 새 도메인 추가**, 에 대 한 **도메인 유형 선택**, 선택 **트리 도메인**, 루트 도메인 (예: corp.contoso.com)의 이름을 입력, 새 도메인 (예: fabrikam.com)을 사용 하 여 새 도메인 만들기를 클릭 한 다음에 자격 증명을 입력의 DNS 이름을 입력 **다음**합니다.  

        자세한 내용은 참조 [는 새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 및 #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)합니다.  

    -   새 포리스트를 설치 하는 경우 클릭 **새 포리스트 추가** 고 루트 도메인 (예: corp.contoso.com)의 이름을 입력 합니다.  

        자세한 내용은 참조 [#40; & 새 Windows Server 2012 Active Directory 포리스트 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)합니다.  

11. **도메인 컨트롤러 옵션** 페이지에서 다음 옵션 중 하나를 선택합니다.  

    -   새 포리스트나 도메인을 만드는 경우 도메인 및 포리스트 기능 수준을 선택하고 **DNS(Domain Name System) 서버**를 클릭하고 DSRM 암호를 지정한 후 **다음**을 클릭합니다.  

    -   도메인 컨트롤러를 기존 도메인에 추가하는 경우 필요에 따라 **DNS(Domain Name System) 서버**, **GC(글로벌 카탈로그)** 또는 **RODC(읽기 전용 도메인 컨트롤러)** 를 클릭하고 사이트 이름을 선택하고 DSRM 암호를 입력한 후 **다음**을 클릭합니다.  

    서로 다른 조건에서 이 페이지에서 사용할 수 있거나 사용할 수 없는 옵션에 대한 자세한 내용은 [도메인 컨트롤러 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)을 참조하십시오.  

12. 에 **DNS 옵션** (DNS 서버를 설치 하는 경우에 표시) 페이지에서 클릭 **DNS 위임 업데이트** 필요에 따라 합니다. 이 옵션을 클릭한 경우 부모 DNS 영역에서 DNS 위임 레코드를 만들 권한이 있는 자격 증명을 제공합니다.  

    부모 영역을 호스트하는 DNS 서버에 연결할 수 없는 경우 **DNS 위임 업데이트** 옵션을 사용할 수 없습니다.  

    DNS 위임을 업데이트 해야 하는지 여부에 대 한 자세한 내용은 참조 [영역 위임 이해](https://technet.microsoft.com/library/cc771640.aspx)합니다. DNS 위임 업데이트 시 오류가 발생하면 [DNS 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)을 참조하십시오.  

13. 에 **RODC 옵션** (RODC를 설치 하는 경우에 표시) 페이지에서 그룹 또는 사용자에 게는 RODC를 관리할는 허용 또는 거부 됨 암호 복제 그룹에서 계정을 제거 하 고 클릭 한 다음에 계정을 추가의 이름을 지정 **다음**합니다.  

    자세한 내용은 참조 [암호 복제 정책](https://technet.microsoft.com/library/cc730883(v=ws.10))합니다.  

14. 에 **추가 옵션** 페이지에서 다음 옵션 중 하나를 선택 합니다.  

    -   새 도메인을 만드는 경우 새 NetBIOS 이름을 입력하거나 도메인의 기본 NetBIOS 이름을 확인한 후 **다음**을 클릭합니다.  

    -   기존 도메인에 도메인 컨트롤러를 추가하는 경우 AD DS 설치 데이터를 복제할 도메인 컨트롤러를 선택합니다(또는 마법사에서 도메인 컨트롤러를 선택하도록 허용). 미디어에서 설치 하는 경우 클릭 **미디어 경로에서 설치** 입력 하 고 설치 원본 파일의 경로를 확인 한 다음 클릭 **다음**합니다.  

        도메인에 첫 번째 도메인 컨트롤러를 설치할 때는 IFM(미디어에서 설치)을 사용할 수 없습니다. 서로 다른 운영 체제 버전 간에는 IFM이 작동하지 않습니다. 즉, IFM을 사용 하 여 Windows Server 2012를 실행 하는 추가 도메인 컨트롤러를 설치 하려면 Windows Server 2012 도메인 컨트롤러에서 백업 미디어를 만들 해야 있습니다. IFM에 대 한 자세한 내용은 참조 [IFM을 사용 하 여 추가 도메인 컨트롤러 설치](https://technet.microsoft.com/library/cc816722(WS.10).aspx)합니다.  

15. **경로** 페이지에서 Active Directory 데이터베이스, 로그 파일 및 SYSVOL 폴더에 대한 위치를 입력하고(또는 기본 위치 적용) **다음**을 클릭합니다.  

    > [!IMPORTANT]  
    > ReFS(Resilient File System)로 포맷된 데이터 볼륨에 Active Directory 데이터베이스, 로그 파일 또는 SYSVOL 폴더를 저장하지 마십시오.  

16. **준비 옵션** 페이지에 adprep을 실행할 권한이 있는 자격 증명을 입력합니다. 자세한 내용은 [Adprep.exe를 실행하고 Active Directory Domain Services를 설치하는 데 필요한 자격 증명 요구 사항](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)을 참조하십시오.  

17. 에 **옵션 검토** 페이지에서 선택 사항을 확인을 클릭 하 여 **스크립트를 보려면** 설정을 Windows PowerShell 스크립트를 내보낼을 클릭 한 다음 원하는 경우 **다음**.  

18. 에 **필수 구성 요소 확인** 페이지 해당 필수 구성 요소 유효성 검사 완료를 확인 한 다음 클릭 **설치**합니다.  

19. 에 **결과** 페이지에서 서버를 도메인 컨트롤러로 제대로 구성 되었는지 확인 합니다. AD DS 설치를 완료하기 위해 서버가 자동으로 다시 시작됩니다.  

## <a name="performing-a-staged-rodc-installation-using-the-graphical-user-interface"></a><a name="BKMK_UIStaged"></a>그래픽 사용자 인터페이스를 사용 하 여 단계적 RODC 설치 수행  
단계적 RODC 설치를 통해 두 개의 단계로 RODC를 만들 수 있습니다. 첫 번째 단계에서 Domain Admins 그룹의 구성원이 RODC 계정을 만듭니다. 두 번째 단계에서 서버가 RODC 계정에 연결됩니다. 두 번째 단계는 Domain Admins 그룹의 구성원이나 위임된 도메인 사용자나 그룹에서 완료할 수 있습니다.  

#### <a name="to-create-an-rodc-account-by-using-the-active-directory-management-tools"></a>Active Directory 관리 도구를 사용하여 RODC 계정을 만들려면  

1.  Active Directory 관리 센터나 Active Directory 사용자 및 컴퓨터를 사용하여 RODC 계정을 만들 수 있습니다.  

    1.  클릭 **시작**, 클릭 **관리 도구**, 를 클릭 하 고 **Active Directory 관리 센터**합니다.  

    2.  왼쪽에 있는 탐색 창에서 도메인 이름을 클릭합니다.  

    3.  관리 목록 (가운데 창)에서 클릭 된 **도메인 컨트롤러** OU입니다.  

    4.  작업 창 (오른쪽 창)에서 클릭 **읽기 전용 도메인 컨트롤러 계정 미리 만들기**합니다.  

    -또는-  

    1.  **시작**, **관리 도구**, **Active Directory 사용자 및 컴퓨터**를 차례로 클릭합니다.  

    2.  **Domain Controllers** OU(조직 구성 단위)를 마우스 오른쪽 단추로 클릭하거나 **Domain Controllers** OU를 클릭한 다음 **동작**을 클릭합니다.  

    3.  **읽기 전용 도메인 컨트롤러 계정 미리 만들기**를 클릭합니다.  

2.  에 **Active Directory 도메인 서비스 설치 마법사 시작** 페이지에서 기본값은 정책 PRP (암호 복제)를 선택 수정 하려는 경우 **고급 모드 설치 사용**, 를 클릭 하 고 **다음**합니다.  

3.  에 **네트워크 자격 증명** 페이지의 **설치를 수행 하는 데 계정 자격 증명을 지정**, 클릭 **현재 로그온 자격 증명에 대 한** 키를 누르거나 **대체 자격 증명**, 를 클릭 하 고 **설정**. 에 **Windows 보안** 대화 상자에서 추가 도메인 컨트롤러를 설치할 수 있는 계정의 사용자 이름 및 암호를 제공 합니다. 추가 도메인 컨트롤러를 설치하려면 Enterprise Admins 그룹 또는 Domain Admins 그룹의 구성원이어야 합니다. 자격 증명을 제공했으면 **다음**을 클릭합니다.  

4.  에 **컴퓨터 이름을 지정** 페이지 RODC 될 서버의 컴퓨터 이름을 입력 합니다.  

5.  에 **사이트 선택** 페이지, 목록에서 사이트를 선택 하거나 마법사를 실행 하는 컴퓨터의 IP 주소에 해당 하는 사이트에 도메인 컨트롤러를 설치 하는 옵션을 선택 하 고 클릭 한 다음 **다음**합니다.  

6.  **추가 도메인 컨트롤러 옵션** 페이지에서 다음 항목을 선택하고 **다음**을 클릭합니다.  

    -   **DNS 서버**: 이 옵션은 도메인 컨트롤러가 DNS(Domain Name System) 서버로 작동할 수 있도록 기본적으로 선택되어 있습니다. 도메인 컨트롤러를 DNS 서버로 사용하지 않으려면 이 옵션을 선택 취소합니다. 그러나 RODC에 DNS 서버 역할을 설치하지 않고 RODC가 지점의 유일한 도메인 컨트롤러이면, 허브 사이트에 대한 WAN(광역 네트워크)이 오프라인 상태일 때 지점의 사용자는 이름을 확인할 수 없습니다.  

    -   **글로벌 카탈로그**: 이 옵션은 기본적으로 선택됩니다. 글로벌 카탈로그, 읽기 전용 디렉터리 파티션을 도메인 컨트롤러에 추가하고 글로벌 카탈로그 검색 기능을 사용하도록 설정합니다. 도메인 컨트롤러를 글로벌 카탈로그 서버로 지정하지 않으려면 이 옵션을 선택 취소합니다. 그러나 지점에 글로벌 카탈로그 서버를 설치하지 않거나 RODC가 포함된 사이트에 대해 유니버설 그룹 구성원 자격 캐싱을 사용하도록 설정하지 않으면, 허브 사이트에 대한 WAN이 오프라인 상태일 때 지점의 사용자는 도메인에 로그온할 수 없습니다.  

    -   **읽기 전용 도메인 컨트롤러**: RODC 계정을 만들 때 이 옵션은 기본적으로 선택되며 선택 취소할 수 없습니다.  

7.  선택한 경우에 **고급 모드 설치 사용** 에서 확인란의 **시작** 페이지는 **암호 복제 정책 지정** 페이지가 나타납니다. 기본적으로 계정 암호는 RODC로 복제되지 않으며 보안 관련 계정(예: Domain Admins 그룹 구성원)의 암호는 RODC로 명시적으로 복제될 수 없습니다.  

    정책에 다른 계정을 추가 하려면 클릭 **추가**, 를 클릭 한 다음 **이 RODC로 복제할 계정에 대 한 암호 허용** 키를 누르거나 **이 RODC에 복제에서 계정에 대 한 암호를 거부** 다음 계정을 선택 하 고 있습니다.  

    완료 되 면 (또는 기본 설정을 수락)를 클릭 하 여 **다음**합니다.  

8.  에 **의 RODC 설치 및 관리 위임** 페이지에서 사용자 또는 그룹에서 만들고 있는 RODC 계정에 서버 연결의 이름을 입력 합니다. 보안 주체의 이름은 하나만 입력할 수 있습니다.  

    디렉터리에서 특정 사용자 또는 그룹을 검색하려면 **설정**을 클릭합니다. **사용자 또는 그룹 선택**, 그룹 또는 사용자의 이름을 입력 합니다. RODC 설치 및 관리를 그룹에 위임하는 것이 좋습니다.  

    또한 이 사용자나 그룹은 설치 후에 RODC에 대해 로컬 관리 권한을 갖습니다. 사용자 또는 그룹을 지정하지 않으면 Domain Admins 그룹 또는 Enterprise Admins 그룹의 구성원만 서버를 계정에 연결할 수 있습니다.  

    작업이 완료되면 **다음**을 클릭합니다.  

9. 에 **요약** 페이지에서 선택 항목을 검토 합니다. 클릭 **다시** 필요한 경우 선택 내용을 변경 합니다.  

    선택한 설정을 후속 AD DS 작업을 자동화 하 고 클릭 하는 데 사용할 수 있는 응답 파일에 저장 하려면 **설정 내보내기**합니다. 응답 파일의 이름을 입력하고 **저장**을 클릭합니다.  

    선택한 내용이 정확한 경우 클릭 **다음** RODC 계정을 만들 수 있습니다.  

10. 에 **Active Directory 도메인 서비스 설치 마법사 완료** 페이지에서 클릭 **마침**합니다.  

RODC 계정을 만들었으면 서버를 계정에 연결하여 RODC 설치 작업을 완료할 수 있습니다. 이 두 번째 단계는 RODC가 배치될 지점에서 완료할 수 있습니다. 이 절차를 수행하는 서버는 도메인에 가입할 수 없습니다. Windows Server 2012 부터는 역할 추가 마법사에서 서버 관리자를 사용 하면 서버를 RODC 계정에 연결 합니다.  

#### <a name="to-attach-a-server-to-an-rodc-account-using-server-manager"></a>서버 관리자를 사용하여 서버를 RODC 계정에 연결하려면  

1.  로컬 관리자로 로그온합니다.  

2.  서버 관리자에서 **역할 및 기능 추가**를 클릭합니다.  

3.  **시작하기 전에** 페이지에서 **다음**을 클릭합니다.  

4.  **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치**를 클릭한 후 **다음**을 클릭합니다.  

5.  **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭하고 AD DS를 설치할 서버의 이름을 클릭한 후에 **다음**을 클릭합니다.  

6.  에 **서버 역할 선택** 페이지에서 클릭 **Active Directory 도메인 서비스**, 클릭 **기능 추가** 클릭 하 고 **다음**합니다.  

7.  **기능 선택** 페이지에서 설치할 추가 기능을 선택한 후 **다음**을 클릭합니다.  

8.  에 **Active Directory 도메인 서비스** 페이지, 정보를 검토 한 다음 클릭 **다음**합니다.  

9. **설치 선택 확인** 페이지에서 **설치**를 클릭합니다.  

10. **결과** 페이지에서 **설치 완료**가 표시되는지 확인하고 **이 서버를 도메인 컨트롤러로 승격**을 클릭하여 Active Directory Domain Services 구성 마법사를 시작합니다.  

    > [!IMPORTANT]  
    > 이 시점에서 Active Directory 도메인 서비스 구성 마법사를 시작하지 않고 역할 추가 마법사를 닫은 경우 서버 관리자에서 [작업]을 클릭하여 이 마법사를 다시 시작할 수 있습니다.  

    (media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  

11. **배포 구성** 페이지에서 **기존 도메인에 도메인 컨트롤러 추가**를 클릭하고 도메인 이름(예: emea.contoso.com) 및 자격 증명(예: RODC를 관리 및 설치하도록 위임된 계정 지정)을 입력한 후 **다음**을 클릭합니다.  

12. **도메인 컨트롤러 옵션** 페이지에서 **기존 RODC 계정 사용**을 클릭하고 디렉터리 서비스 복원 모드 암호를 입력 및 확인한 후 **다음**을 클릭합니다.  

13. 에 **추가 옵션** 페이지에서 미디어에서 설치 하는 경우 클릭 **미디어 경로에서 설치** 입력 하 고 설치 원본 파일의 경로를 확인, 도메인 컨트롤러에서 AD DS 설치 데이터를 복제 (또는 마법사 도메인 컨트롤러를 선택 하도록 허용) 하려는 선택 클릭 하 고 **다음**합니다.  

14. 에 **경로** 페이지, Active Directory 데이터베이스, 로그 파일 및 SYSVOL 폴더에 대 한 위치를 입력 하거나 기본 위치를 적용 한 다음 클릭 **다음**합니다.  

15. **검토 옵션** 페이지에서 선택한 항목을 확인한 후 **스크립트 보기**를 클릭하여 Windows PowerShell 스크립트로 설정을 내보낸 후 **다음**을 클릭합니다.  

16. 에 **필수 구성 요소 확인** 페이지 해당 필수 구성 요소 유효성 검사 완료를 확인 한 다음 클릭 **설치**합니다.  

    AD DS 설치를 완료하기 위해 서버가 자동으로 다시 시작됩니다.  

## <a name="see-also"></a>관련 항목  
[도메인 컨트롤러 배포 문제 해결](Troubleshooting-Domain-Controller-Deployment.md)  
[새 Windows Server 2012 Active Directory 포리스트 &#40;수준 200 설치&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)  
[새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 &#40;수준 200 설치&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
[기존 도메인 &#40;수준 200에 복제 Windows Server 2012 도메인 컨트롤러를 설치 합니다.&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  




