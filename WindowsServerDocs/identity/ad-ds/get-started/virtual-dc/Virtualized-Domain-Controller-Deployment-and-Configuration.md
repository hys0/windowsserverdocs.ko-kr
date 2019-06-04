---
ms.assetid: b146f47e-3081-4c8e-bf68-d0f993564db2
title: 가상화된 도메인 컨트롤러 배포 및 구성
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d692e58d616376149e62fbce611fe2a9ac80c743
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863254"
---
# <a name="virtualized-domain-controller-deployment-and-configuration"></a>가상화된 도메인 컨트롤러 배포 및 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에는 다음 내용이 포함됩니다.  
  
-   [설치 고려 사항](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_InstallConsiderations)  
  
    플랫폼 요구 사항 및 기타 중요한 제약 조건을 포함합니다.  
  
-   [가상화 된 도메인 컨트롤러 복제](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCCloning)  
  
    전체 가상화된 도메인 컨트롤러 복제 프로세스에 대해 자세히 설명합니다.  
  
-   [가상화 된 도메인 컨트롤러 안전 복원](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCSafeRestore)  
  
    가상화된 도메인 컨트롤러 안전 복원 중에 수행되는 유효성 검사에 대해 자세히 설명합니다.  
  
## <a name="BKMK_InstallConsiderations"></a>설치 고려 사항  
가상화된 도메인 컨트롤러를 위해 특별히 설치해야 하는 역할이나 기능은 없습니다. 모든 도메인 컨트롤러에는 복제 및 안전 복원 기능이 자동으로 포함됩니다. 이러한 기능을 제거하거나 사용하지 않도록 설정할 수 없습니다.  
  
Windows Server 2012 도메인 컨트롤러를 사용하려면 Windows Server 2012 AD DS 스키마 버전 56 이상 및 Windows Server 2003 기본 모드 이상에 해당하는 포리스트 기능 수준이 필요합니다.  
  
쓰기 가능한 도메인 컨트롤러와 읽기 전용 도메인 컨트롤러 둘 다 글로벌 카탈로그 및 FSMO 역할과 마찬가지로 가상화된 DC의 모든 측면을 지원합니다.  
  
> [!IMPORTANT]  
> 복제를 시작할 때 PDC 에뮬레이터 FSMO 역할 소유자가 온라인 상태여야 합니다.  
  
### <a name="BKMK_PlatformReqs"></a>플랫폼 요구 사항  
가상화된 도메인 컨트롤러 복제에는 다음이 필요합니다.  
  
-   Windows Server 2012 DC에서 호스트되는 PDC 에뮬레이터 FSMO 역할  
  
-   복제 작업 중에 사용 가능한 PDC 에뮬레이터  
  
복제와 안전 복원 모두 다음이 필요합니다.  
  
-   Windows Server 2012 가상화된 게스트  
  
-   VM-Generation ID(VMGID)를 지원하는 가상화 호스트 플랫폼  
  
아래 표에서 가상화 제품 및 이러한 제품이 가상화된 도메인 컨트롤러와 VM-Generation ID를 지원하는지 여부를 검토하세요.  
  
|||  
|-|-|  
|**가상화 제품**|**가상화 된 도메인 컨트롤러 및 VMGID 지원**|  
|**Hyper-v 기능을 사용 하 여 Microsoft Windows Server 2012 서버**|예|  
|**Microsoft Windows Server 2012 Hyper-V Server**|예|  
|**하이퍼-V 클라이언트를 사용 하 여 Microsoft Windows 8 기능**|예|  
|**Windows Server 2008 R2 및 Windows Server 2008**|아니요|  
|**타사 가상화 솔루션**|공급업체에 문의|  
  
Microsoft에서는 Windows 7 Virtual PC, Virtual PC 2007, Virtual PC 2004 및 Virtual Server 2005를 지원하지만 이러한 제품은 64비트 게스트를 실행할 수 없으며 VM-GenerationID를 지원하지도 않습니다.  
  
타사 가상화 제품 및 이러한 제품의 가상화된 도메인 컨트롤러 지원 여부는 해당 공급업체에 직접 문의하세요.  
  
자세한 내용은 [타사 하드웨어 가상화 소프트웨어에서 실행되는 Microsoft 소프트웨어](https://support.microsoft.com/kb/897615)에 대한 지원 정책을 검토하세요.  
  
### <a name="critical-caveats"></a>중요한 제한 사항  
가상화된 도메인 컨트롤러는 다음에 대한 안전 복원을 지원하지 *않습니다*.  
  
-   기존 VHD 파일에 수동으로 복사된 VHD 및 VHDX 파일  
  
-   파일 백업 또는 전체 디스크 백업 소프트웨어를 사용하여 복원된 VHD 및 VHDX 파일  
  
> [!NOTE]  
> VHDX 파일은 Windows Server 2012 Hyper-V의 새로운 기능입니다.  
  
이러한 작업은 VM-GenerationID 의미 체계에서 다루지 않으므로 VM-Generation ID를 변경하지 않습니다. 이러한 방법으로 도메인 컨트롤러를 복원하면 USN 롤백이 발생하고 도메인 컨트롤러가 격리되거나 아니면 느린 개체로 인해 포리스트 수준의 정리 작업이 필요할 수 있습니다.  
  
> [!WARNING]  
> 가상화된 도메인 컨트롤러 안전 복원은 시스템 상태 백업 및 AD DS 휴지통의 대체 기능이 아닙니다.  
>   
> 스냅샷을 복원하면 스냅샷 후 해당 도메인 컨트롤러에서 발생한 이전에 복제되지 않은 변경 내용이 영구적으로 손실됩니다. 안전 복원은 실수로 인한 도메인 컨트롤러 격리 *만*방지하기 위해 신뢰할 수 없는 자동 복원을 구현합니다.  
  
USN 버블 및 느린 개체에 대 한 자세한 내용은 참조 하세요. [오류 8606는 Active Directory 문제 해결 작업: "Insufficient attributes were 개체를 만드는 given"](https://support.microsoft.com/kb/2028495)합니다.  
  
## <a name="BKMK_VDCCloning"></a>가상화 된 도메인 컨트롤러 복제  
그래픽 도구를 사용하든 Windows PowerShell을 사용하든 가상화된 도메인 컨트롤러를 복제하려면 몇 가지 단계를 수행해야 합니다. 상위 수준에는 다음 세 단계가 있습니다.  
  
**환경 준비**  
  
-   1단계: 하이퍼바이저가 VM-Generation ID를 지원하며, 따라서 복제를 지원하는지 확인  
  
-   2단계: PDC 에뮬레이터 역할 복제 하는 동안 복제 된 도메인 컨트롤러에서 Windows Server 2012를 실행 하 고 온라인 상태이 고 연결할 수 있는지는 도메인 컨트롤러에서 호스팅되는 확인 합니다.  
  
**원본 도메인 컨트롤러 준비**  
  
-   3단계: 원본 도메인 컨트롤러 복제 권한 부여  
  
-   4단계: 호환되지 않는 서비스 또는 프로그램을 제거하거나 CustomDCCloneAllowList.xml 파일에 추가  
  
-   5단계: DCCloneConfig.xml 만들기  
  
-   6단계: 원본 도메인 컨트롤러를 오프라인 상태로 전환  
  
**복제 된 도메인 컨트롤러 만들기**  
  
-   7단계: 원본 VM을 복사하거나 내보내고 XML 추가(이미 복사되지 않은 경우)  
  
-   8단계: 복사본에서 새 가상 컴퓨터 만들기  
  
-   9단계: 새 가상 컴퓨터를 시작하여 복제 시작  
  
Hyper-V 관리 콘솔과 같은 그래픽 도구를 사용한 작업과 Windows PowerShell과 같은 명령줄 도구를 사용한 작업에는 절차상의 차이가 없으므로 단계는 두 인터페이스에 단계가 한 번만 나와 있습니다. 이 항목에서는 종단 간 복제 프로세스 자동화를 살펴볼 수 있도록 Windows PowerShell 예제를 제공합니다. 이러한 예제는 어떤 단계에도 필요하지 않습니다. Windows Server 2012에 포함된 가상화된 도메인 컨트롤러용 그래픽 관리 도구는 없습니다.  
  
절차에서 복제된 컴퓨터를 만드는 방법 및 xml 파일을 추가하는 방법을 선택하는 과정이 있으며, 이러한 단계는 아래에 자세히 설명되어 있습니다. 이 프로세스는 다른 방식으로 변경할 수 없습니다.  
  
다음 다이어그램에서는 도메인이 이미 있는 경우의 가상화된 도메인 컨트롤러 복제 프로세스를 보여 줍니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_CloningProcessFlow.png)  
  
### <a name="step-1---validate-the-hypervisor"></a>1 단계 - 하이퍼바이저 유효성 검사  
공급업체 설명서를 검토하여 원본 도메인 컨트롤러가 지원되는 하이퍼바이저에서 실행 중인지 확인합니다. 가상화된 도메인 컨트롤러는 하이퍼바이저에 독립적이므로 Hyper-V가 필요하지 않습니다.  
  
Microsoft Hyper-v 하이퍼바이저를 사용 하는 경우 Windows Server 2012에서 실행 중인 것을 확인 합니다. 장치 관리를 사용하여 확인할 수 있습니다.  
  
**Devmgmt.msc** 를 열고 **시스템 장치** 에서 설치된 Microsoft Hyper-V 장치 및 드라이버를 확인합니다. 가상화된 도메인 컨트롤러에 필요한 특정 시스템 장치는 **Microsoft Hyper-V Generation Counter** (드라이버: vmgencounter.sys)입니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVVMGenIDCounter.png)  
  
