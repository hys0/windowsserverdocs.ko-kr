---
title: 설치 및 부팅 이벤트 컬렉션 시작
description: 설치 및 부팅 이벤트 컬렉션 수집기 및 목표 설정
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-sbec
ms.localizationpriority: medium
ms.date: 10/16/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247b3f8
author: jaimeo
ms.author: jaimeo
ms.openlocfilehash: e94659c62db574dc8779c8246d471ab401414ddb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435799"
---
# <a name="get-started-with-setup-and-boot-event-collection"></a>설치 및 부팅 이벤트 컬렉션 시작

>적용 대상: Windows Server

  
## <a name="overview"></a>개요  
다양 한 부팅 하거나 설치 프로세스를 진행 하는 경우 다른 컴퓨터에서 발생 하는 중요 한 이벤트를 수집할 수 있는 "수집기" 컴퓨터를 지정할 수 있도록 허용 하는 Windows Server 2016의 새로운 기능을 설치 하 고 부팅 이벤트를 수집 합니다. 그런 다음 이벤트 뷰어, 메시지 분석기, Wevtutil, 또는 Windows PowerShell cmdlet 통해 수집 된 이벤트를 나중에 분석할 수 있습니다.  
  
이전에 이러한 이벤트를 모니터링할 컴퓨터를 이미 설정 될 때까지 성능 데이터를 수집 하는 데 필요한 인프라가 존재 하지 않아 수 되었습니다 수 있습니다. 모니터링할 수 있는 설정 및 부팅 이벤트의 종류는 다음과 같습니다.  
  
-   드라이버 및 커널 모듈 로드  
  
-   장치 및 해당 드라이버 ("장치" CPU 종류 등 포함)의 초기화 열거형  
  
-   확인 및 파일 시스템  
  
-   실행 파일의 시작  
  
-   시작 및 완료 된 시스템 업데이트  
  
-   도메인 컨트롤러, 네트워크 공유의 가용성 및 서비스를 시작, 완료 된 연결을 설정 하는 시스템 로그온에 사용할 수 있는 지점  
  
수집기 컴퓨터에 Windows Server 2016 (두 서버를 데스크톱 경험 또는 Server Core 모드에 일 수) 실행 되어야 합니다. 대상 컴퓨터는 Windows 10 또는 Windows Server 2016 실행 되어야 합니다. 컴퓨터에서 호스트 되는 가상 컴퓨터에서이 서비스를 실행할 수도 있습니다 **하지** Windows Server 2016를 실행 합니다. 가상화 된 수집기와 대상 컴퓨터의 다음과 같은 조합은 작동 하도록 라고 합니다.  
  
|가상화 호스트|수집기 가상 컴퓨터|대상 가상 컴퓨터|  
|-----------------------|-----------------------------|--------------------------|  
|Windows 8.1|예|예|  
|Windows 10|예|예|  
|Windows Server 2016|예|예|  
|Windows Server 2012 R2|예|no|  
  
## <a name="installing-the-collector-service"></a>수집기 서비스를 설치합니다.  
에서 시작 하 여 Windows Server 2016 이벤트 수집기 서비스를 선택적 기능으로 사용할 수 있습니다. 이 릴리스에서 DISM.exe를 사용 하 여 Windows PowerShell 프롬프트에서이 명령을 사용 하 여 설치할 수 있습니다.  
  
`dism /online /enable-feature /featurename:SetupAndBootEventCollection`  
  
이 명령은 BootEventCollector 라는 서비스를 만들고 빈 구성 파일에 붙습니다.  
  
확인 검사 하 여 설치는 성공 하는 `get-service -displayname *boot*`합니다. 부팅 이벤트 수집기 실행 되어야 합니다. 네트워크 서비스 계정에서 실행 하 고 빈 구성 파일 (Active.xml)에 만듭니다 **%SystemDrive%\ProgramData\Microsoft\BootEventCollector\Config**합니다.  
  
또한 서버 관리자에서 역할 및 기능 추가 마법사를 설치 및 부팅 이벤트 수집 서비스를 설치할 수 있습니다.  
  
## <a name="configuration"></a>Configuration  
설치 및 부팅 이벤트를 수집 하는 두 개의 항목을 구성 해야 합니다.  
  
-   대상 컴퓨터에 있는 이벤트를 전송 합니다 (즉, 설정 및 부팅 된 컴퓨터 모니터링 하려면), 넷 KDNET/이벤트 전송에 사용 하도록 설정 하 고 이벤트 전달을 사용 하도록 설정 합니다.  
  
-   수집기 컴퓨터에서 발생 한 이벤트와 저장 위치를 적용 하려면 컴퓨터를 지정 합니다.  
  
> [!NOTE]  
> 자신에 게 시작 또는 부팅 이벤트를 전송 하는 컴퓨터를 구성할 수 없습니다. 하지만 두 대의 컴퓨터를 모니터링 하려는 경우 서로 이벤트를 보낼 수 있도록를 구성할 수 있습니다.  
  
