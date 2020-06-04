---
ms.assetid: 935ea7c2-4678-4033-b50f-2036a0359c5d
title: 페더레이션 서버를 배치하는 위치
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 503b1f206786d36364f9f0033ec0ea88330c444f
ms.sourcegitcommit: 2cc251eb5bc3069bf09bc08e06c3478fcbe1f321
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84333864"
---
# <a name="where-to-place-a-federation-server"></a>페더레이션 서버를 배치하는 위치

보안 모범 사례로, Active Directory Federation Services \( AD FS \) 페더레이션 서버를 방화벽 뒤에 놓고 회사 네트워크에 연결 하 여 인터넷 노출을 방지 합니다. 이는 페더레이션 서버에 보안 토큰을 부여 하는 전체 권한이 있기 때문에 중요 합니다. 따라서 도메인 컨트롤러와 동일하게 보호되어야 합니다. 페더레이션 서버가 손상 되 면 악의적인 사용자가 모든 웹 응용 프로그램 및 \( \) 모든 리소스 파트너 조직에서 Active Directory Federation Services AD FS 보호 하는 페더레이션 서버에 대 한 전체 액세스 토큰을 발급할 수 있습니다.  
  
> [!NOTE]  
> 보안을 위해 인터넷에서 페더레이션 서버에 직접 액세스할 수 있도록 하는 것이 좋습니다. 테스트 랩 환경을 설정 하거나 조직에 경계 네트워크가 없는 경우에만 페더레이션 서버에 직접 인터넷 액세스를 제공 하는 것이 좋습니다.  
  
일반적인 회사 네트워크의 경우 인트라넷 \- 방화벽은 회사 네트워크와 경계 네트워크 간에 설정 되 고 인터넷 \- 연결 방화벽은 경계 네트워크와 인터넷 간에 설정 되는 경우가 많습니다. 이 경우 페더레이션 서버는 회사 네트워크 내에 있으며 인터넷 클라이언트에서 직접 액세스할 수 없습니다.  
  
> [!NOTE]  
> 회사 네트워크에 연결 된 클라이언트 컴퓨터는 Windows 통합 인증을 통해 페더레이션 서버와 직접 통신할 수 있습니다.  
  
AD FS에 사용할 방화벽 서버를 구성 하기 전에 페더레이션 서버 프록시를 경계 네트워크에 배치 해야 합니다. 자세한 내용은 [페더레이션 서버 프록시를 배치할 위치](Where-to-Place-a-Federation-Server-Proxy.md)를 참조하세요.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server"></a>페더레이션 서버에 대한 방화벽 서버 구성  
페더레이션 서버가 페더레이션 서버 프록시와 직접 통신할 수 있도록 하려면 페더레이션 서버 프록시에서 페더레이션 서버로 보안 하이퍼텍스트 전송 프로토콜 HTTPS 트래픽을 허용 하도록 인트라넷 방화벽 서버를 구성 해야 합니다 \( \) . 이는 경계 네트워크의 페더레이션 서버 프록시가 페더레이션 서버에 액세스할 수 있도록 인트라넷 방화벽 서버에서 포트 443을 사용 하 여 페더레이션 서버를 게시 해야 하기 때문에 필요 합니다.  
  
또한 \- 인터넷 보안 및 가속화 ISA server를 실행 하는 서버와 같은 인트라넷 연결 방화벽 서버 \( 는 \) 서버 게시 라는 프로세스를 사용 하 여 인터넷 클라이언트 요청을 적절 한 회사 페더레이션 서버에 배포 합니다. 즉, http: fs.fabrikam.com와 같이 클러스터형 페더레이션 서버 URL을 게시 하는 ISA Server를 실행 하는 인트라넷 서버에서 서버 게시 규칙을 수동으로 만들어야 합니다 \/ \/ .  
  
경계 네트워크에 서버 게시를 구성하는 방법에 대한 자세한 내용은 [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md)를 참조하세요. 서버를 게시 하도록 ISA Server를 구성 하는 방법에 대 한 자세한 내용은 [안전한 웹 게시 규칙 만들기](https://go.microsoft.com/fwlink/?LinkId=75182)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
