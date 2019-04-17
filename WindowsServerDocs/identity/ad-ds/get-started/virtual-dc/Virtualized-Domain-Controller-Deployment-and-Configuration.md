---
ms.assetid: b146f47e-3081-4c8e-bf68-d0f993564db2
title: "가상화 도메인 컨트롤러 배포 및 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dcb377cef003458bcdf2e4b3564167cee4310020
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-deployment-and-configuration"></a>가상화 도메인 컨트롤러 배포 및 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에 설명 합니다.  
  
-   [설치 고려 사항](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_InstallConsiderations)  
  
    플랫폼 요구 사항 및 기타 중요 한 제한 포함 됩니다.  
  
-   [가상화 도메인 컨트롤러 복제](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCCloning)  
  
    복제 프로세스는 전체 가상화 도메인 컨트롤러에 자세히 설명 합니다.  
  
-   [안전 복원이 가상화 도메인 컨트롤러](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_VDCSafeRestore)  
  
    가상화 도메인 컨트롤러 안전 복원이 중 수행 되는 유효성 검사에 자세히 설명 합니다.  
  
## <a name="BKMK_InstallConsiderations"></a>설치 고려 사항  
특별 한 역할 나 가상화 도메인 컨트롤러;에 대 한 기능 설치 자동으로 모든 도메인 컨트롤러 복제 및 안전 복원이 기능이 포함 되어 있습니다. 제거 하거나 이러한 기능을 사용 하지 않도록 설정할 수 없습니다.  
  
Windows Server 2012 도메인 컨트롤러를 사용 하 여 Windows Server 2012 광고 DS 스키마 버전 56 이상 및 Windows Server 2003 기본 같은 이상 기능 수준 숲 필요합니다.  
  
두 쓸 수 있는 및 읽기 전용 도메인 컨트롤러 삽 니다 글로벌 카탈로그 및 FSMO 역할 가상화 DC의 모든 측면을 지원 합니다.  
  
> [!IMPORTANT]  
> PDC 에뮬레이터 FSMO 역할 소유자 복제 시작 되 면 온라인 상태 여야 합니다.  
  
### <a name="BKMK_PlatformReqs"></a>플랫폼 요구 사항  
도메인 컨트롤러 가상화 복제 필요합니다.  
  
-   Windows Server 2012 dc 호스트 PDC 에뮬레이터 FSMO 역할  
  
-   PDC 에뮬레이터 복제 작업 중 사용 가능  
  
복제 및 안전 복원이 필요 합니다.  
  
-   Windows Server 2012 가상화 게스트  
  
-   Virtualization 호스트 플랫폼을 지원 VM 세대 ID (VMGID)  
  
검토 아래 표 virtualization 제품 및 지원 가상화 도메인 컨트롤러 및 VM 세대 id입니다.  
  
|||  
|-|-|  
|**Virtualization 제품**|**지원 가상화 도메인 컨트롤러 및 VMGID**|  
|**Hyper-v 기능을 사용 하 여 Microsoft Windows Server 2012 서버**|예|  
|**Microsoft Windows Server 2012 Hyper V 서버**|예|  
|**클라이언트 Hyper-v 사용 하 여 Microsoft Windows 8 기능**|예|  
|**Windows Server 2008 R2 및 Windows Server 2008**|아니요|  
|**타사 virtualization 해결 방법**|공급 업체에 문의|  
  
Microsoft Windows 7 가상 PC, 가상 PC 2007, 가상 PC 2004 및 가상 다운로드할을 지 원하는 경우에 64 비트 게스트를 실행할 수 없는 않으며 VM GenerationID 원하는 수행 합니다.  
  
가상화 제 3 자 제품에 대 한 도움말 및 가상화 도메인 컨트롤러 된 해당 지원 자세에 대 한 직접는 공급 업체에 문의 합니다.  
  
자세한 내용은 대 한 지원 정책은 검토 [가상화 소프트웨어 비 Microsoft 하드웨어에서에서 실행 되는 Microsoft 소프트웨어](https://support.microsoft.com/kb/897615)합니다.  
  
### <a name="critical-caveats"></a>중요 한 주의 사항  
가상화 도메인 컨트롤러 수행 *하지* 다음의 안전 복원이 지원:  
  
-   기존 VHD 파일이 위로 복사 수동으로 VHD 및 VHDX 파일  
  
-   파일 백업 또는 전체 디스크 백업 소프트웨어를 사용 하 여 복원 VHD 및 VHDX 파일  
  
> [!NOTE]  
> VHDX 파일은 새로운에 Windows Server 2012 Hyper-v입니다.  
  
VM GenerationID 의미 적용 이러한 작업 중 어느 따라서 변경 하지 않은 VM 세대 id. 복원 하는 도메인 컨트롤러를 사용 하 여 이러한 방법 중 하나 될 수 있습니다. USN 롤백 및 중 하나에 도메인 컨트롤러 격리 또는 느린 개체 및 숲 정리 다양 한 작업에 대 한 필요성을 소개 합니다.  
  
> [!WARNING]  
> 가상화 도메인 컨트롤러 안전 복원이 시스템 상태 백업 및 광고 DS 휴지통을 대체 아닙니다.  
>   
> 스냅숏을 복원한 후 도메인 컨트롤러에서 발생 한 상황의 스냅숏은 후 이전에 없다고 복제 변경 델타 영구적으로 손실 됩니다. 안전 복원이 구현 실수로 도메인 컨트롤러 차단 하지 못하도록 하려면 자동화 된 신뢰할 수 없는 복원 *만*합니다.  
  
느린 개체 USN 거품에 대 한 자세한 내용은 참조 [8606 오류와 함께 실패 하는 문제를 해결 Active Directory 작업: "부족 특성 개체를 만드는 제공 되었습니다."](https://support.microsoft.com/kb/2028495)합니다.  
  
## <a name="BKMK_VDCCloning"></a>가상화 도메인 컨트롤러 복제  
단계와 관계 없이 Windows PowerShell 또는 그래픽 도구를 사용 하는 가상화 도메인 컨트롤러 복제 하는 단계는 여러 가지가 있습니다. 높은 수준의 하는 세 단계는 다음과 같습니다.  
  
**환경을 준비합니다**  
  
-   1 단계: 하이퍼바이저 VM 세대 ID를 지원 하는지 확인 하 고 따라서 복제  
  
-   2 단계: PDC 에뮬레이터 역할 복제 중 도메인 컨트롤러에 의해 Windows Server 2012를 실행 하 고 온라인으로 연결할 수는 복제 도메인 컨트롤러에서 호스트 확인 합니다.  
  
**소스 도메인 컨트롤러**  
  
-   3 단계: 승인할 복제에 대 한 소스 도메인 컨트롤러  
  
-   4 단계: 호환 되지 않는 서비스 또는 프로그램을 제거 하거나 CustomDCCloneAllowList.xml 파일에 추가 합니다.  
  
-   5 단계: DCCloneConfig.xml 만들기  
  
-   6 단계: 오프 라인 원본 도메인 컨트롤러  
  
**복제 도메인 컨트롤러 만들기**  
  
-   7 단계: 복사 VM 소스 내보내고 XML 아직 복사 하는 경우 추가  
  
-   8 단계: 복사본에서 새 가상 컴퓨터를 만들기  
  
-   9 단계: 복제을 위해 새 가상 컴퓨터 시작  
  
하므로 단계 두 인터페이스는 한 번만 제공 됩니다 Hyper-v Management Console 등 그래픽 도구 또는 Windows PowerShell 등 명령줄 도구를 사용 하는 경우 작업에 절차 차이가 없는 합니다. 이 항목에서는 Windows PowerShell 샘플 복제 하는 프로세스; 종단 간 자동화 탐색할 수 단계에 대해 필요 하지 않습니다. Windows Server 2012에 포함 된 가상된 도메인 컨트롤러의 그래픽 관리 도구가 있습니다.  
  
절차 복제 컴퓨터를 만드는 방법 및 xml 파일; 추가 하는 방법을 선택할 수 있는 경우에 몇 가지 사항 이러한 단계는 세부 정보는 아래에 명시 되어 있습니다. 이 프로세스는 그렇지 않은 경우 변경할.  
  
다음 그림 가상화 도메인 컨트롤러 복제 프로세스를 도메인 이미 존재를 나타냅니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_CloningProcessFlow.png)  
  
### <a name="step-1---validate-the-hypervisor"></a>1 단계 – 하이퍼바이저의 유효성을 검사합니다  
원본 도메인 컨트롤러에서 실행 되 고 지원된 하이퍼바이저 공급 업체는 설명서를 검토 하 여 확인 합니다. 가상화 도메인 컨트롤러 하이퍼바이저 독립 되며 Hyper-v 필요 하지 않습니다.  
  
하이퍼바이저 Microsoft Hyper-v 경우, Windows Server 2012에서 실행 되 고 있는지 확인 합니다. 장치 관리를 사용 하 여 확인할 수 있습니다.  
  
열린 **Devmgmt.msc** 검사 **시스템 장치** 에 대 한 Microsoft Hyper-v 디바이스 및 드라이버를 설치 합니다. 가상화 도메인 컨트롤러에 필요한 시스템 특정 디바이스의 **Microsoft Hyper-v 세대 카운터** (드라이버: vmgencounter.sys).  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVVMGenIDCounter.png)  
  
