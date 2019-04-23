---
title: IIS 10.0 튜닝
description: Windows Server 16에서 IIS 10.0 웹 서버에 대 한 recommmendations 튜닝 성능
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: DavSo; Ericam; YaShi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 16ea5c857d99e8a69f528e81178911236341dbb8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869854"
---
# <a name="tuning-iis-100"></a>IIS 10.0 튜닝

인터넷 정보 서비스 (IIS) 10.0 Windows ServerÂ 2016 포함 되어 있습니다. IIS 8.5 및 IIS 7.0의 비슷한 프로세스 모델을 사용합니다. 웹 커널 모드 드라이버 (http.sys) HTTP 요청을 라우팅합니다 받고 해당 응답 캐시에서 요청을 충족 합니다. 작업자 프로세스 URL subspaces 등록 하 고 http.sys 적절 한 프로세스 (또는 응용 프로그램 풀에 대 한 프로세스 집합)에 요청을 라우팅합니다.

HTTP.sys는 연결 관리와 요청 처리 하는 일을 담당 합니다. 요청은 http.sys에서 처리 또는 추가 처리에 대 한 작업자 프로세스를 전달할 수 있습니다. 비용을 절감 하는 격리를 제공 하는 여러 작업자 프로세스가 구성할 수 있습니다. 하는 방법에 대 한 자세한 정보에 대 한 요청 처리 작동, 다음 그림을 참조 하세요.

![iis 10.0의에서 처리를 요청 합니다.](../../media/perftune-guide-iis-request-handling.png)

HTTP.sys는 응답 캐시를 포함합니다. 응답 캐시의 항목과 일치 하는 요청을 하는 경우 HTTP.sys 커널 모드에서 직접 캐시 응답을 보냅니다. 일부 웹 응용 프로그램 플랫폼에서는 ASP.NET과 같은 모든 동적 콘텐츠를 커널 모드 캐시에 캐시를 사용 하도록 설정 하는 메커니즘을 제공 합니다. IIS 10.0에서 정적 파일 처리기는 자동으로 http.sys에 자주 요청 된 파일을 캐시합니다.

웹 서버에 사용자 모드 및 커널 모드 구성 요소에 두 구성 요소는 최적의 성능을 위해 조정 해야 합니다. 따라서 특정 워크 로드에 대 한 IIS 10.0 튜닝 구성이 다음 포함:

-   HTTP.sys 및 연결 된 커널 모드 캐시

-   작업자 프로세스와 IIS 사용자 모드 응용 프로그램 풀 구성을 비롯 한

-   성능에 영향을 주는 특정 튜닝 매개 변수

다음 섹션에서는 IIS 10.0의 커널 모드 및 사용자 모드 측면을 구성 하는 방법에 설명 합니다.

## <a name="kernel-mode-settings"></a>커널 모드 설정

두 가지 범주로 크게 나눌 성능 관련 HTTP.sys 설정: 관리 및 연결 하 고 요청을 캐시 합니다. 모든 레지스트리 설정은 다음 레지스트리 항목에서 저장 됩니다.

``` syntax
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Http\Parameters
```

**참고**   이미 실행 중인 HTTP 서비스를 다시 시작 해야 변경 내용이 적용 됩니다.

Â 

## <a name="cache-management-settings"></a>캐시 관리 설정

HTTP.sys를 제공 하는 이점 중 하나는 커널 모드 캐시 합니다. 응답에 있는 경우 커널 모드 캐시 요청을 처리 하는 CPU 비용을 상당히 줄일 수는 커널 모드에서 HTTP 요청을 충족할 수 있습니다. 그러나 IIS 10.0의 커널 모드 캐시 실제 메모리를 기준으로 하며 항목의 비용이 차지 하는 메모리입니다.

항목이 캐시에 사용 되는 경우에 유용 합니다. 그러나 항목 항상 실제 메모리 사용, 항목을 사용 하 되 고 있는지 여부. 사용 가능한 리소스 (CPU 및 실제 메모리)와 워크 로드를 고려 하 여 항목의 수명 동안 캐시 (캐시에서 사용할 수 없도록 절감) 및 해당 비용 (사용한 실제 메모리)에 있는 항목의 유용성을 평가 해야 합니다. 요구 사항입니다. HTTP.sys를 유용 하 고 적극적으로 액세스 항목 수 있지만 캐시에서 특정 워크 로드에 대 한 HTTP.sys 캐시를 튜닝 하 여 웹 서버의 성능을 높일 수만 유지 하려고 합니다.

다음은 http.sys 커널 모드에 대 한 몇 가지 유용한 설정입니다.

-   **UriEnableCache** 기본값: 1

    0이 아닌 값에는 커널 모드 응답 및 조각 캐싱을 수 있습니다. 대부분의 워크 로드에 대 한 캐시 설정 된 상태로 유지 됩니다. 매우 낮은 응답 및 조각 캐싱 예상 되는 경우 캐시를 사용 하지 않도록 설정 하는 것이 좋습니다.

-   **UriMaxCacheMegabyteCount** 기본값: 0

    커널 모드 캐시에 사용할 수 있는 최대 메모리를 지정 하는 0이 아닌 값입니다. 기본값 0으로 시스템을에서 자동으로 캐시에 사용 가능한 메모리가 얼마나를 조정할 수 있습니다.

    **참고** 만 최대값을 설정 하는 크기를 지정 하 고 시스템 최대 집합 크기 만큼 증가 캐시 수 없는 경우도 있습니다.

    Â 

