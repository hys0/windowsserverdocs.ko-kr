---
ms.assetid: 66fa945e-598d-4f18-b603-97a39ce0d836
title: "Windows Server 2012 Active Directory 설치 Read-Only RODC (도메인 컨트롤러) (200 수준)"
description: "이 항목에서는 RODC 준비 된 계정을 만들려면 다음 RODC 설치 하는 동안 서버를 해당 계정에 연결 하는 방법을 설명 합니다. 또한 단계적된 설치 수행 하지 않고도 RODC 설치 하는 방법에 설명 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 78281ca845f79955aaa25aa45394284c59e639cb
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-windows-server-2012-active-directory-read-only-domain-controller-rodc-level-200"></a>Windows Server 2012 Active Directory 설치 Read-Only RODC (도메인 컨트롤러) (200 수준)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 RODC 준비 된 계정을 만들려면 다음 RODC 설치 하는 동안 서버를 해당 계정에 연결 하는 방법을 설명 합니다. 또한 단계적된 설치 수행 하지 않고도 RODC 설치 하는 방법에 설명 합니다.  
  
## <a name="stage-rodc-workflow"></a>단계 RODC 워크플로  
준비만 도메인 컨트롤러 (RODC) 설치 작동 두 이산 단계로 읽기:  
  
1.  빈된 컴퓨터 계정을 준비  
  
2.  프로 모션 중 RODC 해당 계정에 연결  
  
다음 그림 Active Directory 도메인 서비스 전용 도메인 컨트롤러 준비 과정을 Active Directory 관리 센터 (Dsac.exe)를 사용 하는 도메인에 빈 RODC 컴퓨터 계정 만들기를 나타냅니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stagedcreation.png)  
  
## <a name="BKMK_StagePS"></a>단계 RODC Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수 (**굵게** 인수가 필요 합니다. *기울임꼴로 표시* 인수 Windows PowerShell 또는 광고 DS 구성 마법사를 사용 하 여 지정할 수 있습니다.)|  
|추가 addsreadonlydomaincontrolleraccount|-SkipPreChecks<br /><br />***-DomainControllerAccountName***<br /><br />***-도메인 이름***<br /><br />***-SiteName***<br /><br />*-AllowPasswordReplicationAccountName*<br /><br />***자격 증명***<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-DenyPasswordReplicationAccountName*<br /><br />*-NoGlobalCatalog*<br /><br />*-InstallDNS*<br /><br />-ReplicationSourceDC|  
  
> [!NOTE]  
> **-자격 증명** 인수는만 경우 하지 이미 로그온 도메인 관리자 그룹의 회원으로 필요 합니다.  
  
## <a name="attach-rodc-workflow"></a>RODC 워크플로 연결  
아래 다이어그램 이미 설치한 AD DS 역할, Active Directory 도메인 서비스 구성 프로세스를 보여 줍니다. RODC 계정을 준비 하 고 시작 **도메인 컨트롤러이 서버 홍보** 서버 관리자를 사용 하 여 컴퓨터 준비 된 계정에 연결 하는 기존 도메인에 새 RODC 만들 수 있습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stageddeploy_beta1.png)  
  
## <a name="BKMK_AttachPS"></a>Windows PowerShell RODC 연결  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수 (**굵게** 인수가 필요 합니다. *기울임꼴로 표시* 인수 Windows PowerShell 또는 광고 DS 구성 마법사를 사용 하 여 지정할 수 있습니다.)|  
|설치 AddsDomaincontroller|-SkipPreChecks<br /><br />***-도메인 이름***<br /><br />*-SafeModeAdministratorPassword*<br /><br />*-ApplicationPartitionsToReplicate*<br /><br />*-CreateDNSDelegation*<br /><br />***자격 증명***<br /><br />-CriticalReplicationOnly<br /><br />*-데이터베이스 경로*<br /><br />*-DNSDelegationCredential*<br /><br />*-InstallationMediaPath*<br /><br />*-LogPath*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />***-UseExistingAccount***|  
  
> [!NOTE]  
> **-자격 증명** 인수는만 경우 하지 이미 로그온 도메인 관리자 그룹의 회원으로 필요 합니다.  
  
## <a name="staging"></a>준비  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_PreCreateRODC.png)  
  
Active Directory 관리 센터를 열어 읽기 전용 도메인 컨트롤러 컴퓨터 계정의 준비 작업을 수행 (**Dsac.exe**). 탐색 창에서는 도메인의 이름을 클릭 합니다. 두 번 클릭 **도메인 컨트롤러** 관리 목록에서입니다. 클릭 **읽기 전용 도메인 컨트롤러 계정 만들기 미리** 작업 창에서 합니다.  
  
