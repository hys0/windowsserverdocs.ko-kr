---
title: 여러 관리 서버 관리자를 사용 하 여 원격 서버
description: 서버 관리자
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a17e686-e7f2-47e2-b7af-733777c38b5f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4db3e486cec5cb065bfd202b7da2547be41a01a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847614"
---
# <a name="manage-multiple-remote-servers-with-server-manager"></a>여러 관리 서버 관리자를 사용 하 여 원격 서버

>적용 대상: Windows Server 2016

서버 관리자는 Windows Server 2012 R2 및 Windows Server 2012는 IT 전문가 프로 비전 하 고 로컬 및 원격 Windows 기반 서버 관리 서버에 물리적으로 액세스 하거나 사용 하지 않고도 데스크톱에서 관리 콘솔 또는 각 서버에 대 한 원격 데스크톱 프로토콜 (rdP) 연결을 사용 하도록 설정 해야 합니다. 서버 관리자가 Windows Server 2008 R2 및 Windows Server 2008에서 사용할 수 있지만 서버 관리자는 관리자가 관리할 수는 서버 수가 늘어났으며와 원격 다중 서버 관리를 지원 하려면 Windows Server 2012에서 업데이트 되었습니다.

이 테스트에서 Windows Server 2012 R2 및 Windows Server 2012의 서버 관리자의 일반적인 작업으로 구성 된 100 대의 서버까지 관리에 사용할 수 있습니다. 단일 서버 관리자 콘솔을 사용 하 여 관리할 수 있는 서버 수는 서버 관리자를 실행 하는 컴퓨터에 사용할 수 있는 하드웨어 및 네트워크 리소스 및 관리 되는 서버에서 요청 하는 데이터의 양에 따라 달라질 수 있습니다. 표시 하려는 데이터의 양이 해당 컴퓨터의 리소스 용량에 가까워지면 느린 응답에서 서버 관리자 및 새로 고침 완료 시 지연이 발생할 수 있습니다. 서버 관리자를 사용 하 여 관리할 수 있는 서버 수를 향상 시키기 위해, 서버 관리자의 설정을 사용 하 여 관리 되는 서버에서 가져오는 이벤트 데이터를 제한 권장는 **이벤트 데이터 구성** 대화 상자입니다. 이벤트 데이터 구성은 **이벤트** 타일의 **작업** 메뉴에서 열 수 있습니다. 조직에 있는 서버는 엔터프라이즈 수준의 수를 관리 해야 하는 경우에 제품을 평가 것이 좋습니다는 [Microsoft System Center 제품군](https://go.microsoft.com/fwlink/p/?LinkId=239437)합니다.

이 항목 및 하위 서버 관리자 콘솔의 기능을 사용 하는 방법에 대 한 정보를 제공 합니다. 이 항목에는 다음 섹션이 수록되어 있습니다.

-   [초기 고려 사항 및 시스템 요구 사항 검토](#BKMK_1.1)

-   [서버 관리자에서 수행할 수 있는 작업](#BKMK_tasks)

-   [서버 관리자를 시작 합니다.](#BKMK_start)

-   [원격 서버를 다시 시작](#BKMK_restart)

-   [서버 관리자 설정을 다른 컴퓨터로 내보내려면](#BKMK_export)

## <a name="BKMK_1.1"></a>초기 고려 사항 및 시스템 요구 사항 검토
다음 섹션에는 하드웨어 및 소프트웨어 요구 사항에 대 한 서버 관리자 뿐만 아니라 검토 해야 하는 몇 개의 초기 고려 나열 합니다.

### <a name="hardware-requirements"></a>하드웨어 요구 사항
서버 관리자는 Windows Server 2012 R2 및 Windows Server 2012의 모든 버전에는 기본적으로 설치 됩니다. 서버 관리자에 대 한 존재 하는 추가 하드웨어 요구 사항이 없습니다.

### <a name="BKMK_softconfig"></a>소프트웨어 및 구성 요구 사항
서버 관리자는 Windows Server 2012의 모든 버전에는 기본적으로 설치 됩니다. 서버 관리자를 사용 하 여 관리할 수 있지만 [Server Core 설치 옵션](https://go.microsoft.com/fwlink/p/?LinkID=241573) Windows Server 2012 및 원격 컴퓨터에서 실행 되는 Windows Server 2008 r 2의 서버 관리자가 Server Core 설치 옵션에서 직접 실행 되지 않습니다.

Windows Server 2008을 실행 하는 원격 서버 또는 Windows Server 2008 r 2를 완벽 하 게 관리 하려면 표시 된 순서에서를 관리 하려면 서버에서 다음 업데이트를 설치 합니다.

Windows Server 2012 r 2의 서버 관리자를 사용 하 여 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 하는 서버를 관리 하려면 다음 업데이트는 이전 운영 체제에 적용 됩니다.

-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)

-   [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881). Windows Management Framework 4.0 다운로드 패키지는 Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008에서 Windows Management Instrumentation (WMI) 공급자를 업데이트합니다. 관리 되는 서버에 설치 되어 있는 역할 및 기능에 대 한 정보를 수집 하는 서버 관리자를 사용 하는 업데이트 된 WMI 공급자 있습니다. Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 하는 서버는 관리 효율성 상태는 업데이트가 적용 될 때까지 **액세스할 수 없습니다.** 합니다.

-   와 관련 된 성능 업데이트 [기술 자료 문서 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) 서버 관리자가 Windows Server 2008 및 Windows Server 2008 r 2에서 성능 데이터를 수집 하도록 허용 합니다. 이 성능 업데이트는 Windows Server 2012를 실행 하는 서버에서 필요 하지 않습니다.

Windows Server 2008 r 2를 실행 하는 서버 또는 Windows Server 2008을 관리 하려면 다음 업데이트는 이전 운영 체제에 적용 됩니다.

-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)

-   [Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) The Windows Management Framework 3.0 다운로드 패키지는 Windows Server 2008 및 Windows Server 2008 r 2에서 Windows Management Instrumentation (WMI) 공급자를 업데이트 합니다. 관리 되는 서버에 설치 되어 있는 역할 및 기능에 대 한 정보를 수집 하는 서버 관리자를 사용 하는 업데이트 된 WMI 공급자 있습니다. Windows Server 2008을 실행 하는 서버 또는 Windows Server 2008 R2의 관리 효율성 상태는 업데이트가 적용 될 때까지 **액세스할 수 없음-Windows Management Framework 3.0을 실행 하는 이전 버전을 확인**합니다.

-   와 관련 된 성능 업데이트 [기술 자료 문서 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) 서버 관리자가 Windows Server 2008 및 Windows Server 2008 r 2에서 성능 데이터를 수집 하도록 허용 합니다.

서버 관리자가 최소 서버 그래픽 인터페이스;에서 실행 즉 때 서버 그래픽 셸 기능이 제거 된 합니다. 서버 그래픽 셸 기능은 Windows Server 2012 R2 및 Windows Server 2012에 기본적으로 설치 됩니다. 서버 관리자 콘솔 실행 서버 그래픽 셸을 제거 하면 일부 응용 프로그램 또는 콘솔에서 사용할 수 있는 도구를 사용할 수 없는 경우. HTML 도움말 (mmc F1 도움말, 예를 들어)를 열 수 없습니다 같은 인터넷 브라우저는 서버 그래픽 셸, 따라서 웹 페이지 및 응용 프로그램 없이 실행할 수 없습니다. 서버 그래픽 셸이 설치 되어 있지 않으면; Windows 자동 업데이트 및 피드백을 구성 하기 위한 대화 상자를 열 수 없습니다. 서버 관리자 콘솔에서 이러한 대화 상자를 열고 명령을 실행 하도록 리디렉션됩니다 **sconfig.cmd**합니다.

#### <a name="manage-remote-computers-from-a-client-computer"></a>클라이언트 컴퓨터에서 원격 컴퓨터 관리
서버 관리자 콘솔에 포함 된 [원격 서버 관리 도구](https://go.microsoft.com/fwlink/?LinkID=304145) Windows 8.1 및 [원격 서버 관리 도구](https://go.microsoft.com/fwlink/p/?LinkID=238560) Windows 8 용입니다. 클라이언트 컴퓨터에 원격 서버 관리 도구를 설치 하면 없습니다 관리할 로컬 컴퓨터의 서버 관리자를 사용 하 여 Windows 클라이언트 운영 체제를 실행 하는 컴퓨터 또는 장치를 관리 하려면 서버 관리자를 사용할 수 없습니다. 서버 관리자만 Windows 기반 서버 관리를 사용할 수 있습니다.

|서버 관리자 원본 운영 체제|대상으로 Windows Server 2012 R2 |대상으로 Windows Server 2012 |대상으로 Windows Server 2008 R2 또는 Windows Server 2008 |Windows Server 2003 대상|
|-------------------------------|---------------------------------------|------------------------------------|-----------------------------------------------------------------------|------------------|
|Windows 8 또는 Windows Server 2012 |지원되지 않음|전체 지원|[소프트웨어 및 구성 요구 사항](#BKMK_softconfig)이 충족되면 대부분의 관리 작업을 수행할 수 있지만 역할이나 기능을 설치하거나 제거하는 작업은 수행할 수 없습니다.|제한된 지원, 온라인 및 오프라인 상태만 지원|
|Windows 8.1 또는 Windows Server 2012 R2 |전체 지원|전체 지원|[소프트웨어 및 구성 요구 사항](#BKMK_softconfig)이 충족되면 대부분의 관리 작업을 수행할 수 있지만 역할이나 기능을 설치하거나 제거하는 작업은 수행할 수 없습니다.|제한된 지원, 온라인 및 오프라인 상태만 지원|

###### <a name="to-start-server-manager-on-a-client-computer"></a>클라이언트 컴퓨터에서 서버 관리자를 시작하려면

1.  지침에 따라 [원격 서버 관리 도구 배포](https://go.microsoft.com/fwlink/?LinkID=238562) 원격 서버 관리 도구에 대 한 Windows 8.1 또는 원격 서버 관리 도구에 대 한 Windows 8을 설치 합니다.

2.  에 **시작** 화면에서 클릭 **서버 관리자**합니다. **서버 관리자** 타일은 원격 서버 관리 도구를 설치한 후에 사용할 수 있습니다.

3.  모두를 **관리 도구** 또는 **서버 관리자** 타일에 표시 되는 **시작** 원격 서버 관리 도구를 설치한 후 화면 및 서버 관리자를 검색 합니다 **시작** 화면 결과 표시 되었는지 확인 합니다는 **관리 도구 표시** 설정이 켜져 합니다. 이 설정을 보려면의 오른쪽 위 모퉁이 위로 마우스 커서를 이동 합니다 **시작** 화면의 및 클릭 **설정**합니다. **관리 도구 표시** 가 꺼져 있으면 원격 서버 관리 도구의 일부로 설치된 도구를 표시하도록 설정을 켭니다.

원격 서버 관리 도구에 대 한 Windows 8 원격 서버 관리를 실행 하는 방법에 대 한 자세한 내용은 참조 하십시오 [원격 서버 관리 도구](https://go.microsoft.com/fwlink/?LinkID=221055) TechNet wiki의 합니다.

#### <a name="configure-remote-management-on-servers-that-you-want-to-manage"></a>관리하려는 서버에서 원격 관리 구성

> [!IMPORTANT]
> 기본적으로 서버 관리자 및 Windows PowerShell 원격 관리를 Windows Server 2012 R2 및 Windows Server 2012에서 사용할 수 있습니다.

관리 작업을 수행할 원격 서버에서 서버 관리자를 사용 하 여, 원격 서버를 관리 하려면 서버 관리자 및 Windows PowerShell을 사용 하 여 원격 관리를 허용 하도록 구성 되어야 합니다. Windows Server 2012 R2 또는 Windows Server 2012에서 원격 관리를 사용 하지 않도록 설정 된 경우 다시 활성화 하려면 다음 단계를 수행 합니다.

##### <a name="BKMK_windows"></a>Windows 인터페이스를 사용 하 여 Windows Server 2012 R2 또는 Windows Server 2012에서 서버 관리자 원격 관리를 구성 하려면

1.  > [!NOTE]
    > 제어 하는 설정 합니다 **원격 관리 구성** 대화 상자에 원격 통신에 DCOM을 사용 하는 일부 서버 관리자의 영향을 주지 않습니다.

    아직 열려 있지 않은 경우 서버 관리자를 열려면 다음 중 하나를 수행 합니다.

    -   Windows 작업 표시줄에서 서버 관리자 단추를 클릭 합니다.

    -   에 **시작** 화면에서 클릭 **서버 관리자**합니다.

2.  에 **속성** 영역의 합니다 **로컬 서버** 페이지에 대 한 하이퍼링크 값을 클릭 합니다는 **원격 관리** 속성.

3.  다음 중 하나를 수행한 다음 **확인**을 클릭합니다.

    -   이 컴퓨터를 서버 관리자 (또는 Windows PowerShell 설치 되어 있는 경우)를 사용 하 여 원격으로 관리 하지 않으려면 선택을 취소는 **다른 컴퓨터에서이 서버의 원격 관리 사용** 확인란입니다.

    -   이 컴퓨터는 서버 관리자 또는 Windows PowerShell을 사용 하 여 원격으로 관리할 수 있도록 선택 **다른 컴퓨터에서이 서버의 원격 관리 사용**합니다.

##### <a name="BKMK_ps"></a>Windows PowerShell을 사용 하 여 Windows Server 2012 R2 또는 Windows Server 2012에서 서버 관리자 원격 관리를 사용 하도록 설정 하려면

1.  다음 중 하나를 수행합니다.

    -   관리자 권한으로 Windows PowerShell을 실행 하는 **시작** 화면에서 마우스 오른쪽 단추로 클릭 합니다 **Windows PowerShell** 타일을 마우스 클릭 **관리자 권한으로 실행**합니다.

    -   Windows PowerShell 관리자 권한으로 바탕 화면에서를 실행 하려면 마우스 오른쪽 단추로 클릭는 **Windows PowerShell** 바로 가기를 클릭 한 다음 확인 하 고 작업 표시줄에서 **관리자 권한으로 실행**합니다.

2.  다음을 입력 하 고 다음 키를 누릅니다 **Enter** 필요한 방화벽 규칙 예외를 모두 사용 하도록 설정 합니다.

    **Configure-SMremoting.exe -Enable**

    > [!NOTE]
    > 이 명령은 상승된 사용자 권한(관리자 권한으로 실행)으로 연 명령 프롬프트에서도 사용할 수 있습니다.

    원격 관리를 사용 하도록 설정 하는 작업에 실패 하면, 참조 [about_remote_Troubleshooting](https://go.microsoft.com/fwlink/p/?LinkID=135188) 문제 해결 팁 및 모범 사례에 대 한 Microsoft TechNet에서.

###### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-older-operating-systems"></a>이전 운영 체제에서 서버 관리자 및 Windows PowerShell 원격 관리를 사용하도록 설정하려면

-   다음 중 하나를 수행합니다.

    -   Windows Server 2008 R2를 실행 하는 서버에서 원격 관리를 사용 하려면 [서버 관리자를 사용 하 여 원격 관리](https://go.microsoft.com/fwlink/?LinkID=137378) Windows Server 2008 R2 도움말에서.

    -   Windows Server 2008을 실행 하는 서버에서 원격 관리를 사용 하려면 [을 사용 하도록 설정 하 고 Windows PowerShell에서 원격 명령을 사용 하 여](https://go.microsoft.com/fwlink/p/?LinkId=242565)입니다.

    -   Windows Server 2003을 실행하는 서버에서 원격 관리를 사용하도록 설정하려면 Windows 방화벽에서 WMI DCOM 예외를 사용하도록 설정합니다. Windows Server 2003을 실행하는 서버에서 이 작업을 수행하는 방법에 대한 자세한 내용은 MSDN의 [Windows 방화벽을 통해 연결](https://msdn.microsoft.com/library/aa389286.aspx) 을 참조하세요.

## <a name="BKMK_tasks"></a>서버 관리자에서 수행할 수 있는 작업
서버 관리자 서버 관리를 더 효율적으로 관리자가 단일 도구를 사용 하 여 다음 표에 작업을 수행할 수 있도록 합니다. Windows Server 2012 R2 및 Windows Server 2012에서 모두 서버 표준 사용자와 Administrators 그룹의 구성원 작업을 수행할 수 관리 서버 관리자에서 하지만 기본적으로 표준 사용자는 못하도록 일부 작업을 수행한 다음 표에 나와 있는 것 처럼.

관리자는 서버 관리자 cmdlet 모듈에서 두 개의 Windows PowerShell cmdlet을 사용할 수 있습니다 [Enable-servermanagerstandarduserremoting](https://technet.microsoft.com/library/jj205470.aspx) 하 고 [사용 안 함 ServerManagerStandardUserremoting](https://technet.microsoft.com/library/jj205468.aspx)를 추가 일부 추가 데이터에 대 한 표준 사용자 액세스를 제어 합니다. 합니다 **Enable-servermanagerstandarduserremoting** cmdlet 이벤트, 서비스, 성능 카운터, 역할 및 기능 인벤토리 데이터를 하나 이상의 관리자가 아닌 표준 사용자 액세스를 제공할 수 있습니다.

> [!IMPORTANT]
> Windows Server 운영 체제의 최신 릴리스를 관리 하려면 서버 관리자를 사용할 수 없습니다. Windows Server 2012 r 2를 실행 하는 서버를 관리 하려면 Windows Server 2012 또는 Windows 8에서 실행 되는 서버 관리자를 사용할 수 없습니다.

|태스크 설명|Administrators(기본 제공 관리자 계정 포함)|표준 서버 사용자|
|----------|----------------------------------|-------------|
|서버 관리자가 될 수 있는 서버 풀에 원격 서버 추가 관리 하는 데 사용 합니다.|예|아니오|
|만들고, 특정 지리적 위치에 있는지 또는 특정 목적으로 사용 하는 서버와 같은 서버의 사용자 지정 그룹을 편집 합니다.|예|예|
|설치 또는 역할, 역할 서비스 및 로컬 컴퓨터나 Windows Server 2012 r 2를 실행 하는 원격 서버 또는 Windows Server 2012 기능을 제거 합니다. 역할, 역할 서비스 및 기능 정의 참조 하십시오. [역할, 역할 서비스 및 기능](https://go.microsoft.com/fwlink/p/?LinkId=239558)합니다.|예|아니오|
|로컬 또는 원격 서버에 설치된 서버 역할 및 기능을 보고 변경합니다. **참고:** 서버 관리자에서 역할 및 기능 데이터는 시스템 기본 GUI 언어 또는 운영 체제의 설치 중에 선택한 언어 라고도 하는 시스템의 기본 언어로 표시 됩니다.|예|표준 사용자는 역할 및 기능을 보고 관리하며 역할 이벤트 보기 등과 같은 작업을 수행할 수 있지만 역할 서비스를 추가하거나 제거할 수는 없습니다.|
|Windows PowerShell 또는 mmc 스냅인과 같은 관리 도구를 시작 합니다. 서버를 마우스 오른쪽 단추로 클릭 하 여 원격 서버에서 대상으로 Windows PowerShell 세션을 시작할 수는 **서버** 타일을 클릭 한 다음 마우스 **Windows PowerShell**합니다. mmc 스냅인을 시작할 수 있습니다 합니다 **도구** 가리킵니다 mmc 스냅인 후 원격 컴퓨터에 대해 확인 하 고 서버 관리자 콘솔의 메뉴를 엽니다.|예|예|
|**서버** 타일에서 서버를 마우스 오른쪽 단추로 클릭하고 **다음으로 관리**를 클릭하여 서로 다른 자격 증명을 포함한 원격 서버를 관리합니다. 일반 서버와 File and Storage Services 관리 작업에 대해 **다음으로 관리**를 사용할 수 있습니다.|예|아니오|
|서비스, 시작 또는 중지와 같은 서버의 작동 수명 주기와 연관 된 관리 작업 수행 한 서버 네트워크 설정, 사용자 및 그룹 및 원격 데스크톱 연결을 구성할 수 있도록 하는 다른 도구를 시작 합니다.|예|표준 사용자는 서비스를 시작하거나 중지할 수 없습니다. 로컬 서버 이름, 작업 그룹 또는 도메인 구성원 자격 및 원격 데스크톱 설정을 변경할 수 있지만 사용자 계정 컨트롤에서 이러한 작업을 수행 하기 전에 관리자 자격 증명을 제공 하 라는 메시지가 표시 됩니다. 표준 사용자는 원격 관리 설정은 변경할 수 없습니다.|
|모범 사례 준수를 위한 역할 검사를 포함하여 서버에 설치된 역할의 작동 수명 주기와 관련된 관리 작업을 수행합니다.|예|표준 사용자가 모범 사례 분석기 검사를 실행할 수 없습니다.|
|서버 상태와 중요 이벤트를 확인하고, 구성 문제 또는 실패를 분석하고 문제를 해결합니다.|예|예|
|이벤트, 성능 데이터, 서비스 및 모범 사례 분석기 결과 대 한 서버 관리자 대시보드의 경고를 표시 하려면 사용자 지정 합니다.|예|예|
|서버를 다시 시작합니다.|예|아니오|
|관리 되는 서버에 대 한 서버 관리자 콘솔에 표시 되는 데이터를 새로 고칩니다.|예|아니요|

> [!NOTE]
> 서버 관리자는 Windows Server 2003을 실행 하는 서버에서 온라인 또는 오프 라인 상태만을 받을 수 있습니다. Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행 하는 서버에 역할 및 기능을 추가 하려면 서버 관리자를 사용할 수 없습니다.

## <a name="BKMK_start"></a>서버 관리자를 시작 합니다.
서버 관리자는 기본적으로 서버 관리자 그룹 로그온의 구성원이 Windows Server 2012를 실행 하는 서버에서 자동으로 시작 합니다. 서버 관리자를 닫으면 다음 방법 중 하나에서 다시 시작 합니다. 이 섹션에는 기본 동작을 변경 하 고 서버 관리자가 자동으로 시작을 방지 하기 위한 단계도 포함 되어 있습니다.

#### <a name="to-start-server-manager-from-the-start-screen"></a>시작 화면에서 서버 관리자를 시작 하려면

-   Windows에서 **시작** 화면에서 클릭 합니다 **서버 관리자** 타일입니다.

#### <a name="to-start-server-manager-from-the-windows-desktop"></a>Windows 바탕 화면에서 서버 관리자를 시작하려면

-   Windows 작업 표시줄에서 **서버 관리자**를 클릭합니다.

#### <a name="to-prevent-server-manager-from-starting-automatically"></a>서버 관리자가 자동으로 시작되지 않도록 하려면

1.  서버 관리자 콘솔에서에 **관리** 메뉴 클릭 **서버 관리자 속성**합니다.

2.  **서버 관리자 속성** 대화 상자에서 **로그온 시 서버 관리자를 자동으로 시작 안 함**확인란을 선택합니다. **확인**을 클릭합니다.

3.  또는 그룹 정책 설정을 사용 하 여 자동으로 시작 서버 관리자를 방지할 수 **로그온 시 서버 관리자를 자동으로 시작 않는**합니다. 이 정책 설정은 로컬 그룹 정책 편집기 콘솔에서 경로가 컴퓨터 구성 \ 관리 템플릿 \ 시스템 \ 서버 관리자입니다.

## <a name="BKMK_restart"></a>원격 서버를 다시 시작
원격 서버를 다시 시작할 수는 **서버** 역할이 나 그룹 페이지에서 서버 관리자의 분할 합니다.

> [!IMPORTANT]
> 원격 서버를 다시 시작하면 사용자가 원격 서버에 로그온되어 있는 경우에도 그리고 저장되지 않은 데이터가 포함된 프로그램이 열려 있는 경우에도 서버가 강제로 다시 시작됩니다. 이 동작은 로컬 컴퓨터 종료나 다시 시작과 다릅니다. 로컬 컴퓨터를 종료하거나 다시 시작할 경우에는 저장되지 않은 프로그램 데이터를 저장할지 여부를 묻고, 로그온된 사용자를 강제로 로그오프할 것인지 확인합니다. 원격 서버의 다른 사용자를 강제로 로그오프시키고 원격 서버에서 실행 중인 프로그램의 저장되지 않은 데이터가 무시될 수 있습니다.
> 
> 자동 새로 고침을 관리 되는 서버에서 종료 되 고 새로 고침 및 관리 효율성 상태 오류가 발생할 수 있습니다 관리 되는 서버에 대 한 서버 관리자는 완료 될 때까지 원격 서버에 연결할 수 없습니다를 다시 시작 하는 동안 서버 관리자에서 발생 하는 경우 다시 시작합니다.

#### <a name="to-restart-remote-servers-in-server-manager"></a>서버 관리자에서 원격 서버를 다시 시작하려면

1.  서버 관리자에서 역할 또는 서버 그룹 홈 페이지를 엽니다.

2.  서버 관리자에 추가 된 하나 이상의 원격 서버를 선택 합니다. **Ctrl** 키를 누른 채 클릭하면 한 번에 여러 개의 서버를 선택할 수 있습니다. 서버 관리자 서버 풀에 서버를 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [서버 관리자에 서버 추가](add-servers-to-server-manager.md)합니다.

3.  선택한 서버를 마우스 오른쪽 단추로 클릭한 다음 **서버 다시 시작**을 클릭합니다.

## <a name="BKMK_export"></a>서버 관리자 설정을 다른 컴퓨터로 내보내려면
서버 관리자에서 관리 되는 서버 목록 변경 하 고 서버 관리자 콘솔 설정 및 사용자 지정 그룹을 만든 다음 두 파일에 저장 됩니다. 서버 관리자 (하지 Server Core 설치 옵션을 실행 하는 컴퓨터) 또는 Windows 8의 동일한 릴리스를 실행 하는 다른 컴퓨터에서 이러한 설정을 다시 사용할 수 있습니다. 원격 서버 관리 도구는 해당 컴퓨터에 서버 관리자 설정을 내보내려면 Windows 클라이언트 기반 컴퓨터에서 실행 되어야 합니다.

-   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

-   %*appdata*%\Local\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config

> [!NOTE]
> -   서버 풀의 서버에 대한 다음으로 관리(또는 대체 항목) 자격 증명은 로밍 프로필에 저장되지 않습니다. 서버 관리자 사용자가 이러한 관리 하고자 하는 각 컴퓨터에 추가 해야 합니다.
> -   사용자가 네트워크에 로그온하고 처음으로 로그오프해야 네트워크 공유 로밍 프로필이 만들어집니다. **Serverlist.xml** 파일도 이때 만들어집니다.

서버 관리자 설정을 내보내려면, 서버 관리자 설정을 이식 하거나 다른 컴퓨터에는 다음 두 가지 방법 중 하나에 사용 합니다.

-   다른 도메인에 가입 된 컴퓨터에 설정을 내보내려면, 서버 관리자 사용자에 게 active directory 사용자의에서 로밍 프로필 및 컴퓨터를 구성 합니다. 사용자 active directory에서 사용자 속성 및 컴퓨터를 변경 하려면 도메인 관리자 여야 합니다.

-   설정을 작업 그룹에서 다른 컴퓨터로 내보내려면, 서버 관리자를 사용 하 여 관리 하려는 컴퓨터에서 동일한 위치에 위의 두 파일을 복사 합니다.

#### <a name="to-export-server-manager-settings-to-other-domain-joined-computers"></a>서버 관리자 설정을 다른 도메인 가입 컴퓨터로 내보내려면

1.  Active directory 사용자 및 컴퓨터에서 엽니다는 **속성** 서버 관리자 사용자에 대 한 대화 상자.

2.  에 **프로필** 탭에서 사용자의 프로필을 저장할 네트워크 공유 경로 추가 합니다.

3.  다음 중 하나를 수행합니다.

    -   미국 영어 (en-우리) 작성, 변경 된 **Serverlist.xml** 파일 프로필에 자동으로 저장 됩니다. 다음 단계로 이동합니다.

    -   다른 빌드에는 사용자의 로밍 프로필의 일부인 네트워크 공유에 서버 관리자를 실행 하는 컴퓨터에서 다음 두 파일을 복사 합니다.

        -   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

        -   %*localappdata*%\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config

4.  **확인** 을 클릭하여 변경 내용을 저장하고 **속성** 대화 상자를 닫습니다.

#### <a name="to-export-server-manager-settings-to-computers-in-workgroups"></a>서버 관리자 설정을 작업 그룹의 컴퓨터로 내보내려면

-   원격 서버를 관리 하려는 컴퓨터에서 서버 관리자를 실행 하 고 원하는 설정을 포함 하는 다른 컴퓨터에서 동일한 파일을 다음 두 파일을 덮어씁니다.

    -   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

    -   %*localappdata*%\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config


