---
title: "지리적 중복 SQL Server 복제 설정"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: a9f29c1eb19a8241eac5afb5c87581e6c988c3c8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>지리적 중복 SQL Server 복제 설정

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

> [!IMPORTANT]  
> ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 이상 사용할 수 있습니다.
  
SQL Server ADFS 구성 데이터베이스와를 사용 하는 경우 SQL Server 복제 사용 하 여 ADFS 팜에 대 한 geo\ 중복을 설정할 수 있습니다. Geo\ 중복 응용 프로그램 다른 사이트 간에 전환할 수 있도록 데이터 두 떨어진 사이트 사이 복제 합니다. 이 이렇게 한 사이트에 오류가 발생 하는 경우 할 수 있습니다 계속 사용할 수 있는 모든 구성 데이터 두 번째 사이트에서. 자세한 내용은에 "SQL Server 지리적 중복"섹션 참조 [사용 하 여 Federation 서버 농장 SQL Server](../design/Federation-Server-Farm-Using-SQL-Server.md)합니다.  
  
## <a name="prerequisites"></a>필수  
설치 및 구성 SQL server 팜. 자세한 내용은 참조 [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)합니다. 초기 SQL Server, SQL Server 에이전트 서비스가 실행 되 고 있는지 확인 하 고 자동으로 시작 하도록 설정 합니다.  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>두 번째 \(replica\) SQL Server geo\ 중복에 만들기  
  
1.  설치 SQL Server \ (자세한 내용은 참조 [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)합니다. 복제본 SQL server 결과 CreateDB.sql 및 SetPermissions.sql 스크립트 파일을 복사 합니다.  
  
2.  SQL Server 에이전트 서비스가 실행 되 고 있는지 확인 하 고 자동으로 시작 설정  
  
3.  실행 **Export\ AdfsDeploymentSQLScript** 기본 ADFS 노드에서 CreateDB.sql 및 SetPermissions.sql 파일을 만들 수 있습니다.  예를 들어:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql2.png)
  
4.  스크립트 보조 서버를 복사 합니다.  CreateDB.sql 스크립트 열고 **SQL Management Studio** 클릭 **실행**합니다.
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql4.png)

5. 에 SetPermissions.sql 스크립트 열고 **SQL Management Studio** 클릭 **실행**합니다.
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql6.png) 

   

>[!NOTE]
>명령줄에서 다음을 사용할 수 있습니다. 
>
>    `c:\>sqlcmd –i CreateDB.sql`  
>  
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
## <a name="create-publisher-settings-on-the-initial-sql-server"></a>초기 SQL Server에서 게시자 설정을 만들기  
  
1.  SQL Server 관리 studio에서 아래 **복제**를 마우스 오른쪽 단추로 클릭 **로컬 게시** 선택 **새 게시... **<ph x="4">
![</ph> 지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql7.png) </br>  

2.  새 게시 마법사 화면 클릭 **다음**합니다.</br>
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql8.png) </br> 
  
3.  **배포자** 페이지 로컬 서버 배포자로 선택 하 고 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql9.png) </br>   

4.  에 **스냅숏을** 폴더 페이지에서 \\\SQL1\repldata 기본 폴더 위치를 입력 합니다. \ (참고:이 공유 yourself\ 만들 수도 있습니다).  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql10.png) </br>   
  
5.  선택 **AdfsConfigurationV3** 게시 데이터베이스 및 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql11.png) </br>
  
6.  **게시 유형**, 선택 **병합 게시** 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql12.png) </br>
  
7.  **구독자 유형**, 선택 **SQL Server 2008 이상** 클릭 **다음**합니다.  
 ![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql13.png) </br> 

8.  에 **문서** 선택 페이지 **표** 노드 모든 테이블 다음 **un\ 확인 SyncProperties** 테이블 \ (이 안 replicated\)</br>
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql14.png) </br>    
  
