---
ms.assetid: c4d83dd3-2846-4658-8b9c-93901ee69766
title: "Federation 서버를 배포"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 225e6b52ed46eef6f2ccacb5b0d9c6e6d880f475
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-federation-servers"></a>Federation 서버를 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services \(AD FS\) federation 서버를 배포 하려면 각에서 작업을 완료 [검사: Federation 서버 설정을](Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
> [!NOTE]  
> 이 검사를 사용 하는 경우 먼저 federation 서버에 계획에 대 한 언급을 읽고는 것이 좋습니다는 [Windows Server 2012에서 광고 FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 서버 구성 하는 절차를 시작 하기 전에 합니다. 이런 방법으로 검사를 수행 federation 서버에 대 한 배포 및 디자인 프로세스를 더 잘 이해를 제공 합니다.  
  
## <a name="about-federation-servers"></a>Federation 서버에 대 한  
Federation 서버는 federation 서버 역할에서 작동 하도록 구성 된 컴퓨터 ADFS 소프트웨어가 설치 된 Windows Server 2008 실행 합니다. Federation 서버 인증 하거나 요청 클라이언트 컴퓨터 될 수 있는 위치 어디서 나 인터넷 및 다른 조직에서 사용자 계정에서 보낸 합니다.  
  
컴퓨터에서 ADFS 소프트웨어를 설치 하 고 AD FS Federation 서버 구성 마법사 federation 서버 역할 구성를 사용 하 여 하면 해당 컴퓨터 federation 서버가 됩니다. 하기가 AD FS 관리 snap\에서 해당 컴퓨터에 사용할 수 있는 **Start\\Administrative Tools\\** 메뉴 다음 지정할 수 있도록 다음과 같습니다.  
  
-   토큰 요청 하 고 응답 파트너 조직 및 응용 프로그램은 전송 되는 위치 ADFS 호스트 이름  
  
-   고유한 이름을 또는 회사의 위치를 식별 하 파트너 조직 및 응용 프로그램의 ADFS 식별자를 사용할지  
  
-   토큰 서명 하 고 문제를 서버 그룹의 모든 federation 서버를 사용할 token\ 서명 인증서  
  
-   로그인, 로그 오프 및 클라이언트 환경이 개선 됩니다 계정 파트너 검색에 대 한 사용자 지정 된 ASP.NET 웹 페이지의 위치  
  
    > [!NOTE]  
    > 대부분의 핵심 이러한 사용자 인터페이스 \(UI\) 설정에서 각 federation 서버의 토큰과에 포함 되어 있습니다. ADFS 호스트 이름과 ADFS 식별자 값에는 토큰과 지정 되지 않습니다.  
  
Federation 서버 개최 된 자격 증명에 따라 토큰 문제는 클레임 발급 엔진 \ (예를 들어, 사용자 이름 및 password\)에 제공 되는 합니다. 보안 토큰은 하나 이상의 클레임 표현 하는 암호로 서명 된 데이터 단위 합니다. 클레임은 서버는 문을 \ (예: 이름, 신원을, 키, 그룹, 권한이 또는 capability\)에 대 한 클라이언트 합니다. 자격 증명 federation 서버에 확인 된 후 \ (의 사용자 로그온 process\)를 통해 사용자에 대 한 주장 사용자 지정 된 특성 스토어에 저장 되어 있는 특성 중 조사를 통해 수집 됩니다.  
  
웹 Single\-Sign\-On 연방 \(SSO\)에서 디자인 \ (ADFS 두 개 이상의 조직이 involved\ 되는 디자인) 청구 특정 당사자에 대 한 청구 규칙 수정할 수 있습니다. 클레임은 토큰 리소스 파트너 조직에서 federation 서버에 전송 된에 기본 제공 됩니다. Federation 서버 리소스 파트너에 들어오는 클레임으로 클레임을 받은 후 클레임 규칙 필터링 통과 또는 변환 클레임을 실행할 수 클레임 발급 엔진을 실행 합니다. 다음 리소스 파트너에는 웹 서버에 전송 된 새로운 토큰으로 클레임이 빌드됩니다.  
  
웹 SSO 디자인 \ (하나만 조직 인 involved\는 ADFS 디자인), 직원에 한 번에 로그인을 여러 응용 프로그램에 계속 액세스할 수 있도록 단일 federation 서버를 사용할 수 있습니다.  
  
