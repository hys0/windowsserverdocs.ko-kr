---
title: ReFSUtil
description: ReFSUtil 도구에 대 한 참조 문서로, 과도 한 손상 된 ReFS 볼륨을 진단 하 고, 나머지 파일을 식별 하 고, 해당 파일을 다른 볼륨에 복사 합니다.
author: laknight5
ms.author: laknight
ms.date: 6/29/2020
ms.prod: windows-server
ms.technology: storage-file-systems
ms.topic: article
ms.openlocfilehash: c84aaed5b34c535221247dcdd6ab0a5462fd4aad
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931105"
---
# <a name="refsutil"></a>ReFSUtil

>적용 대상: Windows Server 2019, Windows 10

ReFSUtil는 Windows 및 Windows Server에 포함 된 도구로, 과도 하 게 손상 된 ReFS 볼륨을 진단 하 고, 나머지 파일을 식별 하 고, 해당 파일을 다른 볼륨에 복사 합니다. 이는 폴더의 Windows 10 `%SystemRoot%\Windows\System32` 또는 폴더의 Windows Server에서 제공 `%SystemRoot%\\System32` 됩니다.

ReFS 잔존은 ReFSUtil의 기본 기능이 며 디스크 관리에 RAW로 표시 되는 볼륨에서 데이터를 복구 하는 데 유용 합니다. ReFS Salvage에는 두 단계인 스캔 단계와 복사 단계가 있습니다. 자동 모드에서는 검색 단계와 복사 단계가 순차적으로 실행 됩니다. 수동 모드에서는 각 단계를 개별적으로 실행할 수 있습니다. 진행률 및 로그는 작업 디렉터리에 저장 되어 단계를 별도로 실행할 수 있을 뿐만 아니라 검사 단계를 일시 중지 하 고 다시 시작할 수 있습니다. 볼륨이 RAW가 아니면 ReFSutil 도구를 사용할 필요가 없습니다. 읽기 전용 이면 데이터에 계속 액세스할 수 있습니다.

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `<source volume>` | 처리할 ReFS 볼륨을 지정 합니다. 드라이브 문자는 "L:" 형식으로 포맷 해야 합니다. 또는 볼륨 탑재 지점의 경로를 제공 해야 합니다. |
| `<working directory>` | 임시 정보 및 로그를 저장할 위치를 지정 합니다. 에 위치 해서는 **안** `<source volume>` 됩니다. |
| `<target directory>` | 식별 된 파일이 복사 되는 위치를 지정 합니다. 에 위치 해서는 **안** `<source volume>` 됩니다. |
| \-분 | 삭제 된 파일을 포함 하 여 가능한 모든 파일을 복구 합니다.<p>**경고:** 이 매개 변수를 사용 하면 프로세스를 실행 하는 데 시간이 더 오래 걸리지만 예기치 않은 결과가 발생할 수도 있습니다. |
| \-hyper-v | 자세한 정보 표시 모드를 사용 하도록 지정 합니다. |
| \-.x | 필요한 경우 볼륨을 먼저 분리 되도록 합니다. 그러면 볼륨에 대해 열린 모든 핸들이 무효화 됩니다. 예: `refsutil salvage -QA R: N:\\WORKING N:\\DATA -x`. |

## <a name="usage-and-available-options"></a>사용 및 사용 가능한 옵션

### <a name="quick-automatic-mode-command-line-usage"></a>빠른 자동 모드 명령줄 사용

빠른 검색 단계 다음에 복사 단계를 수행 합니다. 이 모드는 볼륨의 일부 중요 한 구조가 손상 되지 않았다고 가정 하므로 더 빠르게 실행 되므로 전체 볼륨을 검색 하 여 찾을 필요가 없습니다. 이를 통해 오래 된 파일/디렉터리/볼륨의 복구도 줄어듭니다.

```
refsutil salvage -QA <source volume> <working directory> <target directory> <options>
```

### <a name="full-automatic-mode-command-line-usage"></a>전체 자동 모드 명령줄 사용

전체 검색 단계를 수행 하 고 복사 단계를 수행 합니다. 이 모드는 복구 가능한 파일/디렉터리/볼륨에 대해 전체 볼륨을 검색 하는 데 시간이 오래 걸릴 수 있습니다.

