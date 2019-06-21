---
title: 5 단계는 DC1 구성
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70357156-fcb0-4346-a61e-4ea963e3ffb0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 108e517923c75f685d817cdf9fad9b14132e3bb0
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281440"
---
# <a name="step-5-configure-dc1"></a>5 단계는 DC1 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

DC1은 도메인 컨트롤러, DNS 서버 및 corp.contoso.com 도메인에 대 한 DHCP 서버 작동합니다.  
  
멀티 사이트 토폴로지를 사용 하려면 원격 액세스를 구성 하려면 두 번째 도메인 컨트롤러 2-DC1에 대 한 추가 Active Directory Domain Services (AD DS) 사이트를 추가 하 고 서브넷 간에 라우팅을 구성 하는 데 필요한 됩니다.  
  
1. 도메인 컨트롤러에서 기본 게이트웨이 구성 합니다. DC1에서 기본 게이트웨이 구성 합니다.  
  
2. DC1에서 Windows 7 DirectAccess 클라이언트에 대 한 보안 그룹을 만듭니다. DirectAccess를 구성한 경우 자동으로 만들면 그룹 정책 개체 (Gpo) 및 DirectAccess 클라이언트 및 서버에 적용 되는 GPO 설정 합니다. DirectAccess 클라이언트 GPO는 특정 Active Directory 보안 그룹에 적용 됩니다.  
  
3. 새 AD DS 사이트를 추가 합니다. 두 번째 AD DS 사이트를 만듭니다.  
  
## <a name="to-configure-the-default-gateway-on-the-domain-controller"></a>도메인 컨트롤러에서 기본 게이트웨이 구성 하려면  
  
1.  서버 관리자 콘솔에서 클릭 **로컬 서버**를 선택한 다음는 **속성** 영역에서 다음을 **유선 이더넷 연결**, 링크를 클릭 합니다.  
  
2.  네트워크 연결 창에서 마우스 오른쪽 단추로 클릭 **유선 이더넷 연결**를 클릭 하 고 **속성**합니다.  
  
3.  **Internet Protocol Version 4(TCP/IPv4)** 를 클릭하고 **속성**을 클릭합니다.  
  
4.  **기본 게이트웨이**, 형식 **10.0.0.254**, 및 **대체 DNS 서버**, 형식 **10.2.0.1**를 클릭 하 고 **확인** .  
  
5.  **인터넷 프로토콜 버전 6(TCP/IPv6)** , **속성**을 차례로 클릭합니다.  
  
6.  **기본 게이트웨이**, 형식 **2001:db8:1::fe**, 및 **대체 DNS 서버**, 형식 **2001:db8:2::1**를 클릭및**확인**합니다.  
  
7.  에 **유선 이더넷 연결 속성** 대화 상자, 클릭 **닫기**합니다.  
  
8.  **네트워크 연결** 창을 닫습니다.  
  
## <a name="create-security-groups-for-windows-7-directaccess-clients-on-dc1"></a>DC1에서 Windows 7 DirectAccess 클라이언트에 대 한 보안 그룹 만들기  
다음 절차를 사용 하 여 Windows 7 DirectAccess 보안 그룹을 만듭니다.  
  
 Windows 7 클라이언트 컴퓨터만 단일 액세스 지점을 통해 내부 리소스에 연결할 수 있기 때문에 별도 보안 그룹의 구성원 이어야 합니다. 다중 사이트 지원을 사용 하도록 설정 하거나 항목을 추가 가리킬 때, Windows 7 지원을 요청 하는 경우, 자동으로 별도 GPO 각 진입점에 대 한 Windows 7 DirectAccess 클라이언트에서 생성 됩니다.  
  
### <a name="create-security-groups"></a>보안 그룹 만들기  
  
1.  에 **시작** 화면에서 입력**dsa.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  왼쪽된 창에서 확장 **corp.contoso.com**, 클릭 **사용자**를 마우스 오른쪽 단추로 클릭 **사용자**, 가리킨 **새**, 클릭하고**그룹**합니다.  
  
3.  에 **새 개체-그룹** 대화 상자의 **그룹 이름**를 입력 **Win7_Clients_Site1**합니다.  
  
