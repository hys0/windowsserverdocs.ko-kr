---
title: IIS 10.0 조정
description: Windows Server 16의 IIS 10.0 웹 서버에 대 한 성능 조정 recommmendations
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: davso; ericam; yashi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 229c4f53578430e35a66e3dbe50f0d9a8e9ac2f5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851666"
---
# <a name="tuning-iis-100"></a>IIS 10.0 조정

인터넷 정보 서비스 (IIS) 10.0는 Windows Server 2016에 포함 되어 있습니다. IIS 8.5 및 IIS 7.0와 유사한 프로세스 모델을 사용 합니다. 커널 모드 웹 드라이버 (http.sys)는 HTTP 요청을 받아서 라우팅합니다. 응답 캐시의 요청을 충족 합니다. 작업자 프로세스는 URL 하위 공간을 등록 하 고 http.sys는 해당 프로세스 (또는 응용 프로그램 풀에 대 한 프로세스 집합)로 요청을 라우팅합니다.

Http.sys는 연결 관리 및 요청 처리를 담당 합니다. 요청은 http.sys 캐시에서 제공 되거나 추가 처리를 위해 작업자 프로세스로 전달 될 수 있습니다. 여러 작업자 프로세스를 구성 하 여 비용을 줄일 수 있습니다. 요청 처리의 작동 방식에 대 한 자세한 내용은 다음 그림을 참조 하세요.

![iis 10.0의 요청 처리](../../media/perftune-guide-iis-request-handling.png)

Http.sys에는 응답 캐시가 포함 되어 있습니다. 요청이 응답 캐시의 항목과 일치 하는 경우 http.sys는 커널 모드에서 직접 캐시 응답을 보냅니다. ASP.NET와 같은 일부 웹 응용 프로그램 플랫폼은 커널 모드 캐시에서 동적 콘텐츠를 캐시할 수 있도록 하는 메커니즘을 제공 합니다. IIS 10.0의 정적 파일 처리기는 일반적으로 요청 되는 파일을 http.sys에 자동으로 캐시 합니다.

웹 서버에는 커널 모드와 사용자 모드 구성 요소가 있으므로 최적의 성능을 위해서는 두 구성 요소를 모두 조정 해야 합니다. 따라서 특정 워크 로드에 대해 IIS 10.0을 조정 하려면 다음을 구성 하는 것이 포함 됩니다.

-   HTTP.SYS 및 관련 커널 모드 캐시

-   응용 프로그램 풀 구성을 비롯 한 작업자 프로세스 및 사용자 모드 IIS

-   성능에 영향을 주는 특정 튜닝 매개 변수

다음 섹션에서는 IIS 10.0의 커널 모드 및 사용자 모드 측면을 구성 하는 방법에 대해 설명 합니다.

## <a name="kernel-mode-settings"></a>커널 모드 설정

성능 관련 HTTP.SYS 설정은 캐시 관리 및 연결 및 요청 관리와 같은 두 가지 광범위 한 범주로 나뉩니다. 모든 레지스트리 설정은 다음 레지스트리 항목에 저장 됩니다.

``` syntax
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters
```

**참고**  HTTP 서비스가 이미 실행 중인 경우 변경 내용을 적용 하려면 다시 시작 해야 합니다.

Â 

## <a name="cache-management-settings"></a>캐시 관리 설정

HTTP.SYS에서 제공 하는 장점 중 하나는 커널 모드 캐시입니다. 응답이 커널 모드 캐시에 있는 경우 커널 모드에서 완전히 HTTP 요청을 충족할 수 있으므로 요청을 처리 하는 CPU 비용이 크게 줄어듭니다. 그러나 IIS 10.0의 커널 모드 캐시는 실제 메모리를 기반으로 하며, 항목 비용은 사용 하는 메모리입니다.

캐시의 항목은 사용 되는 경우에만 유용 합니다. 그러나 항목을 사용 하 고 있는지 여부에 관계 없이이 항목은 항상 실제 메모리를 사용 합니다. 사용 가능한 리소스 (CPU 및 실제 메모리) 및 워크 로드 요구 사항을 고려 하 여 항목의 수명 동안 캐시에 있는 항목의 유용성 (캐시에서 서비스를 제공할 수 없는 공간) 및 비용 (사용 된 실제 메모리)을 평가 해야 합니다. Http.sys는 캐시에서 적극적으로 액세스 되는 항목을 유지 하려고 하지만 특정 작업에 대 한 HTTP.SYS 캐시를 조정 하 여 웹 서버의 성능을 향상 시킬 수 있습니다.

다음은 HTTP.SYS 커널 모드 캐시에 대 한 몇 가지 유용한 설정입니다.

-   **UriEnableCache** 기본값: 1

    0이 아닌 값은 커널 모드 응답과 조각 캐싱을 사용 하도록 설정 합니다. 대부분의 작업의 경우 캐시를 사용 하도록 설정 된 상태로 유지 해야 합니다. 매우 낮은 응답과 조각 캐싱을 원하는 경우 캐시를 사용 하지 않도록 설정 하는 것이 좋습니다.

-   **UriMaxCacheMegabyteCount** 기본값: 0

    커널 모드 캐시에서 사용할 수 있는 최대 메모리를 지정 하는 0이 아닌 값입니다. 기본값인 0은 시스템에서 캐시에 사용할 수 있는 메모리 양을 자동으로 조정할 수 있도록 합니다.

    **참고** 크기를 지정 하면 최대값이 설정 되며, 시스템에서 캐시 크기를 최대 설정 크기로 늘릴 수 없습니다.

    Â 

-   **Urimaxuribytes** 기본값: 262144 바이트 (256 KB)

    커널 모드 캐시에 있는 항목의 최대 크기입니다. 이 보다 큰 응답 또는 조각은 캐시 되지 않습니다. 메모리가 충분 한 경우 제한을 늘립니다. 메모리가 제한적이 고 큰 항목이 작은 항목 crowding 경우 제한을 낮춰 주는 것이 도움이 될 수 있습니다.

