---
ms.assetid: f74eec9a-2485-4ee0-a0d8-cce01250a294
title: "AD DS 단순한 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6232e281c47f3b5b4627bc9d8ccf53269aafc390
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-simplified-administration"></a>AD DS 단순한 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 새 기능 및 Windows Server 2012 도메인 컨트롤러 배포 및 관리 및 이전 운영 체제 DC 배포와 새로운 Windows Server 2012 구현 간의 차이점의 혜택에 설명 합니다.  
  
Windows Server 2012 차세대 Active Directory 도메인 서비스 간체 관리를 소개 하 고에서 가장 부 도메인 다시 계획 Windows 2000 Server 이후입니다. 광고 DS 간체 관리 Active Directory 12 년간에서 배운 교훈을 수행 하 고 설계자와 관리자는 더 지원 더 유연한, 더욱 직관적인 관리 환경을 만듭니다. 이것은 새 버전으로 확장 구성 요소 Windows Server 2008 r 2에 출시 된 기능 뿐만 아니라 기술을 기존 의미 합니다.  
  
광고 DS 간체 관리 도메인 배포는 reimagining입니다.  
  
-   AD DS 역할 배포 새 관리자 서버가 아키텍처 포함 되어 있으며 원격 설치  
  
-   새 AD DS 구성 마법사를 사용 하는 경우에 AD DS 배포 및 구성 엔진은 이제 Windows PowerShell  
  
-   스키마 확장, 숲 준비 도메인 준비 자동으로 도메인 컨트롤러 프로 모션에 포함 된 및 특수 서버 스키마 마스터 등에 별도 작업을 더 이상 필요  
  
-   프로 모션 이제 실패 프로 모션 기회가 내려 새 도메인 컨트롤러에 대 한 준비를 숲 및 도메인의 유효성을 검사 필수 검사 포함 됩니다.  
  
-   이제 포함 되어 cmdlet 복제 토폴로지 관리, 동적 액세스 제어 하 고 다른 작업에 대 한 active Directory Windows PowerShell 모듈  
  
-   Windows Server 2012 숲 수준 새로운 기능을 구현 하지 않는 및 도메인 기능 수준을 선도 관리자는 자주 방문 하는 새로운 Kerberos 기능 중 일부에만 필요 기능 동일한 도메인 컨트롤러 환경에 대 한 필요  
  
-   전체 지원이 도메인 컨트롤러 가상화 자동화 된 배포 및 롤백 보호 기능을 포함 하도록에 대 한 추가  
  
