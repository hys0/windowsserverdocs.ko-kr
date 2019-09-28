---
ms.assetid: b3d6fb87-c4d4-451c-b3de-a53d2402d295
title: 새 Windows Server 2012 Active Directory 포리스트 설치(수준 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a9bdc3b237d0d0f44995f2c359cc3ef6ed8568a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71400369"
---
# <a name="install-a-new-windows-server-2012-active-directory-forest-level-200"></a>새 Windows Server 2012 Active Directory 포리스트 설치(수준 200)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 새 Windows Server 2012 Active Directory 도메인 서비스 도메인 컨트롤러 수준 올리기 기능을 소개 수준에서 설명합니다. Windows Server 2012의 AD DS에서는 Dcpromo 도구를 서버 관리자와 Windows PowerShell 기반 배포 시스템으로 대체합니다.  
  
-   [Active Directory Domain Services 단순화 된 관리](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SimplifiedAdmin)  
  
-   [기술 개요](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_TechOverview)  
  
-   [서버 관리자를 사용 하 여 포리스트 배포](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [Windows PowerShell을 사용 하 여 포리스트 배포](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_PSForest)  
  
## <a name="BKMK_SimplifiedAdmin"></a>Active Directory Domain Services 단순화 된 관리  
Windows Server 2012에서는 차세대 Active Directory Domain Services 간소화된 관리 기능이 도입되었으며 Windows 2000 Server 이후 도메인이 가장 크게 변경되었습니다. AD DS 간소화된 관리에서는 12년 동안 Active Directory에서 얻은 교훈을 바탕으로 설계자와 관리자를 위한 보다 지원 가능하고 유연하며 직관적인 관리 환경을 제공합니다. 이는 기존 기술의 새 버전을 만들 수 있을 뿐만 아니라 Windows Server 2008 R2에서 릴리스된 구성 요소의 기능을 확장할 수도 있습니다.  
  
### <a name="what-is-ad-ds-simplified-administration"></a>AD DS 간소화된 관리란?  
AD DS 간소화된 관리는 도메인 배포의 새로운 디자인입니다. 이러한 기능의 예를 들면 다음과 같습니다.  
  
-   AD DS 역할 배포가 이제 새로운 서버 관리자 아키텍처의 일부이며 원격 설치를 허용합니다.  
  
-   AD DS 배포 및 구성 엔진이 이제 Windows PowerShell이며, 이는 그래픽 설정을 사용하는 경우에도 마찬가지입니다.  
  
-   이제 수준 올리기에 새 도메인 컨트롤러에 대한 포리스트 및 도메인 준비 상태를 확인하는 필수 구성 요소 확인이 포함되어 있어 수준 올리기에 실패할 가능성이 낮아졌습니다.  
  
-   Windows Server 2012 포리스트 기능 수준에서 새로운 기능을 구현하지 않으며 도메인 기능 수준이 새로운 Kerberos 기능의 하위 집합에만 필요하므로 관리자에게 동종 도메인 컨트롤러 환경이 자주 필요하지 않습니다.  
  
### <a name="purpose-and-benefits"></a>목적 및 이점  
이러한 변경 내용은 단순하지 않고 보다 복잡하게 보일 수도 있습니다. 하지만 AD DS 배포 프로세스를 다시 디자인하는 과정에서 많은 단계와 모범 사례를 보다 적고 간편한 작업으로 병합할 기회가 있었습니다. 예를 들어 새 복제본 도메인 컨트롤러의 그래픽 구성이 12개의 대화 상자에서 8개의 대화 상자로 줄었습니다. 도메인 이름이라는 *하나*의 인수를 사용하는 *단일* Windows PowerShell 명령만으로 새 Active Directory 포리스트를 만들 수 있습니다.  
  
Windows Server 2012에서 Windows PowerShell을 이렇게 강조하는 이유는 무엇일까요? 분산 컴퓨팅이 진화함에 따라 Windows PowerShell은 그래픽 인터페이스와 명령줄 인터페이스에서 모두 구성 및 유지 관리에 단일 엔진을 사용하도록 지원합니다. Windows PowerShell을 통해 IT 전문가는 API에서 개발자에게 부여하는 동일한 권한으로 모든 구성 요소에 대해 모든 기능을 갖춘 스크립트를 작성할 수 있습니다. 클라우드 기반 컴퓨팅이 어디에나 존재하게 되면서 Windows PowerShell도 마침내 원격으로 서버를 관리할 수 있게 되었습니다. 그래픽 인터페이스가 없는 컴퓨터에도 모니터와 마우스를 갖춘 컴퓨터와 동일한 관리 기능이 있습니다.  
  
숙련된 AD DS 관리자는 그동안 쌓아 온 지식을 매우 유용하게 활용할 수 있으며, 초보 관리자는 매우 빠르게 관련 지식을 습득할 수 있습니다.  
  
## <a name="BKMK_TechOverview"></a>기술 개요  
  
### <a name="what-you-should-know-before-you-begin"></a>시작하기 전에 알아야 할 사항  
이 항목에서는 이전 버전의 Active Directory 디렉터리 서비스를 잘 알고 있는 것으로 가정하므로 목적 및 기능에 대한 기초적인 정보를 제공하지 않습니다. AD DS에 대한 자세한 내용은 아래에 링크된 TechNet 포털 페이지를 참조하세요.  
  
-   [Active Directory Domain Services Windows Server 2008 R2](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
  
-   [Windows Server 2008에 대 한 Active Directory Domain Services](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
  
-   [Windows Server 기술 참조](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
  
### <a name="functional-descriptions"></a>기능 설명  
  
#### <a name="ad-ds-role-installation"></a>AD DS 역할 설치  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_SelectServerRoles.gif)  
  
Active Directory Domain Services 설치에는 Windows Server 2012의 다른 모든 서버 역할 및 기능과 마찬가지로 서버 관리자 및 Windows PowerShell이 사용됩니다. Dcpromo.exe 프로그램에서는 더 이상 GUI 구성 옵션을 제공하지 않습니다.  
  
로컬 설치와 원격 설치 모두에 서버 관리자의 그래픽 마법사 또는 Windows PowerShell용 ServerManager 모듈을 사용합니다. 이러한 마법사 또는 cmdlet의 여러 인스턴스를 실행하고 다양한 서버를 대상으로 지정하여 단일 콘솔에서 여러 도메인 컨트롤러에 AD DS를 동시에 배포할 수 있습니다. 이러한 새 기능은 Windows Server 2008 R2 이하의 이전 운영 체제와 호환되지 않지만, 이전의 명령줄에서 로컬 역할을 설치하는 데에는 Windows Server 2008 R2에 도입된 Dism.exe 응용 프로그램을 계속 사용할 수 있습니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSAddWindowsFeature.png)  
  
#### <a name="ad-ds-role-configuration"></a>AD DS 역할 구성  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
Active Directory 도메인 서비스 구성 "이전의 DCPROMO"이 이제 역할 설치와에서 별도 작업입니다. AD DS 역할을 설치한 후 관리자가 서버 관리자 내 별도의 마법사를 사용하거나 ADDSDeployment Windows PowerShell 모듈을 사용하여 서버를 도메인 컨트롤러로 구성합니다.  
  
AD DS 역할 구성은 12년간의 현장 경험을 바탕으로 하며, 이제 가장 최근 Microsoft 모범 사례에 따라 도메인 컨트롤러를 구성합니다. 예를 들어 DNS(Domain Name System) 및 글로벌 카탈로그가 모든 도메인 컨트롤러에 기본적으로 설치됩니다.  
  
서버 관리자 AD DS 구성 마법사는 많은 개별 대화 상자를 소수의 프롬프트로 병합 하 고 더 이상 "고급" 모드로 설정을 숨깁니다. 전체 수준 올리기 프로세스가 설치 중 하나의 확장 대화 상자에서 수행됩니다. 마법사와 ADDSDeployment Windows PowerShell 모듈에서는 추가 정보에 대한 링크와 함께 중요한 변경 내용 및 보안 문제를 보여 줍니다.  
  
Dcpromo.exe는 명령줄 무인 설치용으로만 Windows Server 2012에서 지원되며, 더 이상 그래픽 설치 마법사를 실행하지 않습니다. 그러나 무인 설치에 Dcpromo.exe를 사용하지 말고 대신 ADDSDeployment 모듈을 사용하는 것이 좋습니다. 더 이상 사용되지 않는 실행 파일이 다음 버전의 Windows에는 포함되지 않을 것이기 때문입니다.  
  
이러한 새 기능은 Windows Server 2008 R2 이하의 이전 운영 체제와 호환되지 않습니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSForest.png)  
  
> [!IMPORTANT]
> Dcpromo.exe는 더 이상 그래픽 마법사를 제공하지 않으며, 역할 또는 기능 이진 파일을 더 이상 설치하지 않습니다. Explorer 셸에서 Dcpromo.exe를 실행하려고 하면 다음 오류가 반환됩니다.  
> 
> "Active Directory 도메인 서비스 설치 마법사는 서버 관리자에서 재배치 됩니다. 자세한 내용은 <https://go.microsoft.com/fwlink/?LinkId=220921>을 참조 하세요.  
> 
> Dcpromo.exe /unattend를 실행할 경우 여전히 이진 파일이 설치되지만 이전 운영 체제와 마찬가지로 다음 경고가 발생합니다.  
> 
> "Dcpromo 무인된 작업이 Windows PowerShell 용 ADDSDeployment 모듈에 의해 대체 됩니다. 자세한 내용은 <https://go.microsoft.com/fwlink/?LinkId=220924>을 참조 하세요.  
> 
> dcpromo.exe는 Windows Server 2012에서 더 이상 사용되지 않으며, 앞으로의 Windows 버전에 포함되지 않는 것은 물론 이 운영 체제에서도 더 이상 기능이 개선되지 않습니다. 관리자는 dcpromo.exe의 사용을 중단해야 하며, 명령줄에서 도메인 컨트롤러를 만들려는 경우 지원되는 Windows PowerShell 모듈로 전환해야 합니다.  
  
#### <a name="prerequisite-checking"></a>필수 구성 요소 확인  
도메인 컨트롤러 구성에서는 도메인 컨트롤러 수준 올리기를 계속 진행하기 전에 포리스트 및 도메인을 평가하는 필수 구성 요소 확인 단계도 구현합니다. 여기에는 FSMO 역할 가용성, 사용자 권한, 확장된 스키마 호환성 및 기타 요구 사항이 포함됩니다. 이 새로운 디자인은 도메인 컨트롤러 수준 올리기가 시작된 다음 심각한 구성 오류로 인해 도중에 중단되는 문제를 완화합니다. 따라서 포리스트에서 도메인 컨트롤러 메타데이터가 분리되거나 서버가 도메인 컨트롤러로 잘못 인식될 가능성이 줄어듭니다.  
  
## <a name="BKMK_SMForest"></a>서버 관리자를 사용 하 여 포리스트 배포  
이 섹션에서는 그래픽 Windows Server 2012 컴퓨터에서 서버 관리자를 사용하여 포리스트 루트 도메인에 첫 번째 도메인 컨트롤러를 설치하는 방법에 대해 설명합니다.  
  
### <a name="server-manager-ad-ds-role-installation-process"></a>서버 관리자 AD DS 역할 설치 프로세스  
아래의 다이어그램에서는 ServerManager.exe를 실행한 후 도메인 컨트롤러의 수준을 올리기 바로 전까지의 Active Directory 도메인 서비스 역할 설치 프로세스를 보여 줍니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment.png)  
  
#### <a name="server-pool-and-add-roles"></a>서버 풀 및 역할 추가  
서버 관리자를 실행하는 컴퓨터에서 액세스할 수 있는 모든 Windows Server 2012 컴퓨터를 풀링할 수 있습니다. 풀링한 후에는 서버 관리자 내의 사용 가능한 다른 구성 옵션이나 AD DS의 원격 설치를 위해 이 서버를 선택할 수 있습니다.  
  
서버를 추가하려면 다음 중 하나를 선택합니다.  
  
-   대시보드 시작 타일에서 **관리할 다른 서버 추가** 클릭  
  
-   **관리** 메뉴를 클릭하고 **서버 추가** 선택  
  
-   **모든 서버** 를 마우스 오른쪽 단추로 클릭하고 **서버 추가**선택  
  
그러면 서버 추가 대화 상자가 표시됩니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddServers.png)  
  
이 대화 상자에서 사용하거나 그룹화할 서버를 다음 세 가지 방법으로 풀에 추가할 수 있습니다.  
  
-   Active Directory 검색(LDAP를 사용함, 컴퓨터가 도메인에 속해 있어야 함, 운영 체제 필터링을 허용함, 와일드카드를 지원함)  
  
-   DNS 검색(ARP나 NetBIOS 브로드캐스트 또는 WINS 조회를 통해 DNS 별칭 또는 IP 주소 사용, 운영 체제 필터링을 허용하거나 와일드카드를 지원하지 않음)  
  
-   가져오기(CR/LF로 구분된 서버의 텍스트 파일 목록 사용)  
  
**지금 찾기**를 클릭하여 컴퓨터가 가입된 동일한 Active Directory 도메인에서 서버 목록을 가져온 후 이 목록에서 하나 이상의 서버 이름을 클릭합니다. 오른쪽 화살표를 클릭하여 서버를 **선택됨** 목록에 추가합니다. 선택한 서버를 대시보드 역할 그룹에 추가하려면 **서버 추가** 를 사용합니다. 또는 **관리**를 클릭한 다음 **서버 그룹 만들기**를 클릭하거나, **서버 관리자 시작** 대시보드 타일에서 **서버 그룹 만들기**를 클릭하여 사용자 지정 서버 그룹을 만듭니다.  
  
> [!NOTE]  
> 서버 추가 절차에서는 서버가 온라인 상태인지 또는 액세스 가능한지 확인하지 않습니다. 그러나 다음 새로 고침 시 서버 관리자의 관리 효율성 보기에 연결할 수 없는 모든 서버에 대한 플래그가 지정됩니다.  
  
아래 그림과 같이 풀에 추가된 모든 Windows Server 2012 컴퓨터에 원격으로 역할을 설치할 수 있습니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/tADDS_SMI_TR_AddRolesFeatures.png)  
  
