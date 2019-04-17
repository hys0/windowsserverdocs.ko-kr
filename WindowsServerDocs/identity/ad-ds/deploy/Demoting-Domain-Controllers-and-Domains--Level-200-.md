---
ms.assetid: 65ed5956-6140-4e06-8d99-8771553637d1
title: "내리기 도메인 컨트롤러 및 도메인 (200 수준)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c254a01da5534c1ddc673bc1e60382c166ddeda7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="demoting-domain-controllers-and-domains-level-200"></a>내리기 도메인 컨트롤러 및 도메인 (200 수준)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목 제거 AD DS 서버 관리자 또는 Windows PowerShell 사용 하는 방법에 설명 합니다.  
  
-   [AD DS 제거 워크플로](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_Workflow)  
  
-   [수준 내리기 및 Windows PowerShell 역할 제거](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_PS)  
  
-   [내리기](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_Demote)  
  
## <a name="BKMK_Workflow"></a>AD DS 제거 워크플로  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/adds_demotedomainforest.png)  
  
> [!CAUTION]  
> Dism.exe 또는 Windows PowerShell DISM 모듈 AD DS 역할을 제거 하 후 도메인 컨트롤러에 프로 모션은 지원 되지 않으며 서버 정상적으로 부팅 되지 것입니다.  
>   
> 서버 관리자 또는 ADDSDeployment Windows PowerShell 모듈 달리 DISM는 기본 서비스 시스템 하지 못하므로 AD DS 또는 구성을입니다. 서버를 더 이상 도메인 컨트롤러 없으면 AD DS 역할을 제거 하려면 Dism.exe 또는 Windows PowerShell DISM 모듈 사용 하지 마십시오.  
  
## <a name="BKMK_PS"></a>수준 내리기 및 Windows PowerShell 역할 제거  
  
|||  
|-|-|  
|**ADDSDeployment 및 ServerManager Cmdlet**|인수 (**굵게** 인수가 필요 합니다. *기울임꼴로 표시* 인수 Windows PowerShell 또는 광고 DS 구성 마법사를 사용 하 여 지정할 수 있습니다.)|  
|Uninstall-AddsDomainController|-SkipPreChecks<br /><br />*-LocalAdministratorPassword*<br /><br />-확인<br /><br />***자격 증명***<br /><br />-DemoteOperationMasterRole<br /><br />*-DNSDelegationRemovalCredential*<br /><br />힘<br /><br />*-ForceRemoval*<br /><br />*-IgnoreLastDCInDomainMismatch*<br /><br />*-IgnoreLastDNSServerForZone*<br /><br />*-LastDomainControllerInDomain*<br /><br />-Norebootoncompletion<br /><br />*-RemoveApplicationPartitions*<br /><br />*-RemoveDNSDelegation*<br /><br />-RetainDCMetadata|  
|제거-WindowsFeature/제거-WindowsFeature|***이름***<br /><br />***-IncludeManagementTools***<br /><br />*다시 시작*<br /><br />-제거 합니다.<br /><br />힘<br /><br />-ComputerName<br /><br />자격 증명<br /><br />-LogPath<br /><br />-Vhd|  
  
> [!NOTE]  
> **-자격 증명** 인수가 경우 하지 이미 로그온 (도메인에 있는 마지막 DC 내리기) Enterprise 관리자 그룹의 회원으로 필수 또는 (복제본 DC).The **-includemanagementtools** 인수는만 AD DS 관리 유틸리티를 모두 제거 하려는 경우 필요 합니다.  
  
## <a name="BKMK_Demote"></a>내리기  
  
### <a name="remove-roles-and-features"></a>역할 및 기능을 제거  
서버 관리자 Active Directory Domain Services 역할을 제거 하기 위해 두 인터페이스를 제공 합니다.  
  
-   **관리** 주 대시보드에서 메뉴를 사용 하 여 **역할 제거 및 기능**  
  
 ![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Manage.png)  
  
-   클릭 **AD DS** 또는 **모든 서버** 탐색 창에서 합니다. 아래로 스크롤하여는 **역할 및 기능** 섹션. 마우스 오른쪽 단추로 클릭 **Active Directory Domain Services** 에 **역할 및 기능** 목록을 클릭 한 **역할 제거 또는 기능**합니다. 이 인터페이스 건너뛰고는 **서버 선택** 페이지 합니다.  
  
 ![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection.png)  
  