-   **UriMaxUriBytes** 기본값: 262144 바이트 (256KB)

    커널 모드 캐시에 있는 항목의 최대 크기입니다. 응답 또는이 값 보다 큰 조각 캐시 되지 않습니다. 충분 한 메모리에 있는 경우에 제한을 늘려야 하는 것이 좋습니다. 메모리 제한 되며 많은 항목을 더 작은 아웃 채우고 있는 경우에 제한을 낮춥니다에 유용할 수 있습니다.

-   **UriScavengerPeriod** 기본값: 120 초

    Http.sys는 청소에 의해 주기적으로 검색 하 고 청소 검사 액세스 하지 않는 항목 제거 됩니다. 청소 검색 수가 줄어듭니다 청소 기간을 높은 값으로 설정 합니다. 그러나 오래 된, 자주 액세스 하지 않는 항목이 캐시에 남아 있을 수 있으므로 캐시 메모리 사용량을 늘릴 수 있습니다. 너무 기간 설정 낮은 자주 청소 검색 시키고 너무 많은 플러시에서 결과 이탈을 캐시 합니다.

## <a name="request-and-connection-management-settings"></a>요청 및 연결 관리 설정

Windows Server 2016에서 HTTP.sys는 연결을 자동으로 관리합니다. 다음 레지스트리 설정은 더 이상 사용 됩니다.

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

이 섹션의 설정은 IISÂ 10.0 작업자 프로세스 동작을 영향을 줍니다. 다음 XML 구성 파일에서 이러한 설정 중 대부분을 찾을 수 있습니다.

%SystemRoot%\\system32\\inetsrv\\config\\applicationHost.config

Appcmd.exe, IIS 10.0 관리 콘솔, WebAdministration 또는 iis 관리 PowerShell Cmdlet을 사용 하 여 변경 합니다. 대부분의 설정은 자동으로 검색 하 고 IIS 10.0 작업자 프로세스 또는 웹 응용 프로그램 서버를 다시 시작할 필요가 없습니다. ApplicationHost.config 파일에 대 한 자세한 내용은 참조 하세요. [ApplicationHost.config 소개](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig)합니다.


## <a name="ideal-cpu-setting-for-numa-hardware"></a>NUMA 하드웨어에 대 한 이상적인 CPU 설정

Windows 2016에서 시작 하며, IIS 10.0 성능과 NUMA 하드웨어에서 확장성을 향상 시키기 위해 해당 스레드 풀 스레드에 대 한 자동 이상적 CPU 할당을 지원 합니다. 이 기능은 기본적으로 사용 되는데 다음 레지스트리 키를 통해 구성할 수 있습니다.

``` syntax
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\InetInfo\Parameters\ThreadPoolUseIdealCpu
```

이 기능을 사용 하면 IIS 스레드 관리자가 현재 로드에 따라 모든 NUMA 노드에 있는 모든 Cpu에서 IIS 스레드 풀 스레드를 균등 하 게 배포 하기 위해 최상의 노력 수 있습니다. 일반적으로 다음 설정은 NUMA 하드웨어에 대 한 변경 하지 않고이 기본값을 유지 하는 것이 좋습니다.

