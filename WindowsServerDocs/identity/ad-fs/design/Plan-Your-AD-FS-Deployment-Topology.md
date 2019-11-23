---
ms.assetid: 5c8c6cc0-0d22-4f27-a111-0aa90db7d6c8
title: AD FS 배포 토폴로지 계획
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9cd036e9dd0b249197fb475504c9cad532ead0ea
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408035"
---
# <a name="plan-your-ad-fs-deployment-topology"></a>AD FS 배포 토폴로지 계획

Active Directory Federation Services \(AD FS\) 배포를 계획 하는 첫 번째 단계는 조직의 요구 사항을 충족 하는 올바른 배포 토폴로지를 결정 하는 것입니다.  
  
이 항목을 읽기 전에 페더레이션 서버 팜의 다른 페더레이션 서버에 AD FS 데이터를 저장 하 고 복제 하는 방법을 검토 하 고의 목적과 AD FS con에 저장 된 기본 데이터에 사용할 수 있는 복제 방법의 용도를 이해 해야 합니다. f) 데이터베이스.  
  
AD FS 구성 데이터를 저장 하는 데 사용할 수 있는 데이터베이스 유형에는 Windows 내부 데이터베이스 \(WID\) 및 Microsoft SQL Server의 두 가지가 있습니다. 자세한 내용은 [AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)을 참조하세요. 에서 지 원하는 다양 한 응용 프로그램 시나리오와 함께 WID 또는 SQL Server를 AD FS 구성 데이터베이스로 사용 하는 것과 관련 된 다양 한 이점 및 제한 사항을 검토 한 다음 선택 합니다.  
  
