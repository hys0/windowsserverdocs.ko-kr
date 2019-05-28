---
ms.assetid: e33673ff-ea1c-4476-a549-3bf5899a47dd
title: 페더레이션 서비스 역할 서비스 설치
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 80a6cb2bc8e6f0fdb1a777a42f5d245f98ac3dee
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192092"
---
# <a name="install-the-federation-service-role-service"></a>페더레이션 서비스 역할 서비스 설치

Active Directory Federation Services의 페더레이션 서비스 역할 서비스를 설치할 준비가 이제을 필수 구성 요소 응용 프로그램 및 인증서를 사용 하 여 컴퓨터를 올바르게 구성한 \(AD FS\)합니다. 컴퓨터에서 페더레이션 서비스를 설치할 때 해당 컴퓨터에 페더레이션 서버가 됩니다.  
  
> [!NOTE]  
> 페더레이션 웹 단일 항목에 대 한\-Sign\-온 \(SSO\) 디자인, 계정 파트너 조직에서 하나 이상의 페더레이션 서버 및 리소스 파트너 조직에서 하나 이상의 페더레이션 서버를 사용 하도록 해야 . 자세한 내용은 [Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx)를 참조하세요.  
  
첫 번째 페더레이션 서버 될 컴퓨터 또는 기존 페더레이션 서버 팜의 페더레이션 서버 될 컴퓨터의 AD FS 페더레이션 서비스 역할 서비스를 설치 하려면 다음 절차를 사용할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
확인 하는 SSL 인증서 개인 키를 사용 하 여 이미 설치 되어 있지 않거나 로컬 인증서 저장소로 가져올 \(개인 저장소\) 이 절차를 시작 하기 전에 합니다. 토큰을 사용 하려는 경우\-인증 기관에서 발급 한 인증서 서명 \(CA\), 확인 토큰\-서명 인증서 개인 키를 사용 하 여 이미 설치 되어 있지 않거나 가져올 로컬 인증서 저장소 \(개인 저장소\) 이 절차를 시작 하기 전에 합니다. 대신 자체를 만들 수 있습니다\-토큰 서명\-이 절차에 설명 된 대로 역할 추가 마법사를 사용 하 여 인증서를 서명 합니다. 토큰에 대 한 자세한 내용은\-서명 인증서를 참조 하세요 [페더레이션 서버에 대 한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)합니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/? LinkId\=83477\)합니다.   
  
#### <a name="to-install-the-federation-service-role-service"></a>페더레이션 서비스 역할 서비스를 설치하려면  
  
1.  에 **시작** 화면에서 입력**서버 관리자**, 한 다음 ENTER를 누릅니다.  
  
2.  클릭 **관리**를 클릭 하 고 **역할 및 기능 추가** 추가 역할 및 기능 마법사를 시작 합니다.  
  
3.  **시작하기 전** 페이지에서 **다음**을 클릭합니다.  
  
4.  에 **설치 유형 선택** 페이지에서 **역할\-기반 또는 기능\-기반 설치**를 클릭 하 고 **다음**합니다.  
  
5.  에 **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**, 대상 컴퓨터가 강조 표시를 클릭 한 다음 확인 **다음**합니다.  
  
6.  에 **서버 역할 선택** 페이지에서 **Active Directory Federation Services**, 다음을 클릭 하 고 있습니다.  
  
    > [!NOTE]  
    > 추가.NET Framework 또는 Windows Process Activation Service 기능을 설치 하 라는 메시지가 나타나면 클릭 **기능 추가** 설치 합니다.  
  
7.  에 **기능 선택** 페이지에서 확인 하는 기능을 설정 하 고 클릭 **다음**합니다.  
  
8.  에 **Active Directory Federation Service \(AD FS\)**  페이지에서 클릭 **다음**합니다.  
  
9. 에 **역할 서비스 선택** 페이지에서 선택 합니다 **페더레이션 서비스** 확인란을 선택한 다음 클릭 **다음**합니다.  
  
10. 에 **웹 서버 역할 \(IIS\)**  페이지에서 클릭 **다음**합니다.  
  
11. **역할 서비스 선택** 페이지에서 **다음**을 클릭합니다.  
  
12. **설치 선택 확인** 페이지에서 정보를 확인한 후 **필요한 경우 자동으로 대상 서버 다시 시작** 확인란을 선택하고 **설치**를 클릭합니다.  
  
13. **설치 진행률** 페이지에서 모든 항목이 올바르게 설치되었는지 확인하고 **닫기**를 클릭합니다.  
  

