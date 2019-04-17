---
ms.assetid: b3d6fb87-c4d4-451c-b3de-a53d2402d295
title: "새로운 Windows Server 2012 Active Directory 숲 (수준을 200) 설치"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b8a7502a1b9d27b0f61353f2544182a64d311496
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-new-windows-server-2012-active-directory-forest-level-200"></a>새로운 Windows Server 2012 Active Directory 숲 (수준을 200) 설치

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 새로운 Windows Server 2012 Active Directory 도메인 서비스 도메인 컨트롤러 프로 모션 기능 소개 수준에서에 대해 설명 합니다. Windows Server 2012에서 광고 DS 대체 Dcpromo 도구 서버 관리자와 함께 및 배포 Windows PowerShell 기반 시스템 합니다.  
  
-   [Active Directory 도메인 간편한 관리 서비스](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SimplifiedAdmin)  
  
-   [기술 개요](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_TechOverview)  
  
-   [숲 서버 관리자와 함께 배포](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [배포를 Windows PowerShell로 숲](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_PSForest)  
  
## <a name="BKMK_SimplifiedAdmin"></a>Active Directory 도메인 간편한 관리 서비스  
Windows Server 2012 차세대 Active Directory 도메인 서비스 간체 관리를 소개 하 고에서 가장 부 도메인 다시 계획 Windows 2000 Server 이후입니다. 광고 DS 간체 관리 Active Directory 12 년간에서 배운 교훈을 수행 하 고 설계자와 관리자는 더 지원 더 유연한, 더욱 직관적인 관리 환경을 만듭니다. 이것은 새 버전으로 확장 구성 요소 Windows Server 2008 r 2에 출시 된 기능 뿐만 아니라 기술을 기존 의미 합니다.  
  
### <a name="what-is-ad-ds-simplified-administration"></a>관리 간체 AD DS 무엇 인가요?  
광고 DS 간체 관리 도메인 배포는 reimagining입니다. 이러한 기능 중 일부는 다음과 같습니다.  
  
-   광고 DS 역할 배포 새 관리자 서버가 아키텍처 포함 되어 있으며 원격 설치 합니다.  
  
-   그래픽 설정을 사용 하는 경우에 광고 DS 배포 및 구성 엔진은 이제 Windows PowerShell입니다.  
  
-   프로 모션 이제 실패 프로 모션 기회가 내려 새 도메인 컨트롤러에 대 한 준비를 숲 및 도메인의 유효성을 검사 필수 검사 포함 되어 있습니다.  
  
-   Windows Server 2012 숲 수준 새로운 기능을 구현 하지 않는 및 도메인 기능 수준을 선도 관리자는 자주 방문 하는 새로운 Kerberos 기능 중 일부에만 필요 기능 동일한 도메인 컨트롤러 환경에 대 한 필요 합니다.  
  
### <a name="purpose-and-benefits"></a>목적 및 이점  
이러한 변경 내용을 더 복잡 하 고 있지 간단 나타날 수 있습니다. 하지만 광고 DS 배포 프로세스를 새롭게 구성의 수가 적고, 더 쉽게 작업에 많은 단계 및 모범 사례 결합 하는 기회가 했습니다. 즉, 예를 들어, 새 복제 도메인 컨트롤러의 그래픽 구성 이전 12 것이 아니라 대화 상자 8 되었습니다. 새 Active Directory 숲 만들려면 필요는 *단일* 만를 Windows PowerShell 명령 *한* 인수:은 도메인 이름입니다.  
  
Windows Server 2012에서 Windows PowerShell에 중점 이유는? 분산 컴퓨팅 발전 함에 따라 Windows PowerShell 및 유지 관리 그래픽 둘 다에서 구성과 명령줄 인터페이스에 대 한 단일 엔진 수 있게 합니다. API 개발자에 게 권한을 부여 하는 IT 전문가 위한 첫 번째 클래스 국적 같은 부분이 있으면 완전 한 기능의 스크립트를 허용 합니다. 클라우드 기반 컴퓨팅 보편적 되면서 Windows PowerShell 마지막으로 그래픽 인터페이스 없이 컴퓨터 모니터와 마우스가 있는 하나 동일한 관리 기능에 있는 서버를 원격으로 관리 하는 기능을 제공 합니다.  
  
베테랑 AD DS 관리자 이전 지식을 관련성 높은 찾을 수 있습니다. 시작 관리자 보다 수준 수가 가장 적은 학습 곡선 볼 수 있습니다.  
  
## <a name="BKMK_TechOverview"></a>기술 개요  
  
### <a name="what-you-should-know-before-you-begin"></a>항목을 시작 하기 전에 알아야 할  
이 항목 이전 버전의 Active Directory 도메인 서비스 익숙한 따르며 자신의 목적 및 기능 기본 세부 정보를 제공 하지 않습니다. 광고 DS에 대 한 자세한 내용은 아래 링크 TechNet 포털 페이지를 참조 합니다.  
  
-   [Windows Server 2008 r 2에 대 한 active Directory 도메인 서비스](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
  
-   [Windows Server 2008 용 active Directory 도메인 서비스](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
  
-   [Windows Server Technical 참조](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
  
### <a name="functional-descriptions"></a>기능 설명  
  
#### <a name="ad-ds-role-installation"></a>광고 DS 역할 설치  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_SelectServerRoles.gif)  
  
Active Directory 도메인 서비스 설치 서버 관리자 및 Windows PowerShell와 같은 다른 모든 서버 역할 및 Windows Server 2012의 기능 사용. 더 이상 Dcpromo.exe 프로그램 GUI 구성 옵션을 제공합니다.  
  
Windows PowerShell에 대 한 서버 관리자 또는 ServerManager 모듈 그래픽 마법사를 사용 하 여 지역 및 원격 설치 합니다. 이러한 마법사 또는 cmdlet 여러 개 실행 하 고 다른 서버 표적화를에 배포할 수 있습니다 AD DS를 여러 도메인 컨트롤러 동시에 one 콘솔에서 모두 합니다. 이러한 새로운 기능이 이전 버전과 이전 운영 체제 또는 Windows Server 2008 r 2와 호환 되는, 클래식 명령줄에서 로컬 역할 설치를 위해 Windows Server 2008 r 2에 새롭게 적용 된 Dism.exe 응용 프로그램 또한 계속 사용할 수 있습니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSAddWindowsFeature.png)  
  
#### <a name="ad-ds-role-configuration"></a>광고 DS 역할 구성  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
"이전의 DCPROMO" active Directory 도메인 서비스 구성 a 별도 작업의 역할 설치 됩니다. AD DS 역할을 설치한 후 관리자 ADDSDeployment Windows PowerShell 모듈 또는 마법사 별도 내에서 서버 관리자를 사용 하 여 도메인 컨트롤러 서버를 구성 합니다.  
  
광고 DS 역할 구성 12 년간의 필드 경험 빌드 고 이제 가장 최근 Microsoft 모범 사례에 따라 도메인 컨트롤러를 구성 합니다. 예를 들어, Domain Name System 및 카탈로그 전 세계 모든 도메인 컨트롤러에서 기본적으로 설치 됩니다.  
  
서버 관리자 AD DS 구성 마법사 많은 개별 대화 상자에 더 적은 프롬프트 하며 "고급" 모드에서 설정 숨기는 더 이상 합니다. 프로 모션 전체 프로세스 확장 한 대화 상자에 설치 중입니다. 마법사 및 ADDSDeployment Windows PowerShell 모듈 보여 눈에 띄는 변경 내용 및 자세한 정보를 링크가 있는 보안 문제입니다.  
  
Dcpromo.exe 명령줄 자리를 비운 사이만 설치에 대 한 Windows Server 2012에 남아 있으며 더 이상 그래픽 설치 마법사가 실행 됩니다. 좋습니다 Dcpromo.exe 설치 자리를 비운 사이 대 한 사용 중지 하 고 ADDSDeployment 모듈 교체 처럼 지금 사용 되지 실행 다음 버전의 Windows에 포함 되지 것입니다.  
  
이러한 새로운 기능 Windows Server 2008 R2 또는 이전 운영 체제 이전 버전과 호환 되지 않습니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSForest.png)  
  
> [!IMPORTANT]  
> Dcpromo.exe 더 이상 그래픽 마법사를 포함 하 고 더 이상 바이너리 역할 또는 기능을 설치 합니다. Dcpromo.exe 탐색기 셸 반환에서 실행 하는 다음과 같습니다.  
>   
> "Active Directory 도메인 Services 설치 마법사 서버 관리자 재배치입니다. For more information, see https://go.microsoft.com/fwlink/?LinkId=220921."  
>   
> 이전 운영 체제와 같이 바이너리 설치 하지만 경고 여전히 하려고 할 때 실행할 Dcpromo.exe /unattend 다음과 같습니다.  
>   
> "Dcpromo 자리를 비운 사이 작업에 대 한 Windows PowerShell ADDSDeployment 모듈으로 대체 됩니다. For more information, see https://go.microsoft.com/fwlink/?LinkId=220924."  
>   
> Windows Server 2012 deprecates dcpromo.exe 향후 버전의 Windows에 포함 되지 않습니다 없으며 것 받습니다 더욱 향상이 운영 체제에 있습니다. 관리자가 사용 하 고 명령줄에서 도메인 컨트롤러를 원하는 경우 지원 되는 Windows PowerShell 모듈으로 전환 해야 합니다.  
  
#### <a name="prerequisite-checking"></a>필수 확인  
또한 도메인 컨트롤러 구성 반환 숲 및 도메인 도메인 컨트롤러 프로 모션을 계속 하기 전에 필수 확인 단계를 구현 합니다. FSMO 역할 사용 가능 여부, 사용자 권한을, 확장된 스키마 호환성 및 기타 요구 사항을 포함합니다. 이 디자인 줄여 도메인 컨트롤러 프로 모션 시작 하 고 다음으로 구성 오류로 중간 중단 되는 문제를 줍니다. 이 기회를 가지게 숲 고아 도메인 컨트롤러 메타 데이터를 줄어들며 또는 도메인 컨트롤러 서버에 올바르게 생각 하지 않을 수 있습니다.  
  
## <a name="BKMK_SMForest"></a>숲 서버 관리자와 함께 배포  
이 섹션의 첫 번째 도메인 컨트롤러 서버 관리자 그래픽 Windows Server 2012 컴퓨터에서 사용 하 여 이렇게에 설치 하는 방법에 설명 합니다.  
  
### <a name="server-manager-ad-ds-role-installation-process"></a>설치 프로세스 서버 관리자 광고 DS 역할  
아래 다이어그램 ServerManager.exe 실행 중이 고 전에 프로 모션 도메인 컨트롤러의 오른쪽 끝을 부터는 Active Directory 도메인 서비스 역할 설치 프로세스를 보여 줍니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment.png)  
  
#### <a name="server-pool-and-add-roles"></a>서버 풀 역할을 추가 하 고  
서버 관리자 실행 하는 컴퓨터에서 액세스할 수 있는 모든 Windows Server 2012 컴퓨터 풀링을 대 한 자격이 있으며 있습니다. 풀 되 면 원격 설치 AD DS 또는 가능한 내에서 서버 관리자 다른 구성 옵션에 대 한 이러한 서버 선택 합니다.  
  
서버를 추가 하려면 다음 중 하나를 선택 합니다.  
  
-   클릭 **관리에 다른 서버 추가** 대시보드 시작 타일  
  
-   클릭 하 고 **관리** 메뉴 **서버 추가**  
  
-   마우스 오른쪽 단추로 클릭 **모든 서버** 선택 **서버 추가**  
  
이러한 서버 추가 대화 상자를 표시 합니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddServers.png)  
  
