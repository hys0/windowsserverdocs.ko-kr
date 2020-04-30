---
title: AlwaysOn 가용성 그룹를 사용 하 여 AD FS 배포 설정
author: billmath
ms.author: billmath
manager: daveba
ms.date: 01/20/2020
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8660bcab5719029936588738352e542828081ce8
ms.sourcegitcommit: 371e59315db0cca5bdb713264a62b215ab43fd0f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82192619"
---
# <a name="setting-up-an-ad-fs-deployment-with-alwayson-availability-groups"></a>AlwaysOn 가용성 그룹를 사용 하 여 AD FS 배포 설정
항상 사용 가능한 지리적으로 분산 된 토폴로지는 다음을 제공 합니다.
* 단일 실패 지점 제거: 장애 조치 (failover) 기능을 사용 하면 전 세계에 있는 데이터 센터 중 하나가 중단 되더라도 항상 사용 가능한 ADFS 인프라를 달성할 수 있습니다.
* 향상 된 성능: 제안 된 배포를 사용 하 여 고성능 ADFS 인프라를 제공할 수 있습니다.

AD FS는 항상 사용 가능한 지리적으로 분산 된 시나리오에 대해 구성할 수 있습니다.
다음 가이드에서는 SQL Always on 가용성 그룹을 사용 하는 AD FS의 개요를 살펴보고 배포 고려 사항 및 지침을 제공 합니다.

## <a name="overview---alwayson-availability-groups"></a>개요-AlwaysOn 가용성 그룹

