---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: "Federation 서버 팜 WID 및 프록시 사용 하 여"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e372f066fc82b9857d438234b491732a177e24fa
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Federation 서버 팜 WID 및 프록시 사용 하 여

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Windows 내부 데이터베이스 \(WID\) 토폴로지 federation 서버 팜 동일 Active Directory Federation Services \(AD FS\)가 배포가 이지만 프록시 컴퓨터 외부 사용자를 지 원하는 주변 네트워크에 추가 하는 것입니다. 이러한 프록시 federation 서버 팜 하 여 회사 네트워크에서 벗어나 있는 제공 하는 클라이언트 인증 요청 이동 합니다. Adfs의 이전 버전에서는 이러한 프록시 서버 프록시 federation 이라고 했습니다.  
  
> [!IMPORTANT]  
> Windows Server 2012 r 2에서 \(AD FS\) Active Directory Federation Services, federation 서버 프록시 역할 웹 응용 프로그램 프록시 라는 새로운 원격 액세스 역할 서비스에 의해 처리 됩니다. Adfs의 레거시 버전 2.0 FS 및 Windows Server 2012에서 ADFS 광고와 같은 Adfs의 federation 서버 프록시 배포 목적 였으며 회사 네트워크에서 벗어나 있는 접근성에 대 한 사용자 수 있도록 하나 이상의 웹 응용 프로그램 프록시 ADFS Windows Server 2012 r 2에서에 대해 배포할 수 있습니다.  
>   
> Adfs의 컨텍스트에서 웹 응용 프로그램 프록시 ADFS federation 서버 프록시도 작동합니다. 이외에 웹 응용 프로그램 프록시 모든 디바이스에서 사용자가 회사 네트워크에서 벗어나 있는 액세스할 수 있도록 내 회사 네트워크 웹 응용 프로그램에 대 한 프록시 역방향 기능을 제공 합니다. 웹 응용 프로그램 프록시 개요 웹 응용 프로그램 프록시 역할 서비스에 대 한 자세한 내용은 참조 합니다.  
>   
> 프록시 웹 응용 프로그램 배포를 계획 하는 정보는 다음과 같은 항목에 검토할 수 있습니다.  
>   
> -   [웹 응용 프로그램 프록시 인프라 (WAP) 계획](https://technet.microsoft.com/library/dn383648.aspx)  
> -   [웹 응용 프로그램 프록시 서버 계획](https://technet.microsoft.com/library/dn383647.aspx)  
  
## <a name="deployment-considerations"></a>배포 고려  
이 여기서 대상, 혜택을 및이 배포가와 관련 된 제한 사항에 대 한 다양 한 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지 사용 해야 하나요?  
  
-   조직에는 해당 내부 사용자 및 외부 사용자에 게 제공 해야 하는 100 이하의 구성 된 보안 관계 \ (로그온 회사 network\ 밖에 있을 실제로 컴퓨터로) 단일 sign\ 켜 짐 \(SSO\)에 액세스할 수 있는 연결 된 응용 프로그램이 나 서비스  
  
-   Microsoft Office 365에 SSO에 액세스할 수 있는 자신의 내부 사용자 및 외부 사용자에 게 제공 해야 하는 조직  
  
-   중소기업 외부 사용자가 있는 중복, 확장 서비스  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지에 사용 하는 어떤 혜택이 있나요?  
  
-   동일한 혜택에 대 한 나열 된는 [Federation 서버 농장을 사용 하 여 WID](Federation-Server-Farm-Using-WID.md) 토폴로지에서 이용 외부 사용자에 대 한 추가 액세스를 제공의 혜택  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여 제한 이란 무엇 인가요?  
  
-   에 나열 된와 같은 제한은 [Federation 서버 농장을 사용 하 여 WID](Federation-Server-Farm-Using-WID.md) 토폴로지  

||1 \-100 RP 신뢰|100 개 이상의 RP 신뢰 
| ----- |-----| ------ |
|1 \-30 광고 FS 노드|지원 되는 WID|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요 
|30 AD 이상 FS 노드|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요|사용 하 여 WID 지원 되지 않습니다 \-SQL 필요  
  
## <a name="server-placement-and-network-layout-recommendations"></a>네트워크 위치와 위치 레이아웃 추천 서버  
추가 두 웹 응용 프로그램 프록시 외에이 토폴로지 배포 하는 주변 네트워크 두 번째 네트워크 부하 분산 \(NLB\) 호스트 Domain Name System \(DNS\) 서버에 대 한 액세스 제공할 수도 있다는 있는지 확인 해야 합니다. 두 번째 NLB 호스트 Internet\ 액세스할 수 있는 클러스터 IP 주소를 사용 하는 NLB 클러스터로 구성 해야 하 고 회사 네트워크 \(fs.fabrikam.com\)에서 구성 이전 nlb와 동일한 클러스터 DNS name 설정을 사용 해야 합니다. 웹 응용 프로그램 프록시 Internet\ 액세스할 수 있는 IP 주소를 구성 해야 합니다.  
  
다음 그림에서는 기존 federation 서버 농장 WID 이전에 설명 된 토폴로지와 가상 원 창의 회사 주변 DNS 서버에 대 한 액세스를 제공 하는 방법을와 같은 클러스터 DNS 이름 \(fs.fabrikam.com\) NLB 호스트를 두 번째 하 고 추가 두 웹 응용 프로그램 프록시 \(wap1 and wap2\) 주변 네트워크입니다.  
  
![WID 농장 및 프록시](media/WIDFarmADFSBlue.gif)  
  
사용 하기 위해 네트워킹 환경을 federation 서버 또는 웹 응용 프로그램 프록시 구성 하는 방법에 대 한 자세한 내용은 "해상도 요구 사항 이름"을 참조 섹션 [광고 FS 요구](AD-FS-Requirements.md) 및 [웹 응용 프로그램 프록시 Infrastructure (WAP) 계획](https://technet.microsoft.com/library/dn383648.aspx)합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[해당 AD FS 배포가 계획](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 r 2의 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

