---
title: Fsutil 동작
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.assetid: 84eaba2c-c0af-49e1-bbbd-2ed2928e5e4b
ms.openlocfilehash: 3ad6ad8d31bbcb4e9c70192efda37a9836eac14b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377017"
---
# <a name="fsutil-behavior"></a>Fsutil 동작

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

쿼리 또는 포함 된 NTFS 볼륨 동작을 설정 합니다.

-   8\.3 문자 길이 파일 이름 생성

-   NTFS 볼륨의 8.3 문자 길이 짧은 파일 이름에 확장 문자 사용

-   디렉터리는 NTFS 볼륨에 나열 되 면 마지막 액세스 시간 스탬프의 업데이트

-   할당량 이벤트가 시스템 로그에 기록 되는 빈도 및 NTFS 페이징 풀 및 NTFS 비페이징 풀 메모리 캐시 수준

-   마스터 파일 테이블 영역의 크기 (MFT 영역)

-   시스템에서 NTFS 볼륨에 손상을 발견 될 때 데이터의 자동 삭제 합니다.

-   파일 삭제 알림 (trim 또는 매핑 해제 라고도 함)

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil behavior query {allowextchar | bugcheckoncorrupt | disable8dot3 [<VolumePath>] | disablecompression | disablecompressionlimit | disableencryption | disablefilemetadataoptimization | disablelastaccess | disablespotcorruptionhandling | disabletxf | disablewriteautotiering | encryptpagingfile | mftzone | memoryusage | quotanotify | symlinkevaluation | disabledeletenotify}