**참고**   작업자 프로세스 NUMA 노드에 할당 설정을 (numaNodeAssignment 및 numaNodeAffinityMode)에 도입 된 이상적인 CPU 설정을 다릅니다 [응용 프로그램 풀에 대 한 CPU 설정을](https://www.iis.net/configreference/system.applicationhost/applicationpools/add/cpu)합니다. 이상적인 CPU 설정을 작업자 프로세스가 시작 되는 NUMA 노드에 작업자 프로세스 NUMA 노드에 할당 설정을 확인 하는 동안 IIS에서 해당 스레드 풀 스레드를 배포 하는 방법을 하는 영향을 줍니다.

## <a name="user-mode-cache-behavior-settings"></a>사용자 모드 캐시 동작 설정

이 섹션에서는 IISÂ 10.0의 캐싱 동작에 영향을 주는 설정을 설명 합니다. 사용자 모드 캐시 통합된 파이프라인에서 발생 하는 전역 캐싱 이벤트를 수신 하는 모듈로 구현 됩니다. 사용자 모드 캐시를 완전히 사용 하지 않으려면 FileCacheModule (cachfile.dll) 모듈 applicationHost.config에 system.webServer/globalModules 구성 섹션에서 설치 된 모듈 목록에서 제거 합니다.

**system.webServer/caching**

|attribute|설명|기본값|
|--- |--- |--- |
|Enabled|로 설정 하면 사용자 모드 IIS 캐시를 사용 하지 않도록 설정 **False**합니다. 캐시 적중 하는 경우 속도 매우 작은 캐시의 캐시 코드 경로 사용 하 여 연결 된 오버 헤드를 방지할를 완전히 비활성화할 수 있습니다. 사용자 모드 캐시를 사용 하지 않도록 설정 하는 경우에 커널 모드 캐시를 해제 되지 않습니다.|True|
|enableKernelCache|로 설정 된 경우 커널 모드 캐시를 사용 하지 않도록 설정 **False**합니다.|True|
|maxCacheSize|IIS 사용자 모드 캐시 크기를 메가바이트 단위로 지정된 된 크기를 제한합니다. IIS는 사용 가능한 메모리에 따라 기본값을 조정합니다. 액세스 한 RAM 또는 IIS 프로세스 주소 공간의 양과 파일을 자주 집합의 크기에 따라 신중 하 게 값을 선택 합니다.|0|
|maxResponseSize|최대 지정한 크기까지 파일을 캐시합니다. 실제 값 수와 사용 가능한 RAM 및 데이터 집합의 가장 큰 파일 크기에 따라 달라 집니다. 많은 캐싱, 자주 요청 된 파일에 CPU 사용량, 디스크 액세스 및 연결된 대기 시간 줄일 수 있습니다.|262144|

## <a name="compression-behavior-settings"></a>압축 동작 설정

기본적으로 정적 콘텐츠를 압축 하는 IIS 7.0에서 시작 합니다. 또한 동적 콘텐츠 압축은 DynamicCompressionModule 설치 될 때 기본으로 사용 됩니다. 압축 대역폭 줄어들지만 CPU 사용량을 늘립니다. 압축 된 콘텐츠는 가능 하면 커널 모드 캐시에 캐시 됩니다. 8.5에서 시작 하며, IIS는 압축을 정적 및 동적 콘텐츠에 대 한 독립적으로 제어할 수 있습니다. 일반적으로 정적 콘텐츠가 변경 되지 않는, GIF 또는 HTM 파일 같은 콘텐츠를 가리킵니다. 동적 콘텐츠는 일반적으로 서버에서 ASP.NET 페이지, 코드나 스크립트에서 생성 됩니다. 정적 또는 동적으로 모든 특정 확장의 분류를 사용자 지정할 수 있습니다.

압축을 완전히 사용 하지 않으려면 StaticCompressionModule 및 DynamicCompressionModule applicationHost.config에 system.webServer/globalModules 섹션의 모듈 목록에서 제거 합니다.

**system.webServer/httpCompression**

|attribute|설명|기본값|
|--- |--- |--- |
|staticCompression-EnableCpuUsage<br><br>staticCompression-DisableCpuUsage<br><br>dynamicCompression-EnableCpuUsage<br><br>dynamicCompression-DisableCpuUsage|사용 하거나 현재 CPU 사용량 비율 위에 하거나 지정 된 제한 임계값 아래로 떨어질 경우 압축을 사용 하지 않도록 설정 합니다.<br><br>IIS 7.0 부터는 압축은 자동으로 비활성화 넘는 CPU 사용 안 함 임계값 증가 합니다. CPU 사용 임계값 아래로 떨어질 경우 압축이 사용 됩니다.|50, 100, 50, 및 90 각각|
|directory|정적 파일의 압축 된 버전이 임시로 저장 되 고 캐시 디렉터리를 지정 합니다. 자주 액세스 하는 경우 시스템 드라이브가이 디렉터리를 이동 하는 것이 좋습니다.|%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files|
|doDiskSpaceLimiting|모든 압축 된 파일 차지할 수 있는 디스크 공간에 대 한 제한이 있는지 여부를 지정 합니다. 압축 된 파일에 지정 된 압축 디렉터리에 저장 되는 **directory** 특성입니다.|True|
|maxDiskSpaceUsage|압축 디렉터리에 압축 된 파일 차지할 수 있는 디스크 공간의 바이트 수를 지정 합니다.<br><br>이 설정은 모든 압축 된 콘텐츠의 총 크기가 너무 큰 경우 증가 해야 합니다.|100MB|

**system.webServer/urlCompression**

|attribute|설명|기본값|
|--- |--- |--- |
|doStaticCompression|정적 콘텐츠 압축 되어 있는지 여부를 지정 합니다.|True|
|doDynamicCompression|동적 콘텐츠 압축 되어 있는지 여부를 지정 합니다.|True|

**참고** 실행 서버의 IIS 10.0 평균 CPU 사용량이 있는 경우는 것이 좋습니다 동적 콘텐츠 압축을 사용 하도록 설정 하면 응답 큰 경우에 특히 합니다. 이 기준선에서 CPU 사용량에 영향을 평가 하는 테스트 환경에서 먼저 수행 되어야 합니다.


### <a name="tuning-the-default-document-list"></a>기본 문서 목록 튜닝

기본 문서 모듈 디렉터리의 루트에 대 한 HTTP 요청을 처리 하 고 Default.htm Index.htm 등 특정 파일에 대 한 요청으로 변환 됩니다. 인터넷에서 모든 요청의 aroundÂ 25%는 평균적으로 기본 문서 경로 통해 이동합니다. 개별 사이트에 대 한 상당히 다릅니다. HTTP 요청에 파일 이름을 지정 하지 않으면, 기본 문서 모듈 파일 시스템에서 각 이름에 대해 허용 된 기본 문서 목록을 검색 합니다. 이 저하 될 수 있습니다 성능, 특히 콘텐츠에 도달 하려면 네트워크 왕복 여정 또는 디스크 닿아 하는 경우.

줄이거나 문서 목록을 정렬 하 고 선택적으로 기본 문서를 비활성화 하는 오버 헤드를 방지할 수 있습니다. 웹 사이트의 기본 문서를 사용 하는 경우에 사용 되는 기본 문서 종류만 목록을 줄여야 합니다. 또한 순서 목록 액세스 기본 문서 파일 이름으로 가장 자주 시작 합니다.

ApplicationHost.config에서 위치 태그를 내 구성을 사용자 지정 하거나 직접 콘텐츠 디렉터리에에서 web.config 파일을 삽입 하 여 특정 Url에서 기본 문서 동작을 선택적으로 설정할 수 있습니다. 이렇게 하면만 되 필요 하 고 올바른 파일은 각 URL에 대 한 이름을 설정 하는 기본 문서를 사용 하도록 설정 하는 하이브리드 방식을으로, 수 있습니다.

기본 문서를 완전히 비활성화 하려면 DefaultDocumentModule applicationHost.config에 system.webServer/globalModules 섹션의 모듈 목록에서 제거 합니다.

**system.webServer/defaultDocument**

|attribute|설명|기본값|
|--- |--- |--- |
|enabled|기본 문서 설정 되어 있는지를 지정 합니다.|True|
|&lt;파일&gt; 요소|기본 문서 구성 된 파일 이름을 지정 합니다.|기본 목록은 Default.htm, Default.asp, Index.htm, Index.html, Iisstart.htm, 및 Default.aspx입니다.|

## <a name="central-binary-logging"></a>이진 중앙 로깅

수백 개의 개별 URL 그룹에 대 한 서식이 지정 된 로그 파일을 만들고 로그 데이터를 디스크에 쓰는 프로세스 중요 한 CPU 및 메모리 리소스를 만든 후에 새 성능을 신속 하 게 사용할 수 있습니다 서버 세션을 다양 한 URL 그룹 아래에 있는 경우 및 확장성 문제입니다. 이진 중앙 집중식된 로깅 동시 필요로 하는 조직에 대 한 자세한 로그 데이터를 제공 합니다. 로깅에 사용 되는 시스템 리소스의 양을 최소화 합니다. 이진 형식의 로그를 구문 분석 후 처리 하는 도구에 필요 합니다.

이진 중앙 로깅 CentralBinary 및 설정을 centralLogFileMode 특성을 설정 하 여 설정할 수 있습니다.는 **활성화** 특성을 **True**합니다. 시스템 파티션을 오프 및 시스템 작업 및 로깅 작업 간의 경합을 방지 하려면 로깅 전용된 드라이브 중앙 로그 파일의 위치를 이동 하는 것이 좋습니다.

**system.applicationHost/log**

|attribute|설명|기본값|
|--- |--- |--- |
|centralLogFileMode|서버에 대 한 로깅 모드를 지정합니다. CentralBinary 중앙 이진 로깅을 사용 하도록 설정 하려면이 값을 변경 합니다.|사이트|

**system.applicationHost/log/centralBinaryLogFile**

|attribute|설명|기본값|
|--- |--- |--- |
|enabled|중앙 이진 로깅이 사용 되는지 여부를 지정 합니다.|False|
|directory|로그 항목 기록 되는 디렉터리를 지정 합니다.|%SystemDrive%\inetpub\logs\LogFiles|


## <a name="application-and-site-tunings"></a>응용 프로그램 및 사이트 tunings

다음 설정을 응용 프로그램 풀 및 사이트 tunings와 관련이 있습니다.

**system.applicationHost/applicationPools/applicationPoolDefaults**

|attribute|설명|기본값|
|--- |--- |--- |
|queueLength|몇 개의 요청 큐에 대기 됩니다 응용 프로그램 풀에 대 한 이후 요청이 거부 되며 전에 HTTP.sys를 나타냅니다. 이 속성의 값이 초과 되 면 IIS는 503 오류를 사용 하 여 후속 요청을 거부 합니다.<br><br>503 오류가 확인 되 면 높은 대기 시간 백 엔드 데이터 저장소와 통신 하는 응용 프로그램에 대 한이 증가 하는 것이 좋습니다.|1000|
|enable32BitAppOnWin64|True 인 경우에 64 비트 프로세서가 있는 컴퓨터에서 실행 되도록 32 비트 응용 프로그램을 수 있습니다.<br><br>메모리 사용량이 염려 되는 경우에 32 비트 모드를 사용 하도록 설정 하는 것이 좋습니다. 포인터 크기 및 명령 크기 보다 작은 이기 때문에 32 비트 응용 프로그램이 64 비트 응용 프로그램 보다 적은 메모리를 사용 합니다. 64 비트 컴퓨터에서 32 비트 응용 프로그램을 실행 하려면 단점은 사용자 모드 주소 공간은 4GB로 제한 됩니다.|False|

**system.applicationHost/sites/VirtualDirectoryDefault**

|attribute|설명|기본값|
|--- |--- |--- |
|allowSubDirConfig|IIS 찾습니다 현재 보다 낮은 콘텐츠 디렉터리의 web.config 파일에 대 한 수준 (True) 또는 (False)는 현재 수준 보다 낮은 콘텐츠 디렉터리의 web.config 파일을 찾지 않습니다 여부를 지정 합니다. 가상 디렉터리에만 구성에서는 간단한 제한 사항 적용 함으로써 IISÂ 10.0 알 수는 경우가 아니면  **/ &lt;이름&gt;.htm** 가상 디렉터리에 대 한 찾지 해야는 구성 파일입니다. 추가 파일 작업을 건너뛰는 중 매우 큰 정적 콘텐츠를 임의로 액세스 집합이 있는 웹 사이트의 성능을 크게 향상할 수 있습니다.|True|

## <a name="managing-iis-100-modules"></a>IIS 10.0 모듈 관리

모듈형 구조를 지원 하기 위해 여러 사용자를 확장할 수 있는 모듈로 IIS 10.0 팩터링되며 되었습니다. 이 팩 토 링이 화에 적은 비용이 있습니다. 각 모듈에 대 한 통합된 파이프라인 모듈에 관련 된 모든 이벤트에 대 한 모듈을 호출 해야 합니다. 모듈 하나를 수행 해야 하는지 여부에 관계 없이 이런 작업 합니다. 특정 웹 사이트에 관련 되지 않은 모든 모듈을 제거 하 여 CPU 사이클과 메모리를 절약할 수 있습니다.

간단한 정적 파일에 대 한 튜닝는 웹 서버는 다음 다섯 가지 모듈 에서만 포함 될 수 있습니다. UriCacheModule, HttpCacheModule, StaticFileModule, AnonymousAuthenticationModule, 및 HttpLoggingModule 합니다.

ApplicationHost.config에서 모듈을 제거할 system.webServer/globalModules 모듈 선언 제거 하는 것 외에도 system.webServer/handlers 및 system.webServer/modules 섹션에서 모듈에 대 한 모든 참조를 제거 합니다.

## <a name="classic-asp-settings"></a>클래식 ASP 설정

클래식 ASP 요청을 처리 하는 주요 비용 ASP 템플릿에 요청 된 ASP 스크립트를 컴파일하고 스크립트 엔진에 템플릿을 실행 하는 스크립트 엔진을 초기화 하는 포함 되어 있습니다. 템플릿 실행 비용은 요청한 ASP 스크립트의 복잡성에 따라 달라 지지만, IIS 클래식 ASP 모듈 수 캐시 메모리와 디스크에서 메모리 및 캐시 템플릿에서 스크립트 엔진 (경우에 템플릿 메모리 내 캐시가 오버플로될)의 성능을 향상 시키기 위해 CPU 바인딩된 시나리오입니다.

클래식 ASP 템플릿 캐시 및 스크립트 엔진 캐시를 구성 하는 다음 설정을 사용 하 고 ASP.NET 설정이 영향을 주지 않습니다.

**system.webServer/asp/cache**

|attribute|설명|기본값|
|--- |--- |--- |
|diskTemplateCacheDirectory|ASP를 사용 하 여 메모리 내 캐시가 오버플로될 경우 컴파일된 템플릿을 저장할 디렉터리의 이름입니다.<br><br>권장 사항: 과도 하 게 되는 디렉터리 집합 사용, 예를 들어, 운영 체제, IIS 로그와 공유 되지 않은 드라이브 또는 자주 액세스 한 다른 콘텐츠입니다.|%SystemDrive%\inetpub\temp\ASP Compiled Templates|
|maxDiskTemplateCacheFiles|디스크에 캐시할 수 있는 컴파일된 ASP 템플릿의 최대 수를 지정 합니다.<br><br>권장 사항: 0x7FFFFFFF의 최대값을 설정 합니다.|2000|
|scriptFileCacheSize|이 특성 메모리에 캐시할 수 있는 컴파일된 ASP 템플릿의 최대 수를 지정 합니다.<br><br>권장 사항: 가장 자주 요청 ASP 스크립트 응용 프로그램 풀에서 처리의 수 만큼 시로 설정 합니다. 가능한 경우 허용 하는 메모리 제한 만큼 ASP 템플릿을로 설정 합니다.|500|
|scriptEngineCacheMax|메모리에 캐시 하 게 유지할 수 있는 스크립트 엔진의 최대 수를 지정 합니다.<br><br>권장 사항: 가장 자주 요청 ASP 스크립트 응용 프로그램 풀에서 처리의 수 만큼 시로 설정 합니다. 가능한 경우 만큼 스크립트 엔진 메모리 제한을 허용으로 설정 합니다.|250|

**system.webServer/asp/limits**

|attribute|설명|기본값|
|--- |--- |--- |
|processorThreadMax|ASP에서 만들 수 있는 프로세서당 작업자 스레드의 최대 수를 지정 합니다. 현재 설정을 언더의 CPU 리소스 사용량 발생 하거나 요청을 처리 하는 경우 오류를 일으킬 수 있는 부하를 처리 하기에 충분 하지 않을 경우 증가 합니다.|25|

**system.webServer/asp/comPlus**

|attribute|설명|기본값|
|--- |--- |--- |
|executeInMta|로 **True** IIS 콘텐츠 ASP를 제공 되는 동안 오류가 감지 되 면 합니다. 이 발생할 수 있습니다, 예를 들어, 각 사이트는 자체 작업자 프로세스에서 실행 되는 여러 개의 격리 된 사이트를 호스트 하는 경우. 오류는 이벤트 뷰어에서 COM +에서 일반적으로 보고 됩니다. 이 설정은 ASP에서 다중 스레드 아파트 모델을 사용 하도록 설정 합니다.|False|


## <a name="aspnet-concurrency-setting"></a>ASP.NET 동시성 설정

### <a name="aspnet-35"></a>ASP.NET 3.5
기본적으로 ASP.NET 서버에서 안정적인 메모리 소비를 줄이기 위해 요청 동시성을 제한 합니다. 높은 동시성 응용 프로그램 전반적인 성능 향상을 위해 일부 설정을 조정 해야 할 수 있습니다. Aspnet.config 파일에서이 설정을 변경할 수 있습니다.

``` syntax
<system.web>
  <applicationPool maxConcurrentRequestsPerCPU="5000"/>
</system.web>
```

다음 설정을 완전 하 게 리소스를 사용 하 여 시스템에 유용 합니다.

-   **maxConcurrentRequestPerCpu** Default value: 5000

    이 설정은 동시에 시스템에 ASP.NET 요청을 실행 하는 최대 수를 제한 합니다. 기본값은 ASP.NET 응용 프로그램의 메모리 사용량을 줄이는 보수적인 합니다. Long, 동기 I/O 작업을 수행 하는 응용 프로그램을 실행 하는 시스템에서이 한도 늘리는 것이 좋습니다. 이 고, 그렇지 사용자 기본 설정을 사용 하는 경우 높은 부하 상태에서 큐 제한 초과 인해 큐 또는 요청 오류로 인해 대기 시간이 발생할 수 있습니다.

### <a name="aspnet-46"></a>ASP.NET 4.6
ASP.NET 4.7 maxConcurrentRequestPerCpu 설정 외에도 비동기 작업이 크게 의존 하는 응용 프로그램의 성능을 향상 시키는 설정을 제공 합니다. Aspnet.config 파일에서 설정을 변경할 수 있습니다.

``` syntax
<system.web>
  <applicationPool percentCpuLimit="90" percentCpuLimitMinActiveRequestPerCpu="100"/>
</system.web>
```

-   **percentCpuLimit** 기본값: 이러한 시나리오에 큰 부하 (외 하드웨어 기능)을 추가할 경우 90 비동기 요청에 일부 확장성 문제가 있습니다. 문제는 비동기 시나리오에서 할당의 특성 때문입니다. 이러한 상황에서 할당이 발생 비동기 작업이 시작 되 면 작업이 완료 될 때 사용 됩니다. 이때, 구동형 s 엉뚱한 개체 1 또는 2 세대 GC가 이동 되었습니다. 이 경우 부하가 증가 알아보겠습니다 증가 rps (초당) 시점까지 요청 합니다. 이때 전달 하 고 GC에서 소요 된 시간에 문제가 시작 rps dip를 시작, 크기 조정 부정적인 영향을 미칠 있습니다. Cpu 사용량 percentCpuLimit 설정을 초과 하는 경우의 문제를 해결 하려면 요청을 ASP.NET 기본 큐로 보내집니다.
-   **percentCpuLimitMinActiveRequestPerCpu** 기본값: 요청 수 있지만 이들은 드는에 100 CPU 제한 (percentCpuLimit 설정)를 따르지 않습니다. 결과적으로, 들어오는 요청 외에도 빈 수 없으므로 네이티브의 큐에 백업이 발생 하는 몇 가지 CPU를 많이 사용 요청 있을 수 있습니다. 이 problme를 해결 하기 위해 percentCpuLimitMinActiveRequestPerCpu에서 최대로 제한 하기 전에 최소 수의 요청을 처리 되는 확인에 사용할 수 있습니다.

## <a name="worker-process-and-recycling-options"></a>작업자 프로세스 및 옵션을 재활용

IIS 작업자 프로세스를 재활용 하는 것에 대 한 옵션을 구성 하 고 개입할 필요 없이 서비스 또는 컴퓨터를 다시 설정 예 상황 또는 이벤트에 대 한 실용적인 솔루션을 제공할 수 있습니다. 이러한 상황과 이벤트 메모리 누수, 메모리 로드 증가 또는 응답 하지 않거나 유휴 작업자 프로세스를 포함합니다. 일반적인 조건 옵션 재활용 필요할 수 있습니다 및 재활용 해제할 수 있습니다 또는 자주 재활용 하도록 시스템을 구성할 수 있습니다.

특성을 추가 하 여 특정 응용 프로그램에 대 한 프로세스 재활용을 활성화할 수 있습니다 합니다 **재활용 periodicRestart** 요소입니다. 메모리 사용량, 고정된 된 수의 요청 된 고정된 기간 등 몇 가지 이벤트로 재생 이벤트를 트리거할 수 있습니다. 작업자 프로세스 재활용 될 때 큐에 대기 및 실행 중인 요청 종료 되 고 새 프로세스를 동시에 새 요청을 처리 하기 시작 합니다. **재활용 periodicRestart** 요소는 응용 프로그램별는 다음 표에 각 특성 응용 프로그램별 단위로 분할 되는 것을 의미 합니다.

**system.applicationHost/applicationPools/ApplicationPoolDefaults/recycling/periodicRestart**

|attribute|설명|기본값|
|--- |--- |--- |
|메모리|가상 메모리 사용량 (킬로바이트)의 지정 된 한계를 초과 하는 경우 프로세스 재활용을 사용 하도록 설정 합니다. 소규모, 2GB 주소 공간에 있는 32 비트 컴퓨터에 대 한 유용한 설정입니다. 메모리 부족 오류로 인해 실패 한 요청을 방지 하는 것이 도움이 됩니다.|0|
|privateMemory|전용 메모리 할당 (킬로바이트)에서 지정 된 한계를 초과 하는 경우에 프로세스 재활용을 사용 합니다.|0|
|requests|특정 수의 요청을 한 후 프로세스 재활용을 사용 하도록 설정 합니다.|0|
|time|지정 된 시간이 지나면 프로세스 재활용을 사용 하도록 설정 합니다.|29:00:00|


## <a name="dynamic-worker-process-page-out-tuning"></a>동적 작업자 프로세스 페이지 아웃 튜닝

Windows Server 2012 R2부터 IIS (IIS 7부터 사용할 수 있는 terminate의 옵션) 외에도 한 동안 유휴 상태가 된 후 일시 중단 하는 작업자 프로세스를 구성 하는 옵션을 제공 합니다.

유휴 작업자 프로세스 페이지 아웃와 유휴 작업자 프로세스 종료 기능의 주 목적은 것만 중임을 수신 대기 하는 경우에 사이트는 많은 양의 메모리를 사용할 수 있으므로 서버에서 메모리 사용률을 절약 하기 위해. 사이트에서 사용 되는 기술에 따라 (정적 콘텐츠 및 ASP.NET 및 기타 프레임 워크)를 사용 하는 메모리 아무 곳 이나 약 10MB에서 수백 Mb, 되며 즉 서버 가장 효율적인 설정을 파악 하는 여러 사이트를 사용 하 여 구성 된 사이트에 크게 성능을 향상 시킬 수의 활성 및 일시 중단 된 사이트입니다.

세부 정보를 살펴보기 전에 하기만 하면 사이트를 일시 중단 하거나 종료 하지 않습니다를 설정 하려면 가장 하는 것을 메모리 제약 조건이 없는 경우 염두에서 야 합니다. 결국 thereâ s 종료 자가 작은 값이 경우 처리할 컴퓨터에서 유일한 스냅숏이어야 합니다.

**참고**   사이트에는 메모리 누수를 사용 하 여 코드와 같은 불안정 한 코드를 실행 하거나 그렇지 않으면 불안정 유휴 상태에서 종료 하는 사이트를 설정 수 쉬우며 대체 코드 버그를 수정 하는 경우. 이것은 것이 좋습니다, 있지만 분석할 수 있습니다 더 영구적인 솔루션을 작동 중인 동안 정리 메커니즘으로이 기능을 사용 하 여.\]

