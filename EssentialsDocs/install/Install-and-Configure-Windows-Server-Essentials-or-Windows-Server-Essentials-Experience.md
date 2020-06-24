---
title: Windows Server Essentials 또는 Windows Server Essentials Experience 설치 및 구성
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 46fd1ec7f76c6381ed9d725f5628a9a8fc760e9d
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267584"
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Windows Server Essentials 또는 Windows Server Essentials Experience 설치 및 구성

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials는 최대 25 명의 사용자와 50 장치를 갖춘 중소기업에 적합 한 첫 번째 서버입니다. 최대 100 명의 사용자 및 200 장치를 사용 하는 조직의 경우 이제 windows server Essentials Experience 역할이 설치 된 Windows Server 2012 R2를 사용할 수 있습니다. 이 항목에서는 이러한 두 가지 시나리오를 모두 설명합니다.  
  
Windows server Essentials Experience는 windows server essentials에서 적용 되는 잠금 및 제한 없이 Windows server Essentials에서 사용할 수 있는 모든 기능 (예: 원격 웹 액세스 및 PC 백업)을 활용할 수 있도록 하는 Windows Server 2016의 역할입니다. 이 서버 역할은 Windows Server Essentials 에서도 사용할 수 있으며 기본적으로 사용 하도록 설정 되어 있습니다.
  
Windows Server Essentials 또는 Essentials Experience 역할을 설치 하기 전에 다음 제한 사항에 유의 하세요.  
  
|Windows Server Essentials의 windows Server 필수 패키지 환경|Windows Server의 windows server 필수 패키지 환경 2016
|----|----|
|-포리스트 및 도메인의 루트에 있는 도메인 컨트롤러 여야 하며 모든 FSMO 역할을 보유 해야 합니다.<br /><br /> -기존 Active Directory 도메인을 사용 하는 환경에 설치할 수 없습니다. 그러나 마이그레이션을 수행 하는 데는 21 일의 유예 기간이 있습니다.|-기존 Active Directory 도메인을 사용 하는 환경에 설치 된 경우 도메인 컨트롤러가 될 필요는 없습니다.<br /><br /> -Active Directory 도메인이 없는 경우 역할을 설치 하면 Active Directory 도메인이 생성 되 고, 서버가 포리스트 및 도메인의 루트에서 모든 FSMO 역할을 보유 한 도메인 컨트롤러가 됩니다.  
|단일 도메인에만 배포할 수 있습니다.|단일 도메인에만 배포할 수 있습니다.  
|읽기 전용 도메인 컨트롤러는 도메인에 있을 수 없습니다.|읽기 전용 도메인 컨트롤러는 도메인에 있을 수 없습니다.

> [!NOTE]
>  운영 체제의 평가 버전을 다운로드하려면 TechNet Evaluation Center를 방문하세요.  
>   
>  [Windows Server 2016 다운로드](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)  
>   
>  [Windows Server Essentials 다운로드](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)
  
## <a name="installation-options"></a>설치 옵션  
 이 문서는 Windows Server Essentials를 설치 및 구성하는 단계별 지침을 제공합니다. 네트워크 환경에 따라 다음과 같은 설치 옵션을 사용할 수 있습니다.  
  
-    Windows Server Essentials (기본적으로 Windows Server Essentials Experience 역할이 사용 하도록 설정 됨)  
  
-    Windows server Essentials Experience 역할이 설치 된 windows Server 2016  
 
