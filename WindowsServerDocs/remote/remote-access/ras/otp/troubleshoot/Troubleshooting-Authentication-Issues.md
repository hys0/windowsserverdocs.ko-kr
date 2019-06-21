---
title: 인증 문제 해결
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71307757-f8f4-4f82-b8b3-ffd4fd8c5d6d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 08dd6822cc30135506d82041cfbeab0bc1a058ab
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282361"
---
# <a name="troubleshooting-authentication-issues"></a>인증 문제 해결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 사용자가 OTP 인증을 사용 하 여 DirectAccess에 연결 하려고 할 때 할 문제와 관련 된 문제에 대 한 문제 해결 정보를 포함 합니다. DirectAccerss OTP 관련 이벤트에서 이벤트 뷰어 클라이언트 컴퓨터에 로그온 **응용 프로그램 및 서비스 로그/Microsoft/Windows/OtpCredentialProvider**합니다. DirectAccess OTP를 사용 하 여 문제를 해결할 때이 로그를 사용할 수 있는지 확인 하십시오.  
  
## <a name="failed-to-access-the-ca-that-issues-otp-certificates"></a>OTP 인증서를 발급 하는 CA를 액세스 하지 못했습니다.  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). 사용자에 대 한 OTP 인증서 등록 <username> < 합니다 > CA 서버의 실패 한, 실패 한 경우 가능한 오류의 원인은 요청 합니다. CA 서버 이름을 확인할 수 없는, CA 서버는 첫 번째 DirectAccess 터널을 통해 액세스할 수 없습니다 또는 CA 서버에 연결을 설정할 수 없습니다.  
  
**가능한 원인**  
  
사용자는 유효한 일회용 암호를 제공 하 고 DirectAccess 서버 서명 인증서 요청 그러나 클라이언트 컴퓨터 등록 프로세스를 완료 하려면 OTP 인증서를 발급 하는 CA를 연결할 수 없습니다.  
  
**해결 방법**  
  
DirectAccess 서버에서 다음 Windows PowerShell 명령을 실행 합니다.  
  
1.  발급 Ca 구성 된 OTP 목록을 가져오고 'CAServer'의 값을 확인: `Get-DAOtpAuthentication`  
  
2.  Ca 관리 서버로 구성 되어 있는지 확인 합니다. `Get-DAMgmtServer -Type All`  
  
3.  클라이언트 컴퓨터는 인프라 터널 설정에 있는지 확인 합니다. 고급 보안 콘솔을 사용 하 여 Windows 방화벽에서 확장 **모니터링/보안 연결은**, 클릭 **주 모드**, IPsec 보안 연결을 올바른 원격을 사용 하 여 표시 되는지 확인 하 고 DirectAccess 구성에 대 한 주소입니다.  
  
## <a name="directaccess-server-connectivity-issues"></a>DirectAccess 서버 간의 연결 문제  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그)  
  
다음 오류 중 하나입니다.  
  
-   기본 경로 < OTP_authentication_path > 및 < OTP_authentication_port > 포트를 사용 하 여 원격 액세스 서버 < DirectAccess_server_hostname >에 대 한 연결을 설정할 수 없습니다. 오류 코드: < internal_error_code >.  
  
-   기본 경로 < OTP_authentication_path > 및 < OTP_authentication_port > 포트를 사용 하 여 원격 액세스 서버 < DirectAccess_server_hostname >에 사용자 자격 증명을 보낼 수 없습니다. 오류 코드: < internal_error_code >.  
  
-   기본 경로 < OTP_authentication_path > 및 < OTP_authentication_port > 포트를 사용 하 여 < DirectAccess_server_hostname > 원격 액세스 서버에서 응답을 받지 못했습니다. 오류 코드: < internal_error_code >.  
  
**가능한 원인**  
  
