---
title: 원격 데스크톱 클라이언트 FAQ
description: 원격 데스크톱 클라이언트에 대한 질문과 대답
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 785a18cf-a5d0-4bc2-95e4-9ef53ee8f65a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 07/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 54ed455955053ebb234864f827759385ecf3d3c5
ms.sourcegitcommit: 73898afec450fb3c2f429ca373f6b48a74b19390
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71935031"
---
# <a name="frequently-asked-questions-about-the-remote-desktop-clients"></a>원격 데스크톱 클라이언트에 대한 질문과 대답

>적용 대상: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

이제 디바이스(Android, Mac, iOS 또는 Windows)에 원격 데스크톱 클라이언트를 설정했으므로 궁금한 점이 생겼을 것입니다. 다음은 원격 데스크톱 클라이언트에 관한 가장 일반적인 질문과 답변입니다. 

- [설정](#setting-up)
- [연결, 게이트웨이 및 네트워크](#connection-gateway-and-networks)
- [웹 클라이언트](#web-client)
- [모니터, 오디오 및 마우스](#monitors-audio-and-mouse)
- [Mac 하드웨어](#mac-client---hardware-questions)
- [특정 오류 메시지](#specific-errors)

이러한 질문은 대부분 모든 클라이언트에 적용되지만 몇 가지 클라이언트에만 적용되는 항목도 있습니다.

답변을 원하는 추가 질문이 있는 경우 이 문서에 피드백으로 남겨주세요.

## <a name="setting-up"></a>설정

### <a name="which-pcs-can-i-connect-to"></a>에 연결할 수 있는 Pc

체크 아웃 된 [지원 되는 구성](remote-desktop-supported-config.md) 에 연결할 수 있는 Pc에 대 한 정보에 대 한 문서.

### <a name="how-do-i-set-up-a-pc-for-remote-desktop"></a>원격 데스크톱용 PC를 설정하려면 어떻게 해야 하나요?

내 디바이스는 설정했는데 PC가 준비되지 않은 것 같습니다. 도움이 필요하신가요?

먼저 원격 데스크톱 설치 마법사를 본 적이 있으신가요? 이 마법사는 PC의 원격 액세스를 준비하는 과정을 안내합니다. PC에서 해당 도구를 다운로드하고 실행하여 모든 것을 설정하세요. 

그렇지 않고 수동으로 작업을 수행하려면 다음 내용을 계속 읽어보세요.

Windows 10에 대해 다음을 수행 합니다.

1. 연결하려는 디바이스에서 **설정**을 엽니다.
2. **시스템**, **원격 데스크톱**을 차례로 선택합니다.
3. 원격 데스크톱을 사용하도록 설정하려면 슬라이더를 사용하세요.
4. 일반적으로 원활한 연결을 위해 PC의 절전 모드를 해제하고 검색 가능하게 유지하는 것이 가장 좋습니다. **설정 표시**를 클릭하여 이 설정을 변경할 수 있는 PC의 전원 설정으로 이동합니다.
   > [!NOTE]
   > 절전 모드나 최대 절전 모드의 PC에는 연결할 수 없으므로 원격 PC의 절전 및 최대 절전 모드 설정이 **안 함**으로 설정되어 있는지 확인합니다. (일부 PC에서는 최대 절전 모드를 사용할 수 없습니다.)


**이 PC에 연결하는 방법** 아래에 나오는 이 PC의 이름을 기록해 둡니다. 클라이언트를 구성하려면 이 정보가 필요합니다.

특정 사용자에게 이 PC에 액세스할 수 있는 권한을 부여할 수 있습니다. 그러려면 **이 PC에 원격으로 액세스할 수 있는 사용자 선택**을 클릭합니다.
관리자 그룹의 구성원에게는 자동으로 액세스 권한이 부여됩니다.

Windows 8.1에서 원격 연결을 허용 하도록 지침을 따릅니다 [원격 데스크톱 연결을 사용 하 여 다른 데스크톱에 연결](https://support.microsoft.com/en-us/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection#1TC=windows-8)합니다.



## <a name="connection-gateway-and-networks"></a>연결, 게이트웨이 및 네트워크

### <a name="why-cant-i-connect-using-remote-desktop"></a>원격 데스크톱을 사용하여 연결할 수 없는 이유는 무엇인가요?

다음은 몇 가지 가능한 해결 방법이 일반적인 문제는 원격 PC에 연결 하려고 할 때 발생할 수 있습니다. 이러한 솔루션이 작동하지 않으면 [Microsoft 커뮤니티 웹 사이트](https://go.microsoft.com/fwlink/p/?LinkId=242079)에서 추가 도움말을 찾을 수 있습니다.

- **원격 PC를 찾을 수 없습니다.** PC 이름이 올바른지 확인한 후 해당 이름을 올바르게 입력했는지 확인하세요. 여전히 연결할 수 없는 경우 PC 이름 대신 원격 PC의 IP 주소를 입력하세요.
- **네트워크에 문제가 있습니다.** 인터넷에 연결되어 있는지 확인합니다. 
- **원격 데스크톱 포트가 방화벽에 의해 차단되었을 수 있습니다.** Windows 방화벽을 사용 하는 경우 다음이 단계를 따르십시오.

  1. Windows 방화벽을 엽니다. 
  2. **Windows 방화벽을 통해 앱 또는 기능 허용**을 클릭합니다. 
  3. **설정 변경**을 클릭합니다. 관리자 암호 또는 선택 내용을 확인 하 라는 메시지가 표시 될 수 있습니다.
  4. 아래에서 **허용 되는 응용 프로그램 및 기능**, 선택, **원격 데스크톱**, 을 탭 하거나 클릭 하 고 **확인**합니다.

     다른 방화벽을 사용 하는 경우 원격 데스크톱 (일반적으로 3389)에 대 한 포트가 열려 있는지 확인 합니다.
- **원격 PC에서 원격 연결을 설정할 수 없습니다.** 이 문제를 해결하려면 이 항목의 [원격 데스크톱용 PC를 설정하려면 어떻게 해야 하나요?](#how-do-i-set-up-a-pc-for-remote-desktop) 질문으로 다시 스크롤하세요.
- **원격 PC는 네트워크 수준 인증이 설정된 PC만 연결을 허용할 수 있습니다.** 
- **원격 PC가 꺼져 있을 수 있습니다.** 전원이 꺼져 있거나, 절전 모드 또는 최대 절전 모드인 PC에 연결할 수 없으므로 원격 PC의 절전 모드 및 최대 절전 모드 설정이 **안 함**으로 설정되어 있는지 확인합니다(일부 PC에서는 최대 절전 모드를 사용할 수 없음).

### <a name="why-cant-i-find-or-connect-to-my-pc"></a>찾기 또는 내 PC에 연결할 수 없는 이유 있습니까?

다음 사항을 확인합니다.

- PC가 켜져 있고 절전 모드가 아닌가요?
- 올바른 이름 또는 IP 주소를 입력했나요?

   > [!IMPORTANT]
   > PC 이름을 사용하려면 네트워크가 DNS를 통해 올바르게 이름을 확인 해야 합니다. 많은 홈 네트워크에서 연결 하는 호스트 이름 대신 IP 주소를 사용 해야 합니다.
- 다른 네트워크의 PC인가요? 외부 연결을 허용하도록 PC를 구성했나요?  도움이 필요하면 [네트워크 외부에서 PC에 대한 액세스 허용](remote-desktop-allow-outside-access.md)을 확인하세요.
- 지원되는 Windows 버전에 연결하고 있나요? 

   > [!NOTE]
   > Windows XP Home, Windows Media Center Edition, Windows Vista 홈 페이지 및 Windows 7 Home 또는 시작 타사 소프트웨어 없이 지원 되지 않습니다.

### <a name="why-cant-i-sign-in-to-a-remote-pc"></a>원격 PC에 로그인 할 수 없습니다는 이유

원격 PC의 로그인 화면을 볼 수 있지만 로그인 할 수 없습니다, 있습니다 수 추가 되지 원격 데스크톱 사용자 그룹 또는 원격 PC에 대 한 관리자 권한이 있는 모든 그룹입니다. 시스템 관리자에 게 있습니다.

### <a name="which-connection-methods-are-supported-for-company-networks"></a>회사 네트워크에 대 한 어떤 연결 방법이 지원 되나요?

회사 네트워크 외부에서 office 데스크톱에 액세스 하려면 회사 원격 액세스의 의미를 제공 해야 합니다. RD 클라이언트는 현재 다음을 지원합니다.

- 터미널 서버 게이트웨이 또는 원격 데스크톱 게이트웨이
- 원격 데스크톱 웹 액세스
- VPN (통해 VPN 옵션을 기본 제공 하는 iOS)

### <a name="vpn-doesnt-work"></a>VPN 작동 하지 않습니다.

VPN 문제는 여러 가지 원인이 있을 수 있습니다. VPN PC 또는 Mac 컴퓨터와 동일한 네트워크에서 작동 하는지 확인 하는 첫 번째 단계가입니다. PC 또는 Mac를 테스트할 수 없습니다, 디바이스의 브라우저에서 회사 인트라넷 웹 페이지에 액세스 할 수 있습니다.

확인할 기타 사항:
- **3G 네트워크는 VPN을 차단하거나 손상시킵니다.** 블록 또는 손상 3g 트래픽은 전 세계의 여러 3g 공급자 있습니다. VPN 연결 분 당에 대해 적절히 작동을 확인 합니다.
- **L2TP 또는 PPTP VPN.** PPTP 또는 L2TP VPN를 사용 중인 경우 하십시오 모든 트래픽을 보낼에서 ON으로 설정 VPN 구성 합니다.
- **VPN이 잘못 구성되었습니다.** 잘못 구성 된 VPN 서버는 VPN 연결 하지 작동 하거나 이유 잠시 후 작업을 중지할 수 있습니다. 이 경우 동일한 네트워크에서 디바이스의 웹 브라우저 또는 PC 또는 Mac에서 ios 테스트를 확인 합니다.

### <a name="how-can-i-test-if-vpn-is-working-properly"></a>VPN 제대로 작동 하는 경우 어떻게 테스트할 수 있습니까?

VPN 디바이스에서 활성화 되어 있는지 확인 합니다. 내부 네트워크에 웹 페이지를 이동 하거나 VPN을 통해 사용할 수 있는 웹 서비스를 사용 하 여 VPN 연결을 테스트할 수 있습니다.

### <a name="how-do-i-configure-l2tp-or-pptp-vpn-connections"></a>L2TP 또는 PPTP VPN 연결을 구성 하려면 어떻게 해야 합니까?

PPTP 또는 L2TP VPN를 사용 중인 경우 설정 해야 **모든 트래픽 보내기** 에 **ON** VPN 구성에서 합니다.

## <a name="web-client"></a>웹 클라이언트

### <a name="which-browsers-can-i-use"></a>어떤 브라우저를 사용할 수 있나요?

웹 클라이언트는 Microsoft Edge, Internet Explorer 11, Mozilla Firefox(v55.0 이상), Safari 및 Google Chrome을 지원합니다.

### <a name="what-pcs-can-i-use-to-access-the-web-client"></a>웹 클라이언트에 액세스할 때 어떤 PC를 사용할 수 있나요?

웹 클라이언트는 Windows, macOS, Linux 및 ChromeOS를 지원합니다. 현재 모바일 디바이스는 지원되지 않습니다.

### <a name="can-i-use-the-web-client-in-a-remote-desktop-deployment-without-a-gateway"></a>원격 데스크톱 배포의 웹 클라이언트를 게이트웨이 없이 사용할 수 있나요?

아니요. 클라이언트를 사용하려면 원격 데스크톱 게이트웨이를 연결해야 합니다. 방법을 모르시나요? 관리자에게 문의하세요.

### <a name="does-the-remote-desktop-web-client-replace-the-remote-desktop-web-access-page"></a>원격 데스크톱 웹 클라이언트가 원격 데스크톱 웹 액세스 페이지를 대체하나요?

아니요. 원격 데스크톱 웹 클라이언트는 원격 데스크톱 웹 액세스 페이지와 다른 URL에서 호스팅됩니다. 웹 클라이언트 또는 웹 액세스 페이지를 사용하여 브라우저에서 원격 리소스를 볼 수 있습니다.

### <a name="can-i-embed-the-web-client-in-another-web-page"></a>다른 웹 페이지에 웹 클라이언트를 포함할 수 있나요?

현재 이 기능은 지원되지 않습니다.

## <a name="monitors-audio-and-mouse"></a>모니터, 오디오 및 마우스

### <a name="how-do-i-use-all-of-my-monitors"></a>모니터의 모든 사용 하는 방법
두 개 이상의 화면을 사용 하려면 다음을 수행 합니다.

1. 여러 화면을 사용 설정하려는 원격 데스크톱을 마우스 오른쪽 단추로 클릭한 후 **편집**을 클릭합니다.
2. 사용 하도록 설정 **모든 모니터를 사용 하 여** 및 **전체 화면**합니다.

### <a name="is-bi-directional-sound-supported"></a>양방향 소리 지원
양방향 사운드는 Windows 클라이언트에서 연결별로 구성할 수 있습니다. 관련 설정은 **Local Resources** 옵션 탭의 **원격 오디오** 섹션에서 액세스할 수 있습니다.

### <a name="what-can-i-do-if-the-sound-wont-play"></a>소리가 재생 되지 않는 경우 어떻게 해야 합니까?
세션에서 로그 아웃 (안 함만 분리, 로그 아웃까지) 한 다음 다시 로그인 합니다.

## <a name="mac-client---hardware-questions"></a>Mac 클라이언트 - 하드웨어 질문
### <a name="is-retina-resolution-supported"></a>레 티 나 해상도 지원
예, 원격 데스크톱 클라이언트 레 티 나 해상도 지원 합니다.

### <a name="how-do-i-enable-secondary-right-click"></a>보조 마우스 오른쪽 단추 클릭을 어떻게 사용 합니까?
확인 하기 위해 세 가지 옵션이 있습니다 세션이 열린 내 마우스 오른쪽 단추로 사용 합니다.

- 표준 PC 두 단추 USB 마우스
- Apple Magic Mouse: 마우스 오른쪽 단추 클릭을 사용하려면 도크의 **System Preferences**를 클릭하고 **Mouse**를 클릭한 후 **Secondary click**을 사용하도록 설정합니다.
- Apple Magic Trackpad 또는 MacBook Trackpad: 마우스 오른쪽 단추 클릭을 사용하려면 도크의 **System Preferences**를 클릭하고 **Mouse**를 클릭한 후 **Secondary click**을 사용하도록 설정합니다.

### <a name="is-airprint-supported"></a>AirPrint 지원
아니요. 원격 데스크톱 클라이언트는 AirPrint를 지원하지 않습니다. (Mac 및 iOS 클라이언트도 마찬가지입니다.)

### <a name="why-do-incorrect-characters-appear-in-the-session"></a>잘못 된 문자가 세션에 나타나지 않는 이유는?
국제화 된 키보드를 사용 하는 경우 표시 될 수 있습니다 문제 세션에 표시 되는 문자는 문자를 일치지 않습니다 Mac 키보드에 입력 합니다.

이 작업은 다음과 같은 시나리오에서 발생할 수 있습니다.

- 원격 세션에서 인식 하지 못하는 키보드를 사용 합니다. 원격 데스크톱 키보드를 인식 하지 못하는, 마지막 원격 PC와 함께 사용 되는 언어를 기본값으로 합니다.
- 원격 PC에서 이전에 연결이 끊긴된 세션에 연결 하는 원격 PC의 언어와 다른 키보드 언어를 사용 하 고 사용 하려는 현재 합니다.

수동으로 원격 세션에 대 한 키보드 언어를 설정 하 여이 문제를 해결할 수 있습니다. 다음 섹션에서 단계를 참조하세요.

### <a name="how-do-language-settings-affect-keyboards-in-a-remote-session"></a>언어 설정이 원격 세션의 키보드에 미치는 영향은 무엇인가요?
Mac 자판 배열에 여러 유형이 있습니다. 그 중 일부는 Mac 특정 레이아웃 또는를 정확 하 게 일치 하지 못할 원격으로 windows 버전에서 사용자 지정 레이아웃입니다. 원격 세션은 원격 PC에서 사용 가능한 최적의 키보드 언어에 키보드를 매핑합니다. 

Mac 자판 배열을로 설정 된 경우 PC 버전의 모든 키에 올바르게 매핑되어 있어야 언어 키보드 (예: 프랑스어-PC)와 키보드 작동 해야 합니다.

Mac 자판 배열을 키보드 (예를 들어 프랑스어)의 Mac 버전으로 설정 된 경우 원격 세션의 프랑스어 PC 버전에 있습니다 매핑됩니다. OSX에서 사용하던 일부 Mac 바로 가기 키는 원격 Windows 세션에서 작동하지 않습니다.

자판 배열에는 언어 (예를 들어 캐나다 프랑스어)의 변형으로 설정 된 경우 및 원격 세션 수를 정확 하 게 변형에 매핑할 수 없는 경우 원격 세션에 가장 가까운 언어 (예를 들어 프랑스어) 있습니다 매핑됩니다. OSX에서 사용하던 일부 Mac 바로 가기 키는 원격 Windows 세션에서 작동하지 않습니다.

자판 배열을 원격 세션에 일치 시킬 수 없는 레이아웃으로 설정 된 경우 원격 세션 기본값으로 설정 됩니다 마지막 해당 PC와 함께 사용 되는 언어를 제공 합니다. 이 경우 또는 Mac 키보드와 일치 하도록 원격 세션의 언어를 변경 해야 하는 경우에는 다음과 같이 사용 하려는 하나에 가장 일치 하는 언어에 원격 세션에서 키보드 언어 수동으로 설정할 수 있습니다.

원격 데스크톱 세션 내의 키보드 레이아웃을 변경 하려면 다음 지침을 사용 합니다.

**Windows 10 또는 Windows 8:**

1. 원격 세션 내 지역 및 언어를 엽니다. 클릭 **시작 > 설정 > 시간과 언어**합니다. 열기 **지역 및 언어**합니다.
2. 사용 하려는 언어를 추가 합니다. 지역 및 언어 창을 닫습니다.
3. 이제 원격 세션에서 언어 간을 전환 하는 기능이 표시 됩니다. (오른쪽에서 시계 근처 원격 세션의.) 언어를 전환 하려면 클릭 (예: **Eng**).

닫고 적용 되려면 바로 변경 내용에 대 한 현재 사용 중인 응용 프로그램을 다시 시작 해야 합니다.


## <a name="specific-errors"></a>특정 오류

### <a name="why-do-i-get-an-insufficient-privileges-error"></a>"권한 부족" 오류가 발생 합니까?
에 연결 하려는 세션에 액세스 허용 되지 않습니다. 가장 일반적인 원인은 관리자 세션에 연결 하려는 경우 관리자만 콘솔에 연결할 수는 있습니다. 원격 데스크톱의 고급 설정에서 콘솔 스위치 해제 되어 있는지 확인 합니다. 이것이 문제가 발생 하는 경우 시스템 관리자에 게 문의 문의 하십시오.

### <a name="why-does-the-client-say-that-there-is-no-cal"></a>이유는 클라이언트 않다고는 CAL이 없는 무엇입니까?
원격 데스크톱 클라이언트에서 원격 데스크톱 서버에 연결할 때 서버는 원격 데스크톱 서비스 클라이언트 액세스 라이선스 (RDS CAL) 클라이언트에서 저장을 발급 합니다. 클라이언트가 연결 될 때마다 다시 해당 RDS CAL 하 고 사용할 서버 다른 라이선스를 발급 하지 않습니다. 디바이스에서 RDS CAL이 누락 되거나 손상 된 경우 서버에서 다른 라이선스를 실행 합니다. 사용이 허가 된 디바이스의 최대 수에 도달 하면 서버 새 RDS Cal을 발행할 수 없습니다. 지원에 대 한 네트워크 관리자에 게 문의 합니다.

### <a name="why-did-i-get-an-access-denied-error"></a>"액세스 거부" 오류를 가져오는는 이유
"액세스 거부" 오류는 연결 시도 하는 동안 원격 데스크톱 게이트웨이 및 결과 잘못 된 자격 증명에 의해 생성 합니다. 사용자 이름 및 암호를 확인 합니다. 이전 연결이 작동 하는 경우 오류가 최근에 발생 한 가능성이 있는 Windows 사용자 계정 암호를 변경 하를 업데이트 하지 않은 것 아직 원격 데스크톱 설정에 있습니다.

### <a name="what-does-rpc-error-23014-or-error-0x59e6-mean"></a>"RPC 오류 23014" 또는 "Error 0x59e6" 평균 합니까?
경우는 **RPC 오류 23014** 또는 **대기 하는 몇 분 후 다시 시도 오류 0x59E6**, RD 게이트웨이 서버에는 활성 연결의 최대 수에 도달 했습니다. RD 게이트웨이에서 실행되는 Windows 버전에 따라 최대 연결 수가 달라집니다. Windows Server 2008 R2 Standard 구현은 연결 수를 250개로 제한합니다. Windows Server 2008 R2 Foundation 구현 50에 대 한 연결의 수를 제한 합니다. 다른 모든 Windows 구현이 개수에 제한 없이 연결을 허용합니다.

### <a name="what-does-the-failed-to-parse-ntlm-challenge-error-mean"></a>"NTLM 챌린지를 구문 분석하지 못했습니다" 오류는 무엇을 의미하나요?
이 오류는 원격 PC의 잘못된 구성으로 인해 발생합니다. 원격 PC의 RDP 보안 수준 설정이 "클라이언트 호환 가능"으로 설정되어 있는지 확인하세요. (이 작업에 도움이 필요한 경우 시스템 관리자에게 문의하세요.)

### <a name="what-does-ts_rap-you-are-not-allowed-to-connect-to-the-given-host-mean"></a>"TS_RAP 지정된 호스트에 연결할 수 없습니다"는 무엇을 의미하나요?
이 오류는 게이트웨이 서버의 리소스 권한 부여 정책으로 인해 사용자 이름이 원격 PC에 연결하지 못하는 경우에 발생합니다. 이러한 오류는 다음과 같은 경우에 발생할 수 있습니다.

- 원격 PC 이름이 게이트웨이의 이름과 동일한 경우. 이 경우 원격 PC에 연결하려고 하면 액세스 권한이 없는 게이트웨이로 대신 연결됩니다. 게이트웨이에 연결해야 할 경우 외부 게이트웨이 이름을 PC 이름으로 사용하지 마세요. 대신 "localhost" 또는 IP 주소(127.0.0.1)나 내부 서버 이름을 사용하세요.
- 사용자 계정이 원격 액세스용 사용자 그룹의 구성원이 아닌 경우.
