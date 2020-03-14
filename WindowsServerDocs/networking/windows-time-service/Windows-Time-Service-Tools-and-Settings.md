---
ms.assetid: 6086947f-f9ef-4e18-9f07-6c7c81d7002c
title: Windows 시간 서비스 도구 및 설정
description: ''
author: Teresa-Motiv
ms.author: pashort
manager: dougkim
ms.date: 02/24/2020
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.custom:
- CI ID 113344
- CSSTroubleshoot
audience: Admin
ms.openlocfilehash: e99c07428a1689e3c079ff2570759c849a61e945
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323475"
---
# <a name="windows-time-service-tools-and-settings"></a>Windows 시간 서비스 도구 및 설정

> 적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 이상

이 항목에서는 Windows 시간 서비스(W32Time)의 도구 및 설정에 대해 알아봅니다.  

도메인에 가입된 클라이언트 컴퓨터의 시간만 동기화하려면 [자동 도메인 시간 동기화를 위한 클라이언트 컴퓨터 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)을 참조하세요. Windows 시간 서비스를 구성하는 방법에 대한 자세한 내용은 [Windows 시간 서비스 구성 정보를 찾을 수 있는 위치](windows-time-service-top.md)를 참조하세요.  

> [!CAUTION]  
> **Net time** 명령을 사용하여 Windows 시간 서비스가 실행되는 시간을 구성하거나 설정하면 안 됩니다.  
>
> 또한 Windows XP 또는 이전 버전을 실행하는 이전 컴퓨터에서 **Net time /querysntp** 명령은 컴퓨터가 동기화되도록 구성된 NTP(Network Time Protocol) 서버의 이름을 표시하지만, 해당 NTP 서버는 컴퓨터의 시간 클라이언트가 NTP 또는 AllSync로 구성된 경우에만 사용됩니다. 이 명령은 이후부터 더 이상 사용되지 않습니다.  

대부분의 도메인 멤버 컴퓨터에는 NT5DS의 시간 클라이언트 유형이 있습니다. 즉, 도메인 계층에서 시간을 동기화합니다. 이에 대한 유일한 일반적인 예외는 포리스트 루트 도메인의 PDC(주 도메인 컨트롤러) 에뮬레이터 작업 마스터로 작동하는 도메인 컨트롤러입니다. PDC 에뮬레이터 작업 마스터는 일반적으로 시간을 외부 시간 원본과 동기화하도록 구성됩니다. 컴퓨터의 시간 클라이언트 구성(Windows Server 2008 및 Windows Vista에서 시작)을 보려면 관리자 권한 명령 프롬프트에서 **W32tm /query /configuration** 명령을 실행하고 명령 출력에서 **Type** 줄을 읽으십시오. 자세한 내용은 [Windows 시간 서비스의 작동 방식](How-the-Windows-Time-Service-Works.md)을 참조하세요. 또한 **reg query HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters** 명령을 실행하고, 명령 출력에서 **NtpServer** 값을 읽을 수 있습니다.  

> [!IMPORTANT]  
> Windows Server 2016 이전에는 W32Time 서비스에서 시간이 중요한 애플리케이션의 요구 사항을 충족하도록 설계되지 않았습니다. 그러나 이제 Windows Server 2016으로 업데이트하면 도메인에서 1밀리초 정확도의 솔루션을 구현할 수 있습니다. 자세한 내용은 [Windows 2016 정확한 시간](accurate-time.md) 및 [정확도가 높은 환경을 위해 Windows 시간 서비스를 구성할 수 있는 지원 범위](support-boundary.md)를 참조하세요.  

## <a name="windows-time-service-tools"></a>Windows 시간 서비스 도구  

Windows 시간 서비스와 연결되는 도구는 다음과 같습니다.  

### <a name="w32tmexe-windows-time"></a>W32tm.exe: Windows 시간  

**범주**  

이 도구는 Windows(Windows XP 이상 버전) 및 Windows Server(Windows Server 2003 이상 버전)의 기본 설치의 일부입니다.  

**버전 호환성**  

이 도구는 Windows(Windows XP 이상 버전) 및 Windows Server(Windows Server 2003 이상 버전)의 기본 설치에서 작동합니다.  

W32tm.exe를 사용하여 Windows 시간 서비스 설정을 구성하고 시간 서비스 문제를 진단할 수 있습니다. W32tm.exe는 Windows 시간 서비스를 구성, 모니터링 또는 문제 해결을 위한 기본 명령줄 도구입니다.  

다음 표에서는 W32tm.exe에 사용할 수 있는 매개 변수를 설명합니다.  

**W32tm.exe 기본 매개 변수**  

