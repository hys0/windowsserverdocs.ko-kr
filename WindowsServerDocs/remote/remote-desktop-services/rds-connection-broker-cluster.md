---
title: RDS에서 고가용성을 구성 하는 RD 연결 브로커 서버를 추가 합니다.
description: RD 연결 브로커 고가용성을 위해 RDS 배포에 추가 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/10/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: e20b4960faac0ef40ad68271fa907394344e9c47
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034420"
---
# <a name="add-the-rd-connection-broker-server-to-the-deployment-and-configure-high-availability"></a>배포에 RD 연결 브로커 서버 추가 및 고가용성 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016

가용성과 원격 데스크톱 서비스 인프라의 규모를 개선 하기 위해 원격 데스크톱 연결 브로커 (RD 연결 브로커) 클러스터를 배포할 수 있습니다. 

## <a name="pre-requisites"></a>필수 구성 요소

두 번째 RD 연결 브로커-역할을 서버를 설정 합니다.이 VM 또는 물리적 서버를 수 있습니다.

연결 브로커에 대 한 데이터베이스를 설정 합니다. 사용할 수 있습니다 [Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-get-started/#create-a-new-aure-sql-database) 인스턴스 또는 로컬 환경에서 SQL Server입니다. 아래, Azure SQL을 사용 하는 방법에 대 한 이야기 하지만 SQL Server에 단계를 여전히 적용 합니다. 데이터베이스에 대 한 연결 문자열을 찾아 올바른 ODBC 드라이버가 있는지 확인 해야 합니다.

## <a name="step-1-configure-the-database-for-the-connection-broker"></a>1단계: 데이터베이스 연결 브로커에 대 한 구성

1. 만든 데이터베이스에 대 한 연결 문자열을 찾으려면-되도록 모두 필요 하 고 나중에 자체 (3 단계), 연결 브로커를 구성 하는 경우 따라서 문자열을 저장 위치는 쉽게 참조할 수 있습니다 ODBC 드라이버의 버전을 식별 해야 합니다. Azure SQL에 대 한 연결 문자열을 찾는 방법을 다음과 같습니다.  
    1. Azure 포털에서 클릭 **찾아보기 > 리소스 그룹** 배포에 대 한 리소스 그룹을 클릭 합니다.   
    2. (예: CB DB1) 방금 만든 SQL database를 선택 합니다.   
    3. 클릭 **설정 > 속성 > 데이터베이스 연결 문자열 표시**합니다.   
    4. 에 대 한 연결 문자열을 복사 **ODBC (Node.js 포함)** 에 다음과 같아야 합니다.   
      
        Driver={SQL Server Native Client 13.0};Server=tcp:cb-sqls1.database.windows.net,1433;Database=CB-DB1;Uid=sqladmin@contoso;Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;   
  
    5. "Your_password_here를"를 실제 암호로 바꿉니다. 확장 저장 프로시저를 데이터베이스에 연결할 때 포함 된 암호를에이 전체 문자열을 사용 합니다. 
2. 새 연결 브로커에 ODBC 드라이버를 설치 합니다. 
   1. VM 연결 브로커를 사용 하는 경우 첫 번째 RD 연결 브로커에 대 한 공용 IP 주소를 만듭니다. (만 해야 RDMS 가상 머신에 RDP 연결을 허용 하도록 공용 IP가 없는 경우이 작업을 수행 합니다.)
       1. Azure 포털에서 클릭 **찾아보기 > 리소스 그룹**, 리소스 그룹 배포를 클릭 한 다음 첫 번째 RD 연결 브로커 가상 머신 (예: Contoso-Cb1)를 클릭 합니다.
       2. 클릭 **설정 > 네트워크 인터페이스**, 한 다음 해당 네트워크 인터페이스를 클릭 합니다.
       3. 클릭 **설정 > IP 주소**합니다.
       4. 에 대 한 **공용 IP 주소**, 선택, **Enabled**, 를 클릭 하 고 **IP 주소**합니다.
       5. 사용 하려는 기존 공용 IP 주소를 사용 하는 경우 목록에서 선택 합니다. 그렇지 않은 경우 클릭 **새로 만들기**, 는 이름을 입력 하 고 클릭 한 다음 **확인** 차례로 **저장**합니다.
   2. 첫 번째 RD 연결 브로커에 연결 합니다.
       1. Azure 포털에서 클릭 **찾아보기 > 리소스 그룹**, 리소스 그룹 배포를 클릭 한 다음 첫 번째 RD 연결 브로커 가상 머신 (예: Contoso-Cb1)를 클릭 합니다.
       2. 클릭 **연결 > 열고** 를 원격 데스크톱 클라이언트를 엽니다.
       3. 클라이언트에서 클릭 **연결**, 를 클릭 하 고 **다른 사용자 계정을 사용 하 여**합니다. 도메인 관리자 계정의 사용자 이름 및 암호를 입력 합니다.
       4. 클릭 **예** 때 인증서에 대 한 경고 메시지를 받습니다.
   3. 다운로드 합니다 [SQL Server 용 ODBC 드라이버](https://www.microsoft.com/download/confirmation.aspx?id=50420) ODBC 연결 문자열의 버전과 일치 하는 합니다. 위의 예제에서는 문자열에 대 한 버전 13 ODBC 드라이버를 설치 해야 합니다.
   4. 첫 번째 RD 연결 브로커 서버 sqlincli.msi 파일을 복사 합니다.   
   5. Sqlincli.msi 파일을 열고 native client를 설치 합니다.  
   6. 각 추가 RD 연결 브로커 (예: Contoso-Cb2)에 대 한 1 ~ 5 단계를 반복 합니다.
   7. 연결 브로커를 실행 하는 각 서버에서 ODBC 드라이버를 설치 합니다.

## <a name="step-2-configure-load-balancing-on-the-rd-connection-brokers"></a>2단계: RD 연결 브로커에 부하 분산 구성 

Azure 인프라를 사용 하는 경우 만들 수 있습니다는 [Azure load balancer](#create-a-load-balancer)설정 하는 경우, 설정할 수 있습니다 [DNS 라운드 로빈](#configure-dns-round-robin)합니다.

### <a name="create-a-load-balancer"></a>Load balancer 만들기  
1. Azure 부하 분산 장치 만들기   
      1. Azure 포털에서 **찾아보기 > 부하 분산 장치 > 추가**합니다.   
      2. 새 부하 분산 장치 (예를 들어 hacb)에 대 한 이름을 입력 합니다.   
      3. 선택 **내부** 에 대 한 합니다 **구성표**를 **Virtual Network** 배포 (예를 들어 Contoso-VNet)에 대 한 및 **서브넷** 모든 리소스 (예를 들어, 기본값).   
      4. 선택 **정적** 에 대 한 합니다 **IP 주소 할당** 입력 하 고는 **개인 IP 주소** 는 사용 하지 않는 현재 (예를 들어 10.0.0.32).   
      5. 적절 한 선택 **구독**서 **리소스 그룹** 모든 리소스 및 적절 한 **위치**합니다.   
      6. **만들기**를 선택합니다.   
2. 만들기는 [프로브](https://azure.microsoft.com/documentation/articles/load-balancer-custom-probe-overview/) 어떤 서버가 활성 상태인 모니터:   
      1. Azure portal에서 클릭 **찾아보기 > 부하 분산 장치**, 부하 분산 장치를 방금 만든 (예를 들어 CBLB)를 클릭 하 고 있습니다. **설정**을 클릭합니다.   
      2. 클릭 **프로브 > 추가**합니다.   
      3. 프로브에 대 한 이름을 입력 (예를 들어 **RDP**)을 선택 **TCP** 으로 **프로토콜**를 입력 **3389** 에 대 한는 **포트**를 클릭 하 고 **확인**합니다.   
3. 연결 브로커의 백 엔드 풀을 만듭니다.   
      1. **설정을**, 클릭 **백 엔드 주소 풀 > 추가**합니다.   
      2. 이름 (예를 들어 CBBackendPool)을 입력 한 다음 클릭 **가상 머신 추가**합니다.  
      3. 가용성 집합 (예를 들어 CbAvSet)를 선택 하 고 클릭 **확인**합니다.   
      3. 클릭 **virtual machines 선택**각 가상 머신을 선택 하 고 클릭 **선택 > 확인 > 확인**합니다.   
4. RDP 부하를 분산 규칙을 만듭니다.   
      1. **설정을**, 클릭 **부하 분산 규칙**를 클릭 하 고 **추가**합니다.   
      2. 이름을 입력 합니다 (예: RDP)을 선택 합니다 **TCP** 에 대 한 합니다 **프로토콜**를 입력 **3389** 모두에 대 한 **포트** 및 **백 엔드 포트** , 클릭 **확인**합니다.   
5. 부하 분산 장치에 대 한 DNS 레코드를 추가 합니다.   
      1. RDMS 서버 가상 머신 (예: Contoso-CB1)에 연결 합니다. 체크 아웃 합니다 [RD 연결 브로커 VM 준비](Prepare-the-RD-Connection-Broker-VM-for-Remote-Desktop.md) VM에 연결 하는 방법에 대 한 단계는 문서입니다.   
      2. 서버 관리자에서 클릭 **도구 > DNS**합니다.   
      3. 왼쪽 창에서 확장 **DNS**DNS 컴퓨터 클릭, 클릭 **정방향 조회 영역**, 및 도메인 이름 (예: Contoso.com)을 클릭 합니다. (정보에 대 한 DNS 서버 쿼리를 처리 하는 데 몇 초 걸릴 수 있습니다.)  
      4. 클릭 **작업 > 새 호스트 (A 또는 AAAA)** 합니다.   
      9. 이름 (예를 들어 hacb) 및 이전에 지정한 IP 주소 (예를 들어 10.0.0.32)을 입력 합니다.   

### <a name="configure-dns-round-robin"></a>DNS 라운드 로빈 구성  
  
다음 단계는 Azure 내부 부하 분산 장치를 만드는 대신 합니다.   
  
1. Azure portal에서 RDMS 서버에 연결 합니다. 원격 데스크톱 연결 클라이언트를 사용 하 여   
2. DNS 레코드를 만듭니다.   
      1. 서버 관리자에서 클릭 **도구 > DNS**합니다.   
      2. 왼쪽 창에서 확장 **DNS**DNS 컴퓨터 클릭, 클릭 **정방향 조회 영역**, 및 도메인 이름 (예: Contoso.com)을 클릭 합니다. (정보에 대 한 DNS 서버 쿼리를 처리 하는 데 몇 초 걸릴 수 있습니다.)  
      3. 클릭 **동작** 하 고 **새 호스트 (A 또는 AAAA)** 합니다.   
      4. 입력 합니다 **DNS 이름** RD 연결 브로커에 대 한 클러스터 (예: hacb) 하 고 enter를 **IP 주소** 첫 번째 RD 연결 브로커입니다.   
      5. 각 추가 레코드에 대 한 각 고유 IP 주소를 제공 합니다. 각 추가 RD 연결 브로커에 대 한 3 ~ 4 단계를 반복 합니다.


예를 들어 두 RD 연결 브로커 가상 컴퓨터의 IP 주소는 10.0.0.8 및 10.0.0.9 경우 두 개의 DNS 호스트 레코드 만들어집니다.
 - 호스트 이름: hacb.contoso.com, IP 주소: 10.0.0.8
 - 호스트 이름: hacb.contoso.com, IP 주소: 10.0.0.9

## <a name="step-3-configure-the-connection-brokers-for-high-availability"></a>3단계: 고가용성에 대 한 연결 브로커를 구성 합니다.

1. 서버 관리자에 새 RD 연결 브로커 서버를 추가 합니다.
   1. 서버 관리자에서 클릭 **관리 > 서버 추가**합니다.
   2. 클릭 **지금 찾기**합니다.
   3. 새로 만든된 된 RD 연결 브로커 서버 (예: Contoso-Cb2)를 클릭 하 고 클릭 **확인**합니다.
2. RD 연결 브로커에 대 한 고가용성을 구성 합니다.
   1. 서버 관리자에서 클릭 **원격 데스크톱 서비스 > 개요**합니다.
   2. 마우스 오른쪽 단추로 클릭 **RD 연결 브로커**를 클릭 하 고 **가용성 우선 구성**합니다.
   3. 구성 형식 섹션에 도달할 때까지 마법사를 통해 페이지입니다. 선택 **공유 데이터베이스 서버**를 클릭 하 고 **다음**합니다.
   4. RD 연결 브로커 클러스터에 대 한 DNS 이름을 입력 합니다.
   5. SQL DB에 대 한 연결 문자열을 입력 하 고 고가용성을 설정 하려면 마법사를 통해 다음 페이지입니다.
3. 새 RD 연결 브로커 배포에 추가
   1. 서버 관리자에서 클릭 **원격 데스크톱 서비스 > 개요**합니다.
   2. RD 연결 브로커를 마우스 오른쪽 단추로 누른 **RD 연결 브로커 서버 추가**합니다.
   3. 서버 선택 영역에 도달할 때까지 마법사를 통해 페이지에는 다음 새로 만든된 된 RD 연결 브로커 서버 (예: Contoso-CB2) 선택 합니다.
   4. 기본값을 그대로 마법사를 완료 합니다.
4. RD 연결 브로커 서버 및 클라이언트에서 신뢰할 수 있는 인증서를 구성 합니다.

