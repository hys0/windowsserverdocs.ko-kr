---
title: Diskshadow
description: 볼륨 섀도 복사본 서비스 (VSS)에서 제공 하는 기능을 노출 하는 도구인 Diskshadow 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e962537d-b759-4368-b6f1-e8391cf7b221
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae3a4ba57d9c29375c560c300a4e4ead807184fc
ms.sourcegitcommit: aed942d11f1a361fc1d17553a4cf190a864d1268
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235180"
---
# <a name="diskshadow"></a>Diskshadow

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diskshadow는 VSS (볼륨 섀도 복사본 서비스)에서 제공 하는 기능을 제공 하는 도구입니다. 기본적으로 Diskshadow는 Diskraid 또는 Diskpart와 유사한 대화형 명령 인터프리터를 사용 합니다. Diskshadow에는 스크립트 가능한 모드도 포함 됩니다.

> [!NOTE]
> Diskshadow를 실행 하려면 최소한 로컬 Administrators 그룹의 구성원 이거나이에 해당 하는 권한이 있어야 합니다.

## <a name="syntax"></a>구문

대화형 모드의 경우 명령 프롬프트에 다음을 입력 하 여 Diskshadow 명령 인터프리터를 시작 합니다.

```
diskshadow
```

스크립트 모드의 경우 다음을 입력 합니다 *. 여기서 rename.txt* 는 Diskshadow 명령이 포함 된 스크립트 파일입니다.

```
diskshadow -s script.txt
```

### <a name="parameters"></a>매개 변수

Diskshadow 명령 인터프리터 나 스크립트 파일을 통해 다음 명령을 실행할 수 있습니다. 섀도 복사본을 만들려면 최소한 **추가** 및 **만들기** 만 필요 합니다. 그러나이 없애므로 컨텍스트 및 옵션 설정은 복사 백업이 되며 백업 실행 스크립트가 없는 섀도 복사본을 만듭니다.

| 명령 | 설명 |
| --------- | ----------- |
| [set 명령](set_2.md) | 섀도 복사본을 만들기 위한 컨텍스트, 옵션, 자세한 정보 표시 모드 및 메타 데이터 파일을 설정 합니다. |
| [메타 데이터 로드 명령](load-metadata.md) | 변환할 수 있는 섀도 복사본을 가져오기 전에 메타 데이터.cab 파일을 로드 하거나 복원 하는 경우 기록기 메타 데이터를 로드 합니다. |
| [writer 명령](writer.md) | 기록기 또는 구성 요소가 백업 또는 복원 프로시저에서 기록기 또는 구성 요소를 포함 하거나 제외 하는지 확인 합니다. |
| [명령 추가](add.md) | 볼륨 섀도 복사 되는 볼륨의 집합에 추가 하거나 별칭 환경에 별칭을 추가 합니다. |
| [create 명령](create.md) | 현재 컨텍스트 및 옵션 설정을 사용 하 여 섀도 복사본 생성 프로세스를 시작 합니다. |
| [exec 명령](exec.md) | 로컬 컴퓨터에서 파일을 실행합니다. |
| [backup 시작 명령](begin-backup.md) | 전체 백업 세션을 시작 합니다. |
| [backup 종료 명령](end-backup.md) | 전체 백업 세션을 종료 하 고 필요한 경우 적절 한 기록기 상태를 사용 하 여 **backupcomplete** 이벤트를 발급 합니다. |
| [복원 명령 시작](begin-restore.md) | 복원 세션을 시작 하 고 관련 기록기에 **prerestore** 이벤트를 발급 합니다. |
| [restore 명령 종료](end-restore.md) | 복원 세션을 종료 하 고 관련 된 작성기에 **postrestore** 이벤트를 보냅니다. |
| [reset 명령](reset.md) | Diskshadow를 기본 상태로 다시 설정 합니다. |
| [list 명령](list.md) | 작성자, 섀도 복사본 또는 시스템에 있는 현재 등록 된 섀도 복사본 공급자를 나열 합니다. |
| [그림자 명령 삭제](delete-shadows.md) | 섀도 복사본을 삭제 합니다. |
| [import 명령](import.md) | 시스템에 로드 된 메타 데이터 파일에서 전송 가능한 섀도 복사본을 가져옵니다. |
| [mask 명령](mask.md) | 제거를 사용 하 여 가져온 하드웨어 섀도 복사본은 **가져올** 명령입니다. |
| [명령 노출](expose.md) | 드라이브 문자, 공유 또는 탑재 지점으로 영구 섀도 복사본을 노출합니다. |
| [숨깁니다 명령](unexpose.md) | **공개 명령을 사용** 하 여 노출 된 섀도 복사본을 노출 하지 않습니다. |
| [break 명령](break_2.md) | VSS에서 섀도 복사본 볼륨을 분리 합니다. |
| [revert 명령](revert.md) | 지정 된 섀도 복사본으로 볼륨을 되돌립니다. |
| [끝내기 명령](exit.md) | 명령 인터프리터 나 스크립트를 종료 합니다. |

## <a name="examples"></a>예

백업에 대 한 섀도 복사본을 만드는 명령의 샘플 시퀀스입니다. 이 파일을 파일에 스크립트로 저장 하 고를 사용 하 여 실행할 수 `diskshadow /s script.dsh` 있습니다.

다음을 가정 합니다.

- C: diskshadowdata 라는 기존 디렉터리가 있습니다 \\ .

- 시스템 볼륨은 C:이 고 데이터 볼륨은 d:입니다.

- C: diskshadowdata에는 backupscript .cmd 파일이 있습니다 \\ .

- Backupscript .cmd 파일은 섀도 데이터 p: 및 q:를 백업 드라이브에 복사 하는 작업을 수행 합니다.

이러한 명령을 수동으로 입력 하거나 스크립팅할 수 있습니다.

```
#Diskshadow script file
set context persistent nowriters
set metadata c:\diskshadowdata\example.cab
set verbose on
begin backup
add volume c: alias systemvolumeshadow
add volume d: alias datavolumeshadow

create

expose %systemvolumeshadow% p:
expose %datavolumeshadow% q:
exec c:\diskshadowdata\backupscript.cmd
end backup
#End of script
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