4.  아래에서 **그룹 범위**, 클릭 **Global**, 아래에서 **그룹 종류**, 클릭 **보안**, 를 클릭 하 고 **확인**합니다.  
  
5.  두 번 클릭 합니다 **Win7_Clients_Site1** 보안 그룹 및를 **Win7_Clients_Site1 속성** 대화 상자에서 클릭는 **멤버** 탭 합니다.  
  
6.  **구성원** 탭에서 **추가**를 클릭합니다.  
  
7.  에 **사용자 선택, 연락처, 컴퓨터 또는 서비스 계정** 대화 상자, 클릭 **개체 유형**합니다. 에 **개체 유형** 대화 상자에서 **컴퓨터**를 클릭 하 고 **확인**합니다.  
  
8.  **선택할 개체 이름을 입력**, 형식 **client2**를 클릭 하 고 **확인**, 한 후의 **Win7_Clients_Site1 속성** 대화 상자 **확인**합니다.  
  
9. 에 **Active Directory Users and Computers** 콘솔 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **사용자**를 가리킵니다 **새로 만들기**를 클릭 하 고 **그룹** .  
  
10. 에 **새 개체-그룹** 대화 상자의 **그룹 이름**를 입력 **Win7_Clients_Site2**합니다.  
  
11. 아래에서 **그룹 범위**, 클릭 **Global**, 아래에서 **그룹 종류**, 클릭 **보안**, 를 클릭 하 고 **확인**합니다.  
  
12. **Active Directory 사용자 및 컴퓨터** 콘솔을 닫습니다.  
  
## <a name="to-add-a-new-ad-ds-site"></a>새 AD DS 사이트를 추가 하려면  
  
1.  에 **시작** 화면에서 입력**dssite.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  Active Directory 사이트 및 서비스 콘솔의 콘솔 트리에서 마우스 오른쪽 단추로 클릭 **사이트**, 를 클릭 하 고 **새 사이트**합니다.  
  
3.  에 **새 개체-사이트** 대화 상자의 합니다 **이름** 상자에 입력 **두 번째-사이트**합니다.  
  
4.  목록 상자에서 클릭 **DEFAULTIPSITELINK**를 클릭 하 고 **확인** 두 번입니다.  
  
5.  콘솔 트리에서 확장 **사이트**, 를 마우스 오른쪽 단추로 클릭 **서브넷**, 를 클릭 하 고 **새 서브넷**합니다.  
  
6.  에 **새 개체-서브넷** 대화 상자의 **접두사**, 형식 **10.0.0.0/24**를 **이 접두사에 대 한 사이트 개체를 선택** 목록에서 클릭 **기본 첫 번째-사이트 이름**를 클릭 하 고 **확인**합니다.  
  
7.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **서브넷**를 클릭 하 고 **새 서브넷**합니다.  
  
8.  에 **새 개체-서브넷** 대화 상자의 **접두사**, 유형 **2001:db8:1:: / 64**를 **이 접두사에 대 한 사이트 개체를 선택** 목록 클릭 **기본 첫 번째-사이트 이름**를 클릭 하 고 **확인**합니다.  
  
9. 콘솔 트리에서 마우스 오른쪽 단추로 클릭 **서브넷**를 클릭 하 고 **새 서브넷**합니다.  
  
10. 에 **새 개체-서브넷** 대화 상자의 **접두사**, 형식 **10.2.0.0/24**를 **이 접두사에 대 한 사이트 개체를 선택** 목록에서 클릭 **두 번째-사이트**를 클릭 하 고 **확인**합니다.  
  
11. 콘솔 트리에서 마우스 오른쪽 단추로 클릭 **서브넷**를 클릭 하 고 **새 서브넷**합니다.  
  
12. 에 **새 개체-서브넷** 대화 상자의 **접두사**, 유형 **2001:db8:2:: / 64**를 **이 접두사에 대 한 사이트 개체를 선택** 목록 클릭 **두 번째-사이트**를 클릭 하 고 **확인**합니다.  
  
13. Active Directory 사이트 및 서비스를 닫습니다.  
  


