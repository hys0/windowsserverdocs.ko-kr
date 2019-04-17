---
title: "1 단계: Windows Server Essentials 소스 서버 마이그레이션 준비"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 244c8a06-04c6-4863-8b52-974786455373
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 2efb1badde6d0ca11bc3b7526fdfb377d9f95d3f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="step-1-prepare-your-source-server-for-windows-server-essentials-migration"></a>1 단계: Windows Server Essentials 소스 서버 마이그레이션 준비

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 항목에서는 원본 서버 백업 평가 원본 서버 시스템 상태 최신 서비스 팩 및 수정 사항, 설치 하 고 네트워크 구성 확인 하는 방법을 설명 합니다.  
  
## <a name="to-prepare-for-migration"></a>마이그레이션에 대 한 준비를  
 다음 단계를 예비 하는 설정 및 원본 서버에 데이터 마이그레이션 성공적으로 대상 서버를 확인 합니다.  
  
1.  [원본 서버를 백업](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [최신 서비스 팩 설치](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [서비스 계정 설정으로 로그에서 삭제](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_DeleteSvcAcctSetting)  
  
4.  [원본 서버 상태 확인](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_EvaluateHealth)  
  
5.  [온라인 비즈니스 응용 프로그램을 마이그레이션하 옵션 만들기](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MigrateLOB)  
  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>원본 서버를 백업  
 원본 서버 마이그레이션 프로세스를 시작 하기 전에 백업 합니다. 마이그레이션 중 오류가 발생 하면 실수로 손실에서 데이터를 보호 백업는 것입니다.  
  
##### <a name="to-back-up-the-source-server"></a>원본 서버를 백업 하려면  
  
1.  다음 표에 있는 원본 서버의 전체 백업을 수행 하는 데 리소스를 중 하나를 사용 합니다.  
  
2.  백업 성공적으로 실행 있는지 확인 합니다. 백업 무결성을 테스트 임의 파일 백업에서 선택 하 고 다른 위치에 복원 복원된 된 파일은 원래 파일 동일 있는지 확인 합니다.  
  
   |제품|리소스|
   |---|---|
   |Windows 중소기업 Server 2003|[백업 및 복원 Windows 중소기업 Server 2003](https://msdn.microsoft.com/library/cc875809.aspx) 
   |Windows 중소기업 Server 2008|[백업 및 복원 Windows 중소기업 Server 2008 데이터](https://technet.microsoft.com/library/cc527505\(WS.10\).aspx)
   |Windows Server 2008 파운데이션|[백업 및 복구](https://technet.microsoft.com/library/cc754097\(WS.10\).aspx)  
   |Windows 중소기업 Server 2011 필수 패키지|[서버 백업 설정에 대해 자세히 알아보기](https://technet.microsoft.com/library/server-backup-support-1.aspx)
   |Windows 중소기업 Server 2011 표준|[서버 백업 관리](https://technet.microsoft.com/library/cc527488.aspx)  
   |Windows Server Essentials|[백업 관리 및 windows에서 Server Essentials 복원](https://technet.microsoft.com/library/jj713536.aspx)

###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>최신 서비스 팩 설치  
 마이그레이션 이전 원본 서버에 최신 업데이트 및 서비스 팩을 설치 해야 합니다.  
  
###  <a name="BKMK_DeleteSvcAcctSetting"></a>서비스 계정 설정으로 로그에서 삭제  
 Small Business Server 2003 Windows 또는 Windows Server 2003 마이그레이션하려 삭제는 **서비스 로그인** 계정에서 그룹 정책을 설정 합니다.  
  
##### <a name="to-delete-the-log-on-as-a-service-account-setting"></a>서비스 계정 설정으로 로그에서 삭제 하려면  
  
1.  열려면는 **그룹 정책 관리** 도구를 클릭 **시작**, 클릭 **제어판**, 클릭 **관리 도구**을 차례로 클릭 하 고 **그룹 정책 관리**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **기본 도메인 컨트롤러 정책**을 차례로 클릭 하 고 **편집**합니다.  
  
3.  로 이동 **정책 \ 사용자 구성할 보안 로컬 컴퓨터 권한 할당**합니다.  
  
4.  세부 정보 창에서 두 번 클릭 **서비스로 로그온**합니다.  
  
5.  지우기는 **이 정책 설정 정의** 확인란을 선택 합니다.  
  
6.  < Domainname\ > \\\localhost\SYSVOL\\ \scripts\SBS_LOGIN_SCRIPT.bat 삭제 합니다.  
  
###  <a name="BKMK_EvaluateHealth"></a>원본 서버 상태 확인  
 것이 마이그레이션을 시작 하기 전에 소스 Server의 상태를 확인 하는 것이 중요 합니다. 다음 절차를 사용 하 여 업데이트 현재 시스템 건강 보고서를 생성 하 고는 Windows Server 솔루션 가장 좋은 방법은 분석기 (BPA)을 실행할 수 있는지 확인 합니다.  
  
#### <a name="download-and-install-critical-and-security-updates"></a>다운로드 및 설치 중요 한 보안 업데이트  
 원본 서버 보증할 마이그레이션 성공적으로 보호 하는 네트워크 마이그레이션 프로세스 중에 설치 중요 한 보안 업데이트 합니다.  
  
###### <a name="to-check-for-the-latest-updates"></a>최신 업데이트를 확인 하려면  
  
1.  원본 서버에서 클릭 **시작**, 클릭 **모든 프로그램**을 차례로 클릭 하 고 **Windows 업데이트**합니다.  
  
2.  클릭 **업데이트 확인**합니다.  
  
3.  업데이트가 발견 되 면 클릭 **업데이트 설치**합니다.  
  
#### <a name="run-the-best-practices-analyzer"></a>모범 사례 분석기 실행  
 최상의 관행 분석기 (BPA) 마이그레이션 프로세스를 시작 하기 전에 서버, 네트워크 또는 도메인에 문제가 없는지 있는지 확인을 실행할 수 있습니다. BPA 다음 소스에서 구성 정보를 수집 합니다.  
  
-   Active Directory WMI(Windows Management Instrumentation) WMI)  
  
-   레지스트리  
  
-   정보 IIS (인터넷 서비스)  
  
###### <a name="to-use-the-bpa-to-analyze-your-source-server"></a>원본 서버를 분석 하 여 BPA 사용 하 여  
  
1.  다음 표에서 다운로드 하 고에서 원본 서버에 대 한 최상의 관행 분석기 (BPA)를 설치 수 있는 Microsoft 다운로드 센터 링크를 제공 합니다.  
  
   |원본 서버에서 실행 중인 경우|BPA 도구를 가져올 수 있습니다.|
   |---|---|
   |Windows SBS 2003|[Microsoft Windows 작은 Business Server 2003 모범 사례 분석기 웹 사이트](https://www.microsoft.com/download/details.aspx?id=5334)
   |Windows SBS 2008|[Microsoft Windows 작은 Business Server 2008 모범 사례 분석기 웹 사이트](https://www.microsoft.com/download/details.aspx?id=6231)  
   |Windows SBS 2011 필수 패키지 또는 Windows SBS 2011 표준|[Windows Server 솔루션 모범 사례 분석기 웹 사이트](https://www.microsoft.com/download/details.aspx?id=15556) 
   |Windows Server Essentials 또는 Windows Server 2012|서버 대시보드  
  
2.  클릭 하 고 다운로드가 완료 된 후 **시작**, 가리킨 **모든 프로그램**을 차례로 클릭 하 고 **SBS 가장 좋은 방법은 분석기 도구**합니다.  
  
    > [!NOTE]
    >  서버를 검색 하기 전에 업데이트를 확인 합니다.  
  
3.  탐색 창에서 클릭 **검사를 시작할**합니다.  
  
     원본 서버 Windows Server Essentials을 실행 중인 경우 다음을 수행 합니다.  
  
    1.  관리자로 서 대상 서버에에 로그인 하 고 대시보드 다음 엽니다.  
  
    2.  클릭 하 고 대시보드에서 **디바이스** 탭 합니다.  
  
    3.  에 <**서버** >**작업** 창 클릭 **모범 사례 분석기**합니다.  
  
4.  세부 정보 창에서 스캔 레이블 입력 한 다음 **검색 시작**합니다. 예를 들어 스캔 레이블이 검색 보고서의 이름 **SBS BPA 스캔 1 년 7 월 2013**합니다.  
  
5.  검색이 완료 된 후 클릭 **이 모범 사례 검색에 대 한 보고서를 볼**합니다.  
  
 BPA 서버 구성에 대 한 정보를 수집, 정보가 정확 하 고 다음 관리자가 정보와 심각도가 정렬 문제 목록을 표시 확인 합니다. 목록 각 문제에 설명 하 고 가능한 또는 권장 솔루션을 제공 합니다. 세 가지 보고서 종류 사용할 수 있습니다.  
  
|보고서 유형|설명
|-----------------|----------------- 
|목록 보고서|보고서는 차원 목록에 표시 됩니다. 
|나무 보고서|보고서는 계층 목록에 표시 됩니다.

설명 하 고 문제에 대 한 솔루션을 보려면 문제 보고서에을 클릭 합니다. 마이그레이션에 영향을 BPA 도구에 의해 보고 되는 문제를 모두 하지 하지만 많은 마이그레이션 성공적으로 되었는지 확인 하 여 문제를 해결 해야 합니다.  
  
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
  
###  <a name="BKMK_MigrateLOB"></a>온라인 비즈니스 응용 프로그램을 마이그레이션하 옵션 만들기  
 비즈니스 줄 (lob 기간 업무) 응용 프로그램이 중요 한 컴퓨터 응용 프로그램 사업에 매우 중요 합니다. LOB 응용 프로그램 관리, 계정, 공급 체인 포함 및 응용 프로그램 리소스 계획입니다.  
  
 마이그레이션 LOB 응용 프로그램 하려는 경우 각 응용 프로그램을 마이그레이션하는 데 적합 한 방법을 결정 LOB 응용 프로그램 공급자에 게 문의 합니다. 또한 대상 서버의 LOB 응용 프로그램을 설치 하는 데 사용 되는 미디어를 찾아 해야 합니다.  
  
> [!NOTE]
>  Windows 작은 Business Server 2011 Essentials SDK 개발 하는 데 사용 하는 경우 사용자 지정 된 시스템 건강 또는 경고 Add-in와 Windows Server Essentials 추가 기능을 사용 하 여 계속 하려면을 추가 기능을 업데이트 하 고 대상 서버에 배포 해야 합니다.  
  
  
### <a name="create-a-plan-to-migrate-email-hosted-on-windows-sbs-2011-windows-sbs-2008-and-windows-sbs-2003"></a>메일에 SBS 2011 Windows, Windows SBS 2008 및 Windows SBS 2003 호스트 마이그레이션하 옵션 만들기  
 Windows SBS 2011, Windows SBS 2008 및 Windows SBS 2003에서 메일을 통해 Microsoft Exchange Server 제공 됩니다. 그러나 Windows Server Essentials 받은 편지함 메일 서비스를 제공 하지 않습니다. Windows SBS 2011, Windows SBS 2008 또는 Windows SBS 2003을 실행 하는 서버 개최 된 s 회사 메일을 현재 사용 중인을 대체 온-프레미스 하 게 마이그레이션하 필요 하거나 솔루션 호스트 있습니다.  
  
> [!NOTE]
>  업데이트 하 고 원본 서버 마이그레이션에 대 한 준비를 후 마이그레이션 프로세스는 계속 하기 전에 백업 업데이트 서버를 만드는 것이 좋습니다.  
  
#### <a name="migrate-email-to-microsoft-office-365"></a>Microsoft Office 365에 메일 마이그레이션  
 도메인에 대 한 메일 솔루션으로 Microsoft Office 365를 사용 하 여 선택한 경우에 지침에 따라 [모든 사서함 Cutover Exchange 마이그레이션 클라우드로 마이그레이션을](http://help.outlook.com/140/ms.exch.ecp.emailmigrationwizardexchangelearnmore.aspx) 에 Office 365는 메일 마이그레이션 시작 합니다. Windows Server Essentials를 설치 하기 전에 전자 메일 마이그레이션을 완료 하는 것이 좋습니다.  
  
> [!NOTE]
>  온-프레미스 Exchange Server 원본 서버에서 제거 하는 단계는 Windows Server Essentials Office 365와 통합 하려는 경우 필수입니다. Office 365를 공용 폴더 Exchange Server를 마이그레이션해야 하는 방법에 대 한 정보에 대 한 블로그 게시물을 참조 [Microsoft Exchange 2013 공용 폴더 마이그레이션 스크립트 Office 365에 대 한](http://blogs.technet.com/b/fmustafa/archive/2013/04/11/microsoft-exchange-2013-public-folders-migration-scripts-for-office-365.aspx)합니다.  
>   
>  설치를 완료 한 후 켠 Windows Server Essentials의 Office 365 통합 기능을 실행 하 여는 **Microsoft Office 365와 통합** 작업입니다.  
  
> [!IMPORTANT]
>  Office 365 마이그레이션 도구 원본 서버에서 실행 되는 거래소 서버에 연결할 수 있도록 over 원본 서버의 HTTP RPC 설정 해야 합니다. Over HTTP RPC 활성화 하는 방법에 대 한 정보를 참조 하세요. [RPC (표준 또는 프리미엄) Small Business Server 2003에 처음으로 HTTP over 배포 하는 방법을](https://technet.microsoft.com/library/bb123622%28EXCHG.65%29.aspx)합니다. Over HTTP RPC 사용 하도록 설정한 후에 성공적으로 Office 365 마이그레이션 도구를 실행할 수 없다면을 보고 있는 **ValidPorts** 레지스트리의 찾아를 설정 하 고 원본 서버에 대 한 정식된 도메인 이름 (FQDN)가 표시 되는지 확인 합니다. FQDN 나열 되지 않으면 다음 예제를 사용 하 여이 수동으로 추가 합니다.  
>   
>  원격 합니다. *contoso*.com:6001-6002; 원격 합니다. *contoso*.com:6004 (교체 *contoso* 도메인 이름으로).  
  
#### <a name="migrate-email-to-another-on-premises-exchange-server"></a>메일 다른 온-프레미스 Exchange Server를 마이그레이션해야  
 다른 메일 마이그레이션 하는 방법에 대 한 정보 온-프레미스 Exchange Server에 대 한 참고 [Windows Server Essentials 온-프레미스 Exchange Server 부합](https://technet.microsoft.com/library/jj200172.aspx)합니다. Windows Server Essentials를 설치 하 고 원본 서버 내리기 하기 전에 전자 메일 마이그레이션 다음 완료 한 후 새 온-프레미스 Exchange Server를 설정 하는 것이 좋습니다.  
  
> [!NOTE]
>  Windows 작은 Business Server POP3 커넥터 Exchange Server 포함 되어 있습니다. 메일 데이터 다른 Exchange Server를 마이그레이션해야, 후 POP3 커넥터 기능을 더 이상 사용할 수 없습니다.  
  
> [!NOTE]
>  업데이트 하 고 원본 서버 마이그레이션에 대 한 준비를 후 마이그레이션 프로세스는 계속 하기 전에 백업 업데이트 서버를 만들어야 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 Windows Server essentials 마이그레이션에 대 한 소스 서버 준비한 합니다.  지금 이동 [2 단계: Windows Server Essentials 새 복제 도메인 컨트롤러도 설치](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)합니다.  

모든 단계를 참조 [Windows Server essentials 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

