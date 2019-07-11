---
ms.assetid: ec26705c-4446-4226-b9b4-b775b642f0f4
title: 페더레이션 서버 프록시를 배치하는 위치
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 03792d7ae5fec3c209cf1abfaa7af3fdfdb75f08
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792270"
---
# <a name="where-to-place-a-federation-server-proxy"></a>페더레이션 서버 프록시를 배치하는 위치

Active Directory Federation Services를 배치할 수 있습니다 \(AD FS\)페더레이션 서버 프록시는 경계 네트워크에 인터넷에서 제공 될 수 있는 악의적 사용자에 대 한 보호 계층을 제공 합니다. 페더레이션 서버 프록시는 토큰을 만드는 데 사용되는 프라이빗 키에 액세스할 수 없으므로 경계 네트워크 환경에 적합합니다. 그러나 페더레이션 서버 프록시 해당 토큰을 생성할 수 있는 권한이 있는 페더레이션 서버에 들어오는 요청을 라우팅할 효율적으로 수 있습니다.  
  
회사 네트워크에 연결 된 클라이언트 컴퓨터 페더레이션 서버와 직접 통신할 수 있으므로 회사 네트워크 내부에 페더레이션 서버 프록시 계정 파트너 또는 리소스 파트너에 대 한 배치 하는 데 필요한 것입니다. 이 시나리오에서는 페더레이션 서버를 회사 네트워크에서 생성 되는 클라이언트 컴퓨터에 대 한 페더레이션 서버 프록시 기능도 제공 합니다.  
  
인트라넷 경계 네트워크를 사용 하 여 일반적인 그대로\-경계 네트워크와 회사 네트워크와 인터넷 간에 설정 된 방화벽 연결\-경계 네트워크 간에 자주 설정는 방화벽 연결 하며 인터넷입니다. 이 시나리오에서 페더레이션 서버 프록시 간에 이러한 두 방화벽 경계 네트워크에 배치 됩니다.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server-proxy"></a>페더레이션 서버 프록시에 대한 방화벽 서버 구성  
페더레이션 서버 프록시 리디렉션 프로세스에 성공 하려면 모든 방화벽 서버 Secure Hypertext Transfer Protocol을 허용 하도록 구성 해야 합니다 \(HTTPS\) 트래픽입니다. 방화벽 서버는 페더레이션 서버 프록시가 경계 네트워크의 회사 네트워크의 페더레이션 서버에 액세스할 수 있도록 포트 443을 사용 하 여 페더레이션 서버 프록시를 게시 해야 하므로 https를 사용 하 여 필요 합니다.  
  
> [!NOTE]  
> 클라이언트 컴퓨터와의 모든 통신도 HTTPS를 통해 발생합니다.  
  
또한 인터넷\-Microsoft Internet Security and Acceleration를 실행 하는 컴퓨터와 같은 방화벽 서버에 연결 \(ISA\) 서버, 서버 게시 라고 알려진 프로세스를 사용 하 여 인터넷 클라이언트를 배포 하려면 적절 한 경계 및 페더레이션 서버 프록시 또는 페더레이션 서버와 같은 회사 네트워크 서버에 요청 합니다.  
  
서버 게시 규칙은 서버 게시의 작동 방식을 결정하며, 기본적으로 ISA Server 컴퓨터를 통해 들어오고 나가는 모든 요청을 필터링합니다. 서버 게시 규칙은 들어오는 클라이언트 요청을 ISA Server 컴퓨터 뒤의 해당 서버에 매핑합니다. 서버를 게시 하도록 ISA Server를 구성 하는 방법에 대 한 정보를 참조 하세요 [보안 웹 게시 규칙 만들기](https://go.microsoft.com/fwlink/?LinkId=75182)합니다.  
  
AD FS의 페더레이션된 환경에서 이러한 클라이언트 요청이 일반적으로 이루어집니다 특정 URL에 예를 들어, http와 같은 페더레이션 서버 식별자 URL을:\//fs.fabrikam.com 합니다. 이러한 클라이언트 요청 때문에 인터넷에서 인터넷을 통해\-연결 방화벽 서버가 경계 네트워크에 배포 된 각 페더레이션 서버 프록시에 대 한 페더레이션 서버 식별자 URL을 게시 하도록 구성 되어야 합니다.  
  
### <a name="configuring-isa-server-to-allow-ssl"></a>SSL을 허용하도록 ISA Server 구성  
AD FS 통신 보안을 위해 Secure Sockets Layer를 허용 하도록 ISA Server를 구성 해야 합니다 \(SSL\) 다음 간의 통신 합니다.  
  
-   **페더레이션 서버 및 페더레이션 서버 프록시입니다.** SSL 채널은 페더레이션 서버 및 페더레이션 서버 프록시 간의 모든 통신에 필요 합니다. 따라서 회사 네트워크와 경계 네트워크 간에 SSL 연결을 허용하도록 ISA Server를 구성해야 합니다.  
  
-   **클라이언트 컴퓨터, 페더레이션 서버 및 페더레이션 서버 프록시** 클라이언트 컴퓨터와 페더레이션 서버 또는 클라이언트 컴퓨터 및 페더레이션 서버 프록시 간에 통신이 발생할 수 있도록 페더레이션 서버 또는 페더레이션 서버 프록시 앞에 ISA Server를 실행 하는 컴퓨터를 배치할 수 있습니다.  
  
    Pass에대한서버를구성해야페더레이션서버또는페더레이션서버프록시앞에ISAServer를실행하는컴퓨터를배치하는경우페더레이션서버또는페더레이션서버프록시에SSL클라이언트인증을수행하는조직,경우\-를 통해 SSL 연결의 페더레이션 서버 또는 페더레이션 서버 프록시에 SSL 연결 종료 해야 하기 때문에 있습니다.  
  
    ISA Server 및 다시 실행 하는 컴퓨터에서 SSL 연결을 종료 하는 추가 옵션은 조직의 페더레이션 서버 또는 페더레이션 서버 프록시에 SSL 클라이언트 인증을 수행 하지 않으면,\-SSL 연결을 설정 합니다. 페더레이션 서버 또는 페더레이션 서버 프록시입니다.  
  
> [!NOTE]  
> 페더레이션 서버 또는 페더레이션 서버 프록시 연결 보안 토큰의 내용을 보호 하는 SSL로 보호할 수는 필요 합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