-   **UriScavengerPeriod** 기본값: 120 초

    HTTP.SYS 캐시는 청소를 통해 정기적으로 검색 되며 청소 검색 사이에 액세스 하지 않는 항목은 제거 됩니다. 스캐빈저 (scavenger) 기간을 높은 값으로 설정 하면 스캐빈저 검색 횟수가 줄어듭니다. 그러나 자주 액세스 하지 않는 오래 된 항목은 캐시에 남아 있을 수 있으므로 캐시 메모리 사용이 늘어날 수 있습니다. 기간을 너무 낮게 설정 하면 더 자주 청소 하는 검사가 수행 되며,이로 인해 플러시 수와 캐시 변동이 너무 많을 수 있습니다.

## <a name="request-and-connection-management-settings"></a>요청 및 연결 관리 설정

Windows Server 2016에서 HTTP.SYS는 연결을 자동으로 관리 합니다. 다음 레지스트리 설정은 더 이상 사용 되지 않습니다.

-   **MaxConnections**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\MaxConnections
    ```

-   **IdleConnectionsHighMark**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleConnectionsHighMark
    ```

-   **IdleConnectionsLowMark**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleConnectionsLowMark
    ```

-   **IdleListTrimmerPeriod**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\IdleListTrimmerPeriod
    ```

