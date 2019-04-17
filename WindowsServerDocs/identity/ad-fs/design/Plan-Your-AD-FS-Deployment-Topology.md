---
ms.assetid: 5c8c6cc0-0d22-4f27-a111-0aa90db7d6c8
title: "해당 AD FS 배포가 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e41f7728c42912ec6ce680e1ed0c6a906a33392
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="plan-your-ad-fs-deployment-topology"></a>해당 AD FS 배포가 계획

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Active Directory Federation Services \(AD FS\) 배포를 계획 하는 첫 번째 단계는 조직에서 요구 하는 올바른 배포가 결정 하는 것입니다.  
  
이 항목을 읽으려면 먼저 ADFS 데이터 저장 되 고 federation 서버 그룹의 다른 federation 서버에 복제 어떻게 검토 하 고 목적 및 기본 ADFS 구성 데이터베이스에 저장 된 데이터에 사용할 수 있는 복제 방법 이해 하 않도록 합니다.  
  
두 가지가 데이터베이스 ADFS 구성 데이터를 저장 하는 데 사용할 수 있는: Windows 내부 데이터베이스 \(WID\) 및 Microsoft SQL Server 합니다. 자세한 내용은 참조 [AD FS 구성 데이터베이스의 The 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)합니다. 다양 한 혜택 및 다양 한 응용 시나리오를 지원 하 고 선택할 함께 ADFS 구성 데이터베이스와 WID 또는 SQL Server 사용과 관련 된 제한 검토 합니다.  
  
> [!IMPORTANT]  
> 기본 중복, 부하 분산 Federation 서비스 \(if required\) 크기를 조정 하는 옵션을 구현을 두 개 이상의 federation 서버 federation 서버 팜 데이터베이스에 사용할 형식에 관계 없이 모든 생산 환경에 대 한 배포 하는 것이 좋습니다.  
  
## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>사용 하 여 ADFS 구성 데이터베이스 유형을 확인  
ADFS 데이터베이스를 사용 하 여 구성 저장 하 고-경우에 따라-트랜잭션 데이터 Federation 서비스와 관련 된 합니다. built\ Windows 내부 데이터베이스 \(WID\) 또는 Microsoft SQL Server 2008 또는 최신 Federation 서비스의 데이터를 저장 하도록 선택 하는 ADFS 소프트웨어를 사용할 수 있습니다.  
  
대부분의 경우 두 가지 데이터베이스 유형 상대적으로 동일합니다. 그러나 Adfs에 사용할 수 있는 다양 한 배포 토폴로지에 대해 자세히 읽기 시작 하기 전에 주의 해야 할 몇 가지 차이점이 있습니다. 다음 표에서 WID 데이터베이스와 SQL Server 데이터베이스 간의 차이점 지원 되는 기능에 설명합니다.  
  
||기능|WID 지원 하나요?|SQL Server 지원 하나요?
| --- | --- | --- |--- |
|광고 FS 기능|Federation 서버 농장 배포|예입니다. 100 이하의 신뢰 파티 신뢰 하는 경우 WID 농장은 30 federation 서버 제한 됩니다.</br></br>WID 농장 토큰 재생 검색 또는 인공 해상도 (일부 보안 설정 Markup 언어 (SAML) 프로토콜)를 지원 하지 않습니다. |예입니다. 단일 팜에 배포할 수 있는 federation 서버 수에 제한이 없습니다 적용 되어  
|광고 FS 기능|SAML 아티팩트 해상도 </br></br>**참고:** 이 기능은 Microsoft Online Services, Microsoft Office 365, Microsoft Exchange 또는 SharePoint 시나리오 Microsoft Office에 대 한 필요 하지 않습니다.|아니요|예  
|광고 FS 기능|토큰 연합-WS\ SAML\/재생 검색|아니요|예  
|데이터베이스 기능|사용 하 여 위치를 read\ 전용 원본 서버에 대 한 데이터베이스 요청 변경 호스트 하는 하나 이상의 서버 호스트 하는 데이터베이스의 read\/쓰기 복사본 방향으로 빼냅니다 복제 기본 데이터베이스 중복|예|아니요 
|데이터베이스 기능|데이터베이스 중복 장애 클러스터링 또는 미러링 같은 high\ 가용성 솔루션을 사용 하 여 \ (데이터베이스 계층 only\)에서 **참고:** 모든 ADFS 배포 토폴로지 ADFS 서비스 계층 클러스터링을 지원 합니다.|아니요|예  

  
## <a name="sql-server-considerations"></a>SQL Server 고려 사항  
ADFS 배포를 위해 구성 데이터베이스와 SQL Server를 선택 하는 경우 다음 배포 사실 고려해 야 합니다.  
  