> [!IMPORTANT]  
> 기본 중복성, 부하 분산 및 페더레이션 서비스\)\(의 크기를 조정 하는 옵션을 구현 하려면 사용 하는 데이터베이스의 유형에 관계 없이 모든 프로덕션 환경에 대해 페더레이션 서버 팜 당 두 개 이상의 페더레이션 서버를 배포 하는 것이 좋습니다.  
  
## <a name="determining-which-type-of-adfs-configuration-database-to-use"></a>사용할 AD FS 구성 데이터베이스의 유형 결정  
AD FS는 데이터베이스를 사용 하 여 구성을 저장 하며, 경우에 따라 페더레이션 서비스와 관련 된 트랜잭션 데이터를 저장 합니다. AD FS 소프트웨어를 사용 하 여 Windows 내부 데이터베이스 \(WID\) 또는 Microsoft SQL Server 2008 이상에서 빌드된\-를 선택 하 여 페더레이션 서비스에 데이터를 저장할 수 있습니다.  
  
대부분의 용도에는 두 가지 데이터베이스 유형이 비교적 동일합니다. 그러나 AD FS에서 사용할 수 있는 다양 한 배포 토폴로지에 대 한 읽기를 시작 하기 전에 알아두어야 할 몇 가지 차이점이 있습니다. 다음 표에서는 WID 데이터베이스와 SQL Server 데이터베이스 간에 지원되는 기능의 차이점을 설명합니다.  
  
||기능|WID에서 지원?|SQL Server에서 지원?
| --- | --- | --- |--- |
|AD FS 기능|페더레이션 서버 팜 배포|예. WID 팜에 100 개 이하인 신뢰 당사자 트러스트를 설정한 경우 페더레이션 서버를 30 제한 됩니다.</br></br>WID 팜은 토큰 재생 검색 또는 아티팩트 확인을 지원 하지 않습니다 (SAML (Security Assertion Markup Language) 프로토콜의 일부). |예. 단일 팜에 배포할 수 있는 페더레이션 서버 수에 대한 제한 없음  
|AD FS 기능|SAML 아티팩트 확인 </br></br>**참고:** Microsoft Online Services, Microsoft Office 365, Microsoft Exchange 또는 Microsoft Office SharePoint 시나리오에는이 기능이 필요 하지 않습니다.|아니요|예  
|AD FS 기능|SAML\/WS\-페더레이션 토큰 재생 검색|아니요|예  
|데이터베이스 기능|끌어오기 복제를 사용 하는 기본 데이터베이스 중복성-읽기\-를 호스트 하는 하나 이상의 서버가 데이터베이스의 복사본\/읽기를 호스트 하는 원본 서버에서 수행 된 변경 내용을 요청 합니다.|예|아니요 
|데이터베이스 기능|데이터베이스 계층 에서만 장애 조치 (failover) 클러스터링 또는 미러링 \(와 같은 높은\-가용성 솔루션을 사용 하는 데이터베이스 중복성\) **참고:** 모든 AD FS 배포 토폴로지는 AD FS 서비스 계층에서 클러스터링을 지원 합니다.|아니요|예  

  
## <a name="sql-server-considerations"></a>SQL Server 고려 사항  
AD FS 배포를 위한 구성 데이터베이스로 SQL Server를 선택한 경우 다음 배포 정보를 고려해야 합니다.  
  
-   **SAML 기능과 해당 기능이 데이터베이스 크기 및 증가에 미치는 영향**. SAML 아티팩트 확인 또는 SAML 토큰 재생 검색 기능을 사용하는 경우 AD FS는 발급된 각 AD FS 토큰에 대한 정보를 SQL Server 구성 데이터베이스에 저장합니다. 이 활동의 결과로 인한 SQL Server 데이터베이스의 증가는 중요한 것으로 간주되지 않으며, 구성된 토큰 재생 보존 기간에 따라 다릅니다. 각 아티팩트 레코드의 크기는 약 30kb \(KB\)입니다.  
  
-   **배포에 필요한 서버 수**. SQL Server 인스턴스의 전용 호스트 역할을 하는 AD FS 인프라\)를 배포 하는 데 필요한 총 서버 수에 추가 서버 \(를 하나 이상 추가 해야 합니다. 장애 조치(failover) 클러스터링 또는 미러링을 사용하여 SQL Server 구성 데이터베이스에 대한 내결함성 및 확장성을 제공하려면 두 대 이상의 SQL Server가 필요합니다.  
  
## <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>선택한 구성 데이터베이스 유형이 하드웨어 리소스에 미치는 영향  
SQL Server 데이터베이스를 사용하는 팜에 배포된 페더레이션 서버와 달리, WID를 사용하는 팜에 배포된 페더레이션 서버의 하드웨어 리소스에 대한 영향은 중요하지 않습니다. 그러나 팜에 WID를 사용할 경우 해당 팜의 각 페더레이션 서버는 페더레이션 서비스에 필요한 정상 작업을 계속 제공하는 동시에 AD FS 구성 데이터베이스의 로컬 복사본에 대한 복제 변경 내용을 저장, 관리 및 유지해야 합니다.  
  
반면, SQL Server 데이터베이스를 사용하는 팜에 배포된 페더레이션 서버는 AD FS 구성 데이터베이스의 로컬 인스턴스를 포함할 필요가 없습니다. 따라서 하드웨어 리소스에 대한 수요가 조금 더 적습니다.  
  
## <a name="BKMK_1"></a>페더레이션 서버를 넣을 위치  
보안 모범 사례로, AD FS 페더레이션 서버를 방화벽 앞에 배치한 후 회사 네트워크에 연결 하 여 인터넷 노출을 방지 합니다. 이는 페더레이션 서버에 보안 토큰을 부여 하는 전체 권한이 있기 때문에 중요 합니다. 따라서 도메인 컨트롤러와 동일하게 보호되어야 합니다. 페더레이션 서버가 손상 되 면 악의적인 사용자가 모든 웹 응용 프로그램 및 AD FS로 보호 되는 페더레이션 서버에 대 한 전체 액세스 토큰을 발급할 수 있습니다.  
  
> [!NOTE]  
> 보안을 위해 인터넷에서 페더레이션 서버에 직접 액세스할 수 있도록 하는 것이 좋습니다. 테스트 랩 환경을 설정 하거나 조직에 경계 네트워크가 없는 경우에만 페더레이션 서버에 직접 인터넷 액세스를 제공 하는 것이 좋습니다.  
  
일반적인 회사 네트워크의 경우 인트라넷\-방화벽을 통해 회사 네트워크와 경계 네트워크 간에 설정 되 고 인터넷\-방화벽은 경계 네트워크와 인터넷 간에 설정 되는 경우가 많습니다. 이 경우 페더레이션 서버는 회사 네트워크 내에 있으며 인터넷 클라이언트에서 직접 액세스할 수 없습니다.  
  
> [!NOTE]  
> 회사 네트워크에 연결 된 클라이언트 컴퓨터는 Windows 통합 인증을 통해 페더레이션 서버와 직접 통신할 수 있습니다.  
  
AD FS에 사용할 방화벽 서버를 구성 하기 전에 페더레이션 서버 프록시를 경계 네트워크에 배치 해야 합니다.  
  
## <a name="supported-deployment-topologies"></a>지원 되는 배포 토폴로지  
다음 항목에서는 AD FS에서 사용할 수 있는 다양 한 배포 토폴로지를 설명 합니다. 또한 특정 비즈니스 요구 사항에 가장 적합한 토폴로지를 선택할 수 있도록 각 배포 토폴로지와 연관된 이점 및 제한 사항을 설명합니다.  
  
-   [WID를 사용하는 페더레이션 서버 팜](Federation-Server-Farm-Using-WID.md)  
  
-   [WID와 프록시를 사용하는 페더레이션 서버 팜](Federation-Server-Farm-Using-WID-and-Proxies.md)  
  
-   [SQL Server를 사용하는 페더레이션 서버 팜](Federation-Server-Farm-Using-SQL-Server.md)  
  
## <a name="see-also"></a>참고 항목  
[Windows Server 2012 R2의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

