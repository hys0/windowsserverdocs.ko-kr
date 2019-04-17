---
title: Azure AD를 사용하여 VPN 인증에 대한 루트 인증서 만들기
description: Azure AD는 VPN 연결에 대 한 Azure AD를 인증할 때 Windows 10 클라이언트에 발급 된 인증서를 서명 하려면 VPN 인증서를 사용 합니다. 기본로 표시 된 인증서는 Azure AD를 사용 하는 발급자 합니다.
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
ms.openlocfilehash: 14ef17ab403cc4e7c9891f4ede48e41c25e8522d
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067290"
---
# 7.2단계. Azure AD를 사용 하 여 조건부 액세스를 VPN 인증에 대 한 루트 인증서 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **이전:** 7.1 단계입니다. EAP-TLS 인증서 해지 목록 (CRL) 검사 무시 하도록 구성](vpn-config-eap-tls-to-ignore-crl-checking.md)<br>
& #187; [ **다음:** 7.3 단계입니다. 조건부 액세스 정책을 구성](vpn-config-conditional-access-policy.md)

이 단계에서 Azure ad 테 넌 트에 VPN 서버를 호출 하는 클라우드 응용 프로그램을 자동으로 생성 하는 VPN 인증에 대 한 조건부 액세스 루트 인증서를 구성 합니다. VPN 연결에 대 한 조건부 액세스를 구성 하려면 해야 합니다.

1. (인증서를 여러 개 만들 수 있습니다) Azure portal에서 VPN 인증서를 만듭니다.
2. VPN 인증서를 다운로드 합니다.
2. VPN 및 NPS 서버에 인증서를 배포 합니다.

사용자가 VPN 연결을 시도 하는 경우 VPN 클라이언트가 Windows 10 클라이언트의 웹 계정 관리자 (WAM)에 대 한 호출을 만듭니다. WAM은 VPN 서버 클라우드 응용 프로그램에 대 한 호출을 만듭니다. 조건 및 조건부 액세스 정책에서 컨트롤 만족할 경우 Azure AD는 WAM를 일시적인 (1 시간) 인증서의 형태로 토큰을 발급 합니다. WAM는 사용자의 인증서 저장소에 인증서를 배치 하 고 VPN 클라이언트에 컨트롤을 전달 합니다.  

그런 다음 자격 증명 유효성 검사에 대 한 vpn VPN 클라이언트가 Azure AD에서이 인증서 문제를 보냅니다.Azure AD는**기본**으로 표시 된 인증서를 사용 하 여발급자도 VPN 연결 블레이드에서 합니다. 

Azure 포털에서 하나의 인증서 만료 되려고 할 때 전환을 관리 하는 두 개의 인증서를 만듭니다. 인증서를 만들 때 연결에 대 한 인증서를 서명 하는 인증 하는 동안 사용 되는 기본 인증서 인지 여부를 선택할 수 있습니다.

**절차:**

1. 전역 관리자 권한으로 [Azure 포털](https://portal.azure.com) 에 로그인 합니다.

2. 왼쪽된 메뉴에서 **Azure Active Directory**를 클릭 합니다. 

    ![Azure Active Directory를 선택 합니다.](../../media/Always-On-Vpn/01.png)

3. **Azure Active Directory** 페이지 **관리** 섹션의 **조건부 액세스**를 클릭 합니다.

    ![조건부 액세스를 선택 합니다.](../../media/Always-On-Vpn/02.png)

4. **관리** 섹션의 **조건부 액세스** 페이지에서 **VPN 연결 (미리 보기)를**클릭 합니다.

    ![VPN 연결을 선택 합니다.](../../media/Always-On-Vpn/03.png)

5. **VPN 연결** 페이지에서 **새 인증서**를 클릭 합니다.

    ![새 인증서를 선택 합니다.](../../media/Always-On-Vpn/04.png)

6. **새** 페이지에서 다음 단계를 수행 합니다.

    ![기간 및 기본 선택](../../media/Always-On-Vpn/05.png)

    a. **선택한 기간을**1 또는 2 년 선택 합니다. 인증서 만료 되려고 할 때 전환을 관리 하는 최대 2 개의 인증서를 추가할 수 있습니다. 기본 (한 인증 하는 동안 연결에 대 한 인증서를 서명 하는 데 사용)는 것을 선택할 수 있습니다.

    b. **기본**영역에 대 한 **예**를 선택 합니다.

    c. **만들기**를 클릭합니다.

## 다음 단계
[단계 7.3입니다. 조건부 액세스 정책을 구성](vpn-config-conditional-access-policy.md):이 단계에서 VPN 연결에 대 한 조건부 액세스 정책을 구성 합니다. 

---