|매개 변수 |설명 |
| --- | --- |
|**w32tm /?** |W32tm 명령줄 도움말을 표시합니다. |
|**w32tm /register** |서비스로 실행할 시간 서비스를 등록하고 기본 구성 정보를 레지스트리에 추가합니다. |
|**w32tm /unregister** |시간 서비스를 등록 취소하고 레지스트리에서 모든 구성 정보를 제거합니다. |
|**w32tm /monitor [/domain:\<*도메인 이름*>] [/computers:\<*이름*>[,\<*이름*>[,\<*이름*>...]]] [/threads:\<*수*>]** |Windows 시간 서비스를 모니터링합니다.<br /><br />**/domain**: 모니터링할 도메인을 지정합니다. 도메인 이름을 지정하지 않거나 **/domain** 또는 **/computers** 옵션을 지정하지 않으면 기본 도메인이 사용됩니다. 이 옵션은 여러 번 사용할 수 있습니다.<br /><br />**/computers**: 지정된 컴퓨터 목록을 모니터링합니다. 컴퓨터 이름은 공백 없이 쉼표로 구분됩니다. 이름 앞에 **\*** 접두사가 있는 경우 PDC로 처리됩니다. 이 옵션은 여러 번 사용할 수 있습니다.<br /><br />**/threads**: 동시에 분석할 컴퓨터의 수를 지정합니다. 기본값은 3입니다. 허용되는 범위는 1-50입니다. |
|**w32tm /ntte \<NT *time epoch*>** |Windows NT 시스템 시간(1601년 1월 1일 0시부터 10<sup>-7</sup>초 간격으로 측정됨)을 읽을 수 있는 형식으로 변환합니다. |
|**w32tm /ntpte \<NTP *time epoch*>** |NTP 시간(1900년 1월 1일 0시부터 2<sup>-32</sup>초 간격으로 측정됨)을 읽을 수 있는 형식으로 변환합니다. |
|**w32tm /resync [/computer:\<*컴퓨터*>] [/nowait] [/rediscover] [/soft]** |누적된 오류 통계를 모두 제거하여 가능한 한 빨리 시계를 다시 동기화해야 한다고 컴퓨터에 알립니다.<br /><br />**/computer:\<*컴퓨터*>** : 다시 동기화해야 하는 컴퓨터를 지정합니다. 지정하지 않으면 로컬 컴퓨터가 다시 동기화됩니다.<br /><br />**/nowait**: 다시 동기화가 발생할 때까지 기다리지 않습니다. 즉시 반환합니다. 그렇지 않으면 다시 동기화가 완료될 때까지 기다린 후에 돌아옵니다.<br /><br />**/rediscover**: 네트워크 구성을 다시 감지하고, 네트워크 원본을 다시 검색한 다음, 다시 동기화합니다.<br /><br />**/soft**: 기존 오류 통계를 사용하여 다시 동기화합니다. 호환성을 위해 제공되는 경우 유용하지 않습니다. |
|**w32tm /stripchart /computer:\<*대상*> [/period:\<*새로 고침*>] [/dataonly] [/samples:\<*수*>] [/rdtsc]** |이 컴퓨터와 다른 컴퓨터 간의 오프셋에 대한 스트립 차트를 표시합니다.<br /><br />**/computer:\<*대상*>** : 오프셋을 측정할 컴퓨터입니다.<br /><br />**/period:\<*새로 고침*>** : 샘플 간 시간(초)입니다. 기본값은 2초입니다.<br /><br />**/dataonly**: 그래픽 없이 데이터만 표시합니다.<br /><br />**/samples:\<*수*>** : \<*수*>개의 샘플을 수집한 다음, 중지합니다. 지정하지 않으면 **Ctrl+C**를 누를 때까지 샘플이 수집됩니다.<br/><br/>**/rdtsc**: rdtsc: 이 옵션은 각 샘플에 대해 텍스트 그래픽 대신 **RdtscStart**, **RdtscEnd**, **FileTime**, **RoundtripDelay**, **NtpOffset** 헤더와 함께 쉼표로 구분된 값을 출력합니다.<br/><ul><li>**RdtscStart**: NTP 요청이 생성되기 직전에 수집된 [RDTSC(Read Time Stamp Counter)](https://en.wikipedia.org/wiki/Time_Stamp_Counter) 값입니다.</li><li>**RdtscEnd**: NTP 응답을 받고 처리한 직후에 수집된 RDTSC 값입니다.</li><li>**FileTime**: NTP 요청에 사용된 로컬 FILETIME 값입니다.</li><li>**RoundtripDelay**: NTP 요청 생성과 수신된 NTP 응답 처리 사이에 경과된 시간(초)이며, NTP 왕복 계산에 따라 계산됩니다.</li><li>**NTPOffset**: 로컬 머신과 NTP 서버 사이의 시간 오프셋(초)이며, NTP 오프셋 계산에 따라 계산됩니다.</li></ul> |
|**w32tm /config [/computer:\<*대상*>] [/update] [/manualpeerlist:\<*피어*>] [/syncfromflags:\<*소스*>] [/LocalClockDispersion:\<*초*>] [/reliable:(YES\|NO)] [/largephaseoffset:\<*밀리초*>]** |**/computer:\<*대상*>** : \<*대상*>의 구성을 조정합니다. 지정하지 않으면 기본값은 로컬 컴퓨터입니다.<br /><br />**/update**: 구성이 변경되어 변경 내용이 적용된 것을 시간 서비스에 알립니다.<br /><br />**/manualpeerlist:\<*피어*>** : 수동 피어 목록을 \<*피어*>로 설정합니다. 이것은 공백으로 구분된 DNS 및/또는 IP 주소 목록입니다. 여러 피어를 지정하는 경우 이 옵션은 따옴표로 묶어야 합니다.<br /><br />**/syncfromflags:\<*소스*>** : NTP 클라이언트가 동기화해야 하는 소스를 설정합니다. \<*소스*>는 쉼표로 구분된 키워드 목록(대/소문자 구분 안 함)이며 다음과 같습니다.<ul><li>**MANUAL**: 수동 피어 목록의 피어를 포함합니다.</li><li>**DOMHIER**: 도메인 계층의 DC(도메인 컨트롤러)에서 동기화합니다.</li></ul>**/LocalClockDispersion:\<*초*>** : 구성된 소스에서 시간을 가져올 수 없을 때 W32Time이 가정할 내부 클록의 정확도를 구성합니다.<br /><br />**/reliable:(YES\|NO)** : 이 컴퓨터가 신뢰할 수 있는 시간 원본인지 여부를 설정합니다. 이 설정은 도메인 컨트롤러에서만 의미가 있습니다.<ul><li>**YES**: 이 컴퓨터는 신뢰할 수 있는 시간 서비스입니다.</li><li>**NO**: 이 컴퓨터는 신뢰할 수 있는 시간 서비스가 아닙니다.</li></ul>**/largephaseoffset:\<*밀리초*>** : W32Time이 스파이크로 간주할 현지 시간과 네트워크 시간 사이의 차이를 설정합니다. |
|**w32tm /tz** |현재 표준 시간대 설정을 표시합니다. |
|**w32tm /dumpreg [/subkey:\<*키*>] [/computer:\<*대상*>]** |지정된 레지스트리 키와 연결된 값을 표시합니다.<br /><br />기본 키는 **HKLM\System\CurrentControlSet\Services\W32Time**(시간 서비스의 루트 키)입니다.<br /><br />**/subkey:\<*키*>** : 기본 키의 하위 키와 연결된 값을 <key>표시합니다.<br /><br />**/computer:\<*대상*>** : \<*대상*> 컴퓨터에 대한 레지스트리 설정을 쿼리합니다. |
|**w32tm /query [/computer:\<*대상*>] {/source \| /configuration \| /peers \| /status} [/verbose]** |컴퓨터의 Windows 시간 서비스 정보를 표시합니다. 이 매개 변수는 Windows Vista 및 Windows Server 2008의 Windows 시간 클라이언트에서 처음 사용할 수 있게 되었습니다.<br /><br />**/computer:\<*대상*>** : \<*대상*>의 정보를 쿼리합니다. 지정하지 않으면 기본값은 로컬 컴퓨터입니다.<br /><br />**/source**: 시간 원본을 표시합니다.<br /><br />**/configuration**: 실행 시간 구성과 설정이 제공되는 위치를 표시합니다. 자세한 정보 표시 모드에서는 정의되지 않음 또는 사용되지 않음 설정도 표시합니다.<br /><br />**/peers**: 피어 목록과 해당 상태를 표시합니다.<br /><br />**/status**: Windows 시간 서비스 상태를 표시합니다.<br /><br />**/verbose**: 자세한 정보를 표시하도록 자세한 정보 표시 모드를 설정합니다. |
|**w32tm /debug {/disable \| {/enable /file:\<*이름*> /size:/<*바이트*> /entries:\<*값*> [/truncate]}}** |로컬 컴퓨터 Windows 시간 서비스 프라이빗 로그를 사용하거나 사용하지 않도록 설정합니다. 이 매개 변수는 Windows Vista 및 Windows Server 2008의 Windows 시간 클라이언트에서 처음 사용할 수 있게 되었습니다.<br /><br />**/disable**: 프라이빗 로그를 사용하지 않도록 설정합니다.<br /><br />**/enable**: 프라이빗 로그를 사용하도록 설정합니다.<ul><li>**file:\<*이름*>** : 절대 파일 이름을 지정합니다.</li><li>**size:\<*바이트*>** : 순환 로깅의 최대 크기를 지정합니다.</li><li>**entries:\<*값*>** : 숫자로 지정하고 쉼표로 구분하여 기록해야 하는 정보 유형을 지정하는 플래그 목록을 포함합니다. 유효 숫자는 0-300입니다. 단일 숫자뿐만 아니라 숫자 범위(예: 0-100,103,106)도 유효합니다. 모든 정보를 기록하려면 0-300의 값을 설정합니다.</li></ul>**/truncate**: 파일이 있으면 자릅니다. |

**W32tm.exe**에 대한 자세한 내용은 [Windows 도움말](https://support.microsoft.com/hub/4338813/windows-help?os=windows-10)을 참조하세요.  

**예제**

로컬 Windows 시간 클라이언트가 두 가지 다른 시간 서버(하나는 ntpserver.contoso.com, 다른 하나는 clock.adatum.com)를 가리키도록 설정하려면 명령줄에 다음 명령을 입력하고 Enter 키를 누릅니다.

```cmd
w32tm /config /manualpeerlist:"ntpserver.contoso.com clock.adatum.com" /syncfromflags:manual /update
```

외부 시간 동기화를 위해 인터넷에서 사용할 수 있는 유효한 NTP 서버 목록을 보려면 [인터넷에서 사용 가능한 SNTP(Simple Network Time Protocol) 시간 서버 목록](https://go.microsoft.com/fwlink/?linkid=60401)을 참조하세요.

호스트 이름이 CONTOSOW1인 Windows 기반 클라이언트 컴퓨터에서 Windows 시간 클라이언트 구성을 확인하려면 다음 명령을 실행합니다.

```cmd
W32tm /query /computer:contosoW1 /configuration
```

이 명령의 출력은 Windows 시간 클라이언트에 대해 설정된 구성 매개 변수 목록입니다.

## <a name="using-group-policy-to-configure-the-windows-time-service"></a>그룹 정책을 사용하여 Windows 시간 서비스 구성

Windows 시간 서비스는 다수의 구성 속성을 레지스트리 항목으로 저장합니다. 그룹 정책 개체를 사용하여 대부분의 정보를 구성할 수 있습니다. 예를 들어 GPO를 사용하여 컴퓨터를 NTPServer 또는 NTPClient로 구성하거나 시간 동기화 메커니즘을 구성하거나 컴퓨터를 신뢰할 수 있는 시간 원본으로 구성할 수 있습니다.  

> [!NOTE]  
> Windows 시간 서비스에 대한 그룹 정책 설정은 Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2 도메인 컨트롤러에서 구성할 수 있으며, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2를 실행하는 컴퓨터에만 적용할 수 있습니다.  

Windows는 Windows 시간 서비스 정책 정보를 **Computer Configuration\Administrative Templates\System\Windows Time Service**에 있는 W32Time.admx 관리 템플릿 파일에 저장합니다. 정책이 레지스트리에 정의한 구성 정보가 저장되고 이러한 레지스트리 항목을 사용하여 Windows 시간 서비스에 대한 레지스트리 항목이 구성됩니다. 따라서 그룹 정책에 의해 정의된 값이 레지스트리의 Windows 시간 서비스 섹션에 있는 기존 값을 덮어씁니다.

> [!IMPORTANT]  
> 미리 설정된 GPO 설정 중 일부는 해당 기본 레지스트리 항목과 다릅니다. GPO를 사용하여 Windows 시간 설정을 구성하려는 경우 [Windows 시간 서비스 그룹 정책 설정의 사전 설정 값은 Windows Server 2003의 해당 Windows 시간 서비스 레지스트리 항목과 다릅니다](https://go.microsoft.com/fwlink/?LinkId=186066)를 검토하세요. 이 문제는 Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 및 Windows Server 2003에 적용됩니다.

예를 들어 **Windows NTP 클라이언트 구성** 정책에서 정책 설정을 편집한다고 가정합니다.

변경 내용은 관리 템플릿의 다음 위치에 저장됩니다.

> **컴퓨터 구성\관리 템플릿\시스템\Windows 시간 서비스\시간 공급자\Windows NTP 클라이언트 구성**

Windows는 이러한 하위 설정을 다음 하위 키 아래에 있는 레지스트리 정책 영역에 로드합니다.

> **HKLM\Software\Policies\Microsoft\W32time\TimeProviders\NtpClient**

그러면 Windows는 정책 설정을 사용하여 다음 하위 키 아래에서 관련 Windows 시간 서비스 레지스트리 항목을 구성합니다.

> **HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Time Providers\NTPClient\\**

다음 표에는 Windows 시간 서비스에 대해 구성할 수 있는 정책과 이러한 정책이 영향을 주는 레지스트리 하위 키가 나와 있습니다.

> [!NOTE]  
> 그룹 정책 설정을 제거하면 Windows는 레지스트리의 정책 영역에서 해당 항목을 제거합니다.

|정책<sup>1</sup> |레지스트리 위치<sup>2,</sup> <sup>3</sup> |
| --- | --- |
|전역 구성 설정 |W32Time<br />W32Time\Config<br />W32Time\Parameters |
|시간 공급자\Windows NTP 클라이언트 구성 |W32Time\TimeProviders\NtpClient |
|시간 공급자\Windows NTP 클라이언트 사용 |W32Time\TimeProviders\NtpClient |
|시간 공급자\Windows NTP 서버 사용 |W32Time\TimeProviders\NtpServer |

> <sup>1</sup> 범주 경로: **컴퓨터 구성\관리 템플릿\시스템\Windows 시간 서비스**  
> <sup>2</sup> 하위 키: **HKLM\SOFTWARE\Policies\Microsoft\Windows**  
> <sup>3</sup> 하위 키: **HKLM\SYSTEM\CurrentControlSet\Services**

## <a name="enabling-w32time-logging"></a>W32Time 로깅 사용

다음 세 개의 레지스트리 항목은 W32Time 기본 구성에 포함되지 않지만, 로깅 기능을 향상시키기 위해 레지스트리에 추가할 수 있습니다. 시스템 이벤트 로그에 기록된 정보는 그룹 정책 개체 편집기에서 **EventLogFlags** 설정 값을 변경하여 수정할 수 있습니다. 기본적으로 시간 서비스는 새 시간 원본으로 전환할 때마다 이벤트를 기록합니다.

W32Time 로깅을 사용하도록 설정하려면 다음 레지스트리 항목을 추가해야 합니다.  

|레지스트리 항목 |버전 |설명 |
| --- | --- | --- |
|**FileLogEntries** |모든 버전 |Windows 시간 로그 파일에 생성되는 항목 수를 제어합니다. 기본값은 none이며, 이는 Windows 시간 활동을 기록하지 않습니다. 유효한 값은 **0** ~ **300**입니다. 이 값은 일반적으로 Windows 시간에서 만든 이벤트 로그 항목에는 영향을 주지 않습니다. |
|**FileLogName** |모든 버전 |Windows 시간 로그의 위치 및 파일 이름을 제어합니다. 기본값은 비어 있으며, **FileLogEntries**가 변경되지 않는 한 변경하면 안 됩니다. 유효한 값은 Windows 시간에서 로그 파일을 만드는 데 사용할 전체 경로 및 파일 이름입니다. 이 값은 일반적으로 Windows 시간에서 만든 이벤트 로그 항목에는 영향을 주지 않습니다. |
|**FileLogSize** |모든 버전 |Windows 시간 로그 파일의 순환 로깅 동작을 제어합니다. **FileLogEntries** 및 **FileLogName**이 정의된 경우 가장 오래된 로그 항목을 새 항목으로 덮어쓸 때까지 로그 파일에 도달할 수 있는 크기(바이트)를 정의합니다. 이 설정에는 **1000000** 이상의 값을 사용하세요. 이 값은 일반적으로 Windows 시간에서 만든 이벤트 로그 항목에는 영향을 주지 않습니다. |

## <a name="configuring-how-windows-time-service-resets-the-computer-clock"></a>Windows 시간 서비스가 컴퓨터 클록을 재설정하는 방법 구성

W32Time에서 컴퓨터 시계를 점차적으로 설정하려면 오프셋이 **MaxAllowedPhaseOffset** 값보다 작아야 하며 다음 수식을 동시에 충족해야 합니다.  

- Windows Server 2016 이상 버전:

  > |**CurrentTimeOffset**| &divide; (16 &times; **PhaseCorrectRate** &times; **pollIntervalInSeconds**) &le; **SystemClockRate** &divide; 2  

- Windows Server 2012 R2 및 이전 버전:

  > |**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2  

**CurrentTimeOffset** 값은 클록 틱 수로 측정되며, Windows 시스템의 경우 1밀리초 = 10,000 클록 틱입니다.  

**SystemClockRate** 및 **PhaseCorrectRate**도 클록 틱 수로 측정됩니다. **SystemClockRate** 값은 다음 명령을 사용하고 *초* &times; 1,000 &times; 10,000 수식을 사용하여 초 단위에서 클록 틱 수로 변환할 수 있습니다.  

```cmd
W32tm /query /status /verbose  
ClockRate: 0.0156000s  
```  

**SystemClockRate**는 시스템의 클록 속도입니다. 예를 들어 156,000초를 사용하면, **SystemClockRate** 값은 0.0156000 &times; 1,000 &times; 10,000 = 156,000 클록 틱입니다.  

**MaxAllowedPhaseOffset** 역시 초 단위로 측정됩니다. 이것을 클록 틱 수로 변환하려면 **MaxAllowedPhaseOffset** &times; 1,000 &times; 10,000을 곱합니다.  

다음 예제에서는 Windows Server 2012 R2 또는 이전 버전을 사용할 때 이러한 계산을 적용하는 방법을 보여 줍니다.

**예제 1: 4분의 시간 차이**

사용자의 시간은 11:05이고 피어로부터 받았으며 정확하다고 생각되는 시간 샘플은 11:09입니다.

> **PhaseCorrectRate** = 1  
>  
> **UpdateInterval** = 30,000 clock ticks  
>  
> **SystemClockRate** = 156,000 clock ticks  
>  
> **MaxAllowedPhaseOffset** = 10 min = 600 seconds = 600 &times; 1,000 &times; 10,000 = 6,000,000,000 clock ticks  
>  
> |**CurrentTimeOffset**| = 4 min = 4 &times; 60 &times; 1,000 &times; 10,000 = 2,400,000,000 clock ticks  
>  
> Is **CurrentTimeOffset** &le; **MaxAllowedPhaseOffset**?  
>  
> 2,400,000,000 &le; 6,000,000,000: TRUE  

그리고 위의 수식을 충족하나요?

> (|**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2)  

Is 2,400,000,000 / (30,000 &times; 1) &le; 156,000 &divide; 2  

80,000 &le; 78,000: FALSE  

따라서 W32tm은 클록을 즉시 다시 설정합니다.  

> [!NOTE]  
> 이 경우 클록을 다시 느리게 설정하려면 레지스트리에서 **PhaseCorrectRate** 또는 **UpdateInterval**의 값을 조정하여 수식 결과가 **TRUE**가 되도록 해야 합니다.  

**예제 2: 3분의 시간 차이**

> **PhaseCorrectRate** = 1  
> 
> **UpdateInterval** = 30,000 clock ticks  
> 
> SystemClockRate = 156,000 clock ticks  
> 
> **MaxAllowedPhaseOffset** = 10 min = 600 seconds = 600 &times; 1,000 &times; 10,000 = 6,000,000,000 clock ticks  
> 
> |**CurrentTimeOffset**| = 3 mins = 3 &times; 60 &times; 1,000 &times; 10,000 = 1,800,000,000 clock ticks  
> 
> Is |**CurrentTimeOffset**| &le; **MaxAllowedPhaseOffset**?  
> 
> 1,800,000,000 &le; 6,000,000,000: TRUE  

그리고 위의 수식을 충족하나요?

> (|**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2)  
> 
> Is 3 mins &times; (1,800,000,000) &divide; (30,000 &times; 1) &le; 156,000 &divide; 2  
> 
> Is 60,000 &le; 78,000: TRUE  

이 경우 클록이 다시 느리게 설정됩니다.  

## <a name="reference-windows-time-service-registry-entries"></a>참고자료: Windows 시간 서비스 레지스트리 항목

> [!WARNING]  
> 이러한 레지스트리 항목에 대한 정보는 문제를 해결하거나 필요한 설정이 적용되었는지 확인하는 데 사용할 수 있는 참고 자료로 제공됩니다. 레지스트리의 W32Time 섹션에 있는 값은 대부분 W32Time에서 정보를 내부적으로 저장하는 데 사용됩니다. 이러한 값을 수동으로 변경하지 마십시오. 레지스트리 수정 내용은 적용되기 전에 레지스트리 편집기나 Windows에서 유효성이 검사되지 않습니다. 레지스트리에 잘못된 값이 포함되어 있으면 Windows에서 복구할 수 없는 오류가 발생할 수 있습니다.  

Windows 시간 서비스는 다음 레지스트리 하위 키 아래에 정보를 저장합니다.

- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Config**](#config)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters**](#parameters)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient**](#ntpclient)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer**](#ntpserver)

또한 문제 해결을 위한 [로그를 구성하기 위해 항목을 추가](#enabling-w32time-logging)할 수 있습니다.

다음 표에서 "모든 버전"은 Windows 7, Windows 8, Windows 10, Windows Server 2008 및 Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 R2, Windows Server 2016, Windows Server 2019를 포함하는 Windows 버전을 나타냅니다. 일부 항목은 이후 버전의 Windows에서만 사용할 수 있습니다.

> [!NOTE]  
> 레지스트리의 일부 매개 변수는 클록 틱 수로 측정되며, 일부는 초 단위로 측정됩니다. 시간을 클록 틱 수에서 초로 변환하려면 다음 변환 요소를 사용합니다.  
> - 1분 = 60초,  
> - 1초 = 1,000밀리초,  
> - [DateTime.Ticks 속성](https://docs.microsoft.com/dotnet/api/system.datetime.ticks)에서 설명한 대로 Windows 시스템에서 1밀리초 = 10,000 클록 틱입니다.  
>  
> 예를 들어 5분은 5 &times; 60 &times; 1000 &times; 10000 = 3,000,000,000 클록 틱이 됩니다.  

### <a id="config"></a>"HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Config" 하위 키 항목

|레지스트리 항목 |버전 |설명 |
| --- | --- | --- |
|**AnnounceFlags** |모든 버전 |이 컴퓨터가 신뢰할 수 있는 시간 서버로 표시되는지 여부를 제어합니다. 컴퓨터가 시간 서버로 표시되지 않으면 해당 컴퓨터를 신뢰할 수 있는 것으로 표시하지 않습니다.<ul><li>**0x00**. 시간 서버 아님</li><li>**0x01**. 항상 시간 서버</li><li>**0x02**. 자동 시간 서버</li><li>**0x04**. 항상 신뢰할 수 있는 시간 서버</li><li>**0x08**. 신뢰할 수 있는 자동 시간 서버</li></ul><br />도메인 멤버의 기본값은 **10**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **10**입니다. |
|**ChainDisable** | |연결 메커니즘의 비활성화 여부를 제어합니다. 연결이 비활성화되면(0으로 설정) RODC(읽기 전용 도메인 컨트롤러)는 모든 도메인 컨트롤러와 동기화할 수 있지만 RODC에 암호가 캐시되지 않은 호스트는 RODC와 동기화할 수 없습니다. 이 값은 부울 설정이고 기본값은 **0**입니다.|
|**ChainEntryTimeout** | |항목이 만료된 것으로 간주되기 전에 항목이 연결 테이블에 남아 있을 수 있는 최대 시간을 지정합니다. 만료된 항목은 다음 요청 또는 응답이 처리될 때 제거될 수 있습니다. 기본값은 **16**(초)입니다. |
|**ChainLoggingRate** | |성공 및 실패한 연결 시도 횟수를 나타내는 이벤트가 이벤트 뷰어의 시스템 로그에 기록되는 빈도를 제어합니다. 기본값은 **30**(분)입니다. |
|**ChainMaxEntries** | |연결 테이블에 허용되는 최대 항목 수를 제어합니다. 연결 테이블이 가득 차고 만료된 항목을 제거할 수 없으면 들어오는 요청이 모두 삭제됩니다. 기본값은 **128**(항목)입니다. |
|**ChainMaxHostEntries** | |특정 호스트에 대한 연결 테이블에 허용되는 최대 항목 수를 제어합니다. 기본값은 **4**(항목)입니다. |
|**ClockAdjustmentAuditLimit** |Windows Server 2016 버전 1709 이상 버전; Windows 10 버전 1709 이상 버전 |대상 컴퓨터의 W32time 서비스 이벤트 로그에 기록될 수 있는 가장 작은 로컬 클록 조정을 지정합니다. 기본값은 **800**(PPM: 백만 분의 일)입니다. |
|**ClockHoldoverPeriod** |Windows Server 2016 버전 1709 이상 버전; Windows 10 버전 1709 이상 버전 |시스템 클록이 시간 원본과 동기화하지 않고 명목상 정확도를 유지할 수 있는 최대 시간(초)을 나타냅니다. W32time이 입력 공급자로부터 새로운 샘플을 얻지 못하고 이 시간이 경과하면 W32time은 시간 원본 재검색을 시작합니다. Default: 7,800초. |
|**EventLogFlags** |모든 버전 |시간 서비스가 기록하는 이벤트를 제어합니다.<ul><li>**0x1**. 시간 이동</li><li>**0x2**. 소스 변경</li></ul>도메인 멤버의 기본값은 **2**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **2**입니다. |
|**FrequencyCorrectRate** |모든 버전 |클록이 수정되는 속도를 제어합니다. 이 값이 너무 작으면 시계가 불안정해지고 과도하게 수정됩니다. 이 값이 너무 크면 시계를 동기화하는 데 시간이 오래 걸립니다. 도메인 멤버의 기본값은 **4**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **4**입니다.<br /><br />**참고** <br />0은 **FrequencyCorrectRate** 레지스트리 항목의 유효한 값이 아닙니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008, Windows Server 2008 R2 컴퓨터에서 이 값을 **0**으로 설정하면 Windows 시간 서비스가 자동으로 **1**로 변경합니다. |
|**HoldPeriod** |모든 버전 |로컬 클록을 빠르게 동기화하기 위해 스파이크 검색을 사용하지 않도록 설정되는 기간을 제어합니다. 스파이크는 시간 오프셋을 초 단위로 표시하는 시간 샘플이며, 일반적으로 양호한 시간 샘플이 일관되게 반환된 후에 수신됩니다. 도메인 멤버의 기본값은 **5**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **5**입니다. |
|**LargePhaseOffset** |모든 버전 |10<sup>-7</sup>초 동안 이 값보다 크거나 같은 시간 오프셋을 스파이크로 간주하도록 지정합니다. 대량의 트래픽과 같은 네트워크 중단으로 인해 스파이크가 발생할 수 있습니다. 스파이크는 오랫동안 지속되지 않으면 무시됩니다. 도메인 멤버의 기본값은 **50000000**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **50000000**입니다. |
|**LastClockRate** |모든 버전 |W32Time에서 유지 관리됩니다. 여기에는 Windows 운영 체제에서 사용하는 예약된 데이터가 포함되며, 이 설정을 변경하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 멤버의 기본값은 **156250**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **156250**입니다. |
|**LocalClockDispersion** |모든 버전 |유일한 시간 원본과 기본 제공 CMOS 클록인 경우 가정해야 하는 분산(초)을 제어합니다. 도메인 멤버의 기본값은 **10**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **10**입니다. |
|**MaxAllowedPhaseOffset** |모든 버전 |W32Time이 클록 속도를 사용하여 컴퓨터 클록을 조정하려고 시도하는 최대 오프셋(초)을 지정합니다. 오프셋이 이 속도를 초과하면 W32Time에서 컴퓨터 시계를 직접 설정합니다. 도메인 멤버의 기본값은 **300**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **1**입니다. 자세한 내용은 [Windows 시간 서비스가 컴퓨터 클록을 재설정하는 방법 구성](#configuring-how-windows-time-service-resets-the-computer-clock)을 참조하세요. |
|**MaxClockRate** |모든 버전 |W32Time에서 유지 관리됩니다. 여기에는 Windows 운영 체제에서 사용하는 예약된 데이터가 포함되며, 이 설정을 변경하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 멤버의 기본값은 **155860**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **155860**입니다. |
|**MaxNegPhaseCorrection** |모든 버전 |서비스가 수행하는 최대 음수 시간 수정을 초 단위로 지정합니다. 서비스에서 이 값보다 크게 변경해야 한다고 확인되면 이벤트를 대신 기록합니다.<br /><br />**참고**<br />**0xFFFFFFFF** 값은 특별한 경우입니다. 이 값은 서비스가 항상 시간을 수정한다는 의미입니다.<br /><br />도메인 멤버의 기본값은 **0xFFFFFFFF**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **54,000**(15시간)입니다.|
|**MaxPollInterval** |모든 버전 |시스템 폴링 간격에 허용되는 최대 간격(log2 초)을 지정합니다. 시스템에서 예약된 간격에 따라 폴링해야 하지만, 이 폴링이 요청되는 경우 공급자는 샘플 생성을 거부할 수 있습니다. 도메인 컨트롤러의 기본값은 **10**입니다. 도메인 멤버의 기본값은 **15**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **15**입니다. |
|**MaxPosPhaseCorrection** |모든 버전 |서비스가 수행하는 최대 양수 시간 수정(초)을 지정합니다. 서비스에서 이 값보다 크게 변경해야 한다고 확인되면 이벤트를 대신 기록합니다.<br /><br />**참고**<br />**0xFFFFFFFF** 값은 특별한 경우입니다. 이 값은 서비스가 항상 시간을 수정한다는 의미입니다.<br /><br />도메인 멤버의 기본값은 **0xFFFFFFFF**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **54,000**(15시간)입니다. |
|**MinClockRate** |모든 버전 |W32Time에서 유지 관리됩니다. 여기에는 Windows 운영 체제에서 사용하는 예약된 데이터가 포함되며, 이 설정을 변경하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 멤버의 기본값은 **155860**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **155860**입니다. |
|**MinPollInterval** |모든 버전 |시스템 폴링 간격에 허용되는 최소 간격(log2 초)을 지정합니다. 시스템에서 이보다 더 자주 샘플을 요청하지 않지만, 공급자는 예약된 간격 이외의 시간에 샘플을 생성할 수 있습니다. 도메인 컨트롤러의 기본값은 **6**입니다. 도메인 멤버의 기본값은 **10**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **10**입니다. |
|**PhaseCorrectRate** |모든 버전 |단계 오류가 수정되는 속도를 제어합니다. 작은 값을 지정하면 단계 오류가 빠르게 수정되지만 시계가 불안정해질 수 있습니다. 값이 너무 크면 단계 오류를 수정하는 데 시간이 더 오래 걸립니다.<br /><br />도메인 멤버의 기본값은 **1**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **7**입니다.<br /><br />**참고**<br />0은 **PhaseCorrectRate** 레지스트리 항목의 유효한 값이 아닙니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008, Windows Server 2008 R2 컴퓨터에서 이 값을 **0**으로 설정하면 Windows 시간 서비스가 자동으로 **1**로 변경합니다. |
|**PollAdjustFactor** |모든 버전 |시스템의 폴링 간격을 늘리거나 줄이는 결정을 제어합니다. 값이 클수록 폴링 간격을 줄이는 오류의 양이 줄어듭니다. 도메인 멤버의 기본값은 **5**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **5**입니다. |
|**RequireSecureTimeSyncRequests** |Windows 8 이상 버전 |DC가 이전 인증 프로토콜을 사용하는 시간 동기화 요청에 응답할지 여부를 제어합니다. 사용하도록 설정(**1**로 설정)된 경우 DC는 이러한 프로토콜을 사용하는 요청에 응답하지 않습니다. 이 값은 부울 설정이고 기본값은 **0**입니다. |
|**SpikeWatchPeriod** |모든 버전 |의심스러운 오프셋이 올바른 것으로 수락되기 전에 지속되어야 하는 시간(초)을 지정합니다. 도메인 멤버의 기본값은 **900**입니다. 독립 실행형 클라이언트와 워크스테이션의 기본값은 **900**입니다. |
|**TimeJumpAuditOffset** |모든 버전 |시간 이동 감사 임계값을 초 단위로 나타내는 부호 없는 정수입니다. 시간 서비스에서 시계를 직접 설정하여 로컬 시계를 조정하고, 시간 수정이 이 값보다 큰 경우 시간 서비스에서 감사 이벤트를 기록합니다. |
|**UpdateInterval** |모든 버전 |단계 수정 조정 사이의 클록 틱 수를 지정합니다. 도메인 컨트롤러의 기본값은 **100**입니다. 도메인 멤버의 기본값은 **30,000**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **360,000**입니다.<br /><br />**참고**<br />0은 **UpdateInterval** 레지스트리 항목의 유효한 값이 아닙니다. Windows Server 2003, Windows Server 2003 R2, Windows Server 2008, Windows Server 2008 R2를 실행하는 컴퓨터에서 이 값을 **0**으로 설정하면 Windows 시간 서비스가 자동으로 **1**로 변경합니다.|
|**UtilizeSslTimeData** |Windows 10 빌드 1511 이후의 Windows 버전 |값이 **1**이면 W32Time가 여러 SSL 타임스탬프를 사용하여 매우 부정확한 클록을 시드한다는 것을 나타냅니다. |

### <a id="parameters"></a>"HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters" 하위 키 항목

| 레지스트리 항목 | 버전 | 설명 |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |모든 버전 |피어 간 동기화에서 비표준 모드 조합을 사용할 수 있음을 나타냅니다. 도메인 멤버의 기본값은 **1**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **1**입니다. |
|**NtpServer** |모든 버전 |컴퓨터가 타임스탬프를 가져오는 데 사용할 공백으로 구분된 피어 목록을 지정하며, 한 줄에 하나 이상의 DNS 이름 또는 IP 주소로 구성됩니다. 나열되는 각 DNS 이름 또는 IP 주소는 고유해야 합니다. 도메인에 연결된 컴퓨터는 미국의 공식 시간 시계와 같이 더 신뢰할 수 있는 시간 원본과 동기화되어야 합니다.  <ul><li>0x01 SpecialInterval </li><li>0x02 UseAsFallbackOnly</li><li>0x04 SymmetricActive: 이 모드에 대한 자세한 내용은 [Windows 시간 서버: 3.3 작업 모드](https://go.microsoft.com/fwlink/?LinkId=208012)를 참조하세요.</li><li>0x08 Client</li></ul><br />도메인 멤버에는 이 레지스트리 항목의 기본값이 없습니다. 독립 실행형 클라이언트 및 서버의 기본값은 time.windows.com,0x1입니다.<br /><br />**참고**<br />사용 가능한 NTP 서버에 대한 자세한 내용은 KB 262680 [인터넷에서 사용 가능한 SNTP(Simple Network Time Protocol) 시간 서버 목록](https://support.microsoft.com/help/262680/a-list-of-the-simple-network-time-protocol-sntp-time-servers-that-are)을 참조하세요. |
|**ServiceDll** |모든 버전 |W32Time에서 유지 관리됩니다. 여기에는 Windows 운영 체제에서 사용하는 예약된 데이터가 포함되며, 이 설정을 변경하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 멤버와 독립 실행형 클라이언트 및 서버 모두에서 이 DLL의 기본 위치는 %windir%\System32\W32Time.dll입니다. |
|**ServiceMain** |모든 버전 |W32Time에서 유지 관리됩니다. 여기에는 Windows 운영 체제에서 사용하는 예약된 데이터가 포함되며, 이 설정을 변경하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 멤버의 기본값은 **SvchostEntry_W32Time**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **SvchostEntry_W32Time**입니다. |
|**Type** |모든 버전 |동기화를 수락할 피어를 나타냅니다.  <ul><li>**NoSync**. 시간 서비스가 다른 원본과 동기화되지 않습니다.</li><li>**NTP**. 시간 서비스가 **NtpServer**에 지정된 서버에서 동기화됩니다. 레지스트리 항목입니다.</li><li>**NT5DS**. 시간 서비스가 도메인 계층 구조에서 동기화됩니다.  </li><li>**AllSync**. 시간 서비스에서 사용 가능한 모든 동기화 메커니즘을 사용합니다.  </li></ul>도메인 멤버의 기본값은 **NT5DS**입니다. 독립 실행형 클라이언트 및 서버의 기본값은 **NTP**입니다. |

### <a id="ntpclient"></a>"HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient" 하위 키 항목

|레지스트리 항목 |Version |설명 |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |모든 버전 |피어 간 동기화에서 비표준 모드 조합을 사용할 수 있음을 나타냅니다. 도메인 멤버의 기본값은 **1**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **1**입니다.|
|**CompatibilityFlags** |모든 버전 |다음 호환성 플래그 및 값을 지정합니다.<ul><li>**0x00000001** - DispersionInvalid</li><li>**0x00000002** - IgnoreFutureRefTimeStamp</li><li>**0x80000000** - AutodetectWin2K</li><li>**0x40000000** - AutodetectWin2KStage2</li></ul>도메인 멤버의 기본값은 **0x80000000**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **0x80000000**입니다. |
|**CrossSiteSyncFlags** |모든 버전 |서비스가 컴퓨터 도메인 외부의 동기화 파트너를 선택할지 여부를 결정합니다. 옵션 및 값은 다음과 같습니다.<ul><li>**0** - 없음</li><li>**1** - PdcOnly</li><li>**2** - 모두</li></ul>NT5DS 값이 설정되지 않으면 이 값은 무시됩니다. 도메인 멤버의 기본값은 **2**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **2**입니다. |
|**DllName** |모든 버전 |시간 공급자에 대한 DLL 위치를 지정합니다.<br /><br />도메인 멤버와 독립 실행형 클라이언트 및 서버 모두에서 이 DLL의 기본 위치는 **%windir%\System32\W32Time.dll**입니다. |
|**사용** |모든 버전 |현재 시간 서비스에서 NtpClient 공급자를 사용하도록 설정되어 있는지 여부를 나타냅니다.<ul><li>**1** - 예</li><li>**0** - 아니오</li></ul>도메인 멤버의 기본값은 **1**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **1**입니다.|
|**EventLogFlags** |모든 버전 |Windows 시간 서비스에서 기록하는 이벤트를 지정합니다.<ul><li>**0x1** - 연결 변경</li><li>**0x2** - 큰 샘플 시간차(Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 및 Windows Server 2008 R2에만 적용됨)</li></ul>도메인 멤버의 기본값은 **0x1**입니다. 독립 실행형 클라이언트와 서버의 기본값은**0x1**입니다.|
|**InputProvider** |모든 버전 |NtpClient를 NtpServer에서 시간 정보를 가져오는 InputProvider로 사용하도록 설정할지 여부를 나타냅니다. NtpServer는 로컬 시계 동기화에 유용한 시간 샘플을 반환하여 네트워크의 클라이언트 시간 요청에 응답하는 시간 서버입니다. <ul><li>**1** - 예</li><li>**0** - 아니오</li></ul>도메인 멤버 및 독립 실행형 클라이언트 모두의 기본값은 **1**입니다. |
|**LargeSampleSkew** |모든 버전 |로깅에 대한 큰 샘플 시간차를 초 단위로 지정합니다. SEC(미국 증권 거래 위원회) 사양을 준수하려면 3초로 설정해야 합니다. **EventLogFlags**가 0x2 큰 샘플 시간차로 명시적으로 구성된 경우에만 이 설정에 대한 이벤트가 기록됩니다. 도메인 멤버의 기본값은 3입니다. 독립 실행형 클라이언트 및 서버의 기본값은 3입니다. |
|**ResolvePeerBackOffMaxTimes** |모든 버전 |실패와 함께 동기화할 피어를 반복하여 찾으려고 할 때 대기 간격을 두 배로 늘릴 최대 횟수를 정합니다. 값이 0이면 항상 최소 대기 간격임을 의미합니다. 도메인 멤버의 기본값은 **7**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **7**입니다. |
|**ResolvePeerBackoffMinutes** |모든 버전 |동기화할 피어를 찾기 전에 대기할 초기 간격(분)을 지정합니다. 도메인 멤버의 기본값은 **15**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **15**입니다.  |
|**SpecialPollInterval** |모든 버전 |수동 피어의 특수 폴링 간격을 초 단위로 지정합니다. **SpecialInterval** 0x1 플래그를 사용하도록 설정되면 W32Time은 운영 체제가 결정한 폴링 간격 대신 이 폴링 간격을 사용합니다. 도메인 멤버의 기본값은 **3,600**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **604,800**입니다.<br/><br/>빌드 1702의 새로운 기능인 **SpecialPollInterval**은 **MinPollInterval** 및 **MaxPollInterval** 구성 레지스트리 값에 포함됩니다.|
|**SpecialPollTimeRemaining** |모든 버전 |W32Time에서 유지 관리됩니다. 여기에는 Windows 운영 체제에서 사용하는 예약된 데이터가 포함됩니다. 컴퓨터가 다시 시작된 후 W32Time이 다시 동기화될 때까지의 시간(초)을 지정합니다. 이 설정을 변경하면 예기치 않은 결과가 발생할 수 있습니다. 도메인 멤버 및 독립 실행형 클라이언트 및 서버 모두의 기본값은 비어 있습니다. |

### <a id="ntpserver"></a>"HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer" 하위 키 항목

|레지스트리 항목 |버전 |설명 |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |모든 버전 |클라이언트와 서버 간 동기화에서 비표준 모드 조합을 사용할 수 있음을 나타냅니다. 도메인 멤버의 기본값은 **1**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **1**입니다. |
|**DllName** |모든 버전 |시간 공급자에 대한 DLL 위치를 지정합니다. 도메인 멤버와 독립 실행형 클라이언트 및 서버 모두에서 이 DLL의 기본 위치는 **%windir%\System32\W32Time.dll**입니다.  |
|**사용** |모든 버전 |현재 시간 서비스에서 NtpServer 공급자를 사용하도록 설정되어 있는지 여부를 나타냅니다. <ul><li>**1** - 예</li><li>**0** - 아니오</li></ul>도메인 멤버의 기본값은 **1**입니다. 독립 실행형 클라이언트와 서버의 기본값은 **1**입니다. |
|**InputProvider** |모든 버전 |NtpClient를 NtpServer에서 시간 정보를 가져오는 InputProvider로 사용하도록 설정할지 여부를 나타냅니다. NtpServer는 로컬 시계 동기화에 유용한 시간 샘플을 반환하여 네트워크의 클라이언트 시간 요청에 응답하는 시간 서버입니다. <ul><li>**1** - 예</li><li>**0** - 아니오 = 0 </li></ul>도메인 멤버 및 독립 실행형 클라이언트 모두의 기본값: 1 |

## <a name="reference-pre-set-values-for-the-windows-time-service-gpo-settings"></a>참고자료: Windows 시간 서비스 GPO 설정에 대해 미리 설정된 값  

다음 표에는 Windows 시간 서비스와 연결되는 글로벌 그룹 정책 설정 및 각 설정과 연결되는 미리 설정된 값이 나와 있습니다. 각 설정에 대한 자세한 내용은 이 문서 앞부분의 [참조: Windows 시간 서비스 레지스트리 항목](#reference-windows-time-service-registry-entries)을 참조하십시오. **글로벌 구성 설정**이라는 단일 GPO에 포함된 설정은 다음과 같습니다.  

### <a name="pre-set-values-for-global-group-policy-settings"></a>"글로벌 그룹 정책" 설정에 대해 미리 설정된 값

|그룹 정책 설정|미리 설정된 값|  
| --- | --- |
|**AnnounceFlags**|**10**|  
|**EventLogFlags**|**2**|  
|**FrequencyCorrectRate**|**4**|  
|**HoldPeriod**|**5**|  
|**LargePhaseOffset**|**1,280,000**|  
|**LocalClockDispersion**|**10**|  
|**MaxAllowedPhaseOffset**|**300**|  
|**MaxNegPhaseCorrection**|**54,000**(15시간)|  
|**MaxPollInterval**|**15**|  
|**MaxPosPhaseCorrection**|**54,000**(15시간)|  
|**MinPollInterval**|**10**|  
|**PhaseCorrectRate**|**7**|  
|**PollAdjustFactor**|**5**|  
|**SpikeWatchPeriod**|**90**|  
|**UpdateInterval**|**100**|  

### <a name="pre-set-values-for-configure-windows-ntp-client-settings"></a>"Windows NTP 클라이언트 구성" 설정에 대해 미리 설정된 값

다음 표에는 **Windows NTP 클라이언트 구성** GPO 및 Windows 시간 서비스와 연결되는 미리 설정된 값이 나와 있다. 각 설정에 대한 자세한 내용은 이 문서 앞부분의 [참조: Windows 시간 서비스 레지스트리 항목](#reference-windows-time-service-registry-entries)을 참조하십시오.  

|그룹 정책 설정|미리 설정된 값|  
|------------------------|-----------------|  
|**NtpServer**|time.windows.com, **0x1**|  
|**Type**|기본 옵션:<ul><li>**NTP.** 도메인에 조인되지 않은 컴퓨터에서 사용합니다.</li><li>**NT5DS.** 도메인에 조인된 컴퓨터에서 사용합니다.</li></ul>|  
|**CrossSiteSyncFlags**|**2**|  
|**ResolvePeerBackoffMinutes**|**15**|  
|**ResolvePeerBackoffMaxTimes**|**7**|  
|**SpecialPollInterval**|**3,600**|  
|**EventLogFlags**|**0**|  

## <a name="reference-network-ports-that-the-windows-time-service-uses"></a>참고자료: Windows 시간 서비스가 사용하는 네트워크 포트

Windows 시간은 NTP 사양을 따르므로 모든 시간 동기화 통신에 123 UDP 포트를 사용해야 합니다. 이 포트는 Windows 시간에서 예약하고 항상 예약된 상태로 유지됩니다. 컴퓨터에서 시계를 동기화하거나 시간을 다른 컴퓨터에 제공할 때마다 해당 통신은 123 UDP 포트에서 수행됩니다.  

> [!NOTE]  
> 네트워크 어댑터가 여러 개인 컴퓨터(*멀티홈* 컴퓨터라고도 함)를 사용하는 경우 네트워크 어댑터를 기반으로 Windows 시간 서비스를 선택적으로 사용하도록 설정할 수 없습니다.  

## <a name="related-information"></a>관련 정보  

다음 리소스에는 이 섹션과 관련된 추가 정보가 포함되어 있습니다.  

- IETF RFC 데이터베이스의 RFC *1305*  