### <a name="step-2---verify-the-pdce-fsmo-role"></a>2 단계-PDCE FSMO 역할 확인  
DC 복제 하기 전에 주 도메인 컨트롤러 에뮬레이터 FSMO 호스트 도메인 컨트롤러 Windows Server 2012를 실행을 확인 해야 합니다. PDC (PDCE) 에뮬레이터 몇 가지 이유로 필요 합니다.  
  
1.  PDCE 만들어 특수 **복제 가능한 도메인 컨트롤러** 그룹화 하 고 해당 사용 권한을 자체 복제 하는 도메인 컨트롤러를 허용 하는 도메인의 루트 설정 합니다.  
  
2.  DC 복제 컴퓨터 개체를 만들기 위해 DRSUAPI RPC 프로토콜을 사용 하 여 직접 PDCE 복제 도메인 컨트롤러에 접속 합니다.  
  
    > [!NOTE]  
    > Windows Server 2012 확장 하 여 기존 디렉터리 복제 서비스 () 원격 기능이 (UUID **E3514235-4B06-11D1-AB04-00C04FC2DCD2**) 새 RPC 메서드를 포함 하도록 **IDL_DRSAddCloneDC** (Opnum **28**). **IDL_DRSAddCloneDC** 방법 기존 도메인 컨트롤러 개체의 특성을 복사 하 여 새 도메인 컨트롤러 개체를 만듭니다.  
    >   
    > 컴퓨터, 서버, NTDS 설정, FRS, DFSR, 및 연결 개체 각 도메인 컨트롤러에 유지 되는 도메인 컨트롤러의 상태 구성 됩니다. 개체를 복제 하는 경우이 RPC 메서드 새 도메인 컨트롤러의 해당 개체와 원래 도메인 컨트롤러에 대 한 모든 참조를 바꿉니다. 발신자 오른쪽 DS-복제-도메인 컨트롤러 도메인 이름 컨텍스트에 액세스 제어가 있어야 합니다.  
    >   
    > 이 새로운 방법 사용 PDC 에뮬레이터 도메인 컨트롤러에 직접 액세스 발신자에서 항상 필요합니다.  
    >   
    > 새로운이 RPC 방법 이기 때문에 네트워크 분석 소프트웨어는 기존 UUID E3514235 4B06-11 차원 1-AB04-00C04FC2DCD2에서 새 Opnum 28에 대 한 필드를 포함 하도록 업데이트 파서 필요 합니다. 그렇지 않은 경우이 교통을 분석할 수 없습니다.  
    >   
    > 자세한 내용은 참조 [4.1.29 IDL_DRSAddCloneDC (Opnum 28)](https://msdn.microsoft.com/en-us/library/hh554213(v=prot.13).aspx)합니다.  
  
***즉, 아닌 완전히 라우팅된 네트워크를 사용 하는 경우 네트워크 세그먼트 PDCE에 액세스할 수 있는 필요 가상화 도메인 컨트롤러 복제***합니다. AD DS 논리 사이트 정보를 업데이트 하려면 신중 하 게 되는-실제 도메인 컨트롤러-처럼 복제 후 복제 도메인 컨트롤러 서로 다른 네트워크로 이동 하는 것이 좋습니다.  
  
> [!IMPORTANT]  
> 단일 도메인 컨트롤러만 포함 하는 도메인을 복제할 때 복제 복사본 시작 하기 전에 원본 DC 다시 온라인 상태가 확인 해야 합니다. 프로덕션 도메인 항상 두 개 이상 도메인 컨트롤러 있어야 합니다.  
  
#### <a name="active-directory-users-and-computers-method"></a>Active Directory 사용자와 컴퓨터 방법  
  
1.  도메인 마우스 오른쪽 단추로 클릭 하 고 클릭 차례로 스냅인를 사용 하 여, **작업 마스터**합니다. PDC 탭 라는 도메인 컨트롤러 기록한 대화 상자를 닫습니다.  
  
2.  해당 DC 컴퓨터 개체 마우스 오른쪽 단추로 클릭 한 **속성**, 하 고 다음 운영 체제 정보 확인.  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
PDC 에뮬레이터의 버전을 반환 다음 Active Directory Windows PowerShell 모듈 cmdlet을 결합할 수 있습니다.  
  
```  
Get-adddomaincontroller  
Get-adcomputer  
```  
  
도메인 제공 되지 않는 경우이 cmdlet 가정 실행 되는 컴퓨터의 도메인.  
  
다음 명령을 반환 PDCE 및 운영 체제 정보:  
  
```  
get-adcomputer(Get-ADDomainController -Discover -Service "PrimaryDC").name -property * | format-list dnshostname,operatingsystem,operatingsystemversion  
```  
  
아래의이 예제를 도메인 이름 지정 하 고 Windows PowerShell 파이프라인 하기 전에 반환된 속성 필터링 보여 줍니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PDCOSInfo.png)  
  
