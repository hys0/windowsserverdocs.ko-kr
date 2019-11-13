---
title: Azure AD를 사용하여 VPN 인증에 대한 루트 인증서 만들기
description: Azure AD는 vpn 연결을 위해 Azure AD에 인증할 때 VPN 인증서를 사용 하 여 Windows 10 클라이언트에 발급 된 인증서에 서명 합니다. 기본으로 표시 된 인증서는 Azure AD에서 사용 하는 발급자입니다.
services: active-directory
ms.prod: windows-server
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 41e98648ab963347f8370233c320f5e38b5d4d96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388012"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>7\.2단계. Azure AD를 사용 하 여 VPN 인증에 대 한 조건부 액세스 루트 인증서 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** 7.1 단계. EAP-TLS를 구성 하 여 CRL (인증서 해지 목록) 검사 무시](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**다음:** 7.3 단계. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md)

이 단계에서는 Azure AD를 사용 하 여 VPN 인증에 대 한 조건부 액세스 루트 인증서를 구성 하 여 테 넌 트에서 VPN 서버 라는 클라우드 앱을 자동으로 만듭니다. VPN 연결에 대 한 조건부 액세스를 구성 하려면 다음을 수행 해야 합니다.

1. Azure Portal에서 VPN 인증서를 만듭니다.
2. VPN 인증서를 다운로드 합니다.
3. VPN 및 NPS 서버에 인증서를 배포 합니다.

> [!IMPORTANT]
> Azure Portal에서 VPN 인증서가 만들어지면 Azure AD는 VPN 클라이언트에 수명이 짧은 인증서를 즉시 발급 하는 데 사용 하기 시작 합니다. Vpn 클라이언트의 자격 증명 유효성 검사 문제를 방지 하기 위해 vpn 인증서를 VPN 서버에 즉시 배포 하는 것이 중요 합니다.

사용자가 VPN 연결을 시도 하면 VPN 클라이언트는 Windows 10 클라이언트에서 웹 계정 관리자 (WAM)를 호출 합니다. WAM는 VPN 서버 클라우드 앱에 대 한 호출을 수행 합니다. 조건부 액세스 정책의 조건 및 제어가 충족 되 면 Azure AD는 WAM에 단기 (1 시간) 인증서 형식의 토큰을 발급 합니다. WAM 사용자의 인증서 저장소에 인증서를 배치 하 고 VPN 클라이언트에 제어를 전달 합니다.  

그러면 VPN 클라이언트가 자격 증명 유효성 검사를 위해 Azure AD에서 VPN으로 인증서 문제를 보냅니다.  

> [!NOTE]
> Azure AD는 VPN 연결 블레이드에서 가장 최근에 만든 인증서를 발급자로 사용 합니다.

**여기서**

1. 전역 관리자 권한으로 [Azure Portal](https://portal.azure.com) 에 로그인 합니다.
2. 왼쪽 메뉴에서 **Azure Active Directory**를 클릭 합니다.
3. **Azure Active Directory** 페이지의 **관리** 섹션에서 **조건부 액세스**를 클릭 합니다.
4. **조건부 액세스** 페이지의 **관리** 섹션에서 **VPN 연결 (미리 보기)** 을 클릭 합니다.
5. **VPN 연결** 페이지에서 **새 인증서**를 클릭 합니다.
6. **새로 만들기** 페이지에서 다음 단계를 수행 합니다. a. **기간 선택**에서 1, 2 또는 3 년을 선택 합니다.
   b. **만들기**를 선택합니다.

## <a name="next-steps"></a>다음 단계

[7.3 단계. 조건부 액세스 정책 구성](vpn-config-conditional-access-policy.md):이 단계에서는 VPN 연결에 대 한 조건부 액세스 정책을 구성 합니다.
