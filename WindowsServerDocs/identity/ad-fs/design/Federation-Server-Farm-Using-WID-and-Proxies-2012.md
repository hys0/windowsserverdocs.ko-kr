---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: "Federation 서버 팜 WID 및 프록시 사용 하 여"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4bd815daccdd72a8c612b9b728ce12378c1926e7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Federation 서버 팜 WID 및 프록시 사용 하 여

>적용 대상: Windows Server 2012

Active Directory Federation Services \(AD FS\)가 배포가 Windows 내부 데이터베이스 \(WID\) 토폴로지 federation 서버 팜 동일 하지만 federation 서버 프록시 외부 사용자를 지 원하는 주변 네트워크에 추가 합니다. Federation 서버 프록시 federation 서버 팜 하 여 회사 네트워크에서 벗어나 있는 제공 하는 클라이언트 인증 요청 이동 합니다.  
  
## <a name="deployment-considerations"></a>배포 고려  
이 여기서 대상, 혜택을 및이 배포가와 관련 된 제한 사항에 대 한 다양 한 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지 사용 해야 하나요?  
  
-   조직에는 해당 내부 사용자 및 외부 사용자에 게 제공 해야 하는 100 이하의 구성 된 보안 관계 \ (로그온 회사 network\ 밖에 있을 실제로 컴퓨터로) 단일 sign\ 켜 짐 \(SSO\)에 액세스할 수 있는 연결 된 응용 프로그램이 나 서비스  
  
-   Microsoft Office 365에 SSO에 액세스할 수 있는 자신의 내부 사용자 및 외부 사용자에 게 제공 해야 하는 조직  
  
-   중소기업 외부 사용자가 있는 중복, 확장 서비스  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지에 사용 하는 어떤 혜택이 있나요?  
  
-   동일한 혜택에 대 한 나열 된는 [Federation 서버 농장을 사용 하 여 WID](Federation-Server-Farm-Using-WID-2012.md) 토폴로지에서 이용 외부 사용자에 대 한 추가 액세스를 제공의 혜택  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여 제한 이란 무엇 인가요?  
  
-   에 나열 된와 같은 제한은 [Federation 서버 농장을 사용 하 여 WID](Federation-Server-Farm-Using-WID-2012.md) 토폴로지  
  
## <a name="server-placement-and-network-layout-recommendations"></a>네트워크 위치와 위치 레이아웃 추천 서버  
두 federation 서버 프록시 추가 외에이 토폴로지 배포 하는 주변 네트워크 두 번째 네트워크 부하 분산 \(NLB\) 호스트 Domain Name System \(DNS\) 서버에 대 한 액세스 제공할 수도 있다는 있는지 확인 해야 합니다. 두 번째 NLB 호스트 Internet\ 액세스할 수 있는 클러스터 IP 주소를 사용 하는 NLB 클러스터로 구성 해야 하 고 회사 네트워크 \(fs.fabrikam.com\)에서 구성 이전 nlb와 동일한 클러스터 DNS name 설정을 사용 해야 합니다. Federation 서버 프록시 Internet\ 액세스할 수 있는 IP 주소를 구성 해야 합니다.  
  
다음 그림에서는 기존 federation 서버 농장 WID 이전에 설명 된 토폴로지와 가상 원 창의 회사 주변 DNS 서버에 대 한 액세스를 제공 하는 방법을와 같은 클러스터 DNS 이름 \(fs.fabrikam.com\) NLB 호스트를 두 번째 하 고 추가 두 federation 서버 프록시 \(fsp1 and fsp2\) 주변 네트워크입니다.  
  
![서버 농장 WID를 사용 하 여](media/FarmWIDProxies.gif)  
  
사용 하기 위해 네트워킹 환경을 federation 서버 또는 federation 서버 프록시 구성 하는 방법에 대 한 자세한 내용은 참조 [이름을 확인 요구 사항을 Federation 서버에 대 한](Name-Resolution-Requirements-for-Federation-Servers.md) 또는 [이름 해상도 요구 사항을 Federation 서버 프록시](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