### <a name="step-3---authorize-a-source-dc"></a>3 단계-Authorize 소스 DC  
원본 도메인 컨트롤러에서 액세스 제어 권한을 (자동차) 있어야 **DC 자체 복제를 만들 수 있도록** NC 머리 도메인에 있습니다. 기본적으로 유명 그룹 **복제 가능한 도메인 컨트롤러** 이 권한이 있는지와 구성원이 포함 되어 있습니다. Windows Server 2012 도메인 컨트롤러에 전송 하는 해당 FSMO 역할 때 PDCE이이 그룹을 만듭니다.  
  
#### <a name="active-directory-administrative-center-method"></a>관리 센터 active Directory 방법  
  
1.  Dsac.exe 시작 하 고 원본 DC, 이동 한 다음 해당 세부 정보 페이지를 엽니다.  
  
2.  에 **소속** 섹션을 추가 **복제 가능한 도메인 컨트롤러** 해당 도메인에 대 한 그룹입니다.  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
다음 Active Directory Windows PowerShell 모듈 cmdlet 결합할 수 **get adcomputer** 및 **추가 adgroupmember** 도메인 컨트롤러를 추가 하는 **복제 가능한 도메인 컨트롤러** 그룹:  
  
```  
Get-adcomputer <dc name> | %{add-adgroupmember "cloneable domain controllers" $_.samaccountname}  
```  
  
예를 들어 서버 d c 1 그룹 구성원의 고유 이름을 지정를 않고도 그룹에 추가:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_AddDcToGroup.png)  
  
#### <a name="rebuilding-default-permissions"></a>다시 기본 권한  
이 권한을 도메인 헤드를 제거한 경우 복제 작동 하지 않습니다. Windows PowerShell 또는 Active Directory 관리 센터를 사용 하는 권한을 다시 만들 수 있습니다.  
  
##### <a name="active-directory-administrative-center-method"></a>관리 센터 active Directory 방법  
  
1.  열기 **Active Directory 관리 센터**, 도메인 헤드를 마우스 오른쪽 단추로 클릭, **속성**를 클릭는 **확장** 탭을 클릭 **보안**을 차례로 클릭 하 고 **고급**합니다. 클릭 **만이 개체**합니다.  
  
2.  클릭 **추가**, **선택할 개체 이름을 입력**, 그룹 이름을 입력 **도메인 컨트롤러 복제할 수 있습니다.**  
  
3.  사용 권한에서 **DC 자체 복제를 만들 수 있도록**을 차례로 클릭 하 고 **확인**합니다.  
  
> [!NOTE]  
> 기본 권한 제거 하 고 개별 도메인 컨트롤러를 추가할 수도 있습니다. 그러나 유지 관리 문제가 발생할 가능성이 높습니다. 이렇게 새 관리자가 사용자를 인식 하지 않습니다. 기본 설정을 변경 보안을 강화 않는 및 해서는 안 됩니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
관리자 권한이 Windows PowerShell 콘솔 프롬프트에서 다음 명령을 사용 합니다. 이 명령을 도메인 이름 검색 되 고 기본 권한을에 다시 추가:  
  
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
  
또는 실행 하 고 샘플 [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms) 콘솔 영향을 받는 도메인에 있는 도메인 컨트롤러에서 관리자 권한으로 시작 되는 위치를 Windows PowerShell 콘솔에서 합니다. 자동으로 사용 권한을 설정 합니다. 샘플이 모듈이 부록에 있습니다.  
  
### <a name="step-4---remove-incompatible-applications-or-services-if-not-using-customdccloneallowlistxml"></a>4 단계-제거 호환 되지 않는 응용 프로그램 또는 서비스 (되지 않은 경우 사용 하 여 CustomDCCloneAllowList.xml)  
프로그램 또는 서비스 이전에 다운로드 ADDCCloningExcludedApplicationList-에서 반환 *는 CustomDCCloneAllowList.xml에 추가 되지* -복제 이전 제거 해야 합니다. 응용 프로그램 또는 서비스가 제거 권장 되는 방법입니다.  
  
> [!WARNING]  
> 호환 되지 않는 모든 프로그램 또는 서비스는 CustomDCCloneAllowList.xml에 추가 하거나 제거 하지 복제 수 없습니다.  
  