Active Directory 관리 센터에 대 한 자세한 내용은 참조 [AD 고급 DS 관리를 사용 하 여 Active Directory 관리 센터 & #40; 200 수준 & #41; ](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md) 검토 하 고 [Active Directory 관리 센터: 시작](https://technet.microsoft.com/library/dd560651(WS.10).aspx)합니다.  
  
환경을 만드는 읽기 전용 도메인 컨트롤러를 사용 하는 경우 설치 마법사를 볼 수 있는 오래 된 Active Directory 사용자와 컴퓨터 스냅인 Windows Server 2008에서 사용 하는 경우 동일한 그래픽 인터페이스는와 같은 코드를 사용 하는 오래 된 dcpromo unattend 파일 형식으로 구성 내보내기 포함를 사용 하 여 알게  
  
Windows Server 2012 새 ADDSDeployment cmdlet stage RODC 컴퓨터 계정에 있지만 마법사 cmdlet 작업에 대 한 사용 하지 않습니다. 다음 섹션와 관련 된 정보를 각 이해 하기 쉽게 설정 하려면 해당 cmdlet 및 인수를 표시 합니다.  
  
**읽기 전용 도메인 컨트롤러 계정 만들기 미리** Active Directory 관리 센터 작업 창에서 링크 ADDSDeployment Windows PowerShell cmdlet에 해당 하는 다음과 같습니다.  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
### <a name="welcome"></a>시작  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_WelcomeStage1.png)  
  
**Active Directory 도메인 Services 설치 마법사를 시작** 대화 상자에 이름의 옵션 중 하나는 **사용 고급 모드 설치**합니다. 이 옵션을 선택 하 고 클릭 **다음** 암호 복제 정책 옵션을 표시 합니다. (나중에이 섹션에 자세히 설명 되어) 암호 복제 정책 옵션에 대 한 기본값을 사용 하려면이 옵션을 선택 취소 합니다.  
  
### <a name="network-credentials"></a>네트워크 자격 증명  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Creds.png)  
  
도메인 이름 옵션에는 **네트워크 자격 증명** 대화 Active Directory 관리 센터의 대상 도메인 기본적으로 표시 됩니다. 현재 자격 증명은 기본적으로 사용 됩니다. 도메인 관리자 그룹의 회원 포함 되지 않는다는 점을 클릭 **대체 자격 증명**를 클릭 하 고 **설정** 마법사 사용자 이름 및 암호 도메인 관리자의 회원을 제공 하기 위해 합니다.  
  
해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-credential <pscredential>  
```  
  
유념 준비 시스템 Windows Server 2008 R2 내에서 직접 포트 이며 새 Adprep 기능을 제공 하지 않습니다. 준비 된 RODC 계정을 배포를 계획 하는 경우 먼저 자동 rodcprep 작업 실행 되도록 도메인에 준비 된 없다고 RODC를 배포 하거나 수동으로 adprep.exe /rodcprep을 처음 실행 합니다.  
  
그렇지 않은 경우 "됩니다"adprep /rodcprep"실행 되지 않았습니다 때문에이 도메인에 있는 읽기 전용 도메인 컨트롤러 설치할" 오류가 발생 합니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepNotRunError.png)  
  
### <a name="specify-the-computer-name"></a>컴퓨터 이름 지정  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1CompName.png)  
  
**컴퓨터 이름 지정** 대화의 단일 레이블 입력 해야 **컴퓨터 이름을** 존재 하지 않는 도메인 컨트롤러의 합니다. 프로 모션 작업은 준비 계정을 검색 하지 않아서 또는 구성 하 고 나중에이 계정에 연결 하는 도메인 컨트롤러 이름이 같은 있어야 합니다.  
  
해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-domaincontrolleraccountname <string>  
```  
  
### <a name="select-a-site"></a>사이트를 선택 합니다.  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Site.png)  
  
**사이트 선택** 대화 상자에 현재 숲에 대 한 Active Directory 사이트 목록을 표시 합니다. 준비 된 읽기 전용 도메인 컨트롤러 작업 한 사이트 목록에서 선택 해야 합니다. RODC이이 정보를 사용 하 여 구성 파티션에 NTDS 설정 개체 만들고 배포 되 고 후 처음으로 시작 되 면 올바른 사이트에 참여 합니다.  
  
해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-sitename <string>  
```  
  
### <a name="additional-domain-controller-options"></a>추가 도메인 컨트롤러 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DCOptions.png)  
  
**추가 도메인 컨트롤러 옵션** 대화 상자를 사용 하면 도메인 컨트롤러로 실행 포함 지정 하는 **DNS 서버** 와 **드**합니다. 읽기 전용 도메인 컨트롤러 모두 기본적으로 설치 되므로 DNS 및 GC 서비스를 제공 하는 것이 좋습니다. 한 RODC 역할의는 지점 시나리오 다양 한 영역에서 네트워크를 사용할 수 없습니다 하 고 해당 DNS 및 드 서비스를 않고도, 지점에 컴퓨터 AD DS 리소스 기능을 사용할 수 없게 됩니다.  
  
**읽기 전용 RODC (도메인 컨트롤러)** 옵션 미리 선택 하 고 해제할 수 없습니다. 해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-installdns <string>  
-NoGlobalCatalog <{$true | $false}>  
  
```  
  
> [!NOTE]  
> 기본적으로는 **-NoGlobalCatalog** 값이 $false 인수 지정 하지 않은 경우 도메인 컨트롤러 서버 드 됩니다 의미 합니다.  
  
### <a name="specify-the-password-replication-policy"></a>지정 암호 복제 정책  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRP.png)  
  
**암호 복제 정책 지정** 대화 상자에서는이 읽기 전용 도메인 컨트롤러에서 암호를 캐시 수 있는 계정 기본 목록 수정할 수 있습니다. 구성 된 목록에서 계정을 **거부** 에 있지 않은 또는 (암시적) 목록 암호 캐시 하지 않습니다. 계정 RODC에 대 한 캐시 암호를 사용할 수 없습니다 및 수 없는 연결 하 고 쓸 수 있는 도메인 컨트롤러에 인증 리소스 또는 Active Directory에 제공한 기능에 액세스할 수 없습니다.  
  
> [!IMPORTANT]  
> 마법사가 선택 하는 경우이 대화 상자 표시는 **사용 고급 모드 설치** 시작 화면에 확인란을 선택 합니다. 이 확인란의 선택을 취소 하는 경우 기본 그룹와 값 마법사 사용 합니다.  
>   
> -   관리자 거부  
> -   서버 운영자-거부  
> -   백업 관리자-거부  
> -   계정 연산자-거부  
> -   거부 RODC 암호 복제 그룹-거부 되었습니다.  
> -   허용 RODC 암호 복제 그룹-허용  
  
해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRPAllow.png)  
  
