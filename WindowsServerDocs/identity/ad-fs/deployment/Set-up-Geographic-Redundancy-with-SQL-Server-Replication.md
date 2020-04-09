---
title: SQL Server 복제를 사용 하 여 지리적 중복성 설정
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: 54106ae635d44368542986c7c469560981f9888a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855846"
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>SQL Server 복제를 사용 하 여 지리적 중복성 설정


> [!IMPORTANT]  
> AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려면 SQL Server 2008 이상을 사용할 수 있습니다.
  
AD FS 구성 데이터베이스로 SQL Server를 사용 하는 경우 SQL Server 복제를 사용 하 여 AD FS 팜에 대해 지역\-중복성을 설정할 수 있습니다. 지역\-중복성은 응용 프로그램이 한 사이트에서 다른 사이트로 전환할 수 있도록 두 개의 지리적으로 멀리 떨어진 사이트 간에 데이터를 복제 합니다. 이러한 방식으로 한 사이트의 장애가 발생 하는 경우에도 두 번째 사이트에서 모든 구성 데이터를 사용할 수 있습니다. 자세한 내용은 [SQL Server를 사용 하 여 페더레이션 서버 팜](../design/Federation-Server-Farm-Using-SQL-Server.md)에서 "SQL Server 지리적 중복성 섹션"을 참조 하세요.  
  
## <a name="prerequisites"></a>필수 조건  
SQL server 팜을 설치 하 고 구성 합니다. 자세한 내용은 [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)를 참조 하세요. 초기 SQL Server에서 SQL Server 에이전트 서비스가 실행 중이 고 자동 시작으로 설정 되어 있는지 확인 합니다.  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>지역\-중복성에 대 한 두 번째 \(복제본\) SQL Server 만들기  
  
1. SQL Server \(를 설치 합니다. 자세한 내용은 [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)를 참조 하세요. 결과 CreateDB .sql 및 SetPermissions 스크립트 파일을 복제본 SQL server에 복사 합니다.  
  
2. SQL Server 에이전트 서비스가 실행 중이 고 자동으로 시작 되도록 설정 되어 있는지 확인  
  
3. 주 AD FS 노드에서 **내보내기\-AdfsDeploymentSQLScript** 를 실행 하 여 createdb. .Sql 및 SetPermissions 파일을 만듭니다.  예:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql2.png)
  
4. 스크립트를 보조 서버에 복사 합니다.  **Sql Management Studio** 에서 createdb .sql 스크립트를 열고 **실행**을 클릭 합니다.
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql4.png)

5. **Sql Management Studio** 에서 SetPermissions 스크립트를 열고 **실행**을 클릭 합니다.
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql6.png) 

   

> [!NOTE]
> 또한 명령줄에서 다음을 사용할 수 있습니다. 
> 
>    `c:\>sqlcmd –i CreateDB.sql`  
> 
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
> ## <a name="create-publisher-settings-on-the-initial-sql-server"></a>초기 SQL Server에서 게시자 설정 만들기  
  
1. SQL Server Management studio의 **복제**에서 **로컬 게시** 를 마우스 오른쪽 단추로 클릭 하 고 **새 게시** ...
   를 선택 하 ![지리 중복성을 설정](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql7.png) </br>  

2. 새 게시 마법사 화면에서 **다음**을 클릭 합니다.</br>
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql8.png) </br> 
  
3. **배포자** 페이지에서 로컬 서버를 배포자로 선택 하 고 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql9.png) </br>   

4. **스냅숏** 폴더 페이지에서 기본 폴더 대신 \\\SQL1\repldata를 입력 합니다. \(참고:이 공유\)직접 만들어야 할 수도 있습니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql10.png) </br>   
  
5. 게시 데이터베이스로 **AdfsConfigurationV3** 를 선택 하 고 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql11.png) </br>
  
6. **게시 유형**에서 **병합 게시** 를 선택 하 고 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql12.png) </br>
  
7. **구독자 형식**에서 **SQL Server 2008** 이상을 선택 하 고 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql13.png) </br> 

8. **아티클** 페이지에서 **테이블** 선택 노드를 선택 하 여 모든 테이블을 선택 하 고,이 항목을\) 복제 하지 \( **\-확인** 합니다.</br>
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql14.png) </br>    
  