Get AdComputerServiceAccount cmdlet 도메인에 있는 모든 독립 실행형 관리 서비스 계정 (Msa)를 찾을 수 사용 및 경우이 컴퓨터 사용 하는 중입니다. 모든 MSA가 설치 된 경우 제거 ADServiceAccount cmdlet 로컬에 설치 된 서비스 계정을 제거 하려면 사용 합니다. 6 단계에서 원본 도메인 컨트롤러 오프 라인으로 사용 작업이 완료 되 면 서버 다시 온라인 상태가 되 면 ADServiceAccount 설치를 사용 하 여 MSA 다시 추가할 수 있습니다. 자세한 내용은 참조 [제거 ADServiceAccount](https://technet.microsoft.com/en-us/library/hh852310)합니다.  
  
> [!IMPORTANT]  
> -Windows Server 2008 R2에 처음 릴리스-독립 실행형 Msa 그룹 Msa와 Windows Server 2012에서 바뀌었습니다. 그룹 Msa 복제를 지원 합니다.  
  
### <a name="step-5---create-dccloneconfigxml"></a>5 단계-DCCloneConfig.xml 만들기  
DcCloneConfig.xml 파일은 도메인 컨트롤러 복제할 필요 합니다. 내용을 새 컴퓨터 이름 및 IP 주소 같은 고유 세부 정보를 지정할 수 있습니다.  
  
응용 프로그램 또는 잠재적으로 호환 되지 않는 Windows 서비스 원본 도메인 컨트롤러에 설치 하지 않으면 CustomDCCloneAllowList.xml 파일 선택 사항입니다. 정확한 이름, 형식 및 배치; 공간이 필요 합니다. 그렇지 않은 경우 복제 실패 합니다.  
  
따라서 항상 XML 파일을 작성 하 여 정확한 위치에 배치 Windows PowerShell cmdlet을 사용 해야 합니다.  
  
#### <a name="generating-with-new-addccloneconfigfile"></a>새 ADDCCloneConfigFile 생성 하는 경우  
Active Directory Windows PowerShell 모듈 새로운 cmdlet을 Windows Server 2012에 포함 되어 있습니다.  
  
```  
New-ADDCCloneConfigFile  
```  
  
Cmdlet 복제 하는 제안된 원본 도메인 컨트롤러에서 실행할 수 있습니다. Cmdlet 여러 인수 지원 하 고을 사용 하면 항상 테스트 컴퓨터와 지정 하지 않는 한 실행 되는 위치 환경-오프 라인 인수 합니다.  
  
||||  
|-|-|-|  
|**ActiveDirectory**<br /><br />**Cmdlet**|**인수**|**설명**|  
|**새 ADDCCloneConfigFile**|*<no argument specified>*|DSA 작업 디렉터리에 빈 DcCloneConfig.xml 파일을 만들고 (기본: %systemroot%\ntds)|  
||-CloneComputerName|복제 DC 컴퓨터 이름을 지정합니다. 문자열 데이터 형식 있습니다.|  
||경로|폴더는 DcCloneConfig.xml 만들기를 지정 합니다. 지정 하지 DSA 작업 디렉터리에 기록 (기본: systemroot%\ntds %). 문자열 데이터 형식 있습니다.|  
||-SiteName|복제 컴퓨터 계정 만드는 동안 가입 광고 논리 사이트 이름을 지정 합니다. 문자열 데이터 형식 있습니다.|  
||-IPv4Address|복제 컴퓨터의 고정 IPv4 주소를 지정합니다. 문자열 데이터 형식 있습니다.|  
||-IPv4SubnetMask|고정 IPv4 서브넷 마스크 복제 컴퓨터의 지정합니다. 문자열 데이터 형식 있습니다.|  
||-IPv4DefaultGateway|복제 컴퓨터의 정적 IPv4 기본 게이트웨이 주소를 지정합니다. 문자열 데이터 형식 있습니다.|  
||-IPv4DNSResolver|복제 컴퓨터의 IPv4 DNS 정적 항목 쉼표로 구분 목록에 지정합니다. 배열 데이터 형식 있습니다. 최대 4 개의 항목을 제공할 수 있습니다.|  
||-PreferredWINSServer|기본 WINS 서버 고정 IPv4 주소를 지정합니다. 문자열 데이터 형식 있습니다.|  
||-AlternateWINSServer|보조 WINS 서버의 고정 IPv4 주소를 지정합니다. 문자열 데이터 형식 있습니다.|  
||-IPv6DNSResolver|복제 컴퓨터의 IPv6 DNS 정적 항목 쉼표로 구분 목록에 지정합니다. 고정 정보 Ipv6 가상화 도메인 컨트롤러 복제에 명시 된 방법이 없습니다. 배열 데이터 형식 있습니다.|  
||-오프 라인|유효성 검사를 수행 하지 하 고 기존 모든 dccloneconfig.xml를 덮어씁니다. 매개에 있습니다. 자세한 내용은 참조 [실행 중인 새-ADDCCloneConfigFile 오프 라인 모드에서](../../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode)합니다.|  
||*고정*|고정 IP 인수 IPv4SubnetMask, IPv4SubnetMask, 또는 IPv4DefaultGateway 지정 하는 경우 필요 합니다. 매개에 있습니다.|  
  
테스트 수행 온라인 모드에서 실행 하는 경우:  
  
-   PDC 에뮬레이터는 Windows Server 2012 이상  
  
-   원본 도메인 컨트롤러 복제할 수 도메인 컨트롤러 그룹의 회원은  
  
-   원본 도메인 컨트롤러 제외 응용 프로그램 또는 서비스 포함 되지 않는  
  
-   원본 도메인 컨트롤러 포함 되어 있지 않으면 지정된 경로에 DcCloneConfig.xml  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewDCCloneConfig.png)  
  
### <a name="step-6---take-the-source-domain-controller-offline"></a>6 단계-오프 라인 원본 도메인 컨트롤러  
실행 중인 소스 DC; 복사할 수는 없습니다. 적절 하 게 종료 해야 합니다. Graceless 정전에 의해 중단 도메인 컨트롤러를 복제할 하지 않습니다.  
  
#### <a name="graphical-method"></a>그래픽 방법  
실행 중인 DC 내 종료 단추 또는 Hyper-v 관리자 종료 단추를 사용 합니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_Shutdown.png)  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVShutdown.png)  
  
#### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
가상 컴퓨터 다음 cmdlet 중 하나를 사용 하 여 종료할 수 있습니다.  
  
```  
Stop-computer  
Stop-vm  
```  
  
중지 컴퓨터를 지 원하는 가상화에 관계 없이 컴퓨터를 종료 하는 레거시 Shutdown.exe 유틸리티 비슷합니다 cmdlet입니다. 중지 vm Windows Server 2012 Hyper-v Windows PowerShell 모듈에 새 cmdlet 이며 Hyper-v 관리자에 전원 옵션에는 것과 같습니다. 두 번째에 유용 랩 환경 도메인 컨트롤러가 자주 가상된 개인 네트워크에서 작동 합니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopComputer2.png)  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_StopVM.png)  
  
### <a name="step-7---copy-disks"></a>7 단계-복사 디스크  
관리 선택 복사 단계에서 필요 합니다.  
  
-   Hyper-v 하지 않고 수동으로 디스크에 복사  
  
-   Hyper-v를 사용 하 여 VM 내보내기  
  
-   Hyper-v를 사용 하 여 병합된 디스크를 내보내려면  
  
가상 컴퓨터의 디스크를 모두 복사 해야, 시스템 드라이브 뿐 아니라 합니다. 원본 도메인 컨트롤러 보관용 디스크를 사용 하는 또 다른 Hyper-v 호스트 복제 도메인 컨트롤러 이동 하려는 경우 내보내야 합니다.  
  
원본 도메인 컨트롤러에만 해당 하는 경우 권장 수동으로 디스크 복사 *한* 드라이브. 내보내기/가져오기는 Vm와에 대 한 것이 좋습니다 *여러 개* 같은 여러 Nic 드라이브 또는 기타 복잡 한 가상된 하드웨어 사용자 지정 합니다.  
  
파일을 수동으로 복사, 복사 전에 모든 스냅숏은 삭제 합니다. VM를 내보내는 경우 스냅숏을 내보내기 전에 삭제 하거나 새 VM에서 가져온 후 삭제 합니다.  
  
> [!WARNING]  
> 스냅숏을은 도메인 컨트롤러를 이전 상태로 되돌릴 수 있는 디스크 차이 됩니다. 도메인 컨트롤러 복제 하 고 다음 해당 미리 복제 스냅샷이 복원 하는 경우 숲에서 중복 된 도메인 컨트롤러 관련 종료 것입니다. 새로 복제 된 도메인 컨트롤러에서 이전 스냅숏을에 값이 있습니다.  
  
#### <a name="manually-copying-disks"></a>수동으로 디스크를 복사  
  
##### <a name="hyper-v-manager-method"></a>Hyper-v 관리자 방법  
Hyper-v 관리자 스냅인을 사용 하 여 어떤 디스크와 원본 도메인 컨트롤러 관련 된 확인 합니다. 검사 옵션을 사용 하 여 유효성을 검사할 도메인 컨트롤러 보관용 디스크 (필요도 부모 디스크를 복사 하는) 사용 하는 경우  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVInspect.png)  
  
스냅숏을 삭제 하려면 VM 선택한 스냅숏을 하위 삭제 합니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDeleteSnapshot.gif)  
  
다음 사용 하 여 Windows 탐색기, Xcopy.exe, 또는 Robocopy.exe VHD 또는 VHDX 파일 수동으로 복사할 수 있습니다. 특별 한 없음 단계는 필요 합니다. 다른 폴더로 이동 하는 경우에 파일 이름을 변경 하는 것이 좋습니다.  
  