```
refsutil salvage -FA <source volume> <working directory> <target directory> <options>
```

### <a name="diagnose-phase-command-line-usage-manual-mode"></a>진단 단계 명령줄 사용법 (수동 모드)

먼저이 ReFS 볼륨 인지 확인 하 `<source volume>` 고 볼륨을 탑재할 수 있는지 확인 합니다. 볼륨을 탑재할 수 없는 경우에는 이유가 제공 됩니다. 이는 독립 실행형 단계입니다.

```
refsutil salvage -D <source volume> <working directory> <options>
```

### <a name="quick-scan-phase-command-line-usage"></a>빠른 검색 단계 명령줄 사용법

`<source volume>`복구 가능한 모든 파일에 대해 빠른 검색을 수행 합니다. 이 모드는 볼륨의 일부 중요 한 구조가 손상 되지 않았다고 가정 하므로 더 빠르게 실행 되므로 전체 볼륨을 검색 하 여 찾을 필요가 없습니다. 이를 통해 오래 된 파일/디렉터리/볼륨의 복구도 줄어듭니다. 검색 된 파일은 `foundfiles.<volume signature>.txt` 에 있는 파일에 기록 됩니다 `<working directory>` . 검색 단계가 이전에 중지 된 경우 **-QS** 플래그를 사용 하 여 실행 하면 다시 중지 된 위치에서 검색이 다시 시작 됩니다.

```
refsutil salvage -QS <source volume> <working directory> <options>
```

### <a name="full-scan-phase-command-line-usage"></a>전체 검색 단계 명령줄 사용법

전체에서 `<source volume>` 복구 가능한 파일을 검색 합니다. 이 모드는 복구 가능한 모든 파일의 전체 볼륨을 검색 하는 데 시간이 오래 걸릴 수 있습니다. 검색 된 파일은 `foundfiles.<volume signature>.txt` 에 있는 파일에 기록 됩니다 `<working directory>` . 검색 단계가 이전에 중지 된 경우 **-FS** 플래그를 사용 하 여 실행 하면 중지 된 지점부터 검색이 다시 시작 됩니다.

```
refsutil salvage -FS <source volume> <working directory> <options>
```

### <a name="copy-phase-command-line-usage"></a>복사 단계 명령줄 사용법

파일에 설명 된 모든 파일 `foundfiles.<volume signature>.txt` 을에 복사 `<target directory>` 합니다. 검색 단계를 너무 일찍 중지 하는 경우 `foundfiles.<volume signature>.txt` 파일이 아직 존재 하지 않을 수 있으므로에 파일이 복사 되지 않습니다 `<target directory>` .

```
refsutil salvage -C <source volume> <working directory> <target directory> <options>
```

### <a name="copy-phase-with-list-command-line-usage"></a>List 명령줄 사용이 포함 된 복사 단계

에서에 있는 모든 파일 `<file list>` 을에 복사 `<source volume>` `<target directory>` 합니다. `<file list>`검사를 완료 하기 위해 실행 하지 않아도 되지만의 파일은 검색 단계에서 먼저 식별 되어야 합니다. 는 `<file list>` `foundfiles.<volume signature>.txt` 새 파일에 복사 하 고, 복원 하지 않아야 하는 파일을 참조 하는 줄을 제거 하 고, 복원 해야 하는 파일을 유지 하 여 생성할 수 있습니다. PowerShell cmdlet **Select 문자열** 은 `foundfiles.<volume signature>.txt` 원하는 경로, 확장명 또는 파일 이름만 포함 하도록 필터링 하는 데 유용할 수 있습니다.

```
refsutil salvage -SL <source volume> <working directory> <target directory> <file list> <options>
```

### <a name="copy-phase-with-interactive-console"></a>대화형 콘솔을 사용 하 여 단계 복사

고급 사용자는 대화형 콘솔을 사용 하 여 파일을 복구할 수 있습니다. 또한이 모드에는 검색 단계 중 하나에서 생성 된 파일도 필요 합니다.

```
refsutil salvage -IC <source volume> <working directory> <options>
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