### <a name="delegation-of-rodc-installation-and-administration"></a>위임 RODC 설치 및 관리  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DelegateAdmin.png)  
  
**RODC 위임 설치 및 관리** 대화 사용자 또는 그룹 서버 RODC 컴퓨터 계정에 연결할 수 있는 사용자가 포함 된 구성할 수 있습니다. 클릭 **설정** 사용자 또는 그룹에 대 한 도메인 찾아볼 수 있습니다. 사용자 또는 그룹이 대화 향상 로컬 하려면 관리자 권한이 RODC에 지정 합니다. 지정 된 사용자 또는 그룹의 회원 권한 해당 하는 컴퓨터의 관리자가 그룹으로 RODC에서 작업을 수행할 수 있습니다. 이들은 *하지* 도메인 관리자 또는 도메인 기본 관리자가 그룹의 회원 합니다.  
  
분기 office 관리 분기 관리자 멤버십 도메인 관리자 그룹 허용 하지 않고 위임 하려면이 옵션을 사용 합니다. RODC 관리 위임 필요 하지 않습니다.  
  
해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
### <a name="summary"></a>요약  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Summary.png)  
  
**요약** 대화 상자를 사용 하면 설정을 확인 합니다. 마법사가 준비 계정을 만든 하기 전에 설치를 중단 하는 지난 기회입니다. 클릭 **다음** 준비 RODC 컴퓨터 계정을 만드는 준비 되 면 합니다.  클릭 **내보내려면 설정** 오래 된 dcpromo unattend 파일 형식에 응답 파일을 저장 하 합니다.  
  
### <a name="creation"></a>만들기  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1InstallProgress.png)  
  
**Active Directory 도메인 Services 설치 마법사** Active Directory에 준비 된 읽기 전용 도메인 컨트롤러를 만듭니다. 시작 된 후에이 작업을 취소할 수 없습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Complete.png)  
  
다음 cmdlet 사용 하 여 사용 하 여 ADDSDeployment Windows PowerShell 모듈 읽기 전용 도메인 컨트롤러 컴퓨터 계정 준비.  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
참조 [단계 RODC Windows PowerShell](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_StagePS) 인수 필수 및 선택 사항에 대 한 합니다.  
  
때문에 **추가 addsreadonlydomaincontrolleraccount** 한 조치는 다음과 같은 스크린샷을 (필수 확인 하 고 설치) 2 단계와는 최소 인수와 설치 단계가 표시 됩니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODC.png)  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODCValidating.png)  
  
단계 RODC 작업 Active Directory에 RODC 컴퓨터 계정을 만듭니다. Active Directory 관리 센터 표시 되는 **도메인 컨트롤러 종류** 으로 **빈 도메인 컨트롤러 계정**합니다. 이 도메인 컨트롤러 유형 준비 RODC 계정을 읽기만 도메인 컨트롤러에 첨부할 서버에 대 한 준비가 나타냅니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Unoccupied.png)  
  
> [!IMPORTANT]  
> Active Directory 관리 센터는 더 이상 필요 서버 읽기 전용 도메인 컨트롤러 컴퓨터 계정에 연결 합니다. 서버 관리자를 사용 하 고 Active Directory 도메인 서비스 구성 마법사 또는 ADDSDeployment Windows PowerShell 모듈 cmdlet **설치 AddsDomainController** 새로운 RODC 준비 해당 계정에 연결 합니다. 단계 준비 RODC 컴퓨터 계정 RODC 컴퓨터 계정을 준비 된 때를 결정 구성 옵션에는 예외로 기존 도메인에 새 쓸 수 있는 도메인 컨트롤러를 추가 하는 것과 비슷합니다.  
  
## <a name="attaching"></a>연결  
  
### <a name="deployment-configuration"></a>배포 구성  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
서버 관리자 모든 도메인 컨트롤러 프로 모션으로 시작 되 고 **배포 구성** 페이지 합니다. 나머지 옵션과 필수 필드가 페이지에서 다음 페이지를 선택 하는 배포 작업에 따라 변경 됩니다.  
  
읽기 전용 도메인 컨트롤러에 기존 도메인을 추가 하려면 **도메인 컨트롤러 기존 도메인에 추가** 클릭 하 고 있는 **선택** 버튼 **도메인이이 도메인에 대 한 정보를 지정**합니다. 서버 관리자 자동으로 묻는 유효한 자격 증명을 하거나 클릭 하 여 **변경**합니다.  
  
Windows Server 2012에서 도메인 관리자 그룹의 회원이 필요 RODC 첨부 합니다. Active Directory 도메인 서비스 구성 묻는 메시지가 나중에 적절 한 권한이 또는 그룹 구성원 현재 자격 증명 되어 있지 않습니다.  
  
**배포 구성** ADDSDeployment Windows PowerShell cmdlet 및 인수는 다음과 같습니다.  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2DCOptions.png)  
  