> [!NOTE]  
> Lan 호스트 컴퓨터 간에 복사 하는 경우 (Gbit 1 이상), **Xcopy.exe /J** 옵션 보다 훨씬 더 큰 대역폭 사용량이 저하 다른 도구를 상당히 빠르게 VHD/VHDX 파일을 복사 합니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
Windows PowerShell를 사용 하 여 디스크를 확인 하려면 Hyper-v 모듈 사용:  
  
```  
Get-vmidecontroller  
Get-vmscsicontroller  
Get-vmfibrechannelhba  
Get-vmharddiskdrive  
```  
  
예를 들어 모든 IDE 하드 드라이브 라는 VM에서 반환할 수 있습니다 **d c 2** 다음 샘플에서:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_ReturnIDE.png)  
  
디스크를 가리키는 AVHD 또는 AVHDX 파일, 경우 스냅숏을 수 있습니다. 실제 VHD 또는 VHDX 병합 디스크와 관련 된 스냅숏을 삭제 하려면 cmdlet 사용:  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
예를 들어 VM에서 모든 스냅숏을 삭제 하려면 d c 2 SOURCECLONE 라는:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_DelSnapshots.png)  
  
Windows PowerShell를 사용 하 여 파일을 복사 하려면 다음과 같은 cmdlet 사용:  
  
```  
Copy-Item  
```  
  
VM cmdlet 자동화 지원 하기 위해 파이프라인에 결합 되어 있습니다. 파이프라인은 사용 데이터를 전달 하기 위해 여러 cmdlet 간의 채널 합니다. 예를 들어 오프 라인 원본 도메인 컨트롤러의 드라이브에 복사 라는 c:\temp\copy.vhd 정확한 경로 해당 시스템 드라이브를 알고를 않고도 새 디스크에 d c 2 SOURCECLONE 라는:  
  
```  
Get-VMIdeController dc2-sourceclone | Get-VMHardDiskDrive | select-Object {copy-item -path $_.path -destination c:\temp\copy.vhd}  
```  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSCopyDrive.png)  
  
> [!IMPORTANT]  
> 사용 하지 않는 가상 디스크 파일을 대신 하 여 실제 하드 디스크 대로 복제를 통과 디스크를 사용할 수 없습니다.  
  
> [!NOTE]  
> 파이프라인을 사용 하 여 더 많은 Windows PowerShell 작업에 대 한 자세한 내용은 참조 [파이핑 및 Windows powershell에서 파이프라인](https://technet.microsoft.com/en-us/library/ee176927.aspx)합니다.  
  
#### <a name="exporting-the-vm"></a>VM 내보내기  
디스크에 복사 하는 대신, 복사본으로 전체 Hyper-v VM 내보낼 수 있습니다. 자동으로 내보내기 VM에 이름을 지정 하 고 모든 디스크 및 구성 정보가 포함 된 폴더를 만듭니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVExport.png)  
  
##### <a name="hyper-v-manager-method"></a>Hyper-v 관리자 방법  
Hyper-v 관리자 VM 내보내기:  
  
1.  원본 도메인 컨트롤러를 마우스 오른쪽 단추로 클릭 한 **내보내려면**합니다.  
  
2.  내보낼 컨테이너도 기존 폴더를 선택 합니다.  
  
3.  표시를 중지 하려면 상태 열 때까지 기다리는 **내보내기**합니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
Hyper-v Windows PowerShell 모듈을 사용 하 여 VM를 내보내려면 cmdlet 사용:  
  
```  
Export-vm  
```  
  
예를 들어 VM 내보내기 C:\VM 라는 폴더 d c 2 SOURCECLONE 라는:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSExport.png)  
  
> [!NOTE]  
> 새로운 Windows Server 2012 Hyper-v 지원 내보내고 가져오는 기능을이 교육이 범위를 벗어나는 합니다. 자세한 내용은 TechNet을 검토 합니다.  
  
#### <a name="exporting-merged-disks-using-hyper-v"></a>Hyper-v를 사용 하 여 병합된 디스크 내보내기  
마지막 옵션 Hyper-v 내 디스크 병합 하 고 변환 옵션을 사용 하는 것입니다. 이러한 스냅숏을 AVHD/AVHDX 파일이 포함 된 단일 새 디스크에 포함 된 경우에 기존 디스크 구조-의 복사본을 만들 수 있습니다. 수동 디스크 복사 시나리오 같은이 C:\\ 등 드라이브를 사용 하는 간단한 가상 컴퓨터에 대 한 주로 됩니다. 그 외로운 장점은, 복사 수동으로 달리 필요가 없습니다 먼저 스냅숏을 삭제 하입니다. 이 작업을 보다 간단 하 게 스냅숏을 삭제 하 고 디스크 복사 느린 것은 아닙니다.  
  
##### <a name="hyper-v-manager-method"></a>Hyper-v 관리자 방법  
디스크를 만들려면 병합 Hyper-v 관리자를 사용 하 여 다음과 같습니다.  
  
1.  클릭 **디스크 편집**합니다.  
  
2.  최저 자녀 디스크를 찾습니다. 예를 들어, 보관용 디스크를 사용 하는 경우 자녀 디스크가 최저 자녀입니다. 현재 선택 된 스냅숏을 가상 컴퓨터에 스냅숏을 (또는 여러 개의 기능)를 경우 최저 자녀 디스크 수 있습니다.  
  
3.  선택는 **병합** 옵션은 전체 상위 자식 구조 아웃 단일 디스크를 만드는 합니다.  
  
4.  새 가상 하드 디스크를 선택 하 고 경로 제공 합니다. 이 기존 VHD/VHDX 파일을 이전 스냅숏은 복원 하는 위험에 노출 하지 않은 단일 새로운 휴대용 장치 조정 합니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
Hyper-v Windows PowerShell 모듈을 사용 하는 부모님의 복잡 한 집합에서 병합된 디스크를 만들려면 cmdlet 사용:  
  
```  
Convert-vm  
```  
  
예를 들어 VM의 디스크 스냅숏 (이 이번 보관용 디스크를 포함 하지 않음)의 전체 체인 내보내고 디스크에 새 단일 디스크 부모 이름이 지정 DC4 복제 됩니다. VHDX:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSConvertVhd.png)  
  
#### <a name="BKMK_Offline"></a>XML 오프 라인 시스템 디스크에 추가  
Dccloneconfig.xml DC 실행 소스를 복사 무엇을 오프 라인 복사 내보낸 시스템 디스크 업데이트 dccloneconfig.xml 파일 이제 복사 해야 합니다. 에 따라 설치 된 응용 프로그램 이전에 다운로드 ADDCCloningExcludedApplicationList와 검색, 파일을 복사 CustomDCCloneAllowList.xml 디스크에 할 수 있습니다.  
  
다음 위치 DcCloneConfig.xml 파일 포함 될 수 있습니다.  
  
1.  작업 디렉터리 DSA  
  
2.  %windir%\NTDS  
  
3.  순서로 나열 루트 드라이브의 드라이브 문자가의 읽기/쓰기 이동식 미디어  
  
이러한 경로 구성할 수는 없습니다. 복제 시작 된 후 복제 검사 특정 순서 및 사용 하는 첫 번째 DcCloneConfig.xml 해당 저장할 위치로 이러한 위치 파일 폴더의 내용에 관계 없이 검색 합니다.  
  
