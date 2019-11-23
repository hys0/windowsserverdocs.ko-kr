---
title: 인증 문제 해결
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71307757-f8f4-4f82-b8b3-ffd4fd8c5d6d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73fe8458910cbe7dfaf000a6546bcba9263a9683
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404303"
---
# <a name="troubleshooting-authentication-issues"></a>인증 문제 해결

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 OTP 인증을 사용 하 여 DirectAccess에 연결 하려고 할 때 발생 하는 문제와 관련 된 문제에 대 한 문제 해결 정보를 포함 합니다. DirectAccerss OTP 관련 이벤트는 **응용 프로그램 및 서비스 Logs/Microsoft/Windows/OtpCredentialProvider**에서 이벤트 뷰어의 클라이언트 컴퓨터에 기록 됩니다. DirectAccess OTP와 관련 된 문제를 해결할 때이 로그가 활성화 되어 있는지 확인 합니다.  
  
## <a name="failed-to-access-the-ca-that-issues-otp-certificates"></a>OTP 인증서를 발급 하는 CA에 액세스 하지 못했습니다.  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. 사용자 <username>에 대해 OTP 인증서를 등록 하지 못했습니다 < CA_name >, 요청 실패, 가능한 실패 이유: CA 서버 이름을 확인할 수 없거나, 첫 번째 DirectAccess 터널을 통해 CA 서버에 액세스할 수 없거나, CA 서버에 대 한 연결을 설정할 수 없습니다.  
  
**가능한 원인**  
  
사용자가 유효한 일회용 암호를 제공 하 고 DirectAccess 서버에서 인증서 요청을 서명 했습니다. 그러나 클라이언트 컴퓨터는 OTP 인증서를 발급 하는 CA에 연결 하 여 등록 프로세스를 완료할 수 없습니다.  
  
**해결 방법**  
  
DirectAccess 서버에서 다음 Windows PowerShell 명령을 실행 합니다.  
  
1.  구성 된 OTP 발급 Ca 목록을 가져오고 ' CAServer '의 값을 확인 합니다. `Get-DAOtpAuthentication`  
  
2.  Ca가 관리 서버로 구성 되어 있는지 확인 합니다. `Get-DAMgmtServer -Type All`  
  
3.  클라이언트 컴퓨터가 인프라 터널을 설정 했는지 확인 합니다. 고급 보안이 설정 된 Windows 방화벽 콘솔에서 **모니터링/보안 연결**을 확장 하 고, **주 모드**를 클릭 하 고, IPsec 보안 연결이 DirectAccess 구성의 올바른 원격 주소와 함께 표시 되는지 확인 합니다.  
  
## <a name="directaccess-server-connectivity-issues"></a>DirectAccess 서버 연결 문제  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)  
  
다음 오류 중 하나입니다.  
  
-   기본 경로 < OTP_authentication_path > 및 포트 < OTP_authentication_port >를 사용 하 여 원격 액세스 서버 < DirectAccess_server_hostname >에 대 한 연결을 설정할 수 없습니다. 오류 코드: internal_error_code >를 < 합니다.  
  
-   기본 경로 < OTP_authentication_path > 및 포트 < OTP_authentication_port >를 사용 하 여 사용자 자격 증명을 원격 액세스 서버 < DirectAccess_server_hostname >로 전송할 수 없습니다. 오류 코드: internal_error_code >를 < 합니다.  
  
-   기본 경로 < OTP_authentication_path > 및 포트 < OTP_authentication_port >를 사용 하 여 원격 액세스 서버 < DirectAccess_server_hostname >에서 응답을 받지 못했습니다. 오류 코드: internal_error_code >를 < 합니다.  
  
**가능한 원인**  
  
클라이언트 컴퓨터는 네트워크 문제 또는 DirectAccess 서버의 잘못 구성 된 IIS 서버 때문에 인터넷을 통해 DirectAccess 서버에 액세스할 수 없습니다.  
  
**해결 방법**  
  