클라이언트 컴퓨터는 DirectAccess 서버에서 잘못 구성 된 IIS 서버 또는 하거나 네트워크 문제로 인해 인터넷을 통해 DirectAccess 서버를 액세스할 수 없습니다.  
  
**해결 방법**  
  
클라이언트 컴퓨터의 인터넷 연결이 작동 하는지 확인 하 고는 DirectAccess 서비스가 실행 되 고 액세스할 수 있는 인터넷을 통해 해야 합니다.  
  
## <a name="failed-to-enroll-for-the-directaccess-otp-logon-certificate"></a>DirectAccess OTP 로그온 인증서에 대 한 등록 하지 못함  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). < 합니다 > CA에서 인증서 등록에 실패 했습니다. OTP 서명 인증서가 예상 대로 요청 서명 되지 않았습니다 또는 사용자에 게 등록 하는 권한이 있습니다.  
  
**가능한 원인**  
  
사용자가 제공한 일회용 암호 잘못 되었지만 OTP 로그온 인증서를 발급 하도록 발급 인증 기관 (CA) 거부 되었습니다. 올바른 EKU (OTP 등록 기관 응용 프로그램 정책)를 사용 하 여 인증서 요청 제대로 서명 되지 않은 또는 DA OTP 템플릿에서 "Enroll" 권한이 사용자에 게 되지 않습니다.  
  
**해결 방법**  
  
DirectAccess OTP 사용자에 게 권한을 DirectAccess OTP 로그온 인증서를 등록 하 고 적절 한 "응용 프로그램 정책" 서명 템플릿 DA OTP 등록 기관에 포함 되어 있는지 확인 합니다. 또한 원격 액세스 서버에서 DirectAccess 등록 기관 인증서가 유효한 지 확인 합니다. 3\.2 계획 OTP 인증서 템플릿 및 3.3 계획 등록 기관 인증서를 참조 하세요.  
  
## <a name="missing-or-invalid-computer-account-certificate"></a>컴퓨터 계정 인증서가 없거나 잘못 되었습니다  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그).  로컬 컴퓨터 인증서 저장소에서 OTP에 필요한 컴퓨터 인증서를 찾을 수 없으므로 OTP 인증을 완료할 수 없습니다.  
  
**가능한 원인**  
  
DirectAccess OTP 인증에 필요한 DirectAccess 서버를 사용 하 여 SSL 연결을 설정 하기 위해 클라이언트 컴퓨터 인증서 그러나 클라이언트 컴퓨터 인증서를 찾을 수 없습니다 또는 유효 하지 않은 예를 들어, 인증서 만료 된 경우.  
  
**해결 방법**  
  
컴퓨터 인증서가 있으며이 유효 해야 합니다.  
  
1.  로컬 컴퓨터 계정에 대 한 MMC 인증서 콘솔에서 클라이언트 컴퓨터에서 엽니다 **Personal/Certificates**합니다.  
  
2.  인증서 발급 일치 하는 컴퓨터 이름이 있는지 확인 하 고 인증서를 두 번 클릭 합니다.  
  
3.  에 **인증서** 대화 상자의 합니다 **인증서 경로** 탭의 **상태 인증서**, "이이 인증서를 확인 합니다."가 표시 하 고 있는지 확인  
  
유효한 인증서가 없는 경우 삭제 하거나 실행 하 여 잘못 된 인증서 (있는 경우) 및 컴퓨터 인증서를 다시 등록 `gpupdate /Force` 상승된 된 명령 프롬프트 또는 클라이언트 컴퓨터를 다시 시작 합니다.  
  
## <a name="missing-ca-that-issues-otp-certificates"></a>OTP 인증서를 발급 하는 누락 된 CA  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). DA 서버는 발급 CA의 주소를 반환 하지 않았으므로 OTP 인증을 완료할 수 없습니다.  
  
**가능한 원인**  
  
구성 하는 OTP 인증서를 발급 하는 Ca는 또는 모든 OTP 인증서를 발급 하는 구성 된 Ca 응답 하지 않습니다.  
  