ServerManager cmdlet **제거 WindowsFeature** 및 **제거 WindowsFeature** 가 도메인 컨트롤러 내릴 때까지 AD DS 역할을 제거 하면 됩니다.  
  
### <a name="server-selection"></a>서버 선택  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection2.png)  
  
**서버 선택** 대화 상자를 사용 하는 것과 이전에 풀에 추가 하는 서버 중 하나를 선택할 수 있습니다. 서버 관리자 실행 하는 로컬 서버는 항상 자동으로 사용할 수 있습니다.  
  
### <a name="server-roles-and-features"></a>서버 역할 및 기능  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerRoles.png)  
  
지우기는 **Active Directory Domain Services** 도메인 컨트롤러; 내리기 하려면 확인란 도메인 컨트롤러 서버 현재 경우이 AD DS 역할 제거 되지는 않습니다 고 전환 하는 대신는 **유효성 검사 결과** 대화를 제공 합니다. 그렇지 않으면 다른 역할 기능 등 바이너리 간단 하 게 제거합니다.  
  
-   도메인 컨트롤러의 즉시 다시 수준을 하려는 경우 다른 광고 DS 관련 역할 또는 DNS, GPMC RSAT 도구-등 기능-를 제거 하지 않습니다. 다시 홍보 시간이 서버 관리자 역할을 다시 설치 하면 이러한 기능을 다시 설치 증가 추가 역할 및 기능을 제거 합니다.  
  
-   도메인 컨트롤러를 영구적으로 내리기 하려는 경우 불필요 한 AD DS 역할와 사용자의 판단에 기능을 제거 합니다. 이렇게 하려면 해당 역할 및 기능에 대 한 확인란의 선택을 취소 합니다.  
  
    광고 DS 관련 역할와 기능의 전체 목록은 다음과 같습니다.  
  
    -   Windows PowerShell 기능에 대 한 active Directory 모듈  
  
    -   AD DS 및 광고 LDS 도구 기능  
  
    -   Active Directory 관리 센터 기능  
  
    -   AD DS 명령줄 도구 및 스냅인 기능  
  
    -   DNS 서버  
  
    -   그룹 정책 관리 콘솔  
  
해당 하는 ADDSDeployment 및 ServerManager Windows PowerShell cmdlet는 다음과 같습니다.  
  
```  
Uninstall-addsdomaincontroller  
Uninstall-windowsfeature  
  
```  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_RemoveFeatures.png)  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demote.png)  
  
### <a name="credentials"></a>자격 증명  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Credentials.png)  
  
수준 내리기 옵션에서 구성는 **자격 증명** 페이지 합니다. 다음 목록에서 내릴는 데 필요한 자격 증명을 제공 합니다.  
  
