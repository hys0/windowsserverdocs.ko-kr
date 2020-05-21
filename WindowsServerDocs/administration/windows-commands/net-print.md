---
title: Net 인쇄
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f2febdb79f4d0429cfb1cd423188ed9fafc198c
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437258"
---
# <a name="net-print"></a>Net 인쇄

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 프린터 큐 또는 지정된 된 인쇄 작업에 대 한 정보를 표시 하거나 지정 된 인쇄 작업을 제어 합니다.
> [!NOTE]
> 이 명령은 Windows 7 및 Windows Server 2008 r 2에서 더 이상 사용 되지 되었습니다. 그러나 prnjobs.vbs, WMI(Windows Management Instrumentation) (WMI) 또는 Windows PowerShell cmdlet을 사용 하 여 여러 가지 동일한 작업을 수행할 수 있습니다. 자세한 내용은 [prnjobs.vbs](prnjobs.md), [WMI(Windows Management Instrumentation)](https://go.microsoft.com/fwlink/?LinkID=29991) ( https://go.microsoft.com/fwlink/?LinkID=29991) , [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=128426) () https://go.microsoft.com/fwlink/?LinkID=128426) 및 [TechNet 스크립트 센터 갤러리](https://go.microsoft.com/fwlink/?LinkId=164635) (를 참조 하세요 https://go.microsoft.com/fwlink/?LinkId=164635) .
> ## <a name="syntax"></a>구문
> ```
> Net print {\\<computerName>\<Sharename> |
> \\<computerName> <JobNumber> [/hold | /release | /delete]} [help]
> ```
> ### <a name="parameters"></a>매개 변수
>
> |               매개 변수               |                                                                                                                                                                                                                     설명                                                                                                                                                                                                                      |
> |----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |    \\\\<computerName>\\<Sharename>     |                                                                                                                                                                            에 대 한 정보를 표시 하려면 컴퓨터와 인쇄 큐 이름을 사용 하 여 지정 합니다.                                                                                                                                                                             |
> |           \\\\<computerName>           |                                                                                                                                 컨트롤에 인쇄 작업을 호스트 하는 컴퓨터 이름을 사용 하 여 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터 간주 됩니다. 필요는 <JobNumber> 매개 변수입니다.                                                                                                                                  |
> |              <JobNumber>               |                                             제어 하려는 인쇄 작업의 수를 지정 합니다. 이 숫자는 인쇄 작업 전송 대상 인쇄 큐를 호스팅하는 컴퓨터에서 할당 됩니다. 컴퓨터가 숫자에 할당 된 인쇄 작업을 수 해당 컴퓨터에서 호스팅하는 모든 큐의 다른 인쇄 작업에 할당 되지 않은 합니다. 매개 변수를 사용할 때 필요 \\ \\ <computerName> 합니다.                                             |
> | [/ 보류 & #124 /release & #124; /delete] | 인쇄 작업으로 수행할 동작을 지정 합니다.<p>- **보관/** 매개 변수는 작업을 지연 다른 인쇄 작업을 놓을 때까지를 무시 하도록 허용 합니다.<br />- **/릴리스** 매개 변수 연기 된 인쇄 작업을 해제 합니다.<br />- **/Delete** 매개 변수는 인쇄 대기열에서 인쇄 작업을 제거 합니다.<p>작업 번호를 지정 하지만 아무 작업도 지정 하지 않으면 인쇄 작업에 대 한 정보가 표시 됩니다. |
> |                  도움말                  |                                                                                                                                                                                                     에 대 한 도움말을 표시는 **인쇄 Net** 명령입니다.                                                                                                                                                                                                     |
>
>#### <a name="remarks"></a>설명
> - **Net** \\ \\ 인쇄 <computerName> 공유 프린터 큐의 인쇄 작업에 대 한 정보를 표시 합니다. 다음은 레이저 라는 공유 프린터에 대 한 큐에서 모든 인쇄 작업에 대 한 보고서의 예입니다.
>   ```
>   printers at \\PRODUCTION
>   Name              Job #      Size      Status
>   -----------------------------
>   LASER Queue       3 jobs               *printer active*
>      USER1          84        93844      printing
>      USER2          85        12555      Waiting
>      USER3          86        10222      Waiting
>   ```
> - 다음은 인쇄 작업에 대 한 보고서의 예입니다.
>   ```
>   Job #            35
>   Status           Waiting
>   Size             3096
>   remark
>   Submitting user  USER2
>   Notify           USER2
>   Job data type
>   Job parameters
>   additional info
>   ```
>   ## <a name="examples"></a>예
>   Dotmatrix 인쇄 큐의 내용을 나열 하는 방법을 보여 주는이 예제는 \\\Production 컴퓨터:
>   ```
>   Net print \\Production\Dotmatrix
>   ```
>   작업 번호 35에 대 한 정보를 표시 하는 방법을 보여 주는이 예제는 \\\Production 컴퓨터:
>   ```
>   Net print \\Production 35
>   ```
>   작업 번호 263를 지연 하는 방법을 보여 주는이 예제는 \\\Production 컴퓨터:
>   ```
>   Net print \\Production 263 /hold
>   ```
>   작업 번호 263에서 해제 하는 방법을 보여 주는이 예제는 \\\Production 컴퓨터:
>   ```
>   Net print \\Production 263 /release
>   ```
>   ## <a name="additional-references"></a>추가 참조
>   - [명령줄 구문 키](command-line-syntax-key.md) 
>    [인쇄 명령 참조](print-command-reference.md)
