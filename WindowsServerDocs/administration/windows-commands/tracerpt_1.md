---
title: tracerpt
description: 이벤트 추적 로그, 성능 모니터에 의해 생성 된 로그 파일 및 실시간 이벤트 추적 공급자를 구문 분석 하는 tracerpt에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb9eaf86-0ef6-4197-b6c8-9cca8a1d723c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7060932f0b7eb996d0f0934e6945665c0c91e916
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935587"
---
# <a name="tracerpt"></a>tracerpt

**tracerpt** 명령을 이벤트 추적 로그, 성능 모니터 및 실시간 이벤트 추적 공급자에 의해 생성 된 로그 파일의 구문 분석을 사용할 수 있습니다. 덤프 파일, 보고서 파일 및 보고서 스키마를 생성합니다.

## <a name="syntax"></a>구문

```
tracerpt <[-l] <value [value [...]]>|-rt <session_name [session_name [...]]>> [options]
```

## <a name="options"></a>옵션

|              옵션 플래그               |                                                                    설명                                                                    |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
|                   -?                   |                                                         도움말 상황에 맞는 표시 합니다.                                                          |
|          -config\<filename>           |                                                 명령 옵션을 포함 하는 설정 파일을 로드 합니다.                                                  |
|                   -y                   |                                                  메시지를 표시 하지 않고 모든 질문에 예로 답변 합니다.                                                   |
|            -f\<XML\|HTML>             |                                                                  보고서 형식입니다.                                                                   |
|         -/\<CSV\|EVTX\|XML>          |                                                         덤프 형식입니다. 기본값은 XML입니다.                                                          |
|            -df\<filename>             |                                            Microsoft 전용 만들 스키마 파일 수를 계산/보고 합니다.                                            |
|            -int\<filename>            |                                            지정된 된 파일에 해석 된 이벤트 구조를 덤프 합니다.                                            |
|                  -rts                  |                        보고서는 이벤트 추적 헤더에서 원시 타임 스탬프입니다. -O,-보고서 말거나-요약와만 사용할 수 있습니다.                         |
|            -tmf\<filename>            |                                                  추적 메시지 형식 정의 파일을 지정 합니다.                                                  |
|              -tp\<value>              |                            TMF 파일 검색 경로 지정 합니다. 세미콜론 (;)으로 구분 된 여러 경로 사용할 수 있습니다.                            |
|              -i\<value>               | 공급자 이미지 경로 지정 합니다. 일치 하는 PDB 기호 서버에 배치 됩니다. 세미콜론 (;)으로 구분 된 여러 경로 사용할 수 있습니다. |
|             -pdb\<value>              |                             기호 서버 경로 지정 합니다. 세미콜론 (;)으로 구분 된 여러 경로 사용할 수 있습니다.                             |
|                  -gmt                  |                                              그리니치 표준시 WPP 페이로드 타임 스탬프를 변환 합니다.                                               |
|              -rl\<value>              |                                               시스템 보고서 수준 1에서 5로 정의 합니다. 기본값은 1입니다.                                               |
|          -요약 [filename]           |                                  요약 보고서 텍스트 파일을 생성 합니다. 지정 하지 않으면 파일에는 summary.txt입니다.                                   |
|             -o [filename]              |                                      텍스트 출력 파일을 생성 합니다. 지정 하지 않으면 파일에는 dumpfile.xml입니다.                                      |
|           -보고서 [filename]           |                                  텍스트 출력 보고서 파일을 생성 합니다. 지정 하지 않으면 파일에는 workload.xml입니다.                                   |
|                  -lr                   |                        덜 제한적인 값을 지정 합니다. 이 이벤트 스키마와 일치 하지 않는 이벤트에 대 한 최선의 노력을 사용 합니다.                         |
|           -[filename] 내보내기           |                                  이벤트 스키마 내보내기 파일을 생성 합니다. 지정 하지 않으면 파일에는 schema.man입니다.                                   |
|       [-l]\<value [value […]]>        |                                                   처리 이벤트 추적 로그 파일을 지정 합니다.                                                    |
| -rt\<session_name [session_name […]]> |                                                실시간 이벤트 추적 세션 데이터 소스를 지정 합니다.                                                |

## <a name="examples"></a>예

- 이 예제에서는 두 개의 이벤트 로그를 기반으로 보고서를 만듭니다 **logfile1.etl** 및 **logfile2.etl** 덤프 파일을 만들고 **logdump.xml** XML 형식에서입니다.
  ```
  tracerpt logfile1.etl logfile2.etl -o logdump.xml -of XML
  ```
- 이 예제에서는 이벤트 로그에 따라 보고서를 만드는 **logfile.etl**, 덤프 파일을 만듭니다 **logdmp.xml** XML 형식으로 사용 하 여 최상의 노력을 다는 스키마에 없는 이벤트를 식별 하는 요약 보고서 파일을 생성 **logdump.txt**, 보고서 파일을 생성 하 고 **logrpt.xml**합니다.
  ```
  tracerpt logfile.etl -o logdmp.xml -of XML -lr -summary logdmp.txt -report logrpt.xml
  ```
- 이 예제에서는 두 개의 이벤트 로그를 사용 하 여 **logfile1.etl** 및 **logfile2.etl** 덤프 파일을 기본 파일 이름 가진 보고서 파일을 생성 합니다.
  ```
  tracerpt logfile1.etl logfile2.etl -o -report
  ```
- 이 예제에서는 이벤트 로그를 사용 하 여 **logfile.etl** 성능 로그 및 **counterfile.blg** 보고서 파일을 생성 하 **logrpt.xml** 및 Microsoft 특정 XML 스키마 파일 **schema.xml**합니다.
  ```
  tracerpt logfile.etl counterfile.blg -report logrpt.xml -df schema.xml
  ```
- 이 예제에서는 실시간 이벤트 추적 세션 NT 커널로 거를 읽고 덤프 파일 **logfile.csv** 를 CSV 형식으로 생성 합니다.
  ```
  tracerpt -rt NT Kernel Logger -o logfile.csv -of CSV
  ```
