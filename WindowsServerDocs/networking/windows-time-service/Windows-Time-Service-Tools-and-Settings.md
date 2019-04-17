---
ms.assetid: 6086947f-f9ef-4e18-9f07-6c7c81d7002c
title: Windows 서비스 도구 시간 및 설정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 70b7ee4a9955e023d1664a3c29295a22cd5dc75b
ms.sourcegitcommit: fd6a46b702b235f38d90814dd769106ab37cd61b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="windows-time-service-tools-and-settings"></a>Windows 서비스 도구 시간 및 설정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


**이 섹션에서**  
  
-   [Windows 서비스 도구 시간](#w2k3tr_times_tools_dyax)  
  
-   [Windows 서비스 레지스트리 항목이 시간](#w2k3tr_times_tools_uhlp)  
  
-   [Windows 시간이 서비스 그룹 정책 설정](#w2k3tr_times_tools_vwtt)  
  
-   [Windows 시간이 서비스에서 사용 되는 네트워크 포트](#w2k3tr_times_tools_suxb)  
  
-   [관련된 정보](#w2k3tr_times_tools_qoep)  
  
> [!NOTE]  
> 이 항목에서는 도구 및 Windows 시간 (W32Time) 서비스에 대 한 설정에 대해 설명 합니다. If you only want to synchronize time for a domain-joined client computer, see [Configure a client computer for automatic domain time synchronization](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29). Windows 시간 서비스를 구성 하는 방법에 대 한 추가 항목 섹션의 항목의 목록을 보려면에 대 한 [Windows 시간 서비스 구성 정보를 찾을 위치](https://technet.microsoft.com/library/cc773061.aspx)합니다.  
  
> [!CAUTION]  
> 하지 구성 Windows 시간 서비스가 실행 되는 경우 시간을 설정 하거나 Net 시간 명령을 사용 해야 합니다.  

Windows XP 또는 명령 Net 시간 이전 버전을 실행 하는 오래 된 컴퓨터에서 또한 /querysntp 컴퓨터와 동기화 하도록 구성는 없지만 컴퓨터의 시간 클라이언트 NTP 또는 AllSync 구성 된 경우에 해당 NTP 서버를 사용 하는 네트워크 시간 (NTP Protocol) 서버의 이름이 표시 됩니다. 해당 명령이 이후 되지 않습니다.  
  
대부분의 도메인 회원 컴퓨터 NT5DS 도메인 계층에서 시간을 동기화 하는 것을 의미 하는 시간 클라이언트 유형이 있습니다. 이만 일반적인 예외 주 도메인 컨트롤러 (PDC) 에뮬레이터가 작업 마스터 시간 외부 시간 원본을와 동기화 하도록 일반적으로 구성 된 숲 루트 도메인의로 작동 하는 도메인 컨트롤러입니다. 컴퓨터의 시간 클라이언트 구성을 보려면 W32tm /query 실행 /configuration Windows Server 2008 및 Windows Vista에서 시작의 관리자 명령 프롬프트에서 명령 및 읽기는 **종류** 명령 출력에서 줄 합니다. 자세한 내용은 참조 [시간 서비스 작동 방식 Windows](https://go.microsoft.com/fwlink/?LinkId=117753)합니다. 명령을 실행 **등록이 쿼리 HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters** 값 읽고 **NtpServer** 명령 출력에서.  
  
> [!IMPORTANT]  
> Windows Server 2016 전에 W32Time 서비스 시간 응용 프로그램 요구를 충족 되도록 디자인 되지 않았습니다.  그러나 Windows Server 2016 업데이트 이제 수 있도록 1ms 위한 솔루션을 구현 도메인에 정확도 합니다.  See [Windows 2016 Accurate Time](accurate-time.md) and  [Support boundary to configure the Windows Time service for high-accuracy environments](https://go.microsoft.com/fwlink/?LinkID=179459) for more information.  
  
## <a name="w2k3tr_times_tools_dyax"></a>Windows 서비스 도구 시간  
다음 도구 Windows 시간 서비스에 연결 됩니다.  
  
#### <a name="w32tmexe-windows-time"></a>W32tm.exe: Windows 시간  
**범주**  

이 도구는 Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 기본 설치의 일부로 설치 되어 있습니다.  
  
**버전 호환성**  
  
이 도구는 Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 기본 설치에서 작동합니다.  
  
W32tm.exe는 서비스 Windows 시간 설정을 구성 하는 데 사용 됩니다. 수 시간 서비스와 함께 문제를 진단도 사용할 수 있습니다. W32tm.exe 구성 모니터링 또는 Windows 시간 서비스의 문제 해결에 대 한 기본 명령줄 도구입니다.  
  
다음 표에서 W32tm.exe로 사용 되는 매개 설명 합니다.  
  
**기본 매개 W32tm.exe**  
  
|매개|설명|  
|-------------|---------------|  
|W32tm / 있나요?|W32tm 명령줄 도움말|  
|W32tm /register|서비스로 실행 하도록 시간 서비스를 등록 하 고 기본 구성 레지스트리를 추가 합니다.|  
|W32tm /unregister|시간 서비스의 등록을 취소 하 고 레지스트리 구성 정보를 모두 제거 합니다.|  
|w32tm /monitor<br /><br />[/domain:<domain name>] [/computers:<name>[,<name>[,<name>…]]] [/Threads:<num>]|도메인-모니터링 하는 도메인을 지정 합니다. 도메인 이름을 지정 하지 않으면, 또는 도메인 지도 컴퓨터 옵션을 지정 하는 경우 기본 도메인을 사용 합니다. 이 옵션은 두 번 이상 사용할 수 있습니다.<br /><br />컴퓨터에서 지정된 목록이 컴퓨터를 모니터링 합니다. 컴퓨터 이름 공백 없이 쉼표로 구분 됩니다. 이름을 앞으로 하는 경우는 ' *', PDC로 간주 됩니다. 이 옵션은 두 번 이상 사용할 수 있습니다.<br /><br />스레드가-동시에 분석 하는 컴퓨터의 번호를 지정 합니다. 기본값은 3 합니다. 허용 되는 범위는 1 50입니다.|  
|w32tm /ntte <NT time epoch>|NT 시스템 시간을 (10 ^-7) s 간격으로에서 0 h 1-1 월 1601를 읽을 수 있는 형식 있습니다.|  
|w32tm /ntpte <NTP time epoch>|변환 NTP 시간, (2 ^-32)에서 0 h 1-1900 년 1 월 읽을 수 있는 형식 초 간격으로 합니다.|  
|w32tm /resync<br /><br />[/computer:<computer>]<br /><br />[/nowait]<br /><br />[/Rediscover]<br /><br />[/Soft]|모든 누적된 오류 통계 내용을 해당 시계를 가능한 한 빨리 통계를 컴퓨터를 알려 줍니다.<br /><br />컴퓨터:<computer> -컴퓨터 통계를 지정 합니다. 지정 하지 로컬 컴퓨터 동기화 됩니다.<br /><br />nowait-발생; 다시 동기화 기다리지 않습니다 즉시 돌아갑니다. 그렇지 않으면를 반환 하기 전에 완료 하려면 다시 동기화 기다리는 것입니다.<br /><br />다시 검색-네트워크 구성 다시 검색 하 고 네트워크 소스 다시 검색 동기화 합니다.<br /><br />기존 오류 통계를 사용 하 여 동기화 soft-합니다. 유용 하지 않음, 호환성을 제공 합니다.|  
|w32tm /stripchart<br /><br />/computer:<target><br /><br />[/Period:<refresh>]<br /><br />[/dataonly]<br /><br />[/Samples:<count>]<br/><br/>[/rdtsc]<br/>|이 컴퓨터에서 다른 컴퓨터와 오프셋 스트립 차트를 표시 합니다.<br /><br />컴퓨터:<target> -컴퓨터에 대해 오프셋 측정를 합니다.<br /><br />기간:<refresh> -샘플 초에서 간의 시간입니다. 기본값은 2.<br /><br />dataonly-그래픽 없이 데이터에만 표시 됩니다.<br /><br />예제:<count> -수집 <count>샘플을 중지 합니다. 까지 샘플을 수집 됩니다 지정 되지 않은 경우 **Ctrl + C** 를 누르면 됩니다.<br/><br/>rdtsc: 각 샘플을 인쇄 쉼표로 구분 RdtscStart, 머리글 함께 RdtscEnd, FileTime, RoundtripDelay, 텍스트 그래픽 대신 NtpOffset 합니다.<br/><ul><li>[RdtscStart – RDTSC (읽기 타임 스탬프 카운터)](https://en.wikipedia.org/wiki/Time_Stamp_Counter) 값 NTP 요청이 생성 된 직전에 수집 합니다.</li><li>RdtscEnd RDTSC (읽기 타임 스탬프 카운터) 값 NTP 응답 받았으며 처리 후만 수집된 합니다.</li><li>FileTime NTP 요청에 사용 되는 로컬 FILETIME 값 합니다.</li><li>RoundtripDelay – 시간 경과 초 간 NTP 요청을 생성 되 고 NTP 왕복 계산에 따라 계산 받은 NTP 응답 처리 합니다.</li><li>NTPOffset-시간 로컬 컴퓨터와 NTP 서버가 초가 오프셋 계산 NTP 오프셋된 계산에 따라 됩니다.</li></ul>|
|w32tm /config<br /><br />[/computer:<target>]<br /><br />[/Update]<br /><br />[/manualpeerlist:<peers>]<br /><br />[/syncfromflags:<source>]<br /><br />[/LocalClockDispersion:<seconds>]<br /><br />[/Reliable: (예 & #124; 아니요)]<br /><br />[/largephaseoffset:<milliseconds>]|컴퓨터:<target> -구성을 조정 <target>합니다. 지정 하지 기본값은 로컬 컴퓨터 합니다.<br /><br />업데이트-발생 변경 내용을 적용 하려면 구성을 변경 되었음을 시간 서비스 알립니다.<br /><br />manualpeerlist:<peers> -수동 피어 목록을 설정 하 여 <peers>, DNS 및/또는 IP 주소 구분 목록입니다. 여러 피어를 지정 하는 경우이 옵션을 내부 인용에 해야 합니다.<br /><br />syncfromflags:<source> -설정 하는 어떤 소스에서 NTP 클라이언트 동기화 해야 합니다. <source> (하지 대/소문자 구분) 쉼표로 구분 목록이 이러한 키워드를 이어야 합니다.<br /><br />수동-피어 수동 피어 목록에서를 포함 합니다.<br /><br />DOMHIER-는 DC (도메인 컨트롤러) 도메인 계층를 동기화 합니다.<br /><br />LocalClockDispersion:<seconds> -내부의 정확도 구성에서 시간을 설정할 수 없습니다 면 W32Time 갖게 됩니다 시계 소스 구성 했습니다.<br /><br />신뢰할 수 있는: (예 & #124; 아니요) 설정-이 컴퓨터 신뢰할 수 있는 시간 소스 인지 여부.<br /><br />이 설정은 의미 있는 도메인 컨트롤러에만 됩니다.<br /><br />예-이 컴퓨터 신뢰할 수 있는 시간 서비스입니다.<br /><br />더-이 컴퓨터 신뢰할 수 있는 시간 서비스는 없습니다.<br /><br />largephaseoffset:<milliseconds> -로컬 시간 차이점을 설정 및 W32Time는 스파이크가 고려 하 여 시간 네트워크입니다.|  
|w32tm /tz|현재 시간대 설정이 표시 됩니다.|  
|w32tm /dumpreg<br /><br />[/Subkey:<key>]<br /><br />[/computer:<target>]|지정 된 레지스트리 키와 관련 된 값이 표시 됩니다.<br /><br />기본 키는 HKLM\System\CurrentControlSet\Services\W32Time<br /><br />(루트 키 시간 서비스에 대 한).<br /><br />하위:<key> -하위와 관련 된 값이 표시 <key>기본 키.<br /><br />컴퓨터:<target> -컴퓨터에 대 한 설정을 레지스트리 쿼리 <target>|  
|w32tm /query [/computer:<target>] {/source & #124; /configuration & #124; /Peers & #124; /status} [/verbose]|이 매개 먼저 Windows 시간 클라이언트 버전의 Windows Server 2008 및 Windows Vista에서 사용할 수 있게 되었습니다.<br /><br />컴퓨터를 Windows 시간 서비스 정보를 표시 합니다.<br /><br />**컴퓨터:<target>** -쿼리의 정보 **<target>**합니다. 지정 하지 기본값은 로컬 컴퓨터 합니다.<br /><br />**소스** -시간 소스를 표시 합니다.<br /><br />**구성** -구성 런타임 및 설정에서 제공 되는 위치를 표시 합니다. 세부 정보 표시 모드는 지정 되지 않은 하거나 사용 하지 않는 설정도 표시 됩니다.<br /><br />**동료** -동료와 그 상태 목록을 표시 합니다.<br /><br />**상태** -Windows 시간 디스플레이 서비스 상태입니다.<br /><br />**세부 정보 표시** -더 많은 정보를 표시할 자세한 정보 표시 모드를 설정 합니다.|  
|w32tm /debug {/disable & #124; {/Enable /file:<name> /size:<bytes> /entries:<value> [/truncate]}}|이 매개 먼저 Windows 시간 클라이언트 버전의 Windows Server 2008 및 Windows Vista에서 사용할 수 있게 되었습니다.<br /><br />사용 또는 서비스의 개인 로그 Windows 시간 로컬 컴퓨터를 사용 하지 않도록 설정 합니다.<br /><br />**사용 안 함** -개인 로그를 사용 하지 않도록 설정 합니다.<br /><br />**사용 하도록 설정** -개인 로그를 사용 하도록 설정 합니다.<br /><br />-   **파일:<name>** -절대 파일 이름을 지정 합니다.<br />-   **크기:<bytes>** -최대 크기 순을 지정 합니다.<br />-   **항목:<value>** -플래그를 지정 번호로 종류의 기록해 야 하는 정보를 지정 하는 쉼표로 구분 목록이 포함 되어 있습니다. 유효한 숫자는 0에서 300mb. 다양 한 숫자는 0 100,103 같은 단일 숫자 뿐 아니라 유효 106 합니다. 로그인 정보를 모두에 0 300 값이 합니다.<br /><br />**번호를 자릅니다** -파일이 있는 경우 모델 번호를 자릅니다.|  
  
에 대 한 자세한 내용은 **W32tm.exe**를 도움말 및 지원 센터 Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 확인 합니다.  
  
## <a name="w2k3tr_times_tools_uhlp"></a>Windows 서비스 레지스트리 항목이 시간  
다음 레지스트리 항목이 Windows 시간 서비스에 연결 됩니다.  
  
이 정보는 문제를 해결 해야 설정이 적용 됩니다 확인 하거나에서 사용 하기 위해 참조로 제공 됩니다. 편집 하지 않으면 직접 레지스트리 다른 대안이 않는 것이 좋습니다. 레지스트리에 대 한 수정 하지 유효성을 검사는 레지스트리 편집기 또는 Windows를 적용 되기 전에 결과적으로, 잘못 된 값 저장할 수 있습니다. 이 시스템에서 복구할 수 없는 오류가 발생할 수 있습니다.  
  
가능 하면 그룹 정책 또는 Microsoft Management Console (MMC) 등 기타 Windows 도구를 사용 하 여 레지스트리 직접 편집 하는 것이 아니라 작업을 수행할 수 있습니다. 레지스트리를 편집 해야 하는 경우 주의 합니다.  
  
> [!WARNING]  
> 일부 미리 값 시스템 관리 템플릿 파일 (System.adm)에 해당 하는 기본 레지스트리 항목이 다릅니다는 그룹 정책 개체 (GPO) 설정에 대 한 구성 된 합니다. If you plan to use a GPO to configure any Windows Time setting, be sure that you review [Preset values for the Windows Time service Group Policy settings are different from the corresponding Windows Time service registry entries in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). 이 문제는 Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 및 Windows Server 2003에 적용 됩니다.  
  
Windows 시간 서비스에 대 한 많은 레지스트리 항목이 동일한 이름의 그룹 정책 설정을 동일 합니다. 그룹 정책 설정에 동일한 이름의 레지스트리 항목이에 해당 합니다.  
  
>**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\\**

  
레지스트리 여기에는 레지스트리 키입니다. 이러한 키의 모든 Windows 시간 설정 값으로 저장 됩니다.
* [매개](#Parameters)
* [구성](#Configuration)
* [NtpClient](#NtpClient)
* [NtpServer](#NtpServer)
  
> [!NOTE]  
> 대부분의 레지스트리에의 W32Time 섹션 값 내부적으로 사용 W32Time 정보를 저장 합니다. 이 값 언제 든 지 수동으로 변경 되지 해야 합니다. 수정 하지 마십시오이 섹션의 설정을 설정을 익숙한 확실 새 값은 예상 대로 작동 하지 않는 경우 합니다. 아래에서 다음 레지스트리 항목이 있습니다.

>>**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\\**  
  
레지스트리에서 클럭에 저장 된 일부 매개과 초 후에 있습니다. 시간 클럭을 변환할 초 다음과 같습니다.  
  
-   1 분 = 60 초  
  
-   1 초 = 1000 ms  
  
-   1 ms = 10,000 clock ticks on a Windows system, as described at [DateTime.Ticks Property](https://msdn.microsoft.com/en-us/library/system.datetime.ticks.aspx).  
  
예를 들어 5 분 5 됩니다 * 60\ * 1000\ * 10000 3000000000 클럭 = 합니다. 

Windows 7, Windows 8, Windows 10, Windows Server 2008 및 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012R2 Windows Server 2016 모든 버전에 포함 되어 있습니다.  몇 가지 항목은 최신 Windows 버전에 사용할 수만 있습니다.


#### <a name="Parameters"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Parameters

|레지스트리 항목이|버전|설명|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|모든|이 항목 비 표준 모드 조합 동기화 피어 사이에서 사용할 수 있음을 나타냅니다. 도메인 구성원에 대 한 기본값은 1. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 1.|
|NtpServer|모든|이 항목 DNS 이름 또는 한 줄 IP 주소 구성 된 컴퓨터 얻는 타임 스탬프 피어 목록이 구분 지정 합니다. 각 DNS 이름이 나 나열 된 IP 주소 고유 해야 합니다. 컴퓨터가 도메인에 연결 된 신뢰할 수 있는 더 많은 시간 원본을 공식 미국 시간 시계 등 동기화 해야 합니다.  <ul><li>0 x 01 SpecialInterval </li><li>0x02 UseAsFallbackOnly</li><li>0x04 SymmetricActive - For more information about this mode, see [Windows Time Server: 3.3 Modes of Operation](https://go.microsoft.com/fwlink/?LinkId=208012).</li><li>0x08 클라이언트</li></ul><br />이 레지스트리 항목이 도메인 구성원을 위해가 있습니다. 기본값 독립 실행형 클라이언트 및 서버에 0x1 time.windows.com입니다.<br /><br />Note: For more information on available NTP Servers, see [Microsoft Knowledge Base article 262680 - A list of the Simple Network Time Protocol (SNTP) time servers that are available on the Internet](https://go.microsoft.com/fwlink/?LinkId=186067)|
|ServiceDll|모든|이 항목 W32Time로 유지 됩니다. Windows 운영 체제 사용 되는 예약 된 데이터를 포함 하 고이 설정에 변경 내용을 예기치 결과가 발생할 수 있습니다. 이 DLL 도메인 회원 독립 실행형 클라이언트 및 서버에 대 한 기본 위치는 %windir%\System32\W32Time.dll 합니다.  |
|이 ServiceMain|모든|이 항목 W32Time로 유지 됩니다. Windows 운영 체제 사용 되는 예약 된 데이터를 포함 하 고이 설정에 변경 내용을 예기치 결과가 발생할 수 있습니다. 기본값은 도메인 회원 SvchostEntry_W32Time입니다. 독립 실행형 클라이언트 및 서버에 기본값 SvchostEntry_W32Time입니다.  "|
|입력|모든|이 항목에서 동기화를 수락 하도록 피어를 나타냅니다.  <ul><li>**NoSync**합니다. 시간 서비스 다른 소스를 동기화 하지 않습니다.</li><li>**NTP 합니다.** 에 지정 된 서버에서 시간 서비스 동기화 되는 **NtpServer**합니다. 레지스트리 항목이 있습니다.</li><li>**NT5DS**합니다. 도메인 계층에서 시간 서비스를 동기화합니다.  </li><li>**AllSync**합니다. 시간 서비스 모든 사용 가능한 동기화 메커니즘을 사용 합니다.  </li></ul>도메인 구성원에 기본값은 **NT5DS**합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 **NTP**합니다.   |

#### <a name="Configuration"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config

|레지스트리 항목이|버전|설명|
|------------------------------------|---------------|----------------------------|
|AnnounceFlags|모든|이 항목이이 컴퓨터 신뢰할 수 있는 시간 서버로 표시 되어 있는지 여부를 제어 합니다. 시간 서버로 표시 되어 있지 않으면 컴퓨터 안정적으로 표시 되지 않습니다.<br /> -0x00 하지 시간 서버  <br /> -0x01 항상 시간 서버  <br /> -0x02 자동 시간 서버  <br /> -0x04 항상 신뢰할 수 있는 시간 서버  <br /> -0x08 자동 신뢰할 수 있는 시간 서버  <br />도메인 구성원에 대 한 기본값은 10 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 10 합니다.|
|EventLogFlags|모든|이 항목 시간 서비스 기록 하는 이벤트를 제어 합니다.  <br />-점프 시간: 0x1  <br />소스의 변경: 0x2  <br />도메인 구성원에 기본값은 2. 독립 실행형 클라이언트 및 서버에 기본값은 2.  |
|FrequencyCorrectRate|모든|이 항목 시계 해결 되는 속도 제어 합니다. 이 값이 너무 작은 경우 시계 안정적이 고 overcorrects 합니다. 값 너무 큽니다 시계 동기화 하는 데 오랜 시간이 걸립니다. 기본값 도메인 구성원에는 4입니다. 독립 실행형 클라이언트 및 서버에 기본값은 4.  <br /><br />참고 0 FrequencyCorrectRate 레지스트리 항목이 활성화 된에 잘못 된 값은 합니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 컴퓨터에 0으로 설정 된 경우 Windows 시간 서비스 자동으로 변경 됩니다 1.  |
|HoldPeriod|모든|이 항목 스파이크 감지 기능 동기화에 로컬 시계를 신속 하 게 표시 하기 위해 비활성화 되어 있는 시간을 제어할 수 있습니다. 스파이크가 당시 나타내는 시간 샘플 다양 한 초 설정 되어 있지 않으며 일관 되 게 샘플 좋은 시간 반환 된 후 일반적으로 수신 하는입니다. 기본값은 도메인 회원 5입니다. 독립 실행형 클라이언트 및 서버에 기본값은 5.  |
|LargePhaseOffset|모든|이 항목을 한 번 오프셋 보다 큰 또는이 값 10에 동일한 지정<sup>-7</sup> 초 스파이크가 것으로 간주 됩니다. 많은 양의 교통 체증 등 네트워크 중단 스파이크가 될 수 있습니다. 오랜 기간 동안 유지 하지 않으면 스파이크가 무시 됩니다. 기본값은 도메인 회원 50000000입니다. 독립 실행형 클라이언트 및 서버에 기본값 50000000입니다.  |
|LastClockRate|모든|이 항목 W32Time로 유지 됩니다. Windows 운영 체제 사용 되는 예약 된 데이터를 포함 하 고이 설정에 변경 내용을 예기치 결과가 발생할 수 있습니다. 기본값은 도메인 회원 156250입니다. 독립 실행형 클라이언트 및 서버에 기본값 156250입니다.  |
|LocalClockDispersion|모든|이 항목을 제어 가정 시기 해야 하는 초에서 분산에 소스가 내장 시계입니다. 기본값은 도메인 회원 10입니다. 독립 실행형 클라이언트 및 서버에 기본값은 10 합니다.|
|MaxAllowedPhaseOffset|모든|이 W32Time 클럭 속도 사용 하 여 컴퓨터 시계 조정 하려고 초에서 최대 오프셋을 지정 합니다. 오프셋이이 속도 초과 W32Time 컴퓨터 시계 직접 설정 합니다. 도메인 구성원에 대 한 기본값은 300 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 1.  [자세한 내용은 아래를 참조 하십시오](#MaxAllowedPhaseOffset)합니다.|
|MaxClockRate|모든|이 항목 W32Time로 유지 됩니다. Windows 운영 체제 사용 되는 예약 된 데이터를 포함 하 고이 설정에 변경 내용을 예기치 결과가 발생할 수 있습니다. 도메인 구성원에 대 한 기본값은 155860 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 155860 합니다.  |
|MaxNegPhaseCorrection|모든|이 서비스는 초 후에는 최대 부정적인 시간 수정을 지정 합니다. 서비스 보다 더 크게 변경 필요 하다 결정을 이벤트 대신 기록 합니다. 특별 한 경우: 0xFFFFFFFF 의미 항상 시간 수정 합니다. 도메인 구성원에 대 한 기본값은 0xFFFFFFFF 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 54000 (15 시간).  |
|MaxPollInterval|모든|이 항목 지정 시스템 폴링 간격 허용 log2 초 후에는 최대 간격 합니다. Note 시스템에 따라 예정 된 간격 폴링해야, 하지만 샘플 그러기 요청을 생성 하는 공급자 거부할 수 있습니다. 도메인 컨트롤러에 대 한 기본값은 10 합니다. 도메인 구성원에 대 한 기본값은 15 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 15 합니다.  |
|MaxPosPhaseCorrection|모든|이 서비스는 초 후에는 최대 긍정적인 시간 수정을 지정 합니다. 서비스 보다 더 크게 변경 필요 하다 결정을 이벤트 대신 기록 합니다. 특별 한 경우: 0xFFFFFFFF 의미 항상 시간 수정 합니다. 도메인 구성원에 대 한 기본값은 0xFFFFFFFF 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 54000 (15 시간).  |
|MinClockRate|모든|이 항목 W32Time로 유지 됩니다. Windows 운영 체제 사용 되는 예약 된 데이터를 포함 하 고이 설정에 변경 내용을 예기치 결과가 발생할 수 있습니다. 도메인 구성원에 대 한 기본값은 155860 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 155860 합니다.  |
|MinPollInterval|모든|이 항목의 작은 간격 log2 초 후에 허용 지정 시스템 폴링 간격 합니다. 시스템 샘플 이보다 더 자주 요청 하지 않고, 동안 공급자 수 예정 된 간격 이외의 때때로 샘플 생성 note 합니다. 도메인 컨트롤러에 대 한 기본값은 6입니다. 도메인 구성원에 대 한 기본값은 10 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 10 합니다.  |
|PhaseCorrectRate|모든|이 항목 단계 오류가 해결 되는 속도 제어 합니다. 작은 값 지정 하면 신속 하 게 단계 오류를 수정 하지만를 불안정 시계 발생할 수 있습니다. 값 너무 많은 경우 단계 오류를 해결 하려면 오래 시간이 걸립니다. <br /><br />기본값은 도메인 회원은 1입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 7입니다.<br /><br />참고: 0 PhaseCorrectRate 레지스트리 항목이 활성화 된에 잘못 된 값은입니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 컴퓨터에 0으로 설정 된 경우 Windows 시간 서비스 자동으로 변경 1.  |
|PollAdjustFactor|모든|이 항목의 시스템에 대 한 같이 늘리거나 결정을 제어할 수 있습니다. 클수록 값, 양은 줄일 수을 같이 하는 오류입니다. 기본값은 도메인 회원 5입니다. 독립 실행형 클라이언트 및 서버에 기본값은 5. |
|SpikeWatchPeriod|모든|이 항목을 유지 하 여 의심 스러운 오프셋 해야 하는 시간을 지정 초에서으로 올바른 수락 전에 합니다. 기본값은 도메인 회원은 900입니다. 독립 실행형 하는 클라이언트와 워크스테이션 기본값은 900입니다.  |
|TimeJumpAuditOffset|모든|서명 되지 않은 나타내는 정수 점프 감사 임계값 시간 초 후에 있습니다. 시간 서비스 시계 직접를 설정 하 여 로컬 시간을 조정 하 고 시간 수정 된이 값이 보다 시간 서비스 감사 이벤트를 기록 합니다.|
|UpdateInterval|모든|이 항목 단계 보정 조정 간에 클럭 번호를 지정합니다. 도메인 컨트롤러에 대 한 기본값은 100 합니다. 도메인 구성원에 대 한 기본값은 30, 000 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 360,000 합니다.  <br /><br />**참고**: 0 UpdateInterval 레지스트리 항목이 활성화 된에 잘못 된 값이 합니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 실행 하는 컴퓨터에 0으로 설정 된 경우 Windows 시간 서비스 자동으로 변경 1.<br /><br />다음 세 가지 레지스트리 항목이 W32Time 기본 설정의 일부는 아니지만 로깅 향상 된 기능을 얻기 위해 레지스트리를에 추가할 수 있습니다. 그룹 정책 개체 편집기 EventLogFlags 설정에 대 한 값을 변경 하 여 이벤트 시스템 로그에 기록 정보를 수정할 수 있습니다. 기본적으로 시간 서비스 될 때마다 새로운 시간 소스입니다 전환 이벤트 뷰어에서 로그를 만듭니다.<br /><br />**경고**: 레지스트리 항목이 기본 미리 값 그룹 정책 개체 (GPO) 설정은 해당와 다른에 대 한 시스템 관리 템플릿 파일 (System.adm)에서 구성 된의 일부입니다. If you plan to use a GPO to configure any Windows Time setting, be sure that you review [Preset values for the Windows Time service Group Policy settings are different from the corresponding Windows Time service registry entries in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). 이 문제는 Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 및 Windows Server 2003에 적용 됩니다. |
|UtilizeSslTimeData|Windows 10 빌드 1511 게시물|1 항목을는 W32Time 가능한 정확 하지 않은 시계 시드하기 여러 SSL 타임 스탬프에 사용 됩니다 나타냅니다.|

다음 레지스트리 항목이 W32Time 로깅 사용 하기 위해 추가 해야 합니다.  

|레지스트리 항목이|버전|설명|
|------------------------------------|---------------|----------------------------|
|FileLogEntries|모든|이 항목에 Windows 시간 로그 파일 만들어진 항목의 양을 제어할 수 있습니다. 기본값 없음 이며, Windows 시간 활동 기록 하지 않습니다. 유효는 0에서 300mb입니다. 이 값은 일반적으로 Windows 시간 만든 이벤트 로그 항목이 영향을 주지 않습니다.|
|FileLogName|모든|이 항목 위치와 파일 이름을 Windows 시간 로그를 제어 합니다. 기본값 비어 이며 변경할 수 없는 경우가 아니면 **FileLogEntries** 변경 됩니다. 유효한 전체 경로 Windows 시간 로그 파일 만드는 데 사용할 파일 이름입니다. 이 값 일반적으로 Windows 시간 만든 이벤트 로그 항목에 영향을 주지 않습니다.  |
|FileLogSize|모든|이 항목 Windows 시간 로그 파일의 순 동작을 제어할 수 있습니다. 때 **FileLogEntries** 및 **FileLogName** 는 정의이 항목의 크기 정의 바이트 로그 파일 새 항목을 오래 로그 항목 덮어쓰지 하기 전에 연결할 수 있도록 합니다. 긍정적인 번호로 올바르고 3000000 것이 좋습니다. 이 값 일반적으로 Windows 시간 만든 이벤트 로그 항목에 영향을 주지 않습니다.  |



#### <a name="NtpClient"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient

|레지스트리 항목이|버전|설명|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|모든|이 항목 비 표준 모드 조합 동기화 피어 사이에서 사용할 수 있음을 나타냅니다. 도메인 구성원에 대 한 기본값은 1. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 1.|
|CompatibilityFlags|모든|이 항목 값과 다음 호환성 플래그를 지정합니다. <br /><br />-DispersionInvalid: 0x00000001  <br />-IgnoreFutureRefTimeStamp: 0x00000002  <br /> -AutodetectWin2K: 0x80000000  <br />-AutodetectWin2KStage2: 0x40000000  <br /><br />도메인 구성원에 대 한 기본값은 0x80000000 합니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 0x80000000 합니다.  |
|CrossSiteSyncFlags|모든|이 항목 서비스 선택 컴퓨터가 도메인 외부 동기화 파트너 있는지 여부를 결정 합니다. 옵션과 값은 다음과 같습니다.  <br /><br />-없음: 0  <br />-PdcOnly: 1  <br />-모두: 2  <br /><br />이 값은 NT5DS 값 설정 되지 않은 경우 무시 됩니다. 도메인 구성원에 대 한 기본값은 2. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 2.  |
|DllName|모든|이 항목 DLL 시간 공급자에 대 한 위치를 지정합니다.  <br /><br />이 DLL 도메인 회원 독립 실행형 클라이언트 및 서버에 대 한 기본 위치는 %windir%\System32\W32Time.dll 합니다.|
|사용 하도록 설정|모든|이 항목의 현재 시간 서비스 NtpClient 공급자가 사용 하는 경우를 나타냅니다.  <br /><ul><li>예 1</li><li>아니요 0</li></ul>기본값은 도메인 회원은 1입니다. 독립 실행형 클라이언트 및 서버에 기본값은 1.|
|EventLogFlags|모든|이 항목 Windows 시간 서비스에의 한 이벤트를 지정 합니다.<ul><li>0x1 연결성 변경</li><li>0x2 큰 샘플 기울이기 (이것은 Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 r 2에 적용할 수만)</li></ul>기본값 도메인 구성원에 0x1입니다. 기본값 독립 실행형 클라이언트 및 서버에 0x1입니다.|
|InputProvider|모든|이 항목 NtpClient 공급자가 사용 하는 경우를 나타냅니다.  <ul><li>예 1  </li><li>아니요 0 </li></ul>기본값은 도메인 회원은 1입니다. 독립 실행형 클라이언트 및 서버에 기본값은 1.  |
|LargeSampleSkew|모든|이 초 로그인 하기 위한 대용량 샘플 기울이기를 지정 합니다. 보안 및 Exchange 위원회 (초) specifications 준수 하기 3 초를 설정 해야 합니다. 이벤트 0x2 큰 샘플 기울이기 EventLogFlags 명시적으로 구성 된 경우에이 설정에 기록 됩니다. 도메인 구성원에 기본값은 3 합니다. 독립 실행형 클라이언트 및 서버에 기본값은 3 합니다.  |
|ResolvePeerBackOffMaxTimes|모든|이 항목 사이 전환 대기 간격을 두 번 최대 수를 피어 실패와 동기화를 찾으려 시도할 지정 합니다. 0 값 대기 기간은 항상 최소 의미 합니다. 기본값은 도메인 회원은 7입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 7입니다. |
|ResolvePeerBackoffMinutes|모든|이 항목 (분)와 동기화 하도록 피어 찾을 하기 전에 기다리고 초기 간격을 지정 합니다. 기본값은 도메인 회원 15입니다. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 15 합니다.  |
|SpecialPollInterval|모든|이 항목 초 수동 피어에 대 한 특수 설문 간격을 지정 합니다. SpecialInterval 0x1 플래그를 사용 하도록 설정 하는 경우이 설문 간격을 같이 하는 대신 W32Time 사용 하 여 운영 체제에서 결정 합니다. 기본값은 도메인 회원 3, 600입니다. 독립 실행형 클라이언트 및 서버에 기본값 604,800입니다.<br/><br/>새로운 1702 빌드 SpecialPollInterval MinPollInterval 및 MaxPollInterval 구성 레지스트리 값이 포함 되어 있습니다.|
|SpecialPollTimeRemaining|모든|이 항목 W32Time로 유지 됩니다. Windows 운영 체제에서 사용 되는 사용된 데이터를 포함 합니다. 컴퓨터를 다시 시작한 후 W32Time 다시 동기화 초의 시간을 지정 합니다. 이 설정에 변경 내용을 예기치 결과 발생할 수 있습니다. 기본값 독립 실행형 클라이언트 및 서버에 모두 도메인 회원 켜고 비어 있습니다.  |

#### <a name="NtpServer"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer

|레지스트리 항목이|버전|설명|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|모든|이 항목 비 표준 모드 조합 클라이언트 서버와 동기화에 사용할 수 있음을 나타냅니다. 도메인 구성원에 대 한 기본값은 1. 독립 실행형 클라이언트 및 서버에 대 한 기본값은 1.|
|DllName|모든|이 항목 DLL 시간 공급자에 대 한 위치를 지정합니다.<br /><br />이 DLL 도메인 회원 독립 실행형 클라이언트 및 서버에 대 한 기본 위치는 %windir%\System32\W32Time.dll 합니다.  |
|사용 하도록 설정|모든|이 항목의 현재 시간 서비스 NtpServer 공급자가 사용 하는 경우를 나타냅니다. <ul><li>예 1</li><li>아니요 0</li></ul>기본값은 도메인 회원은 1입니다. 독립 실행형 클라이언트 및 서버에 기본값은 1.  |
|InputProvider|모든|이 항목 NtpServer 공급자가 사용 하는 경우를 나타냅니다.  <ul><li>예 1  </li><li>아니요 0 </li></ul>기본값은 도메인 회원은 1입니다. 독립 실행형 클라이언트 및 서버에 기본값은 1.  |

#### <a name="MaxAllowedPhaseOffset"></a>MaxAllowedPhaseOffset 정보
W32Time 컴퓨터 시계 서서히 설정에 대 한 순서를 오프셋 MaxAllowedPhaseOffset 값 보다 수를 한 번에 다음 수식 만족 해야 합니다.  
```  
|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2  
``` 
CurrentTimeOffset 1ms = 10, 000 눈금 Windows 시스템 클록 어디 클럭 측정 됩니다.  
  
SystemClockRate 및 PhaseCorrectRate 클럭에서 측정 합니다. SystemClockRate를 가져오려면 다음 명령을 사용 하는 초 공식 눈금 시계를 초 변환 * 1000\ * 10000:  
  
```  
W32tm /query /status /verbose  
ClockRate: 0.0156000s  
```  
  
SystemclockRate 시스템 클록의 속도입니다. 156000 초 예를 들어를 사용 하 여 SystemclockRate 것 될 = 0.0156000 * 1000 \ * 10000 156000 클럭 = 합니다.  
  
MaxAllowedPhaseOffset 초 이기도합니다. 으로 변환 눈금 시계, MaxAllowedPhaseOffset 곱하려면 * 1000\ * 10000 합니다.  
  
다음 두 가지 예 적용 하는 방법을 보여합니다  
  
**예제 1**: 4 분 정도 따라 다릅니다 시간 (예를 들어, 시간은 오전 11 05 하 고 시간 샘플 피어 로부터 받은 오전 11 09는 올바른 한 것으로 알려져).  
```
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
|currentTimeOffset| = 4mins = 4*60\*1000\*10000 = 2400000000 ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
2400000000 < 6000000000 = TRUE  
```
위의 수식 충족 하 고 있나요? 
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 2,400,000,000 / (30000*1) < 156000/2  
  
Is 100,000 < 78,000  
  
NO/FALSE  
```  
따라서 W32tm 설정 시계 다시 즉시.  
  
> [!NOTE]  
> 이 경우 느리게 시계를 다시 설정 하려면 PhaseCorrectRate 또는 값 레지스트리에서 updateInterval도 참에 수식을 결과를 얻으려면 조정 해야 할가 있습니다.  
  
**예제 2**: 시간 3 분 정도 따라 다릅니다.  
```  
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
currentTimeOffset = 3mins = 3*60\*1000\*10000 = 1800000000 clock ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
1800000000 < 6000000000 = TRUE  
```  
위의 수식 충족 하 고 있나요?
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 3 mins (1,800,000,000) / (30000*1) < 156000/2  
  
Is 60,000 < 78,000  
  
YES/TRUE  
```  
이 경우 시계 설정 됩니다 다시 느리게.  
  
## <a name="w2k3tr_times_tools_vwtt"></a>Windows 시간이 서비스 그룹 정책 설정  
그룹 정책 개체 편집기를 사용 하 여 대부분의 W32Time 매개 변수를 구성할 수 있습니다. 신뢰할 수 있는 시간을 확보할 NTPServer 또는 NTPClient 시간 동기화 메커니즘을 구성 하 고 컴퓨터 구성 된 컴퓨터 구성 포함 됩니다.  
  
> [!NOTE]  
> Windows 시간 서비스에 대 한 그룹 정책 설정을 Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 도메인 컨트롤러에서 구성할 수 있으며 Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 실행 하는 컴퓨터에만 적용 될 수 있습니다.  
  
다음 위치에서 그룹 정책 개체 편집기 끌기 W32Time 구성 하는 데 사용 하는 그룹 정책 설정을 볼 수 있습니다.  
  
-   컴퓨터 구성 \ 관리 템플릿 Templates\System\Windows 시간 서비스  
  
    구성 **글로벌 구성 설정을** 여기 합니다.  
  
-   컴퓨터 구성 \ 관리 템플릿 Templates\System\Windows 시간 Service\Time 공급자  
  
    구성 **Windows NTP 클라이언트** 여기 설정 합니다.  
  
    사용 하도록 설정 **Windows NTP 클라이언트** 여기 합니다.  
  
    사용 하도록 설정 **Windows NTP 서버** 여기 합니다.  
  
> [!WARNING]  
> 일부 미리 값 시스템 관리 템플릿 파일 (System.adm)에 해당 하는 기본 레지스트리 항목이 다릅니다는 그룹 정책 개체 (GPO) 설정에 대 한 구성 된 합니다. If you plan to use a GPO to configure any Windows Time setting, be sure that you review [Preset values for the Windows Time service Group Policy settings are different from the corresponding Windows Time service registry entries in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). 이 문제는 Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 및 Windows Server 2003에 적용 됩니다.  
  
다음 표에서 각 설정과 관련 된 미리 설정된 된 값 Windows 시간 서비스와 관련 된 global 그룹 정책 설정 합니다. 각 설정에 대 한 자세한 내용은 참조에 해당 하는 레지스트리 항목이 "[Windows 시간이 서비스 레지스트리 항목이](#w2k3tr_times_tools_uhlp)"이이 주제에 이전 합니다. 다음 설정은 이라는 단일 GPO에 포함 되어 **글로벌 구성 설정을**합니다.  
  
**Windows 시간와 관련 된 글로벌 그룹 정책 설정**  
  
|그룹 정책 설정|값 미리 설정된|  
|------------------------|------------------|  
|AnnounceFlags|10|  
|EventLogFlags|2|  
|FrequencyCorrectRate|4|  
|HoldPeriod|5|  
|LargePhaseOffset|1280000|  
|LocalClockDispersion|10|  
|MaxAllowedPhaseOffset|300|  
|MaxNegPhaseCorrection|54000 (15 시간)|  
|MaxPollInterval|15|  
|MaxPosPhaseCorrection|54000 (15 시간)|  
|MinPollInterval|10|  
|PhaseCorrectRate|7|  
|PollAdjustFactor|5|  
|SpikeWatchPeriod|90|  
|UpdateInterval|100|  
  
다음 표에서 사용할 수 있는 설정을 **Windows NTP 클라이언트 구성** GPO 및 Windows 시간 서비스와 관련 된 미리 설정된 된 값 합니다. 각 설정에 대 한 자세한 내용은 참조에 해당 하는 레지스트리 항목이 "[Windows 시간이 서비스 레지스트리 항목이](#w2k3tr_times_tools_uhlp)"이이 주제에 이전 합니다.  
  
**Windows 시간와 관련 된 NTP 클라이언트 그룹 정책 설정**  
  
|그룹 정책 설정|기본값|  
|------------------------|-----------------|  
|NtpServer|time.windows.com 0 x 1|  
|입력|기본 옵션:<br /><br />-   **NTP 합니다.** 도메인에 가입 하지 않은 컴퓨터를 사용 합니다.<br />-   **NT5DS 합니다.** 도메인에 가입 하는 컴퓨터를 사용 합니다.|  
|CrossSiteSyncFlags|2|  
|ResolvePeerBackoffMinutes|15|  
|ResolvePeerBackoffMaxTimes|7|  
|SpecialPollInterval|3600|  
|EventLogFlags|0|  
  
## <a name="w2k3tr_times_tools_suxb"></a>Windows 시간이 서비스에서 사용 되는 네트워크 포트  
Windows 시간 모든 시간 동기화 통신 UDP 123 포트를 사용 해야 하는 NTP 사양에는 다음과 같습니다. 이 포트 Windows 시간 예약 하 고 예약된 남아 항상 합니다. 컴퓨터의 시계 동기화 또는 시간 다른 컴퓨터에 제공 될 때마다 통신을 UDP 포트 123에서 수행 됩니다.  
  
> [!NOTE]  
> 네트워크 어댑터가 여러 (다중 홈 컴퓨터 라고도 함)는 컴퓨터를 있는 경우 네트워크 어댑터에 따라 Windows 시간 서비스를 활성화할 수 없습니다.  
  
## <a name="w2k3tr_times_tools_qoep"></a>관련된 정보  
다음 리소스가이 섹션에 관련 된 추가 정보가 포함 됩니다.  
  
-   RFC *1305* IETF RFC 데이터베이스에  