-   추가 도메인 컨트롤러 내리기 도메인 관리자 자격 증명을 해야 합니다. 선택 **강제로이 도메인 컨트롤러의 제거** 도메인 컨트롤러에서 Active Directory 도메인 컨트롤러 개체 메타 데이터를 제거 하지 않고 내립니다.  
  
    > [!WARNING]  
    > 도메인 컨트롤러 다른 도메인 컨트롤러에 연결할 수 없는 고 경우가 아니면이 옵션을 선택 하지 않으면 *적절 한 방법이* 해당 네트워크 문제를 해결 해야 합니다. 강제 수준 내리기 Active Directory에는 숲 속의 나머지 도메인 컨트롤러에서 고아 메타 데이터를 전송 됩니다. 또한, 모든 없다고 복제 변경 새 사용자 계정 또는 암호와 같은 해당 도메인 컨트롤러 손실 됩니다 렉. 고아 메타 데이터 AD DS, Exchange, SQL, 및 기타 소프트웨어에 대 한 Microsoft 고객 지원의 경우의 중요 한 비율로 근본 원인입니다.  
    >   
    > 도메인 컨트롤러 수준을 강제로 경우 하면 *해야* 수동으로 바로 정리 메타 데이터를 수행 합니다. For steps, review [Clean Up Server Metadata](https://technet.microsoft.com/library/cc816907(WS.10).aspx).  
  
   ![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ForceDemote.png)  
  
-   이렇게 하면 도메인 자체 제거 엔터프라이즈 관리자 그룹 구성원 필요 도메인에 있는 마지막 도메인 컨트롤러 내리기 (제거이 숲은 마지막 도메인 숲). 서버 관리자 현재 도메인 컨트롤러 도메인에 있는 마지막 도메인 컨트롤러 인지를 알려줍니다. 선택는 **도메인에 있는 마지막 도메인 컨트롤러** 도메인 컨트롤러를 확인 하려면 확인란 도메인에 있는 마지막 도메인 컨트롤러입니다.  
  
해당 하는 ADDSDeployment Windows PowerShell 인수는 다음과 같습니다.  
  
```  
-credential <pscredential>  
-forceremoval <{ $true | false }>  
-lastdomaincontrollerindomain <{ $true | false }>  
  
```  
  
### <a name="warnings"></a>경고  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Warnings.png)  
  
**경고** 페이지 권한은 제거 하는이 도메인 컨트롤러에 표시 됩니다. 계속 하려면 **제거 된 계속**합니다.  
  
> [!WARNING]  
> 선택한 경우 **강제로이 도메인 컨트롤러의 제거** 에 **자격 증명** 페이지에서 다음 **경고** 페이지에는이 도메인 컨트롤러에서 주최한 모든 단일 마스터 작업 유연한 역할 표시 합니다. 사용자 *해야* 다른 도메인 컨트롤러에서 역할을 중단 *즉시* 이 서버 내리기 후 합니다. 에 대 한 자세한 내용은 FSMO 역할 중단, [마스터 작업의 역할을 중단](https://technet.microsoft.com/library/cc816779(WS.10).aspx)합니다.  
  
이 페이지에는 해당 ADDSDeployment Windows PowerShell 인수 없습니다.  
  
### <a name="removal-options"></a>제거 옵션  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ReviewOptions.png)  
  
**제거 옵션** 페이지가 나타나면 선택 하면 이전에 따라 **도메인에 있는 마지막 도메인 컨트롤러** 에 **자격 증명** 페이지 합니다. 이 페이지에서는 추가 제거 옵션 구성할 수 있습니다. 선택 **영역에 대 한 마지막 DNS 서버를 무시**, **응용 프로그램 파티션을 제거**, 및 **DNS 위임 제거** 에 노출 될 수 있는 **다음** 단추.  
  
옵션에는이 도메인 컨트롤러에 해당 하는 경우에 나타납니다. 예를 들어이 서버에 대 한 DNS 위임 없는 경우 다음 해당 확인란이 표시 되지 않습니다.  
  
클릭 **변경** 대체 DNS 관리자 자격 증명을 지정할 수 있습니다. 클릭 **보기 파티션을** 마법사를 제거 하는 동안 수준 내리기 추가 파티션을 볼 수 있습니다. 기본적으로만 추가 파티션을 DNS 도메인와 숲 DNS 영역 됩니다. 다른 모든 파티션을 비 Windows 파티션이 됩니다.  
  
해당 하는 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```  
-ignorelastdnsserverforzone <{ $true | false }>  
-removeapplicationpartitions <{ $true | false }>  
-removednsdelegation <{ $true | false }>  
-dnsdelegationremovalcredential <pscredential>  
```  
  
### <a name="new-administrator-password"></a>새로운 관리자 암호  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_NewAdminPwd.png)  
  
**새 관리자 암호** 페이지 수준 내리기 완료 하 고 컴퓨터 구성원 서버 도메인 또는 작업 그룹 컴퓨터 되 면 내장 로컬 컴퓨터의 관리자 계정에 대 한 암호를 제공 하도록 요구 합니다.  
  
**제거 ADDSDomainController** cmdlet 및 인수 서버 관리자로 서 같은 기본 설정을 지정 되지 않은 경우 따릅니다.  
  
**LocalAdministratorPassword** 인수 특별 한는 다음과 같습니다.  
  
-   하는 경우 *지정 하지* 를 인수로 다음 cmdlet 묻는 메시지를 입력 하 고 마스크 암호를 확인 합니다. Cmdlet 대화식으로 실행 될 때 이것이 기본 설정된 사용  
  
-   지정 된 경우 *값*, 값 보안 문자열 여야 합니다. 이것이 기본 설정된 사용 cmdlet 대화식으로 실행 될 때  
  
예를 들어, 요청할 수 있습니다 수동으로 암호를 사용 하 여는 **읽기 호스트** cmdlet에 대 한 보안 문자열 묻는  
  
```  
-localadministratorpassword (read-host -prompt "Password:" -assecurestring)  
  
```  
  
> [!WARNING]  
> 주의 사용 하는 이전 두 가지 옵션이 암호 확인 하지 않으면,으로: 암호 보이지 않으면  
  
또한이 것이 좋음 있지만 변환 일반 텍스트 변수와 보안 문자열을 제공할 수 있습니다. 예를 들어:  
  
```  
-localadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
  
```  
  
> [!WARNING]  
> 하지 암호화 되지 않은 텍스트 암호를 저장 하거나 제공 하는 것이 좋습니다. 이 명령을 스크립트에서 실행 또는이 기사를 통해 모든 사용자 해당 컴퓨터의 로컬 관리자 암호를 알고 있습니다. 이 정보를 모든 데이터에 액세스할 수 있는 하며 서버 자체 가장 수 있습니다.  
  
### <a name="confirmation"></a>확인  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Confirmation.png)  
  
**확인** 페이지에 표시 된 계획 된 수준 내리기; 페이지 수준 내리기 구성 옵션 목록이 표시 되지 않습니다. 마법사가 수준 내리기 시작 하기 전에 표시 마지막 페이지입니다. 스크립트 보기 단추 수준 내리기 Windows PowerShell 스크립트를 만듭니다.  
  
클릭 **내리기** 다음 AD DS 배포 cmdlet를 실행 하려면:  
  
```  
Uninstall-DomainController  
  
```  
  
옵션을 사용 하 여 **Whatif** 인수의 **제거 ADDSDomainController** cmdlet 구성 정보를 검토 하 고 있습니다. 이 cmdlet 인수 명시적 및 암묵적인 값을 볼 수 있습니다.  
  
예를 들어:  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstall.png)  
  
다시 시작 하 라는 메시지 ADDSDeployment Windows PowerShell를 사용 하는 경우이 작업을 취소 하 여 마지막 기회입니다. 해당 메시지를 무시 하려면는 **-강제로** 또는 **확인: $false** 인수 합니다.  
  
### <a name="demotion"></a>수준 내리기  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demotion.png)  
  
때는 **수준 내리기** 페이지에 표시, 도메인 컨트롤러 구성 시작 되 고 하거나 수 없는 중단 취소 합니다. 자세한 작업이이 페이지에 표시 되며, 로그에 기록 합니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
이후 **제거 AddsDomainController** 및 **제거 WindowsFeature** 만 시스템이 각각 한 조치는에서 확인 단계는 최소 인수와 여기 표시 됩니다. ENTER 키를 누르는 취소할 수준 내리기 프로세스를 시작 하 고 컴퓨터를 다시 시작 합니다.  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallConfirm.png)  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallWindowsFeature.png)  
  
