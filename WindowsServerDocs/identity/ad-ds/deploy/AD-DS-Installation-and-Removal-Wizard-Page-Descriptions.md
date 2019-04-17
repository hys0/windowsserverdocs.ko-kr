---
ms.assetid: ac727bd1-a892-47ed-a7ba-439b34187d4e
title: "AD DS 설치 및 제거 마법사 페이지 설명"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fa023398822e79ca8c3e93d44bb1e87fc9190cee
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-installation-and-removal-wizard-page-descriptions"></a>AD DS 설치 및 제거 마법사 페이지 설명

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 다음 마법사의 페이지에서 AD DS 서버 역할 설치 및 제거 서버 관리자 구성 하는 컨트롤에 대 한 설명을 제공 합니다.  
  
-   [배포 구성](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DepConfigPage)  
  
-   [도메인 컨트롤러 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)  
  
-   [DNS 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)  
  
-   [RODC 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RODCOptionsPage)  
  
-   [추가 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdditionalOptionsPage)  
  
-   [경로](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Paths)  
  
-   [준비 옵션](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdprepCreds)  
  
-   [옵션을 검토](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ViewInstallOptionsPage)  
  
-   [필수 확인](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_PrerqCheckPage)  
  
-   [결과](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Results)  
  
-   [역할 제거 자격 증명](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalCredsPage)  
  
-   [AD DS 제거 옵션 및 경고](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalOptionsPage)  
  
-   [새로운 관리자 암호](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_NewAdminPwdPage)  
  
-   [확인 역할 제거 선택](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ConfirmRoleRemovalPage)  
  
## <a name="BKMK_DepConfigPage"></a>배포 구성  
서버 관리자 모든 도메인 컨트롤러 설치를 시작 되 고 **배포 구성** 페이지 합니다. 나머지 옵션과 필수 필드가 페이지에서 다음 페이지를 선택 하는 배포 작업에 따라 변경 됩니다. 예를 들어 새 숲 만들는 **준비 옵션** 기존 숲 나 도메인에 있는 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 설치 하는 경우 않으면 되지만 페이지가 표시 되지 않습니다.  
  
이 페이지에 하 고 나중에 다시 필수 검사의 일환으로 일부 유효성 검사가 테스트 수행 됩니다. 예를 들어, Windows 2000 기능 수준이 숲 속의 첫 번째 Windows Server 2012 도메인 컨트롤러를 설치 하려고 하면 오류가이 페이지에 나타납니다.  
  
새 숲 만든 다음 옵션이 나타납니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Forest.gif)  
  
