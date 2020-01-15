---
title: '1단계: Windows Server Essentials 마이그레이션을 위한 원본 서버 준비'
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.openlocfilehash: f95ebfec13c2ec1f374c60f48d5f8af6c4b22324
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947397"
---
# <a name="step-1-prepare-your-source-server-for-windows-server-essentials-migration"></a>1단계: Windows Server Essentials 마이그레이션을 위한 원본 서버 준비

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 항목에서는 원본 서버를 백업하고, 원본 서버 시스템 상태를 평가하며, 최신 서비스 팩 및 수정 프로그램을 설치하고, 네트워크 구성을 확인하는 방법을 설명합니다.  

## <a name="to-prepare-for-migration"></a>마이그레이션을 준비하려면  
 다음 예비 단계를 완료하여 원본 서버의 설정 및 데이터가 대상 서버로 마이그레이션되었는지 확인합니다.  

1.  [원본 서버 백업](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  

2.  [최신 서비스 팩 설치](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  

3.  [서비스로 로그온 계정 설정을 삭제 합니다.](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_DeleteSvcAcctSetting)  

4.  [원본 서버의 상태 평가](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_EvaluateHealth)  

5.  [Lob (기간 업무) 응용 프로그램 마이그레이션 계획 만들기](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MigrateLOB)  

###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>원본 서버 백업  
 마이그레이션 프로세스를 시작하기 전에 원본 서버를 백업합니다. 백업을 생성하면 마이그레이션 중 복구할 수 없는 오류가 발생할 경우 데이터가 손실되는 것을 방지할 수 있습니다.  

##### <a name="to-back-up-the-source-server"></a>원본 서버를 백업하려면  

1. 다음 표의 리소스 중 하나를 사용하여 원본 서버의 전체 백업 수행에 대한 지침에 따릅니다.  

2. 백업이 성공적으로 실행되었는지 확인합니다. 백업의 무결성을 테스트하려면 백업에서 임의 파일을 선택하여 대체 위치에 복원한 후 복원된 파일이 원본 파일과 같은지 확인합니다.  

   |제품|리소스|
   |---|---|
   |Windows Small Business Server 2003|[Windows Small Business Server 2003 백업 및 복원](https://msdn.microsoft.com/library/cc875809.aspx) 
   |Windows Small Business Server 2008|[Windows Small Business Server 2008에서 데이터 백업 및 복원](https://technet.microsoft.com/library/cc527505\(WS.10\).aspx)
   |Windows Server 2008 Foundation|[백업 및 복구](https://technet.microsoft.com/library/cc754097\(WS.10\).aspx)  
   |Windows Small Business Server 2011 Essentials|[서버 백업 설정에 대 한 자세한 정보](https://technet.microsoft.com/library/server-backup-support-1.aspx)
   |Windows Small Business Server 2011 Standard|[서버 백업 관리](https://technet.microsoft.com/library/cc527488.aspx)  
   |Windows Server Essentials|[Windows Server Essentials의 백업 및 복원 관리](https://technet.microsoft.com/library/jj713536.aspx)

###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>최신 서비스 팩 설치  
 마이그레이션을 수행하려면 먼저 원본 서버에 최신 업데이트와 서비스 팩을 설치해야 합니다.  

###  <a name="BKMK_DeleteSvcAcctSetting"></a>서비스로 로그온 계정 설정을 삭제 합니다.  
 Windows Small Business Server 2003 또는 Windows Server 2003에서 마이그레이션하는 경우 그룹 정책에서 **서비스로 로그온** 계정 설정을 삭제합니다.  

##### <a name="to-delete-the-log-on-as-a-service-account-setting"></a>서비스로 로그온 계정 설정을 삭제 하려면  

1.  **그룹 정책 관리** 도구를 열려면 **시작**, **제어판**, **관리 도구**및 **그룹 정책 관리**를 차례로 클릭합니다.  

2.  **기본 도메인 컨트롤러 정책**을 마우스 오른쪽 단추로 클릭한 후 **편집**을 클릭합니다.  

3.  **컴퓨터 구성\Windows 설정\보안 설정\로컬 정책\사용자 권한 할당**으로 이동합니다.  

4.  세부 정보 창에서 **서비스로 로그온**을 두 번 클릭합니다.  

5.  **이 정책 설정 정의** 확인란을 선택 취소합니다.  

6.  \\\localhost\SYSVOL\\< domainname\>\scripts\ SBS_LOGIN_SCRIPT를 삭제 합니다.  

###  <a name="BKMK_EvaluateHealth"></a>원본 서버의 상태 평가  
 마이그레이션을 시작하기 전에 원본 서버의 상태를 평가해야 합니다. 다음 절차를 사용하여 업데이트가 최신 상태인지 확인하고 시스템 상태 보고서를 생성하고 Windows Server Solutions BPA(모범 사례 분석기)를 실행합니다.  

#### <a name="download-and-install-critical-and-security-updates"></a>중요 업데이트와 보안 업데이트 다운로드 및 설치  
 원본 서버에 중요 업데이트와 보안 업데이트를 설치하면 마이그레이션 성공이 보장되며, 마이그레이션 프로세스 동안 네트워크를 보호할 수 있습니다.  

###### <a name="to-check-for-the-latest-updates"></a>최신 업데이트를 확인하려면  

1.  원본 서버에서 **시작**, **모든 프로그램**, **Windows 업데이트**를 차례로 클릭합니다.  

2.  **업데이트 확인**을 클릭합니다.  

3.  업데이트가 있으면 **업데이트 설치**를 클릭합니다.  

#### <a name="run-the-best-practices-analyzer"></a>모범 사례 분석기 실행  
 마이그레이션 프로세스를 시작하기 전에 BPA(모범 사례 분석기)를 실행하여 서버, 네트워크 또는 도메인에 문제가 없는지 확인할 수 있습니다. BPA는 다음 원본에서 구성 정보를 수집합니다.  

-   Active Directory WMI(Windows Management Instrumentation)  

-   레지스트리  

-   IIS(인터넷 정보 서비스)  

###### <a name="to-use-the-bpa-to-analyze-your-source-server"></a>BPA를 사용하여 원본 서버를 분석하려면  

1. 다음 표에는 원본 서버용 BPA(모범 사례 분석기)를 다운로드 및 설치할 수 있는 Microsoft 다운로드 센터 링크가 표시되어 있습니다.  


   |             원본 서버에서를 실행 하는 경우             |                                                     다음에서 BPA 도구를 가져올 수 있습니다.                                                      |
   |----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
   |                     Windows SBS 2003                     | [Microsoft Windows Small Business Server 2003 모범 사례 분석기 웹 사이트](https://www.microsoft.com/download/details.aspx?id=5334) |
   |                     Windows SBS 2008                     | [Microsoft Windows Small Business Server 2008 모범 사례 분석기 웹 사이트](https://www.microsoft.com/download/details.aspx?id=6231) |
   | Windows SBS 2011 Essentials 또는 Windows SBS 2011 Standard |          [웹 사이트 모범 사례 분석기 Windows Server Solutions](https://www.microsoft.com/download/details.aspx?id=15556)           |
   |     Windows Server Essentials 또는 Windows Server 2012     |                                                          서버 대시보드                                                           |


2. 다운로드가 완료되면 **시작**을 클릭하고 **모든 프로그램**을 가리키고 나서 **SBS 모범 사례 분석기 도구**를 클릭합니다.  

   > [!NOTE]
   >  서버를 검색하기 전에 업데이트를 확인합니다.  

3. 탐색 창에서 **검색 시작**을 클릭합니다.  

    원본 서버에서 Windows Server Essentials를 실행 하는 경우 다음을 수행 합니다.  

   1.  관리자로 원본 서버에 로그온하고 대시보드를 엽니다.  

   2.  대시보드에서 **디바이스** 탭을 클릭합니다.  

   3.  **Server** >**작업** 창에서 **모범 사례 분석기**를 클릭 합니다.  

4. 세부 정보 창에서 검색 레이블을 입력하고 **검색 시작**을 클릭합니다. 검색 레이블은 검색 보고서의 이름(예: **SBS BPA Scan 1Jul2013**)입니다.  

5. 검색이 완료되면 **이 Best Practices 검색 보고서 보기**를 클릭합니다.  

   BPA 도구는 서버 구성에 대한 정보를 수집한 후 정보가 올바른지 확인하고, 관리자에게 심각도별로 정렬된 정보 및 문제 목록을 제공합니다. 목록에서는 각 문제를 설명하고 권장 사항 또는 가능한 해결 방법을 제공합니다. 세 가지 보고서 유형을 사용할 수 있습니다.  

|보고서 유형|설명
|-----------------|----------------- 
|목록 보고서|일차원 목록의 보고서를 표시합니다. 
|트리 보고서|계층형 목록의 보고서를 표시합니다.

문제에 대한 설명 및 해결 방법을 보려면 보고서에서 해당 문제를 클릭합니다. BPA 도구에서 보고하는 모든 문제가 마이그레이션에 영향을 주는 것은 아니지만 마이그레이션에 성공하려면 가능한 한 많은 문제를 해결해야 합니다.  

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

###  <a name="BKMK_MigrateLOB"></a>Lob (기간 업무) 응용 프로그램 마이그레이션 계획 만들기  
 LOB(기간 업무) 애플리케이션은 업무 수행에 필수적인 중요한 컴퓨터 애플리케이션입니다. LOB 애플리케이션에는 회계, 공급망 관리 및 리소스 계획 애플리케이션이 포함됩니다.  

 LOB(기간 업무) 애플리케이션을 마이그레이션하려는 경우 기간 업무 애플리케이션 공급자와 상의하여 애플리케이션 마이그레이션에 대한 적합한 방법을 결정합니다. 또한, 대상 서버에 LOB(기간 업무) 애플리케이션을 설치하는 데 사용되는 미디어 위치를 지정해야 합니다.  

> [!NOTE]
>  Windows Small Business Server 2011 Essentials SDK를 사용 하 여 사용자 지정 된 시스템 상태 또는 경고 추가 기능을 개발 했 고 Windows Server Essentials에서 추가 기능을 계속 사용 하려는 경우 추가 기능을 업데이트 하 고 대상 서버에 배포 해야 합니다.  


### <a name="create-a-plan-to-migrate-email-hosted-on-windows-sbs-2011-windows-sbs-2008-and-windows-sbs-2003"></a>Windows SBS 2011, Windows SBS 2008 및 Windows SBS 2003에서 호스트되는 메일 마이그레이션 계획 만들기  
 Windows SBS 2011, Windows SBS 2008 및 Windows SBS 2003에서 메일은 Microsoft Exchange Server를 통해 제공됩니다. 그러나 Windows Server Essentials에서는 받은 편지함 전자 메일 서비스를 제공 하지 않습니다. 현재 Windows SBS 2011, Windows SBS 2008 또는 Windows SBS 2003을 실행 하는 서버를 사용 하 여 회사 메일을 호스트 하는 경우 대체 온-프레미스 또는 호스팅 솔루션으로 마이그레이션해야 합니다.  

> [!NOTE]
>  마이그레이션을 위한 원본 서버 업데이트 및 준비가 끝났으면 마이그레이션 과정을 시작하기 전에 업데이트된 원본 서버를 백업하는 것이 좋습니다.  

#### <a name="migrate-email-to-microsoft-office-365"></a>Microsoft Office 365로 메일 마이그레이션  
 Microsoft Office 365를 도메인의 메일 솔루션으로 사용하기로 선택한 경우 [컷오버 Exchange 마이그레이션을 사용하여 클라우드로 모든 사서함 마이그레이션](https://help.outlook.com/140/ms.exch.ecp.emailmigrationwizardexchangelearnmore.aspx) 의 지침에 따라 Office 365로의 메일 마이그레이션을 시작합니다. Windows Server Essentials를 설치 하기 전에 전자 메일 마이그레이션을 완료 하는 것이 좋습니다.  

> [!NOTE]
>  원본 서버에서 온-프레미스 Exchange Server를 제거 하는 단계는 Windows Server Essentials와 Office 365을 통합 하려는 경우에 필수입니다. Exchange Server 공용 폴더를 Office 365로 마이그레이션하는 방법에 대한 자세한 내용은 블로그 게시물 [Office 365에 대한 Microsoft Exchange 2013 공용 폴더 마이그레이션 스크립트](https://blogs.technet.com/b/fmustafa/archive/2013/04/11/microsoft-exchange-2013-public-folders-migration-scripts-for-office-365.aspx)(영문)를 참조하세요.  
>   
>  설치를 완료 한 후 **Microsoft Office 365와 통합** 작업을 실행 하 여 Windows Server Essentials에서 Office 365 통합 기능을 설정 해야 합니다.  

> [!IMPORTANT]
>  Office 365 마이그레이션 도구가 원본 서버에서 실행되는 Exchange Server에 연결할 수 있도록 하려면 원본 서버에서 RPC over HTTP를 사용하도록 설정해야 합니다. RPC over HTTP를 사용하도록 설정하는 방법에 대한 자세한 내용은 [Small Business Server 2003(Standard 또는 Premium)에 처음으로 RPC over HTTP를 배포하는 방법](https://technet.microsoft.com/library/bb123622%28EXCHG.65%29.aspx)을 참조하세요. RPC over HTTP를 사용하도록 설정한 후 Office 365 마이그레이션 도구를 실행할 수 없는 경우 HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy 레지스트리의 **ValidPorts** 설정에 원본 서버의 FQDN(정규화된 도메인 이름)이 나열되는지 확인하세요. FQDN이 나열되지 않으면 다음 예제를 사용하여 수동으로 추가합니다.  
>   
>  remote. *contoso*.com:6001-6002;remote. *contoso*.com:6004( *contoso* 를 도메인 이름으로 바꿈)  

#### <a name="migrate-email-to-another-on-premises-exchange-server"></a>다른 온-프레미스 Exchange Server로 메일 마이그레이션  
 다른 온-프레미스 Exchange Server로 메일을 마이그레이션하는 방법에 대 한 자세한 내용은 [온-프레미스 Exchange server와 Windows Server Essentials 통합](https://technet.microsoft.com/library/jj200172.aspx)을 참조 하세요. Windows Server Essentials를 설치한 후 새 온-프레미스 Exchange Server를 설정한 다음 원본 서버의 수준을 내리기 전에 전자 메일 마이그레이션을 완료 하는 것이 좋습니다.  

> [!NOTE]
>  Windows Small Business Server POP3 커넥터는 Exchange Server에 포함되어 있지 않습니다. 따라서 메일 데이터를 다른 Exchange Server로 마이그레이션한 후에는 POP3 커넥터 기능을 더 이상 사용할 수 없습니다.  

> [!NOTE]
>  마이그레이션을 위한 원본 서버 업데이트 및 준비가 끝났으면 마이그레이션 프로세스를 계속하기 전에 업데이트된 서버를 백업해야 합니다.  

## <a name="next-steps"></a>다음 단계  
 Windows Server Essentials로 마이그레이션하기 위해 원본 서버를 준비 했습니다.  이제 [2 단계: Windows Server Essentials를 새 복제본 도메인 컨트롤러로 설치](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)로 이동 합니다.  

모든 단계를 보려면 [Windows Server Essentials로 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)을 참조 하세요.