클라이언트 컴퓨터의 인터넷 연결이 작동 중인지 확인 하 고 인터넷을 통해 DirectAccess 서비스가 실행 중 이며 액세스할 수 있는지 확인 합니다.  
  
## <a name="failed-to-enroll-for-the-directaccess-otp-logon-certificate"></a>DirectAccess OTP 로그온 인증서를 등록 하지 못했습니다.  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. CA < CA_name >에서 인증서를 등록 하지 못했습니다. OTP 서명 인증서에서 예상한 대로 요청이 서명 되지 않았거나 사용자에 게 등록할 수 있는 권한이 없습니다.  
  
**가능한 원인**  
  
사용자가 제공한 일회용 암호가 올바르지만 발급 된 CA (인증 기관)가 OTP 로그온 인증서를 발급 하는 것을 거부 했습니다. 인증서 요청이 올바른 EKU (OTP 등록 기관 응용 프로그램 정책)로 올바르게 서명 되지 않았거나 사용자에 게 DA OTP 템플릿에 대 한 "등록" 권한이 없는 것일 수 있습니다.  
  
**해결 방법**  
  
DirectAccess OTP 사용자에 게 DirectAccess OTP 로그온 인증서에 대 한 등록 권한이 있는지 확인 하 고 적절 한 "응용 프로그램 정책"이 DA OTP 등록 기관 서명 템플릿에 포함 되어 있는지 확인 합니다. 또한 원격 액세스 서버에서 DirectAccess 등록 기관 인증서가 유효한 지 확인 합니다. 3\.2 OTP 인증서 템플릿 계획 및 3.3 등록 기관 인증서 계획을 참조 하세요.  
  
## <a name="missing-or-invalid-computer-account-certificate"></a>컴퓨터 계정 인증서가 없거나 잘못 되었습니다.  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다.  OTP에 필요한 컴퓨터 인증서를 로컬 컴퓨터 인증서 저장소에서 찾을 수 없으므로 OTP 인증을 완료할 수 없습니다.  
  
**가능한 원인**  
  
Directaccess OTP 인증에는 DirectAccess 서버와의 SSL 연결을 설정 하기 위해 클라이언트 컴퓨터 인증서가 필요 합니다. 그러나 클라이언트 컴퓨터 인증서가 없거나 유효 하지 않습니다. 예를 들어 인증서가 만료 된 경우입니다.  
  
**해결 방법**  
  
컴퓨터 인증서가 존재 하 고 유효한 지 확인 합니다.  
  
1.  클라이언트 컴퓨터의 MMC 인증서 콘솔에서 로컬 컴퓨터 계정으로 **개인/인증서**를 엽니다.  
  
2.  컴퓨터 이름과 일치 하는 인증서가 발급 되었는지 확인 하 고 인증서를 두 번 클릭 합니다.  
  
3.  **인증서 대화 상자** 에서 인증서 **경로** 탭의 **인증서 상태**아래에 "이 인증서가 정상입니다." 라는 메시지가 표시 되는지 확인 합니다.  
  
유효한 인증서를 찾을 수 없는 경우 유효 하지 않은 인증서 (있는 경우)를 삭제 하 고 관리자 권한 명령 프롬프트에서 `gpupdate /Force`를 실행 하거나 클라이언트 컴퓨터를 다시 시작 하 여 컴퓨터 인증서를 다시 등록 합니다.  
  
## <a name="missing-ca-that-issues-otp-certificates"></a>OTP 인증서를 발급 하는 누락 된 CA  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. DA 서버가 발급 CA의 주소를 반환 하지 않았으므로 OTP 인증을 완료할 수 없습니다.  
  
**가능한 원인**  
  
OTP 인증서를 발급 하는 Ca가 없거나 OTP 인증서를 발급 하는 구성 된 모든 Ca가 응답 하지 않습니다.  
  
**해결 방법**  
  
