---
title: net 인쇄
description: Net print 명령에 대 한 참조 항목입니다. 이 명령은 더 이상 사용 되지 않으며 이후 버전의 Windows에서는 지원 되지 않습니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d8744c3ef4540652b495aea0037e97f433238f2
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354313"
---
# <a name="net-print"></a>net 인쇄

> [!IMPORTANT]
> 이 명령은 더 이상 사용 되지 않습니다. 그러나 [prnjobs.vbs 명령](prnjobs.md), [WMI(Windows Management Instrumentation) (WMI)](https://docs.microsoft.com/windows/win32/wmisdk/wmi-start-page), [POWERSHELL에서 printmanagement](https://docs.microsoft.com/powershell/module/printmanagement)또는 [IT 전문가를 위한 스크립트 리소스](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)를 사용 하 여 여러 가지 동일한 작업을 수행할 수 있습니다.

지정된 된 프린터 큐 또는 지정된 된 인쇄 작업에 대 한 정보를 표시 하거나 지정 된 인쇄 작업을 제어 합니다.

## <a name="syntax"></a>구문

```
net print {\\<computername>\<sharename> | \\<computername> <jobnumber> [/hold | /release | /delete]} [help]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `\\<computername>\<sharename>` | 에 대 한 정보를 표시 하려면 컴퓨터와 인쇄 큐 이름을 사용 하 여 지정 합니다. |
| `\\<computername>` | 컨트롤에 인쇄 작업을 호스트 하는 컴퓨터 이름을 사용 하 여 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터 간주 됩니다. 필요는 `<jobnumber>` 매개 변수입니다. |
| `<jobnumber>` | 제어 하려는 인쇄 작업의 수를 지정 합니다. 이 숫자는 인쇄 작업 전송 대상 인쇄 큐를 호스팅하는 컴퓨터에서 할당 됩니다. 컴퓨터가 숫자에 할당 된 인쇄 작업을 수 해당 컴퓨터에서 호스팅하는 모든 큐의 다른 인쇄 작업에 할당 되지 않은 합니다. 사용할 때 필요한는 `\\<computername>` 매개 변수입니다. |
| `[/hold | /release | /delete]` | 인쇄 작업으로 수행할 동작을 지정 합니다. 작업 번호를 지정 하지만 어떤 조치도 지정 하지 않는 경우에는 인쇄 작업에 대 한 정보가 표시 됩니다.<ul><li>**/보류** -작업을 지연 하 여 다른 인쇄 작업이 해제 될 때까지 무시 하도록 허용 합니다.</li><li>**/release** -지연 된 인쇄 작업을 해제 합니다.</li><li>**/delete** -인쇄 대기열에서 인쇄 작업을 제거 합니다.</li></ul> |
| 도움말 | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- `net print\\<computername>`명령은 공유 프린터 큐에 인쇄 작업에 대 한 정보를 표시 합니다. 다음은 *레이저*라는 공유 프린터에 대 한 큐의 모든 인쇄 작업에 대 한 보고서의 예입니다.

    ```
    printers at \\PRODUCTION
    Name              Job #      Size      Status
    -----------------------------
    LASER Queue       3 jobs               *printer active*
    USER1          84        93844      printing
    USER2          85        12555      Waiting
    USER3          86        10222      Waiting
    ```

- 다음은 인쇄 작업에 대 한 보고서의 예입니다.

    ```
    Job #            35
    Status           Waiting
    Size             3096
    remark
    Submitting user  USER2
    Notify           USER2
    Job data type
    Job parameters
    additional info
    ```

### <a name="examples"></a>예

* \\ 프로덕션* 컴퓨터에 *Dotmatrix* print queue의 콘텐츠를 나열 하려면 다음을 입력 합니다.

```
net print \\Production\Dotmatrix
```

* \\ 프로덕션* 컴퓨터에 작업 번호 *35* 에 대 한 정보를 표시 하려면 다음을 입력 합니다.

```
net print \\Production 35
```

* \\ 프로덕션* 컴퓨터에서 작업 번호 *263* 를 지연 시키려면 다음을 입력 합니다.

```
net print \\Production 263 /hold
```

* \\ 프로덕션* 컴퓨터에서 작업 번호 *263* 를 해제 하려면 다음을 입력 합니다.

```
net print \\Production 263 /release
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)

- [prnjobs.vbs 명령](prnjobs.md)

- [Windows Management Instrumentation(WMI)](https://docs.microsoft.com/windows/win32/wmisdk/wmi-start-page)

- [Powershell에서 PrintManagement](https://docs.microsoft.com/powershell/module/printmanagement)

- [IT 전문가를 위한 스크립트 리소스](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)