AlwaysOn 가용성 그룹에 대 한 자세한 내용은 [AlwaysOn 가용성 그룹 개요 (SQL Server)](https://technet.microsoft.com/library/ff877884.aspx) 를 참조 하세요.

AD FS SQL Server 팜의 노드 관점에서 AlwaysOn 가용성 그룹은 단일 SQL Server 인스턴스를 정책/아티팩트 데이터베이스로 바꿉니다.가용성 그룹 수신기는 클라이언트 (AD FS 보안 토큰 서비스)가 SQL에 연결 하는 데 사용 하는 것입니다.
다음 다이어그램에서는 AlwaysOn 가용성 그룹에 대 한 AD FS SQL 서버 팜 보여 줍니다.

![SQL을 사용 하 여 서버 팜](media/ad-fs-always-on/SQLoverview.png)

AG (Always On 가용성 그룹)는 함께 장애 조치 (failover) 되는 하나 이상의 사용자 데이터베이스입니다. 가용성 그룹은 주 가용성 복제본과 공유 저장소를 필요로 하지 않고 데이터 보호를 위해 로그 기반 데이터 이동을 SQL Server 통해 유지 관리 되는 1-4 개의 보조 복제본으로 구성 됩니다. 각 복제본은 WSFC의 다른 노드에서 SQL Server의 인스턴스에 의해 호스팅됩니다. 가용성 그룹과 해당 가상 네트워크 이름은 WSFC 클러스터에 리소스로 등록됩니다.

주 복제본 노드의 가용성 그룹 수신기는 가상 네트워크 이름에 연결 하기 위해 들어오는 클라이언트 요청에 응답 하 고 연결 문자열의 특성을 기반으로 각 요청을 적절 한 SQL Server 인스턴스로 리디렉션합니다.
장애 조치 (failover) 시 공유 된 실제 리소스의 소유권을 다른 노드로 전송 하는 대신 WSFC를 활용 하 여 다른 SQL Server 인스턴스의 보조 복제본을 가용성 그룹의 주 복제본으로 다시 구성 합니다. 그러면 가용성 그룹의 가상 네트워크 이름 리소스가 해당 인스턴스로 전송됩니다.
지정 된 순간에 단일 SQL Server 인스턴스만 가용성 그룹 데이터베이스의 주 복제본을 호스팅할 수 있습니다. 연결 된 모든 보조 복제본은 각각 별도의 인스턴스에 위치 해야 하며 각 인스턴스는 별도의 실제 노드에 있어야 합니다.

> [!NOTE] 
> 컴퓨터가 Azure에서 실행 중인 경우 수신기 구성이 AlwaysOn 가용성 그룹과 통신할 수 있도록 Azure virtual machines를 설정 합니다. 자세한 내용은 [SQL Always On 수신기를 Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener)합니다.

AlwaysOn 가용성 그룹에 대 한 추가 개요는 [Always On 가용성 그룹 개요 (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-ver15)를 참조 하세요.

> [!NOTE] 
> 조직에서 여러 데이터 센터 간 장애 조치 (failover)를 수행 해야 하는 경우에는 각 데이터 센터에서 아티팩트 데이터베이스를 만들고 요청 처리 중에 대기 시간을 줄이는 백그라운드 캐시를 사용 하는 것이 좋습니다. [SQL을 미세 조정 하 고 대기 시간을 줄여](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/adfs-sql-latency)이 작업을 수행 하려면 지침을 따릅니다.

## <a name="deployment-guidance"></a>배포 지침

1. <b>AD FS 배포의 목적에 맞는 데이터베이스를 고려 하십시오.</b> AD FS는 데이터베이스를 사용 하 여 구성을 저장 하 고, 경우에 따라 페더레이션 서비스와 관련 된 트랜잭션 데이터를 저장 합니다. AD FS 소프트웨어를 사용 하 여 페더레이션 서비스에 데이터를 저장 하기 위해 WID (Windows 내부 데이터베이스) 또는 Microsoft SQL Server 2008 이상 버전을 선택할 수 있습니다.
다음 표에서는 WID와 SQL 데이터베이스 간에 지원 되는 기능의 차이점을 설명 합니다.


| Category      | 기능       | WID에서 지원  | SQL에서 지원 |
| ------------------ |:-------------:| :---:|:---: |
| AD FS 기능     | 페더레이션 서버 팜 배포 | 예  | 예 |
| AD FS 기능     | SAML 아티팩트 확인 참고: SAML 응용 프로그램에는 일반적이 지 않습니다.     |   예 | 예  |
| AD FS 기능 | SAML/WS-FEDERATION 토큰 재생 검색 참고: AD FS는 외부 IDPs에서 토큰을 수신 하는 경우에만 필요 합니다. AD FS 페더레이션 파트너로 작동 하지 않는 경우에는 필요 하지 않습니다.      |    예  | 예 |
| 데이터베이스 기능     |   끌어오기 복제를 사용 하는 기본 데이터베이스 중복성 (데이터베이스의 읽기 전용 복사본을 호스트 하는 하나 이상의 서버에서 원본 서버에 적용 된 변경 내용을 데이터베이스의 읽기/쓰기 복사본으로 요청)    |   아니요 | 예  |
| 데이터베이스 기능 | 데이터베이스 계층에서 클러스터링 또는 미러링 등의 고가용성 솔루션을 사용 하는 데이터베이스 중복성      |    예  | 예 |
| 추가 기능 | OAuth Authcode 시나리오     |   예  | 예 |

페더레이션 응용 프로그램 또는 서비스에 대 한 single sign-on 액세스를 사용 하 여 내부 사용자와 외부 사용자를 모두 제공 해야 하는 100 개 이상의 트러스트 관계가 있는 대기업 인 경우 SQL이 권장 옵션입니다.

구성 된 트러스트 관계가 100 이하인 조직에서는 WID가 데이터 및 페더레이션 서비스 중복성을 제공 합니다. 여기서 각 페더레이션 서버는 동일한 팜의 다른 페더레이션 서버에 변경 내용을 복제 합니다. WID는 토큰 재생 검색 또는 아티팩트 확인을 지원 하지 않으며 페더레이션 서버를 30 개로 제한 합니다.
배포 계획에 대 한 자세한 내용은 [여기](https://docs.microsoft.com/windows-server/identity/ad-fs/design/planning-your-deployment)를 참조 하세요.

## <a name="sql-server-high-availability-solutions"></a>고가용성 솔루션 SQL Server
AD FS 구성 데이터베이스로 SQL Server를 사용 하는 경우 SQL Server 복제를 사용 하 여 AD FS 팜에 대 한 지리적 중복성을 설정할 수 있습니다. 지리적 중복은 두 지리적으로 멀리 떨어진 사이트 간에 데이터를 복제 하므로 응용 프로그램이 한 사이트에서 다른 사이트로 전환할 수 있습니다. 이러한 방식으로 한 사이트의 장애가 발생 하는 경우에도 두 번째 사이트에서 모든 구성 데이터를 사용할 수 있습니다. 
SQL이 배포 목표에 적합 한 데이터베이스인 경우이 배포 가이드를 계속 진행 합니다.

이 가이드는 다음을 안내 합니다.
* AD FS 배포
* AlwaysOn 가용성 그룹를 사용 하도록 AD FS 구성
* 장애 조치 (Failover) 클러스터링 역할 설치
* 클러스터 유효성 검사 테스트 실행
* Always On 가용성 그룹 사용
* AD FS 데이터베이스 백업
* AlwaysOn 가용성 그룹 만들기
* 두 번째 노드에 데이터베이스 추가
* 가용성 그룹에 가용성 복제본 조인
* SQL 연결 문자열 업데이트

## <a name="deploy-ad-fs"></a>AD FS 배포

> [!NOTE] 
> 컴퓨터를 Azure에서 실행 하는 경우 수신기가 Always On 가용성 그룹과 통신할 수 있도록 특정 방법으로 Virtual Machines를 구성 해야 합니다. 구성에 대 한 자세한 내용은 [Azure SQL Server vm에서 가용성 그룹에 대 한 부하 분산 장치 구성](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener) 을 참조 하세요.


이 배포 가이드에서는 두 개의 SQL server가 있는 두 개의 노드 팜을 보여 줍니다.
AD FS 배포 하려면 아래 초기 링크를 따라 AD FS 역할 서비스를 설치 합니다. AoA 그룹에 대해를 구성 하기 위해 역할에 대 한 추가 단계를 수행 합니다.
-   [도메인에 컴퓨터 가입](https://docs.microsoft.com/windows-server/identity/ad-fs/deployment/join-a-computer-to-a-domain)
-   [AD FS용 SSL 인증서 등록](https://docs.microsoft.com/windows-server/identity/ad-fs/deployment/enroll-an-ssl-certificate-for-ad-fs)
-   [AD FS 역할 서비스 설치](https://docs.microsoft.com/windows-server/identity/ad-fs/deployment/install-the-ad-fs-role-service)


## <a name="configuring-ad-fs-to-use-an-alwayson-availability-group"></a>AlwaysOn 가용성 그룹을 사용 하도록 AD FS 구성

AlwaysOn 가용성 그룹을 사용 하 여 AD FS 팜을 구성 하려면 AD FS 배포 절차를 약간 수정 해야 합니다. 각 서버 인스턴스가 같은 버전의 SQL을 실행 하 고 있는지 확인 합니다. Always On 가용성 그룹에 대 한 필수 조건, 제한 사항 및 권장 사항의 전체 목록을 보려면 [여기](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability?view=sql-server-2017#PrerequisitesForDbs)를 참조 하세요.

1.  AlwaysOn 가용성 그룹을 구성 하기 전에 백업 하려는 데이터베이스를 만들어야 합니다.  AD FS 설치 및 새 AD FS SQL 서버 팜의 첫 번째 페더레이션 서비스 노드의 초기 구성의 일부로 해당 데이터베이스를 만듭니다.  SQL server를 사용 하 여 기존 팜에 대 한 데이터베이스 호스트 이름을 지정 합니다. AD FS 구성의 일부로 sql 연결 문자열을 지정 해야 합니다. 따라서 SQL 인스턴스에 직접 연결 하도록 첫 번째 AD FS 팜을 구성 해야 합니다 (임시 전용). SQL server 연결 문자열에서 AD FS 팜에 노드를 구성 하는 등, AD FS 팜 구성에 대 한 특정 지침은 참조 하십시오. [페더레이션 서버 구성](https://docs.microsoft.com/windows-server/identity/ad-fs/deployment/configure-a-federation-server)합니다.

![팜 지정](media/ad-fs-always-on/deploymentSpecifyFarm.png)

2.  SSMS를 사용 하 여 데이터베이스에 대 한 연결을 확인 하 고 대상 데이터베이스 호스트 이름에 연결 합니다. 페더레이션 팜에 다른 노드를 추가 하는 경우 대상 데이터베이스에 연결 합니다.
3.  AD FS 팜에 대 한 SSL 인증서를 지정 합니다.

![ssl 인증서 지정](media/ad-fs-always-on/deploymentSpecifySSL.png)

4.  팜을 서비스 계정 또는 gMSA에 연결 합니다.

![서비스 계정 지정](media/ad-fs-always-on/deploymentSpecifyServiceAccount.png)

5.  AD FS 팜 구성 및 설치를 완료 합니다.

> [!NOTE] 
> Always On 가용성 그룹을 설치 하려면 도메인 계정으로 SQL Server를 실행 해야 합니다. 기본적으로 로컬 시스템으로 실행 됩니다.

## <a name="install-the-failover-clustering-role"></a>장애 조치 (Failover) 클러스터링 역할 설치
Windows server 장애 조치 (failover) 클러스터 역할은 Windows Server 장애 조치 (Failover) 클러스터에 대 한 자세한 정보를 제공 합니다.
1.  서버 관리자를 시작합니다.
2.  관리 메뉴에서 역할 및 기능 추가를 선택 합니다.
3.  시작 하기 전에 페이지에서 다음을 선택 합니다.
4.  설치 유형 선택 페이지에서 역할 기반 또는 기능 기반 설치를 선택 하 고 다음을 선택 합니다.
5.  대상 서버 선택 페이지에서 기능을 설치 하려는 SQL server를 선택 하 고 다음을 선택 합니다.

![대상 서버](media/ad-fs-always-on/clusteringDestinationServer.png)

6.  서버 역할 선택 페이지에서 다음을 선택합니다.
7.  기능 선택 페이지에서 장애 조치(failover) 클러스터링 확인란을 선택합니다.

![클러스터링 기능 선택](media/ad-fs-always-on/clusteringFeature.png)

8.  설치 선택 확인 페이지에서 설치를 선택 합니다.
장애 조치(failover) 클러스터링 기능에는 서버를 다시 시작할 필요가 없습니다.
9.  설치가 완료 되 면 닫기를 선택 합니다.
10. 클러스터 노드로 추가할 모든 서버에 장애 조치(failover) 클러스터링 기능 설치

## <a name="run-cluster-validation-tests"></a>클러스터 유효성 검사 테스트 실행
1.  원격 서버 관리 도구에서 장애 조치(failover) 클러스터 관리 도구를 설치한 컴퓨터 또는 장애 조치(failover) 클러스터링 기능을 설치한 서버에서 장애 조치(failover) 클러스터 관리자를 시작합니다. 서버에서이 작업을 수행 하려면 서버 관리자을 시작 하 고 도구 메뉴에서 장애 조치(Failover) 클러스터 관리자를 선택 합니다.
2.  장애 조치(Failover) 클러스터 관리자 창의 관리에서 구성 유효성 검사를 선택 합니다.
3.  시작하기 전에 페이지에서 다음을 선택합니다.
4.  서버 또는 클러스터 선택 페이지의 이름 입력 상자에 NetBIOS 이름 또는 장애 조치 (failover) 클러스터 노드로 추가 하려는 서버의 정규화 된 도메인 이름을 입력 한 다음 추가를 선택 합니다. 추가하려는 각 서버에 대해 이 단계를 반복합니다. 여러 서버를 동시에 추가하려면 쉼표 또는 세미콜론으로 이름을 구분합니다. 예를 들어 server1.contoso.com, server2.contoso.com 형식으로 이름을 입력합니다. 작업을 마쳤으면 다음을 선택합니다.

![서버 선택 그림](media/ad-fs-always-on/clusterValidationServers.png)

5. 테스트 옵션 페이지에서 모든 테스트 실행 (권장)을 선택 하 고 다음을 선택 합니다.
6. 확인 페이지에서 다음을 선택 합니다.
유효성 검사 중 페이지에 실행 중인 테스트의 상태가 표시됩니다.
7. 요약 페이지에서 다음 중 하나를 수행합니다.
- 결과가 테스트가 성공적으로 완료 되 고 구성이 클러스터링에 적합 한 것으로 표시 되는 경우 클러스터를 즉시 만들려면 유효성이 검사 된 노드를 사용 하 여 클러스터 만들기 확인란이 선택 되어 있는지 확인 한 다음 마침을 선택 합니다. 그런 다음 [장애 조치 (failover) 클러스터 만들기 절차](https://docs.microsoft.com/windows-server/failover-clustering/create-failover-cluster#create-the-failover-cluster)의 4 단계를 계속 진행 합니다.

![구성 확인 그림](media/ad-fs-always-on/clusterValidationResults.png)

-   경고 또는 오류가 발생 했음을 나타내는 결과가 표시 되 면 보고서 보기를 선택 하 여 세부 정보를 확인 하 고 수정 해야 하는 문제를 확인 합니다. 특정 유효성 검사 테스트에 대한 경고에서는 장애 조치(failover) 클러스터의 해당 측면이 지원될 수 있지만 권장 모범 사례에는 맞지 않을 수 있음을 나타냅니다.

> [!NOTE]
> 스토리지 공간 영구 예약 유효성 검사 테스트에 대한 경고를 받은 경우 자세한 내용은 블로그 게시물 [Windows 장애 조치(failover) 클러스터 유효성 검사에서 디스크가 스토리지 공간에 대한 영구 예약을 지원하지 않음을 나타내는 경고가 표시됨](https://blogs.msdn.microsoft.com/clustering/2013/05/24/validate-storage-spaces-persistent-reservation-test-results-with-warning/)을 참조하세요.
> 하드웨어 유효성 검사 테스트에 대한 자세한 내용은 [장애 조치(failover) 클러스터에 대한 하드웨어 유효성 검사](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11))를 참조하세요.

## <a name="create-the-failover-cluster"></a>장애 조치 클러스터 만들기

이 단계를 완료하려면 로그온한 사용자 계정이 이 항목의 [필수 구성 요소 확인](https://docs.microsoft.com/windows-server/failover-clustering/create-failover-cluster#verify-the-prerequisites) 섹션에 설명된 요구 사항을 충족해야 합니다.
1.  서버 관리자를 시작합니다.
2.  도구 메뉴에서 장애 조치(Failover) 클러스터 관리자를 선택 합니다.
3.  장애 조치(Failover) 클러스터 관리자 창의 관리 아래에서 클러스터 만들기를 선택 합니다.
클러스터 만들기 마법사가 열립니다.
4.  시작하기 전에 페이지에서 다음을 선택합니다.
5.  서버 선택 페이지가 표시 되 면 이름 입력 상자에 NetBIOS 이름 또는 장애 조치 (failover) 클러스터 노드로 추가 하려는 서버의 정규화 된 도메인 이름을 입력 한 다음 추가를 선택 합니다. 추가하려는 각 서버에 대해 이 단계를 반복합니다. 여러 서버를 동시에 추가하려면 쉼표 또는 세미콜론으로 이름을 구분합니다. 예를 들어 server1.contoso.com, server2.contoso.com 형식으로 이름을 입력합니다. 작업을 마쳤으면 다음을 선택합니다.

![클러스터 만들기 및 서버 선택](media/ad-fs-always-on/createClusterServers.png)

> [!NOTE]
> [구성 유효성 검사 절차](https://docs.microsoft.com/windows-server/failover-clustering/create-failover-cluster#validate-the-configuration)에서 유효성 검사를 실행 한 직후에 클러스터를 만들도록 선택한 경우에는 서버 선택 페이지가 표시 되지 않습니다. 유효성을 검사한 노드는 클러스터 만들기 마법사에 자동으로 추가되므로 다시 입력할 필요가 없습니다.

6.  앞에서 유효성 검사를 건너뛴 경우 유효성 검사 경고 페이지가 나타납니다. 클러스터 유효성 검사를 실행하는 것이 좋습니다. Microsoft에서는 모든 유효성 검사 테스트를 통과한 클러스터만 지원합니다. 유효성 검사 테스트를 실행 하려면 예를 선택 하 고 다음을 선택 합니다. [구성 유효성 검사](https://docs.microsoft.com/windows-server/failover-clustering/create-failover-cluster#validate-the-configuration)에 설명 된 대로 구성 유효성 검사 마법사를 완료 합니다.
7.  클러스터 관리 액세스 지점 페이지에서 다음을 수행합니다.
-   클러스터 이름 상자에 클러스터를 관리하는 데 사용할 이름을 입력합니다. 그 전에 먼저 다음 정보를 검토합니다.
 -  클러스터를 만드는 동안 이 이름이 AD DS에 클러스터 컴퓨터 개체( 클러스터 이름 개체 또는 CNO라고도 함)로 등록됩니다. 클러스터의 NetBIOS 이름을 지정한 경우 클러스터 노드의 컴퓨터 개체가 있는 곳과 동일한 위치에 CNO가 만들어집니다. 이는 기본 컴퓨터 컨테이너 또는 OU일 수 있습니다.
 -  CNO의 다른 위치를 지정하려면 클러스터 이름 상자에 OU의 고유 이름을 입력하면 됩니다. 예: CN=ClusterName, OU=Clusters, DC=Contoso, DC=com
 -  도메인 관리자가 클러스터 노드에 있는 것과 다른 OU에서 CNO를 사전 준비한 경우 도메인 관리자가 제공하는 고유 이름을 지정합니다.
- 서버에 DHCP를 사용하도록 구성된 네트워크 어댑터가 없는 경우 장애 조치(failover) 클러스터의 고정 IP 주소를 하나 이상 구성해야 합니다. 클러스터 관리에 사용할 각 네트워크 옆의 확인란을 선택합니다. 선택한 네트워크 옆의 주소 필드를 선택한 다음 클러스터에 할당할 IP 주소를 입력 합니다. 이 IP 주소는 DNS(Domain Name System)에서 클러스터 이름에 연결됩니다.
- 작업을 마쳤으면 다음을 선택합니다.

8.  확인 페이지에서 설정을 검토합니다. 기본적으로 클러스터에 사용할 수 있는 모든 저장소를 추가하세요. 확인란이 선택되어 있습니다. 다음 중 하나를 수행하려면 이 확인란의 선택을 취소합니다.
-   나중에 스토리지를 구성하려는 경우
-   파일 및 스토리지 서비스에서 스토리지 공간을 아직 만들지 않았으며, 장애 조치(failover) 클러스터 관리자 또는 장애 조치(failover) 클러스터링 Windows PowerShell cmdlet을 통해 클러스터된 스토리지 공간을 만들려는 경우 자세한 내용은 [클러스터된 스토리지 공간 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11))를 참조하세요.
9.  다음을 선택 하 여 장애 조치 (failover) 클러스터를 만듭니다.
10. 요약 페이지에서 장애 조치(failover) 클러스터가 성공적으로 만들어졌는지 확인합니다. 경고나 오류가 있는 경우 요약 출력을 보거나 보고서 보기를 선택 하 여 전체 보고서를 확인 합니다. 마침을 선택합니다.
11. 클러스터가 만들어졌는지 확인하려면 탐색 트리의 장애 조치(failover) 클러스터 관리자 아래에 클러스터 이름이 있는지 확인합니다. 클러스터 이름을 확장 하 고 노드, 저장소 또는 네트워크 아래의 항목을 선택 하 여 연결 된 리소스를 볼 수 있습니다.
DNS에서 클러스터 이름을 복제하는 데 약간의 시간일 걸릴 수 있습니다. DNS 등록 및 복제가 성공한 후 서버 관리자에서 모든 서버를 선택 하면 클러스터 이름이 관리 효율성 상태가 온라인 인 서버로 나열 됩니다.

![클러스터 만들기 완료](media/ad-fs-always-on/createClusterComplete.png)

## <a name="enable-always-on-availability-groups-with-sql-server-configuration-manager"></a>SQL Server 구성 관리자를 사용 하 여 Always on 가용성 그룹 사용

1.  Always On 가용성 그룹을 사용 하도록 설정 하려는 SQL Server 인스턴스를 호스팅하는 WSFC (Windows Server 장애 조치 (Failover) 클러스터) 노드에 연결 합니다.
2.  시작 메뉴에서 모든 프로그램, Microsoft SQL Server, 구성 도구을 차례로 가리킨 다음 SQL Server 구성 관리자를 클릭 합니다.
3.  SQL Server 구성 관리자에서 SQL Server Services를 클릭 하 고 SQL Server (<instance name>)를 마우스 오른쪽 단추로 <instance name> 클릭 한 다음 속성을 클릭 합니다. 여기서은 Always On 가용성 그룹을 사용 하도록 설정 하려는 로컬 서버 인스턴스의 이름입니다.
4.  Always On 고가용성 탭을 선택합니다.
5.  Windows 장애 조치(failover) 클러스터 이름 필드에 로컬 장애 조치(failover) 클러스터의 이름이 포함되어 있는지 확인합니다. 이 필드가 비어 있으면이 서버 인스턴스에서 현재 Always On 가용성 그룹을 지원 하지 않습니다. 로컬 컴퓨터가 클러스터 노드가 아니거나 WSFC 클러스터가 종료 되었거나 Always On 가용성 그룹를 지원 하지 않는이 버전의 SQL Server입니다.
6.  Always On 가용성 그룹 사용 확인란을 선택하고 확인을 클릭합니다.
SQL Server 구성 관리자가 변경 내용을 저장합니다. 그런 다음 SQL Server 서비스를 수동으로 다시 시작해야 합니다. 이렇게 하면 비즈니스 요구 사항에 가장 적합한 다시 시작 시간을 선택할 수 있습니다. SQL Server 서비스가 다시 시작 되 면 Always On 사용 하도록 설정 되 고 IsHadrEnabled 서버 속성이 1로 설정 됩니다.

![AoA 사용](media/ad-fs-always-on/enableAoAGroup.png)

## <a name="back-up-ad-fs-databases"></a>AD FS 데이터베이스 백업
전체 트랜잭션 로그를 사용 하 여 AD FS 구성 및 아티팩트 데이터베이스를 백업 합니다. 선택한 대상에 백업을 저장 합니다.
ADFS 아티팩트 및 구성 데이터베이스를 백업 합니다.
- 백업 > 백업 > 전체에 추가 > 백업 파일에 추가 > 확인 작업을 만듭니다.

![서버 백업](media/ad-fs-always-on/backUpADFS.png)

## <a name="create-new-availability-group"></a>새 가용성 그룹 만들기

1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.
2.  Always On 고가용성 노드 및 가용성 그룹 노드를 확장합니다.
3.  새 가용성 그룹 마법사를 시작하려면 새 가용성 그룹 마법사 명령을 선택합니다.
4.  이 마법사를 처음 실행하는 경우 소개 페이지가 나타납니다. 다음부터 이 페이지를 건너뛰려면 이 페이지를 다시 표시 안 함을 클릭합니다. 이 페이지를 읽은 후 다음을 클릭합니다.
5.  가용성 그룹 옵션 지정 페이지의 가용성 그룹 이름 필드에서 새 가용성 그룹의 이름을 입력합니다. 이 이름은 클러스터와 도메인 전체에서 고유 하 고 유효한 SQL Server 식별자 여야 합니다. 가용성 그룹 이름의 최대 길이는 128자입니다. e
6.  다음으로 클러스터 유형을 지정합니다. 가능한 클러스터 유형은 SQL Server 버전 및 운영 체제에 따라 달라 집니다. WSFC, 외부 또는 없음 중 하나를 선택합니다. 자세한 내용은 [가용성 그룹 이름 지정](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/specify-availability-group-name-page?view=sql-server-ver15) 페이지를 참조 하세요.

![이름 AoA 그룹 및 클러스터](media/ad-fs-always-on/createAoAName.png)

7.  데이터베이스 선택 페이지의 표에 가용성 데이터베이스로 적합한 연결된 서버 인스턴스의 사용자 데이터베이스가 나열됩니다. 나열된 데이터베이스 중 새 가용성 그룹에 참여할 데이터베이스를 하나 이상 선택합니다. 이러한 데이터베이스가 초기 주 데이터베이스가 됩니다.
나열된 각 데이터베이스의 크기 열에 데이터베이스 크기(알려진 경우)가 표시됩니다. 상태 열에는 지정 된 데이터베이스가 가용성 데이터베이스의 [필수 구성 요소](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability?view=sql-server-ver15) 를 충족 하는지 여부가 표시 됩니다. 필수 구성 요소가 충족되지 않는 경우 데이터베이스가 부적합한 이유(예: 전체 복구 모델을 사용하지 않는 경우)를 설명하는 간략한 상태 설명이 나타납니다. 자세한 내용을 보려면 상태 설명을 클릭하세요.
데이터베이스를 적합하도록 변경한 경우 새로 고침을 클릭하여 데이터베이스 표를 업데이트합니다.
데이터베이스에 데이터베이스 마스터 키가 들어 있는 경우 데이터베이스 마스터 키에 대한 암호를 암호 열에 입력합니다.

![AoA 용 데이터베이스 선택](media/ad-fs-always-on/createAoASelectDb.png)

8. 복제본 지정 페이지에서 새 가용성 그룹에 대해 하나 이상의 복제본을 지정 하 고 구성 합니다. 이 페이지에는 네 개의 탭이 있습니다. 다음 표에서는 이러한 탭을 보여 줍니다. 자세한 내용은 [복제본 지정 페이지 (새 가용성 그룹 마법사: 복제본 추가 마법사)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard?view=sql-server-ver15) 항목을 참조 하세요.

| 탭      | 간략한 설명       |
| ------------------ |:-------------:|
| 복제본     | 이 탭을 사용 하 여 보조 복제본을 호스팅할 SQL Server의 각 인스턴스를 지정할 수 있습니다. 현재 연결된 서버 인스턴스가 주 복제본을 호스팅해야 합니다. |
| 엔드포인트     | 기존 데이터베이스 미러링 엔드포인트를 확인하고, 서비스 계정에서 Windows 인증을 사용하는 서버 인스턴스에 이 엔드포인트가 없는 경우 엔드포인트를 자동으로 만들려면 이 탭을 사용합니다.|
| 백업 기본 설정 | 가용성 그룹 전체에 대한 백업 기본 설정과 개별 가용성 복제본에 대한 백업 우선 순위를 지정하려면 이 탭을 사용합니다.      |
| 수신기     | 이 탭을 사용하여 가용성 그룹 수신기를 만들 수 있습니다. 기본적으로 마법사는 수신기를 만들지 않습니다.      |

![복제본 정보 지정](media/ad-fs-always-on/createAoAchooseReplica.png)

9. 초기 데이터 동기화 선택 페이지에서 새 보조 복제본을 만들고 가용성 그룹에 조인할 방법을 선택합니다. 다음 옵션 중 하나를 선택합니다.
-   자동 시드
 - SQL Server는 자동으로 그룹의 모든 데이터베이스에 대한 보조 복제본을 만듭니다. 자동 시드를 사용하려면 데이터 및 로그 파일 경로가 그룹에 참여하는 모든 SQL Server 인스턴스에서 동일해야 합니다. SQL Server 2016 (17.x) 이상에서 사용할 수 있습니다. [자동으로 Always On 가용성 그룹 초기화](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group?view=sql-server-ver15)를 참조 하세요.
- 전체 데이터베이스 및 로그 백업
 - 사용자 환경이 초기 데이터 동기화를 자동으로 시작 하기 위한 요구 사항을 충족 하는 경우이 옵션을 선택 합니다. 자세한 내용은 [이 항목의 앞부분에 나오는 필수 구성 요소, 제한 사항 및 권장 사항](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio?view=sql-server-ver15#Prerequisites)을 참조 하세요.
전체를 선택한 후 가용성 그룹을 만들면 마법사에서 모든 주 데이터베이스와 해당 트랜잭션 로그를 네트워크 공유에 백업하고 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 백업을 복원합니다. 그런 다음 모든 보조 데이터베이스를 가용성 그룹에 조인합니다.
모든 복제본에서 액세스할 수 있는 공유 네트워크 위치 지정: 필드에서 복제본을 호스팅하는 모든 서버 인스턴스에 읽기/쓰기 액세스 권한이 있는 백업 공유를 지정합니다. 자세한 내용은 이 항목의 앞부분에 나오는 필수 구성 요소를 참조하세요. 유효성 검사 단계에서 마법사는 제공된 네트워크 위치가 유효한지 확인하는 테스트를 수행하고, 테스트는 Guid가 뒤에 오는 "BackupLocDb_"라는 주 복제본에 데이터베이스를 만들고 제공된 네트워크 위치로 백업을 수행한 다음, 보조 복제본에서 복원합니다. 마법사가 삭제하지 못하는 경우에 백업 기록 및 백업 파일과 함께 이 데이터베이스를 삭제하는 것이 안전합니다.
- 조인만
 - 보조 복제본을 호스팅할 서버 인스턴스에서 보조 데이터베이스를 수동으로 준비하는 경우 이 옵션을 선택할 수 있습니다. 마법사에서 기존 보조 데이터베이스를 가용성 그룹에 조인합니다.
- 초기 데이터 동기화 건너뛰기
 - 주 데이터베이스의 로그 백업과 사용자 데이터베이스를 사용하려는 경우 이 옵션을 선택합니다. 자세한 내용은 [Always On 보조 데이터베이스에서 데이터 이동 시작 (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server?view=sql-server-ver15)을 참조 하세요.

![데이터 동기화 옵션 선택](media/ad-fs-always-on/createAoADataSync.png)

9.  유효성 검사 페이지에서는 이 마법사에서 지정한 값이 새 가용성 그룹 마법사의 요구 사항을 충족하는지 여부를 확인합니다. 변경하려면 이전을 클릭하여 이전 마법사 페이지로 돌아가서 하나 이상의 값을 변경합니다. 다음을 클릭하여 유효성 검사 페이지로 돌아가서 유효성 검사 다시 실행을 클릭합니다.

10. 요약 페이지에서 새 가용성 그룹에 대한 선택 사항을 확인합니다. 변경하려면 이전을 클릭하여 관련 페이지로 돌아갑니다. 변경 후에는 다음을 클릭하여 요약 페이지로 돌아갑니다.

> [!NOTE] 
> 새 가용성 복제본을 호스팅하는 서버 인스턴스의 SQL Server 서비스 계정이 로그인으로 존재 하지 않는 경우 새 가용성 그룹 마법사에서 로그인을 만들어야 합니다. 요약 페이지에 만들 로그인에 대한 정보가 표시됩니다. 마침을 클릭하면 SQL Server 서비스 계정에 대해 이 로그인이 만들어지고 로그인에 CONNECT 권한이 부여됩니다.
> 선택이 완료되었으면 필요에 따라 스크립트를 클릭하여 마법사에서 실행할 단계에 대한 스크립트를 만들 수 있습니다. 새 가용성 그룹을 만들어 구성하려면 마침을 클릭합니다.

11. 진행률 페이지에 가용성 그룹을 만들기 위한 단계(엔드포인트 구성, 가용성 그룹 만들기 및 가용성 그룹에 보조 복제본 조인)의 진행 상태가 표시됩니다.
12. 이러한 단계가 완료되면 결과 페이지에 각 단계의 결과가 표시됩니다. 단계가 모두 성공하면 새 가용성 그룹이 완전히 구성됩니다. 어느 단계에서라도 오류가 발생하는 경우 수동으로 구성을 완료하거나 실패한 단계에 대해 마법사를 사용해야 합니다. 주어진 오류의 원인에 대한 자세한 내용을 보려면 결과 열에서 연결된 "오류" 링크를 클릭합니다.
마법사가 완료되면 닫기를 클릭하여 종료합니다.

![유효성 검사 완료](media/ad-fs-always-on/createAoAValidation.png)

## <a name="add-databases-on-secondary-node"></a>보조 노드에 데이터베이스 추가

1.  만든 백업 파일을 사용 하 여 보조 노드의 UI를 통해 아티팩트 데이터베이스를 복원 합니다.
![UI를 통해 복원](media/ad-fs-always-on/restoreDB.png)

2. 복구 불가능 한 상태에서 데이터베이스를 복원 합니다.
![복구를 사용 하지 않는 복원](media/ad-fs-always-on/restoreNonRecovery.png)

3. 프로세스를 반복 하 여 구성 데이터베이스를 복원 합니다.

## <a name="join-availability-replica-to-an-availability-group"></a>가용성 그룹에 가용성 복제본 조인

1.  개체 탐색기에서 보조 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장할 서버 이름을 클릭합니다.
2.  Always On 고가용성 노드 및 가용성 그룹 노드를 확장합니다.
3.  연결된 보조 복제본의 가용성 그룹을 선택합니다.
4.  보조 복제본을 마우스 오른쪽 단추로 클릭하고 가용성 그룹에 조인을 클릭합니다.
5.  가용성 그룹에 복제본 조인 대화 상자가 열립니다.
6.  가용성 그룹에 보조 복제본을 조인하려면 확인을 클릭합니다.

![보조 복제본 조인](media/ad-fs-always-on/jointoAoA.png)

## <a name="update-the-sql-connection-string"></a>SQL 연결 문자열 업데이트
마지막으로 PowerShell을 사용 하 여 AD FS 속성을 편집 하 여 AlwaysOn 가용성 그룹 수신기의 DNS 주소를 사용 하도록 SQL 연결 문자열을 업데이트 합니다.
각 노드에서 구성 데이터베이스 변경을 실행 하 고 모든 ADFS 노드에서 ADFS 서비스를 다시 시작 합니다. 초기 카탈로그 값은 팜 버전에 따라 변경 됩니다.

```
PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService
PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”
PS:\>$temp.put()
PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”
```
