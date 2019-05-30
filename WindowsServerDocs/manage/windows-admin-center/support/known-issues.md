---
title: Windows Admin Center 알려진 문제
description: Windows Admin Center 알려진 문제(Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: 7bf23c5af5620241574864babd07fd852115a450
ms.sourcegitcommit: 39ab8041d166e6817a95417d6aa30bc7abeeef54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66260273"
---
# <a name="windows-admin-center-known-issues"></a>Windows Admin Center 알려진 문제

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 페이지에서 설명하지 않은 문제가 발생하는 경우 [알려주십시오](http://aka.ms/WACfeedback).

## <a name="lenovo-xclarity-integrator"></a>Lenovo XClarity 통합자
이전에 공개 된 호환성 문제 Lenovo XClarity 통합자 확장과 Windows Admin Center 1904 버전의 Windows Admin Center 1904.1 버전을 사용 하 여 해결 되었습니다. Windows Admin Center 지원 되는 최신 버전으로 업데이트 하는 것이 좋습니다.

- Lenovo XClarity 통합자 확장 버전 1.1은 Windows Admin Center 1904.1 완벽 하 게 호환 됩니다. Windows Admin Center 및 Lenovo 확장의 최신 버전으로 업데이트 하는 것이 좋습니다.
- 어떤 이유로 든, 시간에 대 한 Windows Admin Center 1809.5를 사용 하 여 계속 해야 할 경우 사용할 수 없습니다 XClarity 통합자 1.0.4를 기반으로 Windows Admin Center 1809.5 더 이상 지원 될 때까지 Windows Admin Center 확장 피드에서 제공 될 예정입니다. 우리의 [지원 정책](../support/index.md)합니다.

## <a name="installer"></a>설치 관리자

- 직접 인증서를 사용하여 Windows Admin Center를 설치하는 경우 인증서 관리자 MMC 도구에서 지문을 복사하면 [시작 부분에 잘못된 문자가 포함됩니다](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra). 해결 방법으로 지문의 첫 문자를 입력하고 나머지를 복사/붙여넣습니다.

- 1024 아래의 포트를 사용 하는 것은 지원 되지 않습니다. 서비스 모드에서 필요에 따라 지정 된 포트를 리디렉션하려면 80 포트를 구성할 수 있습니다.

- Windows 업데이트 서비스 (wuauserv)가 중지 하 고 사용 하지 않도록 설정 하는 경우 설치 관리자가 실패 합니다. [19100629]

### <a name="upgrade"></a>업그레이드

- 자동 모드에서 msiexec를 사용 하는 경우 Windows Admin Center 서비스 모드에서 이전 버전에서 업그레이드 하는 경우 Windows Admin Center 포트에 대 한 인바운드 방화벽 규칙을 삭제 하는 문제가 발생할 수 있습니다.
  - 규칙 다시 승격된 된 PowerShell 콘솔에서 다음 명령을 수행을 대체 \<포트 > Windows Admin Center (기본값 443입니다.)에 대해 구성 된 포트를 사용 하 여

    ```powershell
    New-NetFirewallRule -DisplayName "SmeInboundOpenException" -Description "Windows Admin Center inbound port exception" -LocalPort <port> -RemoteAddress Any -Protocol TCP
    ```

## <a name="general"></a>일반

- 게이트웨이 설치 하는 Windows Admin Center 있다면 **Windows Server 2016** 많이 사용에서 서비스를 포함 하는 이벤트 로그에 오류와 함께 충돌이 발생할 수 있습니다 ```Faulting application name: sme.exe``` 고 ```Faulting module name: WsmSvc.dll```합니다. Windows Server 2019에 수정 된 버그 때문입니다. 포함 된 Windows Server 2016에 대 한 패치를는 2019 년 2 월 누적 업데이트 [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977)합니다.

- 게이트웨이로 설치 하는 Windows Admin Center 있고 손상 된 것으로 표시 되는 연결 목록에서 다음 단계를 수행 합니다.

>[!WARNING]
>이 게이트웨이의 모든 Windows Admin Center 사용자에 대 한 설정을 확인 하 고 연결 목록에 삭제 됩니다.

  1. Windows Admin Center 제거
  2. **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft** 아래에 있는 **Server Management Experience** 폴더를 삭제합니다.
  3. Windows Admin Center 다시 설치

- 이 도구를 열어 있습니다 및 긴 시간 동안 유휴 상태인 경우 발생할 수 있습니다 여러 경우 **오류: 이 작업에 대 한 runspace 상태가 올바르지** 오류입니다. 이 문제가 발생하는 경우 브라우저를 새로 고칩니다. 이 발생 하는 경우 [피드백 보내기](http://aka.ms/WACfeedback)합니다.

- 매우 긴 URL을 사용하여 페이지를 새로 고칠 때 **500 오류**가 발생할 수 있습니다. [12443710]

- 일부 도구에서 브라우저의 맞춤법 검사가 특정 필드 값의 철자가 잘못된 것으로 표시할 수 있습니다. [12425477]

- 일부 도구에서 명령 단추를 클릭해도 즉시 상태 변경 내용이 반영되지 않을 수 있으며 UI 도구가 특정 속성의 변경 내용을 자동으로 반영하지 않을 수 있습니다. **새로 고침**을 클릭하여 대상 서버에서 최신 상태를 검색할 수 있습니다. [11445790]

- 태그를 다중 선택 확인란을 사용 하 여 연결을 선택한에서 연결 목록을 필터링 하는 경우 태그 연결 목록을-필터링을 수행할 원래 선택 유지 선택 하면 모든 작업 이전에 선택한 모든 컴퓨터에 적용 됩니다. [18099259]

- 타사 타사 소프트웨어 통지 내에 나열 된 Windows Admin Center 모듈에서 실행 되는 OS의 버전 번호 간의 사소한 차이 있을 수 있습니다.

### <a name="extension-manager"></a>확장 관리자

- Windows Admin Center 업데이트 하면 확장을 다시 설치 해야 합니다.
- 피드에 액세스할 수 없는 확장을 추가 하는 경우 경고가 있습니다. [14412861]

## <a name="browser-specific-issues"></a>특정 브라우저 문제

### <a name="microsoft-edge"></a>Microsoft Edge

- 경우에 따라 Microsoft Edge를 사용하여 인터넷을 통해 Windows Admin Center 게이트웨이에 액세스하는 경우 로드 시간이 길어질 수 있습니다. 이는 Windows Admin Center 게이트웨이가 자체 서명된 인증서를 사용하는 Azure VM에서 발생할 수 있습니다. [13819912]

- Azure Active Directory를 ID 공급자로 사용하고 Windows Admin Center가 자체 서명되었거나 신뢰할 수 없는 인증서로 구성된 경우 Microsoft Edge에서 AAD 인증을 완료할 수 없습니다.  [15968377]

- 서비스로 배포 하는 Windows Admin Center 있고 Microsoft Edge 브라우저를 사용 하는 경우 새 브라우저 창을 생성 한 후 실패할 수 있습니다 azure 게이트웨이 연결 합니다. 추가 하 여이 문제를 해결 하려고 https://login.microsoftonline.com, https://login.live.com,으로 게이트웨이의 URL을 신뢰할 수 있는 사이트 및 클라이언트 쪽 브라우저에서 팝업 차단 설정에 대 한 허용 된 사이트 및 합니다. 에 대 한 자세한 지침은이 해결 합니다 [문제 해결 가이드](troubleshooting.md#azlogin)합니다. [17990376]

- Windows Admin Center 데스크톱 모드로 설치 된 경우는 favicon Microsoft Edge 브라우저 탭에 표시 되지 않습니다. [17665801]

### <a name="google-chrome"></a>Google Chrome

- 이전 버전 70 (10 월, 2018 년 말에 출시) Chrome 했습니다를 [버그](https://bugs.chromium.org/p/chromium/issues/detail?id=423609) websocket 프로토콜 및 NTLM 인증에 대 한 합니다. 이 효과 다음과 같은 도구: 이벤트, PowerShell, 원격 데스크톱 연결 합니다.

- Chrome에서 특히 **작업 그룹**(비도메인) 환경에서 연결 환경을 추가하는 동안 여러 자격 증명 메시지를 표시할 수 있습니다.

- Windows Admin Center 서비스로 배포 된 경우 게이트웨이 URL의 팝업 작동 하려면 Azure 통합 기능을 위한 사용 하도록 설정 해야 합니다. 이러한 서비스는 Azure 네트워크 어댑터, Azure 업데이트 관리 및 Azure Site Recovery를 포함 합니다.

### <a name="mozilla-firefox"></a>Mozilla Firefox

Windows Admin Center는 Mozilla Firefox에 대해 테스트되지 않지만 대부분의 기능이 작동해야 합니다.

- Windows 10 설치: Mozilla Firefox 저장소가 자체 인증서를 가져와야 하므로 ```Windows Admin Center Client``` Windows 10에서 Windows Admin Center 사용 하는 Firefox에는 인증서입니다.

<a id="websockets"></a>

## <a name="websocket-compatibility-when-using-a-proxy-service"></a>프록시 서비스를 사용 하는 경우 WebSocket 호환성

Windows Admin Center에서 원격 데스크톱, PowerShell 및 이벤트 모듈은 프록시 서비스를 사용할 때 종종 지원되지 않는 WebSocket 프로토콜을 활용합니다. Azure AD 응용 프로그램 프록시 호환성에서 WebSocket 지원은 [미리 보기](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/)이며 호환성에 대한 피드백을 받고 있습니다.

## <a name="support-for-windows-server-versions-before-2016-2012-r2-2012-2008-r2"></a>Windows Server 버전 (2012 R2, 2012, 2008 R2) 2016 이전에 대 한 지원

> [!NOTE]
> Windows Admin Center는 Windows Server 2012 R2, 2012 또는 2008 R2에에서 포함 되지 않은 PowerShell 기능이 필요 합니다. Windows Server를 Windows Admin Center 사용 하 여 이러한 관리 됩니다을 하는 경우 해당 서버에서 WMF 5.1 이상 버전을 설치 해야 합니다.

WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다.

설치되어있지 않은 경우 [WMF 5.1을 다운로드하여 설치할](https://www.microsoft.com/en-us/download/details.aspx?id=54616)수 있습니다.

<a id="rbacknownissues"></a>

## <a name="role-based-access-control-rbac"></a>역할 기반 Access Control (RBAC)

- RBAC 배포가 Windows Defender Application Control(WDAC, 이전의 코드 무결성)을 사용하기 위해 구성된 컴퓨터에서 성공하지 않습니다. [16568455]

- 클러스터에서 RBAC를 사용하려면 구성을 각 구성원 노드에 개별적으로 배포해야 합니다.

- RBAC를 배포하는 경우 RBAC 구성에 올바르지 않게 지정된 권한이 없는 오류가 발생할 수 있습니다. [16369238]

## <a name="server-manager-solution"></a>서버 관리자 솔루션

### <a name="server-settings"></a>서버 설정

- 설정을 수정 하면 저장 하지 않고 다른 위치로 이동 하려고 하는 경우 페이지에 저장 되지 않은 변경 사항에 대해 경고할 않지만 계속 이동 하려면 사용 합니다. 선택한 설정 탭 페이지의 내용에 맞지 않습니다 상태의 끝날 수도 있습니다. [19905798] [19905787]

### <a name="certificates"></a>인증서

- 현재 사용자 저장소에 .PFX 암호화 인증서를 가져올 수 없습니다. [11818622]

### <a name="devices"></a>장치

- 키보드를 사용 하 여 테이블을 탐색 하는 경우 선택 테이블 그룹의 맨 위에 이동할 수 있습니다. [16646059]

### <a name="events"></a>이벤트

- 이벤트는 [프록시 서비스를 사용할 때 웹 소켓 호환성](#websockets)의 영향을 받습니다.

- 큰 로그 파일을 내보낼 때 "패킷 크기"를 참조하는 오류 메시지가 표시될 수 있습니다. [16630279]

  - 이 해결 하려면 게이트웨이 컴퓨터에서 관리자 권한 명령 프롬프트에서 다음 명령을 사용 합니다. ```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### <a name="files"></a>파일

- 대용량 파일 업로드 또는 다운로드는 아직 지원하지 않습니다. (\~100mb) [12524234]

### <a name="powershell"></a>PowerShell

- PowerShell은 [프록시 서비스를 사용할 때 웹 소켓 호환성](#websockets)의 영향을 받습니다.

- 데스크톱 PowerShell 콘솔에서와 같이 마우스 오른쪽 단추를 한 번 클릭하여 붙여넣는 것은 작동하지 않습니다. 대신 붙여넣기를 선택할 수 있는 브라우저의 컨텍스트 메뉴를 얻을 수 있습니다. Ctrl+V도 작동합니다.

- Ctrl+ C 복사할 수는 없으며 항상 콘솔에 Ctrl+C Break 명령이 보내집니다. 마우스 오른쪽 단추 클릭 컨텍스트 메뉴에서 복사할 수 있습니다.

- Windows Admin Center 창 크기를 줄이면 터미널 콘텐츠는 재배치되지만 다시 크기를 키우면 콘텐츠는 이전 상태로 되돌아가지 않을 수 있습니다. 콘텐츠가 뒤죽박죽으로 섞여 있는 경우 Clear-Host를 시도하거나 터미널 위의 버튼을 사용하여 연결을 끊고 다시 연결합니다.

### <a name="registry-editor"></a>레지스트리 편집기

- 검색 기능이 구현되지 않았습니다. [13820009]

### <a name="remote-desktop"></a>원격 데스크톱

- 원격 데스크톱 도구는 Windows Server 2012를 관리 하는 경우 연결에 실패할 수 있습니다. [20258278]

- 도메인에 가입 되지 않은 컴퓨터에 연결 하려면 원격 데스크톱 사용 하는 경우에 계정에을 입력 해야 합니다 ```MACHINENAME\USERNAME``` 형식입니다.

- 일부 구성은 그룹 정책 사용 하 여 Windows Admin Center 원격 데스크톱 클라이언트를 차단할 수 있습니다. 사용이 발생 한 경우 ```Allow users to connect remotely by using Remote Desktop Services``` 아래 ```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- 원격 데스크톱은 영향을 받지 [websocket 호환성.](#websockets)

- 원격 데스크톱 도구는 현재 로컬 데스크톱 및 원격 세션 간에 모든 텍스트, 이미지 또는 파일 복사/붙여넣기를 지원하지 않습니다.

- 원격 세션 내에서 모든 복사/붙여넣기를 수행하려면 일반적으로(오른쪽 클릭 + 복사 또는 Ctrl+C) 복사하여 오른쪽 클릭 + 붙여넣기로 붙여넣어야 합니다(Ctrl+V는 사용할 수 없습니다).

- 원격 세션에 다음 주요 명령을 보낼 수 없음
  - Alt+Tab
  - 기능 키
  - Windows 키
  - PrtScn

- 원격 앱 – 원격 데스크톱 설정에서 원격 앱 도구를 사용 하도록 설정한 후 도구 나타나지 않을 수 있습니다 도구 목록에서 데스크톱 환경 포함 서버를 관리 하는 경우. [18906904]

### <a name="roles-and-features"></a>역할 및 기능

- 설치에 사용할 수 없는 소스를 사용하여 역할 또는 기능을 선택할 때 건너뛰게 됩니다. [12946914]

- 역할 설치 후 자동으로 다시 부팅하지 않도록 선택하면 다시 묻지 않습니다. [13098852]

- 자동으로 다시 부팅을 선택하는 경우 상태가 100%로 업데이트되기 전에 다시 부팅됩니다. [13098852]

### <a name="storage"></a>저장 공간

- 할당량 정보를 페치하는 오류 알림 없이 실패할 수 있습니다 (것이 오류는 브라우저의 콘솔에서) [18962274]

- 하위 수준: DVD/CD/플로피 드라이브에서 하위 수준 볼륨으로 표시 되지 않습니다.

- 하위 수준: 볼륨 및 디스크에서 일부 속성은 알 수 없거나 빈 세부 정보 패널에 나타나도록 하위 수준으로 사용할 수 없습니다.

- 하위 수준: 새 볼륨을 만들면, ReFS 64k 할당 단위 크기는 Windows 2012 및 2012 R2 컴퓨터에만 지원 합니다. ReFS 볼륨이 하위 수준 대상에서 더 작은 할당 단위 크기로 만들어지면 파일 시스템 포맷이 실패합니다. 새 볼륨을 사용할 수 없습니다. 해결책은 볼륨을 삭제하고 64K 할당 단위 크기를 사용하는 것입니다.

### <a name="updates"></a>업데이트

- 설치 상태 업데이트를 설치한 후 브라우저를 새로 고쳐야 하 고 캐시 될 수 있습니다.

- 다음과 같은 오류가 발생할 수 있습니다. "키 집합 존재 하지 않습니다." Azure 업데이트 관리를 설정 하려고 할 때입니다. 이 경우 관리 되는 노드-다음 수정 단계를 보세요.
    1. ' 암호화 서비스 ' 서비스를 중지 합니다.
    2. 표시할 변경 폴더 옵션 숨김 파일 (필요한 경우).
    3. "%Allusersprofile%\Microsoft\Crypto\RSA\S-1-5-18" 폴더에 있고 모든 내용을 삭제 합니다.
    4. ' 암호화 서비스 ' 서비스를 다시 시작 합니다.
    5. 반복 Windows Admin Center 사용 하 여 업데이트 관리 설정

### <a name="virtual-machines"></a>가상 머신

- Windows Server 2012 호스트에 가상 컴퓨터를 관리 하는 경우 브라우저에서 VM 연결 도구는 VM에 연결 하지 못합니다. VM에 연결할.rdp 파일을 다운로드 해야 계속 작동 합니다. [20258278]

- Azure Site Recovery – ASR WAC, 외부에서 호스트에 설정 되어 있으면 표시 됩니다 WAC [18972276] 내에서 VM을 보호할 수 있습니다.

- 가상 SAN 관리자, VM 이동, VM 내보내기, VM 복제 등 Hyper-V 관리자에서 사용할 수 있는 고급 기능은 현재 지원되지 않습니다.

### <a name="virtual-switches"></a>가상 스위치

- 포함 된 팀 (SET) 전환 합니다. Nic 팀에 추가할 때 동일한 서브넷에 있어야 합니다.

## <a name="computer-management-solution"></a>컴퓨터 관리 솔루션

컴퓨터 관리 솔루션은 서버 관리자 솔루션의 도구 하위 집합을 포함하므로 동일한 알려진 문제가 적용되며 다음 특정 컴퓨터 관리 솔루션의 문제가 포함됩니다.

- Microsoft 계정을 사용 하는 경우 ([MSA](https://account.microsoft.com/account/)) 지정 해야 하면 Windows 10 컴퓨터에 로그온 할 때 Azure Active Directory (AAD)를 사용 하는 경우 또는 "관리-으로" [16568455] 로컬 컴퓨터를 관리 하려면 자격 증명

- 로컬 호스트를 관리하려고 할 때 게이트웨이 프로세스의 권한을 상승하라는 메시지가 나타납니다. 이 다음에 표시되는 사용자 계정 컨트롤 팝업에서 **아니요**를 클릭하면 Windows Admin Center는 이 메시지를 다시 표시하지 않습니다. 이 경우 시스템 트레이에서 Windows Admin Center 아이콘을 마우스 오른쪽 단추로 클릭하고 종료를 선택하여 게이트웨이 프로세스를 종료하고 시작 메뉴에서 Windows Admin Center를 다시 실행합니다.

- 기본적으로 Windows 10에는 WinRM/PowerShell 원격 작업이 없음
  
  - Windows 10 클라이언트의 관리를 사용하도록 설정하려면 관리자 권한 PowerShell 프롬프트에서 ```Enable-PSRemoting``` 명령을 실행해야 합니다.

  - 또한 ```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any```로 방화벽을 업데이트하여 로컬 서브넷 외부에서의 연결을 허용해야 합니다. 보다 제한적인 네트워크 시나리오에 대해 [이 설명서](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1)를 참조하십시오.

## <a name="failover-cluster-manager-solution"></a>장애 조치 클러스터 관리자 솔루션

- 클러스터(하이퍼 컨버지드 또는 기존)를 관리하는 경우 **셸을 찾을 수 없음** 오류가 발생할 수 있습니다. 이런 경우 브라우저를 다시 로드하거나 다른 도구로 이동한 다음 되돌아옵니다. [13882442]

- 완전히 구성하지 않은 하위 수준(Windows Server 2012 또는 2012 R2) 클러스터를 관리할 때 문제가 발생할 수 있습니다. 이 문제를 해결하는 방법은 Windows 기능 **RSAT-클러스터링-PowerShell**이 설치되어 클러스터의 **각 구성원 노드**에서 사용하도록 설정되었는지 확인하는 것입니다. PowerShell로 이 작업을 수행하려면 모든 클러스터 노드에서 `Install-WindowsFeature -Name RSAT-Windows-PowerShell` 명령을 입력합니다. [12524664]

- 클러스터를 올바르게 검색하려면 전체 FQDN으로 추가해야 할 수 있습니다.

- 게이트웨이로 설치된 Windows Admin Center를 사용하여 클러스터에 연결하고 명시적 사용자 이름/암호를 제공하여 인증할 때 자격 증명으로 구성원 노드를 쿼리할 수 있도록 **모든 연결에 이러한 자격 증명 사용**을 선택해야 합니다.

## <a name="hyper-converged-cluster-manager-solution"></a>하이퍼 컨버지드 클러스터 관리자 솔루션

- **드라이브 - 펌웨어 업데이트**, **서버 - 제거**, **볼륨 - 열기**와 같은 일부 명령은 사용하지 않도록 설정되며 현재 지원되지 않습니다.