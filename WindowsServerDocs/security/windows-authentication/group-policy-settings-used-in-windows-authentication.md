---
title: "Windows 인증에 사용 되는 그룹 정책 설정"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e237f89-45b1-4a4e-9b72-11dc7d6a470b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 38df2033b57c0394b96f539f54efe6a3579500f2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="group-policy-settings-used-in-windows-authentication"></a>Windows 인증에 사용 되는 그룹 정책 설정

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 용 참조 여기서 사용 및 인증 과정에서 그룹 정책 설정의 영향에 설명 합니다.

이러한 그룹 정책을 인증을 적용 하 여 다음 하 고 사용자, 컴퓨터 및 서비스 계정 그룹에 추가 하 여 Windows 운영 체제에는 인증을 관리할 수 있습니다. 이 정책이 로컬 보안 정책이 및 관리 템플릿, 그룹 정책 설정 라고도으로 정의 됩니다. 모두 설정 구성 하 고 그룹 정책을 통해 조직에 배포할 수 있습니다.

> [!NOTE]
> 응용 프로그램을 사용 하 여 인증 사일로 져야 계정 보호 또는 기능 Windows Server 2012 r 2에 새롭게 적용 된 대상된 서비스에 대 한 정책을 인증 구성할 수 있습니다. Active Directory에이 작업을 수행 하는 방법에 대 한 정보를 참조 하세요. [계정 보호 구성 하는 방법을](how-to-configure-protected-accounts.md)합니다.

예를 들어 다음 정책을 조직에서의 기능에 따라 그룹을 적용할 수 있습니다.

-   로컬에서 또는 도메인에에 로그인

-   네트워크 로그온 합니다.

-   계정에 다시 설정

-   계정 만들기

다음 표에서 정책 그룹 인증에 관련 된 고 구성 정책 하는 데 도움이 되는 문서에 대 한 링크를 제공 합니다.

