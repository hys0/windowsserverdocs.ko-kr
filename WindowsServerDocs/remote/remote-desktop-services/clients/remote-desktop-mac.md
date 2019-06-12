---
title: Mac에서 원격 데스크톱 시작
description: Mac 용 원격 데스크톱 클라이언트를 설정 하는 방법 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7afc65f8-3158-49c9-9d48-4dab1c69afba
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 10/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: a54ffd3d5596ba8c71deab668e4952da445ca12e
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804946"
---
# <a name="get-started-with-remote-desktop-on-mac"></a>Mac에서 원격 데스크톱 시작

>적용 대상: Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2016

Mac 컴퓨터에서 Windows 앱, 리소스 및 데스크톱을 사용 하 여 작동 하려면 Mac에 대 한 원격 데스크톱 클라이언트를 사용할 수 있습니다. 다음 정보를 사용 하 여 시작 하 고 확인 합니다 [FAQ](remote-desktop-client-faq.md) 질문이 있는 경우.

>[!NOTE]
> - MacOS 클라이언트에 대 한 새 릴리스에 대 한 주는지 궁금 하세요? 체크 아웃 [Mac에서 원격 데스크톱에 대 한 새로운 기능?](mac-whatsnew.md)
> - Mac 클라이언트 10.10 및 최신 macOS를 실행 하는 컴퓨터에서 실행 됩니다.
> - 이 문서의 정보는 Mac 클라이언트-Mac AppStore에서 사용할 수 있는 버전의 전체 버전에 주로 적용 됩니다. 여기서 미리 보기 앱을 다운로드 하 여 새 기능을 시험 사용할 수 있도록 합니다. [베타 클라이언트 릴리스](https://go.microsoft.com/fwlink/?LinkID=619698&clcid=0x409)합니다.

## <a name="get-the-remote-desktop-client"></a>원격 데스크톱 클라이언트
Mac에서 원격 데스크톱을 사용 하 여 시작 하려면 다음이 단계를 수행 합니다.

1. Microsoft 원격 데스크톱 클라이언트 다운로드는 [Mac 앱 스토어](https://itunes.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12)합니다.
2. [원격 연결을 허용 하도록 PC 설정](remote-desktop-client-faq.md#how-do-i-set-up-a-pc-for-remote-desktop)합니다. (이 단계를 건너뛰면 없습니다 연결한 사용자 PC에.)
3. 원격 데스크톱 연결이 나 원격 리소스를 추가 합니다. 연결을 사용 하 여 RemoteApp 프로그램, 세션 기반 데스크톱을 사용 하는 Windows PC 및 원격 리소스에 직접 연결 하거나 가상 데스크톱에 온-프레미스 게시 된 RemoteApp 및 데스크톱 연결을 사용 합니다. 이 기능은 일반적으로 기업 환경에서 사용할 수 있습니다.

## <a name="what-about-the-mac-beta-client"></a>Mac 베타 클라이언트의 경우는 어떻습니까?
에서는 새로운 기능 HockeyApp에서 미리 보기 채널에서 테스트할 수 있습니다. 체크 아웃 하 시겠습니까? 로 이동 [Mac 용 Microsoft 원격 데스크톱](https://go.microsoft.com/fwlink/?LinkID=619698) 누릅니다 **다운로드**합니다. 베타 클라이언트를 다운로드 하려면 HockeyApp에 계정이 나 로그인을 만들 필요가 없습니다.

클라이언트가 이미 있는 경우 최신 버전을 확인 하는 업데이트를 확인할 수 있습니다. 베타 클라이언트에서 클릭 **Microsoft 원격 데스크톱 베타** 위쪽과 클릭 한 다음 **업데이트 확인**합니다. 

## <a name="add-a-remote-desktop-connection"></a>원격 데스크톱 연결을 추가 합니다.
원격 데스크톱 연결을 만들려면:

1. 연결 센터에서 클릭 **+** 를 클릭 하 고 **Desktop**합니다.
2. 다음 정보를 입력 합니다.
   - **PC 이름** -컴퓨터의 이름입니다.
      - Windows 컴퓨터 이름일 수 있습니다 (에 **시스템** 설정), 도메인 이름 또는 IP 주소입니다.
      - 이 이름의 끝에 포트 정보 같은 추가할 수도 *MyDesktop:3389*합니다.
   - **사용자 계정** -원격 PC에 액세스 하는 데 사용자 계정을 추가 합니다.
     - Active Directory (AD)에 컴퓨터 또는 로컬 계정에 가입 된 경우 이러한 형식 중 하나를 사용 합니다. *user_name*를 *domain\user_name*, 또는 <em>user_name@domain.com</em>합니다.
     - 에 대 한 Azure Active Directory (AAD) 가입 컴퓨터를 이러한 형식 중 하나를 사용 합니다. *AzureAD\user_name* 나 <em>AzureAD\user_name@domain.com</em>합니다.
     - 암호 필요 여부를 선택할 수도 있습니다.
     - 동일한 사용자 이름으로 여러 사용자 계정을 관리 하는 경우 계정을 구분 하기 위해 친숙 한 이름을 설정 합니다.
     - 앱의 기본 설정에 저장 된 사용자 계정을 관리 합니다. 

3. 또한 이러한 선택적 설정은 연결을 설정할 수 있습니다.
   - 친숙 한 이름을 설정 합니다. 
   - 게이트웨이 추가
   - 사운드 출력 설정
   - 마우스 단추 스왑
   - 관리자 모드를 사용 하도록 설정
   - 원격 세션으로 로컬 폴더 리디렉션
   - 정방향 로컬 프린터
   - 앞으로 스마트 카드
4. **저장**을 클릭합니다.

연결을 시작 하려면 방금 두 번 클릭 합니다. 원격 리소스에 대 한도 마찬가지입니다.

### <a name="export-and-import-connections"></a>내보내기 및 가져오기 연결
원격 데스크톱 연결 정의 내보내고 다른 장치에서 사용할 수 있습니다. 원격 데스크톱은 별도 저장 됩니다. RDP 파일입니다.

1. 연결 센터에서 원격 데스크톱을 마우스 오른쪽 단추로 클릭 합니다.
2. **내보내기**를 클릭합니다.
3. 원격 데스크톱을 저장 하려는 위치로 이동 합니다. RDP 파일입니다.
4. **확인**을 클릭합니다.

원격 데스크톱을 가져오려면 다음 단계를 따르십시오. RDP 파일입니다.

1. 메뉴 모음에서 클릭 **파일** > **가져오기**합니다.
2. 이동 하 고 있습니다. RDP 파일입니다.
3. **열기**를 클릭합니다.

## <a name="add-a-remote-resource"></a>원격 리소스를 추가 합니다.
원격 리소스는 RemoteApp 프로그램, 세션 기반 데스크톱 및 RemoteApp 및 데스크톱 연결을 사용 하 여 게시 하는 가상 데스크톱.

- RemoteApp 및 데스크톱 연결에 액세스할 수는 RD 웹 액세스 서버에 링크를 표시 하는 URL입니다.
- 구성 된 RemoteApp 및 데스크톱 연결 나열 됩니다.

원격 리소스를 추가 합니다.

1. 연결 센터에서 **+** 를 클릭 하 고 **원격 리소스 추가**합니다. 
2. 원격 리소스에 대 한 정보를 입력 합니다.
   - **피드 URL** -URL RD 웹 액세스 서버입니다. 전자 메일 주소와 연결 된 RD 웹 액세스 서버를 검색 하도록 클라이언트를 이렇게 하면 회사 메일 계정과 –이 필드에 입력할 수도 있습니다.
   - **사용자 이름** -에 연결 하는 RD 웹 액세스 서버에 사용할 사용자 이름입니다.
   - **암호** -에 연결 하는 RD 웹 액세스 서버에 사용할 암호입니다.
3. **저장**을 클릭합니다.


원격 리소스 연결 센터에서 표시 됩니다.


## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>내부 자산에 액세스 하는 RD 게이트웨이 연결

원격 데스크톱 게이트웨이 (RD 게이트웨이) 어디에서 회사 네트워크의 원격 컴퓨터에 연결 하면 인터넷에서. 만들기 및 새 데스크톱 연결을 설정 하는 동안 또는 앱의 기본 설정에서 게이트웨이 관리할 수 있습니다.

기본 설정에서 새 게이트웨이를 설정 하려면:

1. 연결 센터에서 클릭 **기본 설정 > 게이트웨이**합니다. 
2. 클릭 합니다 **+** 다음 정보를 입력 테이블의 맨 위에 있는 단추:
   - **서버 이름** –를 게이트웨이로 사용 하려면 컴퓨터의 이름입니다. 이 Windows 컴퓨터 이름, 인터넷 도메인 이름으로 또는 IP 주소일 수 있습니다. 서버 이름에 포트 정보를 추가할 수도 있습니다 (예: **RDGateway:443** 나 **10.0.0.1: 443**).
   - **사용자 이름** -사용자 이름 및 암호를 연결 하는 원격 데스크톱 게이트웨이를 사용 해야 합니다. 선택할 수도 있습니다 **연결 자격 증명을 사용 하 여** 원격 데스크톱 연결에 사용 되는 동일한 사용자 이름 및 암호를 사용 하도록 합니다.


## <a name="manage-your-user-accounts"></a>사용자 계정 관리

데스크톱 또는 원격 리소스에 연결할 때 다시에서 선택 하려면 사용자 계정을 저장할 수 있습니다. 원격 데스크톱 클라이언트를 사용 하 여 사용자 계정을 관리할 수 있습니다.

새 사용자 계정을 만들려면

1. 연결 센터에서 클릭 **설정을** > **계정**합니다.
2. 클릭 **사용자 계정을 추가**합니다.
3. 다음 정보를 입력 합니다.
   - **사용자 이름** -원격 연결을 사용 하도록 저장 하는 사용자의 이름입니다. 다음 형식 중 하나에서 사용자 이름을 입력할 수 있습니다: domain\user_name, user_name 또는 user_name@domain.com합니다.
   - **암호** -지정한 사용자의 암호입니다. 원격 연결에 사용 하 여 저장 하려는 모든 사용자 계정이 연결 된 암호가 있어야 합니다.
   - **이름을** -서로 다른 암호를 사용 하 여 동일한 사용자 계정을 사용 하는 경우 해당 사용자 계정을 구분 하기 위해 친숙 한 이름을 설정 합니다.
4. 누르기 **저장**, 를 누른 다음 **설정을**합니다.

## <a name="customize-your-display-resolution"></a>디스플레이 해상도 사용자 지정
원격 데스크톱 세션에 대 한 디스플레이 해상도 지정할 수 있습니다.

1. 연결 센터에서 클릭 **기본 설정**합니다.
2. 클릭 **해상도**합니다. 
3. 클릭 **+** 합니다.
4. 해상도 높이 너비를 입력 한 다음 클릭 **확인 합니다.**

해상도 삭제 하려면 선택한 다음 클릭 **-** 합니다.

**표시에는 별도 공백을** Mac OS X 10.9를 실행 하 고 사용 하지 않도록 설정 하는 경우 **표시에는 별도 공백을** Mavericks에서 (**시스템 기본 설정 > 임무 컨트롤**)를 구성 해야 같은 옵션을 사용 하 여 원격 데스크톱 클라이언트에서이 설정입니다.

### <a name="drive-redirection-for-remote-resources"></a>원격 리소스에 대 한 드라이브 리디렉션
로컬 mac에는 원격 응용 프로그램을 사용 하 여 만든 파일을 저장할 수 있도록 원격 리소스에 대 한 드라이브 리디렉션이 지원 됩니다. 리디렉션된 폴더는 항상 원격 세션에서 네트워크 드라이브로 표시 된 홈 디렉터리입니다.

> [!NOTE]
> 이 기능을 사용 하기 위해 관리자가 서버에 적절 한 설정을 설정 해야 합니다.


## <a name="use-a-keyboard-in-a-remote-session"></a>원격 세션에서 키보드 사용

Mac 자판 배열 Windows 자판 배열에서 다릅니다. 

- 명령 키를 Mac 키보드에서 Windows 키를 같습니다.
- Mac에서 명령 단추를 사용 하는 작업을 수행 하려면 Windows에서 단추 컨트롤을 사용 해야 합니다 (예: 복사 = Ctrl + C).
- 키를 눌러 또한 FN 세션에서 기능 키를 활성화할 수 있습니다 (예: FN + F1)입니다.
- Alt 키를를 Mac 키보드의 공간 표시줄의 오른쪽 창에서 Alt Gr/오른쪽 Alt 키를 같습니다.

기본적으로 원격 세션은 클라이언트에서 실행 중인 OS로 동일한 키보드 로캘에서 사용 합니다. (Mac en를 실행 하는 경우-도 원격 세션에 사용할 OS 주세요. OS 키보드 로캘에서 사용 하지 않으면 키보드 원격 PC에 설정 및 설정 변경 확인 수동으로. 참조 된 [원격 데스크톱 클라이언트 FAQ](remote-desktop-client-faq.md) 키보드 및 로캘에 대 한 자세한 내용은 합니다.


## <a name="support-for-remote-desktop-gateway-pluggable-authentication-and-authorization"></a>원격 데스크톱 게이트웨이 플러그 가능 인증 및 권한 부여에 대 한 지원

Windows Server 2012 r 2에는 새 인증 방법, 원격 데스크톱 게이트웨이 플러그 가능 인증 및 사용자 지정 인증 루틴에 대 한 유연성을 제공 하는 권한 부여에 대 한 지원이 추가 되었습니다. 수행할 수 있습니다이 인증 모델 Mac 클라이언트입니다. 

> [!IMPORTANT]
> Windows 8.1 하기 전에 사용자 지정 인증 및 권한 부여 모델 위의 문서를 설명 하 고 있지만 지원 되지 않습니다.

이 기능에 대 한 자세한 내용은 체크 아웃 [ http://aka.ms/paa-sample ](http://aka.ms/paa-sample)합니다.


> [!TIP]
> 질문이 나 의견은 언제나 환영 합니다. 그러나 게시 하지 마십시오이 문서의 끝에서 주석 기능을 사용 하 여 문제 해결 도움말에 대 한 요청입니다. 대신, 이동 하려면는 [원격 데스크톱 클라이언트 포럼](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc) 하 고 새 스레드를 시작 합니다. 기능 제안할 사항이 있으시면 알려 고 [클라이언트 사용자 의견 포럼](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android)합니다.

