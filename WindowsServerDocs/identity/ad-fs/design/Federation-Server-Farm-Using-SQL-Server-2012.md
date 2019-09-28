---
ms.assetid: 6618b3ce-0e94-4009-b887-d8e05453358b
title: SQL Server를 사용하는 페더레이션 서버 팜
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 358199fd37cdbb320bc8f3e3e5b2900d261986f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359147"
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server를 사용하는 페더레이션 서버 팜

AD FS \( \(\) Active Directory Federation Services에 대 한이 토폴로지는 Windows 내부 데이터베이스 WID 배포 토폴로지를 사용 하는 페더레이션 서버 팜과 다릅니다 .이 토폴로지는에 데이터를 복제 하지 않습니다.\) 팜의 각 페더레이션 서버. 대신, 팜의 모든 페더레이션 서버는 회사 네트워크에 있는 Microsoft SQL Server을 실행 하는 서버에 저장 된 공통 데이터베이스로 데이터를 읽고 쓸 수 있습니다.  
  
## <a name="deployment-considerations"></a>배포 고려 사항  
이 섹션에서는 대상, 이점 및이 배포 토폴로지와 연결 된 제한 사항에 대 한 다양 한 고려 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지를 사용 해야 합니까?  
  
-   단일 로그인으로의 내부 사용자와 외부 사용자에 게 제공 해야 하는 100 개가 넘는 신뢰 관계가 있는 대규모 조직\-에 \(SSO\) 페더레이션된 응용 프로그램 또는 서비스에 대 한 액세스  
  
-   이미 SQL Server를 사용 하 고 기존 도구와 전문 지식을 활용 하려는 조직  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 장점은 무엇입니까?  
  
-   더 많은 수의 트러스트 관계 \(지원 100\)  
  
-   토큰 재생 검색 \(에 대 한 지원 Security Assertion Markup Language\) \(SAML\) 2.0 프로토콜 \(의 보안 기능 및 아티팩트 해결 부분\)  
  
-   데이터베이스 미러링, 장애 조치 (failover) 클러스터링, 보고 및 관리 도구와 같은 SQL Server의 모든 이점에 대 한 지원  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 제한 사항은 무엇입니까?  
  
-   이 토폴로지는 기본적으로 데이터베이스 중복성을 제공 하지 않습니다. WID 토폴로지를 사용 하는 페더레이션 서버 팜은 팜의 각 페더레이션 서버에서 WID 데이터베이스를 자동으로 복제 하지만 SQL Server 토폴로지를 사용 하는 페더레이션 서버 팜은 데이터베이스의 복사본을 하나만 포함 합니다.  
  
> [!NOTE]  
> SQL Server는 장애 조치 (failover) 클러스터링, 데이터베이스 미러링 및 여러 가지 유형의 SQL Server 복제를 비롯 한 다양 한 데이터 및 응용 프로그램 중복성 옵션을 지원 합니다.  
  
\(Microsoft Information 기술 IT\) 부서는 보호 우선\- \(동기\) 모드 및 장애 조치 (failover) 클러스터링에 SQL Server 데이터베이스 미러링을\- 사용 하 여 높은 수준의 기능을 제공 합니다. SQL Server 인스턴스에 대 한 가용성 지원. SQL Server 트랜잭션 \(\-피어투피어\)및 병합 복제가 Microsoft의 AD FS 제품 팀에서 테스트 되지 않았습니다.\- SQL Server에 대 한 자세한 내용은 참조 [고가용성 솔루션 개요](https://go.microsoft.com/fwlink/?LinkId=179853) 또는 [적절 한 복제 유형을 선택 하면](https://go.microsoft.com/fwlink/?LinkId=214648)합니다.  
  
### <a name="supported-sql-server-versions"></a>지원 되는 SQL Server 버전  
다음 SQL server 버전은 Windows Server 2012와 함께 설치 된 AD FS와 함께 지원 됩니다.  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>서버 배치와 네트워크 레이아웃 권장 사항  
WID 토폴로지는 페더레이션 서버 팜을 마찬가지로, 페더레이션 서버 팜에 있는 모든 사용 하도록 구성 된 하나의 클러스터 Domain Name System \(DNS\) 이름 \(페더레이션 서비스 이름을 나타내는\) 및 네트워크 부하 분산의 일부로 클러스터 IP 주소 \(NLB\) 클러스터 구성 합니다. 그러면 NLB 호스트 클라이언트 요청을 개별 페더레이션 서버를 할당할 수 있습니다. 페더레이션 서버 팜에 대 한 프록시 클라이언트 요청에 페더레이션 서버 프록시를 사용할 수 있습니다.  
  
다음 그림에서는 가상의 Contoso Pharmaceuticals 회사가 회사 네트워크의 SQL Server 토폴로지를 사용 하 여 페더레이션 서버 팜을 배포 하는 방법을 보여 줍니다. 또한 회사의 DNS 서버를 동일한 클러스터 DNS 이름을 사용 하는 추가 NLB 호스트에 액세스할 수 있는 경계 네트워크를 구성 하는 방법을 설명 \(fs.contoso.com\) 와 두 명의 페더레이션 서버 프록시는 회사 네트워크 NLB 클러스터에서 사용 되는 \(fsp1 및 fsp2\)합니다.  
  
![SQL을 사용 하 여 서버 팜](media/FarmSQLProxies.gif)  
  
페더레이션 서버 또는 페더레이션 서버 프록시를 사용 하기 위해 네트워킹 환경을 구성 하는 방법에 대 한 자세한 내용은 참조 [페더레이션 서버에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Servers.md) 또는 [페더레이션 서버 프록시에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