Â 

고려해 야 할 요소에 있으면는 사이트에서 많은 메모리를 사용 하는 경우 컴퓨터의 디스크에 작업자 프로세스에 의해 사용 되는 데이터를 작성 하기 때문에 일시 중단 프로세스 자체는 감소 합니다. 작업자 프로세스 메모리의 큰 덩어리를 사용 하는 경우에 다음 일시 중단 다시 시작 되도록 기다리지 않아도 비용에 비해 수 있습니다.

작업자 프로세스가 일시 중단 기능 최선을 다, 각 응용 프로그램 풀에서 사이트를 검토 하 고 일시 중단 되어야 하는는 종료할지 무기한 활성 야 결정 해야 합니다. 각 사이트와 각 작업에 대 한 이상적인 제한 시간을 파악 해야 합니다.

이상적으로 일시 중단 또는 종료에 대 한 구성 하는 사이트는 매일 방문자에 게 있는 하지만 항상 활성 상태로 유지 하는 포함 되어 맵이 충분 하지 않습니다. 이 일반적으로 하루 약 20 고유 방문자를 사용 하 여 사이트 미만입니다. 사이트의 로그 파일을 사용 하 여 트래픽 패턴을 분석 하 고 평균 일일 트래픽을 계산할 수 있습니다.

