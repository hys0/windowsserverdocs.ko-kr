---
ms.assetid: 6618b3ce-0e94-4009-b887-d8e05453358b
title: "Federation 서버 팜 SQL Server를 사용 하 여"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a0fff975b9cb278e59686323d2bd72e641597573
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="federation-server-farm-using-sql-server"></a>Federation 서버 팜 SQL Server를 사용 하 여

>적용 대상: Windows Server 2012

이 대 한 Active Directory Federation Services \(AD FS\)이 토폴로지 해당 그룹에 각 federation 서버에 데이터 복제 하지 않고 Windows 내부 데이터베이스 \(WID\) 배포가 사용 하 여 federation 서버 농장에서 다릅니다. 대신, 그룹의 모든 federation 서버 읽고 회사 네트워크에 있는 Microsoft SQL Server 실행 하는 서버에 저장 된 일반적인 데이터베이스에 데이터 쓸 수 있습니다.  
  
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
다음 SQL server 버전 Windows Server 2012와 함께 설치 Adfs로 지원 됩니다.  
  
-   SQL Server 2008 \ / R2  
  
-   SQL Server 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>네트워크 위치와 위치 레이아웃 추천 서버  
Federation 서버 팜 WID 토폴로지와 마찬가지로의 모든 팜 federation 서버 사용 하도록 구성 된 하나 클러스터 Domain Name System \(DNS\) 이름 \ (Federation 서비스 name\ 나타내는) 및 네트워크 부하 분산 \(NLB\) 클러스터 구성의 일환으로 한 클러스터 IP 주소 합니다. 이렇게 하면 NLB 호스트가 개별 federation 서버에 요청 클라이언트를 할당 합니다. Federation 서버 프록시 federation 서버 그룹에 대 한 프록시 클라이언트 요청을 사용할 수 있습니다.  
  
다음 그림 가상 금강 회사 SQL Server 토폴로지 회사 네트워크에서 사용 하 여 해당 federation 서버 농장 배포 하는 방법을 보여 줍니다. 또한 DNS 서버를 사용 하 여 회사 네트워크 NLB 클러스터에 사용 되는 동일한 클러스터 DNS 이름 \(fs.contoso.com\) 추가 NLB 호스트 프로그램에 대 한 액세스 및 federation 서버 프록시 두 개를 사용 하 여 해당 회사는 주변 네트워크를 구성 하는 방법을 보여 \(fsp1 and fsp2\) 합니다.  
  
![사용 하 여 SQL server 팜](media/FarmSQLProxies.gif)  
  
사용 하기 위해 네트워킹 환경을 federation 서버 또는 federation 서버 프록시 구성 하는 방법에 대 한 자세한 내용은 참조 [이름을 확인 요구 사항을 Federation 서버에 대 한](Name-Resolution-Requirements-for-Federation-Servers.md) 또는 [이름 해상도 요구 사항을 Federation 서버 프록시](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
