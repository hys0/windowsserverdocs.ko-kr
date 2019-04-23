---
ms.assetid: 935ea7c2-4678-4033-b50f-2036a0359c5d
title: 페더레이션 서버를 배치하는 위치
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 376cec7f3a4fb1f988ac5d458b05220c7b9de970
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857694"
---
# <a name="where-to-place-a-federation-server"></a>페더레이션 서버를 배치하는 위치

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

보안 모범 사례로, 내부 Active Directory Federation Services \(AD FS\)방화벽 앞에 페더레이션 서버를 인터넷에 노출 되지 않도록 회사 네트워크에 연결할 수 있습니다. 이 페더레이션 서버에 보안 토큰을 부여 하려면 전체 권한 부여 중요 합니다. 따라서 도메인 컨트롤러와 동일하게 보호되어야 합니다. 악의적 사용자가 모든 웹 응용 프로그램을 Active Directory Federation Services로 보호 되는 페더레이션 서버에 대 한 전체 액세스 토큰을 발급 하는 기능에 페더레이션 서버 보안이 손상 되 면 \(AD FS\) 모든 리소스 파트너 조직입니다.  
  
> [!NOTE]  
> 보안 모범 사례, 인터넷에 직접 액세스할 수 있는 페더레이션 서버에 있지 않도록 합니다. 테스트 랩 환경 또는 조직에 경계 네트워크가 없을 때를 설정 하는 경우에 페더레이션 서버 직접 인터넷 액세스를 제공 하는 것이 좋습니다.  
  
일반적인 회사 네트워크의 경우 인트라넷\-회사 네트워크 경계 네트워크 및 인터넷 간에 설정 된 방화벽 연결\-경계 네트워크 간에 자주 설정는 방화벽 연결 하며 인터넷입니다. 이 경우 회사 네트워크 내에서 페더레이션 서버 배치 및 인터넷 클라이언트가 직접 액세스할 수 없는 합니다.  
  
> [!NOTE]  
> 회사 네트워크에 연결 된 클라이언트 컴퓨터는 Windows 통합 인증을 통해 페더레이션 서버와 직접 통신할 수 있습니다.  
  
페더레이션 서버 프록시는 AD FS와 함께 사용할 방화벽 서버를 구성 하기 전에 경계 네트워크에 배치 되어야 합니다. 자세한 내용은 참조 [페더레이션 서버 프록시 배치 위치](Where-to-Place-a-Federation-Server-Proxy.md)합니다.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server"></a>페더레이션 서버에 대한 방화벽 서버 구성  
페더레이션 서버는 페더레이션 서버 프록시를 사용 하 여 직접 통신할 수 있습니다, 있도록 인트라넷 방화벽 서버 Secure Hypertext Transfer Protocol을 허용 하도록 구성 해야 합니다 \(HTTPS\) 트래픽과에 페더레이션 서버 프록시 페더레이션 서버입니다. 이것이 요구 사항은 인트라넷 방화벽 서버는 경계 네트워크의 페더레이션 서버 프록시가 페더레이션 서버에 액세스할 수 있도록 포트 443을 사용 하 여 페더레이션 서버를 게시 해야 합니다.  
  
또한 인트라넷\-Internet Security and Acceleration를 실행 하는 서버와 같은 방화벽 서버에 연결 \(ISA\) 서버, 서버 게시 라고 알려진 프로세스를 사용 하 여 인터넷 클라이언트 요청을 배포 하는 적절 한 회사 페더레이션 서버입니다. 즉, 예를 들어, http, 클러스터 된 페더레이션 서버 URL을 게시 하는 ISA Server를 실행 하는 인트라넷 서버에서 서버 게시 규칙을 수동으로 만들어야 합니다.\/\/fs.fabrikam.com입니다.  
  
경계 네트워크에 서버 게시를 구성하는 방법에 대한 자세한 내용은 [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md)를 참조하세요. 서버를 게시 하도록 ISA Server를 구성 하는 방법에 대 한 정보를 참조 하세요 [안전한 웹 게시 규칙 만들기](https://go.microsoft.com/fwlink/?LinkId=75182)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
