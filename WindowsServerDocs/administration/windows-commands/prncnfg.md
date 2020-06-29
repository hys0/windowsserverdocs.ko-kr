---
title: prncnfg
description: Prncnfg.vbs 명령에 대 한 참조 항목으로, 프린터에 대 한 구성 정보를 구성 하거나 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: b60faaa5537ebdf8860c9b0471cf879677b80f1d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472308"
---
# <a name="prncnfg"></a>prncnfg

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

구성 하거나 프린터에 대 한 구성 정보를 표시 합니다. 이 명령은 디렉터리에 있는 Visual Basic 스크립트입니다 `%WINdir%\System32\printing_Admin_Scripts\<language>` . 명령 프롬프트에서이 명령을 사용 하려면 **cscript** 다음에 prncnfg.vbs 파일의 전체 경로를 입력 하거나 디렉터리를 적절 한 폴더로 변경 합니다. 예를 들어 `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg`을 참조하십시오.

## <a name="syntax"></a>구문

```
cscript prncnfg {-g | -t | -x | -?} [-S <Servername>] [-P <Printername>] [-z <newprintername>] [-u <Username>] [-w <password>] [-r <portname>] [-l <location>] [-h <sharename>] [-m <comment>] [-f <separatorfilename>] [-y <datatype>] [-st <starttime>] [-ut <untiltime>] [-i <defaultpriority>] [-o <priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| -g | 프린터에 대 한 구성 정보를 표시 합니다. |
| -t | 프린터를 구성합니다. |
| -X | 프린터를 이름을 바꿉니다. |
| -S`<Servername>` | 프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다. |
| -P`<Printername>` | 관리 하려는 프린터의 이름을 지정 합니다. 필수 사항입니다. |
| -z`<newprintername>` | 새 프린터 이름을 지정합니다. 필요는 **-x** 및 **-P** 매개 변수입니다. |
| -u `<Username>` -w`<password>` | 프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않는 경우 명령이 작동 하려면 이러한 권한이 있는 계정으로 로그온 해야 합니다. |
| -r`<portname>` | 프린터가 연결 되어 있는 포트를 지정 합니다. 병렬 또는 직렬 포트 인 경우 (예를 들어 LPT1 또는 COM1) 포트의 ID를 사용 합니다. TCP/IP 포트 이면 포트를 추가할 때 지정 된 포트 이름을 사용 합니다. |
| -l`<location>` | **Copyroom**과 같은 프린터 위치를 지정 합니다. 위치에 공백이 포함 되어 있으면 **"방 복사"** 와 같이 텍스트 주위에 따옴표를 사용 합니다.|
| -h`<sharename>` | 프린터의 공유 이름을 지정합니다. |
| -m`<comment>` | 프린터의 설명 문자열을 지정합니다. |
| -f`<separatorfilename>` | 구분 기호 페이지에 표시 되는 텍스트를 포함 하는 파일을 지정 합니다. |
| -y`<datatype>` | 프린터를 수락할 수 있는 데이터 형식을 지정 합니다. |
| -st`<starttime>` | 사용 가능한 제한에 대 한 프린터를 구성합니다. 프린터를 사용할 수 있는 시간을 지정 합니다. 문서는 프린터를 사용할 수 없을 때를 보내면 프린터 사용 가능할 때까지 문서 (스풀링) 유지 됩니다. 24 시간 형식으로 시간을 지정 해야 합니다. 예를 들어 오후 11시 지정 하려면 입력 **2300**합니다. |
| -전 세계`<endtime>` | 사용 가능한 제한에 대 한 프린터를 구성합니다. 프린터는 더 이상 사용할 하루 중 시간을 지정 합니다. 문서는 프린터를 사용할 수 없을 때를 보내면 프린터 사용 가능할 때까지 문서 (스풀링) 유지 됩니다. 24 시간 형식으로 시간을 지정 해야 합니다. 예를 들어 오후 11시 지정 하려면 입력 **2300**합니다. |
| -o`<priority>` | 스풀러가 인쇄 작업이 인쇄 큐에 라우팅하는 사용 하 여 우선 순위를 지정 합니다. 인쇄 큐에서 우선 순위가 높은 우선 순위가 낮은 큐 보다 먼저 모든 작업을 받습니다. |
| -i`<defaultpriority>` | 각 인쇄 작업에 할당 된 기본 우선 순위를 지정 합니다. |
| `{+|-}`공유할 | 네트워크에서이 프린터를 공유 하는지 여부를 지정 합니다. |
| `{+|-}`계좌 | 문서 스풀 있는 하지 않고 직접 프린터로 보낼지 여부를 지정 합니다. |
| `{+|-}`게시할지 | 이 프린터를 active directory에 게시할지 여부를 지정 합니다. 프린터를 게시 하는 경우 위치 및 기능 (예: 컬러 인쇄 및 스테이플링)에 따라 다른 사용자가 검색할 수 있습니다. |
| `{+|-}`hidden | 예약 된 함수입니다. |
| `{+|-}`rawonly | 원시 데이터 인쇄 작업만이 큐에 스풀링된 수 있는지 여부를 지정 합니다. |
| `{+|-}`} 대기 | 프린터 문서의 마지막 페이지가 스풀링되 후 될 때까지 인쇄를 시작 하도록 지정 합니다. 문서 인쇄가 완료 될 때까지 인쇄 프로그램 사용할 수 없는 경우 그러나이 매개 변수를 사용 하 여 프린터를 사용할 수 있는 전체 문서 중인지 확인 합니다. |
| `{+|-}`keepprintedjobs | 스풀러가 인쇄 된 후 문서를 유지 해야 하는지 여부를 지정 합니다. 이 옵션을 사용 하면 인쇄 프로그램에서 인쇄 큐 대신에서 프린터에 문서를 다시 전송 하도록 사용자가 있습니다. |
| `{+|-}`workoffline | 사용자 컴퓨터가 네트워크에 연결 되지 않은 경우 인쇄 작업이 인쇄 큐에 보낼 수 있는지 여부를 지정 합니다. |
| `{+|-}`enabledevq | 프린터 설정과 일치 하지 않는 인쇄 작업을 인쇄 하지 않고 큐에 저장 해야 하는지 여부를 지정 합니다. 예를 들어 postscript 파일이 아닌 프린터에 스풀 합니다. |
| `{+|-}`docompletefirst | 스풀러는 인쇄 작업을 우선 순위가 낮은 우선 순위가 높은 스풀링 완료 되지 않은 인쇄 작업을 보내기 전에 스풀링을 보내야 하는지 여부를 지정 합니다. 이 옵션을 사용 하는 경우 문서가 스풀링을 스풀러가 더 작은 작업 하기 전에 큰 문서를 전송 합니다. 작업 우선 순위 프린터 능률을 최대화 하려는 경우이 옵션을 사용 해야 합니다. 이 옵션을 사용할 경우 스풀러 항상 우선 순위가 높은 작업은 각각의 큐를 먼저 보냅니다. |
| `{+|-}`양방향 텍스트 | 프린터 스풀러에 상태 정보를 전송 하는지 여부를 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예제

*HRServer*이라는 원격 컴퓨터에서 호스트 하는 인쇄 큐가 있는 *colorprinter_2* 이라는 프린터에 대 한 구성 정보를 표시 하려면 다음을 입력 합니다.

```
cscript prncnfg -g -S HRServer -P colorprinter_2
```

*HRServer* 라는 원격 컴퓨터의 스풀러가 인쇄 된 후 인쇄 작업을 유지 하도록 *colorprinter_2* 이라는 프린터를 구성 하려면 다음을 입력 합니다.

```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs
```

*HRServer* 이라는 원격 컴퓨터에서 프린터 이름을 *colorprinter_2* 에서 *colorprinter 3*으로 변경 하려면 다음을 입력 합니다.

```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3"
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)