### <a name="configuring-a-target-computer"></a>대상 컴퓨터를 구성합니다.  
각 대상 컴퓨터에 먼저 넷 KDNET/이벤트 전송에 사용 하도록 설정 다음 ETW 이벤트의 전송을 통해 보낼 수를 대상 컴퓨터를 다시 시작 합니다. NET 이벤트는 KDNET (커널 디버거 프로토콜) 하는 커널에 전송 프로토콜입니다. 만 NET 이벤트는 이벤트를 전송 하 고 디버거 액세스를 허용 하지 않습니다. 이 두 가지 프로토콜은 상호 배타적입니다. 둘 중 한 번에 사용할 수 있습니다.  
  
이벤트 전송 원격 (Windows PowerShell과 함께)을 사용 하도록 설정할 수 또는 로컬로 합니다.  
  
##### <a name="to-enable-event-transport-remotely"></a>이벤트 전송을 원격으로 사용 하도록 설정 하려면  
  
1.  이미 설정한 경우 Windows PowerShell 원격을 대상 컴퓨터에, 3 단계로 건너뜁니다. 그렇지 않은 경우 대상 컴퓨터에서 명령 프롬프트를 열고 하 고 다음 명령을 실행 합니다.  
  
    winrm quickconfig  
  
2.  메시지에 응답 하 고 대상 컴퓨터를 다시 시작 합니다. 대상 컴퓨터는 수집기 컴퓨터와 동일한 도메인에 없는 경우 신뢰할 수 있는 호스트도 정의 해야 합니다. 가상 하드 디스크 파일에 대한 중요 정보를 제공하려면  
  
3.  수집기 컴퓨터에서 다음이 명령 중 하나를 실행 합니다.  
  
    -   Windows PowerShell 프롬프트에서: `Set-Item -Force WSMan:\localhost\Client\TrustedHosts "<target1>,<target2>,..."`, 뒤따릅니다 `Set-Item -Force WSMan:\localhost\Client\AllowUnencrypted true` 여기서 \<target1 > 등은 이름 또는 대상 컴퓨터의 IP 주소입니다.  
  
    -   또는 명령 프롬프트에서: **winrm 설정 winrm/config/client @{TrustedHosts = "\<target1 >,\<target2 >,..."; AllowUnencrypted = "true"}**  
  
        > [!IMPORTANT]  
        > 이 랩 환경 외부에서 이렇게 하지 되므로 암호화 되지 않은 통신을 설정 합니다.  
  
4.  수집기 컴퓨터 하 고 다음 Windows PowerShell 명령 중 하나를 실행 하 여 원격 연결을 테스트 합니다.  
  
    대상 컴퓨터는 수집기 컴퓨터와 동일한 도메인에 있으면 실행 `New-PSSession -Computer <target> | Remove-PSSession`  
  
    대상 컴퓨터는 동일한 도메인에 없는 경우 실행 `New-PSSession -Computer  <target>  -Credential Administrator | Remove-PSSession`, 자격 증명을 묻는 됩니다입니다.  
  
    명령이 아무것도 반환 하지 않습니다, remoting이 했습니다.  
  
5.  대상 컴퓨터에서 관리자 권한 Windows PowerShell 프롬프트를 열고이 명령을 실행 합니다.  
  
    `Enable-SbecBcd -ComputerName <target_name> -CollectorIP <ip> -CollectorPort <port> -Key <a.b.c.d>`  
  
    다음 < target_name >은 대상 컴퓨터의 이름을 \<ip > 수집기 컴퓨터의 IP 주소입니다. \<포트 >는 포트 번호는 수집기가 실행 하는 위치입니다. < A.b.c.d > 키는 통신에 필요한 암호화 키를 점으로 구분 된 4 개의 영숫자 문자열을 구성 합니다. 이 키 수집기 컴퓨터에서 사용 됩니다. 키를 입력 하지 않으면, 시스템에서 임의 키입니다. 수집기 컴퓨터에 대해이 필요 합니다 기록해 둡니다.  
  
6.  설정 하는 수집기 컴퓨터를 이미 있는 경우 새 대상 컴퓨터에 대 한 정보로 수집기 컴퓨터에서 구성 파일을 업데이트 합니다. 자세한 내용은 "수집기 컴퓨터 구성" 섹션을 참조 합니다.  
  
##### <a name="to-enable-event-transport-locally-on-the-target-computer"></a>대상 컴퓨터에서 로컬로 전송 시 이벤트를 사용 하도록 설정 하려면  
  
1.  관리자 권한 명령 프롬프트를 시작 하 고이 명령을 실행 합니다.  
  
    **bcdedit /event 예**  
  
    **bcdedit /eventsettings net hostip:1.2.3.4 포트: 50000 key: a.b.c.d**  
  
    여기 "1.2.3.4"은 예입니다. 수집기 컴퓨터의 IP 주소로 대체 합니다. 또한 통신에 필요한 암호화 키가 있는 "50000을" "a.b.c.d" 및 포트 번호는 수집기가 실행 될 위치와 바꿉니다. 이 키 수집기 컴퓨터에서 사용 됩니다. 키를 입력 하지 않으면, 시스템에서 임의 키입니다. 수집기 컴퓨터에 대해이 필요 합니다 기록해 둡니다.  
  
2.  설정 하는 수집기 컴퓨터를 이미 있는 경우 새 대상 컴퓨터에 대 한 정보로 수집기 컴퓨터에서 구성 파일을 업데이트 합니다. 자세한 내용은 "수집기 컴퓨터 구성" 섹션을 참조 합니다.  
  