9. **아티클** 페이지에서 **사용자 정의 함수** 노드를 선택 하 여 모든 사용자 정의 함수를 선택 하 고 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql15.png) </br>    

10. **아티클 문제** 페이지에서 **다음**을 클릭 합니다.  
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql16.png) </br>   

11. **테이블 행 필터** 페이지에서 **다음**을 클릭 합니다.  
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql17.png) </br>   
12. **스냅숏 에이전트** 페이지에서 직접 및 14 일의 기본값을 선택 하 고 **다음**을 클릭 합니다.  
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql18.png) </br>   
    SQL 에이전트에 대 한 도메인 계정을 만들어야 할 수도 있습니다. [도메인 계정 CONTOSO\\sqlagent에 대 한 sql 로그인 구성](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent) 의 단계를 사용 하 여이 새 AD 사용자에 대 한 sql 로그인을 만들고 특정 사용 권한을 할당 합니다.  
  
13. **에이전트 보안** 페이지에서 **보안 설정** 을 클릭 하 고, SQL 에이전트에 대해 생성 된 GMSA\) 아닌 도메인 \(계정의 사용자 이름\/암호를 입력 하 고 **확인**을 클릭 합니다.  **다음**을 클릭합니다.  
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql19.png) </br>  

14. **마법사 작업** 페이지에서 **다음**을 클릭 합니다.   
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql20.png) </br>

15. **마법사 완료** 페이지에서 게시에 대 한 이름을 입력 하 고 **마침**을 클릭 합니다. 
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql21.png) </br>  

16. 게시가 만들어지면 성공 상태가 표시 됩니다.  **닫기**를 클릭합니다.
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql22.png) </br>  

17. SQL Server Management Studio로 돌아가서 새 게시를 마우스 오른쪽 단추로 클릭 하 고 **복제 모니터 시작**을 클릭 합니다.  
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>복제본 SQL Server에 대 한 구독 설정 만들기  
위에서 설명한 대로 초기 SQL Server에서 게시자 설정을 만들었는지 확인 하 고 다음 절차를 완료 합니다.  
  
1. 복제본 SQL Server SQL Server Management studio의 **복제**에서 **로컬 구독** 을 마우스 오른쪽 단추로 클릭 하 고 **새 구독**...을 선택 합니다. 지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql24.png) </br>  

2. **새 구독 마법사** 페이지에서 **다음**을 클릭 합니다.
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql25.png) </br>   
  
3. **게시** 페이지의 드롭다운에서 게시자를 선택 합니다.  **AdfsConfigurationV3** 를 확장 하 고 위에서 만든 게시의 이름을 선택 하 고 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql26.png) </br> 
  
4. **병합 에이전트 위치** 페이지에서 **각 에이전트를 해당 구독자에서 실행 \(** 선택 하 고 기본\) \(\)한 후 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql27.png) </br> 이는 아래 구독 유형과 함께 충돌 해결 논리를 결정 합니다. 자세한 내용은 [병합 복제 충돌 검색 및 해결](https://technet.microsoft.com/library/ms151191.aspx)을 참조 하세요. \( </br>
 
5. **구독자** 페이지에서 **AdfsConfigurationV3** 를 구독자 데이터베이스로 선택 하 고 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql28.png) </br> 
  
6. **병합 에이전트 보안** 페이지에서 **...** 를 클릭 하 고 줄임표 (...) 상자를 사용 하 여 SQL 에이전트에 대해 생성 된 GMSA\) 아닌 도메인 \(계정의 사용자 이름과 암호를 입력 하 고 **다음**을 클릭 합니다.
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql30.png) </br> 
  
7. **동기화 일정**에서 **계속 실행** 을 선택 하 고 **다음**을 클릭 합니다. 
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql31.png) </br> 
 
8. **구독 초기화**에서 **다음**을 클릭 합니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql32.png) </br> 
  
9. **구독 유형**에서 **클라이언트** 를 선택 하 고 **다음**을 클릭 합니다.  
  
   이에 대 한 의미는 여기 및 [여기](https://technet.microsoft.com/library/ms151170.aspx)에 [설명 되어 있습니다](https://technet.microsoft.com/library/ms151191.aspx) .  기본적으로 "먼저 게시자 우선" 충돌 해결을 수행 하 고 다른 구독자에 다시 게시 하지 않아도 됩니다.  
   지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql33.png) </br>
   