### <a name="step-2---verify-the-pdce-fsmo-role"></a>2 단계 - PDCE FSMO 역할 확인  
DC를 복제하기 전에 주 도메인 컨트롤러 에뮬레이터 FSMO를 호스트하는 도메인 컨트롤러에서 Windows Server 2012를 실행하는지 확인해야 합니다. 다음과 같은 여러 가지 이유로 PDCE(PDC 에뮬레이터)가 필요합니다.  
  
1.  PDCE는 특정 **복제 가능 도메인 컨트롤러** 그룹을 만들고 도메인 루트에서 해당 권한을 도메인 컨트롤러가 자체를 복제할 수 있도록 설정합니다.  
  
2.  복제 도메인 컨트롤러는 복제 DC의 컴퓨터 개체를 만들기 위해 DRSUAPI RPC 프로토콜을 사용하여 PDCE에 직접 연결합니다.  
  
    > [!NOTE]  
    > Windows Server 2012는 새 RPC 메서드 **IDL_DRSAddCloneDC**(Opnum **28**)를 포함하도록 기존 DRS(디렉터리 복제 서비스) 원격 프로토콜(UUID **E3514235-4B06-11D1-AB04-00C04FC2DCD2**)을 확장합니다. **IDL_DRSAddCloneDC** 메서드는 기존 도메인 컨트롤러 개체의 특성을 복사하여 새 도메인 컨트롤러 개체를 만듭니다.  
    >   
    > 도메인 컨트롤러의 상태는 각 도메인 컨트롤러에 대해 유지 관리되는 컴퓨터, 서버, NTDS 설정, FRS, DFSR 및 연결 개체로 구성됩니다. 개체를 복제할 때 이 RPC 메서드는 원본 도메인 컨트롤러에 대한 모든 참조를 새 도메인 컨트롤러의 상응하는 개체로 바꿉니다. 호출자는 도메인 명명 컨텍스트에서 액세스 제어 권한 DS-Clone-Domain-Controller가 있어야 합니다.  
    >   
    > 이 새 메서드를 사용하려면 항상 호출자가 PDC 에뮬레이터 도메인 컨트롤러에 직접 액세스해야 합니다.  
    >   
    > 이 RPC 메서드는 새로운 기능이므로 네트워크 분석 소프트웨어에 새 Opnum 28 필드를 기존 UUID E3514235-4B06-11D1-AB04-00C04FC2DCD2에 포함하도록 업데이트된 파서가 필요합니다. 그렇지 않으면 이 트래픽의 구문을 분석할 수 없습니다.  
    >   
    > 자세한 내용은 [4.1.29 IDL_DRSAddCloneDC(Opnum 28)](https://msdn.microsoft.com/en-us/library/hh554213(v=prot.13).aspx)를 참조하세요.  
  
***즉, 완전히 라우팅되지 않은 네트워크를 사용 하는 경우에 PDCE 액세스 권한이 있는 네트워크 세그먼트가 필요 가상화 된 도메인 컨트롤러 복제***합니다. AD DS 논리 사이트 정보를 업데이트하는 데 주의하기만 한다면 실제 도메인 컨트롤러와 마찬가지로 복제 후 복제된 도메인 컨트롤러를 다른 네트워크로 이동할 수 있습니다.  
  
> [!IMPORTANT]  
> 단일 도메인 컨트롤러만 포함된 도메인을 복제할 때는 복제본 복사를 시작하기 전에 원본 DC가 다시 온라인 상태로 전환되었는지 확인해야 합니다. 프로덕션 도메인에는 항상 2개 이상의 도메인 컨트롤러가 있어야 합니다.  
  
#### <a name="active-directory-users-and-computers-method"></a>Active Directory 사용자 및 컴퓨터 사용  
  
1.  Dsa.msc 스냅인을 사용하는 경우 도메인을 마우스 오른쪽 단추로 클릭하고 **작업 마스터**를 클릭합니다. PDC 탭에 이름이 표시된 도메인 컨트롤러를 확인하고 대화 상자를 닫습니다.  
  
2.  해당 DC의 컴퓨터 개체를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 운영 체제 정보를 확인합니다.  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
다음 Active Directory Windows PowerShell 모듈 cmdlet을 조합하여 PDC 에뮬레이터 버전을 반환할 수 있습니다.  
  
```  
Get-adddomaincontroller  
Get-adcomputer  
```  
  
도메인을 제공하지 않으면 이러한 cmdlet에서 현재 실행 중인 컴퓨터의 도메인을 가정합니다.  
  
다음 명령은 PDCE 및 운영 체제 정보를 반환합니다.  
  
```  
get-adcomputer(Get-ADDomainController -Discover -Service "PrimaryDC").name -property * | format-list dnshostname,operatingsystem,operatingsystemversion  
```  
  
아래 예에서는 도메인 이름을 지정하고 Windows PowerShell 파이프라인 앞에 반환되는 속성을 필터링한 결과를 보여 줍니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PDCOSInfo.png)  
  
