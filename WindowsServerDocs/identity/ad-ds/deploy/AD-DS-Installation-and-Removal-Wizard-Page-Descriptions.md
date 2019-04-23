---
ms.assetid: ac727bd1-a892-47ed-a7ba-439b34187d4e
title: AD DS 설치 및 제거 마법사 페이지 설명
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 52e4b215c406eeae11dbab41e367f6ce4cd83507
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849254"
---
# <a name="ad-ds-installation-and-removal-wizard-page-descriptions"></a>AD DS 설치 및 제거 마법사 페이지 설명

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 서버 관리자에서 AD DS 서버 역할 설치 및 제거를 구성하는 다음과 같은 마법사 페이지의 컨트롤에 대해 설명합니다.  
  
-   [배포 구성](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DepConfigPage)  
  
-   [도메인 컨트롤러 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)  
  
-   [DNS 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)  
  
-   [RODC 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RODCOptionsPage)  
  
-   [추가 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdditionalOptionsPage)  
  
-   [경로](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Paths)  
  
-   [준비 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdprepCreds)  
  
-   [옵션 검토](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ViewInstallOptionsPage)  
  
-   [필수 구성 요소 확인](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_PrerqCheckPage)  
  
-   [결과](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Results)  
  
-   [역할 제거 자격 증명](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalCredsPage)  
  
-   [AD DS 제거 옵션 및 경고](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalOptionsPage)  
  
-   [새 관리자 암호](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_NewAdminPwdPage)  
  
-   [역할 제거 선택 확인](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ConfirmRoleRemovalPage)  
  
## <a name="BKMK_DepConfigPage"></a>배포 구성  
서버 관리자가 모든 도메인 컨트롤러 설치를 시작 하는 **배포 구성** 페이지입니다. 선택한 배포 작업에 따라 이 페이지 및 다음 페이지에 표시되는 나머지 옵션 및 필수 필드가 바뀝니다. 예를 들어, 새 포리스트를 만드는 경우는 **준비 옵션** 기존 포리스트나 도메인에서 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 설치 하는 경우 수행 하지만 페이지가 표시 되지 않습니다.  
  
일부 유효성 검사 테스트가 이 페이지에서 수행되며 이 테스트는 나중에 필수 구성 요소 확인 과정으로 다시 수행됩니다. 예를 들어, 기능 수준이 Windows 2000 포리스트에서 첫 번째 Windows Server 2012 도메인 컨트롤러를 설치 하려고 하면 오류가이 페이지에 나타납니다.  
  
