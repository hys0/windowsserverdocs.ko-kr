---
title: 조건부 액세스 정책 구성
description: 루트 인증서를 만든 후 'VPN 연결' 고객의 테 넌 트에서 ' VPN 서버 ' 클라우드 응용 프로그램의 생성을 트리거합니다.
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 8c00855c50de79efa1b48c7b8762e1b679db4a87
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870284"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>7.3단계. 조건부 액세스 정책 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**이전:** 7.2단계. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)<br>
&#187;[ **다음:** 7.4단계. 온-프레미스에 조건부 액세스 루트 인증서를 배포할 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

이 단계에서는 VPN 연결에 대 한 조건부 액세스 정책을 구성할 수 있습니다. 'VPN 연결' 블레이드에서는 첫 번째 루트 인증서를 만들 때 테 넌 트에서 ' VPN 서버 ' 클라우드 응용 프로그램을 자동으로 만듭니다. 

VPN 사용자 그룹 및 범위에 할당 되는 조건부 액세스 정책 만들기는 **클라우드 앱** 하 **VPN 서버**: 

- **Users**: VPN 사용자
- **클라우드 앱**: VPN 서버
- **(액세스 제어) 권한 부여**: ' Multi-factor authentication이 필요 ' 합니다. 원하는 경우 다른 컨트롤을 사용할 수 있습니다.

**절차:** 이 단계에서는 가장 기본적인 조건부 액세스 정책 만들기를 설명합니다.  원하는 경우 추가 조건 및 컨트롤을 사용할 수 있습니다.


1. 에 **조건부 액세스** 페이지에서 맨 위의 도구 모음에서 클릭 **추가**합니다.

    ![조건부 액세스 페이지에서 추가 선택](../../media/Always-On-Vpn/07.png)

2. 에 **새로 만들기** 페이지의 **이름** 상자에 정책의 이름을 입력 합니다. 예를 들어 입력 **VPN 정책**합니다.

    ![조건부 액세스 페이지에서 정책에 대 한 이름 추가](../../media/Always-On-Vpn/08.png)

3. 에 **할당** 섹션에서 클릭 **사용자 및 그룹**합니다.

    ![사용자 및 그룹 선택](../../media/Always-On-Vpn/09.png)

4. 에 **사용자 및 그룹** 페이지에서 다음 단계를 수행 합니다.

    ![테스트 사용자 선택](../../media/Always-On-Vpn/10.png)

    a. 클릭 **사용자 및 그룹 선택**합니다.

    b. 클릭 **선택**합니다.

    다. 에 **선택** 페이지를 선택 합니다 **VPN 사용자** 그룹을 마우스 클릭 **선택**합니다.

    d. 에 **사용자 및 그룹** 페이지에서 클릭 **수행**합니다.

5. 에 **새로 만들기** 페이지에서 다음 단계를 수행 합니다.

    ![클라우드 앱 선택](../../media/Always-On-Vpn/11.png)

    a. 에 **할당** 섹션에서 클릭 **클라우드 앱**합니다.

    b. 에 **클라우드 앱** 페이지에서 클릭 **앱 선택**합니다.

    d. 선택 **VPN 서버**합니다.

13. 에 **새로 만들기** 를 열려면 페이지는 **권한 부여** 페이지를 **컨트롤** 섹션에서 **부여**합니다.

    ![권한 부여 선택](../../media/Always-On-Vpn/13.png)

14. 에 **부여** 페이지에서 다음 단계를 수행 합니다.

    ![다단계 인증 필요 선택](../../media/Always-On-Vpn/14.png)

    a. 선택 **multi-factor authentication 요구**합니다.

    b. 클릭 **선택**합니다.

15. 에 **새로 만들기** 페이지의 **정책을 사용 하도록 설정**, 클릭 **에서**합니다.

    ![정책을 사용 하도록 설정](../../media/Always-On-Vpn/15.png)

16. 에 **새로 만들기** 페이지에서 클릭 **만들기**합니다.


## <a name="next-step"></a>다음 단계
[7.4 단계입니다. 온-프레미스에 조건부 액세스 루트 인증서를 배포할 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md): 이 단계에서는 조건부 액세스 루트 인증서와 VPN 인증에 대 한 신뢰할 수 있는 루트 인증서에 배포한 온-프레미스 AD입니다.

---