---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: WID와 프록시를 사용하는 페더레이션 서버 팜
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 60072037aea4ecd81376e1334f3a89b7bb2ff851
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408088"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>WID와 프록시를 사용하는 페더레이션 서버 팜

Active Directory Federation Services \(AD FS @ no__t-1에 대 한이 배포 토폴로지는 Windows 내부 데이터베이스 \(WID @ no__t 토폴로지를 사용 하는 페더레이션 서버 팜과 동일 하지만 경계 네트워크에 페더레이션 서버 프록시를 추가 합니다. 외부 사용자를 지원 합니다. 페더레이션 서버 프록시는 페더레이션 서버 팜에 회사 네트워크 외부에서 발생 하는 클라이언트 인증 요청을 리디렉션합니다.  
  
## <a name="deployment-considerations"></a>배포 고려 사항  
이 섹션에서는 대상, 이점 및이 배포 토폴로지와 연결 된 제한 사항에 대 한 다양 한 고려 사항을 설명 합니다.  
  
### <a name="who-should-use-this-topology"></a>누가이 토폴로지를 사용 해야 합니까?  
  
-   조직에서는 자신의 내부 사용자와 외부 사용자에 게 제공 해야 하는 구성 된 트러스트 관계를 100 개 이하인 \(회사 네트워크 외부에 있는 컴퓨터에 로그온\) 단일 기호로\-에 \(SSO\) 페더레이션된 응용 프로그램 또는 서비스에 대 한 액세스  
  
-   Microsoft Office 365에 SSO 액세스는 내부 사용자와 외부 사용자에 게 제공 해야 하는 조직  
  
-   외부 사용자가 고 중복이 고 확장 가능한 서비스를 요구 하는 소규모 조직  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 장점은 무엇입니까?  
  
-   에 나열과 같은 혜택은 [WID 페더레이션 서버 팜을 사용 하 여](Federation-Server-Farm-Using-WID-2012.md) 토폴로지를 더한 외부 사용자에 대 한 추가 액세스를 제공 하는 혜택  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>이 토폴로지를 사용 하 여의 제한 사항은 무엇입니까?  
  
-   에 대 한 나열과 같은 제한 사항이 [WID 페더레이션 서버 팜을 사용 하 여](Federation-Server-Farm-Using-WID-2012.md) 토폴로지  
  
## <a name="server-placement-and-network-layout-recommendations"></a>서버 배치와 네트워크 레이아웃 권장 사항  
두 명의 페더레이션 서버 프록시를 추가 하는 것 외에도이 토폴로지를 배포 하 여 경계 네트워크 도메인 이름 시스템에 대 한 액세스를 제공할 수도 있습니다 있는지 확인 해야 \(DNS\) 서버 및 두 번째 네트워크 부하 분산을 \(NLB\) 호스트 합니다. 두 번째 NLB 호스트는 인터넷을 사용 하는 NLB 클러스터에 구성 해야\-하며 액세스 가능 클러스터 IP 주소를 회사 네트워크에 대해 구성한 이전 NLB 클러스터와 동일한 클러스터 DNS 이름 설정 사용 해야 \(fs.fabrikam.com\)합니다. 인터넷으로 페더레이션 서버 프록시 구성도 해야\-액세스할 수 있는 IP 주소입니다.  
  
동일한 클러스터 DNS 이름으로 두 번째 NLB 호스트를 추가 하는 다음 그림에서는 이전에 설명한 WID 토폴로지 및 가상의 Fabrikam, Inc., 회사에서 경계 DNS 서버에 대 한 액세스를 제공 하는 방법을 사용 하 여 기존 페더레이션 서버 팜에 \(fs.fabrikam.com\), 두 명의 페더레이션 서버 프록시를 추가 하 고 \(fsp1 및 fsp2\) 경계 네트워크에 있습니다.  
  
![WID를 사용 하 여 서버 팜](media/FarmWIDProxies.gif)  
  
페더레이션 서버 또는 페더레이션 서버 프록시를 사용 하기 위해 네트워킹 환경을 구성 하는 방법에 대 한 자세한 내용은 참조 [페더레이션 서버에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Servers.md) 또는 [페더레이션 서버 프록시에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
