---
ms.assetid: e983d2ab-4153-41e7-b243-12cf7d71a552
title: "Federation 서버 팜 SQL Server를 사용 하 여"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2333f79c733415833b1d54afc8c385700ac5581e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="federation-server-farm-using-sql-server"></a>Federation 서버 팜 SQL Server를 사용 하 여

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

이 대 한 Active Directory Federation Services \(AD FS\)이 토폴로지 해당 그룹에 각 federation 서버에 데이터 복제 하지 않고 Windows 내부 데이터베이스 \(WID\) 배포가 사용 하 여 federation 서버 농장에서 다릅니다. 대신, 그룹의 모든 federation 서버 읽고 회사 네트워크에 있는 Microsoft SQL Server 실행 하는 서버에 저장 된 일반적인 데이터베이스에 데이터 쓸 수 있습니다.  
  
> [!IMPORTANT]  
> ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 및 SQL Server 2012와 SQL Server 2014를 포함 하 여 최신 버전을 사용할 수 있습니다.  
  
## <a name="deployment-considerations"></a>배포 고려  
이 여기서 대상, 혜택을 및이 배포가와 관련 된 제한 사항에 대 한 다양 한 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지 사용 해야 하나요?  
  
-   대기업 단일 sign\ 켜 짐 \(SSO\)에 액세스할 수 있는 연결 된 응용 프로그램 또는 서비스의 내부 사용자 및 외부 사용자에 게 제공 해야 하는 100 개 이상의 보안 관계  
  
-   이미 조직 SQL Server 사용와의 기존 도구 및 전문가 이용.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지에 사용 하는 어떤 혜택이 있나요?  
  
-   많은 수의 신뢰 관계에 대 한 지원이 \(more than 100\)  
  
-   토큰 재생 검색에 대 한 지원이 \(a security feature\) 아티팩트 해상도 \ (보안 설정 Markup Language \(SAML\) 2.0의 일부로 protocol\)  
  
-   미러링, 클러스터링, 보고 하 고, 관리 도구 장애 조치 같은 SQL Server 전체 혜택에 대 한 지원  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여 제한 이란 무엇 인가요?  
  
-   이 토폴로지 기본적으로 중복 데이터베이스를 제공 하지 않습니다. 자동으로 WID 토폴로지 federation 서버 팜 팜 각 federation 서버에서 WID 데이터베이스를 복제, 있지만 SQL Server 토폴로지 federation 서버 팜 하나만 데이터베이스를 포함 하는  
  
> [!NOTE]  
> SQL Server 여러 다양 한 데이터와 클러스터링, 데이터베이스 미러링 및 여러 가지 유형의 SQL Server 복제 포함 하 여 응용 프로그램 중복 옵션을 지원 합니다.  
  