Windows Server 2012 이전 운영 체제를 실행하는 서버는 완전하게 관리할 수 없습니다. **역할 및 기능 추가** 선택에서는 ServerManager Windows PowerShell 모듈 **Install-WindowsFeature**를 실행합니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddADDSToAnotherServer.png)  
  
또한 기존 도메인 컨트롤러의 서버 관리자 대시보드에서 AD DS 대시보드 타일을 마우스 오른쪽 단추로 클릭하고 **다른 서버에 AD DS 추가**를 선택하여 이미 미리 선택된 역할과 함께 원격 서버 AD DS 설치를 선택할 수 있습니다. 그러면 **Install-WindowsFeature AD-Domain-Services**가 호출됩니다.  
  
컴퓨터가 풀 자체에서 서버 관리자를 자동으로 실행하기 때문에 여기에 AD DS 역할을 설치하려면 **관리** 메뉴를 클릭한 다음 **역할 및 기능 추가**를 클릭하기만 하면 됩니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ManageAddRoles.png)  
  
#### <a name="installation-type"></a>설치 유형  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectInstallationType.png)  
  
**설치 유형** 대화 상자에서는 Active Directory 도메인 서비스를 지원하지 않는 **원격 데스크톱 서비스 시나리오 기반 설치**옵션을 제공합니다. 이 옵션은 다중 서버 분산 작업에서 원격 데스크톱 서비스만 허용합니다. 이 옵션을 선택한 경우에는 AD DS를 설치할 수 없습니다.  
  