-   새 숲을 만들 때 숲 루트 도메인에 이름을 지정 해야 합니다. 숲 루트 도메인 이름 단일 레이블이 표시 될 수 없습니다 (예를 들어, 것 이어야 함 "contoso" 대신 "contoso.com"). 허용된 DNS 도메인 명명 규칙을 사용 해야 합니다. 프로그램 다국어 도메인 이름 (IDN)를 지정할 수 있습니다. For more information about DNS domain naming conventions, see [KB 909264](https://support.microsoft.com/kb/909264).  
  
-   외부 DNS 이름 이름이 같은 새로운 Active Directory 숲 만들지 않습니다. 예를 들어, 인터넷 DNS URL http://contoso.com 이면 향후 호환성 문제를 방지 하 여 내부 숲에 대 한 다른 이름을 선택 해야 합니다. 해당 이름은 고유 하 고 웹 교통량 corp.contoso.com 등 해야 합니다.  
  
-   새 숲 만들려는 서버의 관리자가 그룹 속해야 합니다.  
  
숲을 만드는 방법에 대 한 자세한 내용은 참조 [는 새로운 Windows Server 2012 Active Directory 숲 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
새 도메인 만들 다음과 같은 옵션이 나타납니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_ChildDomain.gif)  
  
> [!NOTE]  
> 새 밤나무 도메인 만들면 부모 도메인 대신 이렇게의 이름을 지정 필요는 없지만 마법사 나머지 페이지 및 옵션 동일 합니다.  
  
-   클릭 **선택** 부모 도메인 또는 Active Directory 트리 또는 올바른 상위 도메인 또는 나무 이름을 입력 합니다. 다음에 새는 도메인의 이름을 입력 **새 도메인 이름**합니다.  
  
-   트리 도메인: 제공 유효한, 정식 루트 도메인 이름입니다. 단일 레이블이 표시 될 수 없는 이름과 DNS 도메인 이름 요구 사항에 사용 해야 합니다.  
  
-   자녀가 도메인: 제공 유효한, 단일 레이블 자녀 도메인 이름입니다. 이름은 DNS 도메인 이름 요구 사용 해야 합니다.  
  
-   Active Directory Domain Services 구성 묻는 도메인 자격 증명을 현재 자격 증명 도메인 없는 경우입니다. 클릭 **변경** 도메인 자격 증명을 제공 합니다.  
  
도메인을 만드는 방법에 대 한 자세한 내용은 참조 [새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
새 도메인 컨트롤러 기존 도메인에 추가 하면 다음과 같은 옵션이 나타납니다.  
  
![AD DS 설치](./media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Replica.gif)  
  
-   클릭 **선택** 도메인을 찾아보거나 유효한 도메인 이름을 입력 합니다.  
  
-   서버 관리자 묻는 유효한 자격 증명 필요 합니다. 추가 도메인 컨트롤러를 설치 하려면 관리자 도메인 그룹의 회원이 필요 합니다.  
  
    또한 한 숲 속의 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러 설치 그룹 구성원 엔터프라이즈 관리자와 스키마 관리자 그룹에 포함 된 자격 증명을 해야 합니다. Active Directory 도메인 서비스 구성 묻는 메시지가 나중에 적절 한 권한이 또는 그룹 구성원 현재 자격 증명 되어 있지 않습니다.  
  
도메인 컨트롤러 기존 도메인에 추가 하는 방법에 대 한 자세한 내용은 참조 [복제 Windows Server 2012 도메인 컨트롤러에 기존 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_DCOptionsPage"></a>도메인 컨트롤러 옵션  
새 숲 만드는 경우 도메인 컨트롤러 옵션 페이지에는 이러한 옵션:  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Forest.gif)  
  
-   Windows Server 2012 기본적으로 숲 및 도메인 기능 수준은 설정 합니다.  
  
    Windows Server 2012 도메인 기능 수준 새로운 기능이 하나는: 동적 액세스 제어 및 관리 템플릿 정책 KDC armoring Kerberos에 대 한 지원에는 Windows Server 2012 도메인 기능 수준 해야 하는 두 가지 설정이 (항상 클레임 제공 하 고 실패 무방비 인증 요청). For more information, see "Support for claims, compound authentication and Kerberos armoring" in [What's new in Kerberos Authentication](https://technet.microsoft.com/library/hh831747.aspx).    
    Windows Server 2012 숲 기능 수준 새로운 기능을 제공 하지는 않지만 보장 숲에서 만든 새 도메인 Windows Server 2012 도메인 기능 수준에서 자동으로 작동 합니다. Windows Server 2012 도메인 기능 수준 제공 하지 않는 모든 새로운 동적 액세스 제어 및 Kerberos armoring에 대 한 지원이 옆에 있는 다른 기능 있지만 도메인에 있는 도메인 컨트롤러 Windows Server 2012를 실행 하면 됩니다. 다른 기능 수준에서 사용할 수 있는 다른 기능에 대 한 자세한 내용은 참조 [이해 Active Directory 도메인 서비스 (AD DS) 기능 수준](../active-directory-functional-levels.md)합니다.  
  
    기능 수준 이외 Windows Server 2012를 실행 하는 도메인 컨트롤러에서 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러에서 사용할 수 있는 추가 기능을 제공 합니다. 예를 들어, Windows Server 2012를 실행 하는 도메인 컨트롤러 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러 수 있지만 가상 도메인 컨트롤러 복제할 사용할 수 있습니다.  
  
-   DNS 서버 새 숲 생성 하면 기본적으로 선택 됩니다. 숲 속의의 첫 번째 도메인 컨트롤러 드 (GC) 서버, 및 읽기만 도메인 컨트롤러 (RODC) 일 수는 없습니다.  
  
-   디렉터리 서비스 복원 모드 (DSRM) 암호가 AD DS 실행 하지 않는 도메인 컨트롤러에 로그온 하기 위해 필요 합니다. 사용자가 지정 암호 기본적으로 강력한 암호를; 하지 않아도 하는 서버에 적용 되는 암호 정책을 준수 해야 공백 암호만 합니다. 항상 복잡 하 고 강력한 암호 또는 암호를 선택 합니다. For information about how to synchronize the DSRM password with the password of a domain user account, see [KB 961320](https://support.microsoft.com/kb/961320).  
  
숲을 만드는 방법에 대 한 자세한 내용은 참조 [는 새로운 Windows Server 2012 Active Directory 숲 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
자녀가 도메인 만드는 경우 도메인 컨트롤러 옵션 페이지에는 이러한 옵션:  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Child.gif)  
  
-   도메인 기능 수준 Windows Server 2012 기본적으로 설정 됩니다. 다른 값 숲 기능 수준을 이상 값을 이상의 지정할 수 있습니다.  
  
-   가능한 도메인 컨트롤러 옵션이 포함 **DNS 서버** 및 **드**; 새 도메인의 첫 번째 도메인 컨트롤러 읽기 전용 도메인 컨트롤러를 구성할 수 없습니다.  
  
    모든 도메인 컨트롤러 DNS 및 마법사 새 도메인을 만들 때 기본적으로 이러한 옵션을 사용 하는 이유는 분산된 환경 항상 사용 가능 드 서비스를 제공 하는 것이 좋습니다.  
  
-   **도메인 컨트롤러 옵션** 페이지도 논리 적절 한 Active Directory를 선택할 수 있습니다 **사이트 이름** 숲 구성에서 합니다. 기본적으로 가장 적은 서브넷 사이트에서는 선택 합니다. 하나의 사이트가 경우 해당 사이트 자동으로 선택 됩니다.  
  
    > [!IMPORTANT]  
    > 서버 Active Directory 서브넷에 속하지 않는 경우 둘 이상의 사이트가 아무 것도 선택 및 **다음** 단추는 목록에서 사이트를 선택할 때까지 사용할 수 없습니다.  
  
도메인을 만드는 방법에 대 한 자세한 내용은 참조 [새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
도메인에 도메인 컨트롤러를 추가 하는 경우 도메인 컨트롤러 옵션 페이지 이러한 옵션은 다음과 같습니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Replica.gif)  
  
-   가능한 도메인 컨트롤러 옵션이 포함 **DNS 서버** 및 **드**, 및 **읽기 전용 도메인 컨트롤러**합니다.  
  
    모든 도메인 컨트롤러 DNS 및는 마법사 이러한 옵션을 사용 하면 기본적으로 이유 분산된 환경 항상 사용 가능 드 서비스를 제공 하는 것이 좋습니다. For more information about deploying RODCs, see [Read-Only Domain Controller Planning and Deployment Guide](https://technet.microsoft.com/library/cc771744(v=WS.10).aspx).  
  
도메인 컨트롤러 기존 도메인에 추가 하는 방법에 대 한 자세한 내용은 참조 [복제 Windows Server 2012 도메인 컨트롤러에 기존 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_DNSOptionsPage"></a>DNS 옵션  
DNS 서버, 다음을 설치 하는 경우 **DNS 옵션** 페이지가 나타납니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DNSOptions_Replica.gif)  
  
DNS 서버를 설치 하면 해당 영역에 대 한 권한이 DNS 서버를 가리키는 위임 레코드 부모 시스템 DNS (도메인 이름) 영역에 만들어야 합니다. 위임 이름 확인 권한을 이전 기록과 다른 DNS 서버와은 한 권한이 부여 된 새 영역에 대 한 새로운 서버의 클라이언트가 올바른 추천을 제공 합니다. 이러한 리소스 레코드는 다음과 같습니다.  
  
-   위임 영향을 이름 (NS) 서버 리소스 레코드 합니다. 이 리소스 레코드 ns1.na.example.microsoft.com 이라는 서버 위임된 하위에 대 한 권한 있는 서버 임을 알립니다.  
  
-   호스트 A 등의 AAAA 리소스 기록 라고도 붙이기 기록 있어야 IP 주소를 (NS) 서버 리소스 이름 레코드에 지정 된 server의 이름을 확인 하려면. 이 리소스 레코드에 호스트 이름을 이름 (NS) 서버 리소스 레코드에 위임된 DNS 서버를 확인 하는 과정은 라고도 "추적 붙입니다."  
  
자동으로 만드는 Active Directory Domain Services 구성 마법사 할 수 있습니다. 마법사 클릭 한 후 해당 기록 부모 DNS 영역에 있는지 확인 **다음** 에 **도메인 컨트롤러 옵션** 페이지 합니다. 마법사 레코드가 부모 도메인에 있는지 확인할 수 없는, 마법사 자동으로 새로운 도메인에 대 한 새로운 DNS 위임 만드는 (또는 기존 위임 업데이트) 수 있는 옵션이 제공 하 고 새 도메인 컨트롤러 설치를 계속 수행 합니다.  
  
또는, DNS 서버를 설치 하기 전에 이러한 DNS 위임 레코드 만들 수 있습니다. 만들려면 영역 위임을 열어 **DNS 관리자**를 부모 도메인을 마우스 오른쪽 단추로 클릭 한 다음 **새 위임**합니다. 위임 만드는 새로운 위임 마법사의 단계를 따릅니다.  
  
설치 프로세스를 만드는 다른 도메인에 있는 컴퓨터에서 DNS 하위 도메인 컨트롤러 구성원 컴퓨터 등 호스트 DNS 쿼리에 확인할 수 있는지 확인 하려면 위임 시도 합니다. Note 위임 레코드 DNS 서버에만 자동으로 만들 수 있습니다. 부모 DNS 도메인 영역 BIND와 같은 제 3 자 DNS 서버에 있으면 위임 DNS 레코드 만드는 오류에 대 한 경고 필수 확인 페이지에 나타납니다. For more information about the warning, see [Known issues for installing AD DS](https://technet.microsoft.com/library/cc754463(v=WS.10).aspx).  
  
부모 도메인 및 올렸습니다 하위 간 위임 생성 하 고 유효성을 검사 하기 전에 또는 설치 후 수 있습니다. 새 도메인 컨트롤러의 설치 만들거나 DNS 위임 업데이트할 수 없습니다 때문에 지연을 이유가 있습니다.  
  
For more information about delegation, see [Understanding Zone Delegation](https://go.microsoft.com/fwlink/?LinkId=164773) (https://go.microsoft.com/fwlink/?LinkId=164773). 영역 위임 상황에서 수 없는 경우 도메인에 있는 호스트 다른 도메인의 이름을 확인을 제공 하기 위해 다른 방법 고려할 수 있습니다. 예를 들어 조건 전달을, 스텁 영역 또는 보조 DNS 관리자 다른 도메인에 구성할 수 영역 도메인의 이름을 확인 하려면. 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [Understanding zone types](https://go.microsoft.com/fwlink/?LinkID=157399) (https://go.microsoft.com/fwlink/?LinkID=157399)  
  
-   [Understanding stub zones](https://go.microsoft.com/fwlink/?LinkId=164776) (https://go.microsoft.com/fwlink/?LinkId=164776)  
  
-   [Understanding forwarders](https://go.microsoft.com/fwlink/?LinkId=164778) (https://go.microsoft.com/fwlink/?LinkId=164778)  
  
## <a name="BKMK_RODCOptionsPage"></a>RODC 옵션  
다음 옵션을 읽기 전용 RODC (도메인 컨트롤러)를 설치 하는 경우 표시 됩니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_RODCOptions.gif)  
  
-   위임된 관리자 계정 RODC 하려면 관리자 권한이 로컬 얻을 수 있습니다. 이러한 사용자가 로컬 컴퓨터의 관리자가 그룹에 해당 권한으로 작동할 수 있습니다. 도메인 관리자 나 도메인 기본 관리자가 그룹의 회원 하지 않습니다. 이 옵션은 도메인 관리자 권한으로 제공 하지 않고 분기 사무실 관리에 위임 하는 데 유용 합니다. 관리 위임 구성 필요 하지 않습니다. For more information, see [Administrator Role Separation](https://technet.microsoft.com/library/cc753170(v=WS.10).aspx).  
  
-   암호 복제 정책 (ACL)는 액세스 제어 목록 역할을 합니다. RODC 암호 캐시 하도록 허용 하는 경우를 결정 합니다. RODC 인증 된 사용자 또는 컴퓨터 로그온 요청을 받은 후 확인 하는 경우 암호는 계정에 대 한 캐시 해야 하는 암호 복제 정책을 참조 합니다. 동일한 계정을 이후 로그온 더 효율적으로 수행할 수 있습니다.  
  
    암호 복제 정책 (PRP) 암호는 캐시 될 수 있도록 계정 및 계정 암호 캐시에서 거부 명시적으로 나열 됩니다. 캐시 될 수 있는 사용자와 컴퓨터 계정 목록이 RODC가 해당 계정에 대 한 암호 캐시 반드시 의미 하지 않습니다. 관리자는 RODC는 캐시 하는 모든 계정의 미리 지정 예를 들어 수 있습니다. 이런 방법이으로 RODC 해당 계정 인증할 수, 허브 사이트는 오프 라인 WAN에 연결 하는 경우에입니다.  
  
    사용자 또는 컴퓨터가 아닌 허용 (암묵적인 포함) 또는 암호 캐시 거부 된 수행 합니다. 이러한 사용자 또는 컴퓨터 없는 쓸 수 있는 도메인 컨트롤러에 대 한 액세스를 광고 DS 제공 리소스 또는 기능 자녀가 액세스할 수 없습니다. For more information about the PRP, see [Password Replication Policy](https://technet.microsoft.com/library/cc730883(v=ws.10).aspx). For more information about managing the PRP, see [Administering the Password Replication Policy](https://technet.microsoft.com/library/rodc-guidance-for-administering-the-password-replication-policy(v=ws.10).aspx).  
  
Rodc 설치에 대 한 자세한 내용은 참조 [Windows Server 2012 Active Directory 설치 Read-Only 도메인 컨트롤러 & #40; RODC & #41; & #40; 200 수준 & #41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md).  
  
## <a name="BKMK_AdditionalOptionsPage"></a>추가 옵션  
다음과 같은 옵션에 표시 되는 **추가 옵션** 새 도메인 만드는 경우 페이지:  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Child.gif)  
  
다음과 같은 옵션에 표시 되는 **추가 옵션** 기존 도메인에 추가 도메인 컨트롤러를 설치 하는 경우 페이지:  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Replica.gif)  
  
-   도메인 컨트롤러 복제 원본으로 지정 하거나 복제 원본으로 도메인 컨트롤러를 선택 하 고 마법사 허용할 수 있습니다.  
  
-   있습니다 하도록 선택할 수도 있는 도메인 컨트롤러를 사용 하 여 설치 미디어 (IFM) 옵션에서 설치를 사용 하 여 미디어를 백업 합니다. 설치 미디어를 로컬로 저장 되어 있는 경우는 **경로 미디어에서 설치** 옵션 파일 위치를 검색할 수 있습니다. 찾아보기 옵션을 원격 설치에 사용할 수 없습니다. 클릭 하면 **확인** 제공된 경로 사용할 미디어는 수 있도록 합니다. IFM 옵션으로 사용 되는 미디어 Ntdsutil.exe 또는 Windows Server 백업에서에서 만들어야 다른 기존 Windows Server 2012 컴퓨터만 사용 합니다. Windows Server 2012 도메인 컨트롤러에 대해 미디어를 만드는 Windows Server 2008 R2 또는 이전 운영 체제를 사용할 수 없습니다. 미디어를 SYSKEY로 보호를 확인 하는 동안 서버 관리자 이미지의 암호를 묻습니다.  
  
도메인을 만드는 방법에 대 한 자세한 내용은 참조 [새로운 Windows Server 2012 Active Directory 자녀 또는 밤나무 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md). 도메인 컨트롤러 기존 도메인에 추가 하는 방법에 대 한 자세한 내용은 참조 [복제 Windows Server 2012 도메인 컨트롤러에 기존 도메인 & #40; 설치 200 수준 & #41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
## <a name="BKMK_Paths"></a>경로  
다음과 같은 옵션에 표시 되는 **경로** 페이지 합니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_Paths.gif)  
  
-   **경로** SYSVOL 공유 및 페이지 데이터베이스 트랜잭션 로그가 광고 DS 데이터베이스의 기본 폴더 위치를 무시할 수 있습니다. 기본 위치는 항상 시스템 루트 %입니다.  
  
AD DS 데이터베이스 (NTDS.DIT), 파일 및 SYSVOL 로그온 합니다. 로컬 설치에 대 한 파일을 저장할 위치를 찾아볼 수 있습니다.  
  
## <a name="BKMK_AdprepCreds"></a>준비 옵션  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PreparationOptions.gif)  
  
하지 현재 로그온 adprep.exe 명령을 실행 하려면 충분 자격 증명으로 adprep AD DS 설치를 완료 하기 위해 실행 해야 하는 경우 실행 adprep.exe 자격 증명을 입력할 하 라는 메시지가 표시 됩니다. 기존 도메인 또는 숲을 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 추가 하려면 실행 Adprep 필요 합니다. 특히:  
  
-   Adprep /forestprep 기존 숲을 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 추가할 실행 해야 합니다. 이 명령은 엔터프라이즈 관리자 그룹, 스키마 관리 그룹 및 도메인 관리자 그룹 스키마 마스터 호스트 하는 도메인의의 구성원 하 여 실행 해야 합니다. 이 명령의 성공적으로 완료 명령을 실행 되는 컴퓨터와 숲은 스키마 마스터 사이 연결 여야 합니다.  
  
-   Adprep /domainprep 기존 도메인 Windows Server 2012를 실행 하는 첫 번째 도메인 컨트롤러를 추가할 실행 해야 합니다. 이 명령은 Windows Server 2012를 실행 하는 도메인 컨트롤러 설치 하는 도메인의 관리자 도메인 그룹의 회원 하 여 실행 해야 합니다. 성공적으로 완료이 명령의 명령을 실행 되는 컴퓨터 사이 infrastructure 마스터 도메인에 연결 여야 합니다.  
  
-   Adprep /rodcprep 첫 번째 RODC 기존 숲을 추가 하려면 실행 해야 합니다. 이 명령은 Enterprise 관리자 그룹의 회원 하 여 실행 해야 합니다. 이 명령의 성공적으로 완료 명령을 실행 되는 컴퓨터와 숲 각 응용 프로그램 파티션 infrastructure 마스터 사이 연결 여야 합니다.  
  
For more information about Adprep.exe, see [Adprep.exe integration](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep) and see [Running Adprep.exe](https://technet.microsoft.com/library/dd464018(WS.10).aspx).  
  
## <a name="BKMK_ViewInstallOptionsPage"></a>옵션을 검토  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_ReviewOptions.gif)  
  
-   **리뷰 옵션** 페이지를 설정을 확인 하 고 설치를 시작 하기 전에 사용자의 요구 사항을 충족 시키는 확인 수 있습니다. 마지막 기회를 서버 관리자를 사용 하 고 설치를 중단 되었습니다. 이 페이지 간단 하 게 검토 하 고 설정을 구성 계속 하기 전에 확인 수 있습니다.  
  
-   **리뷰 옵션** 서버 관리자의 페이지도 선택적 제공 **스크립트 보기** 단추를 현재 ADDSDeployment 구성을 하나의 Windows PowerShell 스크립트도 포함 유니코드 텍스트 파일을 만듭니다. 서버 관리자 그래픽 인터페이스 Windows PowerShell 배포 studio로 사용할 수 있습니다. Active Directory 도메인 서비스 구성 마법사를 사용 하 여 옵션 구성 구성, 내보내고 마법사 취소 합니다. 이 프로세스 추가 수정 또는 직접 사용에 대해 유효 하 고 구문이 샘플을 만듭니다.  
  
## <a name="BKMK_PrerqCheckPage"></a>필수 확인  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PrerequisitesCheck.gif)  
  
이 페이지에 표시 되는 경고 중 일부는 다음과 같습니다.  
  
-   Windows Server 2008 실행 하거나 나중에 안전 하 게 채널 세션을 설정할 때 약한 암호화 알고리즘 하지 못하는 "허용 암호화 알고리즘 Windows NT 4 호환"에 대 한 기본 설정 하는 도메인 컨트롤러 합니다. For more information about the potential impact and a workaround, see KB article [942564](https://support.microsoft.com/kb/942564).  
  
-   DNS 위임 생성 하거나 업데이트할 수 없습니다. 자세한 내용은 참조 [DNS 옵션](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)합니다.  
  
-   필수 검사 WMI 호출 필요합니다. 차단 된 방화벽 규칙 차단 되 RPC 서버 반환 경우 실패할 수 있기 사용할 수 없는 오류 합니다.  
  
AD DS 설치를 위해 수행 하는 특정 필수 검사에 대 한 자세한 내용은 참조 [필수 테스트](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_ADDSInstallPrerequisiteTests)합니다.  
  
## <a name="BKMK_Results"></a>결과  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_SMResultsBeta.gif)  
  
이 페이지에서 설치 결과 검토할 수 있습니다.  
  
마법사를 완료 한 후 해당 옵션을 선택 있는지 여부에 상관 없이 서버가 다시 시작 항상 설치에 성공 하면, 대상 서버를 다시 시작 하도록 선택할 수도 있습니다. 경우에 따라 설치 하기 전에 도메인에 가입 하지 된 대상 서버의 마법사를 완료 한 후 대상 서버 시스템 상태 서버 연결할 수 없는 네트워크에서 하거나 시스템 상태 원격 서버 관리에 대 한 권한을 가질 수 방지할 수 있습니다.  
  
대상 서버를 여기에 다시 시작 하지 못하는 경우 수동으로 다시 시작 해야 합니다. 도구를 Windows PowerShell shutdown.exe 등 수 없는 다시 시작 합니다. 원격 데스크톱 서비스에 로그인 하 고 대상 서버를 원격으로 종료를 사용할 수 있습니다.  
  
## <a name="BKMK_RemovalCredsPage"></a>역할 제거 자격 증명  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Credentials.gif)  
  
수준 내리기 옵션에서 구성는 **자격 증명** 페이지 합니다. 다음 목록에서 내릴는 데 필요한 자격 증명을 제공 합니다.  
  
-   추가 도메인 컨트롤러 내리기 도메인 관리자 자격 증명을 해야 합니다. 선택 **강제 도메인 컨트롤러의 제거** 도메인 컨트롤러에서 Active Directory 도메인 컨트롤러 개체 메타 데이터를 제거 하지 않고 내립니다.  
  
    > [!IMPORTANT]  
    > 도메인 컨트롤러 다른 도메인 컨트롤러에 연결할 수 없는 고 경우가 아니면이 옵션을 선택 하지 않으면 *적절 한 방법이* 해당 네트워크 문제를 해결 해야 합니다. 강제 수준 내리기 Active Directory에는 숲 속의 나머지 도메인 컨트롤러에서 고아 메타 데이터를 전송 됩니다. 또한, 모든 없다고 복제 변경 새 사용자 계정 또는 암호와 같은 해당 도메인 컨트롤러 손실 됩니다 렉. 고아 메타 데이터 AD DS, Exchange, SQL, 및 기타 소프트웨어에 대 한 Microsoft 고객 지원의 경우의 중요 한 비율로 근본 원인입니다. 도메인 컨트롤러 수준을 강제로 경우 하면 *해야* 수동으로 바로 정리 메타 데이터를 수행 합니다. For steps, review [Clean Up Server Metadata](https://technet.microsoft.com/library/cc816907(WS.10).aspx).  
  
-   이렇게 하면 도메인 자체 제거 엔터프라이즈 관리자 그룹 구성원 필요 도메인에 있는 마지막 도메인 컨트롤러 내리기 (마지막 도메인의 숲 속의 경우 이렇게 하면 제거 숲). 서버 관리자 현재 도메인 컨트롤러 도메인에 있는 마지막 도메인 컨트롤러 인지를 알려줍니다. 선택 **도메인에 있는 마지막 도메인 컨트롤러** 확인 도메인 컨트롤러는 도메인에 있는 마지막 도메인 컨트롤러 합니다.  
  
AD DS 제거에 대 한 자세한 내용은 참조 [Active Directory Domain Services (수준을 100) 제거](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) 및 [내리기 도메인 컨트롤러 및 도메인 & #40; 200 수준 & #41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_RemovalOptionsPage"></a>AD DS 제거 옵션 및 경고  
리뷰 옵션 페이지에서 사용 하는 데 도움이 필요한 경우 리뷰 옵션을 참조 하십시오.  
  
도메인 컨트롤러 호스트 글로벌 카탈로그 서버 또는 DNS 서버 역할 같은 추가 역할을 하는 경우 다음과 같은 경고 페이지가 나타납니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Warnings.gif)  
  
클릭 해야 **제거 된 계속** 는 추가 역할은 더 이상 사용할 수 클릭할 수 승인 하기 위해 **다음** 을 계속 합니다.  
  
도메인 컨트롤러의 제거를 강제로 도메인에 있는 다른 도메인 컨트롤러에 복제 하지 않은 모든 Active Directory 개체 변경 손실 됩니다. 또한 도메인 컨트롤러를 작업이 마스터 역할, 드, 또는 DNS 서버 역할 호스트, 도메인 및 숲 속의 중요 한 작업 다음과 같이 영향 수 있습니다. 모든 작업 마스터 역할 호스트 하는 도메인 컨트롤러를 제거 하기 전에 다른 도메인 컨트롤러 역할 이전 하려고 합니다. 역할을 전송할 수 없는 경우 먼저 Active Directory Domain Services이이 컴퓨터에서 제거 하 고를 사용 하 여 Ntdsutil.exe 역할을 중단 합니다. 여러분의 계획을; 역할을 중단 하는 도메인 컨트롤러에서 Ntdsutil를 사용 하 여 가능한 경우 같은 사이트에서 최근 복제 파트너는이 도메인 컨트롤러 사용 합니다. For more information about transferring and seizing operations master roles, see [article 255504](https://go.microsoft.com/fwlink/?LinkId=80395) in the Microsoft Knowledge Base. 마법사 도메인 컨트롤러 작업 마스터 역할 호스팅할 경우을 확인할 수 없는 경우에이 도메인 컨트롤러 작업 마스터 역할을 수행 하는지 여부를 확인 하려면 netdom.exe 명령을 실행 합니다.  
  
-   드: 사용자가 숲에서 도메인 로그온 로그인 하는 데 문제가 있을 수 있습니다. 드 서버를 제거 하기 전에이 숲 및 서비스가 사용자의 로그온 하는 사이트에 충분 한 드 서버가 되어 있는지 확인 합니다. 필요한 경우 다른 드 서버 지정 하 고에 새 정보는 클라이언트와 응용 프로그램을 업데이트 합니다.  
  
-   DNS 서버: DNS Active Directory 통합 영역에 저장 된 데이터를 모두 손실 됩니다. AD DS 제거한 후이 DNS 서버 이름 확인 Active Directory 통합 된 DNS 영역에 대 한 수행할 수 없습니다. 따라서 현재 참조이 DNS 서버 이름 확인을 위해의 IP 주소 새 DNS 서버를의 IP 주소를 사용 하는 모든 컴퓨터의 DNS 구성 업데이트 하는 것이 좋습니다.  
  
-   Infrastructure 마스터: 클라이언트 도메인에 있는 다른 도메인에 있는 개체를 찾는 데 문제가 있을 수 있습니다. 계속 하기 전에 infrastructure 마스터 역할은 전 세계 카탈로그 서버 도메인 컨트롤러에 전송 합니다.  
  
-   제거 마스터: 새 사용자 계정 만들기, 컴퓨터 계정 및 보안 그룹 문제가 있을 수 있습니다. 계속 하기 전에이 도메인 컨트롤러와 같은 도메인에 있는 도메인 컨트롤러에 RID 마스터 역할을 전송 합니다.  
  
-   주 도메인 컨트롤러 (PDC) 에뮬레이터: 업데이트를 그룹 정책 및 AD 비 DS 계정에 대 한 암호 재설정 등 PDC 에뮬레이터 하 여 수행 하는 작업 제대로 작동 하지 것입니다. 계속 하기 전에이 도메인 컨트롤러와 같은 도메인에 있는 도메인 컨트롤러에 PDC 에뮬레이터가 마스터 역할을 전송 합니다.  
  
-   스키마 마스터: 더 이상이 숲이에 대 한 스키마를 수정할 수 없습니다. 계속 하기 전에 숲 속의 루트 도메인에 있는 도메인 컨트롤러에 스키마 마스터 역할을 전송 합니다.  
  
-   도메인 이름 지정 마스터: 도메인을을 추가 하거나 제거 하는 도메인이이 숲 수 없습니다. 계속 하기 전에 도메인 마스터 숲에서 루트 도메인에 있는 도메인 컨트롤러 역할 명명 전송 합니다.  
  
-   모든 응용 프로그램 파티션이 Active Directory 도메인 컨트롤러에서 제거 됩니다. 도메인 컨트롤러 마지막 복제본 응용 프로그램 디렉터리 파티션 하나 이상의 제거 작업이 완료 되 면, 이러한 파티션을 더 이상 존재 합니다.  
  
도메인에 있는 마지막 도메인 컨트롤러의 Active Directory Domain Services을 제거한 후 도메인 더 이상 존재은 주의 해야 합니다.  
  
도메인 컨트롤러 DNS 서버 개최 된 DNS 영역에 위임 하는 경우, 다음 페이지 DNS 영역 위임에서 DNS 서버를 제거 하는 옵션을 제공 합니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_RemovalOptions.gif)  
  
AD DS 제거에 대 한 자세한 내용은 참조 [Active Directory Domain Services (수준을 100) 제거](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) 및 [내리기 도메인 컨트롤러 및 도메인 & #40; 200 수준 & #41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_NewAdminPwdPage"></a>새로운 관리자 암호  
**새 관리자 암호** 페이지 수준 내리기 완료 하 고 컴퓨터 구성원 서버 도메인 또는 작업 그룹 컴퓨터 되 면 내장 로컬 컴퓨터의 관리자 계정에 대 한 암호를 제공 하도록 요구 합니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_NewAdminPwd.gif)  
  
AD DS 제거에 대 한 자세한 내용은 참조 [Active Directory Domain Services (수준을 100) 제거](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) 및 [내리기 도메인 컨트롤러 및 도메인 & #40; 200 수준 & #41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).  
  
## <a name="BKMK_ConfirmRoleRemovalPage"></a>옵션을 검토  
**리뷰 옵션** 페이지 추가 내리는 자동화 수 있도록 Windows PowerShell 스크립트를 설정 하는 수준 내리기 내보낼 기회를 제공 합니다. 클릭 **내리기** AD DS 제거 합니다.  
  
![AD DS 설치](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_ReviewOptions.gif)  
  


