---
title: RD 연결 브로커 서버를 추가하여 RDS에서 고가용성 구성
description: 고가용성을 위해 RD 연결 브로커를 RDS 배포에 추가하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/10/2017
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: dc6a9fa0d6834f63c9935518e4b2c26320a04082
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852966"
---
# <a name="add-the-rd-connection-broker-server-to-the-deployment-and-configure-high-availability"></a>배포에 RD 연결 브로커 서버 추가 및 고가용성 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

원격 데스크톱 연결 브로커(RD 연결 브로커) 클러스터를 배포하여 원격 데스크톱 서비스 인프라의 가용성 및 규모를 개선할 수 있습니다. 

## <a name="pre-requisites"></a>필수 구성 요소

두 번째 RD 연결 브로커 역할을 하는 서버 설정 - 물리적 서버 또는 VM일 수 있습니다.

연결 브로커를 위해 데이터베이스를 설정합니다. 로컬 환경에서 [Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-get-started/#create-a-new-aure-sql-database) 인스턴스 또는 SQL Server를 사용할 수 있습니다. 아래쪽에서 Azure SQL 사용 방법을 살펴보겠지만, 해당 단계는 SQL Server에 적용됩니다. 데이터베이스에 대한 연결 문자열을 찾고, 올바른 ODBC 드라이버가 있는지 확인해야 합니다.

## <a name="step-1-configure-the-database-for-the-connection-broker"></a>1단계: 연결 브로커에 대해 데이터베이스 구성

1. 만든 데이터베이스에 대한 연결 문자열을 찾습니다. 이 연결 문자열은 필요한 ODBC 드라이버 버전을 식별하고, 나중에 연결 브로커 자체를 구성할 때(3단계) 필요하므로 쉽게 참조할 수 있게 저장해야 합니다. Azure SQL에 대한 연결 문자열을 찾는 방법은 다음과 같습니다.  
    1. Azure Portal에서 **찾아보기 > 리소스 그룹**을 클릭하고 배포를 위한 리소스 그룹을 클릭합니다.   
    2. 방금 만든 SQL Database(예: CB-DB1)를 선택합니다.   
    3. **설정** > **속성** > **데이터베이스 연결 문자열 표시**를 클릭합니다.   
    4. 다음과 같은 **ODBC(Node.js 포함)** 에 대한 연결 문자열을 복사합니다.   
      
        ```
        Driver={SQL Server Native Client 13.0};Server=tcp:cb-sqls1.database.windows.net,1433;Database=CB-DB1;Uid=sqladmin@contoso;Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
        ```
  
    5. "your_password_here"를 실제 암호로 바꿉니다. 데이터베이스에 연결할 때 이 전체 문자열을 포함된 암호와 함께 사용합니다. 
2. 다음과 같이 새 연결 브로커에 ODBC 드라이버를 설치합니다. 
   1. 연결 브로커에 VM을 사용하는 경우 첫 번째 RD 연결 브로커에 대한 공용 IP 주소를 만듭니다. (RDMS 가상 머신에 RDP 연결을 허용하기 위한 공용 IP가 없는 경우에만 이 작업을 수행해야 합니다.)
       1. Azure Portal에서 **찾아보기** > **리소스 그룹**을 클릭하고 배포를 위한 리소스 그룹을 클릭한 다음, 첫 번째 RD 연결 브로커 가상 머신(예: Contoso-Cb1)을 클릭합니다.
       2. 클릭 **설정 > 네트워크 인터페이스**, 한 다음 해당 네트워크 인터페이스를 클릭 합니다.
       3. 클릭 **설정 > IP 주소**합니다.
       4. 에 대 한 **공용 IP 주소**, 선택, **Enabled**, 를 클릭 하 고 **IP 주소**합니다.
       5. 사용 하려는 기존 공용 IP 주소를 사용 하는 경우 목록에서 선택 합니다. 그렇지 않은 경우 클릭 **새로 만들기**, 는 이름을 입력 하 고 클릭 한 다음 **확인** 차례로 **저장**합니다.
   2. 첫 번째 RD 연결 브로커에 연결합니다.
       1. Azure Portal에서 **찾아보기** > **리소스 그룹**을 클릭하고 배포를 위한 리소스 그룹을 클릭한 다음, 첫 번째 RD 연결 브로커 가상 머신(예: Contoso-Cb1)을 클릭합니다.
       2. 클릭 **연결 > 열고** 를 원격 데스크톱 클라이언트를 엽니다.
       3. 클라이언트에서 클릭 **연결**, 를 클릭 하 고 **다른 사용자 계정을 사용 하 여**합니다. 도메인 관리자 계정의 사용자 이름 및 암호를 입력 합니다.
       4. 클릭 **예** 때 인증서에 대 한 경고 메시지를 받습니다.
   3. ODBC 연결 문자열의 버전과 일치하는 [SQL Server용 ODBC 드라이버](https://www.microsoft.com/download/confirmation.aspx?id=50420)를 다운로드합니다. 위의 예제 문자열에서는 버전 13 ODBC 드라이버를 설치해야 합니다.
   4. 첫 번째 RD 연결 브로커 서버에 sqlincli.msi 파일을 복사합니다.   
   5. sqlincli.msi 파일을 열고 Native Client를 설치합니다.  
   6. 각 추가 RD 연결 브로커(예: Contoso-Cb2)에 대해 1~5단계를 반복합니다.
   7. 연결 브로커를 실행할 각 서버에서 ODBC 드라이버를 설치합니다.

## <a name="step-2-configure-load-balancing-on-the-rd-connection-brokers"></a>2단계: RD 연결 브로커에서 부하 분산 구성 

Azure 인프라를 사용하는 경우 [Azure Load Balancer](#create-a-load-balancer)를 만들 수 있으며, 그렇지 않은 경우 [DNS 라운드 로빈](#configure-dns-round-robin)을 설정할 수 있습니다.

### <a name="create-a-load-balancer"></a>부하 분산 장치 만들기  
1. Azure Load Balancer 만들기   
      1. Azure Portal에서 **찾아보기 > 부하 분산 장치 > 추가**를 클릭합니다.   
      2. 새 부하 분산 장치의 이름(예: hacb)을 입력합니다.   
      3. **체계**에 대해 **내부**, 배포에 대해 **가상 네트워크**(예: Contoso-VNet)를 선택하고 모든 리소스가 있는 **서브넷**(예: 기본값)을 선택합니다.   
      4. **IP 주소 할당**에 대해 **정적**을 선택하고 현재 사용하고 있지 않은 **개인 IP 주소**(예: 10.0.0.32)를 입력합니다.   
      5. 해당 **구독**, 모든 리소스를 포함하는 **리소스 그룹**, 해당 **위치**를 선택합니다.   
      6. **만들기**를 선택합니다.   
2. 다음과 같이 [프로브](https://azure.microsoft.com/documentation/articles/load-balancer-custom-probe-overview/)를 만들어 활성 상태인 서버를 모니터링합니다.   
      1. Azure Portal에서 **찾아보기 > Load Balancer**를 클릭하고 방금 만든 부하 분산 장치(예: CBLB)를 클릭합니다. **설정**을 클릭합니다.   
      2. **프로브 > 추가**를 클릭합니다.   
      3. 프로브의 이름(예: **RDP**)을 선택하고 **프로토콜**로 **TCP**를 선택한 후 **포트**에 대해 **3389**를 입력하고 **확인**을 클릭합니다.   
3. 다음과 같이 연결 브로커의 백 엔드 풀을 만듭니다.   
      1. **설정**에서 **백 엔드 주소 풀 > 추가**를 클릭합니다.   
      2. 이름(예: CBBackendPool)을 입력한 다음, **가상 머신 추가**를 클릭합니다.  
      3. 가용성 집합(예: CbAvSet)을 선택하고 **확인**을 클릭합니다.   
      3. **가상 머신 선택**을 클릭하고 각 가상 머신을 선택한 후 **선택 > 확인 > 확인**을 클릭합니다.   
4. 다음과 같이 RDP 부하 분산 규칙을 만듭니다.   
      1. **설정**에서 **부하 분산 규칙**을 클릭하고 **추가**를 클릭합니다.   
      2. 이름(예: RDP)을 입력하고 **프로토콜**로 **TCP**를 선택한 후 **포트** 및 **백 엔드 포트** 둘 다에 대해 **3389**를 입력하고 **확인**을 클릭합니다.   
5. 다음과 같이 Load Balancer의 DNS 레코드를 추가합니다.   
      1. RDMS 서버 가상 머신(예: Contoso-CB1)에 연결합니다. VM에 연결하는 방법에 대한 단계는 [RD 연결 브로커 VM 준비](Prepare-the-RD-Connection-Broker-VM-for-Remote-Desktop.md) 문서를 확인하세요.   
      2. 서버 관리자에서 **도구 > DNS**를 클릭합니다.   
      3. 왼쪽 창에서 **DNS**를 확장하고 DNS 머신을 클릭한 후 **정방향 조회 영역**을 클릭하고 도메인 이름(예: Contoso.com)을 클릭합니다. (정보를 얻기 위해 DNS 서버에 대한 쿼리를 처리하는 데 몇 초 정도 걸릴 수 있습니다.)  
      4. **작업 > 새 호스트(A 또는 AAAA)** 를 클릭합니다.   
      9. 이름(예: hacb) 및 이전에 지정한 IP 주소(예: 10.0.0.32)를 입력합니다.   

### <a name="configure-dns-round-robin"></a>DNS 라운드 로빈 구성  
  
다음 단계는 Azure Internal Load Balancer를 만드는 대신 사용할 수 있습니다.   
  
1. Azure Portal에서 RDMS 서버에 연결합니다. 원격 데스크톱 연결 클라이언트 사용   
2. 다음과 같이 DNS 레코드를 만듭니다.   
      1. 서버 관리자에서 **도구 > DNS**를 클릭합니다.   
      2. 왼쪽 창에서 **DNS**를 확장하고 DNS 머신을 클릭한 후 **정방향 조회 영역**을 클릭하고 도메인 이름(예: Contoso.com)을 클릭합니다. (정보를 얻기 위해 DNS 서버에 대한 쿼리를 처리하는 데 몇 초 정도 걸릴 수 있습니다.)  
      3. **작업** 및 **새 호스트(A 또는 AAAA)** 를 클릭합니다.   
      4. RD 연결 브로커 클러스터의 **DNS 이름**(예: hacb)을 입력하고 첫 번째 RD 연결 브로커의 **IP 주소**를 입력합니다.   
      5. 각 추가 레코드의 고유한 각각의 IP 주소를 제공하여 각 추가 RD 연결 브로커에 대해 3~4단계를 반복합니다.


예를 들어, 두 RD 연결 브로커 가상 머신의 IP 주소가 10.0.0.8 및 10.0.0.9인 경우 다음과 같은 두 개의 DNS 호스트 레코드가 만들어집니다.
 - 호스트 이름: hacb.contoso.com, IP 주소: 10.0.0.8
 - 호스트 이름: hacb.contoso.com, IP 주소: 10.0.0.9

## <a name="step-3-configure-the-connection-brokers-for-high-availability"></a>3단계: 고가용성을 위해 연결 브로커 구성

1. 서버 관리자에 새 RD 연결 브로커 서버를 추가합니다.
   1. 서버 관리자에서 **관리 > 서버 추가**를 클릭합니다.
   2. **지금 찾기**를 클릭합니다.
   3. 새로 만든 RD 연결 브로커 서버(예: Contoso-Cb2)를 클릭하고 **확인**을 클릭합니다.
2. RD 연결 브로커의 고가용성 구성:
   1. 서버 관리자에서 클릭 **원격 데스크톱 서비스 > 개요**합니다.
   2. **RD 연결 브로커**를 마우스 오른쪽 단추로 클릭하고 **고가용성 구성**을 클릭합니다.
   3. 구성 형식 섹션에 도달할 때까지 마법사 페이지를 넘깁니다. **공유 데이터베이스 서버**를 선택하고 **다음**을 클릭합니다.
   4. RD 연결 브로커 클러스터의 DNS 이름을 입력합니다.
   5. SQL DB의 연결 문자열을 입력하고 마법사 페이지를 넘기면서 고가용성을 설정합니다.
3. 배포에 새 RD 연결 브로커 추가
   1. 서버 관리자에서 클릭 **원격 데스크톱 서비스 > 개요**합니다.
   2. RD 연결 브로커를 마우스 오른쪽 단추로 클릭하고 **RD 연결 브로커 서버 추가**를 클릭합니다.
   3. 마법사 페이지를 넘겨 서버 선택 영역에 도달한 후 새로 만든 RD 연결 브로커 서버(예: Contoso-CB2)를 선택합니다.
   4. 기본값을 그대로 적용하여 마법사를 완료합니다.
4. RD 연결 브로커 서버 및 클라이언트에서 신뢰할 수 있는 인증서를 구성합니다.

