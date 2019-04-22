---
title: 서버 관리자에서 원격 관리 구성
description: 서버 관리자
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 509182ed-c37d-4b81-84bc-aee43d006873
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a66fe7a274756de9bed9f6b14f5b9e491e5b623
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819584"
---
# <a name="configure-remote-management-in-server-manager"></a>서버 관리자에서 원격 관리 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server의 원격 서버에서 관리 작업을 수행 하려면 서버 관리자를 사용할 수 있습니다. Windows Server 2016을 실행 하는 서버에서 기본적으로 원격 관리가 사용 됩니다. 서버를 원격으로 관리 하려면 서버 관리자를 사용 하 여 서버 관리자 서버 풀에는 서버를 추가 합니다.

서버 관리자를 사용 하 여 이전 버전의 Windows Server를 실행 하는 원격 서버를 관리할 수 있지만 이러한 이전 운영 체제를 완벽 하 게 관리 하는 다음 업데이트가 필요 합니다.

Windows Server 2016 보다 오래 된 Windows Server 릴리스를 실행 하는 서버를 관리 하려면 다음 소프트웨어 및 Windows Server 2016에서 서버 관리자를 사용 하 여 이전 버전의 Windows Server를 관리 하기 위해 업데이트를 설치 합니다.

|운영 체제|필요한 소프트웨어|관리 효율성|
|----------|-----------|---------|
| Windows Server 2012 R2 또는 Windows Server 2012 |-   [.NET Framework 4.6](https://www.microsoft.com/download/details.aspx?id=45497)<br />-   [Windows Management Framework 5.0](https://go.microsoft.com/fwlink/?LinkID=395058). Windows 관리 프레임 워크 5.0 다운로드 패키지는 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 r 2에서 Windows Management Instrumentation (WMI) 공급자를 업데이트합니다. 관리 되는 서버에 설치 되어 있는 역할 및 기능에 대 한 정보를 수집 하는 서버 관리자를 사용 하는 업데이트 된 WMI 공급자 있습니다. Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2를 실행 하는 서버는 관리 효율성 상태는 업데이트가 적용 될 때까지 **액세스할 수 없습니다.** 합니다.<br />-성능 업데이트와 관련 된 [기술 자료 문서 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) 은 Windows Server 2012 r 2를 실행 하는 서버 또는 Windows Server 2012에 필요 하지 않습니다.||
| Windows Server 2008 R2 |-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)<br />-   [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881). Windows Management Framework 4.0 다운로드 패키지는 Windows Server 2008 r 2에서 Windows Management Instrumentation (WMI) 공급자를 업데이트합니다. 관리 되는 서버에 설치 되어 있는 역할 및 기능에 대 한 정보를 수집 하는 서버 관리자를 사용 하는 업데이트 된 WMI 공급자 있습니다. Windows Server 2008 r 2를 실행 하는 서버는 관리 효율성 상태는 업데이트가 적용 될 때까지 **액세스할 수 없습니다.** 합니다.<br />-성능 업데이트와 관련 된 [기술 자료 문서 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) 서버 관리자 Windows Server 2008 r 2에서 성능 데이터를 수집할 수 있습니다.||
| Windows Server 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />-   [Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) The Windows Management Framework 3.0 다운로드 패키지는 Windows Server 2008에서 Windows Management Instrumentation (WMI) 공급자를 업데이트 합니다. 관리 되는 서버에 설치 되어 있는 역할 및 기능에 대 한 정보를 수집 하는 서버 관리자를 사용 하는 업데이트 된 WMI 공급자 있습니다. Windows Server 2008을 실행 하는 서버에는 관리 효율성 상태는 업데이트가 적용 될 때까지 **액세스할 수 없음-Windows Management Framework 3.0을 실행 하는 이전 버전을 확인**합니다.<br />-성능 업데이트와 관련 된 [기술 자료 문서 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) 서버 관리자에서 Windows Server 2008 성능 데이터를 수집할 수 있습니다.||

