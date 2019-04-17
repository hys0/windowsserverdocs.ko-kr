---
title: "Windows Server Essentials 또는 Windows Server Essentials 환경 설치 및 구성"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8a2310b178663c6ca32a4e07d11656f1aaf2a11b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Windows Server Essentials 또는 Windows Server Essentials 환경 설치 및 구성

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

Windows Server Essentials은 소기업 최대 25 명의 사용자와 50 장치에 대 한 첫 번째 서버 적합 합니다. 조직에 최대 100 사용자 및 200 장치를 Windows Server Essentials 경험 역할이 설치 된 Windows Server 2012 r 2 이제 사용할 수 있습니다. 이 항목 모두 시나리오를 해결합니다.  
  
Windows Server Essentials 환경 (예: PC 및 원격 Web Access 백업)에서 사용할 수 있는 사용자를 Windows Server Essentials 잠금 및 Windows Server Essentials에 적용 되어 제한 없이 모든 기능을 이용할 수 있도록 Windows Server 2016에 역할입니다. 이 서버 역할 Windows Server Essentials에서 사용할 수 있는 되며 기본적으로 활성화 됩니다.
  
Windows Server Essentials 또는 Essentials 경험 역할을 설치 하기 전에 다음과 같은 제한 note 합니다.  
  
|Windows Server Essentials의 Windows Server Essentials 환경|Windows Server 2016에에서 Windows Server Essentials 환경
|----|----|
|-도메인 컨트롤러의 루트 숲와 도메인에 및 모든 FSMO 역할 유지 해야 합니다.<br /><br /> 그러나-기존 Active Directory 도메인 (가 마이그레이션을 수행 하기 위한 21 일 유예 기간이)는 환경에서 설치할 수 없습니다.|-하지 않아도 도메인 컨트롤러 기존 Active Directory 도메인 있는 환경에서 설치 되어 있습니다.<br /><br /> -Active Directory 도메인 존재 하지 않는 경우 서버의 루트 숲 및 도메인의 모든 FSMO 역할 유지 도메인 컨트롤러가와 역할을 설치 된 Active Directory 도메인 만듭니다.  
|단일 도메인에만 배포 수 있습니다.|단일 도메인에만 배포 수 있습니다.  
|읽기 전용 도메인 컨트롤러 도메인에 있을 수 없습니다.|읽기 전용 도메인 컨트롤러 도메인에 있을 수 없습니다.

> [!NOTE]
>  TechNet 평가 센터를 방문 하는 운영 체제의 버전 평가 다운로드 하려면:  
>   
>  [Windows Server 2016 다운로드](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)  
>   
>  [Windows Server Essentials 다운로드](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)
  
## <a name="installation-options"></a>설치 옵션  
 이 문서 설치 및 Windows Server Essentials 구성에 대 한 단계별 지침을 제공 합니다. 네트워크 환경에 따라 된 다음 설치 옵션을 사용할 수 있습니다.  
  