### <a name="step-3---authorize-a-source-dc"></a>3단계 - 원본 DC에 권한 부여  
원본 도메인 컨트롤러에 도메인 NC 헤드에서 **DC가 자신의 복제를 만들도록 허용**하는 CAR(액세스 제어 권한)이 있어야 합니다. 기본적으로 널리 알려진 **복제 가능 도메인 컨트롤러** 그룹에는 이 권한이 있으며 구성원은 포함되어 있지 않습니다. PDCE는 해당 FSMO 역할이 Windows Server 2012 도메인 컨트롤러로 전송될 때 이 역할을 만듭니다.  
  
#### <a name="active-directory-administrative-center-method"></a>Active Directory 관리 센터 사용  
  
1.  Dsac.exe를 시작하고 원본 DC로 이동한 후 해당 세부 정보 페이지를 엽니다.  
  
2.  **소속** 섹션에서 해당 도메인에 대한 **복제 가능 도메인 컨트롤러** 그룹을 추가합니다.  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
Active Directory Windows PowerShell 모듈 cmdlet **get-adcomputer**와 **add-adgroupmember**를 조합하여 **복제 가능 도메인 컨트롤러** 그룹에 도메인 컨트롤러를 추가할 수 있습니다.  
  
```  
Get-adcomputer <dc name> | %{add-adgroupmember "cloneable domain controllers" $_.samaccountname}  
```  
  
예를 들어 다음 명령은 그룹 구성원의 고유 이름을 지정하지 않고도 DC1 서버를 그룹에 추가합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_AddDcToGroup.png)  
  
#### <a name="rebuilding-default-permissions"></a>기본 권한 다시 생성  
도메인 헤드에서 이 권한을 제거하면 복제에 실패합니다. Active Directory 관리 센터 또는 Windows PowerShell을 사용하여 권한을 다시 만들 수 있습니다.  
  
##### <a name="active-directory-administrative-center-method"></a>Active Directory 관리 센터 사용  
  
1.  **Active Directory 관리 센터**를 열고 도메인 헤드를 마우스 오른쪽 단추로 클릭한 다음 **속성**, **확장** 탭, **보안**, **고급**을 차례로 클릭합니다. **이 개체만**을 클릭합니다.  
  
2.  **추가**를 클릭하고 **선택할 개체 이름 입력** 아래에 그룹 이름 **복제 가능 도메인 컨트롤러**를 입력합니다.  
  
3.  사용 권한에서 **DC가 자신의 복제를 만들도록 허용**을 클릭한 다음 **확인**을 클릭합니다.  
  
> [!NOTE]  
> 기본 권한을 제거하고 개별 도메인 컨트롤러를 추가할 수도 있습니다. 그러나 이렇게 하면 새 관리자가 이 사용자 지정을 모를 경우 지속적인 유지 관리에 문제가 발생할 수 있습니다. 기본 설정을 변경해도 보안이 강화되지 않으므로 변경하지 않는 것이 좋습니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
관리자 권한의 Windows PowerShell 콘솔 프롬프트에서 다음 명령을 사용합니다. 이러한 명령은 도메인 이름을 검색하여 기본 권한에 다시 추가합니다.  
  
```  
import-module activedirectory  
cd ad:  
$domainNC = get-addomain  
$dcgroup = get-adgroup "Cloneable Domain Controllers"  
$sid1 = (get-adgroup $dcgroup).sid  
$acl = get-acl $domainNC  
$objectguid = new-object Guid 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e  
$ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid1,"ExtendedRight","Allow",$objectguid  
$acl.AddAccessRule($ace1)  
set-acl -aclobject $acl $domainNC  
cd c:  
```  
  
또는 Windows PowerShell 콘솔에서 예제 [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)을 실행합니다. 그러면 영향을 받는 도메인의 도메인 컨트롤러에서 관리자 권한으로 콘솔이 시작되며, 사용 권한이 자동으로 설정됩니다. 이 예제는 이 모듈의 부록에 있습니다.  
  
### <a name="step-4---remove-incompatible-applications-or-services-if-not-using-customdccloneallowlistxml"></a>4단계 - 호환되지 않는 응용 프로그램 또는 서비스 제거(CustomDCCloneAllowList.xml을 사용하지 않는 경우)  
이전에 Get-ADDCCloningExcludedApplicationList에서 반환되고 *CustomDCCloneAllowList.xml에 추가되지 않은* 모든 프로그램 또는 서비스를 복제 전에 제거해야 합니다. 응용 프로그램이나 서비스를 제거하는 것이 좋습니다.  
  
> [!WARNING]  
> 호환되지 않는 프로그램이나 서비스를 제거하거나 CustomDCCloneAllowList.xml에 추가하지 않으면 복제가 차단됩니다.  
  
Get-AdComputerServiceAccount cmdlet을 사용하여 도메인에서 독립 실행형 MSA(관리 서비스 계정)를 찾을 수 있습니다(해당 컴퓨터에서 MSA를 사용하는 경우). MSA가 설치된 경우 Uninstall-ADServiceAccount cmdlet을 사용하여 로컬로 설치된 서비스 계정을 제거합니다. 6단계에서 원본 도메인 컨트롤러를 오프라인 상태로 전환하는 작업을 마치고 나면 서버가 다시 온라인 상태로 전환된 후 Install-ADServiceAccount를 사용하여 MSA를 다시 추가할 수 있습니다. 자세한 내용은 [Uninstall-ADServiceAccount](https://technet.microsoft.com/library/hh852310)를 참조하세요.  
  
> [!IMPORTANT]  
> Windows Server 2008 R2에서 처음 릴리스된 독립 실행형 MSA는 Windows Server 2012에서 그룹 MSA로 대체되었습니다. 그룹 MSA는 복제를 지원합니다.  
  
### <a name="step-5---create-dccloneconfigxml"></a>5단계 - DCCloneConfig.xml 만들기  
도메인 컨트롤러를 복제하려면 DcCloneConfig.xml 파일이 필요합니다. 이 파일의 콘텐츠를 통해 새 컴퓨터 이름 및 IP 주소와 같은 고유한 정보를 지정할 수 있습니다.  
  
응용 프로그램 또는 잠재적으로 호환되지 않는 Windows 서비스를 원본 도메인 컨트롤러에 설치하지 않은 한 CustomDCCloneAllowList.xml 파일은 선택 사항입니다. 이 파일에 이름, 형식 및 위치를 정확하게 지정해야 합니다. 그러지 않으면 복제에 실패합니다.  
  
따라서 항상 Windows PowerShell cmdlet을 사용하여 XML 파일을 만들어 올바른 위치에 배치해야 합니다.  
  
#### <a name="generating-with-new-addccloneconfigfile"></a>New-ADDCCloneConfigFile로 생성  
Windows Server 2012의 Active Directory Windows PowerShell 모듈에는 다음 새 cmdlet이 포함되어 있습니다.  
  
```  
New-ADDCCloneConfigFile  
```  
  
복제하려는 제안된 원본 도메인 컨트롤러에서 이 cmdlet을 실행합니다. 이 cmdlet은 여러 인수를 지원하며, 사용된 경우 -offline 인수를 지정하지 않는 한 항상 해당 cmdlet이 실행되는 컴퓨터와 환경을 테스트합니다.  
  
||||  
|-|-|-|  
|**ActiveDirectory**<br /><br />**Cmdlet**|**인수**|**설명**|  
|**New-ADDCCloneConfigFile**|*<no argument specified>*|DSA 작업 디렉터리(기본값: %systemroot%\ntds)에 빈 DcCloneConfig.xml 파일을 만듭니다.|  
||-CloneComputerName|복제 DC 컴퓨터 이름을 지정합니다. 문자열 데이터 형식입니다.|  
||-Path|DcCloneConfig.xml을 만들 폴더를 지정합니다. 지정하지 않으면 DSA 작업 디렉터리(기본값: %systemroot%\ntds)에 기록합니다. 문자열 데이터 형식입니다.|  
||-SiteName|복제된 컴퓨터 계정을 만드는 동안 연결할 AD 논리 사이트 이름을 지정합니다. 문자열 데이터 형식입니다.|  
||-IPv4Address|복제된 컴퓨터의 고정 IPv4 주소를 지정합니다. 문자열 데이터 형식입니다.|  
||-IPv4SubnetMask|복제된 컴퓨터의 고정 IPv4 서브넷 마스크를 지정합니다. 문자열 데이터 형식입니다.|  
||-IPv4DefaultGateway|복제된 컴퓨터의 고정 IPv4 기본 게이트웨이 주소를 지정합니다. 문자열 데이터 형식입니다.|  
||-IPv4DNSResolver|복제된 컴퓨터의 고정 IPv4 DNS 항목을 쉼표로 구분된 목록으로 지정합니다. 배열 데이터 형식입니다. 최대 4개의 항목을 입력할 수 있습니다.|  
||-PreferredWINSServer|주 WINS 서버의 고정 IPv4 주소를 지정합니다. 문자열 데이터 형식입니다.|  
||-AlternateWINSServer|보조 WINS 서버의 고정 IPv4 주소를 지정합니다. 문자열 데이터 형식입니다.|  
||-IPv6DNSResolver|복제된 컴퓨터의 고정 IPv6 DNS 항목을 쉼표로 구분된 목록으로 지정합니다. 가상화된 도메인 컨트롤러 복제에서는 고정 Ipv6 정보를 설정할 방법이 없습니다. 배열 데이터 형식입니다.|  
||-Offline|유효성 검사 테스트를 수행하지 않으며 모든 기존 dccloneconfig.xml을 덮어씁니다. 매개 변수는 없습니다. 자세한 내용은 [오프라인 모드에서 New-ADDCCloneConfigFile 실행](../../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode)을 참조하십시오.|  
||*-Static*|고정 IP 인수인 IPv4SubnetMask, IPv4SubnetMask 또는 IPv4DefaultGateway를 지정하는 경우에 필요합니다. 매개 변수는 없습니다.|  
  
온라인 모드로 실행할 때 수행되는 테스트는 다음과 같습니다.  
  
-   PDC 에뮬레이터가 Windows Server 2012 이상인지 여부  
  
-   원본 도메인 컨트롤러가 복제 가능 도메인 컨트롤러 그룹의 구성원인지 여부  
  
-   원본 도메인 컨트롤러에 제외된 응용 프로그램 또는 서비스가 포함되어 있지 않은지 여부  
  
-   원본 도메인 컨트롤러의 지정된 경로에 DcCloneConfig.xml이 이미 포함되어 있지 않은지 여부  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewDCCloneConfig.png)  
  