9.  에 **문서** 페이지를 선택 하 고 **사용자 정의 기능** 노드 모든 사용자 정의 된 기능을 선택 하 고 누릅니다 **다음**...  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql15.png) </br>    

10. 에 **문제 문서** 페이지 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql16.png) </br>   

11. 에 **필터 표 행** 페이지, 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql17.png) </br>   
12. 에 **스냅숏을 에이전트** 14 일와 직접 실행 기본값을 선택할 페이지, 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql18.png) </br>   
SQL 에이전트 도메인 계정을 만들려면 해야 할 수 있습니다. 단계를 사용 하 여 [CONTOSO\\sqlagent 도메인 계정에 대 한 구성 SQL 로그인](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent) 이 새로운 광고 사용자에 대 한 로그인 SQL 만들고 특정 권한이 지정 합니다.  
  
13. 에 **에이전트 보안** 페이지, 클릭 **보안 설정** 도메인 계정 username\/암호를 입력 하 고 \ (하지 GMSA\) SQL 에이전트 및 클릭 용으로 만들어진 **확인**합니다.  클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql19.png) </br>  

14. 에 **마법사 작업** 페이지, 클릭 **다음**합니다.   
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql20.png) </br>

15. 에 **마법사를 완료** 페이지 파일 이름을 입력 하 고 클릭 **완료**합니다. 
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql21.png) </br>  

16. 게시 생성 되 면 성공 상태가 표시 되어야 합니다.  클릭 **닫기**합니다.
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql22.png) </br>  

17. 다시 SQL Server Management Studio 새 게시 마우스 오른쪽 단추로 클릭 하 고 클릭 **복제 모니터 시작**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>구독 설정 복제본 SQL Server에서 만들기  
위의 설명에 따라 초기 SQL Server에서 게시자 설정 만든 하는 있는지 확인 한 후 다음 단계를 수행 합니다.  
  
1.  복제 SQL Server, SQL Server 관리 studio에서에 **복제**를 마우스 오른쪽 단추로 클릭 **로컬 구독** 선택 **새 구독... **. ![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql24.png) </br>  

2.  에 **새 구독 마법사** 페이지, 클릭 **다음**합니다.
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql25.png) </br>   
  
3.  에 **게시** 페이지 게시자 드롭다운 목록에서 선택 합니다.  확장 **AdfsConfigurationV3** 위에서 만든 게시의 이름을 선택 하 고 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql26.png) </br> 
  
4.  에 **에이전트 위치 병합** 페이지를 선택 하 고 **해당 구독자 \(pull subscriptions\)에서 각 에이전트 실행** \(the default\) 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql27.png) </br> 이 구독 유형 아래 함께 결정 충돌 해상도 논리 합니다. \ (자세한 내용은 참조 [검색 및 복제 병합 충돌을 해결](https://technet.microsoft.com/library/ms151191.aspx)합니다. </br>
 
5.  에 **구독자** 페이지를 선택 하 고 **AdfsConfigurationV3** 구독자 데이터베이스 및 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql28.png) </br> 
  
6.  에 **에이전트 보안 병합** 페이지, 클릭 **... **이름과 도메인 계정 암호를 입력 하 고 \ (하지 GMSA\) SQL 상담원에 대 한 줄임표 상자를 사용 하 여 작성 및 클릭 하 고 **다음**합니다.
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql30.png) </br> 
  
7.  **동기화 일정**, 선택 **지속적으로 실행** 클릭 **다음**합니다. 
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql31.png) </br> 
 
8.  **초기화 구독**, 클릭 **다음**합니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql32.png) </br> 
  
9.  **구독 유형**, 선택 **클라이언트** 클릭 **다음**합니다.  
  
    이러한 사실을 설명 [여기](https://technet.microsoft.com/library/ms151191.aspx) 및 [여기](https://technet.microsoft.com/library/ms151170.aspx)합니다.  기본적으로, 취할는 간단히 "게시자 wins 첫 번째" 충돌을 해결 하 고 다른 구독자 다시 게시 필요가 없습니다.  
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql33.png) </br>
   
