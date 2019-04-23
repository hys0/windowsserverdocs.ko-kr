---
title: Azure AD를 사용하여 VPN 인증에 대한 루트 인증서 만들기
description: Azure AD는 VPN 연결에 대 한 Azure AD에 인증할 때 Windows 10 클라이언트에 발급 된 인증서를 서명 하는 VPN 인증서를 사용 합니다. 기본으로 표시 된 인증서가 Azure AD를 사용 하는 발급자입니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851564"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>7.2단계. Azure AD를 사용 하 여 조건부 액세스를 VPN 인증에 대 한 루트 인증서 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**이전:** 7.1단계. 인증서 해지 목록 (CRL) 검사를 무시 하도록 EAP-TLS 구성](vpn-config-eap-tls-to-ignore-crl-checking.md)<br>
&#187;[ **다음:** 7.3단계. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md)

이 단계에서는 자동으로 테 넌 트에서 VPN 서버를 호출 하는 클라우드 앱을 만드는 Azure AD와 VPN 인증에 대 한 조건부 액세스 루트 인증서를 구성 합니다. VPN 연결에 대 한 조건부 액세스를 구성 하려면:

1. (둘 이상의 인증서를 만들 수)는 Azure 포털에서 VPN 인증서를 만듭니다.
2. VPN 인증서를 다운로드 합니다.
2. VPN 및 NPS 서버에 인증서를 배포 합니다.

사용자가 VPN 연결을 시도 하는 경우 VPN 클라이언트는 Windows 10 클라이언트에서 웹 계정 관리자 (WAM)를 호출 합니다. WAM은 VPN 서버 클라우드 앱을 호출 합니다. 조건 및 조건부 액세스 정책에서 컨트롤을 만족할 경우 Azure AD는 WAM에 단기 (1 시간) 인증서의 형태로 토큰을 발급 합니다. WAM 사용자의 인증서 저장소에 인증서를 배치 및 VPN 클라이언트에 컨트롤을 전달 합니다.  

그런 다음 VPN 클라이언트 자격 증명 유효성 검사에 대 한 vpn 인증서 문제를 Azure AD에서 보냅니다.  로 표시 된 인증서를 사용 하는 azure AD **주** 를 발급자로 VPN 연결 블레이드에서 합니다. 

Azure portal에서 두 가지 인증서 하나의 인증서가 만료 될 때 전환을 관리할를 만들 수 있습니다. 인증서를 만들 때 연결에 대 한 인증서를 서명 하는 인증 시 사용 되는 기본 인증서 인지 여부를 선택할 수 있습니다.

**절차:**

1. 에 로그인 하 여 [Azure portal](https://portal.azure.com) 전역 관리자입니다.

2. 왼쪽된 메뉴에서 클릭 **Azure Active Directory**합니다. 

    ![Azure Active Directory 선택](../../media/Always-On-Vpn/01.png)

3. 에 **Azure Active Directory** 페이지를 **관리** 섹션에서 클릭 **조건부 액세스**합니다.

    ![조건부 액세스 선택](../../media/Always-On-Vpn/02.png)

4. 에 **조건부 액세스** 페이지를 **관리** 섹션에서 클릭 **VPN 연결 (미리 보기)** 합니다.

    ![VPN 연결을 선택 합니다.](../../media/Always-On-Vpn/03.png)

5. 에 **VPN 연결** 페이지에서 클릭 **새 인증서**합니다.

    ![새 인증서를 선택 합니다.](../../media/Always-On-Vpn/04.png)

6. 에 **새로 만들기** 페이지에서 다음 단계를 수행 합니다.

    ![기간 및 기본 선택](../../media/Always-On-Vpn/05.png)

    a. 에 대 한 **기간 선택**, 1 또는 2 년을 선택 합니다. 인증서가 만료 되려고 할 때 전환을 관리할 수 있는 최대 2 개의 인증서를 추가할 수 있습니다. (사용 된 계정이 인증 하는 동안 연결을 위한 인증서 서명에) 주 어떤 것을 선택할 수 있습니다.

    b. 에 대 한 **주**를 선택 **예**합니다.

    다. **만들기**를 클릭합니다.

## <a name="next-step"></a>다음 단계
[7.3 단계입니다. 조건부 액세스 정책을 구성](vpn-config-conditional-access-policy.md): 이 단계에서는 VPN 연결에 대 한 조건부 액세스 정책을 구성할 수 있습니다. 

---