### <a name="step-6---take-the-source-domain-controller-offline"></a>6단계 - 원본 도메인 컨트롤러를 오프라인으로 전환  
실행 중인 원본 DC는 복사할 수 없으므로 정상적으로 종료해야 합니다. 비정상적인 정전으로 인해 중지된 도메인 컨트롤러는 복제하지 마세요.  
  
#### <a name="graphical-method"></a>그래픽 사용  
실행 중인 DC 내의 종료 단추 또는 Hyper-V 관리자 종료 단추를 사용합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_Shutdown.png)  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVShutdown.png)  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
다음 cmdlet 중 하나를 사용하여 가상 컴퓨터를 종료할 수 있습니다.  
  
```  
Stop-computer  
Stop-vm  
```  
  
Stop-computer는 가상화에 상관없이 컴퓨터 종료를 지원하는 cmdlet이며, 레거시 Shutdown.exe 유틸리티와 유사합니다. Stop-vm은 Windows Server 2012 Hyper-V Windows PowerShell 모듈의 새로운 cmdlet이며, Hyper-V 관리자의 전원 옵션에 해당합니다. Stop-vm은 도메인 컨트롤러가 종종 프라이빗 가상화 네트워크에서 작동하는 랩 환경에 유용합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopComputer2.png)  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopVM.png)  
  
### <a name="step-7---copy-disks"></a>7단계 - 디스크 복사  
복사 단계에서는 관리자가 다음 사항을 선택해야 합니다.  
  
-   Hyper-V 없이 수동으로 디스크 복사  
  
-   Hyper-V를 사용하여 VM 내보내기  
  
-   Hyper-V를 사용하여 병합된 디스크 내보내기  
  
시스템 드라이브뿐만 아니라 가상 컴퓨터의 모든 디스크를 복사해야 합니다. 원본 도메인 컨트롤러에서 차이점 보관용 디스크를 사용하는 경우 복제된 도메인 컨트롤러를 다른 Hyper-V 호스트로 이동하려면 내보내기를 수행해야 합니다.  
  
디스크 수동 복사는 원본 도메인 컨트롤러에 드라이브가 *하나*만 있는 경우에 권장됩니다. 내보내기/가져오기는 *둘 이상* 의 드라이브가 있거나 다른 복잡한 가상화된 하드웨어 사용자 지정 항목(예: 여러 NIC)이 있는 VM에 권장됩니다.  
  
파일을 수동으로 복사하는 경우에는 복사하기 전에 모든 스냅샷을 삭제합니다. VM을 내보내는 경우에는 내보내기 전에 스냅샷을 삭제하거나 가져온 후 새 VM에서 스냅샷을 삭제합니다.  
  
> [!WARNING]  
> 스냅샷은 도메인 컨트롤러를 이전 상태로 되돌릴 수 있는 차이점 보관용 디스크입니다. 도메인 컨트롤러를 복제한 다음 사전 복제 스냅샷을 복원하면 결국 포리스트에 도메인 컨트롤러가 중복되게 됩니다. 새로 복제된 도메인 컨트롤러의 이전 스냅샷에는 값이 없습니다.  
  
#### <a name="manually-copying-disks"></a>수동으로 디스크 복사  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V 관리자 사용  
Hyper-V 관리자 스냅인을 사용하여 원본 도메인 컨트롤러에 연결된 디스크를 확인합니다. 검사 옵션을 사용하여 도메인 컨트롤러에서 차이점 보관용 디스크(부모 디스크도 함께 복사해야 함)를 사용하는지 확인할 수 있습니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVInspect.png)  
  
스냅샷을 삭제하려면 VM을 선택하고 스냅샷 하위 트리를 삭제합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDeleteSnapshot.gif)  
  
그런 다음 Windows 탐색기, Xcopy.exe 또는 Robocopy.exe를 사용하여 VHD 또는 VHDX 파일을 수동으로 복사할 수 있습니다. 특별한 단계가 필요 없습니다. 다른 폴더로 이동하는 경우에도 파일 이름을 변경하는 것이 좋습니다.  
  
> [!NOTE]  
> LAN(1Gb 이상)에 있는 호스트 컴퓨터 간에 복사할 경우 **Xcopy.exe /J** 옵션을 사용하면 훨씬 적은 대역폭으로 다른 어떤 도구보다 훨씬 빠르게 VHD/VHDX 파일을 복사할 수 있습니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
Windows PowerShell을 사용하여 디스크를 확인하려면 다음 Hyper-V 모듈을 사용합니다.  
  
