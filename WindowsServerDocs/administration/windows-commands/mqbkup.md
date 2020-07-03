---
title: mqbkup
description: MSMQ 메시지 파일 및 레지스트리 설정을 저장 장치에 백업 하 고 이전에 저장 된 메시지와 설정을 복원 하는 mqbkup 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7bdd41c4-75ef-455f-b241-1d64a4c7acf5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 131d80f32a3c3324dad08b876dd4f4f8610b93e2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936302"
---
# <a name="mqbkup"></a>mqbkup

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

스토리지 디바이스 설정을 MSMQ 메시지 파일 및 레지스트리를 백업 하 고 이전에 저장 된 메시지 및 설정을 복원 합니다.

백업과 복원 작업 모두 로컬 MSMQ 서비스를 중지 합니다. MSMQ 서비스가 이미 시작 된 경우이 유틸리티는 백업 또는 복원 작업의 끝에 MSMQ 서비스를 다시 시작 하려고 합니다. 이 유틸리티를 실행 하기 전에 서비스가 이미 중지 된 서비스를 다시 시작 하려고 하지 이루어집니다.

MSMQ 메시지 백업/복원 유틸리티를 사용 하기 전에 MSMQ를 사용 하는 모든 로컬 애플리케이션을 닫아야 합니다.

## <a name="syntax"></a>구문

```
mqbkup {/b | /r} <folder path_to_storage_device>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ------- | -------- |
| /b | 백업 작업을 지정 합니다. |
| /r | 복원 작업을 지정 합니다. |
| `<folder path_to_storage_device>` | MSMQ 메시지 파일 및 레지스트리 설정을 저장할 경로를 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 백업 또는 복원 작업을 수행 하는 동안 지정 된 폴더가 존재 하지 않는 경우이 폴더는 유틸리티에 의해 자동으로 만들어집니다.

- 기존 폴더를 지정 하도록 선택 하는 경우에는 비어 있어야 합니다. 비어 있지 않은 폴더를 지정 하는 경우 유틸리티는 여기에 포함 된 모든 파일과 하위 폴더를 삭제 합니다. 이 경우 기존 파일 및 하위 폴더를 삭제할 수 있는 권한을 부여 하 라는 메시지가 표시 됩니다. 사용할 수는 **/y** 모든 기존 파일 및 지정된 된 폴더에 하위 삭제에 미리 동의 함을 나타내는 매개 변수를 합니다.

- MSMQ 메시지 파일을 저장 하는 데 사용 되는 폴더의 위치는 레지스트리에 저장 됩니다. 따라서 유틸리티는 복원 작업 이전에 사용 되는 저장소 폴더가 아니라 레지스트리에 지정 된 폴더로 MSMQ 메시지 파일을 복원 합니다.

### <a name="examples"></a>예

모든 MSMQ 메시지 파일 및 레지스트리 설정을 백업 하 고 C: 드라이브의 *msmqbkup* 폴더에 저장 하려면 다음을 입력 합니다.

```
mqbkup /b c:\msmqbkup
```

C: 드라이브의 *oldbkup* 폴더에 있는 모든 기존 파일과 하위 폴더를 삭제 한 다음 MSMQ 메시지 파일 및 레지스트리 설정을 폴더에 저장 하려면 다음을 입력 합니다.

```
mqbkup /b /y c:\oldbkup
```

MSMQ 메시지 및 레지스트리 설정을 복원 하려면 다음을 입력 합니다.

```
mqbkup /r c:\msmqbkup
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [MSMQ Powershell 참조](https://docs.microsoft.com/powershell/module/msmq/?view=win10-ps)