Microsoft 정보 기술 \(IT\) 부서 SQL Server \(synchronous\) high\ 안전 모드 및 장애 조치 SQL Server 인스턴스 high\ 가용성 지원을 제공 하기 위해 클러스터링 미러링 사용 합니다. 트랜잭션 \(peer\-to\-peer\) SQL Server 및 병합 복제 Microsoft ADFS 제품 팀에서 테스트 되지 않았습니다. SQL Server에 대 한 자세한 내용은 참조 [높은 가용성 솔루션 개요](https://go.microsoft.com/fwlink/?LinkId=179853) 또는 [적절 한 복제 유형 선택](https://go.microsoft.com/fwlink/?LinkId=214648)합니다.  
  
### <a name="supported-sql-server-versions"></a>지원 되는 SQL Server 버전  
다음 SQL server 버전이 ADFS Windows Server 2012 r 2에서와 지원 됩니다.  
  
-   SQL Server 2008 \ / R2  
  
-   SQL Server 2012  
  
-   2014 SQL Server  
  
## <a name="server-placement-and-network-layout-recommendations"></a>네트워크 위치와 위치 레이아웃 추천 서버  
Federation 서버 팜 WID 토폴로지와 마찬가지로의 모든 팜 federation 서버 사용 하도록 구성 된 하나 클러스터 Domain Name System \(DNS\) 이름 \ (Federation 서비스 name\ 나타내는) 및 네트워크 부하 분산 \(NLB\) 클러스터 구성의 일환으로 한 클러스터 IP 주소 합니다. 이렇게 하면 NLB 호스트가 개별 federation 서버에 요청 클라이언트를 할당 합니다. Federation 서버 프록시 federation 서버 그룹에 대 한 프록시 클라이언트 요청을 사용할 수 있습니다.  
  
다음 그림 가상 금강 회사 SQL Server 토폴로지 회사 네트워크에서 사용 하 여 해당 federation 서버 농장 배포 하는 방법을 보여 줍니다. 또한 DNS 서버를 사용 하 여 회사 네트워크 NLB 클러스터에 사용 되는 동일한 클러스터 DNS 이름 \(fs.contoso.com\) 추가 NLB 호스트 프로그램에 대 한 액세스 및 웹 응용 프로그램 프록시 두 개를 사용 하 여 해당 회사는 주변 네트워크를 구성 하는 방법을 보여 \(wap1 and wap2\) 합니다.  
  
![사용 하 여 SQL server 팜](media/SQLFarmADFSBlue.gif)  
  
사용 하기 위해 네트워킹 환경을 federation 서버 또는 웹 응용 프로그램 프록시 구성 하는 방법에 대 한 자세한 내용은 "해상도 요구 사항 이름"을 참조 섹션 [광고 FS 요구](AD-FS-Requirements.md) 및 [웹 응용 프로그램 프록시 Infrastructure (WAP) 계획](https://technet.microsoft.com/library/dn383648.aspx)합니다.  
  
## <a name="high-availability-options-for-sql-server-farms"></a>SQL Server 그룹에 높은 가용성 옵션  
Windows Server 2012 r 2에 ADFS 있는 옵션은 두 새로운 높은 가용성 ADFS 농장 SQL Server를 사용 하 여에서 지원 됩니다.  
  
-   SQL Server AlwaysOn 공급 그룹에 대 한 지원  
  
-   병합 복제 SQL Server 지리적 분산된 높은 가용성에 대 한 지원  
  
이러한 옵션에 설명 자신이 각각 해결할 문제 및 배포 하는 옵션을 결정 하기 위한 몇 가지 주요 고려 합니다.  
  
> [!NOTE]  
> Windows 내부 데이터베이스 \(WID\)를 사용 하는 광고 FS 농장 보조 노드에서 기본 데이터 중복 read\/쓰기 기본 federation 서버 노드 및 read\ 전용 액세스를 제공 합니다.  이 지리적 로컬 또는 지리적 분산된 토폴로지에서 사용할 수 있습니다.  
>   
> WID 사용 하는 경우는 다음과 같은 제한 알고 있어야 합니다.  
>   
> -   100 이하의 신뢰 파티 신뢰 하는 경우 WID 농장은 30 federation 서버 제한 됩니다.  
> -   WID 농장 토큰 재생 검색 또는 인공 해상도 지원 하지 않는 \ (보안 설정 Markup Language \(SAML\) protocol\의 일부로).  
  
다음 표에서 WID 농장 사용에 대 한 요약 정보를 제공 합니다.  
  
||||  
|-|-|-|  
||1 \-100 RP 신뢰|100 개 이상의 RP 신뢰|  
|1 \-30 광고 FS 노드|지원 되는 WID|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요|  
|30 AD 이상 FS 노드|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요|  
  
### <a name="alwayson-availability-groups"></a>사용 가능한 그룹 AlwaysOn  
**개요**  
  
AlwaysOn 가용성 SQL Server 2012에에서 소개 된 그룹과 높은 가용성 SQL Server 인스턴스를 만들 수는 새로운 방법을 제공 합니다.  AlwaysOn 공급 그룹 클러스터링 및 데이터베이스에 중복 및 SQL 인스턴스 계층와 데이터베이스 계층 장애 조치 미러링 요소가 결합 합니다.  이전 높은 가용성 옵션 달리 AlwaysOn 공급 그룹 일반적인 저장소 필요 하지 않은 \ (또는 저장소 영역 network\) 데이터베이스 계층입니다.  
  
주 복제본으로 이루어진 가용성 그룹 \ (read\ 쓰기 기본 databases\ 설정) 및 1 ~ 4 가용성 복제본 \ (해당 보조 databases\ 세트).  가용성 그룹 지원 단일 read\ 쓰기 복사본 \ (기본 replica\) 하 고 1 ~ 4 read\ 전용 가용성 복제본 합니다.  각 가용성 복제본 다른 단일 Windows Server 장애 클러스터링 \(WSFC\) 클러스터 노드에서 있어야 합니다.  그룹 AlwaysOn 가용성에 대 한 자세한 내용은 참조 [AlwaysOn 공급 그룹 개요 \ (SQL Server \)](https://technet.microsoft.com/library/ff877884.aspx)합니다.  
  
광고 FS SQL Server 팜 노드 관점에서 AlwaysOn 공급 그룹 정책으로 단일 SQL Server 인스턴스를 대체 \ / 아티팩트 데이터베이스 합니다.  가용성 그룹 수신기 클라이언트는 \ (ADFS 보안 토큰 service\) SQL에 연결 하기 위해 사용 합니다.  
  
다음 그림 AlwaysOn 가용성 그룹과 AD FS SQL Server 팜을 보여 줍니다.  
  
![사용 하 여 SQL server 팜](media/alwaysonavailabilitygroups.jpg)  
  
> [!NOTE]  
> AlwaysOn 공급 그룹 SQL Server 인스턴스 Windows Server 장애 클러스터링 \(WSFC\) 노드에서 있는 필요 합니다.  
  
> [!NOTE]  
> 세 가지 다른 자동 장애 대상 수동 장애 의존으로 하나만 가용성 복제본 작동할 수 있습니다.  
  
**주요 배포 고려**  
  
AlwaysOn 공급 그룹 SQL Server 병합 복제 함께 사용 하려면 아래에서 "ADFS SQL Server 병합 복제와 함께 사용 되는 키 배포 고려" 설명 하는 문제를 기록을 주십시오.  특히, 복제 구독자 인 한 데이터베이스를 포함 하는 AlwaysOn 공급 그룹 장애 조치를 복제 구독 실패 합니다. 복제, 다시 시작 하려면 복제 관리자 구독자를 다시 수동으로 합니다.  특정 문제에 SQL Server 설명 참조 [복제 구독자 및 AlwaysOn 공급 그룹 \ (SQL Server \)](https://technet.microsoft.com/library/hh882436.aspx) 전반적인 문을에 복제 옵션이 AlwaysOn 공급 그룹에 대 한 지원 하 고 [복제, 변경 추적, 변경 데이터가 캡처 및 AlwaysOn 공급 그룹 \ (SQL Server \)](https://technet.microsoft.com/library/hh403414.aspx)합니다.  
  
**ADFS AlwaysOn 공급 그룹을 사용 하도록 구성**  
  
ADFS 농장 AlwaysOn 가용성 그룹과 구성 약간 수정 ADFS 배포 절차에 필요 합니다.  
  
1.  백업 하는 데이터베이스를 만들어야 AlwaysOn 공급 그룹 구성할 수 있습니다.  ADFS 설정 및 초기 구성 새로운 광고 FS SQL Server 발전소의 첫 번째 federation 서비스 노드의 일환으로 데이터베이스를 만듭니다.  ADFS 구성의 일환으로, 지정 해야 구성 첫 번째 ADFS 농장 노드 SQL 인스턴스에 직접 연결할 필요가 SQL 연결 문자열을 \ (만 temporary\은).   ADFS 농장 노드 SQL server 연결 문자열으로 구성 포함 된 ADFS 농장 구성에 특정 지침은 [Federation 서버 구성](../../ad-fs/deployment/Configure-a-Federation-Server.md)합니다.  
  
2.  ADFS 데이터베이스를 만든 후 AlwaysOn 공급 그룹으로 지정 하 고 SQL Server 도구를 사용 하 여 일반적인 TCPIP 수신기 만들고 프로세스에 [생성 및 사용 가능 여부 그룹 구성 \ (SQL Server \)](https://technet.microsoft.com/library/ff878265.aspx)합니다.  
  
3.  마지막으로, PowerShell를 사용 하 여 SQL 연결 문자열 AlwaysOn 공급 그룹 수신기 DNS 주소를 사용 하 여 업데이트 하려면 ADFS 속성 편집할 수 있습니다.  
  
    예제 PSH 명령 SQL 연결 문자열 ADFS 정책 데이터베이스에 대 한 업데이트:  
  
    ```  
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService  
    PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”  
    PS:\>$temp.put()  
  
    ```  
  
4.  예제 PSH 명령 SQL 연결 문자열 ADFS 정책 데이터베이스에 대 한 업데이트:  
  
    ```  
    PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”  
    ```  
  
### <a name="sql-server-merge-replication"></a>SQL Server 병합 복제  
병합 복제 SQL Server 2012에서에서 도입도 다음과 같은 특성으로 ADFS 정책 데이터 중복에 있습니다.  
  
-   읽고 모든 노드에서 쓰기 기능 \ (primary\ 뿐 아니라)  
  
-   소량의 시스템 대기 막기 비동기적 복제 하는 데이터  
  
다음 그림 병합 복제 지리적 중복 광고 FS SQL Server 농장 \ (게시자 1, 2 subscribers\):  
  
![사용 하 여 SQL server 팜](media/ADFSSQLGeoRedundancy3.png)  
  
**ADFS SQL Server 병합 복제와 함께 사용 되는 키 배포 고려 \ (다이어그램 above\의 숫자가 주의)**  
  
-   배포자 데이터베이스 AlwaysOn 가용성 그룹이 나 미러링와 함께 사용에 대 한 지원 되지 않습니다.  문을에 복제 옵션이 AlwaysOn 공급 그룹에 대 한 지원 SQL Server 참조 [복제, 변경 추적, 변경 데이터가 캡처 및 AlwaysOn 공급 그룹 \ (SQL Server \)](https://technet.microsoft.com/library/hh403414.aspx)합니다.  
  
-   복제 구독자 인 한 데이터베이스를 포함 하는 AlwaysOn 공급 그룹 장애 조치를 복제 구독 실패 합니다. 복제, 다시 시작 하려면 복제 관리자 구독자를 다시 수동으로 합니다.  특정 문제에 SQL Server 설명 참조 [복제 구독자 및 AlwaysOn 공급 그룹 \ (SQL Server \)](https://technet.microsoft.com/library/hh882436.aspx) 전반적인 문을 복제 옵션이 AlwaysOn 공급 그룹에 대 한 지원 하 고 [복제, 변경 추적, 변경 데이터가 캡처 및 AlwaysOn 공급 그룹 \ (SQL Server \)](https://technet.microsoft.com/library/hh403414.aspx)합니다.  
  
SQL Server 병합 복제 사용 하 여 ADFS 구성 하는 방법에 대해 더 자세한 내용은 참조 [SQL Server 복제 설치 지리적 중복](https://technet.microsoft.com/en-us/library/dn632406.aspx)합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[해당 AD FS 배포가 계획](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 r 2의 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