1.  다음 명령을 사용 하 여 OTP 인증서를 발급 하는 Ca 목록을 가져옵니다 (CA 이름이 CAServer에 표시 됨). `Get-DAOtpAuthentication`.  
  
2.  구성 된 Ca가 없는 경우:  
  
    1.  명령 `Set-DAOtpAuthentication` 또는 원격 액세스 관리 콘솔을 사용 하 여 DirectAccess OTP 로그온 인증서를 발급 하는 Ca를 구성 합니다.  
  
    2.  새 구성을 적용 하 고 클라이언트 컴퓨터를 다시 시작 하거나 관리자 권한 명령 프롬프트에서 `gpupdate /Force`를 실행 하 여 클라이언트에서 DirectAccess GPO 설정을 새로 고치도록 합니다.  
  
3.  구성 된 Ca가 있는 경우 온라인 상태이 고 등록 요청에 응답 하는지 확인 합니다.  
  
## <a name="misconfigured-directaccess-server-address"></a>잘못 구성 되어 있는 DirectAccess 서버 주소  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. OTP 인증은 예상 대로 완료할 수 없습니다. 원격 액세스 서버의 이름이 나 주소를 확인할 수 없습니다.  오류 코드: error_code >를 < 합니다. 서버 관리자가 DirectAccess 설정의 유효성을 검사 해야 합니다.  
  
**가능한 원인**  
  
DirectAccess 서버의 주소가 제대로 구성 되지 않았습니다.  
  
**해결 방법**  
  
`Get-DirectAccess`를 사용 하 여 구성 된 DirectAccess 서버 주소를 확인 하 고 잘못 구성 된 경우 주소를 수정 합니다.  
  
관리자 권한 명령 프롬프트에서 `gpupdate /force`를 실행 하거나 클라이언트 컴퓨터를 다시 시작 하 여 최신 설정이 클라이언트 컴퓨터에 배포 되어 있는지 확인 합니다.  
  
## <a name="failed-to-generate-the-otp-logon-certificate-request"></a>OTP 로그온 인증서 요청을 생성 하지 못했습니다.  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. OTP 인증에 대 한 인증서 요청을 초기화할 수 없습니다. 개인 키를 생성할 수 없거나 사용자 <username>가 도메인 컨트롤러에서 인증서 템플릿 < OTP_template_name >에 액세스할 수 없습니다.  
  
**가능한 원인**  
  
이 오류의 가능한 원인은 두 가지입니다.  
  
-   사용자에 게 OTP 로그온 템플릿을 읽을 수 있는 권한이 없습니다.  
  
-   네트워크 문제로 인해 사용자의 컴퓨터에서 도메인 컨트롤러에 액세스할 수 없습니다.  
  
**해결 방법**  
  
-   OTP 로그온 템플릿의 권한 설정을 검토 하 고 DirectAccess OTP에 대해 프로 비전 된 모든 사용자에 게 ' 읽기 ' 권한이 있는지 확인 합니다.  
  
-   도메인 컨트롤러를 관리 서버로 구성 하 고 클라이언트 컴퓨터가 인프라 터널을 통해 도메인 컨트롤러에 연결할 수 있는지 확인 합니다. 3\.2 OTP 인증서 템플릿 계획을 참조 하세요.  
  
## <a name="no-connection-to-the-domain-controller"></a>도메인 컨트롤러에 대 한 연결 없음  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. OTP 인증을 위해 도메인 컨트롤러와의 연결을 설정할 수 없습니다. 오류 코드: error_code >를 < 합니다.  
  
**가능한 원인**  
  
이 오류의 가능한 원인은 두 가지입니다.  
  
-   사용자의 컴퓨터가 네트워크에 연결 되어 있지 않습니다.  
  
-   도메인 컨트롤러는 인프라 터널을 통해 액세스할 수 없습니다.  
  
**해결 방법**  
  
-   PowerShell 프롬프트에서 다음 명령을 실행 하 여 도메인 컨트롤러가 관리 서버로 구성 되어 있는지 확인 합니다. `Get-DAMgmtServer -Type All`합니다.  
  