따라서 AD DS를 설치할 때는 항상 기본적으로 선택되어 있는 **역할 기반 또는 기능 기반 설치**를 그대로 두세요.  
  
#### <a name="server-selection"></a>서버 선택  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectDestinationServer.png)  
  
**서버 선택** 대화 상자에서는 이전에 풀에 추가한 서버 중 하나를 선택할 수 있습니다(액세스 가능한 경우). 서버 관리자를 실행하는 로컬 서버는 자동으로 사용할 수 있습니다.  
  
또한 Windows Server 2012 운영 체제에서 오프라인 Hyper-V VHD 파일을 선택할 수 있습니다. 그러면 서버 관리자에서 구성 요소 서비스를 통해 이러한 파일에 역할을 직접 추가합니다. 이렇게 하면 추가로 구성하기 전에 필요한 구성 요소를 가상 서버에 프로비전할 수 있습니다.  
  
#### <a name="server-roles-and-features"></a>서버 역할 및 기능  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectServerRoles.png)  
  
도메인 카탈로그의 수준을 올리려면 **Active Directory Domain Services** 역할을 선택합니다. 그러면 모든 Active Directory 관리 기능 및 필요한 서비스가 자동으로 설치되며, 이는 해당 기능 및 서비스가 표면적으로 다른 역할의 일부이거나 서버 관리자 인터페이스에 선택된 것으로 표시되지 않은 경우에도 마찬가지입니다.  
  
서버 관리자에서는 이 역할에서 암시적으로 설치하는 관리 기능이 표시된 정보 대화 상자도 제공합니다. 이는 **-IncludeManagementTools** 인수에 상응합니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddFeaturesDialog.gif)  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_SelectFeatures.png)  
  
여기에서 추가 **기능** 을 원하는 대로 추가할 수 있습니다.  
  
#### <a name="active-directory-domain-services"></a>Active Directory 도메인 서비스  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSIntro.png)  
  
**Active Directory Domain Services** 대화 상자에서는 요구 사항 및 모범 사례에 대한 제한된 정보를 제공합니다. 주로 역할을 하며 AD DS 역할을 선택 했음을 확인 "이이 화면이 표시 되지 않으면, 선택 하지 않은 AD DS 합니다.  
  
#### <a name="confirmation"></a>확인  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Confirmation.png)  
  