특정 사용자가 사이트에 연결 되 면 일반적으로 머무르는에 적어도 한 동안 추가 요청을 수행 하 고 있으므로 매일 요청을 계산 나타내지 않을 수 있습니다 정확 하 게 실제 트래픽 패턴 염두에 두어야 합니다. 읽을 수 있는 보다 정확 하 게, 요청 사이의 평균 시간을 계산 하려면 Microsoft Excel 같은 도구를을 사용할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

||요청 URL|요청 시간|델타|
|--- |--- |--- |--- |
|1|/SourceSilverLight/Geosource.web/grosource.html|10:01||
|2|/SourceSilverLight/Geosource.web/sliverlight.js|10:10|0:09|
|3|/SourceSilverLight/Geosource.web/clientbin/geo/1.aspx|10:11|0:01|
|4|/lClientAccessPolicy.xml|10:12|0:01|
|5|/ SourceSilverLight/GeosourcewebService/Service.asmx|10:23|0:11|
|6|/ SourceSilverLight/Geosource.web/GeoSearchServer...¦ 합니다.|11:50|1:27|
|7|/rest/Services/CachedServices/Silverlight_load_la...¦|12:50|1:00|
|8|/rest/Services/CachedServices/Silverlight_basemap...¦.|12:51|0:01|
|9|/ rest/Services/DynamicService/Silverlight_basemap... 해 보아야 합니다.|12:59|0:08|
|10|/rest/Services/CachedServices/Ortho_2004_cache.as...|13:40|0:41|
|11|/rest/Services/CachedServices/Ortho_2005_cache.js|13:40|0:00|
|12|/rest/Services/CachedServices/OrthoBaseEngine.aspx|13:41|0:01|