다음 위치 CustomDCCloneAllowList.xml 파일 포함 될 수 있습니다.  
  
1.  찾아  
  
    AllowListFolder (*REG_SZ*)  
  
2.  작업 디렉터리 DSA  
  
3.  %windir%\NTDS  
  
4.  순서로 나열 루트 드라이브의 드라이브 문자가의 읽기/쓰기 이동식 미디어  
  
새로 ADDCCloneConfigFile를 실행할 수 있는 **-오프 라인** 인수 (라고도 오프 라인 모드) DcCloneConfig.xml 파일을 만들고 정확한 위치를 합니다. 다음 예제 새로 ADDCCloneConfigFile 오프 라인 모드에서 실행 하는 방법을 보여 줍니다.  
  
고정 IPv4 주소와 "REDMOND" 이라고 하는 사이트에서 오프 라인 모드에서 CloneDC1 라는 복제 도메인 컨트롤러 만들 수를 입력 합니다.  
  
```  
New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS  
```  
  
고정 IPv4와 고정 IPv6 설정을 입력 오프 라인 모드에서 Clone2 라는 복제 도메인 컨트롤러 만들려면 다음과 같습니다.  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS  
```  
  
만들어 복제본 도메인 컨트롤러 고정 IPv4와 동적 IPv6 설정 오프 라인 모드에서 DNS 확인자 설정에 대 한 여러 DNS 서버를 지정를 입력 합니다.  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS   
```  
  
동적 IPv4와 고정 IPv6 설정을 입력 오프 라인 모드에서 Clone1 라는 복제 도메인 컨트롤러 만들려면 다음과 같습니다.  
  
```  
New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS  
```  
  
동적 IPv4와 동적 IPv6 설정 오프 라인 모드에서 복제본 도메인 컨트롤러를 만들려면 입력 합니다.  
  
```  
New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS  
  
```  
  
##### <a name="windows-explorer-method"></a>Windows 탐색기 방법  
이제 Windows Server 2012 장착 VHD 및 VHDX 파일에 대 한 그래픽 옵션을 제공 합니다. Windows Server 2012에서 데스크톱 경험 기능 설치가 필요합니다.  
  
1.  원본 DC의 시스템 드라이브나 DSA 작업 디렉터리 위치 폴더를 포함 하는 새로 복사 VHD/VHDX 파일 클릭 한 다음 클릭 **탑재** 에서 **디스크 이미지 도구** 메뉴 합니다.  
  
2.  지금 장착 된 드라이브에 유효한 위치로 XML 파일을 복사 합니다. 폴더에 대 한 권한을 대 한 하 라는 메시지가 표시 될 수 있습니다.  
  
3.  탑재 드라이브 누르고 **꺼내기** 에서 **디스크 도구** 메뉴 합니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVClickMountedDrive.png)  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVDetailsMountedDrive.gif)  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVEjectMountedDrive.gif)  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
또는 오프 라인 디스크 탑재 하 고 사용 하 여 Windows PowerShell cmdlet XML 파일을 복사할 수 있습니다.  
  
```  
mount-vhd  
get-disk  
get-partition  
get-volume  
Add-PartitionAccessPath  
Copy-Item  
```  
  
프로세스를 완전히 제어할을 수 있습니다. 드라이브 수 예를 들어 특정 드라이브 문자가 포함 된 탑재 된 파일을 복사할 및 드라이브 분리 합니다.  
  
```  
mount-vhd <disk path> -passthru -nodriveletter | get-disk | get -partition | get-volume | get-partition | where {$_.partition number -eq 2} | Add-PartitionAccessPath -accesspath <drive letter>  
  
copy-item <xml file path><destination path>\dccloneconfig.xml  
  
dismount-vhd <disk path>  
```  
  
예를 들어:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSMountVHD.png)  
  
또는 있습니다 사용할 수 있는 새로운 **산 DiskImage** 파일 VHD (또는 ISO)이 탑재 cmdlet 합니다.  
  
### <a name="step-8---create-the-new-virtual-machine"></a>8 단계-새 가상 컴퓨터 만들기  
복제 프로세스를 시작 하기 전에 최종 구성 단계는 만드는 복사한 원본 도메인 컨트롤러에서 디스크를 사용 하는 새 VM 것입니다. 선택 영역 복사 디스크 단계에 따라 두 가지 옵션이 있습니다.  
  
1.  복사한 디스크에 새 VM 연결  
  
2.  내보낸된 VM 가져오기  
  
#### <a name="associating-a-new-vm-with-copied-disks"></a>복사한 디스크에 새 VM 연결  
직접 복사한 시스템 디스크를 복사한 디스크를 사용 하 여 새 가상 컴퓨터를 만들어야 합니다. 새 VM; 만들 때 하이퍼바이저 VM 세대 ID를 자동으로 설정 VM 또는 Hyper-v 호스트 구성을 변경 해야 합니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVConnectVHD.gif)  
  
##### <a name="hyper-v-manager-method"></a>Hyper-v 관리자 방법  
  
1.  새 가상 컴퓨터를 만듭니다.  
  
2.  VM 이름, 메모리 및 네트워크 지정 합니다.  
  
3.  가상 하드 디스크 연결 페이지에서 시스템 복사 디스크를 지정 합니다.  
  
4.  VM 만들기 마법사를 완료 합니다.  
  
여러 개의 디스크 인 경우 네트워크 어댑터 또는 기타 사용자 지정 하도록 구성 도메인 컨트롤러를 시작 하기 전에 합니다. 디스크 복사 중 "내보내기 가져오기" 방법 복잡 한 Vm 좋습니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
Hyper-v Windows PowerShell 모듈 자동화 VM 상황은 다음과 같은 cmdlet 사용 하 여 Windows Server 2012에서 사용할 수 있습니다.  
  
```  
New-VM  
```  
  
예를 들어, 여기서 DC4 CLONEDFROMDC2 VM를 사용 하 여 만들어집니다 1GB의 RAM c:\vm\dc4-systemdrive-clonedfromdc2.vhd 파일에서 부팅 하 고 10.0 가상 네트워크를 사용 하 여 다음과 같습니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSNewVM.png)  
  
#### <a name="import-vm"></a>VM 가져오기  
가져올 해야 사용자 VM, 이전에 내보낼 경우 복사본을으로 다시 합니다. 내보낸된 XML 모든 이전 설정, 드라이브, 네트워크 및 설정 메모리를 사용 하 여 컴퓨터를 다시 만드는 데 사용 합니다.  
  
동일한 내보낸된 VM에서 추가 복사본을 만들 하려는 경우 필요에 따라 내보낸된 VM의 복사본을 확인 합니다. 가져오기 각 복사본을 사용 합니다.  
  
> [!IMPORTANT]  
> 이 사용 하 여 중요는 **복사** 옵션을 내보내기 소스의; 모든 정보를 유지 서버를 가져오는 **이동** 또는 **제자리에** 같은 Hyper-v 호스트 서버의 완료 하는 경우 정보 충돌이 발생 합니다.  
  
