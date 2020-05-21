---
title: fsutil behavior
description: NTFS 볼륨 동작을 쿼리하거나 설정 하는 fsutil behavior 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.topic: article
ms.date: 10/16/2017
ms.assetid: 84eaba2c-c0af-49e1-bbbd-2ed2928e5e4b
ms.openlocfilehash: f1196169ea1d198c4855f06edef542ef34876a2a
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436008"
---
# <a name="fsutil-behavior"></a>fsutil behavior

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

쿼리 또는 포함 된 NTFS 볼륨 동작을 설정 합니다.

- 8.3 문자 길이 파일 이름 만들기

- NTFS 볼륨에서 문자 길이의 짧은 파일 이름 8.3에서 문자 사용을 확장 합니다.

- 디렉터리가 NTFS 볼륨에 나열 될 때 **마지막 액세스 타임** 스탬프 업데이트

- 할당량 이벤트가 시스템 로그와 NTFS 페이징 풀 및 NTFS 비페이징 풀 메모리 캐시 수준에 기록 되는 빈도입니다.

- 마스터 파일 테이블 영역 (MFT 영역)의 크기입니다.

- 시스템에서 NTFS 볼륨에 손상을 발견 될 때 데이터의 자동 삭제 합니다.

- 파일-삭제 알림 (trim 또는 매핑 해제 라고도 함)

## <a name="syntax"></a>구문

