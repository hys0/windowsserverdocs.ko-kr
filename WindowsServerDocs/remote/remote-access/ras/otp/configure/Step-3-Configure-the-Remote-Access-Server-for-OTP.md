---
title: 3 단계 OTP에 대 한 원격 액세스 서버 구성
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: df1e87f2-6a0f-433b-8e42-816ae75395f9
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 98de4a1e673065e0b759186a7a53ce45675302be
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858216"
---
# <a name="step-3-configure-the-remote-access-server-for-otp"></a>3 단계 OTP에 대 한 원격 액세스 서버 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

소프트웨어 배포 토큰을 사용 하 여 RADIUS 서버를 구성 하 고 나면 통신 포트가 열려, 공유 암호가 생성 되 고, Active Directory에 해당 하는 사용자 계정이 RADIUS 서버에서 생성 되었으며, 원격 액세스 서버에 RADIUS 인증 에이전트로 구성 된 후 OTP를 지원 하도록 원격 액세스 서버를 구성 해야 합니다.  
  
|작업|설명|  
|----|--------|  
|[3.1 OTP 인증에서 사용자를 제외 합니다 (선택 사항).](#BKMK_Exempt)|OTP 인증을 사용 하 여 DirectAccess에서 특정 사용자가 제외 되는 경우에는 다음 예비 단계를 따르세요.|  
|[3.2 OTP를 지원 하도록 원격 액세스 서버 구성](#BKMK_Config)|원격 액세스 서버에서 OTP 2 단계 인증을 지원 하도록 원격 액세스 구성을 업데이트 합니다.|  
|[3.3 추가 권한 부여에 대 한 스마트 카드](#BKMK_Smartcard)|스마트 카드 사용과 관련 된 추가 정보입니다.|  
  
> [!NOTE]  
> 이 항목에는 설명된 일부 절차를 자동화하는 데 사용할 수 있는 예제 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="31-exempt-users-from-otp-authentication-optional"></a><a name="BKMK_Exempt"></a>3.1 OTP 인증에서 사용자를 제외 합니다 (선택 사항).  
특정 사용자가 OTP 인증에서 제외 되는 경우 원격 액세스 구성 전에 다음 단계를 수행 해야 합니다.  
  
> [!NOTE]  
> OTP 예외 그룹을 구성할 때 도메인 간 복제가 완료 될 때까지 기다려야 합니다.  
  
#### <a name="create-user-exemption-security-group"></a>사용자 예외 보안 그룹 만들기  
  
1.  목적 OTP 예외에 대 한 Active Directory에 보안 그룹을 만듭니다.  
  
2.  OTP 인증에서 제외 될 모든 사용자를 보안 그룹에 추가 합니다.  
  
    > [!NOTE]  
    > OTP 예외 보안 그룹에는 컴퓨터 계정이 아닌 사용자 계정만 포함 해야 합니다.  
  
## <a name="32-configure-the-remote-access-server-to-support-otp"></a><a name="BKMK_Config"></a>3.2 OTP를 지원 하도록 원격 액세스 서버 구성  
위의 섹션에서 RADIUS 서버 및 인증서 배포와 함께 2 단계 인증 및 OTP를 사용 하도록 원격 액세스를 구성 하려면 다음 단계를 사용 합니다.  
  
#### <a name="configure-remote-access-for-otp"></a>OTP에 대 한 원격 액세스 구성  
  
1.  **원격 액세스 관리** 를 열고 **구성**을 클릭 합니다.  
  
2.  **DirectAccess 설정** 창의 **2 단계-원격 액세스 서버**에서 **편집**을 클릭 합니다.  
  
3.  **다음** 을 세 번 클릭 하 고 **인증** 섹션에서 **2 단계 인증** 을 선택 하 고 **OTP를 사용**하 고 **컴퓨터 인증서 사용** 이 선택 되어 있는지 확인 합니다.  
  
    > [!NOTE]  
    > 원격 액세스 서버에서 OTP를 사용 하도록 설정한 후 otp **사용**을 선택 취소 하 여 otp를 사용 하지 않도록 설정 하면 서버에서 ISAPI 및 CGI 확장이 제거 됩니다.  
  
4.  Windows 7 지원이 필요한 경우 **windows 7 클라이언트 컴퓨터에서 DirectAccess를 통해 연결 하도록 설정** 확인란을 선택 합니다. 참고: 계획 섹션에 설명 된 대로, OTP를 사용 하 여 DirectAccess를 지원 하려면 Windows 7 클라이언트에 DCA 2.0이 설치 되어 있어야 합니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  **OTP RADIUS 서버** 섹션에서 빈 **서버 이름** 필드를 두 번 클릭 합니다.  
  
7.  **Radius 서버 추가** 대화 상자에서 **서버 이름** 필드에 radius 서버 이름을 입력 합니다. **공유 암호** 필드 옆의 **변경** 을 클릭 하 고 **새** 암호 및 **새 암호 확인** 필드에서 RADIUS 서버를 구성할 때 사용한 것과 동일한 암호를 입력 합니다. **확인** 을 두 번 클릭 하 고 **다음**을 클릭 합니다.  
  
    > [!NOTE]  
    > RADIUS 서버가 원격 액세스 서버와 다른 도메인에 있는 경우 **서버 이름** 필드는 RADIUS 서버의 FQDN을 지정 해야 합니다.  
  
8.  **OTP CA 서버** 섹션에서 otp 클라이언트 인증 인증서를 등록 하는 데 사용할 CA 서버를 선택 하 고 **추가**를 클릭 합니다. **다음**을 클릭합니다.  
  
9. **Otp 인증서 템플릿** 섹션에서 **찾아보기** 를 클릭 하 여 otp 인증에 대해 발급 된 인증서를 등록 하는 데 사용 되는 인증서 템플릿을 선택 합니다.  
  
    > [!NOTE]  
    > 회사 CA에서 발급 한 OTP 인증서의 인증서 템플릿은 "발급 된 인증서에 해지 정보 포함 안 함" 옵션을 사용 하지 않고 구성 해야 합니다. 인증서 템플릿을 만드는 동안이 옵션을 선택 하면 OTP 클라이언트 컴퓨터가 제대로 로그온 하지 못합니다.  
  
    **찾아보기** 를 클릭 하 여 원격 액세스 서버에서 OTP 인증서 등록 요청에 서명 하는 데 사용 하는 인증서를 등록 하는 데 사용 되는 인증서 템플릿을 선택 합니다. **확인**을 클릭합니다. **다음**을 클릭합니다.  
  
10. OTP를 사용 하 여 DirectAccess에서 제외 특정 사용자가 필요한 경우 **Otp 예외** 섹션에서 **지정 된 보안 그룹의 사용자가 2 단계 인증을 사용 하 여 인증**하지 않아도 됨을 선택 합니다. **보안 그룹** 을 클릭 하 고 OTP 예외에 대해 만든 보안 그룹을 선택 합니다.  
  
11. **원격 액세스 서버 설치** 페이지에서 **마침**을 클릭 합니다.  
  
12. **DirectAccess 설정** 창의 **3 단계-인프라 서버**에서 **편집**을 클릭 합니다.  
  
13. **다음** 을 두 번 클릭 하 고 **관리** 섹션에서 **관리 서버** 필드를 두 번 클릭 합니다.  
  
14. OTP 인증서를 발급 하도록 구성 된 CA 서버의 **컴퓨터 이름** 또는 **주소** 를 입력 하 고 **확인**을 클릭 합니다.  
  
15. **원격 액세스 설정** 창에서 **마침**을 클릭 합니다.  
  
16. **DirectAccess 전문가 마법사**에서 **마침** 을 클릭 합니다.  
  
17. **원격 액세스 검토** 대화 상자에서 **적용**을 클릭 하 고, DirectAccess 정책이 업데이트 될 때까지 기다린 후 **닫기**를 클릭 합니다.  
  
18. **시작** 화면에서**powershell**을 입력 하 고 **powershell**을 마우스 오른쪽 단추로 클릭 한 다음 **고급**을 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다. **사용자 계정 컨트롤** 대화 상자가 표시되면 원하는 작업이 표시되어 있는지 확인하고 **예**를 클릭합니다.  
  
19. Windows PowerShell 창에서 **gpupdate/force** 를 입력 하 고 enter 키를 누릅니다.  
  
PowerShell 명령을 사용 하 여 OTP에 대 한 원격 액세스를 구성 하려면:  
  
![Windows PowerShell](../../../../media/Step-3-Configure-the-Remote-Access-Server-for-OTP/PowerShellLogoSmall.gif)**Windows powershell 해당 명령**  
  
다음 Windows PowerShell cmdlet은 이전 절차와 동일한 기능을 수행합니다. 서식 조건 때문에 각 cmdlet이 여러 줄로 자동 줄 바꿈되어 표시되더라도 한 줄에 입력합니다.  
  
현재 컴퓨터 인증서 인증을 사용 하는 배포에서 2 단계 인증을 사용 하도록 원격 액세스를 구성 하려면:  
  
```  
Set-DAServer -UserAuthentication TwoFactor  
```  
  
다음 설정을 사용 하 여 OTP 인증을 사용 하도록 원격 액세스를 구성 하려면:  
  
-   OTP.corp.contoso.com 라는 OTP 서버  
  
-   APP1 라는 CA 서버. com\corp-APP1-CA1.  
  
-   OTP 인증에 대해 발급 된 인증서를 등록 하는 데 사용 되는 DAOTPLogon 라는 인증서 템플릿입니다.  
  
-   OTP 인증서 등록 요청을 서명 하기 위해 원격 액세스 서버에서 사용 하는 등록 기관 인증서를 등록 하는 데 사용 되는 DAOTPRA 라는 인증서 템플릿입니다.  
  
```  
Enable-DAOtpAuthentication -CertificateTemplateName 'DAOTPLogon' -SigningCertificateTemplateName 'DAOTPRA' -CAServer @('APP1.corp.contoso.com\corp-APP1-CA1') -RadiusServer OTP.corp.contoso.com -SharedSecret Abcd123$  
```  
  
PowerShell 명령을 실행 한 후 이전 절차의 12-19 단계를 완료 하 여 OTP를 지원 하도록 원격 액세스 서버를 구성 합니다.  
  
> [!NOTE]  
> 진입점을 추가 하기 전에 원격 액세스 서버에 OTP 설정을 적용 했는지 확인 해야 합니다.  
  
## <a name="33-smart-cards-for-additional-authorization"></a><a name="BKMK_Smartcard"></a>3.3 추가 권한 부여에 대 한 스마트 카드  
원격 액세스 설치 마법사에서 2 단계의 인증 페이지에서 내부 네트워크에 액세스 하기 위해 스마트 카드를 사용 하도록 요구할 수 있습니다. 이 옵션을 선택 하면 원격 액세스 설치 마법사가 DirectAccess 서버에서 인트라넷 터널에 대 한 IPsec 연결 보안 규칙을 구성 하 여 스마트 카드를 통한 터널 모드 인증을 요구 합니다. 터널 모드 권한 부여를 사용 하면 권한 있는 컴퓨터 또는 사용자만 인바운드 터널을 설정할 수 있도록 지정할 수 있습니다.  
  
인트라넷 터널에 대해 IPsec 터널 모드 인증을 사용 하는 스마트 카드를 사용 하려면 스마트 카드 인프라를 사용 하 여 PKI (공개 키 인프라)를 배포 해야 합니다.  
  
DirectAccess 클라이언트는 인트라넷에 액세스 하기 위해 스마트 카드를 사용 하기 때문에 Windows Server 2008 r 2의 기능인 인증 메커니즘 보증을 사용 하 여 파일, 폴더 및 프린터와 같은 리소스에 대 한 액세스를 제어할 수도 있습니다. 사용자가 스마트 카드 기반 인증서를 사용 하 여 로그온 했습니다. 인증 메커니즘 보증에는 Windows Server 2008 r 2의 도메인 기능 수준이 필요 합니다.  
  
### <a name="allowing-access-for-users-with-unusable-smart-cards"></a>사용할 수 없는 스마트 카드를 사용 하는 사용자에 대 한 액세스 허용  
사용할 수 없는 스마트 카드를 사용 하는 사용자에 대 한 임시 액세스를 허용 하려면 다음을 수행 합니다.  
  
1.  해당 스마트 카드를 일시적으로 사용할 수 없는 사용자의 사용자 계정을 포함 하는 Active Directory 보안 그룹을 만듭니다.  
  
2.  DirectAccess 서버 그룹 정책 개체의 경우 IPsec 터널 권한 부여에 대 한 글로벌 IPsec 설정을 구성 하 고 권한 있는 사용자 목록에 Active Directory 보안 그룹을 추가 합니다.  
  
스마트 카드를 사용할 수 없는 사용자에 게 액세스 권한을 부여 하려면 Active Directory 보안 그룹에 해당 사용자 계정을 임시로 추가 합니다. 스마트 카드를 사용할 수 있는 경우 그룹에서 사용자 계정을 제거 합니다.  
  
### <a name="under-the-covers-smart-card-authorization"></a>커버: 스마트 카드 권한 부여  
스마트 카드 권한 부여는 특정 Kerberos 기반 SID (보안 식별자)에 대 한 DirectAccess 서버의 인트라넷 터널 연결 보안 규칙에서 터널 모드 권한 부여를 사용 하도록 설정 하는 방식으로 작동 합니다. 스마트 카드 인증의 경우,이는 스마트 카드 기반 로그온에 매핑되는 잘 알려진 SID (S-1-5-65-1)입니다. 이 SID는 DirectAccess 클라이언트의 Kerberos 토큰에 존재 하며, 전역 IPsec 터널 모드 권한 부여 설정에서 구성 된 경우 "이 조직 인증서"로 지칭 됩니다.  
  
DirectAccess 설치 마법사의 2 단계에서 스마트 카드 인증을 사용 하도록 설정 하는 경우 directaccess 설치 마법사는 DirectAccess 서버 그룹 정책 개체에 대해이 SID를 사용 하 여 전역 IPsec 터널 모드 권한 부여 설정을 구성 합니다. DirectAccess 서버 그룹 정책 개체에 대 한 고급 보안이 설정 된 Windows 방화벽 스냅인에서이 구성을 보려면 다음을 수행 합니다.  
  
1.  고급 보안이 포함 된 Windows 방화벽을 마우스 오른쪽 단추로 클릭 한 다음 속성을 클릭 합니다.  
  
2.  Ipsec 설정 탭의 IPsec 터널 권한 부여에서 사용자 지정을 클릭 합니다.  
  
3.  사용자 탭을 클릭 합니다. 권한 있는 사용자로 "NT AUTHORITY\This 조직 인증서"가 표시 되어야 합니다.  
  