##### <a name="hyper-v-manager-method"></a>Hyper-v 관리자 방법  
Hyper-v 관리자 스냅인를 사용 하 여 가져올:  
  
1.  클릭 **가상 컴퓨터를 가져오려면**  
  
2.  에 **폴더를 찾습니다** 페이지에서 검색 단추를 사용 하 여 내보낸된 VM 정의 파일을 선택 합니다.  
  
3.  에 **가상 컴퓨터 선택** 페이지에서 원본 컴퓨터를 클릭 합니다.  
  
4.  에 **가져오기 유형 선택** 페이지, 클릭 **복사 가상 컴퓨터 (새 고유 ID를 생성)**, 클릭 한 다음 **완료**합니다.  
  
5.  동일한 Hyper-v 호스트;에서 가져올 경우 가져온된 VM 이름 바꾸기 이름이 같은 내보낸된 원본 도메인 컨트롤러 경우일 됩니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportLocateFolder.png)  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportSelectVM.png)  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportChooseType.gif)  
  
Hyper-v 관리 스냅인를 사용 하 여 모든 가져온된 스냅숏의 제거 해야 합니다.  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_HyperVImportDelSnap.gif)  
  
> [!WARNING]  
> 삭제 된 가져온된 스냅숏을 매우 중요 합니다. 적용 하는 경우를 복제 오류, 중복 IP 정보 및 기타 중단 복제 도메인 컨트롤러 이전-및 줄 라이브-DC의 상태를 반환 것 됩니다.  
  
##### <a name="windows-powershell-method"></a>Windows PowerShell 방법  
Windows Server 2012를 사용 하 여 다음 cmdlet에 VM 가져오기 자동화 Hyper-v Windows PowerShell 모듈에 사용할 수 있습니다.  
  
```  
Import-VM  
Rename-VM  
```  
  
예를 들어 여기 내보낸된는 자동으로 결정된 XML 파일을 사용 하 여 다음 새 VM 이름 DC5 CLONEDFROMDC2 이름이 즉시 가져온 VM d c 2 복제:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSImportVM.png)  
  
다음 cmdlet 사용 하 여 모든 가져온된 스냅숏의 제거 해야 합니다.  
  
```  
Get-VMSnapshot  
Remove-VMSnapshot  
```  
  
예를 들어:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSGetVMSnap.png)  
  
> [!WARNING]  
> 컴퓨터를 가져올 때 고정 MAC 주소 된에 할당 되지 원본 도메인 컨트롤러 있는지 확인 하세요. 고정 MAC 소스 컴퓨터를 복제 하는 경우 컴퓨터에 복사한을 제대로 되지 보내거나 받을 네트워크 트래픽을 합니다. 경우에는이 새로운 고유한 고정 하거나 동적 MAC 주소를 설정 합니다. VM 명령을 사용 하 여 고정 MAC 주소를 사용 하는 경우 확인할 수 있습니다.  
>   
> **Get VM VMName**   
>  ***테스트 vm* | Get VMNetworkAdapter | fl \ ***  
  
### <a name="step-9---clone-the-new-virtual-machine"></a>9 단계-새 가상 컴퓨터를 복제  
필요에 따라 복제 시작 하기 전에 오프 라인 복제 원본 도메인 컨트롤러 다시 시작 합니다. PDC 에뮬레이터 온라인에 관계 없이 인지 확인 합니다.  
  
복제을 시작 하려면 하기만 하면 새 가상 컴퓨터를 시작 합니다. 프로세스를 자동으로 시작 하 고 복제 완료 된 후 도메인 컨트롤러 자동으로 부팅 합니다.  
  
> [!IMPORTANT]  
> 오랜된 시간 동안 해제 도메인 컨트롤러 유지 권장 되지 않습니다 및 복제 DC 원본으로 동일한 사이트 참가 하 고, 경우 초기 내 및 간 사이트 복제 토폴로지 오래 걸릴 수 있습니다 원본 도메인 컨트롤러 오프 라인 상태인 경우 빌드 합니다.  
  
Windows PowerShell를 사용 하 여 VM 시작, 새 Hyper-v 모듈 cmdlet는 다음과 같습니다.  
  
```  
Start-VM  
```  
  
예를 들어:  
  
![가상된 DC 배포](media/Virtualized-Domain-Controller-Deployment-and-Configuration/ADDS_VDC_PSStartVM.png)  
  
컴퓨터가 복제 완료 되 면는 도메인 컨트롤러 고 일반적인 작업을 확인 정상적으로에 로그온 수 있습니다. 오류가 경우 확인을 위해 디렉터리 서비스 복원 모드를 시작 하는 서버 설정 됩니다.  
  
## <a name="BKMK_VDCSafeRestore"></a>Virtualization 보호 기능  
가상화 도메인 컨트롤러 복제 달리 virtualization 보호 기능이 Windows Server 2012 없는 구성 단계 했습니다. 몇 가지 간단한 조건을 충족으로 작업 없이 기능이 작동 합니다.  
  
-   하이퍼바이저 VM 세대 ID를 지원합니다.  
  
-   복원 된 도메인 컨트롤러에서 변경 내용을 비 정식 복제할 수 있는 유효한 파트너 도메인 컨트롤러가 있습니다.  
  
### <a name="validate-the-hypervisor"></a>하이퍼바이저의 유효성을 검사합니다  
원본 도메인 컨트롤러에서 실행 되 고 지원된 하이퍼바이저 공급 업체는 설명서를 검토 하 여 확인 합니다. 가상화 도메인 컨트롤러 하이퍼바이저 독립 되며 Hyper-v 필요 하지 않습니다.  
  
이전 검토 [플랫폼 요구](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_PlatformReqs) 섹션 알려진 VM 세대 ID 지원 합니다.  
  
다른 대상 하이퍼바이저 소스 하이퍼바이저에서 Vm 마이그레이션하는, virtualization 되는지 궁금할 수 있습니다 또는 아래에 설명 된 대로 하이퍼바이저 VM 세대 ID를 지원 하는지 여부에 따라 시작 될 수 있습니다.  
  
|원본 하이퍼바이저|대상 하이퍼바이저|결과|  
|---------------------|---------------------|----------|  
|지원 VM 세대 ID|VM 세대 ID를 지원 하지 않는|보호 기능이 트리거되지 (에 DCCloneConfigFile.xml 있으면 DC 부팅 DSRM로)|  
|VM 세대 ID를 지원 하지 않는|지원 VM 세대 ID|발생 하는 보호 기능|  
|지원 VM 세대 ID|지원 VM 세대 ID|트리거되지 VM 정의 변경 되지 VM 세대 ID 동일 하 게 유지 되므로 의미 하는 보호 기능|  
  
### <a name="validate-the-replication-topology"></a>복제 토폴로지의 유효성을 검사합니다  
Virtualization 보호 기능으로 Active Directory 복제 신뢰할 수 없는 모든 SYSVOL 내용 동기화 델타 신뢰할 수 없는 인바인드 복제가 시작합니다. 이렇게 하면 도메인 컨트롤러 모든 기능 스냅샷을에서 반환 및 결국 환경의 나머지 부분와 일치 합니다.  
  