이렇게 하면 서버를 사용 하거나 그룹화 풀에 추가 하는 세 가지 방법은 다음과 같습니다.  
  
-   Active Directory 검색 (ldap는 컴퓨터가 도메인에 속한, 운영 체제 필터링 허용 및 필요 와일드 카드 지원)  
  
-   검색 DNS (ARP 또는 NetBIOS 브로드캐스트 또는 WINS 조회 통해 IP 주소 또는 DNS 별칭을 사용 하 여 허용 하지 않습니다 운영 체제 필터링 또는 지원 와일드 카드)  
  
-   (CR /LF로 구분 서버 텍스트 파일 목록을 사용 하 여) 가져오기  
  
클릭 **지금 찾기** 서버 목록에서 컴퓨터에 가입 하는 동일한 Active Directory 도메인 돌아가려면 서버 목록에서 하나 이상의 서버 이름을 클릭 합니다. 오른쪽 화살표를 클릭 하 고 서버 추가 **선택한** 목록입니다. 사용 하는 **서버 추가** 대화 상자를 선택한 서버 대시보드 역할 그룹에 추가 합니다. 키를 누르거나 **관리**을 차례로 클릭 하 고 **서버 그룹 만들기**, 키를 누르거나 **서버 그룹 만들기** 대시보드에서 **서버 관리자를 시작** 타일을 사용자 지정 서버 그룹을 만들 합니다.  
  
