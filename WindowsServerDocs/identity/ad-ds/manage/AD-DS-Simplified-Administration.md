---
ms.assetid: f74eec9a-2485-4ee0-a0d8-cce01250a294
title: AD DS 간소화된 관리
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 4f12b1e88414a17c8fb82a707bd4399505df4c6c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369452"
---
# <a name="ad-ds-simplified-administration"></a>AD DS 간소화된 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server 2012 도메인 컨트롤러 배포 및 관리의 기능과 이점, 이전 운영 체제 DC 배포와 새로운 Windows Server 2012 구현 간의 차이점에 대해 설명 합니다.  
  
Windows Server 2012는 차세대 Active Directory Domain Services 단순화 된 관리를 도입 했으며 Windows 2000 서버부터 가장 많은 부를 다시 구상 했습니다. AD DS 간소화된 관리에서는 12년 동안 Active Directory에서 얻은 교훈을 바탕으로 설계자와 관리자를 위한 보다 지원 가능하고 유연하며 직관적인 관리 환경을 제공합니다. 이는 기존 기술의 새 버전을 만들 수 있을 뿐만 아니라 Windows Server 2008 R2에서 릴리스된 구성 요소의 기능을 확장할 수도 있습니다.  
  
AD DS 간소화된 관리는 도메인 배포의 새로운 디자인입니다.  
  
