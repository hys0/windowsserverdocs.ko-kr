---
title: evntcmd
description: 구성 파일의 정보에 따라 이벤트를 트랩, 트랩 대상 또는 둘 다로 변환 하도록 구성 하는 evntcmd 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c1aabb74-76e7-4304-95a6-50ad87e92fd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e922d7876a8065a0e05e9fa7bf2cf8db45bffd25
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437098"
---
# <a name="evntcmd"></a>evntcmd

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

트랩, 트랩 대상 또는 구성 파일의 정보에 따라 두 이벤트의 번역을 구성 합니다.

## <a name="syntax"></a>구문

```
evntcmd [/s <computername>] [/v <verbositylevel>] [/n] <filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /s`<computername>` | 경우 이벤트 트랩, 트랩 대상 또는 둘 모두를 구성 하려는 컴퓨터 이름으로 지정 합니다. 컴퓨터를 지정 하지 않으면 구성을 로컬 컴퓨터에서 발생 합니다. |
| /v`<verbositylevel>` | 구성 된 상태 메시지 트랩으로 나타나고 트랩 대상의 유형을 지정 합니다. 이 매개 변수는 0에서 10 사이의 정수 여야 합니다. 10을 지정 하면 추적 메시지 및 트랩 구성에 성공 했는지 여부에 대 한 경고를 포함 하 여 모든 종류의 메시지가 나타납니다. 0을 지정 하는 경우 메시지가 나타나지 않습니다. |
| /n | SNMP 서비스 하지를 다시 시작 해야이 컴퓨터 구성 변경 내용을 트랩을 수신 하는 경우를 지정 합니다. |
| `<filename>` | 구성 하려는 대상 및 트랩으로의 이벤트 변환에 대 한 정보를 포함 하는 구성 파일의 이름을 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 트랩을 구성 하지만 트랩 대상은 구성 하지 않으려는 경우 그래픽 유틸리티인 번역기에 이벤트를 사용 하 여 유효한 구성 파일을 만들 수 있습니다. SNMP 서비스가 설치 되어 있으면 입력 하 여 트랩 변환기에 대 한 이벤트를 시작할 수 있습니다 **evntwin** 명령 프롬프트입니다. 원하는 트랩을 정의한 후 **내보내기** 를 클릭 하 여 **evntcmd**에서 사용 하기에 적합 한 파일을 만듭니다. 트랩 변환기에 대 한 이벤트를 사용 하 여 쉽게 구성 파일을 만든 다음 사용 하 여 구성 파일을 사용 하 여 **evntcmd** 신속 하 게 구성 트랩 여러 컴퓨터에서 명령 프롬프트입니다.

- 트랩을 구성 하기 위한 구문은 다음과 같습니다.

  ```
  #pragma add <eventlogfile> <eventsource> <eventID> [<count> [<period>]]
  ```

  다음 텍스트는 다음과 같습니다.

    - **#pragma** 는 파일의 모든 항목의 시작 부분에 표시 되어야 합니다.

    - **Add** 매개 변수는 트랩 구성에 이벤트를 추가 하도록 지정 합니다.

    - **Eventlogfile**, **eventsource**및 **eventID** 매개 변수는 필수 이며 **eventlogfile** 은 이벤트가 기록 되는 파일을 지정 합니다. **eventsource** 는 이벤트를 생성 하는 응용 프로그램을 지정 하 고 **eventID** 는 각 이벤트를 식별 하는 고유 번호를 지정 합니다.

    각 이벤트에 해당 하는 값을 확인 하려면 명령 프롬프트에서 **evntwin** 를 입력 하 여 변환기를 트래핑 하는 이벤트를 시작 합니다. **사용자 지정**을 클릭 한 다음 **편집**을 클릭 합니다. **이벤트 원본**에서 구성할 이벤트를 찾을 때까지 폴더를 검색 하 고 클릭 한 다음 **추가**를 클릭 합니다. 이벤트 원본, 이벤트 로그 파일 및 이벤트 ID에 대 한 내용은 아래에 표시 **로그, 소스**, 및 **특정 ID를 트래핑**, 각각.

    - **Count** 매개 변수는 선택 사항이 며 트랩 메시지가 전송 되기 전에 이벤트가 발생 해야 하는 횟수를 지정 합니다. 이 매개 변수를 사용 하지 않으면 이벤트를 한 번 발생 한 후 트랩 메시지가 전송 됩니다.

    - **Period** 매개 변수는 선택 사항 이지만 **count** 매개 변수를 사용 해야 합니다. **Period** 매개 변수는 이벤트를 수신 하는 시간 (초)을 지정 합니다. 트랩 메시지를 보내기 전에 **count** 매개 변수로 지정 된 횟수를 지정 합니다. 이 매개 변수를 사용 하지 않는 경우 발생 하는 시간에 관계 없이 ***count*** 매개 변수로 지정 된 횟수 만큼 이벤트가 발생 한 후 트랩 메시지가 전송 됩니다.

- 트랩을 제거 하기 위한 구문은 다음과 같습니다.

  ```
  #pragma delete <eventlogfile> <eventsource> <eventID>
  ```

  다음 텍스트는 다음과 같습니다.

    - **#pragma** 는 파일의 모든 항목의 시작 부분에 표시 되어야 합니다.

    - 매개 변수 **삭제** 는 이벤트를 트랩 구성으로 제거 하도록 지정 합니다.

    - **Eventlogfile**, **eventsource**및 **eventID** 매개 변수는 필수 이며 **eventlogfile** 은 이벤트가 기록 되는 파일을 지정 합니다. **eventsource** 는 이벤트를 생성 하는 응용 프로그램을 지정 하 고 **eventID** 는 각 이벤트를 식별 하는 고유 번호를 지정 합니다.

    각 이벤트에 해당 하는 값을 확인 하려면 명령 프롬프트에서 **evntwin** 를 입력 하 여 변환기를 트래핑 하는 이벤트를 시작 합니다. **사용자 지정**을 클릭 한 다음 **편집**을 클릭 합니다. **이벤트 원본**에서 구성할 이벤트를 찾을 때까지 폴더를 검색 하 고 클릭 한 다음 **추가**를 클릭 합니다. 이벤트 원본, 이벤트 로그 파일 및 이벤트 ID에 대 한 내용은 아래에 표시 **로그, 소스**, 및 **특정 ID를 트래핑**, 각각.

- 트랩 대상을 구성 하는 것에 대 한 구문은 다음과 같습니다.

  ```
  #pragma add_TRAP_DEST <communityname> <hostID>
  ```

  다음 텍스트는 다음과 같습니다.

    - **#pragma** 는 파일의 모든 항목의 시작 부분에 표시 되어야 합니다.

    - **Add_TRAP_DEST** 매개 변수는 커뮤니티 내의 지정 된 호스트로 트랩 메시지를 보내도록 지정 합니다.

    - **Communityname** 매개 변수는 트랩 메시지가 전송 되는 커뮤니티를 이름으로 지정 합니다.

    - 매개 변수 **hostID** 는 이름 또는 IP 주소를 기준으로 트랩 메시지를 보낼 호스트를 지정 합니다.

- 트랩 대상을 제거에 대 한 구문은 다음과 같습니다.

  ```
  #pragma delete_TRAP_DEST <communityname> <hostID>
  ```

  다음 텍스트는 다음과 같습니다.

    - **#pragma** 는 파일의 모든 항목의 시작 부분에 표시 되어야 합니다.

    - 매개 변수 **delete_TRAP_DEST** 는 커뮤니티 내에서 지정 된 호스트로 트랩 메시지를 보내지 않도록 지정 합니다.

    - **Communityname** 매개 변수는 트랩 메시지를 보낼 수 없는 커뮤니티를 이름으로 지정 합니다.

    - 매개 변수 **hostID** 는 트랩 메시지를 보내지 않으려는 호스트의 이름 또는 IP 주소를 지정 합니다.

### <a name="examples"></a>예

다음 예제에 대 한 구성 파일 항목에에서 설명 된 **evntcmd** 명령입니다. 명령 프롬프트에서 입력 하도록 설계 되지 않은 것입니다.

트랩 메시지가 이벤트 로그 서비스를 다시 시작할 경우 입력 보내려고 합니다.

```
#pragma add System Eventlog 2147489653
```

트랩 메시지가 이벤트 로그 서비스를 3 분에 두 번 다시 시작한 경우 입력 보내려고 합니다.

```
#pragma add System Eventlog 2147489653 2 180
```

이벤트 로그 서비스를 다시 시작 하는 경우 트랩 메시지를 보내는 중지 하려면 다음을 입력 합니다.

```
#pragma delete System Eventlog 2147489653
```

IP 주소가 *192.168.100.100*인 호스트로 *Public* 이라는 커뮤니티 내에서 트랩 메시지를 보내려면 다음을 입력 합니다.

```
#pragma add_TRAP_DEST public 192.168.100.100
```

*Host1*라는 호스트에 *Private* 이라는 커뮤니티 내에서 트랩 메시지를 보내려면 다음을 입력 합니다.

```
#pragma add_TRAP_DEST private Host1
```

*개인* 커뮤니티 내의 트랩 메시지를 트랩 대상을 구성 하는 컴퓨터와 동일한 컴퓨터로 전송 하지 않으려면 다음을 입력 합니다.

```
#pragma delete_TRAP_DEST private localhost
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