> [!NOTE]  
> 서버 추가 절차는 서버를 했거나 온라인으로 액세스할 수 있는지 확인 하지 않습니다. 그러나 다음 새로 고침에 효율성 보기로 서버 관리자에는 연결할 수 없는 서버 플래그를 지정합니다  
  
역할 설치할 수 원격으로 모든 Windows Server 2012에서 컴퓨터 추가 풀을와 같이:  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/tADDS_SMI_TR_AddRolesFeatures.png)  
  
Windows Server 2012 보다 오래 된 운영 체제를 실행 하는 서버를 완벽 하 게 관리할 수 없습니다. **역할 추가 및 기능** 선택 ServerManager Windows PowerShell 모듈 실행 **설치 WindowsFeature**합니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddADDSToAnotherServer.png)  
  
원격 서버 광고 DS 설치 AD DS 대시보드 타일 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 이미 미리 선택 역할을 선택할 수 서버 관리자 대시보드 기존 도메인 컨트롤러에서 사용할 수도 있습니다 **AD DS 다른 서버에 추가**합니다. 이 호출 **설치-WindowsFeature 광고 도메인 서비스**합니다.  
  
컴퓨터에서 관리자 서버를 실행 하는 자체 자동으로 풀 합니다. AD DS 역할 여기를 설치 하려면 클릭 하기만 하면는 **관리** 메뉴를 클릭 **역할 추가 및 기능**합니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ManageAddRoles.png)  
  
#### <a name="installation-type"></a>설치 유형  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectInstallationType.png)  
  
**설치 유형을** 대화 Active Directory 도메인 서비스를 지원 하지 않는 옵션을 제공:는 **원격 데스크톱 서비스 시나리오 따라 설치**합니다. 해당 옵션 다중 서버 분산된 작업에서 원격 데스크톱 서비스가 허용합니다. 을 선택 하면 광고 DS 설치할 수 없습니다.  
  
항상 선택 된 상태로 둔 기본 곳에서 광고 DS 설치 하는 경우: **역할 또는 기능 기반 설치**합니다.  
  
#### <a name="server-selection"></a>서버 선택  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectDestinationServer.png)  
  
**서버 선택** 대화 상자를 사용 하는 것과 이전에 풀에 추가 하는 서버 중 하나를 선택할 수 있습니다. 서버 관리자 실행 하는 로컬 서버는 자동으로 사용할 수 있습니다.  
  
또한 Windows Server 2012 운영 체제에서 오프 라인 Hyper-v VHD 파일 선택한 서버 관리자에 구성 요소 서비스를 통해 직접 역할을 추가 합니다. 추가 구성 하기 전에 필요한 구성 된 가상 서버를 제공할 수 있습니다.  
  
#### <a name="server-roles-and-features"></a>서버 역할 및 기능  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectServerRoles.png)  
  
선택는 **Active Directory 도메인 서비스** 하려면 홍보 도메인 컨트롤러 역할입니다. 모든 Active Directory 관리 기능과 필요한 서비스 자동으로 설치 되거나 다른 역할의 일부인 겉 서버 관리자 인터페이스에서 선택한 표시 되지 않는 경우에 합니다.  
  
서버 관리자가이 역할 암시적 설치; 관리 기능을 보여 주는 정보 대화도 표시 이 해당 하는 **-IncludeManagementTools** 인수 합니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddFeaturesDialog.gif)  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectFeatures.png)  
  
추가 **기능** 여기에 추가할 수 원하는 대로 합니다.  
  
#### <a name="active-directory-domain-services"></a>Active Directory Domain Services  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSIntro.png)  
  
**Active Directory 도메인 서비스** 대화 요구 사항 및 모범 사례에 제한 된 정보를 제공 합니다. 주로 AD DS 역할 선택한 확인 역할도 "이이 화면이 표시 되지 않으면 선택 하지 않은 AD DS 합니다.  
  
#### <a name="confirmation"></a>확인  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Confirmation.png)  
  
