---
title: 3 단계 OTP 용 원격 액세스 서버를 구성 합니다.
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df1e87f2-6a0f-433b-8e42-816ae75395f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5e192c062e8ecd18128109321058ddc58b6b1e4a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839844"
---
# <a name="step-3-configure-the-remote-access-server-for-otp"></a>3 단계 OTP 용 원격 액세스 서버를 구성 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016

소프트웨어 배포 토큰을 사용 하 여 RADIUS 서버를 구성한 후 통신 포트가 열려 있는지, 공유 암호를 만든, RADIUS 서버에서 생성 된 Active Directory에 해당 하는 사용자 계정 및 원격 액세스 서버에 원격 액세스 서버의 OTP를 지원 하도록 구성 해야 합니다. 그런 다음 RADIUS 인증 에이전트로 구성 되었습니다.  
  
|태스크|설명|  
|----|--------|  
|[3.1 OTP 인증 (선택 사항)에서 사용자 제외](#BKMK_Exempt)|특정 사용자에 게 OTP 인증을 사용 하 여 DirectAccess에서 제외 됩니다, 경우에 다음 예비 단계를 수행 합니다.|  
|[3.2 OTP를 지원 하도록 원격 액세스 서버를 구성 합니다.](#BKMK_Config)|원격 액세스 서버의 OTP 2 단계 인증을 지원 하도록 원격 액세스 구성을 업데이트 합니다.|  
|[3.3 추가 권한 부여에 대 한 스마트 카드](#BKMK_Smartcard)|스마트 카드의 사용과 관련 된 추가 정보입니다.|  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_Exempt"></a>3.1 OTP 인증 (선택 사항)에서 사용자 제외  
특정 사용자가 OTP 인증에서 제외 해야 하는 경우 원격 액세스 구성 하기 전에 이러한 단계를 수행 해야 합니다.  
  
> [!NOTE]  
> OTP 예외 그룹을 구성할 때 완료 하는 도메인 간에 복제 될 때까지 기다려야 합니다.  
  
#### <a name="create-user-exemption-security-group"></a>사용자 예외 보안 그룹 만들기  
  
1.  OTP 예외 목적을 위해 Active Directory에서 보안 그룹을 만듭니다.  
  
2.  보안 그룹에 OTP 인증에서 제외 해야 하는 모든 사용자를 추가 합니다.  
  
    > [!NOTE]  
    > OTP 예외 보안 그룹의 사용자 계정 및 컴퓨터 계정을 포함 해야 합니다.  
  
## <a name="BKMK_Config"></a>3.2 OTP를 지원 하도록 원격 액세스 서버를 구성 합니다.  
2 단계 인증을 사용 하도록 원격 액세스 및 OTP RADIUS 서버와 이전 섹션에서 인증서 배포를 구성 하려면 다음 단계를 사용 합니다.  
  
#### <a name="configure-remote-access-for-otp"></a>OTP에 대 한 원격 액세스 구성  
  
1.  오픈 **원격 액세스 관리** 누릅니다 **구성**합니다.  
  
2.  에 **DirectAccess 설정을** 창 아래에 있는 **2 단계-원격 액세스 서버**, 클릭 **편집**합니다.  
  
3.  클릭 **다음** 세 번 및 합니다 **인증** 섹션을 모두 선택 **2 단계 인증을** 및 **사용 하 여 OTP**, 확인 **컴퓨터 인증서를 사용 하 여** 확인란이 선택 되어 있습니다.  
  
    > [!NOTE]  
    > OTP 설정한 후 원격 액세스 서버의 OTP를 사용 하지 않도록 선택 취소 하 여 **OTP 사용**, ISAPI 및 CGI 확장을 서버에서 제거 됩니다.  
  
4.  Windows 7 지원이 필요한 경우 선택 합니다 **DirectAccess를 통한 연결을 사용 하도록 설정 하는 Windows 7 클라이언트 컴퓨터** 확인란 합니다. 참고: 계획 섹션에서 설명 했 듯이 Windows 7 클라이언트 DCA 2.0 OTP 사용 하 여 DirectAccess를 지원 하기 위해 설치 해야 합니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  에 **OTP RADIUS 서버** 섹션을 두 번 클릭 하 고 빈 **서버 이름** 필드입니다.  
  
7.  에 **RADIUS 서버 추가** 대화 상자에서에서 RADIUS 서버의 이름을 입력 합니다 **서버 이름** 필드입니다. 클릭 **변경** 옆에 **공유 비밀** 필드를 제거한에서 RADIUS 서버를 구성할 때 사용한 동일한 암호를 입력 합니다 **새 암호** 및  **새 암호 확인** 필드입니다. 클릭 **확인** 을 두 번 클릭 **다음**합니다.  
  
    > [!NOTE]  
    > RADIUS 서버는 원격 액세스 서버를 다른 도메인에 있으면 해당 **서버 이름** 필드는 RADIUS 서버의 FQDN을 지정 해야 합니다.  
  
8.  에 **OTP CA 서버** 클릭 하 여 OTP 클라이언트 인증 인증서의 등록을 위해 사용할 CA 서버를 선택 하는 섹션 **추가**합니다. **다음**을 클릭합니다.  
  
9. 에 **OTP 인증서 템플릿을** 섹션 클릭 **찾아보기** OTP 인증을 위해 발급 된 인증서를 등록에 사용 된 인증서 템플릿을 선택 합니다.  
  
    > [!NOTE]  
    > "발급 된 인증서에서 해지 정보를 포함지 않습니다" 옵션 없이 회사 CA에서 발급 한 OTP 인증서에 대 한 인증서 템플릿을 구성 되어야 합니다. 인증서 템플릿 만드는 동안이 옵션을 선택 하면 OTP 클라이언트 컴퓨터는 제대로 로그온에 실패 합니다.  
  
    클릭 **찾아보기** OTP 인증서 등록 요청을 서명 하려면 원격 액세스 서버에서 사용 된 인증서를 등록 하는 데 인증서 템플릿을 선택 합니다. **확인**을 클릭합니다. **다음**을 클릭합니다.  
  
10. Directaccess OTP 사용 하 여 특정 사용자를 대상 필요한 경우 그런 다음 합니다 **OTP 예외** 선택 섹션 **2 단계 인증을 사용 하 여 인증을 지정 된 보안 그룹의 사용자는 필요 하지 않습니다** . 클릭 **보안 그룹** OTP 예외에 대해 생성 된 보안 그룹을 선택 합니다.  
  
11. 에 **원격 액세스 서버 설치** 페이지 **마침**합니다.  
  
12. 에 **DirectAccess 설정을** 창 아래에 있는 **3 단계-인프라 서버**, 클릭 **편집**합니다.  
  
13. 클릭 **다음** 을 두 번 및 합니다 **관리** 섹션 두 번 클릭 합니다 **관리 서버** 필드.  
  
14. 입력 된 **컴퓨터 이름** 또는 **주소** OTP 인증서를 발급 하 고 클릭 하도록 구성 된 CA 서버의 **확인**합니다.  
  
15. 에 **원격 액세스 설정** windows 클릭 **마침**합니다.  
  
16. 클릭 **완료** 에 **DirectAccess 전문가 마법사**합니다.  
  
17. 에 **원격 액세스 검토** 대화 상자 클릭 **적용**, DirectAccess 정책을 업데이트할, 대기 및 클릭 **닫기**합니다.  
  
18. 에 **시작** 화면에서 입력**powershell.exe**를 마우스 오른쪽 단추로 클릭 **powershell**, 클릭 **고급**를 클릭 하 고 **으로 실행 관리자**합니다. **사용자 계정 컨트롤** 대화 상자가 나타나면 원하는 작업이 표시되었는지 확인한 다음 **예**를 클릭합니다.  
  
19. Windows PowerShell 창에서 입력 **gpupdate /force** ENTER 키를 누릅니다.  
  
원격 액세스 PowerShell 명령을 사용 하 여 otp 구성:  
  
![Windows PowerShell](../../../../media/Step-3-Configure-the-Remote-Access-Server-for-OTP/PowerShellLogoSmall.gif)**Windows PowerShell 해당 명령**  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
현재 컴퓨터 인증서 인증을 사용 하는 배포에서 2 단계 인증을 사용 하려면 원격 액세스를 구성 합니다.  
  
```  
Set-DAServer -UserAuthentication TwoFactor  
```  
  
다음 설정을 사용 하 여 OTP 인증을 사용 하도록 원격 액세스를 구성 합니다.  
  
-   OTP 서버를 이름이 OTP.corp.contoso.com입니다.  
  
-   CA 서버 이름이 APP1.corp.contoso.com\corp-APP1-CA1입니다.  
  
-   인증서 템플릿 이름이 DAOTPLogon OTP 인증을 위해 발급 된 인증서를 등록에 사용 되는입니다.  
  
-   OTP 인증서 등록 요청을 서명 하는 원격 액세스 서버에서 사용 하는 등록 기관 인증서를 등록 하려면 DAOTPRA 라는 이름의 인증서 템플릿을 사용 합니다.  
  
```  
Enable-DAOtpAuthentication -CertificateTemplateName 'DAOTPLogon' -SigningCertificateTemplateName 'DAOTPRA' -CAServer @('APP1.corp.contoso.com\corp-APP1-CA1') -RadiusServer OTP.corp.contoso.com -SharedSecret Abcd123$  
```  
  
PowerShell 명령을 실행 한 후 12-19 OTP를 지원 하도록 원격 액세스 서버를 구성 하는 이전 절차에서 단계를 완료 합니다.  
  
> [!NOTE]  
> 진입점을 추가 하기 전에 원격 액세스 서버의 OTP 설정을 적용 확인 해야 합니다.  
  
## <a name="BKMK_Smartcard"></a>3.3 추가 권한 부여에 대 한 스마트 카드  
원격 액세스 설치 마법사의 2 단계 인증 페이지에서 내부 네트워크에 대 한 액세스에 대 한 스마트 카드 사용을 요구할 수 있습니다. 이 옵션을 선택 하면 원격 액세스 설치 마법사는 스마트 카드를 사용 하 여 터널 모드 인증을 요구 하도록 DirectAccess 서버에서 인트라넷 터널에 대 한 IPsec 연결 보안 규칙을 구성 합니다. 터널 모드 인증에는 컴퓨터만 승인 되도록 지정할 수 있습니다 또는 사용자가 인바운드 터널을 설정할 수 있습니다.  
  
스마트 카드 IPsec 터널 모드 인증을 사용 하 여 인트라넷 터널에 대 한를 사용 하려면 스마트 카드 인프라를 사용 하 여 공개 키 인프라 (PKI)를 배포 해야 합니다.  
  
DirectAccess 클라이언트는 스마트 카드를 사용 하는 인트라넷에 대 한 액세스를 하기 때문에 사용할 수도 있습니다 인증 메커니즘 보증, Windows Server 2008 R2의 기능에 따라 프린터, 파일 및 폴더 등의 리소스에 대 한 액세스를 제어 하는 스마트 카드 기반 인증서를 사용 하 여 로그온 한 사용자. 인증 메커니즘 보증에는 Windows Server 2008 R2의 도메인 기능 수준이 필요합니다.  
  
### <a name="allowing-access-for-users-with-unusable-smart-cards"></a>스마트 카드를 사용할 수 없는 사용자에 대 한 액세스를 허용합니다.  
사용할 수 없는 경우 스마트 카드를 사용 하 여 사용자에 대 한 임시 액세스를 허용 하려면 다음을 수행 합니다.  
  
1.  일시적으로 해당 스마트 카드를 사용할 수 없는 사용자의 사용자 계정을 포함 하도록 Active Directory 보안 그룹을 만듭니다.  
  
2.  DirectAccess 서버의 그룹 정책 개체에 대 한 IPsec 터널 권한 부여에 대 한 전역 IPsec 설정을 구성 하 고 권한이 있는 사용자 목록을 Active Directory 보안 그룹을 추가 합니다.  
  
에 스마트 카드를 사용할 수 없는 사용자에 게 액세스 권한을 부여 하려면 일시적으로 사용자 계정 Active Directory 보안 그룹에 추가 합니다. 스마트 카드를 사용할 때 사용자 계정 그룹에서 제거 합니다.  
  
### <a name="under-the-covers-smart-card-authorization"></a>내부적: 스마트 카드 인증  
스마트 카드 인증 특정 Kerberos 기반 보안 식별자 (SID)에 대 한 DirectAccess 서버의 인트라넷 터널 연결 보안 규칙의 터널 모드 인증을 사용 하 여 작동 합니다. 스마트 카드 인증 기반 스마트 카드 로그온에 매핑되는 잘 알려진 SID (S-1-5-65-1)입니다. 이 SID는 DirectAccess 클라이언트의 Kerberos 토큰에 표시 되며, "이 조직 인증서로" 전역 IPsec에서 구성 된 경우 터널 모드 권한 부여 설정으로 참조 됩니다.  
  
DirectAccess 설치 마법사의 2 단계에서에서 스마트 카드 인증을 사용 하도록 설정 하면 DirectAccess 설치 마법사를 DirectAccess 서버 그룹 정책 개체에 대 한이 SID를 사용 하 여 전역 IPsec 터널 모드 권한 부여 설정을 구성 합니다. 고급 보안이 스냅인 DirectAccess 서버 그룹 정책 개체에 대 한 Windows 방화벽에서이 구성을 보려면 다음을 수행 합니다.  
  
1.  고급 보안이 포함 된 Windows 방화벽을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 합니다.  
  
2.  IPsec 터널 권한 부여에서 IPsec 설정 탭에서 사용자 지정을 클릭 합니다.  
  
3.  사용자 탭을 클릭 합니다. "NT AUTHORITY\This 조직 인증서" 권한 있는 사용자로 표시 됩니다.  
  