관리 또는 서버 관리자를 실행 하는 작업 그룹 컴퓨터에서 원격 서버를 관리할 작업 그룹에 있는 서버를 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [서버 관리자에 서버 추가](add-servers-to-server-manager.md)합니다.

## <a name="BKMK_remote"></a>원격 관리 사용 여부 설정
Windows Server 2016에서 원격 관리는 기본적으로 사용 됩니다. 서버 관리자를 사용 하 여 Windows Server 2016를 원격으로 실행 되는 컴퓨터에 연결할 수 있습니다, 해제 된 경우 대상 컴퓨터에서 서버 관리자 원격 관리 설정 해야 합니다. 이 섹션의 절차에서는 원격 관리를 사용하지 않도록 설정하는 방법 및 사용하지 않도록 설정된 원격 관리를 다시 사용하도록 설정하는 방법에 대해 설명합니다. 서버 관리자 콘솔에서 로컬 서버에 대 한 원격 관리 상태에 표시 됩니다는 **속성** 영역에는 **로컬 서버** 페이지입니다.

기본 제공 Administrator 계정이 아닌 로컬 관리자 계정은 원격 관리를 사용하도록 설정한 경우에도 원격으로 서버를 관리하는 권한이 없을 수 있습니다. 원격 사용자 계정 컨트롤 (UAC) **LocalAccountTokenFilterPolicy** 레지스트리 설정을 원격으로 관리 하려면 기본 제공 관리자 계정인 아닌 Administrators 그룹의 로컬 계정이 허용 하도록 구성 해야 합니다 서버입니다.

