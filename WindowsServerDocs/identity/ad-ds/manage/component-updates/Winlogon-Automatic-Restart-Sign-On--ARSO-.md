---
ms.assetid: cb834273-828a-4141-9387-37dd8270e932
title: "Winlogon 자동 다시 시작 Sign-on (ARSO)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 27d4285d34105908555458a95bd70fc04fd2901a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Winlogon 자동 다시 시작 Sign-on (ARSO)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**작성자**: Windows 그룹과 조자룡 Turner, 선임 지원 엔지니어로

> [!NOTE]
> 이 콘텐츠는 Microsoft 고객 지원 담당자가 작성 하며 경험이 관리자와 technet 항목 일반적으로 제공 하는 것 보다에 대 한 보다 긴밀 기술 설명은 기능 및 Windows Server 2012 r 2에 대 한 해결 방법을 찾는 누가 시스템 개발자를 위한 것입니다. 그러나 받지 않았습니다 동일한 편집 가공 일부 언어 일반적으로 technet 찾을 수 보다 세련 된 적게 보일 수 있도록 합니다.

## <a name="overview"></a>개요
Windows 8 잠금 화면 앱을 도입 했습니다.  실행 하 고 하면 사용자 세션 휴대폰이 잠겼을 때 알림을 표시 하는 응용 프로그램은 이러한 (일정 약속, 이메일 및 메시지 등).  디바이스는 Windows 업데이트 하는 프로세스로 인해 다시 시작 하는 다시 시작할 때 잠금 화면 알림이 표시 되지 않습니다.  일부 사용자는 이러한 잠금 화면 응용 프로그램에 따라 다릅니다.

## <a name="whats-changed"></a>변경 된 내용
사용자가 Windows 8.1 디바이스에 로그인 하는 경우 LSA는 lsass.exe 해야만 사용자 자격 증명을 액세스할 수 있는 암호화 된 메모리에 저장 됩니다. Windows 업데이트는 자동으로 다시 부팅 사용자 존재 여부를 않고도 시작 하는 경우 해당 자격이 증명 로그온 사용자에 대 한 구성 하 사용 됩니다. 시스템 TCB 권한으로 실행 하는 Windows 업데이트가 작업을 수행 하는 RPC 호출을 시작 됩니다.

을 다시 부팅 한에서 사용자를 자동으로 로그온 메커니즘을 통해 로그인 한 후 사용자의 세션을 보호 하기 위해 또한 잠겨 있습니다. 잠금 시작 됩니다 Winlogon 통해 반면 자격 증명 관리 LSA 하면 됩니다.  자동으로 로그인 하 고 본체에서 사용자를 잠그는 다시 시작 하 고 사용할 수 있는 사용자의 잠금 화면 응용 프로그램 됩니다.

> [!NOTE]
> Windows 업데이트를 다시 부팅 일으킨 마지막 대화형 사용자는 자동으로 로그인 하 고 세션 잠겨 후 하므로 사용자의 잠금 화면 앱 실행할 수 있습니다.

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreenApp.gif)

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreen.gif)

**빠른 개요**

-   Windows 업데이트에는 다시 시작 해야 함

-   컴퓨터를 다시 시작할 수 (*없는 앱을 실행 하는 데이터가 손실 될*)?

    -   다시 시작

    -   다시 로그인

    -   디바이스 잠금

-   사용 또는 그룹 정책에 따라 사용 하지 않도록 설정

    -   서버 Sku에서에서 기본적으로 사용 안 함

-   이유가 무엇 일까요?

    -   일부 업데이트는 사용자가 로그인 다시 시작할 때까지 완료 됩니다.

    -   사용자 환경 향상: 업데이트를 설치를 완료 하기 위해 15 분까지 기다릴 필요가

-   어떻게 하나요? 로그온

    -   암호 저장, 해당 자격 증명으로 로그인을 사용 하 여

    -   페이지의 메모리에 LSA 비밀로 자격 증명 저장

    -   BitLocker를 활성화 된 경우에 사용할 수

## <a name="group-policy-sign-in-last-interactive-user-automatically-after-a-system-initiated-restart"></a>그룹 정책: 로그인 마지막 대화형 사용자 시스템 시작 다시 시작 후 자동으로
Windows 8.1 Windows Server 2012 R2, Windows 업데이트를 다시 시작 된 후 잠금 화면 사용자의 로그온 Server 제품에 대 한 옵트인 및 Sku 클라이언트에 대 한 옵트아웃 / 합니다.

**정책 위치:** 컴퓨터 구성 > 정책을 > 관리 템플릿 > Windows 구성 요소 > Windows 로그온 옵션

**정책 이름:** 로그인 마지막 대화형 사용자 시스템 시작 다시 시작 후 자동으로

