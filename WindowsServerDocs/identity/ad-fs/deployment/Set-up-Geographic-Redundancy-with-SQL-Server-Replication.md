---
title: SQL Server 복제 설치 지리적 중복
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: 00880d06835fad08538f634fdf2868146fc23b1a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442922"
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>SQL Server 복제 설치 지리적 중복


> [!IMPORTANT]  
> AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우에 SQL Server 2008 이상을 사용할 수 있습니다.
  
SQL Server로 AD FS 구성 데이터베이스를 사용 하는 경우에 지역에서 설정할 수 있습니다\-SQL Server 복제를 사용 하 여 AD FS 팜에 대 한 중복 됩니다. 지역\-중복 응용 프로그램에서 다른 사이트 간에 전환할 수 있도록 지리적으로 떨어져 있는 두 사이트 간에 데이터를 복제 합니다. 이러한 방식으로 한 사이트의 오류를 발생 시 사용할 수 있습니다 여전히 사용 가능한 모든 구성 데이터 두 번째 사이트입니다. 자세한 내용은 "SQL Server 지리적 복제"섹션을 참조 [페더레이션 서버 팜을 사용 하 여 SQL Server](../design/Federation-Server-Farm-Using-SQL-Server.md)합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
설치 하 고 SQL server 팜을 구성 합니다. 자세한 내용은 [ https://technet.microsoft.com/evalcenter/hh225126.aspx ](https://technet.microsoft.com/evalcenter/hh225126.aspx)합니다. 초기 SQL server에서 SQL Server 에이전트 서비스가 실행 중인지 확인 하 고 자동으로 시작 되도록 설정 합니다.  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>두 번째를 만드는 \(복제본\) 지역에 대 한 SQL Server\-중복성  
  
1. SQL Server 설치 \(자세한 내용은 참조 하십시오 [ https://technet.microsoft.com/evalcenter/hh225126.aspx ](https://technet.microsoft.com/evalcenter/hh225126.aspx)합니다. 복제본 SQL server에 결과 SetPermissions.sql 및 CreateDB.sql 스크립트 파일을 복사 합니다.  
  
2. SQL Server 에이전트 서비스가 실행 중인지 확인 하 고 자동으로 시작 되도록 설정  
  
3. 실행 **내보낼\-AdfsDeploymentSQLScript** 노드에서 기본 AD FS CreateDB.sql 및 SetPermissions.sql 파일을 만듭니다.  예를 들어:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql2.png)
  
4. 보조 서버에 스크립트를 복사 합니다.  CreateDB.sql 스크립트를 엽니다 **SQL Management Studio** 누릅니다 **Execute**합니다.
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql4.png)

5. SetPermissions.sql 스크립트를 엽니다 **SQL Management Studio** 누릅니다 **Execute**합니다.
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql6.png) 

   

> [!NOTE]
> 또한 명령줄에서 다음을 사용할 수 있습니다. 
> 
>    `c:\>sqlcmd –i CreateDB.sql`  
> 
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
> ## <a name="create-publisher-settings-on-the-initial-sql-server"></a>게시자 설정 초기 SQL Server에서 만들기  
  
1. SQL Server Management studio에서 아래의 **복제**를 마우스 오른쪽 단추로 클릭 **로컬 게시** 선택한 **새 게시 하는 중... ** 
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql7.png) </br>  

2. 새 게시 마법사 화면을 누릅니다 **다음**합니다.</br>
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql8.png) </br> 
  
3. 온 **배포자** 페이지에서 배포자로 로컬 서버를 선택 하 고 클릭 **다음**합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql9.png) </br>   

4. 에 **스냅샷** 폴더 페이지에서 입력 \\\SQL1\repldata 기본 폴더 대신 합니다. \(참고: 이 공유를 직접 만들 수도 있습니다\)합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql10.png) </br>   
  
5. 선택할 **AdfsConfigurationV3** 게시 데이터베이스와 클릭 **다음**합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql11.png) </br>
  
6. 온 **게시 유형**, 선택 **병합 게시** 클릭 **다음**합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql12.png) </br>
  
7. 온 **구독자 유형**, 선택 **SQL Server 2008 이상** 클릭 **다음**합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql13.png) </br> 