```
fsutil behavior query {allowextchar | bugcheckoncorrupt | disable8dot3 [<volumepath>] | disablecompression | disablecompressionlimit | disableencryption | disablefilemetadataoptimization | disablelastaccess | disablespotcorruptionhandling | disabletxf | disablewriteautotiering | encryptpagingfile | mftzone | memoryusage | quotanotify | symlinkevaluation | disabledeletenotify}

fsutil behavior set {allowextchar {1|0} | bugcheckoncorrupt {1|0} | disable8dot3 [ <value> | [<volumepath> {1|0}] ] | disablecompression {1|0} | disablecompressionlimit {1|0} | disableencryption {1|0} | disablefilemetadataoptimization {1|0} | disablelastaccess {1|0} | disablespotcorruptionhandling {1|0} | disabletxf {1|0} | disablewriteautotiering {1|0} | encryptpagingfile {1|0} | mftzone <Value> | memoryusage <Value> | quotanotify <frequency> | symlinkevaluation <symboliclinktype> | disabledeletenotify {1|0}}
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| Query | 파일 시스템 동작 매개 변수를 쿼리합니다. |
| set | 파일 시스템 동작 매개 변수를 변경합니다. |
| allowextchar`{1|0}` | NTFS 볼륨의 8.3 문자 길이 짧은 파일 이름에 사용 되는 확장 문자 집합 (예를 들어,**0****)의**문자를 허용 하거나 허용 하지 않습니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| 잘못 된 checkon손상`{1|0}` | NTFS 볼륨에 손상이 있는 경우 (**1**) 또는 (**0**) 버그 확인 생성을 허용 하지 않습니다. 이 기능을 사용 하면 자동 복구 NTFS 기능과 함께 사용 하는 경우 NTFS에서 자동으로 데이터를 삭제 하지 않도록 방지할 수 있습니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| disable8dot3 [ <volumepath> ]`{1|0}` | (**1**)을 사용 하지 않도록 설정 하거나 (**0**) FAT 및 NTFS 형식 볼륨에서 8.3 문자 길이 파일 이름을 만듭니다. 필요에 따라 *volumepath* 를 사용 하 여 드라이브 이름 뒤에 콜론 또는 GUID를 지정 하 여 접두사를 지정 합니다. |
| disablecompression`{1|0}` | **(1)** 또는 **(0)** NTFS 압축을 사용 하지 않도록 설정 합니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| disablecompressionlimit`{1|0}` | NTFS 볼륨에 대해 ( **1)** 또는 **(0)** ntfs 압축 제한을 사용 하지 않도록 설정 합니다. 압축 된 파일이 파일을 확장 하는 데 실패 하는 대신 특정 수준의 조각화에 도달 하면 NTFS는 파일의 추가 익스텐트 압축을 중지 합니다. 압축 된 파일이 일반적으로 보다 커질 수 있도록 하기 위해 수행 되었습니다. 이 값을 **TRUE** 로 설정 하면이 기능을 사용 하지 않도록 설정 하 여 시스템의 압축 파일 크기를 제한 합니다. 이 기능을 사용 하지 않도록 설정 하는 것은 권장 되지 않습니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| disableencryption`{1|0}` | **(1)** 을 사용 하지 않도록 설정 하거나 **(0)** NTFS 볼륨의 폴더 및 파일 암호화를 사용 하도록 설정 합니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| disablefilemetadataoptimization`{1|0}` | **(1)** 을 사용 하지 않도록 설정 하거나 **(0)** 파일 메타 데이터 최적화를 사용 하도록 설정 합니다. NTFS에는 지정 된 파일에 포함 될 수 있는 익스텐트의 수에 대 한 제한이 있습니다. 압축 된 파일 및 스파스 파일은 매우 조각화 될 수 있습니다. 기본적으로 NTFS는 더 많은 조각난 파일을 허용 하도록 내부 메타 데이터 구조를 정기적으로 압축 합니다. 이 값을 **TRUE** 로 설정 하면이 내부 최적화를 사용 하지 않습니다. 이 기능을 사용 하지 않도록 설정 하는 것은 권장 되지 않습니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| disablelastaccess`{1|0}` | 디렉터리가 NTFS 볼륨에 나열 될 때 (**1**)를 사용 하지 않도록 설정 하거나 (**0**) 각 디렉터리의 마지막 액세스 타임 스탬프에 대 한 업데이트를 사용 하도록 설정 합니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| disablespotcorruptionhandling`{1|0}` | **(1)** 또는 **(0)** 스폿 손상 처리를 사용 하지 않도록 설정 합니다. 또한 시스템 관리자가 CHKDSK를 실행 하 여 볼륨을 오프 라인으로 전환 하지 않고도 볼륨 상태를 분석할 수 있습니다. 이 기능을 사용 하지 않도록 설정 하는 것은 권장 되지 않습니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| disabletxf`{1|0}` | 지정 된 NTFS 볼륨에서 ( **1)** 또는 **(0)** txf를 사용 하지 않도록 설정 합니다. TxF는 파일 시스템 작업에 대 한 의미 체계와 같은 트랜잭션을 제공 하는 NTFS 기능입니다. TxF는 현재 사용 되지 않지만 기능을 계속 사용할 수 있습니다. C: 볼륨에서는이 기능을 사용 하지 않는 것이 좋습니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| disablewriteautotiering`{1|0}` | 계층화 된 볼륨에 대해 ReFS v2 자동 계층화 논리를 사용 하지 않도록 설정 합니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| encryptpagingfile`{1|0}` | 는 (**1**)을 암호화 하거나 Windows**0**운영 체제의 메모리 페이징 파일을 암호화 하지 않습니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| mftzone`<value>` | MFT 영역의 크기를 설정 하 고 200 MB 단위의 배수로 표현 됩니다. *값* 을 **1** (기본값은 200 mb)에서 **4** (최대 800 mb) 사이의 숫자로 설정 합니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| memoryusage`<value>` | NTFS 페이징 풀 메모리 및 NTFS 비페이징 풀 메모리의 내부 캐시 수준을 구성 합니다. 로 설정 **1** 또는 **2**합니다. **1** (기본값)로 설정 된 경우 NTFS는 기본 크기의 페이징 풀 메모리를 사용 합니다. 로 설정 하면 **2**, NTFS 할당 준비 목록 및 메모리 임계값 크기를 늘립니다. 할당 준비 list는 파일 읽기와 같은 파일 시스템 작업을 위해 커널 및 장치 드라이버가 전용 메모리 캐시로 만드는 고정 크기 메모리 버퍼의 풀입니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| quotanotify`<frequency>` | NTFS 할당량 위반 시스템 로그에 보고 되는 빈도 구성 합니다. 에 유효한 값은 **0-4294967295**범위에 있습니다. 기본 빈도는 **3600** 초 (1 시간)입니다.<p>이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다. |
| symlinkevaluation`<symboliclinktype>` | 컴퓨터에 만들 수 있는 바로 가기 링크의 종류를 제어 합니다. 유효한 선택할 수 있습니다.<ul><li>**1** -로컬 기호화 된 링크`L2L:{0|1}`</li><li>**2** -로컬에서 원격 기호화 된 링크,`L2R:{1|0}`</li><li>**3** -원격에서 로컬 기호화 된 링크`R2R:{1|0}`</li><li>**4** -원격에서 원격 기호화 된 링크,`R2L:{1|0}`</li></ul> |
| disabledeletenotify | (**1**) 또는 (**0**) 삭제 알림을 사용 하지 않도록 설정 합니다. 삭제 알림 (trim 또는 매핑 해제 라고도 함)은 파일 삭제 작업으로 인해 해제 된 클러스터의 기본 저장 장치에 알리는 기능입니다. 이 밖에도 다음 지침을 따릅니다.<ul><li>ReFS v2를 사용 하는 시스템의 경우 trim은 기본적으로 사용 되지 않습니다.</li><li>ReFS v1을 사용 하는 시스템의 경우 trim은 기본적으로 사용 하도록 설정 됩니다.</li><li>NTFS를 사용 하는 시스템의 경우, 관리자가 사용 하지 않도록 설정 하지 않는 한 trim은 기본적으로 사용 됩니다.</li><li>하드 디스크 드라이브 또는 SAN에서 트리밍을 지원 하지 않는 것으로 보고 하는 경우 하드 디스크 드라이브 및 San에서 트리밍 알림을 받지 않습니다.</li><li>를 사용 하거나 사용 하지 않도록 설정 하면 다시 시작이 필요 하지 않습니다.</li><li>Trim은 다음 매핑 해제 명령이 실행 될 때 적용 됩니다.</li><li>기존 처리 중인 IO는 레지스트리 변경의 영향을 받지 않습니다.</li><li>Trim을 사용 하거나 사용 하지 않도록 설정 하는 경우 서비스를 다시 시작 하지 않아도 됩니다.</li></ul> |

#### <a name="remarks"></a>설명

- MFT 영역은 mft 조각화를 방지 하기 위해 필요에 따라 MFT (마스터 파일 테이블)를 확장할 수 있는 예약 영역입니다. 볼륨의 평균 파일 크기가 2kb 이하인 경우 **mftzone** 값을 **2**로 설정 하는 것이 유용할 수 있습니다. 볼륨의 평균 파일 크기가 1kb 이하인 경우 **mftzone** 값을 **4**로 설정 하는 것이 유용할 수 있습니다.

- **Disable8dot3** 을 **0**으로 설정 하면 긴 파일 이름으로 파일을 만들 때마다 NTFS에서 8.3 문자 길이 파일 이름이 있는 두 번째 파일 항목을 만듭니다. NTFS는 디렉터리에 파일을 만들 때 긴 파일 이름과 연결 된 8.3 문자 길이 파일 이름을 조회 해야 합니다. 이 매개 변수는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation** 레지스트리 키를 업데이트 합니다.

- **Allowextchar** 매개 변수는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsAllowExtendedCharacterIn8dot3Name** 레지스트리 키를 업데이트 합니다.

- **Disablelastaccess** 매개 변수를 사용 하면 파일 및 디렉터리에 대 한 **마지막 액세스 타임** 스탬프에 대 한 로깅 업데이트의 영향을 줄일 수 있습니다. 사용 하지 않도록 설정 된 **마지막 액세스 시간** 기능은 파일 및 디렉터리 액세스의 속도 향상 시킵니다. 이 매개 변수는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate** 레지스트리 키를 업데이트 합니다.

    **참고:**

    - 모든 디스크 값이 최신이 아닌 경우에도 파일 기반 **마지막 액세스 시간** 쿼리는 정확 합니다. NTFS는 정확한 값은 메모리에 저장 되므로 쿼리에 올바른 값을 반환 합니다.

    - 1 시간은 NTFS에서 디스크에 대 한 **마지막 액세스 시간** 업데이트를 지연 시킬 수 있는 최대 시간입니다. NTFS와 같은 파일 특성을 업데이트 하는 경우 **마지막 수정 시간**, 및 **마지막 액세스 시간** 업데이트 보류 중, NTFS 업데이트는 **마지막 액세스 시간** 추가 성능 영향을 주지 않고 다른 업데이트와 합니다.

    - **Disablelastaccess** 매개 변수는이 기능을 사용 하는 백업 및 원격 저장소와 같은 프로그램에 영향을 줄 수 있습니다.

- 실제 메모리를 늘리면 항상 NTFS에서 사용할 수 있는 페이징 풀 메모리의 양이 증가 하지 않습니다. 설정 **memoryusage** 에 **2** 페이징된 풀 메모리 한도를 발생 시킵니다. 시스템이 동일한 파일 집합에서 많은 파일을 열고 닫고 다른 앱 또는 캐시 메모리에 대해 많은 양의 시스템 메모리를 사용 하 고 있지 않은 경우 성능이 향상 될 수 있습니다. 컴퓨터에서 다른 앱 이나 캐시 메모리에 대해 많은 양의 시스템 메모리를 이미 사용 하 고 있는 경우, NTFS 페이징 및 비페이징 풀 메모리 제한을 높이면 다른 프로세스에 대해 사용 가능한 풀 메모리가 줄어듭니다. 이 전체 시스템 성능이 저하 될 수 있습니다. 이 매개 변수는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsMemoryUsage** 레지스트리 키를 업데이트 합니다.

- 에 지정 된 값은 **mftzone** 매개 변수는 mft MFT 영역에 새 볼륨의 초기 크기의 추정치 이며 각 파일 시스템 탑재 시 설정 됩니다. NTFS 볼륨에 공간을 사용 하면 다음 MFT 확장에 대 한 예약 된 공간을 조정 합니다. MFT 영역이 이미 큰, 전체 MFT 영역 크기 다시 예약 되지 않습니다. MFT 영역 MFT의 끝을 지난 인접 한 범위를 기반으로 하므로 공간을 사용 하는 대로 축소 합니다.

    현재 MFT 영역을 완전히 사용할 때까지 파일 시스템에서 새 MFT 영역 위치를 확인 하지 않습니다. 이 발생 하지 않으며 일반적인 시스템 note 합니다.

- 삭제 알림 기능이 설정 된 경우 일부 디바이스에서 성능 저하가 발생할 수 있습니다. 이 경우에 사용 된 **disabledeletenotify** 옵션 알림 기능을 해제 합니다.

### <a name="examples"></a>예

GUID, {928842df-5a01-11de-a85c-806e6f6e6963}를 사용 하 여 지정 된 디스크 볼륨에 대 한 8.3 이름 사용 안 함 동작을 쿼리하려면 다음을 입력 합니다.

```
fsutil behavior query disable8dot3 volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

사용 하 여 8.3 형식이 이름 동작을 쿼리할 수도 있습니다는 **8dot3name** 하위 명령입니다.

TRIM가 설정 하는 경우에 시스템을 쿼리하려면 다음을 입력 합니다.

```
fsutil behavior query DisableDeleteNotify
```

그러면 다음과 유사한 출력이 생성 됩니다.

```
NTFS DisableDeleteNotify = 1
ReFS DisableDeleteNotify is not currently set
```

ReFS v2의 TRIM (disabledeletenotify)에 대 한 기본 동작을 재정의 하려면 다음을 입력 합니다.

```
fsutil behavior set disabledeletenotify ReFS 0
```

NTFS 및 ReFS v1의 TRIM (disabledeletenotify)에 대 한 기본 동작을 재정의 하려면 다음을 입력 합니다.

```
fsutil behavior set disabledeletenotify 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [fsutil 8dot3name](fsutil-8dot3name.md)
