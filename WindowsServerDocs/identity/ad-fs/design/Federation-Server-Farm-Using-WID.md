---
ms.assetid: f775cbda-a75d-439d-9aa7-82f3bc8dc932
title: WID를 사용하는 페더레이션 서버 팜
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 41c2179cbd8bf2c6032f233335099b512c02f880
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832504"
---
# <a name="federation-server-farm-using-wid"></a>WID를 사용하는 페더레이션 서버 팜

>적용 대상: Windows Server 2016, Windows Server 2012 R2

Active Directory Federation Services의 기본 토폴로지 \(AD FS\) Windows 내부 데이터베이스를 사용 하 여 페더레이션 서버 팜 \(WID\)합니다. 이 토폴로지에서 AD FS를 해당 팜에 가입 된 모든 페더레이션 서버에 대 한 AD FS 구성 데이터베이스에 대 한 저장소로 WID를 사용 합니다. 팜에서는 각 서버의 페더레이션 데이터를 구성 데이터베이스에 복제하고 유지 관리합니다. Windows Server 2012 r 2에서 AD FS WID를 사용 하 여 최대 30 명의 서버와 페더레이션 서버 팜을 구성 하려면 100 개 이하인 신뢰 당사자 트러스트를 통해 조직 수 있습니다.  
  
또한 팜의 첫 번째 페더레이션 서버를 만드는 작업에서는 새 페러데이션 서비스도 만듭니다. AD FS 구성 데이터베이스에 대 한 WID를 사용 하는 경우 팜에에서 만드는 첫 번째 페더레이션 서버 라고 합니다 *기본 페더레이션 서버*합니다. 즉,이 컴퓨터가 읽기로 구성 되어 있다고\/AD FS 구성 데이터베이스의 복사본을 작성 합니다.  
  
이 팜에 대해 구성 하는 다른 모든 페더레이션 서버 라고 *보조 페더레이션 서버* 읽기 기본 페더레이션 서버에 적용 된 변경 내용을 복제 해야 하기 때문\-만 로컬로 저장 하는 AD FS 구성 데이터베이스의 복사본입니다.  
  
> [!IMPORTANT]  
> 부하가에 두 개 이상의 페더레이션 서버를 사용 하는 것이 좋습니다\-균형 잡힌된 구성 합니다.  
  
## <a name="deployment-considerations"></a>배포 고려 사항  
이 섹션에서는 대상, 이점 및이 배포 토폴로지와 연결 된 제한 사항에 대 한 다양 한 고려 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지를 사용 해야 합니까?  
  
-   내부 사용자에 게 제공 해야 하는 100 개 이하인 구성 된 트러스트 관계가 있는 조직에서는 \(물리적으로 회사 네트워크에 연결 된 컴퓨터에 로그온 한\) 단일 기호로\-에 \(SSO\) 페더레이션된 응용 프로그램 또는 서비스에 대 한 액세스  
  
-   Microsoft Online Services 또는 Microsoft Office 365에 대 한 SSO 액세스를 사용 하 여 내부 사용자에 게 제공 하려는 조직에  
  
-   중복이 고 확장 가능한 서비스를 필요로 하는 소규모 조직  
  
> [!NOTE]  
> 조직에 더 큰 데이터베이스를 사용 하 여 고려해 야는 [페더레이션 서버 팜을 사용 하 여 SQL Server](Federation-Server-Farm-Using-SQL-Server.md) 배포 토폴로지입니다. 네트워크 외부에서 로그인 된 사용자와 조직에서 사용 하 여를 고려해 야는 [페더레이션 서버 팜을 사용 하 여 WID 및 프록시](Federation-Server-Farm-Using-WID-and-Proxies.md) 토폴로지 또는 [페더레이션 서버 팜을 사용 하 여 SQL Server](Federation-Server-Farm-Using-SQL-Server.md) 토폴로지입니다.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 장점은 무엇입니까?  
  
-   내부 사용자에 게 SSO 액세스를 제공합니다.  
  
-   데이터 및 페더레이션 서비스 중복성 \(각 페더레이션 서버는 동일한 팜의 다른 페더레이션 서버에 변경 내용을 복제\)  
  
-   WID는 Windows;에 포함 따라서 구입할 필요가 없습니다 SQL Server  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 제한 사항은 무엇입니까?  
  
-   WID 팜에 100 개 이하인 신뢰 당사자 트러스트를 설정한 경우 페더레이션 서버를 30 제한 됩니다.  
  
-   WID 팜 토큰 재생 검색 또는 아티팩트 해상도 지원 하지 않는 \(Security Assertion Markup Language의 일부가 \(SAML\) 프로토콜\)합니다.  
  
다음 표에서 WID 팜 사용에 대 한 요약을 제공 합니다.  구현 계획을 사용 합니다.  
  
|| 1 \- 100 RP 트러스트 | 100 개가 넘는 RP 트러스트 |
| --- | --- | --- |
|1 \- 30 AD FS 노드|WID 지원|WID-필요한 SQL을 사용 하 여 지원 되지 않습니다. 
|개 이상의 30 AD FS 노드|WID-필요한 SQL을 사용 하 여 지원 되지 않습니다.|WID-필요한 SQL을 사용 하 여 지원 되지 않습니다.  
  
## <a name="server-placement-and-network-layout-recommendations"></a>서버 배치와 네트워크 레이아웃 권장 사항  
네트워크 부하 분산 뒤의 회사 네트워크에 배치 하는 모든 페더레이션 서버를 계획 해야 네트워크에서이 토폴로지를 배포를 시작할 준비가 때 \(NLB\) Domain Name System 전용된 클러스터를 NLB 클러스터에 대해 구성할 수 있는 호스트 \(DNS\) 이름 및 클러스터 IP 주소입니다.  
  
> [!NOTE]  
> 이 클러스터 DNS 이름은 페더레이션 서비스 이름, 예를 들어 fs.fabrikam.com 일치 해야 합니다.  
  
NLB 호스트에는 클라이언트 요청을 개별 페더레이션 서버에 할당할이 NLB 클러스터에 정의 된 설정을 사용할 수 있습니다. 다음 그림은 가상의 Fabrikam, Inc., 회사 2를 사용 하 여 해당 배포의 첫 번째 단계를 설정 하는 방법을 보여 줍니다.\-컴퓨터 페더레이션 서버 팜 \(fs1 및 fs2\) WID와 DNS 서버와 회사 네트워크에 연결 되는 단일 NLB 호스트를 사용 합니다.  
  
![WID를 사용 하 여 서버 팜](media/FarmWID.gif)  
  
> [!NOTE]  
> 이 단일 NLB 호스트에 오류가 있는 경우 사용자가 페더레이션된 응용 프로그램 또는 서비스에 액세스할 수 없습니다. 비즈니스 요구 사항이 단일 지점에서 실패하는 것을 허용하지 않는 경우 추가 NLB 호스트를 추가합니다.  
  
페더레이션 서버와 함께 사용 하기 위해 네트워킹 환경을 구성 하는 방법에 대 한 자세한 내용은에서 이름 확인 요구 사항 섹션을 참조 하십시오. [AD FS 요구 사항](AD-FS-Requirements.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
[AD FS 배포 토폴로지 계획](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