10. **마법사 동작** 페이지에서 **구독 만들기** 가 선택 되어 있는지 확인 하 고 **다음**을 클릭 합니다. 
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql34.png) </br>

11. **마법사 완료** 페이지에서 **마침**을 클릭 합니다. 
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql35.png) </br>

12. 구독이 생성 프로세스를 완료 하면 성공이 표시 됩니다. **닫기**를 클릭합니다. 
    지리적 중복성을 설정 ![](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>초기화 및 복제 프로세스 확인  
  
1.  주 SQL server에서 **복제** 노드를 마우스 오른쪽 단추로 클릭\-**복제 모니터 시작**을 클릭 합니다.  
  
2.  **복제 모니터**에서 게시를 클릭 합니다.  
  
3.  **모든 구독** 탭에서 마우스 오른쪽 단추를 클릭 하 고 **자세히 보기**를 클릭 합니다.  
  
    초기 복제에 대 한 **작업** 에서 많은 항목을 볼 수 있어야 합니다.  
  
4.  또한 **SQL Server 에이전트\\작업** 노드 아래에서 게시\/구독의 작업을 실행 하도록 예약 된\) 작업\(을 확인할 수 있습니다.  로컬 작업만 표시 되므로 문제 해결을 위해 게시자와 구독자를 확인 해야 합니다.  작업을 마우스 오른쪽 단추로 클릭 하 고 **기록 보기** 를 선택 하 여 실행 기록 및 결과를 표시\-합니다.  
  
## <a name="configure-sql-login-for-the-domain-account-contososqlagent"></a><a name="sqlagent"></a>도메인 계정 CONTOSO\\sqlagent에 대 한 SQL 로그인 구성  
  
1.  위의 절차에서 **에이전트 보안** 페이지에서 만들고 구성한 새 도메인 사용자의 이름을 \(CONTOSO\\sqlagent 이라는 기본 및 복제본 SQL Server에 새 로그인을 만듭니다.\)  
  
2.  SQL Server에서 사용자가 만든 로그인을 마우스 오른쪽 단추로\-클릭 하 고 속성을 선택한 다음 **사용자 매핑** 탭에서이 로그인을 public 및 db\_genevaservice 역할이 있는 **AdfsConfiguration** 및 **AdfsArtifact** 데이터베이스에 매핑합니다. 또한이 로그인을 배포 데이터베이스에 매핑하고 배포 및 adfsconfiguration 테이블에 대 한 db\_소유자 역할을 추가 합니다.  주 서버와 복제 SQL server 모두에 해당 하는 경우이 작업을 수행 합니다. 자세한 내용은 [Replication Agent Security Model](https://technet.microsoft.com/library/ms151868.aspx)을 참조 하세요.  
  
3.  배포자로 구성 된 공유에 대 한 읽기 및 쓰기 권한을 해당 도메인 계정에 부여 합니다.  공유 권한 및 로컬 파일 사용 권한에 대 한 읽기 및 쓰기 권한을 설정 해야 합니다.  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>SQL Server 복제본 팜을 가리키도록 AD FS 노드\(s\) 구성  
이제 지리적 중복성을 설정 했으므로 AD FS 구성 마법사 UI 또는 Windows PowerShell을 사용 하 여 표준 AD FS "조인" 팜 기능을 사용 하 여 복제본 SQL Server 팜을 가리키도록 AD FS 팜 노드를 구성할 수 있습니다.  
  
AD FS 구성 마법사 UI를 사용 하는 경우 페더레이션 서버 **팜에 페더레이션 서버 추가**를 선택 합니다. **페더레이션 서버 팜에서 첫 번째 페더레이션 서버 만들기**를 선택 **하지 마십시오** .  
  
Windows PowerShell을 사용 하는 경우 **Add\-add-adfsfarmnode**를 실행 합니다. **AdfsFarm\-설치**를 실행 **하지** 않습니다.  
  
메시지가 표시 되 면 초기 SQL Server가 **아닌** 복제본 SQL Server의 호스트 및 인스턴스 이름을 제공 합니다.  