|그룹 정책|위치|설명|
|--------|------|--------|
|**암호 정책**|로컬 컴퓨터 정책 구성 보안 설정 정책|암호 정책을 특징과 동작 암호에 영향을 줍니다. 도메인 계정 또는 로컬 사용자 계정에 대 한 암호 정책은 사용 됩니다. 이러한 집행 및 수명 같은 암호에 대 한 설정을 확인합니다.<br /><br />특정 설정에 대 한 내용은 [암호 정책](https://technet.microsoft.com/itpro/windows/keep-secure/password-policy)합니다.|
|**계정 잠금 정책**|로컬 컴퓨터 정책 구성 보안 설정 정책|계정 잠금 정책 옵션 횟수 로그온 시도가 실패 한 후 계정을 안 함 이러한 옵션을 사용 하 여 검색 및 암호 중단 하려는 시도 차단할 수 하는 데 도움이 수 있습니다.<br /><br />계정 잠금 정책 옵션에 대 한 내용은 [계정 잠금 정책](https://technet.microsoft.com/itpro/windows/keep-secure/account-lockout-policy)합니다.|
|**Kerberos 정책**|로컬 컴퓨터 정책 구성 보안 설정 정책|설정 Kerberos 관련 티켓 수명 및 집행 규칙을 포함 합니다. 로컬 계정 데이터베이스에 Kerberos 인증 프로토콜 로컬 계정 인증 하는 데 사용 되지 Kerberos 정책이 적용 되지 않습니다. 따라서 기본 도메인 그룹 정책 개체 GPO (), 도메인 로그온 어디에 영향을 통해만 Kerberos 정책 설정은 구성할 수 있습니다.<br /><br />도메인 컨트롤러에 대 한 옵션 Kerberos 정책에 대 한 내용은 [Kerberos 정책](https://technet.microsoft.com/itpro/windows/keep-secure/kerberos-policy)합니다.|
|**감사 정책**|로컬 컴퓨터 정책 구성할 보안 로컬 감사 정책|감사 정책 개체, 파일, 폴더 등 및 사용자 및 그룹 계정 및 사용자 로그온 로그 오프 관리에 대 한 액세스를 이해 옵션과 제어할 수 있습니다. 감사 정책을 감사할 크기와 보안 로그의 동작을 설정 하 고 모니터링 액세스 하려는 어떤 개체 및 모니터링 하려는 어떤 종류의 액세스를 확인 하려는 이벤트 범주를 지정할 수 있습니다.<br /><br />|
|**권한 사용자 지정**|로컬 컴퓨터 정책 구성할 보안 로컬 \ 사용자 권한 할당|사용자는 속해 있는, 관리자가, 고급 사용자 또는 사용자가 같은 보안 그룹을 기반으로 사용자 권한은 할당 일반적으로 됩니다. 이 범주에 속하는 정책 설정 하거나 액세스 및 보안 그룹 등록 하는 방법에 따라 컴퓨터에 액세스할 수 있는 권한이 거부할 수 일반적으로 사용 됩니다.|
|**보안 옵션**|로컬 컴퓨터 정책 구성할 보안 로컬 보안 옵션|인증에 관련 된 정책 다음과 같습니다.<br /><br />-장치<br />도메인 컨트롤러<br />도메인 구성원이<br />대화형 로그온<br />네트워크 Microsoft 서버<br />네트워크 액세스<br />네트워크 보안<br />콘솔 복구<br />종료<br /><br />|
|**자격 증명 위임**|컴퓨터 구성 \ 관리 템플릿 Templates\System\Credentials 위임|자격 증명 위임 장치가 로컬 자격 증명 다른 시스템 가장 주목할 만한 구성원 서버와 내 도메인 도메인 컨트롤러에서 사용할 수 있습니다. 이러한 설정은 자격 증명 보안 지원 공급자 (자격 증명 SSP)를 사용 하 여 응용 프로그램에 적용 됩니다. 원격 데스크톱 연결 예입니다.|
|**KDC**|컴퓨터 구성 \ 관리 템플릿 Templates\System\KDC|이 정책 설정의 키 센터 (KDC 배포)를 도메인 컨트롤러에서 서비스는 Kerberos 인증 요청을 처리 하는 방법에 영향을 합니다.|
|**Kerberos**|컴퓨터 구성 \ 관리 템플릿 Templates\System\Kerberos|이 정책 설정 Kerberos 클레임, Kerberos armoring, 복합 인증, 신원 파악이 가능한 프록시 서버 및 기타 구성에 대 한 지원을 처리 하도록 구성 된 어떻게 영향을 줍니다.|
|**로그온**|시스템 컴퓨터 구성 \ 관리 템플릿 \ 로그온|이 정책 설정 시스템이 사용자의 로그온 경험을 제공 하는 방법을 제어 합니다.|
|**네트워크 로그온**|컴퓨터 구성 \ 관리 템플릿 Templates\System\Net 로그온|이 정책 설정의 시스템 도메인 컨트롤러 Locator 동작 하는 방법을 포함 하 여 네트워크 로그온 요청을 처리 하는 방법을 제어 합니다.<br /><br />도메인 컨트롤러 Locator 복제 프로세스를 적용 하는 방법에 대 한 자세한 내용은 참조 [사이트 간 이해 복제](https://technet.microsoft.com/library/cc771251.aspx)합니다.|
|**생체 인식**|컴퓨터 구성 \ 관리 템플릿 요소 Components\Biometrics|이 정책 설정 일반적으로 허용 또는 생체 인식 인증 방법으로 사용 거부 합니다.<br /><br />Windows 구현 생체 인식에 대 한 정보를 Windows 생체 프레임 워크 개요를 참조 하십시오.|
|**자격 증명 사용자 인터페이스**|컴퓨터 구성 \ 관리 템플릿 요소 Components\Credential 사용자 인터페이스|이 정책 설정 자격 증명 입력 시 관리 어떻게 제어 합니다.|
|**암호 동기화**|컴퓨터 구성 \ 관리 템플릿 요소 Components\Password 동기화|이 정책 설정의 시스템 창과 UNIX 기반 운영 체제 간 암호 동기화를 관리 하는 방법을 결정 합니다.<br /><br />자세한 내용은 참조 [암호 동기화](https://technet.microsoft.com/library/cc732609.aspx)합니다.|
|**스마트 카드**|컴퓨터 구성 \ 관리 템플릿 요소 Components\Smart 카드|이 정책 설정 방법을 제어 시스템 스마트 카드 로그온 합니다.<br /><br />|
|**Windows 로그온 옵션**|컴퓨터 구성 \ 관리 템플릿 요소 Components\Windows 로그온 옵션|이 정책 설정 로그온 기회 사용할 수 있는 방법과 시기를 제어 합니다.|
|**Ctrl + Alt + Del 옵션**|컴퓨터 구성 \ 관리 템플릿 요소 Components\Ctrl + Alt + Del 옵션|이 정책 설정의 모양 및 접근성에 로그온 UI (Secure 바탕 화면), 작업 관리자는 컴퓨터의 키보드 잠금 등의 기능에 영향을 줍니다.|
|**로그온**|컴퓨터 구성 \ 관리 템플릿 요소 Components\Logon|이 정책 설정 하는 경우에 따라 또는 프로세스는 사용자의 로그온 할 때 실행할 수 있습니다.|

## <a name="see-also"></a>참조 하십시오
[Windows 인증 기술 개요](windows-authentication-technical-overview.md)