-   **RequestBufferLookasideDepth**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\RequestBufferLookasideDepth
    ```

-   **InternalRequestLookasideDepth**

    ``` syntax
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters\InternalRequestLookasideDepth
    ```


## <a name="user-mode-settings"></a>사용자 모드 설정

이 섹션의 설정은 IISÂ 작업자 프로세스 동작에 영향을 줍니다. 이러한 설정은 대부분 다음 XML 구성 파일에서 찾을 수 있습니다.

% SystemRoot%\\system32\\inetsrv config administration.config\\config\\Applicationhost.config

Appcmd.exe, IIS 10.0 관리 콘솔, WebAdministration 또는 IISAdministration PowerShell Cmdlet을 사용 하 여 변경 합니다. 대부분의 설정은 자동으로 검색 되며 IIS 10.0 작업자 프로세스 또는 웹 응용 프로그램 서버를 다시 시작 하지 않아도 됩니다. Applicationhost.config 파일에 대 한 자세한 내용은 [Applicationhost.config 소개](https://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig)를 참조 하십시오.


## <a name="ideal-cpu-setting-for-numa-hardware"></a>NUMA 하드웨어에 대해 이상적인 CPU 설정

Windows 2016부터 IIS 10.0는 NUMA 하드웨어의 성능 및 확장성을 향상 시키기 위해 스레드 풀 스레드에 대해 자동 이상적인 CPU 할당을 지원 합니다. 이 기능은 기본적으로 사용 하도록 설정 되어 있으며 다음 레지스트리 키를 통해 구성할 수 있습니다.

``` syntax
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\InetInfo\Parameters\ThreadPoolUseIdealCpu
```

이 기능을 사용 하도록 설정 하면 IIS 스레드 관리자는 현재 로드에 따라 모든 NUMA 노드의 모든 Cpu에서 IIS 스레드 풀 스레드를 균등 하 게 분산 하는 데 가장 적합 합니다. 일반적으로이 기본 설정은 NUMA 하드웨어에 대해 변경 되지 않은 상태로 유지 하는 것이 좋습니다.

이상적인 CPU 설정은 [응용 프로그램 풀의 Cpu 설정](https://www.iis.net/configreference/system.applicationhost/applicationpools/add/cpu)에 도입 된 작업자 프로세스 NUMA 노드 할당 설정 (NumaNodeAssignment 및 numaNodeAffinityMode)과 다릅니다 **. ** 이상적인 CPU 설정은 IIS에서 스레드 풀 스레드를 배포 하는 방법에 영향을 주며, 작업자 프로세스 NUMA 노드 할당 설정에 따라 작업자 프로세스가 시작 되는 NUMA 노드를 결정 합니다.

## <a name="user-mode-cache-behavior-settings"></a>사용자 모드 캐시 동작 설정

이 섹션에서는 IISÂ 10.0의 캐싱 동작에 영향을 주는 설정을 설명 합니다. 사용자 모드 캐시는 통합 파이프라인에서 발생 하는 전역 캐싱 이벤트를 수신 하는 모듈로 구현 됩니다. 사용자 모드 캐시를 완전히 사용 하지 않도록 설정 하려면 Applicationhost.config의 System.webserver/globalModules 구성 섹션에 있는 설치 된 모듈 목록에서 FileCacheModule (cachfile .dll) 모듈을 제거 합니다.

**System.webserver/캐싱**

|특성|설명|기본|
|--- |--- |--- |
|사용|**False**로 설정 된 경우 사용자 모드 IIS 캐시를 사용 하지 않도록 설정 합니다. 캐시 적중률이 매우 작은 경우 캐시 코드 경로와 관련 된 오버 헤드를 방지 하기 위해 캐시를 완전히 사용 하지 않도록 설정할 수 있습니다. 사용자 모드 캐시를 사용 하지 않도록 설정 해도 커널 모드 캐시가 사용 되지 않습니다.|True|
|enableKernelCache|**False**로 설정 된 경우 커널 모드 캐시를 사용 하지 않도록 설정 합니다.|True|
|maxCacheSize|IIS 사용자 모드 캐시 크기를 지정 된 크기 (Mb)로 제한 합니다. IIS는 사용 가능한 메모리에 따라 기본값을 조정 합니다. 자주 액세스 하는 파일 집합의 크기와 RAM 또는 IIS 프로세스 주소 공간의 크기를 기준으로 값을 신중 하 게 선택 합니다.|0|
|maxResponseSize|지정 된 크기까지 파일을 캐시 합니다. 실제 값은 데이터 집합에 있는 가장 큰 파일의 수와 크기와 사용 가능한 RAM에 따라 달라 집니다. 자주 요청 되는 크고 많은 파일을 캐시 하면 CPU 사용량, 디스크 액세스 및 관련 대기 시간을 줄일 수 있습니다.|262144|

## <a name="compression-behavior-settings"></a>압축 동작 설정

7\.0에서 시작 하는 IIS는 기본적으로 정적 콘텐츠를 압축 합니다. 또한 동적 콘텐츠 압축은 DynamicCompressionModule가 설치 될 때 기본적으로 사용 하도록 설정 됩니다. 압축 하면 대역폭 사용량이 줄어들지만 CPU 사용량이 늘어납니다. 가능 하면 압축 된 콘텐츠가 커널 모드 캐시에 캐시 됩니다. 8\.5부터 IIS는 정적 및 동적 콘텐츠에 대해 독립적으로 압축을 제어할 수 있습니다. 정적 콘텐츠는 일반적으로 GIF 또는 HTM 파일과 같이 변경 되지 않는 콘텐츠를 나타냅니다. 동적 콘텐츠는 일반적으로 서버 (ASP.NET 페이지)의 스크립트나 코드에 의해 생성 됩니다. 특정 확장의 분류를 정적 또는 동적으로 사용자 지정할 수 있습니다.

압축을 완전히 사용 하지 않도록 설정 하려면 Applicationhost.config에서 System.webserver/globalModules 섹션의 모듈 목록에서 StaticCompressionModule 및 DynamicCompressionModule를 제거 합니다.

**System.webserver/httpCompression**

|특성|설명|기본|
|--- |--- |--- |
|staticCompression-EnableCpuUsage<br><br>staticCompression-DisableCpuUsage<br><br>dynamicCompression-EnableCpuUsage<br><br>dynamicCompression-DisableCpuUsage|현재 백분율 CPU 사용량이 지정 된 제한 보다 높거나 낮은 경우 압축을 사용 하거나 사용 하지 않도록 설정 합니다.<br><br>IIS 7.0 부터는 안정적인 상태 CPU가 비활성화 임계값을 초과 하는 경우 압축이 자동으로 사용 하지 않도록 설정 됩니다. CPU가 사용 임계값 아래로 떨어지면 압축이 사용 됩니다.|50, 100, 50 및 90 각각|
|디렉터리|압축 된 버전의 정적 파일을 일시적으로 저장 하 고 캐시 하는 디렉터리를 지정 합니다. 자주 액세스 하는 경우이 디렉터리를 시스템 드라이브 밖으로 이동 하는 것이 좋습니다.|%SystemDrive%\inetpub\temp\IIS 임시 압축 파일|
|doDiskSpaceLimiting|모든 압축 파일이 차지할 수 있는 디스크 공간의 크기에 대 한 제한이 있는지 여부를 지정 합니다. 압축 된 파일은 **디렉터리** 특성으로 지정 된 압축 디렉터리에 저장 됩니다.|True|
|maxDiskSpaceUsage|압축 된 파일이 압축 디렉터리에서 차지할 수 있는 디스크 공간의 바이트 수를 지정 합니다.<br><br>압축 된 모든 콘텐츠의 전체 크기가 너무 큰 경우이 설정을 늘려야 할 수 있습니다.|100MB|

**System.webserver/urlCompression**

|특성|설명|기본|
|--- |--- |--- |
|doStaticCompression|정적 콘텐츠를 압축할지 여부를 지정 합니다.|True|
|doDynamicCompression|동적 콘텐츠를 압축할지 여부를 지정 합니다.|True|

**참고** 평균 CPU 사용량이 낮은 IIS 10.0를 실행 하는 서버의 경우 특히 응답이 많은 경우 동적 콘텐츠에 대 한 압축을 사용 하도록 설정 하는 것이 좋습니다. 먼저 테스트 환경에서이 작업을 수행 하 여 기준선의 CPU 사용량에 미치는 영향을 평가 해야 합니다.


### <a name="tuning-the-default-document-list"></a>기본 문서 목록 튜닝

기본 문서 모듈은 디렉터리의 루트에 대 한 HTTP 요청을 처리 하 고이를 default.htm 또는 index.htm과 같은 특정 파일에 대 한 요청으로 변환 합니다. 평균적으로 인터넷에서 모든 요청의 25% aroundÂ 기본 문서 경로를 통과 합니다. 이는 개별 사이트에 대해 크게 달라 집니다. HTTP 요청에서 파일 이름을 지정 하지 않은 경우 기본 문서 모듈은 파일 시스템의 각 이름에 대해 허용 되는 기본 문서 목록을 검색 합니다. 이로 인해 성능에 부정적인 영향을 줄 수 있습니다. 특히 콘텐츠를 연결 하려면 네트워크 왕복을 수행 하거나 디스크를 터치 해야 합니다.

기본 문서를 선택적으로 비활성화 하 고 문서 목록을 줄이거나 정렬 하 여 오버 헤드를 방지할 수 있습니다. 기본 문서를 사용 하는 웹 사이트의 경우에는 사용 되는 기본 문서 유형 으로만 목록을 줄여야 합니다. 또한 가장 자주 액세스 하는 기본 문서 파일 이름으로 시작 되도록 목록을 정렬 합니다.

Applicationhost.config의 위치 태그 내에서 구성을 사용자 지정 하거나 콘텐츠 디렉터리에 직접 web.config 파일을 삽입 하 여 특정 Url에 대 한 기본 문서 동작을 선택적으로 설정할 수 있습니다. 이를 통해 필요한 경우에만 기본 문서를 사용 하 고 목록을 각 URL의 올바른 파일 이름으로 설정 하는 하이브리드 방법을 사용할 수 있습니다.

기본 문서를 완전히 사용 하지 않도록 설정 하려면 Applicationhost.config에서 System.webserver/globalModules 섹션의 모듈 목록에서 DefaultDocumentModule을 제거 합니다.

**System.webserver/defaultDocument**

|특성|설명|기본|
|--- |--- |--- |
|enabled|기본 문서를 사용 하도록 지정 합니다.|True|
|&lt;files&gt; 요소|기본 문서로 구성 된 파일 이름을 지정 합니다.|기본 목록은 default.htm, Default .asp, index.htm, index.htm, Iisstart 및 Default.aspx입니다 (기본값).|

## <a name="central-binary-logging"></a>중앙 이진 로깅

서버 세션에 많은 URL 그룹이 있는 경우 개별 URL 그룹에 대해 수백 개의 형식이 지정 된 로그 파일을 만들고 로그 데이터를 디스크에 기록 하는 과정에서 중요 한 CPU 및 메모리 리소스를 빠르게 사용 하 여 성능 및 확장성 문제를 만들 수 있습니다. 중앙 집중식 이진 로깅은 로깅에 사용 되는 시스템 리소스의 양을 최소화 하는 동시에이를 요구 하는 조직에 대 한 자세한 로그 데이터를 제공 합니다. 이진 형식 로그를 구문 분석 하려면 후 처리 도구가 필요 합니다.

CentralLogFileMode 특성을 CentralBinary로 설정 하 고 **enabled** 특성을 **True**로 설정 하 여 중앙 이진 로깅을 사용 하도록 설정할 수 있습니다. 시스템 작업과 로깅 작업 간의 경합을 방지 하기 위해 중앙 로그 파일의 위치를 시스템 파티션과 전용 로깅 드라이브로 이동 하는 것이 좋습니다.

**system.webserver/log**

|특성|설명|기본|
|--- |--- |--- |
|centralLogFileMode|서버에 대 한 로깅 모드를 지정 합니다. 이 값을 CentralBinary로 변경 하 여 중앙 이진 로깅을 사용 하도록 설정 합니다.|사이트|

**system.webserver/log/centralBinaryLogFile**

|특성|설명|기본|
|--- |--- |--- |
|enabled|중앙 이진 로깅을 사용할지 여부를 지정 합니다.|False|
|디렉터리|로그 항목이 기록 될 디렉터리를 지정 합니다.|%SystemDrive%\inetpub\logs\LogFiles|


## <a name="application-and-site-tunings"></a>응용 프로그램 및 사이트 응용 프로그램

다음 설정은 응용 프로그램 풀 및 사이트의 사이트와 관련 됩니다.

**system.webserver/applicationPools/applicationPoolDefaults**

|특성|설명|기본|
|--- |--- |--- |
|queueLength|이후 요청을 거부 하기 전에 응용 프로그램 풀에 대해 큐에 대기 중인 요청 수를 http.sys에 나타냅니다. 이 속성의 값이 초과 되 면 IIS에서 503 오류가 발생 한 이후의 요청을 거부 합니다.<br><br>503 오류가 관찰 되는 경우 대기 시간이 긴 백 엔드 데이터 저장소와 통신 하는 응용 프로그램에 대해이를 증가 시키는 것이 좋습니다.|1000|
|enable32BitAppOnWin64|True로 설정 하면 64 비트 프로세서가 있는 컴퓨터에서 32 비트 응용 프로그램을 실행할 수 있습니다.<br><br>메모리 소비가 중요 한 경우 32 비트 모드를 사용 하도록 설정 하는 것이 좋습니다. 포인터 크기와 명령 크기가 작으므로 32 비트 응용 프로그램은 64 비트 응용 프로그램 보다 적은 메모리를 사용 합니다. 64 비트 컴퓨터에서 32 비트 응용 프로그램을 실행 하는 경우의 단점은 사용자 모드 주소 공간이 4gb로 제한 된다는 것입니다.|False|

**system.webserver/sites/VirtualDirectoryDefault**

|특성|설명|기본|
|--- |--- |--- |
|Allowsubdirconfig 있어서|IIS가 현재 수준 (True) 보다 낮은 콘텐츠 디렉터리의 web.config 파일을 찾을 지 아니면 현재 수준 (False) 보다 낮은 콘텐츠 디렉터리의 web.config 파일을 찾을 수 없는지를 지정 합니다. 가상 디렉터리에만 구성을 허용 하는 간단한 제한 사항을 적용 하 여 IISÂ은 **/&lt;이름&gt;** 를 사용 하는 경우를 제외 하 고 구성 파일을 찾을 수 없다는 것을 알 수 있습니다. 추가 파일 작업을 건너뛰면 고정 콘텐츠를 임의로 액세스할 수 있는 웹 사이트의 성능이 크게 향상 될 수 있습니다.|True|

## <a name="managing-iis-100-modules"></a>IIS 10.0 모듈 관리

IIS 10.0는 모듈식 구조를 지원 하기 위해 여러 사용자 확장 가능 모듈로 구성 되어 있습니다. 이 인수분해에는 약간의 비용이 있습니다. 각 모듈에 대해 통합 파이프라인은 모듈과 관련 된 모든 이벤트에 대해 모듈을 호출 해야 합니다. 이는 모듈에서 작업을 수행 해야 하는지 여부에 관계 없이 발생 합니다. 특정 웹 사이트와 관련이 없는 모든 모듈을 제거 하 여 CPU 주기와 메모리를 절약할 수 있습니다.

간단한 정적 파일용으로 튜닝 된 웹 서버에는 UriCacheModule, HttpCacheModule, StaticFileModule, AnonymousAuthenticationModule 및 HttpLoggingModule와 같은 5 개의 모듈만 포함 될 수 있습니다.

Applicationhost.config에서 모듈을 제거 하려면 system.webserver/globalModules에서 모듈 선언을 제거 하는 것 외에도 system.web/처리기 및 system.webserver/modules 섹션에서 모듈에 대 한 모든 참조를 제거 합니다.

## <a name="classic-asp-settings"></a>기본 ASP 설정

클래식 ASP 요청을 처리 하는 주요 비용에는 스크립트 엔진 초기화, 요청 된 ASP 스크립트를 ASP 템플릿에 컴파일 및 스크립트 엔진에서 템플릿 실행이 포함 됩니다. 템플릿 실행 비용은 요청 된 ASP 스크립트의 복잡도에 따라 달라 지지만 IIS 클래식 ASP 모듈은 메모리에 스크립트 엔진을 캐시 하 고 메모리와 디스크 모두에 메모리와 디스크의 템플릿을 캐시할 수 있습니다 (메모리 내 템플릿 캐시 오버플로 인 경우에만).

다음 설정은 기본 ASP 템플릿 캐시 및 스크립트 엔진 캐시를 구성 하는 데 사용 되며 ASP.NET 설정에 영향을 주지 않습니다.

**System.webserver/asp/cache**

|특성|설명|기본|
|--- |--- |--- |
|diskTemplateCacheDirectory|메모리 내 캐시가 오버플로될 때 ASP가 컴파일된 템플릿을 저장 하기 위해 사용 하는 디렉터리의 이름입니다.<br><br>권장 사항: 과도 하 게 사용 되지 않는 디렉터리 (예: 운영 체제, IIS 로그 또는 기타 자주 액세스 하는 콘텐츠와 공유 되지 않음)로 설정 합니다.|%SystemDrive%\inetpub\temp\ASP 컴파일된 템플릿|
|maxDiskTemplateCacheFiles|디스크에 캐시할 수 있는 컴파일된 ASP 템플릿의 최대 수를 지정 합니다.<br><br>권장 사항: 최 댓 값을 0x7FFFFFFF로 설정 합니다.|2000|
|scriptFileCacheSize|이 특성은 메모리에 캐시할 수 있는 컴파일된 ASP 템플릿의 최대 수를 지정 합니다.<br><br>권장 사항: 응용 프로그램 풀에서 처리 하는 자주 요청 되는 ASP 스크립트 수 만큼 이상으로 설정 합니다. 가능 하면 메모리 한도가 허용 하는 만큼 ASP 템플릿으로 설정 합니다.|500|
|scriptEngineCacheMax|메모리에 캐시 된 상태로 유지 되는 최대 스크립트 엔진 수를 지정 합니다.<br><br>권장 사항: 응용 프로그램 풀에서 처리 하는 자주 요청 되는 ASP 스크립트 수 만큼 이상으로 설정 합니다. 가능 하면 메모리 제한에서 허용 하는 만큼의 스크립트 엔진으로 설정 합니다.|250|

**System.webserver/asp/limits**

|특성|설명|기본|
|--- |--- |--- |
|processorThreadMax|ASP에서 만들 수 있는 프로세서당 최대 작업자 스레드 수를 지정 합니다. 현재 설정이 로드를 처리 하기에 충분 하지 않은 경우 증가 합니다 .이로 인해 요청을 처리 하는 동안 또는 CPU 리소스가 사용 되는 경우 오류가 발생할 수 있습니다.|25|

**System.webserver/asp/comPlus**

|특성|설명|기본|
|--- |--- |--- |
|executeInMta|IIS에서 ASP 콘텐츠를 제공 하는 동안 오류 또는 오류가 검색 되는 경우 **True** 로 설정 합니다. 예를 들어 각 사이트가 자체 작업자 프로세스에서 실행 되는 여러 격리 된 사이트를 호스트 하는 경우이 문제가 발생할 수 있습니다. 오류는 일반적으로 이벤트 뷰어의 COM +에서 보고 됩니다. 이 설정은 ASP에서 다중 스레드 아파트 모델을 사용 하도록 설정 합니다.|False|


## <a name="aspnet-concurrency-setting"></a>ASP.NET 동시성 설정

### <a name="aspnet-35"></a>ASP.NET 3.5
기본적으로 ASP.NET는 서버에서 안정적인 상태 메모리 사용을 줄이기 위해 요청 동시성을 제한 합니다. 높은 동시성 응용 프로그램은 전체 성능을 향상 시키기 위해 일부 설정을 조정 해야 할 수 있습니다. 이 설정은 다음과 같이 aspnet .config 파일에서 변경할 수 있습니다.

``` syntax
<system.web>
  <applicationPool maxConcurrentRequestsPerCPU="5000"/>