**확인** 대화 역할 설치를 시작 하기 전에 최종 검사점입니다. 역할 설치 후 필요에 따라 컴퓨터를 다시 시작 하는 옵션이 제공 하지만 광고 DS 설치 다시 부팅 필요 하지 않습니다.  
  
클릭 하 여 **설치**, 역할 설치를 시작할 준비가 확인 합니다. 시작 된 후 역할 설치를 취소할 수 없습니다.  
  
#### <a name="results"></a>결과  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Results.png)  
  
**결과** 현재 설치 진행률과 설치 상태를 현재 대화 상자에 표시 됩니다. 역할 설치 관리자 서버를 닫을 여부에 상관 없이 계속 됩니다.  
  
설치 결과 확인 하는 여전히는 것이 좋습니다. 사용 중지 하는 경우는 **결과** 설치를 완료 하기 전에 대화 상자에서 서버 관리자 알림 플래그를 사용 하 여 결과 확인할 수 있습니다. 또한 서버 관리자 AD DS 역할 설치 했지만 더로 구성 되지 도메인 컨트롤러 서버에 대 한 경고 메시지를 표시 합니다.  
  
**작업 알림**  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskNotofications.png)  
  
**광고 DS 세부 정보**  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSDetails.png)  
  
**작업 세부 정보**  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskDetails.png)  
  
#### <a name="promote-to-domain-controller"></a>도메인 컨트롤러에 홍보 합니다.  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Promote.png)  
  
AD DS 역할 설치 끝 계속할 수 구성을 사용 하 여는 **도메인 컨트롤러이 서버 홍보** 링크입니다. 이 도메인 컨트롤러 서버를 확인 하는 데 필요한 하지만 구성 마법사를 즉시 실행 하지 않아도 됩니다. 예를 들어 서버 AD DS 바이너리 이후 구성에 대 한 또 다른 지점에 게 보내기 전에 프로 비전만 좋습니다. 배송 되기 전에 AD DS 역할을 추가 하 여 목적지에 도달한 경우 시간을 절약할 수 있습니다. 오프 라인으로 도메인 컨트롤러 며칠 또는 몇 주 후에 유지 되지의 가장 좋은 방법은 수행 수도 있습니다. 마지막으로,이 후속 하나 이상 다시 부팅할 절약 도메인 컨트롤러 프로 모션 전에 구성 요소를 업데이트할 수 있습니다.  
  
ADDSDeployment cmdlet 호출 나중에이 링크를 선택 하: **설치 addsforest**, **설치 addsdomain**, 또는 **설치 addsdomaincontroller**합니다.  
  
### <a name="uninstallingdisabling"></a>제거/사용 안 함  
사용자 도메인 컨트롤러 서버를 수준 올렸습니다 있는지 여부에 상관 없이 다른 역할을와 같은 AD DS 역할을 제거 합니다. 그러나 AD DS 역할 제거 완료 되 면 컴퓨터를 다시 시작을 해야 합니다.  
  
Active Directory 도메인 서비스 역할 제거와에서는 다릅니다 설치를 완료 하기 전에 도메인 컨트롤러 수준 내리기 있어야 한다는입니다. 이 도메인 컨트롤러 역할 바이너리 숲에서 적절 한 메타 데이터 정리 없이 제거 하는 데 하지 못하도록 합니다. 자세한 내용은 참조 [내리기 도메인 컨트롤러 및 도메인 & #40; 200 수준 & #41; ](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
> [!WARNING]  
> Dism.exe 또는 Windows PowerShell DISM 모듈 AD DS 역할을 제거 하 후 도메인 컨트롤러에 프로 모션은 지원 되지 않으며 서버 정상적으로 부팅 되지 것입니다.  
>   
> 서버 관리자 나 Windows PowerShell는 광고 DS 배포 모듈 달리 DISM는 기본 서비스 시스템에 하지 못하므로 AD DS 또는 구성을입니다. 서버를 더 이상 도메인 컨트롤러 없으면 AD DS 역할을 제거 하려면 Dism.exe 또는 Windows PowerShell DISM 모듈 사용 하지 마십시오.  
  
### <a name="create-an-ad-ds-forest-root-domain-with-server-manager"></a>AD DS 숲 루트 도메인 서버 관리자를 사용 하 여 만들기  
다음 다이어그램 Active Directory 도메인 서비스 구성 프로세스를 이전에 설치 AD DS 역할을 시작 하는 경우 나와 있는 **Active Directory 도메인 서비스 구성 마법사** 서버 관리자를 사용 합니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_forestdeploy2.png)  
  
#### <a name="deployment-configuration"></a>배포 구성  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddNewForest.png)  
  
서버 관리자 모든 도메인 컨트롤러 프로 모션으로 시작 되 고 **배포 구성** 페이지 합니다. 나머지 옵션과 필수 필드가 페이지에서 다음 페이지를 선택 하는 배포 작업에 따라 변경 됩니다.  
  
새 Active Directory 숲 만들려면 클릭 **새 숲 추가**합니다. 제공 해야 유효한 루트 도메인 이름입니다. 단일 레이블이 지정 된 이름이 수 없습니다 (이름은 해야 예를 들어, *contoso.com* 유사한 및 뿐 아니라 *contoso*) 하 고 허용된 DNS 도메인 이름 요구 사용 해야 합니다.  
  