어려운 부분은 그러나 파악 하는 것이 좋습니다에 적용할 설정입니다. 경우에 사이트, 사용자에 게 다양 한 요청을 가져옵니다 및 위의 표에서 4 시간 동안에는 총 4 개의 고유 세션 발생 했음을 보여 줍니다. 응용 프로그램 풀의 작업자 프로세스가 일시 중단에 대 한 기본 설정으로 사이트 스핀업 주기에서 발생 하는 이러한 사용자 각각의 의미는 20 분의 기본 제한 시간 후 사이트를 종료 됩니다. 이렇게 하면 작업자 프로세스가 일시 중단에 대 한 적합 한 후보가 이므로 대부분의 시간에 대해 사이트 유휴 상태 이므로 리소스를 절약 하 고 사이트에 거의 즉시 연결할 수는 일시 중단 합니다.

이 대 한 최종 및 매우 중요 한 정보를 디스크 성능이이 기능에 대 한 중요 한 된다는 것입니다. 사용 되므로 일시 중단 및 절전 모드 해제 프로세스를 작성 하 고 많은 양의 하드 드라이브에 데이터를 읽고,이 대 한 고속 디스크를 사용 하는 것이 좋습니다. 반도체 드라이브 (Ssd) 이상적이 고이 위해 권장 되며 Windows 페이지 파일에 저장 되도록 해야 (운영 체제 자체는 SSD에 설치 되어 있지 않으면, 페이지 파일을 이동할 대상 운영 체제를 구성 함).

