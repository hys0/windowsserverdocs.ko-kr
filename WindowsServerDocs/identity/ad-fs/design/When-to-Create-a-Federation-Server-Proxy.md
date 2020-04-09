---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: 페더레이션 서버 프록시를 만들어야 하는 경우
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 13ca7d49e8044273c9f40e58c06e705e758c68bf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858486"
---
# <a name="when-to-create-a-federation-server-proxy"></a>페더레이션 서버 프록시를 만들어야 하는 경우

조직에서 페더레이션 서버 프록시를 만들면 Active Directory Federation Services \(AD FS\) 배포에 추가 보안 계층이 추가 됩니다. 다음을 수행 하려는 경우 조직의 경계 네트워크에 페더레이션 서버 프록시를 배포 하는 것이 좋습니다.  
  
-   외부 클라이언트 컴퓨터가 페더레이션 서버에 직접 액세스 하지 못하도록 합니다. 경계 네트워크에 페더레이션 서버 프록시를 배포 하면 페더레이션 서버 프록시를 통해 회사 네트워크에 로그인 한 클라이언트 컴퓨터에만 액세스할 수 있도록 페더레이션 서버를 효과적으로 격리 합니다 .이는 외부 클라이언트 컴퓨터를 대신 하 여 작동 합니다. 페더레이션 서버 프록시가 토큰을 생성하는 데 사용되는 프라이빗 키에 액세스할 수 없는 경우. 자세한 내용은 참조 [페더레이션 서버 프록시 배치 위치](Where-to-Place-a-Federation-Server-Proxy.md)합니다.  
  
-   Windows 통합 인증을 사용 하 여 회사 네트워크에서 들어오는 사용자와 달리, 인터넷에서 들어오는 사용자에 대 한 로그인\-의 편리한 방법을 제공 합니다. 페더레이션 서버 프록시는 페더레이션 서버 프록시에 저장 된 homerealmdiscovery.aspx\) 페이지 \(로그온, 로그 아웃 및 id 공급자 검색을 사용 하 여 인터넷 클라이언트 컴퓨터에서 자격 증명 또는 홈 영역 세부 정보를 수집 합니다.  
  
    반면, 회사 네트워크에서 제공 되는 클라이언트 컴퓨터는 페더레이션 서버의 구성에 따라 다른 환경이 발생 합니다. 회사 네트워크 페더레이션 서버는 Windows 통합 인증에 대해 구성 되는 경우가 많으므로 회사 네트워크의 사용자에 게 원활한 서명\-를 제공 합니다.  
  
페더레이션 서버 프록시가 조직에서 수행 하는 역할은 계정 파트너 조직 또는 리소스 파트너 조직에 페더레이션 서버 프록시를 배치할지 여부에 따라 달라 집니다. 예를 들어 페더레이션 서버 프록시가 계정 파트너의 경계 네트워크에 배치 된 경우 해당 역할은 브라우저 클라이언트에서 사용자 자격 증명 정보를 수집 하는 것입니다. 페더레이션 서버 프록시는 리소스 파트너의 경계 네트워크에 배치 되는 경우 리소스 페더레이션 서버에 보안 토큰 요청을 릴레이 하 고 계정 파트너가 제공한 보안 토큰에 대 한 응답으로 조직 보안 토큰을 생성 합니다.  
  
자세한 내용은 [Review the Role of the Federation Server Proxy in the Account Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) 및 [Review the Role of the Federation Server Proxy in the Resource Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)를 참조하세요.  
  
## <a name="how-to-create-a-federation-server-proxy"></a>페더레이션 서버 프록시를 만드는 방법  
페더레이션 서버 프록시는 AD FS 페더레이션 서버 프록시 구성 마법사나 Fsconfig 명령\-줄 도구를 사용 하 여 만들 수 있습니다. 이 작업을 수행하는 방법에 대한 지침은 [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)을 참조하세요.  
  
페더레이션 서버 프록시를 배포하는 데 필요한 모든 필수 구성 요소를 설정하는 방법에 대한 일반적인 내용은 [Checklist: Setting Up a Federation Server Proxy](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
