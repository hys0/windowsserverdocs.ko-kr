---
title: "자격 증명 보호 및 관리"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e457229c-0126-40fe-948c-101c943e1b57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 16cc1f2260bf0552da6902dc3e97de65d29c7931
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="credentials-protection-and-management"></a>자격 증명 보호 및 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목 기능과 자격 증명 도용의 줄이기 위해 Windows Server 2012 R2 및 Windows 8.1 도메인 인증 컨트롤 및 보호 자격 증명에 도입 하는 방법에 설명 합니다.

## <a name="BKMK_CredentialsProtectionManagement"></a>
### <a name="restricted-admin-mode-for-remote-desktop-connection"></a>원격 데스크톱 연결에 대 한 제한 관리자 모드
제한 된 관리자 모드 대화형 자격 증명 서버에 전송 하지 않고 호스트 원격 서버에 로그온 하는 방법을 제공 합니다. 이렇게 하면 더라도 서버 초기 연결 과정 수집 되 고에서 자격 증명을 않습니다.

원격 데스크톱 클라이언트가이 모드를 사용 하 여 관리자 자격 증명을 자격 증명을 보내지 않고이 모드를 지원 되는 호스트에 로그온 대화형 하려고 합니다. 호스트 확인 사용자 계정에 연결 관리자 권한이 한 제한 된 관리자 모드가 지원, 연결 성공 합니다. 그렇지 않은 경우 연결이 실패 합니다. 제한 관리자 모드가 지점 보내기 일반 텍스트 또는 다시 사용할 수 있는 기타 형태의 자격 증명을 원격 컴퓨터에서 하지 않습니다.

### <a name="lsa-protection"></a>LSA 보호
LSA 로컬 보안 기관을 (), 있는 로컬 보안 기관을 서비스 LSASS (보안) 프로세스 내에서 서버 지역 및 원격 기호 기능에 대 한 사용자의 유효성을 검사 하 고 로컬 보안 정책이 적용 됩니다. Windows 8.1 운영 체제 LSA 코드 삽입 비 암호로 보호 된 프로세스를 통해 방지에 대 한 추가 보호 기능을 제공 합니다. 더 나은 보안 LSA 저장 하 고 관리 자격 증명을 제공 합니다. 이 보호 된 프로세스 LSA에 대 한 Windows 8.1 구성할 수 있습니다 하지만 Windows RT 8.1에서에서 기본적으로 켜져 설정과 변경할 수 없습니다.

구성 LSA 보호에 대 한 정보를 참조 하세요. [추가 LSA 보호 구성](configuring-additional-lsa-protection.md)합니다.

### <a name="protected-users-security-group"></a>사용자가 보안 그룹 보호
이 새 도메인 전 세계 그룹 트리거하 장치 및 Windows Server 2012 R2 및 Windows 8.1 실행 호스트 컴퓨터에서 새 구성할 수 없는 보호 합니다. Users 보호 그룹 도메인 컨트롤러 및 Windows Server 2012 R2 도메인에 있는 도메인에 대 한 추가 보호 수 있습니다. 이렇게 하면 줄어듭니다 유형의 자격 증명을 사용할 수 있는 사용자가 로그인 네트워크에서 컴퓨터에 아닌 손상 컴퓨터에서 합니다.

보호 사용자 그룹의 회원은 제한 된 인증 다음과 같은 방법으로 추가 합니다.

-   보호 사용자 그룹의 회원 Kerberos 프로토콜을 사용 하 여에 로그인 할 수 있습니다. 계정을 사용 하 여 NTLM, 요약 인증 또는 CredSSP 인증할 수 없습니다. .1 Windows 8을 실행 하는 디바이스에서 암호 캐시 되지 않으므로 하므로 이러한 보안 지원 공급자 (규칙이) 중 하나를 사용 하는 장치는 계정을 보호 사용자 그룹의 회원 때 도메인에 인증 되지 않습니다.

-   Kerberos 프로토콜 사전 인증 과정에서 DES 또는 r c 4 암호화 약한 종류를 사용 하지 않습니다. 즉, 도메인 최소한 AES 암호 제품군을 지원 하도록 구성 되어야 합니다.

-   사용자의 계정을 Kerberos 제약 없이 또는 제한 된 위임 수 없는 위임 합니다. 즉, 사용자가 보호 사용자 그룹의 회원 경우 다른 시스템을 이전 연결 되지 않을 수 있습니다.

-   4 시간이 Kerberos 티켓 부여 티켓 (Tgt) 수명 기본 설정을 인증 정책 및 사일로 액세스를 통해의 Active Directory 관리 센터 (ADAC)를 사용 하 여 구성할 수 있습니다. 이 4 시간 경과 때 사용자가 인증 해야 다시 의미 합니다.

> [!WARNING]
> 서비스 및 컴퓨터에 대 한 계정을 보호 사용자 그룹의 회원 수 없습니다. 이 그룹 암호 또는 인증서 항상 호스트에서 사용할 수 없기 때문 없이 로컬 보호를 제공 합니다. Authentication will fail with the error "the user name or password is incorrect" for any service or computer that is added to the Protected Users group.

이 그룹에 대 한 자세한 내용은 참조 [사용자가 보안 그룹 보호](protected-users-security-group.md)합니다.

### <a name="authentication-policy-and-authentication-policy-silos"></a>인증 정책 및 인증 정책 사일로
숲 기반 Active Directory 정책 도입 하 고 Windows Server 2012 R2 도메인 기능 수준으로 도메인에 있는 계정에 적용 될 수 있습니다. 이러한 인증 정책을 사용자에 로그인 하는 데 사용할 수 있는 호스트 제어할 수 있습니다. 관리자 계정 인증에 대 한 액세스를 제어 조건 적용할 수 있는 및 사용자를 보호 보안 그룹와 함께에서 작동 합니다. 이러한 인증 정책 관련된 계정을 제한 네트워크 범위를 분리 합니다.

새 Active Directory 개체 클래스 인증 정책, Windows Server 2012 R2 도메인 기능 수준으로 도메인에 있는 계정 클래스 인증 구성 적용할 수 있습니다. Kerberos AS 또는 TGS 중 인증 정책이 적용 되어 exchange 합니다. Active Directory 계정 클래스는 다음과 같습니다.

-   사용자

-   컴퓨터

-   관리 서비스 계정

-   그룹 관리 서비스 계정

자세한 내용은 참조 [인증 정책 및 인증 정책 사일로](authentication-policies-and-authentication-policy-silos.md)합니다.

자세한 내용은 구성 계정을 보호 하는 방법을 참조 [계정 보호 구성 하는 방법을](how-to-configure-protected-accounts.md)합니다.

## <a name="see-also"></a>참조 하십시오
For more information about the LSA and the LSASS, see the [Windows Logon and Authentication Technical Overview](https://technet.microsoft.com/library/dn169029(v=ws.10).aspx).



