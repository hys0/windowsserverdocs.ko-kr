---
title: 조건부 액세스 정책 구성
description: 루트 인증서를 만든 후 'VPN 연결' 고객의 테 넌 트에 ' VPN 서버 ' 클라우드 응용 프로그램의 생성을 트리거합니다.
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067297"
---
# 7.3단계. 조건부 액세스 정책 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **이전:** 7.2 단계입니다. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)<br>
& #187; [ **다음:** 7.4 단계입니다. 온-프레미스에 조건부 액세스 루트 인증서를 배포 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

이 단계에서 VPN 연결에 대 한 조건부 액세스 정책을 구성할 수 있습니다. 첫 번째 루트 인증서가 'VPN 연결' 블레이드에서 만들어지면 테 넌 트에 자동으로 ' VPN 서버 ' 클라우드 응용 프로그램을 만듭니다. 

VPN 사용자 그룹 및 범위 **VPN 서버**에 **클라우드 앱** 에 할당 되는 조건부 액세스 정책을 만듭니다. 

- **사용자**: 사용자가 VPN
- **클라우드 앱**: VPN 서버
- **권한 부여 (액세스 제어)**: '다단계 인증이 필요'. 원하는 경우 다른 컨트롤을 사용할 수 있습니다.

**절차:** 이 단계에서는 가장 기본적인 조건부 액세스 정책 만들기를 설명합니다.원한다 면 추가 조건 및 컨트롤을 사용할 수 있습니다.


1. **조건부 액세스** 페이지 맨 위에 도구 모음에서 **추가**클릭 합니다.

    ![조건부 액세스 페이지에서 추가 선택](../../media/Always-On-Vpn/07.png)

2. **새** 페이지에서 **이름** 상자에 정책에 대 한 이름을 입력 합니다. 예를 들어 **VPN 정책을**입력 합니다.

    ![조건부 액세스 페이지에서 정책 이름을 추가합니다](../../media/Always-On-Vpn/08.png)

3. **할당** 섹션에서 **사용자 및 그룹을**클릭 합니다.

    ![사용자 및 그룹을 선택 합니다.](../../media/Always-On-Vpn/09.png)

4. **사용자 및 그룹** 페이지에서 다음 단계를 수행 합니다.

    ![사용자 선택 테스트](../../media/Always-On-Vpn/10.png)

    a. **사용자 및 그룹 선택**을 클릭 합니다.

    b. **선택**을 클릭 합니다.

    c. **선택** 페이지에서 **VPN 사용자** 그룹을 선택 하 고 **선택**을 클릭 합니다.

    d. **사용자 및 그룹** 페이지에서 **완료**를 클릭 합니다.

5. **새** 페이지에서 다음 단계를 수행 합니다.

    ![클라우드 앱 선택](../../media/Always-On-Vpn/11.png)

    a. **할당** 섹션에서 **클라우드 앱**을 클릭 합니다.

    b. **클라우드 앱** 페이지에서 **선택 앱을**클릭 합니다.

    d. **VPN 서버**를 선택 합니다.

13. **새** 페이지 **컨트롤** 섹션에서 **부여** 페이지를 열려고 **권한 부여**를 클릭 합니다.

    ![권한 부여를 선택 합니다.](../../media/Always-On-Vpn/13.png)

14. **권한 부여** 페이지에서 다음 단계를 수행 합니다.

    ![다단계 인증을 요구 하는 선택](../../media/Always-On-Vpn/14.png)

    a. **다단계 인증**을 선택 합니다.

    b. **선택**을 클릭 합니다.

15. ** **새** 페이지에서 **정책을 사용**을 클릭 합니다.**

    ![정책을 사용 하도록 설정](../../media/Always-On-Vpn/15.png)

16. **새** 페이지 **만들기**를 클릭 합니다.


## 다음 단계
[단계 7.4입니다. 온-프레미스에 조건부 액세스 루트 인증서를 배포 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md):이 단계에서는 조건부 액세스 루트 인증서로 VPN 인증에 대 한 신뢰할 수 있는 루트 인증서를 배포 온-프레미스 AD 합니다.

---