8. 에 **문서** 페이지 선택 **테이블** 노드를 모든 테이블을 선택한 후 **취소\-SyncProperties 확인** 테이블 \(이 안 됩니다 복제\)</br>
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql14.png) </br>    
  
9. 에 **아티클** 페이지에서 **사용자 정의 함수** 노드를 모든 사용자 정의 함수를 선택 하 고 클릭 **다음**...  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql15.png) </br>    

10. 에 **아티클 문제** 페이지 **다음**합니다.  
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql16.png) </br>   

11. 에 **테이블 행 필터** 페이지에서 클릭 **다음**합니다.  
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql17.png) </br>   
12. 에 **스냅숏 에이전트** 페이지, 직접 실행 및 14 일의 기본값 선택, 클릭 **다음**합니다.  
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql18.png) </br>   
    SQL 에이전트에 대 한 도메인 계정을 만들려면 해야 합니다. 단계를 따르세요 [CONTOSO 도메인 계정에 대 한 구성 SQL 로그인\\sqlagent](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent) 이 새 AD 사용자에 대 한 SQL 로그인을 만들고 특정 사용 권한을 할당 합니다.  
  
13. 에 **에이전트 보안** 페이지에서 클릭 **보안 설정을** 사용자 이름을 입력 하 고\/도메인 계정의 암호 \(GMSA를 하지\) SQL 에이전트에 대 한 생성 및 클릭 **확인**합니다.  **다음**을 클릭합니다.  
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql19.png) </br>  

14. 에 **마법사 동작** 페이지에서 클릭 **다음**합니다.   
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql20.png) </br>

15. 에 **마법사를 완료 합니다** 페이지에서 게시에 대 한 이름을 입력 하 고 클릭 **마침**합니다. 
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql21.png) </br>  

16. 게시를 만든 후 성공 상태가 표시 됩니다.  **닫기**를 클릭합니다.
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql22.png) </br>  

17. 다시 SQL Server Management Studio에서 새로운 게시를 마우스 오른쪽 단추로 클릭 하 고 클릭 **복제 모니터 시작**합니다.  
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>SQL Server 복제본에 대해 구독 설정 만들기  
위에서 설명한 대로 초기 SQL Server에서 게시자 설정을 만들어졌는지 확인 하 고 다음 절차를 완료 합니다.  
  
1. SQL Server Management studio에서 SQL Server 복제본에서 아래의 **복제**를 마우스 오른쪽 단추로 클릭 **로컬 구독** 선택한 **새 구독...** . ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql24.png) </br>  

2. 에 **새 구독 마법사** 페이지에서 클릭 **다음**합니다.
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql25.png) </br>   
  
3. 에 **게시** 페이지 드롭다운 목록에서 게시자를 선택 합니다.  확장 **AdfsConfigurationV3** 위에서 만든 게시의 이름을 선택 하 고 클릭 **다음**합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql26.png) </br> 
  
4. 에 **병합 에이전트 위치** 페이지에서 **각 에이전트를 해당 구독자에서 실행 \(끌어오기 구독이\)**  \(기본값\) 클릭 **다음**합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql27.png) </br> 따라서 아래 구독 유형과 함께 결정 충돌 해결 논리를 합니다. \(자세한 내용은 [감지 및 Resolve Merge Replication Conflicts](https://technet.microsoft.com/library/ms151191.aspx)합니다. </br>
 
5. 에 **구독자** 페이지에서 **AdfsConfigurationV3** 구독자 데이터베이스와 클릭 **다음**합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql28.png) </br> 
  
6. 에 **병합 에이전트 보안** 페이지에서 **...**  사용자 이름 및 도메인 계정의 암호를 입력 하 고 \(GMSA 없습니다\) 클릭 확인 하 고 줄임표 상자를 사용 하 여 SQL 에이전트에 대해 만든 **다음**합니다.
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql30.png) </br> 
  
7. 온 **동기화 일정**, 선택 **지속적으로 실행** 클릭 **다음**합니다. 
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql31.png) </br> 
 
8. 온 **구독 초기화**, 클릭 **다음**합니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql32.png) </br> 
  
