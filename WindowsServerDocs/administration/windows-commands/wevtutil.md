---
title: wevtutil
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4c791e0-7e59-45c5-aa55-0223b77a4822 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d99b1f1da3bcf2c59236ce9a8c41f933b100bf7a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440105"
---
# <a name="wevtutil"></a>wevtutil



이벤트 로그 및 게시자에 대한 정보를 검색할 수 있습니다. 이 명령을 사용하여 이벤트 매니페스트를 설치 및 제거하고, 쿼리를 실행하며, 로그 내보내기, 보관 및 지우기 작업을 수행할 수 있습니다. 이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
wevtutil [{el | enum-logs}] [{gl | get-log} <Logname> [/f:<Format>]]
[{sl | set-log} <Logname> [/e:<Enabled>] [/i:<Isolation>] [/lfn:<Logpath>] [/rt:<Retention>] [/ab:<Auto>] [/ms:<MaxSize>] [/l:<Level>] [/k:<Keywords>] [/ca:<Channel>] [/c:<Config>]] 
[{ep | enum-publishers}] 
[{gp | get-publisher} <Publishername> [/ge:<Metadata>] [/gm:<Message>] [/f:<Format>]] [{im | install-manifest} <Manifest>] 
[{um | uninstall-manifest} <Manifest>] [{qe | query-events} <Path> [/lf:<Logfile>] [/sq:<Structquery>] [/q:<Query>] [/bm:<Bookmark>] [/sbm:<Savebm>] [/rd:<Direction>] [/f:<Format>] [/l:<Locale>] [/c:<Count>] [/e:<Element>]] 
[{gli | get-loginfo} <Logname> [/lf:<Logfile>]] 
[{epl | export-log} <Path> <Exportfile> [/lf:<Logfile>] [/sq:<Structquery>] [/q:<Query>] [/ow:<Overwrite>]] 
[{al | archive-log} <Logpath> [/l:<Locale>]] 
[{cl | clear-log} <Logname> [/bu:<Backup>]] [/r:<Remote>] [/u:<Username>] [/p:<Password>] [/a:<Auth>] [/uni:<Unicode>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|{el \| enum 로그}|모든 로그의 이름을 표시합니다.|
|{gl \| get 로그} \<Logname > [/ f:\<형식 >]|로그 저장 된 파일에 지정 된 로그 사용 여부를 포함 하는 로그, 경로 로그의 현재 최대 크기 한도 대 한 구성 정보를 표시 합니다.|
|{sl \| 집합 로그} \<Logname > [/ e:\<사용 >] [/ 할까요\<격리 >] [/ lfn:\<Logpath >] [/ rt:\<보존 >] [/ ab:\<자동 >] [/ms:\< MaxSize >] [/ /l:\<수준 >] [/ k:\<키워드 >] [/ ca:\<채널 >] [/ c:\<구성 >]|지정된 된 로그의 구성을 수정합니다.|
|{ep \| enum 게시자}|이벤트 게시자는 로컬 컴퓨터에 표시 됩니다.|
|{gp \| get 게시자} \<Publishername > [/ ge:\<메타 데이터 >] [/ gm:\<메시지 >] [/ f:\<형식 >]]|지정 된 이벤트 게시자에 대 한 구성 정보를 표시 합니다.|
|{im \| 설치 매니페스트} \<매니페스트 >|매니페스트에서 이벤트 게시자 및 로그를 설치합니다. 이벤트 매니페스트 및이 매개 변수를 사용 하는 방법에 대 한 자세한 내용은 Microsoft 개발자 네트워크 (MSDN) 웹 사이트에서 Windows 이벤트 로그 SDK를 참조 ([https://msdn.microsoft.com](https://msdn.microsoft.com)).|
|{um \| 제거 매니페스트} \<매니페스트 >|매니페스트에서 모든 게시자와 로그를 제거합니다. 이벤트 매니페스트 및이 매개 변수를 사용 하는 방법에 대 한 자세한 내용은 Microsoft 개발자 네트워크 (MSDN) 웹 사이트에서 Windows 이벤트 로그 SDK를 참조 ([https://msdn.microsoft.com](https://msdn.microsoft.com)).|
|{qe \| 쿼리 이벤트} \<경로 > [/ lf:\<로그 파일 >] [/lf:\<Structquery >] [/ q:\<쿼리 >] [/ bm:\<책갈피 >] [/ sbm:\<Savebm >] [/ rd:\< 방향 >] [/ f:\<형식 >] [/ /l:\<로캘 >] [/ c:\<개수 >] [/ e:\<요소 >]|로그 파일 또는 구조화 된 쿼리를 사용 하는 이벤트 로그에서 이벤트를 읽습니다. 에 대 한 로그 이름을 기본적으로 제공 \<경로 >. 그러나 사용 하는 경우는 **/lf** 옵션을 다음 \<경로 > 로그 파일 경로 여야 합니다. 사용 하는 경우는 **/sq** 매개 변수를 \<경로 >는 구조적 된 쿼리를 포함 하는 파일 경로 여야 합니다.|
|{gli \| get loginfo} \<Logname > [/ lf:\<로그 파일 >]|이벤트 로그 또는 로그 파일에 대 한 상태 정보를 표시합니다. 경우는 **/lf** 옵션을 사용 하면 \<Logname > 로그 파일 경로입니다. 실행할 수 있습니다 **wevtutil el** 로그 이름의 목록을 가져올 수 있습니다.|
|{epl \| 내보내기 로그} \<경로 > \<Exportfile > [/ lf:\<로그 파일 >] [/lf:\<Structquery >] [/ q:\<쿼리 >] [/ow:\<덮어쓰기 >]|로그 파일 또는 구조적된 쿼리를 사용 하 여 지정된 된 파일에는 이벤트 로그에서 이벤트를 내보냅니다. 에 대 한 로그 이름을 기본적으로 제공 \<경로 >. 그러나 사용 하는 경우는 **/lf** 옵션을 다음 \<경로 > 로그 파일 경로 여야 합니다. 사용 하는 경우는 **/sq** 옵션을 \<경로 >는 구조적 된 쿼리를 포함 하는 파일 경로 여야 합니다. \<Exportfile > 내보낸된 이벤트를 저장할 파일 경로입니다.|
|{al \| 아카이브 로그} \<Logpath > [/ /l:\<로캘 >]|자체 포함 된 형식으로 지정 된 로그 파일에 보관합니다. 로캘 이름의 하위 디렉터리가 만들어지고 로캘별 정보를 모든 해당 하위 디렉터리에 저장 됩니다. 디렉터리 및 로그 파일을 실행 하 여 만들어진 후 **wevtutil al**, 게시자 설치 되어 있는지 여부를 파일에 이벤트를 읽을 수 있습니다.|
|{cl \| 일반 로그} \<Logname > [/ bu:\<백업 >]|지정된 된 이벤트 로그에서 이벤트를 지웁니다. **/bu** 지운된 이벤트를 백업 하려면 옵션을 사용할 수 있습니다.|

## <a name="options"></a>변수

|       옵션       |                                                                                                                                                                                                                                                                 설명                                                                                                                                                                                                                                                                  |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /f:\<형식 >    |                                                                                                                                                               출력 XML 또는 텍스트 형식으로이 되도록 지정 합니다. 경우 \<형식 >는 XML 출력은 XML 형식으로 표시 됩니다. 경우 \<형식 >은 텍스트 출력 XML 태그 없이 표시 됩니다. 기본값은 Text입니다.                                                                                                                                                                |
|   /e:\<사용 >    |                                                                                                                                                                                                                                         로그를 사용 하지 않도록 설정 하거나 사용 합니다. \<설정 > true 또는 false 일 수 있습니다.                                                                                                                                                                                                                                          |
|  /i:\<격리 >   | 로그 격리 모드를 설정합니다. \<격리 > 시스템, 응용 프로그램 또는 사용자 지정 될 수 있습니다. 격리 모드는 로그의 로그는 같은 격리 클래스의 다른 로그 세션을 공유 하는지 여부를 결정 합니다. 대상 로그 공유 시스템 격리를 지정 하는 경우 시스템 로그를 사용 하 여 권한 쓰기입니다. 대상 로그 공유 응용 프로그램 격리를 지정 하면 응용 프로그램 로그를 사용 하 여 권한 쓰기입니다. 사용 하 여 보안 설명자를 제공 해야 사용자 지정 격리를 지정 하는 경우는 **/ca** 옵션입니다. |
|  /lfn:\<Logpath>   |                                                                                                                                                                                                           로그 파일 이름을 정의합니다. \<Logpath > 이벤트 로그 서비스에서이 로그에 대 한 이벤트를 저장 하는 위치 파일에 전체 경로입니다.                                                                                                                                                                                                           |
|  /rt:\<보존 >  |                                                            로그 보존 모드를 설정합니다. \<보존 > true 또는 false 일 수 있습니다. 로그 보존 모드 로그 최대 크기에 도달할 때 이벤트 로그 서비스의 동작을 결정 합니다. 이벤트 로그에는 최대 크기에 도달 하는 경우 로그 보존 모드가 true 기존 이벤트를 보존할 하 고 들어오는 이벤트는 삭제 됩니다. 로그 보존 모드 false 이면 들어오는 이벤트 로그에서 가장 오래 된 이벤트를 덮어씁니다.                                                             |
|    /ab:\<자동 >     |                                                                                                                                   로그 자동 백업 정책을 지정합니다. \<자동 > true 또는 false 일 수 있습니다. 이 값이 true 이면 로그는 백업할 자동으로 최대 크기에 도달 하면 합니다. 이 값이 true 이면 보존 (지정 된 고 **/rt** 옵션) 설정 해야 true로 합니다.                                                                                                                                    |
|   /ms:\<MaxSize>   |                                                                                                                                                                        로그의 최대 크기를 바이트 단위로 설정 합니다. 최소 로그 크기는 1048576 바이트 (1024KB) 및 로그 파일은 항상 64KB의 배수로 입력 되므로 반올림 됩니다 적절 하 게 합니다.                                                                                                                                                                         |
|    /l:\<수준 >     |                                                                                                                                                                     로그 수준 필터를 정의합니다. \<수준 > 유효한 수준 값이 될 수 있습니다. 이 옵션은 전용된 세션을 사용 하 여 로그에 적용할 수만 있습니다. 설정 하 여 수준 필터를 제거할 수 <Level> 0입니다.                                                                                                                                                                      |
|   /k:\<Keywords>   |                                                                                                                                                                                         로그의 키워드 필터를 지정합니다. \<키워드 > 모든 유효한 64 비트 키워드 마스크 될 수 있습니다. 이 옵션은 전용된 세션을 사용 하 여 로그에 적용할 수만 있습니다.                                                                                                                                                                                         |
|   /ca:\<채널 >   |                                                                                                                   이벤트 로그에 대 한 액세스 권한을 설정합니다. \<채널 > 보안 설명자 정의 언어 (SDDL)를 사용 하는 보안 설명자가 있습니다. SDDL 형식에 대 한 자세한 내용은 Microsoft 개발자 네트워크 (MSDN) 웹 사이트를 참조 하세요. ([https://msdn.microsoft.com](https://msdn.microsoft.com)).                                                                                                                    |
|    /c:\<Config>    |                                                                                                                                  구성 파일의 경로를 지정합니다. 이 옵션에 정의 된 구성 파일에서 읽을 로그 속성 하면 \<구성 >. 하는 경우이 옵션을 사용 하면를 지정 하지는 <Logname> 매개 변수입니다. 로그 이름은 구성 파일에서 읽힙니다.                                                                                                                                   |
|  /ge:\<메타 데이터 >   |                                                                                                                                                                                                                 이 게시자가 발생할 수 있는 이벤트에 대 한 메타 데이터 정보를 가져옵니다. \<메타 데이터 > true 또는 false 일 수 있습니다.                                                                                                                                                                                                                 |
|   /gm:\<Message>   |                                                                                                                                                                                                                       숫자 메시지 id입니다. 대신 실제 메시지를 표시합니다. \<메시지 > true 또는 false 일 수 있습니다.                                                                                                                                                                                                                        |
|   /lf:\<Logfile>   |                                                                                                                                                                                  로그 파일 또는 로그에서 이벤트를 읽어들여야 함을 지정 합니다. \<로그 파일 > true 또는 false 일 수 있습니다. True 이면 명령에 매개 변수는 로그 파일의 경로입니다.                                                                                                                                                                                   |
| /sq:\<Structquery> |                                                                                                                                                                                이벤트는 구조화 된 쿼리로 변수를 지정 합니다. \<Structquery > true 또는 false 일 수 있습니다. True 이면 <Path> 경로 구조적된 쿼리를 포함 하는 파일입니다.                                                                                                                                                                                |
|    /q:\<Query>     |                                                                                                                                                                     읽거나 내보낸 있는 이벤트를 필터링 하려면 XPath 쿼리를 정의 합니다. 이 옵션을 지정 하지 않으면 모든 이벤트가 반환 되거나 내보낸 됩니다. 이 옵션 사용할 수 없는 경우 **/sq** 그렇습니다.                                                                                                                                                                     |
|  /bm:\<책갈피 >   |                                                                                                                                                                                                                                 이전 쿼리에서 책갈피가 있는 파일의 경로를 지정 합니다.                                                                                                                                                                                                                                 |
|   /sbm:\<Savebm >   |                                                                                                                                                                                                             이 쿼리는 책갈피를 저장 하는 데 사용 되는 파일의 경로를 지정 합니다. 파일 이름 확장명은.xml 이어야 합니다.                                                                                                                                                                                                              |
|  /rd:\<방향 >  |                                                                                                                                                                                                   이벤트를 읽고 방향을 지정 합니다. \<방향 > true 또는 false 일 수 있습니다. True 인 경우, 가장 최근의 이벤트 먼저 반환 됩니다.                                                                                                                                                                                                   |
|    /l:\<로캘 >    |                                                                                                                                                                                          특정 로캘의 이벤트 텍스트를 인쇄 하는 데 사용 되는 로캘 문자열을 정의 합니다. 이벤트 형식을 사용 하 여 텍스트를 인쇄할 때만 사용할 수는 **/f** 옵션입니다.                                                                                                                                                                                          |
|    /c:\<Count>     |                                                                                                                                                                                                                                                  읽을 수 있는 이벤트의 최대 수를 설정 합니다.                                                                                                                                                                                                                                                  |
|   /e:\<요소 >    |                                                                                                                                                           XML에서 이벤트를 표시할 때 루트 요소가 포함 됩니다. \<요소 > 루트 요소 내에서 원하는 된 문자열입니다. 예를 들어 **/e:root** 인해 XML 루트 요소 쌍이 포함 된 \<루트 ></root>합니다.                                                                                                                                                            |
|  /ow:\<덮어쓰기 >  |                                                                                                                                                                 내보내기 파일을 덮어쓰도록 지정 합니다. \<덮어쓰기 > true 또는 false 일 수 있습니다. True 및 내보내기 파일에 지정 된 경우 <Exportfile> 이미 확인 하지 않고 덮어씁니다.                                                                                                                                                                 |
|   /bu:\<Backup>    |                                                                                                                                                                                                      지운된 이벤트를 저장할 파일의 경로를 지정 합니다. 백업 파일의 이름을.evtx 확장명을 포함 합니다.                                                                                                                                                                                                       |
|    r:\<원격 >    |                                                                                                                                                                                            원격 컴퓨터에서 명령을 실행 합니다. \<원격 > 원격 컴퓨터의 이름입니다. **im** 및 **um** 매개 변수는 원격 작업을 지원 하지 않습니다.                                                                                                                                                                                            |
|   /u:\<사용자 이름 >   |                                                                                                                                                                          원격 컴퓨터에 로그온 하는 다른 사용자를 지정 합니다. \<사용자 이름 > 양식 도메인 \ 사용자 또는 사용자의 사용자 이름이 있습니다. 이 옵션은만 적용 될 때의 **/r** 옵션을 지정 합니다.                                                                                                                                                                          |
|   /p:\<암호 >   |                                                                                                                                               사용자에 대 한 암호를 지정합니다. 경우는 **/u** 옵션을 사용 하 고이 옵션을 지정 하지 또는 \<암호 >는 " *", 사용자 암호를 입력 하 라는 메시지가 표시 됩니다. 이 옵션은만 적용 될 때 합니다 \* \*/u* \* 옵션을 지정 합니다.                                                                                                                                                |
|     >batchsettings-&lt\<Auth >     |                                                                                                                                                                                             원격 컴퓨터에 연결 하기 위한 인증 유형을 정의 합니다. \<Auth > 기본, Negotiate, Kerberos 또는 NTLM을 수 있습니다. 기본값은 협상 합니다.                                                                                                                                                                                              |
|  /uni:\<Unicode>   |                                                                                                                                                                                                             유니코드로 출력을 표시합니다. \<유니코드 > true 또는 false 일 수 있습니다. 경우 <Unicode> 유니코드로 출력은 그렇습니다.                                                                                                                                                                                                             |

## <a name="remarks"></a>설명

-   Sl 매개 변수와 함께 구성 파일을 사용합니다.

    구성 파일은 wevtutil gl의 출력으로 동일한 형식 사용 하 여 XML 파일로 \<Logname > /f: xml 합니다. 다음 예제에는 보존을 사용 하 고, autobackup, 응용 프로그램 로그에 최대 로그 크기를 설정 하는 구성 파일의 형식을 보여 줍니다.  
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <channel name="Application" isolation="Application"
    xmlns="https://schemas.microsoft.com/win/2004/08/events">
    <logging>
    <retention>true</retention>
    <autoBackup>true</autoBackup>
    <maxSize>9000000</maxSize>
    </logging>
    <publishing>
    </publishing>
    </channel>
    ```

## <a name="BKMK_examples"></a>예제

모든 로그의 이름을 나열 합니다.
```
wevtutil el
```
XML 형식으로 로컬 컴퓨터에서 시스템 로그에 대 한 구성 정보를 표시 합니다.
```
wevtutil gl System /f:xml
```
(구성 파일의 예는 설명 참조) 이벤트 로그 속성을 설정 하는 구성 파일을 사용 합니다.
```
wevtutil sl /c:config.xml
```
게시자에서 발생 시킬 수 있는 이벤트에 대 한 메타 데이터를 포함 하 여 Microsoft-Windows-이벤트 로그 이벤트 게시자에 대 한 정보를 표시 합니다.
```
wevtutil gp Microsoft-Windows-Eventlog /ge:true
```
게시자 및 로그 myManifest.xml 매니페스트 파일에서 설치 합니다.
```
wevtutil im myManifest.xml
```
게시자 및 로그 myManifest.xml 매니페스트 파일에서 제거 합니다.
```
wevtutil um myManifest.xml
```
텍스트 형식으로 응용 프로그램 로그에서 세 가지 가장 최근의 이벤트를 표시 합니다.
```
wevtutil qe Application /c:3 /rd:true /f:text
```
응용 프로그램 로그의 상태를 표시 합니다.
```
wevtutil gli Application 
```
C:\backup\system0506.evtx를 시스템 로그에서 이벤트를 내보냅니다.
```
wevtutil epl System C:\backup\system0506.evtx
```
C:\admin\backups\a10306.evtx에 저장 한 후 모든 응용 프로그램 로그에서 이벤트를 지웁니다.
```
wevtutil cl Application /bu:C:\admin\backups\a10306.evtx
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