```  
Get-vmidecontroller  
Get-vmscsicontroller  
Get-vmfibrechannelhba  
Get-vmharddiskdrive  
```  
  
예를 들어 다음 예제를 사용하면 **DC2** 라는 VM에서 모든 IDE 하드 드라이브를 반환할 수 있습니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_ReturnIDE.png)  
  
디스크 경로가 AVHD 또는 AVHDX 파일을 가리키면 이는 스냅샷입니다. 디스크와 연결된 스냅샷을 삭제하고 실제 VHD 또는 VHDX에 병합하려면 다음 cmdlet을 사용합니다.  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
예를 들어 DC2-SOURCECLONE이라는 VM에서 모든 스냅샷을 삭제하려면 다음 명령을 입력합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_DelSnapshots.png)  
  
Windows PowerShell을 사용하여 파일을 복사하려면 다음 cmdlet을 사용합니다.  
  
```  
Copy-Item  
```  
  
파이프라인의 VM cmdlet과 결합하면 자동화에 도움이 됩니다. 파이프라인은 여러 cmdlet 간에 데이터를 전달하는 데 사용되는 채널입니다. 예를 들어 시스템 드라이브의 정확한 경로를 모르는 상태에서 DC2-SOURCECLONE이라는 오프라인 원본 도메인 컨트롤러의 드라이브를 c:\temp\copy.vhd라는 새 디스크에 복사하려면 다음 명령을 입력합니다.  
  
```  
Get-VMIdeController dc2-sourceclone | Get-VMHardDiskDrive | select-Object {copy-item -path $_.path -destination c:\temp\copy.vhd}  
```  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSCopyDrive.png)  
  
> [!IMPORTANT]  
> 복제할 때는 passthru 디스크를 사용할 수 없습니다. 이 디스크에서는 가상 디스크 파일을 사용하지 않고 대신 실제 하드 디스크를 사용하기 때문입니다.  
  
> [!NOTE]  
> 파이프라인을 사용하는 다양한 Windows PowerShell 작업에 대한 자세한 내용은 [Windows PowerShell의 파이프 및 파이프라인](https://technet.microsoft.com/library/ee176927.aspx)을 참조하세요.  
  
#### <a name="exporting-the-vm"></a>VM 내보내기  
디스크를 복사하는 방법의 대안으로 전체 Hyper-V VM을 복사본으로 내보낼 수 있습니다. 내보내기에서는 VM의 이름이 지정되고 모든 디스크 및 구성 정보를 포함하는 폴더를 자동으로 만듭니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVExport.png)  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V 관리자 사용  
Hyper-V 관리자를 사용하여 VM을 내보내려면  
  
1.  원본 도메인 컨트롤러를 마우스 오른쪽 단추로 클릭하고 **내보내기**를 클릭합니다.  
  
2.  기존 폴더를 내보내기 컨테이너로 선택합니다.  
  
3.  상태 열에 **내보내는 중**표시가 중지될 때까지 기다립니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
Hyper-V Windows PowerShell 모듈을 사용하여 VM을 내보내려면 다음 cmdlet을 사용합니다.  
  
```  
Export-vm  
```  
  
예를 들어 DC2-SOURCECLONE이라는 VM을 C:\VM이라는 폴더로 내보내려면 다음 명령을 입력합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSExport.png)  
  
> [!NOTE]  
> Windows Server 2012 Hyper-V에서는 이 교육 과정의 범위를 벗어나는 새로운 내보내기 및 가져오기 기능을 지원합니다. 자세한 내용은 TechNet을 검토하세요.  
  
#### <a name="exporting-merged-disks-using-hyper-v"></a>Hyper-V를 사용하여 병합된 디스크 내보내기  
마지막 옵션은 Hyper-V 내에서 디스크 병합 및 변환 옵션을 사용하는 것입니다. 이를 통해 스냅샷 AVHD/AVHDX 파일이 포함되어 있는 경우에도 기존 디스크 구조를 단일 새 디스크에 복사할 수 있습니다. 수동 디스크 복사 시나리오와 같은이 주로 예: c: 드라이브를 사용 하는 보다 단순한 가상 컴퓨터에 대 한\\합니다. 한 가지 장점은 수동 복사와 달리 스냅샷을 먼저 삭제할 필요가 없다는 것입니다. 이 작업은 단순히 스냅샷을 삭제하고 디스크를 복사하는 작업보다 느릴 수밖에 없습니다.  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V 관리자 사용  
Hyper-V 관리자를 사용하여 병합된 디스크를 만들려면  
  
1.  클릭 **디스크 편집**합니다.  
  
2.  최하위 자식 디스크를 찾아봅니다. 예를 들어 차이점 보관용 디스크를 사용하는 경우 해당 자식 디스크가 최하위 자식이고, 가상 컴퓨터에 하나 이상의 스냅샷이 있는 경우 현재 선택된 스냅샷이 최하위 자식 디스크입니다.  
  
3.  **병합** 옵션을 선택하여 전체 부모-자식 구조에서 단일 디스크를 만듭니다.  
  
4.  새 가상 하드 디스크를 선택하고 경로를 지정합니다. 그러면 이전 스냅샷 복원 위험이 없는 이식 가능한 새 단일 단위로 기존 VHD/VHDX 파일이 조정됩니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
Hyper-V Windows PowerShell 모듈을 사용하여 복잡한 부모 집합에서 병합된 디스크를 만들려면 다음 cmdlet을 사용합니다.  
  
```  
Convert-vm  
```  
  
예를 들어 VM의 전체 디스크 스냅샷 체인(이번에는 차이점 보관용 디스크가 포함되지 않음)과 부모 디스크를 DC4-CLONED.VHDX라는 새 단일 디스크로 내보내려면 다음 명령을 입력합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSConvertVhd.png)  
  
#### <a name="BKMK_Offline"></a>오프 라인 시스템 디스크에 XML을 추가합니다.  
실행 중인 원본 DC에 Dccloneconfig.xml을 복사한 경우 업데이트된 dccloneconfig.xml 파일을 복사한/내보낸 오프라인 시스템 디스크에 즉시 복사해야 합니다. 이전에 Get-ADDCCloningExcludedApplicationList를 사용하여 검색한 설치된 응용 프로그램에 따라 CustomDCCloneAllowList.xml 파일을 디스크에 복사해야 할 수도 있습니다.  
  
다음 위치에 DcCloneConfig.xml 파일을 포함할 수 있습니다.  
  
1.  DSA 작업 디렉터리  
  
2.  %windir%\NTDS  
  
3.  드라이브의 루트에서 시작하여 드라이브 문자 순의 이동식 읽기/쓰기 미디어  
  
이러한 경로는 구성할 수 없습니다. 복제가 시작된 후 복제 작업에서 특정한 순서로 이러한 위치를 확인하고 다른 폴더의 내용에 상관없이 처음 발견된 DcCloneConfig.xml 파일을 사용합니다.  
  
다음 위치에 CustomDCCloneAllowList.xml 파일을 포함할 수 있습니다.  
  
1.  HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters  
  
    AllowListFolder(*REG_SZ*)  
  
2.  DSA 작업 디렉터리  
  
3.  %windir%\NTDS  
  
4.  드라이브의 루트에서 시작하여 드라이브 문자 순의 이동식 읽기/쓰기 미디어  
  
**-offline** 인수(오프라인 모드라고도 함)와 함께 New-ADDCCloneConfigFile을 실행하여 DcCloneConfig.xml 파일을 만들고 이를 올바른 위치에 배치할 수 있습니다. 다음 예제에서는 오프라인 모드에서 New-ADDCCloneConfigFile을 실행하는 방법을 보여 줍니다.  
  