-   **SAML 기능과 데이터베이스 크기와 성장에 미치는 영향**합니다. SAML 아티팩트 해상도 또는 SAML 토큰 재생 감지 기능이 활성화 되어 있으면 ADFS 정보 발생 하는 각 ADFS 토큰 SQL Server 구성 데이터베이스에 저장 합니다. 이 활동으로 인해 SQL Server 데이터베이스의 증가, 중요 한 것으로 간주 되지 않습니다 및 토큰 구성 된 재생 보존 기간에 따라 달라 집니다. 각 아티팩트 레코드 약 30 킬로바이트 \(KB\)의 크기를 있습니다.  
  
-   **서버에 배포 하는 데 필요한 수가**합니다. 하나 이상의 추가 서버에 추가 해야 합니다 \ 서버 ADFS infrastructure\ 배포 하는 데 필요한의 총) (를 있는 SQL Server 인스턴스 전용된 호스트 처럼 작동 합니다. 무결성 및 확장성 SQL Server 구성 데이터베이스를 제공 하기 위해 장애 클러스터링 사용 하거나 사용 하려는 경우 두 가지 SQL server 최소 공간이 필요 합니다.  
  
## <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>선택한 구성 데이터베이스 형식 있습니다 어떤 영향을 주나요 하드웨어 리소스  
중요 한 하드웨어 리소스 WID federation 서버 SQL Server 데이터베이스를 사용 하 여 팜에 배포 되는 것이 아니라 사용 하 여 팜에 배포 되는 federation 서버에 영향을 않습니다. 그러나이 그룹에 대 한 WID를 사용 하는 경우 해당 농장의 각 federation 서버 해야 저장, 관리 및도 계속 Federation 서비스에 필요한 기본 작업을 제공 하는 동안 복제 변경 ADFS 구성 데이터베이스의 로컬 복사본을 유지 고려해 야 할 중요 합니다.  
  
비교, SQL Server 데이터베이스를 사용 하는 농장에 배포 되는 federation 서버가 ADFS 구성 데이터베이스의 로컬 인스턴스를 반드시 포함 되지 않습니다. 따라서 하드웨어 리소스에 약간 더 적은 수의 요구를 만들 수 있습니다.  
  
## <a name="BKMK_1"></a>위치를 federation 서버  
보안 가장 연습 방화벽 앞 ADFS federation 서버 놓고 노출은 인터넷에서 되지 않도록 하 여 회사 네트워크에 연결 합니다. 이 federation 서버 전체 수 있는 권한이 부여 보안 토큰 중요 합니다. 따라서 도메인 컨트롤러도 동일한 보호가 있어야 합니다. Federation 서버 손상 되 면 악의적인 사용자가 및 federation 서버 Adfs로 보호 되는 모든 웹 응용 프로그램에 대 한 전체 액세스 토큰 드릴 수 있습니다.  
  
> [!NOTE]  
> 보안을 위해 인터넷에 액세스할 수 있는 직접 federation 서버 되지 않도록 합니다. 테스트 랩 환경 또는 조직이 주변 네트워크 없는 설정 하는 경우에 해당 federation 서버 직접 인터넷 액세스를 제공 하는 것이 좋습니다.  
  
일반적인 회사 네트워크에 대 한 주변 네트워크 회사 네트워크와 intranet\ 전면 방화벽 설정 되 고 Internet\ 전면 방화벽 주변 네트워크 및 인터넷 간에 자주 설정 됩니다. 이 경우 회사의 네트워크 안에 federation 서버에 위치 하 고 직접 인터넷 클라이언트에서 액세스할 수 없는 합니다.  
  
> [!NOTE]  
> 회사 네트워크에 연결 하는 클라이언트 컴퓨터 Windows 통합 인증을 통해 federation 서버를 사용 하 여 직접 통신할 수 있습니다.  
  
Adfs로 사용 하기 위해 방화벽 서버 구성 하기 전에 federation 서버 프록시 주변 네트워크에 있어야 합니다.  
  
## <a name="supported-deployment-topologies"></a>지원 되는 배포 토폴로지  
다음 항목 Adfs에 사용할 수 있는 다양 한 배포 토폴로지에 설명 합니다. 또한 특정 비즈니스 요구에 가장 적합 한 토폴로지 선택할 수 있도록 각각 배포가와 관련 된 장단점 설명 합니다.  
  
-   [사용 하 여 WID federation 서버 농장](Federation-Server-Farm-Using-WID.md)  
  
-   [Federation 서버 팜 WID 및 프록시 사용 하 여](Federation-Server-Farm-Using-WID-and-Proxies.md)  
  
-   [Federation 서버 팜 SQL Server를 사용 하 여](Federation-Server-Farm-Using-SQL-Server.md)  
  
## <a name="see-also"></a>참조 하십시오  
[Windows Server 2012 r 2의 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

