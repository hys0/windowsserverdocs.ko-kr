---
ms.assetid: ec26705c-4446-4226-b9b4-b775b642f0f4
title: "위치를 Federation 프록시 서버"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4bde30f694c6490962edaa0c3fe1543e74ba7fd7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="where-to-place-a-federation-server-proxy"></a>위치를 Federation 프록시 서버

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

인터넷에서 가져온 수 악의적인 사용자 로부터 보호 계층을 제공 하기 위해 주변 네트워크에서 Active Directory Federation Services \(AD FS\) federation 서버 프록시 배치할 수 있습니다. 토큰 만드는 데 사용 되는 개인 키에 대 한 액세스 없기 때문에 federation 서버 프록시는 주변 네트워크 환경에 대 한 적합 합니다. 그러나 federation 서버 프록시 이러한 토큰 생성 하기 위해 실시 권 자는 federation 서버에 들어오는 요청을 보낼 효율적으로 수 있습니다.  
  
회사 네트워크에 연결 하는 클라이언트 컴퓨터 federation 서버 직접와 통신할 수 있으므로 계정 파트너 또는 리소스 파트너 회사의 네트워크 안에 federation 서버 프록시를 필요는 없습니다. 이 경우에는 federation 서버 회사 네트워크에서 제공 하는 클라이언트 컴퓨터에 대 한 federation 서버 프록시 기능을 제공 합니다.  
  
주변 네트워크 회사 네트워크와 intranet\ 전면 방화벽 설정 되와 마찬가지로 주변 네트워크를 하 고 Internet\ 전면 방화벽 주변 네트워크 및 인터넷 간에 자주 설정 됩니다. 이 경우 두 가지 주변 네트워크에 이러한 방화벽 사이 federation 서버 프록시 위치 합니다.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server-proxy"></a>방화벽 서버 federation 프록시 서버에 대 한 구성  
Federation 서버 프록시 리디렉션 프로세스에 성공적으로 모든 방화벽 서버가 프로토콜을 전송 하이퍼텍스트 보안 \(HTTPS\) 교통 수 있도록 설정 해야 합니다. HTTPS 사용 하는 방화벽 서버 주변 네트워크에 federation 서버 프록시 federation 서버 회사 네트워크에 액세스할 수 있도록 443, 포트를 사용 하 여 federation 서버 프록시 게시 해야 필요 합니다.  
  
> [!NOTE]  
> HTTPS를 통해 하 고 클라이언트 컴퓨터의 모든 통신도 발생합니다.  
  
또한 Internet\ 전면 방화벽 가속 및 Microsoft Internet Security 실행 하는 컴퓨터와 같은 서버 \(ISA\) 서버를 사용 하 여 서버 게시로 알려진 프로세스 인터넷 클라이언트 요청 적절 한 주변 및 회사 네트워크 서버 federation 서버 프록시 서버 federation 등을 배포 합니다.  
  
서버 게시 규칙 서버 게시 작동 하는 방법을 결정-스크리닝하 컴퓨터를 통해 모든 송수신 요청을 기본적으로 필터링 합니다. 서버 게시 규칙 들어오는 클라이언트 요청 스크리닝하 컴퓨터 뒤에 적절 한 서버에 매핑됩니다. 서버를 게시 하 스크리닝하 구성 하는 방법에 대 한 정보를 참조 하세요. [보안 웹 게시 규칙 만들](https://go.microsoft.com/fwlink/?LinkId=75182)합니다.  
  
Adfs의 연결 된 세계에서 이러한 클라이언트 요청 특정 URL 예를 들어, federation 서버 식별자 URL http://fs.fabrikam.com 등 일반적으로 변경 됩니다. 이러한 클라이언트 요청 제공 하기 때문에 인터넷에서 Internet\ 전면 방화벽 서버 구성 해야 주변 네트워크에 배포 되는 각 federation 서버 프록시 federation 서버 식별자 URL을 게시할 수 있습니다.  
  
### <a name="configuring-isa-server-to-allow-ssl"></a>구성 스크리닝하 SSL 허용 하려면  
보안 ADFS 통신을 위해 다음 간 통신 안전한 주소 \(SSL\) 수 있도록 스크리닝하 구성 해야 합니다.  
  
-   **Federation 서버 및 federation 서버 프록시 합니다.** SSL 채널은 federation 서버 federation 서버 프록시와의 모든 통신 필요 합니다. 따라서 스크리닝하 SSL 주변 네트워크 회사 네트워크와 연결을 허용 하려면 구성 해야 합니다.  
  
-   **클라이언트 컴퓨터, federation 서버 및 federation 서버 프록시 합니다.** 통신 클라이언트 컴퓨터와 federation 서버 또는 클라이언트 컴퓨터와 federation 서버 프록시 발생할 수 있도록 federation 서버 또는 federation 서버 프록시 앞 스크리닝하 실행 하는 컴퓨터를 배치할 수 있습니다.  
  
    서버에 대 한 구성 해야 경우 조직의 SSL 클라이언트 인증 federation 서버 또는 federation 서버 프록시 federation 서버 또는 federation 서버 프록시 앞 스크리닝하 실행 하는 컴퓨터 위치, pass\ 쓰루 SSL 연결 SSL 연결 federation 서버 또는 federation 서버 프록시 종료 해야 하기 때문입니다.  
  
    옵션을 추가로 스크리닝하 및 re\ 실행 하는 컴퓨터에서 SSL 연결 종료 하는 조직에서 federation 서버 또는 federation 서버 프록시 SSL 클라이언트 인증 작동 하지 않으면,-federation 서버 또는 federation 서버 프록시 SSL 연결을 설정 합니다.  
  
> [!NOTE]  
> Federation 서버 또는 federation 서버 프록시 연결 보안 토큰의 콘텐츠를 보호 하기 위해 SSL으로 보호 되지 필요 합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
