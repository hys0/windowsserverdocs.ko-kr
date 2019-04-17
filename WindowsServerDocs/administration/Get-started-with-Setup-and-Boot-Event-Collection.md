---
title: 설치 및 부팅 이벤트 컬렉션 시작
description: 설치 및 부팅 이벤트 컬렉션 수집기 및 목표 설정
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-sbec
ms.localizationpriority: high
ms.date: 10/16/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247b3f8
author: jaimeo
ms.author: jaimeo
ms.openlocfilehash: c21c6f188a95caac79b461300bcc3d6e318f58d8
ms.sourcegitcommit: 8e2903c9b58646840eedd63b47a9bba6c6a06bf7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "1934414"
---
# <a name="get-started-with-setup-and-boot-event-collection"></a>설치 및 부팅 이벤트 컬렉션 시작

>적용 대상: Windows Server

  
## <a name="overview"></a>개요  
설치 및 부팅 이벤트 컬렉션은 부팅하거나 설치 프로세스를 수행할 때 다른 컴퓨터에서 발생하는 중요한 여러 이벤트를 수집할 수 있는 "수집기" 컴퓨터를 지정할 수 있도록 하는 Windows Server 2016의 새로운 기능입니다. 그런 다음 이벤트 뷰어, 메시지 분석기, Wevtutil 또는 Windows PowerShell cmdlet을 통해 수집된 이벤트를 나중에 분석할 수 있습니다.  
  
이전에는 컴퓨터가 아직 설정되지 않은 경우 이벤트를 수집하는 데 필요한 인프라가 존재하지 않으므로 이 이벤트를 모니터링할 수 없었습니다. 모니터링할 수 있는 설치 및 부팅 이벤트의 종류는 다음과 같습니다.  
  
-   커널 모듈 및 드라이버 로드  
  
-   장치 열거 및 해당 드라이버(예: CPU 형식 등의 "장치")의 초기화  
  
-   파일 시스템 확인 및 탑재  
  
-   실행 파일의 시작  
  
-   시작 및 완료된 시스템 업데이트  
  
-   시스템에 대해 로그온을 사용할 수 있을 때, 도메인 컨트롤러와의 연결을 설정할 때, 서비스 완료가 시작할 때, 네트워크 가용성이 공유할 때 지점  
  
수집기 컴퓨터는 Windows Server 2016(데스크톱 경험 또는 Server Core 모드의 서버에서 가능)을 실행해야 합니다. 대상 컴퓨터는 Windows 10 또는 Windows Server 2016을 실행해야 합니다. 또한 이 서비스를 Windows Server 2016을 실행하지 **않는** 가상 컴퓨터에서 실행할 수 있습니다. 다음과 같은 가상화된 수집기 및 대상 컴퓨터의 조합은 작동하는 것으로 알려져 있습니다.  
  
|가상화 호스트|수집기 가상 컴퓨터|대상 가상 컴퓨터|  
|-----------------------|-----------------------------|--------------------------|  
|Windows 8.1|예|예|  
|Windows10|예|예|  
|Windows Server 2016|예|예|  
|WindowsServer 2012 R2|예|아니요|  
  
## <a name="installing-the-collector-service"></a>수집기 서비스 설치  
Windows Server 2016부터 이벤트 수집기 서비스를 선택적인 기능으로 사용할 수 있습니다. 이 릴리스에서 DISM.exe를 사용하여 관리자 권한 Windows PowerShell 프롬프트에서 이 명령으로 설치할 수 있습니다.  
  
`dism /online /enable-feature /featurename:SetupAndBootEventCollection`  
  
이 명령은 BootEventCollector라는 서비스를 만들고 빈 구성 파일로 시작합니다.  
  
`get-service -displayname *boot*`를 검토하여 설치에 성공했는지 확인합니다. 부팅 이벤트 수집기를 실행해야 합니다. 네트워크 서비스 계정에서 실행되며 **%SystemDrive%\ProgramData\Microsoft\BootEventCollector\Config**에 빈 구성 파일(Active.xml)을 만듭니다.  
  
서버 관리자에서 역할 및 기능 추가 마법사를 사용하여 설치 및 부팅 이벤트 컬렉션 서비스를 설치할 수도 있습니다.  
  
## <a name="configuration"></a>구성  
설치 및 부팅 이벤트를 수집하려면 두 항목을 구성해야 합니다.  
  
-   이벤트를 전송할 대상 컴퓨터에서(즉, 설치 및 부팅을 모니터링할 컴퓨터) KDNET/EVENT-NET 전송을 사용하도록 설정하고 이벤트 전달을 사용하도록 설정합니다.  
  
-   수집기 컴퓨터에서 이벤트를 허용할 컴퓨터와 이를 저장할 위치를 지정합니다.  
  
> [!NOTE]  
> 자신에게 시작 또는 부팅 이벤트를 보내도록 컴퓨터를 구성할 수 없습니다. 하지만 두 대의 컴퓨터를 모니터링하려는 경우 이벤트를 서로에게 보낼 수 있도록 구성할 수 있습니다.  
  