이 새로운 기능으로 요구 사항 및 제한 사항이 몇 가지를 제공 합니다.  
  
-   복원 된 도메인 컨트롤러 쓸 수 DC 연결할 수 있어야 합니다.  
  
-   도메인에 있는 모든 도메인 컨트롤러 동시에 복원 해야  
  
-   복원 된 도메인 컨트롤러에서 발생 복제 하지 않은 아직 아웃 바운드 스냅샷이 된 이후 변경 렉 손실 됩니다.  
  
문제 해결 섹션 이러한 시나리오를 포함 하는 동안 문제가 발생할 수 있는 토폴로지에서 만들 아래의 세부 정보 확인 합니다.  
  
#### <a name="writable-domain-controller-availability"></a>쓰기 도메인 컨트롤러 공급 일  
도메인 컨트롤러 쓸 수 있는 도메인 컨트롤러;에 대 한 연결이 있어야 복원 하는 경우 읽기 전용 도메인 컨트롤러 업데이트 델타를 보낼 수 없습니다. 토폴로지 쓸 수 있는 도메인 컨트롤러 아직이 대 한 올바른 쓸 수 있는 파트너에 언제 든 지 필요한 되었을 수 있습니다. 그러나 모든 쓸 수 있는 도메인 컨트롤러 동시에 복원 하는 유효한 소스를 찾을 수 그 중입니다. 마찬가지 쓸 수 있는 도메인 컨트롤러 유지 관리 오프 라인 또는 그렇지 않은 경우 네트워크를 통해 연결할 수 없는 경우입니다.  
  
#### <a name="simultaneous-restore"></a>동시 복원  
동시에 단일 도메인에 있는 모든 도메인 컨트롤러를 복원 하지 마십시오. 모든 스냅숏을 복원 정상적으로 Active Directory 복제 작동 한 번에 있지만 SYSVOL 복제 중지 합니다. FRS 및 DFSR 복원 아키텍처의 복제본 인스턴스 신뢰할 수 없는 동기화 모드를 설정 해야 합니다. 한 번에 모두 도메인 컨트롤러 복원 하 고 각 도메인 컨트롤러 표시 자체 신뢰할 수 없는 sysvol를 모두 다음을 시도 그룹 정책 및 스크립트 신뢰할 수 있는 파트너;에서 동기화 이 시점에서 하지만 모든 파트너 신뢰할 수 없는 수도 있습니다.  
  
> [!IMPORTANT]  
> 모든 도메인 컨트롤러 한 번에 복원 하는 경우 다음 문서를 정상적으로 작동 하는 도메인 컨트롤러 돌아갈 수 있도록 한 도메인 컨트롤러에서 일반적으로 PDC 에뮬레이터-신뢰할 수 홈페이지로 설정할 사용:  
>   
> [복제본 설정 BurFlags 레지스트리 키를 사용 하 여 파일 복제 서비스 다시 초기화 하려면](https://support.microsoft.com/kb/290762)  
>   
> [DFSR 복제 SYSVOL (예: "d 4/d 2" FRS에 대 한)에 대 한 권한을 보유 하 고 신뢰할 수 없는 동기화 하는 방법](https://support.microsoft.com/kb/2218556)  
  
> [!WARNING]  
> 동일한 하이퍼바이저 호스트에서 도메인에 있는 모든 도메인 컨트롤러를 실행 하지 않습니다. 단일 광고 DS, Exchange, SQL, 및 기타 엔터프라이즈 작업 하이퍼바이저 오프 라인 때마다 cripples 실패 한을 도입 합니다. 이것이 더 다른 하나만 도메인 컨트롤러를 사용 하 여 전체 도메인 또는 숲입니다. 여러 도메인 컨트롤러 여러 플랫폼에서 중복 및 결함 허용을 제공 하는 데 도움이 됩니다.  
  
#### <a name="post-snapshot-replication"></a>이후 스냅숏 복제  
로컬에서 원래 이후의 모든 변경 내용을 스냅숏을 만드는 복제 아웃 바운드까지 스냅숏을 복원 하지 마십시오. 다른 도메인 컨트롤러 이미 받지 못한을 통해 복제 하는 경우 원래 변경 렉 손실 됩니다.  
  
Repadmin.exe을 사용 하 여 도메인 컨트롤러의 파트너와 모든 없다고 복제 아웃 바운드 변화를 볼 수 있습니다.  
  
1.  이름 및와 개체 Guid DSA DC의 파트너 반환 다음과 같습니다.  
  
    ```  
    Repadmin.exe /showrepl <DC Name of the partner> /repsto  
    ```  
  
2.  복원 하는 도메인 컨트롤러에 보류 중인 인바인드 복제가 파트너 도메인 컨트롤러의 반환 다음과 같습니다.  
  
    ```  
    Repadmin.exe /showchanges < Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare>  
    ```  
  
변경 내용 취소 복제의 수를 볼 수만 또는 다음과 같습니다.  
  
```  
Repadmin.exe /showchanges <Name of partner DC><DSA Object GUID of the domain controller being restored><naming context to compare> /statistics  
```  
  
예를 들어 (수정 가독성 및 중요 한 항목에 대 한 출력으로 ***기울임꼴로 표시 된***), DC4의 복제 파트너 살펴보면 다음과:  
  
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
  
이제 d c 2와 d c 3 복제 알 수 있습니다. 다음에 d c 2 내용이 것도 않습니다 하지에서 DC4, 하며 새 그룹 확인 변경 목록을 표시 합니다.  
  
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
  
다른 파트너는 것가 이미 복제 되지 되도록 테스트가 있습니다.  
  
또는 상관 하지 않은 경우 개체 복제 되지 했 고 기준은 개체 대기 중인에 사용할 수 있는 **/statistics** 옵션:  
  
```  
C:\>repadmin /showchanges dc2.corp.contoso.com 5d083398-4bd3-48a4-a80d-fb2ebafb984f dc=corp,dc=contoso,dc=com /statistics  
  
***********************************************  
********* Grand total *************************  
Packets:              1  
Objects:              1Object Additions:     1Object Modifications: 0Object Deletions:     0Object Moves:         0Attributes:           12Values:               13  
```  
  
> [!IMPORTANT]  
> 오류 또는 뛰어난 복제 표시 하는 경우 모든 쓸 수 있는 파트너 테스트 합니다. 수렴는 하나 이상의으로 전이적 복제 다른 서버 결국 조정 처럼 스냅숏을 복원할 일반적으로 안전 합니다.  
>   
> 해결 될 때까지 진행 하지 않는 고 복제 /showchanges에 표시 된에 오류가 있는 있음에 유의 해야 합니다.  
  
### <a name="windows-powershell-snapshot-cmdlets"></a>Windows 스냅숏을 PowerShell Cmdlet  
다음 Windows PowerShell Hyper-v 모듈 cmdlet Windows Server 2012에서 스냅숏을 기능을 제공 합니다.  
  
```  
Checkpoint-VM  
Export-VMSnapshot  
Get-VMSnapshot  
Remove-VMSnapshot  
Rename-VMSnapshot  
Restore-VMSnapshot  
```  
  


