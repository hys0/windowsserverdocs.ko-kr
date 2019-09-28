---
ms.assetid: e33673ff-ea1c-4476-a549-3bf5899a47dd
title: 페더레이션 서비스 역할 서비스 설치
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 73c564e1c1117b229f759ca114b18a2d4c8002fa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408381"
---
# <a name="install-the-federation-service-role-service"></a>페더레이션 서비스 역할 서비스 설치

이제 필수 구성 요소 응용 프로그램 및 인증서를 사용 하 여 컴퓨터를 올바르게 구성 했으므로 Active Directory Federation Services \(AD FS @ no__t-1의 페더레이션 서비스 역할 서비스를 설치할 준비가 되었습니다. 컴퓨터에 페더레이션 서비스을 설치 하면 해당 컴퓨터가 페더레이션 서버가 됩니다.  
  
> [!NOTE]  
> 페더레이션된 웹 Single @ no__t-0Sign @ no__t On \(SSO @ no__t 디자인의 경우 계정 파트너 조직에 하나 이상의 페더레이션 서버가 있어야 하 고 리소스 파트너 조직의 페더레이션 서버는 하나 이상 있어야 합니다. 자세한 내용은 [Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx)를 참조하세요.  
  
다음 절차를 사용 하 여 첫 번째 페더레이션 서버가 될 컴퓨터 또는 기존 페더레이션 서버 팜에 대 한 페더레이션 서버가 될 컴퓨터에 AD FS의 페더레이션 서비스 역할 서비스를 설치할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 절차를 시작 하기 전에 개인 키가 있는 SSL 인증서를 로컬 인증서 저장소 \(Personal store @ no__t-1에 이미 설치 하거나 가져왔는지 확인 합니다. No__t 인증 @no__t 기관에서 발급 한 토큰 @-0signing 인증서를 사용 하는 경우-1CA @ no__t-2를 사용 하는 경우 개인 키가 포함 된 token @ no__t 서명 인증서가 이미 설치 되어 있거나 로컬 인증서 저장소로 가져왔는지 확인 합니다. 이 절차를 시작 하기 전에 \(Personal store @ no__t-5입니다. 또는이 절차에 설명 된 대로 역할 추가 마법사를 사용 하 여 자체 @ no__t-0으로 서명 된 토큰 @ no__t 서명 인증서를 만들 수 있습니다. 토큰 @ no__t-0signing 인증서에 대 한 자세한 내용은 [페더레이션 서버에 대 한 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)을 참조 하세요.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477) \(에서 적절 한 계정 및 그룹 구성원 자격 사용에 대 한 자세한 내용은\/http\/: go.microsoft.com fwlink?를 참조 하세요.\/\/ LinkId\=83477\).   
  
#### <a name="to-install-the-federation-service-role-service"></a>페더레이션 서비스 역할 서비스를 설치하려면  
  
1.  **시작** 화면에서**서버 관리자**를 입력 한 다음 enter 키를 누릅니다.  
  
2.  **관리**, **역할 및 기능 추가** 를 차례로 클릭 하 여 역할 및 기능 추가 마법사를 시작 합니다.  
  
3.  **시작하기 전** 페이지에서 **다음**을 클릭합니다.  
  
4.  **설치 유형 선택** 페이지에서 **역할 @ no__t-2Based 또는 기능 @ no__t-3based 설치**를 클릭 하 고 **다음**을 클릭 합니다.  
  
5.  **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭 하 고 대상 컴퓨터가 강조 표시 되었는지 확인 한 후 **다음**을 클릭 합니다.  
  
6.  **서버 역할 선택** 페이지에서 **Active Directory Federation Services**를 클릭 한 후 다음을 클릭 합니다.  
  
    > [!NOTE]  
    > 추가 .NET Framework 또는 Windows Process Activation Service 기능을 설치 하 라는 메시지가 표시 되 면 **기능 추가** 를 클릭 하 여 설치 합니다.  
  
7.  **기능 선택** 페이지에서 기능이 설정 되어 있는지 확인 하 고 **다음**을 클릭 합니다.  
  
8.  **Active Directory 페더레이션 서비스 \(AD FS @ no__t-2** 페이지에서 **다음**을 클릭 합니다.  
  
9. **역할 서비스 선택** 페이지에서 **페더레이션 서비스** 확인란을 선택 하 고 **다음**을 클릭 합니다.  
  
10. **웹 서버 역할 \(IIS @ no__t-2** 페이지에서 **다음**을 클릭 합니다.  
  
11. **역할 서비스 선택** 페이지에서 **다음**을 클릭합니다.  
  
12. **설치 선택 확인** 페이지에서 정보를 확인한 후 **필요한 경우 자동으로 대상 서버 다시 시작** 확인란을 선택하고 **설치**를 클릭합니다.  
  
13. **설치 진행률** 페이지에서 모든 항목이 올바르게 설치되었는지 확인하고 **닫기**를 클릭합니다.  
  

