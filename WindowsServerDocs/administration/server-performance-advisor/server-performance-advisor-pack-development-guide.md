---
title: 서버 성능 Advisor 팩 개발 가이드
description: 서버 성능 Advisor 팩 개발 가이드
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c647e8a335aac924067d92dcb41ab4d17e0cceef
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884864"
---
# <a name="server-performance-advisor-pack-development-guide"></a>서버 성능 Advisor 팩 개발 가이드

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 8, Windows 10

이 개발 가이드 Microsoft 서버 성능 Advisor (SPA)에 대 한 개발자와 관리자 팩을 개발 하는 시스템 관리자 서버 성능 분석을 하기 위한 지침을 제공 합니다.

성능 로그 및 경고 PLA (), 성능 카운터, 레지스트리 설정, Windows Management Instrumentation (WMI), 이벤트 추적에 대 한 ETW (Windows), 및 TRANSACT-SQL (T-SQL)에 잘 알고 있다면 가정 합니다.

SPA를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [서버 성능 관리자 사용자 가이드](server-performance-advisor-users-guide.md)합니다.

## <a name="spa-advisor-pack-overview"></a>SPA Advisor 팩 개요


Advisor 팩은 특정 서버 역할의 경우 일반적으로 디자인 하 고 다음을 정의 합니다.

* 데이터를 통해 Windows Management Instrumentation (WMI), 성능 카운터, 레지스트리 설정, 파일 및 이벤트 추적에 대 한 ETW (Windows)를 포함 하 여 PLA 수집

* 경고 및 권장 사항 보여 주는 규칙

* 데이터가 (수집 된 원시 데이터, 집계 된 데이터 또는 상위 10 개 목록)에 표시 됩니다

* 통계는 시간이 지남에 따라 변경 되는 값을 보려면

* 원하는 현재의 추세가 반영 될 수 있는 통계 값

Advisor 팩에는 다음 요소가 포함 됩니다.

