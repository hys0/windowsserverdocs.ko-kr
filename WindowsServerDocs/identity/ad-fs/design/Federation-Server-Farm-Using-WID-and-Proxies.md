---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: WID와 프록시를 사용하는 페더레이션 서버 팜
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d49ae34d83d4a0b912bd92dbb9de16e18cc5b7ff
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191343"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID와 프록시를 사용하는 페더레이션 서버 팜

Active Directory Federation Services에 대 한이 배포 토폴로지 \(AD FS\) 는 Windows 내부 데이터베이스를 사용 하 여 페더레이션 서버 팜에 동일 \(WID\) 토폴로지를 만들었지만 프록시 컴퓨터를 추가 합니다 외부 사용자를 지원 하도록 경계 네트워크입니다. 이러한 프록시는 페더레이션 서버 팜에 회사 네트워크 외부에서 제공 하는 클라이언트 인증 요청을 리디렉션합니다. AD FS의 이전 버전에서는 이러한 프록시는 페더레이션 서버 프록시를 이라고 했습니다.  
  
> [!IMPORTANT]  
> Active Directory Federation services에서 \(AD FS\) 웹 응용 프로그램 프록시 라는 새 원격 액세스 역할 서비스에서 Windows Server 2012 R2에서 페더레이션 서버 프록시 역할이 처리 됩니다. 레거시 버전의 AD FS 2.0 및 Windows Server 2012에서 AD FS와 같은 AD FS 페더레이션 서버 프록시 배포의 용도 회사 네트워크 외부에서 내게 필요한 옵션에 대 한 AD FS를 사용 하도록 설정 하려면 A에 대 한 하나 이상의 웹 응용 프로그램 프록시를 배포할 수 있습니다. Windows Server 2012 R2의 D FS 합니다.  
>   
> AD FS의 컨텍스트에서 웹 응용 프로그램 프록시는 AD FS 페더레이션 서버 프록시로 작동합니다. 이 외에도 웹 응용 프로그램 프록시는 회사 네트워크 내부의 웹 응용 프로그램에 대해 역방향 프록시 기능을 제공하여 모든 장치의 사용자가 회사 네트워크 권역을 벗어나서도 해당 네트워크에 접근할 수 있습니다. 웹 응용 프로그램 프록시 역할 서비스에 대한 자세한 내용은 웹 응용 프로그램 프록시 개요를 참조하세요.  
>   
> 웹 응용 프로그램 프록시 배포를 계획하려면 다음 항목의 정보를 검토하면 됩니다.  
>   
> -   [웹 응용 프로그램 프록시 인프라 (WAP) 계획](https://technet.microsoft.com/library/dn383648.aspx)  
> -   [웹 응용 프로그램 프록시 서버 계획](https://technet.microsoft.com/library/dn383647.aspx)  
  
## <a name="deployment-considerations"></a>배포 고려 사항  
이 섹션에서는 대상, 이점 및이 배포 토폴로지와 연결 된 제한 사항에 대 한 다양 한 고려 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지를 사용 해야 합니까?  
  
-   조직에서는 자신의 내부 사용자와 외부 사용자에 게 제공 해야 하는 구성 된 트러스트 관계를 100 개 이하인 \(회사 네트워크 외부에 있는 컴퓨터에 로그온\) 단일 기호로\-에 \(SSO\) 페더레이션된 응용 프로그램 또는 서비스에 대 한 액세스  
  
-   Microsoft Office 365에 SSO 액세스는 내부 사용자와 외부 사용자에 게 제공 해야 하는 조직  
  
-   외부 사용자가 고 중복이 고 확장 가능한 서비스를 요구 하는 소규모 조직  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 장점은 무엇입니까?  
  
-   에 나열과 같은 혜택은 [WID 페더레이션 서버 팜을 사용 하 여](Federation-Server-Farm-Using-WID.md) 토폴로지를 더한 외부 사용자에 대 한 추가 액세스를 제공 하는 혜택  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 제한 사항은 무엇입니까?  
  
-   에 대 한 나열과 같은 제한 사항이 [WID 페더레이션 서버 팜을 사용 하 여](Federation-Server-Farm-Using-WID.md) 토폴로지  

||1 \- 100 RP 트러스트|100 개가 넘는 RP 트러스트 
| ----- |-----| ------ |
|1 \- 30 AD FS 노드|WID 지원|WID를 사용 하 여 지원 되지 않는 \- 필요한 SQL 
|개 이상의 30 AD FS 노드|WID를 사용 하 여 지원 되지 않는 \- 필요한 SQL|WID를 사용 하 여 지원 되지 않는 \- 필요한 SQL  
  
## <a name="server-placement-and-network-layout-recommendations"></a>서버 배치와 네트워크 레이아웃 권장 사항  
두 개의 웹 응용 프로그램 프록시를 추가 하는 것 외에도이 토폴로지를 배포 해야 경계 네트워크 도메인 이름 시스템에 대 한 액세스를 제공할 수도 있습니다 \(DNS\) 서버 및 두 번째 네트워크 부하 분산에 \( NLB\) 호스트 합니다. 두 번째 NLB 호스트는 인터넷을 사용 하는 NLB 클러스터에 구성 해야\-하며 액세스 가능 클러스터 IP 주소를 회사 네트워크에 대해 구성한 이전 NLB 클러스터와 동일한 클러스터 DNS 이름 설정 사용 해야 \(fs.fabrikam.com\)합니다. 인터넷을 사용 하 여 웹 응용 프로그램 프록시 구성도 해야\-액세스할 수 있는 IP 주소입니다.  
  
두 번째 NLB 호스트를 동일한 클러스터 DNS 이름 추가하는다음그림에서는이전에설명한WID토폴로지및가상의Fabrikam,Inc.,회사경계DNS서버에대한액세스를제공하는방법을사용하여기존페더레이션서버팜에보여줍니다.\(fs.fabrikam.com\), 두 개의 웹 응용 프로그램 프록시를 추가 하 고 \(wap1 및 wap2\) 경계 네트워크에 있습니다.  
  
![WID 팜 및 프록시](media/WIDFarmADFSBlue.gif)  
  
페더레이션 서버 또는 웹 응용 프로그램 프록시 사용 하기 위해 네트워킹 환경을 구성 하는 방법에 대 한 자세한 내용은 "이름 확인 요구 사항"을 참조 하십시오. 섹션 [AD FS 요구 사항](AD-FS-Requirements.md) 및 [웹 응용 프로그램 프록시 인프라 (WAP) 계획](https://technet.microsoft.com/library/dn383648.aspx)합니다.  
  
## <a name="see-also"></a>관련 항목  
[AD FS 배포 토폴로지 계획](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