**해결 방법**  
  
1.  OTP 인증서 (CA 이름을 CAServer에 표시 됨)를 발급 하는 Ca의 목록을 가져오려면 다음 명령을 사용 하 여: `Get-DAOtpAuthentication`합니다.  
  
2.  Ca는 구성 된 경우:  
  
    1.  두 명령을 사용 하 여 `Set-DAOtpAuthentication` 또는 DirectAccess OTP 로그온 인증서 발급 Ca를 구성 하려면 원격 액세스 관리 콘솔.  
  
    2.  새 구성을 적용 하 고 클라이언트를 실행 하 여 DirectAccess GPO 설정 새로 고침을 강제 적용 `gpupdate /Force` 상승된 된 명령 프롬프트 또는 클라이언트 컴퓨터를 다시 시작 합니다.  
  
3.  구성 Ca가 온라인 상태이 고 등록 요청에 응답 하는 있는지 확인 합니다.  
  
## <a name="misconfigured-directaccess-server-address"></a>잘못 구성 된 DirectAccess 서버 주소  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). OTP 인증을 정상적으로 완료할 수 없습니다. 이름 또는 원격 액세스 서버의 주소를 확인할 수 없습니다.  오류 코드: < error_code >. DirectAccess 설정은 서버 관리자가 유효성을 검사 해야 합니다.  
  
**가능한 원인**  
  
DirectAccess 서버의 주소를 제대로 구성 되지 않았습니다.  
  
**해결 방법**  
  
검사는 구성 된 DirectAccess 서버 주소를 사용 하 여 `Get-DirectAccess` 가 잘못 구성 하는 경우 주소를 수정 하 고 있습니다.  
  
최신 설정을 실행 하 여 클라이언트 컴퓨터에 배포 되 고 있는지 확인 `gpupdate /force` 관리자 권한 명령 프롬프트 또는 클라이언트 컴퓨터를 다시 시작 합니다.  
  
## <a name="failed-to-generate-the-otp-logon-certificate-request"></a>OTP 로그온 인증서 요청을 생성 하지 못했습니다.  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). OTP 인증을 위한 인증서 요청을 초기화할 수 없습니다. 개인 키를 생성할 수 없습니다, 사용자나 <username> 인증서 템플릿을 < OTP_template_name > 도메인 컨트롤러에 액세스할 수 없습니다.  
  
**가능한 원인**  
  
이 오류의 가능한 원인은 두 가지 있습니다.  
  
-   사용자는 OTP 로그온 템플릿을 읽을 수 있는 권한이 없습니다.  
  
-   사용자의 컴퓨터는 네트워크 문제로 인해 도메인 컨트롤러를 액세스할 수 없습니다.  
  
**해결 방법**  
  
-   OTP 로그온 서식 파일에 설정 권한을 검토 하 고는 DirectAccess otp 프로 비전 된 모든 사용자에 게 '읽기' 권한이 있는지 확인 합니다.  
  
-   도메인 컨트롤러를 관리 서버로 구성 되어 있는지 및 인프라 터널을 통해 클라이언트 컴퓨터는 도메인 컨트롤러에 연결할 수 있는지에 있는지 확인 합니다. 3\.2 계획 OTP 인증서 템플릿을 참조 하세요.  
  
## <a name="no-connection-to-the-domain-controller"></a>도메인 컨트롤러에 연결 하지 않고  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). OTP 인증을 위해 도메인 컨트롤러와의 연결을 설정할 수 없습니다. 오류 코드: < error_code >.  
  
**가능한 원인**  
  
이 오류의 가능한 원인은 두 가지 있습니다.  
  
-   사용자의 컴퓨터에 네트워크 연결이 없으므로 있습니다.  
  
-   인프라 터널을 통해 도메인 컨트롤러에 액세스할 수 없습니다.  
  
**해결 방법**  
  
