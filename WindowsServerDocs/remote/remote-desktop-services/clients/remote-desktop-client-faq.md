---
title: 원격 데스크톱 클라이언트 FAQ
description: 원격 데스크톱 클라이언트에 대 한 질문과 대답
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: e6f91aa02cd0f19d480c24309be5797c273b0f2e
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804953"
---
# <a name="frequently-asked-questions-about-the-remote-desktop-clients"></a>원격 데스크톱 클라이언트에 대 한 질문과 대답

>적용 대상: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

원격 데스크톱 클라이언트에서 장치 (Android, Mac, iOS 또는 Windows)에서 설정한 했으므로 질문을 할 수 있습니다. 다음은 원격 데스크톱 클라이언트에 대 한 가장 일반적으로 묻는 질문과 대답입니다. 

- [설정](#setting-up)
- [연결, 게이트웨이 및 네트워크](#connection-gateway-and-networks)
- [웹 클라이언트](#web-client)
- [모니터, 오디오 및 마우스](#monitors-audio-and-mouse)
- [Mac 하드웨어](#mac-client---hardware-questions)
- [특정 오류 메시지](#specific-errors)

대부분 이러한 질문의 모든 클라이언트에 적용 되지만 몇 가지 클라이언트 특정 항목입니다.

추가 질문이 있는 답변을 원하는 경우 그대로 피드백으로이 문서에 있습니다.

## <a name="setting-up"></a>설정

### <a name="which-pcs-can-i-connect-to"></a>에 연결할 수 있는 Pc

체크 아웃 된 [지원 되는 구성](remote-desktop-supported-config.md) 에 연결할 수 있는 Pc에 대 한 정보에 대 한 문서.

### <a name="how-do-i-set-up-a-pc-for-remote-desktop"></a>설정 하려면 어떻게 합니까 PC를 원격 데스크톱에 대 한?

내 장치를 설정 했지만 PC의 준비 생각 합니다. 도움말?

원격 데스크톱 설치 마법사를 먼저 본 있습니까? 이 PC를 원격 액세스를 위한 준비를 안내 합니다. 모든 PC에서 도구를 다운로드 및 실행 설정 합니다. 

그렇지 않은 경우 수동으로 수행 하려는 경우 계속 읽어보세요.

Windows 10에 대해 다음을 수행 합니다.

1. 에 연결 하려는 장치에서 엽니다 **설정을**합니다.
2. 선택 **시스템** 차례로 **원격 데스크톱**합니다.
3. 슬라이더를 사용 하 여 원격 데스크톱을 사용 하도록 설정 합니다.
4. 일반적으로 절전 모드 해제 하 고 연결을 용이 하 게 검색 가능한 PC를 유지 하는 것이 좋습니다. 클릭 **설정 표시** 이 설정을 변경할 수 있는 PC에 대 한 전원 설정으로 이동 합니다.
   > [!NOTE]
   > 절전 모드에 있는 PC에 연결할 수 없거나, 절전 있으므로 하는지 확인 한 설정을 절전 모드 및 원격 PC에 최대 절전 모드 설정 되어 **Never**합니다. (최대 절전 모드를 모든 Pc에서 사용할 수 없습니다.)


이 PC에서의 이름을 기록해 **이 PC에 연결 하는 방법을**합니다. 이 클라이언트를 구성 해야 합니다.

-클릭을이 PC에 액세스 하는 특정 사용자에 대 한 권한을 부여할 수 있습니다 **이 PC를 원격으로 액세스할 수 있는 사용자 선택**합니다.
Administrators 그룹의 멤버는 자동으로 액세스할을 수 있습니다.

Windows 8.1에서 원격 연결을 허용 하도록 지침을 따릅니다 [원격 데스크톱 연결을 사용 하 여 다른 데스크톱에 연결](https://support.microsoft.com/en-us/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection#1TC=windows-8)합니다.



## <a name="connection-gateway-and-networks"></a>연결, 게이트웨이 및 네트워크

### <a name="why-cant-i-connect-using-remote-desktop"></a>원격 데스크톱을 사용 하 여 연결할 수 없습니다. 이유는 무엇입니까?

다음은 몇 가지 가능한 해결 방법이 일반적인 문제는 원격 PC에 연결 하려고 할 때 발생할 수 있습니다. 자세한 도움말을 찾을 수 작동 하지 않으면 이러한 솔루션은 [Microsoft 커뮤니티 웹 사이트](https://go.microsoft.com/fwlink/p/?LinkId=242079)합니다.

- **원격 PC는 찾을 수 없습니다.** 오른쪽 PC 이름 및 해당 이름을 올바르게 입력 했는지를 확인할 했는지 확인 합니다. 여전히 연결할 수 없는 경우에 PC 이름 대신 원격 PC의 IP 주소를 사용해 보세요.
- **네트워크에 문제가 있습니다.** 인터넷 연결이 되어 있는지 확인 합니다. 
- **원격 데스크톱 포트는 방화벽으로 차단 될 수 있습니다.** Windows 방화벽을 사용 하는 경우 다음이 단계를 따르십시오.

  1. Windows 방화벽을 엽니다. 
  2. 클릭 **앱 또는 기능 Windows 방화벽을 통해 허용**합니다. 
  3. 클릭 **설정을 변경**합니다. 관리자 암호 또는 선택 내용을 확인 하 라는 메시지가 표시 될 수 있습니다.
  4. 아래에서 **허용 되는 응용 프로그램 및 기능**, 선택, **원격 데스크톱**, 을 탭 하거나 클릭 하 고 **확인**합니다.

     다른 방화벽을 사용 하는 경우 원격 데스크톱 (일반적으로 3389)에 대 한 포트가 열려 있는지 확인 합니다.
- **원격 PC에 대 한 원격 연결 설정할 수 있습니다.** 이 해결 하려면까지 다시 스크롤하고 [설정 하려면 어떻게 합니까 PC 원격 데스크톱용?](#how-do-i-set-up-a-pc-for-remote-desktop) 이 항목에서 질문 합니다.
- **원격 PC에 연결할 네트워크 수준 인증을 설정 하는 Pc 수만 있습니다.** 
- **원격 PC 해제 될 수 있습니다.** 해제 된 경우, PC에 연결할 수 없거나, 절전 있으므로 주의 해야 설정 하기 위해 절전 모드와 원격 PC에 최대 절전 모드 설정에 대 한 **Never** (최대 절전 모드를 모든 Pc에서 사용할 수 없습니다.).

### <a name="why-cant-i-find-or-connect-to-my-pc"></a>찾기 또는 내 PC에 연결할 수 없는 이유 있습니까?

다음 사항을 확인합니다.

- 절전 모드 해제 및 PC 인가요?
- 권한 이름 또는 IP 주소를 입력 않은?

   > [!IMPORTANT]
   > PC 이름을 사용 하 여 DNS 통해 올바르게 이름을 확인 하 여 네트워크가 필요 합니다. 많은 홈 네트워크에서 연결 하는 호스트 이름 대신 IP 주소를 사용 해야 합니다.
- 다른 네트워크에 PC 인가요? 연결을 통해 외부 있도록 PC 구성 했습니까?  체크 아웃 [네트워크 외부에서 PC에 액세스할 수 있도록](remote-desktop-allow-outside-access.md) 도움말에 대 한 합니다.
- 지원 되는 Windows 버전에 연결 중 입니까? 

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

VPN 문제는 여러 가지 원인이 있을 수 있습니다. VPN PC 또는 Mac 컴퓨터와 동일한 네트워크에서 작동 하는지 확인 하는 첫 번째 단계가입니다. PC 또는 Mac를 테스트할 수 없습니다, 장치의 브라우저에서 회사 인트라넷 웹 페이지에 액세스 할 수 있습니다.

확인할 기타 사항:
- **3g 네트워크 VPN 손상 또는 차단 합니다.** 블록 또는 손상 3g 트래픽은 전 세계의 여러 3g 공급자 있습니다. VPN 연결 분 당에 대해 적절히 작동을 확인 합니다.
- **L2TP 또는 PPTP Vpn입니다.** PPTP 또는 L2TP VPN를 사용 중인 경우 하십시오 모든 트래픽을 보낼에서 ON으로 설정 VPN 구성 합니다.
- **VPN 잘못 구성 되었습니다.** 잘못 구성 된 VPN 서버는 VPN 연결 하지 작동 하거나 이유 잠시 후 작업을 중지할 수 있습니다. 이 경우 동일한 네트워크에서 장치의 웹 브라우저 또는 PC 또는 Mac에서 ios 테스트를 확인 합니다.

### <a name="how-can-i-test-if-vpn-is-working-properly"></a>VPN 제대로 작동 하는 경우 어떻게 테스트할 수 있습니까?

VPN 장치에서 활성화 되어 있는지 확인 합니다. 내부 네트워크에 웹 페이지를 이동 하거나 VPN을 통해 사용할 수 있는 웹 서비스를 사용 하 여 VPN 연결을 테스트할 수 있습니다.

### <a name="how-do-i-configure-l2tp-or-pptp-vpn-connections"></a>L2TP 또는 PPTP VPN 연결을 구성 하려면 어떻게 해야 합니까?

PPTP 또는 L2TP VPN를 사용 중인 경우 설정 해야 **모든 트래픽 보내기** 에 **ON** VPN 구성에서 합니다.

## <a name="web-client"></a>웹 클라이언트

### <a name="which-browsers-can-i-use"></a>어떤 브라우저를 사용할 수 있나요?

웹 클라이언트에서 Microsoft Edge, Internet Explorer 11, Mozilla Firefox 지원 (v55.0 이상), Safari 및 Google Chrome입니다.

### <a name="what-pcs-can-i-use-to-access-the-web-client"></a>웹 클라이언트에 액세스 하려면 사용할 수 있는 Pc

웹 클라이언트는 Windows, macOS, Linux 및 ChromeOS를 지원합니다. 이 이번에는 모바일 장치 지원 되지 않습니다.

### <a name="can-i-use-the-web-client-in-a-remote-desktop-deployment-without-a-gateway"></a>웹 클라이언트의 경우 게이트웨이 없이 원격 데스크톱 배포에서 사용할 수 있습니까?

아니요. 클라이언트는 원격 데스크톱 게이트웨이 연결에 필요 합니다. 모르는 즉? 에 대 한 관리자에 게 문의 합니다.

### <a name="does-the-remote-desktop-web-client-replace-the-remote-desktop-web-access-page"></a>원격 데스크톱 웹 클라이언트 원격 데스크톱 웹 액세스 페이지를 대체 하나요?

아니요. 원격 데스크톱 웹 클라이언트 원격 데스크톱 웹 액세스 페이지 보다 다른 URL에서 호스트 됩니다. 브라우저에서 원격 리소스를 보려면 웹 클라이언트 또는 웹 액세스 페이지를 사용할 수 있습니다.

### <a name="can-i-embed-the-web-client-in-another-web-page"></a>다른 웹 페이지에서 웹 클라이언트 포함

이 기능은 현재 지원 되지 않습니다.

## <a name="monitors-audio-and-mouse"></a>모니터, 오디오 및 마우스

### <a name="how-do-i-use-all-of-my-monitors"></a>모니터의 모든 사용 하는 방법
두 개 이상의 화면을 사용 하려면 다음을 수행 합니다.

1. 에 대 한 여러 화면을 사용 하도록 설정 하 고 클릭 하려는 원격 데스크톱을 마우스 오른쪽 단추로 클릭 **편집**합니다.
2. 사용 하도록 설정 **모든 모니터를 사용 하 여** 및 **전체 화면**합니다.

### <a name="is-bi-directional-sound-supported"></a>양방향 소리 지원
원격 데스크톱 클라이언트에서 소리를 업스트림 (마이크에 대 한 서버에 클라이언트)에서 지원 되지 않습니다.

### <a name="what-can-i-do-if-the-sound-wont-play"></a>소리가 재생 되지 않는 경우 어떻게 해야 합니까?
세션에서 로그 아웃 (안 함만 분리, 로그 아웃까지) 한 다음 다시 로그인 합니다.

## <a name="mac-client---hardware-questions"></a>Mac 클라이언트-하드웨어 질문
### <a name="is-retina-resolution-supported"></a>레 티 나 해상도 지원
예, 원격 데스크톱 클라이언트 레 티 나 해상도 지원 합니다.

### <a name="how-do-i-enable-secondary-right-click"></a>보조 마우스 오른쪽 단추 클릭을 어떻게 사용 합니까?
확인 하기 위해 세 가지 옵션이 있습니다 세션이 열린 내 마우스 오른쪽 단추로 사용 합니다.

- 표준 PC 두 단추 USB 마우스
- Apple 매직 마우스 사용: 마우스 오른쪽 단추 클릭을 사용 하도록 설정 하려면 **시스템 기본 설정** 도크를 클릭 **마우스**를 사용 하도록 설정 하 고 **보조 클릭**합니다.
- Apple 마법 트랙 패드 또는 MacBook 트랙 패드: 마우스 오른쪽 단추 클릭을 사용 하도록 설정 하려면 **시스템 기본 설정** 도크를 클릭 **마우스**를 사용 하도록 설정 하 고 **보조 클릭**합니다.

### <a name="is-airprint-supported"></a>AirPrint 지원
아니요, 원격 데스크톱 클라이언트는 AirPrint를 지원 하지 않습니다. (이 iOS 및 Mac 클라이언트에 대 한 합니다.)

### <a name="why-do-incorrect-characters-appear-in-the-session"></a>잘못 된 문자가 세션에 나타나지 않는 이유는?
국제화 된 키보드를 사용 하는 경우 표시 될 수 있습니다 문제 세션에 표시 되는 문자는 문자를 일치지 않습니다 Mac 키보드에 입력 합니다.

이 작업은 다음과 같은 시나리오에서 발생할 수 있습니다.

- 원격 세션에서 인식 하지 못하는 키보드를 사용 합니다. 원격 데스크톱 키보드를 인식 하지 못하는, 마지막 원격 PC와 함께 사용 되는 언어를 기본값으로 합니다.
- 원격 PC에서 이전에 연결이 끊긴된 세션에 연결 하는 원격 PC의 언어와 다른 키보드 언어를 사용 하 고 사용 하려는 현재 합니다.

수동으로 원격 세션에 대 한 키보드 언어를 설정 하 여이 문제를 해결할 수 있습니다. 다음 섹션의 단계를 참조 하세요.

### <a name="how-do-language-settings-affect-keyboards-in-a-remote-session"></a>언어 설정이 미치는 영향은 무엇입니까 키보드 원격 세션에서?
Mac 자판 배열에 여러 유형이 있습니다. 그 중 일부는 Mac 특정 레이아웃 또는를 정확 하 게 일치 하지 못할 원격으로 windows 버전에서 사용자 지정 레이아웃입니다. 원격 세션 가장 근접 한 원격 PC에 사용할 수 있는 키보드 언어 키보드를 매핑합니다. 

Mac 자판 배열을로 설정 된 경우 PC 버전의 모든 키에 올바르게 매핑되어 있어야 언어 키보드 (예: 프랑스어-PC)와 키보드 작동 해야 합니다.

Mac 자판 배열을 키보드 (예를 들어 프랑스어)의 Mac 버전으로 설정 된 경우 원격 세션의 프랑스어 PC 버전에 있습니다 매핑됩니다. 일부 Mac 바로 가기 키를 사용 하는 데 OSX에서 원격 Windows 세션에서 작동 하지 않습니다.

자판 배열에는 언어 (예를 들어 캐나다 프랑스어)의 변형으로 설정 된 경우 및 원격 세션 수를 정확 하 게 변형에 매핑할 수 없는 경우 원격 세션에 가장 가까운 언어 (예를 들어 프랑스어) 있습니다 매핑됩니다. 일부 Mac 바로 가기 키를 사용 하는 데 OSX에서 원격 Windows 세션에서 작동 하지 않습니다.

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
원격 데스크톱 클라이언트에서 원격 데스크톱 서버에 연결할 때 서버는 원격 데스크톱 서비스 클라이언트 액세스 라이선스 (RDS CAL) 클라이언트에서 저장을 발급 합니다. 클라이언트가 연결 될 때마다 다시 해당 RDS CAL 하 고 사용할 서버 다른 라이선스를 발급 하지 않습니다. 장치에서 RDS CAL이 누락 되거나 손상 된 경우 서버에서 다른 라이선스를 실행 합니다. 사용이 허가 된 장치의 최대 수에 도달 하면 서버 새 RDS Cal을 발행할 수 없습니다. 지원에 대 한 네트워크 관리자에 게 문의 합니다.

### <a name="why-did-i-get-an-access-denied-error"></a>"액세스 거부" 오류를 가져오는는 이유
"액세스 거부" 오류는 연결 시도 하는 동안 원격 데스크톱 게이트웨이 및 결과 잘못 된 자격 증명에 의해 생성 합니다. 사용자 이름 및 암호를 확인 합니다. 이전 연결이 작동 하는 경우 오류가 최근에 발생 한 가능성이 있는 Windows 사용자 계정 암호를 변경 하를 업데이트 하지 않은 것 아직 원격 데스크톱 설정에 있습니다.

### <a name="what-does-rpc-error-23014-or-error-0x59e6-mean"></a>"RPC 오류 23014" 또는 "Error 0x59e6" 평균 합니까?
경우는 **RPC 오류 23014** 또는 **대기 하는 몇 분 후 다시 시도 오류 0x59E6**, RD 게이트웨이 서버에는 활성 연결의 최대 수에 도달 했습니다. Windows 버전에 따라 다른 연결의 최대 수는 RD 게이트웨이에서 실행: Windows Server 2008 R2 Standard 구현 250에 대 한 연결 수를 제한 합니다. Windows Server 2008 R2 Foundation 구현 50에 대 한 연결의 수를 제한 합니다. 다른 모든 Windows 구현이 개수에 제한 없이 연결을 허용합니다.

### <a name="what-does-the-failed-to-parse-ntlm-challenge-error-mean"></a>"NTLM 챌린지를 구문 분석 하지 못했습니다" 오류는 무엇을 의미 할까요?
이 오류는 원격 PC에 잘못 된 구성으로 발생 합니다. RDP 보안 수준 설정에는 원격 PC 설정 되어 있는지 확인 "클라이언트 호환 가능 합니다." (설명 시스템 관리자에 게이 작업을 수행 하는 데 도움이 필요한 경우.)

### <a name="what-does-tsrap-you-are-not-allowed-to-connect-to-the-given-host-mean"></a>"TS_RAP 사용자는 허용 되지 않습니다 지정된 된 호스트에 연결" 하는 것이 무엇을 의미?
이 오류는 게이트웨이 서버에서 리소스 권한 부여 정책에서 원격 PC에 연결할 사용자 이름을 중지 될 때 발생 합니다. 이 작업은 다음과 같은 경우에 발생할 수 있습니다.

- 원격 PC 이름 게이트웨이의 이름으로 동일 합니다. 그런 다음 원격 PC에 연결 하려고 할 때 연결 이동 게이트웨이 대신 아마도 액세스할 수 있는 권한이 없는입니다. 게이트웨이에 연결 해야 할 경우 외부 게이트웨이 이름이 PC 이름으로 사용 하지 마십시오. "Localhost" 또는 IP 주소 (127.0.0.1) 또는 내부 서버 이름을 대신 사용 합니다.
- 사용자 계정에 원격 액세스를 위한 사용자 그룹의 구성원이 아닙니다.