**도메인 컨트롤러 옵션** 페이지 도메인 컨트롤러 옵션에 대 한 새 도메인 컨트롤러에 표시 됩니다. 이 페이지를 로드할 때 Active Directory 도메인 서비스 구성 마법사 LDAP 쿼리를 빈된 계정을 확인 하려면 기존 도메인 컨트롤러를 보냅니다. 쿼리 발견 빈된 도메인 컨트롤러 컴퓨터 계정 이름이 같은 현재 컴퓨터를 공유 하는 경우 다음 마법사 읽고 페이지의 맨 알림 메시지를 표시 "**대상 서버의 이름과 일치 하는 미리 작성된 된 RODC 계정을 디렉터리에 있습니다. 도메인 컨트롤러가 다시 설치 하거나 기존이 RODC 계정을 사용 하도록 선택할**. " 마법사를 사용 하는 **기존 RODC 계정을 사용 하 여** 기본 설정으로 합니다.  
  
> [!IMPORTANT]  
> 사용할 수 있는 **도메인 컨트롤러가 다시 설치** 옵션 도메인 컨트롤러 되었다는 실제 문제 및 기능으로 되돌릴 수 없습니다. 이 인해 컴퓨터 계정을 도메인 컨트롤러 두면 교체 도메인 컨트롤러를 구성할 때 시간과 메타 데이터 Active directory에서 개체 합니다. 새 컴퓨터에 설치는 *이름이 같은*, 도메인에 있는 도메인 컨트롤러 홍보 하 고 있습니다. **도메인 컨트롤러가 다시 설치** 옵션은 Active Directory (메타 데이터 정리)에서 도메인 컨트롤러 개체 메타 데이터를 제거 하는 경우 사용할 수 없습니다.  
  
서버 RODC 컴퓨터 계정에 연결 하는 경우 도메인 컨트롤러 옵션을 구성할 수 없습니다. 준비 된 RODC 컴퓨터 계정을 만들 때 도메인 컨트롤러 옵션을 구성 합니다.  
  
지정 된 **디렉터리 서비스 복원 모드 암호** 서버에 적용 암호 정책을 준수 해야 합니다. 항상 복잡 하 고 강력한 암호 또는 암호를 선택 합니다.  
  
**도메인 컨트롤러 옵션** ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> 인수로 제공 된 경우에 이미 사이트 이름이 있어야 **-sitename**합니다. **설치-AddsDomainController** cmdlet 사이트의 이름을 생성 하지 않습니다. Cmdlet 사용할 수 **새로운 adreplicationsite** 새 사이트를 만들 수 있습니다.  
  
**설치 ADDSDomainController** 인수 지정 되지 않은 경우 동일한 기본값 서버 관리자로 서을 따릅니다.  
  
**SafeModeAdministratorPassword** 특별 한 인수의 작업은 다음과 같습니다.  
  
-   하는 경우 *지정 하지* 를 인수로 cmdlet 묻는 메시지를 입력 하 고 마스크 암호를 확인 합니다. 기본 설정된 사용 cmdlet 대화식으로 실행 될 때입니다.  
  
    예를 들어, 하 고 있는 corp.contoso.com에서 새 RODC 만들기 하 라는 메시지가 표시 입력 하 고 마스크 비밀 번호를 확인 합니다.  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
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
  
### <a name="additional-options"></a>추가 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2AdditionalOptions.png)  
  
**추가 옵션** 페이지 구성 복제 원본으로 도메인 컨트롤러의 이름을 지정 하는 옵션이 제공 하거나 도메인 컨트롤러 복제 원본으로 사용할 수 있습니다.  
  
있습니다 하도록 선택할 수도 있는 도메인 컨트롤러를 사용 하 여 설치 미디어 (IFM) 옵션에서 설치를 사용 하 여 미디어를 백업 합니다. **설치 미디어에서** 확인란을 한 번 찾아보기 옵션을 선택 하 고 클릭 해야 제공 **확인** 제공된 경로 사용할 미디어 확인 하기 위해 합니다. IFM 옵션으로 사용 되는 미디어는 Windows Server 백업 또는 Ntdsutil.exe 컴퓨터에서 만든 다른 기존 Windows Server 2012만 사용 합니다. Windows Server 2012 도메인 컨트롤러에 대해 미디어를 만드는 Windows Server 2008 R2 또는 이전 운영 체제를 사용할 수 없습니다. 변경 IFM에 대 한 자세한 내용은 참조 [Ntdsutil.exe 설치 미디어 변경에서](../../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)합니다. 한 SYSKEY로 보호 된 미디어를 사용 하 여 확인 하는 동안 서버 관리자 이미지의 암호를 묻습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_StagedIFM.png)  
  
**추가 옵션** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>경로  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Paths.png)  
  
**경로** SYSVOL 공유 및 페이지 데이터베이스 트랜잭션 로그가 광고 DS 데이터베이스의 기본 폴더 위치를 무시할 수 있습니다. 기본 위치는 항상 하위 시스템 루트 %의입니다. **경로** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>스크립트 보기 및 리뷰 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2ReviewOptions.png)  
  