-    기본적으로 활성화 Windows Server Essentials 경험 역할) (와 Windows Server Essentials  
  
-    Windows Server Essentials 경험 역할이 설치와 Windows Server 2016  
 
|배포 환경|설명|관련된 섹션|  
|----------------------------|-----------------|---------------------|  
|새로운 Active Directory 환경|새 Active Directory 환경을 만드는 Windows Server Essentials를 설치할 수 있습니다.|[새 Active Directory 환경을 설정 하는 Windows Server Essentials 배포](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|  
|기존 Active Directory 환경|기존 Active Directory 환경에 Windows Server Essentials를 설치할 수 있습니다.|[기존 Active Directory 환경에 Windows Server Essentials 배포](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|  
|가상 환경|Windows Server Essentials 가상 컴퓨터도 배포할 수 있습니다.|[가상화 귀하의 환경](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|  
|자동된 배포|Windows Server Essentials의 배포 Windows PowerShell를 사용 하 여 자동 수 있습니다.|[설치 하 고 Windows PowerShell를 사용 하 여 Windows Server Essentials 구성](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|  
  
## <a name="before-you-begin"></a>시작 하기 전에  
 설치, 시작 하기 전에 다음과 같은 설명서를 검토 합니다.  
  
-   [Windows Server Essentials 제품 개요](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)  
  

-   [Windows Server Essentials의 시스템 요구 사항](../get-started/system-requirements.md)   

  
##  <a name="BKMK_NewAD"></a>새 Active Directory 환경을 설정 하는 Windows Server Essentials 배포  
 Windows Server Essentials Active Directory 환경 및 관련된 서버 기능을 신속 하 게 설정 하는 방법을 제공 합니다.  
  
###  <a name="BKMK_WSEDeploy"></a>Windows Server Essentials 배포  
 Windows Server Essentials을 사용 하는 경우 Windows Server Essentials 경험 이미 설정 되어 있습니다. 그러나 서버 구성 하려면 몇 가지 단계를 완료 해야 합니다.  
  
##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>Windows Server Essentials 실제 서버에서 구성 하려면  
  
1.  Windows 후 **시작** 페이지의 **구성 Windows Server Essentials 마법사** 바탕 화면에 표시 됩니다.  
  
2.  다음과 같이 마법사를 완료 하 고 지침을 따르세요.  
  
    1.  에 **Windows Server Essentials 구성** 페이지, 클릭 **다음**합니다.  
  
    2.  **시간 설정을**날짜, 시간 및 표준 시간대 올바른지 확인을 클릭 한 다음 **다음**합니다.  
  
    3.  **회사 정보**와 같은 회사 이름을 입력 **감사 합니다**을 차례로 클릭 하 고 **다음**합니다. 원하는 경우 도메인 내부 이름과 서버 변경할 수 있습니다.  
  
    4.  **네트워크 관리자 만들**, 새 관리자 계정 이름 및 암호를 입력 합니다.  
  
        > [!NOTE]
        >  기본 설정 사용 하지 마십시오 **관리자** 계정 이름 및 암호입니다.  
  
    5.  클릭 **구성**합니다.  
  
3.  구성 하는 동안 서버 여러 번 다시 시작 됩니다 고 구성을 완료 될 때까지 사용자 로그온 자동 됩니다. 이 프로세스 20 분 정도 걸립니다.  
  
4.  바탕 화면을 대시보드 서버를 시작 하려면 대시보드 아이콘을 클릭 합니다. 에 **Home** 페이지을 완료 하는 **시작** 작업에 나열 된는 **설치** 탭 합니다.  
  
 서버 구성을 완료 되 면 Windows Server Essentials 실행 하는 서버 도메인 컨트롤러도 설정 됩니다.  
  
###  <a name="BKMK_DeployWSERole"></a>Windows Server Essentials 경험 역할 Windows Server 2012 r 2 표준 및 데이터 센터에 배포  
 설정 하 고 다음 절차를 사용 하 여 Windows Server Essentials 경험 역할 Windows Server 2012 r 2 표준 또는 Windows Server 2012 R2 Datacenter 구성 관리자 서버를 사용할 수 있습니다.  
  
##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서는 Windows Server Essentials 경험 역할을 배포할  
  
1.  서버에 로컬 관리자 권한으로 로그온 합니다.  
  
2.  열기 **서버 관리자**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다.  
  
3.  **서버 역할 선택**는 **Windows Server Essentials 경험** 역할 합니다. 대화 상자에서 클릭 **기능 추가**을 차례로 클릭 하 고 **다음**합니다.  
  
4.  **기능**, 클릭 **다음**합니다.  
  
5.  리뷰는 **Windows Server Essentials 경험** 역할 설명 하 고 다음 클릭 **다음**합니다.  
  
6.  에 따라, 클릭는 페이지에서 **다음**, 확인 페이지, 클릭 한 다음 한 **설치**합니다.  
  
7.  설치가 완료 되 면 Windows Server Essentials 경험 서버 역할 서버 관리자도 나열 됩니다.  
  
8.  서버 관리자의 플래그 알림 영역에 플래그를 클릭 한 다음 클릭 **Windows Server Essentials 구성**합니다.  
  
9. (선택 사항) 서버 이름 필요한 경우 변경 합니다.  
  
    > [!IMPORTANT]
    >  서버 이름 Windows Server Essentials 구성한 경우 변경할 수 없습니다.  
  

10. 이전에 설명 된 대로 Windows Server Essentials 구성 하 고 마법사에 따라는 [배포 Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) 섹션.  

10. 이전에 설명 된 대로 Windows Server Essentials 구성 하 고 마법사에 따라는 [배포 Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) 섹션.  

  
##  <a name="BKMK_ExistingAD"></a>기존 Active Directory 환경에 Windows Server Essentials 배포  
 조직에는 기존 Active Directory 환경 있는 경우 Windows Server Essentials 배포할 수도 있습니다. 또한 Windows Server Essentials 도메인 컨트롤러 배포 하려면 선택할 수 있습니다.  
  
> [!IMPORTANT]
>  이 옵션은 Windows Server 2012 r 2 표준 또는 Windows Server 2012 R2 Datacenter Windows Server Essentials 경험 역할을 배포 하는 경우 사용할 수만 있습니다.  
  
#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>기존 Active Directory 환경에서 배포 하는 Windows Server Essentials  
  
1.  (선택 사항) 서버 이름 필요한 경우 변경 합니다.  
  
    > [!IMPORTANT]
    >  서버 이름 Windows Server Essentials 구성한 경우 변경할 수 없습니다.  
  
2.  다음과 같이 기존 도메인 Windows Server Essentials 실행 하는 서버에 참여 합니다.  
  
    1.  이 도메인 컨트롤러이 서버 하려는 경우 복제본 도메인 컨트롤러 서버를 설정 합니다.  
  
    2.  이 도메인 컨트롤러이 서버를 하지 않을 경우 Windows 기본 도구를 사용 하 여이 서버 도메인에 연결 합니다.  
  
3.  서버를 다시 시작 하 고 서버 도메인 관리자 권한으로 로그온 합니다.  
  
4.  서버 관리자를 열고 클릭 한 다음 **역할 추가 및 기능**합니다.  
  
5.  에 따라, 클릭는 페이지에서 **다음**합니다.  
  
6.  **서버 역할 선택**선택 **Windows Server Essentials 경험**합니다. 대화 상자에서 클릭 **기능 추가**을 차례로 클릭 하 고 **다음**합니다.  
  
7.  **기능**, 클릭 **다음**합니다.  
  
8.  리뷰는 **Windows Server Essentials 경험** 설명 및 클릭 **다음**합니다.  
  
9. 에 따라, 클릭는 페이지에서 **다음**, 확인 페이지, 클릭 한 다음 한 **설치**합니다.  
  
10. 설치가 완료 되 면 Windows Server Essentials 경험 서버 역할 서버 관리자도 나열 됩니다.  
  
11. 플래그 알림 영역에서 **서버 관리자**, 플래그를 클릭 한 다음 클릭 **Windows Server Essentials 구성**합니다.  
  
12. Windows Server Essentials 구성 하 고 마법사를 따릅니다. Active Directory 구성에 따라 알려 드립니다 도메인 컨트롤러에서 또는 도메인 구성원 Windows Server Essentials 여부를 구성 하 고 있습니다. 클릭 **구성** 구성을 시작 합니다. 구성 프로세스를 완료 하려면 10 분 정도 걸립니다.  
  
##  <a name="BKMK_VirtualWSE"></a>가상화 귀하의 환경  
  Windows Server Essentials, Windows Server 2012 r 2 표준, 및 Windows Server 2012 R2 Datacenter 가상 컴퓨터도 실행 될 수 있습니다. Hyper-v를 실행 하는 서버에 Hyper-v 관리 도구를 사용 하 여 가상 컴퓨터를 실행 합니다. 라이선스 관점에서 Windows Server Essentials Hyper-v 역할을 설정 하 고 귀하의 환경 가상화 수 있습니다. 라이선스를 사용 하면 Windows Server Essentials 실행 하는 다른 게스트 운영 체제를 설정할 수 있습니다. 시스템 공급자에 따라 "™의 구성 Windows Server Essentials 수 있도록 가상화 환경 원활 하 게 설정할 수 있습니다.  
  
#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>Windows Server Essentials 가상 컴퓨터도 배포  
  
1.  (시스템 구성에 따라 공급자"™ s), Windows 시작 페이지 후는 **시작 하기 전에** 페이지 가상 인스턴스를 실제 하드웨어에서 또는 Windows Server Essentials를 설정 하는 옵션을 제공 합니다. 사용 가능한이 옵션은 시스템 공급자가 미리 및 옵션을 모두 수 항상 사용할 수 없습니다. 가상 컴퓨터에서 Windows Server Essentials를 설치 하 **Windows Server Essentials 설치**선택 **가상 인스턴스를 설치**을 차례로 클릭 하 고 **구성**합니다.  
  
2.  마법사 약 5 분 찍습니다 가상 컴퓨터 프로 비전 됩니다.  
  

3.  이전에 설명 된 대로 Windows Server Essentials 다음으로 구성는 [배포 Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) 섹션.  

3.  이전에 설명 된 대로 Windows Server Essentials 다음으로 구성는 [배포 Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) 섹션.  

  
##  <a name="BKMK_PowerShell"></a>설치 하 고 Windows PowerShell를 사용 하 여 Windows Server Essentials 구성  
 Windows PowerShell cmdlet 사용 하 여 Windows Server Essentials의 설치를 자동화 수 있습니다.  
  
#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>Windows PowerShell를 사용 하 여 Windows Server Essentials를 설치 하려면  
  
1.  관리자 권한 명령 프롬프트에서 Windows PowerShell console을 엽니다.  
  
2.  다음 명령을 사용 하 여 Windows Server Essentials 경험 역할을 설치 합니다.  
  
    ```  
    Add-WindowsFeature ServerEssentialsRole  
    ```  
  
3.  실행 `Get-Help Start-WssConfigurationService`합니다.  
  
    1.  구성 Windows Server Essentials 도메인 컨트롤러를 설정 하려면 시작에서 다음 명령을 실행 합니다.  
  
        ```  
        Start-WssConfigurationService -CompanyName "ContosoTest" -DNSName "ContosoTest.com" -NetBiosName "ContosoTest" -ComputerName "YourServerName  œNewAdminCredential $cred  
        ```  
  
    2.  구성 기존 도메인 멤버와 Windows Server Essentials를 설정 하려면 시작에서 다음 명령을 실행 합니다. 이 작업을 수행 하려면 관리자 엔터프라이즈 그룹 및 Active Directory에 도메인 관리자 그룹의 속해야 합니다.  
  
        ```  
        Start-WssConfigurationService  œCredential <Your Credential>  
  
        ```  
  
4.  다음 명령을 사용 하 여의 설치 진행률을 모니터링 합니다.  
  
    -   진행률 표시줄에 표시 되는 설치 상태를 실행 `Get-WssConfigurationStatus  œShowProgress`합니다.  
  
    -   진행률 표시줄 하지 않고 바로 진행률, 실행 `Get-WssConfigurationStatus`합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server Essentials의 새로운 기능](../get-started/what-s-new.md)  
  
-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 시작](../get-started/get-started.md)
