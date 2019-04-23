---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: 페더레이션 서버 프록시를 만들어야 하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1f0253dfb5a690371dae1a2bfcb6b7520077d473
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883204"
---
# <a name="when-to-create-a-federation-server-proxy"></a>페더레이션 서버 프록시를 만들어야 하는 경우

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에 추가 보안 계층이 추가 조직에서 페더레이션 서버 프록시를 만드는 \(AD FS\) 배포 합니다. 하려는 경우 조직의 경계 네트워크의 페더레이션 서버 프록시를 배포 하는 것이 좋습니다.  
  
-   외부 클라이언트 컴퓨터를 직접 페더레이션 서버에 액세스 하지 못하도록 방지 합니다. 경계 네트워크의 페더레이션 서버 프록시를 배포 하 여 효과적으로 격리, 페더레이션 서버를 대신 하 여 작동 하는 페더레이션 서버 프록시를 통해 회사 네트워크에 로그인 하는 클라이언트 컴퓨터에 의해서만 액세스할 수 있도록 외부 클라이언트 컴퓨터입니다. 페더레이션 서버 프록시가 토큰을 생성하는 데 사용되는 개인 키에 액세스할 수 없는 경우. 자세한 내용은 참조 [페더레이션 서버 프록시 배치 위치](Where-to-Place-a-Federation-Server-Proxy.md)합니다.  
  
-   기호를 구분 하는 편리한 방법을 제공\-Windows 통합 인증을 사용 하 여 회사 네트워크에서 들어오는 사용자 달리, 인터넷에서 들어오는 사용자에 대 한 환경에서. 페더레이션 서버 프록시의 경우 로그온, 로그 아웃 및 id 공급자 검색을 사용 하 여 인터넷 클라이언트 컴퓨터에서 자격 증명 또는 홈 영역 세부 정보 수집 \(homerealmdiscovery.aspx\) 페더레이션에 저장 된 페이지 서버 프록시입니다.  
  
    반면, 다른 환경이 회사 네트워크 발생에서 제공 하는 클라이언트 컴퓨터 페더레이션 서버 구성에 기반 합니다. 회사 네트워크의 페더레이션 서버는 종종 원활 하 게 기호를 제공 하는 Windows 통합 인증을 구성\-회사 네트워크에서 사용자에 대 한 환경에서.  
  
조직에서 페더레이션 서버 프록시를 수행 하는 역할 계정 파트너 조직 또는 리소스 파트너 조직의 페더레이션 서버 프록시 배치 여부에 따라 달라 집니다. 예를 들어, 페더레이션 서버 프록시 계정 파트너의 경계 네트워크에 위치한, 해당 역할 때 브라우저 클라이언트에서 사용자 자격 증명 정보를 수집 합니다. 리소스 페더레이션 서버에 요청 하 고에서 제공 하는 보안 토큰에 대 한 응답으로 조직 보안 토큰을 생성 하는 보안 토큰 릴레이 리소스 파트너의 경계 네트워크에 페더레이션 서버 프록시를 배치 하면 해당 계정 파트너입니다.  
  
자세한 내용은 [Review the Role of the Federation Server Proxy in the Account Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) 및 [Review the Role of the Federation Server Proxy in the Resource Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)를 참조하세요.  
  
## <a name="how-to-create-a-federation-server-proxy"></a>페더레이션 서버 프록시를 만드는 방법  
AD FS 페더레이션 서버 프록시 구성 마법사 또는 Fsconfig.exe 명령을 사용 하 여 페더레이션 서버 프록시를 만들 수 있습니다\-명령줄 도구입니다. 이 작업을 수행하는 방법에 대한 지침은 [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)을 참조하세요.  
  
페더레이션 서버 프록시를 배포 하는 데 필요한 모든 필수 구성 요소를 설정 하는 방법에 대 한 일반 정보를 참조 하세요. [검사 목록: 페더레이션 서버 프록시 설정](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