**리뷰 옵션** 페이지를 설정을 확인 하 고 설치를 시작 하기 전에 사용자의 요구 사항을 충족 시키는 확인 수 있습니다. 마지막 기회를 서버 관리자를 사용 하 고 설치를 중단 되었습니다. 이 페이지 간단 하 게 검토 하 고 설정을 구성 계속 하기 전에 확인 수 있습니다. **리뷰 옵션** 서버 관리자의 페이지도 선택적 제공 **스크립트 보기** 단추를 현재 ADDSDeployment 구성을 하나의 Windows PowerShell 스크립트도 포함 유니코드 텍스트 파일을 만듭니다. 서버 관리자 그래픽 인터페이스 Windows PowerShell 배포 studio로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용 하 여 옵션 구성 구성, 내보내고 마법사 취소 합니다. 이 프로세스 추가 수정 또는 직접 사용에 대해 유효 하 고 구문이 샘플을 만듭니다. 예를 들어:  
  
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
> 일반적으로 서버 관리자 모든 인수 및 (에 따라 수 향후 버전의 Windows 또는 서비스 팩 간에) 기본값에 의존 하지 않는 경우 값을 입력 합니다. 이 한 가지 예외는는 **-safemodeadministratorpassword** 인수 합니다. 강제로 프롬프트가 생략 값 cmdlet 대화식으로 실행 될 때  
  
옵션을 사용 하 여 **Whatif** 인수의 **설치 ADDSDomainController** cmdlet 구성 정보를 검토 합니다. 이렇게 하면 cmdlet에 대 한 인수 명시적 및 암묵적인 값을 볼 수 있습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2WhatIf.png)  
  
### <a name="prerequisites-check"></a>필수 확인  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2PrereqCheck.png)  
  
**필수 확인** 광고 DS 도메인 구성의 새로운 기능입니다. 이 새로운 단계 서버 구성 새 AD DS 숲 지원 확인 합니다.  
  
새 숲 루트 도메인을 설치할 때는 서버 관리자 Active Directory 도메인 서비스 구성 마법사 호출 일련의 연속된 모듈식 테스트 합니다. 이러한 테스트 제안 된 복구 옵션을 알립니다. 필요에 따라 여러 번 테스트를 실행할 수 있습니다. 도메인 컨트롤러 설치 프로세스를 모든 필수 테스트 될 때까지 계속 전달 됩니다.  
  
**필수 확인** 이전 운영 체제에 영향을 주는 보안 변경와 같은 관련 정보를 표면 수도 있습니다. 필수 검사에 대 한 자세한 내용은 참조 [필수 검사](../../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)합니다.  
  
무시할 수 없는 **필수 확인** 때 되는데 서버 관리자를 사용 하 여 건너뛸 수 프로세스 AD DS 배포 cmdlet 인수를 사용 하 여 사용 하는 경우:  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> Microsoft 부분 도메인 컨트롤러 프로 모션 발생할 수 있는 되거나 손상 AD DS 숲 필수 검사를 건너뛰는 것이 수 없게 됩니다.  
  
클릭 **설치** 도메인 컨트롤러 프로 모션 프로세스를 시작 합니다. 설치를 취소 하 마지막 기회입니다. 시작 된 후 프로 모션 프로세스를 취소할 수 없습니다. 컴퓨터가 끝 프로 모션 결과 관계 없이 프로 모션에 자동으로 재부팅 됩니다.  
  
### <a name="installation"></a>설치  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Installation.png)  
  
설치 페이지 표시 되 면 도메인 컨트롤러 구성 시작 하 고 하거나 수 없는 중단 취소 합니다. 자세한 작업이이 페이지에 표시 되며, 로그에 기록 합니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment 모듈을 사용 하 여 새 Active Directory 숲을 설치 하려면 다음 cmdlet 사용:  
  
```  
Install-addsdomaincontroller  
  
```  
  
참조 [RODC Windows PowerShell 연결](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_AttachPS) 인수 필수 및 선택 사항에 대 한 합니다.  
  
**설치 addsdomaincontroller** cmdlet (필수 확인 하 고 설치) 2 단계에 있습니다. 아래 두 그림 표시 설치 단계와의 최소는 인수 **-도메인 이름**, **-useexistingaccount**, 및 **-자격 증명**합니다. 참고 방법을 지난번 처럼 서버 관리자 **설치 ADDSDomainController** 프로 모션 서버 자동으로 재부팅을 미리 알려:  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2.png)  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2Complete.png)  
  
다시 부팅 메시지를 자동으로 동의를 사용 하 여는 **-강제로** 또는 **-확인: $false** 인수 모든 ADDSDeployment Windows PowerShell cmdlet 사용 합니다. 서버 끝 프로 모션에 자동으로 다시 부팅 되지 않도록 하려면 사용는 **-norebootoncompletion** 인수 합니다.  
  
> [!WARNING]  
> 다시 부팅 재정의 것이 좋습니다. 도메인 컨트롤러 제대로 작동 하려면 다시 부팅 해야 합니다.  
  
### <a name="results"></a>결과  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**결과** 프로 모션 및 관리 중요 한 정보가의 성공 여부 페이지에 표시 됩니다. 도메인 컨트롤러 10 초 후 자동으로 다시 부팅 됩니다.  
  
## <a name="rodc-without-staging-workflow"></a>준비 워크플로 없이 RODC  
다음 그림 AD DS 역할을 이전에 설치 되어 있고 Active Directory 도메인 서비스 구성 마법사 서버 관리자를 사용 하 여 기존 Windows Server 2012 도메인에 새 비 준비 읽기 전용 도메인 컨트롤러를 만들기 시작 때 Active Directory 도메인 서비스 구성 프로세스를 보여 줍니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_rodcdeploy.png)  
  