**확인** 대화 상자는 역할 설치를 시작하기 전의 마지막 검사점입니다. 이 대화 상자에서는 역할 설치 후 필요에 따라 컴퓨터를 다시 시작할 수 있는 옵션을 제공하지만 AD DS 설치에는 다시 부팅이 필요하지 않습니다.  
  
역할 설치를 시작할 준비가 완료되었으면 **설치**를 클릭하여 확인합니다. 역할 설치를 시작한 후에는 취소할 수 없습니다.  
  
#### <a name="results"></a>결과  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Results.png)  
  
**결과** 대화 상자에는 현재 설치 진행률 및 현재 설치 상태가 표시됩니다. 서버 관리자를 닫아도 역할 설치는 계속됩니다.  
  
설치 결과를 확인하는 것은 여전히 모범 사례 중 하나입니다. 설치가 완료되기 전에 **결과** 대화 상자를 닫은 경우 서버 관리자 알림 플래그를 사용하여 결과를 확인할 수 있습니다. AD DS 역할을 설치했지만 도메인 컨트롤러로 추가 구성하지 않은 서버에 대한 경고 메시지도 서버 관리자에 표시됩니다.  
  
**작업 알림**  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskNotofications.png)  
  
**AD DS 세부 정보**  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ADDSDetails.png)  
  
**작업 세부 정보**  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_TaskDetails.png)  
  
#### <a name="promote-to-domain-controller"></a>도메인 컨트롤러로 수준 올리기  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_Promote.png)  
  
AD DS 역할 설치가 끝나면 **이 서버를 도메인 컨트롤러로 승격** 링크를 사용하여 구성을 계속할 수 있습니다. 이 구성은 서버를 도메인 컨트롤러로 지정하는 데 필요하지만 구성 마법사를 즉시 실행해야 하는 것은 아닙니다. 예를 들어 나중에 구성할 수 있도록 다른 지점으로 보내기 전에 AD DS 이진 파일을 서버에 프로비전하기만 할 수도 있습니다. 배송 전에 AD DS 역할을 추가하면 목적지에 도착한 후 시간이 절약됩니다. 도메인 컨트롤러를 며칠 또는 몇 주간 오프라인 상태로 두지 않는 것이 좋습니다. 끝으로 이 방법을 사용하면 도메인 컨트롤러의 수준을 올리기 전에 구성 요소를 업데이트할 수 있으므로 이후에 다시 부팅해야 하는 횟수를 한 번 이상 생략할 수 있습니다.  
  
나중에 이 링크를 선택하면 ADDSDeployment cmdlet **install-addsforest**, **install-addsdomain**또는 **install-addsdomaincontroller**가 호출됩니다.  
  
### <a name="uninstallingdisabling"></a>제거/사용 안 함  
서버의 수준을 도메인 컨트롤러로 올렸는지 여부에 상관없이, 다른 모든 역할과 마찬가지로 AD DS 역할을 제거할 수 있습니다. 그러나 AD DS 역할을 제거한 경우 작업이 완료되면 다시 시작해야 합니다.  
  
Active Directory 도메인 서비스 역할 제거는 도메인 컨트롤러의 수준을 내려야 완료된다는 점에서 설치와 다릅니다. 이는 포리스트의 적절한 메타데이터 정리 없이 도메인 컨트롤러에서 해당 역할 이진 파일을 제거하지 못하도록 하기 위해 필요합니다. 자세한 내용은 참조 [도메인 컨트롤러 수준 내리기 및 도메인 & #40; 200 수준 & #41;](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)합니다.  
  
> [!WARNING]  
> 도메인 컨트롤러로 수준을 올린 후 Dism.exe 또는 Windows PowerShell DISM 모듈을 사용하여 AD DS 역할을 제거하는 작업은 지원되지 않으며, 이 작업을 수행할 경우 서버가 정상적으로 부팅되지 않습니다.  
>   
> 서버 관리자 또는 Windows PowerShell용 AD DS 배포 모듈과 달리 DISM은 AD DS 또는 해당 구성에 대한 내재된 지식이 없는 기본 서비스 시스템입니다. 서버가 더 이상 도메인 컨트롤러가 아닌 경우 외에는 Dism.exe 또는 Windows PowerShell DISM 모듈을 사용하여 AD DS 역할을 제거하지 마세요.  
  
### <a name="create-an-ad-ds-forest-root-domain-with-server-manager"></a>서버 관리자를 사용하여 AD DS 포리스트 루트 도메인 만들기  
다음 다이어그램에서는 이전에 AD DS 역할을 설치하고 서버 관리자를 사용하여 **Active Directory 도메인 서비스 구성 마법사** 를 시작한 경우의 Active Directory 도메인 서비스 구성 프로세스를 보여 줍니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_forestdeploy2.png)  
  
#### <a name="deployment-configuration"></a>배포 구성  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_AddNewForest.png)  
  
서버 관리자는 **배포 구성** 페이지에서 모든 도메인 컨트롤러 수준 올리기를 시작합니다. 선택한 배포 작업에 따라 이 페이지 및 다음 페이지에 표시되는 나머지 옵션 및 필수 필드가 바뀝니다.  
  
새 Active Directory 포리스트를 만들려면 **새 포리스트 추가**를 클릭합니다. 올바른 루트 도메인 이름을 제공해야 합니다. 이름에 단일 레이블을 지정할 수 없으며(예: 이름은 *contoso*가 아니라 *contoso.com* 또는 이와 유사해야 함), 허용된 DNS 도메인 명명 요구 사항을 사용해야 합니다.  
  
