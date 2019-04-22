---
ms.assetid: e983d2ab-4153-41e7-b243-12cf7d71a552
title: SQL Server를 사용하는 페더레이션 서버 팜
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e26b7cac971f472bc8b5e48e3dc8cd2592dc22ce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814784"
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server를 사용하는 페더레이션 서버 팜

>적용 대상: Windows Server 2016, Windows Server 2012 R2

Active Directory Federation Services에 대 한이 토폴로지 \(AD FS\) Windows 내부 데이터베이스를 사용 하 여 페더레이션 서버 팜에서 다릅니다 \(WID\) 는 배포 토폴로지를 복제 하지 않고 데이터를 팜의 각 페더레이션 서버입니다. 대신 팜의 모든 페더레이션 서버 읽고 회사 네트워크에 있는 Microsoft SQL Server를 실행 하는 서버에 저장 된 일반 데이터베이스로 데이터를 쓸 수 있습니다.  
  
> [!IMPORTANT]  
> AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우에 SQL Server 2008 및 SQL Server 2012 및 SQL Server 2014를 포함 하 여 최신 버전에서 사용할 수 있습니다.  
  
## <a name="deployment-considerations"></a>배포 고려 사항  
이 섹션에서는 대상, 이점 및이 배포 토폴로지와 연결 된 제한 사항에 대 한 다양 한 고려 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지를 사용 해야 합니까?  
  
-   단일 로그인으로의 내부 사용자와 외부 사용자에 게 제공 해야 하는 100 개가 넘는 신뢰 관계가 있는 대규모 조직\-에 \(SSO\) 페더레이션된 응용 프로그램 또는 서비스에 대 한 액세스  
  
-   조직은 이미 SQL Server를 사용 하 고 자신의 기존 도구 및 전문 지식을 활용 하려는  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 장점은 무엇입니까?  
  
-   많은 수의 트러스트 관계에 대 한 지원을 \(100 개가 넘는\)  
  
-   토큰 재생 검색에 대 한 지원을 \(보안 기능\) 및 아티팩트 확인 \(Security Assertion Markup Language의 일부가 \(SAML\) 2.0 프로토콜\)  
  
-   데이터베이스 미러링, 장애 조치 클러스터링, 보고 및 관리 도구 같은 SQL Server의 전체 혜택에 대 한 지원  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 제한 사항은 무엇입니까?  
  
-   이 토폴로지는 기본적으로 데이터베이스 중복성을 제공 하지 않습니다. SQL Server 토폴로지를 사용 하 여 페더레이션 서버 팜에 데이터베이스의 복사본을 하나만 포함 되어 있지만 WID 토폴로지를 사용 하 여 페더레이션 서버 팜의 각 페더레이션 서버 팜에 WID 데이터베이스에 자동으로 복제  
  
> [!NOTE]  
> SQL Server는 여러 다른 데이터 및 장애 조치 클러스터링, 데이터베이스 미러링 및 여러 다른 유형의 SQL Server 복제를 포함 하 여 응용 프로그램 중복성 옵션을 지원 합니다.  
  
