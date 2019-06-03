---
title: Evntcmd
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1aabb74-76e7-4304-95a6-50ad87e92fd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a149e78170f2849512dcfc0a0a82f9eed979abe2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885984"
---
# <a name="evntcmd"></a>Evntcmd

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

트랩, 트랩 대상 또는 구성 파일의 정보에 따라 두 이벤트의 번역을 구성 합니다.   
## <a name="syntax"></a>구문  
```  
evntcmd [/s <computerName>] [/v <verbosityLevel>] [/n] <FileName>  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|/s <computerName>|경우 이벤트 트랩, 트랩 대상 또는 둘 모두를 구성 하려는 컴퓨터 이름으로 지정 합니다. 컴퓨터를 지정 하지 않으면 구성을 로컬 컴퓨터에서 발생 합니다.|  
|/v <verbosityLevel>|구성 된 상태 메시지 트랩으로 나타나고 트랩 대상의 유형을 지정 합니다. 이 매개 변수는 0에서 10 사이의 정수 여야 합니다. 10을 지정 하면 추적 메시지 및 트랩 구성에 성공 했는지 여부에 대 한 경고를 포함 하 여 모든 종류의 메시지가 나타납니다. 0을 지정 하는 경우 메시지가 나타나지 않습니다.|  
|/n|SNMP 서비스 하지를 다시 시작 해야이 컴퓨터 구성 변경 내용을 트랩을 수신 하는 경우를 지정 합니다.|  
|<FileName>|구성 하려는 대상 및 트랩으로의 이벤트 변환에 대 한 정보를 포함 하는 구성 파일의 이름을 지정 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  
## <a name="remarks"></a>설명  
-   트랩을 구성 하지만 대상을 트래핑 하지 않으면 하려는 경우 그래픽 유틸리티인 트랩 변환기에 대 한 이벤트를 사용 하 여 유효한 구성 파일을 만들 수 있습니다. SNMP 서비스가 설치 되어 있으면 입력 하 여 트랩 변환기에 대 한 이벤트를 시작할 수 있습니다 **evntwin** 명령 프롬프트입니다. 원하는 트랩을 정의한 후에 파일을 만들려면 사용에 적합 한 내보내기를 클릭 **evntcmd**합니다. 트랩 변환기에 대 한 이벤트를 사용 하 여 쉽게 구성 파일을 만든 다음 사용 하 여 구성 파일을 사용 하 여 **evntcmd** 신속 하 게 구성 트랩 여러 컴퓨터에서 명령 프롬프트입니다.  
-   트랩을 구성 하기 위한 구문은 다음과 같습니다.  
    * *#pragma add***<EventLogFile> <EventSource> <EventID> [<Count> [<Period>]]*  
    -   텍스트 **#pragma** 는 파일의 모든 항목의 시작 부분에 표시 되어야 합니다.  
    -   매개 변수 **추가** 트랩 구성에 이벤트를 추가할 것임을 지정 합니다.  
    -   매개 변수 *EventLogFile*, *EventSource*, 및 *EventID* 필요 합니다. 매개 변수 *EventLogFile* 이벤트가 기록 되는 파일을 지정 합니다. 매개 변수 *EventSource* 이벤트를 생성 하는 응용 프로그램을 지정 합니다. *EventID* 매개 변수는 각 이벤트를 식별 하는 고유 번호를 지정 합니다. 특정 이벤트에 해당 하는 값을 알아보려면 이벤트 트랩 번역기를 입력 하 여 시작 **evntwin** 명령 프롬프트입니다. 클릭 **사용자 지정**를 클릭 하 고 **편집**합니다. 아래 **이벤트 원본**, 구성를 클릭 한 다음 클릭 하려는 이벤트를 찾을 때까지 폴더를 찾습니다 **추가**합니다. 이벤트 원본, 이벤트 로그 파일 및 이벤트 ID에 대 한 내용은 아래에 표시 **로그, 소스**, 및 **특정 ID를 트래핑**, 각각.  
    -   *Count* 매개 변수는 선택적 이며 트랩 메시지를 보내기 전에 발생 하는 이벤트 횟수를 지정 합니다. 사용 하지 않는 경우는 *Count* 매개 변수를 이벤트는 한 번 발생 한 후 트랩 메시지가 전송 됩니다.  
    -   *기간* 매개 변수는 선택 사항 이지만 사용 하 여 필요는 *Count* 매개 변수입니다. *기간* 매개 변수는 시간 (초) 동안 발생 하는 이벤트 트랩 메시지를 보내기 전에 Count 매개 변수를 사용 하 여 지정 된 횟수 만큼의 길이 지정 합니다. 사용 하지 않는 경우는 *기간* 매개 변수, 트랩 메시지를 보내는 이벤트와 지정 된 횟수 만큼 발생 한 후는 *Count* 일치 항목 사이 경과 시간 없이 매개 변수입니다.  
-   트랩을 제거 하기 위한 구문은 다음과 같습니다.  
    * *#pragma delete***<EventLogFile> <EventSource> <EventID>*  
    -   텍스트 **#pragma** 는 파일의 모든 항목의 시작 부분에 표시 되어야 합니다.  
    -   매개 변수 *삭제* 트랩 구성에 이벤트를 제거할 것임을 지정 합니다.  
    -   매개 변수 *EventLogFile*,  *EventSource*, 및 *EventID* 필요 합니다. 매개 변수 *EventLogFile* 로그를 지정에 해당 이벤트가 기록 됩니다. 매개 변수 *EventSource* 이벤트를 생성 하는 응용 프로그램을 지정 합니다. *EventID* 매개 변수는 각 이벤트를 식별 하는 고유 번호를 지정 합니다.  
-   트랩 대상을 구성 하는 것에 대 한 구문은 다음과 같습니다.  
    * *#pragma add_TRAP_DEST***<CommunityName> <HostID>*  
    -   텍스트 **#pragma** 는 파일의 모든 항목의 시작 부분에 표시 되어야 합니다.  
    -   매개 변수 **add_TRAP_DEST** 트랩 메시지를 커뮤니티 내에서 지정된 된 호스트에 보낼 것임을 지정 합니다.  
    -   매개 변수 *CommunityName* 는 트랩 메시지가 전송 되는 커뮤니티 이름으로 지정 합니다.  
    -   매개 변수 *HostID* 트랩 메시지를 보낼 수 있도록 호스트 이름이 나 IP 주소를 지정 합니다.  
-   트랩 대상을 제거에 대 한 구문은 다음과 같습니다.  
    * *#pragma delete_TRAP_DEST***<CommunityName> <HostID>*  
    -   텍스트 **#pragma** 는 파일의 모든 항목의 시작 부분에 표시 되어야 합니다.  
    -   매개 변수 *delete_TRAP_DEST* 트랩 메시지를 커뮤니티 내에서 지정된 된 호스트에 보낼 것임을 지정 합니다.  
    -   매개 변수 *CommunityName* 는 트랩 메시지가 전송 되는 커뮤니티 이름으로 지정 합니다.  
    -   매개 변수 *HostID* 이름 또는 IP 주소를 원하지 않는 트랩 메시지를 보낼 수 있도록 호스트를 지정 합니다.  
## <a name="BKMK_Examples"></a>예제  
다음 예제에 대 한 구성 파일 항목에에서 설명 된 **evntcmd** 명령입니다. 명령 프롬프트에서 입력 하도록 설계 되지 않은 것입니다.  
트랩 메시지가 이벤트 로그 서비스를 다시 시작할 경우 입력 보내려고 합니다.  
```  
#pragma add System "Eventlog" 2147489653  
```  
트랩 메시지가 이벤트 로그 서비스를 3 분에 두 번 다시 시작한 경우 입력 보내려고 합니다.  
```  
#pragma add System "Eventlog" 2147489653 2 180  
```  
이벤트 로그 서비스를 다시 시작 하는 경우 트랩 메시지를 보내는 중지 하려면 다음을 입력 합니다.  
```  
#pragma delete System "Eventlog" 2147489653  
```  
호스트에 IP 주소가 192.168.100.100 Public 이라는 커뮤니티 내에서 트랩 메시지를 보내려면 다음을 입력 합니다.  
```  
#pragma add_TRAP_DEST public 192.168.100.100  
```  
Host1라는 호스트에 Private이라는 커뮤니티 내에서 트랩 메시지를 보내려면 다음을 입력합니다.  
```  
#pragma add_TRAP_DEST private Host1  
```  
동일한 컴퓨터를 구성하는 트랩 대상 프라이빗이라는 커뮤니티 내에서 트랩 메시지를 보내는 중지 하려면 다음을 입력합니다.  
```  
#pragma delete_TRAP_DEST private localhost  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