## <a name="rodc-without-staging-windows-powershell"></a>Windows PowerShell 준비를 않고도 RODC  
  
|||  
|-|-|  
|**ADDSDeployment Cmdlet**|인수 (**굵게** 인수가 필요 합니다. *기울임꼴로 표시* 인수 Windows PowerShell 또는 광고 DS 구성 마법사를 사용 하 여 지정할 수 있습니다.)|  
|설치 AddsDomainController|-SkipPreChecks<br /><br />***-도메인 이름***<br /><br />*-SafeModeAdministratorPassword*<br /><br />***-SiteName***<br /><br />*-ApplicationPartitionsToReplicate*<br /><br />*-CreateDNSDelegation*<br /><br />***자격 증명***<br /><br />*-CriticalReplicationOnly*<br /><br />*-데이터베이스 경로*<br /><br />*-DNSDelegationCredential*<br /><br />-DNSOnNetwork<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />*-NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-AllowPasswordReplicationAccountName*<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-DenyPasswordReplicationAccountName*<br /><br />***-ReadOnlyReplica***|  
  
> [!NOTE]  
> **-자격 증명** 인수는만 경우 하지 이미 로그온 도메인 관리자 그룹의 회원으로 필요 합니다.  
  
## <a name="rodc-without-staging-deployment"></a>준비 배포를 않고도 RODC  
  
### <a name="deployment-configuration"></a>배포 구성  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
서버 관리자 모든 도메인 컨트롤러 프로 모션으로 시작 되 고 **배포 구성** 페이지 합니다. 나머지 옵션과 필수 필드가 페이지에서 다음 페이지를 선택 하는 배포 작업에 따라 변경 됩니다.  
  
기존 Windows Server 2012 도메인에 있는 없다고 준비 읽기 전용 도메인 컨트롤러를 추가 하려면 **도메인 컨트롤러 기존 도메인에 추가** 클릭 하 고 있는 **선택** 버튼 **도메인이이 도메인에 대 한 정보를 지정**합니다. 서버 관리자 자동으로 묻는 유효한 자격 증명을 하거나 클릭 하 여 **변경**합니다.  
  
Windows Server 2012에서 도메인 관리자 그룹의 회원이 필요 RODC 첨부 합니다. Active Directory 도메인 서비스 구성 묻는 메시지가 나중에 적절 한 권한이 또는 그룹 구성원 현재 자격 증명 되어 있지 않습니다.  
  
**배포 구성** ADDSDeployment Windows PowerShell cmdlet 및 인수는 다음과 같습니다.  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDCOptions.png)  
  
**도메인 컨트롤러 옵션** 페이지 새 도메인 컨트롤러에 대 한 도메인 컨트롤러 기능을 지정 합니다. 가능한 도메인 컨트롤러 기능은 **DNS 서버**, **드**, 및 **읽기 전용 도메인 컨트롤러**합니다. 모든 도메인 컨트롤러 분산된 환경에서 사용 가능 하도록 DNS 및 GC 서비스를 제공 하는 것이 좋습니다. 기본적으로 GC은 항상 선택 하 고 현재 도메인 호스트 권한 시작 쿼리 기반 DNS 해당 Dc에 이미 있는 경우 DNS 서버 기본적으로 선택 됩니다.  
  
**도메인 컨트롤러 옵션** 페이지도 논리 적절 한 Active Directory를 선택할 수 있습니다 **사이트 이름** 숲 구성에서 합니다. 기본적으로 가장 적은 서브넷 사이트에서는 선택 합니다. 하나의 사이트가 경우 해당 사이트 자동으로 선택 됩니다.  
  
> [!IMPORTANT]  
> 서버 Active Directory 서브넷에 속하지 않는 경우 둘 이상의 Active Directory 사이트가 아무 것도 선택 및 **다음** 단추는 목록에서 사이트를 선택할 때까지 사용할 수 없습니다.  
  
지정 된 **디렉터리 서비스 복원 모드 암호** 서버에 적용 암호 정책을 준수 해야 합니다. 항상 복잡 하 고 강력한 암호 또는 암호를 선택 합니다. **도메인 컨트롤러 옵션** ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> 인수로 제공 된 경우에 이미 사이트 이름이 있어야 **-sitename**합니다. **설치-AddsDomainController** cmdlet 사이트의 이름을 생성 하지 않습니다. Cmdlet 사용할 수 **새로운 adreplicationsite** 새 사이트를 만들 수 있습니다.  
  
**설치 ADDSDomainController** 인수 지정 되지 않은 경우 동일한 기본값 서버 관리자로 서을 따릅니다.  
  
**SafeModeAdministratorPassword** 특별 한 인수의 작업은 다음과 같습니다.  
  
-   하는 경우 *지정 하지* 를 인수로 cmdlet 묻는 메시지를 입력 하 고 마스크 암호를 확인 합니다. 기본 설정된 사용 cmdlet 대화식으로 실행 될 때입니다.  
  
    예를 들어, 하 고 있는 corp.contoso.com에서 새 RODC 만들기 하 라는 메시지가 표시 입력 하 고 마스크 비밀 번호를 확인 합니다.  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
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
  
### <a name="rodc-options"></a>RODC 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCOptions.png)  
  
**RODC 옵션** 페이지 설정을 수정할 수 있습니다.  
  
-   위임된 관리자 계정  
  
-   암호 RODC 복제 하도록 허용 하는 계정  
  