10. 에 **마법사 작업** 페이지에서 확인 **구독을 만들어야** 을 선택 하 고 클릭 **다음**합니다. 
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql34.png) </br>

11. 에 **마법사를 완료** 페이지, 클릭 **완료**합니다. 
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql35.png) </br>

12. 구독이 작성 과정을 완료 하면 성공을 표시 됩니다. 클릭 **닫기**합니다. 
![지리적 중복 설정](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>초기화 및 복제 하는 과정 확인  
  
1.  기본 SQL server에서 right\ 클릭은 **복제** 노드와 클릭 **복제 모니터 시작**합니다.  
  
2.  **복제 모니터**를 클릭 하 여 게시 됩니다.  
  
3.  에 **모든 구독** 탭을 마우스 오른쪽 단추로 클릭 하 고 **세부 정보 보기**합니다.  
  
    아래에서 여러 항목을 볼 수 **작업** 초기 복제 합니다.  
  
4.  또한 아래에서 볼 수는 **SQL Server 에이전트 \\Jobs** publication\/구독의 작업을 실행 하는 job\(s\) 보려면 노드 예정입니다.  로컬 작업 표시 되어, 문제 해결을 위해 구독자 게시자에 확인 하 않도록만 합니다.  작업을 Right\ 클릭 하 고 선택 **기록 보기** 실행 기록 보기 및 결과를 합니다.  
  
## <a name="sqlagent"></a>SQL 로그인 CONTOSO\\sqlagent 도메인 계정에 대 한 구성  
  
1.  기본 및 복제본 CONTOSO\\sqlagent 라는 SQL Server의 새 로그인 만들기 \ (새 도메인 사용자의 이름 만들고 구성에 **에이전트 보안** 위의 절차에 페이지. \)  
  
2.  SQL Server, right\ 클릭 로그인 작성 하 고 아래에서 속성을 선택한 다음에 **사용자 매핑** 탭이 로그인에 지도 **AdfsConfiguration** 및 **AdfsArtifact** 공개 및 db\_genevaservice 역할 데이터베이스 합니다. 이 로그인 배포 데이터베이스에 매핑됩니다 하 고 메일 및 adfsconfiguration 테이블 db\_owner 역할을 추가할 수도 있습니다.  기본 및 복제본 SQL server에서 해당으로이 작업을 수행 합니다. 자세한 내용은 참조 [복제 에이전트 보안 모델](https://technet.microsoft.com/library/ms151868.aspx)합니다.  
  
3.  해당 도메인 계정 읽기 제공 하 고 배포자로 구성 공유에 사용 권한을 쓸 수 있게 합니다.  읽기 설정 하 고 쓰기 공유 사용 권한 및 로컬 파일 권한에 권한이 있는지 확인 합니다.  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>ADFS node\(s\) SQL Server 복제본 농장 가리키도록 구성  
지리 중복 설정한 했으므로 ADFS 농장 노드 Windows PowerShell 또는 광고 FS 구성 마법사 UI에서 중 하나는 표준 광고 FS "가입" 농장 기능을 사용 하 여 복제 SQL Server 팜 가리키도록 구성할 수 있습니다.  
  
AD FS 구성 마법사 UI를 사용 하면 선택 **federation 서버 federation 서버 팜을 추가**합니다. **그렇지 않은** 선택 **federation 서버 농장의 첫 번째 federation 서버를 만들**합니다.  
  
Windows PowerShell를 사용 하는 경우 실행 **Add\ AdfsFarmNode**합니다. **그렇지 않은** 실행 **Install\ AdfsFarm**합니다.  
  
메시지가 표시 되 면 제공 복제 SQL Server 인스턴스 이름과 호스트 **하지** 초기 SQL server 합니다.  