올바른 도메인 이름에 대한 자세한 내용은 기술 자료 문서, [컴퓨터, 도메인, 사이트 및 OU에 대한 Active Directory의 명명 규칙](https://support.microsoft.com/kb/909264)을 참조하세요.  
  
> [!WARNING]  
> 외부 DNS 이름과 동일한 이름으로 새 Active Directory 포리스트를 만들지 마세요. 예를 들어 인터넷 DNS URL이 http://contoso.com 인 경우 향후 호환성 문제를 방지 하려면 내부 포리스트에 대해 다른 이름을 선택 해야 합니다. 내부 포리스트 이름은 웹 트래픽에 대해 고유하고 제공될 가능성이 없는 이름이어야 합니다(예: corp.contoso.com).  
  
새 포리스트에는 도메인의 관리자 계정에 대한 새 자격 증명이 필요하지 않습니다. 도메인 컨트롤러 수준 올리기 프로세스에서는 포리스트 루트를 만드는 데 사용된 첫 번째 도메인 컨트롤러의 기본 제공 관리자 계정에 대한 자격 증명을 사용합니다. 기본 제공 관리자 계정을 사용하지 않도록 설정하거나 잠글 수 있는 방법은 기본적으로 없습니다. 이는 다른 관리 도메인 계정을 사용할 수 없는 경우 포리스트의 유일한 진입점일 수 있기 때문입니다. 새 포리스트를 배포하기 전에 암호를 알아야 합니다.  
  
**DomainName** 은 필수 항목이며, 올바른 정규화된 도메인 DNS 이름이 필요합니다.  
  
#### <a name="domain-controller-options"></a>도메인 컨트롤러 옵션  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_DCOptions_Forest.gif)  
  
**도메인 컨트롤러 옵션**을 사용하여 새 포리스트 루트 도메인에 대해 **포리스트 기능 수준** 및 **도메인 기능 수준**을 구성할 수 있습니다. 기본적으로 이러한 설정은 새 포리스트 루트 도메인에서 Windows Server 2012입니다. Windows Server 2012 포리스트 기능 수준을 Windows Server 2008 R2 포리스트 기능 수준을 통해 모든 새 기능을 제공 하지 않습니다. Windows Server 2012 도메인 기능 수준이 새로운 Kerberos 설정인을 구현 하는 데에 필요는 "항상 클레임 제공" 및 "아머 링 되지 않은 인증 요청 실패 합니다." Windows Server 2012의 기능 수준에 대 한 기본 사용 허용 되는 최소 운영 체제 요구 사항을 충족 하는 도메인에 도메인 컨트롤러의 참여를 제한 하는 것입니다. 즉, Windows Server 2012 도메인 기능 수준 유일한 도메인 컨트롤러가 Windows Server 2012를 실행 하는 도메인을 호스트할 수를 지정할 수 있습니다.  이라는 새 도메인 컨트롤러 플래그를 구현 하는 Windows Server 2012 **DS_WIN8_REQUIRED** 에 **DSGetDcName** Windows Server 2012 도메인 컨트롤러는 NetLogon의 기능입니다. 이는 도메인 컨트롤러에서 실행할 수 있는 운영 체제 면에서 동종 또는 이기종 포리스트의 유연성을 더해 줍니다.  
  
도메인 컨트롤러 위치에 대 한 자세한 내용은 [디렉터리 서비스 기능](https://msdn.microsoft.com/library/ms675900(VS.85).aspx)을 검토 하십시오.  
  
구성 가능한 도메인 컨트롤러 기능은 DNS 서버 옵션뿐입니다. 분산된 환경의 고가용성을 위해 모든 도메인 컨트롤러에서 DNS 서비스를 제공하는 것이 좋습니다. 이러한 이유 때문에 어떤 모드 또는 도메인에서 도메인 컨트롤러를 설치하든 이 옵션이 기본적으로 선택되어 있습니다. 글로벌 카탈로그 및 읽기 전용 도메인 컨트롤러 옵션은 새 포리스트 루트 도메인을 만들 때 사용할 수 없습니다. 첫 번째 도메인 컨트롤러는 GC여야 하며 RODC(읽기 전용 도메인 컨트롤러)일 수 없기 때문입니다.  
  
지정한 **디렉터리 서비스 복원 모드 암호**는 서버에 적용된 암호 정책을 준수해야 하는데, 이 정책에서는 기본적으로 강력한 암호를 요구하지 않으며 빈 암호만 아니면 됩니다. 항상 강력하고 복잡한 암호 또는 암호 문구를 선택하십시오.  
  
#### <a name="dns-options-and-dns-delegation-credentials"></a>DNS 옵션 및 DNS 위임 자격 증명  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestDNSOptions.png)  
  
**DNS 옵션** 페이지에서는 DNS 위임을 구성하고 대체 DNS 관리 자격 증명을 제공할 수 있습니다.  
  
**도메인 컨트롤러 옵션** 페이지에서 **DNS 서버**를 선택하여 새 Active Directory 포리스트 루트 도메인을 설치할 때는 Active Directory 도메인 서비스 구성 마법사에서 DNS 옵션 또는 위임을 구성할 수 없습니다. **DNS 위임 만들기** 옵션은 기존 DNS 서버 인프라에 새 포리스트 루트 DNS 영역을 만들 때 사용할 수 있습니다. 이 옵션을 사용하면 DNS 영역을 업데이트할 권한이 있는 대체 DNS 관리 자격 증명을 제공할 수 있습니다.  
  
DNS 위임을 업데이트해야 하는지 여부에 대한 자세한 내용은 [영역 위임 이해](https://technet.microsoft.com/library/cc771640.aspx)를 참조하세요.  
  
#### <a name="additional-options"></a>추가 옵션  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestAdditionalOptions.png)  
  
**추가 옵션** 페이지에는 도메인의 NetBIOS 이름이 표시되며 이를 재정의할 수 있습니다. 기본적으로 NetBIOS 도메인 이름은 **배포 구성** 페이지에 제공된 정규화된 도메인 이름의 맨 왼쪽 레이블과 일치합니다. 예를 들어 corp.contoso.com의 정규화된 도메인 이름을 제공한 경우 기본 NetBIOS 도메인 이름은 CORP입니다.  
  
이름이 15자 이하이고 다른 NetBIOS 이름과 충돌하지 않으면 변경되지 않습니다. 반면, 다른 NetBIOS 이름과 충돌하면 이름에 숫자가 추가됩니다. 이름이 15자를 넘으면 마법사에서 잘린 고유 이름을 제안합니다. 두 경우 모두 마법사에서 WINS 조회 및 NetBIOS 브로드캐스트를 통해 해당 이름이 이미 사용 중이지 않은지 먼저 확인합니다.  
  
올바른 도메인 이름에 대한 자세한 내용은 기술 자료 문서, [컴퓨터, 도메인, 사이트 및 OU에 대한 Active Directory의 명명 규칙](https://support.microsoft.com/kb/909264)을 참조하세요.  
  
#### <a name="paths"></a>경로  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPaths.png)  
  
**경로** 페이지에서 AD DS 데이터베이스, 데이터베이스 트랜잭션 로그 및 SYSVOL 공유의 기본 폴더 위치를 재정의할 수 있습니다. 기본 위치는 항상 %systemroot%의 하위 디렉터리(예: C:\Windows)입니다.  
  
#### <a name="review-options-and-view-script"></a>옵션 검토 및 스크립트 보기  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestReviewOptions.png)  
  
**옵션 검토** 페이지에서 설치를 시작하기 전에 설정을 확인하고 이러한 설정이 요구 사항을 충족하는지도 확인할 수 있습니다. 이것이 서버 관리자를 사용할 때 설치를 중지할 수 있는 마지막 기회는 아닙니다. 구성을 계속하기 전에 설정을 확인하는 옵션일 뿐입니다.  
  
서버 관리자의 **옵션 검토** 페이지는 현재 ADDSDeployment 구성을 단일 Windows PowerShell 스크립트로 포함하는 유니코드 텍스트 파일을 만들 수 있도록 **스크립트 보기** 단추(선택 사항)도 제공합니다. 이 단추를 통해 서버 관리자 그래픽 인터페이스를 Windows PowerShell 배포 스튜디오로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용하여 옵션을 구성하고 구성을 내보낸 다음 마법사를 취소합니다. 이 프로세스를 통해 향후 수정을 위해 사용하거나 직접 사용하기 위한 유효하고 구문상으로 정확한 샘플이 만들어집니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
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
> 서버 관리자는 수준을 올릴 때 일반적으로 모든 인수의 값을 채우며 기본값에 의존하지 않습니다. 기본값은 향후 버전의 Windows 또는 서비스 팩 간에 변경될 수 있기 때문입니다. 단, **-safemodeadministratorpassword** 인수(스크립트에서 의도적으로 생략됨)는 예외입니다. 확인 프롬프트를 강제로 표시하려면 대화형으로 cmdlet을 실행할 때 이 값을 생략합니다.  
  
#### <a name="prerequisites-check"></a>필수 구성 요소 확인  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestPrereqCheck.png)  
  
**필수 구성 요소 확인**은 AD DS 도메인 구성의 새로운 기능입니다. 이 새 단계에서는 서버 구성이 새 AD DS 포리스트를 지원할 수 있는지 확인합니다.  
  
새 포리스트 루트 도메인을 설치할 때 서버 관리자 Active Directory 도메인 서비스 구성 마법사는 일련의 모듈식 테스트를 호출합니다. 이러한 테스트에서는 제안된 복구 옵션을 알려 줍니다. 필요한 만큼 여러 번 테스트를 실행할 수 있습니다. 모든 필수 구성 요소 테스트를 통과해야만 도메인 컨트롤러 프로세스를 계속 진행할 수 있습니다.  
  
**필수 구성 요소 확인**에서는 이전 운영 체제에 영향을 주는 보안 변경 내용과 같은 관련 정보도 제공합니다.  
  
특정 필수 구성 요소 검사에 대 한 자세한 내용은 참조 하십시오. [필수 구성 요소 확인](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)합니다.  
  
#### <a name="installation"></a>설치  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestInstallation.png)  
  
**설치** 페이지가 표시되면 도메인 컨트롤러 구성이 시작되며 이는 중지하거나 취소할 수 없습니다. 세부 작업이 이 페이지에 표시되고 다음 로그에 기록됩니다.  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
> [!NOTE]  
> 동일한 서버 관리자 콘솔에서 여러 역할 설치 및 AD DS 구성 마법사를 동시에 실행할 수 있습니다.  
  
#### <a name="results"></a>결과  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**결과** 페이지에는 수준 올리기의 성공 또는 실패와 중요한 관리 정보가 표시됩니다. 10초 후 도메인 컨트롤러가 자동으로 다시 부팅됩니다.  
  
## <a name="BKMK_PSForest"></a>Windows PowerShell을 사용 하 여 포리스트 배포  
이 섹션에서는 핵심 Windows Server 2012 컴퓨터에서 Windows PowerShell을 사용하여 포리스트 루트 도메인에 첫 번째 도메인 컨트롤러를 설치하는 방법에 대해 설명합니다.  
  
### <a name="windows-powershell-ad-ds-role-installation-process"></a>Windows PowerShell AD DS 역할 설치 프로세스  
몇 가지 간단한 서버 관리자 배포 cmdlet을 배포 프로세스에 구현하여 AD DS 간소화된 관리의 비전을 더욱 확고하게 실현할 수 있습니다.  
  
다음 그림에서는 **PowerShell.exe**를 실행한 후 도메인 컨트롤러의 수준을 올리기 바로 전까지의 Active Directory Domain Services 역할 설치 프로세스를 보여 줍니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/adds_servermanagerdeployment_powershell.png)  
  
|||  
|-|-|  
|ServerManager Cmdlet|인수(**굵게** 표시된 인수는 필수 항목이며, *기울임꼴* 인수는 Windows PowerShell 또는 AD DS 구성 마법사를 사용하여 지정할 수 있음)|  
|Install-WindowsFeature/Add-WindowsFeature|***-Name***<br /><br />*-Restart*<br /><br />*-IncludeAllSubFeature*<br /><br />*-IncludeManagementTools*<br /><br />-Source<br /><br />*-ComputerName*<br /><br />-Credential<br /><br />-LogPath<br /><br />*-Vhd*<br /><br />*-ConfigurationFilePath*|  
  
> [!NOTE]  
> **-IncludeManagementTools** 인수는 필수는 아니지만 AD DS 역할 파일을 설치할 때 매우 권장됩니다.  
  
서버 관리자 모듈은 Windows PowerShell용 새 DISM 모듈의 역할 설치, 상태 및 제거 부분을 노출합니다. 이렇게 계층화하면 대부분의 작업이 간소화되며, 강력한(그러나 잘못 사용할 경우 위험한) DISM 모듈을 직접 사용해야 할 필요성이 줄어듭니다.  
  
**Get-Command**를 사용하여 서버 관리자에서 별칭 및 cmdlet을 내보낼 수 있습니다.  
  
```powershell  
Get-Command -module ServerManager  
```  
  
예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetCommand.png)  
  
Active Directory 도메인 서비스 역할을 추가하려면 AD DS 역할 이름을 인수로 사용하여 **Install-WindowsFeature** 를 실행하기만 하면 됩니다. 서버 관리자와 마찬가지로 AD DS 역할에 암시적인 모든 필수 서비스도 자동으로 설치됩니다.  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services  
```  
  
AD DS 관리 도구도 함께 설치(매우 권장됨)하려면 **-IncludeManagementTools** 인수를 제공합니다.  
  
```powershell  
Install-WindowsFeature -name AD-Domain-Services -IncludeManagementTools  
```  
  
예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallWinFeature.png)  
  
모든 기능 및 역할을 해당 설치 상태와 함께 나열하려면 인수 없이 **Get-WindowsFeature** 를 사용합니다. 원격 서버에서 설치 상태를 보려면 **-ComputerName** 인수를 지정합니다.  
  
```powershell  
Get-WindowsFeature  
```  
  
**Get-WindowsFeature** 에는 필터링 메커니즘이 없으므로 특정 기능을 찾으려면 파이프라인과 함께 **Where-Object** 를 사용해야 합니다. 파이프라인은 여러 cmdlet 간에 데이터를 전달하는 데 사용되는 채널이며 Where-Object cmdlet은 필터 역할을 합니다. 기본 제공 **$_** 변수는 현재 파이프라인을 통과하는 개체 역할을 하며, 속성을 포함할 수 있습니다.  
  
```powershell  
Get-WindowsFeature | where-object <options>  
```  
  
예를 들어 **표시 이름** 속성에 "Active Dir"이 포함된 모든 기능을 찾으려면 다음을 사용합니다.  
  
```powershell  
Get-WindowsFeature | where displayname -like "*active dir*"  
```  
  
아래에 추가 예가 나와 있습니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSGetWindowsFeature.png)  
  
파이프라인 및 Where-Object를 사용하는 다양한 Windows PowerShell 작업에 대한 자세한 내용은 [Windows PowerShell의 파이프 및 파이프라인](https://technet.microsoft.com/library/ee176927.aspx)을 참조하세요.  
  
Windows PowerShell 3.0에서는 이 파이프라인 작업에 필요한 명령줄 인수가 크게 간소화되었습니다. Windows PowerShell 2.0에서는 다음이 필요했습니다.  
  
```powershell  
Get-WindowsFeature | where {$_.displayname - like "*active dir*"}  
```  
  
Windows PowerShell 파이프라인을 사용하면 읽을 수 있는 형식의 결과를 만들 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```powershell  
Install-WindowsFeature | Format-List  
Install-WindowsFeature | select-object | Format-List  
  
```  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDS.png)  
  
**-expandproperty** 인수와 함께 **Select-Object** cmdlet을 사용하면 다음과 같은 흥미로운 데이터가 반환됩니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallADDSWithTools.png)  
  
> [!NOTE]  
> **Select-Object -expandproperty** 인수를 사용하면 전체 설치 성능이 약간 느려집니다.  
  
### <a name="BKMK_PS"></a>Windows PowerShell을 사용 하 여 AD DS 포리스트 루트 도메인 만들기  
ADDSDeployment 모듈을 사용하여 새 Active Directory 포리스트를 설치하려면 다음 cmdlet을 사용합니다.  
  
```powershell  
Install-addsforest  
```  
  
**Install-AddsForest** cmdlet은 두 단계(필수 구성 요소 확인 및 설치)만 수행합니다. 아래 두 그림에는 최소 필수 인수인 **-domainname**을 사용한 설치 단계가 나와 있습니다.  
  
|||  
|-|-|  
|ADDSDeployment Cmdlet|인수(**굵게** 표시된 인수는 필수 항목이며, *기울임꼴* 인수는 Windows PowerShell 또는 AD DS 구성 마법사를 사용하여 지정할 수 있음)|  
|install-addsforest|-Confirm<br /><br />*-CreateDNSDelegation*<br /><br />*-DatabasePath*<br /><br />*-DomainMode*<br /><br />***-DomainName***<br /><br />***-DomainNetBIOSName***<br /><br />*-DNSDelegationCredential*<br /><br />*-ForestMode*<br /><br />-Force<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-NoDnsOnNetwork<br /><br />-NoRebootOnCompletion<br /><br />*-SafeModeAdministratorPassword*<br /><br />-SkipAutoConfigureDNS<br /><br />-SkipPreChecks<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> DNS 도메인 이름 접두사를 바탕으로 자동으로 생성된 15자 이름을 변경하기를 원하거나 이름이 15자를 초과하는 경우 **-DomainNetBIOSName** 인수가 필요합니다.  
  
상응하는 서버 관리자 **배포 구성** ADDSDeployment cmdlet 및 인수는 다음과 같습니다.  
  
```powershell  
Install-ADDSForest  
-DomainName <string>  
```  
  
상응하는 서버 관리자 도메인 컨트롤러 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```powershell  
-ForestMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-InstallDNS <{$false | $true}>  
-SafeModeAdministratorPassword <secure string>  
  
```  
  
**Install-ADDSForest** 인수는 서버 관리자와 동일한 기본값을 따릅니다(지정하지 않은 경우).  
  
**SafeModeAdministratorPassword** 인수의 작업은 특별합니다.  
  
-   인수로 *지정하지 않을 경우* cmdlet은 마스킹된 암호를 입력 및 확인하라는 메시지를 표시합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법입니다.  
  
    예를 들어 corp.contoso.com이라는 새 포리스트를 만들고 마스킹된 암호를 입력하고 확인하라는 메시지를 표시하려면 다음 명령을 실행합니다.  
  
    ```powershell  
    Install-ADDSForest "DomainName corp.contoso.com  
    ```  
  
-   *값과 함께* 지정한 경우 값은 보안 문자열이어야 합니다. cmdlet을 대화형으로 실행할 경우 기본 설정된 사용법이 아닙니다.  
  
예를 들어 **Read-Host** cmdlet을 사용하여 수동으로 암호를 물어 사용자에게 보안 문자열을 물을 수 있습니다.  
  
```powershell  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> 이전 옵션이 암호를 확인하지 않으므로 각별히 주의해야 합니다. 암호는 표시되지 않습니다.  
  
변환된 일반 텍스트 변수로 보안 문자열을 제공할 수도 있습니다(권장되지 않음).  
  
```powershell  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
마지막으로 난독 처리된 암호를 파일에 저장한 다음 일반 텍스트 암호를 표시하지 않고 나중에 다시 사용할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```powershell  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> 일반 또는 난독 처리된 텍스트 암호는 제공하거나 저장하지 않는 것이 좋습니다. 스크립트에서 이 명령을 실행하는 사용자나 어깨 너머로 보고 있는 다른 사용자가 해당 도메인 컨트롤러의 DSRM 암호를 알게 될 수 있습니다. 파일에 액세스할 수 있는 모든 사람이 난독 처리된 암호를 반전시킬 수 있습니다. 이 정보를 알면 DSRM에서 시작된 DC에 로그온하여 도메인 컨트롤러 자체를 가장함으로써 Active Directory 포리스트에서 가장 높은 수준으로 해당 권한을 상승시킬 수 있습니다. **System.Security.Cryptography**를 사용하여 텍스트 파일 데이터를 암호화하는 추가 단계를 수행하는 것이 좋지만 이러한 단계는 이 문서의 범위를 벗어납니다. 암호 저장을 완전히 피하는 것이 가장 좋습니다.  
  
ADDSDeployment cmdlet에서는 DNS 클라이언트 설정, 전달자 및 루트 힌트의 자동 구성을 건너뛸 수 있는 추가 옵션을 제공합니다. 서버 관리자를 사용할 때는 이 구성 옵션을 건너뛸 수 없습니다. 이 인수는 도메인 컨트롤러를 구성하기 전에 DNS 서버 역할을 설치한 경우에만 적용됩니다.  
  
```powershell  
-SkipAutoConfigureDNS  
```  
  
**DomainNetBIOSName** 작업도 특별합니다.  
  
-   **DomainNetBIOSName** 인수를 NetBIOS 도메인 이름과 함께 지정하지 않고 **DomainName** 인수의 단일 레이블 접두사 도메인 이름이 15자 이하인 경우 자동으로 생성된 이름으로 수준 올리기가 계속 진행됩니다.  
  
-   **DomainNetBIOSName** 인수를 NetBIOS 도메인 이름과 함께 지정하지 않고 **DomainName** 인수의 단일 레이블 접두사 도메인 이름이 16자 이상인 경우 수준 올리기에 실패합니다.  
  
-   **DomainNetBIOSName** 인수를 15자 이하의 NetBIOS 도메인 이름과 함께 지정한 경우 이 지정한 이름으로 수준 올리기가 계속 진행됩니다.  
  
-   **DomainNetBIOSName** 인수를 16자 이상의 NetBIOS 도메인 이름과 함께 지정한 경우 수준 올리기에 실패합니다.  
  
상응하는 서버 관리자 추가 옵션 ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```powershell  
-domainnetbiosname <string>  
```  
  
상응하는 서버 관리자 **경로** ADDSDeployment cmdlet 인수는 다음과 같습니다.  
  
```powershell  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
  
```  
  
선택적 **Whatif** 인수를 **Install-ADDSForest** cmdlet과 함께 사용하여 구성 정보를 검토합니다. 이를 통해 cmdlet 인수의 명시적 및 암시적 값을 확인할 수 있습니다.  
  
예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSPaths.png)  
  
서버 관리자를 사용할 때는 **필수 구성 요소 확인** 을 무시할 수 없지만 AD DS 배포 cmdlet을 사용할 때는 다음 인수를 사용하여 프로세스를 건너뛸 수 있습니다.  
  
```powershell  
-skipprechecks  
```  
  
> [!WARNING]  
> 필수 구성 요소 확인을 건너뛰면 도메인 컨트롤러 수준 올리기가 부분적으로 완료되거나 AD DS 포리스트가 손상될 수 있으므로 건너뛰지 않는 것이 좋습니다.  
  
서버 관리자와 마찬가지로 **Install-ADDSForest**에서도 수준 올리기 후 서버가 자동으로 다시 부팅됨을 미리 알려 줍니다.  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSReboot.png)  
  
