---
title: typeperf
description: 명령 창 또는 로그 파일에 성능 데이터를 기록 하는 typeperf에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a996abc1417fdb6aa50370a942433716d8df2cbe
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721214"
---
# <a name="typeperf"></a>typeperf

**typeperf** 또는 로그 파일 명령 창에 명령 성능 데이터를 기록 합니다. 중지 하려면 **typeperf**, CTRL + C를 누릅니다.

## <a name="syntax"></a>구문

```
typeperf <counter [counter ...]> [options]
typeperf -cf <filename> [options]
typeperf -q [object] [options]
typeperf -qx [object] [options]
```

### <a name="parameters"></a>매개 변수

|매개 변수|Description|
|---------|-----------|
|\<카운터 [카운터 [...]] >|모니터링 하는 성능 카운터를 지정 합니다.|

> [!NOTE]
> counter>** \\는 \\Server1\Processor (0)\% 사용자 시간과**같은 * \\ \\Computer\Object (인스턴스) \ 카운터* 형식으로 된 성능 카운터의 전체 이름입니다. ** \<**

## <a name="options"></a>옵션

|                   옵션                   |                                                         설명                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               도움말 상황에 맞는 표시 합니다.                                               |
| -f \<CSV&verbar;TSV&verbar;BIN&verbar;SQL> |                                    출력 파일 형식을 지정합니다. 기본값은 CSV입니다.                                     |
|              -cf \<파일 이름>               |              줄당 하나의 카운터를 모니터링 하는 성능 카운터 목록을 포함 하는 파일을 지정 합니다.               |
|             -si < [[hh:] mm:] ss >             |                                  샘플 간격을 지정합니다. 기본값은 1 초입니다.                                   |
|               -o \<파일 이름>               |     출력 파일 또는 SQL 데이터베이스에 대 한 경로 지정합니다. 기본값은 STDOUT (명령 창에 기록).      |
|                -q [object]                 | 설치 된 카운터 (인스턴스가 없음)의 목록을 표시 합니다. 하나의 개체에 대 한 카운터를 나열 하려면 개체 이름을 포함 합니다. \*\*\*예 들어 |
|                -qx [object]                |        인스턴스와 함께 설치 된 카운터의 목록을 표시 합니다. 하나의 개체에 대 한 카운터를 나열 하려면 개체 이름을 포함 합니다.        |
|               -sc \<샘플>               |             수집 하는 샘플 수를 지정 합니다. CTRL + C를 누를 때까지 데이터를 수집 하는 것이 기본값이입니다.              |
|            -config \<파일 이름>             |                                    명령 옵션을 포함 하는 설정 파일을 지정 합니다.                                     |
|            -s \<computer_name>             |                   카운터 경로에 지정 된 컴퓨터가 있는 경우에 모니터링을 위해 원격 컴퓨터를 지정 합니다.                    |
|                     -y                     |                                        메시지를 표시 하지 않고 모든 질문에 예로 답변 합니다.                                        |

## <a name="examples"></a>예

- 로컬 컴퓨터의 성능 카운터 ** \\ \\프로세서 (_Total)\% 프로세서 시간** 값을 명령 창에 기록 하려면 CTRL + C를 누를 때까지 1 초의 기본 샘플 간격입니다.  
  ```
  typeperf \Processor(_Total)\% Processor Time
  ```  
- Domain2> 파일의 카운터 목록에 대 한 값을 **탭으로 구분** 된 파일 **tsv** 에 기록 합니다 .이 샘플 간격으로 5 초 후에 50 샘플이 수집 됩니다.  
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```  
- 카운터 개체 PhysicalDisk에 대해 인스턴스를 사용 하 여 설치 된 카운터를 쿼리하고 결과 목록을 **PhysicalDisk** 파일 **에 쓰도록 합니다.**  
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
