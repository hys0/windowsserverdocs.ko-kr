---
title: Windows 인증에 사용된 그룹 정책 설정
description: Windows Server 보안
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847934"
---
# <a name="group-policy-settings-used-in-windows-authentication"></a>Windows 인증에 사용된 그룹 정책 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가 위한이 참조 항목에는 인증 프로세스의 그룹 정책 설정의 영향을 확인 하 고 사용 하 여 설명합니다.

사용자, 컴퓨터 및 서비스 계정 그룹에 추가 하 여 한 다음 해당 그룹에 인증 정책을 적용 하 여 Windows 운영 체제에서 인증을 관리할 수 있습니다. 이러한 정책은 로컬 보안 정책 및 그룹 정책 설정이 라고도 관리 템플릿으로 정의 됩니다. 두 집합 모두를 구성 하 고 그룹 정책을 사용 하 여 조직 전체에 분산 수 있습니다.

> [!NOTE]
> Windows Server 2012 R2에 도입 된 기능을 사용 하면 대상된 서비스에 대 한 인증 정책을 구성할 수 있습니다 또는 보호 된 계정을 응용 프로그램에 일반적으로 사용 하 여 인증 사일로 호출 합니다. Active Directory에서이 작업을 수행 하는 방법에 대 한 정보를 참조 하세요 [How to Configure Protected Accounts](how-to-configure-protected-accounts.md)합니다.

예를 들어, 조직에서 해당 기능에 따라 그룹에 다음 정책을 적용할 수 있습니다.

-   로컬 또는 도메인에 로그온

-   네트워크를 통해 로그온

-   계정 재설정

-   계정 만들기

다음 표에서 인증과 관련 된 정책 그룹을 나열 하 고 이러한 정책을 구성 하는 도움이 될 수 있는 설명서의 링크를 제공 합니다.