* **XML 메타 데이터** (ProvisionMetadata.xml)

    * [성능 로그 및 경고 (PLA)](https://msdn.microsoft.com/library/windows/desktop/aa372635.aspx) 데이터 수집기 집합

    * 보고서 레이아웃

* **SQL 스크립트**

    * 기본 저장된 프로시저

    * 저장된 프로시저 및 사용자 정의 함수 같은 SQL 개체

* **ETW 스키마 파일** 선택 사항입니다 (Schema.man)

### <a name="advisor-pack-workflow"></a>Advisor 팩 워크플로

![advisor 팩 워크플로](../media/server-performance-advisor/spa-dev-guide-workflow.png)

이 순서도에서 녹색 원 advisor 팩을 나타냅니다. 다른 모든 원 SPA 프레임 워크 중 실행 되는 단계를 나타냅니다. SPA는 데이터를 수집, 데이터베이스로 데이터를 가져오고, 실행 환경 초기화 및 SQL 스크립트를 실행 하는 advisor 팩을 사용 합니다.

### <a name="collect-data"></a>데이터 수집

Advisor 팩은 큐에 대기 되는 특정 서버용 SPA를 사용 하 여 데이터 수집 모듈 advisor 팩에서 데이터 수집기 집합 XML을 쿼리하고 대상 서버에서 데이터를 수집 합니다. 원시 데이터는 사용자가 지정한 파일 공유에 저장 됩니다. SPA를 실행 하는 사용자가 지정 하는 기간을 초과할 때까지 데이터 수집 중지 되지 않습니다.

### <a name="import-data-into-the-database"></a>데이터베이스에 데이터 가져오기

데이터 컬렉션이 완료 되 면 각 데이터 형식에는 SQL Server 데이터베이스에 해당 하는 테이블으로 가져옵니다. 예를 들어 레지스트리 설정을 라는 테이블에 가져올 \#설정값입니다.

파일을 가져오는 ETW는 ETW 스키마 파일 디코딩.etl 파일에 대 한 필요 합니다. ETW 스키마 파일은 XML 파일입니다. Windows에 포함 되어 있는 tracerpt.exe를 사용 하 여 생성할 수 있습니다. ETW 스키마 파일은만 advisor 팩 필요한 ETW 데이터를 가져올 때 필요 합니다.

### <a name="switch-to-low-user-rights"></a>낮은 사용자 권한으로 전환

SPA 프레임 워크는 필요한 보안 액세스 수준을 최소화 하기 위해 권한을 자동으로 조정 합니다. 없기 때문에 advisor 팩 개발 하거나 수정할 수 있습니다 누구나, advisor 팩 변조 된 SQL 스크립트를 포함 하도록 합니다. 보안 위험을 줄이려면 낮은 사용자 권한을 가진 관리자 팩에 대 한 SQL 스크립트를 실행 해야 합니다. 임시 테이블 및 저장 프로시저로 노출 SPA Api 같은 제한 된 데이터베이스 개체를 액세스할 수만 있습니다. Advisor 팩에는 SQL 스크립트를 호출할 수 SPA 프레임 워크와 상호 작용 하는 프로시저를 저장 합니다.

### <a name="initialize-execution-environment"></a>실행 환경 초기화

Advisor 팩에는 다양 한 유형의 알림을, 권장 사항, 팩트 테이블, 통계 및 통계에 대 한 차트와 같은 출력을 생성할 수 있습니다. SQL 스크립트는 수집 된 데이터에 대 한 특정 계산을 수행합니다. 생성 된 결과 SPA 공용 Api 통해 임시 테이블에 저장 됩니다. 초기화 단계에서 이러한 임시 테이블 및 기타 시스템 리소스를 프로 비전 해야 합니다.

### <a name="run-sql-scripts"></a>SQL 스크립트를 실행 합니다.

Advisor 팩 개발자에 의해 이름이 지정 되는 주 저장된 프로시저를 있습니다. SPA 프레임 워크는 계산을 시작 하려면이 저장된 프로시저를 호출 합니다. 저장된 프로시저가 수집 된 데이터를 사용 하 고 SPA 프레임 워크를 최종 결과 통신 합니다.

### <a name="switch-to-administrative-rights"></a>관리 권한으로 전환

보고서를 생성 하려면 관리자 권한이 필요 합니다. 보고서를 생성 하 여 SPA 완벽 하 게 제어 됩니다. 이기 변조 될 가능성이 적습니다.

### <a name="generate-a-report"></a>보고서 생성

기본 저장된 프로시저는 advisor 팩에 대 한 완료 되기 전에 알림 및 통계와 같은 계산 된 모든 결과 유지 되지 않습니다. 이 단계에서는 SPA 프레임 워크 임시 테이블에서 최종 결과 특정 형식의 테이블에 전송합니다. 이 단계를 완료 한 후에 SPA 콘솔을 사용 하 여 보고서를 볼 수 있습니다.

## <a name="authoring-an-advisor-pack"></a>Advisor 팩 제작


### <a name="quick-guidelines"></a>빠른 지침

다음 순서도 모든 기능을 갖춘 advisor 팩을 개발 하는 단계를 설명 합니다. 이 섹션에는 각 단계를 더 잘 설명 하는 단계별 예제도 포함 되어 있습니다.

![advisor 팩 개발 프로세스](../media/server-performance-advisor/spa-dev-guide-dev-flowchart.png)

Advisor 팩은 일반적으로 다음과 같은 방식으로 구성 합니다.

Advisor 팩

ProvisionMetadata.xml

스크립트

main.sql

func.sql

Schema.man

모든 advisor 팩 ProvisionMetadata.xml 파일이 있어야 합니다. 기본 관리자 팩 정보, 데이터를 수집, 알림, 규칙 및 보고서를 저장 하 고 표시 해야 하는 방법을 정의 합니다. SPA 프레임 워크는이 정보를 사용 하 여를 임시 테이블을 생성 한 다음 사용자가 액세스할 수 있는 테이블에 임시 테이블의 결과 전송 합니다.

SQL 스크립트 이라는 하위 폴더에 저장 해야 모든 보고 **스크립트**합니다. 유지 관리를 위해 서로 다른 SQL Server 파일에서 다른 데이터베이스 개체를 저장 하는 것이 좋습니다. 주 진입점와 저장된 프로시저를 적어도 하나 있어야 합니다.

> [!NOTE]
> Advisor 팩 ETW 추적을 수집 하지 않는 한 schema.man 파일이 필요 하지 않습니다. 이 스키마 파일은 ETW 이벤트의 스키마를 설명 하 고 ETW 이벤트가 디코딩되지 사용 됩니다.

### <a name="defining-basic-information"></a>기본 정보를 정의합니다.

이 섹션에는 ProvisionMetadata.xml 및 특성을 포함 하는 advisor 팩에 구성 하는 기본 요소 중 일부를 설명 합니다.

다음은 ProvisionMetadata.xml 파일에 대 한 헤더의 예입니다.

``` syntax
<advisorPack
xmlns="http://microsoft.com/schemas/ServerPerformanceAdvisor/ap/2010"
name="Microsoft.ServerPerformanceAdvisor.CoreOS.V2"
displayName="Microsoft CoreOS Advisor Pack V2"
description="Microsoft CoreOS Advisor Pack"
author="Microsoft"
version="1.0"
frameworkversion="3.0"
minOSversion="6.0"
reportScript="ReportScript">
</advisorPack>
```

### <a name="advisor-pack-version"></a>Advisor 팩 버전

특성 이름: **버전**

Advisor 팩 개발자는 advisor 팩에 대 한 주 버전과 부 버전을 정의할 수 있습니다.

* 주 버전에는 일반적으로 한 주요 개선 기능이 포함 됩니다. 이전 버전에서 생성 되는 결과 새 호환 수 있습니다. Advisor 팩 이름에는 주 버전을 포함 하는 것이 좋습니다.

* 데이터 비 호환성 문제가 없는 사소한 변경만 있으면 SPA 부 버전 업그레이드를 수 있습니다.

버전 관리에 대 한 자세한 내용은 참조 하세요. [고급 항목](#bkmk-advancedtopics)합니다.

### <a name="script-entry-point"></a>따라서 스크립트 진입점

특성 이름: **reportScript**

SPA 프레임 워크 기본 저장 된 프로시저 이름에 대 한 스크립트 진입점에서 찾아 보안 방식으로 실행 합니다.

### <a name="other-attributes"></a>다른 특성

다음은 advisor 팩을 식별 하는 데 사용할 수 있는 몇 가지 다른 특성입니다.

* 표시 이름: **displayName**

* 설명: **설명**

* 작성자: **작성자**

* 프레임 워크 버전: **frameworkversion** (기본값: 3.0)

* 최소 운영 체제 버전: **minOSversion** (향후 확장성을 위해 예약 됩니다).

* 이벤트 알림이 손실: **showEventLostWarning**

### <a href="" id="bkmk-definedatacollector"></a>데이터 수집기 집합을 정의합니다.

데이터 수집기 집합 SPA 프레임 워크를 대상 서버에서 수집 해야 하는 성능 데이터를 정의 합니다. ETW 고 대상 서버에서 파일, 레지스트리 설정, WMI, 성능 카운터를 지원 합니다.

``` syntax
<advisorPack>
<dataSourceDefinition xmlns="http://microsoft.com/schemas/ServerPerformanceAdvisor/dc/2010">
 <dataCollectorSet duration="10">
<registryKeys>
 ?<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\\</registryKey>
</registryKeys>
<managementpaths>
 ?<path>Root\Cimv2:select * FROM Win32_DiskDrive</path>
</managementpaths>
<performanceCounters interval="2">
 ?<performanceCounter>\PhysicalDisk(*)\Avg. Disk sec/Transfer</performanceCounter>
</performanceCounters>
<files>
 ?<path>%windir%\System32\inetsrv\config\applicationHost.config</path>
</files>
<providers>
 ?<provider session="NT Kernel Logger" guid="{9E814AAD-3204-11D2-9A82-006008A86939}" keywordsany="06010201" keywordsAll="00000000" level="00000000" />
</providers>
 </dataCollectorSet>
</dataSourceDefinition>
</advisorPack>
```

**기간** 특성 **&lt;dataCollectorSet /&gt;** 이전 예제에서 데이터 수집 (시간 단위 시간은 초)의 기간을 정의 합니다. **기간** 필수 특성입니다. 이 설정은 성능 카운터 및 ETW에서 사용 되는 컬렉션 기간을 제어 합니다.

### <a name="collect-registry-data"></a>레지스트리 데이터를 수집 합니다.

다음 레지스트리 하이브를 레지스트리 데이터를 수집할 수 있습니다.

* HKEY\_클래스\_루트

* HKEY\_현재\_구성

* HKEY\_CURrenT\_USER

* HKEY\_로컬\_컴퓨터

* HKEY\_사용자

레지스트리 설정을 수집 하려면 값 이름에 전체 경로 지정 합니다. HKEY\_LOCAL\_MACHINE\\MyKey\\MyValue

레지스트리 키 설정을 모두를 수집 하려면 레지스트리 키의 전체 경로 지정 합니다. HKEY\_LOCAL\_MACHINE\\MyKey\\

레지스트리 키 및 해당 하위 키 (PLA 재귀적으로 레지스트리 데이터를 수집 하는 데 사용)에서 모든 값을 수집 하려면 마지막 경로 구분 기호에 대 한 두 개의 백슬래시를 사용 합니다. HKEY\_LOCAL\_MACHINE\\MyKey\\\\

원격 컴퓨터에서 레지스트리 정보를 수집 하려면 레지스트리 경로의 시작 부분에 있는 컴퓨터 이름을 포함 합니다. HKEY\_LOCAL\_MACHINE\\MyKey\\MyValue

예를 들어 다음과 같이 표시 되는 레지스트리 키를 할 수 있습니다.

``` syntax
Windows registry editor version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes]
"activePowerScheme"="db310065-829b-4671-9647-2261c00e86ef"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\db310065-829b-4671-9647-2261c00e86ef]
"Description"=
 FriendlyName = Power Source Optimized 

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\db310065-829b-4671-9647-2261c00e86ef \0012ee47-9041-4b5d-9b77-535fba8b1442\6738e2c4-e8a5-4a42-b16a-e040e769756e
"ACSettingIndex"=dword:000000b4
"DCSettingIndex"=dword:0000001e
```

예 1: 활성 PowerSchemes만 및 해당 값을 반환 합니다.

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes</registryKey>
```

예 2: 이 경로 아래의 모든 키 값 쌍을 반환합니다.

> [!NOTE]
> PLA는 사용자 자격 증명으로 실행 됩니다. 일부 레지스트리 키에는 관리자 자격 증명이 필요 합니다. 열거형에는 하위 키에 액세스 하는 데 실패할 경우 중지 합니다.

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\\</registryKey>
```

라는 임시 테이블에 모든 수집 된 데이터를 가져올  **\#설정값** SQL 보고서 하기 전에 스크립트가 실행 됩니다. 다음 표에서 예를 들어 2 결과 보여 줍니다.

키 이름 | KeytypeId | 값
------ | ----- | -------
HKEY_LOCAL_MACHINE...\PowerSchemes | 1 | db310065-829b-4671-9647-2261c00e86ef
\db310065-829b-4671-9647-2261c00e86ef\Description | 2 | |
\db310065-829b-4671-9647-2261c00e86ef\FriendlyName | 2 | 전원 최적화
...\6738e2c4-e8a5-4a42-b16a-e040e769756e\ACSettingIndex | 4 | 180
...\6738e2c4-e8a5-4a42-b16a-e040e769756e\DCSettingIndex | 4 | 30

에 대 한 스키마를 **#registryKeys** a를 테이블은 다음과 같습니다.

열 이름 | SQL 데이터 형식 | 설명
-------- | -------- | --------
키 이름 | NULL이 아닌 Nvarchar(300) | 레지스트리 키의 전체 경로 이름
KeytypeId | NULL이 아닌 Smallint | 내부 유형 Id
값 | Nvarchar (4000) NULL이 아님 | 모든 값

합니다 **KeytypeID** 열 다음 유형 중 하나일 수 있습니다.
ID | 형식
--- | ---
1 | 문자열
2 | expandString
3 | 이진
4 | Dword
5 | DWordBigEndian
6 | 링크
7 | MultipleString
8 | Resourcelist
9 | FullResourceDescriptor
10 | ResourceRequirementslist
11 | Qword

### <a name="collect-wmi"></a>WMI를 수집 합니다.

WMI 쿼리를 추가할 수 있습니다. WMI 쿼리를 작성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [WQL (WMI에 대 한 SQL)](https://msdn.microsoft.com/library/windows/desktop/aa394606.aspx)합니다. 다음 예제에서는 페이지 파일 위치를 쿼리합니다.

``` syntax
<path>Root\Cimv2:select * FROM Win32_PageFileUsage</path>
```

위의 예에서 쿼리는 하나의 레코드를 반환합니다.

캡션 | 이름 | PeakUsage
----- | ----- | -----
C:\pagefile.sys | C:\pagefile.sys | 215

WMI를 반환 하므로 서로 다른 열이 있는 테이블을 데이터베이스에 수집 된 데이터를 가져오면 SPA 데이터 정규화를 수행 하 고 다음 테이블에 추가 됩니다.

**\#WMIObjects 테이블**

SequenceID | Namespace | 응용 프로그램 이름 | Relativepath | WmiqueryID
----- | ----- | ----- | ----- | -----
10 | Root\Cimv2 | Win32_PageFileUsage | Win32_PageFileUsage.Name=<br>C:\\pagefile.sys | 1

**\#WmiObjectsProperties 테이블**

ID | 쿼리
--- | ---
1 | Root\Cimv2:select * FROM Win32_PageFileUsage

**\#WmiQueries 테이블**

ID | 쿼리
--- | ---
1 | Root\Cimv2:select * FROM Win32_PageFileUsage

**\#WmiObjects 테이블 스키마**

열 이름 | SQL 데이터 형식 | 설명
--- | --- | ---
SequenceId | NULL이 아닌 Int | 행 및 해당 속성을 상호 연결
Namespace | NULL이 아닌 nvarchar (200) | WMI 네임 스페이스
응용 프로그램 이름 | NULL이 아닌 nvarchar (200) | WMI 클래스 이름
Relativepath | Nvarchar (500) NULL이 아님 | WMI 상대 경로
WmiqueryId | NULL이 아닌 Int | #WmiQueries의 키를 상호 연결

**\#WmiObjectProperties 테이블 스키마**

열 이름 | SQL 데이터 형식 | 설명
--- | --- | ---
SequenceId | NULL이 아닌 Int | 행 및 해당 속성을 상호 연결
이름 | Nvarchar (1000) NULL이 아님 | 속성 이름
값 | Nvarchar (4000) NULL | 현재 속성의 값

**\#WmiQueries 테이블 스키마**

열 이름 | SQL 데이터 형식 | 설명
--- | --- | ---
Id | NULL이 아닌 Int | > 고유 쿼리 ID
쿼리 | Nvarchar (4000) NULL이 아님 | 프로 비전 메타 데이터에 원래 쿼리 문자열

### <a name="collect-performance-counters"></a>성능 카운터를 수집 합니다.

S 성능 카운터를 수집 하는 방법의 예는 다음과 같습니다.

``` syntax
<performanceCounters interval="1">
  <performanceCounter>\PhysicalDisk(*)\Avg. Disk sec/Transfer</performanceCounter>
</performanceCounters>
```

**간격** 특성은 모든 성능 카운터에 대 한 필요한 전역 설정입니다. 성능 데이터 수집 간격 (시간 단위 시간은 초)을 정의 합니다.

이전 예제에서는 카운터 \\실제 디스크 (\*)\\avg. Disk sec/Transfer는 매 초 마다 쿼리할 수 있습니다.

두 인스턴스가 있을 수 있습니다. **\_총** 고 **0 c: D:**, 출력은 다음과 같이 수 있습니다.

타임 스탬프 | CategoryName | CounterName | _Total 인스턴스 값 | 인스턴스 값의 0 c: D:
---- | ---- | ---- | ---- | ----
13:45:52.630 | PhysicalDisk | Avg. Disk sec/Transfer | 0.00100008362473995 |0.00100008362473995
13:45:53.629 | PhysicalDisk | Avg. Disk sec/Transfer | 0.00280023414927187 | 0.00280023414927187
13:45:54.627 | PhysicalDisk | Avg. Disk sec/Transfer | 0.00385999853230048 | 0.00385999853230048
13:45:55.626 | PhysicalDisk | Avg. Disk sec/Transfer | 0.000933297607934224 | 0.000933297607934224

데이터베이스에 데이터를 가져오려면 데이터 라는 테이블에 정규화 됩니다 **\#PerformanceCounters**합니다.

CategoryDisplayName | InstanceName | CounterdisplayName | 값
---- | ---- | ---- | ----
PhysicalDisk | _Total | Avg. Disk sec/Transfer | 0.00100008362473995
PhysicalDisk | 0 C: D: | Avg. Disk sec/Transfer | 0.00100008362473995
PhysicalDisk | _Total | Avg. Disk sec/Transfer | 0.00280023414927187
PhysicalDisk | 0 C: D: | Avg. Disk sec/Transfer | 0.00280023414927187
PhysicalDisk | _Total | Avg. Disk sec/Transfer | 0.00385999853230048
PhysicalDisk | 0 C: D: | Avg. Disk sec/Transfer | 0.00385999853230048
PhysicalDisk | _Total | Avg. Disk sec/Transfer | 0.000933297607934224
PhysicalDisk | 0 C: D: | Avg. Disk sec/Transfer | 0.000933297607934224

**참고** 는 지역화 된 이름와 같은 **CategoryDisplayName** 및 **CounterdisplayName**, 대상 서버에서 사용 되는 표시 언어에 따라 달라 집니다. 언어 중립 advisor 팩을 만들려는 경우 해당 필드를 사용 하지 마십시오.

**\#PerformanceCounters** 테이블 스키마

열 이름 | SQL 데이터 형식 | 설명
---- | ---- | ---- | ----
타임 스탬프 | datetime2(3) NOT NULL | UNC에서 수집 된 날짜 시간
CategoryName | NULL이 아닌 nvarchar (200) | 범주 이름
CategoryDisplayName | NULL이 아닌 nvarchar (200) | 지역화 된 범주 이름
InstanceName | NULL nvarchar (200) | 인스턴스 이름
CounterName | NULL이 아닌 nvarchar (200) | 카운터 이름
CounterdisplayName | NULL이 아닌 nvarchar (200) | 지역화 된 카운터 이름
값 | NULL이 아닌 부동 소수점 | 수집 된 값

### <a name="collect-files"></a>파일 수집

절대 또는 상대 경로 수 있습니다. 파일 이름이 와일드 카드 문자를 포함할 수 있습니다 (\*) 및 물음표 (?). 예를 들어 임시 폴더에 있는 모든 파일을 수집 하도록 지정할 수 있습니다: c:\\temp\\\*합니다. 와일드 카드 문자는 지정된 된 폴더의 파일에 적용 됩니다.

또한 지정된 된 폴더의 하위 폴더에서 파일을 수집 하려는 경우 예를 들어 c: 마지막 폴더 구분에 대 한 두 개의 백슬래시를 사용\\temp\\\\\*합니다.

다음 쿼리 하는 예제는 **applicationHost.config** 파일:

``` syntax
<path>%windir%\System32\inetsrv\config\applicationHost.config</path>
```

라는 테이블에 결과 찾을 수 **\#파일**, 예:

querypath | fullpath | Parentpath | FileName | 콘텐츠
----- | ----- | ----- | ----- | -----
%windir%\.... \applicationHost.config |C:\Windows<br>\...\applicationHost.config | C:\Windows<br>\...\config | applicationHost.confi | 0x3C3F78

**\#파일 테이블 스키마**

열 이름 | SQL 데이터 형식 | 설명
---- | ---- | ----
querypath | NULL이 아닌 Nvarchar(300) | 원래 쿼리 문
fullpath | NULL이 아닌 Nvarchar(300) | 절대 파일 경로 및 파일 이름
Parentpath | NULL이 아닌 Nvarchar(300) | 파일 경로
FileName | NULL이 아닌 Nvarchar(300) |  파일 이름 
콘텐츠 | Varbinary (max) NULL | 이진에서 파일 콘텐츠

### <a name="defining-rules"></a>규칙 정의

충분 한 데이터를 수집한 후 PLA 대상 서버에서 사용 하 여, advisor 팩 유효성 검사를 위해이 데이터를 사용 하 고 시스템 관리자에 게 빠른 요약을 표시할 수 있습니다.

규칙의 성능을 서버에 대 한 간략 한 개요를 제공합니다. 이러한 문제를 강조 표시 하 고 권장 사항을 제공 합니다. Advisor 팩에 대 한 유효성을 검사 하려고 하는 모든 규칙을 나열할 수 있습니다. 예를 들어, 핵심 운영 체제 관리자 팩을 개발 하려는 경우 가능한 규칙 포함할 수 있습니다.

* CPU 전원 모드 여부는 절전

* 가상화 된 환경에서 인지 여부

* 디스크 I/O 압력 있는지 여부

규칙에는 다음과 같은 요소가 있습니다.

* 종속 임계값 (규칙의 구성 가능한 일부)

* 규칙 정의 (경고 및 권장 사항)

S 간단한 규칙의 예는 다음과 같습니다.

``` syntax
<advisorPack>
   
  <reportDefinition>
    <thresholds>
      <threshold  />
    </thresholds>
    <rules>
      <rule  />
      </rule>
    </rules>
  </reportDefinition>
</advisorPack>
```

### <a name="threshold"></a>임계값

임계값은 시스템 관리자는 좋은 일 이나 잘못 된 상태 규칙을 표시 해야 결정할 수 있도록 하는 구성 가능한 요소입니다. 다음 예제에서는 사용 가능한 공간이 10GB 보다 작음 때 시스템 드라이브 및 경고에서 사용 가능한 공간을 검색 하는 규칙을 보여 줍니다.

``` syntax
<threshold name="freediskSize" caption="Free Disk Size (GB)" description="Free Disk Size  value="10" />
```

그러나이 경우 시스템 관리자가 더 작은 하드 드라이브입니다. 5GB의 여유 공간을 양호한 상태로 수 및 경고가 표시 되도록 않으려면 말하곤 합니다. Advisor 팩을 개발 하는 방법을 알 필요 없이 5 SPA 콘솔을 통해 10에서 기본값을 업데이트할 수 그.

Advisor 팩을 수정 하지 않고도 신속 하 게 값을 변경 하는 시스템 관리자를 사용 하면 임계값을 소개 합니다.

제외 하 고 특성 모든 예제에서는 **설명** 필요 합니다. 에 대 한 숫자를 사용할 수 **값**합니다.

임계값 규칙에서 공유할 수 있습니다.

### <a name="alerts-and-recommendations"></a>경고 및 권장 사항

규칙 정의는 모든 논리 계산 포함 되지 않습니다. UI 어떻게 정의 하 고 UI에 결과 통신 하는 SQL Server 스크립트를 보고 하는 방법입니다.

규칙에 세 부분으로 이루어져 있습니다.

* 경고 (규칙 캡션)

* 권장 사항 (도움말)

* 연결된 임계값 (종속성에 대 한 선택적 정보)

규칙의 예는 다음과 같습니다.

``` syntax
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No Recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on system drive.">
Install OS on larger disk.</advice>
<dependencies>
 <threshold ref="freediskSize"/>
</dependencies>
</rule>
```

일반적으로 권장 사항을 정의 하 고 원하는 대로 조언을 정의할 수 있습니다. **수준** 의 권장 사항 수 **성공** 또는 **경고**합니다.

원하는 만큼 많은 임계값에 연결할 수 있습니다. 현재 규칙에 관련 되지 않은 임계값도 연결할 수 있습니다. 연결 SPA 콘솔 임계값을 쉽게 관리할 수 있습니다.

규칙 이름 및 권장 사항을, 키 및 하는 고유한 범위에 속합니다. 두 개의 규칙이 없습니다 수 동일한 이름을 있으며 하나의 규칙 내에서 두 개의 제시 하지는 않습니다 동일한 이름을 가질 수 있습니다. 이러한 이름은 SQL 스크립트 보고서를 작성할 때 매우 중요 됩니다. 호출할 수는 \[dbo\].\[SetNotification\] 규칙 상태를 설정 하는 API입니다.

### <a name="defining-ui-display-elements"></a>UI 표시 요소를 정의합니다.

규칙을 정의한 후 시스템 관리자는 요약 보고서를 볼 수 있습니다. 그러나, 종종 시스템 관리자가 집계 된 데이터에 관심이 있는 되며 성능 규칙에 사용 된 데이터 소스를 확인 하려는 합니다.

이전 예에서 사용자 시스템 드라이브에 디스크 공간이 충분 한지 알고 있습니다. 사용자의 사용 가능한 공간이의 실제 크기에 관련도 합니다. 단일 값 그룹이 사용 되는 저장 하 고 이러한 결과 표시 합니다. 여러 개의 단일 값 및 그룹화 SPA 콘솔에는 테이블에 표시할 수 있습니다. 테이블에 두 개의 열, 이름 및 값을 다음과 같이 합니다.

이름 | 값
---- | ----
시스템 드라이브 (GB)에 사용 가능한 디스크 크기 | 100
설치 된 총 디스크 크기 (GB) | 500 

사용자가 서버 및 해당 디스크 크기에 설치 된 모든 하드 드라이브의 목록을 보려면, 다음 그림과 같이 3 개의 열과 여러 행에 있는 목록 값을 호출할 수 있습니다.

Disk | 사용 가능한 디스크 크기 (GB) | 총 크기 (GB)
---- | ---- | ----
0 | 100 | 500
1 | 20 | 320

advisor 팩 (단일 값 그룹 및 값 테이블 목록)에 많은 테이블이 있을 수 있습니다. 섹션을 구성 하 고 이러한 테이블을 분류에 사용할 수 있습니다.

요약 하자면,는 세 가지 유형의 UI 요소

* [섹션](#bkmk-ui-section)

* [단일 값 그룹](#bkmk-ui-svg)

* [목록 값 테이블](#bkmk-ui-lvt)

여기서는 예제는 UI 요소를 보여:

``` syntax
<advisorPack>
<dataSourceDefinition/>
<reportDefinition>
 <datatypes>
<datatype .../>
 </datatypes>
 <thresholds/>
 <rule/>
 <sections>
<section .../>
 </sections>
 <singleValues>
<singleValue .../>
 </singleValues>
 <listValues>
<listValue .../>
 </listValues>
</reportDefinition>
</advisorPack>
```

### <a href="" id="bkmk-ui-section"></a>섹션

섹션은 단지 UI 레이아웃입니다. 논리 계산에는 참여 하지 않습니다. 각 단일 보고서에 부모 섹션 없는 최상위 섹션 집합이 포함 되어 있습니다. 최상위 섹션 보고서 탭으로 표시 됩니다. 섹션에는 최대 수준 10의 하위 섹션 가질 수 있습니다. 최상위 섹션 아래의 모든 하위 섹션은 확장 가능한 영역에 표시 됩니다. 여러 하위 섹션, 단일 값 그룹 및 값 테이블 목록 섹션을 포함할 수 있습니다. 단일 값 그룹 및 값 테이블 목록 테이블로 표시 됩니다.

최상위 섹션의 예는 다음과 같습니다.

``` syntax
<section name="CPU" caption="CPU"/>
```

섹션 이름은 고유 해야 합니다. 다른 섹션, 단일 값 그룹 및 값 테이블을 나열 하 여 연결 될 수 있는 키로 사용 됩니다.

다음 예제에는 특성을 **부모**, CPU 섹션을 가리키는 하 고 있습니다. CPUFacts는 CPU를 명명 된 섹션의 자식입니다. **부모** 는 이전 이름 섹션을 참조 해야 하는 루프 그렇지 않은 경우 발생할 수 있습니다.

``` syntax
<section name="CPUFacts" caption="Facts" parent="CPU"/>
```

다음과 같은 단일 값 그룹에 특성을 **섹션**, 그 UI 디자인에 따라 모든 섹션을 가리킬 수 있습니다.

``` syntax
<singleValue name="CPUInformation" section="CPUFacts" caption="Physical CPU Information"> </singleValue>
```

### <a name="data-types"></a>데이터 형식

단일 값 그룹과 목록 값 테이블에 서로 다른 유형의 문자열, 정수 및 부동 소수점 등의 데이터를 포함 합니다. 이러한 값은 SQL Server 데이터베이스에 저장 되므로, 각 데이터 속성에 대 한 SQL 데이터 형식을 정의할 수 있습니다. 그러나 SQL 데이터 형식을 정의 상당히 복잡 합니다. 길이 또는 변경 되어야 할 수 있는 전체 자릿수를 지정 해야 했습니다.

논리 데이터 종류를 정의 하려면 첫 번째 자식을 사용할 수 있습니다 **&lt;reportDefinition /&gt;**, 즉, SQL 데이터 형식 및 논리 사용자 형식 매핑을 정의할 수 있습니다.

다음 예제에서는 두 가지 데이터 형식을 정의합니다. 하나는 **문자열** 고 다른 하나는 **companyCode**합니다.

``` syntax
<datatype name="string" = sqltype="nvarchar(4000)" />
<datatype name="companyCode" sqltype="nvarchar(100)" />
```

데이터 형식 이름에는 유효한 모든 문자열일 수 있습니다. 허용 된 SQL 데이터 형식의 목록은 다음과 같습니다.

* BIGINT

* 이진 파일

* bit

* char

* date

* Datetime

* Datetime2

* datetimeoffset

* Decimal

* FLOAT

* ssNoversion

* 비용

* nchar

* 숫자

* NVARCHAR

* REAL

* Smalldatetime

* SMALLINT

* smallmoney

* time

* TINYINT

* uniqueidentifier

* varbinary

* varchar

이러한 SQL 데이터 형식에 대 한 자세한 내용은 참조 하세요. [데이터 형식 (Transact SQL)](https://msdn.microsoft.com/library/ms187752.aspx)합니다.

### <a href="" id="bkmk-ui-svg"></a>단일 값 그룹

단일 값 그룹을 다음과 같이 테이블에 있는 여러 단일 값을 그룹화 합니다.

``` syntax
<singleValue name="Systemoverview" section="SystemoverviewSection" caption="Facts">
<value name="OsName" type="string" caption="Operating system" description="WMI: Win32_OperatingSystem/Caption"/>
<value name="Osversion" type="string" caption="OS version" description="WMI: Win32_OperatingSystem/version"/>
<value name="OsLocation" type="string" caption="OS location" description="WMI: Win32_OperatingSystem/SystemDrive"/>
</singleValue>
```

앞의 예제는 단일 값 그룹을 정의 했습니다. 섹션의 자식 노드인 **SystemoverviewSection**합니다. 이 그룹에는 단일 값을 **OsName**하십시오 **Osversion**, 및 **OsLocation**합니다.

단일 값에는 전역 고유 이름 특성이 있어야 합니다. 이 예제에서는 전역 고유 이름 특성은 **Systemoverview**합니다. 사용자 지정 보고서에 대 한 해당 뷰를 생성 하는 고유 이름 사용 됩니다. 접두사를 포함 하는 각 뷰에 **vw**, vwsystemoverview 합니다.

여러 개의 단일 값 그룹을 정의할 수 있지만 두 개의 단일 값 이름이 수 동일한 경우에 서로 다른 그룹에. 단일 값 이름 값을 적절 하 게 설정 하는 SQL 스크립트 보고서에 사용 됩니다.

각 단일 값에 대 한 데이터 형식을 정의할 수 있습니다. 허용 되는 입력에 대 한 **형식** 에 정의 된  **&lt;datatype /&gt;** 합니다. 최종 보고서는 다음과 같습니다.

**Facts**

이름 | 값
--- | ---
운영 체제 | &lt;_보고서 스크립트에서 값을 설정_&gt;
OS 버전 | &lt;_보고서 스크립트에서 값을 설정_&gt;
운영 체제 위치 | &lt;_보고서 스크립트에서 값을 설정_&gt;

**캡션** 특성 **&lt;값 /&gt;** 첫 번째 열에 표시 됩니다. 값 열에는 값을 통해 스크립트 보고서에 의해 나중에 설정 된 \[dbo\].\[SetSingleValue\]합니다. **설명** 특성 **&lt;값 /&gt;** 도구 설명에 표시 됩니다. 일반적으로 도구 설명에 표시할 데이터의 원본을 사용자를 표시합니다. 도구 설명에 대 한 자세한 내용은 참조 하십시오. [도구 설명](#bkmk-tooltips)합니다.

### <a href="" id="bkmk-ui-lvt"></a>목록 값 테이블

테이블 정의와 같은 것으로 목록 값을 정의 합니다.

``` syntax
<listValue name="NetworkAdapterInformation" section="NetworkIOFacts" caption="Physical network adapter information">
<column name="NetworkAdapterId" type="string" caption="ID" description="WMI: Win32_NetworkAdapter/DeviceID"/>
<column name="NetworkAdapterName" type="string" caption="Name" description="WMI: Win32_NetworkAdapter/Name"/>
<column name="type" type="string" caption="type" description="WMI: Win32_NetworkAdapter/Adaptertype"/>
<column name="Speed" type="decimal" caption="Speed (Mbps)" description="WMI: Win32_NetworkAdapter/Speed"/>
<column name="MACaddress" type="string" caption="MAC address" description="WMI: Win32_NetworkAdapter/MACaddress"/>
</listValue>
```

목록 값 이름은 전역적으로 고유 해야 합니다. 이 이름은 임시 테이블의 이름이 됩니다. 이전 예제에서는 테이블 명명 \#NetworkAdapterInformation 설명 하는 모든 열을 포함 하는 실행 환경 초기화 단계에서 생성 됩니다. 단일 값 이름을 마찬가지로, 목록 값 이름은 사용 됩니다 vwNetworkAdapterInformation 예를 들어, 사용자 지정 뷰 이름의 일부로.

@type &lt;열 /&gt; 정의한 &lt;datatype /&gt;

최종 보고서의 모의 UI 다음과 같이 표시 될 수 있습니다.

**실제 네트워크 어댑터 정보**

ID | 이름 | 형식 | 속도 (Mbps) | MAC 주소
--- | --- | --- | --- | ---
 | <br> | | |
 | | | |


**캡션** 특성 &lt;열 /&gt; 열 이름으로 표시 됩니다 및 **설명** 특성 &lt;열 /&gt; 해당 열 머리글에 대 한 도구 설명으로 표시 됩니다. 일반적으로 도구 설명에 표시할 데이터의 원본을 사용자를 표시합니다. 자세한 내용은 참조 하십시오. [도구 설명](#bkmk-tooltips)합니다.

일부 경우에 테이블 많은 열을 가질 수 있습니다를 찾아서만 몇 개의 행을 테이블의 열과 행을 교환 없게 되므로 훨씬 더 좋습니다. 열과 행을 교환 하려면 다음과 같은 스타일 특성을 추가할 수 있습니다.

``` syntax
<listValue style="Transpose"  
```

### <a name="defining-charting-elements"></a>차트 요소를 정의합니다.

모든 통계 키를 선택 하 고는 기록 차트 또는 추세 차트에서 값을 볼 수 있습니다. 통계는 다음과 같은 두 종류가 있습니다.

* **정적 통계** 는 디자인 타임에 알려진 단일 값입니다. 예를 들어 시스템 드라이브의 디스크 여유 공간을 정적 통계 것입니다.

* **동적 통계** 디자인 타임에 알려진 못할 수도 있습니다. 예를 들어 각 코어의 평균 CPU 사용량은 디자인 타임에 시스템에 얼마나 많은 CPU 코어 수 알지 못하므로 동적 통계입니다.

통계 키에 데이터를 double 데이터 형식와 호환 되어야 하는 제한이 있습니다. integer, decimal 또는 double로 변환 될 수 있는 문자열로 수 있습니다.

SPA 정적 통계 및 동적 통계를 지원 하기 위해 목록 값 테이블을 지원 하기 위해 단일 값 그룹을 사용 합니다. 다음 섹션에서는 통계 정적 및 동적 통계 키를 정의 하는 방법에 설명 합니다.

### <a name="static-statistics"></a>정적 통계

앞에서 설명한 대로 정적 통계는 단일 값입니다. 논리적으로 단일 값을 정적 통계로 정의할 수 있습니다. 그러나는 숫자 형식으로 캐스팅할 수 없는 단일 값을 확인 하는 의미가 없습니다. 정적 통계를 정의 하려면 추가할 수 있습니다 단순히 특성 **trendable** 해당 단일 값 키에 표시 된 것 처럼 아래:

``` syntax
<value name="freediskSize" type="int" trendable="true"  
```

### <a name="dynamic-statistics"></a>동적 통계

가능한 값의 수를 알 되지 않으므로 디자인 타임에 동적 통계 키 알려져 있지 않습니다. 그러나 목록 값에 여러 행에 저장 되므로 쉽도록 동적 통계를 저장 하는 목록 값 테이블을 사용 하도록 합니다.

예를 들어, 다른 코어의 평균 CPU 사용량에 대 한 차트를 표시 하려고 하는 경우 열이 포함 된 테이블 정의 수 **CpuId** 하 고 **AverageCpuUsage**:

``` syntax
<listValue name="CpuPerformance">
<column name="CpuId" type="string" caption="CPU ID" columntype="Key"/>
<column name="AverageCpuUsage" type="decimal" caption="Average" columntype="Value"/>
</listValue>
```

다른 특성 **columntype**, 될 수 있습니다 **키**를 **값**, 또는 **Informational**합니다. 데이터 형식이 **키** 열 double 이어야 합니다. 또는 double 변환 가능 합니다. 에 **키** 열을 테이블에 동일한 키를 삽입할 수 없습니다. **값** 또는 **정보** 열이이 제한 사항이 없습니다.

통계 값에 저장 됩니다 **값** 열입니다.

**정보 제공 용 이므로** 일반 목록 값 테이블의 일반 열과 같은 열이 있습니다. **정보 제공 용 이므로** 텍스트를 지정 하지 않으면 기본 열 유형입니다. 이러한 열 통계 키의 수에 영향을 줄 또는 계산 관련 된 통계에에서 참여 안 됩니다.

서버에 있는 경우 두 개의 CPU 코어 앞의 예제를 계속, 테이블에 결과 다음과 같습니다.

CpuId | AverageCpuUsage
:---: | :---:
0 | 10
1 | 30

같은 시간에 두 개의 통계 키는 SPA 프레임 워크에 의해 생성 됩니다. 하나 CPU 0에 대 한 고 다른 하나는 CPU 1입니다.

다음 예제에서는 여러 나타나듯이 **값** 여러 개의 열 **키** 열이 지원 됩니다.

CounterName | InstanceName | 평균 | 합계
--- | :---: | :---: | :---:
프로세서 시간 비율 | _Total | 10 | 20
프로세서 시간 비율 | CPU0 | 20 | 30 

이 예제에서는 두 개 있는 **키** 열과 두 **값** 열입니다. SPA는 Average 열에 대 한 두 개의 통계 키 및 합계 열에 대 한 다른 두 개의 키를 생성합니다. 통계 키는 있습니다.

* CounterName (% 프로세서 시간) / InstanceName (\_총) / 평균

* CounterName (% 프로세서 시간) / InstanceName (CPU0) / 평균

* CounterName (% 프로세서 시간) / InstanceName (\_총) / 합계 계산

* CounterName (% 프로세서 시간) / InstanceName (CPU0) / 합계 계산

CounterName 및 InstanceName는 하나의 키로 결합 됩니다. 결합 된 키에 중복을 가질 수 없습니다.

SPA 많은 통계 키를 생성합니다. 그 중 일부 필요 하지 않을 수, 있으며 UI에서 아이콘을 숨기려면 수 있습니다. SPA는 개발자가 유용한 통계 키만을 표시 하는 필터를 만들 수 있습니다.

이전 예를 들어 시스템 관리자만 관심이 있을 수는 InstanceName 인 키 \_합계 또는 CPU1 합니다. 필터는 다음과 같이 정의할 수 있습니다.

``` syntax
<listValue name="CpuPerformance">
<column name="CounterName" type="string" columntype="Key"/>
<column name="InstanceName" type="string" columntype="Key">
 <trendableKeyValues>
<value>_Total</value>
<value>CPU1</value>
 </trendableKeyValues>
</column>
<column name="Average" type="decimal" columntype="Value"/>
<column name="Sum" type="decimal" columntype="Value"/>
</listValue>
```

**&lt;trendableKeyValues /&gt;**  키 열을 정의할 수 있습니다. 둘 이상의 하나의 키 열에 필터를 구성 하 고 논리 적용 됩니다.

### <a name="developing-report-scripts"></a>보고서 스크립트 개발

프로 비전 메타 데이터를 정의한 후에 T-SQL 저장 프로시저는 보고서 스크립트에서 쓰기를 시작할 수 있습니다.

**이름** 및 **reportScript** 프로 비전 메타 데이터 헤더의 특성을 다음과 같이 합니다.

``` syntax
<advisorPack name="Microsoft.ServerPerformanceAdvisor.CoreOS.V1" reportScript="ReportScript"  
```

결합 하 여 주 보고서 스크립트 라고는 **이름** 및 **reportScript** 특성입니다. 다음 예제에서는 수 \[Microsoft.ServerPerformanceAdvisor.CoreOS.V2\].\[ReportScript\]합니다.

``` syntax
create PROCEDURE [Microsoft.ServerPerformanceAdvisor.CoreOS.V2].[ReportScript] AS SET NOCOUNT ON

- Set alert and notification

- Prepare data for report view
```

**이름** 특성은 네임 스페이스와 같은 데이터베이스 스키마 이름으로 사용 됩니다. 이 규칙에 목록 값 및 저장된 프로시저와 같은 현재 advisor 팩에 속해 있는 다른 모든 데이터베이스 개체에 적용 됩니다.

데이터베이스 개체 앞에이 스키마 이름을 지정 하는 이점은 다음과 같습니다.

* 다른 advisor 팩에 대 한 이름 충돌 방지

* 보안이 강화

SQL Server 데이터베이스의 기본 스키마 이름을 **dbo**합니다. 데이터베이스 소유자 자격 증명은 데이터베이스 개체에서 작동 해야 일반적으로 **dbo**합니다. 각 advisor 팩에 대 한 스키마를 만들려면 우리 호스팅되고 두 advisor 팩 동일한 이름 가진 목록 값을 정의 합니다. 이렇게 하지 관련 되므로 해야이 문제를 해결 하는 스키마 이름을 제공할 수 있습니다. 또한 advisor 팩 프로 비전 해제 훨씬 쉽습니다. Advisor 팩 개체가 아닌 다른 스키마에 속해 있으므로 **dbo**, 이 통해 액세스 하는 데 더 낮은 사용자 권한을 사용 하 여 SPA 합니다.

일반 보고서 스크립트는 다음을 수행 합니다.

* 원시 수집 된 데이터에 액세스

* 원시 데이터를 기반으로 하는 계산을 수행 합니다.

* 변경 알림 및 권장 사항

* 보고서 보기에 대 한 데이터를 준비합니다.

### <a name="access-raw-collected-data"></a>원시 수집 된 데이터에 액세스

다음 해당 테이블에 모든 수집 된 데이터를 가져옵니다. 테이블 스키마에 대 한 자세한 내용은 참조 하십시오. [데이터 수집기 집합을 정의](#bkmk-definedatacollector)합니다.

* registry

    * \#registryKeys

* WMI

    * \#WMIObjects

    * \#WmiObjectProperties

    * \#WmiQueries

* 성능 카운터

    * \#PerformanceCounters

* 파일

    * \#파일

* ETW

    * \#이벤트

    * \#EventProperties

### <a name="set-rule-status"></a>규칙 상태 설정

\[dbo\].\[SetNotification\] 볼 수 있도록 규칙 상태를 설정 하는 API는 **성공** 또는 **경고** UI의 아이콘입니다.

* @ruleName nvarchar(50)

* @adviceName nvarchar(50)

경고 및 권장 사항 메시지 프로 비전 메타 데이터 XML 파일에 저장 됩니다. 이렇게 하면 보고서 스크립트를 쉽게 관리할 수 있습니다.

처음에 모든 규칙 상태는 해당 되지 않음입니다. 조언을 이름을 지정 하 여 규칙 상태를 설정 하려면이 API를 사용할 수 있습니다. 조언 이름 수준의 규칙 상태에 사용 됩니다.

다음과 같은 규칙이 앞서 정의한를 회수 합니다.

``` syntax
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on the system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on system drive.">Install the operating system on a larger disk.</advice>
</rule>
```

사용 가능한 공간이 2GB 미만으로 가정 하 고 필요한 설정 규칙는 **경고** 수준입니다. SQL 스크립트를 다음과 같이 됩니다.

``` syntax
if (@freediskSizeInGB < 2)
BEGIN
    exec dbo.SetNotification N'freediskSize', N'WarningAdvice'
END
ELSE
BEGIN
    exec dbo.SetNotification N'freediskSize', N'SuccessAdvice'
END 
```

### <a name="get-threshold-value"></a>임계값 값 가져오기

\[dbo\].\[GetThreshold\] API의 임계값을 가져옵니다.

* @key nvarchar(50)

* @value float 출력

> [!NOTE]
> 임계값 이름-값 쌍 이며 모든 규칙에서 참조할 수 있습니다. 시스템 관리자가 임계값을 조정 하려면 SPA 콘솔을 사용할 수 있습니다.

 임계값에 대 한 이전 예에서 정의 다음과 같이 설정 됩니다.

``` syntax
<thresholds>
  <threshold name="freediskSize" caption="Free Disk Size (GB)" description="Free Disk Size  value="10" />
</thresholds>
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on the system drive.">
Install the operating system on a larger disk.</advice>
<dependencies>
 <threshold ref="freediskSize"/>
</dependencies>
</rule>
```

다음과 같이 보고서 스크립트를 수정할 수 있습니다.

``` syntax
DECLARE @freediskSize FLOat
exec dbo.GetThreshold N freediskSize , @freediskSize output

if (@freediskSizeInGB < @freediskSize)
 
```

### <a name="set-or-remove-the-single-value"></a>설정 또는 단일 값 제거

\[dbo\].\[SetSingleValue\] API 단일 값을 설정 합니다.

* @key nvarchar(50)

* @value sql\_variant

이 값 같은 단일 값 키에 대 한 여러 번 실행할 수 있습니다. 마지막 값이 저장 됩니다.

다음 예제에서는 일부 단일 값을 정의 합니다.

``` syntax
<singleValue section="Systemoverview" caption="Facts">
<value name="OsName" type="string" caption="Operating System" description="WMI: Win32_OperatingSystem/Caption"/>
<value name="Osversion" type="string" caption="OS version" description="WMI: Win32_OperatingSystem/version"/>
<value name="OsLocation" type="string" caption="OS Location" description="WMI: Win32_OperatingSystem/SystemDrive"/>
</singleValue>
```

그런 다음 다음과 같이 단일 값을 설정할 수 있습니다.

``` syntax
exec dbo.SetSingleValue N OsName ,  Windows 7 
exec dbo.SetSingleValue N Osversion ,  6.1.7601 
exec dbo.SetSingleValue N OsLocation ,  c:\ 
```

드문 경우를 사용 하 여 이전에 설정한 결과 제거 하려는 합니다 \[dbo\].\[ removeSingleValue\] API.

* @key nvarchar(50)

다음 스크립트를 사용 하 여 이전에 설정한 제거할 값입니다.

``` syntax
exec dbo.removeSingleValue N Osversion 
```

### <a name="get-data-collection-information"></a>데이터 컬렉션 정보 가져오기

\[dbo\].\[GetDuration\] API 사용자가 지정 기간 (초)에 데이터 컬렉션을 가져옵니다.

* @duration int 출력

여기서는 예제 스크립트를 보고 합니다.

``` syntax
DECLARE @duration int
exec dbo.GetDuration @duration output
```

\[dbo\].\[GetInternal\] API 성능 카운터의 간격을 가져옵니다. 현재 보고서에 성능 카운터 정보가 없는 경우 NULL을 반환할 수 것입니다.

* @interval int 출력

여기서는 예제 스크립트를 보고 합니다.

``` syntax
DECLARE @interval int
exec dbo.GetInterval @interval output
```

### <a name="set-a-list-value-table"></a>목록 값 테이블 설정

목록 값 테이블을 업데이트 하기 위한 API는 없습니다. 그러나 목록 값 테이블을 직접 액세스할 수 있습니다. 초기화 단계에서 해당 하는 임시 테이블을 각 목록 값에 대해 만들어집니다.

다음 예제에서는 목록 값 테이블을 보여 줍니다.

``` syntax
<listValue name="NetworkAdapterInformation" section="NetworkIOFacts" caption="Physical Network Adapter Information">
<column name="NetworkAdapterId" type="string" caption="ID" description="WMI: Win32_NetworkAdapter/DeviceID"/>
<column name="NetworkAdapterName" type="string" caption="Name" description="WMI: Win32_NetworkAdapter/Name"/>
<column name="type" type="string" caption="type" description="WMI: Win32_NetworkAdapter/Adaptertype"/>
<column name="Speed" type="decimal" caption="Speed (Mbps)" description="WMI: Win32_NetworkAdapter/Speed"/>
<column name="MACaddress" type="string" caption="MAC address" description="WMI: Win32_NetworkAdapter/MACaddress"/>
</listValue>
```

그런 다음 삽입, 업데이트 또는 결과 삭제 하는 SQL 스크립트를 작성할 수 있습니다.

``` syntax
INSERT INTO #NetworkAdapterInformation (
  NetworkAdapterId,
  NetworkAdapterName,
  type,
  Speed,
  MACaddress
)
VALUES (
   
)
```

## <a name="development-and-debugging"></a>개발 및 디버깅


### <a name="writing-logs"></a>로그를 작성합니다.

추가 정보를 시스템 관리자에 게 전달 하려면 모두 있으면 로그를 작성할 수 있습니다. 특정 보고서에 대 한 모든 로그 이면 노란색 배너의 보고서 머리글에 표시 됩니다. 다음 예제에서는 로그를 작성 하는 방법을 보여 줍니다.

``` syntax
exec dbo.WriteSystemLog N'Any information you want to show to the system administrators , N Warning 
```

첫 번째 매개 변수는 로그에 메시지를 표시 합니다. 두 번째 매개 변수는 로그 수준입니다. 두 번째 매개 변수에 대 한 유효한 입력 수 **정보**, **경고**, 또는 **오류**합니다.

### <a name="debug"></a>디버그

SPA 콘솔 수 실행 하는 두 가지 모드에서 디버그 또는 릴리스 합니다. 릴리스 모드, 기본 인증 이며 보고서가 생성 한 후 모든 수집 된 원시 데이터를 정리 하는 것입니다. 디버그 모드는 나중에 보고서 스크립트를 디버깅할 수 있도록 파일 공유 및 데이터베이스에 모든 원시 데이터를 유지 합니다.

**보고서 스크립트를 디버깅 하려면**

1.  Microsoft SQL Server Management Studio (SSMS)를 설치 합니다.

2.  Localhost에 연결 하는 SSMS를 시작한 후\\SQLExpress입니다. 대신 localhost를 사용 해야 함을 알아야 합니다. . 그렇지 않으면 SQL Server에서 디버거를 시작할 수 없습니다.

3.  디버그 모드를 사용 하도록 설정 하려면 다음 스크립트를 실행 합니다.

    ``` syntax
    USE SPADB
    UPdate dbo.Configurations
    SET Value = N'true'
    WHERE Name = N'Debugmode'
    ```

4.  SPA 콘솔을 시작 하 고 디버그 하려는 advisor 팩을 실행 합니다.

5.  작업이 완료 될 때까지 기다립니다. 보고서가 성공적으로 생성 하는 경우 SSMS로 다시 전환 하 고 최신 작업에 대 한 확인 합니다.

    ``` syntax
    select TOP 1 * FROM dbo.Tasks OrdER BY Id DESC
    ```

    예를 들어 출력 수 있습니다.

    Id | 세션 Id | AdvisoryPackageId | ReportStatusId | LastUpdatetime | ThresholdversionId
    :---: | :---: | :---: | :---: | :---: | :---:
    12 | 17 | 1 | 2 | 2011-05-11 05:35:24.387 | 1

6.  Id 12에 대 한 보고서 스크립트를 실행 하 고 원하는 횟수 만큼 다음 스크립트를 실행할 수 있습니다.

    ``` syntax
    exec dbo.DebugReportScript 12
    ```

    **참고** 이전 문 및 디버그를 한 단계씩 실행 하려면 f11 키를 누를 수도 있습니다.

     

실행 중인 \[dbo\].\[DebugReportScript\] 포함 하 여 여러 결과 집합을 반환 합니다.

1.  Microsoft SQL Server 메시지 및 advisor 팩 로그

2.  규칙의 결과

3.  통계 키 및 값

4.  단일 값

5.  모든 목록 값 테이블

## <a name="best-practices"></a>모범 사례

### <a name="naming-convention-and-styles"></a>명명 규칙 및 스타일

파스칼식 대/소문자 구분 | 카멜식 대/소문자 | 대문자
--- | ---- | ---
<ul><li>ProvisionMetadata.xml에는 이름</li><li>저장 프로시저</li><li>함수</li><li>뷰 이름</li><li>임시 테이블 이름</li></ul> | <ul><li>매개 변수 이름</li><li>지역 변수</li></ul> | 모든 SQL 예약 키워드 사용

### <a name="other-recommendations"></a>기타 권장 사항

* 다른 저장된 프로시저 및 사용자 정의 함수를 가장 논리적 부분을 이동 합니다.

* 유지 관리를 위해 가능한 한 간결 기본 스크립트를 확인 합니다.

* SQL 개체의 전체 이름을 사용 합니다.

* 대/소문자 구분으로 SQL 코드를 처리 합니다.

* 추가 **SET NOCOUNT ON** 모든 저장된 프로시저의 시작 부분에 있습니다.

* 임시 테이블을 사용 하 여 다량의 데이터를 전송 하는 것이 좋습니다.

* 사용 하는 것이 좋습니다 **설정 XACT\_중단 ON** 오류가 발생 하는 경우 프로세스를 종료 하려면.

* 항상 advisor 팩 표시 이름에 주 버전 번호를 포함 합니다.

## <a href="" id="bkmk-advancedtopics"></a>고급 항목

### <a name="run-multiple-advisor-packs-simultaneously"></a>여러 advisor 팩을 동시에 실행

SPA 동시에 실행 되는 여러 advisor 팩을 지원 합니다. 인터넷 정보 서비스 (IIS) 및 동시에 핵심 운영 체제 성능 확인 하려는 경우 특히 유용 합니다. IIS 관리자 팩에서 사용 되는 데이터 수집기가 많은 핵심 OS advisor 팩에서 사용할 수도 있습니다. 두 개 이상의 advisor 팩 동일한 대상 컴퓨터에서 실행 되 고 있으면 SPA 수집 하지 않습니다 동일한 데이터가 두 번.

다음 예제에서는 두 개의 advisor 팩을 실행 하기 위한 워크플로 보여 줍니다.

![실행 되는 여러 advisor 팩](../media/server-performance-advisor/spa-dev-guide-multi-advisor-packs.png)

성능 카운터 및 ETW 데이터 원본에 대해서만 합병 데이터 수집기 집합입니다. 다음 병합 규칙이 적용 됩니다.

1.  SPA는 가장 큰 기간에서 새 기간을 사용합니다.

2.  병합 충돌 인 경우에 다음 규칙이 적용 됩니다.

    1.  새 간격으로 최소 간격을 가져옵니다.

    2.  성능 카운터의 상위 집합을 수행 합니다. 예를 들어 **프로세스 (\*)\\% Processor time** 및 **프로세스 (\*)\\\*하십시오\\프로세스 (\*)\\ \***  더 많은 데이터를 반환 하므로 **프로세스 (\*)\\% Processor time** 고 **프로세스 (\*)\\ \***  병합 된 데이터 수집기 집합에서 제거 됩니다.

### <a name="collect-dynamic-data"></a>동적 데이터 수집

SPA 요구는 정의 된 데이터 수집기 집합에서 디자인 타임. 항상 수 없으면 동적 데이터 및 쿼리 경로 알 수 없으므로 해당 종속 데이터가 있을 때까지 보고서 생성을 위해 필요한 데이터를 알아야 합니다.

예를 들어 네트워크 어댑터의 모든 친숙 한 이름을 나열 하려는 경우 모든 네트워크 어댑터를 열거 하는 WMI 쿼리 먼저 해야 합니다. 반환 된 각 WMI 개체에 레지스트리 키 경로 이름을 저장 한 위치입니다. 레지스트리 키 경로 디자인 타임에 알려진 아닙니다. 이 경우 동적 데이터 필요를 지원 합니다.

모든 네트워크 어댑터를 열거 하려면 Windows PowerShell을 사용 하 여 다음 WMI 쿼리를 사용할 수 있습니다.

``` syntax
Get-WmiObject -Namespace Root\Cimv2 -query "select PNPDeviceID FROM Win32_NetworkAdapter" | forEach-Object { Write-Output $_.PNPDeviceID }
```

네트워크 어댑터 개체의 목록을 반환합니다. 각 개체에 라는 속성이 **PNPDeviceID**, 상대 레지스트리 키 경로 유지 하 합니다. 여기가 서 이전 쿼리로부터 샘플 출력:

``` syntax
ROOT\*ISatAP\0001
PCI\VEN_8086&DEV_4238&SUBSYS_11118086&REV_35\4&372A6B86&0&00E4
ROOT\*IPHTTPS\0000
 
```

찾으려는 합니다 **FriendlyName** 값, 레지스트리 편집기를 열고 레지스트리 설정을 조합 하 여 **HKEY\_로컬\_MACHINE\\SYSTEM\\ CurrentControlSet\\Enum\\**  이전 샘플의 각 줄. 예를 들어: **HKEY\_로컬\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\ 루트\\\*IPHTTPS\\0000**합니다.

SPA 프로 비전 메타 데이터에 이전 단계를 변환 하려면 다음 코드 샘플에는 스크립트를 추가 합니다.

``` syntax
<advisorPack>
<dataSourceDefinition xmlns="http://microsoft.com/schemas/ServerPerformanceAdvisor/dc/2010">
 <dataCollectorSet >
<registryKeys>
 ?<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\$(NetworkAdapter.PNPDeviceID)\FriendlyName</registryKey>
</registryKeys>
<managementpaths>
 ?<path name="NetworkAdapter">Root\Cimv2:select PNPDeviceID FROM Win32_NetworkAdapter</path>
</managementpaths>
```

이 예제에서는 먼저 추가 managementpaths에서 WMI 쿼리 하는 키 이름을 정의 **NetworkAdapter**합니다. 레지스트리 키를 추가 하 고 참조 **네트워크 어댑터** 구문을 사용 하 여 **$(NetworkAdapter.PNPDeviceID)** 합니다.

다음 표에서 동적 데이터와 다른 데이터 수집기에서 참조할 수 있는지 여부는 데이터 수집기 SPA에서 지 원하는 경우를 정의 합니다.

데이터 형식 | 동적 데이터를 지원 합니다. | 참조할 수 있습니다.
--- | :---: | :---:
레지스트리 키 | 예 | 예
WMI | 예 | 예
파일 | 예 | 아니오
성능 카운터 | 아니요 | 아니요
ETW | 아니오 | 아니오

WMI 데이터 수집기에 대 한 각 WMI 개체에는 연결 된 특성이 있습니다. 모든 종류의 WMI 개체는 항상 세 가지 특성을 가집니다. \_\_네임 스페이스 \_ \_클래스와 \_ \_RELpath 합니다.

다른 데이터 수집기에서 참조 되는 데이터 수집기를 정의 하려면 할당 된 **이름** 는 ProvisionMetadata.xml에서 고유 키를 사용 하 여 특성입니다. 이 키는 동적 데이터를 생성 하려면 종속 데이터 수집기에서 사용 됩니다.

S 예제 레지스트리 키에는 다음과 같습니다.

``` syntax
<registryKey  name="registry">HKEY_LOCAL_MACHINE </registryKey>
```

및 WMI에 대 한 예제:

``` syntax
<path name="wmi">Root\Cimv2:select PNPDeviceID FROM Win32_NetworkAdapter</path>
```

종속 데이터 수집기를 정의 하려면 다음 구문을 사용 합니다. $(*{name}*.*{특성}*).

*{name}* 및 *{특성}* 자리 표시 자가 있습니다.

패턴 $ SPA 대상 서버에서 데이터를 수집 하는 경우 동적으로 대체 (\*.\*)의 참조 데이터 수집기에서 수집 된 데이터와 실제 (레지스트리 키 / WMI), 예:

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\$(registry.key)\ </registryKey>
<registryKey  name="registry">HKEY_LOCAL_MACHINE\$(wmi.Relativeregistrypath)\ </registryKey>
<path name="wmi"> </path>
<file>$(wmi.FileName)</file>
```

**참고** SPA 참조의 무제한 깊이 지원 하지만 수준이 너무 많은 성능 오버 헤드가 알 수 있습니다. 순환 참조가 없으면 또는 자체 참조가 지원 되지 않는 있는지 확인 합니다.

### <a name="versioning-limitations"></a>버전 관리 제한 사항

SPA 재설정 및 부 버전 업데이트를 지원합니다. 이러한 프로세스는 동일한 알고리즘을 사용 합니다. 프로세스는 기존 데이터를 유지 하면서 모든 데이터베이스 개체 및 임계값 설정 새로 고침 하는 것입니다. 이 더 높은 버전으로 업그레이드 하거나 수 낮은 버전으로 다운 그레이드 합니다. advisor 팩을 선택한 다음 클릭 **재설정** 에 **Advisor 팩 구성** 대화 상자를 다시 설정 하거나 적용 SPA 또는 업데이트 합니다.

이 기능은 주로 부 업데이트입니다. UI 표시 요소를 크게 변경할 수 없습니다. 중요 한 변경 하려는 경우 다른 관리자 팩을 만드는 해야 합니다. Advisor 팩 이름에는 주 버전을 포함 해야 합니다.

부 버전 수정 제한은 있는 있습니다 **없습니다** 다음 중 하나를 수행 합니다.

* 스키마 이름 변경

* 단일 값 그룹의 데이터 형식이 나 목록 값 테이블의 열 변경

* 추가 또는 제거 임계값

* 추가 또는 제거 규칙

* 추가 하거나 advice를 제거

* 단일 값 추가 또는 제거

* 목록 값 추가 또는 제거

* 추가 하거나 목록 값의 열을 제거

### <a href="" id="bkmk-tooltips"></a>도구 설명

거의 모든 **설명** 특성 SPA 콘솔의 도구 설명으로 표시 됩니다.

목록 값 테이블에 대해 행을 기준으로 도구 설명에 다음 특성을 추가 하 여 수행할 수 있습니다.

``` syntax
<listValue descriptionColumn="Description">
<column name="Name"/>
<column name="Description"/>
</listValue>
```

**descriptionColumn** 특성 열의 이름을 가리킵니다. 이 예에서 설명 열 실제 열으로 표시 되지 않습니다. 그러나 표시 도구 설명으로 각 행의 첫째 열 위로 마우스를 이동할 때.

도구 설명에 표시할 사용자에 게 데이터 소스를 표시 하는 것이 좋습니다. 다음은 데이터 소스 표시에 대 한 형식입니다.

데이터 원본 | 형식 | 예제
--- | --- | ---
WMI | : WMI &lt;wmiclass&gt;/&lt;필드&gt; | WMI: Win32_OperatingSystem/Caption
성능 카운터 | 성능 카운터: &lt;CategoryName&gt;/&lt;InstanceName&gt; | 성능 카운터: Process/% 프로세서 시간
registry | registry: &lt;registerKey&gt; | 레지스트리: HKLM\SOFTWARE\Microsoft<br>\\ASP.NET\\Rootver
구성 파일 | ConfigFile: &lt;Filepath&gt;\[; Xpath: &lt;Xpath&gt;\]<br>**참고**<br>Xpath는 선택 사항 고 파일은 xml 파일이 있는 경우에 유효 합니다. | ConfigFile: windir %\\System32\\inetsrv\config\\applicationHost.config<br>Xpath: 구성&frasl;system.webServer<br>&frasl;httpProtocol&frasl;@allowKeepAlive
ETW | ETW: &lt;공급자 /&gt;(키워드) | ETW: Windows 커널 추적 (프로세스, net)

### <a name="table-collation"></a>테이블 데이터 정렬

Advisor 팩 더 복잡 해지면 고유한 변수 테이블 또는 보고서 스크립트의 중간 결과 저장 하는 임시 테이블을 만들 수 있습니다.

문자열 열 데이터 정렬를 만들면 테이블 데이터 정렬을 SPA 프레임 워크에 의해 만들어진 것과 다른 될 수 있으므로 문제가 될 수 있습니다. 서로 다른 테이블에 두 개의 문자열 열 상관 관계를 지정 하는 경우 데이터 정렬 오류가 표시 될 수 있습니다. 이 문제를 방지 하려면 항상로 열 데이터 정렬에 대 한 문자열을 정의 해야 **SQL\_Latin1\_일반\_CP1\_CI\_AS** 테이블을 정의 합니다.

다음 변수 테이블을 정의 하는 방법.

``` syntax
DECLARE @filesIO TABLE (
 Name nvarchar(500) COLLatE SQL_Latin1_General_CP1_CI_AS,
 AverageFileAccessvolume float,
 AverageFileAccessCount float,
 Filepath nvarchar(500) COLLatE SQL_Latin1_General_CP1_CI_AS
)
```

### <a name="collect-etw"></a>ETW를 수집 합니다.

다음 ETW ProvisionMetadata.xml 파일에서 정의 하는 방법.

``` syntax
<dataSourceDefinition>
  <providers>
    <provider session="NT Kernel Logger" guid="{9E814AAD-3204-11D2-9A82-006008A86939}"/>
  </providers>
</dataSourceDefinition>
```

다음 공급자 특성은 ETW 수집에 사용할 수 있습니다.

attribute | 형식 | 설명
--- | --- | ---
guid | GUID | 공급자 GUID
세션 | string | ETW 세션 이름 (선택 사항, 커널 이벤트에만)
keywordsany | Hex | 키워드 (선택 사항, 0x 접두사 없음)
keywordsAll | Hex | (선택 사항) 모든 키워드
속성 | Hex | 속성 (옵션)
수준(level) | Hex | (선택 사항) 수준
bufferSize | Int | 버퍼 크기 (선택 사항)
flushtime | Int | (선택 사항) 플러시 시간
maxBuffer | Int | 최대 버퍼 (선택 사항)
minBuffer | Int | 최소 버퍼 (선택 사항)

다음과 같이 두 개의 출력 테이블을 있습니다.

**\#이벤트 테이블 스키마**

열 이름 | SQL 데이터 형식 | 설명
--- | --- | ---
SequenceID | NULL이 아닌 Int | 상관 관계 시퀀스 ID
EventtypeId | NULL이 아닌 Int | 이벤트 유형 ID (참조 [dbo]. [ Eventtypes])
ProcessId | NULL이 아닌 BigInt | 프로세스 ID
스레드 Id | NULL이 아닌 BigInt | 스레드 ID
타임 스탬프 | datetime2 NULL이 아님 | 타임 스탬프
Kerneltime | NULL이 아닌 BigInt | 커널 시간
Usertime | NULL이 아닌 BigInt | 사용자 시간

**\#EventProperties 테이블 스키마**

열 이름 | SQL 데이터 형식 | 설명
--- | --- | ---
SequenceID | NULL이 아닌 Int | 상관 관계 시퀀스 ID
이름 | Nvarchar(100) | 속성 이름
값 | Nvarchar (4000) | 값

### <a name="etw-schema"></a>ETW 스키마

.Etl 파일에 대해 tracerpt.exe를 실행 하 여 ETW 스키마를 생성할 수 있습니다. Schema.man 파일이 생성 됩니다. .Etl 파일의 형식이 종속 컴퓨터 이기 때문에 다음 스크립트는 다음과 같은 경우에만 작동 합니다.

1.  매개 변수는 해당.etl 파일 수집 되는 컴퓨터에는 스크립트를 실행 합니다.

2.  또는 동일한 운영 체제 및 구성 요소가 설치 된 컴퓨터에서 스크립트를 실행 합니다.

``` syntax
tracerpt *.etl -export
```

## <a name="glossary"></a>용어 설명


이 문서에는 다음과 같은 용어가 사용 됩니다.

**Advisor 팩**

Advisor 팩은 메타 데이터와 대상 서버에서 수집 된 성능 로그를 처리 하는 SQL 스크립트의 컬렉션입니다. Advisor 팩 성능 로그 데이터에서 보고서를 생성합니다. Advisor 팩에 있는 메타 데이터는 성능 측정에 대 한 대상 서버에서 수집할 데이터를 정의 합니다. 또한 메타 데이터의 규칙과 임계값, 보고서 형식 집합을 정의합니다. 대부분의 경우 advisor 팩은 특별히 작성 된 예를 들어, 인터넷 정보 서비스 (IIS)는 단일 서버 역할을 합니다.

**SPA 콘솔**

SPA 콘솔 Server Performance Advisor의 중앙 구성 요소인 SpaConsole.exe를 가리킵니다. SPA를 테스트 하는 대상 서버에서 실행할 필요는 없습니다. SPA 콘솔에서 보고서 보기 및 분석을 실행 하려면 프로젝트 설정 SPA를 모든 사용자 인터페이스를 포함 합니다. 기본적으로 SPA는 2 계층 응용 프로그램을 사용 합니다. SPA 콘솔 UI 계층 및 비즈니스 논리 계층의 일부를 포함합니다. SPA 콘솔을 예약 하 고 성능 분석 요청을 처리 합니다.

**SPA 프레임 워크**

SPA는 두 개의 주요 부분, 프레임 워크 및 advisor 팩을 포함합니다. SPA 프레임 워크는 모든 사용자 인터페이스, 로그 처리 성능, 구성, 오류 처리 및, 데이터베이스 Api 및 관리 절차를 제공합니다.

**SPA 프로젝트**

SPA 프로젝트는 대상 서버, advisor 팩 및 advisor 팩에 대 한 대상 서버에서 생성 되는 성능 분석 보고서에 대 한 모든 정보를 포함 하는 데이터베이스. 비교 하 고 동일한 SPA 프로젝트 내에서 기록 및 추세 차트를 볼 수 있습니다. 사용자는 둘 이상의 프로젝트를 만들 수 있습니다. SPA 프로젝트를 서로 독립적 이며 프로젝트에서 공유 되는 데이터가 없습니다.

**대상 서버**

대상 서버는 물리적 컴퓨터 또는 IIS와 같은 특정 서버 역할을 갖는 Windows Server를 실행 하는 가상 컴퓨터입니다.

**데이터 분석 세션**

데이터 분석 세션은 특정 대상 서버에 대 한 성능 분석. 데이터 분석 세션 advisor 팩을 여러 개 포함할 수 있습니다. 이러한 advisor 팩에서 데이터 수집기 집합은 단일 데이터 수집기 집합으로 병합 됩니다. 단일 데이터 분석 세션에 대 한 모든 성능 로그는 동일한 시간 동안 수집 됩니다. 동일한 데이터 분석 세션에서 실행 되는 advisor 팩에 의해 생성 된 보고서를 분석 사용자가 전체 성능 상황을 이해 하 고 성능 문제에 대 한 근본 원인을 식별 하는 데 도움이 됩니다.

**Windows 용 이벤트 추적**

[이벤트 추적](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) ETW (Windows)는 Windows 운영 체제에서 제공 하는 고성능, 오버 헤드가 낮은, 확장 가능한 추적 시스템에 대 한 합니다. 프로 파일링 및 디버깅 다양 한 시나리오의 문제를 해결 하는 데 사용할 수 있는 기능을 제공 합니다. SPA 성능 보고서를 생성 하기 위한 데이터 원본으로 ETW 이벤트를 사용 합니다. ETW에 대 한 일반 정보를 참조 하십시오. [디버깅 및 ETW를 사용한 성능 조정 개선](https://msdn.microsoft.com/magazine/cc163437.aspx)합니다.

**WMI 쿼리**

Windows Management Instrumentation (WMI)는 관리 데이터와 Windows 운영 체제에서 작업에 대 한 인프라입니다. WMI 스크립트 또는 원격 컴퓨터에서 관리 작업을 자동화 하는 응용 프로그램을 작성할 수 있습니다. 또한 WMI는 운영 체제의 다른 부분에 및 제품 관리 데이터를 제공합니다. SPA 성능 보고서 생성에 소스로 WMI 클래스 정보 및 데이터 요소를 사용합니다.

**성능 카운터**

성능 카운터는 얼마나 잘 운영 체제 또는 응용 프로그램, 서비스 또는 드라이버는 수행 하는 방법에 대 한 정보를 제공 하는 데 사용 됩니다. 성능 카운터 데이터는 시스템 병목 현상을 확인 하 고 시스템 및 응용 프로그램 성능을 세부적으로 조정할 수 있습니다. 운영 체제, 네트워크 및 장치에 응용 프로그램에서 시스템 얼마나 잘 수행의 한 그래픽 뷰를 제공 하기 위해 사용할 수 있는 카운터 데이터를 제공 합니다. SPA를 사용 하 여 성능 카운터 정보 및 데이터 요소 원본으로 성능 보고서를 생성 합니다.

**성능 로그 및 경고**

성능 로그 및 경고 PLA ()는 Windows 운영 체제의 기본 제공 서비스입니다. 성능 로그 및 추적을 수집 하도록 설계 되었습니다 및 특정 트리거가 충족 될 때 성능 경고가 발생 합니다. 성능 카운터, 이벤트를 ETW (Windows), WMI 쿼리, 레지스트리 키 및 구성에 대 한 파일 추적을 수집 하도록 PLA는 사용할 수 있습니다. 또한 PLA 원격 프로시저 호출 (RPC)을 통해 원격 데이터 수집을 지원합니다. 사용자는 데이터를 수집, 데이터 컬렉션 빈도, 데이터 컬렉션 기간, 필터, 결과 파일을 저장할 위치에 대 한 정보를 포함 하는 데이터 수집기 집합을 정의 합니다. SPA PLA를 사용 하 여 대상 서버에서 모든 성능 데이터를 수집 합니다.

**단일 보고서**

단일 보고서는 단일 대상 서버에서 advisor 팩 하나에 대 한 하나의 데이터 분석 세션을 기반으로 생성 되는 SPA 보고서입니다. 알림 및 다양 한 데이터 섹션을 포함할 수 있습니다.

**Side-by-side-보고서**

Side-by-side-보고서에는 동일한 advisor 팩에 대 한 두 개의 단일 보고서를 비교 하는 SPA 보고서가입니다. 동일한 대상 서버에 별도 성능 분석 실행 또는 다른 대상 서버에서 두 개의 보고서를 생성할 수 있습니다. Side-by-side-보고서 비정상적인 동작이 나 보고서 중 하나에서 설정을 식별할 수 있도록 하는 두 개의 보고서를 비교 하는 기능을 만듭니다. 알림 및 다양 한 데이터 섹션 side-by-side-보고서에 포함 되어 있습니다. 각 섹션에서 두 보고서 데이터를에서 나열된 하 여 함께 합니다.

**추세 차트**

추세 차트에는 성능 문제의 반복적인 패턴을 조사 하는 데 사용 되는 SPA 보고서입니다. 매주 또는 매일 발생할 수 있는 클라이언트 컴퓨터 또는 서버에서 예약 된 서버 부하 변경 많은 반복적인 성능 문제 발생 됩니다. SPA는 24 시간 추세 차트 및 이러한 문제를 식별 하는 7 일 추세 차트를 제공 합니다.

사용자와 같은 단일 보고서 내에서 숫자 값은 한 번에 하나 이상의 데이터 계열을 선택할 수 **평균 총 CPU 사용량**합니다. 구체적으로 말하면, 숫자 값에는에서 주어진된 된 시간 인스턴스 단일 AP에서 생성 되는 단일 서버에서 스칼라 값이입니다. SPA (각 요일에 대 한 일 보고서의 경우 7)은 하루 중 각 시간에 대해 하나씩 24 그룹으로 해당 값을 그룹화합니다. SPA 평균, 최소값, 최대값 및 각 그룹에 대 한 표준 편차를 계산합니다.

**기록 차트**

기록 된 차트에는 시간이 지남에 따라 지정 된 서버 및 관리자 팩 쌍에 대 한 단일 보고서 내 특정 숫자 값에서 변경 내용을 표시 하는 데 사용 되는 SPA 보고서입니다. 사용자는 여러 데이터 계열을 선택 하 고 다른 데이터 계열 간의 상관 관계를 이해 하는 기록 차트에 함께 표시할 수 있습니다.

**데이터 계열**

데이터 계열에는 시간 동안 동일한 데이터 소스에서 수집 되는 숫자 데이터입니다. 동일한 소스에서 데이터에는 하나의 서버에서 IIS에 대 한 평균 요청 큐 길이 같은 동일한 대상 서버에서 온 것으로 의미 합니다.

**규칙**

규칙은 논리, 임계값 및 설명의 조합입니다. 잠재적인 성능 문제를 나타냅니다. 각 advisor 팩 규칙을 여러 개 포함 되어 있습니다. 각 규칙은 보고서 생성 프로세스에 의해 트리거됩니다. 규칙에 단일 보고서의 데이터에는 논리 및 임계값이 적용 됩니다. 조건에 해당 하는 경우에 경고 알림이 발생 합니다. 알림을로 설정 된 그렇지 않은 경우는 **확인** 상태입니다. 해당 사항 없음로 알림이 설정 되어 규칙이 적용 되지 않는 경우 (**NA**) 상태입니다.

**알림**

알림 규칙을 사용자에 게 표시 되는 정보입니다. 규칙의 상태를 포함 (**확인**, **NA**, 또는 **경고**), 이름, 규칙 및 성능 문제를 해결 하기 위해 가능한 권장 사항입니다.