고정 IPv4 주소를 사용 하 여 "REDMOND"를 호출 하는 사이트의 오프 라인 모드에서 CloneDC1 라는 복제 도메인 컨트롤러를 만들려면 다음을 입력 합니다.  
  
```  
New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS  
```  
  
정적 IPv4 및 정적 IPv6 설정을 사용하는 Clone2라는 복제 도메인 컨트롤러를 오프라인 모드에서 만들려면 다음을 입력합니다.  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS  
```  
  
정적 IPv4 및 동적 IPv6 설정을 사용하는 복제 도메인 컨트롤러를 오프라인 모드에서 만들고 DNS 확인자 설정에 대해 여러 DNS 서버를 지정하려면 다음을 입력합니다.  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS   
```  
  
동적 IPv4 및 정적 IPv6 설정을 사용하는 Clone1라는 복제 도메인 컨트롤러를 오프라인 모드에서 만들려면 다음을 입력합니다.  
  
```  
New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS  
```  
  
동적 IPv4 및 동적 IPv6 설정을 사용하는 복제 도메인 컨트롤러를 오프라인 모드에서 만들려면 다음을 입력합니다.  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS  
  
```  
  
##### <a name="windows-explorer-method"></a>Windows 탐색기 사용  
이제 Windows Server 2012에서 VHD 및 VHDX 파일을 탑재할 수 있는 그래픽 옵션을 제공합니다. 이 옵션을 사용하려면 Windows Server 2012의 데스크톱 경험 기능을 설치해야 합니다.  
  
1.  원본 DC의 시스템 드라이브 또는 DSA 작업 디렉터리 위치 폴더가 포함된 새로 복사한 VHD/VHDX 파일을 클릭한 다음 **디스크 이미지 도구** 메뉴에서 **탑재**를 클릭합니다.  
  
2.  현재 탑재된 드라이브에서 올바른 위치에 XML 파일을 복사합니다. 폴더 사용 권한을 묻는 메시지가 표시될 수 있습니다.  
  
3.  탑재된 드라이브를 클릭한 다음 **디스크 도구** 메뉴에서 **꺼내기**를 클릭합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVClickMountedDrive.png)  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDetailsMountedDrive.gif)  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVEjectMountedDrive.gif)  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
또는 오프라인 디스크를 탑재하고 Windows PowerShell cmdlet을 사용하여 XML 파일을 복사할 수 있습니다.  
  
```  
mount-vhd  
get-disk  
get-partition  
get-volume  
Add-PartitionAccessPath  
Copy-Item  
```  
  
이렇게 하면 프로세스를 완전히 제어할 수 있습니다. 예를 들어 특정 드라이브 문자로 드라이브를 탑재하고, 파일을 복사하고, 드라이브를 분리할 수 있습니다.  
  
```  
mount-vhd <disk path> -passthru -nodriveletter | get-disk | get -partition | get-volume | get-partition | where {$_.partition number -eq 2} | Add-PartitionAccessPath -accesspath <drive letter>  
  
copy-item <xml file path><destination path>\dccloneconfig.xml  
  
