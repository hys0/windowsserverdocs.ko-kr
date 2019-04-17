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
ms.openlocfilehash: b0159d88251c7f4f6422dffd8f1e1414e1f30f33
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297047"
---
# Windows Admin Center 알려진 문제

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 페이지에서 설명하지 않은 문제가 발생하는 경우 [알려주십시오](http://aka.ms/WACfeedback).

## Lenovo XClarity 통합자
비 호환성 Lenovo XClarity 통합자 조합을 특정 버전 및 Windows Admin Center 사이 존재 합니다. 현재 사용 하거나 Windows Admin Center의 Lenovo XClarity 통합자 확장을 사용 하려면, 알아야 할 사항 다음과 같습니다.

- Lenovo XClarity 통합자 확장 버전 1.0.4 Windows Admin Center 1809.5 완벽 하 게 호환 됩니다.
- Lenovo XClarity 통합자 확장 버전 1.0.4 Windows Admin Center 1904에서 호환성 문제를 노출 했습니다. Microsoft 및 Lenovo 엔지니어는 함께 적극적으로 모색 하 고 가능한 한 빨리 솔루션을 제공 하기 위해 노력 합니다. Windows Admin Center 문서 사이트에서 모든 업데이트가 여기 게시 될 및 참조에 대 한 [Lenovo의 지원 페이지](https://support.lenovo.com/solutions/ht507549) 를 참조할 수도 있습니다.
- Lenovo의 XClarity 기능의 자주 사용자 인 경우 계속 XClarity 통합자 1.0.4를 사용 하려면 Windows Admin Center 1809.5에서 어느 유지 하거나 Windows Admin Center 1904로 업그레이드 하 고 별도로 독립 실행형 XClarity 관리자를 사용할 수 있습니다. 지금은 대 안으로 소프트웨어입니다.


## 설치 관리자

- 직접 인증서를 사용하여 Windows Admin Center를 설치하는 경우 인증서 관리자 MMC 도구에서 지문을 복사하면 [시작 부분에 잘못된 문자가 포함됩니다](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra). 해결 방법으로 지문의 첫 문자를 입력하고 나머지를 복사/붙여넣습니다.

- 1024 아래 포트를 사용 하 여 지원 되지 않습니다. 서비스 모드에서 포트 80에 지정 된 포트를 리디렉션할 수 있으며 선택적으로 구성할 수 있습니다.

- Windows 업데이트 (wuauserv) 서비스를 중지 하 고 사용 하지 않도록 설정 하는 경우 설치 프로그램 실패 합니다. [19100629]

### 업그레이드

- Msiexec 자동 모드에서 사용 하는 경우 이전 버전에서 서비스 모드에서 Windows Admin Center를 업그레이드 하는 경우 Windows Admin Center 포트에 대 한 인바운드 방화벽 규칙을 삭제 하는 문제가 발생할 수 있습니다.
  - 규칙을 다시 구성 (기본 443). Windows Admin Center에 대 한 포트 \<port> 교체를 관리자 권한 PowerShell 콘솔에서 다음 명령을 수행합니다

    ```powershell
    New-NetFirewallRule -DisplayName "SmeInboundOpenException" -Description "Windows Admin Center inbound port exception" -LocalPort <port> -RemoteAddress Any -Protocol TCP
    ```

## 일반

- 과도 하 게 사용에서 **Windows Server 2016** 에 게이트웨이로 설치 된 Windows Admin Center가 서비스를 포함 하는 이벤트 로그에 오류가 발생 충돌할 수 있습니다 ```Faulting application name: sme.exe``` 및 ```Faulting module name: WsmSvc.dll```합니다. 이것은 버그를 Windows Server 2019에서 해결 되었습니다. Windows Server 2016에 대 한 패치 포함 된 누적 2 월 2019 [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977)업데이트 합니다.

- Windows Admin Center를 게이트웨이로 설치 있고 손상 된 것으로 연결 목록이 나타나면 다음 단계를 수행 합니다.

>[!WARNING]
>연결 목록 및 게이트웨이의 모든 Windows Admin Center 사용자에 대 한 설정을 삭제 됩니다.

  1. Windows Admin Center 제거
  2. **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft** 아래에 있는 **Server Management Experience** 폴더를 삭제합니다.
  3. Windows Admin Center 다시 설치

- 오랜 시간 동안 이 도구를 열어 놓고 사용하지 않으면 여러 **오류: 이 작업에 대한 runspace 상태가 잘못됨** 오류가 발생합니다. 이 문제가 발생하는 경우 브라우저를 새로 고칩니다. 문제가 발생 하면, [피드백을 보내 주세요](http://aka.ms/WACfeedback).

- 매우 긴 URL을 사용하여 페이지를 새로 고칠 때 **500 오류**가 발생할 수 있습니다. [12443710]

- 일부 도구에서 브라우저의 맞춤법 검사가 특정 필드 값의 철자가 잘못된 것으로 표시할 수 있습니다. [12425477]

- 일부 도구에서 명령 단추를 클릭해도 즉시 상태 변경 내용이 반영되지 않을 수 있으며 UI 도구가 특정 속성의 변경 내용을 자동으로 반영하지 않을 수 있습니다. **새로 고침**을 클릭하여 대상 서버에서 최신 상태를 검색할 수 있습니다. [11445790]

- 태그 다중 선택 확인란을 사용 하 여 연결을 선택 하 여 연결 목록을 필터링 경우 태그에 연결 목록-필터링, 원래 선택 지속 선택한 모든 작업 이전에 선택한 모든 컴퓨터에 적용 됩니다. [18099259]

- Windows Admin Center 모듈 및 타사 소프트웨어 공지 내에 표시 된에서 실행 중인 OS의 버전 번호에 차이가 있을 수 있습니다.

### 확장 관리자

- Windows Admin Center를 업데이트할 때 확장을 다시 설치 해야 합니다.
- 액세스할 수 있는 확장 피드를 추가 하면 경고 없이 있습니다. [14412861]

## 특정 브라우저 문제

### Microsoft Edge

- 경우에 따라 Microsoft Edge를 사용하여 인터넷을 통해 Windows Admin Center 게이트웨이에 액세스하는 경우 로드 시간이 길어질 수 있습니다. 이는 Windows Admin Center 게이트웨이가 자체 서명된 인증서를 사용하는 Azure VM에서 발생할 수 있습니다. [13819912]

- Azure Active Directory를 ID 공급자로 사용하고 Windows Admin Center가 자체 서명되었거나 신뢰할 수 없는 인증서로 구성된 경우 Microsoft Edge에서 AAD 인증을 완료할 수 없습니다.  [15968377]

- Windows Admin Center를 서비스로 배포 있고 브라우저로 Microsoft Edge를 사용 하는 경우 새 브라우저 창을 생성 후 실패할 수 있습니다 게이트웨이를 Azure에 연결 합니다. 추가 하 여이 문제를 해결 하려면 https://login.microsoftonline.com, https://login.live.com,으로 게이트웨이의 URL 신뢰할 수 있는 사이트 및 클라이언트 측 브라우저에서 팝업 차단 설정에 대 한 사이트를 허용 하 고 있습니다. 에 대 한 자세한 지침은 [문제 해결 가이드](troubleshooting.md#azlogin)에이 해결 합니다. [17990376]

- 데스크톱 모드에서 설치 된 Windows Admin Center가 경우 Microsoft Edge에서 브라우저 탭의 즐겨찾기 아이콘을 표시 되지 않습니다. [17665801]

### Google Chrome

- 이전 버전 70 (늦은 2018 년 10 월에 출시) Chrome 웹 소켓 프로토콜 및 NTLM 인증에 대 한 [버그](https://bugs.chromium.org/p/chromium/issues/detail?id=423609) 했습니다. 이는 이벤트, PowerShell, 원격 데스크톱과 같은 도구에 영향을 줍니다.

- Chrome에서 특히 **작업 그룹**(비도메인) 환경에서 연결 환경을 추가하는 동안 여러 자격 증명 메시지를 표시할 수 있습니다.

- 서비스로 배포 된 Windows Admin Center가 경우 팝업 게이트웨이 URL에서 작동 하도록 Azure 통합 기능 사용 하도록 설정 해야 합니다. 이러한 서비스는 Azure 네트워크 어댑터, Azure 업데이트 관리 및 Azure Site Recovery 포함 됩니다.

### Mozilla Firefox

Windows Admin Center는 Mozilla Firefox에 대해 테스트되지 않지만 대부분의 기능이 작동해야 합니다.

- Windows 10 설치의 경우: Mozilla Firefox에는 자체 인증서 저장소가 있으므로 Windows 10에서 Windows Admin Center를 사용하려면 Firefox에 ```Windows Admin Center Client``` 인증서를 가져와야 합니다.

<a id="websockets"></a>

## 프록시 서비스를 사용하는 경우 WebSocket 호환성

Windows Admin Center에서 원격 데스크톱, PowerShell 및 이벤트 모듈은 프록시 서비스를 사용할 때 종종 지원되지 않는 WebSocket 프로토콜을 활용합니다. Azure AD 응용 프로그램 프록시 호환성에서 WebSocket 지원은 [미리 보기](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/)이며 호환성에 대한 피드백을 받고 있습니다.

## 2016 (2012 R2, 2012, 2008 R2) 이전 Windows Server 버전에 대 한 지원

> [!NOTE]
> Windows Admin Center는 Windows Server 2012 R2, 2012, 또는 2008 r 2에에서 포함 되지 않은 PowerShell 기능이 필요 합니다. Windows Server는 Windows Admin Center를 사용 하 여 이러한 관리는, 해당 서버에서 WMF 버전 5.1 이상을 설치 해야 합니다.

WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다.

설치되어있지 않은 경우 [WMF 5.1을 다운로드하여 설치할](https://www.microsoft.com/en-us/download/details.aspx?id=54616)수 있습니다.

<a id="rbacknownissues"></a>

## RBAC(역할 기반 액세스 제어)

- RBAC 배포가 Windows Defender Application Control(WDAC, 이전의 코드 무결성)을 사용하기 위해 구성된 컴퓨터에서 성공하지 않습니다. [16568455]

- 클러스터에서 RBAC를 사용하려면 구성을 각 구성원 노드에 개별적으로 배포해야 합니다.

- RBAC를 배포하는 경우 RBAC 구성에 올바르지 않게 지정된 권한이 없는 오류가 발생할 수 있습니다. [16369238]

## 서버 관리자 솔루션

### 서버 설정

- 설정을 수정 하면 저장 하지 않고 이동 하려고 하는 경우 페이지를 저장 되지 않은 변경에 대해 경고 하지만 계속 이동 합니다. 설정 탭을 선택 하는 페이지의 콘텐츠가 일치 하지 않는 상태가 될 수 있습니다. [19905798] [19905787]

### 인증서

- 현재 사용자 저장소에 .PFX 암호화 인증서를 가져올 수 없습니다. [11818622]

### 장치

- 키보드를 사용 하 여 표를 탐색할 때 선택 표 그룹의 위쪽으로 이동 될 수 있습니다. [16646059]

### 이벤트

- 이벤트는 [프록시 서비스를 사용할 때 웹 소켓 호환성](#websockets)의 영향을 받습니다.

- 큰 로그 파일을 내보낼 때 "패킷 크기"를 참조하는 오류 메시지가 표시될 수 있습니다. [16630279]

  - 이를 해결하려면 게이트웨이 컴퓨터에서 관리자 권한 명령 프롬프트에서 다음 명령을 사용합니다. ```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### 파일

- 대용량 파일 업로드 또는 다운로드는 아직 지원하지 않습니다. (\~100mb 제한) [12524234]

### PowerShell

- PowerShell은 [프록시 서비스를 사용할 때 웹 소켓 호환성](#websockets)의 영향을 받습니다.

- 데스크톱 PowerShell 콘솔에서와 같이 마우스 오른쪽 단추를 한 번 클릭하여 붙여넣는 것은 작동하지 않습니다. 대신 붙여넣기를 선택할 수 있는 브라우저의 컨텍스트 메뉴를 얻을 수 있습니다. Ctrl+V도 작동합니다.

- Ctrl+ C 복사할 수는 없으며 항상 콘솔에 Ctrl+C Break 명령이 보내집니다. 마우스 오른쪽 단추 클릭 컨텍스트 메뉴에서 복사할 수 있습니다.

- Windows Admin Center 창 크기를 줄이면 터미널 콘텐츠는 재배치되지만 다시 크기를 키우면 콘텐츠는 이전 상태로 되돌아가지 않을 수 있습니다. 콘텐츠가 뒤죽박죽으로 섞여 있는 경우 Clear-Host를 시도하거나 터미널 위의 버튼을 사용하여 연결을 끊고 다시 연결합니다.

### 레지스트리 편집기

- 검색 기능이 구현되지 않았습니다. [13820009]

### 원격 데스크톱

- 원격 데스크톱 도구는 Windows Server 2012를 관리 하는 경우 연결에 실패할 수 있습니다. [20258278]

- 원격 데스크톱을 사용 하 여 도메인에 가입 되지 않은 컴퓨터에 연결을 계좌에 입력 해야 합니다 ```MACHINENAME\USERNAME``` 형식입니다.

- 일부 구성 그룹 정책 사용 하 여 Windows 관리 센터의 원격 데스크톱 클라이언트를 차단할 수 있습니다. 이 문제가 발생 하는 경우 사용할 ```Allow users to connect remotely by using Remote Desktop Services``` 아래에서 ```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- 원격 데스크톱은 영향을 [소켓 호환성.](#websockets)

- 원격 데스크톱 도구는 현재 로컬 데스크톱 및 원격 세션 간에 모든 텍스트, 이미지 또는 파일 복사/붙여넣기를 지원하지 않습니다.

- 원격 세션 내에서 모든 복사/붙여넣기를 수행하려면 일반적으로(오른쪽 클릭 + 복사 또는 Ctrl+C) 복사하여 오른쪽 클릭 + 붙여넣기로 붙여넣어야 합니다(Ctrl+V는 사용할 수 없습니다).

- 원격 세션에 다음 주요 명령을 보낼 수 없음
  - Alt+Tab
  - 기능 키
  - Windows 키
  - PrtScn

- 원격 앱 – 원격 데스크톱 설정에서 원격 앱 도구를 사용 하도록 설정한 후 도구 나타나지 않을 수 도구 목록에 데스크톱 환경 포함 서버를 관리 하는 경우. [18906904]

### 역할 및 기능

- 설치에 사용할 수 없는 소스를 사용하여 역할 또는 기능을 선택할 때 건너뛰게 됩니다. [12946914]

- 역할 설치 후 자동으로 다시 부팅하지 않도록 선택하면 다시 묻지 않습니다. [13098852]

- 자동으로 다시 부팅을 선택하는 경우 상태가 100%로 업데이트되기 전에 다시 부팅됩니다. [13098852]

### 저장소

- 할당량 정보를 가져오는 오류 알림 없이 실패할 수 있습니다 (것이 오류가 브라우저의 콘솔에서) [18962274]

- 하위 수준: DVD/CD/플로피 드라이브가 하위 수준에서 볼륨으로 표시되지 않습니다.

- 하위 수준: 볼륨 및 디스크에 있는 일부 속성이 하위 수준에서 사용할 수 없으므로 세부 정보 창에 알 수 없거나 비어 있는 것으로 나타납니다.

- 하위 수준: 새 볼륨을 만들 때 ReFS는 Windows 2012 및 2012 R2 컴퓨터에서 64K의 할당 단위 크기를 지원합니다. ReFS 볼륨이 하위 수준 대상에서 더 작은 할당 단위 크기로 만들어지면 파일 시스템 포맷이 실패합니다. 새 볼륨을 사용할 수 없습니다. 해결책은 볼륨을 삭제하고 64K 할당 단위 크기를 사용하는 것입니다.

### 업데이트

- 업데이트를 설치한 후 설치 상태 캐시 될 수 있으며 브라우저를 새로 고쳐야 합니다.

- 오류가 발생할 수 있습니다. "키 존재 하지 않는" Azure 업데이트 관리 설정 하려고 할 때입니다. 이 경우 관리 되는 노드에서 다음 문제 해결 단계를 보십시오.
    1. ' 암호화 서비스 '를 중지 합니다.
    2. 폴더 옵션 표시 하도록 변경 숨김 파일 (필요한 경우).
    3. "%Allusersprofile%\Microsoft\Crypto\RSA\S-1-5-18" 폴더에 있고 모든 내용을 삭제 합니다.
    4. ' 암호화 서비스 '를 다시 시작 합니다.
    5. Windows Admin Center를 사용 하 여 업데이트 관리 설정을 반복 합니다.

### 가상 컴퓨터

- 브라우저에서 VM에 연결 하는 Windows Server 2012 호스트에서 가상 컴퓨터를 관리할 때 도구 VM에 연결 되지 것입니다. VM에 연결 하 고.rdp 파일 다운로드 계속 작동 해야 합니다. [20258278]

- Azure Site Recovery – ASR WAC, 외부 호스트에는 설정 된 경우 수 없게 됩니다 WAC [18972276] 내에서 VM을 보호 하기

- 가상 SAN 관리자, VM 이동, VM 내보내기, VM 복제 등 Hyper-V 관리자에서 사용할 수 있는 고급 기능은 현재 지원되지 않습니다.

### 가상 스위치

- 스위치 포함 팀(SET): 팀에 NIC을 추가할 때 팀과 NIC이 동일한 서브넷에 있어야 합니다.

## 컴퓨터 관리 솔루션

컴퓨터 관리 솔루션은 서버 관리자 솔루션의 도구 하위 집합을 포함하므로 동일한 알려진 문제가 적용되며 다음 특정 컴퓨터 관리 솔루션의 문제가 포함됩니다.

- Microsoft 계정 ([MSA](https://account.microsoft.com/account/))을 사용 하거나 Azure Active Directory (AAD)를 사용 하 여 Windows 10 컴퓨터에 로그온 할 때 지정 해야 하는 경우 "관리-으로" [16568455] 로컬 컴퓨터를 관리 하는 자격 증명

- 로컬 호스트를 관리하려고 할 때 게이트웨이 프로세스의 권한을 상승하라는 메시지가 나타납니다. 이 다음에 표시되는 사용자 계정 컨트롤 팝업에서 **아니요**를 클릭하면 Windows Admin Center는 이 메시지를 다시 표시하지 않습니다. 이 경우 시스템 트레이에서 Windows Admin Center 아이콘을 마우스 오른쪽 단추로 클릭하고 종료를 선택하여 게이트웨이 프로세스를 종료하고 시작 메뉴에서 Windows Admin Center를 다시 실행합니다.

- 기본적으로 Windows 10에는 WinRM/PowerShell 원격 작업이 없음
  
  - Windows 10 클라이언트의 관리를 사용하도록 설정하려면 관리자 권한 PowerShell 프롬프트에서 ```Enable-PSRemoting``` 명령을 실행해야 합니다.

  - 또한 ```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any```로 방화벽을 업데이트하여 로컬 서브넷 외부에서의 연결을 허용해야 합니다. 보다 제한적인 네트워크 시나리오에 대해 [이 설명서](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1)를 참조하십시오.

## 장애 조치 클러스터 관리자 솔루션

- 클러스터(하이퍼 컨버지드 또는 기존)를 관리하는 경우 **셸을 찾을 수 없음** 오류가 발생할 수 있습니다. 이런 경우 브라우저를 다시 로드하거나 다른 도구로 이동한 다음 되돌아옵니다. [13882442]

- 완전히 구성하지 않은 하위 수준(Windows Server 2012 또는 2012 R2) 클러스터를 관리할 때 문제가 발생할 수 있습니다. 이 문제를 해결하는 방법은 Windows 기능 **RSAT-클러스터링-PowerShell**이 설치되어 클러스터의 **각 구성원 노드**에서 사용하도록 설정되었는지 확인하는 것입니다. PowerShell로 이 작업을 수행하려면 모든 클러스터 노드에서 `Install-WindowsFeature -Name RSAT-Windows-PowerShell` 명령을 입력합니다. [12524664]

- 클러스터를 올바르게 검색하려면 전체 FQDN으로 추가해야 할 수 있습니다.

- 게이트웨이로 설치된 Windows Admin Center를 사용하여 클러스터에 연결하고 명시적 사용자 이름/암호를 제공하여 인증할 때 자격 증명으로 구성원 노드를 쿼리할 수 있도록 **모든 연결에 이러한 자격 증명 사용**을 선택해야 합니다.

## 하이퍼 컨버지드 클러스터 관리자 솔루션

- **드라이브 - 펌웨어 업데이트**, **서버 - 제거**, **볼륨 - 열기**와 같은 일부 명령은 사용하지 않도록 설정되며 현재 지원되지 않습니다.