-   클라이언트 컴퓨터가 인프라 터널을 통해 도메인 컨트롤러에 연결할 수 있는지 확인 합니다.  
  
## <a name="otp-provider-requires-challengeresponse"></a>OTP 공급자에 게 챌린지/응답이 필요 합니다.  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. 사용자 (<username>)에 대해 원격 액세스 서버 (< DirectAccess_server_name >)를 사용 하는 OTP 인증에는 사용자의 과제가 필요 합니다.  
  
**가능한 원인**  
  
사용 되는 OTP 공급자를 사용 하려면 사용자가 RADIUS 챌린지/응답 교환 형식으로 추가 자격 증명을 제공 해야 합니다 .이는 Windows Server 2012 DirectAccess OTP에서 지원 되지 않습니다.  
  
**해결 방법**  
  
모든 시나리오에서 챌린지/응답을 요구 하지 않도록 OTP 공급자를 구성 합니다.  
  
## <a name="incorrect-otp-logon-template-used"></a>잘못 된 OTP 로그온 템플릿이 사용 됨  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. 사용자 <username> 인증서를 요청한 CA 템플릿에서 OTP 인증서를 발급 하도록 구성 되지 않았습니다.  
  
**가능한 원인**  
  
DirectAccess OTP 로그온 템플릿이 대체 되었고 클라이언트 컴퓨터가 이전 템플릿을 사용 하 여 인증을 시도 하 고 있습니다.  
  
**해결 방법**  
  
클라이언트 컴퓨터에서 다음 중 하나를 수행 하 여 최신 OTP 구성을 사용 하 고 있는지 확인 합니다.  
  
-   관리자 권한 명령 프롬프트에서 다음 명령을 실행 하 여 그룹 정책 업데이트를 적용 합니다. `gpupdate /Force`.  
  
-   클라이언트 컴퓨터를 다시 시작 합니다.  
  
## <a name="missing-otp-signing-certificate"></a>OTP 서명 인증서 누락  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)입니다. OTP 서명 인증서를 찾을 수 없습니다. OTP 인증서 등록 요청에 서명할 수 없습니다.  
  
**가능한 원인**  
  
원격 액세스 서버에서 DirectAccess OTP 서명 인증서를 찾을 수 없습니다. 따라서 사용자 인증서 요청은 원격 액세스 서버에서 서명할 수 없습니다. 서명 인증서가 없거나 서명 인증서가 만료 되어 갱신 되지 않았습니다.  
  
**해결 방법**  
  
원격 액세스 서버에서 다음 단계를 수행 합니다.  
  
1.  PowerShell cmdlet `Get-DAOtpAuthentication`를 실행 하 여 구성 된 OTP 서명 인증서 템플릿 이름을 확인 하 고 `SigningCertificateTemplateName`의 값을 검사 합니다.  
  
2.  인증서 MMC 스냅인을 사용 하 여이 템플릿에서 등록 된 올바른 인증서가 컴퓨터에 있는지 확인 합니다.  
  
3.  이러한 인증서가 없는 경우 만료 된 인증서 (있는 경우)를 삭제 하 고이 템플릿을 기반으로 새 인증서를 등록 합니다.  
  
OTP 서명 인증서 템플릿을 만들려면 3.3 등록 기관 인증서 계획을 참조 하세요.  
  
## <a name="missing-or-incorrect-upndn-for-the-user"></a>사용자의 UPN/DN이 없거나 잘못 되었습니다.  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 이벤트 로그)  
  
다음 오류 중 하나입니다.  
  
-   OTP를 사용 하 여 사용자 <username>을 인증할 수 없습니다. Active Directory의 사용자 이름에 UPN이 정의 되어 있는지 확인 합니다. 오류 코드: error_code >를 < 합니다.  
  
