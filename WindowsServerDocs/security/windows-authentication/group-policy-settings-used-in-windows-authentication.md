---
title: Windows 인증에 사용된 그룹 정책 설정
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-windows-auth
ms.topic: article
ms.assetid: 9e237f89-45b1-4a4e-9b72-11dc7d6a470b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 7acd7439ec2e0382f1e2c725d66363e6b3a50b40
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857576"
---
# <a name="group-policy-settings-used-in-windows-authentication"></a>Windows 인증에 사용된 그룹 정책 설정

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 참조 항목에서는 인증 프로세스의 그룹 정책 설정에 대 한 사용 및 영향을 설명 합니다.

사용자, 컴퓨터 및 서비스 계정을 그룹에 추가 하 고 해당 그룹에 인증 정책을 적용 하 여 Windows 운영 체제에서 인증을 관리할 수 있습니다. 이러한 정책은 로컬 보안 정책 및 관리 템플릿 (그룹 정책 설정 라고도 함)으로 정의 됩니다. 그룹 정책를 사용 하 여 조직 전체에서 두 집합을 구성 하 고 배포할 수 있습니다.

> [!NOTE]
> Windows Server 2012 r 2에 도입 된 기능을 사용 하면 보호 된 계정을 사용 하 여 일반적으로 인증 사일로 라고 불리는 대상 서비스 또는 응용 프로그램에 대 한 인증 정책을 구성할 수 있습니다. Active Directory에서이 작업을 수행 하는 방법에 대 한 자세한 내용은 [보호 된 계정을 구성 하는 방법](how-to-configure-protected-accounts.md)을 참조 하세요.

예를 들어 조직에서 해당 기능에 따라 그룹에 다음 정책을 적용할 수 있습니다.

-   로컬 또는 도메인에 로그온

-   네트워크를 통해 로그온

-   계정 다시 설정

-   계정 만들기

다음 표에서는 인증과 관련 된 정책 그룹을 나열 하 고 이러한 정책을 구성 하는 데 도움이 되는 설명서에 대 한 링크를 제공 합니다.

