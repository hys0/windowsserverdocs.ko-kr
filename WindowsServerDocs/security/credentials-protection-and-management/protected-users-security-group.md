---
title: "사용자가 보안 그룹 보호"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f296
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: bd6b53c0febdfb2d344136097a9654c981405568
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="protected-users-security-group"></a>사용자가 보안 그룹 보호

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목의 Active Directory 보안 그룹 보호 사용자 및 작동 방식을 설명 합니다. 이 그룹 Windows Server 2012 R2 도메인 컨트롤러에 도입 되었습니다.

## <a name="BKMK_ProtectedUsers"></a>개요

이 보안 그룹 기업 내에서 자격 증명 노출 관리 하도록 전략의 일환으로 설계 되었습니다. 이 그룹의 회원은 자동으로 구성할 수 없는 보호 자신의 계정에 적용 되는 합니다. 보호 사용자 그룹의 회원은 제한적 미리 기본적으로 보안을 위한 것입니다. 이 보호 된 계정에 대 한 수정 하는 유일한 방법은 보안 그룹에서 계정을 제거 하는 것입니다.

> [!WARNING]
> 서비스 및 컴퓨터에 대 한 계정을 보호 사용자 그룹의 회원 안 됩니다. 이 그룹 암호 또는 인증서가 호스트에서 사용할 수 있는 항상 불완전 한 보호를 계속 제공 것 합니다. 오류 \"the 사용자 이름으로 인증 되지 것입니다 나 암호가 incorrect\" 서비스 또는 보호 사용자 그룹에 추가 하는 컴퓨터에 대 한 합니다.

이 도메인 관련, 글로벌 그룹 구성할 수 없는 보호 도메인에 있는 사용자가 나중에 대 한 또는 디바이스와 Windows Server 2012 r 2와.1 Windows 8을 실행 하는 호스트 컴퓨터에서 실행 중인 Windows Server 2012 r 2 주 도메인 컨트롤러 트리거됩니다. 이 경우 사용자가 로그인 이러한 보호도 컴퓨터에 기본 메모리 사용량을 자격 증명 크게 줄입니다.

