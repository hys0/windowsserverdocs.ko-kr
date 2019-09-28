---
title: 조건부 액세스 정책 구성
description: 루트 인증서를 만든 후 ' VPN 연결 '은 고객의 테 넌 트에서 ' VPN 서버 ' 클라우드 응용 프로그램 만들기를 트리거합니다.
services: active-directory
ms.prod: windows-server
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
ms.openlocfilehash: 22983c085f2b9d9e7e16810e25c6fa50111f9fa6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404346"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>7\.3단계. 조건부 액세스 정책 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**선행** 7.2단계. Azure AD를 사용하여 VPN 인증에 대한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)
- [**그런** 7.4단계. 온-프레미스 AD에 조건부 액세스 루트 인증서 배포 @ no__t-0

이 단계에서는 VPN 연결에 대 한 조건부 액세스 정책을 구성 합니다. ' VPN 연결 ' 블레이드에서 첫 번째 루트 인증서가 생성 되 면 테 넌 트에서 ' VPN 서버 ' 클라우드 응용 프로그램을 자동으로 만듭니다.

VPN 사용자 그룹에 할당 된 조건부 액세스 정책을 만들고 **클라우드 앱** 을 **vpn 서버로**범위를 지정 합니다.

- **Users**: VPN 사용자
- **클라우드 앱**: VPN 서버
- **Grant (access control)** : ' Multi-factor authentication 필요 '가 있습니다. 원하는 경우 다른 컨트롤을 사용할 수 있습니다.

**여기서** 이 단계에서는 가장 기본적인 조건부 액세스 정책 만들기에 대해 설명 합니다.  원하는 경우 추가 조건 및 컨트롤을 사용할 수 있습니다.


1. **조건부 액세스** 페이지의 위쪽에 있는 도구 모음에서 **추가**를 선택 합니다.

    ![조건부 액세스 페이지에서 추가를 선택 합니다.](../../media/Always-On-Vpn/07.png)

2. **새로 만들기** 페이지의 **이름** 상자에 정책의 이름을 입력 합니다. 예를 들어 **VPN 정책을**입력 합니다.

    ![조건부 액세스 페이지에서 정책에 대 한 이름 추가](../../media/Always-On-Vpn/08.png)

3. **할당** 섹션에서 **사용자 및 그룹**을 선택 합니다.

    ![사용자 및 그룹 선택](../../media/Always-On-Vpn/09.png)

4. **사용자 및 그룹** 페이지에서 다음 단계를 수행 합니다.

    ![테스트 사용자 선택](../../media/Always-On-Vpn/10.png)

    a. **사용자 및 그룹 선택**을 선택 합니다.

    b. **선택**을 선택 합니다.

    c. **선택** 페이지에서 **VPN 사용자** 그룹을 선택한 다음 **선택**을 선택 합니다.

    d. **사용자 및 그룹** 페이지에서 **완료**를 선택 합니다.

5. **새로 만들기** 페이지에서 다음 단계를 수행 합니다.

    ![클라우드 앱 선택](../../media/Always-On-Vpn/11.png)

    a. **할당** 섹션에서 **클라우드 앱**을 선택 합니다.

    b. **클라우드 앱** 페이지에서 **앱 선택**을 선택 합니다.

    d. **VPN 서버**를 선택 합니다.

6.  **새** 페이지에서 **권한 부여** 페이지를 열려면 **제어** 섹션에서 **부여**를 선택 합니다.

    ![권한 부여 선택](../../media/Always-On-Vpn/13.png)

7.  **허용** 페이지에서 다음 단계를 수행 합니다.

    ![Multi-factor authentication 필요를 선택 합니다.](../../media/Always-On-Vpn/14.png)

    a. **Multi-factor Authentication 필요**를 선택 합니다.

    b. **선택**을 선택 합니다.

8.  **새로 만들기** 페이지의 **정책 사용**에서 **켜기**를 선택 합니다.

    ![정책 사용](../../media/Always-On-Vpn/15.png)

9.  **새로** 만들기 페이지에서 **만들기**를 선택 합니다.


## <a name="next-steps"></a>다음 단계
[7.4단계. 온-프레미스 AD @ no__t에 조건부 액세스 루트 인증서 배포-0: 이 단계에서는 조건부 액세스 루트 인증서를 온-프레미스 AD에 대 한 VPN 인증에 대 한 신뢰할 수 있는 루트 인증서로 배포 합니다.