가상화 도메인 컨트롤러에 대 한 자세한 내용은 참조 [Active Directory Domain Services & #40; 소개 AD DS & #41; Virtualization & #40; 수준을 100 & #41;](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).  
  
또한 다음과 같은 여러 가지 관리 및 유지 관리 개선 사항:  
  
-   그래픽 Active Directory 휴지통, 세분화 암호 정책 관리 및 Windows PowerShell 기록 뷰어 Active Directory 관리 센터 포함  
  
-   새로운 서버 관리자가 광고 DS 관련 인터페이스 성능 모니터링, 가장 좋은 방법은 분석, 중요 한 서비스 및 이벤트 로그에  
  
-   그룹 관리 서비스 계정 동일한 보안 사용자를 사용 하 여 여러 대의 컴퓨터를 지원 합니다.  
  
-   관련 식별자 (RID) 발급 및 모니터링 하 고 효율적으로 관리 연령 Active Directory 도메인에서의 개선 사항  
  
마지막으로, AD DS 이익와 같은 Windows Server 2012에 포함 된 새로운 기능 다른에서:  
  
-   NIC 팀 및 Datacenter Bridging  
  
-   DNS 보안 및 부팅 후 빠르게 광고 통합 영역 공급 일  
  
-   Hyper-v 확장성 및 신뢰성 개선  
  
-   BitLocker 네트워크 잠금 해제  
  
-   추가 Windows PowerShell 구성 요소 관리 모듈  
  
## <a name="technical-overview"></a>기술 개요  
  
### <a name="adprep-integration"></a>ADPREP 통합  
Active Directory 숲 스키마 확장 및 도메인 준비 이제 도메인 컨트롤러 구성 프로세스에 통합 됩니다. 기존 숲에 새 도메인 컨트롤러를 홍보 하는 프로세스 업그레이드 상태를 감지 하 고 스키마 확장 및 도메인 준비 단계는 자동으로 수행 합니다. 첫 번째 Windows Server 2012 도메인 컨트롤러를 설치 하는 사용자도 Enterprise 관리자를 스키마 관리자 하거나 올바른 암호 확인용 자격 증명을 제공 해야 합니다.  
  
Adprep.exe 별도 숲 및 도메인 준비 DVD에 남아 있습니다. Windows Server 2012에 포함 된 도구 버전은 Windows Server 2008 R2 및 Windows Server 2008 x64에 이전 버전과 호환입니다. Adprep.exe 원격 forestprep 및 도메인 준비 ADDSDeployment 기반 도메인 컨트롤러의 구성 도구와 마찬가지로 지원합니다.  
  
Adprep 하 고 이전 운영 체제 숲 준비에 대 한 정보를 참조 하세요. [실행 Adprep (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd464018(WS.10).aspx)합니다.  
  
### <a name="server-manager-ad-ds-integration"></a>서버 관리자 AD DS 통합  
![단순한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_Dashboard.png)  
  
서버 관리자 역할 허브에 대 한 서버 관리 작업을 합니다. 대시보드 스타일 등장 정기적으로 설치 역할 및 원격 서버 그룹의 보기를 새로 고칩니다. 서버 관리자 중앙 집중식된 콘솔에 액세스 하지 않고도 지역 및 원격 서버 관리 기능을 제공 합니다.  
  
Active Directory Domain Services는이 허브 역할; 중 하나 서버 관리자 도메인 컨트롤러 또는 Windows 8에서 원격 서버 관리 도구를 실행 하 여 사용자 숲 속의 도메인 컨트롤러에서 중요 한 최근 문제 표시 됩니다.  
  
이 보기 다음과 같습니다.  
  
-   서버 공급 일  
  
-   높은 CPU 및 메모리 사용량에 대 한 성능 모니터 알림  
  
-   Windows 서비스 AD DS 특정 상태  
  
-   최근 디렉터리 서비스 관련 오류 및 경고 로그에서 항목 이벤트  
  
-   가장 좋은 방법은 분석 일련의 Microsoft 권장 규칙 도메인 컨트롤러의  
  
### <a name="active-directory-administrative-center-recycle-bin"></a>관리 센터 active Directory 휴지통  
![단순한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_ADAC.png)  
  
Windows Server 2008 r 2는 Active Directory 휴지통을 백업 으로부터 복원, AD DS 서비스를 다시 시작 또는 도메인 컨트롤러 재부팅 하지 않고 삭제 된 Active Directory 개체를 복구 하는 도입 되었습니다.  
  
Windows Server 2012 Active Directory 관리 센터에서 새로운 그래픽 인터페이스 된 기존 Windows PowerShell 기반 복원 기능을 향상 합니다. 관리자를 휴지통을 사용 하도록 설정 하 고 찾거나 Windows PowerShell cmdlet 직접 실행 하지 않고 모든 숲 속의 경우 도메인에에서 삭제 개체 복원할 수 있습니다. Active Directory 관리 센터 한 Active Directory 휴지통도 사용 하 여 Windows PowerShell 내부적으로 이전 스크립트 및 절차는 여전히 중요 하므로.  
  
Active Directory에 대 한 내용은 [휴지통, Active Directory 휴지통 표시 Step-by-Step 가이드 (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd392261(WS.10).aspx)합니다.  
  
### <a name="active-directory-administrative-center-fine-grained-password-policy"></a>관리 센터 세밀 암호 정책 active Directory  
![단순한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_FGPP.png)  
  
Windows Server 2008 도입 세분화 암호 정책을 관리자 여러 암호 및 계정 잠금 정책을 각 도메인 구성할 수 있습니다. 이렇게 하면 도메인 유연한 솔루션 사용자 및 그룹에 따라 더 많거나 제한적인 암호 규칙을 적용할 수 있습니다. 관리 인터페이스 및 필요 관리자 Ldp.exe 또는 Adsiedit.msc 사용 하 여 구성할 수 없음 했습니다. Windows Server 2008 R2 Windows PowerShell을 관리자 명령줄 인터페이스 FGPP 부여에 대 한 Active Directory 모듈을 도입 되었습니다.  
  
Windows Server 2012 그래픽 인터페이스 세분화 암호 정책을를 제공 합니다. Active Directory 관리 센터 FGPP 관리를 간소화 된 모든 관리자에 게 제공 하는이 새로운 대화 홈입니다.  
  
세분화 암호 정책에 대 한 내용은 [광고 DS 세분화 암호와 잠금 정책 단계별 가이드 계정 (Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx)합니다.  
  
### <a name="active-directory-administrative-center-windows-powershell-history-viewer"></a>관리 센터 Windows PowerShell 기록 뷰어 active Directory  
![단순한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_HistoryViewer.png)  
  
Windows Server 2008 R2 오래 된 Active Directory 사용자 및 컴퓨터 스냅인 Windows 2000에서 만든 대체 된 Active Directory 관리 센터를 도입 했습니다. Active Directory 관리 센터 그래픽 관리 인터페이스 새로운 Active Directory 모듈을 Windows PowerShell 만듭니다.  
  
위로 백 cmdlet Active Directory 모듈 포함 되어, 관리자가 학습 곡선 가파른 수 있습니다. 이후 Windows 관리 전략을 Windows PowerShell 과도 하 게 통합, Active Directory 관리 센터의 그래픽 인터페이스 cmdlet 실행 볼 수 있도록 뷰어를 포함 됩니다. 검색 복사 및 검색 기록 지우기 간단한 인터페이스 사용 하 여 메모를 추가할 수 있습니다. 의도 그래픽 인터페이스 사용을 만들고 개체를 수정 하 고 기록 뷰어를 Windows PowerShell 스크립트에 대 한 자세한 예제 수정 검토 하려면 관리자입니다.  
  
### <a name="ad-replication-windows-powershell"></a>광고 복제 Windows PowerShell  
![단순한 관리](media/AD-DS-Simplified-Administration/ADDS_PSNewADReplSite.png)  
  
Windows Server 2012 추가 Active Directory 복제 cmdlet Active Directory Windows PowerShell 모듈에 추가합니다. 이러한 새로운 기능이 나 기존 사이트, 서브넷, 연결, 사이트 링크, 및 다리 구성할을 수 있습니다. 자녀가 반환 Active Directory 복제 메타 데이터, 복제 상태, 대기열에서 및 최신 버전 vector 정보 합니다. 배포 및 기타 기존 AD DS cmdlet-함께 복제 cmdlet-도입을 Windows PowerShell만 사용 하 여 숲 관리할 수 있습니다. 관리자가 제공 하 고 Windows Server 2012 다음 운영 체제의 공격을 줄입니다 그래픽 인터페이스를 않고도 관리 하고자 하 고 요구 서비스에 대 한 새로운 기회를 만듭니다. 이 서버 시크릿 인터넷 프로토콜 라우터 (SIPR) 및 회사 Dmz 같은 고급 보안 네트워크에 배포 하는 경우 특히 중요 합니다.  
  
AD DS 사이트 토폴로지와 복제에 대 한 자세한 내용은 참조는 [Windows Server Technical 참조](https://technet.microsoft.com/library/cc739127(WS.10).aspx)합니다.  
  
### <a name="rid-management-and-issuance-improvements"></a>제거 관리 및 발급 개선 사항  
Windows 2000 Active Directory 어떤 문제 풀의 보안 Sid (식별자) 보안 트러스티의 만들기 위해 도메인 컨트롤러 관련 식별자 같은 사용자에 게, 그룹과 컴퓨터 제거 마스터 도입 되었습니다.  기본적으로이 전 세계 RID 공간은 제한 2<sup>30</sup> (또는 1073741823) 총 Sid 도메인에서 만든 합니다. Sid 풀 돌아가서 하거나 다시 실행 수 없습니다. 시간이 지남에 따라 큰 도메인 Rid, 부족 하기 시작할 수 있습니다 또는 사고 불필요 한 RID 소모 하 고 최종 소모 될 수 있습니다.  
  
Windows Server 2012 주소 1999 년에 처음 Active Directory 도메인 생성 이후 성숙 과정 다양 한 RID 발급 및 관리 문제 고객 및 Microsoft 고객 지원 AD DS으로 처리 합니다. 이러한 다음과 같습니다.  
  
-   주기적 RID 소비 경고는 이벤트 로그에 기록  
  
-   이벤트는 관리자 무효화 RID 풀 때 로그인  
  
-   지우려는 블록 크기가 적용 이제는 RID 정책에 최대 뚜껑  
  
-   인공 RID 방 이제 시행 하 고 전 세계 RID 공간이 부족 관리자 글로벌 공간 모두 사용 하려면 먼저 조치를 취할 수 있게 될 때 기록  
  
-   글로벌 RID 공간 크기 2 배로 1 비트 증가 이제 수<sup>31</sup> (2147483648 Sid)  
  
Rid와 제거 마스터에 대 한 자세한 정보를 검토 [보안 식별자 작업 어떻게](https://technet.microsoft.com/library/cc778824(WS.10).aspx)합니다.  
  
## <a name="new-ad-ds-deployment-architecture"></a>새 AD DS 구축 구조  
  
### <a name="ad-ds-role-deployment-and-management-architecture"></a>AD DS 역할 배포 및 아키텍처 관리  
서버 관리자 및 ADDSDeployment Windows PowerShell 배포 또는 AD DS 역할을 관리 하는 경우 기능에 대 한 다음 핵심 어셈블리에 의존 합니다.  
  
-   Microsoft.ADroles.Aspects.dll  
  
-   Microsoft.ADroles.Instrumentation.dll  
  
-   Microsoft.ADRoles.ServerManager.Common.dll  
  
-   Microsoft.ADRoles.UI 합니다. Common.dll  
  
-   Microsoft.DirectoryServices.Deployment.Types.dll  
  
-   Microsoft.DirectoryServices.ServerManager.dll  
  
-   Addsdeployment.psm1  
  
-   Addsdeployment.psd1  
  
Windows PowerShell 및 해당 원격 호출-명령 원격 역할을 설치 및 구성 둘 다 사용합니다.  
  
![단순한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_DepDLLs.png)  
  
Windows Server 2012 다양 한 LSASS.EXE의 일환으로:  
  
-   DS 역할 서버 서비스 (DsRoleSvc)  
  
-   DSRoleSvc.dll (DsRoleSvc 서비스에 의해 로드)  
  
이 서비스를 제공 하기 위해 홍보 내리기, 또는 복제 가상 도메인 컨트롤러 실행 되 고 있어야 합니다. AD DS 역할 설치가이 서비스를 추가 하 고 설명서를 시작 형식을 기본적으로 설정 합니다. 이 서비스를 비활성화 하지 않습니다.  
  
### <a name="adprep-and-prerequisite-checking-architecture"></a>ADPrep 및 아키텍처 검사의 필수 조건  
더 이상 도메인 컨트롤러 스키마 마스터 실행에서는 합니다. Windows Server 2008 x64 실행 하는 컴퓨터에서 원격으로 실행 이상 수 있습니다.  
  
> [!NOTE]  
> Adprep은 LDAP Schxx.ldf 파일을 가져올 때 사용 하 고 가져오는 동안 스키마 마스터 연결이 끊어지면에 자동으로 다시 연결 되지 않습니다. 가져오기 과정의 일환으로, 스키마 마스터 특정 모드로 설정 되어 하 고 있기 때문에 LDAP 연결이 끊어지면 후에 다시 연결 되 면 경우 재 연결 하지 특정 모드에서는 자동 다시 연결 사용할 수 없습니다. 이 경우 스키마 올바르게 업데이트 되지 것입니다.  
  
필수 확인 하면 특정 조건에 해당 합니다. 이러한 조건이 AD DS 성공적으로 설치 해야 합니다. 일부 필수 조건이 되지 않을 경우 설치를 계속 하기 전에 해결할 수 있습니다. 또한 감지 하는 숲 또는 도메인 하지 아직 대 한 준비가 Adprep 배포 코드가 자동으로 실행 되도록 합니다.  
  
#### <a name="adprep-executables-dlls-ldfs-files"></a>실행 파일 ADPrep LDFs, Dll 파일  
  
-   ADprep.dll  
  
-   Ldifde.dll  
  
-   Csvde.dll  
  
-   Sch14.ldf-Sch56.ldf  
  
-   Schupgrade.cat  
  
-   *dcpromo.csv  
  
Adprep.dll에 이전의 ADprep.exe에 보관 광고 준비 코드 리팩터링 됩니다. 이렇게 하면 ADPrep.exe을 모두 ADDSDeployment Windows PowerShell 모듈에 대해 동일한 작업을 라이브러리를 사용 하 고 동일한 기능이 있습니다. Adprep.exe 설치 미디어에 포함 되어 있지만 자동화 된 프로세스 호출 하지는 않습니다 직접-관리자만 수동으로 실행 합니다. Windows Server 2008 x64 및 이상 운영 체제에서 실행할만 있습니다. Ldifde.exe 및 csvde.exe 수도 있는 리팩터링 버전 Dll 준비 과정에서 로드 하는으로 합니다. 여전히 스키마 확장 같은 서명이 확인 LDF 파일 이전 운영 체제 버전에서을 사용 합니다.  
  
![단순한 관리](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_AdprepDLLs.png)  
  
> [!IMPORTANT]  
> Windows Server 2012 용 32 비트 Adprep32.exe 도구가 있습니다. 하나 이상의 Windows Server 2008 x64, Windows Server 2008 R2 또는 Windows Server 2012 컴퓨터를 숲 및 도메인을 준비 하는 도메인 컨트롤러 구성원 서버 또는 작업 그룹에서 실행 있어야 합니다. Windows Server 2003 x64 Adprep.exe 실행 되지 않습니다.  
  
#### <a name="BKMK_PrereuisiteChecking"></a>필수 확인  
다른 작업에 따라 모드로 필수 관리 ADDSDeployment Windows PowerShell 코드에 기본 제공 되는 시스템 검사 작동 합니다. 다음 표에서 사용 하는 경우 각 테스트 하 고 방법에 대 한 설명 및 것 유효성을 검사 설명 합니다. 이 표를 유효성 검사에 실패 하 고 오류는 문제를 해결 하는 데 충분 문제가 있는 경우에 유용할 수 있습니다.  
  
이러한 테스트 로그인는 **위해 배포** 작업 범주에서 작업 이벤트 로그 채널 **Core**, 이벤트 ID로 항상 **103**합니다.  
  
##### <a name="prerequisite-windows-powershell"></a>필수 Windows PowerShell  
모든 도메인 컨트롤러 배포 cmdlet에 대 한 ADDSDeployment Windows PowerShell cmdlet 가지가 있습니다. 자녀가 관련된 cmdlet와 같은 인수 약 갖습니다.  
  
-   테스트 ADDSDomainControllerInstallation  
  
-   Test-ADDSDomainControllerUninstallation  
  
-   테스트 ADDSDomainInstallation  
  
-   테스트 ADDSForestInstallation  
  
-   테스트 ADDSReadOnlyDomainControllerAccountCreation  
  
필요는 없습니다; 일반적으로이 cmdlet 실행 하려면 자녀가 이미 자동으로 실행 배포 cmdlet 기본적으로 합니다.  
  
##### <a name="BKMK_ADDSInstallPrerequisiteTests"></a>필수 테스트  
  
||||  
|-|-|-|  
|테스트 이름|프로토콜<br /><br />사용|설명 하 고 메모|  
|VerifyAdminTrusted<br /><br />ForDelegationProvider|LDAP|"사용 위임 신뢰할 수 있도록 컴퓨터 및 사용자 계정을" 있는지 확인 (SeEnableDelegationPrivilege) 권한 기존 파트너 도메인 컨트롤러에 있습니다. 이 토큰 생성된 그룹 특성 액세스가 필요합니다.<br /><br />Windows Server 2003 도메인 컨트롤러에 연결할 때 사용 되지 않습니다. 이 프로 모션 전에 사용이 권한을 수동으로 확인 해야|  
|VerifyADPrep<br /><br />필수 (숲)|LDAP|검색 하 고 스키마 마스터 rootDSE namingContexts 특성과 스키마 명명 상황에 맞는 fsmoRoleOwner 특성을 사용 하 여 연결 합니다. AD DS 설치를 위해 필요한 (forestprep, 도메인 준비를 하거나 rodcprep) 어떤 준비 작업을 결정 합니다. 스키마의 유효성을 검사를 확장 필요한 추가 objectVersion 필요 합니다.|  
|VerifyADPrep<br /><br />필수 (도메인 및 RODC)|LDAP|검색 하 고 인프라 마스터 rootDSE namingContexts 특성과 인프라 컨테이너 fsmoRoleOwner 특성을 사용 하 여 연결 합니다. 설치의 경우이 테스트 도메인 이름 지정 마스터를 검색 하 고 온라인 되었는지 확인 합니다.|  
|CheckGroup<br /><br />멤버십|LDAP,<br /><br />RPC SMB (LSARPC)을 통해|유효성 검사는 사용자가 (추가 하거나 추가 하거나 제거 하는 도메인 EA 도메인 컨트롤러 내리기 DA) 작업에 따라 도메인 관리자 또는 Enterprise 관리자 그룹의 회원|  
|CheckForestPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC SMB (LSARPC)을 통해|유효성 검사는 사용자가 스키마 관리자의 회원 엔터프라이즈 관리자 그룹화 하 고 관리 감사 및 기존 도메인 컨트롤러에 보안 이벤트 로그 (SesScurityPrivilege) 권한|  
|CheckDomainPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC SMB (LSARPC)을 통해|사용자의 유효성을 검사 도메인 관리자 그룹의 회원은 관리 감사 하 고 있고 기존 도메인 컨트롤러에 보안 이벤트 로그 (SesScurityPrivilege) 권한|  
|CheckRODCPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC SMB (LSARPC)을 통해|사용자의 유효성을 검사 Enterprise 관리자 그룹의 회원은 관리 감사 하 고 있고 기존 도메인 컨트롤러에 보안 이벤트 로그 (SesScurityPrivilege) 권한|  
|VerifyInitSync<br /><br />AfterReboot|LDAP|RootDSE 특성 becomeSchemaMaster 더미 값으로 설정 하 여 다시 시작 된 이후 스키마 마스터에 한 번 이상 복제 유효성 검사|  
|VerifySFUHotFix<br /><br />적용|LDAP|기존 숲 속의 유효성을 검사 스키마 UID 특성 OID 1.2.840.113556.1.4.7000.187.102 사용에 대 한 알려진된 문제가 SFU2 확장 없으면<br /><br />([https://support.microsoft.com/kb/821732](https://support.microsoft.com/kb/821732))|  
|VerifyExchange<br /><br />SchemaFixed|LDAP WMI DCOM RPC|기존 숲 속의 유효성을 검사 스키마 되지 않는 문제 조직이 나 확장 ms 포함 되어 있을-Exch-도우미-이름, ms-Exch-LabeledURI, ms Exch-집 식별자 ([https://support.microsoft.com/kb/314649](https://support.microsoft.com/kb/314649))|  
|VerifyWin2KSchema<br /><br />일관성|LDAP|기존 숲 속의 유효성을 검사 스키마 (타사에서 수정 되지 잘못) 일관 된 특성과 클래스 핵심 합니다.|  
|DCPromo|RPC 통해 DRSR<br /><br />LDAP,<br /><br />DNS<br /><br />RPC SMB (SAMR)을 통해|프로 모션 코드 및 테스트 프로 모션에 전달 명령줄 구문을 유효성을 검사 합니다. 숲 속의 유효성을 검사 또는 새로 만드는 경우 도메인 이미 존재 하지 않습니다.|  
|VerifyOutbound<br /><br />ReplicationEnabled|LDAP DRSR SMB, RPC SMB (LSARPC)을 통해 위로|복제 파트너 NTDS 설정을 개체 옵션 특성 NTDSDSA_OPT_DISABLE_OUTBOUND_REPL (0x00000004) 확인 하 여 활성화 아웃 바운드 복제가 지정 된 기존 도메인 컨트롤러의 유효성을 검사합니다|  
|VerifyMachineAdmin<br /><br />암호|RPC 통해 DRSR<br /><br />LDAP,<br /><br />DNS<br /><br />RPC SMB (SAMR)을 통해|안전 모드 암호 DSRM 도메인 복잡성 요구 사항을 충족 설정 검사 합니다.|  
|VerifySafeModePassword|*해당 없음*|로컬 관리자가 암호 설정 충족 컴퓨터 보안 정책이 복잡성 요구 사항을 확인 합니다.|  
  