자세한 내용은 참조 [보호 사용자가 작동을 그룹화 하는 방법을](#BKMK_HowItWorks) 이 항목의 합니다.



## <a name="BKMK_Requirements"></a>보호 된 사용자 그룹 요구 사항
보호 사용자 그룹의 회원에 대해 디바이스 보호를 제공 하기 위해 요구 사항은 다음과 같습니다.

- 도메인 계정에 있는 모든 도메인 컨트롤러에 보호 사용자 전 세계 보안 그룹 복제 됩니다.

- Windows 8.1 및 Windows Server 2012 r 2 지원 기본적으로 추가 됩니다. [Microsoft 보안 공지 2871997](https://technet.microsoft.com/library/security/2871997) Windows 7, Windows Server 2008 R2 및 Windows Server 2012에 지원을 추가 합니다.

보호 사용자 그룹의 회원 도메인 컨트롤러 보호를 제공 하기 위해 요구 사항은 다음과 같습니다.

- Windows Server 2012 R2 도메인 기능 상위는 도메인에 있는 사용자가 있어야 합니다.

### <a name="adding-protected-user-global-security-group-to-down-level-domains"></a>추가 보호 사용자 글로벌 보안 그룹 하위 수준 도메인을

Windows Server 2012 r 2 이전 운영 체제를 실행 하는 도메인 컨트롤러에 새 사용자 보호 보안 그룹 구성원을 추가 지원할 수 있습니다. 이렇게 하면 사용자 도메인 업그레이드 하기 전에 디바이스가 보호 기능을 활용할 수 있습니다. 

> [!Note]
> 도메인 컨트롤러 도메인 보호를 지원 하지 않습니다. 

보호 사용자 그룹이 하 여 만들 수 [주 도메인 컨트롤러 (PDC) 에뮬레이터 역할 전송](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) Windows Server 2012 r 2를 실행 하는 도메인 컨트롤러에 있습니다. 해당 그룹에 복제 되므로 다른 도메인 컨트롤러를 후 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러에서 PDC 에뮬레이터 역할을 호스트할 수 있습니다.

### <a name="BKMK_ADgroup"></a>보호 되는 사용자가 광고 group 속성

다음 표에서 보호 사용자 group 속성을 지정합니다.

|특성|값|
|-------|-----|
|알려진 SID/RID|S-1-5 번 21-<domain>-525|
|입력|글로벌 도메인|
|기본 컨테이너|CN = DC 사용자 =<domain>, DC =|
|기본 멤버|없음|
|기본 멤버의|없음|
|ADMINSDHOLDER에 의해 보호 하나요?|아니요|
|기본 컨테이너 밖으로 이동 하 여 안전 하 게 보호 하나요?|예|
|이 그룹 서비스 비 관리자의 관리 위임 하 안전 하 게 보호 하나요?|아니요|
|기본 사용자 권한|기본 사용자 권한 없음|

## <a name="BKMK_HowItWorks"></a>보호 사용자 그룹이 작동 방식
Users 보호 그룹 때의 작동 방식에 대해 설명이 합니다.

-   Windows 디바이스에 로그인

-   사용자 계정 도메인 높은 도메인 기능 수준 또는 Windows Server 2012 r 2에는

### <a name="device-protections-for-signed-in-protected-users"></a>로그인 한 사용자 보호에 대 한 장치 보호
로그인된 한 사용자가 보호 사용자 그룹의 회원 다음 보호 적용 됩니다.

-   위임 (CredSSP)는 경우에 사용자의 텍스트만 자격 증명 캐시 하지 자격 증명은 **위임 기본 자격 증명을 허용** 그룹 정책 설정을 사용 합니다.

-   부터.1 Windows 8 및 Windows Server 2012 R2, Windows 요약은 하지 캐시 사용자의 텍스트만 자격 증명 Windows 요약 활성화 되어 있는 경우에 합니다.

> [!Note]
> 설치한 후 [Microsoft 보안 공지 2871997](https://technet.microsoft.com/library/security/2871997) Windows 요약 자격 증명을 캐시 레지스트리 키가 구성 되어 될 때까지 계속 됩니다. 참조 [Microsoft 보안 공지: 보호 및 관리 자격 증명을 위한 업데이트: 2014 년 5 월 13 일](https://support.microsoft.com/en-us/help/2871997/microsoft-security-advisory-update-to-improve-credentials-protection-a) 지침은 합니다.

-   사용자의 텍스트만 자격 증명 또는 NT 단방향 기능 (NTOWF) NTLM 캐시 하지 않습니다.

-   더 이상 Kerberos DES 또는 r c 4 키 만듭니다. 또한 하지를 캐시 합니다 사용자의 자격 증명 일반 텍스트 또는 장기 키 초기 TGT 획득 한 후 합니다.

-   확인자 캐시 된 로그인 시 만들어지지 또는 잠금 해제를 오프 라인 로그인 더 이상 사용할 수 있도록 합니다.

사용자 계정 보호 사용자 그룹에 추가 되는 사용자 디바이스에 로그인 하는 경우 보호 시작 됩니다.

### <a name="domain-controller-protections-for-protected-users"></a>보호 사용자 도메인 컨트롤러 보호
Windows Server 2012 R2 도메인에 인증 된 사용자 보호 그룹의 회원 계정을 수 없는 다음과 같습니다.

-   NTLM 인증 인증 합니다.

-   DES 또는 r c 4 암호화 유형을 사용 하 여 Kerberos 미리 인증에서 합니다.

-   무제한 또는 제한 된 위임와 위임 수 있습니다.

-   초기 4 시간 수명 이상 Kerberos Tgt 갱신 합니다.

Tgt 만료 될 때까지 구성 가능 비 설정은 보호 사용자 그룹의 모든 계정에 대 한 설정 됩니다. 도메인 컨트롤러 Tgt 수명 및 도메인 정책에 따라 갱신을 설정 하는 일반적으로 **최대 수명 사용자 티켓** 및 **최대 수명 사용자 티켓 갱신**합니다. 사용자가 보호 그룹에 대 일 분이 도메인 정책에 대 한 설정 됩니다.

자세한 내용은 참조 [계정 보호 구성 하는 방법을](how-to-configure-protected-accounts.md)합니다.

## <a name="troubleshooting"></a>문제 해결
두 개의 작업 관리자 로그 보호 사용자와 관련이 이벤트를 해결 하기 위해 사용할 수 있습니다. 이러한 새 로그 위치 이벤트 뷰어 및 기본적으로 사용 하지 않도록 설정 하 고 아래에 있는 **응용 프로그램과 서비스 Logs\Microsoft\Windows\Microsoft\Authentication**합니다.

|이벤트 ID와 로그|설명|
|----------|--------|
|104<br /><br />**ProtectedUser 클라이언트**|이유: 클라이언트에서 보안 패키지 자격 증명 포함 되어 있지 않습니다.<br /><br />이 오류는 계정을 보호 하는 사용자가 보안 그룹의 회원 때 클라이언트 컴퓨터에 기록 됩니다. 이 이벤트가 나타냅니다 보안 패키지 서버 인증 하는 데 필요한 자격 증명 캐시 하지 않습니다.<br /><br />패키지 이름, 사용자 이름, 도메인 이름 및 서버 이름이 표시 됩니다.|
|304<br /><br />**ProtectedUser 클라이언트**|이유: 보안 패키지 보호 사용자의 자격 증명을 저장 하지 않습니다.<br /><br />정보 이벤트 보안 패키지가 사용자의 로그인 자격 증명 캐시 나타내기 위해 클라이언트로에 기록 됩니다. 요약 (WDigest), 자격 증명을 위임 (CredSSP) 및 NTLM 실패 보호 사용자의 로그인 자격 증명이 필요 합니다. 자격 증명 응용 프로그램 성공 여전히 수 있습니다.<br /><br />패키지 이름, 사용자 이름 및 도메인 이름 표시 됩니다.|
|100<br /><br />**ProtectedUserFailures 도메인 컨트롤러**|이유: 보호 사용자가 보안 그룹에 있는 계정에 대 한 NTLM 로그인 오류가 발생 합니다.<br /><br />오류가 발생 못했다는 메시지가 NTLM 인증 계정을 보호 하는 사용자가 보안 그룹의 회원 되었기 때문에 도메인 컨트롤러에 기록 됩니다.<br /><br />계정 이름 및 디바이스 이름을 표시합니다.|
|104<br /><br />**ProtectedUserFailures 도메인 컨트롤러**|로그인 오류가 발생 하는 사용자의 사용자 보호 보안 그룹에 대 한 그리고 이유: DES 또는 r c 4 암호화 유형 Kerberos 인증에 대 한 사용 됩니다.<br /><br />Kerberos 사전 실패 DES 및 r c 4 암호화 유형은 계정을 보호 하는 사용자가 보안 그룹의 회원 때 사용할 수 없습니다.<br /><br />(AES는 사용할 수 있습니다.)|
|303<br /><br />**ProtectedUserSuccesses 도메인 컨트롤러**|이유: Kerberos 티켓-부여-티켓 (TGT) 성공적으로 보호 된 사용자 그룹의 회원에 대해 발급 되었습니다.|



## <a name="additional-resources"></a>추가 리소스

-   [자격 증명 보호 및 관리](credentials-protection-and-management.md)

-   [인증 정책 및 인증 정책 사일로](authentication-policies-and-authentication-policy-silos.md)

-   [계정 보호를 구성 하는 방법](how-to-configure-protected-accounts.md)