dismount-vhd <disk path>  
```  
  
예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSMountVHD.png)  
  
또는 새 **Mount-DiskImage** cmdlet을 사용하여 VHD(또는 ISO) 파일을 탑재할 수 있습니다.  
  
### <a name="step-8---create-the-new-virtual-machine"></a>8단계 - 새 가상 컴퓨터 만들기  
복제 프로세스를 시작하기 전 마지막 구성 단계는 복사한 원본 도메인 컨트롤러의 디스크를 사용하는 VM을 만드는 것입니다. 디스크 복사 단계에서 선택한 항목에 따라 다음 두 가지 옵션 중 하나를 선택할 수 있습니다.  
  
1.  복사한 디스크에 새 VM 연결  
  
2.  내보낸 VM 가져오기  
  
#### <a name="associating-a-new-vm-with-copied-disks"></a>복사한 디스크에 새 VM 연결  
시스템 디스크를 수동으로 복사한 경우 복사한 디스크를 사용하여 새 가상 컴퓨터를 만들어야 합니다. 새 VM이 만들어지면 하이퍼바이저에서 VM-Generation ID를 자동으로 설정합니다. VM 또는 Hyper-V 호스트에서 구성을 변경할 필요가 없습니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVConnectVHD.gif)  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V 관리자 사용  
  
1.  새 가상 컴퓨터를 만듭니다.  
  
2.  VM 이름, 메모리 및 네트워크를 지정합니다.  
  
3.  가상 하드 디스크 연결 페이지에서 복사한 시스템 디스크를 지정합니다.  
  
4.  마법사를 완료하여 VM을 만듭니다.  
  
여러 디스크, 네트워크 어댑터 또는 기타 사용자 지정 항목이 있는 경우 도메인 컨트롤러를 시작하기 전에 구성합니다. 복잡한 VM의 경우 "내보내기-가져오기" 방법으로 디스크를 복사하는 것이 좋습니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
Hyper-V Windows PowerShell 모듈에서 다음 cmdlet을 사용하여 Windows Server 2012에서의 VM 만들기를 자동화할 수 있습니다.  
  
```  
New-VM  
```  
  
예를 들어 다음 예제에서는 1GB RAM을 사용하고, c:\vm\dc4-systemdrive-clonedfromdc2.vhd 파일에서 부팅되며, 10.0 가상 네트워크를 사용하는 DC4-CLONEDFROMDC2 VM을 만듭니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewVM.png)  
  
#### <a name="import-vm"></a>VM 가져오기  
이전에 VM을 내보낸 경우 이제 해당 VM을 복사본으로 가져와야 합니다. 이 작업에서는 이전에 내보낸 XML을 통해 모든 이전 설정, 드라이브, 네트워크 및 메모리 설정을 사용하여 컴퓨터를 다시 만듭니다.  
  
내보낸 동일한 VM에서 추가 복사본을 만들려면 내보낸 VM의 복사본을 필요한 만큼 여러 개 만듭니다. 그런 다음 각 복사본에 대해 가져오기를 사용합니다.  
  
> [!IMPORTANT]  
> 내보내기에서는 원본의 모든 정보를 유지하므로 **복사** 옵션을 사용해야 합니다. **이동** 또는 **원본 위치** 를 사용하여 서버를 가져오면 Hyper-V 호스트 서버가 동일한 경우 정보가 충돌하게 됩니다.  
  
##### <a name="hyper-v-manager-method"></a>Hyper-V 관리자 사용  
Hyper-V 관리자 스냅인을 사용하여 가져오려면  
  
1.  **가상 컴퓨터 가져오기**를 클릭합니다.  
  
2.  **폴더 찾기** 페이지에서 찾아보기 단추를 사용하여 내보낸 VM 정의 파일을 선택합니다.  
  
3.  **가상 컴퓨터 선택** 페이지에서 원본 컴퓨터를 클릭합니다.  
  
4.  **가져오기 유형 선택** 페이지에서 **가상 컴퓨터 복사(새로운 고유 ID 만들기)** 를 클릭한 다음 **마침**을 클릭합니다.  
  
5.  동일한 Hyper-V 호스트에서 가져오는 경우 가져온 VM의 이름을 바꿉니다. 기본적으로 가져온 VM의 이름은 내보낸 원본 도메인 컨트롤러와 같은 이름으로 지정됩니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportLocateFolder.png)  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportSelectVM.png)  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportChooseType.gif)  
  
Hyper-V 관리 스냅인을 사용하여 가져온 스냅샷을 모두 제거해야 합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportDelSnap.gif)  
  
> [!WARNING]  
> 가져온 스냅샷을 삭제하는 것은 매우 중요합니다. 가져온 스냅샷이 적용되면 복제된 도메인 컨트롤러가 이전(및 라이브) DC의 상태로 되돌아가 복제 실패, IP 정보 중복 및 기타 중단을 일으키게 됩니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 사용  
Hyper-V Windows PowerShell 모듈에서 다음 cmdlet을 사용하여 Windows Server 2012에서의 VM 가져오기를 자동화할 수 있습니다.  
  
```  
Import-VM  
Rename-VM  
```  
  
예를 들어 다음 예제에서는 자동으로 확인된 XML 파일을 사용하여 VM DC2-CLONED를 가져온 다음 즉시 새 VM 이름 DC5-CLONEDFROMDC2로 이름을 바꿉니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSImportVM.png)  
  
다음 cmdlet을 사용하여 가져온 스냅샷을 모두 제거해야 합니다.  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSGetVMSnap.png)  
  
> [!WARNING]  
> 컴퓨터를 가져올 때 정적 MAC 주소가 원본 도메인 컨트롤러에 할당되지 않았는지 확인해야 합니다. 정적 MAC 주소를 사용하는 원본 컴퓨터를 복제한 경우에는 이러한 복사한 컴퓨터에서 네트워크 트래픽을 올바르게 보내거나 받지 못합니다. 이 경우 새로운 고유한 정적 또는 동적 MAC 주소를 설정합니다. 다음 명령을 사용하여 VM에서 정적 MAC 주소를 사용하는지 확인할 수 있습니다.  
>   
> **Get-VM -VMName**   
>  ***test-vm* | Get-VMNetworkAdapter | fl \***  
  
### <a name="step-9---clone-the-new-virtual-machine"></a>9단계 - 새 가상 컴퓨터 복제  
필요한 경우 복제를 시작하기 전에 오프라인 복제 원본 도메인 컨트롤러를 다시 시작합니다. 이와 상관없이 PDC 에뮬레이터가 온라인 상태인지 확인합니다.  
  
복제를 시작하려면 새 가상 컴퓨터를 시작하기만 하면 됩니다. 프로세스가 자동으로 시작되며, 복제가 완료된 후 도메인 컨트롤러가 자동으로 다시 부팅됩니다.  
  
> [!IMPORTANT]  
> 도메인 컨트롤러를 오랫동안 꺼진 상태로 유지하지 않는 것이 좋습니다. 복제본이 해당 원본 DC와 동일한 사이트에 가입된 경우 원본 도메인 컨트롤러가 오프라인 상태에 있으면 초기 사이트 내 및 사이트 간 복제 토폴로지를 생성하는 데 시간이 더 오래 걸릴 수 있습니다.  
  
Windows PowerShell을 사용하여 VM을 시작하는 경우 새 Hyper-V 모듈 cmdlet은 다음과 같습니다.  
  
```  
Start-VM  
```  
  
예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
![가상화 된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSStartVM.png)  
  
복제가 완료된 후 컴퓨터가 다시 시작되고 나면 해당 컴퓨터가 도메인 컨트롤러가 되며, 정상적으로 로그온하여 정상 작동을 확인할 수 있습니다. 오류가 발생하면 조사를 위해 서버가 디렉터리 서비스 복원 모드로 시작하도록 설정됩니다.  
  
## <a name="BKMK_VDCSafeRestore"></a>가상화 세이프 가드  
가상화된 도메인 컨트롤러 복제와 달리 Windows Server 2012 가상화 세이프가드에는 구성 단계가 없습니다. 몇 가지 간단한 조건만 충족하면 사용자 개입 없이 기능이 작동합니다.  
  
-   하이퍼바이저에서 VM-Generation ID를 지원합니다.  
  
-   복원된 도메인 컨트롤러에서 신뢰할 수 없는 방식으로 변경 내용을 복제할 수 있는 유효한 파트너 도메인 컨트롤러가 있습니다.  
  
### <a name="validate-the-hypervisor"></a>하이퍼바이저 유효성 검사  
공급업체 설명서를 검토하여 원본 도메인 컨트롤러가 지원되는 하이퍼바이저에서 실행 중인지 확인합니다. 가상화된 도메인 컨트롤러는 하이퍼바이저에 독립적이므로 Hyper-V가 필요하지 않습니다.  
  
알려진 VM-Generation ID 지원은 [플랫폼 요구 사항](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_PlatformReqs) 섹션을 검토하세요.  
  
원본 하이퍼바이저에서 다른 대상 하이퍼바이저로 VM을 마이그레이션하는 경우 다음 표에 설명된 대로 하이퍼바이저에서 VM-Generation ID를 지원하는지 여부에 따라 가상화 세이프가드이 트리거될 수도 있고 트리거되지 않을 수도 있습니다.  
  
|원본 하이퍼바이저|대상 하이퍼바이저|결과|  
|---------------------|---------------------|----------|  
|VM-Generation ID 지원|VM-Generation ID 지원 안 함|보호 기능이 트리거되지 않음(DCCloneConfigFile.xml이 있는 경우 DC가 DSRM으로 부팅됨)|  
|VM-Generation ID 지원 안 함|VM-Generation ID 지원|보호 기능이 트리거됨|  
|VM-Generation ID 지원|VM-Generation ID 지원|VM 정의가 변경되지 않아 VM-Generation ID가 동일하게 유지되므로 보호 기능이 트리거되지 않음|  
  
### <a name="validate-the-replication-topology"></a>복제 토폴로지 유효성 검사  
가상화 세이프가드은 Active Directory 복제 변경에 대한 신뢰할 수 없는 인바운드 복제뿐 아니라 모든 SYSVOL 콘텐츠의 신뢰할 수 없는 다시 동기화를 시작합니다. 이를 통해 도메인 컨트롤러가 완전한 기능을 갖춘 스냅샷에서 복구되며 나머지 환경과 일치하게 됩니다.  
  
이 새 기능에는 몇 가지 요구 사항과 제한 사항이 있습니다.  
  
-   복원된 도메인 컨트롤러에서 쓰기 가능한 DC에 연결할 수 있어야 합니다.  
  
-   도메인의 모든 도메인 컨트롤러를 동시에 복원해서는 안 됩니다.  
  
-   복원된 도메인 컨트롤러에서 발생한 변경 내용이 스냅샷 생성 후 아웃바운드로 복제되지 않은 경우 해당 변경 내용은 영구적으로 손실됩니다.  
  
문제 해결 섹션에서 이러한 시나리오를 다루지만 아래 정보를 통해 문제를 일으킬 수 있는 토폴로지를 만들지 않을 수 있습니다.  
  
#### <a name="writable-domain-controller-availability"></a>쓰기 가능한 도메인 컨트롤러 가용성  
복원된 경우 도메인 컨트롤러는 쓰기 가능한 도메인 컨트롤러에 연결할 수 있어야 합니다. 읽기 전용 도메인 컨트롤러는 업데이트 변경 내용을 보낼 수 없습니다. 쓰기 가능한 도메인 컨트롤러에는 항상 쓰기 가능한 파트너가 필요하므로 이러한 연결이 이미 설정되어 있다면 토폴로지가 올바를 가능성이 높습니다. 그러나 모든 쓰기 가능한 도메인 컨트롤러를 동시에 복원하는 경우에는 어떤 도메인 컨트롤러도 유효한 소스를 찾을 수 없습니다. 이는 쓰기 가능한 도메인 컨트롤러가 유지 관리 중 오프라인 상태이거나 네트워크를 통해 연결할 수 없는 경우에도 마찬가지입니다.  
  
#### <a name="simultaneous-restore"></a>동시 복원  
단일 도메인의 모든 도메인 컨트롤러를 동시에 복원하지 마세요. 모든 스냅샷이 한 번에 복원되면 Active Directory 복제는 정상적으로 작동하지만 SYSVOL 복제는 중단됩니다. FRS 및 DFSR의 복원 아키텍처를 사용하려면 해당 복제본 인스턴스를 신뢰할 수 없는 동기화 모드로 설정해야 합니다. 모든 도메인 컨트롤러가 한 번에 복원되고 각 도메인 컨트롤러가 자체를 SYSVOL에 대해 신뢰할 수 없는 것으로 표시한 경우에는 모든 도메인 컨트롤러가 신뢰할 수 있는 파트너의 그룹 정책 및 스크립트를 동기화하며, 이는 모든 파트너가 신뢰할 수 없는 파트너인 경우에도 마찬가지입니다.  
  
> [!IMPORTANT]  
> 모든 도메인 컨트롤러가 한 번에 복원된 경우 다음 문서를 사용하여 하나의 도메인 컨트롤러(일반적으로 PDC 에뮬레이터)를 신뢰할 수 있는 것으로 설정하세요. 그래야 나머지 도메인 컨트롤러가 정상 작동으로 복구될 수 있습니다.  
>   
> [BurFlags 레지스트리 키를 사용하여 파일 복제 서비스 복제 집합 다시 초기화](https://support.microsoft.com/kb/290762)  
>   
> [DFSR 복제 된 SYSVOL (예: "D4/D2" FRS 용)에 대 한 신뢰할 수 있는 도메인과 신뢰할 수 없는 동기화를 강제 하는 방법](https://support.microsoft.com/kb/2218556)  
  
> [!WARNING]  
> 같은 하이퍼바이저 호스트에서 포리스트 또는 도메인의 모든 도메인 컨트롤러를 실행 하지 마십시오. 하이퍼바이저가 오프라인 상태로 전환될 때마다 AD DS, Exchange, SQL 및 기타 엔터프라이즈 작업을 중단시키는 단일 실패 지점이 발생합니다. 이는 전체 도메인 또는 포리스트에 하나의 도메인 컨트롤러만 사용하는 것과 같습니다. 여러 플랫폼에서 여러 도메인 컨트롤러를 사용하면 중복성과 내결함성을 유지하는 데 도움이 됩니다.  
  
#### <a name="post-snapshot-replication"></a>스냅숏 후 복제  
스냅샷 만들기가 인바운드로 복제된 이후에 로컬로 발생한 모든 변경 내용이 적용될 때까지 스냅샷을 복원하지 마세요. 다른 도메인 컨트롤러에서 복제를 통해 받지 못한 경우 발생하는 모든 변경 내용이 영구적으로 손실됩니다.  
  
Repadmin.exe를 사용하여 도메인 컨트롤러와 해당 파트너 간의 복제되지 않은 모든 아웃바운드 변경 내용을 표시할 수 있습니다.  
  
1.  다음을 사용하여 DC의 파트너 이름과 DSA 개체 GUID를 반환합니다.  
  
    ```  
    Repadmin.exe /showrepl <DC Name of the partner> /repsto  
    ```  
  
2.  파트너 도메인 컨트롤러의 보류 중인 인바운드 복제를 복원할 도메인 컨트롤러로 반환합니다.  
  
    ```  
    Repadmin.exe /showchanges < Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare>  
    ```  
  
또는 복제되지 않은 변경 내용 수를 확인하기만 합니다.  
  
```  
Repadmin.exe /showchanges <Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare> /statistics  
```  
  
예를 들어 다음 예제에서는 DC4의 복제 파트너 관계를 확인합니다(읽기 쉽도록 출력이 수정되고 중요한 항목은 ***기울임꼴***로 표시됨).  
  
```  
C:\>repadmin.exe /showrepl dc4.corp.contoso.com /repsto  
  