**지원 되는:** 적어도 Windows Server 2012 R2, Windows 8.1 또는 Windows RT 8.1

**도움말/설명 합니다.**

이 정책 설정은 디바이스는 자동으로 로그인 마지막 대화형 사용자 Windows 업데이트 시스템이 다시 시작 된 후 여부를 제어 합니다.

사용 하도록 설정 하거나이 정책 설정을 하지 않는 경우 장치 Windows 업데이트를 다시 시작한 후에 자동 로그인 구성 하려면 사용자의 자격 증명 (사용자 이름, 도메인 및 암호화 암호 포함)를 안전 하 게 저장 합니다. Windows 업데이트를 다시 시작 된 후 사용자에 자동으로 로그인 되며 해당 사용자에 대해 구성 모든 잠금 화면 앱으로 세션이 자동으로 잠겨 있습니다.

이 정책 설정을 사용 하는 경우 Windows 업데이트를 다시 시작한 후 장치에 자동 로그인에 대 한 사용자의 자격 증명을 저장 하지 않습니다. 시스템이 다시 시작 된 후 잠금 화면이 앱은 사용자의를 다시 시작 됩니다.

**레지스트리 편집기**

|이름 값|입력|데이터|
|--------------|--------|--------|
|DisableAutomaticRestartSignOn|DWORD|0<br /><br />**예:**<br /><br />0 (사용 가능)<br /><br />1 (사용 안 함)|

**정책 레지스트리 위치:** HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System

**유형:** DWORD

**레지스트리 이름:** DisableAutomaticRestartSignOn

값: 0 또는 1

0 = 사용

1 = 사용 안 함

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_SignInPolicy.gif)

## <a name="troubleshooting"></a>문제 해결
WinLogon 자동으로 잠급니다 WinLogon의 상태 추적 WinLogon 이벤트 로그에 설정이 저장 됩니다.

구성 로그온 시도가 상태 기록

-   성공 경우

    -   따라서 기록

-   오류가 경우:

    -   오류가 발생 했습니다 기록

-   BitLocker의 상태가 변경 될 때:

    -   기록 됩니다 자격 증명을 제거

        -   이러한 작업 LSA 로그에 저장 됩니다.

### <a name="reasons-why-autologon-might-fail"></a>왜 로그온 실패 하는 이유
사용자 자동 로그인을 얻을 수 없는 경우가 있습니다.  이 섹션 캡처할 알려진된 시나리오가 발생할 수 있는 것입니다.

### <a name="user-must-change-password-at-next-login"></a>반드시 다음 로그인 할 때 암호 변경
사용자의 로그인 다음 로그인 할 때 암호 변경을 요구 되는 경우 차단 된 상태를 입력할 수 있습니다.  대부분의 경우 다시 시작 하기 전에 감지 있지만 일부 될 수 있습니다 (예를 들어, 비밀 번호 만료 연결할 수 종료 사이의 다음 로그인 합니다.

### <a name="user-account-disabled"></a>사용자 계정 사용 안 함
사용 하지 않도록 설정 하는 경우에 기존 사용자 세션을 유지할 수 있습니다.  불가능 하는 계정에 다시 시작 감지할 수 로컬로 대부분의 경우 사전에 따라 gp (일부 도메인 계정을 DC에서 사용할 수 없는 경우에 로그인 시나리오 작업 캐시) 도메인 계정에 대 한 되지 않을 수 있습니다.

### <a name="logon-hours-and-parental-controls"></a>로그온 시와 자녀 보호
로그온 시와 자녀 생성 되지 않도록 새로운 사용자 세션을 금지 수 있습니다.  컴퓨터를 다시 시작,이 창을 하는 동안 발생 하는 경우 해당 사용자가 로그인 할 수 없습니다.  추가 정책을 준수 동작으로 로그 아웃 또는 잠금 하는 경우  일반적으로이 기간 동안 유지 관리 창이 않은 경우에 특히 침대 시간과 웨이크 접속 간에 계정 잠금 발생할 수 있는 많은 자녀 경우 문제가 발생할 수 있습니다.

## <a name="additional-resources"></a>추가 리소스
**테이블 SEQ 테이블 \\\ * 아랍어 3: ARSO 용어**

|용어|정의|
|--------|--------------|
|로그온|로그온 여러 릴리스를 위해 Windows에 포함 된 기능입니다.  Windows 용 자동 로그온 v3.01 같은 도구에도 windows 문서화 기능은 *[http:/technet.microsoft.com/sysinternals/bb963905.aspx](https://technet.microsoft.com/sysinternals/bb963905.aspx)*<br /><br />디바이스의 단일 사용자를 자격 증명을 입력 하지 않고 자동으로 로그인 할 수 있습니다. 자격 증명 구성 하 고 암호화 된 LSA 비밀로 레지스트리에 저장 됩니다.|