|정책 그룹|Location|설명|
|--------|------|--------|
|**암호 정책**|로컬 컴퓨터 정책 구성 설정 \ 보안 계정 정책|암호 정책 특성 및 암호의 동작에 영향을 줍니다. 도메인 계정 또는 로컬 사용자 계정에 대 한 암호 정책이 사용 됩니다. 암호를 적용 등 수명에 대 한 설정을 결정합니다.<br /><br />특정 설정에 대 한 자세한 내용은 [암호 정책](https://technet.microsoft.com/itpro/windows/keep-secure/password-policy)합니다.|
|**계정 잠금 정책**|로컬 컴퓨터 정책 구성 설정 \ 보안 계정 정책|계정 잠금 정책 옵션 계정을 사용 하지 않도록 설정 된 개수의 실패 한 로그온 시도 후입니다. 이러한 옵션을 사용 하 여 도움이 될 수 있습니다 검색 하 고 암호를 손상 시키려는 시도 차단 합니다.<br /><br />계정 잠금 정책 옵션에 대 한 정보를 참조 하세요 [계정 잠금 정책](https://technet.microsoft.com/itpro/windows/keep-secure/account-lockout-policy)합니다.|
|**Kerberos 정책**|로컬 컴퓨터 정책 구성 설정 \ 보안 계정 정책|Kerberos 관련 설정을 티켓 수명 및 적용 규칙을 포함합니다. 로컬 계정은 인증에 Kerberos 인증 프로토콜을 사용 하지 않으므로 Kerberos 정책 로컬 계정 데이터베이스에 적용 되지 않습니다. 따라서 Kerberos 정책 설정은 기본 도메인 그룹 정책 개체 (GPO), 도메인 로그온에 영향을 주므로 여기서로 구성할 수 있습니다.<br /><br />도메인 컨트롤러에 대 한 Kerberos 정책 옵션에 대 한 정보를 참조 하세요 [Kerberos 정책](https://technet.microsoft.com/itpro/windows/keep-secure/kerberos-policy)합니다.|
|**감사 정책**|로컬 컴퓨터 정책 구성 설정 \ 보안 설정 \ 로컬 정책 \ 감사 정책|감사 정책을 사용 하 여 제어 하 고 사용자 및 그룹 계정 및 사용자 로그온 및 로그 오프를 관리 하 고 파일 및 폴더와 같은 개체에 대 한 액세스를 이해할 수 있습니다. 감사 정책, 감사 하 고, 크기 및 보안 로그의 동작을 설정 하 고, 개체의 액세스를 모니터링 하려면 모니터링 하려는 액세스 유형을 결정 하려는 이벤트의 범주를 지정할 수 있습니다.<br /><br />|
|**사용자 권한 할당**|로컬 컴퓨터 정책 구성 설정 \ 보안 설정 \ 로컬 정책 \ 사용자 권한 할당|사용자 권한은 사용자, 속해 있는 관리자나 고급 사용자, 사용자 같은 보안 그룹 기준으로 일반적으로 할당 됩니다. 이 범주에서 정책 설정은 액세스 및 보안 그룹 멤버 자격의 방법에 따라 컴퓨터에 액세스 하려면 권한을 부여 하거나 거부할 일반적으로 사용 됩니다.|
|**보안 옵션**|로컬 컴퓨터 정책 구성 설정 \ 보안 설정 \ 로컬 정책 \ 보안 옵션|인증과 관련 된 정책에는 다음이 포함 됩니다.<br /><br />-장치<br />도메인 컨트롤러<br />-도메인 구성원<br />대화형 로그온<br />Microsoft 네트워크 서버<br />-네트워크 액세스<br />-네트워크 보안<br />복구 콘솔<br />종료<br /><br />|
|**자격 증명 위임**|컴퓨터 구성 \ 관리 템플릿 시스템 위임|자격 증명의 위임에는 로컬 자격 증명 구성원 서버 및 도메인 컨트롤러는 도메인 내에서 가장 주목할 만한 다른 시스템에서 사용할 수 있는 메커니즘입니다. 이러한 설정은 Credential Security Support Provider (자격 증명 SSP)를 사용 하 여 응용 프로그램에 적용 됩니다. 원격 데스크톱 연결은 예시입니다.|
|**KDC**|컴퓨터 구성 \ 관리 템플릿 Templates\System\KDC|이 정책 설정의 키 배포 센터 (KDC)에 도메인 컨트롤러에서 서비스는 Kerberos 인증 요청을 처리 하는 방법을 하는 영향을 줍니다.|
|**Kerberos**|컴퓨터 구성 \ 관리 템플릿 Templates\System\Kerberos|이러한 정책 설정은 클레임, Kerberos 아머 링, 복합 인증, 식별 프록시 서버 및 기타 구성을 지원 하기 위해 Kerberos가 구성 하는 방법을 적용 됩니다.|
|**Logon**|컴퓨터 구성\관리 템플릿\시스템\로그인|이러한 정책 설정은 시스템 사용자에 대 한 로그온 환경을 제공 하는 방법을 제어 합니다.|
|**Net Logon**|컴퓨터 구성 \ 관리 템플릿 Templates\System\Net 로그온|이러한 정책 설정은 시스템에서 도메인 컨트롤러 로케이터 동작 하는 방식을 포함 하는 네트워크 로그온 요청을 처리 하는 방법을 제어 합니다.<br /><br />도메인 컨트롤러 로케이터 복제 프로세스에 적용 하는 방법에 대 한 자세한 내용은 참조 하세요. [사이트 간 복제 이해](https://technet.microsoft.com/library/cc771251.aspx)합니다.|
|**Biometrics**|컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\Biometrics|이러한 정책 설정은 일반적으로 허용 하거나 거부 생체 인식 인증 방법으로 사용 합니다.<br /><br />생체 인식의 Windows 구현에 대 한 자세한 내용은 Windows 생체 인식 프레임 워크 개요를 참조 하세요.|
|**자격 증명 사용자 인터페이스**|컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\Credential 사용자 인터페이스|이러한 정책 설정은 항목 지점에서 자격 증명 관리 하는 방법을 제어 합니다.|
|**암호 동기화**|컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\Password 동기화|이러한 정책 설정은 시스템에서 Windows와 UNIX 기반 운영 체제 간의 암호 동기화를 관리 하는 방법을 결정 합니다.<br /><br />자세한 내용은 [암호 동기화](https://technet.microsoft.com/library/cc732609.aspx)합니다.|
|**스마트 카드**|컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\Smart 카드|이러한 정책 설정은 시스템에서 스마트 카드 로그온을 관리 하는 방법을 제어 합니다.<br /><br />|
|**Windows 로그온 옵션**|컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\Windows 로그온 옵션|이러한 정책 설정은 로그온 기회 사용할 시기와 방법을 제어 합니다.|
|**Ctrl + Alt + Del 옵션**|컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\Ctrl + Alt + Del 옵션|이러한 정책 설정은의 모양 및 로그온 UI (보안 데스크톱)에서 작업 관리자 등 컴퓨터의 키보드 잠금 기능에 대 한 접근성에 영향을 줍니다.|
|**Logon**|컴퓨터 구성 \ 관리 템플릿 Templates\Windows Components\Logon|이러한 정책 설정을 확인 하는 경우 또는 사용자가 로그온 할 때 프로세스를 실행할 수 있습니다.|

## <a name="see-also"></a>참조
[Windows 인증 기술 개요](windows-authentication-technical-overview.md)