9. 온 **구독 유형**, 선택 **클라이언트** 클릭 **다음**합니다.  
  
   이것이 어떤 의미가 나와 [여기](https://technet.microsoft.com/library/ms151191.aspx) 하 고 [여기](https://technet.microsoft.com/library/ms151170.aspx)합니다.  기본적으로, 간단한 "first 게시자 내용 적용" 충돌 해결 수행 및 다른 구독자로 다시 게시할 필요가 없습니다.  
   ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql33.png) </br>
   
10. 에 **마법사 동작** 페이지에서 **구독을 만듭니다** 을 선택 하 고 클릭 **다음**합니다. 
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql34.png) </br>

11. 에 **마법사를 완료** 페이지에서 클릭 **마침**합니다. 
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql35.png) </br>

12. 구독 만들기 프로세스가 완료 되 면 성공을 표시 되어야 합니다. **닫기**를 클릭합니다. 
    ![지리적 중복성 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>초기화 하 고 복제 프로세스를 확인 합니다.  
  
1.  주 SQL server에서 마우스 오른쪽\-를 클릭 합니다 **복제** 노드를 클릭 **복제 모니터 시작**합니다.  
  
2.  **복제 모니터**, 게시를 클릭 합니다.  
  
3.  에 **모든 구독** 탭을 마우스 오른쪽 단추로 클릭 하 고 **세부 정보 보기**합니다.  
  
    여러 항목을 볼 수 있습니다 **작업** 초기 복제에 대 한 합니다.  
  
4.  또한 아래에서 확인할 수 있습니다 합니다 **SQL Server 에이전트\\작업** 노드에서 작업을 볼 수\(s\) 게시 작업을 실행 하도록 예약\/구독 합니다.  로컬 작업으로 표시 되어만 문제 해결을 위해 게시자 및 구독자에서 확인 해야 합니다.  오른쪽\-작업을 클릭 하 고 선택 **기록 보기** 실행 기록 보기 및 결과입니다.  
  
## <a name="sqlagent"></a>CONTOSO 도메인 계정에 대 한 SQL 로그인 구성\\sqlagent  
  
1.  주 및 복제본 CONTOSO 라는 SQL Server에 새 로그인을 만듭니다\\sqlagent \(새 도메인 사용자의 이름을 만들고 구성 합니다 **에이전트 보안** 위의 절차에는 페이지입니다.\)  
  
2.  SQL Server에서 마우스 오른쪽\-를 만든 로그인을 클릭 하 고 아래에서 다음 속성을 선택 합니다 **사용자 매핑** 탭에서이 로그인에 매핑합니다 **AdfsConfiguration** 및 **AdfsArtifact**  공용 및 db를 사용 하 여 데이터베이스\_genevaservice 역할입니다. 또한 배포 데이터베이스로이 로그인에 매핑합니다 및 db 추가\_배포와 adfsconfiguration 테이블에 대 한 소유자 역할입니다.  주 및 복제본 SQL server에 해당 하는 경우이 작업을 수행 합니다. 자세한 내용은 [Replication Agent Security Model](https://technet.microsoft.com/library/ms151868.aspx)합니다.  
  
3.  해당 도메인 계정 읽기를 지정 하 고 배포자로 구성 된 공유에 대 한 쓰기 권한이 있습니다.  읽기 쓰기 권한을 모두 로컬 파일 권한과 공유 권한을 하에 있는지 확인 합니다.  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>AD FS 노드 구성\(s\) SQL Server 복제본 팜을 가리키도록  
지역 중복 설정한 했으므로 AD FS 팜 노드는 표준 AD FS "join" 팜 기능, AD FS 구성 마법사 UI에서 사용 하거나 Windows PowerShell을 사용 하 여 복제본 SQL Server 팜을 가리키도록 구성할 수 있습니다.  
  
AD FS 구성 마법사 UI를 사용 하면 선택할 **페더레이션 서버 팜에 페더레이션 서버 추가**합니다. **하지** 선택 **페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기**합니다.  
  
Windows PowerShell을 사용 하는 경우 실행할 **추가\-AdfsFarmNode**합니다. **하지** 실행할 **설치\-AdfsFarm**합니다.  
  
메시지가 표시 되 면 복제본 SQL Server의 호스트 및 인스턴스 이름을 제공 **되지** 초기 SQL server입니다.  