|정책 그룹|위치|설명|
|--------|------|--------|
|**암호 정책**|로컬 컴퓨터 Policy\Computer 구성 \ 보안 설정 \ Settings\Account 정책|암호 정책은 암호의 특징 및 동작에 영향을 줍니다. 암호 정책은 도메인 계정 또는 로컬 사용자 계정에 사용 됩니다. 암호에 대 한 설정 (예: 적용 및 수명)을 결정 합니다.<p>특정 설정에 대 한 자세한 내용은 [암호 정책](https://technet.microsoft.com/itpro/windows/keep-secure/password-policy)을 참조 하세요.|
|**계정 잠금 정책**|로컬 컴퓨터 Policy\Computer 구성 \ 보안 설정 \ Settings\Account 정책|계정 잠금 정책 옵션은 실패 한 로그온 시도 횟수를 설정한 후 계정을 사용 하지 않도록 설정 합니다. 이러한 옵션을 사용 하면 암호 해제 시도를 감지 하 고 차단할 수 있습니다.<p>계정 잠금 정책 옵션에 대 한 자세한 내용은 [계정 잠금 정책](https://technet.microsoft.com/itpro/windows/keep-secure/account-lockout-policy)을 참조 하세요.|
|**Kerberos 정책**|로컬 컴퓨터 Policy\Computer 구성 \ 보안 설정 \ Settings\Account 정책|Kerberos 관련 설정에는 티켓 수명 및 적용 규칙이 포함 됩니다. Kerberos 인증 프로토콜은 로컬 계정을 인증 하는 데 사용 되지 않으므로 kerberos 정책은 로컬 계정 데이터베이스에 적용 되지 않습니다. 따라서 Kerberos 정책 설정은 도메인 로그온에 영향을 주는 기본 도메인 그룹 정책 개체 (GPO)를 통해서만 구성할 수 있습니다.<p>도메인 컨트롤러의 Kerberos 정책 옵션에 대 한 자세한 내용은 [Kerberos 정책](https://technet.microsoft.com/itpro/windows/keep-secure/kerberos-policy)을 참조 하십시오.|
|**감사 정책**|로컬 컴퓨터 Policy\Computer 구성 \ 로컬 정책 감사 정책|감사 정책을 사용 하면 파일 및 폴더와 같은 개체에 대 한 액세스를 제어 및 이해 하 고 사용자 및 그룹 계정과 사용자 로그온 및 logoffs을 관리할 수 있습니다. 감사 정책은 감사 하려는 이벤트 범주를 지정 하 고, 보안 로그의 크기와 동작을 설정 하 고, 액세스를 모니터링할 개체와 모니터링할 액세스 유형을 결정할 수 있습니다.<p>|
|**사용자 권한 할당**|로컬 컴퓨터 Policy\Computer 구성 \ 로컬 정책 \ 로컬 정책 \ 보안 설정|사용자 권한은 일반적으로 사용자가 속한 보안 그룹 (예: 관리자, 고급 사용자 또는 사용자)의 기반으로 할당 됩니다. 이 범주의 정책 설정은 일반적으로 액세스 및 보안 그룹 멤버 자격 방법에 따라 컴퓨터에 대 한 액세스 권한을 부여 하거나 거부 하는 데 사용 됩니다.|
|**보안 옵션**|로컬 컴퓨터 Policy\Computer 구성 \ 로컬 정책 \ 로컬 정책 \ 보안 옵션|인증과 관련 된 정책은 다음과 같습니다.<p>-장치<br />-도메인 컨트롤러<br />-도메인 구성원<br />-대화형 로그온<br />-Microsoft 네트워크 서버<br />-네트워크 액세스<br />-네트워크 보안<br />-복구 콘솔<br />-Shutdown<p>|
|**자격 증명 위임**|컴퓨터 구성 \ Templates\System\Credentials 위임|자격 증명 위임은 도메인 내의 구성원 서버 및 도메인 컨트롤러와 같은 다른 시스템에서 로컬 자격 증명을 사용할 수 있도록 하는 메커니즘입니다. 이러한 설정은 자격 증명 SSP (보안 지원 공급자)를 사용 하 여 응용 프로그램에 적용 됩니다. 예 원격 데스크톱 연결입니다.|
|**KDC**|컴퓨터 구성 \ Templates\System\KDC|이러한 정책 설정은 도메인 컨트롤러의 서비스인 KDC (키 배포 센터)가 Kerberos 인증 요청을 처리 하는 방법에 영향을 줍니다.|
|**Kerberos**|컴퓨터 구성 \ Templates\System\Kerberos|이러한 정책 설정은 Kerberos가 클레임, Kerberos 아머 링, 복합 인증, 프록시 서버 식별 및 기타 구성에 대 한 지원을 처리 하도록 구성 하는 방법에 영향을 줍니다.|
|**로그온**|컴퓨터 구성\관리 템플릿\시스템\로그인|이러한 정책 설정은 시스템에서 사용자에 대 한 로그온 환경을 표시 하는 방법을 제어 합니다.|
|**Net Logon**|컴퓨터 구성 \ Templates\System\Net 로그온|이러한 정책 설정은 도메인 컨트롤러 로케이터의 동작을 포함 하 여 시스템에서 네트워크 로그온 요청을 처리 하는 방법을 제어 합니다.<p>도메인 컨트롤러 로케이터가 복제 프로세스에 얼마나 적합 한지에 대 한 자세한 내용은 [사이트 간 복제 이해](https://technet.microsoft.com/library/cc771251.aspx)를 참조 하세요.|
|**인식을**|컴퓨터 구성 \ 구성 \ Components\Biometrics|일반적으로 이러한 정책 설정은 인증 방법으로 생체 인식 사용을 허용 하거나 거부 합니다.<p>생체 인식의 Windows 구현에 대 한 자세한 내용은 Windows 생체 인식 프레임워크 개요를 참조 하세요.|
|**자격 증명 사용자 인터페이스**|컴퓨터 구성 \ 사용자 \ Components\Credential 사용자 인터페이스|이러한 정책 설정은 진입 지점에서 자격 증명을 관리 하는 방법을 제어 합니다.|
|**암호 동기화**|컴퓨터 구성 \ 구성 \ Components\Password 동기화|이러한 정책 설정은 시스템에서 Windows 및 UNIX 기반 운영 체제 간의 암호 동기화를 관리 하는 방법을 결정 합니다.<p>자세한 내용은 [암호 동기화](https://technet.microsoft.com/library/cc732609.aspx)를 참조 하세요.|
|**스마트 카드**|컴퓨터 구성 \ 구성 \ Components\Smart 카드|이러한 정책 설정은 시스템에서 스마트 카드 로그온을 관리 하는 방법을 제어 합니다.<p>|
|**Windows 로그온 옵션**|컴퓨터 구성 \ 구성 \ 로그온 옵션|이러한 정책 설정은 로그온 기회를 사용할 수 있는 시기 및 방법을 제어 합니다.|
|**Ctrl + Alt + Del 옵션**|컴퓨터 구성 \ 구성 \ Components\Ctrl + Alt + Del 옵션|이러한 정책 설정은 작업 관리자 및 컴퓨터의 키보드 잠금과 같은 로그온 UI (보안 데스크톱)의 기능에 적용 되는 모양 및 접근성에 영향을 줍니다.|
|**로그온**|컴퓨터 구성 \ 구성 \ Components\Logon|이러한 정책 설정은 사용자가 로그온 할 때 실행할 수 있는 프로세스를 결정 합니다.|

## <a name="see-also"></a>참고 항목
[Windows 인증 기술 개요](windows-authentication-technical-overview.md)


