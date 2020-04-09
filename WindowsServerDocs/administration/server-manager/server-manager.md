---
title: 서버 관리자
description: 서버 관리자
ms.prod: windows-server
ms.technology: manage-server-manager
ms.topic: article
ms.assetid: d996ef40-8bcc-42b0-b6ae-806b828223f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41d9227dd5472fc55858d75fa25e728dc69c2c7c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851476"
---
# <a name="server-manager"></a>서버 관리자

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버 관리자는 Windows Server의 관리 콘솔로, IT 전문가가 서버에 물리적으로 액세스 하거나 각 서버에 rdP (원격 데스크톱 프로토콜) 연결을 설정 하지 않고도 데스크톱에서 로컬 및 원격 Windows 기반 서버를 프로 비전 하 고 관리할 수 있도록 도와줍니다. 서버 관리자가 Windows Server 2008 R2 및 Windows Server 2008에서 사용할 수 있지만 서버 관리자는 관리자가 관리할 수는 서버 수가 늘어났으며와 원격 다중 서버 관리를 지원 하려면 Windows Server 2012에서 업데이트 되었습니다.

이 테스트에서 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012의 서버 관리자 데 사용할 수 있는 서버를 실행 하는 작업에 따라 최대 100 명의 서버를 관리 합니다. 단일 서버 관리자 콘솔을 사용 하 여 관리할 수 있는 서버 수는 서버 관리자를 실행 하는 컴퓨터에 사용할 수 있는 하드웨어 및 네트워크 리소스 및 관리 되는 서버에서 요청 하는 데이터의 양에 따라 달라질 수 있습니다. 표시 하려는 데이터의 양이 해당 컴퓨터의 리소스 용량에 가까워지면 느린 응답에서 서버 관리자 및 새로 고침 완료 시 지연이 발생할 수 있습니다. 서버 관리자를 사용 하 여 관리할 수 있는 서버 수를 향상 시키기 위해, 서버 관리자의 설정을 사용 하 여 관리 되는 서버에서 가져오는 이벤트 데이터를 제한 권장는 **이벤트 데이터 구성** 대화 상자입니다. 이벤트 데이터 구성은 **이벤트** 타일의 **작업** 메뉴에서 열 수 있습니다. 조직에 있는 서버는 엔터프라이즈 수준의 수를 관리 해야 하는 경우에 제품을 평가 것이 좋습니다는 [Microsoft System Center 제품군](https://go.microsoft.com/fwlink/p/?LinkId=239437)합니다.

이 항목 및 하위 서버 관리자 콘솔의 기능을 사용 하는 방법에 대 한 정보를 제공 합니다. 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

-   [초기 고려 사항 및 시스템 요구 사항 검토](#review-initial-considerations-and-system-requirements)

-   [서버 관리자에서 수행할 수 있는 작업](#tasks-that-you-can-perform-in-server-manager)

-   [시작 서버 관리자](#start-server-manager)

-   [원격 서버 다시 시작](#restart-remote-servers)

-   [서버 관리자 설정을 다른 컴퓨터로 내보내기](#export-server-manager-settings-to-other-computers)

## <a name="review-initial-considerations-and-system-requirements"></a>초기 고려 사항 및 시스템 요구 사항 검토
다음 섹션에는 하드웨어 및 소프트웨어 요구 사항에 대 한 서버 관리자 뿐만 아니라 검토 해야 하는 몇 개의 초기 고려 나열 합니다.

### <a name="hardware-requirements"></a>하드웨어 요구 사항
서버 관리자는 Windows Server 2016의 모든 버전에는 기본적으로 설치 됩니다. 서버 관리자에 대 한 존재 하는 추가 하드웨어 요구 사항이 없습니다.

### <a name="software-and-configuration-requirements"></a>소프트웨어 및 구성 요구 사항
서버 관리자는 Windows Server 2016의 모든 버전에는 기본적으로 설치 됩니다. Windows Server 2016 서버 관리자를 사용 하 여 관리 하는 수 [Server Core 설치 옵션](https://go.microsoft.com/fwlink/p/?LinkID=241573) Windows Server 2016, Windows Server 2012 및 원격 컴퓨터에서 실행 되는 Windows Server 2008 r 2입니다. 서버 관리자는 Windows Server 2016의 Server Core 설치 옵션에서 실행 됩니다.

서버 관리자가 최소 서버 그래픽 인터페이스;에서 실행 즉, 서버 그래픽 셸 기능이 설치 될 때 되지 않습니다. Windows Server 2016에서 기본적으로 서버 그래픽 셸 기능이 설치 되지 않았습니다. 실행 하지 않는 서버 그래픽 셸, 서버 관리자 콘솔이 실행 되지만 일부 애플리케이션 또는 콘솔에서 사용할 수 있는 도구를 사용할 수 없는. 인터넷 브라우저는 서버 그래픽 셸이 없으면 실행 되지 않으므로 HTML 도움말 (예: mmc F1 도움말)과 같은 웹 페이지 및 응용 프로그램을 열 수 없습니다. 서버 그래픽 셸이 설치 되어 있지 않으면; Windows 자동 업데이트 및 피드백을 구성 하기 위한 대화 상자를 열 수 없습니다. 서버 관리자 콘솔에서 이러한 대화 상자를 열고 명령을 실행 하도록 리디렉션됩니다 **sconfig.cmd**합니다.

Windows Server 2016 보다 오래 된 Windows Server 릴리스를 실행 하는 서버를 관리 하려면 다음 소프트웨어 및 Windows Server 2016에서 서버 관리자를 사용 하 여 이전 버전의 Windows Server를 관리 하기 위해 업데이트를 설치 합니다.

|운영 체제|필수 소프트웨어|
|----------|-----------|
| Windows Server 2012 R2 또는 Windows Server 2012 |-   [.NET Framework 4.6](https://www.microsoft.com/download/details.aspx?id=45497)<br />[Windows Management Framework 5.0](https://go.microsoft.com/fwlink/?LinkID=395058)을 -   합니다. Windows 관리 프레임 워크 5.0 다운로드 패키지는 Windows Server 2012 R2 및 Windows Server 2012에서 Windows Management Instrumentation (WMI) 공급자를 업데이트합니다. 관리 되는 서버에 설치 되어 있는 역할 및 기능에 대 한 정보를 수집 하는 서버 관리자를 사용 하는 업데이트 된 WMI 공급자 있습니다. Windows Server 2012 r 2를 실행 하는 서버 또는 Windows Server 2012의 관리 효율성 상태는 업데이트가 적용 될 때까지 **액세스할 수 없습니다.** 합니다.<br />-성능 업데이트와 관련 된 [기술 자료 문서 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) 은 Windows Server 2012 r 2를 실행 하는 서버 또는 Windows Server 2012에 필요 하지 않습니다.|
| Windows Server 2008 R2 |-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)<br />[Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881)을 -   합니다. Windows Management Framework 4.0 다운로드 패키지는 Windows Server 2008 r 2에서 Windows Management Instrumentation (WMI) 공급자를 업데이트합니다. 관리 되는 서버에 설치 되어 있는 역할 및 기능에 대 한 정보를 수집 하는 서버 관리자를 사용 하는 업데이트 된 WMI 공급자 있습니다. Windows Server 2008 r 2를 실행 하는 서버는 관리 효율성 상태는 업데이트가 적용 될 때까지 **액세스할 수 없습니다.** 합니다.<br />-성능 업데이트와 관련 된 [기술 자료 문서 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) 서버 관리자 Windows Server 2008 r 2에서 성능 데이터를 수집할 수 있습니다.|
| Windows Server 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />windows management framework [3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) -   Windows management framework 3.0 windows Server 2008의 WMI (패키지 업데이트 WMI(Windows Management Instrumentation)) 공급자를 다운로드 합니다. 관리 되는 서버에 설치 되어 있는 역할 및 기능에 대 한 정보를 수집 하는 서버 관리자를 사용 하는 업데이트 된 WMI 공급자 있습니다. 업데이트가 적용 될 때까지 Windows Server 2008를 실행 하는 서버의 관리 효율성 상태는 **액세스할 수 없음-이전 버전에서 Windows Management Framework 3.0를 실행 하는지 확인**합니다.<br />-성능 업데이트와 관련 된 [기술 자료 문서 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) 서버 관리자에서 Windows Server 2008 성능 데이터를 수집할 수 있습니다.|

#### <a name="manage-remote-computers-from-a-client-computer"></a>클라이언트 컴퓨터에서 원격 컴퓨터 관리
서버 관리자 콘솔에 포함 된 [원격 서버 관리 도구](https://go.microsoft.com/fwlink/?LinkID=404281) Windows 10 용입니다. 클라이언트 컴퓨터에 원격 서버 관리 도구를 설치 하면 없습니다 관리할 로컬 컴퓨터의 서버 관리자를 사용 하 여 Windows 클라이언트 운영 체제를 실행 하는 컴퓨터 또는 디바이스를 관리 하려면 서버 관리자를 사용할 수 없습니다. 만 Windows 기반 서버를 관리 하려면 서버 관리자를 사용할 수 있습니다.

|서버 관리자 원본 운영 체제|대상으로 Windows Server 2016|대상으로 Windows Server 2012 R2 |대상으로 Windows Server 2012 |대상으로 Windows Server 2008 R2 또는 Windows Server 2008 |Windows Server 2003 대상|
|-------------------------------|--------------------------------------------|---------------------------------------|------------------------------------|-----------------------------------------------------------------------|------------------|
|Windows 10 또는 Windows Server 2016|전체 지원|전체 지원|전체 지원|[소프트웨어 및 구성 요구 사항](#software-and-configuration-requirements)이 충족되면 대부분의 관리 작업을 수행할 수 있지만 역할이나 기능을 설치하거나 제거하는 작업은 수행할 수 없습니다.|지원되지 않음|
|Windows 8.1 또는 Windows Server 2012 R2 |지원되지 않음|전체 지원|전체 지원|[소프트웨어 및 구성 요구 사항](#software-and-configuration-requirements)이 충족되면 대부분의 관리 작업을 수행할 수 있지만 역할이나 기능을 설치하거나 제거하는 작업은 수행할 수 없습니다.|제한된 지원, 온라인 및 오프라인 상태만 지원|
|Windows 8 또는 Windows Server 2012 |지원되지 않음|지원되지 않음|전체 지원|[소프트웨어 및 구성 요구 사항](#software-and-configuration-requirements)이 충족되면 대부분의 관리 작업을 수행할 수 있지만 역할이나 기능을 설치하거나 제거하는 작업은 수행할 수 없습니다.|제한된 지원, 온라인 및 오프라인 상태만 지원|

###### <a name="to-start-server-manager-on-a-client-computer"></a>클라이언트 컴퓨터에서 서버 관리자를 시작하려면

1.  지침에 따라 [원격 서버 관리 도구](../../remote/remote-server-administration-tools.md) 원격 서버 관리 도구에 대 한 Windows 10을 설치 합니다.

2.  **시작** 화면에서 **서버 관리자**를 클릭 합니다. **서버 관리자** 타일은 원격 서버 관리 도구를 설치한 후에 사용할 수 있습니다.

3.  원격 서버 관리 도구를 설치한 후 **시작** 화면에 **관리 도구** 및 **서버 관리자** 타일이 모두 표시 되지 않고 **시작** 화면에서 서버 관리자를 검색 해도 결과가 표시 되지 않으면 **관리 도구 표시** 설정이 켜져 있는지 확인 합니다. 이 설정을 보려면 **시작** 화면의 오른쪽 위 모서리를 마우스 커서로 가리킨 다음 **설정**을 클릭 합니다. **관리 도구 표시**가 꺼져 있으면 원격 서버 관리 도구의 일부로 설치된 도구를 표시하도록 설정을 켭니다.

Windows 10에서 원격 서버를 관리 하기 위해 원격 서버 관리 도구를 실행 하는 방법에 대 한 자세한 내용은 TechNet Wiki의 [원격 서버 관리 도구](https://go.microsoft.com/fwlink/?LinkID=221055) 을 참조 하십시오.

#### <a name="configure-remote-management-on-servers-that-you-want-to-manage"></a>관리하려는 서버에서 원격 관리 구성

> [!IMPORTANT]
> 기본적으로 Windows Server 2016에서 서버 관리자 및 Windows PowerShell 원격 관리를 사용 합니다.

관리 작업을 수행할 원격 서버에서 서버 관리자를 사용 하 여, 원격 서버를 관리 하려면 서버 관리자 및 Windows PowerShell을 사용 하 여 원격 관리를 허용 하도록 구성 되어야 합니다. Windows Server 2012 R2 또는 Windows Server 2012에서 원격 관리를 사용 하지 않도록 설정 된 경우 다시 활성화 하려면 다음 단계를 수행 합니다.

##### <a name="to-configure-server-manager-remote-management-on--windows-server-2012-r2--or--windows-server-2012--by-using-the-windows-interface"></a>Windows 인터페이스를 사용 하 여 Windows Server 2012 R2 또는 Windows Server 2012에서 서버 관리자 원격 관리를 구성 하려면

1.  > [!NOTE]
    > **원격 관리 구성** 대화 상자에서 제어 하는 설정은 원격 통신에 DCOM을 사용 하는 서버 관리자 부분에 영향을 주지 않습니다.

    아직 열려 있지 않은 경우 서버 관리자를 열려면 다음 중 하나를 수행 합니다.

    -   Windows 작업 표시줄에서 서버 관리자 단추를 클릭 합니다.

    -   **시작** 화면에서 **서버 관리자**를 클릭 합니다.

2.  **로컬 서버** 페이지의 **속성** 영역에서 **원격 관리** 속성에 대 한 하이퍼링크 값을 클릭 합니다.

3.  다음 중 하나를 수행한 다음 **확인**을 클릭합니다.

    -   이 컴퓨터를 서버 관리자 (또는 Windows PowerShell 설치 되어 있는 경우)를 사용 하 여 원격으로 관리 하지 않으려면 선택을 취소는 **다른 컴퓨터에서이 서버의 원격 관리 사용** 확인란입니다.

    -   이 컴퓨터는 서버 관리자 또는 Windows PowerShell을 사용 하 여 원격으로 관리할 수 있도록 선택 **다른 컴퓨터에서이 서버의 원격 관리 사용**합니다.

##### <a name="to-enable-server-manager-remote-management-on--windows-server-2012-r2--or--windows-server-2012--by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 Windows Server 2012 R2 또는 Windows Server 2012에서 서버 관리자 원격 관리를 사용 하도록 설정 하려면

1.  다음 중 하나를 수행합니다.

    -   **시작** 화면에서 관리자 권한으로 windows powershell을 실행 하려면 **windows powershell** 타일을 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.

    -   Windows PowerShell 관리자 권한으로 바탕 화면에서를 실행 하려면 마우스 오른쪽 단추로 클릭는 **Windows PowerShell** 바로 가기를 클릭 한 다음 확인 하 고 작업 표시줄에서 **관리자 권한으로 실행**합니다.

2.  다음을 입력 하 고 **enter** 키를 눌러 필요한 모든 방화벽 규칙 예외를 사용 하도록 설정 합니다.

    **Configure-smremoting.exe-Enable**

    > [!NOTE]
    > 이 명령은 상승된 사용자 권한(관리자 권한으로 실행)으로 연 명령 프롬프트에서도 사용할 수 있습니다.

    원격 관리를 사용 하도록 설정 하지 못한 경우 문제 해결 팁 및 모범 사례는 Microsoft TechNet의 [about_remote_Troubleshooting](https://go.microsoft.com/fwlink/p/?LinkID=135188) 을 참조 하세요.

###### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-older-operating-systems"></a>이전 운영 체제에서 서버 관리자 및 Windows PowerShell 원격 관리를 사용하도록 설정하려면

-   다음 중 하나를 수행합니다.

    -   Windows Server 2008 r 2를 실행 하는 서버에서 원격 관리를 사용 하도록 설정 하려면 Windows Server 2008 R2 도움말의 [서버 관리자 원격 관리](https://go.microsoft.com/fwlink/?LinkID=137378) 를 참조 하세요.

    -   Windows Server 2008를 실행 하는 서버에서 원격 관리를 사용 하도록 설정 하려면 [Windows PowerShell에서 원격 명령 설정 및 사용](https://go.microsoft.com/fwlink/p/?LinkId=242565)을 참조 하세요.

## <a name="tasks-that-you-can-perform-in-server-manager"></a>서버 관리자에서 수행할 수 있는 작업
서버 관리자 서버 관리를 더 효율적으로 관리자가 단일 도구를 사용 하 여 다음 표에 작업을 수행할 수 있도록 합니다. Windows Server 2012 R2 및 Windows Server 2012에서 모두 서버 표준 사용자와 Administrators 그룹의 구성원 작업을 수행할 수 관리 서버 관리자에서 하지만 기본적으로 표준 사용자는 못하도록 일부 작업을 수행한 다음 표에 나와 있는 것 처럼.

관리자는 서버 관리자 cmdlet 모듈 ( [인 enable-servermanagerstandarduserremoting](https://technet.microsoft.com/library/jj205470.aspx) 및 [인 enable-servermanagerstandarduserremoting)](https://technet.microsoft.com/library/jj205468.aspx)에서 두 개의 Windows PowerShell cmdlet을 사용 하 여 추가 데이터에 대 한 표준 사용자 액세스를 추가로 제어할 수 있습니다. **인 enable-servermanagerstandarduserremoting** cmdlet은 이벤트, 서비스, 성능 카운터, 역할 및 기능 인벤토리 데이터에 대 한 액세스 권한이 있는 표준 관리자가 아닌 사용자를 하나 이상 제공할 수 있습니다.

> [!IMPORTANT]
> Windows Server 운영 체제의 최신 릴리스를 관리 하려면 서버 관리자를 사용할 수 없습니다. Windows Server 2012 r 2를 실행 하는 서버를 관리 하려면 Windows Server 2012 또는 Windows 8에서 실행 되는 서버 관리자를 사용할 수 없습니다.

|태스크 설명|Administrators(기본 제공 관리자 계정 포함)|표준 서버 사용자|
|----------|----------------------------------|-------------|
|를 관리 하는 데 사용할 수 서버 관리자 있는 서버 풀에 원격 서버를 추가 합니다.|예|아니요|
|특정 지리적 위치에 있거나 특정 용도를 제공 하는 서버와 같은 사용자 지정 서버 그룹을 만들고 편집 합니다.|예|예|
|설치 또는 역할, 역할 서비스 및 로컬 컴퓨터나 Windows Server 2012 r 2를 실행 하는 원격 서버 또는 Windows Server 2012 기능을 제거 합니다. 역할, 역할 서비스 및 기능 정의 참조 하십시오. [역할, 역할 서비스 및 기능](https://go.microsoft.com/fwlink/p/?LinkId=239558)합니다.|예|아니요|
|로컬 또는 원격 서버에 설치된 서버 역할 및 기능을 보고 변경합니다. **참고:** 서버 관리자에서 역할 및 기능 데이터는 시스템 기본 GUI 언어 또는 운영 체제의 설치 중에 선택한 언어 라고도 하는 시스템의 기본 언어로 표시 됩니다.|예|표준 사용자는 역할 및 기능을 보고 관리하며 역할 이벤트 보기 등과 같은 작업을 수행할 수 있지만 역할 서비스를 추가하거나 제거할 수는 없습니다.|
|Windows PowerShell 또는 mmc 스냅인과 같은 관리 도구를 시작 합니다. **서버 타일에서** 서버를 마우스 오른쪽 단추로 클릭 한 다음 **windows powershell**을 클릭 하 여 원격 서버를 대상으로 하는 windows powershell 세션을 시작할 수 있습니다. 서버 관리자 콘솔의 **도구** 메뉴에서 mmc 스냅인을 시작한 후 스냅인이 열려 있는 후 원격 컴퓨터를 가리키도록 mmc를 지정할 수 있습니다.|예|예|
|**서버** 타일에서 서버를 마우스 오른쪽 단추로 클릭하고 **다음으로 관리**를 클릭하여 서로 다른 자격 증명을 포함한 원격 서버를 관리합니다. 일반 서버와 File and Storage Services 관리 작업에 대해 **다음으로 관리**를 사용할 수 있습니다.|예|아니요|
|서비스, 시작 또는 중지와 같은 서버의 작동 수명 주기와 연관 된 관리 작업 수행 한 서버 네트워크 설정, 사용자 및 그룹 및 원격 데스크톱 연결을 구성할 수 있도록 하는 다른 도구를 시작 합니다.|예|표준 사용자는 서비스를 시작하거나 중지할 수 없습니다. 로컬 서버 이름, 작업 그룹 또는 도메인 구성원 자격 및 원격 데스크톱 설정을 변경할 수 있지만 사용자 계정 컨트롤에서 이러한 작업을 수행 하기 전에 관리자 자격 증명을 제공 하 라는 메시지가 표시 됩니다. 표준 사용자는 원격 관리 설정은 변경할 수 없습니다.|
|모범 사례 준수를 위한 역할 검사를 포함하여 서버에 설치된 역할의 작동 수명 주기와 관련된 관리 작업을 수행합니다.|예|표준 사용자가 모범 사례 분석기 검사를 실행할 수 없습니다.|
|서버 상태와 중요 이벤트를 확인하고, 구성 문제 또는 실패를 분석하고 문제를 해결합니다.|예|예|
|이벤트, 성능 데이터, 서비스 및 모범 사례 분석기 결과 대 한 서버 관리자 대시보드의 경고를 표시 하려면 사용자 지정 합니다.|예|예|
|서버를 다시 시작합니다.|예|아니요|
|관리 되는 서버에 대 한 서버 관리자 콘솔에 표시 되는 데이터를 새로 고칩니다.|예|아니요|

> [!NOTE]
> Windows Server 2008 r 2를 실행 하는 서버 또는 Windows Server 2008로 역할 및 기능을 추가 하려면 서버 관리자를 사용할 수 없습니다.

## <a name="start-server-manager"></a>시작 서버 관리자
서버 관리자는 기본적으로 Windows Server 2016 때 서버 관리자 그룹 로그온의 멤버를 실행 하는 서버에서 자동으로 시작 합니다. 서버 관리자를 닫으면 다음 방법 중 하나에서 다시 시작 합니다. 이 섹션에는 기본 동작을 변경 하 고 서버 관리자가 자동으로 시작을 방지 하기 위한 단계도 포함 되어 있습니다.

#### <a name="to-start-server-manager-from-the-start-screen"></a>시작 화면에서 서버 관리자를 시작 하려면

-   Windows **시작** 화면에서 **서버 관리자** 타일을 클릭 합니다.

#### <a name="to-start-server-manager-from-the-windows-desktop"></a>Windows 바탕 화면에서 서버 관리자를 시작하려면

-   Windows 작업 표시줄에서 **서버 관리자**를 클릭합니다.

#### <a name="to-prevent-server-manager-from-starting-automatically"></a>서버 관리자가 자동으로 시작되지 않도록 하려면

1.  서버 관리자 콘솔에서에 **관리** 메뉴 클릭 **서버 관리자 속성**합니다.

2.  **서버 관리자 속성** 대화 상자에서 **로그온 시 서버 관리자를 자동으로 시작 안 함** 확인란을 선택합니다. **확인**을 클릭합니다.

3.  또는 그룹 정책 설정을 사용 하 여 자동으로 시작 서버 관리자를 방지할 수 **로그온 시 서버 관리자를 자동으로 시작 않는**합니다. 로컬 그룹 정책 editor console에서이 정책 설정의 경로는 computer 시스템 \ 서버 Manager입니다.

## <a name="restart-remote-servers"></a>원격 서버 다시 시작
원격 서버를 다시 시작할 수는 **서버** 역할이 나 그룹 페이지에서 서버 관리자의 분할 합니다.

> [!IMPORTANT]
> 원격 서버를 다시 시작하면 사용자가 원격 서버에 로그온되어 있는 경우에도 그리고 저장되지 않은 데이터가 포함된 프로그램이 열려 있는 경우에도 서버가 강제로 다시 시작됩니다. 이 동작은 로컬 컴퓨터 종료나 다시 시작과 다릅니다. 로컬 컴퓨터를 종료하거나 다시 시작할 경우에는 저장되지 않은 프로그램 데이터를 저장할지 여부를 묻고, 로그온된 사용자를 강제로 로그오프할 것인지 확인합니다. 원격 서버의 다른 사용자를 강제로 로그오프시키고 원격 서버에서 실행 중인 프로그램의 저장되지 않은 데이터가 무시될 수 있습니다.
> 
> 관리 되는 서버가 종료 되 고 다시 시작 되는 동안 서버 관리자에서 자동 새로 고침이 수행 되 면가 다시 시작을 완료할 때까지 원격 서버에 연결할 수 서버 관리자 없으므로 관리 되는 서버에 대해 새로 고침 및 관리 효율성 상태 오류가 발생할 수 있습니다.

#### <a name="to-restart-remote-servers-in-server-manager"></a>서버 관리자에서 원격 서버를 다시 시작하려면

1.  서버 관리자에서 역할 또는 서버 그룹 홈 페이지를 엽니다.

2.  서버 관리자에 추가한 원격 서버를 하나 이상 선택 합니다. **Ctrl** 키를 누른 채 클릭하면 한 번에 여러 개의 서버를 선택할 수 있습니다. 서버를 서버 관리자 서버 풀에 추가 하는 방법에 대 한 자세한 내용은 [서버 관리자에 서버 추가](add-servers-to-server-manager.md)를 참조 하세요.

3.  선택한 서버를 마우스 오른쪽 단추로 클릭한 다음 **서버 다시 시작**을 클릭합니다.

## <a name="export-server-manager-settings-to-other-computers"></a>다른 컴퓨터로 서버 관리자 설정 내보내기
서버 관리자에서 관리 되는 서버 목록 변경 하 고 서버 관리자 콘솔 설정 및 사용자 지정 그룹을 만든 다음 두 파일에 저장 됩니다. 서버 관리자 (또는 원격 서버 관리 도구가 설치 된 Windows 10)의 동일한 릴리스를 실행 하는 다른 컴퓨터에서 이러한 설정을 다시 사용할 수 있습니다. 원격 서버 관리 도구는 해당 컴퓨터에 서버 관리자 설정을 내보내려면 Windows 클라이언트 기반 컴퓨터에서 실행 되어야 합니다.

-   %*appdata*% \ Microsoft\Windows\ServerManager\Serverlist.xml

-   %*appdata*% \ Local \ Microsoft_Corporation \Servermanager. exe_StrongName_*GUID*\6.2.0.0\user.config

> [!NOTE]
> -   서버 풀의 서버에 대한 다음으로 관리(또는 대체 항목) 자격 증명은 로밍 프로필에 저장되지 않습니다. 서버 관리자 사용자가 이러한 관리 하고자 하는 각 컴퓨터에 추가 해야 합니다.
> -   사용자가 네트워크에 로그온하고 처음으로 로그오프해야 네트워크 공유 로밍 프로필이 만들어집니다. **Serverlist.xml** 파일도 이때 만들어집니다.

서버 관리자 설정을 내보내려면, 서버 관리자 설정을 이식 하거나 다른 컴퓨터에는 다음 두 가지 방법 중 하나에 사용 합니다.

-   설정을 도메인에 가입 된 다른 컴퓨터로 내보내려면 사용자가 active directory 사용자 및 컴퓨터에서 로밍 프로필을 갖도록 서버 관리자 구성 합니다. Active directory 사용자 및 컴퓨터에서 사용자 속성을 변경 하려면 도메인 관리자 여야 합니다.

-   설정을 작업 그룹에서 다른 컴퓨터로 내보내려면, 서버 관리자를 사용 하 여 관리 하려는 컴퓨터에서 동일한 위치에 위의 두 파일을 복사 합니다.

#### <a name="to-export-server-manager-settings-to-other-domain-joined-computers"></a>서버 관리자 설정을 다른 도메인 가입 컴퓨터로 내보내려면

1.  Active directory 사용자 및 컴퓨터에서 서버 관리자 사용자에 대 한 **속성** 대화 상자를 엽니다.

2.  에 **프로필** 탭에서 사용자의 프로필을 저장할 네트워크 공유 경로 추가 합니다.

3.  다음 중 하나를 수행합니다.

    -   미국 영어 (en-us) 빌드에서 **serverlist가** 파일에 대 한 변경 내용은 자동으로 프로필에 저장 됩니다. 다음 단계로 이동합니다.

    -   다른 빌드에는 사용자의 로밍 프로필의 일부인 네트워크 공유에 서버 관리자를 실행 하는 컴퓨터에서 다음 두 파일을 복사 합니다.

        -   %*appdata*% \ Microsoft\Windows\ServerManager\Serverlist.xml

        -   %*localappdata*% \ Microsoft_Corporation \Servermanager. exe_StrongName_*GUID*\6.2.0.0\user.config

4.  **확인**을 클릭하여 변경 내용을 저장하고 **속성** 대화 상자를 닫습니다.

#### <a name="to-export-server-manager-settings-to-computers-in-workgroups"></a>서버 관리자 설정을 작업 그룹의 컴퓨터로 내보내려면

-   원격 서버를 관리 하려는 컴퓨터에서 서버 관리자를 실행 하 고 원하는 설정을 포함 하는 다른 컴퓨터에서 동일한 파일을 다음 두 파일을 덮어씁니다.

    -   %*appdata*% \ Microsoft\Windows\ServerManager\Serverlist.xml

    -   %*localappdata*% \ Microsoft_Corporation \Servermanager. exe_StrongName_*GUID*\6.2.0.0\user.config