-   OTP를 사용 하 여 사용자 <username>을 인증할 수 없습니다. Active Directory의 사용자 이름에 대해 DN이 정의 되어 있는지 확인 합니다. 오류 코드: error_code >를 < 합니다.  
  
**받은 오류** (서버 이벤트 로그)  
  
OTP 인증에 지정 된 사용자 이름 <username> 존재 하지 않습니다.  
  
**가능한 원인**  
  
사용자 계정에 UPN (사용자 계정 이름) 또는 DN (고유 이름) 특성이 적절히 설정 되지 않았습니다. 이러한 속성은 DirectAccess OTP의 적절 한 기능을 위해 필요 합니다.  
  
**해결 방법**  
  
도메인 컨트롤러의 Active Directory 사용자 및 컴퓨터 콘솔을 사용 하 여 이러한 두 특성이 인증 사용자에 대해 올바르게 설정 되어 있는지 확인 합니다.  
  
## <a name="otp-certificate-is-not-trusted-for-login"></a>OTP 인증서를 로그인에 대해 신뢰할 수 없음  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**가능한 원인**  
  
OTP 인증서를 발급 하는 CA가 enterprise NTAuth 스토어에 없습니다. 따라서 등록 된 인증서는 로그온에 사용할 수 없습니다. 이는 도메인 간 CA 트러스트가 설정 되지 않은 다중 도메인 및 다중 포리스트 환경에서 발생할 수 있습니다.  
  
**해결 방법**  
  
OTP 인증서를 발급 하는 CA 계층 구조의 루트 인증서가 사용자가 인증을 시도 하는 도메인의 enterprise NTAuth 인증서 저장소에 설치 되어 있는지 확인 합니다.  
  
## <a name="windows-could-not-verify-user-credentials"></a>Windows에서 사용자 자격 증명을 확인할 수 없습니다.  
**시나리오**. "내부 오류로 인해 인증 하지 못했습니다." 라는 오류로 인해 사용자가 OTP를 사용 하 여 인증 하지 못했습니다.  
  
**받은 오류** (클라이언트 컴퓨터)입니다. Windows에서 자격 증명을 확인 하는 동안 문제가 발생 했습니다. 다시 시도 하거나 관리자에 게 도움을 요청 하십시오.  
  
**가능한 원인**  
  
DirectAccess OTP 로그온 인증서에 CRL이 포함 되지 않은 경우 Kerberos 인증 프로토콜이 작동 하지 않습니다. 다음 중 하나가 발생 하므로 DirectAccess OTP 로그온 인증서에 CRL이 포함 되지 않습니다.  
  
-   **발급 된 인증서에 해지 정보를 포함 하지**않음 옵션을 사용 하 여 DirectAccess OTP 로그온 템플릿이 구성 되었습니다.  
  
-   CA가 Crl을 게시 하지 않도록 구성 되어 있습니다.  
  
**해결 방법**  
  
1.  이 오류의 원인을 확인 하려면 원격 액세스 관리 콘솔의 **2 단계 원격 액세스 서버**에서 **편집**을 클릭 한 다음 **원격 액세스 서버 설치** 마법사에서 **OTP 인증서 템플릿**을 클릭 합니다. OTP 인증에 대해 발급 된 인증서를 등록 하는 데 사용 되는 인증서 템플릿을 적어 둡니다. 인증 기관 콘솔을 열고 왼쪽 창에서 **인증서 템플릿**을 클릭 한 후 OTP 로그온 인증서를 두 번 클릭 하 여 인증서 템플릿 속성을 확인 합니다.  
  
    이 문제를 해결 하려면 OTP 로그온 인증서에 대 한 인증서를 구성 하 고 템플릿 속성 대화 상자의 **서버** 탭에서 **발급 된 인증서에 해지 정보 포함 안 함** 확인란을 선택 하지 않습니다.  
  
2.  CA 서버에서 인증 기관 MMC를 열고 발급 CA를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다. **확장** 탭에서 CRL 게시가 올바르게 구성 되어 있는지 확인 합니다.  
  