</system.web>
```

다음 설정은 시스템에서 리소스를 완전히 사용 하는 데 유용 합니다.

-   **maxConcurrentRequestPerCpu** 기본값: 5000

    이 설정은 시스템에서 동시에 실행 되는 ASP.NET 요청의 최대 수를 제한 합니다. 기본값은 ASP.NET 응용 프로그램의 메모리 사용을 줄이기 위한 것입니다. 긴 동기 i/o 작업을 수행 하는 응용 프로그램을 실행 하는 시스템에서이 제한을 늘려야 합니다. 그렇지 않으면 기본 설정을 사용 하는 경우 높은 부하 상태에서 큐 제한 초과로 인 한 큐 또는 요청 실패로 인해 대기 시간이 길어질 수 있습니다.

### <a name="aspnet-46"></a>ASP.NET 4.6
MaxConcurrentRequestPerCpu 설정 외에도 ASP.NET 4.7는 비동기 작업을 많이 사용 하는 응용 프로그램의 성능을 향상 시키기 위한 설정을 제공 합니다. 이 설정은 aspnet .config 파일에서 변경할 수 있습니다.

``` syntax
<system.web>
  <applicationPool percentCpuLimit="90" percentCpuLimitMinActiveRequestPerCpu="100"/>
</system.web>
```

-   **percentCpuLimit** 기본값: 90 비동기 요청에는 이러한 시나리오에 대 한 큰 부하 (하드웨어 용량 외)가 있는 경우 확장성 문제가 있습니다. 이 문제는 비동기 시나리오에 대 한 할당의 성격 때문에 발생 합니다. 이러한 경우에는 비동기 작업이 시작 될 때 할당이 발생 하 고 완료 되 면 사용 됩니다. 이 시간을 기준으로 개체는 GC에 의해 1 또는 2 세대로 이동 itâs 가능성이 높습니다. 이 경우 부하를 늘리면 시점까지 rps (초당 요청 수)가 증가 합니다. 해당 지점을 전달 하면 GC에 소요 된 시간이 문제가 되기 시작 하 고 rps가 dip를 시작 하 여 크기 조정 효과가 적용 됩니다. 이 문제를 해결 하기 위해 cpu 사용량이 percentCpuLimit 설정을 초과할 경우 요청이 ASP.NET 기본 큐로 전송 됩니다.
-   **percentCpuLimitMinActiveRequestPerCpu** 기본값: 100 CPU 제한 (percentCpuLimit 설정)은 요청 수에 따라 달라 지는 데 비용이 많이 듭니다. 결과적으로, 들어오는 요청을 제외 하 고는 기본 큐에서 백업을 유발 하는 CPU를 많이 사용 하는 요청만 있을 수 있습니다. 이 problme를 해결 하기 위해 percentCpuLimitMinActiveRequestPerCpu를 사용 하 여 조정이 시작 되기 전에 최소 개수의 요청이 처리 되도록 할 수 있습니다.

## <a name="worker-process-and-recycling-options"></a>작업자 프로세스 및 재활용 옵션

IIS 작업자 프로세스를 재활용 하는 옵션을 구성 하 고, 사용자 개입을 요구 하거나 서비스 또는 컴퓨터를 다시 설정 하지 않고도 특정 상황 또는 이벤트에 대 한 실용적인 솔루션을 제공 합니다. 이러한 상황 및 이벤트에는 메모리 누수, 메모리 부하가 늘어나는 또는 응답 하지 않거나 유휴 작업자 프로세스가 포함 됩니다. 일반적인 상황에서 재활용 옵션은 필요 하지 않으며 재활용을 끄거나 시스템을 가끔씩 재활용 하도록 구성할 수 있습니다.

**재순환/periodicRestart** 요소에 특성을 추가 하 여 특정 응용 프로그램에 대 한 프로세스 재활용을 사용 하도록 설정할 수 있습니다. 재생 이벤트는 메모리 사용량, 고정 된 수의 요청 수 및 고정 된 기간을 비롯 한 여러 이벤트에 의해 트리거될 수 있습니다. 작업자 프로세스가 재활용 되 면 큐에 대기 중인 요청 및 실행 중인 요청은 모두 새 요청을 처리 하기 위해 동시에 시작 됩니다. **재순환/periodicRestart** 요소는 응용 프로그램별로, 다음 표의 각 특성이 응용 프로그램 별로 분할 됩니다.

**system.webserver/applicationPools/ApplicationPoolDefaults/재활용/periodicRestart**

|특성|설명|기본|
|--- |--- |--- |
|메모리|가상 메모리 소비가 지정 된 한도 (kb)를 초과 하는 경우 프로세스 재활용을 사용 하도록 설정 합니다. 2gb 주소 공간이 작은 32 비트 컴퓨터의 경우이 설정을 유용 하 게 사용할 수 있습니다. 메모리 부족 오류로 인해 실패 한 요청을 방지 하는 데 도움이 될 수 있습니다.|0|
|privateMemory|개인 메모리 할당이 지정 된 한도 (kb)를 초과 하는 경우 프로세스 재활용을 사용 하도록 설정 합니다.|0|
|요청|특정 요청 수 후에 프로세스 재활용을 사용 하도록 설정 합니다.|0|
|time|지정 된 기간 후에 프로세스 재활용을 사용 하도록 설정 합니다.|29:00:00|


## <a name="dynamic-worker-process-page-out-tuning"></a>동적 작업자-프로세스 페이지 아웃 튜닝

Windows Server 2012 r 2부터 IIS는 시간 동안 유휴 상태가 된 후 (IIS 7 이후 존재 했던 종료 옵션) 작업자 프로세스가 일시 중단 되도록 구성 하는 옵션을 제공 합니다.

유휴 작업자 프로세스 페이지 아웃 및 유휴 작업자 프로세스 종료 기능의 주된 목적은 서버에서 메모리 사용률을 절약 하는 것입니다. 사이트에서 수신 하는 경우에도 많은 메모리가 사용 될 수 있기 때문입니다. 사이트에서 사용 되는 기술 (정적 콘텐츠 vs ASP.NET 및 기타 프레임 워크)에 따라 사용 되는 메모리는 약 10mb에서 수백 메가바이트 사이에 있을 수 있습니다. 즉, 서버가 여러 사이트를 사용 하 여 구성 된 경우 사이트에 대 한 가장 효과적인 설정을 파악 하면 활성 및 일시 중단 된 사이트의 성능을 크게 향상 시킬 수 있습니다.

자세히 설명 하기 전에 메모리 제약 조건이 없는 경우 일시 중단 또는 종료 하지 않도록 사이트를 설정 하는 것이 좋습니다. 그 후에는 thereâs가 컴퓨터에 유일한 값인 경우 작업자 프로세스를 종료 하는 것이 거의 없습니다.

**참고**  메모리 누수가 있는 코드와 같이 불안정 한 코드를 실행 하거나 불안정 한 경우 사이트를 유휴 상태에서 종료 하도록 설정 하는 것은 코드 버그를 수정 하는 데 도움이 될 수 있습니다. 권장 사항이 아니지만 고속 처리에서이 기능을 정리 메커니즘으로 사용 하는 것이 좋지만, 더 영구적인 솔루션이 작동 하는 것이 더 좋을 수 있습니다.\]

Â 

고려해 야 할 또 다른 요소는 사이트에서 많은 메모리를 사용 하는 경우 컴퓨터가 작업자 프로세스에서 사용 하는 데이터를 디스크에 써야 하기 때문에 일시 중단 프로세스 자체에서 부담을 취하는 것입니다. 작업자 프로세스에서 많은 메모리 청크를 사용 하는 경우 일시 중지 하는 것이 백업이 시작 될 때까지 대기 하는 것 보다 비용이 더 많이 들 수 있습니다.

작업자 프로세스 일시 중단 기능을 최대한 활용 하려면 각 응용 프로그램 풀에서 사이트를 검토 하 고 일시 중단 해야 하는 일시 중단 해야 하는 작업을 결정 해야 합니다. 각 작업 및 각 사이트에 대해 이상적인 시간 제한 기간을 파악 해야 합니다.

즉, 일시 중단 또는 종료에 대해 구성할 사이트는 매일 방문자를 포함 하는 사이트 이지만 항상 활성 상태로 유지 하는 데 충분 하지 않습니다. 일반적으로 매일 약 20 개의 고유한 방문자가 있는 사이트입니다. 사이트의 로그 파일을 사용 하 여 트래픽 패턴을 분석 하 고 평균 일별 트래픽 계산을 수행할 수 있습니다.

특정 사용자가 사이트에 연결 되 면 일반적으로 최소한 한 번 이상 요청을 하 고 추가 요청을 수행 하므로 일일 요청 수를 계산 하는 것은 실제 트래픽 패턴을 정확 하 게 반영 하지 않을 수 있습니다. 보다 정확한 정보를 얻기 위해 Microsoft Excel과 같은 도구를 사용 하 여 요청 사이의 평균 시간을 계산할 수도 있습니다. 예를 들면 다음과 같습니다.

||요청 URL|요청 시간|삼각|
|--- |--- |--- |--- |
|1|/SourceSilverLight/Geosource.web/grosource.html|10:01||
|2|/SourceSilverLight/Geosource.web/sliverlight.js|10:10|0:09|
|3|/SourceSilverLight/Geosource.web/clientbin/geo/1.aspx|10:11|0:01|
|4|/lClientAccessPolicy.xml|10:12|0:01|
|5|/원본 Ilverlight/GeosourcewebService/Service .asmx|10:23|0:11|
|6|/SourceSilverLight/Geosource. 웹/GeoSearchServer ...|11:50|1:27|
|7|/rest/Services/CachedServices/Silverlight_load_la ...|12:50|1:00|
|8|/rest/Services/CachedServices/Silverlight_basemap ...|12:51|0:01|
|9|/rest/Services/DynamicService/Silverlight_basemap ...|12:59|0:08|
|10|/rest/Services/CachedServices/Ortho_2004_cache ...|13:40|0:41|
|11|/rest/Services/CachedServices/Ortho_2005_cache|13:40|0:00|
|12|/rest/Services/CachedServices/OrthoBaseEngine.aspx|13:41|0:01|

그러나 하드 부분은 적용 하기 위해 적용 해야 하는 설정을 파악 하는 것입니다. 이 경우 사이트는 사용자 로부터 다양 한 요청을 가져오고 위의 표에 4 시간 동안 총 4 개의 고유 세션이 발생 했음을 보여 줍니다. 응용 프로그램 풀의 작업자 프로세스 일시 중단에 대 한 기본 설정을 사용 하 여 사이트는 기본 제한 시간 (20 분) 후에 종료 됩니다. 즉, 이러한 각 사용자는 사이트 스핀 주기를 경험 하 게 됩니다. 이를 통해 작업자 프로세스를 일시 중단 하는 것이 가장 좋습니다. 대부분의 시간에는 사이트가 유휴 상태 이므로이를 일시 중단 하면 리소스가 절약 되 고 사용자가 거의 즉시 사이트에 연결할 수 있습니다.

이에 대 한 마지막 및 매우 중요 한 정보는이 기능에 디스크 성능이 매우 중요 하다는 것입니다. 일시 중단 및 절전 모드 해제 프로세스에는 하드 드라이브에 많은 양의 데이터를 쓰고 읽는 작업이 포함 되므로이를 위해 고속 디스크를 사용 하는 것이 좋습니다. Ssd (반도체 드라이브)를 사용 하는 것이 좋지만이 경우에는 Windows 페이지 파일이 저장 되어 있는지 확인 해야 합니다. 운영 체제 자체를 SSD에 설치 하지 않은 경우에는 운영 체제를 구성 하 여 페이지 파일을 이동 합니다.

SSD를 사용 하는지 여부에 관계 없이 페이지 파일 크기를 수정 하 여 파일 크기 조정 없이 페이지 아웃 데이터를 해당 파일에 쓸 수 있도록 하는 것이 좋습니다. 페이지 파일 크기 조정은 운영 체제가 데이터를 페이지 파일에 저장 해야 하는 경우에 발생할 수 있습니다. 기본적으로 Windows는 필요에 따라 크기를 자동으로 조정 하도록 구성 되어 있기 때문입니다. 크기를 고정 하나로 설정 하면 크기 조정을 방지 하 고 성능을 크게 향상 시킬 수 있습니다.

미리 고정 된 페이지 파일 크기를 구성 하려면 일시 중단 하는 사이트 수 및 사용 중인 메모리 크기에 따라 이상적인 크기를 계산 해야 합니다. 활성 작업자 프로세스에 대 한 평균이 200이 고 일시 중단할 서버에 500 사이트가 있는 경우 페이지 파일의 기본 크기 () 이상 (이 예제에서는 기본 + 100 GB) 이상으로 페이지 파일의 크기 (200 \* 500) 이상 이어야 합니다.

**참고** 사이트가 일시 중단 되 면 각 사이트는 약 6gb를 사용 하므로,이 경우 모든 사이트를 일시 중단 하는 경우 메모리 사용량이 약 3gb가 됩니다. 그러나 실제로 youâre는 모두 동시에 일시 중단 된 것은 아닙니다.

 
## <a name="transport-layer-security-tuning-parameters"></a>전송 계층 보안 튜닝 매개 변수

TLS (전송 계층 보안)를 사용 하면 CPU 비용이 추가로 부과 됩니다. TLS의 가장 저렴 한 구성 요소는 전체 핸드셰이크를 포함 하기 때문에 세션 설정을 설정 하는 비용입니다. 다시 연결, 암호화 및 암호 해독이 비용에도 추가 됩니다. TLS 성능을 향상 시키려면 다음을 수행 합니다.

-   TLS 세션에 대해 HTTP 연결 유지를 사용 하도록 설정 합니다. 이렇게 하면 세션 설정 비용이 제거 됩니다.

-   필요에 따라 세션을 다시 사용 합니다. 특히 연결 되지 않은 트래픽을 사용 합니다.

-   전체 사이트가 아닌 필요한 사이트 또는 페이지의 일부분에만 암호화를 선택적으로 적용 합니다.

**참고**
-   키가 클수록 보안성이 향상 되지만 더 많은 CPU 시간이 사용 됩니다.

-   모든 구성 요소는 암호화 하지 않아도 됩니다. 그러나 일반 HTTP와 HTTPS를 함께 설치 하면 페이지의 일부 콘텐츠가 안전 하지 않은 팝업 경고가 발생할 수 있습니다.

 
## <a name="internet-server-application-programming-interface-isapi"></a>ISAPI (인터넷 서버 응용 프로그래밍 인터페이스)

ISAPI 응용 프로그램에는 특별 한 튜닝 매개 변수가 필요 하지 않습니다. 개인 ISAPI 확장을 작성 하는 경우 성능 및 리소스 사용을 위해 작성 되었는지 확인 합니다.

## <a name="managed-code-tuning-guidelines"></a>관리 코드 조정 지침

IIS 10.0의 통합 파이프라인 모델을 통해 높은 수준의 유연성과 확장성을 사용할 수 있습니다. 네이티브 또는 관리 코드에서 구현 된 사용자 지정 모듈을 파이프라인에 삽입 하거나 기존 모듈을 바꿀 수 있습니다. 이 확장성 모델은 편의성과 단순성을 제공 하지만 전역 이벤트에 연결 되는 새 관리 모듈을 삽입 하기 전에 주의 해야 합니다. 전역 관리 모듈을 추가 하는 것은 정적 파일 요청을 비롯 한 모든 요청이 관리 코드를 터치 해야 함을 의미 합니다. 사용자 지정 모듈은 가비지 수집과 같은 이벤트에 취약 합니다. 또한 사용자 지정 모듈은 네이티브 코드와 관리 코드 간에 데이터를 마샬링하는 것으로 인해 상당한 CPU 비용을 추가 합니다. 가능 하면 관리 되는 모듈에 대 한 managedHandler로 사전 조건을 설정 해야 합니다.

콜드 시작 성능을 향상 시키려면 ASP.NET 웹 사이트를 미리 컴파일하거나 IIS 응용 프로그램 초기화 기능을 활용 하 여 응용 프로그램을 준비 해야 합니다.

세션 상태가 필요 하지 않은 경우 각 페이지에 대해 해제 해야 합니다.

I/o 바인딩된 작업이 많은 경우 더 나은 확장성을 제공 하는 관련 Api의 비동기 버전을 사용 합니다.

또한 출력 캐시를 적절히 사용 하면 웹 사이트의 성능도 향상 됩니다.

격리 모드에서 ASP.NET 스크립트를 포함 하는 여러 호스트를 실행 하는 경우 (사이트당 하나의 응용 프로그램 풀) 메모리 사용량을 모니터링 합니다. 서버에 동시에 실행 되는 응용 프로그램 풀의 예상 수에 대 한 충분 한 RAM이 있는지 확인 합니다. 여러 개의 격리 된 프로세스 대신 여러 응용 프로그램 도메인을 사용 하는 것이 좋습니다.


## <a name="other-issues-that-affect-iis-performance"></a>IIS 성능에 영향을 주는 기타 문제

IIS 성능에 영향을 줄 수 있는 문제는 다음과 같습니다.

-   캐시를 인식 하지 않는 필터 설치

    HTTP 캐시가 인식 되지 않는 필터를 설치 하면 IIS에서 캐싱을 완전히 사용 하지 않도록 설정 하 여 성능이 저하 됩니다. IISÂ 6.0 이전에 작성 된 ISAPI 필터는이 동작을 유발할 수 있습니다.

-   CGI (Common Gateway Interface) 요청

    성능상의 이유로 IIS에서는 CGI 응용 프로그램을 사용 하 여 요청을 처리 하지 않는 것이 좋습니다. 자주 발생 하는 CGI 프로세스 만들기 및 삭제는 상당한 오버 헤드를 포함 합니다. 더 나은 대안은 FastCGI, ISAPI 응용 프로그램 스크립트 및 ASP 또는 ASP.NET 스크립트를 사용 하는 것입니다. 이러한 각 옵션에 대해 격리를 사용할 수 있습니다.

## <a name="see-also"></a>참고 항목
- [웹 서버 성능 조정](index.md) 
- [HTTP 1.1/2 튜닝](http-performance.md)
