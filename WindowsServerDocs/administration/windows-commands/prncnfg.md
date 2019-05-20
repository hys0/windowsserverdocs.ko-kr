---
title: prncnfg
description: Prncfg 명령을 사용 하 여 프린터를 구성 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6426b053a5c56918768f82cbd7631631abcf0a6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859154"
---
# <a name="prncnfg"></a>prncnfg

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

구성 하거나 프린터에 대 한 구성 정보를 표시 합니다.

## <a name="syntax"></a>구문
```
cscript Prncnfg {-g | -t | -x | -?} [-S <ServerName>] [-P <printerName>] [-z <NewprinterName>] [-u <UserName>] [-w <Password>] [-r <PortName>] [-l <Location>] [-h <Sharename>] [-m <Comment>] [-f <SeparatorFileName>] [-y <Datatype>] [-st <starttime>] [-ut <Untiltime>] [-i <DefaultPriority>] [-o <Priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|-g|프린터에 대 한 구성 정보를 표시 합니다.|
|-t|프린터를 구성합니다.|
|-x|프린터를 이름을 바꿉니다.|
|-S \<ServerName\>|프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다.|
|-P \<printerName\>|관리 하려는 프린터의 이름을 지정 합니다. 필수.|
|-z \<NewprinterName\>|새 프린터 이름을 지정합니다. 필요는 **-x** 및 **-P** 매개 변수입니다.|
|-u \<사용자 이름\> -w \<암호\>|프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않으면, 작동 하려면 명령에 대 한 이러한 사용 권한이 있는 계정으로 로그온 해야 합니다.|
|-r \<PortName\>|프린터가 연결 되어 있는 포트를 지정 합니다. 병렬 또는 직렬 포트 인 경우 (예를 들어 LPT1 또는 COM1) 포트의 ID를 사용 합니다. TCP/IP 포트 이면 포트를 추가할 때 지정 된 포트 이름을 사용 합니다.|
|-l \<위치\>|"복사 실."와 같은 프린터 위치를 지정합니다.|
|-h \<Sharename\>|프린터의 공유 이름을 지정합니다.|
|-m \<주석\>|프린터의 설명 문자열을 지정합니다.|
|-f \<SeparatorFileName\>|구분 기호 페이지에 표시 되는 텍스트를 포함 하는 파일을 지정 합니다.|
|-y \<데이터 형식\>|프린터를 수락할 수 있는 데이터 형식을 지정 합니다.|
|-st \<starttime\>|사용 가능한 제한에 대 한 프린터를 구성합니다. 프린터를 사용할 수 있는 시간을 지정 합니다. 문서는 프린터를 사용할 수 없을 때를 보내면 프린터 사용 가능할 때까지 문서 (스풀링) 유지 됩니다. 24 시간 형식으로 시간을 지정 해야 합니다. 예를 들어 오후 11시 지정 하려면 입력 **2300**합니다.|
|-ut \<Endtime\>|사용 가능한 제한에 대 한 프린터를 구성합니다. 프린터는 더 이상 사용할 하루 중 시간을 지정 합니다. 문서는 프린터를 사용할 수 없을 때를 보내면 프린터 사용 가능할 때까지 문서 (스풀링) 유지 됩니다. 24 시간 형식으로 시간을 지정 해야 합니다. 예를 들어 오후 11시 지정 하려면 입력 **2300**합니다.|
|-o \<우선 순위\>|스풀러가 인쇄 작업이 인쇄 큐에 라우팅하는 사용 하 여 우선 순위를 지정 합니다. 인쇄 큐에서 우선 순위가 높은 우선 순위가 낮은 큐 보다 먼저 모든 작업을 받습니다.|
|-i \<DefaultPriority\>|각 인쇄 작업에 할당 된 기본 우선 순위를 지정 합니다.|
|{+ &#124;-} 공유|네트워크에서이 프린터를 공유 하는지 여부를 지정 합니다.|
|{+ &#124;-} 직접|문서 스풀 있는 하지 않고 직접 프린터로 보낼지 여부를 지정 합니다.|
|{+ &#124;-} 게시|Active directory에서이 프린터를 게시 해야 하는지 여부를 지정 합니다. 프린터를 게시 하는 경우 위치 및 기능 (예: 컬러 인쇄 및 스테이플링)에 따라 다른 사용자가 검색할 수 있습니다.|
|{+ &#124;-} 숨겨진|예약 된 함수입니다.|
|{+ &#124;-} 처리|원시 데이터 인쇄 작업만이 큐에 스풀링된 수 있는지 여부를 지정 합니다.|
|{+ &#124;을 (를) 큐에 대기|프린터 문서의 마지막 페이지가 스풀링되 후 될 때까지 인쇄를 시작 하도록 지정 합니다. 문서 인쇄가 완료 될 때까지 인쇄 프로그램 사용할 수 없는 경우 그러나이 매개 변수를 사용 하 여 프린터를 사용할 수 있는 전체 문서 중인지 확인 합니다.|
|{+ &#124;-} 인쇄 된 작업 보관|스풀러가 인쇄 된 후 문서를 유지 해야 하는지 여부를 지정 합니다. 이 옵션을 사용 하면 인쇄 프로그램에서 인쇄 큐 대신에서 프린터에 문서를 다시 전송 하도록 사용자가 있습니다.|
|{+ &#124;을 (를) 오프 라인으로 작업|사용자 컴퓨터가 네트워크에 연결 되지 않은 경우 인쇄 작업이 인쇄 큐에 보낼 수 있는지 여부를 지정 합니다.|
|{+ &#124;-} devq 사용|프린터 설정 (예: PostScript 포스트 스크립트가 아닌 프린터에 스풀 파일)과 일치 하지 않는 인쇄 작업을 큐에 보관 해야 하는지 여부를 지정 합니다. 인쇄 하지 않고 있습니다.|
|{+ &#124;-} 우선 완성|스풀러는 인쇄 작업을 우선 순위가 낮은 우선 순위가 높은 스풀링 완료 되지 않은 인쇄 작업을 보내기 전에 스풀링을 보내야 하는지 여부를 지정 합니다. 이 옵션을 사용 하는 경우 문서가 스풀링을 스풀러가 더 작은 작업 하기 전에 큰 문서를 전송 합니다. 작업 우선 순위 프린터 능률을 최대화 하려는 경우이 옵션을 사용 해야 합니다. 이 옵션을 사용할 경우 스풀러 항상 우선 순위가 높은 작업은 각각의 큐를 먼저 보냅니다.|
|{+ &#124;-} 양방향 사용|프린터 스풀러에 상태 정보를 전송 하는지 여부를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   합니다 **prncnfg** 명령입니다는 %WINdir%\System32\printing_Admin_Scripts에 있는 Visual Basic 스크립트\\ <language> 디렉터리입니다. 명령 프롬프트에서이 명령을 사용 하려면 입력 **cscript** 전체 경로 뒤에 prncnfg 파일 또는 디렉터리 적절 한 폴더로 변경 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg
    ```
-   텍스트 주위에 따옴표를 사용 하 여 사용자가 제공한 정보에 공백이 있으면 (예를 들어 `"computer Name"`).

## <a name="BKMK_examples"></a>예제
Colorprinter_2 HRServer 라는 원격 컴퓨터에서 호스팅하는 인쇄 대기열을 사용 하 여 명명 된 프린터에 대 한 구성 정보를 표시 하려면 다음을 입력 합니다.
```
cscript prncnfg -g -S HRServer -P colorprinter_2 
```

스풀러 HRServer 라는 원격 컴퓨터에서 인쇄 된 후 인쇄 작업을 계속 되도록 colorprinter_2 라는 프린터를 구성 하려면 다음을 입력 합니다.
```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs 
```

원격 컴퓨터에 있는 프린터의 이름을 변경 하려면 colorprinter 3, 유형 하에서 colorprinter_2 HRServer 라는:
```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3" 
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[인쇄 명령 참조](print-command-reference.md)
