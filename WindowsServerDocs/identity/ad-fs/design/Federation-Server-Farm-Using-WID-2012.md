---
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: "사용 하 여 WID federation 서버 농장"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bb4e5f88f3d62511b185a2b4317416169717c860
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid"></a>사용 하 여 WID federation 서버 농장

>적용 대상: Windows Server 2012

\(AD FS\) Active Directory Federation Services에 대 한 기본 토폴로지 조직의 Federation 서비스 호스트 최대 5 대의 federation 서버 구성 된 Windows 내부 데이터베이스 \(WID\)를 사용 하 여 federation 서버 팜입니다. 이 토폴로지 ADFS 해당 그룹에 연결 된 모든 federation 서버에 대 한 구성 ADFS 데이터베이스에 대 한 WID 스토어로 사용 합니다. 팜 복제 하 고 각 팜 서버에에서 걸쳐 구성 데이터베이스에 Federation 서비스 데이터를 유지 합니다.  
  
또한 농장의 첫 번째 federation 서버를 만드는 새로운 Federation 서비스를 만듭니다. WID ADFS 구성 데이터베이스를 사용 하면 팜에서 만드는 첫 번째 federation 서버 라고는 *기본 federation 서버*합니다. 이 컴퓨터의 ADFS 구성 데이터베이스 read\/쓰기 복사본으로 구성 되어 의미 합니다.  
  
이 그룹에 대 한 구성 하는 다른 모든 federation 서버 라고 *보조 federation 서버* 로컬로 저장 하는 ADFS 구성 데이터베이스의 read\ 전용 복사본을 기본 federation 서버에서 변경 내용이 복제 해야 하기 때문입니다.  
  
> [!NOTE]  
> Load\ 분산 구성에서 두 개 이상의 federation 서버를 사용할을 것이 좋습니다.  
  
## <a name="deployment-considerations"></a>배포 고려  
이 여기서 대상, 혜택을 및이 배포가와 관련 된 제한 사항에 대 한 다양 한 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지 사용 해야 하나요?  
  
-   내부 사용자에 게 제공 해야 하는 100 이하의 구성 된 보안 관계에는 조직 \ (회사 network\에 실제로 연결 된 컴퓨터에 로그온) 단일 sign\ 켜 짐 \(SSO\)에 액세스할 수 있는 연결 된 응용 프로그램이 나 서비스  
  
-   Microsoft Office 365 또는 Microsoft Online Services에 SSO에 액세스할 수 있는 내부 사용자에 게 제공 하려는 조직  
  
-   중소기업 필요한 중복, 확장 서비스  
  
> [!NOTE]  
> 조직 대규모 데이터베이스에 사용 하 여 고려해 야는 [사용 하 여 Federation 서버 농장 SQL Server](Federation-Server-Farm-Using-SQL-Server.md) 나중에이 섹션에 설명 된 배포가 합니다. 네트워크에서 벗어나 있는 로그인 사용자와 조직이 중 하나를 사용 하 여 고려해 야는 [Federation 서버 농장을 사용 하 여 WID 및 프록시](Federation-Server-Farm-Using-WID-and-Proxies.md) 토폴로지 또는 [사용 하 여 Federation 서버 농장 SQL Server](Federation-Server-Farm-Using-SQL-Server.md) 토폴로지 합니다.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지에 사용 하는 어떤 혜택이 있나요?  
  
-   내부 사용자에 게 SSO 액세스를 제공합니다.  
  
-   데이터와 Federation 서비스 중복 \ (각 federation 서버 동일한 farm\의 다른 federation 서버에 변경 내용을 복제)  
  
-   팜 확장할 수 있도록 하려면 최대 5 대의 federation 서버를 추가 하 여  
  
-   Windows,에 포함 된 WID 따라서 필요가 없습니다 SQL Server 구입  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여 제한 이란 무엇 인가요?  
  
-   WID 농장은 5 federation 서버 제한 됩니다. 자세한 내용은 참조 [광고 FS 배포 토폴로지 고려](AD-FS-Deployment-Topology-Considerations.md)합니다.  
  
-   WID 농장 토큰 재생 검색 또는 인공 해상도 지원 하지 않는 \ (보안 설정 Markup Language \(SAML\) protocol\의 일부로).  
  
## <a name="server-placement-and-network-layout-recommendations"></a>네트워크 위치와 위치 레이아웃 추천 서버  
사용자의 네트워크 안에이 토폴로지 배포 시작할 준비가 되 면 전용된 클러스터 Domain Name System \(DNS\) 이름, 클러스터 IP 주소와 NLB 클러스터에 대 한 구성 될 수 있는 네트워크 부하 분산 \(NLB\) 호스트 뒤 회사 네트워크에 배치 모든 federation 서버에 계획 해야 합니다.  
  
> [!NOTE]  
> 이 클러스터 DNS 이름은 Federation 서비스 이름, 예를 들어, fs.fabrikam.com 일치 해야 합니다.  
  
NLB 호스트가 개별 federation 서버에 대 한 클라이언트 요청 할당 하려면이 NLB 클러스터에 정의 된 설정을 사용할 수 있습니다. 다음 그림에서는 가상 원 창의 회사 federation 팜 two\ 컴퓨터를 사용 하 여 배포의 첫 번째 단계를 설정 하는 방법을 \(fs1 and fs2\)와 WID DNS 서버 및 단일 NLB 호스트 회사 네트워크에 연결 하는 위치를 지정 합니다.  
  
![서버 농장 WID를 사용 하 여](media/FarmWID.gif)  
  
> [!NOTE]  
> 이 단일 NLB 호스트에 오류가 있으면 사용자가 연결 된 응용 프로그램 및 서비스에 액세스할 수 없습니다. 이래 실패 한 곳을 허용 하지 않는 경우 추가 NLB 호스트를 추가 합니다.  
  
사용 하기 위해 네트워킹 환경을 federation 서버 구성 하는 방법에 대 한 자세한 내용은 참조 [이름을 확인 요구 사항을 Federation 서버에 대 한](Name-Resolution-Requirements-for-Federation-Servers.md) AD FS 디자인 가이드에 있습니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