-   암호를 RODC 복제 거부 된 계정  
  
위임된 관리자 계정 RODC 하려면 관리자 권한이 로컬 얻을 수 있습니다. 이러한 사용자가 로컬 컴퓨터의 관리자가 그룹에 해당 권한으로 작동할 수 있습니다.  도메인 관리자 나 도메인 기본 관리자가 그룹의 회원 하지 않습니다. 이 옵션은 도메인 관리자 권한으로 제공 하지 않고 분기 사무실 관리에 위임 하는 데 유용 합니다. 관리 위임 구성 필요 하지 않습니다.  
  
해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
계정 RODC에 대 한 캐시 암호를 사용할 수 없습니다 및 수 없는 연결 하 고 쓸 수 있는 도메인 컨트롤러에 인증 리소스 또는 Active Directory에 제공한 기능에 액세스할 수 없습니다.  
  
> [!IMPORTANT]  
> 수정 되지 기본 그룹과 설정 사용 됩니다.  
>   
> -   관리자 거부  
> -   서버 운영자-거부  
> -   백업 관리자-거부  
> -   계정 연산자-거부  
> -   거부 RODC 암호 복제 그룹-거부 되었습니다.  
> -   허용 RODC 암호 복제 그룹-허용  
  
해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_SelectDelAdmin.png)  
  
### <a name="additional-options"></a>추가 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCAdditionalOptions.png)  
  
**추가 옵션** 페이지 구성 복제 원본으로 도메인 컨트롤러의 이름을 지정 하는 옵션이 제공 하거나 도메인 컨트롤러 복제 원본으로 사용할 수 있습니다.  
  
있습니다 하도록 선택할 수도 있는 도메인 컨트롤러를 사용 하 여 설치 미디어 (IFM) 옵션에서 설치를 사용 하 여 미디어를 백업 합니다. **설치 미디어에서** 확인란을 한 번 찾아보기 옵션을 선택 하 고 클릭 해야 제공 **확인** 제공된 경로 사용할 미디어 확인 하기 위해 합니다. IFM 옵션으로 사용 되는 미디어는 Windows Server 백업 또는 Ntdsutil.exe 컴퓨터에서 만든 다른 기존 Windows Server 2012만 사용 합니다. Windows Server 2012 도메인 컨트롤러에 대해 미디어를 만드는 Windows Server 2008 R2 또는 이전 운영 체제를 사용할 수 없습니다.  부록은 IFM의 변경에 더 많은 정보를 제공 합니다. 한 SYSKEY로 보호 된 미디어를 사용 하 여 확인 하는 동안 서버 관리자 이미지의 암호를 묻습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSIFM.png)  
  
추가 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>경로  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPaths.png)  
  
**경로** SYSVOL 공유 및 페이지 데이터베이스 트랜잭션 로그가 광고 DS 데이터베이스의 기본 폴더 위치를 무시할 수 있습니다. 기본 위치는 항상 하위 시스템 루트 %의입니다. **경로** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>준비 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepOptions.png)  
  
**준비 옵션** 페이지에 표시 광고 DS 구성 스키마 (forestprep)를 확장 하 고 업데이트 하는 도메인 (도메인 준비)에 포함 됩니다. 이전 Windows Server 2012 도메인 컨트롤러 설치 하거나 수동으로 Adprep.exe 실행 숲 또는 도메인 준비 되지 않았습니다 때만이 페이지를 표시 합니다. 예를 들어, Active Directory 도메인 서비스 구성 마법사 표시 새 복제 도메인 컨트롤러 기존 Windows Server 2012 숲 루트 도메인에 추가 하는 경우이 페이지를 않습니다.  
  
스키마를 확장 하 고 업데이트 하는 도메인 클릭할 때 발생 하지 않으면 **다음**합니다. 이러한 이벤트 설치 단계 에서만 발생합니다. 이 페이지는 설치 나중에 발생 하는 행사에 대해 인식 간단 하 게 제공 됩니다.  
  
이 페이지도의 유효성을 검사 현재 사용자 자격 증명 스키마 관리자 및 Enterprise 관리자 그룹의 회원 있는 스키마 확장 하거나 도메인 준비 이러한 그룹의 회원 필요 합니다. 클릭 **변경** 페이지 알려 현재 자격 증명 충분 한 사용 권한을 제공 하지 않는 경우 사용자 자격 증명을 합니다.  
  
추가 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> 서 이전 버전의 Windows Server, Windows Server 2012 자동화 된 도메인 준비 실행 되지 않습니다 GPPREP. 실행 **adprep.exe /gpprep** 이전에 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 r 2에 대 한 준비 되지 된 모든 도메인에 대 한 수동으로 합니다. 모든 업그레이드를 하지는 도메인의 기록에 한 번만 GPPrep 실행 해야 합니다. 해당 작업 모든 도메인 컨트롤러에 다시 복제할 SYSVOL 폴더의 모든 파일 및 폴더를 시킬 수 있으므로 Adprep.exe /gpprep 자동으로 실행 되지 않습니다.  
>   
> 도메인의 첫 번째 없다고 준비 RODC 홍보 RODCPrep 자동 실행 됩니다. 첫 번째 쓰기 Windows Server 2012 도메인 컨트롤러 홍보 때 발생 하지 않습니다. 또한 수동으로 실행할 수 **adprep.exe /rodcprep** 읽기 전용 도메인 컨트롤러 배포를 계획 하는 경우입니다.  
  