- AD DS 역할 배포가 이제 새로운 서버 관리자 아키텍처의 일부이며 원격 설치를 허용합니다.  
- AD DS 배포 및 구성 엔진이 이제 Windows PowerShell이며, 이는 새로운 AD DS 구성 마법사를 사용하는 경우에도 마찬가지입니다.  
- 스키마 확장, 포리스트 준비 및 도메인 준비가 도메인 컨트롤러 수준 올리기 프로세스의 일부로 자동으로 수행되므로 더 이상 스키마 마스터와 같은 특정 서버에서 별도의 작업을 수행할 필요가 없습니다.  
- 이제 수준 올리기에 새 도메인 컨트롤러에 대한 포리스트 및 도메인 준비 상태를 확인하는 필수 구성 요소 확인이 포함되어 있어 수준 올리기에 실패할 가능성이 낮아졌습니다.  
- 이제 Windows PowerShell용 Active Directory 모듈에 복제 토폴로지 관리, 동적 액세스 제어 및 기타 작업을 위한 cmdlet이 포함되어 있습니다.  
- Windows Server 2012 포리스트 기능 수준에서 새로운 기능을 구현하지 않으며 도메인 기능 수준이 새로운 Kerberos 기능의 하위 집합에만 필요하므로 관리자에게 동종 도메인 컨트롤러 환경이 자주 필요하지 않습니다.  
- 자동화된 배포 및 롤백 보호를 포함하도록 가상화된 도메인 컨트롤러에 대한 완벽한 지원 기능이 추가되었습니다.  
   - 가상화 된 도메인 컨트롤러에 대 한 자세한 내용은 참조 [Active Directory 도메인 서비스 및 #40; 도입 AD DS & #41; 가상화 & #40입니다. 수준 100 & #41;](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)합니다.

그 밖에 다음과 같은 많은 관리 및 유지 관리 기능이 향상되었습니다.  

- Active Directory 관리 센터에 그래픽 Active Directory 휴지통, 세분화된 암호 정책 관리 및 Windows PowerShell 기록 뷰어가 포함되어 있습니다.
- 새로운 서버 관리자에 성능 모니터링, 모범 사례 분석, 중요한 서비스 및 이벤트 로그에 대한 AD DS 관련 인터페이스가 있습니다.  
- 그룹 관리 서비스 계정에서 동일한 보안 주체를 사용하여 여러 컴퓨터를 지원합니다.  
- 성숙한 Active Directory 도메인에서 관리 효율성을 향상시킬 수 있도록 RID(상대 식별자) 발급 및 모니터링 기능이 향상되었습니다.  

다음과 같이 Windows Server 2012에 포함 된 다른 새로운 기능을 AD DS 수익  

- NIC 팀 및 데이터 센터 브리징  
- DNS 보안 및 부팅 후 보다 빠른 AD 통합 영역 가용성  
- 향상된 Hyper-V 안정성 및 확장성 기능  
- BitLocker 네트워크 잠금 해제  
- 추가 Windows PowerShell 구성 요소 관리 모듈  

## <a name="adprep-integration"></a>ADPREP 통합

Active Directory 포리스트 스키마 확장 및 도메인 준비가 이제 도메인 컨트롤러 구성 프로세스에 통합되었습니다. 새 도메인 컨트롤러를 기존 포리스트로 수준을 올릴 경우 프로세스에서 업그레이드 상태 및 스키마 확장을 감지하며 도메인 준비 단계가 자동으로 실행됩니다. 첫 번째 Windows Server 2012 도메인 컨트롤러를 설치하는 사용자는 여전히 Enterprise Admin 및 Schema Admin이거나 유효한 대체 자격 증명을 제공해야 합니다.  
  
Adprep.exe는 개별 포리스트 및 도메인 준비를 위해 DVD로 계속 제공됩니다. Windows Server 2012에 포함된 도구의 버전은 이전 Windows Server 2008 x64 및 Windows Server 2008 R2와 호환됩니다. Adprep.exe는 ADDSDeployment 기반 도메인 컨트롤러 구성 도구와 마찬가지로 원격 forestprep 및 domainprep도 지원합니다.  
  
Adprep 및 이전 운영 체제 포리스트 준비에 대 한 정보를 참조 하십시오. [Adprep 실행 (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd464018(WS.10).aspx)합니다.  

## <a name="server-manager-ad-ds-integration"></a>서버 관리자 AD DS 통합

![간편한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_Dashboard.png)  
  
서버 관리자는 서버 관리 작업의 허브 역할을 합니다. 대시보드 스타일로 디자인되어 있는 설치된 역할 및 원격 서버 그룹의 보기가 주기적으로 새로 고쳐집니다. 서버 관리자는 콘솔에 액세스하지 않고도 로컬 및 원격 서버를 중앙 집중식으로 관리할 수 있는 기능을 제공합니다.  
  
Active Directory 도메인 서비스는 이러한 허브 역할 중 하나 도메인 컨트롤러 또는 Windows 8에서 원격 서버 관리 도구에서 서버 관리자를 실행 하 여 포리스트의 도메인 컨트롤러에서 최근의 중요 한 문제를 참조 합니다.  
  
이러한 보기에는 다음이 포함됩니다.  
  
- 서버 가용성  
- 높은 CPU 및 메모리 사용량에 대한 성능 모니터 경고  
- AD DS에 특정한 Windows 서비스의 상태  
- 디렉터리 서비스와 관련된 이벤트 로그의 최근 경고 및 오류 항목  
- Microsoft 권장 규칙 집합에 대한 도메인 컨트롤러의 모범 사례 분석  

## <a name="active-directory-administrative-center-recycle-bin"></a>Active Directory 관리 센터 휴지통

![간편한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_ADAC.png)  
  
Windows Server 2008 R2에서는 백업에서 복원하거나, AD DS 서비스를 다시 시작하거나, 도메인 컨트롤러를 다시 부팅하지 않고도 삭제된 Active Directory 개체를 복구하는 Active Directory 휴지통이 도입되었습니다.  
  
Windows Server 2012는 Active Directory 관리 센터의 새로운 그래픽 인터페이스로 기존 Windows PowerShell 기반 복원 기능을 개선합니다. 이를 통해 관리자는 휴지통을 사용하도록 설정하여 Windows PowerShell cmdlet을 직접 실행하지 않고도 포리스트의 도메인 컨텍스트에서 삭제된 개체를 찾거나 복원할 수 있습니다. Active Directory 관리 센터와 Active Directory 휴지통에서는 Windows PowerShell을 내부적으로 계속 사용하므로 이전 스크립트와 절차가 여전히 중요합니다.  
  
Active Directory에 대 한 내용은 [휴지통 Active Directory 휴지통 단계별 가이드 (Windows Server 2008 R2)을 참조 하십시오](https://technet.microsoft.com/library/dd392261(WS.10).aspx)합니다.  
  
## <a name="active-directory-administrative-center-fine-grained-password-policy"></a>Active Directory 관리 센터 세분화된 암호 정책

![간편한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_FGPP.png)  
  
Windows Server 2008에서는 관리자가 도메인당 여러 암호 및 계정 잠금 정책을 구성할 수 있는 세분화된 암호 정책이 도입되었습니다. 이를 통해 도메인에서 사용자 및 그룹에 따라 제한 수준이 다른 암호 규칙을 유연하게 적용할 수 있습니다. 하지만 관리 인터페이스가 없어 관리자가 Ldp.exe 또는 Adsiedit.msc를 사용하여 구성해야 했습니다. Windows Server 2008 R2에서는 관리자에게 FGPP에 대한 명령줄 인터페이스를 제공하는 Windows PowerShell용 Active Directory 모듈이 도입되었습니다.  
  
이제 Windows Server 2012에서는 세분화된 암호 정책에 대한 그래픽 인터페이스를 제공합니다. Active Directory 관리 센터는 모든 관리자에게 간소화된 FGPP 관리 기능을 제공하는 이 새로운 대화 상자의 홈입니다.  
  
세분화된 암호 정책에 대한 자세한 내용은 [AD DS 세분화된 암호 및 계정 잠금 정책 단계별 가이드(Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx)를 참조하세요.  
  
## <a name="active-directory-administrative-center-windows-powershell-history-viewer"></a>Active Directory 관리 센터 Windows PowerShell 기록 뷰어

![간편한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_HistoryViewer.png)  
  
Windows Server 2008 R2에서는 Windows 2000에서 만들어진 이전 Active Directory 사용자 및 컴퓨터 스냅인을 대체하는 Active Directory 관리 센터가 도입되었습니다. 이 Active Directory 관리 센터에서는 당시에 새로운 Windows PowerShell용 Active Directory 모듈의 그래픽 관리 인터페이스를 만듭니다.  
  
Active Directory 모듈에는 100개가 넘는 cmdlet이 포함되어 있지만 관리자가 빠르게 습득할 수 있습니다. Windows PowerShell은 Windows 관리 전략에 긴밀하게 통합되므로 이제 Active Directory 관리 센터에 그래픽 인터페이스에서 cmdlet 실행을 확인할 수 있는 뷰어가 포함되어 있습니다. 단순한 인터페이스에서 검색, 복사, 기록 지우기, 메모 추가 등의 작업을 수행할 수 있습니다. 이는 관리자가 그래픽 인터페이스를 사용하여 개체를 만들고 수정한 다음 기록 뷰어에서 검토하여 Windows PowerShell 스크립팅에 대한 자세한 정보를 얻고 예제를 수정할 수 있도록 하기 위한 것입니다.  

## <a name="ad-replication-windows-powershell"></a>AD 복제 Windows PowerShell

![간편한 관리](media/AD-DS-Simplified-Administration/ADDS_PSNewADReplSite.png)  
  
Windows Server 2012는 추가 Active Directory 복제 cmdlet을 Active Directory Windows PowerShell 모듈에 추가합니다. 이를 통해 기존 또는 새 사이트, 서브넷, 연결, 사이트 링크 및 브리지를 구성할 수 있습니다. 또한 이러한 cmdlet은 Active Directory 복제 메타데이터, 복제 상태, 큐 및 최신 버전 벡터 정보를 반환합니다. 배포 및 기타 기존 AD DS cmdlet 외에 복제 cmdlet이 도입됨으로써 Windows PowerShell만으로 포리스트를 관리할 수 있게 되었습니다. 이는 그래픽 인터페이스 없이 Windows Server 2012를 프로비전 및 관리하려는 관리자에게 새로운 기회를 열어 주며, 운영 체제의 공격 노출 및 서비스 요구 사항을 감소시킵니다. 이는 SIPR(Secret Internet Protocol Router) 및 기업 DMZ와 같은 보안이 매우 엄격한 네트워크에 서버를 배포할 때 특히 중요합니다.  
  
AD DS 사이트 토폴로지 및 복제 하는 방법에 대 한 자세한 내용은 참조는 [Windows Server 기술 참조](https://technet.microsoft.com/library/cc739127(WS.10).aspx)합니다.  

## <a name="rid-management-and-issuance-improvements"></a>RID 관리 및 발급 개선 사항

Windows 2000 Active Directory에서는 사용자, 그룹 및 컴퓨터와 같은 보안 트러스티의 SID(보안 식별자)를 만들기 위해 상대 식별자 풀을 도메인 컨트롤러에 발급하는 RID 마스터가 도입되었습니다.  기본적으로 이 전역 RID 공간은 도메인에서 만들 수 있는 총 SID가 2<sup>30</sup> (또는 1073741823)개로 제한됩니다. SID는 풀로 반환하거나 다시 발급할 수 없습니다. 따라서 시간이 지남에 대규모 도메인에서 RID가 부족해지기 시작하고, 실수로 인해 RID가 불필요하게 고갈됨으로써 결과적으로 소진될 수 있습니다.  
  
Windows Server 2012는 1999년에 최초의 Active Directory 도메인을 만든 이후 AD DS가 성숙됨에 따라 고객 및 Microsoft 고객 지원에서 다루지 못하는 여러 가지 RID 발급 및 관리 문제를 해결합니다. 이러한 개체는 다음과 같습니다.  

- 정기적인 RID 사용 경고가 이벤트 로그에 기록됩니다.  
- 관리자가 RID 풀을 무효화한 경우 이벤트가 로깅됩니다.  
- 이제 RID 정책 RID 블록 크기에 대한 최대 한도가 적용됩니다.  
- 이제 인공 RID 최대값이 적용되며 전역 RID 공간이 적은 경우 로깅되므로 관리자가 전역 공간이 소진되기 전에 조치를 취할 수 있습니다.
- 이제 전역 RID 공간을 1비트 증가시켜 크기를 두 배(2<sup>31</sup>, 즉 2,147,483,648개의 SID)로 늘릴 수 있습니다.  

RID 및 RID 마스터에 대한 자세한 내용은 [보안 식별자 작동 방식](https://technet.microsoft.com/library/cc778824(WS.10).aspx)을 참조하세요.  
  
## <a name="ad-ds-role-deployment-and-management-architecture"></a>AD DS 역할 배포 및 관리 아키텍처

서버 관리자 및 ADDSDeployment Windows PowerShell은 다음 핵심 어셈블리를 기반으로 AD DS 역할 배포 또는 관리 기능을 제공합니다.  

- Microsoft.ADroles.Aspects.dll  
- Microsoft.ADroles.Instrumentation.dll  
- Microsoft.ADRoles.ServerManager.Common.dll  
- Microsoft.ADRoles.UI.Common.dll  
- Microsoft.DirectoryServices.Deployment.Types.dll  
- Microsoft.DirectoryServices.ServerManager.dll  
- Addsdeployment.psm1  
- Addsdeployment.psd1  

원격 역할 설치 및 구성의 경우 둘 다 Windows PowerShell 및 해당 원격 invoke-command를 기반으로 합니다.  

![간편한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_DepDLLs.png)  

또한 Windows Server 2012는 여러 이전 수준 올리기 작업을 다음의 일부로 LSASS.EXE에서 리팩터링합니다.  

- DS 역할 서버 서비스(DsRoleSvc)  
- DSRoleSvc.dll(DsRoleSvc 서비스에 의해 로드됨)  

가상 도메인 컨트롤러의 수준 올리기, 수준 내리기 또는 복제에는 이 서비스가 존재하고 실행되어야 합니다. AD DS 역할 설치에서는 이 서비스를 추가하고 시작 유형을 기본적으로 수동으로 설정합니다. 이 서비스를 사용하지 않도록 설정하지 마세요.  

## <a name="adprep-and-prerequisite-checking-architecture"></a>ADPrep 및 필수 구성 요소 확인 아키텍처

더 이상 스키마 마스터에서 Adprep를 실행할 필요가 없습니다. Windows Server 2008 x64 이상을 실행하는 컴퓨터에서 원격으로 실행할 수 있습니다.  
  
> [!NOTE]  
> Adprep는 LDAP를 사용하여 Schxx.ldf 파일을 가져오며, 가져오기 중에 스키마 마스터의 연결이 끊어진 경우 자동으로 다시 연결되지 않습니다. 가져오기 프로세스 중에 스키마 마스터는 특정 모드로 설정되고 자동 다시 연결은 사용하지 않도록 설정됩니다. 이는 연결이 끊어진 후 LDAP가 다시 연결되면 다시 설정된 연결이 특정 모드에 있지 않을 수 있기 때문입니다. 이 경우 스키마를 제대로 업데이트할 수 없습니다.  
  
필수 구성 요소 확인에서는 특정 조건을 충족하는지 확인합니다. 이러한 조건은 성공적인 AD DS 설치에 필요합니다. 일부 필수 조건이 충족되지 않은 경우 설치를 계속하기 전에 해결할 수 있습니다. 또한 필수 구성 요소 확인에서는 Adprep 배포 코드가 자동으로 실행되도록 포리스트 또는 도메인이 아직 준비되지 않았는지 검색합니다.  

### <a name="adprep-executables-dlls-ldfs-files"></a>ADPrep 실행 파일, DLL, LDF, 파일

- ADprep.dll  
- Ldifde.dll  
- Csvde.dll  
- Sch14.ldf - Sch56.ldf  
- Schupgrade.cat  
- *dcpromo.csv  

이전에 ADprep.exe에 있던 AD 준비 코드가 adprep.dll로 리팩터링되었습니다. 따라서 ADPrep.exe와 ADDSDeployment Windows PowerShell 모듈 모두 동일한 작업에 라이브러리를 사용하고 동일한 기능을 유지할 수 있습니다. Adprep.exe는 설치 미디어에 포함되어 있지만 자동화된 프로세스에서 호출되지 않습니다. 관리자가 수동으로만 실행합니다. 또한 Windows Server 2008 x64 이상 운영 체제에서만 실행될 수 있습니다. Ldifde.exe 및 csvde.exe도 준비 프로세스에서 로드되는 DLL로 버전이 리팩터링되었습니다. 스키마 확장에서는 이전 운영 체제 버전과 마찬가지로 여전히 서명 확인된 LDF 파일을 사용합니다.  
  
![간편한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_AdprepDLLs.png)  
  
> [!IMPORTANT]  
> Windows Server 2012용 32비트 Adprep32.exe 도구는 없습니다. 포리스트와 도메인을 준비하려면 도메인 컨트롤러 또는 구성원 서버로 실행되거나 작업 그룹에서 실행되는 Windows Server 2008 x64, Windows Server 2008 R2 또는 Windows Server 2012 컴퓨터가 하나 이상 있어야 합니다. Adprep.exe는 Windows Server 2003 x64에서 실행되지 않습니다.  
  
## <a name="BKMK_PrereuisiteChecking"></a>필수 구성 요소 확인

ADDSDeployment Windows PowerShell 관리 코드에 기본 제공되는 필수 구성 요소 확인은 작업에 따라 여러 모드로 작동합니다. 아래 표에서는 각 테스트와 이러한 테스트가 사용되는 경우, 각 테스트에서 유효성을 검사하는 방법 및 대상에 대해 설명합니다. 이 표는 유효성 검사에 실패하고 오류 정보가 문제를 해결하는 데 부족한 경우에 유용할 수 있습니다.  
  
이러한 테스트는 **DirectoryServices-Deployment** 작업 이벤트 로그의 **Core**작업 범주 아래에 항상 이벤트 ID **103**으로 로깅됩니다.  
  
### <a name="prerequisite-windows-powershell"></a>필수 Windows PowerShell

모든 도메인 컨트롤러 배포 cmdlet에 필요한 ADDSDeployment Windows PowerShell cmdlet이 있습니다. 이러한 cmdlet의 인수는 관련 cmdlet과 거의 동일합니다.  

- Test-ADDSDomainControllerInstallation  
- Test-ADDSDomainControllerUninstallation  
- Test-ADDSDomainInstallation  
- Test-ADDSForestInstallation  
- Test-ADDSReadOnlyDomainControllerAccountCreation  

이러한 cmdlet은 대개 별도로 실행할 필요가 없습니다. 기본적으로 배포 cmdlet과 함께 자동으로 실행됩니다.  

#### <a name="BKMK_ADDSInstallPrerequisiteTests"></a>필수 구성 요소 테스트

||||  
|-|-|-|  
|테스트 이름|프로토콜<br /><br />프로토콜|설명 및 참고 사항|  
|VerifyAdminTrusted<br /><br />ForDelegationProvider|LDAP|기존 파트너 도메인 컨트롤러에 대한 "위임 시 컴퓨터 및 사용자 계정을 신뢰할 수 있도록 설정"(SeEnableDelegationPrivilege) 권한이 있는지 확인합니다. 그러려면 생성된 tokenGroups 특성에 액세스할 수 있어야 합니다.<br /><br />Windows Server 2003 도메인 컨트롤러에 연결할 때는 사용되지 않습니다. 수준을 올리기 전에 이 권한을 수동으로 확인해야 합니다.|  
|VerifyADPrep<br /><br />Prerequisites(포리스트)|LDAP|rootDSE namingContexts 특성 및 스키마 명명 컨텍스트 fsmoRoleOwner 특성을 사용하여 스키마 마스터를 검색하고 연결합니다. AD DS 설치에 필요한 준비 작업(forestprep, domainprep 또는 rodcprep)을 확인합니다. 스키마 objectVersion과 해당 추가 확장이 필요한지 확인합니다.|  
|VerifyADPrep<br /><br />Prerequisites(도메인 및 RODC)|LDAP|rootDSE namingContexts 특성 및 인프라 컨테이너 fsmoRoleOwner 특성을 사용하여 인프라 마스터를 검색하고 연결합니다. RODC 설치의 경우 이 테스트는 도메인 명명 마스터를 검색하고 온라인 상태인지 확인합니다.|  
|CheckGroup<br /><br />멤버 자격|LDAP,<br /><br />RPC over SMB(LSARPC)|작업에 따라 사용자가 Domain Admins 또는 Enterprise Admins 그룹의 구성원인지 확인합니다(도메인 컨트롤러 추가 또는 수준 내리기의 경우 DA, 도메인 추가 또는 제거의 경우 EA).|  
|CheckForestPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC over SMB(LSARPC)|사용자가 Schema Admins 및 Enterprise Admins 그룹의 구성원이고 기존 도메인 컨트롤러에 대한 감사 및 보안 이벤트 로그 관리(SesScurityPrivilege) 권한이 있는지 확인합니다.|  
|CheckDomainPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC over SMB(LSARPC)|사용자가 Domain Admins 그룹의 구성원이고 기존 도메인 컨트롤러에 대한 감사 및 보안 이벤트 로그 관리(SesScurityPrivilege) 권한이 있는지 확인합니다.|  
|CheckRODCPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC over SMB(LSARPC)|사용자가 Enterprise Admins 그룹의 구성원이고 기존 도메인 컨트롤러에 대한 감사 및 보안 이벤트 로그 관리(SesScurityPrivilege) 권한이 있는지 확인합니다.|  
|VerifyInitSync<br /><br />AfterReboot|LDAP|rootDSE 특성 becomeSchemaMaster에서 더미 값을 설정하여 스키마 마스터가 다시 시작된 이후 한 번 이상 복제되었는지 확인합니다.|  
|VerifySFUHotFix<br /><br />Applied|LDAP|기존 포리스트 스키마에 OID가 1.2.840.113556.1.4.7000.187.102인 UID 특성에 대한 SFU2 확장 관련 알려진 문제가 없는지<br /><br />([https://support.microsoft.com/kb/821732](https://support.microsoft.com/kb/821732))|  
|VerifyExchange<br /><br />SchemaFixed|LDAP, WMI, DCOM, RPC|기존 포리스트 스키마의 유효성을 검사 하는 데 문제가 Exchange 2000 확장명 ms-Exch-Name, ms Exch-LabeledURI 및 ms-Exch-Id ([https://support.microsoft.com/kb/314649](https://support.microsoft.com/kb/314649))에 아직 포함 되지 않았습니다.|  
|VerifyWin2KSchema<br /><br />일관성|LDAP|기존 포리스트 스키마에 일관된(타사에서 잘못 수정하지 않은) 핵심 특성 및 클래스가 있는지 확인합니다.|  
|DCPromo|DRSR over RPC,<br /><br />LDAP,<br /><br />DNS<br /><br />RPC over SMB(SAMR)|수준 올리기 코드로 전달된 명령줄 구문의 유효성을 검사하고 수준 올리기를 테스트합니다. 포리스트 또는 도메인을 새로 만드는 경우 이미 존재하지 않는지 확인합니다.|  
|VerifyOutbound<br /><br />ReplicationEnabled|LDAP, DRSR over SMB, RPC over SMB(LSARPC)|NTDS 설정 개체의 옵션 특성에서 NTDSDSA_OPT_DISABLE_OUTBOUND_REPL(0x00000004)을 확인하여 복제 파트너로 지정된 기존 도메인 컨트롤러에 아웃바운드 복제가 사용하도록 설정되어 있는지 확인합니다.|  
|VerifyMachineAdmin<br /><br />암호|DRSR over RPC,<br /><br />LDAP,<br /><br />DNS<br /><br />RPC over SMB(SAMR)|DSRM에 대해 설정된 안전 모드 암호가 도메인 복잡성 요구 사항을 충족하는지 확인합니다.|  
|VerifySafeModePassword|*해당 없음*|설정된 로컬 관리자 암호가 컴퓨터 보안 정책 복잡성 요구 사항을 충족하는지 확인합니다.|  
