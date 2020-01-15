---
title: Windows Server Essentials migration1에 대 한 원본 서버 준비
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5861ae9-77cb-4d37-b4c5-8f0757213385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d09ad4b66029c40c840ff5764fdaa2705b44bac2
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947442"
---
# <a name="prepare-your-source-server-for-windows-server-essentials-migration1"></a>Windows Server Essentials migration1에 대 한 원본 서버 준비

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

다음 예비 단계를 완료하여 원본 서버의 설정 및 데이터가 대상 서버로 마이그레이션되었는지 확인합니다.  
  
#### <a name="to-prepare-for-migration"></a>마이그레이션을 준비하려면  
  

1.  [원본 서버 백업](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [최신 서비스 팩 설치](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [원본 서버의 상태 평가](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [원본 서버에서 마이그레이션 준비 도구 실행](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [Lob (기간 업무) 응용 프로그램 마이그레이션 계획 만들기](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

1.  [원본 서버 백업](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [최신 서비스 팩 설치](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [원본 서버의 상태 평가](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [원본 서버에서 마이그레이션 준비 도구 실행](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [Lob (기간 업무) 응용 프로그램 마이그레이션 계획 만들기](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>원본 서버 백업  
 마이그레이션 프로세스를 시작하기 전에 원본 서버를 백업합니다. 백업을 생성하면 마이그레이션 중 복구할 수 없는 오류가 발생할 경우 데이터가 손실되는 것을 방지할 수 있습니다.  
  
##### <a name="to-back-up-the-source-server"></a>원본 서버를 백업하려면  
  
1.  원본 서버에 대해 전체 백업을 수행합니다. Windows Small Business Server 2011 Essentials를 백업 하는 방법에 대 한 자세한 내용은 [서버 백업 설정에 대 한 자세한](https://technet.microsoft.com/library/server-backup-support-1.aspx)정보를 참조 하세요.  
  
2.  백업이 성공적으로 실행되었는지 확인합니다. 백업의 무결성을 테스트하려면 백업에서 임의 파일을 선택하여 대체 위치에 복원한 후 복원된 파일이 원본 파일과 같은지 확인합니다.  
  
###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>최신 서비스 팩 설치  
 마이그레이션을 수행하려면 먼저 원본 서버에 최신 업데이트와 서비스 팩을 설치해야 합니다.  
  
###  <a name="BKMK_UseWindowsBestPracticeAnalyzer"></a>원본 서버의 상태 평가  
 마이그레이션을 시작하기 전에 원본 서버의 상태를 평가해야 합니다. 다음 절차를 사용하여 업데이트가 최신 상태인지 확인하고 시스템 상태 보고서를 생성하고 Windows Server Solutions BPA(모범 사례 분석기)를 실행합니다.  
  
#### <a name="download-and-install-critical-and-security-updates"></a>중요 업데이트와 보안 업데이트 다운로드 및 설치  
 원본 서버에 중요 업데이트와 보안 업데이트를 설치하면 마이그레이션 성공이 보장되며, 마이그레이션 프로세스 동안 네트워크를 보호할 수 있습니다.  
  
###### <a name="to-check-for-the-latest-updates"></a>최신 업데이트를 확인하려면  
  
1.  원본 서버에서 **시작**, **모든 프로그램**, **Windows 업데이트**를 차례로 클릭합니다.  
  
2.  **업데이트 확인**을 클릭합니다.  
  
3.  업데이트가 있으면 **업데이트 설치**를 클릭합니다.  
  
#### <a name="check-the-alert-viewer-for-critical-errors"></a>경고 뷰어의 중대한 오류 확인  
 대시보드에서 경고 뷰어를 확인하여 중대한 오류가 있는지 확인할 수 있습니다.  
  
#### <a name="run-the-windows-server-solutions-best-practices-analyzer"></a>Windows Server Solutions 모범 사례 분석기를 실행합니다.  
 Windows Server Solutions BPA(모범 사례 분석기)를 실행하여 마이그레이션 프로세스를 시작하기 전에 서버, 네트워크 또는 도메인에 문제가 없는지 확인합니다. BPA는 다음 원본에서 구성 정보를 수집합니다.  
  
-   Active Directory® WMI(Windows Management Instrumentation)  
  
-   레지스트리  
  
-   IIS(인터넷 정보 서비스) 메타베이스  
  
###### <a name="to-use-the-windows-server-solutions-bpa-to-analyze-your-source-server"></a>Windows Server Solutions BPA를 사용하여 원본 서버를 분석하려면  
  
1. Microsoft 다운로드 센터에서 [Windows Server Solutions 모범 사례 분석기](https://www.microsoft.com/download/details.aspx?id=15556)를 다운로드하고 설치하세요.  
  
2. 다운로드가 완료되면 **시작**을 클릭하고 **모든 프로그램**을 가리키고 나서 **SBS 모범 사례 분석기 도구**를 클릭합니다.  
  
   > [!NOTE]
   >  서버를 검색하기 전에 업데이트를 확인합니다.  
  
3. 탐색 창에서 **검색 시작**을 클릭합니다.  
  
4. 세부 정보 창에서 검색 레이블을 입력하고 **검색 시작**을 클릭합니다. 검사 레이블은 검사 보고서의 이름(예: **SBS BPA Scan 1Jul2012**)입니다.  
  
5. 검색이 완료되면 **이 Best Practices 검색 보고서 보기**를 클릭합니다.  
  
   서버 구성에 대한 정보를 수집하고 나서 Windows Server Solutions BPA에서는 정보가 올바른지 확인하고 관리자에게 심각도별로 정렬된 정보 및 문제 목록을 제공합니다. 목록에서는 각 문제를 설명하고 권장 사항 또는 가능한 해결 방법을 제공합니다. 세 가지 보고서 유형을 사용할 수 있습니다.  
  
|보고서 유형|설명|  
|-----------------|-----------------|  
|목록 보고서|일차원 목록의 보고서를 표시합니다.|  
|트리 보고서|계층형 목록의 보고서를 표시합니다.|  
|기타 보고서|실행 시간 로그와 같은 보고서를 표시합니다.|  
  
 문제에 대한 설명 및 해결 방법을 보려면 보고서에서 해당 문제를 클릭합니다. Windows SBS 2011 Essentials BPA에서 보고 하는 모든 문제가 마이그레이션에 영향을 주는 것은 아니지만 마이그레이션에 성공 하려면 가능한 한 많은 문제를 해결 해야 합니다.  
  
####  <a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a>원본 서버 시간을 외부 시간 원본과 동기화  
 원본 서버의 시간과 대상 서버의 시간은 5분 이내로 설정해야 하며 날짜 및 시간대는 두 서버에서 동일해야 합니다. 원본 서버가 가상 머신에서 실행 중인 경우, 호스트 서버의 날짜, 시간 및 시간대는 원본 서버 및 대상 서버의 설정과 일치해야 합니다. Windows Server Essentials가 성공적으로 설치 되도록 하려면 원본 서버 시간을 인터넷의 NTP (Network Time Protocol) 서버와 동기화 해야 합니다.  
  
###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>원본 서버 시간을 NTP 서버와 동기화하려면  
  
1.  도메인 관리자 계정과 암호를 사용하여 원본 서버에 로그온합니다.  
  
2.  **시작**, **실행**을 차례로 클릭하고 텍스트 상자에 **cmd** 를 입력한 다음 Enter 키를 누릅니다.  
  
3.  명령 프롬프트에 w32tm /config /syncfromflags:domhier /reliable:no /update를 입력하고 Enter 키를 누릅니다.  
  
4.  명령 프롬프트에 net stop w32time을 입력하고 Enter 키를 누릅니다.  
  
5.  명령 프롬프트에 net start w32time을 입력하고 Enter 키를 누릅니다.  
  
> [!IMPORTANT]
>  Windows Server Essentials를 설치 하는 동안 대상 서버에서 시간을 확인 하 고 필요한 경우 변경할 수 있습니다. 시간이 원본 서버에 설정된 시간의 5분 이내인지 확인합니다. 설치가 끝나면 대상 서버가 NTP와 동기화됩니다. 원본 서버를 포함하여 도메인에 가입된 모든 컴퓨터가 PDC(주 도메인 컨트롤러) 에뮬레이터 마스터 역할을 하는 대상 서버에 동기화됩니다.  
  
###  <a name="BKMK_MPT"></a>원본 서버에서 마이그레이션 준비 도구 실행  
 먼저 원본 서버에서 마이그레이션 준비 도구를 실행해야 마이그레이션 모드 설치를 수행할 수 있습니다. 이 도구는 Windows Server Essentials로 마이그레이션할 원본 서버와 도메인을 준비 하기 위해 설계 되었습니다.  
  
> [!IMPORTANT]
>  마이그레이션 준비 도구를 실행하기 전에 원본 서버를 백업해야 합니다. 마이그레이션 준비 도구가 스키마에 대해 수행하는 모든 변경 내용은 되돌릴 수 없습니다. 마이그레이션 중 문제가 발생하는 경우, 원본 서버를 마이그레이션 준비 도구를 실행하기 이전 상태로 되돌리는 유일한 방법은 시스템 백업에서 서버를 복원하는 것입니다.  
  
 마이그레이션 준비 도구를 실행하려면 Enterprise Admins 그룹, Schema Admins 그룹 및 Domain Admins 그룹의 구성원이어야 합니다.  
  
##### <a name="to-verify-that-you-have-the-appropriate-permissions-to-run-the-tool-on-the-source-server"></a>원본 서버에서 도구를 실행할 해당 권한이 있는지 확인하는 방법  
  
1. 원본 서버에서 **시작**, **관리 도구**, **Active Directory 사용자 및 컴퓨터**를 차례로 클릭합니다.  
  
2. 콘솔 트리에서 도메인을 클릭하여 확장하고 **사용자**를 클릭합니다.  
  
3. 마이그레이션에 사용 중인 관리자 계정을 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
4. **구성원 소속** 탭을 클릭한 후 **구성원 소속** 텍스트 상자에 Enterprise Admins, Schema Admins 및 Domain Admins이 나열되는지 확인합니다.  
  
5. 그룹이 나열되지 않는 경우, **추가**를 클릭한 후 나열되지 않은 각 그룹을 추가합니다.  
  
   > [!NOTE]
   > - Netlogon 서비스가 시작되지 않은 경우 권한 오류가 발생할 수 있습니다.  
   >   -   변경 내용을 적용하려면 서버에서 로그오프한 후 다시 로그온해야 합니다.  
  
    Windows Update 에이전트 최신 버전을 사용하여 서버 업데이트 프로세스가 올바르게 작동하는지 확인할 수 있습니다.  
  
   Windows Update 에이전트 최신 버전을 사용하여 서버 업데이트 프로세스가 올바르게 작동하는지 확인할 수 있습니다.  
  
   원본 서버에 Windows 업데이트 Agent를 설치 하려면 먼저 Windows PowerShell 2.0 및 Microsoft 기준선 구성 분석기 2.0를 설치 해야 합니다.  
  
-   Windows PowerShell 2.0을 다운로드 하 고 설치 하려면 Microsoft 기술 자료 [문서 968929](https://go.microsoft.com/fwlink/p/?LinkId=241483) 를 참조 하십시오.  
  
-   Microsoft 기준선 구성 분석기 2.0을 다운로드 하 고 설치 하려면 microsoft 다운로드 센터에서 [Microsoft 기준선 구성 분석기 2.0](https://go.microsoft.com/fwlink/p/?LinkId=241484) 를 참조 하세요.  
  
-   Windows 업데이트 에이전트의 최신 버전을 다운로드하고 설치하려면 Microsoft 기술 자료에서 [문서 949104](https://go.microsoft.com/fwlink/p/?LinkId=237493)를 참조하세요.  
  
##### <a name="to-install-and-run-the-migration-preparation-tool-on-the-source-server"></a>원본 서버에서 마이그레이션 준비 도구를 설치하려면  
  
1. 원본 서버의 DVD 드라이브에 Windows Server Essentials DVD1을 삽입 합니다.  
  
2. Windows 탐색기를 열고 DVD의 **\support\tools** 폴더로 이동하고 나서 **sourcetool.msi** 파일을 두 번 클릭합니다.  
  
   > [!NOTE]
   > - 서버에 마이그레이션 준비 도구가 이미 설치되어 있으면 **시작** 메뉴에서 도구를 실행합니다.  
   >   -   최상의 마이그레이션 준비를 했는지 확인하려면 항상 최신 업데이트 설치를 선택하는 것이 좋습니다.  
  
    마법사가 원본 서버에 마이그레이션 준비 도구를 설치합니다. 설치가 완료되면 마이그레이션 준비 도구가 자동으로 실행되고 최신 업데이트를 설치합니다.  
  
3. 마이그레이션 준비 도구에서 **백업이 있으며 계속할 준비가 되었습니다.** 를 선택한 후 **다음**을 클릭합니다.  
  
   > [!WARNING]
   >  핫픽스 설치와 관련 된 오류 메시지가 표시 되 면 방법 2: Microsoft 기술 자료 [문서 822798](https://go.microsoft.com/FWLink/p/?LinkID=118672) 에서 Catroot2 폴더 이름 바꾸기를 참조 하세요.  
  
    마이그레이션 준비 도구가 Active Directory 스키마를 확장함으로써 마이그레이션을 위해 원본 도메인을 준비합니다. 작업이 완료되면 **다음**을 클릭하여 계속하세요.  
  
4. 원본 도메인의 준비를 마친 후 마이그레이션 준비 도구가 2가지 유형의 잠재적 문제를 확인하기 위해 원본 서버를 검사합니다.  
  
   - **오류** 마이그레이션을 차단 하거나 마이그레이션을 실패할 수 있는 원본 서버에서 문제가 발생 했습니다. 오류 메시지의 지침을 따라 문제를 해결한 후 **다시 검사**를 클릭합니다.  
  
   - **경고** 마이그레이션 중에 기능 문제를 일으킬 수 있는 원본 서버에서 발견 된 문제입니다. 오류 메시지의 지침을 따라 마이그레이션 진행 전에 문제를 해결하는 것이 좋습니다.  
  
     모든 문제를 해결하거나 확인한 후 **다음**을 클릭합니다.  
  
5. 마이그레이션 준비 도구에서 **완료**를 클릭합니다.  
  
6. 마이그레이션 준비 도구가 완료 되 면 Windows Server Essentials로 마이그레이션을 시작 하기 전에 원본 서버를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.  
  
> [!NOTE]
>  대상 서버에 Windows Server Essentials를 설치한 후 2 주 이내에 원본 서버에서 마이그레이션 준비 도구를 성공적으로 실행 해야 합니다. 그렇지 않으면 대상 서버에 Windows Server Essentials 설치가 차단 됩니다. 이 경우 원본 서버에서 마이그레이션 준비 도구를 다시 실행해야 합니다.  
  
###  <a name="BKMK_PlanToMigrateLineOfBusinessApplications"></a>Lob (기간 업무) 응용 프로그램 마이그레이션 계획 만들기  
 LOB(기간 업무) 애플리케이션은 업무 수행에 필수적인 중요한 컴퓨터 애플리케이션입니다. LOB 애플리케이션에는 회계, 공급망 관리 및 리소스 계획 애플리케이션이 포함됩니다.  
  
 LOB(기간 업무) 애플리케이션을 마이그레이션하려는 경우 기간 업무 애플리케이션 공급자와 상의하여 애플리케이션 마이그레이션에 대한 적합한 방법을 결정합니다. 또한, 대상 서버에 LOB(기간 업무) 애플리케이션을 설치하는 데 사용되는 미디어 위치를 지정해야 합니다.  
  
> [!NOTE]
>  Windows Small Business Server 2011 Essentials SDK를 사용 하 여 사용자 지정 된 시스템 상태 또는 경고 추가 기능을 개발 했 고 Windows Server Essentials에서 추가 기능을 계속 사용 하려는 경우 추가 기능을 업데이트 하 고 대상 서버에 배포 해야 합니다.  
  
