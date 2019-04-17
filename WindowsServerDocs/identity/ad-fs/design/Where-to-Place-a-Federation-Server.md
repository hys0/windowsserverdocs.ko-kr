---
ms.assetid: 935ea7c2-4678-4033-b50f-2036a0359c5d
title: "위치를 Federation 서버"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 376cec7f3a4fb1f988ac5d458b05220c7b9de970
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="where-to-place-a-federation-server"></a>위치를 Federation 서버

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

보안 가장 연습 방화벽 앞 Active Directory Federation Services \(AD FS\) federation 서버 놓고 노출은 인터넷에서 되지 않도록 하 여 회사 네트워크에 연결 합니다. 이 federation 서버 전체 수 있는 권한이 부여 보안 토큰 중요 합니다. 따라서 도메인 컨트롤러도 동일한 보호가 있어야 합니다. Federation 서버 손상 되 면 악의적인 사용자가 및 federation 서버 Active Directory Federation Services \(AD FS\) 모든 리소스 파트너 조직에 의해 보호 되는 모든 웹 응용 프로그램에 대 한 전체 액세스 토큰 드릴 수 있습니다.  
  
> [!NOTE]  
> 보안을 위해 인터넷에 액세스할 수 있는 직접 federation 서버 되지 않도록 합니다. 테스트 랩 환경 또는 조직이 주변 네트워크 없는 설정 하는 경우에 해당 federation 서버 직접 인터넷 액세스를 제공 하는 것이 좋습니다.  
  
일반적인 회사 네트워크에 대 한 주변 네트워크 회사 네트워크와 intranet\ 전면 방화벽 설정 되 고 Internet\ 전면 방화벽 주변 네트워크 및 인터넷 간에 자주 설정 됩니다. 이 경우 회사의 네트워크 안에 federation 서버에 위치 하 고 직접 인터넷 클라이언트에서 액세스할 수 없는 합니다.  
  
> [!NOTE]  
> 회사 네트워크에 연결 하는 클라이언트 컴퓨터 Windows 통합 인증을 통해 federation 서버를 사용 하 여 직접 통신할 수 있습니다.  
  
Adfs로 사용 하기 위해 방화벽 서버 구성 하기 전에 federation 서버 프록시 주변 네트워크에 있어야 합니다. 자세한 내용은 참조 [Federation 서버 프록시 위치](Where-to-Place-a-Federation-Server-Proxy.md)합니다.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server"></a>방화벽 서버 federation 서버에 대 한 구성  
Federation 서버 프록시와 직접 federation 서버 통신할 수, 방화벽 인트라넷 서버 federation 서버에 federation 서버 프록시에서 프로토콜을 전송 하이퍼텍스트 보안 \(HTTPS\) 교통 수 있도록 설정 해야 합니다. 요구 사항을 방화벽 인트라넷 서버 주변 네트워크에 federation 서버 프록시 federation 서버에 액세스할 수 있도록 443 포트를 사용 하 여 federation 서버 게시 해야 하기 때문입니다.  
  
또한 intranet\ 전면 방화벽 인터넷 보안 및 가속 실행 하는 서버와 같은 서버 \(ISA\) 서버를 사용 하 여 서버 게시로 알려진 프로세스 회사 해당 federation 서버로 인터넷 클라이언트 요청을 배포 합니다. 즉, 예를 들어, http:///\/fs.fabrikam.com 클러스터 federation 서버 URL 게시 스크리닝하 실행 인트라넷 서버에 서버 게시 규칙 수동으로 만들 해야 합니다.  
  
주변 네트워크에 게시 서버 구성 하는 방법에 대 한 자세한 내용은 참조 [Federation 서버 프록시 위치](Where-to-Place-a-Federation-Server-Proxy.md)합니다. 서버를 게시 하 스크리닝하 구성 하는 방법에 대 한 정보를 참조 하세요. [안전한 웹 게시 규칙 만들](https://go.microsoft.com/fwlink/?LinkId=75182)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