사용할지 SSD 여부, 좋습니다 페이지 파일의 크기를 수정 합니다. 파일 크기를 조정 하지 않고 페이지 아웃 데이터 쓰기를 수용 하기 위해. 페이지 파일 크기를 조정 발생할 수 있습니다 Windows 기본적으로 구성 되었기 때문에 운영 체제 페이지 파일에 데이터를 저장 해야 하는 경우에 따라 크기가 자동으로 조정 해야 합니다. 고정으로 크기를 설정 하 여 크기 조정을 방지 수 있으며 훨씬 성능을 향상 시킬 수 있습니다.

이상적인 크기를 계산 해야 미리 고정된 페이지 파일 크기를 구성 하려면 얼마나 많은 사이트에 따라 다릅니다은 수 일시 중단 및 메모리 양을 사용 합니다. 평균 200MB를 활성 작업자 프로세스에 대 한 및 500 개의 사이트를 일시 중단 되어야 하는 서버에 있는 경우 페이지 파일 이상 이어야 합니다 (200 \* 500) 페이지 파일 (이 예제의 하므로 기본 + 100 GB)의 기본 크기 (mb)입니다.

**참고** 하므로 여기서는 모든 사이트는 일시 중단 된 경우 메모리 사용량은 약 3GB 약 6MB 각각 사용 하는 것 사이트는 일시 중지 하면 됩니다. 실제로 통해 다시 모든 동시에 일시 중단 하도록 하려고 하지 않을 수도 있습니다.

 
## <a name="transport-layer-security-tuning-parameters"></a>전송 계층 보안 매개 변수를 튜닝 합니다.

