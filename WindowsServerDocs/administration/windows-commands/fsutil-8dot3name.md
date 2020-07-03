---
title: fsutil 8dot3name
description: 약식 이름 (8.3 이름) 동작에 대 한 설정을 쿼리하거나 변경 하는 fsutil 8dot3name command에 대 한 참조 문서입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: a0c6dbfe-d898-496d-9356-825f7fbd90ec
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 069f7fed72cfe50ef15c869b129dbf98363d9111
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922389"
---
# <a name="fsutil-8dot3name"></a>fsutil 8dot3name

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

다음을 포함 하 여 약식 이름 (8.3 이름) 동작에 대 한 설정을 쿼리하거나 변경 합니다.

- 약식 이름 동작에 대 한 현재 설정 쿼리

- 지정 된 디렉터리 경로에서 짧은 이름이 제거 된 경우 영향을 받을 수 있는 레지스트리 키에 대해 지정 된 디렉터리 경로를 검색 합니다.

- 짧은 이름 동작을 제어 하는 설정 변경 이 설정은 기본 볼륨 설정 또는 지정 된 볼륨에 적용할 수 있습니다.

- 디렉터리 내의 모든 파일에 대 한 짧은 이름 제거

> [!IMPORTANT]
> 8.3 형식이 파일 이름을 영구적으로 제거 하 고 8.3 형식이 파일 이름을 가리키는 레지스트리 키를 수정 하지 예기치 않은 애플리케이션 오류를 애플리케이션을 제거할 수 없다는 점을 포함 하 여 발생할 수 있습니다. 8.3 형식이 파일 이름을 제거 하려고 하면 전에 먼저 디렉터리 또는 볼륨을 백업 하는 것이 좋습니다.

## <a name="syntax"></a>구문

```
fsutil 8dot3name [query] [<volumepath>]
fsutil 8dot3name [scan] [/s] [/l [<log file>] ] [/v] <directorypath>
fsutil 8dot3name [set] { <defaultvalue> | <volumepath> {1|0}}
fsutil 8dot3name [strip] [/t] [/s] [/f] [/l [<log file.] ] [/v] <directorypath>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 쿼리입니다`[<volumepath>]` | 8.3 형식이 약식 이름 만들기 동작의 상태에 대 한 파일 시스템을 쿼리합니다.<p>*Volumepath* 가 매개 변수로 지정 되지 않은 경우 모든 볼륨에 대 한 기본 8dot3name 생성 동작 설정이 표시 됩니다. |
| 있는지`<directorypath>` | 8.3 짧은 이름이 파일 이름에서 제거 된 경우 영향을 받을 수 있는 레지스트리 키에 대해 지정 된 *directorypath* 에 있는 파일을 검색 합니다. |
| 설정`<defaultvalue> | <volumepath>}` | 다음과 같은 경우에서 8.3 이름 만들기에 대 한 파일 시스템 동작을 변경 합니다.<ul><li>*Defaultvalue* 를 지정 하는 경우 레지스트리 키 **HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreationNtfsDisable8dot3NameCreationNtfsDisable8dot3NameCreation**는 *defaultvalue*로 설정 됩니다.<p>*DefaultValue* 값은 다음과 같을 수 있습니다.<ul><li>**0**: 시스템에서 모든 볼륨에서 8.3 이름 만들기를 사용 합니다.</li><li>**1**: 시스템에서 모든 볼륨에서 8.3 이름 만들기를 사용 하지 않도록 설정 합니다.</li><li>**2**: 당 볼륨 별로 8.3 이름 만들기를 설정 합니다.</li><li>**3**: 시스템 볼륨을 제외한 모든 볼륨에 대해에서 8.3 이름 만들기를 사용 하지 않도록 설정 합니다.</li></ul><li>*Volumepath* 가 지정 되 면 디스크 플래그 8dot3name 속성의 지정 된 볼륨이 지정 된 볼륨에 대해 8.3 이름 만들기를 사용 하도록 설정 되거나 (**0**) 지정 된 볼륨에서 8.3 이름 만들기를 사용 하지 않도록 설정 됩니다 (**1**).<p>기본 파일 시스템 동작에서 8.3 이름 만들기에 대 한 값으로 설정 해야 **2** 전에 지정 된 볼륨에서 8.3 이름 만들기를 사용 하지 않도록 설정 하거나 설정할 수 있습니다.</li></ul> |
| 줄무늬`<directorypath>` | 지정 된 *directorypath*에 있는 모든 파일에 대 한 8.3 파일 이름을 제거 합니다. 파일 이름으로 결합 된 *directorypath* 가 260 자를 초과 하는 파일의 경우에는 8.3 파일 이름이 제거 되지 않습니다.<p>이 명령은 목록, 있지만 8.3 형식이 파일 이름을 영구적으로 제거 하는 파일을 가리키는 레지스트리 키를 수정 하지는 않습니다. |
| `<volumepath>` | 드라이브 이름 뒤에 콜론 또는 GUID (형식)를 지정 합니다 `volume{GUID}` . |
| /f | 8.3 파일 이름을 사용 하 여 파일을 가리키는 레지스트리 키가 있는 경우에도 지정 된 *directorypath* 에 있는 모든 파일의 8.3 파일 이름이 제거 되도록 지정 합니다. 이 경우 작업이 8.3 형식이 파일 이름을 제거 했지만 8.3 형식이 파일 이름을 사용 하는 파일을 가리키도록 하는 모든 레지스트리 키를 수정 하지는 않습니다. **경고:** **/F** 매개 변수를 사용 하기 전에 디렉터리 또는 볼륨을 백업 하는 것이 좋습니다 .이는 프로그램을 제거할 수 없는 경우를 비롯 하 여 예기치 않은 응용 프로그램 오류가 발생할 수 있기 때문입니다. |
| /l`[<log file>]` | 정보가 기록 되는 로그 파일을 지정 합니다.<p>**/L** 매개 변수를 지정 하지 않으면 모든 정보가 기본 로그 파일인 `%temp%\8dot3_removal_log@(GMT YYYY-MM-DD HH-MM-SS)` .log * *에 기록 됩니다. |
| /s | 지정 된 *directorypath*의 하위 디렉터리에 작업을 적용 하도록 지정 합니다. |
| /t | 8.3 형식이 파일 이름의 제거 테스트 모드에서 실행 해야 함을 지정 합니다. 8.3 형식이 파일 이름의 행이 실제로 삭제를 제외한 모든 작업 수행 됩니다. 키 8.3 형식이 파일 이름을 사용 하는 파일을 가리키도록 하는 레지스트리를 검색 하려면 테스트 모드를 사용할 수 있습니다. |
| /v | 로그 파일에 기록 되는 모든 정보가 명령줄에도 표시 되도록 지정 합니다. |

### <a name="examples"></a>예

GUID, {928842df-5a01-11de-a85c-806e6f6e6963}를 사용 하 여 지정 된 디스크 볼륨에 대 한 8.3 이름 사용 안 함 동작을 쿼리하려면 다음을 입력 합니다.

```
fsutil 8dot3name query volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

사용 하 여 8.3 형식이 이름 동작을 쿼리할 수도 있습니다는 **동작** 하위 명령입니다.

*D:\mydata* 디렉터리와 모든 하위 디렉터리에서 8.3 파일 이름을 제거 하는 동안 *mylogfile .log*로 지정 된 로그 파일에 정보를 기록 하려면 다음을 입력 합니다.

```
fsutil 8dot3name strip /l mylogfile.log /s d:\MyData
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [fsutil behavior](fsutil-behavior.md)