다시 부팅 메시지를 자동으로 동의를 사용 하 여는 **-강제로** 또는 **-확인: $false** 인수 모든 ADDSDeployment Windows PowerShell cmdlet 사용 합니다. 서버 끝 프로 모션에 자동으로 다시 부팅 되지 않도록 하려면 사용는 **-norebootoncompletion: $false** 인수 합니다.  
  
> [!WARNING]  
> 다시 부팅 재정의 것이 좋습니다. 구성원 서버 제대로 작동 하려면 다시 부팅 해야 합니다.  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallFinished.png)  
  
최소 필요한 인수 내리기 강제로의 예는 다음과 같습니다 **-forceremoval** 및 **-demoteoperationmasterrole**합니다. **-자격 증명** Enterprise 관리자 그룹의 회원으로 로그온 인수 필요 하지 않습니다.  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleForce.png)  
  
다음은 마지막 도메인 컨트롤러의 최소 필요한 인수 된 도메인의 제거 예 **-lastdomaincontrollerindomain** 및 **-removeapplicationpartitions**:  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleLastDC.png)  
  
서버 내리기 하기 전에 AD DS 역할 제거 하려고 하면 Windows PowerShell 의도적 오류 차단 합니다.  
  
```  
Uninstall-WindowsFeature : An uninstallation prerequisite step failed duringthe removal of AD-Domain-Services, and uninstallation cannot continue.1. The domain controller needs to be demoted before the Active DirectoryDomain Services Role can be uninstalled.  
```  
  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallError.png)  
  
> [!IMPORTANT]  
> 광고 도메인 서비스 역할 이진 파일을 제거 하려면 먼저 서버 내리기 후 컴퓨터를 다시 시작 해야 합니다.  
  
### <a name="results"></a>결과  
![DC 내리기](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_DemoteSignoff.png)  
  
**결과** 프로 모션 및 관리 중요 한 정보가의 성공 여부 페이지에 표시 됩니다. 도메인 컨트롤러 10 초 후 자동으로 다시 부팅 됩니다.  
  