![새 포리스트 설치](media/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-/ADDS_PSInstallProgress.png)  
  
다시 부팅 프롬프트를 자동으로 허용하려면 임의의 ADDSDeployment Windows PowerShell cmdlet에서 **-force** 또는 **-confirm:$false** 인수를 사용합니다. 수준 올리기가 끝난 후 서버가 자동으로 다시 부팅되는 것을 방지하려면 **-norebootoncompletion** 인수를 사용합니다.  
  
> [!WARNING]  
> 다시 부팅을 무시하지 않는 것이 좋습니다. 도메인 컨트롤러가 올바르게 작동하려면 다시 부팅해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
[Active Directory Domain Services (TechNet 포털)](https://technet.microsoft.com/library/cc770946(WS.10).aspx)  
[Active Directory Domain Services Windows Server 2008 R2](https://technet.microsoft.com/library/dd378801(WS.10).aspx)  
[Windows Server 2008에 대 한 Active Directory Domain Services](https://technet.microsoft.com/library/dd378891(WS.10).aspx)  
[Windows Server 기술 참조 (Windows Server 2003)](https://technet.microsoft.com/library/cc739127(WS.10).aspx)  
[ Active Directory 관리 센터: 시작 (Windows Server 2008 R2) ](https://technet.microsoft.com/library/dd560651(WS.10).aspx)  
[Windows PowerShell을 사용 하 여 Active Directory 관리 (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd378937(WS.10).aspx)  
[디렉터리 서비스 팀에 문의 (공식 Microsoft 상용 기술 지원 블로그)](http://blogs.technet.com/b/askds)  
  