**이벤트 전송 자체는 사용 하도록 설정 했으므로 실제로 해당 전송을 통해 ETW 이벤트를 전송 하려면 시스템을 활성화 해야 합니다.**  
  
##### <a name="to-enable-sending-of-etw-events-through-the-transport-remotely"></a>ETW 이벤트 전송을 통해 보내는 원격으로 사용 하도록 설정 하려면  
  
1.  수집기 컴퓨터에서 관리자 권한 Windows PowerShell 프롬프트를 엽니다.  
  
2.  실행 `Enable-SbecAutologger -ComputerName <target_name>`, 여기서 < target_name >은 대상 컴퓨터의 이름입니다.  
  
Windows PowerShell 원격을 설정할 수 없는 경우 대상 컴퓨터에 직접 이벤트를 보내는 항상 사용할 수 있습니다.  
  
##### <a name="to-enable-sending-of-etw-events-through-the-transport-locally"></a>로컬로 전송을 통해 ETW 이벤트를 보내는 사용 하도록 설정 하려면  
  
1.  대상 컴퓨터에 Regedit.exe를이 레지스트리 키를 찾습니다.  
  
    **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WMI\AutoLogger**합니다. 다양 한 로그 세션은이 키 아래에 하위 키로 나열 됩니다. **플랫폼 설정**, **NT 커널으로 거**, 및 **Microsoft Windows 설정** 설정 및 부팅 이벤트를 수집, 사용 가능한 옵션을 선택할 수 있지만 권장된 옵션은 **이벤트 로그 시스템**합니다. 이러한 키에 자세히 설명 되어 [AutoLogger 세션 구성 및 시작할](https://msdn.microsoft.com/library/windows/desktop/aa363687(v=vs.85).aspx)합니다.  
  
2.  이벤트 로그 시스템 키에서 값을 변경 **LogFileMode** 에서 **0x10000180** 에 **0x10080180**합니다. 이러한 설정의 세부 정보에 대 한 자세한 내용은 참조 [로깅 모드 상수](https://msdn.microsoft.com/library/windows/desktop/aa364080(v=vs.85).aspx)합니다.  
  
3.  필요에 따라 버그는 수집기 컴퓨터에 데이터를 검사 한 전달을 활성화할 수 있습니다. 이 작업을 수행 하려면 레지스트리를 찾아 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager 키 및 키를 만들 **디버그 인쇄 필터** 값이 **0x1**합니다.  
  
4.  대상 컴퓨터를 다시 시작 합니다.  
  
### <a name="choosing-the-network-adapter"></a>네트워크 어댑터를 선택합니다.  
대상 컴퓨터에 둘 이상의 네트워크 어댑터가 있는 경우 첫 번째 표에 나열 된 지원 KDNET 드라이버를 선택 합니다. 다음이 단계를 사용 하 여 설치 이벤트를 전달 하기 위해 사용 하 여 특정 네트워크 어댑터를 지정할 수 있습니다.  
  
##### <a name="to-specify-a-network-adapter"></a>네트워크 어댑터를 지정 하려면  
  
1.  대상 컴퓨터에서 장치 관리자를 열고 확장 **네트워크 어댑터**, 를 사용 하려면 네트워크 어댑터를 찾을 마우스 오른쪽 단추로 클릭 합니다.  
  
2.  열리는 메뉴에서 **속성**, 를 클릭 하 고는 **세부 정보** 탭 합니다. 메뉴를 확장 하 고는 **속성** 필드, 스크롤 찾을 수 **위치 정보** (목록은 아닐 알파벳 순서로 정렬), 다음을 클릭 합니다. 값 형식의 문자열 됩니다 **PCI 버스 X, Y 장치, Z 함수**합니다. X.Y.Z; 기록 이들은 다음 명령에 대 한 필요한 버스 매개 변수입니다.  
  
3.  이러한 명령 중 하나를 실행 합니다.  
  
    관리자 권한 Windows PowerShell 프롬프트: `Enable-SbecBcd -ComputerName <target_name> -CollectorIP <ip> -CollectorPort <port> -Key <a.b.c.d> -BusParams <X.Y.Z>`  
  
    관리자 권한 명령 프롬프트에서: **bcdedit /eventsettings net hostip:aaa 포트: 50000 키: bbb busparams:X.Y.Z**  
  
### <a name="validate-target-computer-configuration"></a>대상 컴퓨터 구성의 유효성을 검사합니다  
대상 컴퓨터에서 설정을 확인 하려면 관리자 권한 명령 프롬프트를 열고 실행 **bcdedit /enum**합니다. 다음 실행이 완료 되 면 **bcdedit /eventsettings**합니다. 다음 값을 다시 확인 수 있습니다.  
  
-   Key  
  
-   Debugtype = NET  
  
-   Hostip = \<수집기의 IP 주소 >  
  
-   포트 = \<수집기를 사용 하는 데 지정 된 포트 번호 >  
  
-   DHCP = 예  
  
또한 설정 했는지 확인 **bcdedit /event**, 이후 **디버그** 및 **/event** 함께 사용할 수 없습니다. 둘 중 하나 에서만 실행할 수 있습니다. 마찬가지로, /eventsettings /debug 또는 /dbgsettings /event와 혼합할 수 없습니다.  
  
또한 note 직렬 포트에 설정 하는 경우 이벤트 수집 작동 하지 않습니다.  
  
### <a name="configuring-the-collector-computer"></a>수집기 컴퓨터를 구성합니다.  
수집기 서비스 이벤트를 수신 하 고 ETL 파일에 저장 합니다. 이러한 ETL 파일 수 읽을 수 이벤트 뷰어와 같은 다른 도구를 통해 메시지 분석기, Wevtutil 및 Windows PowerShell cmdlet.  
  
ETW 형식을 허용 하지 않으면 대상 컴퓨터 이름을 지정할 수 있으므로 각 대상 컴퓨터에 대 한 이벤트를 별도 파일에 저장 해야 합니다. 표시 도구는 컴퓨터 이름이 표시 될 수 있습니다 않으며 도구가 실행 되는 컴퓨터의 이름이 됩니다.  
  
보다 정확 하 게 각 대상 컴퓨터는 링 ETL 파일에 할당 됩니다. 각 파일 이름 (최대 999)를 구성 하는 최대 값으로 000에서 인덱스를 포함 합니다. 파일에서 구성 된 최대 크기에 도달 하면 다음 파일에 쓰기 이벤트를 전환 합니다. 가능한 가장 높은 파일 후 파일 000 인덱스를 다시를 전환 됩니다. 이러한 방식으로 파일은 자동으로 재활용의 디스크 공간 사용량을 제한 합니다. 디스크 사용량; 더욱 제한 하려면 추가 외부 보존 정책을 설정할 수도 있습니다. 예를 들어 일 수 집합 보다 오래 된 파일을 삭제할 수 있습니다.  
  
수집 된 ETL 파일은 일반적으로 디렉터리에 보관 **c:\ProgramData\Microsoft\BootEventCollector\Etl** (있는 하위 디렉터리). 마지막으로 수정한 시간으로 정렬 하 여 가장 최근의 로그 파일을 찾을 수 있습니다. 또한 상태 로그 (보통 **c:\ProgramData\Microsoft\BootEventCollector\Logs**), 새 파일에 쓰기를 전환 하는 수집기 때마다 레코드입니다.  
  
자체는 수집기에 대 한 정보를 기록 하는 수집기 로그 이기도 합니다. ETW 형식 (있는 Windows 로그 서비스에 이벤트를 보고, 기본값) 또는 파일에서이 로그를 유지할 수 있습니다 (일반적으로 **c:\ProgramData\Microsoft\BootEventCollector\Logs**). 파일을 사용 하는 많은 양의 데이터를 생성 하는 자세한 정보 표시 모드를 사용 하도록 설정 하려는 경우에 유용할 수 있습니다. 명령줄에서 수집기를 실행 하 여 표준 출력에 쓸 로그를 설정할 수 있습니다.  
  
**수집기 구성 파일 만들기**  
  
세 개의 XML 구성 파일을 만들고에 저장 된 서비스를 사용 하는 경우 **c:\ProgramData\Microsoft\BootEventCollector\Config**:  
  
-   **Active.xml** 이 파일에는 수집기 서비스의 현재 활성 구성을 포함 합니다.  바로 설치 후이 파일의 내용이 동일한 Empty.xml. 새 수집기 구성을 설정 하는 경우이 파일에 저장 합니다.  
  
-   **Empty.xml** 이 파일에 포함 최소 구성 요소 필요를 해당 기본값으로 설정 됩니다. 모든 컬렉션을 사용 하지 않는 수집기 서비스를 유휴 모드에서 시작 하도록 허용 합니다.  
  
-   **Example.xml** 이 파일은 예제와 설명이 가능한 구성 요소를 제공 합니다.  
  
**최대 파일 크기를 선택합니다.**  
  
파일 크기 제한을 설정 해야 할 결정 사항 중 하나입니다. 최상의 파일 크기 제한을 이벤트 및 사용 가능한 디스크 공간이 예상된 볼륨에 따라 달라 집니다. 더 작은 파일은 이전 데이터 정리의 관점에서 더 편리 합니다. 그러나 각 파일에는 저마다 64 KB 헤더의 오버 헤드가 있으며 많은 파일을 결합된 한 기록 읽기 불편할 수 있습니다. 절대 최소 파일 크기 제한은 256KB입니다. 적절 한 실제 파일 크기 제한을 1MB 이상 이어야 합니다 10MB는 아마도 좋은 일반적인 값입니다. 더 높은 한도 많은 이벤트를 예상 하는 경우 적절 한 수 있습니다.  
  
자세한 정보는 구성 파일에 대 한 염두에 두 가지가 있습니다.  
  
-   대상 컴퓨터의 주소입니다. IPv4 주소, MAC 주소 또는 SMBIOS GUID를 사용할 수 있습니다. 사용 하는 주소를 선택할 때 이러한 요소를 염두에 두십시오.  
  
    -   IPv4 주소는 IP 주소의 정적 할당 적합합니다. 그러나도 고정 IP 주소는 DHCP를 통해 사용할 수 있어야 합니다.  
  
    -   MAC 주소 또는 SMBIOS GUID이 사전에 확인 되었지만 IP 주소를 동적으로 할당 된 경우에 편리 합니다.  
  
    -   IPv6 주소는 NET 이벤트 프로토콜에서 지원 되지 않습니다.  
  
    -   컴퓨터를 식별 하는 여러 방법을 지정 하는 것이 불가능 합니다. 예를 들어 물리적 하드웨어를 교체할 경우 기존 및 새 MAC 주소를 입력할 수 있는 및 하거나 수락 합니다.  
  
-   수집기 컴퓨터와의 통신에 사용 되는 암호화 키  
  
-   대상 컴퓨터의 이름입니다. 컴퓨터 이름으로 IP 주소, 호스트 이름 또는 다른 이름을 사용할 수 있습니다.  
  
-   사용 하 고 링 크기 구성에 대 한 ETL 파일의 이름  
  
##### <a name="to-create-the-configuration-file"></a>구성 파일을 만들려면  
  
1.  관리자 권한 Windows PowerShell 프롬프트를 열고 %SystemDrive%\ProgramData\Microsoft\BootEventCollector\Config 디렉터리를 변경 합니다.  
  
2.  형식 `notepad .\newconfig.xml` ENTER 키를 누릅니다.  
  
3.  이 예제에서는 구성 메모장 창에 복사 합니다.  
  
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
    > 루트 노드는 \<수집기 >. 해당 특성의 구성 파일 구문 버전 및 상태 로그 파일의 이름을 지정합니다.  
    >   
    > \<일반적인 > 요소를 함께 그룹화 여러 대상을 지정 하는 공통 구성 요소 그대로 거의 같은 여러 사용자에 대 한 일반적인 사용 권한을 지정 하는 사용자 그룹을 사용할 수 있습니다.  
    >   
    > \<collectorport > 요소는 들어오는 데이터에 대 한 수집기를 수신 대기할 UDP 포트 번호를 정의 합니다. Bcdedit에 대 한 대상 구성 단계에서 지정 된 것과 동일한 포트입니다. 수집기 포트를 하나만 지원 하 고 모든 대상에서 동일한 포트에 연결 해야 합니다.  
    >   
    > \<전달자 > 요소는 대상 컴퓨터에서 수신 하는 ETW 이벤트는 전달 하는 방법을 지정 합니다. ETL 파일에 기록 하는 전달자의 한 가지 형식만이 있습니다. 매개 변수는 파일 이름 패턴을 각 컴퓨터에 대 한 각 파일에는 링과 링의 크기에 대 한 크기 제한을 지정합니다. "설정"toxml ETW 이벤트 수신 되는, XML로 변환 하지 않고으로 이진 형식으로 기록 됩니다 지정 합니다. 또는 XML로 이벤트를 부여 하지 않을 지 여부를 결정 하는 방법에 대 한 정보에 대 한 "XML 이벤트 변환" 섹션을 참조 합니다. 이러한 대체 단어를 포함 하는 파일 이름 패턴: {컴퓨터} 컴퓨터 이름 및 {# 3을 (를)에 대 한 링에는 파일의 인덱스입니다.  
    >   
    > 이 예제에서는 파일에 두 개의 대상 컴퓨터 정의 \<대상 > 요소입니다. 각 정의 된 IP 주소를 지정 합니다. \<ipv4 >, MAC 주소를 사용할 수도 있지만 (예를 들어 < mac 값 = "11:22:33:44:55:66"\/> 또는 < value="11-22-33-44-55-66 mac"\/>) 또는 SMBIOS GUID (예를 들어 < guid 값 "{269076F9-4B77-46E1-B03B-CA5003775B88}" =\/>) 대상 컴퓨터를 식별 합니다. 암호화 키 (동일 지정 하거나 대상 컴퓨터에서 Bcdedit를 사용 하 여 생성 된) 및 컴퓨터 이름의 note도 합니다.  
  
4.  별도의 각 대상 컴퓨터에 대 한 세부 정보를 입력 \<대상 > 요소 구성 파일을 선택한 후 저장 Newconfig.xml 및 메모장을 닫습니다.  
  
5.  사용 하 여 새 구성을 적용 `$result = (Get-Content .\newconfig.xml | Set-SbecActiveConfig); $result`합니다. 출력은 성공 필드 "true입니다."와 되돌아가야 합니다. 다른 결과 얻으려면이 항목의 문제 해결 섹션을 참조 합니다.  
  
현재 활성 구성으로 검사할 수 `(Get-SbecActiveConfig).text`합니다.  
  
사용 하 여 구성 파일의 유효성 검사를 수행할 수 있습니다 `$result = (Get-Content .\newconfig.xml | Check-SbecConfig); $result`합니다.  
  
다시 시작할 필요 없이 서비스를 업데이트 하는 자동으로 새 구성을 적용 하려면 Windows PowerShell 명령, 경우에 항상 다시 시작할 수 있습니다 서비스 직접 사용 하 여 다음이 명령 중:  
  
-   Windows powershell: `Restart-Service BootEventCollector`  
  
-   일반 명령 프롬프트에: **BootEventCollector 중지 sc; sc BootEventCollector 시작**  
  
## <a name="configuring-nano-server-as-a-target-computer"></a>대상 컴퓨터와 Nano 서버 구성  
Nano 서버에 의해 제공 되는 최소 인터페이스 때로는 하기가 더 된 문제를 진단 하기 어려운 합니다. 사용자에 게 서 추가 개입 없이 수집기 컴퓨터에 진단 데이터를 전송 자동으로 설치 및 부팅 이벤트 수집에 참여 하 여 Nano 서버 이미지를 구성할 수 있습니다. 이렇게 하려면 다음 단계를 수행합니다.  
  
#### <a name="to-configure-nano-server-as-a-target-computer"></a>대상 컴퓨터와 Nano 서버를 구성 하려면  
  
1.  기본 Nano 서버 이미지를 만듭니다. 참조 [Nano 서버 시작](https://technet.microsoft.com/library/mt126167.aspx) 대 한 자세한 내용은 합니다.  
  
2.  이 항목의 "수집기 컴퓨터 구성" 섹션에서와 같이 수집기 컴퓨터를 설정 합니다.  
  
3.  진단 메시지를 보낼 수 있도록 AutoLogger 레지스트리 키를 추가 합니다. 1 단계에서에서 만든 Nano 서버 VHD를 탑재 합니다. 이렇게 하려면 레지스트리 하이브를 로드 고 특정 레지스트리 키를 추가 합니다. 이 예에서 Nano 서버 이미지 C:\NanoServer;에 경로는 다를 수, 있으므로 단계를 적절 하 게 조정 수도 있습니다.  
  
    1.  수집기 컴퓨터에서 복사 된 **... \Windows\System32\WindowsPowerShell\v1.0\Modules\BootEventCollector** 폴더에 붙여 넣을 **... \Windows\System32\WindowsPowerShell\v1.0\Modules** 디렉터리 Nano 서버 VHD를 수정 하는 데 사용 하는 컴퓨터에 있습니다.  
  
    2.  승격 된 권한으로 Windows PowerShell 콘솔을 시작 하 고 실행 `Import-Module BootEventCollector` 합니다.  
  
    3.  AutoLoggers 사용할 수 있도록 Nano 서버 VHD 레지스트리를 업데이트 합니다. 이 위해 실행 `Enable-SbecAutoLogger -Path C:\NanoServer\Workloads\IncludingWorkloads.vhd`합니다. 가장 일반적인 설치 및 부팅 이벤트;의 기본 목록 추가 다른 사용자를 알아보고 [이벤트 추적 세션을 제어](https://msdn.microsoft.com/library/windows/desktop/aa363694(v=vs.85).aspx)합니다.  
  
4.  이벤트 플래그를 설정 하 고 올바른 서버에 전송 되 게 진단 이벤트 수집기 컴퓨터를 설정 하려면 Nano 서버 이미지에 BCD 설정을 업데이트 합니다. Note 수집기 컴퓨터의 IPv4 주소, TCP 포트 및 암호화 키 (이 항목에서 다른 곳에서 설명)는 수집기 Active.XML 파일에서 구성 합니다. 관리자 권한으로 Windows PowerShell 콘솔에서이 명령을 사용 합니다. `Enable-SbecBcd -Path C:\NanoServer\Workloads\IncludingWorkloads.vhd -CollectorIp 192.168.100.1 -CollectorPort 50000 -Key a.b.c.d`  
  
5.  수집기 컴퓨터에서 Active.XML 파일에 IPv4 주소 범위, 특정 IPv4 주소 또는 Nano 서버의 MAC 주소를 추가 하 여 Nano 서버 컴퓨터에서 보낸 이벤트를 받도록 수집기 컴퓨터 업데이트 (이 항목의 "수집기 컴퓨터 구성" 섹션 참조).  
  
## <a name="starting-the-event-collector-service"></a>이벤트 수집기 서비스를 시작합니다.  
수집기 컴퓨터에서 유효한 구성 파일을 저장 하 고 대상 컴퓨터 구성 된 대상 컴퓨터를 다시 시작, 수집기에 연결 되 고 이벤트를 수집 합니다.  
  
(이 서비스에 의해 수집 된 설정 및 부팅 데이터 구분) 수집기 서비스 자체에 대 한 로그는 Microsoft-Windows-BootEvent-수집기/관리자에서 찾을 수 있습니다. 이벤트에 대 한 그래픽 인터페이스에 대 한 이벤트 뷰어를 사용 합니다. 새 보기, 만들기 확장 **응용 프로그램 및 서비스 로그**, 를 확장 한 다음 **Microsoft** 차례로 **Windows**합니다. 찾을 **BootEvent 수집기**, 확장 하 고 찾을 **Admin**합니다.  

-   Windows powershell: `Get-WinEvent -LogName Microsoft-Windows-BootEvent-Collector/Admin`  
  
-   일반 명령 프롬프트에: **wevtutil qe Microsoft-Windows-BootEvent-수집기/관리**  
  
## <a name="troubleshooting"></a>문제 해결  
  
### <a name="troubleshooting-installation-of-the-feature"></a>기능의 설치 문제 해결  
  
||Error|오류 설명|증상|잠재적인 문제|  
|-|---------|---------------------|-----------|---------------------|  
|Dism.exe|87|기능 이름 옵션은이 컨텍스트에서 아닙니다.||-이 기능 이름이 잘못 된 경우 발생할 수 있습니다. 올바른 철자 있고 다시 시도 확인 합니다.<br />-이 기능은 사용 중인 운영 체제 버전에서 사용할 수 있는지 확인 합니다. Windows PowerShell에서 실행 **dism /online /get-features &#124; ?{$_ -"부팅"과 일치}** 합니다. 일치 하는 항목이 반환 되 면이 기능을 지원 하지 않는 버전을 실행 아마도 해야 합니다.|  
|Dism.exe|0x800f080c|기능 \<이름 >를 알 수 없습니다.||위와 동일|  
  
### <a name="troubleshooting-the-collector"></a>수집기 문제 해결  
  
**로깅:**  
수집기는 ETW 공급자 Microsoft Windows-BootEvent 수집기 고유한 이벤트를 기록합니다. 이 수집기와 함께 문제 해결을 위한 같아야 합니다. 첫 번째 위치입니다. 이벤트 뷰어에서 응용 프로그램 및 서비스 로그에서 찾을 수 있습니다 > Microsoft > Windows > BootEvent 수집기 > 관리자 또는 사용자에서 읽을 수 명령 창을 사용 하 여 다음이 명령 중:  
  
일반 명령 프롬프트에: **wevtutil qe Microsoft-Windows-BootEvent-수집기/관리**  
  
Windows PowerShell 프롬프트에서: `Get-WinEvent -LogName Microsoft-Windows-BootEvent-Collector/Admin` (추가할 수 있습니다 `-Oldest` 을 반환 하는 가장 오래 된 이벤트와 함께 시간 순서 대로 먼저)  
  
"" 오류 "경고"를 통해에서 로그에 대 한 세부 정보 수준을 조정할 수 있습니다 (기본값) "info", "verbose" 및 "debug"입니다. 보다 자세한 수준 보다 "info"는 대상 컴퓨터를 연결 하지 않으면 문제를 진단 하는 데 유용 하지만 많은 양의 데이터를 생성 될 수 있습니다 따라서 사용에 주의 하 여 합니다.  
  
최소 로그 수준에 설정 된 \<수집기 > 구성 파일의 요소입니다. 예: < 수집기 configVersionMajor = "1" minlog\="verbose" >.  
  
자세한 정보 표시 수준 모든 패킷이 처리 되는 동안 수신에 대 한 레코드를 기록 합니다. 디버그 수준 자세히 처리를 추가 하 고 수신된 된 모든 ETW 패킷에의 콘텐츠를 덤프 합니다.  
  
디버그 수준에서 일반적인 로깅 시스템에서에 보려고 하는 대신 파일에 로그를 쓰는 것이 유용할 수 있습니다. 이 위해 추가 요소에 추가 된 \<수집기 > 구성 파일의 요소:  
  
< 수집기 configVersionMajor "1" minlog = = "debug" 로그\="c:\ProgramData\Microsoft\BootEventCollector\Logs\log.txt" >  
      
 **수집기 문제 해결 권장 된 방법:**  
   
1. 첫째, 수집기가 받았는지 확인 연결 (만들어집니다 파일 대상에서 메시지를 보내기 시작 하는 경우에) 대상에서 사용   
   ```  
   Get-SbecForwarding  
   ```  
   이 대상에서 연결 되어 있는 반환 하는 경우에 autologger 설정에는 문제 수 있습니다. Nothing을 반환 하는 경우 문제가 KDNET 연결으로 시작 하 여이 있습니다. KDNET 연결 문제를 진단 하려는 확인하실 양쪽 끝에서 연결 (즉, 대상 및 수집기에서).  
  
2. 보려면 수집기에서 진단 유틸리티 추가 추가 하려면이 옵션은 \<수집기 > 구성 파일의 요소:  
   \<collector ... minlog="verbose">  
   이렇게 하면 모든 받은 패킷에 대 한 메시지입니다.  
3. 모든 패킷이 전혀 수신 되는지 여부를 확인 합니다. 필요에 따라 다음 파일을 대신 ETW를 통해 직접 세부 정보 표시 모드에서 로그를 작성 하는 것이 좋습니다. 이 추가 하려면이 옵션은 \<수집기 > 구성 파일의 요소:  
   \<collector ... minlog="verbose" log="c:\ProgramData\Microsoft\BootEventCollector\Logs\log.txt">  
      
4. 받은 패킷에 대 한 메시지에 대 한 이벤트 로그를 확인 합니다. 모든 패킷이 전혀 수신 되는지 여부를 확인 합니다. 패킷을 수신 하는 잘못 된 경우 세부 정보에 대 한 이벤트 메시지를 확인 합니다.  
5. 대상 쪽에서 KDNET 레지스트리에 일부 진단 정보를 기록 합니다. 찾는 위치   
   **HKLM\SYSTEM\CurrentControlSet\Services\kdnet** 메시지입니다.  
   (DWORD) KdInitStatus = 성공 시 0 되며 오류 발생 시 오류 코드를 보여 줍니다.  
   KdInitErrorString 오류 설명은 = (도 포함 됩니다 정보 메시지 없음 오류)  
  
6. 대상 및 장치 이름 보고에 대 한 확인에서 Ipconfig.exe를 실행 합니다. KDNET 적절히 로드 된 경우 원래 공급 업체의 카드 이름 대신 "kdnic" 같은 장치 이름 이어야 합니다.  
7. DHCP는 대상에 대해 구성 되어 있는지 확인 합니다. KDNET DHCP를 절대적으로 필요합니다.  
8. 수집기를 대상으로 동일한 네트워크에 있는지 확인 하십시오. 그렇지 않으면 라우팅 구성 되어 있는지 확인 올바르게, 특히 DHCP에 대 한 설정 기본 게이트웨이.  
  
  
**연결 상태**  
  
현재 설정 된 연결 및 데이터를 전달 하는 위치에 대 한 정보 목록을 확인할 수 있습니다 `Get-SbecForwarding`합니다.  
  
와 연결에 상태 변경의 최근 기록을 가져올 수도 있습니다 `Get-SbecHistory`합니다.  
  
### <a name="troubleshooting-setting-a-new-configuration"></a>새 구성을 설정 하는 문제 해결  
Windows PowerShell 명령 사용 하 여 구성을 적용 한 경우 `$result = (Get-Content .\newconfig.xml | Set-SbecActiveConfig); $result`, 다음 변수 `$result` 배포에 대 한 정보가 포함 됩니다. 이 변수에서 서로 다른 정보를 쿼리할 수 있습니다.  
  
사용 하 여 오류에 대 한 정보를 가져올 `$result.ErrorString`합니다. 여기에 오류가 보고 되, 새 구성을 적용 하지 않습니다 하 고 이전 구성을 변경 되지 않습니다.  
  
경고를 가져오는 `$result.WarningString`합니다.  
  
구성에 대 한 세부 정보에 대 한 정보를 가져올 `$result.InfoString`합니다.  
  
전체 결과를 가져올 수 있습니다 `$result | fl *`합니다.  
또는 결과 변수에 저장 하지 않으려는 경우 사용할 수 있습니다 `Get-Content .\newconfig.xml | Set-SbecActiveConfig | fl *`합니다.  
  
### <a name="troubleshooting-target-computers"></a>대상 컴퓨터의 문제 해결  
  
||Error|오류 설명|증상|잠재적인 문제|  
|-|---------|---------------------|-----------|---------------------|  
|대상 컴퓨터||대상은 수집기에 연결 되지 않습니다.||-대상 컴퓨터를 구성한 후 다시 시작 가져오기 하지 않았습니다. 대상 컴퓨터를 다시 시작 합니다.<br />-대상 컴퓨터에 잘못 된 BCD 설정이 있습니다. "유효성 검사 대상 컴퓨터 설정" 섹션의 설정을 확인 합니다. 필요에 따라 잡고 대상 컴퓨터를 다시 시작 합니다.<br />-KDNET/이벤트-NET 드라이버는 네트워크 어댑터에 연결할 수 없거나 잘못 된 네트워크 어댑터에 연결 되어 없습니다. Windows PowerShell에서 실행 `gwmi Win32_NetworkAdapter` ServiceName 사용에 대 한 출력을 확인 하 고 **kdnic**합니다. 잘못 된 네트워크 어댑터를 선택 하는 경우 "에 네트워크 어댑터를 지정 합니다."의 단계를 다시 수행 네트워크 어댑터 전혀 나타나지 않으면 드라이버는 네트워크 어댑터를 지원 하지 않습니다 수 있습니다.<br>**참고 항목** "수집기를 해결 하는 제안 된 방안을" 위에 특히 단계 5-8입니다.|  
|Collector||더 이상 이벤트 수집기 내에서 호스팅되는 VM을 마이그레이션한 후 표시 합니다.||수집기 컴퓨터의 IP 주소 변경 되지 않은 것을 확인 합니다. 있는 경우, "을 사용 하도록 원격으로 ETW 이벤트 전송을 통해 보내는" 검토|  
|Collector||ETL 파일 생성 되지 않습니다.|`Get-SbecForwarding` 나타나지만 오류 없이 대상 연결에 ETL 파일이 생성 되지 않습니다.|대상 컴퓨터에서 아직; 모든 데이터를 보내 않을 ETL 파일은 데이터를 받을 때에 만들어집니다.|  
|Collector||이벤트는 ETL 파일에는 표시 되지 않습니다.|대상 컴퓨터에 이벤트 보냈지만 Message Analyzer의 이벤트 뷰어, ETL 파일을 읽고 이벤트가 없는 경우.|-이벤트 버퍼에 해질 수 있습니다. 이벤트는 수집 되는 전체 64KB 버퍼 또는 없는 새 이벤트로 약 10-15 초 시간 제한이 발생 될 때까지 ETL 파일에 기록 되지 않습니다. 제한 시간이 만료 되거나와 버퍼를 플러시하게 기다리거나 `Save-SbecInstance`합니다.<br />-이벤트 매니페스트를 수집기 컴퓨터 또는 이벤트 뷰어 또는 Message Analyzer 실행 되는 컴퓨터에서 사용할 수 없습니다.  이 경우에 수집기 (수집기 로그를 확인) 이벤트를 처리 하지 못할 수 있습니다 또는 뷰어에 표시 되도록 못할 수 있습니다.  수집기 컴퓨터에 설치 된 모든 매니페스트는 대상 컴퓨터에 설치 하기 전에 수집기 컴퓨터에서 업데이트를 설치 하는 것이 좋습니다.|
