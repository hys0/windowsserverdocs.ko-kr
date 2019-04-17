---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: "Federation 서버 프록시 만들어야 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1f0253dfb5a690371dae1a2bfcb6b7520077d473
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="when-to-create-a-federation-server-proxy"></a>Federation 서버 프록시 만들어야 하는 경우

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에서 federation 서버 프록시 만들기 추가 보안 계층 Active Directory Federation Services \(AD FS\) 배포를 추가 합니다. 주변 조직의 네트워크에 federation 서버 프록시 하려는 경우 배포 하는 것이 좋습니다.  
  
-   직접 federation 서버에 액세스 하지 못하도록 클라이언트 외부 컴퓨터를 방지 합니다. 주변 네트워크에서 federation 서버 프록시를 배포 하 여 효과적으로 격리 federation 서버 클라이언트 외부 컴퓨터를 대신 하는 federation 서버 프록시 통해 회사 네트워크에 로그인 하는 컴퓨터 에서만 하 여 액세스할 수 있도록 합니다. Federation 서버 프록시 토큰 생성 하는 데 사용 하는 개인 키에 대 한 액세스를 권한이 수 없습니다. 자세한 내용은 참조 [Federation 서버 프록시 위치](Where-to-Place-a-Federation-Server-Proxy.md)합니다.  
  
-   사용자는 사용자에 게 Windows 통합 인증을 사용 하 여 회사 네트워크에서 출시 하지 않고 인터넷에서 제공한 것임를 위한 sign\의 경험을 구분 하는 편리한 방법을 제공 합니다. Federation 서버 프록시 로그온, 로그 아웃 및 해당 federation 서버 프록시에 저장 된 신원 공급자 검색 \(homerealmdiscovery.aspx\) 페이지를 사용 하 여 인터넷 클라이언트 컴퓨터에서 자격 증명 또는 홈 영역 세부 정보를 수집 합니다.  
  
    반면, 회사 네트워크 발견 다른 환경에서에서 제공 하는 클라이언트 컴퓨터 federation 서버 구성에 따라 합니다. 회사 네트워크 federation 서버 회사 네트워크에 사용자를 위한 원활 하 게 sign\의 경험을 제공 하는 Windows 통합 인증에 대 한 구성 자주 됩니다.  
  
조직에서 재생 federation 서버 프록시 역할 리소스 파트너 조직 또는 계정 파트너 조직에서 federation 서버 프록시 배치 있는지 여부에 따라 달라 집니다. 예를 들어 계정 파트너의 주변 네트워크에 federation 서버 프록시 놓으면의 역할 브라우저 클라이언트에서의 사용자 자격 증명 정보를 수집 하는 합니다. Federation 서버 프록시 리소스 파트너의 주변 네트워크 놓으면 리소스 federation 서버에 대 한 보안 토큰 요청 릴레이 하 고 계정 파트너도 제공 되는 보안 토큰에 대 한 응답에서 조직의 보안 토큰 생성 합니다.  
  
자세한 내용은 참조 [계정 파트너의 Federation 서버 프록시 역할을 검토](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) 및 [리소스 파트너에 Federation 서버 프록시 역할을 검토](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)  
  
## <a name="how-to-create-a-federation-server-proxy"></a>Federation 프록시 서버를 만드는 방법  
AD Federation 서버 FS 프록시 구성을 마법사 또는 Fsconfig.exe command\ 선 도구를 사용 하 여 federation 서버 프록시를 만들 수 있습니다. 이 작업을 수행 하는 방법에 대 한 지침은 참조 [Federation 서버 프록시 역할 컴퓨터 구성](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)합니다.  
  
Federation 서버 프록시 배포 하는 데 필요한 모든 필수를 설정 하는 방법에 대 한 일반 정보를 참조 하세요. [검사: 설정을을 Federation 서버 프록시](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
