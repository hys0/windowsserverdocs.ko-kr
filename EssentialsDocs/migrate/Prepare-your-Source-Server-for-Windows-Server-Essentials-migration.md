---
title: "Windows Server Essentials 원본 서버 준비 migration1"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 929c7506c78667646e429c4f28df7e5642c575ab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="prepare-your-source-server-for-windows-server-essentials-migration1"></a>Windows Server Essentials 원본 서버 준비 migration1

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

다음 단계를 예비 하는 설정 및 원본 서버에 데이터 마이그레이션 성공적으로 대상 서버를 확인 합니다.  
  
#### <a name="to-prepare-for-migration"></a>마이그레이션에 대 한 준비를  
  

1.  [원본 서버를 백업](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [최신 서비스 팩 설치](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [원본 서버 상태 확인](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [원본 서버의 마이그레이션 준비 도구 실행](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [온라인 비즈니스 응용 프로그램을 마이그레이션하 옵션 만들기](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

1.  [원본 서버를 백업](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [최신 서비스 팩 설치](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [원본 서버 상태 확인](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [원본 서버의 마이그레이션 준비 도구 실행](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [온라인 비즈니스 응용 프로그램을 마이그레이션하 옵션 만들기](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>원본 서버를 백업  
 원본 서버 마이그레이션 프로세스를 시작 하기 전에 백업 합니다. 마이그레이션 중 오류가 발생 하면 실수로 손실에서 데이터를 보호 백업는 것입니다.  
  
##### <a name="to-back-up-the-source-server"></a>원본 서버를 백업 하려면  
  
1.  전체 백업을 원본 서버를 수행 합니다. Windows 작은 Business Server 2011 Essentials 백업에 대 한 자세한 내용은 참조 [서버 백업 설정에 대 한 자세한](https://technet.microsoft.com/library/server-backup-support-1.aspx)합니다.  
  
2.  백업 성공적으로 실행 있는지 확인 합니다. 백업 무결성을 테스트 임의 파일 백업에서 선택 하 고 다른 위치에 복원 복원된 된 파일은 원래 파일 동일 있는지 확인 합니다.  
  
###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>최신 서비스 팩 설치  
 마이그레이션 이전 원본 서버에 최신 업데이트 및 서비스 팩을 설치 해야 합니다.  
  
###  <a name="BKMK_UseWindowsBestPracticeAnalyzer"></a>원본 서버 상태 확인  
 것이 마이그레이션을 시작 하기 전에 소스 Server의 상태를 확인 하는 것이 중요 합니다. 다음 절차를 사용 하 여 업데이트 현재 시스템 건강 보고서를 생성 하 고는 Windows Server 솔루션 가장 좋은 방법은 분석기 (BPA)을 실행할 수 있는지 확인 합니다.  
  
#### <a name="download-and-install-critical-and-security-updates"></a>다운로드 및 설치 중요 한 보안 업데이트  
 원본 서버 보증할 마이그레이션 성공적으로 보호 하는 네트워크 마이그레이션 프로세스 중에 설치 중요 한 보안 업데이트 합니다.  
  
###### <a name="to-check-for-the-latest-updates"></a>최신 업데이트를 확인 하려면  
  
1.  원본 서버에서 클릭 **시작**, 클릭 **모든 프로그램**을 차례로 클릭 하 고 **Windows 업데이트**합니다.  
  
2.  클릭 **업데이트 확인**합니다.  
  
3.  업데이트가 발견 되 면 클릭 **업데이트 설치**합니다.  
  
#### <a name="check-the-alert-viewer-for-critical-errors"></a>심각한 오류에 대 한 경고 뷰어 확인  
 모든 중요 한 오류에 대 한 대시보드에서 alert 뷰어를 확인할 수 있습니다.  
  
#### <a name="run-the-windows-server-solutions-best-practices-analyzer"></a>Windows Server 솔루션 모범 사례 분석기 실행  
 Windows Server 솔루션 최상의 관행 분석기 (BPA) 마이그레이션 프로세스를 시작 하기 전에 서버, 네트워크 또는 도메인에 문제가 없는지 있는지 확인을 실행할 수 있습니다. BPA 다음 소스에서 구성 정보를 수집 합니다.  
  
-   활성 Directory® WMI(Windows Management Instrumentation) WMI)  
  
-   레지스트리  
  
-   서비스 IIS (인터넷 정보) 메타 베이스  
  
###### <a name="to-use-the-windows-server-solutions-bpa-to-analyze-your-source-server"></a>Windows Server 솔루션 BPA 원본 서버 분석을 사용 하 여  
  
1.  다운로드 및 설치는 [Windows Server 솔루션 모범 사례 분석기](https://www.microsoft.com/en-us/download/details.aspx?id=15556) Microsoft 다운로드 센터에서 합니다.  
  
2.  클릭 하 고 다운로드가 완료 된 후 **시작**, 가리킨 **모든 프로그램**을 차례로 클릭 하 고 **SBS 가장 좋은 방법은 분석기 도구**합니다.  
  
    > [!NOTE]
    >  서버를 검색 하기 전에 업데이트를 확인 합니다.  
  
3.  탐색 창에서 클릭 **검사를 시작할**합니다.  
  
4.  세부 정보 창에서 스캔 레이블 입력 한 다음 **검색 시작**합니다. 예를 들어 스캔 레이블이 검색 보고서의 이름 **SBS BPA 스캔 1 년 7 월 2012**합니다.  
  
5.  검색이 완료 된 후 클릭 **이 모범 사례 검색에 대 한 보고서를 볼**합니다.  
  
 다음 서버 구성에 대 한 정보를 수집, Windows Server 솔루션 BPA 확인 정보가 정확 하 고 다음 관리자가 정보와 심각도가 정렬 문제 목록을 표시 합니다. 목록 각 문제에 설명 하 고 가능한 또는 권장 솔루션을 제공 합니다. 세 가지 보고서 종류 사용할 수 있습니다.  
  
|보고서 유형|설명|  
|-----------------|-----------------|  
|목록 보고서|보고서는 차원 목록에 표시 됩니다.|  
|나무 보고서|보고서는 계층 목록에 표시 됩니다.|  
|다른 보고서|실시간 로그 등 보고서가 표시 됩니다.|  
  
 설명 하 고 문제에 대 한 솔루션을 보려면 문제 보고서에을 클릭 합니다. 일부 Windows SBS 2011 Essentials BPA 하 여 보고 되는 문제, 마이그레이션에 영향을 있지만 마이그레이션 성공적으로 되었는지을 최대한 많은 문제를 해결 해야 합니다.  
  
####  <a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a>외부 시간 원본과 소스 서버에 동기화  
 원본 서버에서 시간 5 분 대상 서버에서 시간을 내으로 설정 되어 있어야 하며 날짜 및 표준 시간대 두 서버에서 동일한 되어야 합니다. 원본 서버 가상 컴퓨터에서 실행 하는 경우 날짜, 시간 및 표준 시간대 호스트 서버의 일치 해야 원본 서버 및 대상 서버 합니다. Windows Server Essentials 성공적으로 설치 되도록 하려면 한 소스 서버 시간 인터넷에 네트워크 시간 (NTP Protocol) 서버의을 동기화 해야 합니다.  
  
###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>원본 서버 시간 NTP 서버와 동기화  
  
1.  도메인 관리자 계정 및 암호를 사용 하 여 원본 서버에 로그인 합니다.  
  
2.  클릭 **시작**, 클릭 **실행**, 입력 **cmd** 텍스트 상자와 ENTER 키를 누릅니다.  
  
3.  명령 프롬프트에 입력 w32tm /config /syncfromflags: domhier /reliable: 없음 /update, 하 고 ENTER 키를 누릅니다.  
  
4.  명령 프롬프트 net 중지 w32time를 입력 한 다음 ENTER 키를 누릅니다.  
  
5.  명령 프롬프트 net 시작 w32time를 입력 한 다음 ENTER 키를 누릅니다.  
  
> [!IMPORTANT]
>  Windows Server Essentials 설치 하는 동안 필요한 경우 대상 서버에서 시간을 확인 하 고을 변경 하는 기회를 가지게. 원본 서버에 설정 된 시간 5 분 내에 있는지 확인 합니다. 설치가 완료 되 면 대상 서버 NTP와 동기화 합니다. 원본 서버를 포함 하 여 모든 도메인에 가입 컴퓨터 역할을 주 도메인 컨트롤러 (PDC) 에뮬레이터 마스터 가정 대상 서버로 동기화 됩니다.  
  
###  <a name="BKMK_MPT"></a>원본 서버의 마이그레이션 준비 도구 실행  
 원본 서버의 마이그레이션 준비 도구를 실행 하지 않고 마이그레이션 모드 설치를 수행할 수 없습니다. 이 도구를 Windows Server essentials 마이그레이션해야 원본 서버와 도메인 준비 하도록 설계 되었습니다.  
  
> [!IMPORTANT]
>  원본 서버 마이그레이션 준비 도구를 실행 하기 전에 백업 합니다. 마이그레이션 준비 도구 스키마를 하는 모든 변경 되돌릴 수 하지 않습니다. 마이그레이션 하는 동안 문제가 발생 하면 도구를 실행 하기 전의 소스 서버의 상태로 되돌릴 수 있는 유일한 방법은 서버 시스템 백업에서 복원 하는 합니다.  
  
 마이그레이션 준비 도구를 실행 하려면 Enterprise 관리자 그룹, 스키마 관리 그룹 및 도메인 관리자 그룹의 회원 이어야 합니다.  
  
##### <a name="to-verify-that-you-have-the-appropriate-permissions-to-run-the-tool-on-the-source-server"></a>원본 서버의 도구를 실행 하 고 적절 한 권한이 있는지 확인 하려면  
  
1.  원본 서버의 클릭 **시작**, 클릭 **관리 도구**을 차례로 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다.  
  
2.  콘솔 트리에서 도메인을 확장을 클릭 한 다음 클릭 **사용자**합니다.  
  
3.  관리자 계정 마이그레이션에 대 한 사용 하 고 클릭 한 다음에 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
4.  클릭 하 고 **소속** 탭을 선택한 다음 Enterprise 관리자, 스키마 관리 및 도메인 관리자에 나열 되어 있는지 확인는 **의 회원** 텍스트 상자 합니다.  
  
5.  클릭 하 고 그룹 나열 되지 않은 경우 **추가**, 다음 나열 되지 않은 각 그룹을 추가 합니다.  
  
    > [!NOTE]
    >  -   Netlogon 서비스 시작 되지 않은 경우 사용 권한 오류가 나타날 수 있습니다.  
    > -   로그 오프 한 변경 사항이 적용 되려면에 대 한 서버에 다시 로그인 해야 합니다.  
  
     서버 업데이트 프로세스 제대로 작동 하도록 하려면 최신 버전의 Windows 업데이트 에이전트 사용할 수 있습니다.  
  
 서버 업데이트 프로세스 제대로 작동 하도록 하려면 최신 버전의 Windows 업데이트 에이전트 사용할 수 있습니다.  
  
 Windows 업데이트 에이전트 원본 서버의 설치 하기 전에 2.0 Windows PowerShell 및 Microsoft 초기 구성 분석기 2.0를 설치 합니다.  
  
-   다운로드를 설치 하려면 Windows PowerShell 2.0 참조 [968929 문서](https://go.microsoft.com/fwlink/p/?LinkId=241483) Microsoft 기술 자료 합니다.  
  
-   다운로드를 설치 하려면 Microsoft 초기 구성 분석기 2.0 참조는 [Microsoft 초기 구성 분석기 2.0](https://go.microsoft.com/fwlink/p/?LinkId=241484) Microsoft 다운로드 센터에서 합니다.  
  
-   다운로드 하 고 설치 최신 버전의 Windows 업데이트 에이전트, 참조 [949104 문서](https://go.microsoft.com/fwlink/p/?LinkId=237493) Microsoft 기술 자료 합니다.  
  
##### <a name="to-install-and-run-the-migration-preparation-tool-on-the-source-server"></a>설치 하 고 원본 서버의 마이그레이션 준비 도구를 실행 하려면  
  
1.  Windows Server Essentials DVD1 원본 서버에서 DVD 드라이브에 삽입 합니다.  
  
2.  Windows 탐색기를 열고를 찾은 **\support\tools** DVD 및 다음 두 번 클릭 폴더는 **sourcetool.msi** 파일.  
  
    > [!NOTE]
    >  -   마이그레이션 준비 도구 서버에 이미 설치 되어 실행에서 도구는 **시작** 메뉴 합니다.  
    > -   최상의 가능한 후 마이그레이션 환경에 대 한 준비가 위해 최신 업데이트를 설치 하도록 항상 선택 했는지 좋습니다.  
  
     마법사 원본 서버의 마이그레이션 준비 도구를 설치합니다. 설치가 완료 되 면 마이그레이션 준비 도구 자동으로 실행 하 고 최신 업데이트를 설치 합니다.  
  
3.  마이그레이션 준비 도구에서 **백업 있고 진행할 준비가**을 차례로 클릭 하 고 **다음**합니다.  
  
    > [!WARNING]
    >  핫픽스 설치 관련 된 오류 메시지가 나타나면 참조 방법 2: Catroot2 폴더의 이름 바꾸기 [822798 문서](https://go.microsoft.com/FWLink/p/?LinkID=118672) Microsoft 기술 자료 합니다.  
  
     마이그레이션 준비 도구 마이그레이션에 대 한 Active Directory 스키마를 확장 하 여 원본 도메인을 준비 합니다. 클릭 하 고 작업이 완료 된 후 **다음** 을 계속 합니다.  
  
4.  원본 도메인, 그 후 마이그레이션 준비 도구 두 가지 유형의 발생할 수 있는 문제를 식별 하기 위해 소스 서버를 검색 합니다.  
  
    -   **오류** 마이그레이션 차단 하거나 실패 마이그레이션 발생할 수 있는 원본 서버의 문제를 찾지 합니다. 오류 메시지는 문제를 해결를 클릭 한 다음 지침에 따라 **다시 스캔**합니다.  
  
    -   **경고** 마이그레이션 중 기능 문제를 일으킬 수 있는 원본 서버의 문제를 찾지 합니다. 마이그레이션 진행 하기 전에 문제를 해결 하는 오류 메시지에 지침에 따라 하는 것이 가장 좋습니다.  
  
     문제를 해결 하거나 문제를 모두 확인 한 후 클릭 **다음**합니다.  
  
5.  마이그레이션 준비 도구 클릭 **완료**합니다.  
  
6.  마이그레이션 준비 도구 완료 되 면 Windows Server Essentials로 마이그레이션할 하기 전에 소스 서버를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.  
  
> [!NOTE]
>  성공적으로 실행 하는 마이그레이션 준비 도구 원본 서버의 대상 서버의 Windows Server Essentials 설치 2 주 내 완료 해야 합니다. 그렇지 않으면 대상 서버에 Windows Server Essentials의 설치를 차단 됩니다. 이 문제가 발생 하는 경우 원본 서버의 마이그레이션 준비 도구 다시 실행 해야 합니다.  
  
###  <a name="BKMK_PlanToMigrateLineOfBusinessApplications"></a>온라인 비즈니스 응용 프로그램을 마이그레이션하 옵션 만들기  
 비즈니스 줄 (lob 기간 업무) 응용 프로그램이 중요 한 컴퓨터 응용 프로그램 사업에 매우 중요 합니다. LOB 응용 프로그램 관리, 계정, 공급 체인 포함 및 응용 프로그램 리소스 계획입니다.  
  
 마이그레이션 LOB 응용 프로그램 하려는 경우 각 응용 프로그램을 마이그레이션하는 데 적합 한 방법을 결정 LOB 응용 프로그램 공급자에 게 문의 합니다. 또한 대상 서버의 LOB 응용 프로그램을 설치 하는 데 사용 되는 미디어를 찾아 해야 합니다.  
  
> [!NOTE]
>  Windows 작은 Business Server 2011 Essentials SDK 개발 하는 데 사용 하는 경우 사용자 지정 된 시스템 건강 또는 경고 Add-in와 Windows Server Essentials 추가 기능을 사용 하 여 계속 하려면을 추가 기능을 업데이트 하 고 대상 서버에 배포 해야 합니다.  
  
