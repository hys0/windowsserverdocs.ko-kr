---
title: Winlogon ARSO(자동 다시 시작 로그온)
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15cddcfa-8a8e-45e4-bb76-b8e1a14ceac0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: f085cf78a01148f97a450577131213ce977a432a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402326"
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Winlogon ARSO(자동 다시 시작 로그온)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

**작성자**: Justin Turner, Windows 그룹이 포함 된 선임 지원 에스컬레이션 엔지니어  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
## <a name="overview"></a>개요  
Windows 8 잠금 화면 앱을 도입 되었습니다.  이 실행 하 고 사용자의 세션 잠겨 있는 동안 알림을 표시 하는 응용 프로그램 (일정 약속, 전자 메일 및 메시지 등).  Windows 업데이트 과정으로 인해 다시 시작 하는 장치 다시 시작 될 때 이러한 잠금 화면 알림을 표시 하지 못합니다.  일부 사용자에 게 이러한 잠금 화면 응용 프로그램에 따라 달라 집니다.  
  
## <a name="whats-changed"></a>변경 된 내용  
사용자가 Windows 8.1 장치에 로그인 하는 경우 LSA는 lsass.exe에 의해서만 사용자 자격 증명을 액세스할 수 있는 암호화 된 메모리에 저장 됩니다. Windows Update가 사용자 망이 자동으로 다시 부팅을 시작 사용자에 대 한 자동 로그온을 구성 하려면 이러한 자격 증명 사용 됩니다. TCB 권한으로 시스템으로 실행 되는 Windows Update는이 작업을 수행 하는 RPC 호출을 시작 합니다.  
  
재부팅 과정에 사용자에 게 자동으로 자동 로그온 메커니즘을 통해 로그인 하 고 사용자의 세션을 보호 하려면 또한 잠겨 있습니다. 잠금가 시작 됩니다 Winlogon 통해 반면 자격 증명 관리 LSA에 의해 수행 됩니다.  자동으로 로그온 하 고 콘솔에 사용자 잠금에 사용자의 잠금 화면 응용 프로그램 다시 시작 된 사용할 수 있게 됩니다.  
  
> [!NOTE]  
> Windows Update 유도 다시 부팅 되는 마지막 대화형 사용자가 자동으로 서명 하 고 세션이 잠깁니다 후 따라서 사용자의 잠금 화면 앱을 실행할 수 있습니다.  
  
![잠금 화면을 보여 주는 스크린샷](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_LockScreenApp.gif)  
  
![잠금 화면 앱을 보여 주는 스크린샷](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_LockScreen.gif)  
  
**간략 한 개요**  
  
-   Windows Update에 다시 시작 해야 함  
  
-   컴퓨터를 다시 시작할 수는 (*실행 하는 앱이 없는 데이터가 손실 될*)?  
  
    -   다시 시작  
  
    -   다시 로그인  
  
    -   잠금 컴퓨터  
  
-   사용 하거나 그룹 정책을 사용 하지 않도록 설정  
  
    -   서버 Sku에서에서 기본적으로 사용 안 함  
  
-   이유가 무엇일까요?  
  
    -   일부 업데이트는 다시 사용자가 로그 될 때까지 완료할 수 없습니다.  
  
    -   사용자 환경을 향상: 설치를 완료 하는 업데이트에 대 일 분이 소요 필요가 없습니다  
  
-   어떻게 하냐고요? 자동 로그온  
  
    -   암호를 저장 하면 로그인을 위해 해당 자격 증명을 사용 하 여,  
  
    -   페이징된 메모리에는 LSA 암호로 저장 자격 증명  
  
    -   BitLocker가 활성화 하는 경우에 설정할 수 있습니다.  
  
## <a name="group-policy-sign-in-last-interactive-user-automatically-after-a-system-initiated-restart"></a>그룹 정책: 시스템에서 시작한 다시 시작 후 자동으로 마지막 대화형 사용자 로그인  
Windows 8.1에서 Windows Server 2012 R2, Windows Update 다시 시작 된 후에 잠금 화면 사용자의 자동 로그온 서버 Sku에 대해 옵트인 및 클라이언트 Sku에 대 한 참여 하지 않음 /.  
  
**정책 위치:** 컴퓨터 구성 > 정책 > 관리 템플릿 > Windows 구성 요소 > Windows 로그온 옵션  
  
**정책 이름:** 시스템에서 시작한 다시 시작 후 자동으로 마지막 대화형 사용자 로그인  
  
**지원 되는 위치:** Windows Server 2012 R2, Windows 8.1 또는 Windows RT 8.1 이상  
  
**설명/도움말:**  
  
이 정책 설정은 장치는 자동으로 로그인 마지막 대화형 사용자 Windows Update 시스템을 다시 시작 후 여부를 제어 합니다.  
  