Windows Server 2016에서 서버 관리자는 분산 구성 요소 개체 모델 (DCOM) 원격 통신에 대 한 Windows 원격 관리 (WinRM)에 사용합니다. 제어 하는 설정 합니다 **원격 관리 구성** 대화 상자는 서버 관리자 및 Windows PowerShell의 원격 통신에 WinRM을 사용 하는 부분에만 영향을 줍니다. 원격 통신에 DCOM을 사용 하는 서버 관리자의 파트에는 영향을 주지 않습니다. 예를 들어 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 원격 서버와 통신 하는 WinRM을 사용 하 여 있지만 Windows Server 2008 및 Windows Server 2008 r 2를 실행 하지 않은 하지만 서버와 통신 하는 DCOM을 사용 하 여 서버 관리자는 [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881) 또는 [Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) 업데이트를 적용 합니다. Microsoft Management Console (mmc) 및 기타 레거시 관리 도구는 DCOM을 사용합니다. 이러한 설정을 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [DCOM을 통해 mmc 또는 기타 도구 원격 관리를 구성 하려면](#BKMK_dcom) 이 항목의 합니다.

> [!NOTE]
> 이 섹션의 절차는 Windows Server가 실행되는 컴퓨터에서만 완료할 수 있습니다. 사용 하도록 설정 하거나 서버 관리자를 사용 하 여 클라이언트 운영 체제를 관리할 수 없는 때문에이 절차를 사용 하 여 Windows 10를 실행 중인 컴퓨터에서 원격 관리를 사용 하지 않도록 설정할 수 없습니다.

-   WinRM 원격 관리를 사용하도록 설정하려면 다음 절차 중 하나를 선택합니다.

    -   [Windows 인터페이스를 사용 하 여 서버 관리자 원격 관리를 사용 하도록 설정 하려면](#BKMK_windows)

    -   [Windows PowerShell을 사용 하 여 서버 관리자 원격 관리를 사용 하도록 설정 하려면](#BKMK_ps)

    -   [명령줄을 사용 하 여 서버 관리자 원격 관리를 사용 하도록 설정 하려면](#BKMK_cmdline)

    -   [서버 관리자 및 Windows PowerShell의 원격 관리를 이전 버전 Windows Server를 사용 하도록 설정 하려면](#BKMK_old)

-   WinRM 및 서버 관리자 원격 관리를 해제 하려면 다음 절차 중 하나를 선택 합니다.

    -   [그룹 정책을 사용 하 여 원격 관리를 사용 하지 않도록 설정](#BKMK_disableGP)

    -   [무인된 설치 동안 응답 파일을 사용 하 여 원격 관리를 사용 하지 않도록 설정](#BKMK_unattend)

-   DCOM 원격 관리를 구성하려면 [DCOM 원격 관리를 구성하려면](#BKMK_dcom)을 참조하십시오.

### <a name="BKMK_windows"></a>Windows 인터페이스를 사용 하 여 서버 관리자 원격 관리를 사용 하도록 설정 하려면

1.  > [!NOTE]
    > 제어 하는 설정 합니다 **원격 관리 구성** 대화 상자에 원격 통신에 DCOM을 사용 하는 일부 서버 관리자의 영향을 주지 않습니다.

    원격으로 관리 하려는 컴퓨터에서 아직 열려 있지 않은 경우 서버 관리자를 엽니다. Windows 작업 표시줄에서 **서버 관리자**를 클릭합니다. 에 **시작** 화면에서 클릭 합니다 **서버 관리자** 타일입니다.

2.  에 **속성** 영역의 합니다 **로컬 서버** 페이지에 대 한 하이퍼링크 값을 클릭 합니다는 **원격 관리** 속성.

3.  다음 중 하나를 수행한 다음 **확인**을 클릭합니다.

    -   이 컴퓨터를 서버 관리자 (또는 Windows PowerShell 설치 되어 있는 경우)를 사용 하 여 원격으로 관리 하지 않으려면 선택을 취소는 **다른 컴퓨터에서이 서버의 원격 관리 사용** 확인란입니다.

    -   이 컴퓨터는 서버 관리자 또는 Windows PowerShell을 사용 하 여 원격으로 관리할 수 있도록 선택 **다른 컴퓨터에서이 서버의 원격 관리 사용**합니다.

### <a name="BKMK_ps"></a>Windows PowerShell을 사용 하 여 서버 관리자 원격 관리를 사용 하도록 설정 하려면

1.  원격으로 관리 하려는 컴퓨터에서 관리자 권한으로 Windows PowerShell 세션을 열려면 다음 중 하나를 수행 합니다.

    -   Windows 바탕 화면의 작업 표시줄에서 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.

    -   Windows에서 **시작** 화면에서 마우스 오른쪽 단추로 클릭 **Windows PowerShell**에 다음 앱 바에서를 클릭 하 고 **관리자 권한으로 실행**합니다.

2.  다음을 입력 하 고 다음 키를 누릅니다 **Enter** 필요한 방화벽 규칙 예외를 모두 사용 하도록 설정 합니다.

    **Configure-SMremoting.exe -enable**

### <a name="BKMK_cmdline"></a>명령줄을 사용 하 여 서버 관리자 원격 관리를 사용 하도록 설정 하려면

1.  원격으로 관리할 컴퓨터에서 관리자 권한으로 명령 프롬프트 세션을 엽니다. 이 작업을 수행 하는 **시작** 화면에서 입력 **cmd**를 마우스 오른쪽 단추로 클릭 합니다 **명령 프롬프트** 타일에 표시 되 면를 **앱** 결과 및 그런 다음 앱 바에서 클릭 **관리자 권한으로 실행**합니다.

2.  다음과 같은 실행 파일을 실행합니다.

    **%windir%\system32\Configure-SMremoting.exe**

3.  다음 중 하나를 수행합니다.

    -   원격 관리를 해제 하려면 입력 **SMremoting.exe--사용 안 함**, 누릅니다 **Enter**합니다.

    -   원격 관리를 사용 하려면 입력 **SMremoting.exe--사용 하도록 설정**, 누릅니다 **Enter**합니다.

    -   현재 원격 관리 설정을 보려면 입력 **SMremoting.exe--가져오기**, 한 다음 ENTER를 누릅니다.

### <a name="BKMK_old"></a>서버 관리자 및 Windows PowerShell의 원격 관리를 이전 버전 Windows Server를 사용 하도록 설정 하려면

-   다음 중 하나를 수행합니다.

    -   Windows Server 2012를 실행 하는 서버에서 원격 관리를 사용 하려면 [Windows 인터페이스를 사용 하 여 서버 관리자 원격 관리를 사용 하도록 설정 하려면](#BKMK_windows) 이 여기에 있습니다.

    -   Windows Server 2008 R2를 실행 하는 서버에서 원격 관리를 사용 하려면 [서버 관리자를 사용 하 여 원격 관리](https://go.microsoft.com/fwlink/?LinkID=137378) Windows Server 2008 R2 도움말에서.

    -   Windows Server 2008을 실행 하는 서버에서 원격 관리를 사용 하려면 [을 사용 하도록 설정 하 고 Windows PowerShell에서 원격 명령을 사용 하 여](https://go.microsoft.com/fwlink/p/?LinkId=242565)입니다.

### <a name="BKMK_dcom"></a>DCOM을 통해 mmc 또는 기타 도구 원격 관리를 구성 하려면

1.  다음 중 하나를 수행하여 고급 보안이 포함된 Windows 방화벽 스냅인을 엽니다.

    -   에 **속성** 영역에는 **로컬 서버** 서버 관리자의 페이지에 대 한 하이퍼텍스트 값을 클릭 합니다는 **Windows 방화벽** 속성을 클릭 한 다음 **고급 설정**합니다.

    -   에 **시작** 화면에서 입력 **WF.msc**, 다음에 표시 되는 스냅인 타일을 클릭 하 고는 **앱** 결과입니다.

2.  트리 창에서 **인바운드 규칙**을 선택합니다.

3.  다음 방화벽 규칙의 예외 항목을 사용 하는 그룹 정책 설정으로 사용할 수 없습니다 확인 합니다. 설정된 설정이 없으면 다음 단계를 수행합니다.

    -   COM+ 네트워크 액세스(DCOM-In)

    -   원격 이벤트 로그 관리 (Np-in)

    -   원격 이벤트 로그 관리 (RPC)

    -   원격 이벤트 로그 관리 (RPC-EPMAP)

4.  설정되지 않은 규칙을 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **규칙 사용** 을 클릭합니다.

5.  고급 보안이 포함된 Windows 방화벽 스냅인을 닫습니다.

### <a name="BKMK_disableGP"></a>그룹 정책을 사용 하 여 원격 관리를 사용 하지 않도록 설정

1.  로컬 그룹 정책 편집기를 열려면 다음 중 하나를 수행 합니다.

    -   Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012에서 실행 하는 서버에는 **시작** 화면에서 입력 **gpedit.msc**를 클릭 하 고는 **gpedit** 타일 표시 되 면 합니다.

    -   Windows Server 2008 R2 또는 Windows Server 2008에서 실행 하는 서버에는 **실행** 대화 상자에서 **gpedit.msc**, 누릅니다 **Enter**합니다.

2.  오픈 **컴퓨터 구성 \ 관리 템플릿 Templates\Windows components\Windows 원격 관리 (WinRM) \WinRM 서비스**합니다.

3.  내용 창에서 **WinRM을 통한 원격 서버 관리 허용**을 두 번 클릭합니다.

4.  **WinRM을 통한 원격 서버 관리 허용** 정책 설정 대화 상자에서 **사용 안 함** 을 선택하여 원격 관리를 사용하지 않도록 설정합니다. **확인**을 클릭하여 변경 내용을 저장하고 정책 설정 대화 상자를 닫습니다.

### <a name="BKMK_unattend"></a>무인된 설치 동안 응답 파일을 사용 하 여 원격 관리를 사용 하지 않도록 설정

1.  Windows 시스템 이미지 관리자 Windows SIM ()를 사용 하 여 Windows Server 2016 설치에 대 한 무인된 설치 응답 파일을 만듭니다. 응답 파일을 만들고 Windows SIM을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows 시스템 이미지 관리자란?](https://technet.microsoft.com/library/cc766347.aspx) 고 [단계별: IT 전문가 용 기본 Windows 배포](https://technet.microsoft.com/library/dd349348.aspx)합니다.

2.  응답 파일의 설정을 찾아서 **Microsoft-Windows-Web-Services-for-Management-Core\EnableServerremoteManagement**합니다.

3.  응답 파일을 적용 하려는 모든 서버에서 기본적으로 서버 관리자 원격 관리를 사용 하지 않도록 설정, 설정 **Microsoft-Windows-Web-Services-for-Management-Core \EnableServerremoteManagement** 에 **False** .

    > [!NOTE]
    > 이 설정은 운영 체제 설치 프로세스 일부로 원격 관리를 사용하지 않도록 설정합니다. 이 설정을 구성 해도 관리자가 운영 체제 설치가 완료 된 후에 서버에서 서버 관리자 원격 관리를 사용할 수 있게 합니다. 관리자가 서버 관리자 원격 관리를 사용 하 여 다시의 단계를 사용 하도록 설정할 수 [Windows 인터페이스를 사용 하 여 서버 관리자 원격 관리를 구성 하려면](#BKMK_windows) 또는 [Windows PowerShell을 사용 하 여 서버 관리자 원격 관리를 사용 하도록 설정 하려면](#BKMK_ps) 이 항목의 합니다.
    > 
    > 무인된 설치의 일부로 기본적으로 원격 관리를 비활성화 하 고 설치 후 다시 서버에서 원격 관리를 사용 하지 않으면 하는 경우 서버 관리자를 사용 하 여이 응답 파일이 적용 되는 서버를 완전히 관리할 수 없습니다. 서버 관리자 서버 풀에 추가 된 후 서버 관리자 콘솔에서 관리 효율성 상태 오류를 생성 하는 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 (및 기본적으로 비활성화 하는 원격 관리가) 서버.

## <a name="windows-remote-management-winrm-listener-settings"></a>Windows 원격 관리 (WinRM) 수신기 설정
서버 관리자를 관리 하려면 원격 서버의 기본 WinRM 수신기 설정을 기반으로 합니다. 기본 설정에서 기본 인증 메커니즘 또는 원격 서버에 WinRM 수신기 포트 번호가 변경 된 경우 서버 관리자는 원격 서버와 통신할 수 없습니다.

다음 목록에는 서버 관리자를 사용 하 여 관리에 대 한 기본 WinRM 수신기 설정을 보여 줍니다.

-   WinRM 서비스가 실행되고 있습니다.

-   포트 번호 5985를 통해 HTTP 요청을 수신하도록 WinRM 수신기를 만듭니다.

-   포트 번호 5985는 Windows 방화벽 설정에서 WinRM을 통해 요청을 허용하도록 설정되어 있습니다.

-   **Kerberos** 및 **협상** 인증 유형 모두 사용하도록 설정합니다.

WinRM이 원격 컴퓨터와 통신하는 기본 포트 번호는 5985입니다.

명령 프롬프트에서 WinRM 수신기 설정을 구성 하는 방법에 대 한 자세한 정보 입력 **winrm 도움말 구성**, 한 다음 ENTER를 누릅니다.

## <a name="see-also"></a>관련 항목
[서버 관리자에 서버 추가](add-servers-to-server-manager.md)
[Windows PowerShell: Windows Server TechCenter의 about_remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx)
[사용자 계정 컨트롤 설명](https://support.microsoft.com/kb/951016)