### <a name="configuring-a-target-computer"></a>대상 컴퓨터 구성  
각 대상 컴퓨터에서 먼저 KDNET/EVENT-NET 전송을 활성화한 다음 전송을 통해 ETW 이벤트 전송을 활성화하고 대상 컴퓨터를 다시 시작합니다. EVENT-NET은 KDNET(커널 디버거 프로토콜)과 유사한 커널 내 전송 프로토콜입니다. EVENT-NET 이벤트만 전송하고 디버거 액세스를 허용하지 않습니다. 이러한 두 프로토콜은 함께 사용할 수 없습니다. 한번에 둘 중 하나만 사용할 수 있습니다.  
  
이벤트 전송을 원격으로(Windows PowerShell을 사용하여) 또는 로컬로 사용하도록 설정할 수 있습니다.  
  
##### <a name="to-enable-event-transport-remotely"></a>이벤트 전송을 원격으로 사용하도록 설정하려면  
  
1.  이미 대상 컴퓨터에 Windows PowerShell 원격 작업을 설정한 경우 3단계로 건너뜁니다. 그렇지 않은 경우 대상 컴퓨터에서 명령 프롬프트를 열고 다음 명령을 실행합니다.  
  
    winrm quickconfig  
  
2.  프롬프트에 응답하고 대상 컴퓨터를 다시 시작합니다. 대상 컴퓨터가 수집기 컴퓨터와 동일한 도메인에 없는 경우 신뢰할 수 있는 호스트로 정의해야 할 수도 있습니다. 이를 수행하려면 다음과 같이 하세요.  
  
3.  수집기 컴퓨터에서 다음 명령 중 하나를 실행합니다.  
  
    -   Windows PowerShell 프롬프트에서: `Set-Item -Force WSMan:\localhost\Client\TrustedHosts "<target1>,<target2>,..."`와 이어서 `Set-Item -Force WSMan:\localhost\Client\AllowUnencrypted true`. 여기에서 \<target1> 등은 대상 컴퓨터의 이름 또는 IP 주소입니다.  
  
    -   또는 명령 프롬프트에서: **winrm set winrm/config/client @{TrustedHosts="\<target1>,\<target2>,...";AllowUnencrypted="true"}**  
  
        > [!IMPORTANT]  
        > 이는 암호화되지 않은 통신을 설정하므로 랩 환경 외부에서 이를 수행하지 마십시오.  
  
4.  수집기 컴퓨터로 이동한 다음 Windows PowerShell 명령 중 하나를 실행하여 원격 연결을 테스트합니다.  
  
    대상 컴퓨터가 수집기 컴퓨터와 동일한 도메인에 있으면 실행합니다. `New-PSSession -Computer <target> | Remove-PSSession`  
  
    대상 컴퓨터가 동일한 도메인에 없는 경우 `New-PSSession -Computer  <target>  -Credential Administrator | Remove-PSSession`을 실행합니다. 그러면 자격 증명을 요구하는 메시지가 표시됩니다.  
  
    명령이 아무것도 반환하지 않으면 원격 작업에 성공한 것입니다.  
  
5.  대상 컴퓨터에서 관리자 권한 Windows PowerShell 프롬프트를 열고 이 명령을 실행합니다.  
  
    `Enable-SbecBcd -ComputerName <target_name> -CollectorIP <ip> -CollectorPort <port> -Key <a.b.c.d>`  
  
    여기서 <target_name>은 대상 컴퓨터의 이름이고 \<ip>는 수집기 컴퓨터의 IP 주소입니다. \<port>는 수집기를 실행할 포트 번호입니다. <a.b.c.d> 키는 점으로 구분되는 4가지 영숫자 문자열로 구성된 통신에 필요한 암호화 키입니다. 수집기 컴퓨터에서 이 동일한 키를 사용합니다. 키를 입력하지 않으면 시스템은 임의의 키를 생성합니다. 수집기 컴퓨터에 이 키가 필요하므로 기록해둡니다.  
  
6.  이미 수집기 컴퓨터를 설정한 경우 수집기 컴퓨터에서 새 대상 컴퓨터에 대한 정보로 구성 파일을 업데이트합니다. 자세한 내용은 "수집기 컴퓨터 구성" 섹션을 참조하십시오.  
  
##### <a name="to-enable-event-transport-locally-on-the-target-computer"></a>대상 컴퓨터에서 로컬로 이벤트 전송을 사용하도록 설정하려면  
  
1.  관리자 권한 명령 프롬프트를 시작하고 이러한 명령을 실행합니다.  
  
    **bcdedit /event yes**  
  
    **bcdedit /eventsettings net hostip:1.2.3.4 port:50000 key:a.b.c.d**  
  
    여기에서 "1.2.3.4"는 예입니다. 이 숫자를 수집기 컴퓨터의 IP 주소로 교체합니다. 또한 "50000"을 수집기를 실행할 포트 번호로, "a.b.c.d"를 통신에 필요한 암호화 키로 교체합니다. 수집기 컴퓨터에서 이 동일한 키를 사용합니다. 키를 입력하지 않으면 시스템은 임의의 키를 생성합니다. 수집기 컴퓨터에 이 키가 필요하므로 기록해둡니다.  
  
2.  이미 수집기 컴퓨터를 설정한 경우 수집기 컴퓨터에서 새 대상 컴퓨터에 대한 정보로 구성 파일을 업데이트합니다. 자세한 내용은 "수집기 컴퓨터 구성" 섹션을 참조하십시오.  
  