사용 하거나이 정책 설정을 구성 하지 않으면, 장치 Windows 업데이트를 다시 시작 후 자동 로그인을 구성 하는 사용자의 자격 증명 (사용자 이름, 도메인 및 암호화 된 암호 포함)를 안전 하 게 저장 합니다. Windows Update 다시 시작한 후 사용자가 자동으로 로그인 하 고 해당 사용자에 대해 구성 된 모든 잠금 화면 앱에 세션이 자동으로 잠깁니다.  
  
이 정책 설정을 사용 하지 않으면 Windows Update를 다시 시작한 후 장치에 자동 로그인에 대 한 사용자의 자격 증명을 저장 하지 않습니다. 시스템 다시 시작 된 후 사용자의 잠금 화면 앱을 다시 시작 됩니다.  
  
**레지스트리 편집기**  
  
|값 이름|형식|data|  
|-------|----|----|  
|DisableAutomaticRestartSignOn|DWORD|0<br /><br />**예 들어**<br /><br />0 (사용)<br /><br />1 (사용 안 함)|  
  
**정책 레지스트리 위치:** HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System  
  
**유형:** DWORD  
  
**레지스트리 이름:** DisableAutomaticRestartSignOn  
  
값: 0 또는 1  
  
0 = 사용  
  
1 = 사용 안 함  
  
![Windows 업데이트 시스템을 다시 시작한 후 장치가 마지막 대화형 사용자에 게 자동으로 로그인 하는지 여부를 지정할 수 있는 정책 설정 제어 UI를 보여 주는 스크린샷](../media/winlogon-automatic-restart-sign-on-arso/GTR_ADDS_SignInPolicy.gif)  
  
## <a name="troubleshooting"></a>문제 해결  
WinLogon를 자동으로 잠그는 경우에 WinLogon의 상태 추적 WinLogon 이벤트 로그에 저장 됩니다.  
  
자동 로그온 구성 시도의 상태는 기록  
  
-   성공한 경우  
  
    -   따라서 기록  
  
-   실패 인 경우  
  
    -   하면 오류를 기록 합니다.  
  
-   BitLocker의 상태가 변경 될 때:  
  
    -   자격 증명 제거가 로깅됩니다.  
  
        -   LSA에 대 한 작업 로그에 저장 됩니다.  
  
### <a name="reasons-why-autologon-might-fail"></a>자동 로그온 수 실패 하는 이유  
자동 사용자 로그인 달성 되지 않을 수 없는 몇 가지 경우가 있습니다.  이 섹션은이 발생할 수 있는 알려진된 시나리오 캡처 위한 것입니다.  
  
### <a name="user-must-change-password-at-next-login"></a>사용자는 다음 로그인 할 때 암호를 변경 해야 합니다.  
다음 로그인 시 암호 변경이 필요한 경우 사용자 로그인 차단 된 상태를 입력할 수 있습니다.  대부분의 경우에서 다시 시작 하기 전에 검색 된 전부는 아니지만이 수 있습니다 (예를 들어 암호 만료를 연결할 수 사이의 종료 및 다음 로그인 합니다.  
  
### <a name="user-account-disabled"></a>사용자 계정 사용 안 함  
사용 하지 않도록 설정 하는 경우에 기존 사용자 세션을 유지할 수 있습니다.  사용 하지 않도록 하는 계정에 대 한 다시 시작을 검색할 수 로컬로 대부분의 경우에서 사전에 따라 gp 도메인 계정 (일부 도메인 DC에서 계정이 비활성화 되어 있는 경우에 로그인 시나리오 작업 캐시)에 대 한 아닐 수 있습니다.  
  
### <a name="logon-hours-and-parental-controls"></a>로그온 시간 및 자녀 보호  
로그온 시간 및 자녀 보호 하지 못할 수 있습니다 새 사용자 세션이 만들어지지 않도록 합니다.  다시 시작이이 기간 동안 발생 한다면 사용자 하지 로그인 허용 됩니다.  잠금 또는 규정 준수 동작으로 로그 아웃 시키는 추가 정책이 있습니다.  이 유지 관리 기간이이 시간 동안 일반적으로 경우에 특히 평판 시간 사이의 절전, 계정 잠금 발생할 수 있는 많은 자식 경우 문제가 될 수 있습니다.  
  
## <a name="additional-resources"></a>추가 리소스  
**Table SEQ 테이블 \\ @ no__t-2 아랍어 3: ARSO 용어집 @-0  
  
|용어|정의|  
|----|-------|  
|자동 로그온|자동 로그온은 Windows에 몇 가지 릴리스에 제공 된 기능입니다.  이 기능은 문서화의 자동 로그온에 대 한 Windows v3.01와 같은 도구에도 있는 Windows *[http:/technet.microsoft.com/sysinternals/bb963905.aspx](https://technet.microsoft.com/sysinternals/bb963905.aspx)*<br /><br />단일 사용자를 장치의 자격 증명을 입력 하지 않고 자동으로 로그인 할 수 있습니다. 자격 증명 구성 되 고 레지스트리에 암호화 된 LSA 암호로 저장 됩니다.|  
  