새 포리스트를 만들 경우 다음 옵션이 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
-   새 포리스트를 만들 때 포리스트 루트 도메인의 이름을 지정해야 합니다. 포리스트 루트 도메인 이름을 단일 레이블이 지정 된 일 수 없습니다 (예를 들어 이어야 함 "contoso" 대신 "contoso.com"). 허용된 DNS 도메인 명명 규칙을 사용해야 합니다. IDN(다국어 도메인 이름)을 지정할 수 있습니다. DNS 도메인 명명 규칙에 대 한 자세한 내용은 참조 [KB 909264](https://support.microsoft.com/kb/909264)합니다.  
  
-   외부 DNS 이름과 동일한 이름으로 새 Active Directory 포리스트를 만들지 마십시오. 예를 들어 인터넷 DNS URL이 http://contoso.com, 이후 버전과 호환성 문제를 방지 하려면 내부 포리스트에 대해 다른 이름을 선택 해야 합니다. 내부 포리스트 이름은 웹 트래픽에 대해 고유하고 제공될 가능성이 없는 이름이어야 합니다(예: corp.contoso.com).  
  
-   새 포리스트를 만들 서버에서 관리자그룹의 구성원이어야 합니다.  
  
포리스트를 만드는 방법에 대 한 자세한 내용은 참조 [#40; & 새 Windows Server 2012 Active Directory 포리스트 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)합니다.  
  
새 도메인을 만들 경우 다음 옵션이 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_ChildDomain.gif)  
  
> [!NOTE]  
> 새 트리 도메인을 만드는 경우 부모 도메인 대신 포리스트 루트 도메인의 이름을 지정해야 합니다. 단, 나머지 마법사 페이지 및 옵션은 동일합니다.  
  
-   **선택**을 클릭하여 부모 도메인이나 Active Directory 트리를 검색하거나 유효한 부모 도메인이나 트리 이름을 입력합니다. 다음에 새 도메인의 이름을 입력 **새 도메인 이름을**합니다.  
  
-   트리 도메인: 정규화된 유효한 루트 도메인 이름을 제공합니다. 이름은 단일 레이블로 구성된 이름일 수 없으며, DNS 도메인 이름 요구 사항을 사용해야 합니다.  
  
-   자식 도메인: 단일 레이블로 구성된 유효한 자식 도메인 이름을 제공합니다. 이름은 DNS 도메인 이름 요구 사항을 사용해야 합니다.  
  
-   현재 자격 증명이 도메인 범위에 속하지 않는 경우 Active Directory 도메인 서비스 구성 마법사에 도메인 자격 증명을 제공하라는 메시지가 표시됩니다. 클릭 **변경** 도메인 자격 증명을 제공 합니다.  
  
도메인을 만드는 방법에 대 한 자세한 내용은 참조 [는 새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 및 #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)합니다.  
  
기존 도메인에 새 도메인 컨트롤러를 추가하는 경우 다음 옵션이 표시됩니다.  
  
![AD DS 설치](./media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Replica.gif)  
  
-   클릭 **선택** 에 도메인을 검색 하거나 유효한 도메인 이름을 입력 합니다.  
  
-   필요한 경우 서버 관리자에 유효한 자격 증명을 제공하라는 메시지가 표시됩니다. 추가 도메인 컨트롤러를 설치하려면 Domain Admins 그룹의 구성원이어야 합니다.  
  
    또한 Enterprise Admins 및 Schema Admins 그룹의 그룹 구성원을 포함 하는 자격 증명이 필요 포리스트의 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 설치 합니다. 현재 자격 증명에 적절한 사용 권한이나 그룹 구성원이 없는 경우 나중에 Active Directory Domain Services 구성 마법사에 자격 증명을 제공하라는 메시지가 표시됩니다.  
  
기존 도메인에 도메인 컨트롤러를 추가 하는 방법에 대 한 자세한 내용은 참조 [기존 도메인 & #40;에 복제 Windows Server 2012 도메인 컨트롤러를 설치 합니다. 200 수준 & #41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)합니다.  
  
## <a name="BKMK_DCOptionsPage"></a>도메인 컨트롤러 옵션  
새 포리스트를 만드는 경우 도메인 컨트롤러 옵션 페이지에 다음 옵션이 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Forest.gif)  
  
-   포리스트 및 도메인 기능 수준은 기본적으로 Windows Server 2012로 설정 됩니다.  
  
    Windows Server 2012 도메인 기능 수준에서 새로운 기능 중 하나는: 동적 액세스 제어 및 Kerberos 아머 KDC 관리 템플릿 정책에 대 한 지원에 Windows Server 2012 도메인 기능 수준이 필요로 하는 두 가지 설정이 (항상 클레임 제공 및 아머 링 되지 않은 인증 요청 실패). 자세한 내용은 "클레임, 복합 인증 및 Kerberos 아머 링 지원"을 참조 [Kerberos 인증의 새로운](https://technet.microsoft.com/library/hh831747.aspx)합니다.    
    Windows Server 2012 포리스트 기능 수준이 새로운 모든 기능을 제공 하지는 않지만 포리스트에서 만들어진 새 도메인이 Windows Server 2012 도메인 기능 수준에서 자동으로 작동 되도록 보장 합니다. Windows Server 2012 도메인 기능 수준에서는 모든 새 다른 기능은 동적 액세스 제어 및 Kerberos 아머 링을 지원 하지만 도메인의 모든 도메인 컨트롤러에 Windows Server 2012 실행 되는지 확인 합니다. 다양한 기능 수준에서 사용할 수 있는 기타 기능에 대한 자세한 내용은 [AD DS(Active Directory 도메인 서비스) 기능 수준 이해](../active-directory-functional-levels.md)를 참조하세요.  
  
    기능 수준 이외 Windows Server 2012를 실행 하는 도메인 컨트롤러는 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러에서 사용할 수 없는 추가 기능을 제공 합니다. 예를 들어 Windows Server 2012를 실행 하는 도메인 컨트롤러를 사용할 수 있습니다 가상 도메인 컨트롤러 복제에 대 한 반면 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러 수 없습니다.  
  
-   새 포리스트를 만드는 경우 기본적으로 DNS 서버가 선택됩니다. 포리스트의 첫 번째 도메인 컨트롤러는 GC(글로벌 카탈로그) 서버여야 합니다. RODC(읽기 전용 도메인 컨트롤러)일 수 없습니다.  
  
-   AD DS가 실행되고 있지 않은 도메인 컨트롤러에 로그온하려면 DSRM(디렉터리 서비스 복원 모드) 암호가 필요합니다. 지정한 암호는 서버에 적용된 암호 정책을 준수해야 합니다. 기본적으로 강력한 암호가 필요하지 않습니다. 빈 암호만 아니면 됩니다. 항상 강력하고 복잡한 암호 또는 암호 문구를 선택하십시오. 도메인 사용자 계정의 암호와 DSRM 암호를 동기화 하는 방법에 대 한 정보를 참조 하십시오. [KB 961320](https://support.microsoft.com/kb/961320)합니다.  
  
포리스트를 만드는 방법에 대 한 자세한 내용은 참조 [#40; & 새 Windows Server 2012 Active Directory 포리스트 설치 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)합니다.  
  
자식 도메인을 만드는 경우 도메인 컨트롤러 옵션 페이지에 다음 옵션이 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Child.gif)  
  
-   도메인 기능 수준이 기본적으로 Windows Server 2012로 설정 됩니다. 포리스트 기능 수준 값 이상인 다른 값을 지정할 수 있습니다.  
  
-   구성 가능한 도메인 컨트롤러 옵션에는 **DNS 서버** 및 **글로벌 카탈로그**가 포함됩니다. 읽기 전용 도메인 컨트롤러는 새 도메인의 첫 번째 도메인 컨트롤러로 구성할 수 없습니다.  
  
    Microsoft에서는 모든 도메인 컨트롤러가 분산된 환경에서 고가용성을 위해 DNS 및 글로벌 카탈로그 서비스를 제공할 것을 권장합니다. 이러한 이유로 새 도메인을 만드는 경우 마법사는 기본적으로 이 옵션을 사용하도록 설정합니다.  
  
-   **도메인 컨트롤러 옵션** 페이지에서는 포리스트 구성에서 적절한 Active Directory 논리 **사이트 이름** 을 선택할 수도 있습니다. 기본적으로 가장 정확한 서브넷을 포함한 사이트가 선택됩니다. 사이트가 1개 있는 경우 자동으로 그 사이트가 선택됩니다.  
  
    > [!IMPORTANT]  
    > 서버 Active Directory 서브넷에 속해 있지 않는 경우 둘 이상의 사이트 아무 것도 선택 및 **다음** 단추 사용할 수 없는 목록에서 사이트를 선택 합니다.  
  
도메인을 만드는 방법에 대 한 자세한 내용은 참조 [는 새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 및 #40; 설치 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)합니다.  
  
도메인에 도메인 컨트롤러를 추가하는 경우 도메인 컨트롤러 옵션 페이지에 다음 옵션이 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Replica.gif)  
  
-   구성 가능한 도메인 컨트롤러 옵션에는 **DNS 서버**, **글로벌 카탈로그** 및 **읽기 전용 도메인 컨트롤러**가 포함됩니다.  
  
    Microsoft에서는 모든 도메인 컨트롤러가 분산된 환경에서 고가용성을 위해 DNS 및 글로벌 카탈로그 서비스를 제공할 것을 권장합니다. 이러한 이유로 마법사는 기본적으로 이 옵션을 사용하도록 설정합니다. Rodc를 배포 하는 방법에 대 한 자세한 내용은 참조 [읽기 전용 도메인 컨트롤러 계획 및 배포 가이드](https://technet.microsoft.com/library/cc771744(v=WS.10).aspx)합니다.  
  
기존 도메인에 도메인 컨트롤러를 추가 하는 방법에 대 한 자세한 내용은 참조 [기존 도메인 & #40;에 복제 Windows Server 2012 도메인 컨트롤러를 설치 합니다. 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)합니다.  
  
## <a name="BKMK_DNSOptionsPage"></a>DNS 옵션  
다음 DNS 서버를 설치 하는 경우 **DNS 옵션** 페이지가 나타납니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DNSOptions_Replica.gif)  
  
DNS 서버를 설치하는 경우 영역에 대해 권한 있는 DNS 서버를 가리키는 위임 레코드는 부모 DNS(Domain Name System) 영역에 만들어야 합니다. 위임 레코드는 이름 확인 권한을 이전하고 다른 DNS 서버와 새 영역에 대한 권한이 부여된 새 서버의 클라이언트에 올바른 참조를 제공합니다. 이러한 리소스 레코드는 다음과 같습니다.  
  
-   위임을 적용할 NS(이름 서버) 리소스 레코드. 이 리소스 레코드는 ns1.na.example.microsoft.com이라는 서버가 위임된 하위 도메인에 대한 권한이 있는 서버임을 알리는 데 사용됩니다.  
  
-   호스트 (A 또는 AAAA) 리소스 레코드 라고도 글 루 레코드 있어야 해당 IP 주소로 이름 서버 (NS) 리소스 레코드에 지정 된 서버의 이름을 확인할 수 있습니다. 이 리소스 레코드의 호스트 이름을 NS(이름 서버) 리소스 레코드의 위임된 DNS 서버로 확인하는 프로세스를 "글루 추적"이라고도 합니다.  
  
Active Directory Domain Services 구성 마법사에서 레코드를 자동으로 만들도록 할 수 있습니다. 마법사는 클릭 한 후 적절 한 레코드는 부모 DNS 영역에 있는지 확인 **다음** 에 **도메인 컨트롤러 옵션** 페이지입니다. 마법사에서 부모 도메인에 레코드가 있는지 확인할 수 없으면 자동으로 새 도메인에 대한 새 DNS 위임을 만들거나 기존 위임을 업데이트하는 옵션을 제공하고 새 도메인 컨트롤러 설치를 계속합니다.  
  
또는 DNS 서버를 설치하기 전에 이러한 DNS 위임 레코드를 만들 수 있습니다. 영역 위임을 만들려면, **DNS 관리자**, 부모 도메인을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **새 위임**합니다. 새 위임 마법사를 단계별로 진행하면 위임을 만들 수 있습니다.  
  
설치 프로세스는 다른 도메인의 컴퓨터가 DNS 하위 도메인의 구성원 컴퓨터, 도메인 컨트롤러를 비롯하여 호스트에 대한 DNS 쿼리를 해결할 수 있도록 위임을 만들려고 시도합니다. 위임 레코드는 Microsoft DNS 서버에서만 자동으로 만들어질 수 있습니다. 부모 DNS 도메인 영역이 BIND와 같은 타사 DNS 서버에 있는 경우 필수 구성 요소 확인 페이지에 DNS 위임 레코드 만들기 실패와 관련한 경고가 표시됩니다. 경고에 대 한 자세한 내용은 참조 [알려진 AD DS를 설치 하기 위한 문제](https://technet.microsoft.com/library/cc754463(v=WS.10).aspx)합니다.  
  
설치 전이나 설치 후에 승격 중인 부모 도메인 및 하위 도메인 간 위임을 만들고 확인할 수 있습니다. DNS 위임을 만들거나 업데이트할 수 없으므로 새 도메인 컨트롤러 설치를 지연시킬 이유가 없습니다.  
  
위임에 대 한 자세한 내용은 참조 하세요. [영역 위임 이해](https://go.microsoft.com/fwlink/?LinkId=164773) (https://go.microsoft.com/fwlink/?LinkId=164773)합니다. 영역 위임이 불가능한 상황에서는 다른 방법을 통해 다른 도메인에서 사용자 도메인의 호스트 이름을 확인하는 기능을 제공할 수 있습니다. 예를 들어 다른 도메인의 DNS 관리자가 사용자 도메인의 이름을 확인하기 위해 조건부 전달, 스텁 영역 또는 보조 영역을 구성할 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [영역 종류 이해](https://go.microsoft.com/fwlink/?LinkID=157399) (https://go.microsoft.com/fwlink/?LinkID=157399)  
  
-   [스텁 영역 이해](https://go.microsoft.com/fwlink/?LinkId=164776) (https://go.microsoft.com/fwlink/?LinkId=164776)  
  
-   [전달자 이해](https://go.microsoft.com/fwlink/?LinkId=164778) (https://go.microsoft.com/fwlink/?LinkId=164778)  
  
## <a name="BKMK_RODCOptionsPage"></a>RODC 옵션  
RODC(읽기 전용 도메인 컨트롤러)를 설치하는 경우 다음 옵션이 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_RODCOptions.gif)  
  
-   위임된 관리자 계정은 RODC에 대한 로컬 관리 권한을 가집니다. 이러한 사용자는 로컬 컴퓨터의 관리자 그룹에 해당 하는 권한으로 작동할 수 있습니다. Domain Admins 또는 도메인 기본 제공관리자그룹의 구성원은 아닙니다 이 옵션은 도메인 관리 권한을 정지하지 않고도 지점 관리를 위임하는 데 유용합니다. 관리 위임을 별도로 구성하지 않아도 됩니다. 자세한 내용은 참조 [관리자 역할 구분](https://technet.microsoft.com/library/cc753170(v=WS.10).aspx)합니다.  
  
-   암호 복제 정책은 ACL(액세스 제어 목록)로 사용되며 RODC에서 암호를 캐시하도록 허용할지 여부를 결정합니다. RODC는 인증된 사용자 또는 컴퓨터 로그온 요청을 받은 후 암호 복제 정책을 참조하여 계정에 대한 암호가 캐시되도록 할지 여부를 결정합니다. 그러면 동일한 계정으로의 이후 로그온이 더 효율적으로 이루어집니다.  
  
    PRP(암호 복제 정책)는 암호 캐시가 허용된 계정과 암호 캐시가 명시적으로 거부된 계정을 나열합니다. 사용자 및 컴퓨터 계정 목록이 캐시할 수 있게 허용되었다고 해서 RODC가 해당 계정의 암호를 반드시 캐시했다고 할 수는 없습니다. 예를 들어 관리자는 RODC가 캐시할 계정을 미리 지정할 수 있습니다. 이러한 방식으로 허브 사이트에 대한 WAN 연결이 오프라인 상태일 때도 RODC는 해당 계정을 인증할 수 있게 됩니다.  
  
    허용되지 않았거나(암시적 허용 포함) 거부된 모든 사용자나 컴퓨터는 해당 암호를 캐시하지 않습니다. 해당 사용자나 컴퓨터가 쓰기 가능한 도메인 컨트롤러에 액세스할 수 없는 경우 AD DS에서 제공하는 리소스나 기능에 액세스할 수 없습니다. PRP에 대 한 자세한 내용은 참조 [암호 복제 정책](https://technet.microsoft.com/library/cc730883(v=ws.10).aspx)합니다. PRP를 관리 하는 방법에 대 한 자세한 내용은 참조 [암호 복제 정책 관리](https://technet.microsoft.com/library/rodc-guidance-for-administering-the-password-replication-policy(v=ws.10).aspx)합니다.  
  
Rodc를 설치 하는 방법에 대 한 자세한 내용은 참조 [#40; 및 Windows Server 2012 Active Directory 읽기 전용 도메인 컨트롤러를 설치 합니다. RODC & #41; & #40; 200 수준 & #41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md)합니다.  
  
## <a name="BKMK_AdditionalOptionsPage"></a>추가 옵션  
새 도메인을 만드는 경우 **추가 옵션** 페이지에 다음 옵션이 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Child.gif)  
  
기존 도메인에 추가 도메인 컨트롤러를 설치하는 경우 **추가 옵션** 페이지에 다음 옵션이 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Replica.gif)  
  
-   복제 원본으로 도메인 컨트롤러를 지정하거나 마법사에서 복제 원본으로 도메인 컨트롤러를 선택하도록 허용할 수 있습니다.  
  
-   또한 IFM(미디어에서 설치) 옵션을 통해 백업된 미디어를 사용하여 도메인 컨트롤러를 설치하도록 선택할 수도 있습니다. 설치 미디어를 로컬로 저장 되는 경우는 **미디어에서 설치 경로** 옵션을 사용 하면 파일 위치를 찾아볼 수 있습니다. 원격 설치 시에는 검색 옵션을 사용할 수 없습니다. **확인**을 클릭하여 제공된 경로가 유효한 미디어인지 확인할 수 있습니다. IFM 옵션에서 사용 된 미디어 만들어야 Ntdsutil.exe 나 Windows Server 백업 다른 기존 Windows Server 2012 컴퓨터에서만 사용 합니다. Windows Server 2012 도메인 컨트롤러에 대 한 미디어를 만드는 데는 Windows Server 2008 R2 또는 이전 운영 체제를 사용할 수 없습니다. 미디어가 SYSKEY로 보호된 경우 검증하는 동안 서버 관리자에는 이미지 암호를 제공하라는 메시지가 표시됩니다.  
  
도메인을 만드는 방법에 대 한 자세한 내용은 참조 [는 새 Windows Server 2012 Active Directory 자식 또는 트리 도메인 및 #40; 설치 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)합니다. 기존 도메인에 도메인 컨트롤러를 추가 하는 방법에 대 한 자세한 내용은 참조 [기존 도메인 & #40;에 복제 Windows Server 2012 도메인 컨트롤러를 설치 합니다. 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)합니다.  
  
## <a name="BKMK_Paths"></a>경로  
에 다음 옵션이 표시 된 **경로** 페이지입니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_Paths.gif)  
  
-   **경로** 페이지에서 AD DS 데이터베이스, 데이터베이스 트랜잭션 로그 및 SYSVOL 공유의 기본 폴더 위치를 재정의할 수 있습니다. 기본 위치는 항상 %systemroot%입니다.  
  
AD DS 데이터베이스(NTDS.DIT), 로그 파일 및 SYSVOL의 위치를 지정합니다. 로컬 설치의 경우 파일을 저장할 위치를 검색할 수 있습니다.  
  
## <a name="BKMK_AdprepCreds"></a>준비 옵션  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PreparationOptions.gif)  
  
현재 adprep.exe 명령을 실행할 권한이 있는 자격 증명으로 로그온되어 있지 않고 AD DS 설치를 완료하기 위해 adprep을 실행해야 하는 경우 adprep.exe를 실행하는 데 필요한 자격 증명을 제공하라는 메시지가 표시됩니다. Adprep은 기존 도메인 또는 포리스트를 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 추가 하기 위해 실행 해야 합니다. 즉,  
  
-   기존 포리스트를 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 추가 하려면 Adprep /forestprep을 실행 해야 합니다. 이 명령을 실행하려면 스키마 마스터를 호스트하는 도메인의 Enterprise Admins 그룹, Schema Admins 그룹 및 Domain Admins 그룹의 구성원이어야 합니다. 이 명령을 완료하려면 명령을 실행하는 컴퓨터와 포리스트의 스키마 마스터 간 연결이 설정되어야 합니다.  
  
-   기존 도메인에 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 추가 하려면 Adprep /domainprep 실행 되어야 합니다. 이 명령은 Windows Server 2012를 실행 하는 도메인 컨트롤러를 설치 하는 도메인의 Domain Admins 그룹의 구성원으로 실행 되어야 합니다. 이 명령을 완료하려면 명령을 실행하는 컴퓨터와 도메인의 인프라 마스터 간 연결이 설정되어야 합니다.  
  
-   첫 번째 RODC를 기존의 포리스트에 추가하려면 Adprep /rodcprep을 실행해야 합니다. 이 명령을 실행하려면 Enterprise Admins 그룹의 구성원이어야 합니다. 이 명령을 완료하려면 명령을 실행하는 컴퓨터와 포리스트의 각 응용 프로그램 디렉터리 파티션의 인프라 마스터 간 연결이 설정되어야 합니다.  
  
Adprep.exe에 대 한 자세한 내용은 참조 [Adprep.exe 통합](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep) 참조 및 [Adprep.exe 실행](https://technet.microsoft.com/library/dd464018(WS.10).aspx)합니다.  
  
## <a name="BKMK_ViewInstallOptionsPage"></a>옵션 검토  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_ReviewOptions.gif)  
  
-   **옵션 검토** 페이지에서 설치를 시작하기 전에 설정을 확인하고 이러한 설정이 요구 사항을 충족하는지도 확인할 수 있습니다. 서버 관리자를 사용하여 설치를 중지할 수 있는 마지막 기회는 아닙니다. 이 페이지에서는 단지 구성을 계속하기 전에 설정을 검토하고 확인합니다.  
  
-   서버 관리자의 **옵션 검토** 페이지는 현재 ADDSDeployment 구성을 단일 Windows PowerShell 스크립트로 포함하는 유니코드 텍스트 파일을 만들 수 있도록 **스크립트 보기** 단추(선택 사항)도 제공합니다. 이 단추를 통해 서버 관리자 그래픽 인터페이스를 Windows PowerShell 배포 스튜디오로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용하여 옵션을 구성하고 구성을 내보낸 다음 마법사를 취소합니다. 이 프로세스를 통해 향후 수정을 위해 사용하거나 직접 사용하기 위한 유효하고 구문상으로 정확한 샘플이 만들어집니다.  
  
## <a name="BKMK_PrerqCheckPage"></a>필수 구성 요소 확인  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PrerequisitesCheck.gif)  
  
이 페이지에 나타나는 경고 중 일부는 다음과 같습니다.  
  
-   Windows Server 2008을 실행 하거나 나중에 "허용 암호화 알고리즘 Windows NT 4와 호환"에 대 한 보안 채널 세션을 설정할 때 취약 한 암호화 알고리즘을 방지 하는 기본 설정 하는 도메인 컨트롤러입니다. 잠재적인 영향 및 해결 방법은 기술 자료 문서를 참조 하는 방법에 대 한 자세한 내용은 [942564](https://support.microsoft.com/kb/942564)합니다.  
  
-   DNS 위임은 만들거나 업데이트할 수 없습니다. 자세한 내용은 참조 [DNS 옵션](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)합니다.  
  
-   필수 구성 요소 확인을 수행하려면 WMI를 호출해야 합니다. 방화벽 규칙 블럭에서 이 호출이 차단된 경우 호출이 실패하고 "RPC 서버를 사용할 수 없음" 오류가 반환될 수 있습니다.  
  
AD DS 설치에 대해 수행되는 특정 필수 구성 요소 확인에 대한 자세한 내용은 [필수 구성 요소 테스트](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_ADDSInstallPrerequisiteTests)를 참조하십시오.  
  
## <a name="BKMK_Results"></a>결과  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_SMResultsBeta.gif)  
  
이 페이지에서 설치 결과를 확인할 수 있습니다.  
  
마법사가 완료되면 대상 서버를 다시 시작하도록 선택할 수도 있습니다. 단, 설치가 성공할 경우 해당 옵션 선택 여부에 상관없이 서버가 항상 다시 시작됩니다. 경우에 따라 설치 전에 도메인에 가입되지 않은 대상 서버에서 마법사가 완료되면 대상 서버의 시스템 상태로 인해 네트워크에서 서버에 연결할 수 없거나 원격 서버에 대한 관리 권한을 갖지 못하도록 제한될 수 있습니다.  
  
이 경우 대상 서버가 다시 시작되지 않았으면 수동으로 다시 시작해야 합니다. shutdown.exe나 Windows PowerShell과 같은 도구로는 대상 서버를 다시 시작할 수 없습니다. 원격 데스크톱 서비스를 사용하여 대상 서버에 로그온하고 이 서버를 원격으로 종료할 수 있습니다.  
  
## <a name="BKMK_RemovalCredsPage"></a>역할 제거 자격 증명  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Credentials.gif)  
  
**자격 증명** 페이지에서 수준 내리기 옵션을 구성합니다. 다음 목록에서 수준 내리기를 수행하는 데 필요한 자격 증명을 제공합니다.  
  
-   추가 도메인 컨트롤러의 수준을 내리려면 Domain Admin 자격 증명이 필요합니다. 선택 하면 **강제 제거는 도메인 컨트롤러의** Active Directory에서 도메인 컨트롤러 개체의 메타 데이터를 제거 하지 않고 도메인 컨트롤러 수준을 내립니다.  
  
    > [!IMPORTANT]  
    > 도메인 컨트롤러에서 다른 도메인 컨트롤러에 연결할 수 없고 해당 네트워크 문제를 해결할 *합리적인 방법이 없는* 경우가 아니면 이 옵션을 선택하지 마십시오. 강제로 수준을 내리면 포리스트에서 남아 있는 도메인 컨트롤러의 Active Directory에서 메타데이터가 분리되게 됩니다. 또한 암호나 새 사용자 계정과 같이 해당 도메인 컨트롤러에서 복제되지 않은 모든 변경 사항이 영구 손실됩니다. 분리된 메타데이터는 AD DS, Exchange, SQL 및 기타 소프트웨어와 관련한 Microsoft 고객 지원 사례의 상당 부분을 차지하는 근본 원인입니다. 도메인 컨트롤러의 수준을 강제로 내리려면 바로 메타데이터 정리 작업을 수동으로 *수행해야 합니다*. 단계에 대 한 검토 [서버 메타 데이터 정리](https://technet.microsoft.com/library/cc816907(WS.10).aspx)합니다.  
  
-   도메인에서 마지막 도메인 컨트롤러의 수준을 내리려면 이 작업은 도메인 자체를 제거하므로 Enterprise Admins 그룹의 구성원이어야 합니다(포리스트의 마지막 도메인일 경우 포리스트 자체가 제거됨). 서버 관리자는 현재 도메인 컨트롤러가 도메인의 마지막 도메인 컨트롤러인지 여부를 알려줍니다. **도메인의 마지막 도메인 컨트롤러**를 선택하여 도메인 컨트롤러가 도메인의 마지막 도메인 컨트롤러인지 확인합니다.  
  
AD DS를 제거 하는 방법에 대 한 자세한 내용은 참조 [Active Directory 도메인 서비스 제거 (수준 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) 및 [도메인 컨트롤러 수준 내리기 및 도메인 & #40; 200 수준 & #41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md)합니다.  
  
## <a name="BKMK_RemovalOptionsPage"></a>AD DS 제거 옵션 및 경고  
옵션 검토 페이지와 관련하여 도움이 필요한 경우 옵션 검토를 참조하십시오.  
  
도메인 컨트롤러가 DNS 서버 역할이나 글로벌 카탈로그 서버와 같은 추가 역할을 호스트하는 경우 다음과 같은 경고 페이지가 표시됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Warnings.gif)  
  
클릭 해야 **제거 진행** 는 추가 역할은 더 이상 사용할 수 클릭 하기 전에 승인 하려면 **다음** 를 계속 합니다.  
  
도메인 컨트롤러를 강제로 제거하면 도메인의 다른 도메인 컨트롤러에 복제되지 않은 모든 Active Directory 개체 변경 사항이 손실됩니다. 또한 도메인 컨트롤러가 작업 마스터 역할, 글로벌 카탈로그 또는 DNS 서버 역할을 호스트하는 경우 다음과 같이 도메인 및 포리스트의 중요한 작업에 영향을 미칠 수 있습니다. 작업 마스터 역할을 호스트하는 도메인 컨트롤러를 제거하기 전에 역할을 다른 도메인 컨트롤러로 전송합니다. 역할을 전송할 수 없는 경우 먼저 이 컴퓨터에서 Active Directory Domain Services를 제거한 후 Ntdsutil.exe를 사용하여 역할을 점유합니다. 역할을 점유할 도메인 컨트롤러에 대해 Ntdsutil을 사용합니다. 가능하면 이 도메인 컨트롤러와 동일한 사이트에서 최신 복제 파트너를 사용합니다. 전송 하 고 작업 마스터 역할 점유 하는 방법에 대 한 자세한 내용은 참조 [255504 문서](https://go.microsoft.com/fwlink/?LinkId=80395) Microsoft 기술 자료에서 합니다. 마법사에서 도메인 컨트롤러가 작업 마스터 역할을 호스트하는지 여부를 확인할 수 없는 경우에는 netdom.exe 명령을 사용하여 이 도메인 컨트롤러가 작업 마스터 역할을 수행하는지 여부를 확인합니다.  
  
-   글로벌 카탈로그: 사용자가 포리스트의 도메인에 로그온 하는 데 문제가 로깅이 있을 수 있습니다. 글로벌 카탈로그 서버를 제거하기 전에 이 포리스트 및 사이트에 사용자 로그온을 처리할 충분한 글로벌 카탈로그 서버가 있는지 확인하십시오. 필요한 경우 다른 글로벌 카탈로그 서버를 지정하고 새로운 정보로 클라이언트 및 응용 프로그램을 업데이트하십시오.  
  
-   DNS 서버: 모든 Active Directory 통합 영역에 저장 되는 DNS 데이터가 손실 됩니다. AD DS를 제거하고 나면 Active Directory가 통합된 DNS 영역에 대해 이 DNS 서버가 이름을 확인할 수 없습니다. 따라서 이름 확인을 위해 현재 이 DNS 서버의 IP 주소를 참조하는 모든 컴퓨터의 DNS 구성을 새 DNS 서버의 IP 주소로 업데이트하는 것이 좋습니다.  
  
-   인프라 마스터: 도메인의 클라이언트가 다른 도메인의 개체를 찾지 못할 수 있습니다. 계속하려면 인프라 마스터 역할을 글로벌 카탈로그 서버가 아닌 도메인 컨트롤러에 전송하십시오.  
  
-   RID 마스터: 새 사용자 계정, 컴퓨터 계정 및 보안 그룹을 만들 때 문제가 발생할 수 있습니다. 계속하려면 RID 마스터 역할을 이 도메인 컨트롤러와 동일한 도메인에 있는 도메인 컨트롤러에 전송하십시오.  
  
-   PDC(주 도메인 컨트롤러) 에뮬레이터: AD DS 이외의 계정에 대한 그룹 정책 업데이트 및 암호 재설정 등과 같이 PDC 에뮬레이터에서 수행된 작업이 제대로 작동하지 않습니다. 계속하려면 PDC 에뮬레이터 마스터 역할을 이 도메인 컨트롤러와 동일한 도메인에 있는 도메인 컨트롤러에 전송하십시오.  
  
-   스키마 마스터: 더 이상 이 포리스트의 스키마를 수정할 수 없습니다. 계속하려면 스키마 마스터 역할을 포리스트의 루트 도메인에 있는 도메인 컨트롤러에 전송하십시오.  
  
-   도메인 명명 마스터: 더 이상 이 포리스트에 도메인을 추가할 수 없거나 이 포리스트에서 도메인을 제거할 수 없습니다. 계속하려면 도메인 명명 마스터 역할을 포리스트에 있는 루트 도메인의 도메인 컨트롤러에 전송하십시오.  
  
-   이 Active Directory 도메인 컨트롤러의 모든 응용 프로그램 디렉터리 파티션은 제거됩니다. 도메인 컨트롤러에 하나 이상의 응용 프로그램 디렉터리 파티션에 대한 마지막 복제본이 있더라도 제거 작업을 완료하면 해당 파티션이 더 이상 존재하지 않게 됩니다.  
  
도메인의 마지막 도메인 컨트롤러에서 Active Directory 도메인 서비스를 제거하고 나면 도메인이 더 이상 존재하지 않게 됩니다.  
  
도메인 컨트롤러가 DNS 영역을 호스트하도록 위임된 DNS 서버일 경우 다음 페이지에 DNS 영역 위임에서 DNS 서버를 제거하는 옵션이 제공됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_RemovalOptions.gif)  
  
AD DS를 제거 하는 방법에 대 한 자세한 내용은 참조 [Active Directory 도메인 서비스 제거 (수준 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) 및 [도메인 컨트롤러 수준 내리기 및 도메인 & #40; 200 수준 & #41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md)합니다.  
  
## <a name="BKMK_NewAdminPwdPage"></a>새 관리자 암호  
**새 관리자 암호** 페이지 수준 내리기를 완료 되 고 컴퓨터가 도메인 구성원 서버나 작업 그룹 컴퓨터에 기본 제공 로컬 컴퓨터의 관리자 계정에 대 한 암호를 제공 해야 합니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_NewAdminPwd.gif)  
  
AD DS를 제거 하는 방법에 대 한 자세한 내용은 참조 [Active Directory 도메인 서비스 제거 (수준 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) 및 [도메인 컨트롤러 수준 내리기 및 도메인 & #40; 200 수준 & #41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md)합니다.  
  
## <a name="BKMK_ConfirmRoleRemovalPage"></a>옵션 검토  
**옵션 검토** 페이지에서는 추가 수준 내리기를 자동화할 수 있도록 수준 내리기에 대 한 구성 설정을 Windows PowerShell 스크립트를 내보낼 수 있습니다. **수준 내리기**를 클릭하여 AD DS를 제거합니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_ReviewOptions.gif)  
  