|배포 환경|Description|관련 섹션|  
|----------------------------|-----------------|---------------------|  
|새 Active Directory 환경|Windows Server Essentials를 설치하여 새 Active Directory 환경을 만들 수 있습니다.|[Windows Server Essentials를 배포하여 새 Active Directory 환경 설정](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|  
|기존 Active Directory 환경|기존 Active Directory 환경에 Windows Server Essentials를 설치할 수 있습니다.|[기존 Active Directory 환경에 Windows Server Essentials 배포](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|  
|가상 환경|Windows Server Essentials를 가상 머신으로 배포할 수 있습니다.|[환경 가상화](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|  
|자동화된 배포|Windows PowerShell을 사용하여 Windows Server Essentials의 배포를 자동화할 수 있습니다.|[Windows PowerShell을 사용하여 Windows Server Essentials 설치 및 구성](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|  
  
## <a name="before-you-begin"></a>시작하기 전에  
 설치를 시작하기 전에 다음 문서를 검토하세요.  
  
-   [Windows Server Essentials 제품 개요](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)  
  

-   [Windows Server Essentials의 시스템 요구 사항](../get-started/system-requirements.md)   

  
##  <a name="deploy-windows-server-essentials-to-set-up-a-new-active-directory-environment"></a><a name="BKMK_NewAD"></a>Windows Server Essentials를 배포 하 여 새 Active Directory 환경 설정  
 Windows Server Essentials는 Active Directory 환경 및 관련 서버 기능을 신속하게 설정할 수 있는 방법을 제공합니다.  
  
###  <a name="deploying-windows-server-essentials"></a><a name="BKMK_WSEDeploy"></a>Windows Server Essentials 배포  
 Windows Server Essentials를 사용 하는 경우 Windows Server Essentials Experience가 이미 사용 하도록 설정 되어 있습니다. 그러나 서버를 구성하는 일부 단계를 완료해야 합니다.  
  
##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>물리적 서버에서 Windows Server Essentials를 구성 하려면  
  
1. Windows **시작** 페이지가 표시된 후 **Windows Server Essentials 구성 마법사**가 바탕 화면에 표시됩니다.  
  
2. 다음과 같이 지침에 따라 마법사를 완료합니다.  
  
   1.  **Windows Server Essentials 구성** 페이지에서 **다음**을 클릭합니다.  
  
   2.  **시간 설정**에서 날짜, 시간 및 표준 시간대가 올바른지 확인한 후 **다음**을 클릭합니다.  
  
   3.  **회사 정보**에 해당 회사 이름(예: **Contoso,Ltd.**)을 입력한 후 **다음**을 클릭합니다. 필요에 따라 내부 도메인 이름 및 서버 이름을 변경할 수 있습니다.  
  
   4.  **네트워크 관리자 만들기**에 새 관리자 계정 이름 및 암호를 입력합니다.  
  
       > [!NOTE]
       >  기본 **관리자** 계정 이름 및 암호를 사용하지 마세요.  
  
   5.  **구성**을 클릭합니다.  
  
3. 구성 프로세스가 진행되는 동안 서버가 여러 번 다시 시작되고, 구성이 완료될 때까지 로그온은 자동입니다. 이 프로세스는 20분 정도 걸립니다.  
  
4. 바탕 화면에서 대시보드 아이콘을 클릭하여 서버 대시보드를 시작합니다. **홈** 페이지에서 **설치** 탭에 나열된 **시작** 작업을 완료합니다.  
  
   서버 구성을 완료한 후 Windows Server Essentials를 실행하는 서버가 도메인 컨트롤러로 설정됩니다.  
  
###  <a name="deploying-the-windows-server-essentials-experience-role-in-windows-server-2012-r2-standard-and-datacenter"></a><a name="BKMK_DeployWSERole"></a>Windows Server 2012 R2 Standard 및 Datacenter에 Windows Server 필수 패키지 환경 역할 배포  
 서버 관리자를 사용 하 여 다음 절차를 통해 windows server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter에서 Windows Server Essentials Experience 역할을 사용 하도록 설정 하 고 구성할 수 있습니다.  
  
##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>Windows Server 2012 R2에 Windows Server 필수 패키지 환경 역할을 배포하려면  
  
1.  서버에 로컬 관리자로 로그온합니다.  
  
2.  **서버 관리자**를 연 후 **역할 및 기능 추가**를 클릭합니다.  
  
3.  **서버 역할 선택**에서 **Windows Server 필수 패키지 환경** 역할을 선택합니다. 대화 상자에서 **기능 추가**를 클릭한 후 **다음**을 클릭합니다.  
  
4.  **기능**에서 **다음**을 클릭합니다.  
  
5.  **Windows Server 필수 패키지 환경** 역할 설명을 검토한 후 **다음**을 클릭합니다.  
  
6.  이어지는 페이지에서 **다음**을 클릭한 후 확인 페이지에서 **설치**를 클릭합니다.  
  
7.  설치가 완료 되 면 Windows Server 필수 패키지 환경이 서버 관리자에 서버 역할로 나열 되어야 합니다.  
  
8.  서버 관리자의 플래그 알림 영역에서 플래그를 클릭한 후 **Windows Server Essentials 구성**을 클릭합니다.  
  
9. (선택 사항) 필요한 경우 서버 이름을 변경합니다.  
  
    > [!IMPORTANT]
    >  Windows Server Essentials를 구성한 후에는 서버 이름을 변경할 수 없습니다.  
  

10. 마법사의 지침에 따라 windows [Server Essentials 배포](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) 섹션의 앞부분에서 설명한 대로 Windows server essentials를 구성 합니다.  

10. 마법사의 지침에 따라 windows [Server Essentials 배포](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) 섹션의 앞부분에서 설명한 대로 Windows server essentials를 구성 합니다.  

  
##  <a name="deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a><a name="BKMK_ExistingAD"></a>기존 Active Directory 환경에 Windows Server Essentials 배포  
 조직에 기존 Active Directory 환경이 이미 있는 경우에도 Windows Server Essentials를 배포할 수 있습니다. 또한 Windows Server Essentials를 도메인 컨트롤러로 배포할지 여부를 선택할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter에서 Windows Server 필수 패키지 환경 역할을 배포 하는 경우에만이 옵션을 사용할 수 있습니다.  
  
#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>기존 Active Directory 환경에 Windows Server Essentials를 배포하려면  
  
1.  (선택 사항) 필요한 경우 서버 이름을 변경합니다.  
  
    > [!IMPORTANT]
    >  Windows Server Essentials를 구성한 후에는 서버 이름을 변경할 수 없습니다.  
  
2.  다음과 같이 Windows Server Essentials를 실행하는 서버를 기존 도메인에 가입시킵니다.  
  
    1.  이 서버를 도메인 컨트롤러로 사용하려는 경우 서버를 복제본 도메인 컨트롤러로 설정합니다.  
  
    2.  이 서버를 도메인 컨트롤러로 사용하지 않으려는 경우 Windows 네이티브 도구를 사용하여 이 서버를 도메인에 가입시킵니다.  
  
3.  서버를 다시 시작하고 서버에 도메인 관리자로 로그온합니다.  
  
4.  서버 관리자를 연 후 **역할 및 기능 추가**를 클릭합니다.  
  
5.  이어지는 페이지에서 **다음**을 클릭합니다.  
  
6.  **서버 역할 선택**에서 **Windows Server 필수 패키지 환경**을 선택합니다. 대화 상자에서 **기능 추가**를 클릭한 후 **다음**을 클릭합니다.  
  
7.  **기능**에서 **다음**을 클릭합니다.  
  
8.  **Windows Server 필수 패키지 환경** 설명을 검토한 후 **다음**을 클릭합니다.  
  
9. 이어지는 페이지에서 **다음**을 클릭한 후 확인 페이지에서 **설치**를 클릭합니다.  
  
10. 설치가 완료 되 면 Windows Server Essentials Experience가 서버 관리자에 서버 역할로 나열 됩니다.  
  
11. **서버 관리자**의 플래그 알림 영역에서 플래그를 클릭한 후 **Windows Server Essentials 구성**을 클릭합니다.  
  
12. 마법사의 지침에 따라 Windows Server Essentials를 구성합니다. Active Directory 구성에 따라 Windows Server Essentials를 도메인 컨트롤러로 구성하는지 아니면 도메인 구성원으로 구성하는지에 대한 정보가 제공됩니다. **구성**을 클릭하여 구성을 시작합니다. 구성 프로세스를 완료하는 데 10분 정도 걸립니다.  
  
##  <a name="virtualize-your-environment"></a><a name="BKMK_VirtualWSE"></a>환경 가상화  
  Windows Server Essentials, Windows Server 2012 R2 Standard 및 Windows Server 2012 R2 Datacenter를 가상 컴퓨터로 실행할 수 있습니다. Hyper-V를 실행하는 서버에서 Hyper-V 관리 도구를 사용하여 가상 컴퓨터를 실행합니다. 라이선스 관점에서 Windows Server Essentials를 사용 하면 Hyper-v 역할을 설정 하 고 환경을 가상화 할 수 있습니다. 라이선스를 통해 Windows Server Essentials를 실행 하는 다른 게스트 운영 체제를 설정할 수 있습니다. 시스템 공급자의 구성에 따라 Windows Server Essentials를 사용 하면 가상화 된 환경을 원활 하 게 설정할 수 있습니다.  
  
#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>Windows Server Essentials를 가상 머신으로 배포하려면  
  
1.  Windows 시작 페이지가 표시 된 후 (시스템 공급자의 구성에 따라), **시작 하기 전에** 페이지에 Windows Server Essentials를 가상 인스턴스로 또는 실제 하드웨어에 설정 하는 옵션이 제공 됩니다. 이러한 옵션의 가용성은 시스템 공급자에 의해 미리 정의되며, 두 옵션을 모두 항상 사용할 수 있는 것은 아닙니다. Windows Server Essentials를 가상 컴퓨터로 설치 하려면 **Windows Server Essentials 설치**에서 **가상 인스턴스로 설치**를 선택한 다음 **구성**을 클릭 합니다.  
  
2.  마법사가 가상 머신을 프로비전하며, 이 작업은 5분 정도 걸립니다.

3.  그런 다음 windows server [Essentials 배포](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) 섹션의 앞부분에서 설명한 대로 Windows server essentials를 구성 합니다.  

  
##  <a name="install-and-configure-windows-server-essentials-by-using-windows-powershell"></a><a name="BKMK_PowerShell"></a>Windows PowerShell을 사용 하 여 Windows Server Essentials 설치 및 구성  
 Windows PowerShell cmdlet을 사용하여 Windows Server Essentials의 설치를 자동화할 수 있습니다.  
  
#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 Windows Server Essentials를 설치하려면  
  
1.  관리자 권한 명령 프롬프트에서 Windows PowerShell 콘솔을 엽니다.  
  
2.  다음 명령을 사용 하 여 Windows Server 필수 패키지 환경 역할을 설치 합니다.  
  
    ```  
    Add-WindowsFeature ServerEssentialsRole  
    ```  
  
3.  `Get-Help Start-WssConfigurationService`을 실행합니다.  
  
    1.  Windows Server Essentials를 도메인 컨트롤러로 설정하는 구성을 시작하려면 다음 명령을 실행합니다.  
  
        ```  
        Start-WssConfigurationService -CompanyName "ContosoTest" -DNSName "ContosoTest.com" -NetBiosName "ContosoTest" -ComputerName "YourServerName  œNewAdminCredential $cred  
        ```  
  
    2.  Windows Server Essentials를 기존 도메인 구성원으로 설정하는 구성을 시작하려면 다음 명령을 실행합니다. 이 작업을 수행하려면 Active Directory에서 엔터프라이즈 관리자 그룹 및 도메인 관리자 그룹의 구성원이어야 합니다.  
  
        ```  
        Start-WssConfigurationService  œCredential <Your Credential>  
  
        ```  
  
4.  다음 명령을 사용하여 설치 진행률을 모니터링합니다.  
  
    -   설치 상태를 진행률 표시줄에 표시하려면 `Get-WssConfigurationStatus  œShowProgress`를 실행합니다.  
  
    -   진행률 표시줄 없이 즉각적인 진행률을 가져오려면 `Get-WssConfigurationStatus`를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
  
-   [Windows Server Essentials의 새로운 기능](../get-started/what-s-new.md)  
  
-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 시작 하기](../get-started/get-started.md)