### <a name="review-options-and-view-script"></a>스크립트 보기 및 리뷰 옵션  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCReviewOptions.png)  
  
**리뷰 옵션** 페이지를 설정을 확인 하 고 설치를 시작 하기 전에 사용자의 요구 사항을 충족 시키는 확인 수 있습니다. 마지막 기회를 서버 관리자를 사용 하 고 설치를 중단 되었습니다. 이 페이지 간단 하 게 검토 하 고 설정을 구성 계속 하기 전에 확인 수 있습니다.  
  
**리뷰 옵션** 서버 관리자의 페이지도 선택적 제공 **스크립트 보기** 단추를 현재 ADDSDeployment 구성을 하나의 Windows PowerShell 스크립트도 포함 유니코드 텍스트 파일을 만듭니다. 서버 관리자 그래픽 인터페이스 Windows PowerShell 배포 studio로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용 하 여 옵션 구성 구성, 내보내고 마법사 취소 합니다. 이 프로세스 추가 수정 또는 직접 사용에 대해 유효 하 고 구문이 샘플을 만듭니다. 예를 들어:  
  
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
> 일반적으로 서버 관리자 모든 인수 및 (에 따라 수 향후 버전의 Windows 또는 서비스 팩 간에) 기본값에 의존 하지 않는 경우 값을 입력 합니다. 이 한 가지 예외는는 **-safemodeadministratorpassword** 인수 합니다. 확인 메시지가 되도록 값을 생략 cmdlet 대화식으로 실행 될 때 합니다.  
  
선택적 Whatif 인수 구성 정보를 검토 설치 ADDSDomainController cmdlet 사용 합니다. 이렇게 하면 cmdlet에 대 한 인수 명시적 및 암묵적인 값을 볼 수 있습니다.  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCWhatIf.png)  
  
### <a name="prerequisites-check"></a>필수 확인  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrereqCheck.png)  
  
**필수 확인** 광고 DS 도메인 구성의 새로운 기능입니다. 이 새로운 단계 서버 구성 새 AD DS 숲 지원 확인 합니다.  
  
새 숲 루트 도메인을 설치할 때는 서버 관리자 Active Directory 도메인 서비스 구성 마법사 호출 일련의 연속된 모듈식 테스트 합니다. 이러한 테스트 제안 된 복구 옵션을 알립니다. 필요에 따라 여러 번 테스트를 실행할 수 있습니다. 도메인 컨트롤러 프로세스 수 없는 모든 필수 테스트까지 계속 제공 전달 됩니다.  
  
**필수 확인** 이전 운영 체제에 영향을 주는 보안 변경와 같은 관련 정보를 표면 수도 있습니다.  
  
무시할 수 없는 **필수 확인** 때 되는데 서버 관리자를 사용 하 여 건너뛸 수 프로세스 AD DS 배포 cmdlet 인수를 사용 하 여 사용 하는 경우:  
  
```  
-skipprechecks  
  
```  
  
클릭 **설치** 도메인 컨트롤러 프로 모션 프로세스를 시작 합니다. 설치를 취소 하 마지막 기회입니다. 시작 된 후 프로 모션 프로세스를 취소할 수 없습니다. 컴퓨터가 끝 프로 모션 결과 관계 없이 프로 모션에 자동으로 재부팅 됩니다.  
  
### <a name="installation"></a>설치  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCInstallation.png)  
  
때는 **설치** 페이지에 표시, 도메인 컨트롤러 구성 시작 되 고 하거나 수 없는 중단 취소 합니다. 자세한 작업이이 페이지에 표시 되며, 로그에 기록 합니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment 모듈을 사용 하 여 새 Active Directory 숲을 설치 하려면 다음 cmdlet 사용:  
  
```  
Install-addsdomaincontroller  
  
```  
  
참조는 **ADDSDeployment Cmdlet** 인수 필수 및 선택 사항에 대 한이 섹션의 begininng 테이블 합니다.  
  
**설치 addsdomaincontroller** cmdlet (필수 확인 하 고 설치) 2 단계에 있습니다. 아래 두 그림 표시 설치 단계와의 최소는 인수 **-도메인 이름**, **-readonlyreplica**, **-sitename**, 및 **-자격 증명**합니다. 참고 방법을 지난번 처럼 서버 관리자 **설치 ADDSDomainController** 프로 모션 서버 자동으로 재부팅을 미리 알려:  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODC.png)  
  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODCProgress.png)  
  
다시 부팅 메시지를 자동으로 동의를 사용 하 여는 **-강제로** 또는 **-확인: $false** 인수 모든 ADDSDeployment Windows PowerShell cmdlet 사용 합니다. 서버 끝 프로 모션에 자동으로 다시 부팅 되지 않도록 하려면 사용는 **-norebootoncompletion** 인수 합니다.  
  
> [!WARNING]  
> 다시 부팅 재정의 권장 하지 않습니다. 도메인 컨트롤러 제대로 작동 하려면 다시 부팅 해야 합니다. 도메인 컨트롤러 오프 로그인 할 경우 로그온 할 수 없습니다 다시 대화식으로 다시 시작 해야 합니다.  
  
### <a name="results"></a>결과  
![RODC 설치](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCSignoff.png)  
  
**결과** 프로 모션 및 관리 중요 한 정보가의 성공 여부 페이지에 표시 됩니다. 도메인 컨트롤러 10 초 후 자동으로 다시 부팅 됩니다.  
  

