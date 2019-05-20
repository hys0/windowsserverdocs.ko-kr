---
title: Fsutil 동작
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.assetid: 84eaba2c-c0af-49e1-bbbd-2ed2928e5e4b
ms.openlocfilehash: 4593739f25c356e72ea39947c67f3e1301573137
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838274"
---
# <a name="fsutil-behavior"></a>Fsutil 동작

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

쿼리 또는 포함 된 NTFS 볼륨 동작을 설정 합니다.

-   8.3 문자 길이 파일 이름 생성

-   NTFS 볼륨에서 8.3 문자 길이가 짧은 파일 이름에서 확장 된 문자 사용

-   디렉터리는 NTFS 볼륨에 나열 되 면 마지막 액세스 시간 스탬프의 업데이트

-   빈도 할당량으로 이벤트 NTFS와 시스템 로그에 기록 됩니다 페이징 풀 및 NTFS 비페이징 풀 메모리 캐시 수준

-   영역의 크기를 마스터 파일 테이블 (MFT 영역)

-   시스템에서 NTFS 볼륨에 손상을 발견 될 때 데이터의 자동 삭제 합니다.

-   파일 삭제 알림 (라고도 trim 또는 매핑 해제)

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil behavior query {allowextchar | bugcheckoncorrupt | disable8dot3 [<VolumePath>] | disablecompression | disablecompressionlimit | disableencryption | disablefilemetadataoptimization | disablelastaccess | disablespotcorruptionhandling | disabletxf | disablewriteautotiering | encryptpagingfile | mftzone | memoryusage | quotanotify | symlinkevaluation | disabledeletenotify}