-   PowerShell 프롬프트에서 다음 명령을 실행 하 여 도메인 컨트롤러를 관리 서버로 구성 되어 있는지 확인: `Get-DAMgmtServer -Type All`합니다.  
  
-   클라이언트 컴퓨터 인프라 터널을 통해 도메인 컨트롤러를 연결할 수 있는지 확인 합니다.  
  
## <a name="otp-provider-requires-challengeresponse"></a>OTP 공급자 필요 시도/응답  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). 사용자에 대 한 원격 액세스 서버 (< DirectAccess_server_name >)를 사용 하 여 OTP 인증 (<username>) 사용자의 과제가 요구 되었습니다.  
  
**가능한 원인**  
  
사용 하는 OTP 공급자는 Windows Server 2012 DirectAccess OTP에서 지원 되지 않는 한 RADIUS 시도/응답 exchange의 형태로 추가 자격 증명을 제공 하도록 사용자에 필요 합니다.  
  
**해결 방법**  
  
모든 시나리오에서 시도/응답을 요구 하지 않도록 OTP 공급자를 구성 합니다.  
  
## <a name="incorrect-otp-logon-template-used"></a>잘못 된 OTP 로그온 템플릿 사용  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). 사용자에서 CA 템플릿을 <username> 인증서 OTP 인증서를 발급 하도록 구성 되지 않은 요청 합니다.  
  
**가능한 원인**  
  
DirectAccess OTP 로그온 템플릿 바뀌었으면 및 클라이언트 컴퓨터는 이전 템플릿을 사용 하 여 인증 하려고 합니다.  
  
**해결 방법**  
  
클라이언트 컴퓨터 중 하나를 수행 하 여 최신 OTP 구성을 사용 하는지 확인 합니다.  
  
-   관리자 권한 명령 프롬프트에서 다음 명령을 실행 하 여 그룹 정책 업데이트 강제: `gpupdate /Force`합니다.  
  
-   클라이언트 컴퓨터를 다시 시작 합니다.  
  
## <a name="missing-otp-signing-certificate"></a>OTP 서명 인증서 누락  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그). OTP 서명 인증서를 찾을 수 없습니다. OTP 인증서 등록 요청을 서명할 수 없습니다.  
  
**가능한 원인**  
  
원격 액세스 서버에서 DirectAccess OTP 서명 인증서를 찾을 수 없습니다. 따라서 원격 액세스 서버에서 사용자 인증서 요청을 서명할 수 없습니다. 인증서가 없습니다. 서명, 또는 서명 인증서 만료 및 갱신 되지 않았습니다.  
  
**해결 방법**  
  
원격 액세스 서버에서 다음이 단계를 수행 합니다.  
  
1.  PowerShell cmdlet을 실행 하 여 구성 된 OTP 서명 인증서 템플릿 이름 확인 `Get-DAOtpAuthentication` 값을 검사 하 고 `SigningCertificateTemplateName`입니다.  
  
2.  인증서 MMC 스냅인을 사용 하 여이 템플릿에서 등록 된 유효한 인증서를 컴퓨터에 있는지 확인 합니다.  
  
3.  이러한 인증서가 있으면 (있는 경우) 만료 된 인증서를 삭제 하 고이 템플릿을 바탕으로 새 인증서를 등록 합니다.  
  
서명 OTP 인증서 템플릿 참조 3.3 계획 등록 기관 인증서입니다.  
  
## <a name="missing-or-incorrect-upndn-for-the-user"></a>누락 되거나 잘못 된 UPN/DN 사용자  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 이벤트 로그)  
  
다음 오류 중 하나입니다.  
  
-   사용자 <username> OTP를 사용 하 여 인증할 수 없습니다. UPN을 Active Directory에서 사용자 이름에 정의 되어 있는지 확인 합니다. 오류 코드: < error_code >.  
  
-   사용자 <username> OTP를 사용 하 여 인증할 수 없습니다. DN을 Active Directory에서 사용자 이름에 정의 되어 있는지 확인 합니다. 오류 코드: < error_code >.  
  