Microsoft Information Technology \(IT\) 부서에서 높은 SQL Server 데이터베이스 미러링을 사용\-안전성 \(동기\) 모드 및 장애 조치 클러스터링을 제공 하려면\- SQL Server 인스턴스에 대 한 지원입니다. SQL Server 트랜잭션 \(피어\-하\-피어\) 및 병합 복제 microsoft AD FS 제품 팀에서 테스트 되지 않았습니다. SQL Server에 대 한 자세한 내용은 참조 [고가용성 솔루션 개요](https://go.microsoft.com/fwlink/?LinkId=179853) 또는 [적절 한 복제 유형을 선택 하면](https://go.microsoft.com/fwlink/?LinkId=214648)합니다.  
  
### <a name="supported-sql-server-versions"></a>지원 되는 SQL Server 버전  
다음 SQL server 버전은 Windows Server 2012 r 2에서 AD FS와 함께 지원 됩니다.  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
-   SQL Server 2014  
  
## <a name="server-placement-and-network-layout-recommendations"></a>서버 배치와 네트워크 레이아웃 권장 사항  
WID 토폴로지는 페더레이션 서버 팜을 마찬가지로, 페더레이션 서버 팜에 있는 모든 사용 하도록 구성 된 하나의 클러스터 Domain Name System \(DNS\) 이름 \(페더레이션 서비스 이름을 나타내는\) 및 네트워크 부하 분산의 일부로 클러스터 IP 주소 \(NLB\) 클러스터 구성 합니다. 그러면 NLB 호스트 클라이언트 요청을 개별 페더레이션 서버를 할당할 수 있습니다. 페더레이션 서버 팜에 대 한 프록시 클라이언트 요청에 페더레이션 서버 프록시를 사용할 수 있습니다.  
  
다음 그림에서는 가상의 Contoso Pharmaceuticals 회사 회사 네트워크에서 SQL Server 토폴로지를 사용 하 여 해당 페더레이션 서버 팜을 배포 하는 방법을 보여 줍니다. 또한 회사의 DNS 서버를 동일한 클러스터 DNS 이름을 사용 하는 추가 NLB 호스트에 액세스할 수 있는 경계 네트워크를 구성 하는 방법을 설명 \(fs.contoso.com\) 두 명의 웹 응용 프로그램 프록시를 사용 하 여 회사 네트워크 NLB 클러스터에 사용 되는 \(wap1 및 wap2\)합니다.  
  
![SQL을 사용 하 여 서버 팜](media/SQLFarmADFSBlue.gif)  
  
페더레이션 서버 또는 웹 응용 프로그램 프록시 사용 하기 위해 네트워킹 환경을 구성 하는 방법에 대 한 자세한 내용은 "이름 확인 요구 사항"을 참조 하십시오. 섹션 [AD FS 요구 사항](AD-FS-Requirements.md) 및 [웹 응용 프로그램 프록시 인프라 (WAP) 계획](https://technet.microsoft.com/library/dn383648.aspx)합니다.  
  
## <a name="high-availability-options-for-sql-server-farms"></a>SQL 서버 팜에 대 한 고가용성 옵션  
Windows Server 2012 r 2에서 AD FS에 있는 두 가지 새 옵션이 AD FS 팜의 SQL Server를 사용 하 여 고가용성을 지원 하기 위해.  
  
-   SQL Server AlwaysOn 가용성 그룹에 대 한 지원  
  
-   SQL Server 병합 복제를 사용 하 여 지리적으로 분산 된 고가용성에 대 한 지원  
  
이 섹션에서는 이러한 각 옵션을 설명 하 고 자신이 각각 해결할 문제를 배포 하는 옵션을 결정 하기 위한 몇 가지 주요 고려 사항입니다.  
  
> [!NOTE]  
> Windows 내부 데이터베이스를 사용 하는 AD FS 팜의 \(WID\) 읽기 기본 데이터 중복성을 제공\/기본 페더레이션 서버 노드에 대 한 액세스를 쓰고 읽는\-만 보조 노드에 액세스 합니다.  이 지리적으로 로컬 또는 지리적으로 분산 된 토폴로지 사용 수 있습니다.  
>   
> WID를 사용 하는 경우 다음 제한 사항을 고려해 야 합니다.  
>   
> -   WID 팜에 100 개 이하인 신뢰 당사자 트러스트를 설정한 경우 페더레이션 서버를 30 제한 됩니다.  
> -   WID 팜 토큰 재생 검색 또는 아티팩트 해상도 지원 하지 않는 \(Security Assertion Markup Language의 일부가 \(SAML\) 프로토콜\)합니다.  
  
다음 표에서 WID 팜 사용에 대 한 요약을 제공 합니다.  
  
||||  
|-|-|-|  
||1 \- 100 RP 트러스트|100 개가 넘는 RP 트러스트|  
|1 \- 30 AD FS 노드|WID 지원|WID를 사용 하 여 지원 되지 않는 \- 필요한 SQL|  
|개 이상의 30 AD FS 노드|WID를 사용 하 여 지원 되지 않는 \- 필요한 SQL|WID를 사용 하 여 지원 되지 않는 \- 필요한 SQL|  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn 가용성 그룹  
**개요**  
  
AlwaysOn 가용성 그룹 SQL Server 2012에 도입 된 및 고가용성 SQL Server 인스턴스를 만들려고 하는 새로운 방법을 제공 합니다.  AlwaysOn 가용성 그룹의 중복 및 SQL 인스턴스 계층 및 데이터베이스 계층 모두에서 장애 조치를 위한 데이터베이스 미러링 및 클러스터링 요소를 결합 합니다.  이전 고가용성 옵션과 달리, AlwaysOn 가용성 그룹 없이 일반 저장소 \(나 저장 영역 네트워크\) 데이터베이스 계층입니다.  
  
주 복제본의 가용성 그룹 구성 됩니다 \(읽기 집합이\-주 데이터베이스 쓰기\) 및 1 ~ 4 개의 가용성 복제본 \(개의 해당 보조 데이터베이스 설정\)합니다.  가용성 그룹은 단일 읽기를 지원\-복사본 작성 \(주 복제본\), 및 1 ~ 4 개의 읽기\-가용성 복제본만 합니다.  각 가용성 복제본을 단일 Windows Server 장애 조치 클러스터링의 다른 노드에 있어야 합니다. \(WSFC\) 클러스터 합니다.  AlwaysOn 가용성에 대 한 자세한 내용은 그룹 참조 [AlwaysOn 가용성 그룹 개요 \(SQL Server\)](https://technet.microsoft.com/library/ff877884.aspx)합니다.  
  
AD FS SQL 서버 팜 노드의 관점에서 AlwaysOn 가용성 그룹 정책으로 단일 SQL Server 인스턴스를 대체 \/ 아티팩트 데이터베이스입니다.  가용성 그룹 수신기는 클라이언트 \(AD FS 보안 토큰 서비스\) SQL 연결에 사용 합니다.  
  
다음 다이어그램에서는 AlwaysOn 가용성 그룹에 대 한 AD FS SQL 서버 팜 보여 줍니다.  
  
![SQL을 사용 하 여 서버 팜](media/alwaysonavailabilitygroups.jpg)  
  
> [!NOTE]  
> AlwaysOn 가용성 그룹의 경우 SQL Server 인스턴스가 Windows Server 장애 조치 클러스터링에 위치 하 \(WSFC\) 노드.  
  
> [!NOTE]  
> 수동 장애 조치를 사용 하 고 나머지 세는 자동 장애 조치 대상에 따라 하나의 가용성 복제본만 작동할 수 있습니다.  
  
**키 배포 고려 사항**  
  
SQL Server 병합 복제와 함께의 AlwaysOn 가용성 그룹을 사용 하려는 경우 아래의 "AD FS를 사용 하 여 SQL Server 병합 복제에 대 한 키 배포 고려 사항"에서 설명 하는 문제를 메모해를 주십시오.  특히, 데이터베이스는 복제 구독자를 포함 하는 AlwaysOn 가용성 그룹 장애 조치, 복제 구독이 실패 합니다. 복제를 재개 하려면 복제 관리자가 수동으로 다시 구성 해야 구독자입니다.  특정 문제에 대 한 SQL Server 설명을 참조 [복제 구독자 및 AlwaysOn 가용성 그룹 \(SQL Server\)](https://technet.microsoft.com/library/hh882436.aspx) 전반적인 문을 AlwaysOn 가용성 그룹에서 복제 옵션에 대 한 지원 및 [복제, 변경 내용 추적, 변경 데이터 캡처 및 AlwaysOn 가용성 그룹 \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)합니다.  
  
**AlwaysOn 가용성 그룹을 사용 하도록 AD FS를 구성 합니다.**  
  
AlwaysOn 가용성 그룹을 사용 하 여 AD FS 팜을 구성 하는 AD FS 배포 절차를 약간 수정 사항이 필요 합니다.  
  
1.  AlwaysOn 가용성 그룹을 구성 하기 전에 백업 하려는 데이터베이스를 만들어야 합니다.  AD FS 설치 및 새 AD FS SQL 서버 팜의 첫 번째 페더레이션 서비스 노드의 초기 구성의 일부로 해당 데이터베이스를 만듭니다.  AD FS 구성의 일부로 지정 해야가 직접 SQL 인스턴스에 연결 하려면 첫 번째 AD FS 팜에 노드를 구성 해야 하는 SQL 연결 문자열 \(일시적인 것 이라고\)합니다.   SQL server 연결 문자열에서 AD FS 팜에 노드를 구성 하는 등, AD FS 팜 구성에 대 한 특정 지침은 참조 하십시오. [페더레이션 서버 구성](../../ad-fs/deployment/Configure-a-Federation-Server.md)합니다.  
  
2.  AD FS 데이터베이스를 만든 후 AlwaysOn 가용성 그룹에 할당 하 고 SQL Server 도구를 사용 하 여 일반적인 TCPIP 수신기 만들고에 처리 [생성 및 구성의 가용성 그룹 \(SQL Server\)](https://technet.microsoft.com/library/ff878265.aspx)합니다.  
  
3.  마지막으로, PowerShell을 사용 하 여 AlwaysOn 가용성 그룹 수신기의 DNS 주소를 사용 하 여 SQL 연결 문자열을 업데이트 하려면 AD FS 속성을 편집 합니다.  
  
    AD FS 구성 데이터베이스에 대 한 SQL 연결 문자열을 업데이트 하려면 예제 PSH 명령:  
  
    ```  
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService  
    PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”  
    PS:\>$temp.put()  
  
    ```  
  
4.  AD FS 아티팩트 확인 서비스 데이터베이스에 대 한 SQL 연결 문자열을 업데이트 하려면 예제 PSH 명령:  
  
    ```  
    PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”  
    ```  
  
### <a name="sql-server-merge-replication"></a>SQL Server 병합 복제  
또한 SQL Server 2012에 도입 된, 병합 복제는 다음과 같은 특징을 가진 AD FS 정책 데이터 중복 허용 됩니다.  
  
-   읽기 및 쓰기 기능을 모든 노드에서 \(뿐 아니라 주\)  
  
-   적은 양의 데이터를 시스템에 대기 시 키 지 않도록 비동기적으로 복제  
  
다음 다이어그램에서는 병합 복제를 사용 하 여 지리적으로 중복 AD FS SQL 서버 팜은 \(1 게시자, 구독자가 2\):  
  
![SQL을 사용 하 여 서버 팜](media/ADFSSQLGeoRedundancy3.png)  
  
**SQL Server 병합 복제를 사용 하 여 AD FS를 사용 하는 것에 대 한 키 배포 고려 사항 \(위의 다이어그램에는 번호\)**  
  
-   배포자 데이터베이스는 AlwaysOn 가용성 그룹 또는 데이터베이스 미러링을 사용 하도록 지원 되지 않습니다.  SQL Server AlwaysOn 가용성 그룹에서 복제 옵션에 대 한 문을 지원 참조 [복제, 변경 내용 추적, 변경 데이터 캡처 및 AlwaysOn 가용성 그룹 \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)합니다.  
  
-   데이터베이스는 복제 구독자를 포함 하는 AlwaysOn 가용성 그룹 장애 조치, 복제 구독이 실패 합니다. 복제를 재개 하려면 복제 관리자가 수동으로 다시 구성 해야 구독자입니다.  특정 문제에 대 한 SQL Server 설명을 참조 [복제 구독자 및 AlwaysOn 가용성 그룹 \(SQL Server\)](https://technet.microsoft.com/library/hh882436.aspx) 전반적인 문을 AlwaysOn 가용성 그룹 복제 옵션에 대 한 지원 및 [복제, 변경 내용 추적, 변경 데이터 캡처 및 AlwaysOn 가용성 그룹 \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)합니다.  
  
SQL Server 병합 복제를 사용 하 여 AD FS를 구성 하는 방법에 더 자세한 내용은 참조 하십시오. [SQL Server 복제 설치 지리적 중복](https://technet.microsoft.com/library/dn632406.aspx)합니다.  
  
## <a name="see-also"></a>관련 항목  
[AD FS 배포 토폴로지 계획](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