fsutil behavior set {allowextchar {1|0} | bugcheckoncorrupt {1|0} | disable8dot3 [ <Value> | [<VolumePath> {1|0}] ] | disablecompression {1|0} | disablecompressionlimit {1|0} | disableencryption {1|0} | disablefilemetadataoptimization {1|0} | disablelastaccess {1|0} | disablespotcorruptionhandling {1|0} | disabletxf {1|0} | disablewriteautotiering {1|0} | encryptpagingfile {1|0} | mftzone <Value> | memoryusage <Value> | quotanotify <Frequency> | symlinkevaluation <SymbolicLinkType> | disabledeletenotify {1|0}}
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|쿼리|파일 시스템 동작 매개 변수를 쿼리합니다.|
|집합|파일 시스템 동작 매개 변수를 변경합니다.|
|allowextchar {1 &#124; 0}|수 있습니다 (**1**) 하거나 허용 하지 않습니다 (**0**) 확장 문자에서는 문자 (분음 부호 문자 포함)로 설정 NTFS 볼륨에서 8.3 문자 길이가 짧은 파일 이름에 사용할 수 있습니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|Bugcheckoncorrupt {1 &#124; 0}|있습니다 (**1**) 하거나 허용 하지 않습니다 (**0**) NTFS 볼륨에 손상 된 경우 버그 검사를 생성 합니다. 이 기능은 NTFS 치유 NTFS 기능과 함께 사용할 때 데이터를 자동으로 삭제 되지 않도록 하려면 사용할 수 있습니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.<br /><br />이 매개 변수가 적용 됩니다.  Windows Server 2008 R2 및 Windows 7입니다.|
|disable8dot3 [<VolumePath>] {1&#124;0}|사용 하지 않도록 설정 (**1**)을 선택 하거나 (**0**) FAT 및 NTFS로 포맷 된 볼륨에서 8.3 문자 길이 파일 이름 생성 합니다. 필요에 따라 앞의 *VolumePath* 뒤에 콜론 또는 GUID 드라이브 이름으로 지정 합니다.|
|disablecompression {1 &#124; 0}|사용 하지 않도록 설정 **(1)** 을 선택 하거나 **(0)** NTFS 압축 합니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|disablecompressionlimit {1&#124;0}| 사용 하지 않도록 설정 **(1)** 을 선택 하거나 **(0)** NTFS 볼륨에서 NTFS 압축 제한 합니다. 압축된 된 파일에서 파일을 확장 하는 데 실패 하는 것이 아니라 조각화의 특정 수준에 도달 하면 NTFS 압축 파일의 추가 익스텐트를 중지 합니다. 이 작업은 압축된 파일을 평소 보다 클 수 있도록 수행 되었습니다. 시스템의 파일로 압축의 크기를 제한 하는이 기능 TRUE 사용 하지 않도록 설정 하려면이 값을 설정 합니다. 이 기능을 사용 하지 않도록 설정 하는 것은 좋지 않습니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|disableencryption {1 &#124; 0}|사용 하지 않도록 설정 **(1)** 을 선택 하거나 **(0)** NTFS 볼륨에서 파일과 폴더를 암호화 합니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|disablefilemetadataoptimization {1&#124;0}|사용 하지 않도록 설정 **(1)** 을 선택 하거나 **(0)** 파일 메타 데이터를 최적화 합니다. NTFS의 제한은 얼마나 많은 익스텐트에 지정 된 파일을 가질 수 있습니다. 압축 및 예비 부품 파일 매우 조각화 될 수 있습니다. 기본적으로 NTFS 보다 조각화 된 파일 수 있도록 해당 내부 메타 데이터 구조를 주기적으로 압축 합니다. 이 내부 최적화 TRUE 사용 하지 않도록 설정 하려면이 값을 설정 합니다. 이 기능을 사용 하지 않도록 설정 하는 것은 좋지 않습니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|disablelastaccess {1 &#124; 0}|사용 하지 않도록 설정 (**1**)을 선택 하거나 (**0**) 디렉터리가 NTFS 볼륨에 나열 될 때 액세스 타임 스탬프가 각 디렉터리에 마지막으로 업데이트 합니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|disablespotcorruptionhandling {1&#124;0}|사용 하지 않도록 설정 **(1)** 을 선택 하거나 **(0)** 스폿 손상 처리 합니다. Windows 8 및 Windows Server 2012에 도입 된 새로운 기능 중 하나는 새로운 고가용성 형태의 CHKDSK입니다. 이 기능에는 시스템 관리자가 오프 라인으로 전환 하지 않고 볼륨의 상태를 분석 하는 CHKDSK를 실행할 수 있습니다. 이 기능을 사용 하지 않도록 설정 하는 것은 좋지 않습니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|disabletxf {1&#124;0}|사용 하지 않도록 설정 **(1)** 을 선택 하거나 **(0)** 지정한 NTFS 볼륨에서 txf 합니다. TxF는 파일 시스템 작업에 대 한 의미 체계와 같은 트랜잭션 제공 하는 NTFS 기능입니다. TxF는 deprected 현재 기능은 여전히 사용할 수 있습니다. C: 볼륨에서이 기능을 사용 하지 않도록 설정 하는 것은 좋지 않습니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|disablewriteautotiering {1&#124;0}|ReFS v2 자동 계층화 된 볼륨에 대 한 계층화 논리를 사용 하지 않도록 설정 합니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|encryptpagingfile {1&#124;0}|암호화 (**1**) 또는 암호화 되지 않습니다 (**0**) Windows 운영 체제에서 메모리 페이징 파일입니다.<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|mftzone <Value>|MFT 영역의 크기를 설정 하 고 200 MB 단위의 배수로 표현 됩니다. 설정할 *값* 에서 숫자로 **1** (기본값은 200MB)를 **4** (최대값은 800MB).<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|memoryusage <Value>|내부 캐시 수준의 NTFS 페이징 풀 메모리 및 NTFS 비페이징된 풀 메모리를 구성합니다. 로 설정 **1** 또는 **2**합니다. 로 설정 하면 **1** (기본값), NTFS 페이징 풀 메모리의 기본 크기를 사용 합니다. 로 설정 하면 **2**, NTFS 할당 준비 목록 및 메모리 임계값 크기를 늘립니다. (할당 준비 목록에는 전용 메모리 캐시 파일 읽기와 같은 파일 시스템 작업에 대 한 커널 및 장치 드라이버를 만들 수는 고정 크기 메모리 버퍼의 풀입니다.)<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|quotanotify <Frequency>|NTFS 할당량 위반 시스템 로그에 보고 되는 빈도 구성 합니다. 유효한 값은 범위는 0-4294967295입니다. 기본 빈도 3600 초 (1 시간).<br /><br />이 매개 변수를 적용에 대 한 컴퓨터를 다시 시작 해야 합니다.|
|symlinkevaluation <SymbolicLinkType>|컴퓨터에 만들 수 있는 바로 가기 링크의 종류를 제어 합니다. 유효한 선택할 수 있습니다.<br /><br />1.  로컬 기호화 된 링크를 L2L 로컬: {0 &#124; 1을 (를)<br />2.  원격 기호화 된 링크를 L2R 로컬: {0 &#124; 1을 (를)<br />3.  원격 위치에 로컬 기호화 된 링크를 R2R: {0 &#124; 1을 (를)<br />4.  원격 위치에 원격 기호화 된 링크를 R2L: {0 &#124; 1을 (를)|
|DisableDeleteNotify|사용 하지 않도록 설정 \( **1** \) 을 선택 하거나 \( **0** \) 알림을 삭제 합니다. 알림 삭제 \(trim 또는 매핑 해제 라고도\) 파일로 인해 해제 된 클러스터의 기본 저장 장치에 게 알려 주는 기능 작업을 삭제 합니다. 이 밖에도 다음 지침을 따릅니다.<br /><br />-ReFS를 사용 하 여 시스템에 대 한 trim v2는 기본적으로 비활성화 됩니다. Windows Server 2016에 적용 됩니다.<br />-ReFS를 사용 하 여 시스템에 대 한 trim v1은 기본적으로 사용 됩니다. Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016에 적용 됩니다.<br />-NTFS를 사용 하 여 시스템에 대 한 trim는 비활성화할 경우 관리자가 아니면 기본적으로 사용 됩니다.<br />-하드 디스크 드라이브 또는 SAN 보고 하는 경우 trim을 지원 하지 않습니다 다음 하드 디스크 드라이브와 San에 trim 알림을 받지 않습니다.<br />-설정 또는 해제를 다시 시작 하지 않아도 됩니다.<br />-Trim는 다음 명령을 매핑을 해제 하는 경우 발생 합니다.<br />-기존 처리 중인 IO 레지스트리 변경의 영향을 받지 않습니다.<br />-하지 않아도 모든 서비스를 다시 시작 하거나 하면 trim을 사용 하지 않도록 설정 됩니다.<br /><br />이 매개 변수는 Windows Server 2008 R2 및 Windows 7에서 도입 되었습니다. | 

## <a name="remarks"></a>설명

-   MFT 영역이 마스터 파일 테이블 (MFT)를 MFT 조각화를 방지 하기 위해 필요에 따라 확장할 수 있도록 예약된 된 영역입니다. 볼륨의 평균 파일 크기는 2KB 또는 이하인 것이 좋습니다 설정 하는 경우는 **mftzone** 값 2입니다. 볼륨에는 평균 파일 크기는 1KB 또는 이하인 것이 좋습니다 설정 하는 경우는 **mftzone** 4 사이의 값입니다.

-   때 **disable8dot3** 로 설정 된 **0**, 때마다 긴 파일 이름으로 파일을 만들면, NTFS 8.3 문자 길이 파일 이름에는 있는 두 번째 파일 항목을 만듭니다. NTFS 파일 디렉터리에서를 만들 때 긴 파일 이름과 연관 된 8.3 문자 길이 파일 이름 조회 해야 합니다. 이 매개 변수를 업데이트 합니다 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation** 레지스트리 키입니다.

-   합니다 **allowextchar** 매개 변수 업데이트는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsAllowExtendedCharacterIn8dot3Name** 레지스트리 키입니다.

-   **disablelastaccess** 매개 변수 파일 및 디렉터리에 마지막 액세스 시간 스탬프에 로깅 업데이트의 피해를 줄일 수 있습니다. 사용 하지 않도록 설정 된 **마지막 액세스 시간** 기능은 파일 및 디렉터리 액세스의 속도 향상 시킵니다. 이 매개 변수를 업데이트 합니다 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate** 레지스트리 키입니다.

    참고:

    -   파일 기반 **마지막 액세스 시간** 쿼리는 모든 디스크에 값을 현재 없는 경우에 정확 하 게 합니다. NTFS는 정확한 값은 메모리에 저장 되므로 쿼리에 올바른 값을 반환 합니다.

    -   1 시간 동안은 NTFS 업데이트할 때 지연 시간의 최대 **마지막 액세스 시간** 디스크에 있습니다. NTFS와 같은 파일 특성을 업데이트 하는 경우 **마지막 수정 시간**, 및 **마지막 액세스 시간** 업데이트 보류 중, NTFS 업데이트는 **마지막 액세스 시간** 추가 성능 영향을 주지 않고 다른 업데이트와 합니다.

    -   **disablelastaccess** 매개 변수는이 기능을 사용 하는 백업 및 원격 저장소와 같은 프로그램에 영향을 줄 수 있습니다.

-   실제 메모리를 늘려 NTFS로 사용할 수 있는 페이지 풀 메모리의 양을 항상 증가 하지 않습니다. 설정 **memoryusage** 에 **2** 페이징된 풀 메모리 한도를 발생 시킵니다. 이렇게 시스템을 열고 및 설정 하 고 사용 하지 않는 이미 많은 양의 시스템 메모리 캐시 메모리 또는 다른 응용 프로그램에 대 한 동일한 파일에 많은 파일을 닫는 경우 성능이 향상 될 수 있습니다. 컴퓨터에서 이미 사용 중인 많은 양의 시스템 메모리 캐시 메모리 또는 다른 응용 프로그램, NTFS의 제한을 늘려 페이징 고 비페이징 풀 메모리가 다른 프로세스에 대 한 사용 가능한 풀 메모리의 양이 줄어듭니다. 이 전체 시스템 성능이 저하 될 수 있습니다. 이 매개 변수를 업데이트 합니다 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsMemoryUsage** 레지스트리 키입니다.

-   에 지정 된 값은 **mftzone** 매개 변수는 mft MFT 영역에 새 볼륨의 초기 크기의 추정치 이며 각 파일 시스템 탑재 시 설정 됩니다. NTFS 볼륨에 공간을 사용 하면 다음 MFT 확장에 대 한 예약 된 공간을 조정 합니다. MFT 영역이 이미 큰, 전체 MFT 영역 크기 다시 예약 되지 않습니다. MFT 영역 MFT의 끝을 지난 인접 한 범위를 기반으로 하므로 공간을 사용 하는 대로 축소 합니다.

    파일 시스템 현재 MFT 영역을 완전히 사용할 때까지 새 MFT 영역 위치를 확인 하지 않습니다. 이 발생 하지 않으며 일반적인 시스템 note 합니다.

-   삭제 알림 기능이 설정 된 경우 일부 장치에서 성능 저하가 발생할 수 있습니다. 이 경우에 사용 된 **disabledeletenotify** 옵션 알림 기능을 해제 합니다.

### <a name="BKMK_examples"></a>예제
{928842df-5a01-11de-a85c-806e6f6e6963} GUID를 가진 지정 된 디스크 볼륨에 대 한 사용 안 함 8.3 형식이 이름 동작에 대 한 쿼리를 입력 합니다.

```
fsutil behavior query disable8dot3 Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

사용 하 여 8.3 형식이 이름 동작을 쿼리할 수도 있습니다는 **8dot3name** 하위 명령입니다.

TRIM가 설정 하는 경우에 시스템을 쿼리하려면 다음을 입력 합니다.

```
fsutil behavior query DisableDeleteNotify
```
다음과 유사한 출력이 생성 됩니다.

    NTFS DisableDeleteNotify = 1
    ReFS DisableDeleteNotify is not currently set

TRIM에 대 한 기본 동작을 재정의할 \(disabledeletenotify\) ReFS v2에 대 한 입력:

```
fsutil behavior set DisableDeleteNotify ReFS 0
```

TRIM에 대 한 기본 동작을 재정의할 \(disabledeletenotify\) NTFS 및 ReFS v1에 대 한 입력:
```
fsutil behavior set DisableDeleteNotify 1
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[Fsutil 8dot3name](Fsutil-8dot3name.md)