보안 TLS (전송 계층)를 사용 하 여 추가 CPU 비용을 부과합니다. TLS의 가장 비용이 많이 드는 구성 요소는 세션 설정을 설정 하 여 전체 핸드셰이크를 사용 하므로 비용. 다시 연결, 암호화 및 암호 해독도 비용을 추가합니다. TLS 성능 향상을 위해 다음을 수행 합니다.

-   TLS 세션에 대 한 HTTP 연결 유지를 사용 합니다. 이 세션 설정 비용을 제거 합니다.

-   세션을 다시 사용할 경우 적절 한, 비-유지 트래픽이 있는 특히 합니다.

-   선택적으로 페이지 또는 전체 사이트를 대신 해야 하는 사이트의 일부에만 암호화를 적용 합니다.

**참고**
-   자세한 보안을 제공 하는 큰 키 하지만 CPU 시간이 더 많이 사용할 수도 있습니다.

-   구성 요소를 모두 암호화할 필요가 없을 수도 있습니다. 그러나 일반 HTTP 및 HTTPS 혼합 페이지의 일부 콘텐츠는 보안 경고 팝업 될 수 있습니다.

 
## <a name="internet-server-application-programming-interface-isapi"></a>인터넷 서버 응용 프로그래밍 인터페이스 (ISAPI)

ISAPI 응용 프로그램에 대 한 특별 한 튜닝 매개 변수 없이 필요 합니다. 개인 ISAPI 확장을 작성 하는 경우는 성능 및 리소스 사용에 대 한 기록 되어 있는지 있는지 확인 해야 합니다.

## <a name="managed-code-tuning-guidelines"></a>관리 코드 조정 지침

IIS 10.0에서 통합된 파이프라인 모델을 통해 높은 수준의 유연성과 확장성을 수 있습니다. 네이티브 또는 관리 코드에서 구현 되는 사용자 지정 모듈을 파이프라인에 삽입할 수 또는 기존 모듈을 바꿀 수 있습니다. 편의성과 단순성을 제공 하는이 확장성 모델을 있지만 전역 이벤트에 연결 하 여 새 관리 되는 모듈을 삽입 하기 전에 주의 해야 합니다. 관리 되는 코드 추가 관리 되는 전역 모듈 의미 정적 파일 요청을 비롯 한 모든 요청에 액세스 해야 하는 중입니다. 사용자 지정 모듈은 가비지 수집 등의 이벤트에 취약 합니다. 또한 사용자 지정 모듈 네이티브 및 관리 코드 간의 마샬링 데이터로 인해 상당한 CPU 비용을 추가합니다. 가능한 경우 사전 조건 관리 되는 모듈에 대 한 managedHandler로 설정 해야 합니다.

콜드 시작 성능 향상을 가져오려면 응용 프로그램 준비 ASP.NET 웹 사이트 또는 활용 하 여 IIS 응용 프로그램 초기화 기능을 미리 컴파일하는 있는지를 확인 합니다.

세션 상태가 필요 하지 않은 경우 해제 하는 각 페이지에 있는지 확인 합니다.

많은 I/O 바인딩된 작업 없으면, 훨씬 더 나은 확장성을 제공 됩니다 하는 관련 Api의 비동기 버전을 사용 하려고 합니다.

또한 출력 캐시를 올바르게 사용 웹 사이트의 성능을 높일 수도 됩니다.

격리 모드 (사이트당 하나의 응용 프로그램 풀)에서 ASP.NET 스크립트를 포함 하는 여러 호스트를 실행 하면 메모리 사용량을 모니터링 합니다. 서버 응용 프로그램 풀을 동시에 실행에 대 한 예상된 개수를 충분 한 RAM에 있는지 확인 합니다. 여러 응용 프로그램 도메인을 사용 하 여 여러 개의 격리 된 프로세스를 대신 하는 것이 좋습니다.


## <a name="other-issues-that-affect-iis-performance"></a>IIS 성능에 영향을 주는 기타 문제

다음과 같은 문제가 IIS 성능에 영향을 줄 수 있습니다.

-   캐시에서 인식 되지 않는 필터 설치

    HTTP 캐시 인식 되지 않는 필터를 설치 하면 성능이 저하는 완전히 캐싱을 사용 하지 않으려면 IIS입니다. IISÂ 6.0 이전에 작성 된 ISAPI 필터는이 동작이 발생할 수 있습니다.

-   인터페이스 CGI (common Gateway) 요청

    성능상의 이유로 IIS를 사용 하 여 요청을 처리 하는 CGI 응용 프로그램 사용 권장 되지 않습니다. 자주 만들고 CGI 프로세스를 삭제 하면 상당한 오버 헤드가 포함 됩니다. 더 나은 대안 ISAPI 응용 프로그램 스크립트 및 ASP 또는 ASP.NET 스크립트 FastCGI를 사용 하 여 포함 합니다. 격리는 이러한 각 옵션에 대해 사용할 수 있습니다.

# <a name="see-also"></a>참조
- [웹 서버 성능 조정](index.md) 
- [HTTP 1.1/2 튜닝](http-performance.md)