**수신 된 오류** (서버 이벤트 로그)  
  
사용자 이름을 <username> OTP 인증 존재 하지 않습니다 지정 합니다.  
  
**가능한 원인**  
  
사용자는 사용자 이름 (UPN)을 사용 되지 않은 또는 사용자 계정의 고유 이름 (DN) 특성이 제대로 설정, 이러한 속성은 DirectAccess OTP 적절 하 게 작동에 필요 합니다.  
  
**해결 방법**  
  
두이 특성 모두 인증 사용자를 위해 제대로 설정 되었는지 확인 하려면 도메인 컨트롤러에서 Active Directory 사용자 및 컴퓨터 콘솔을 사용 합니다.  
  
## <a name="otp-certificate-is-not-trusted-for-login"></a>OTP 인증서 로그인을 신뢰 하지 않습니다.  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**가능한 원인**  
  
OTP 인증서를 발급 하는 CA enterprise NTAuth 저장소에 있는 아닙니다. 따라서 로그온에 대 한 등록 된 인증서를 사용할 수 없습니다. 도메인 간 CA 신뢰 설정 되지 않으며 다중 도메인 및 다중 포리스트 환경에서 발생할 수 있습니다.  
  
**해결 방법**  
  
OTP 인증서를 발급 하는 CA 계층 구조의 루트의 인증서를 엔터프라이즈 NTAuth 인증서 인증을 시도 하는 사용자는 도메인의 저장소에 설치 되어 있는지 확인 합니다.  
  
## <a name="windows-could-not-verify-user-credentials"></a>Windows는 사용자 자격 증명을 확인 하지 못했습니다.  
**시나리오**합니다. 사용자는 OTP를 사용 하 여 오류를 사용 하 여 인증에 실패 합니다. "내부 오류로 인해 인증에 실패 했습니다"  
  
**수신 된 오류** (클라이언트 컴퓨터). 오류가 발생 했습니다 동안 Windows 자격 증명을 확인 했습니다. 다시 시도 하거나 관리자에 게 도움을 요청 합니다.  
  
**가능한 원인**  
  
DirectAccess OTP 로그온 인증서에 CRL을 포함 되지 않은 경우에 Kerberos 인증 프로토콜이 작동 하지 않습니다. 때문에 DirectAccess OTP 로그온 인증서 CRL을 다루지 않습니다 중 하나:  
  
-   옵션을 사용 하 여 구성 된 DirectAccess OTP 로그온 템플릿을 **발급 된 인증서에서 해지 정보를 포함 하지 않는**합니다.  
  
-   CA는 Crl을 게시 하지 않도록 구성 됩니다.  
  
**해결 방법**  
  
1.  원격 액세스 관리 콘솔에서이 오류의 원인을 확인 하려면 **2 단계 원격 액세스 서버**, 클릭 **편집**를 선택한 후는 **원격 액세스 서버 설치** 마법사를 클릭 **OTP 인증서 템플릿**합니다. OTP 인증을 위해 발급 된 인증서를 등록에 사용 된 인증서 템플릿을 기록해 둡니다. 열고 왼쪽된 창에서 인증 기관 콘솔에서 클릭 **인증서 템플릿**, 인증서 템플릿 속성을 보려는 OTP 로그온 인증서를 두 번 클릭 합니다.  
  
    이 문제를 해결 하려면 OTP 로그온 인증서에 대 한 인증서를 구성 하 고 선택 하지 않으면 합니다 **발급 된 인증서에서 해지 정보를 포함 하지 않는** 확인란 합니다 **서버** 템플릿 탭 속성 대화 상자입니다.  
  
2.  CA 서버에서 인증 기관 MMC를 열고, 발급 CA를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다. 에 **확장** 탭 CRL 게시가 올바르게 구성 되었는지 확인 합니다.  
  