Default-First-Site-Name\DC4  
DSA Options: IS_GC  
Site Options: (none)  
DSA object GUID: 5d083398-4bd3-48a4-a80d-fb2ebafb984f  
DSA invocationID: 730fafec-b6d4-4911-88f2-5b64e48fc2f1  
  
==== OUTBOUND NEIGHBORS FOR CHANGE NOTIFICATIONS ============  
  
DC=corp,DC=contoso,DC=com  
    Default-First-Site-Name\DC3 via RPC  
        DSA object GUID: f62978a8-fcf7-40b5-ac00-40aa9c4f5ad3  
        Last attempt @ 2011-11-11 15:04:12 was successful.  
    Default-First-Site-Name\DC2 via RPC  
        DSA object GUID: 3019137e-d223-4b62-baaa-e241a0c46a11  
        Last attempt @ 2011-11-11 15:04:15 was successful.  
```  
  
이제 DC2 및 DC3과 복제됨을 알았습니다. DC2가 DC4에서 받지 못한 변경 내용 목록을 표시하고 새 그룹 하나가 있음을 확인합니다.  
  
```  
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com  
  
==== SOURCE DSA: (null) ====  
Objects returned: 1  
(0) add CN=newgroup4,CN=Users,DC=corp,DC=contoso,DC=com  
    1> parentGUID: 55fc995a-04f4-4774-b076-d6a48ac1af99  
    1> objectGUID: 96b848a2-df1d-433c-a645-956cfbf44086  
    2> objectClass: top; group  
    1> instanceType: 0x4 = ( WRITE )  
    1> whenCreated: 11/11/2011 3:03:57 PM Eastern Standard Time  
```  
  
다른 파트너를 테스트하여 해당 파트너도 아직 복제되지 않았음을 확인할 수 있습니다.  
  
또는 복제되지 않은 개체를 확인하지 않고 보류 중인 개체만 확인하려는 경우 **/statistics** 옵션을 사용할 수 있습니다.  
  
```  
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com /statistics  
  
***********************************************  
********* Grand total *************************  
Packets:              1  
Objects:              1Object Additions:     1Object Modifications: 0Object Deletions:     0Object Moves:         0Attributes:           12Values:               13  
```  
  
> [!IMPORTANT]  
> 실패하거나 보류 중인 복제를 확인하려면 모든 쓰기 가능한 파트너를 테스트합니다. 하나 이상이 수렴된 경우 전이적 복제가 나머지 서버를 조정하므로 일반적으로 스냅샷을 안전하게 복원할 수 있습니다.  
>   
> /showchanges를 통해 표시되는 복제 오류를 확인하고 이를 해결할 때까지 복제를 계속 진행하지 않아야 합니다.  
  
### <a name="windows-powershell-snapshot-cmdlets"></a>Windows PowerShell 스냅샷 Cmdlet  
다음 Windows PowerShell Hyper-V 모듈 cmdlet은 Windows Server 2012에서 스냅샷 기능을 제공합니다.  
  
```  
Checkpoint-VM  
Export-VMSnapshot  
Get-VMSnapshot  
Remove-VMSnapshot  
Rename-VMSnapshot  
Restore-VMSnapshot  
```  
  