**이제 이벤트 전송이 활성화되었으므로 해당 전송을 통해 시스템이 실제로 ETW 이벤트를 전송하도록 설정해야 합니다.**  
  
##### <a name="to-enable-sending-of-etw-events-through-the-transport-remotely"></a>원격으로 전송을 통해 ETW 이벤트 전송을 활성화하려면  
  
1.  수집기 컴퓨터에서 관리자 권한 Windows PowerShell 프롬프트를 엽니다.  
  
2.  대상 컴퓨터의 이름이 <target_name>인 `Enable-SbecAutologger -ComputerName <target_name>`을 실행합니다.  
  
Windows PowerShell 원격 작업을 설정할 수 없는 경우 항상 대상 컴퓨터에서 직접 이벤트 전송을 활성화할 수 있습니다.  
  
##### <a name="to-enable-sending-of-etw-events-through-the-transport-locally"></a>로컬로 전송을 통해 ETW 이벤트 전송을 활성화하려면  
  
1.  대상 컴퓨터에서 Regedit.exe를 시작하고 이 레지스트리 키를 찾습니다.  
  
    **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WMI\AutoLogger** 다양한 로그 세션이 이 키 아래에 하위 키로 표시됩니다. **설치 플랫폼**, **NT 커널 로거**, **Microsoft-Windows-Setup**은 설치 및 부팅 이벤트 컬렉션과 함께 사용할 수 있는 선택 사항이지만 권장된 옵션은 **EventLog-System**입니다. 이러한 키는 [AutoLogger 세션 구성 및 시작](https://msdn.microsoft.com/library/windows/desktop/aa363687(v=vs.85).aspx)에 자세히 설명되어 있습니다.  
  
2.  EventLog-System 키에서 **LogFileMode**의 값을 **0x10000180**에서 **0x10080180**으로 변경합니다. 이러한 설정의 세부 정보에 대한 자세한 내용은 [모드 상수 로깅](https://msdn.microsoft.com/library/windows/desktop/aa364080(v=vs.85).aspx)을 참조하세요.  
  
3.  필요에 따라 수집기 컴퓨터에 대한 버그 검사 데이터 전달을 사용하도록 설정할 수 있습니다. 이 작업을 수행하려면 레지스트리 키 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager를 찾아 **0x1** 값으로 키 **인쇄 필터 디버그**를 만듭니다.  
  
4.  대상 컴퓨터를 다시 시작합니다.  
  
### <a name="choosing-the-network-adapter"></a>네트워크 어댑터 선택  
대상 컴퓨터에 둘 이상의 네트워크 어댑터가 있는 경우 KDNET 드라이버는 나열된 첫 번째 지원 어댑터를 선택합니다. 다음 단계를 사용하여 설치 이벤트 전달을 사용하기 위해 특정 네트워크 어댑터를 지정할 수 있습니다.  
  
##### <a name="to-specify-a-network-adapter"></a>네트워크 어댑터를 지정하려면  
  
1.  대상 컴퓨터에서 장치 관리자를 열고 **네트워크 어댑터**를 확장하고 사용할 네트워크 어댑터를 찾아 마우스 오른쪽 단추로 클릭합니다.  
  
2.  표시되는 메뉴에서 **속성**을 클릭하고 **세부 정보** 탭을 클릭합니다. **속성** 필드에서 메뉴를 확장하고 스크롤을 내려 **위치 정보**(목록이 알파벳 순서로 정렬되어 있지 않을 수 있음)를 찾아 클릭합니다. 값은 **PCI bus X, device Y, function Z** 형식의 문자열입니다. X.Y.Z를 적어 두십시오. 다음 명령에 필요한 버스 매개 변수입니다.  
  
3.  다음 명령 중 하나를 실행합니다.  
  
    관리자 권한 Windows PowerShell 프롬프트에서: `Enable-SbecBcd -ComputerName <target_name> -CollectorIP <ip> -CollectorPort <port> -Key <a.b.c.d> -BusParams <X.Y.Z>`  
  
    관리자 권한 명령 프롬프트에서: **bcdedit /eventsettings  net hostip:aaa port:50000 key:bbb busparams:X.Y.Z**  
  
### <a name="validate-target-computer-configuration"></a>대상 컴퓨터 구성의 유효성 검사  
대상 컴퓨터에서 설정을 확인하려면 관리자 권한 명령 프롬프트를 열고 **bcdedit /enum**을 실행합니다. 완료되면 **bcdedit /eventsettings**를 실행합니다. 다음 값을 다시 확인할 수 있습니다.  
  
-   키  
  
-   Debugtype = NET  
  
-   Hostip = \ <수집기의 IP 주소>  
  
-   Port = \<사용할 수집기에 대해 지정된 포트 번호>  
  
-   DHCP = yes  
  
또한 **/debug** 및 **/event**를 함께 사용할 수 없으므로 **bcdedit /event**를 활성화했는지 확인하세요. 둘 중 하나만 실행할 수 있습니다. 마찬가지로 /eventsettings를 /debug와, 또는 /dbgsettings를 /event와 혼합할 수 없습니다.  
  
또한 이를 직렬 포트로 설정하는 경우 이벤트 컬렉션이 작동하지 않습니다.  
  
### <a name="configuring-the-collector-computer"></a>수집기 컴퓨터 구성  
수집기 서비스는 이벤트를 수신하고 ETL 파일에 저장합니다. 그러면 이벤트 뷰어, Message Analyzer, Wevtutil, Windows PowerShell cmdlet 등의 다른 도구에서 이러한 ETL을 파일을 읽을 수 있습니다.  
  
ETW 형식이 대상 컴퓨터 이름을 지정하도록 허용하지 않기 때문에 각 대상 컴퓨터에 대한 이벤트를 별도 파일에 저장해야 합니다. 디스플레이 도구가 컴퓨터의 이름을 표시하지 않을 수 있지만 도구가 실행되는 컴퓨터 이름입니다.  
  
보다 정확하게, 각 대상 컴퓨터는 ETL 파일의 링에 할당됩니다. 각 파일 이름은 000에서 사용자가 구성한 최대 값(최대 999)의 인덱스를 포함합니다. 파일이 구성된 최대 크기에 도달하면 다음 파일로 쓰기 이벤트를 전환합니다. 가장 가능성이 높은 파일 이후 다시 파일 인덱스 000으로 전환합니다. 이와 같은 방식으로 파일은 자동으로 재생되며, 디스크 공간 사용량을 제한합니다. 또한 추가 외부 보유 정책을 설정하여 디스크 사용량을 제한할 수도 있습니다. 예를 들면 특정 개수의 날짜보다 오래된 파일을 삭제할 수 있습니다.  
  
수집된 ETL 파일은 일반적으로 **c:\ProgramData\Microsoft\BootEventCollector\Etl** 디렉터리에 보관됩니다(추가 하위 디렉터리가 있을 수 있음). 마지막으로 수정한 시간으로 정렬하여 가장 최근 로그 파일을 찾을 수 있습니다. 또한 수집기가 새 파일에 쓰기로 전환할 때마다 기록하는 상태 로그(보통 **c:\ProgramData\Microsoft\BootEventCollector\Logs**에 위치)도 있습니다.  
  
수집기 자체에 대한 정보를 기록하는 수집기 로그도 있습니다. 이 로그를 ETW 형식(이벤트가 Windows 로그 서비스에 보고됨, 기본값)으로 또는 파일(일반적으로 **c:\ProgramData\Microsoft\BootEventCollector\Logs**)에서 유지할 수 있습니다. 많은 양의 데이터를 생성하는 자세한 정보 표시 모드를 사용하도록 설정하려는 경우 파일을 사용하는 것이 유용할 수 있습니다. 명령줄에서 수집기를 실행하여 표준 출력에 로그를 쓰도록 설정할 수도 있습니다.  
  
**수집기 구성 파일 만들기**  
  
서비스를 활성화하면 세 XML 구성 파일이 만들어져 **c:\ProgramData\Microsoft\ BootEventCollector\Config**에 저장됩니다.  
  
-   **Active.xml** 이 파일은 수집기 서비스의 현재 활성 구성을 포함합니다.  설치 직후 이 파일은 Empty.xml과 동일한 콘텐츠를 가집니다. 새 수집기 구성을 설정한 경우 이 파일에 저장합니다.  
  
-   **Empty.xml** 이 파일은 기본값 설정에 필요한 최소 구성 요소를 포함합니다. 어떤 컬렉션도 활성화하지 않습니다. 수집기 서비스가 유휴 모드에서 시작하는 것만 허용합니다.  
  
-   **Example.xml** 이 파일은 가능한 구성 요소의 예제와 설명을 제공합니다.  
  
**파일 크기 제한 선택**  
  
결정해야 하는 사항 중 하나는 파일 크기 제한을 설정하는 것입니다. 최상의 파일 크기 제한은 예상된 이벤트의 볼륨과 사용 가능한 디스크 공간에 따라 달라집니다. 더 작은 파일은 이전 데이터 정리의 관점에서 볼 때 보다 편리합니다. 그러나 각 파일에는 64KB 헤더의 오버헤드가 수반되며, 결합된 기록을 가져오기 위해 많은 파일을 읽는 것은 번거로울 수 있습니다. 절대 최소 파일 크기 제한은 256KB입니다. 적절한 실용적인 파일 크기 제한은 1MB 이상이어야 하며 10MB가 일반적으로 좋은 값입니다. 많은 이벤트가 예상되는 경우 더 높은 제한이 적절할 수 있습니다.  
  
구성 파일에 대해 주의해야 할 몇 가지 세부 정보가 있습니다.  
  
-   대상 컴퓨터 주소. 해당 IPv4 주소, MAC 주소 또는 SMBIOS GUID를 사용할 수 있습니다. 사용할 주소를 선택할 때 이러한 요소를 염두에 두십시오.  
  
    -   IPv4 주소는 IP 주소의 정적 할당에 적합합니다. 그러나 고정 IP 주소도 DHCP를 통해 사용할 수 있어야 합니다.  
  
    -   MAC 주소 또는 SMBIOS GUID는 미리 알려진 경우 편리하지만 IP 주소는 동적으로 할당됩니다.  
  
    -   IPv6 주소는 EVENT-NET 프로토콜을 통해 지원되지 않습니다.  
  
    -   컴퓨터를 식별하는 방법을 지정할 수 있습니다. 예를 들어 실제 하드웨어를 교체하려고 하는 경우 기존 및 새로운 MAC 주소를 둘 다 입력할 수 있지만 하나만 허용됩니다.  
  
-   수집기 컴퓨터와의 통신에 사용되는 암호화 키  
  
-   대상 컴퓨터의 이름. 컴퓨터 이름으로 IP 주소, 호스트 이름 또는 다른 이름을 사용할 수 있습니다.  
  
-   사용할 ETL 파일의 이름 및 이를 위한 링 크기 구성  
  
##### <a name="to-create-the-configuration-file"></a>구성 파일을 만들려면  
  
1.  관리자 권한 Windows PowerShell 프롬프트를 열고 %SystemDrive%\ProgramData\Microsoft\BootEventCollector\Config로 디렉터리를 변경합니다.  
  
2.  `notepad .\newconfig.xml`을 입력하고 Enter 키를 누릅니다.  
  
3.  이 예제 구성을 Windows 메모장 창에 복사합니다.  
  
    ```  
    <collector configVersionMajor="1" statuslog="c:\ProgramData\Microsoft\BootEventCollector\Logs\statuslog.xml">  
      <common>  
        <collectorport value="50000"/>  
        <forwarder type="etl">  
          <set name="file" value="c:\ProgramData\Microsoft\BootEventCollector\Etl\{computer}\{computer}_{#3}.etl"/>  
          <set name="size" value="10mb"/>  
          <set name="nfiles" value="10"/>  
          <set name="toxml" value="none"/>  
        </forwarder>  
        <target>  
          <ipv4 value="192.168.1.1"/>  
          <key value="a.b.c.d"/>  
          <computer value="computer1"/>  
        </target>  
        <target>  
          <ipv4 value="192.168.1.2"/>  
          <key value="d1.e2.f3.g4"/>  
          <computer value="computer2"/>  
        </target>  
      </common>  
    </collector>  
    ```  
  
    > [!NOTE]  
    > 루트 노드는 \<수집기>입니다. 해당 특성은 구성 파일 구문의 버전 및 상태 로그 파일의 이름을 지정합니다.  
    >   
    > \<common> 요소는 공통 구성 요소를 지정하는 여러 대상을 그룹화합니다. 이와 매우 유사하게 사용자 그룹을 사용하여 여러 사용자에 대한 공통 권한을 지정할 수 있습니다.  
    >   
    > \<collectorport> 요소는 수집기가 수신 데이터의 수신을 대기할 UDP 포트 번호를 정의합니다. 이는 Bcdedit에 대한 대상 구성 단계에서 지정된 것과 동일한 포트입니다. 수집기는 한 개의 포트만 지원하며 모든 대상을 동일한 포트에 연결해야 합니다.  
    >   
    > \<forwarder> 요소는 대상 컴퓨터에서 수신한 ETW 이벤트가 전달되는 방식을 지정합니다. 이벤트를 ETL 파일에 쓰는 전달자의 유형은 한 가지입니다. 매개 변수는 파일 이름 패턴, 링의 각 파일에 대한 크기 제한, 각 컴퓨터에 대한 링의 크기를 지정합니다. 설정 "toxml"은 ETW 이벤트가 수신될 때 XML로 변환하지 않고 이진 형식으로 쓸 수 있음을 지정합니다. 이벤트를 XML로 변환할지 여부를 결정하는 것에 대한 자세한 정보는 "XML 이벤트 변환" 섹션을 참조하십시오. 파일 이름 패턴은 컴퓨터 이름에 대한 {computer} 및 링의 파일 인덱스에 대한 {#3}의 대체를 포함합니다.  
    >   
    > 이 예제 파일에서 두 대상 컴퓨터는 \<target> 요소로 정의됩니다. 각 정의는 \<ipv4>로 IP 주소를 지정하지만 MAC 주소(예: <mac value="11:22:33:44:55:66"\/> 또는 <mac value="11-22-33-44-55-66"\/>) 또는 SMBIOS GUID(예: <guid value="{269076F9-4B77-46E1-B03B-CA5003775B88}"\/>)를 사용하여 대상 컴퓨터를 식별할 수도 있습니다. 암호화 키(지정한 것과 동일하거나 대상 컴퓨터에서 Bcdedit으로 생성된 것과 동일)와 컴퓨터 이름을 기록해 두십시오.  
  
4.  각 대상 컴퓨터에 대한 세부 정보를 구성 파일의 개별 \<target> 요소로 입력한 다음 Newconfig.xml을 저장하고 메모장을 닫습니다.  
  
5.  `$result = (Get-Content .\newconfig.xml | Set-SbecActiveConfig); $result`으로 새 구성을 적용합니다. 출력은 성공 필드 "true"로 반환되어야 합니다. 다른 결과를 얻은 경우 이 항목의 문제 해결 섹션을 참조하십시오.  
  
항상 `(Get-SbecActiveConfig).text`로 현재 활성 구성을 검사할 수 있습니다.  
  
`$result = (Get-Content .\newconfig.xml | Check-SbecConfig); $result`를 사용하여 구성 파일의 유효성 검사를 수행할 수 있습니다.  
  
다시 시작할 필요 없이 새 구성을 적용할 Windows PowerShell 명령은 자동으로 서비스를 업데이트하지만 항상 다음 명령 중 하나를 사용해 서비스를 다시 시작할 수 있습니다.  
  
-   Windows PowerShell 사용: `Restart-Service BootEventCollector`  
  
-   일반 명령 프롬프트에서: **sc stop BootEventCollector; sc start BootEventCollector**  
  
## <a name="configuring-nano-server-as-a-target-computer"></a>Nano 서버를 대상 컴퓨터로 구성  
Nano 서버에서 제공하는 최소한의 인터페이스는 종종 문제를 진단하기가 어렵습니다. 추가 작업 없이 수집기 컴퓨터에 진단 데이터를 보내 자동으로 설치 및 부팅 이벤트 컬렉션에 참여하도록 Nano 서버 이미지를 구성할 수 있습니다. 이렇게 하려면 다음 단계를 따르세요.  
  
#### <a name="to-configure-nano-server-as-a-target-computer"></a>Nano 서버를 대상 컴퓨터로 구성하려면  
  
1.  기본 Nano 서버 이미지를 만듭니다. 자세한 내용은 [Nano 서버 시작](https://technet.microsoft.com/library/mt126167.aspx)을 참조하세요.  
  
2.  이 항목의 "수집기 컴퓨터 구성" 섹션에서와 같이 수집기 컴퓨터를 설정합니다.  
  
3.  진단 메시지를 보낼 수 있도록 AutoLogger 레지스트리 키를 추가합니다. 이 작업을 수행하려면 1단계에서 만든 Nano 서버 VHD를 마운트하고, 레지스트리 하이브를 로드한 후 특정 레지스트리 키를 추가합니다. 이 예에서 Nano 서버 이미지는 C:\NanoServer에 있습니다. 자신의 경로가 다를 수 있으므로 단계를 적절하게 조정하세요.  
  
    1.  수집기 컴퓨터에서 **..\Windows\System32\WindowsPowerShell\v1.0\Modules\BootEventCollector** 폴더를 복사하여 Nano 서버 VHD를 수정하기 위해 사용하는 컴퓨터의 **..\Windows\System32\WindowsPowerShell\v1.0\Modules** 디렉터리에 붙여넣습니다.  
  
    2.  관리자 권한으로 Windows PowerShell 콘솔을 시작하고 `Import-Module BootEventCollector`을 실행합니다.  
  
    3.  Nano 서버 VHD 레지스트리를 업데이트하여 AutoLogger를 사용하도록 설정합니다. 이를 위해 `Enable-SbecAutoLogger -Path C:\NanoServer\Workloads\IncludingWorkloads.vhd`를 실행합니다. 가장 일반적인 설치 및 부팅 이벤트의 기본 목록을 추가합니다. 추가 사항은 [이벤트 추적 세션 제어](https://msdn.microsoft.com/library/windows/desktop/aa363694(v=vs.85).aspx)에서 검색할 수 있습니다.  
  
4.  Nano 서버 이미지의 BCD 설정을 업데이트하여 이벤트 플래그를 활성화하고 수집기 컴퓨터를 설정하여 진단 이벤트가 올바른 서버에 전송되는지 확인합니다. 수집기 컴퓨터의 IPv4 주소, TCP 포트, Active.XML 파일에서 구성한 암호화 키를 주목합니다(이 항목의 다른 곳에서 설명). 관리자 권한으로 Windows PowerShell 콘솔에서 이 명령을 사용합니다. `Enable-SbecBcd -Path C:\NanoServer\Workloads\IncludingWorkloads.vhd -CollectorIp 192.168.100.1 -CollectorPort 50000 -Key a.b.c.d`  
  
5.  IPv4 주소 범위, 특정 IPv4 주소 또는 Nano 서버의 MAC 주소 중 하나를 수집기 컴퓨터의 Active.XML 파일에 추가하여 이벤트를 받기 위해 수집기 컴퓨터를 업데이트합니다(이 항목의 "수집기 컴퓨터 구성" 섹션 참조).  
  
## <a name="starting-the-event-collector-service"></a>이벤트 수집기 서비스 시작  
수집기 컴퓨터에 유효한 구성 파일을 저장하고 대상 컴퓨터를 구성하면 대상 컴퓨터를 다시 시작하는 즉시 수집기에 대한 연결이 설정되고 이벤트가 수집됩니다.  
  
수집기 서비스 자체에 대한 로그(서비스에 의해 수집된 설치 및 부팅 데이터와 다름)는 Microsoft-Windows-BootEvent-Collector/Admin 아래에서 확인할 수 있습니다. 이벤트에 대한 그래픽 인터페이스는 이벤트 뷰어를 사용합니다. 새 보기를 만들고 **응용 프로그램 및 서비스 로그**를 확장한 다음 **Microsoft**, **Windows**를 차례로 확장합니다. **BootEvent-Collector**를 찾아 확장하고 **Admin**을 찾습니다.  

-   Windows PowerShell 사용: `Get-WinEvent -LogName Microsoft-Windows-BootEvent-Collector/Admin`  
  
-   일반 명령 프롬프트에서: **wevtutil qe Microsoft-Windows-BootEvent-Collector/Admin**  
  
## <a name="troubleshooting"></a>문제 해결  
  
### <a name="troubleshooting-installation-of-the-feature"></a>기능 설치 관련 문제 해결  
  
||오류|오류 설명|증상|잠재적 문제|  
|-|---------|---------------------|-----------|---------------------|  
|Dism.exe|87|기능 이름 옵션이 이 컨텍스트에서 인식되지 않습니다.||- 이 문제는 기능 이름이 잘못된 경우에 발생할 수 있습니다. 맞춤법이 올바른지 확인하고 다시 시도합니다.<br />- 이 기능이 사용하는 운영 체제 버전에서 사용할 수 있는지 확인합니다. Windows PowerShell에서 **dism /online /get-features &#124; ?{$_ -match "boot"}** 를 실행합니다. 반환되는 일치가 없으면 이 기능을 지원하지 않는 버전을 실행 중입니다.|  
|Dism.exe|0x800f080c|기능 \<이름>을 알 수 없습니다.||위와 동일|  
  
### <a name="troubleshooting-the-collector"></a>수집기 문제 해결  
  
**로깅:**  
수집기는 자체 이벤트를 ETW 공급자 Microsoft-Windows-BootEvent-Collector로 기록합니다. 수집기에 대한 문제를 해결할 때 살펴보아야 할 첫 번째 사항입니다. 이벤트 뷰어에서 응용 프로그램 아래에서 서비스 로그 > Microsoft > Windows > BootEvent-Collector > Admin에서 찾을 수 있으며, 다음 명령 중 하나를 사용하여 명령 창에서 읽을 수 있습니다.  
  
일반 명령 프롬프트에서: **wevtutil qe Microsoft-Windows-BootEvent-Collector/Admin**  
  
Windows PowerShell 프롬프트에서: `Get-WinEvent -LogName Microsoft-Windows-BootEvent-Collector/Admin`(`-Oldest`를 추가하여 가장 오래된 이벤트부터 시간 순서대로 목록을 반환할 수 있음)  
  
"error"의 로그에서 "warning," "info"(기본값), "verbose", "debug"를 통해 세부 정보 수준을 조정할 수 있습니다. "info"보다 자세한 수준은 대상 컴퓨터가 연결되지 않는 문제를 진단하는 데 유용하지만 많은 양의 데이터를 생성할 수 있으므로 주의해서 사용해야 합니다.  
  
구성 파일의 \<collector> 요소에서 최소 로그 수준을 설정합니다. 예: <collector configVersionMajor="1" minlog\="verbose">  
  
자세한 정보 표시 수준은 처리될 때 수신한 모든 패킷에 대한 레코드를 기록합니다. 디버그 수준은 처리 세부 정보를 추가하고 수신한 모든 ETW 패킷의 콘텐츠도 덤프합니다.  
  
디버그 수준에서 일반적인 로깅 시스템에서 보려고 하지 않고 파일에 로그를 작성하는 것이 유용할 수 있습니다. 이 작업을 수행하려면 구성 파일의 \<collector> 요소에 추가 요소를 추가합니다.  
  
<collector configVersionMajor="1" minlog="debug" log\="c:\ProgramData\Microsoft\BootEventCollector\Logs\log.txt">  
      
 **수집기의 문제를 해결하기 위해 제안된 접근 방식:**  
   
 1. 첫째, 수집기가 대상에서 연결을 수신했는지 확인합니다(대상이 메시지 전송을 시작한 경우에만 파일을 만듭니다).   
```  
Get-SbecForwarding  
```  
이 대상으로부터의 연결이 있음을 반환하는 경우 AutoLogger 설정의 문제일 수 있습니다. 아무 것도 반환하지 않는 경우 문제는 시작할 KDNET 연결과 관련이 있습니다. KDNET 연결 문제를 진단하려면, 양쪽 끝에서(즉, 수집기 및 대상에서) 연결을 확인합니다.  
  
2. 수집기에서 확장된 진단을 보려면 이를 구성 파일의 \<collector> 요소에 추가합니다.  
\<collector ... minlog="verbose">  
이렇게 하면 수신한 받은 패킷에 대한 메시지를 활성화합니다.  
3. 수신된 패킷이 있는지 여부를 확인합니다. 필요에 따라 ETW를 통하지 않고 파일에 직접 자세한 정보 표시 모드에서 로그를 작성하고자 할 수 있습니다. 이 작업을 수행하려면 이를 구성 파일의 \<collector> 요소에 추가합니다.  
\<collector ... minlog="verbose" log="c:\ProgramData\Microsoft\BootEventCollector\Logs\log.txt">  
      
4. 수신된 패킷에 대한 모든 메시지의 이벤트 로그를 확인합니다. 수신된 패킷이 있는지 여부를 확인합니다. 패킷을 수신했지만 잘못된 경우 자세한 내용을 이벤트 메시지에서 확인합니다.  
5. 대상 측에서 KDNET은 레지스트리에 일부 진단 정보를 기록합니다. 찾는 위치   
**HKLM\SYSTEM\CurrentControlSet\Services\kdnet**(메시지용).  
  성공 시 KdInitStatus (DWORD)는 = 0이며 오류 시 오류 코드가 표시됨  
  KdInitErrorString = 오류에 대한 설명(오류가 없는 경우 정보 메시지 포함)  
  
6. 대상에서 Ipconfig.exe를 실행하고 보고하는 장치 이름을 확인합니다. KDNET이 제대로 로드된 경우장치 이름은 원래 공급업체의 카드 이름이 아닌 "kdnic"과 같은 것이어야 합니다.  
7. 대상에 대해 DHCP가 구성되었는지 확인합니다. KDNET에는 DHCP가 절대적으로 필요합니다.  
8. 수집기가 대상과 동일한 네트워크에 있는지 확인합니다. 그렇지 않은 경우 라우팅이 올바르게 구성되었는지, 특히 DHCP에 대한 기본 게이트웨이 설정을 확인합니다.  
  
  
**연결 상태**  
  
`Get-SbecForwarding`으로 데이터가 전달되는 위치에서 설정된 연결 및 정보의 현재 목록을 확인할 수 있습니다.  
  
또한 `Get-SbecHistory`와의 연결에서 상태 변경의 최근 기록을 가져올 수도 있습니다.  
  
### <a name="troubleshooting-setting-a-new-configuration"></a>새 구성 설정 문제 해결  
Windows PowerShell 명령 `$result = (Get-Content .\newconfig.xml | Set-SbecActiveConfig); $result`를 사용하여 구성을 적용한 경우 변수 `$result`에 배포에 대한 정보가 포함됩니다. 이 변수를 쿼리하여 이에 대한 다른 정보를 가져올 수 있습니다.  
  
`$result.ErrorString`을 사용하여 오류에 대한 정보를 가져옵니다. 여기에 오류가 보고되면 새 구성이 적용되지 않았으며 이전 구성이 변경되지 않습니다.  
  
`$result.WarningString`으로 경고를 가져옵니다.  
  
`$result.InfoString`으로 구성에 대한 세부 정보를 가져옵니다.  
  
`$result | fl *`로 전체 결과를 가져올 수 있습니다.  
또는 변수에 결과를 저장하지 않으려는 경우 `Get-Content .\newconfig.xml | Set-SbecActiveConfig | fl *`을 사용할 수 있습니다.  
  
### <a name="troubleshooting-target-computers"></a>대상 컴퓨터의 문제 해결  
  
||오류|오류 설명|증상|잠재적 문제|  
|-|---------|---------------------|-----------|---------------------|  
|대상 컴퓨터||대상이 수집기에 연결되지 않음||- 대상 컴퓨터를 구성한 후 다시 시작하지 않았습니다. 대상 컴퓨터를 다시 시작합니다.<br />- 대상 컴퓨터의 BCD 설정이 잘못되었습니다. "대상 컴퓨터 설정 유효성 검사" 섹션에서 설정을 확인합니다. 필요에 따라 수정하고 대상 컴퓨터를 다시 시작합니다.<br />- KDNET/EVENT-NET 드라이버가 네트워크 어댑터에 연결할 수 없거나 잘못된 네트워크 어댑터에 연결되었습니다. Windows PowerShell에서 `gwmi Win32_NetworkAdapter`를 실행하고 ServiceName **kdnic**으로 한 어댑터에 대한 출력을 확인합니다. 잘못된 네트워크 어댑터를 선택한 경우 "네트워크 어댑터를 지정하려면"의 단계를 다시 수행합니다. 네트워크 어댑터가 전혀 표시되지 않으면, 드라이버가 어떤 네트워크 어댑터도 지원하지 않기 때문일 수 있습니다.<br>**참고 항목** 위의 "수집기의 문제를 해결하기 위해 제안된 접근 방식", 특히 5~8 단계|  
|수집기||내 수집기를 호스팅하는 VM을 마이그레이션한 후 이벤트가 나타나지 않습니다.||수집기 컴퓨터의 IP 주소가 변경되지 않았는지 확인합니다. 변경된 경우 "원격으로 전송을 통해 ETW 이벤트 전송을 활성화하려면"을 검토합니다.|  
|수집기||ETL 파일이 만들어지지 않습니다.|`Get-SbecForwarding` 대상이 오류 없이 연결된 것으로 나타나지만 ETL 파일이 만들어지지 않습니다.|대상 컴퓨터가 아직 데이터를 전송하지 않았을 수 있습니다. ETL 파일은 데이터를 수신할 때에만 만들어집니다.|  
|수집기||ETL 파일에서 이벤트가 표시되지 않습니다.|대상 컴퓨터에서 이벤트를 전송했지만 메시지 분석기의 이벤트 뷰어로 ETL 파일을 읽으면 이벤트가 존재하지 않습니다.|- 이벤트가 버퍼에 있을 수 있습니다. 전체 64KB 버터가 수집될 때까지 또는 새 이벤트가 없는 약 10-15초의 시간 초과가 발생하기 전까지 이벤트가 ETL 파일에 쓰여지지 않습니다. 제한 시간이 만료될 때까지 기다리거나 `Save-SbecInstance`를 사용하여 버퍼를 플러시합니다.<br />- 이벤트 매니페스트를 수집기 컴퓨터 또는 이벤트 뷰어나 메시지 분석기가 실행되는 컴퓨터에서 사용할 수 없습니다.  이 경우 수집기가 이벤트를 처리할 수 없거나(수집기 로그 확인) 뷰어가 이를 표시하지 못할 수 있습니다.  수집기 컴퓨터에 설치된 모든 매니페스트를 포함하고 업데이트를 대상 컴퓨터에 설치하기 전에 수집기 컴퓨터에 설치하는 것이 좋습니다.|