For more information on valid domain names, see KB article [Naming conventions in Active Directory for computers, domains, sites, and OUs](https://support.microsoft.com/kb/909264).  
  
> [!WARNING]  
> 새 Active Directory 숲 외부 DNS 이름으로 동일한 이름의 만들지 않습니다. 예를 들어, 인터넷 DNS URL http://contoso.com 이면 향후 호환성 문제를 방지 하 여 내부 숲에 대 한 다른 이름을 선택 해야 합니다. 해당 이름은 고유 하 고 웹 교통량 해야 합니다. 예: corp.contoso.com 합니다.  
  
새 숲 도메인의 관리자 계정에 대 한 새로운 자격 증명을 필요 하지 않습니다. 도메인 컨트롤러 프로 모션 프로세스 숲 루트 만드는 데 사용 하는 첫 번째 도메인 컨트롤러에서 기본 제공 된 관리자 계정 자격 증명을 사용 합니다. 방법은 없습니다 기본적으로 기본 관리자 계정으로 잠그는 하거나 사용 하지 않도록 설정 하 고 다른 관리 도메인 계정에 사용할 수 없는 경우 숲을에 유일한 진입점 될 수 있습니다. 것이 중요 하며, 새 숲 배포 하기 전에 암호를 알고 있습니다.  
  
**도메인 이름** 유효한 정식된 도메인 DNS 이름이 필요 하 고 필요 합니다.  
  
#### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DCOptions_Forest.gif)  
  
**도메인 컨트롤러 옵션** 구성할 수 있습니다의 **기능 수준 포리스트** 및 **도메인 기능 수준** 의 새 이렇게 합니다. 기본적으로 이러한 설정은 Windows Server 2012에서 새 숲 루트 도메인 합니다. Windows Server 2012 숲 기능 수준 Windows Server 2008 R2 숲 기능 수준 통해 새 기능을 제공 하지 않습니다. Windows Server 2012 도메인 기능 수준을 새 Kerberos 설정 구현 하는 데 필요한 "항상 클레임 제공" 및 "무방비 인증 요청 실패 합니다." Windows Server 2012에서 기능 수준에 기본 사용 운영 체제 보다 최소 허용 요구 사항을 충족 하는 도메인 도메인 컨트롤러 참여를 제한 하는 것입니다. 즉, Windows Server 2012 도메인 기능 수준만 도메인 컨트롤러 Windows Server 2012를 실행 하는 도메인 호스트할 수 지정할 수 있습니다.  Windows Server 2012 이라는 새로운 도메인 컨트롤러 플래그 구현 **DS_WIN8_REQUIRED** 에 **DSGetDcName** 의 NetLogon 단독으로 Windows Server 2012 도메인 컨트롤러를 찾는 기능은 합니다. 이렇게 하면는 유연성 더 유형이 또는 다른 유형의 숲은 측면에서 운영 체제 도메인 컨트롤러에서 실행 되도록 허용 됩니다.  
  
For more information about domain controller Location, review [Directory Service Functions](https://msdn.microsoft.com/library/ms675900(VS.85).aspx).  
  
구성할 수 도메인 컨트롤러 기능이 DNS 서버 옵션입니다. 모든 도메인 컨트롤러 사용 가능 하도록 분산된 환경에는 기본적으로이 옵션을 선택 모드 나 도메인에 있는 도메인 컨트롤러를 설치할 때 이유 DNS 서비스를 제공 하는 것이 좋습니다. 드 및 읽기 도메인 컨트롤러 옵션만 때 사용할 수 없는 만들어 새로 숲 루트 도메인.입니다. 첫 번째 도메인 컨트롤러 GC, 있어야 하 고는 읽기만 RODC (도메인 컨트롤러)를 수 없습니다.  
  
지정 된 **디렉터리 서비스 복원 모드 암호** 기본적으로 강력한 암호를; 하지 않아도 하는 서버에 적용 되는 암호 정책을 준수 해야 공백 하나의 합니다. 항상 복잡 하 고 강력한 암호 또는 암호를 선택 합니다.  
  
#### <a name="dns-options-and-dns-delegation-credentials"></a>DNS 옵션과 DNS 위임 자격 증명  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestDNSOptions.png)  
  
**DNS 옵션** 페이지 DNS 위임 구성 하 고 대체 DNS 관리자 자격 증명을 제공할 수 있습니다.  
  
구성할 수 없습니다 DNS 옵션이 나 위임 Active Directory 도메인 서비스 구성 마법사에서 새로운 Active Directory 숲 루트 도메인 선택한 위치를 설치할 때의 **DNS 서버** 에 **도메인 컨트롤러 옵션** 페이지 합니다. **DNS 만들기 위임** 기존 DNS 서버 인프라에 새 숲 루트 DNS 영역을 만들 때이 옵션을 사용할 수 있습니다. 이 옵션을 사용 하면 대체 DNS 관리자 자격 증명을 DNS 영역 업데이트에 대 한 권한이 제공할 수 있습니다.  
  
For more information about whether you need to create a DNS delegation, see [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx).  
  
#### <a name="additional-options"></a>추가 옵션  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestAdditionalOptions.png)  
  
**추가 옵션** 페이지 표시 되는 도메인의 NetBIOS 이름 및 재정의 수 있습니다. 기본적으로 NetBIOS 도메인 이름 일치 제공 정식된 도메인 이름의 왼쪽 맨 레이블을 **배포 구성** 페이지 합니다. 예를 들어 corp.contoso.com 정식된 도메인 이름을 제공한 경우 기본 NetBIOS 도메인 이름은 CORP.  
  
이름이 15 자 충돌 하지 않는 다른 NetBIOS 이름의 유효 하지 변경 합니다. NetBIOS 다른 이름으로 충돌 하 않도록 숫자 이름에 추가 됩니다. 이름이 15 자 경우 마법사 고유한, 잘림 제안을 제공 합니다. 두 경우 모두 마법사 먼저의 유효성을 검사 이름이 없는 통해 WINS 조회 사용에서 및 NetBIOS 브로드캐스트 됩니다.  
  
For more information on valid domain names, see KB article [Naming conventions in Active Directory for computers, domains, sites, and OUs](https://support.microsoft.com/kb/909264).  
  
#### <a name="paths"></a>경로  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPaths.png)  
  
**경로** SYSVOL 공유 및 페이지 데이터베이스 트랜잭션 로그가 광고 DS 데이터베이스의 기본 폴더 위치를 무시할 수 있습니다. 기본 위치는 항상 하위 % 시스템 루트 % (즉, C:\Windows)입니다.  
  
#### <a name="review-options-and-view-script"></a>스크립트 보기 및 리뷰 옵션  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestReviewOptions.png)  
  
**리뷰 옵션** 페이지를 설정을 확인 하 고 설치를 시작 하기 전에 사용자의 요구 사항에 맞는지 확인 수 있습니다. 설치 관리자 서버를 사용할 때 중지 마지막 기회 않습니다. 이 옵션은 구성 계속 하기 전에 설정을 확인 하는 옵션 간단 하 게  
  
**리뷰 옵션** 서버 관리자의 페이지도 선택적 제공 **스크립트 보기** 단추를 현재 ADDSDeployment 구성을 하나의 Windows PowerShell 스크립트도 포함 유니코드 텍스트 파일을 만듭니다. 서버 관리자 그래픽 인터페이스 Windows PowerShell 배포 studio로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용 하 여 옵션 구성 구성, 내보내고 마법사 취소 합니다. 이 프로세스 추가 수정 또는 직접 사용에 대해 유효 하 고 구문이 샘플을 만듭니다. 예를 들어:  
  
```powershell 
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSForest `  
-CreateDNSDelegation `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainMode "Win2012" `  
-DomainName "corp.contoso.com" `  
-DomainNetBIOSName "CORP" `  
-ForestMode "Win2012" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-NoRebootOnCompletion:$false `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> 일반적으로 서버 관리자 모든 인수 및 (에 따라 수 향후 버전의 Windows 또는 서비스 팩 간에) 기본값에 의존 하지 않는 경우 값을 입력 합니다. 이 한 가지 예외는는 **-safemodeadministratorpassword** 인수 (스크립트에서 의도적으로 생략은). 확인 메시지가 되도록 값을 생략 cmdlet 대화식으로 실행 될 때 합니다.  
  
#### <a name="prerequisites-check"></a>필수 확인  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPrereqCheck.png)  
  
**필수 확인** 광고 DS 도메인 구성의 새로운 기능입니다. 이 새로운 단계 서버 구성 새 AD DS 숲 지원 확인 합니다.  
  
새 숲 루트 도메인을 설치할 때는 서버 관리자 Active Directory 도메인 서비스 구성 마법사 호출 일련의 모듈식 테스트 합니다. 이러한 테스트 제안 된 복구 옵션을 알립니다. 필요에 따라 여러 번 테스트를 실행할 수 있습니다. 도메인 컨트롤러 프로세스 수 없는 모든 필수 테스트까지 계속 제공 전달 됩니다.  
  
**필수 확인** 이전 운영 체제에 영향을 주는 보안 변경와 같은 관련 정보를 표면 수도 있습니다.  
  
에 대 한 자세한 내용은 특정 필수 검사를 [필수 검사](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)합니다.  
  
#### <a name="installation"></a>설치  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestInstallation.png)  
  
때는 **설치** 페이지에 표시, 도메인 컨트롤러 구성 시작 되 고 하거나 수 없는 중단 취소 합니다. 자세한 작업이이 페이지에 표시 되며, 로그에 기록 합니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
> [!NOTE]  
> 실행할 수 있습니다 여러 역할 설치 및 구성 마법사 AD DS 동일한 서버 관리자 본체에서 동시에 있습니다.  
  
#### <a name="results"></a>결과  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**결과** 프로 모션 및 관리 중요 한 정보가의 성공 여부 페이지에 표시 됩니다. 도메인 컨트롤러 10 초 후 자동으로 다시 부팅 됩니다.  
  
## <a name="BKMK_PSForest"></a>배포를 Windows PowerShell로 숲  
이 섹션의 첫 번째 도메인 컨트롤러의 핵심 Windows Server 2012 컴퓨터에서 Windows PowerShell를 사용 하 여 이렇게 설치 하는 방법에 설명 합니다.  
  
### <a name="windows-powershell-ad-ds-role-installation-process"></a>Windows PowerShell 광고 DS 역할 설치 프로세스  
몇 가지 간단한 ServerManager 배포 cmdlet 배포 프로세스를 구현 하 여 더욱 사실을 AD DS 비전 간체 관리 합니다.  
  
다음 그림을 실행 하면 부터는 Active Directory 도메인 서비스 역할 설치 프로세스를 보여 줍니다. **PowerShell.exe** 도메인 컨트롤러의 프로 모션 하기 전에 바로 종료 하 고 있습니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment_powershell.png)  
  
|||  
|-|-|  
|ServerManager Cmdlet|인수 (**굵게** 인수가 필요 합니다. *기울임꼴로 표시* 인수 Windows PowerShell 또는 광고 DS 구성 마법사를 사용 하 여 지정할 수 있습니다.)|  
|설치-WindowsFeature/추가-WindowsFeature|***이름***<br /><br />*다시 시작*<br /><br />*-IncludeAllSubFeature*<br /><br />*-IncludeManagementTools*<br /><br />소스<br /><br />*-ComputerName*<br /><br />자격 증명<br /><br />-LogPath<br /><br />*-Vhd*<br /><br />*-ConfigurationFilePath*|  
  
> [!NOTE]  
> 시간이 필수는 인수 **-IncludeManagementTools** 권장 AD DS 역할 바이너리를 설치 하는 경우  
  
ServerManager 모듈 Windows PowerShell에 대 한 새 DISM 모듈의 역할 설치, 상태 및 제거 부분을 제공합니다. 이 표시 되는이 층 가장 많은 작업을 간소화 하 고 위험할 오용 때) (그러나 강력한 직접 사용에 대 한 필요성을 줄일 수 DISM 모듈 합니다.  
  
사용 하 여 **Get 명령을** 별칭와 cmdlet에 ServerManager 내보내려면 합니다.  
  
```powershell  
Get-Command -module ServerManager  
```  
  
예를 들어:  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetCommand.png)  
  
간단 하 게 실행 Active Directory 도메인 서비스 역할을 추가 하는 **설치 WindowsFeature** 인수로 AD DS 역할 이름으로 합니다. 서버 관리자 같은 AD DS 역할 암묵적인 필요한 모든 서비스 자동으로 설치 됩니다.  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services  
```  
  
AD DS 관리 도구 설치 하려는 경우이 가장 좋습니다-제공 다음는 **-IncludeManagementTools** 인수:  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools  
```  
  
예를 들어:  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallWinFeature.png)  
  
모든 기능와 역할을 설치 상태를 표시 하려면 사용 **Get WindowsFeature** 인수 없이 합니다. 지정 **-ComputerName** 인수 원격 서버에서 설치 상태입니다.  
  
```powershell  
Get-WindowsFeature  
```  
  
때문에 **Get WindowsFeature** 필터링는 하지 않은 사용 해야 메커니즘을 **Where-object** 파이프라인 특정 기능을 찾을 수 있습니다. 사용 데이터를 전달 하기 위해 여러 cmdlet 간의 채널 파이프라인 및 Where-object cmdlet 필터 역할을 합니다. 기본 제공 **$_** 변수 파이프라인 포함 될 수 있는 속성을 통해 전달 현재 개체 역할도 합니다.  
  
```powershell  
Get-WindowsFeature | where-object <options>  
```  
  
예를 들어 모든 찾으려면에 "활성 디렉터리" 포함 기능 자신의 **표시 이름** 속성을 사용 합니다.  
  
```powershell  
Get-WindowsFeature | where displayname -like "*active dir*"  
```  
  
아래와 더 이상 예:  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetWindowsFeature.png)  
  
For more information about more Windows PowerShell operations with pipelines and Where-Object, see [Piping and the Pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).  
  
또한 Windows PowerShell 3.0에 크게이 파이프라인 작업에 필요한 명령줄 인수 간소화 note 합니다. Windows PowerShell 2.0이 요구 합니다.  
  
```powershell  
Get-WindowsFeature | where {$_.displayname - like "*active dir*"}  
```  
  
Windows PowerShell 파이프라인을 사용 하 여 읽을 수 있는 결과 만들 수 있습니다. 예를 들어:  
  
```powershell  
Install-WindowsFeature | Format-List  
Install-WindowsFeature | select-object | Format-List  
  
```  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDS.png)  
  
참고 어떻게 사용는 **선택 개체** 와 cmdlet는 **-expandproperty** 인수 흥미로운 데이터를 반환 합니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSWithTools.png)  
  
> [!NOTE]  
> **선택 개체 expandproperty** 전체 설치 성능 인수 약간 느려집니다.  
  
### <a name="BKMK_PS"></a>AD DS 숲 루트 도메인을 Windows PowerShell로 만들기  
ADDSDeployment 모듈을 사용 하 여 새 Active Directory 숲을 설치 하려면 다음 cmdlet 사용:  
  
```powershell  
Install-addsforest  
```  
  
**설치 AddsForest** cmdlet (필수 확인 하 고 설치) 2 단계에 있습니다. 아래 두 그림 표시 설치 단계와의 최소 반드시 **-도메인 이름**합니다.  
  
|||  
|-|-|  
|ADDSDeployment Cmdlet|인수 (**굵게** 인수가 필요 합니다. *기울임꼴로 표시* 인수 Windows PowerShell 또는 광고 DS 구성 마법사를 사용 하 여 지정할 수 있습니다.)|  
|설치 Addsforest|-확인<br /><br />*-CreateDNSDelegation*<br /><br />*-데이터베이스 경로*<br /><br />*-DomainMode*<br /><br />***-도메인 이름***<br /><br />***-DomainNetBIOSName***<br /><br />*-DNSDelegationCredential*<br /><br />*-포리스트*<br /><br />힘<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-NoDnsOnNetwork<br /><br />-NoRebootOnCompletion<br /><br />*-SafeModeAdministratorPassword*<br /><br />-SkipAutoConfigureDNS<br /><br />-SkipPreChecks<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-DomainNetBIOSName** DNS 도메인 이름 접두사에 따라 자동으로 생성 된 15 자의 이름 변경 하려는 경우 또는 이름을 초과 15 자 하는 경우의 인수가 필요 합니다.  
  
해당 하는 서버 관리자 **배포 구성** ADDSDeployment cmdlet 및 인수는 다음과 같습니다.  
  
```powershell  
Install-ADDSForest  
-DomainName <string>  
```  
  
해당 하는 서버 관리자 도메인 컨트롤러 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```powershell  
-ForestMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-InstallDNS <{$false | $true}>  
-SafeModeAdministratorPassword <secure string>  
  
```  
  
**설치 ADDSForest** 인수 지정 되지 않은 경우 동일한 기본값 서버 관리자로 서을 따릅니다.  
  
**SafeModeAdministratorPassword** 특별 한 인수의 작업은 다음과 같습니다.  
  
-   하는 경우 *지정 하지* 를 인수로 cmdlet 묻는 메시지를 입력 하 고 마스크 암호를 확인 합니다. 기본 설정된 사용 cmdlet 대화식으로 실행 될 때입니다.  
  
    예를 들어, corp.contoso.com 라는 새 숲 만들고 수 하 라는 메시지가 표시 입력 하 고 마스크 비밀 번호를 확인 합니다.  
  
    ```powershell  
    Install-ADDSForest "DomainName corp.contoso.com  
    ```  
  
-   지정 된 경우 *값*, 값 보안 문자열 여야 합니다. Cmdlet 대화식으로 실행 될 때 기본 설정된 사용 아닙니다.  
  
예를 들어, 요청할 수 있습니다 수동으로 암호를 사용 하 여는 **읽기 호스트** cmdlet에 대 한 보안 문자열 묻는:  
  
```powershell  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> 이전 옵션 암호를 확인 하지 않는 주의 사용 하 여: 암호가 표시 되지 않습니다.  
  
또한이 것이 좋음 있지만 변환 일반 텍스트 변수와 보안 문자열을 제공할 수 있습니다.  
  
```powershell  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
마지막으로 애매 암호에 파일을 저장 하 고 나타나지 암호화 되지 않은 텍스트 암호 없이 나중에 다시 수 있습니다. 예를 들어:  
  
```powershell  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> 지우기 또는 애매 텍스트 암호를 저장 또는 제공 권장 하지 않습니다. 스크립트가이 명령을 실행 또는이 기사를 통해 모든 사용자 해당 도메인 컨트롤러의 DSRM 암호를 알고 있습니다. 애매 암호를 취소할 수 파일에 액세스할 수 있는 모든 사람이. 해당 정보를 DSRM 시작 DC에 로그온 하 고 자녀의 권한 Active Directory 숲에서 가장 높은 수준의에 상승 도메인 컨트롤러 자체, 가장 결국 수 있습니다. 추가 단계를 사용 하 여 집합 **System.Security.Cryptography** 데이터는 것이 좋습니다 하지만 아니었습니다 텍스트 파일을 암호화 됩니다. 완전히 암호 저장을 방지 하는 것이 좋습니다.  
  
ADDSDeployment cmdlet 자동으로 DNS 클라이언트 설정, 전달자 및 루트 힌트 구성을 건너뛰게 하는 추가 옵션을 제공 합니다. 서버 관리자를 사용 하는 경우이 구성 옵션을 건너뛸 수 없습니다. 이 인수 도메인 컨트롤러 구성 전에 DNS 서버 역할을 설치한 경우에 중요 합니다.  
  
```powershell  
-SkipAutoConfigureDNS  
```  
  
**DomainNetBIOSName** 작업이 특별 한 이기도 합니다.  
  
-   하는 경우는 **DomainNetBIOSName** 인수 NetBIOS 도메인 이름와의 단일 레이블 접두사 도메인 이름 지정 하지 않으면는 **도메인 이름** 인수가 15 자 이하로 다음 프로 모션 계속 자동으로 생성 된 이름입니다.  
  
-   하는 경우는 **DomainNetBIOSName** 인수 NetBIOS 도메인 이름와의 단일 레이블 접두사 도메인 이름 지정 하지 않으면는 **도메인 이름** 인수는 16 자로 이상 프로 모션 실패 합니다.  
  
-   하는 경우는 **DomainNetBIOSName** 인수 15 자 이하로 NetBIOS 도메인 이름으로 지정 프로 모션 지정 된 이름이 계속 합니다.  
  
-   하는 경우는 **DomainNetBIOSName** 인수 16 자로의 NetBIOS 도메인 이름 또는 기타를 지정 프로 모션 실패 합니다.  
  
해당 하는 서버 관리자 추가 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```powershell  
-domainnetbiosname <string>  
```  
  
해당 하는 서버 관리자 **경로** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```powershell  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
  
```  
  
옵션을 사용 하 여 **Whatif** 인수의 **설치 ADDSForest** cmdlet 구성 정보를 검토 합니다. 이 cmdlet 인수 명시적 및 암묵적인 값을 볼 수 있습니다.  
  
예를 들어:  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSPaths.png)  
  
무시할 수 없는 **필수 확인** 때 되는데 서버 관리자를 사용 하 여 건너뛸 수 프로세스 AD DS 배포 cmdlet 인수를 사용 하 여 사용 하는 경우:  
  
```powershell  
-skipprechecks  
```  
  
> [!WARNING]  
> Microsoft 부분 도메인 컨트롤러 프로 모션 발생할 수 있는 되거나 손상 AD DS 숲 필수 검사를 건너뛰는 것이 수 없게 됩니다.  
  
참고 방법을 지난번 처럼 서버 관리자 **설치 ADDSForest** 프로 모션 서버 자동으로 부팅 하 게 알려줍니다.  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSReboot.png)  
  
![새 숲 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallProgress.png)  
  
다시 부팅 메시지를 자동으로 동의를 사용 하 여는 **-강제로** 또는 **-확인: $false** 인수 모든 ADDSDeployment Windows PowerShell cmdlet 사용 합니다. 서버 끝 프로 모션에 자동으로 다시 부팅 되지 않도록 하려면 사용는 **-norebootoncompletion** 인수 합니다.  
  
> [!WARNING]  
> 다시 부팅 재정의 것이 좋습니다. 도메인 컨트롤러 제대로 작동 하려면 다시 부팅 해야 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[도메인 서비스 active Directory (TechNet 포털)](https://technet.microsoft.com/library/cc770946(WS.10).aspx)  
[Windows Server 2008 r 2에 대 한 active Directory 도메인 서비스](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
[Windows Server 2008 용 active Directory 도메인 서비스](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
[Windows Server Technical 참조 (Windows Server 2003)](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
[관리 센터 active Directory: 시작 (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd560651(WS.10).aspx)  
[(Windows Server 2008 r 2) Windows PowerShell 된 active Directory 관리](https://technet.microsoft.com/library/dd378937(WS.10).aspx)  
[디렉터리 서비스 팀 (공식 Microsoft 상업적인 기술 지원 블로그)에 게 물어보기](http://blogs.technet.com/b/askds)  
  