fsutil behavior set {allowextchar {1|0} | bugcheckoncorrupt {1|0} | disable8dot3 [ <Value> | [<VolumePath> {1|0}] ] | disablecompression {1|0} | disablecompressionlimit {1|0} | disableencryption {1|0} | disablefilemetadataoptimization {1|0} | disablelastaccess {1|0} | disablespotcorruptionhandling {1|0} | disabletxf {1|0} | disablewriteautotiering {1|0} | encryptpagingfile {1|0} | mftzone <Value> | memoryusage <Value> | quotanotify <Frequency> | symlinkevaluation <SymbolicLinkType> | disabledeletenotify {1|0}}
```

## <a name="parameters"></a>매개 변수

|                 매개 변수                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                   쿼리                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            파일 시스템 동작 매개 변수를 쿼리합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|                    집합                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            파일 시스템 동작 매개 변수를 변경합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|          allowextchar {1 &#124; 0}           |                                                                                                                                                                                                                                                                                                                                                                                                                                  NTFS 볼륨의 8.3 문자 길이 짧은 파일 이름에 사용 되는 확장 문자 집합 (예를 들어,**0** **)의**문자를 허용 하거나 허용 하지 않습니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|        Bugcheckoncorrupt {1 &#124; 0}        |                                                                                                                                                                                                                                                                                                                                                                      NTFS 볼륨에 손상이 있는 경우 (**1**) 또는 (**0**) 버그 확인 생성을 허용 하지 않습니다. 이 기능을 사용 하면 자동 복구 NTFS 기능과 함께 사용 하는 경우 NTFS에서 자동으로 데이터를 삭제 하지 않도록 방지할 수 있습니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.<br /><br />이 매개 변수는 다음에 적용 됩니다.  Windows Server 2008 R2 및 Windows 7                                                                                                                                                                                                                                                                                                                                                                      |
|   disable8dot3 [<VolumePath>] {1&#124;0}   |                                                                                                                                                                                                                                                                                                                                                                                                                                                       (**1**)을 사용 하지 않도록 설정 하거나 (**0**) FAT 및 NTFS 형식 볼륨에서 8.3 문자 길이 파일 이름을 만듭니다. 필요에 따라 앞의 *VolumePath* 뒤에 콜론 또는 GUID 드라이브 이름으로 지정 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|       disablecompression {1 &#124; 0}        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 **(1)** 또는 **(0)** NTFS 압축을 사용 하지 않도록 설정 합니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|     disablecompressionlimit {1&#124;0}     |                                                                                                                                                                                                                                                                                   NTFS 볼륨에 대해 ( **1)** 또는 **(0)** ntfs 압축 제한을 사용 하지 않도록 설정 합니다. 압축 된 파일이 파일을 확장 하는 데 실패 하는 대신 특정 수준의 조각화에 도달 하면 NTFS는 파일의 추가 익스텐트 압축을 중지 합니다. 압축 된 파일이 일반적으로 보다 커질 수 있도록 하기 위해 수행 되었습니다. 이 값을 TRUE로 설정 하면이 기능을 사용 하지 않도록 설정 하 여 시스템의 압축 파일 크기를 제한 합니다. 이 기능은 사용 하지 않는 것이 좋습니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                   |
|        disableencryption {1 &#124; 0}        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                **(1)** 을 사용 하지 않도록 설정 하거나 **(0)** NTFS 볼륨의 폴더 및 파일 암호화를 사용 하도록 설정 합니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| disablefilemetadataoptimization {1&#124;0} |                                                                                                                                                                                                                                                                                                                      **(1)** 을 사용 하지 않도록 설정 하거나 **(0)** 파일 메타 데이터 최적화를 사용 하도록 설정 합니다. NTFS에는 지정 된 파일에 포함 될 수 있는 익스텐트의 수에 대 한 제한이 있습니다. 압축 및 예비 파일은 매우 조각화 될 수 있습니다. 기본적으로 NTFS는 더 많은 조각난 파일을 허용 하도록 내부 메타 데이터 구조를 정기적으로 압축 합니다. 이 값을 TRUE로 설정 하면이 내부 최적화를 사용 하지 않습니다. 이 기능은 사용 하지 않는 것이 좋습니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                       |
|        disablelastaccess {1 &#124; 0}        |                                                                                                                                                                                                                                                                                                                                                                                                                                                       디렉터리가 NTFS 볼륨에 나열 될 때 (**1**)를 사용 하지 않도록 설정 하거나 (**0**) 각 디렉터리의 마지막 액세스 타임 스탬프에 대 한 업데이트를 사용 하도록 설정 합니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|  disablespotcorruptionhandling {1&#124;0}  |                                                                                                                                                                                                                                                                                                                                                    **(1)** 또는 **(0)** 스폿 손상 처리를 사용 하지 않도록 설정 합니다. Windows 8 및 Windows Server 2012에 도입 된 새로운 기능 중 하나는 CHKDSK의 새로운 고가용성 형식입니다. 이 기능을 사용 하면 시스템 관리자가 CHKDSK를 실행 하 여 볼륨을 오프 라인으로 전환 하지 않고도 볼륨 상태를 분석할 수 있습니다. 이 기능은 사용 하지 않는 것이 좋습니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                    |
|           disabletxf {1&#124;0}            |                                                                                                                                                                                                                                                                                                                                                                         지정 된 NTFS 볼륨에서 ( **1)** 또는 **(0)** txf를 사용 하지 않도록 설정 합니다. TxF는 파일 시스템 작업에 대 한 의미 체계와 같은 트랜잭션을 제공 하는 NTFS 기능입니다. 현재는 기능을 계속 사용할 수 있지만 TxF는 현재 deprected 됩니다. C: 볼륨에서는이 기능을 사용 하지 않는 것이 좋습니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                          |
|     disablewriteautotiering {1&#124;0}     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                계층화 된 볼륨에 대해 ReFS v2 자동 계층화 논리를 사용 하지 않도록 설정 합니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|        encryptpagingfile {1&#124;0}        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                          는 (**1**)을 암호화 하거나 Windows 운영 체제의 메모리 페이징 파일을 암호화 하지 않습니다 (**0**).<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|              mftzone <Value>               |                                                                                                                                                                                                                                                                                                                                                                                                                                           MFT 영역의 크기를 설정 하 고 200 MB 단위의 배수로 표현 됩니다. *값* 을 **1** (기본값은 200 mb)에서 **4** (최대 800 mb) 사이의 숫자로 설정 합니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|            memoryusage <Value>             |                                                                                                                                                                                                                                                                                   NTFS 페이징 풀 메모리 및 NTFS 비페이징 풀 메모리의 내부 캐시 수준을 구성 합니다. 로 설정 **1** 또는 **2**합니다. **1** (기본값)로 설정 된 경우 NTFS는 기본 크기의 페이징 풀 메모리를 사용 합니다. 로 설정 하면 **2**, NTFS 할당 준비 목록 및 메모리 임계값 크기를 늘립니다. 할당 준비 list는 파일 읽기와 같은 파일 시스템 작업을 위해 커널 및 장치 드라이버가 전용 메모리 캐시로 만드는 고정 크기 메모리 버퍼의 풀입니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                   |
|          quotanotify <Frequency>           |                                                                                                                                                                                                                                                                                                                                                                                                                                  NTFS 할당량 위반 시스템 로그에 보고 되는 빈도 구성 합니다. 유효한 값은 범위는 0-4294967295입니다. 기본 빈도는 3600 초 (1 시간)입니다.<br /><br />이 매개 변수를 적용 하려면 컴퓨터를 다시 시작 해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|    symlinkevaluation <SymbolicLinkType>    |                                                                                                                                                                                                                                                                                                                                                                                                   컴퓨터에 만들 수 있는 바로 가기 링크의 종류를 제어 합니다. 유효한 선택할 수 있습니다.<br /><br />1.  로컬 기호화 된 링크를 L2L 로컬: {0 &#124; 1을 (를)<br />2.  원격 기호화 된 링크를 L2R 로컬: {0 &#124; 1을 (를)<br />3.  원격 위치에 로컬 기호화 된 링크를 R2R: {0 &#124; 1을 (를)<br />4.  원격 위치에 원격 기호화 된 링크를 R2L: {0 &#124; 1을 (를)                                                                                                                                                                                                                                                                                                                                                                                                   |
|            DisableDeleteNotify             | @No__t-0**1**\)를 사용 하지 않도록 설정 하거나 @no__t 3**0**\) 삭제 알림을 사용 하도록 설정 합니다. 알림 삭제 \(trim 또는 매핑 해제 라고도\) 파일로 인해 해제 된 클러스터의 기본 저장 장치에 게 알려 주는 기능 작업을 삭제 합니다. 이 밖에도 다음 지침을 따릅니다.<br /><br />-ReFS v2를 사용 하는 시스템의 경우 trim은 기본적으로 사용 되지 않습니다. Windows Server 2016에 적용 됩니다.<br />-ReFS v1을 사용 하는 시스템의 경우 trim은 기본적으로 사용 하도록 설정 됩니다. Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016에 적용 됩니다.<br />-NTFS를 사용 하는 시스템의 경우, 관리자가 사용 하지 않도록 설정 하지 않는 한 trim은 기본적으로 사용 됩니다.<br />-하드 디스크 드라이브 또는 SAN에서 트리밍을 지원 하지 않는 것으로 보고 하는 경우 하드 디스크 드라이브 및 San은 트리밍 알림을 받지 않습니다.<br />-설정 또는 해제를 다시 시작 하지 않아도 됩니다.<br />-Trim는 다음 명령을 매핑을 해제 하는 경우 발생 합니다.<br />-기존 처리 중인 IO 레지스트리 변경의 영향을 받지 않습니다.<br />-하지 않아도 모든 서비스를 다시 시작 하거나 하면 trim을 사용 하지 않도록 설정 됩니다.<br /><br />이 매개 변수는 Windows Server 2008 R2 및 Windows 7에서 도입 되었습니다. |

## <a name="remarks"></a>설명

-   MFT 영역은 mft 조각화를 방지 하기 위해 필요에 따라 MFT (마스터 파일 테이블)를 확장할 수 있는 예약 영역입니다. 볼륨의 평균 파일 크기는 2KB 또는 이하인 것이 좋습니다 설정 하는 경우는 **mftzone** 값 2입니다. 볼륨에는 평균 파일 크기는 1KB 또는 이하인 것이 좋습니다 설정 하는 경우는 **mftzone** 4 사이의 값입니다.

-   **Disable8dot3** 을 **0**으로 설정 하면 긴 파일 이름으로 파일을 만들 때마다 NTFS에서 8.3 문자 길이 파일 이름이 있는 두 번째 파일 항목을 만듭니다. NTFS는 디렉터리에 파일을 만들 때 긴 파일 이름과 연결 된 8.3 문자 길이 파일 이름을 조회 해야 합니다. 이 매개 변수는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation** 레지스트리 키를 업데이트 합니다.

-   **Allowextchar** 매개 변수는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsAllowExtendedCharacterIn8dot3Name** 레지스트리 키를 업데이트 합니다.

-   **disablelastaccess** 매개 변수 파일 및 디렉터리에 마지막 액세스 시간 스탬프에 로깅 업데이트의 피해를 줄일 수 있습니다. 사용 하지 않도록 설정 된 **마지막 액세스 시간** 기능은 파일 및 디렉터리 액세스의 속도 향상 시킵니다. 이 매개 변수는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate** 레지스트리 키를 업데이트 합니다.

    참고:

    -   모든 디스크 값이 최신이 아닌 경우에도 파일 기반 **마지막 액세스 시간** 쿼리는 정확 합니다. NTFS는 정확한 값은 메모리에 저장 되므로 쿼리에 올바른 값을 반환 합니다.

    -   1 시간 동안은 NTFS 업데이트할 때 지연 시간의 최대 **마지막 액세스 시간** 디스크에 있습니다. NTFS와 같은 파일 특성을 업데이트 하는 경우 **마지막 수정 시간**, 및 **마지막 액세스 시간** 업데이트 보류 중, NTFS 업데이트는 **마지막 액세스 시간** 추가 성능 영향을 주지 않고 다른 업데이트와 합니다.

    -   **disablelastaccess** 매개 변수는이 기능을 사용 하는 백업 및 원격 저장소와 같은 프로그램에 영향을 줄 수 있습니다.

-   실제 메모리를 늘려 NTFS로 사용할 수 있는 페이지 풀 메모리의 양을 항상 증가 하지 않습니다. 설정 **memoryusage** 에 **2** 페이징된 풀 메모리 한도를 발생 시킵니다. 이렇게 시스템을 열고 및 설정 하 고 사용 하지 않는 이미 많은 양의 시스템 메모리 캐시 메모리 또는 다른 응용 프로그램에 대 한 동일한 파일에 많은 파일을 닫는 경우 성능이 향상 될 수 있습니다. 컴퓨터에서 다른 응용 프로그램 또는 캐시 메모리에 대해 많은 양의 시스템 메모리를 이미 사용 하 고 있는 경우 페이징 및 비페이징 풀 메모리의 제한을 높이면 다른 프로세스에 대해 사용 가능한 풀 메모리가 줄어듭니다. 이 전체 시스템 성능이 저하 될 수 있습니다. 이 매개 변수는 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsMemoryUsage** 레지스트리 키를 업데이트 합니다.

-   에 지정 된 값은 **mftzone** 매개 변수는 mft MFT 영역에 새 볼륨의 초기 크기의 추정치 이며 각 파일 시스템 탑재 시 설정 됩니다. NTFS 볼륨에 공간을 사용 하면 다음 MFT 확장에 대 한 예약 된 공간을 조정 합니다. MFT 영역이 이미 큰, 전체 MFT 영역 크기 다시 예약 되지 않습니다. MFT 영역 MFT의 끝을 지난 인접 한 범위를 기반으로 하므로 공간을 사용 하는 대로 축소 합니다.

    파일 시스템 현재 MFT 영역을 완전히 사용할 때까지 새 MFT 영역 위치를 확인 하지 않습니다. 이 발생 하지 않으며 일반적인 시스템 note 합니다.

-   삭제 알림 기능이 설정 된 경우 일부 장치에서 성능 저하가 발생할 수 있습니다. 이 경우에 사용 된 **disabledeletenotify** 옵션 알림 기능을 해제 합니다.

### <a name="BKMK_examples"></a>예와
GUID, {928842df-5a01-11de-a85c-806e6f6e6963}를 사용 하 여 지정 된 디스크 볼륨에 대 한 8.3 이름 사용 안 함 동작을 쿼리하려면 다음을 입력 합니다.

```
fsutil behavior query disable8dot3 Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

사용 하 여 8.3 형식이 이름 동작을 쿼리할 수도 있습니다는 **8dot3name** 하위 명령입니다.

TRIM가 설정 하는 경우에 시스템을 쿼리하려면 다음을 입력 합니다.

```
fsutil behavior query DisableDeleteNotify
```
그러면 다음과 유사한 출력이 생성 됩니다.

    NTFS DisableDeleteNotify = 1
    ReFS DisableDeleteNotify is not currently set

0disabledeletenotify @ no__t에 @no__t 대 한 기본 동작을 재정의 하려면 ReFS v 2의 경우 다음을 입력 합니다.

```
fsutil behavior set DisableDeleteNotify ReFS 0
```

0disabledeletenotify @ no__t에 대 @no__t 한 기본 동작을 재정의 하려면 NTFS 및 ReFS v1에 대해 다음을 입력 합니다.
```
fsutil behavior set DisableDeleteNotify 1
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[Fsutil 8dot3name](Fsutil-8dot3name.md)


