---
title: schtasks
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e713203-3dd8-491b-b9e1-9423618dc7e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76ae264ded3cd0611c06b56c1074a2d916513da4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441608"
---
# <a name="schtasks"></a>schtasks



명령 및 프로그램이 정기적으로 또는 특정 시간에 실행 되도록 예약 합니다. 추가 및 일정에서 작업을 제거, 시작 요청 시 작업을 중지 하 고 표시 되며 및 예약 된 작업을 변경 합니다.

다음 명령 구문을 보려면 다음 명령 중 하나를 클릭 합니다.
-   [매개 변수 만들기](#BKMK_create)
-   [schtasks change](#BKMK_change)
-   [실행 매개 변수](#BKMK_run)
-   [schtasks 끝](#BKMK_end)
-   [매개 변수 삭제](#BKMK_delete)
-   [매개 변수 쿼리](#BKMK_query)

## <a name="remarks"></a>설명

- **SchTasks.exe** 와 같은 작업을 수행 **예약 된 작업** 에서 **제어판**합니다. 이러한 도구를 서로 교환해 서 사용할 수 있습니다.
- **Schtasks** 대체 **At.exe**, 이전 버전의 Windows에 포함 하는 도구입니다. 하지만 **At.exe** Windows Server 2003 제품군에 여전히 포함 되어 **schtasks** 권장된 명령줄 작업 일정 관리 도구입니다.
- 매개 변수는 **schtasks** 명령이 임의의 순서로 나타날 수 있습니다. 입력 **schtasks** 매개 변수는 쿼리를 수행 하지 않고 있습니다.
- 에 대 한 권한을 **schtasks**  
  -   명령을 실행할 수 있는 권한이 있어야 합니다. 모든 사용자는 로컬 컴퓨터에서 작업을 예약할 수 및 확인 하 고 예약 된 작업을 변경 합니다. Administrators 그룹의 구성원 예약, 보기 및 로컬 컴퓨터에 있는 모든 작업을 변경할 수 있습니다.
  -   일정을 보거나 변경 하려면 원격 컴퓨터에서 작업을 원격 컴퓨터에서 Administrators 그룹의 구성원 이어야 하거나 사용 해야는 **/u** 매개 변수는 원격 컴퓨터의 관리자의 자격 증명을 제공 합니다.
  -   사용할 수는 **/u** 매개 변수는 **만들기 /** 또는 **/변경** 로컬 및 원격 컴퓨터가 동일한 도메인에 있는지 또는 원격 컴퓨터 도메인에서 트러스트 된 도메인에는 로컬 컴퓨터의 경우에 작업입니다. 그렇지 않으면, 원격 컴퓨터의 지정 된 사용자 계정을 인증할 수 없는 하 고 계정이 Administrators 그룹의 구성원 인지 확인할 수 없습니다.
  -   작업을 실행할 수 있는 권한이 있어야 합니다. 작업에 필요한 권한이 달라 집니다. 기본적으로 작업 실행 하 여 지정 된 사용자의 권한으로 또는 로컬 컴퓨터의 현재 사용자의 권한으로는 **/u** 매개 변수를 포함 된 경우. 사용 하 여 파일을 다른 사용자 계정의 사용 권한으로 또는 시스템 권한으로 작업을 실행 하려면는 **/ru** 매개 변수입니다.
- 예약 된 작업 실행 했는지 확인 하거나 작업 스케줄러 서비스 트랜잭션 로그를 확인 하려면 이유는 예약 된 작업 실행 되지 않았거나 *SystemRoot*\SchedLgU.txt 합니다. 이 로그 레코드는 서비스를 사용 하는 모든 도구에서 시작한 실행 시도 포함 하 여 **예약 된 작업** 및 **SchTasks.exe**합니다.
- 경우에 따라 작업 파일이 손상 되었습니다. 손상 된 작업을 실행 하지 마십시오. 손상 된 작업에 대 한 작업을 수행 하려고 할 때 **SchTasks.exe** 다음과 같은 오류 메시지가 표시 됩니다.  
  ```
  ERROR: The data is invalid.
  ```  
  손상 된 작업을 복구할 수 없습니다. 작업 일정은 시스템의 기능을 복원 하려면 **SchTasks.exe** 또는 **예약 된 작업** 하는 시스템에서 작업을 삭제 하 고 일정을 조정 합니다.

## <a name="BKMK_create"></a>매개 변수 만들기

작업을 예약 합니다.

**Schtasks** 각 일정 유형에 대해 다른 매개 변수 조합을 사용 합니다. 작업을 만들기 위한 결합 된 구문을 또는 특정 일정 유형으로 작업을 만들기 위한 구문을 보려면 다음 옵션 중 하나를 클릭 합니다.
-   [결합 된 구문 및 매개 변수 설명](#BKMK_syntax)
-   [N 분 마다 실행 되는 작업을 예약 하려면](#BKMK_minutes)
-   [N 시간 마다 실행 되는 작업을 예약 하려면](#BKMK_hours)
-   [N 일 마다 실행 되는 작업을 예약 하려면](#BKMK_days)
-   [N 주마다를 실행 하는 작업을 예약 하려면](#BKMK_weeks)
-   [3 개월 마다 실행 되는 작업을 예약 하려면](#BKMK_months)
-   [특정 요일에 실행 되는 작업을 예약 하려면](#BKMK_spec_day)
-   [해당 월의 특정 주에 실행 되는 작업을 예약 하려면](#BKMK_spec_week)
-   [특정 날짜 각 월에 실행 되는 작업을 예약 하려면](#BKMK_spec_date)
-   [한 달의 마지막 날에 실행 되는 작업을 예약 하려면](#BKMK_last_day)
-   [한 번 실행 하는 작업을 예약 하려면](#BKMK_once)
-   [시스템을 시작할 때마다 실행 되는 작업을 예약 하려면](#BKMK_startup)
-   [로그온 하는 사용자를 실행 하는 작업을 예약 하려면](#BKMK_logon)
-   [시스템이 유휴 상태일 때 실행 되는 작업을 예약 하려면](#BKMK_idle)
-   [지금 실행 되는 작업을 예약 하려면](#BKMK_now)
-   [다른 사용 권한으로 실행 되는 작업을 예약 하려면](#BKMK_diff_perms)
-   [시스템 권한으로 실행 되는 작업을 예약 하려면](#BKMK_sys_perms)
-   [둘 이상의 프로그램을 실행 하는 작업을 예약 하려면](#BKMK_multi_progs)
-   [원격 컴퓨터에서 실행 되는 작업을 예약 하려면](#BKMK_remote)

### <a name="BKMK_syntax"></a>결합 된 구문 및 매개 변수 설명

#### <a name="syntax"></a>구문

```
schtasks /create /sc <ScheduleType> /tn <TaskName> /tr <TaskRun> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]] [/ru {[<Domain>\]<User> | System}] [/rp <Password>] [/mo <Modifier>] [/d <Day>[,<Day>...] | *] [/m <Month>[,<Month>...]] [/i <IdleTime>] [/st <StartTime>] [/ri <Interval>] [{/et <EndTime> | /du <Duration>} [/k]] [/sd <StartDate>] [/ed <EndDate>] [/it] [/z] [/f]
```

#### <a name="parameters"></a>매개 변수

##### <a name="sc-scheduletype"></a>/sc \<ScheduleType>

일정 유형을 지정합니다. 유효한 값은 분, 매시간, 매일, 매주, 매월 한 번, ONSTART, 유형에, ONIDLE 합니다.

|일정 유형|설명|
|-------------|-----------|
|분, 매시간, 매일, 매주, 매월|일정에 대 한 시간 단위를 지정합니다.|
|한 번|지정 된 날짜 및 시간에 작업을 한 번 실행 합니다.|
|ONSTART|시스템 시작 될 때마다 작업을 실행 합니다. 시작 날짜를 지정 하거나 다음 시스템을 시작할 때 작업을 실행 수 있습니다.|
|트리거|사용자 (사용자)가 로그온 할 때마다 작업을 실행 합니다. 날짜를 지정 하거나 다음에 사용자가 로그온 작업을 실행할 수 있습니다.|
|ONIDLE|작업에는 지정 된 시간 동안 시스템이 유휴 상태일 때마다 실행 됩니다. 다음에 시스템이 유휴 상태일 때 작업을 실행 하거나 날짜를 지정 수 있습니다.|

##### <a name="tn-taskname"></a>/tn \<작업 이름 >

작업에 대 한 이름을 지정합니다. 시스템에서 각 작업에는 고유한 이름이 있어야 합니다. 이름을 파일 이름에 대 한 규칙을 준수 해야 하며 238 자를 초과할 수 없습니다. 인용 부호를 사용 하 여 공백을 포함 하는 이름을 묶습니다.

##### <a name="tr-taskrun"></a>/tr \<TaskRun>

프로그램이 나 작업을 실행 하는 명령을 지정 합니다. 실행 파일, 스크립트 파일 또는 배치 파일의 정규화 된 경로 파일 이름을 입력 합니다. 경로 이름은 262 자를 초과할 수 없습니다. 경로 생략 하면 **schtasks** 파일에 있다고 가정은 *SystemRoot*\System32 디렉터리입니다.

##### <a name="s-computer"></a>/s \<컴퓨터 >

지정된 된 원격 컴퓨터에서 작업을 예약 합니다. 이름 또는 원격 컴퓨터 (백슬래시 없이 또는)의 IP 주소를 입력 합니다. 기본값은 로컬 컴퓨터입니다. **/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다.

##### <a name="u-domainuser"></a>/u [\<도메인 >\]<User>

이 명령은 지정된 된 사용자 계정 권한으로 실행 됩니다. 기본값은 로컬 컴퓨터의 현재 사용자의 권한. **/u** 및 **/p** 매개 변수는 원격 컴퓨터에서 작업을 예약할 경우에 유효한 ( **/s**).

지정 된 계정의 사용 권한 작업을 예약 하 고 작업을 실행에 사용 됩니다. 다른 사용자의 권한으로 작업을 실행 하려면 사용 합니다 **/ru** 매개 변수입니다.

사용자 계정에는 원격 컴퓨터에서 Administrators 그룹의 구성원 이어야 합니다. 또한 로컬 컴퓨터의 원격 컴퓨터와 동일한 도메인에 있어야 하거나 원격 컴퓨터 도메인에서 신뢰 하는 도메인에 있어야 합니다.

##### <a name="p-password"></a>/p \<Password>

에 지정 된 사용자 계정에 대 한 암호를 제공 된 **/u** 매개 변수입니다. 사용 하는 경우는 **/u** 매개 변수를 생략 하는 **/p** 매개 변수 또는 password 인수 **schtasks** 암호를 묻는 메시지를 표시 하 고 입력 한 텍스트를가 려 합니다.

**/u** 및 **/p** 매개 변수는 원격 컴퓨터에서 작업을 예약할 경우에 유효한 ( **/s**).

##### <a name="ru-domainuser--system"></a>/ru {[\<Domain>\]<User> | System}

지정 된 사용자 계정 권한으로 작업을 실행 합니다. 기본적으로 작업이 실행 하 여 지정 된 사용자의 사용 권한 또는 로컬 컴퓨터의 현재 사용자의 권한으로는 **/u** 매개 변수를 포함 된 경우. **/ru** 매개 변수는 로컬 또는 원격 컴퓨터에서 작업을 예약 하는 경우에 유효 합니다.


|       값        |                                                    설명                                                    |
|--------------------|-------------------------------------------------------------------------------------------------------------------|
| [\<Domain>\]<User> |                                       다른 사용자 계정을 지정합니다.                                        |
|    시스템 또는 ""    | 운영 체제와 시스템 서비스에서 사용 하는 강력한 권한의 계정이 로컬 시스템 계정을 지정 합니다. |

##### <a name="rp-password"></a>/rp \<암호 >

에 지정 된 사용자 계정에 대 한 암호를 제공 된 **/ru** 매개 변수입니다. 사용자 계정을 지정할 때이 매개 변수를 생략 하면 **SchTasks.exe** 암호를 묻는 메시지를 표시 하 고 입력 한 텍스트를가 려 합니다.

사용 하지 않는 **/rp** 시스템 계정 자격 증명으로 실행 하는 작업에 대 한 매개 변수 ( **/ru 시스템**). 시스템 계정에 암호가 없는 및 **SchTasks.exe** 하나 마다 표시 되지는 않습니다.

##### <a name="mo-modifier"></a>/ 월 \<한정자 >

일정 유형 내에서 작업을 실행 하는 빈도 지정 합니다. 이 매개 변수 유효 하지만 선택 사항 1 분을 시간별, 일별, 주별 및 월별 예약 합니다. 기본값은 1입니다.

|일정 유형|한정자 값|설명|
|-------------|---------------|-----------|
|MINUTE|1 - 1439|작업을 실행 마다 \<N > 분입니다.|
|시간 단위|1 - 23|작업을 실행 마다 \<N > 시간입니다.|
|매일|1 - 365|작업을 실행 마다 \<N > 일입니다.|
|매주|1 - 52|작업을 실행 마다 \<N > 주입니다.|
|한 번|한정자가 없습니다.|작업을 한 번 실행 합니다.|
|ONSTART|한정자가 없습니다.|작업 시작 시 실행합니다.|
|트리거|한정자가 없습니다.|작업을 실행 하 여 사용자 지정 하는 경우는 **/u** 매개 변수를 로그온 합니다.|
|ONIDLE|한정자가 없습니다.|시스템이 유휴 상태일 때 (분)로 지정 된 후 작업을 실행는 **/i** 매개 변수인 ONIDLE와 함께 사용 해야 합니다.|
|월별|1 - 12|작업을 실행 마다 \<N > 개월입니다.|
|월별|말일|월의 마지막 날에 작업을 실행 합니다.|
|월별|첫째, 둘째, 셋째, 넷째, 마지막|사용 된 **/d**\<일 > 매개 변수를 특정 주 및 일에 작업을 실행 합니다. 예를 들어 해당 월의 세 번째 수요일에.|

##### <a name="d-dayday--"></a>/d 요일 [,...] | *

주 또는 하루에 (또는 일) 한 달의 일 (또는 일)을 지정합니다. 매주 또는 매월 일정에만 유효 합니다.


| 일정 유형 |              보조키              |     날짜 값 (/d)      |                                                                                                 설명                                                                                                 |
|---------------|------------------------------------|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    매주     |               1 - 52               | 월요일-일요일 [, 월요일-일요일...] |                                                                                                     \*                                                                                                      |
|    월별    | 첫째, 둘째, 셋째, 넷째, 마지막 |        월요일-일요일         |                                                                                   특정 주 일정에 필요합니다.                                                                                    |
|    월별    |          없음 또는 {1-12}          |          1 - 31          | 선택 사항이 며 어떠한 한정자만 유효 ( **/월**) 매개 변수 (특정 날짜 일정) 때나 합니다 **/월** 가 1-12 (을 "모든 \<N > 개월" 일정). 기본값은 일 (월의 첫 번째 날) 1입니다. |

##### <a name="m-monthmonth"></a>/m 월 [,... 월]

한 달 또는 예약된 된 작업을 실행 해야 하는 연도의 월을 지정 합니다. 유효한 값은 JAN-DEC 및 * (매월). **/m** 매개 변수는 월별 일정에만 유효 합니다. 그는 말일 한정자를 사용 하는 경우에 필요 합니다. 그렇지 않으면 선택적 이며 기본값은 * (매월).

##### <a name="i-idletime"></a>/i \<IdleTime>

얼마나 많은 분 작업이 시작 되기 전에 컴퓨터가 유휴 상태일 지정 합니다. 유효한 값은 1에서 999 사이의 정수입니다. 이 매개 변수는 ONIDLE 일정에만 유효 하 고 필요한 됩니다.

##### <a name="st-starttime"></a>/st \<StartTime >

작업 시작 (시작)에 하루 중 시간을 지정 \<hh: mm > 24-시간 형식입니다. 기본값은 로컬 컴퓨터에 현재 시간입니다. **/st** 매개 변수는 사용할 수 분, 매시간, 매일, 매주, 매월 및 한 번을 예약 합니다. 한 번 일정 되어야합니다.

##### <a name="ri-interval"></a>/ri \<간격 >

되풀이 간격을 분 단위로 지정 합니다. 이 일정 유형에 적합 하지 않습니다. 분, 매시간, ONSTART, 유형 및 ONIDLE 합니다. 유효 범위는 599, 940을 1 분 (599940 분 = 9, 999 시간). /ET 또는 /DU를 지정 하는 되풀이 간격 기본 10 분입니다.

##### <a name="et-endtime"></a>/et \<EndTime>

분 또는 매시간 작업 일정의 종료 시간을 지정 \<hh: mm > 24-시간 형식입니다. 지정 된 종료 시간 이후 **schtasks** 오지 않습니다 작업 다시 시작 시간이 될 때까지 합니다. 기본적으로 작업 일정에는 종료 시간이 없습니다. 이 매개 변수가 선택적 이며 분 또는 매시간 일정에만 유효 합니다.

예를 들어, 다음을 참조 하십시오.
-   "100 분 업무 외 시간 마다 실행 되는 작업을 예약"는 **를 실행 하는 작업을 예약 하려면 모든** \<N > **분** 섹션입니다.

##### <a name="du-duration"></a>/du \<기간 >

분 또는 매시간 일정에 대 한 최대 기간 지정 \<hhhh: mm > 24-시간 형식입니다. 지정 된 시간이 경과 된 후 **schtasks** 오지 않습니다 작업 다시 시작 시간이 될 때까지 합니다. 기본적으로 작업 일정에는 최대 기간이 없습니다. 이 매개 변수가 선택적 이며 분 또는 매시간 일정에만 유효 합니다.

예를 들어, 다음을 참조 하십시오.
-   "10 시간 동안 3 시간 마다 실행 되는 작업을 예약"는 **를 실행 하는 작업을 예약 하려면 모든** \<N > **시간** 섹션입니다.

##### <a name="k"></a>/k

지정 된 시간에 작업을 실행 하는 프로그램을 중지 **/et** 또는 **/du**합니다. 없이 **/k**, **schtasks** 않습니다 하지 프로그램을 다시 시작 하 여 지정 된 시간에 도달한 후 **/et** 또는 **/du**, 하지만 여전히 실행 중이면 프로그램을 중지 하지 않습니다. 이 매개 변수가 선택적 이며 분 또는 매시간 일정에만 유효 합니다.

예를 들어, 다음을 참조 하십시오.
-   "100 분 업무 외 시간 마다 실행 되는 작업을 예약"는 **를 실행 하는 작업을 예약 하려면 모든** \<N > **분** 섹션입니다.

##### <a name="sd-startdate"></a>/sd \<StartDate >

작업 일정 시작 날짜를 지정 합니다. 기본값은 로컬 컴퓨터에 현재 날짜입니다. **/sd** 모든 일정을 형식에 대 한 유효 하 고 선택적 매개 변수는 합니다.

형식은 *StartDate* 로컬 컴퓨터에 대해 선택한 로캘에 따라 달라 지 며 **국가 및 언어 옵션** 에서 **제어판**합니다. 한 가지 형식만 각 로캘에 대해 유효합니다.

올바른 날짜 형식이 다음 표에 나열 됩니다. 가장에 대해 선택한 형식으로 유사한 형식을 사용 하 여 **간단한 날짜** 에서 **국가 및 언어 옵션** 에서 **제어판** 로컬 컴퓨터에 있습니다.


|       값       |                                        설명                                         |
|-------------------|--------------------------------------------------------------------------------------------|
| \<MM>/<DD>/<YYYY> | 와 같은, 월-첫 번째 형식에 사용할 **영어 (미국)** 및 **스페인어 (파나마)** 합니다. |
| \<DD>/<MM>/<YYYY> |       와 같은, 하루 첫 번째 형식에 사용할 **불가리아어** 및 **네덜란드어 (네덜란드)** 합니다.        |
| \<YYYY>/<MM>/<DD> |          와 같은, 연도가 먼저 나오는 형식에 사용할 **스웨덴어** 및 **프랑스어 (캐나다)** 합니다.          |

/ed \<EndDate >

일정 종료 날짜를 지정 합니다. 이 매개 변수는 선택 사항입니다. 한 번, ONSTART, 유형에 또는 ONIDLE 일정에 올바르지 않습니다. 기본적으로 일정에는 종료 날짜가 없습니다.

형식은 *EndDate* 로컬 컴퓨터에 대해 선택한 로캘에 따라 달라 지 며 **국가 및 언어 옵션** 에서 **제어판**합니다. 한 가지 형식만 각 로캘에 대해 유효합니다.

올바른 날짜 형식이 다음 표에 나열 됩니다. 가장에 대해 선택한 형식으로 유사한 형식을 사용 하 여 **간단한 날짜** 에서 **국가 및 언어 옵션** 에서 **제어판** 로컬 컴퓨터에 있습니다.


|       값       |                                        설명                                         |
|-------------------|--------------------------------------------------------------------------------------------|
| \<MM>/<DD>/<YYYY> | 와 같은, 월-첫 번째 형식에 사용할 **영어 (미국)** 및 **스페인어 (파나마)** 합니다. |
| \<DD>/<MM>/<YYYY> |       와 같은, 하루 첫 번째 형식에 사용할 **불가리아어** 및 **네덜란드어 (네덜란드)** 합니다.        |
| \<YYYY>/<MM>/<DD> |          와 같은, 연도가 먼저 나오는 형식에 사용할 **스웨덴어** 및 **프랑스어 (캐나다)** 합니다.          |

##### <a name="it"></a>/it

작업을 실행 하려면 지정 합니다. 경우에만 "으로 실행된" 사용자 (작업이 실행 되는 사용자 계정)가 컴퓨터에 로그온 합니다. 이 매개 변수는 시스템 권한으로 실행 되는 작업에 영향을 주지 않습니다.

기본적으로 "작업으로 실행된" 사용자가 작업을 예약할 때 로컬 컴퓨터의 현재 사용자 또는 지정 하는 계정을 **/u** 매개 변수를 사용 하는 경우. 그러나 명령에 포함 된 경우는 **/ru** 매개 변수를 다음의 "으로 실행된" 사용자 지정 되는 계정으로는 **/ru** 매개 변수입니다.

예제를 보려면 다음을 참조 합니다.
-   로그인 한 경우 70 일 마다 실행 되는 작업을 예약"하는 방법"에 **를 실행 하는 작업을 예약 하려면 모든** *N* **일** 섹션.
-   "때 특정 사용자만 작업을 실행 하는 로그인"는 **다른 사용 권한으로 실행 되는 작업을 예약 하려면** 섹션입니다.

##### <a name="z"></a>/z

일정 완료 시 작업을 삭제 하도록 지정 합니다.

##### <a name="f"></a>/f

작업을 만들고 지정한 작업이 이미 있는 경우 경고를 표시 하도록 지정 합니다.

##### <a name=""></a>/?

명령 프롬프트에 도움말을 표시합니다.

### <a name="BKMK_minutes"></a>N 분 마다 실행 되는 작업을 예약 하려면

#### <a name="minute-schedule-syntax"></a>분 단위 일정 구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc minute [/mo {1 - 1439}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [{/et <HH:MM> | /du <HHHH:MM>} [/k]] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

분 일정에는 **/sc 분** 매개 변수는 필수입니다. **/mo** (한정자) 매개 변수는 선택 사항이 며 작업의 실행 간격 (분)을 지정 합니다. 기본값 **/mo** 1 (분)입니다. **/et** (종료 시간) 및 **/du** (기간) 매개 변수는 선택 사항이 며 여부에 관계 없이 사용할 수는 **/k** (최종 작업) 매개 변수입니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-every-20-minutes"></a>20 분 마다 실행 되는 작업을 예약 하려면

다음 명령은 보안 스크립트 Sec.vbs 20 분 마다 실행 되도록 예약 합니다. 이 명령은 사용는 **/sc** 분 일정을 지정 하려면 매개 변수 및 **/mo** 매개 변수를 20 분의 간격을 지정 합니다.

명령이 시작 날짜나 시간이 포함 되어 있지 않으므로, 작업 명령이 완료 되 면 시스템은 실행 될 때마다 20 분 마다 실행 후 20 분을 시작 합니다. 하지만 보안 스크립트 원본 파일은 원격 컴퓨터에 있는 태스크가 예약 되 고 로컬 컴퓨터에서 실행을 확인 합니다.
```
schtasks /create /sc minute /mo 20 /tn "Security Script" /tr \\central\data\scripts\sec.vbs
```

#### <a name="to-schedule-a-task-that-runs-every-100-minutes-during-non-business-hours"></a>업무 외 시간 100 분 마다 실행 되는 작업을 예약 하려면

다음 명령은 보안, Sec.vbs를 실행 하는 스크립트는 로컬 컴퓨터에 100 오후 5시 분 마다 예약 오전 7 시 59 분 및 각 날짜입니다. 이 명령은 사용는 **/sc** 분 일정을 지정 하려면 매개 변수 및 **/mo** 매개 변수를 100 분의 간격을 지정 합니다. 사용 하 여는 **/st** 및 **/et** 시작 시간 및 각 날짜의 일정의 종료 시간을 지정 하는 매개 변수입니다. 또한 사용 하 여 **/k** 오전 7 시 59 분에 실행 중인 스크립트를 중지 하려면 매개 변수 없이 **/k**, **schtasks** 오전 7 시 59 분, 오전 6시 20분 인스턴스가 시작 하는 경우를 제외한 후 스크립트를 시작 합니다 가 실행 중 이더라도를 중지 하지 않습니다.
```
schtasks /create /tn "Security Script" /tr sec.vbs /sc minute /mo 100 /st 17:00 /et 08:00 /k
```

### <a name="BKMK_hours"></a>N 시간 마다 실행 되는 작업을 예약 하려면

#### <a name="hourly-schedule-syntax"></a>시간별 일정 구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc hourly [/mo {1 - 23}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [{/et <HH:MM> | /du <HHHH:MM>} [/k]] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

매시간 일정에는 **/sc 매시간** 매개 변수는 필수입니다. **/mo** (한정자) 매개 변수는 선택 사항이 며 작업의 각 실행 사이의 시간 수를 지정 합니다. 기본값 **/mo** 1 (1 시간)입니다. **/k** (최종 작업) 매개 변수는 선택 사항이 며 함께 사용할 수 **/et** (지정된 된 시간에 끝) 또는 **/du** (지정된 된 간격 후 끝).

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-every-five-hours"></a>5 시간 마다 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 2002 년 3 월의 첫 번째 날부터 5 시간 마다 실행 되도록 예약 합니다. 사용 하 여는 **/mo** 간격을 지정 하려면 매개 변수 및 **/sd** 매개 변수를 시작 날짜를 지정 합니다. 명령이 시작 시간을 지정 하지 않으므로, 현재 시간 시작 시간으로 사용 됩니다.

로컬 컴퓨터 사용 하도록 설정 되어 있으므로 **영어 (짐바브웨)** 옵션 **국가 및 언어 옵션** 에서 **제어판**, 시작 날짜 형식은 MM/DD/YYYY (2002-03-01).
```
schtasks /create /sc hourly /mo 5 /sd 03/01/2002 /tn "My App" /tr c:\apps\myapp.exe
```

#### <a name="to-schedule-a-task-that-runs-every-hour-at-five-minutes-past-the-hour"></a>5 분 사이 1 시간 마다 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램에서 5 분 지난 자정에 시작 1 시간 마다 실행 되도록 예약 합니다. 때문에 **/mo** 매개 변수를 생략 하면, 명령 (1) 시간 마다는 매시간 일정에 대 한 기본값을 그대로 사용 합니다. 오전 12시 05분 후이 명령을 실행 하는 경우 프로그램 다음 날까지 실행 되지 않습니다.
```
schtasks /create /sc hourly /st 00:05 /tn "My App" /tr c:\apps\myapp.exe
```

#### <a name="to-schedule-a-task-that-runs-every-3-hours-for-10-hours"></a>10 시간 동안 3 시간 마다 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램 10 시간 동안 3 시간 마다 실행 되도록 예약 합니다.

이 명령은 사용는 **/sc** 매시간 일정을 지정 하려면 매개 변수 및 **/mo** 매개 변수를 3 시간 간격을 지정 합니다. 사용 하 여는 **/st** 자정에 일정을 시작 하는 매개 변수 및 **/du** 매개 변수를 10 시간 이후에 종료 합니다. 프로그램 단 몇 분 동안 실행 되기 때문에 **/k** 매개 변수를 기간이 만료 될 때 실행 되는 경우에 프로그램을 중지, 필요는 없습니다.
```
schtasks /create /tn "My App" /tr myapp.exe /sc hourly /mo 3 /st 00:00 /du 0010:00
```
이 예제에서는 작업을 실행 오전 오전 12시 오전 3시 6 시와 오전 9시 작업은 기간이 10 시간을 하기 때문에 오후 12 시에 다시 실행 되지 않습니다. 대신, 오전 12 시에 다시 시작 다음 날입니다.

### <a name="BKMK_days"></a>N 일 마다 실행 되는 작업을 예약 하려면

#### <a name="daily-schedule-syntax"></a>일별 일정 구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc daily [/mo {1 - 365}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

매일 일정의 경우에 **/sc daily** 매개 변수는 필수입니다. **/mo** (한정자) 매개 변수는 선택 사항이 며 작업의 각 실행 사이의 일 수를 지정 합니다. 기본값 **/mo** 1 (매일)입니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-every-day"></a>매일 실행 되는 작업을 예약 하려면

다음 예제에서는 MyApp 프로그램이 하루에 한 번, 매일, 오전 8시 실행 되도록 예약 2002 년 12 월 31 일 될 때까지. 생략 하기 때문에 **/mo** 매개 변수를 1의 기본 간격이 매일 명령을 실행 하는 데 사용 됩니다.

이 예제에서는 로컬 컴퓨터 시스템으로 설정 되어 있으므로 **영어 (영국)** 옵션 **국가 및 언어 옵션** 에서 **제어판**, 종료 날짜 형식은 DD/MM/YYYY (31/12/2002)
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc daily /st 08:00 /ed 31/12/2002
```

#### <a name="to-schedule-a-task-that-runs-every-12-days"></a>12 일 마다 실행 되는 작업을 예약 하려면

다음 예제에서는 MyApp 프로그램이 12 일 마다 오후 1 시에 실행 되도록 예약 (13:00) 2002 년 12 월 31 일에 시작 합니다. 명령을 사용 하 여는 **/mo** 2 일 간격을 지정 하려면 매개 변수 및 **/sd** 및 **/st** 날짜와 시간을 지정 하는 매개 변수입니다.

이 예제에서는 시스템으로 설정 되어 있으므로 **영어 (짐바브웨)** 옵션 **국가 및 언어 옵션** 에서 **제어판**, 종료 날짜 형식은 MM/DD/YYYY (12/31/2002)
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc daily /mo 12 /sd 12/31/2002 /st 13:00
```

#### <a name="to-schedule-a-task-that-runs-every-70-days-if-i-am-logged-on"></a>로그인 한 경우 70 일 마다 실행 되는 작업을 예약 하려면

다음 명령은 보안 스크립트 Sec.vbs 70 일 마다 실행 되도록 예약 합니다. 이 명령은 사용는 **/mo** 매개 변수를 70 일 간격을 지정 합니다. 또한 사용 하 여는 **/it** 계정이 작업이 실행 되는 사용자가 컴퓨터에 로그온 하는 경우에 작업이 실행 되도록 지정 하려면 매개 변수입니다. 작업 내 사용자 계정 권한으로 실행 되므로, 로그온 되어 있는 경우에 작업이 실행 됩니다.
```
schtasks /create /tn "Security Script" /tr sec.vbs /sc daily /mo 70 /it
```

> [!NOTE]
> 대화형 전용 있는 작업을 확인 하려면 ( **/it**) 속성을 자세한 정보는 쿼리를 사용 하 여 **(/ /v 쿼리**). 지정한 작업의 자세한 정보 쿼리 표시에서 **/it**,  **로그온 모드** 필드의 값이 **대화형만**합니다.

### <a name="BKMK_weeks"></a>N 주마다를 실행 하는 작업을 예약 하려면

#### <a name="weekly-schedule-syntax"></a>주간 일정 구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc weekly [/mo {1 - 52}] [/d {<MON - SUN>[,MON - SUN...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

주간 일정에서는 **/sc 매주** 매개 변수는 필수입니다. **/mo** (한정자) 매개 변수는 선택 사항이 며 작업의 각 실행 사이의 주 수를 지정 합니다. 기본값 **/mo** 1 (매주)입니다.

주별 일정 수도 선택적인 **/d** 매개 변수에서 지정 된 요일 또는 매일 실행 되도록 작업을 예약할 수 ( *). 기본값은 월요일 (월요일). 매일 (* ) 옵션은 일별 작업을 예약 합니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-every-six-weeks"></a>6 주 간격을 실행 하는 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 6 주 간격 원격 컴퓨터에서 실행 되도록 예약 합니다. 명령을 사용 하는 **/mo** 매개 변수는 간격을 지정 합니다. 생략 하기 때문에 **/d** 매개 변수를 작업을 월요일에 실행 합니다.

이 명령은 또한 사용 하 여는 **/s** 원격 컴퓨터를 지정 하려면 매개 변수 및 **/u** 매개 변수를 사용자의 관리자 계정 권한으로 명령을 실행 합니다. 때문에 **/p** 매개 변수를 생략 하면 **SchTasks.exe** 관리자 계정 암호에 대 한 사용자 요청 합니다.

또한 명령을 원격으로 실행 되므로 모든 경로 MyApp.exe에 대 한 경로 포함 하 여 명령에서 원격 컴퓨터에서 경로를 참조 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 6 /s Server16 /u Admin01
```

#### <a name="to-schedule-a-task-that-runs-every-other-week-on-friday"></a>격주로 금요일에 실행 되는 작업을 예약 하려면

다음 명령을 다른 금요일 마다 실행 되도록 작업을 예약 합니다. 사용 하 여는 **/mo** 2 주 간격을 지정 하려면 매개 변수 및 **/d** 매개 변수는 요일을 지정할 수 있습니다. 실행 되는 작업 일정을 매주 금요일 생략는 **/mo** 매개 변수 1로 설정 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 2 /d FRI
```

### <a name="BKMK_months"></a>3 개월 마다 실행 되는 작업을 예약 하려면

#### <a name="syntax"></a>구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly [/mo {1 - 12}] [/d {1 - 31}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

이 일정 유형에 **/sc monthly** 매개 변수는 필수입니다. **/mo** 작업의 각 실행 간의 개월 수를 지정 하는 (한정자) 매개 변수는 선택 사항이 며 기본값은 1 (매월). 이 일정 유형 역시 선택적 **/d** 매개 변수는 월의 지정한 날짜에 실행 되도록 작업을 예약할 수 있습니다. 기본값은 1 (해당 월의 첫 번째 날)입니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-on-the-first-day-of-every-month"></a>매월 첫째 날에 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 매월 첫째 날에 실행 되도록 예약 합니다. 값이 1이 모두에 대 한 기본값 이기 때문은 **/mo** (한정자) 매개 변수 및 **/d** (일) 매개 변수를 명령에서 이러한 매개 변수는 생략 합니다.
```
schtasks /create /tn "My App" /tr myapp.exe /sc monthly
```

#### <a name="to-schedule-a-task-that-runs-every-three-months"></a>3 개월 마다 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 3 개월 마다 실행 되도록 예약 합니다. 사용 하 여는 **/mo** 매개 변수는 간격을 지정 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo 3
```

#### <a name="to-schedule-a-task-that-runs-at-midnight-on-the-21st-day-of-every-other-month"></a>다른 모든 월 21 일 자정에 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 개월 마다 자정에 월 21 일에 실행 되도록 예약 합니다. 이 명령은 2002 년 7 월 2 일 2003 년 6 월 30 일에서 1 년 동안이 작업이 실행 되도록 지정 합니다.

명령을 사용 하 여는 **/mo** (2 개월 마다), 월별 간격을 지정 하려면 매개 변수는 **/d** 날짜를 지정 하려면 매개 변수 및 **/st** 시간을 지정 합니다. 또한 사용 하 여는 **/sd** 및 **/ed** 시작을 지정 하는 매개 변수는 날짜 및 종료 날짜를 각각. 로컬 컴퓨터에 설정 되어 있으므로 **영어 (남아프리카 공화국)** 옵션 **국가 및 언어 옵션** 에서 **제어판**, 날짜 YYYY/MM/있습니다. 로컬 형식으로 지정 됩니다
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo 2 /d 21 /st 00:00 /sd 2002/07/01 /ed 2003/06/30 
```

### <a name="BKMK_spec_day"></a>특정 요일에 실행 되는 작업을 예약 하려면

#### <a name="weekly-schedule-syntax"></a>주간 일정 구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc weekly [/d {<MON - SUN>[,MON - SUN...] | *}] [/mo {1 - 52}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

"The week day" 일정은 주별 일정의 변형입니다. 주간 일정에서는 **/sc 매주** 매개 변수는 필수입니다. **/mo** (한정자) 매개 변수는 선택 사항이 며 작업의 각 실행 사이의 주 수를 지정 합니다. 기본값 **/mo** 1 (매주)입니다. **/d** 작업이 지정 된 요일 또는 매일 실행 되도록 예약 하는 매개 변수는 선택 항목인 (<em>). 기본값은 월요일 (월요일). 매일 옵션 (</em>* /d \** *)은 일별 작업을 예약 하는 것과 같습니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-every-wednesday"></a>실행 되는 작업 일정을 매주 수요일

다음 명령은 MyApp 프로그램이 매주 수요일에 실행 되도록 예약 합니다. 명령을 사용 하 여는 **/d** 매개 변수는 요일을 지정할 수 있습니다. 이 명령은 생략 때문에 **/mo** 매개 변수를 작업이 매주 실행 됩니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /d WED
```

#### <a name="to-schedule-a-task-that-runs-every-eight-weeks-on-monday-and-friday"></a>8 주마다 월요일과 금요일에 실행 되는 작업을 예약 하려면

다음 명령은 월요일과 8 번째 매주 금요일에 실행 되도록 작업을 예약 합니다. 사용 하 여는 **/d** 는 요일을 지정 하려면 매개 변수 및 **/mo** 매개 변수를 8 주 간격을 지정 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc weekly /mo 8 /d MON,FRI
```

### <a name="BKMK_spec_week"></a>해당 월의 특정 주에 실행 되는 작업을 예약 하려면

#### <a name="specific-week-syntax"></a>특정 주 구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /mo {FIRST | SECOND | THIRD | FOURTH | LAST} /d MON - SUN [/m {JAN - DEC[,JAN - DEC...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

이 일정 유형에 **/sc monthly** 매개 변수는 **/mo** (한정자) 매개 변수 및 **/d** (일) 매개 변수는 필요 합니다. **/mo** (한정자) 매개 변수는 작업이 실행 되는 주를 지정 합니다. **/d** 매개 변수는 요일을 지정 합니다. (이 일정 유형에 대 한 주 1 일에만 지정할 수 있습니다.) 이 일정에는 선택적 **/m** (월) 매개 변수를 사용 하면 특정 월 또는 매월 실행 하는 것에 대 한 작업을 예약 (<em>). 기본값은 * */m</em>* 매개 변수는 매월 (* ).

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-for-the-second-sunday-of-every-month"></a>작업 일정을 매월 두 번째 일요일

다음 명령은 MyApp 프로그램에서 매월 두 번째 일요일에 실행 되도록 예약 합니다. 사용 하 여는 **/mo** 월의 두 번째 주를 지정 하려면 매개 변수 및 **/d** 매개 변수를 지정 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo SECOND /d SUN
```

#### <a name="to-schedule-a-task-for-the-first-monday-in-march-and-september"></a>3 월과 9 월의 첫 번째 월요일에 대 한 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 년 3 월과 9 월의 첫 번째 월요일에 실행 되도록 예약 합니다. 사용 하 여는 **/mo** 월의 첫 번째 주를 지정 하려면 매개 변수 및 **/d** 매개 변수를 지정 합니다. 사용 하 여 **/m** 매개 변수를 월 인수는 쉼표로 구분 하는 월을 지정 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo FIRST /d MON /m MAR,SEP
```

### <a name="BKMK_spec_date"></a>특정 날짜 각 월에 실행 되는 작업을 예약 하려면

#### <a name="specific-date-syntax"></a>특정 날짜 구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /d {1 - 31} [/m {JAN - DEC[,JAN - DEC...] | *}] [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

특정 날짜 일정 유형에 **/sc monthly** 매개 변수 및 **/d** (일) 매개 변수는 필요 합니다. **/d** 매개 변수 (1-31) 요일을 차례로 하지 달의 날짜를 지정 합니다. 일정에만 1 일을 지정할 수 있습니다. **/mo** (한정자) 매개 변수는이 일정 형식으로 유효 하지 않습니다.

합니다 **/m** (월) 매개 변수는이 일정 유형에 대 한 선택 사항이 며 기본값은 매월 (<em>). **Schtasks</em>*  발생 하지 않는 날짜에 대 한 작업을 예약할 수 없습니다 지정 된 달에는 **/m** 매개 변수입니다. 그러나 경우 생략 된 **/m** 매개 변수 및 일정 달에는 31 번째 날, 다음 작업 등 특정 달에 표시 되지 않는 날짜에 대 한 작업 실행 되지 않습니다. 월의 마지막 날에 대 한 작업을 예약 하려면 마지막 날 일정 유형을 사용 합니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-for-the-first-day-of-every-month"></a>매월 첫째 날에 대 한 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 매월 첫째 날에 실행 되도록 예약 합니다. 기본 한정자 none (없음 한정자) 이기 때문에 기본 날짜는 1, 일 및 기본 월은 매월, 명령 추가 매개 변수를 필요 하지 않습니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly
```

#### <a name="to-schedule-a-task-for-the-15th-days-of-may-and-june"></a>5 월과 년 6 월 15 일에 대 한 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 오후 3 시 5 월 15 일과 6 월 15 일에 실행 되도록 예약 (15:00). 사용 하 여는 **/m** 날짜를 지정 하려면 매개 변수 및 **/m** 매개 변수를 월을 지정 합니다. 또한 사용 하 여는 **/st** 매개 변수를 시작 시간을 지정 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /d 15 /m MAY,JUN /st 15:00
```

### <a name="BKMK_last_day"></a>한 달의 마지막 날에 실행 되는 작업을 예약 하려면

#### <a name="last-day-syntax"></a>말일 구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc monthly /mo LASTDAY /m {JAN - DEC[,JAN - DEC...] | *} [/st <HH:MM>] [/sd <StartDate>] [/ed <EndDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

마지막 날 일정 유형에 **/sc monthly** 매개 변수는 **/mo 말일** (한정자) 매개 변수 및 **/m** (월) 매개 변수는 필요 합니다. **/d** (일) 매개 변수가 올바르지 않습니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-for-the-last-day-of-every-month"></a>매월 마지막 날에 대 한 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 매월 마지막 날에 실행 되도록 예약 합니다. 사용 하 여는 **/mo** 마지막 날을 지정 하려면 매개 변수 및 **/m** 프로그램 매월 실행 되도록 나타낼 와일드 카드 문자 (*)와 함께 매개 변수입니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo lastday /m *
```

#### <a name="to-schedule-a-task-at-600-pm-on-the-last-days-of-february-and-march"></a>오후 6 시에 작업을 예약 하려면 2 월과 년 3 월의 마지막 일

다음 명령은 MyApp 프로그램이 오후 6 시에 2 월의 마지막 날 및 년 3 월의 마지막 날에 실행 되도록 예약 사용 하 여는 **/mo** 마지막 날을 지정 하려면 매개 변수는 **/m** 월을 지정 하려면 매개 변수 및 **/st** 매개 변수를 시작 시간을 지정 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /mo lastday /m FEB,MAR /st 18:00
```

### <a name="BKMK_once"></a>한 번 실행 하는 작업을 예약 하려면

#### <a name="syntax"></a>구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc once /st <HH:MM> [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

한 번 실행 일정 유형에 **/sc 한 번** 매개 변수는 필수입니다. **/st** 작업이 실행 하는 시간을 지정 하는 매개 변수는 필수입니다. **/sd** 작업이 실행 되는 날짜를 지정 하는 매개 변수는 선택 사항입니다. **/mo** (한정자) 및 **/ed** (종료 날짜) 매개 변수는이 일정 유형에 적합 하지 않습니다.

**Schtasks** 허용 하지 않는 이전에는 날짜와 시간을 지정 하는 경우 한 번 실행 하는 작업을 예약 하는 로컬 컴퓨터의 시간에 따라 합니다. 다른 표준 시간대에 있는 원격 컴퓨터에서 한 번 실행 되는 작업을 예약 하려면 예약 해야 해당 날짜 전에 및 로컬 컴퓨터에서 시간에 발생 합니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-one-time"></a>한 번 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 2003 년 1 월 1 일 자정에 실행 되도록 예약 합니다. 사용 하 여는 **/sc** 일정 유형을 지정 하려면 매개 변수 및 **/sd** 및 **st** 날짜와 시간을 지정할 수 있습니다.

로컬 컴퓨터에서 사용 하기 때문에 **영어 (미국)** 옵션 **국가 및 언어 옵션** 에서 **제어판**, 시작 날짜 형식은 MM/DD/YYYY입니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc once /sd 01/01/2003 /st 00:00
```

### <a name="BKMK_startup"></a>시스템을 시작할 때마다 실행 되는 작업을 예약 하려면

#### <a name="syntax"></a>구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onstart [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

시작에 일정 유형에 **/sc onstart** 매개 변수는 필수입니다. **/sd** (시작 날짜) 매개 변수는 선택 사항이 며 기본값은 현재 날짜입니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-when-the-system-starts"></a>시스템을 시작할 때 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램 2001 년 3 월 15 일에 시작 하는 시스템을 시작할 때마다 실행 되도록 예약 합니다.

로컬 컴퓨터가 사용 하기 때문에 **영어 (미국)** 옵션 **국가 및 언어 옵션** 에서 **제어판**, 시작 날짜 형식은 MM/DD/YYYY입니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc onstart /sd 03/15/2001
```

### <a name="BKMK_logon"></a>로그온 하는 사용자를 실행 하는 작업을 예약 하려면

#### <a name="syntax"></a>구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onlogon [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

"로그온 시" 일정 유형을 모든 사용자가 컴퓨터에 로그온 할 때마다 실행 되는 작업을 예약 합니다. "로그온 시" 일정 유형에 **/sc 유형에** 매개 변수는 필수입니다. **/sd** (시작 날짜) 매개 변수는 선택 사항이 며 기본값은 현재 날짜입니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-when-a-user-logs-on-to-a-remote-computer"></a>사용자가 실행 되는 작업을 예약 하려면에 로그온 하 여 원격 컴퓨터

다음 명령은 사용자 (사용자)가 원격 컴퓨터에 로그온 할 때마다 실행 하는 배치 파일을 예약 합니다. 사용 하 여는 **/s** 매개 변수를 원격 컴퓨터를 지정 합니다. 명령이 원격 이면 배치 파일의 경로를 포함 하 여 명령에서 모든 경로 원격 컴퓨터의 경로를 참조 합니다.
```
schtasks /create /tn "Start Web Site" /tr c:\myiis\webstart.bat /sc onlogon /s Server23
```

### <a name="BKMK_idle"></a>시스템이 유휴 상태일 때 실행 되는 작업을 예약 하려면

#### <a name="syntax"></a>구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc onidle /i {1 - 999} [/sd <StartDate>] [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="remarks"></a>설명

유휴 상태 시"일정에 지정 된 시간 동안 사용자 작업이 없을 때마다 실행 되는 작업을 예약 하는 형식은 **/i** 매개 변수입니다. 유휴 상태 시"일정에서 형식에는 **/sc onidle** 매개 변수 및 **/i** 매개 변수는 필요 합니다. **/sd** (시작 날짜)은 선택 사항이 며 기본값은 현재 날짜입니다.

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-whenever-the-computer-is-idle"></a>컴퓨터가 유휴 상태일 때마다 실행 되는 작업을 예약 하려면

다음 명령은 MyApp 프로그램이 컴퓨터가 유휴 상태일 때마다 실행 되도록 예약 합니다. 필수 사용 하 여 **/i** 매개 변수 작업을 시작 하는 10 분 동안 컴퓨터 유휴 유지 해야 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc onidle /i 10
```

### <a name="BKMK_now"></a>지금 실행 되는 작업을 예약 하려면

**Schtasks** 않습니다 하지는 "실행" 이제 옵션 사용할 하지만 한 번 실행 하 고 잠시 후에 시작 하는 작업을 만들어 해당 옵션을 시뮬레이션할 수 있습니다.

#### <a name="syntax"></a>구문

```
schtasks /create /tn <TaskName> /tr <TaskRun> /sc once [/st <HH:MM>] /sd <MM/DD/YYYY> [/it] [/ru {[<Domain>\]<User> [/rp <Password>] | System}] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

#### <a name="examples"></a>예

#### <a name="to-schedule-a-task-that-runs-a-few-minutes-from-now"></a>실행을 예약 하려면 작업 하는 몇 분 지금부터입니다.

다음 명령은 오후 2시 18분 2002 년 11 월 13 일에 한 번 실행 하는 작업 예약 현지 시간입니다.

로컬 컴퓨터가 사용 하기 때문에 **영어 (미국)** 옵션 **국가 및 언어 옵션** 에서 **제어판**, 시작 날짜 형식은 MM/DD/YYYY입니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc once /st 14:18 /sd 11/13/2002
```

### <a name="BKMK_diff_perms"></a>다른 사용 권한으로 실행 되는 작업을 예약 하려면

로컬 및 원격 컴퓨터 모두에서 다른 계정의 권한으로 실행 하는 모든 종류의 작업을 예약할 수 있습니다. 특정 일정 유형에 필요한 매개 변수 외에 **/ru** 매개 변수는 필수 및 **/rp** 매개 변수는 선택적입니다.

#### <a name="examples"></a>예

#### <a name="to-run-a-task-with-administrator-permissions-on-the-local-computer"></a>로컬 컴퓨터에서 관리자 권한으로 작업을 실행 하려면

다음 명령은 MyApp 프로그램이 로컬 컴퓨터에서 실행 되도록 예약 합니다. 사용 하 여는 **/ru** 작업 사용자의 관리자 계정 (Admin06) 권한으로 실행 해야 함을 지정 합니다. 이 예제에서는 작업 화요일 마다 실행 되도록 예약 되었지만 다른 사용 권한으로 실행 되는 작업에 대 한 모든 일정 유형을 사용할 수 있습니다.
```
schtasks /create /tn "My App" /tr myapp.exe /sc weekly /d TUE /ru Admin06
```
응답으로 **SchTasks.exe** Admin06 계정에 대 한 "실행된 으로" 암호를 묻는 메시지를 표시 한 다음 성공 메시지를 표시 합니다.
```
Please enter the run as password for Admin06: ********
SUCCESS: The scheduled task "My App" has successfully been created.
```

#### <a name="to-run-a-task-with-alternate-permissions-on-a-remote-computer"></a>원격 컴퓨터에 다른 사용 권한으로 작업을 실행 하려면

다음 명령은 MyApp 프로그램이 4 일 마다 마케팅 컴퓨터에서 실행 되도록 예약 합니다.

이 명령은 **/sc** 일별 일정을 지정 하려면 매개 변수 및 **/mo** 매개 변수 4 일 간격을 지정 합니다.

명령을 사용 하 여는 **/s** 매개 변수는 원격 컴퓨터의 이름을 입력 하 고 **/u** 원격 컴퓨터에서 작업을 예약할 수 있는 권한이 있는 계정을 지정 하려면 매개 변수 (Admin01 마케팅 컴퓨터에서). 또한 사용 하 여는 **/ru** 작업 관리자가 아닌 사용자의 계정 권한으로 실행 해야 함을 지정 하려면 매개 변수 (User01 Reskits 도메인에서). 없이 **/ru** 매개 변수를 사용 하 여 지정 된 계정의 사용 권한 작업을 실행 **/u**합니다.
```
schtasks /create /tn "My App" /tr myapp.exe /sc daily /mo 4 /s Marketing /u Marketing\Admin01 /ru Reskits\User01
```
**Schtasks** 먼저 하 여 명명 된 사용자의 암호를 요청는 **/u** 매개 변수 (명령을 실행 하는)를 다음으로 명명 된 사용자의 암호를 요청 하 고는 **/ru** 실행할 매개 변수 (작업). 암호를 인증 한 후 **schtasks** 작업 일정을 나타내는 메시지를 표시 합니다.
```
Type the password for Marketing\Admin01:********

Please enter the run as password for Reskits\User01: ********

SUCCESS: The scheduled task "My App" has successfully been created.
```

#### <a name="to-run-a-task-only-when-a-particular-user-is-logged-on"></a>가 로그온 때 특정 사용자만 작업을 실행 하려면

다음 명령을 컴퓨터에서 실행 하는 공용 매주 금요일 오전 4시 컴퓨터의 관리자가 로그온 하는 경우 AdminCheck.exe 프로그램을 예약 합니다.

명령을 사용 하 여는 **/sc** 주간 일정을 지정 하려면 매개 변수는 **/d** 날짜를 지정 하려면 매개 변수 및 **/st** 매개 변수를 시작 시간을 지정 합니다.

명령을 사용 하 여는 **/s** 매개 변수는 원격 컴퓨터의 이름을 입력 하 고 **/u** 매개 변수를 원격 컴퓨터에서 작업을 예약할 수 있는 권한이 있는 계정을 지정 합니다. 또한 사용 하 여는 **/ru** (Public\Admin01) 공용 컴퓨터의 관리자 권한으로 실행 되도록 작업을 구성 하려면 매개 변수 및 **/it** Public\Admin01 계정의 로그온 하는 경우에 작업을 실행 함을 나타내기 위해 매개 변수입니다.
```
schtasks /create /tn "Check Admin" /tr AdminCheck.exe /sc weekly /d FRI /st 04:00 /s Public /u Domain3\Admin06 /ru Public\Admin01 /it
```
**참고**
-   대화형 전용 있는 작업을 확인 하려면 ( **/it**) 속성을 자세한 정보는 쿼리를 사용 하 여 **(/ /v 쿼리**). 지정한 작업의 자세한 정보 쿼리 표시에서 **/it**,  **로그온 모드** 필드의 값이 **대화형만**합니다.

### <a name="BKMK_sys_perms"></a>시스템 권한으로 실행 되는 작업을 예약 하려면

모든 종류의 작업 원격 컴퓨터와 로컬 시스템 계정 권한으로 실행할 수 있습니다. 특정 일정 유형에 필요한 매개 변수 외에 **/ru 시스템** (또는 **/ru ""** ) 매개 변수는 필수 및 **/rp** 매개 변수가 올바르지 않습니다.

**중요**
-   시스템 계정에 대화식 로그온 권한이 없습니다. 사용자가 보거나 프로그램과 상호 작용할 수 없는 또는 작업 시스템 권한으로 실행 합니다.
-   **/ru** 매개 변수는 작업이 실행 되는 작업을 예약 하는 데 사용 권한이 아닌 권한을 결정 합니다. 관리자의 값에 상관 없이 작업을 예약할 수만 **/ru** 매개 변수입니다.

**참고**

시스템 권한으로 실행 되는 작업을 식별 하려면 자세한 정보를 사용 하는 쿼리를 사용 하 여 (**쿼리** **/v**). 시스템 실행 하는 작업의 자세한 정보 쿼리 표시에는 **사용자로 실행** 필드의 값이 **NT AUTHORITY\SYSTEM** 및 **로그온 모드** 필드의 값이 **만 배경**합니다.

#### <a name="examples"></a>예

#### <a name="to-run-a-task-with-system-permissions"></a>시스템 권한으로 작업을 실행 하려면

다음 명령은 MyApp 프로그램이 시스템 계정의 사용 권한이 있는 로컬 컴퓨터에서 실행 되도록 예약 합니다. 이 예제에서는 작업 매월 15 번째 날에 실행 되도록 예약 되어 있지만 시스템 권한으로 실행 되는 작업에 대 한 모든 일정 유형을 사용할 수 있습니다.

이 명령은 사용는 **/ru System** 매개 변수를 시스템 보안 컨텍스트를 지정 합니다. 시스템 작업에서는 암호를 사용 하지 않으므로 **/rp** 매개 변수를 생략 합니다.
```
schtasks /create /tn "My App" /tr c:\apps\myapp.exe /sc monthly /d 15 /ru System
```
응답으로 **SchTasks.exe** 정보 메시지 및 성공 메시지가 표시 됩니다. 암호는 표시 하지 않습니다.
```
INFO: The task will be created under user name ("NT AUTHORITY\SYSTEM").
SUCCESS: The Scheduled task "My App" has successfully been created.
```

#### <a name="to-run-a-task-with-system-permissions-on-a-remote-computer"></a>원격 컴퓨터에서 시스템 권한으로 작업을 실행 하려면

다음 명령은 MyApp 프로그램이 Finance01 컴퓨터에서 매일 아침 오전 4 시에 실행 되도록 예약 시스템 사용 권한 사용

명령을 사용 하 여는 **/tn** 작업 이름을 지정 하는 매개 변수 및 **/tr** 매개 변수를 MyApp 프로그램에서의 원격 복사본을 지정 합니다. 사용 하 여는 **/sc** 일별 일정을 지정 하려면 매개 변수를 생략 되지만 **/mo** 매개 변수 1 (매일)이 고 기본값 이기 때문입니다. 사용 하 여는 **/st** 매개 변수는 중요 한 작업을 매일 실행할 시작 시간을 지정할 수 있습니다.

명령을 사용 하 여는 **/s** 매개 변수는 원격 컴퓨터의 이름을 입력 하 고 **/u** 매개 변수를 원격 컴퓨터에서 작업을 예약할 수 있는 권한이 있는 계정을 지정 합니다. 또한 사용 하 여는 **/ru** 매개 변수를 시스템 계정에서 작업을 실행 해야 함을 지정 합니다. 없이 **/ru** 매개 변수를 사용 하 여 지정 된 계정의 사용 권한 작업을 실행 **/u**합니다.
```
schtasks /create /tn "My App" /tr myapp.exe /sc daily /st 04:00 /s Finance01 /u Admin01 /ru System
```
**Schtasks** 하 여 명명 된 사용자의 암호를 요청은 **/u** 매개 변수 및 암호를 인증 한 후 작업이 만들어지고 시스템 계정의 사용 권한으로 실행 됨을 나타내는 메시지를 표시 합니다.
```
Type the password for Admin01:**********

INFO: The Schedule Task "My App" will be created under user name ("NT AUTHORITY\
SYSTEM").
SUCCESS: The scheduled task "My App" has successfully been created.
```

### <a name="BKMK_multi_progs"></a>둘 이상의 프로그램을 실행 하는 작업을 예약 하려면

각 작업이 하나의 프로그램을 실행합니다. 그러나 여러 프로그램을 실행 하는 배치 파일을 만들고 배치 파일을 실행 하는 작업을 예약할 수 있습니다. 다음 절차에서는이 메서드를 보여 줍니다.
1. 실행 하려는 프로그램을 시작 하는 배치 파일을 만듭니다.

   이 예제에서는 이벤트 뷰어 (Eventvwr.exe) 및 시스템 모니터 (Perfmon.exe)를 시작 하는 배치 파일을 만듭니다.  
   - 메모장과 같은 텍스트 편집기를 엽니다.
   - 각 프로그램 실행 파일에 정규화 된 경로 이름을 입력 합니다. 이 경우에 파일에 다음 문을 포함 합니다.  
     ```
     C:\Windows\System32\Eventvwr.exe 
     C:\Windows\System32\Perfmon.exe
     ```  
   - MyApps.bat로 파일을 저장 합니다.
2. 사용 하 여 **Schtasks.exe** MyApps.bat 실행 되는 작업을 만들려고 합니다.

   다음 명령은 모든 사용자가 로그온 할 때마다 실행 되는 모니터 작업을 만듭니다. 사용 하 여는 **/tn** 작업의 이름을 매개 변수 및 **/tr** 매개 변수 MyApps.bat를 실행 합니다. 사용 하 여는 **/sc** 유형에 일정 유형을 나타내는 매개 변수를 및 **/ru** 매개 변수를 사용자의 관리자 계정 권한으로 작업을 실행 합니다.  
   ```
   schtasks /create /tn Monitor /tr C:\MyApps.bat /sc onlogon /ru Reskit\Administrator
   ```  
   이 명령을 때마다 사용자는 컴퓨터에 로그온 하는 작업 시작 이벤트 뷰어와 시스템 모니터.

### <a name="BKMK_remote"></a>원격 컴퓨터에서 실행 되는 작업을 예약 하려면

원격 컴퓨터에서 실행 되도록 작업을 예약 하려면 원격 컴퓨터의 일정에 작업을 추가 해야 합니다. 원격 컴퓨터에서 모든 종류의 작업을 예약할 수 있지만 다음 조건이 충족 되어야 합니다.
-   작업을 예약할 수 있는 권한이 있어야 합니다. 따라서 원격 컴퓨터에서 Administrators 그룹의 구성원 인 계정으로 로컬 컴퓨터에 로그온 하거나 사용 해야는 **/u** 매개 변수는 원격 컴퓨터의 관리자의 자격 증명을 제공 합니다.
-   사용할 수는 **/u** 로컬 및 원격 컴퓨터가 동일한 도메인에 있는지 또는 원격 컴퓨터 도메인에서 트러스트 된 도메인에는 로컬 컴퓨터의 경우에 매개 변수입니다. 그렇지 않으면, 원격 컴퓨터의 지정 된 사용자 계정을 인증할 수 없는 하 고 계정이 Administrators 그룹의 구성원 인지 확인할 수 없습니다.
-   작업이 원격 컴퓨터에서 실행 되도록 충분 한 권한이 있어야 합니다. 작업에 필요한 권한이 달라 집니다. 기본적으로 로컬 컴퓨터의 현재 사용자의 권한으로 실행 하는 작업 또는 **/u** 매개 변수를 사용 하 여 지정 된 계정의 권한으로 실행 된 작업는 **/u** 매개 변수입니다. 사용할 수 있습니다는 **/ru** 매개 변수를 다른 사용자 계정의 사용 권한으로 또는 시스템 권한으로 작업을 실행 합니다.

#### <a name="examples"></a>예

#### <a name="an-administrator-schedules-a-task-on-a-remote-computer"></a>관리자는 원격 컴퓨터에서 작업 예약

다음 명령은 MyApp 프로그램이 즉시 시작 10 일 마다 SRV01 원격 컴퓨터에서 실행 되도록 예약 합니다. 이 명령은 사용는 **/s** 매개 변수를 원격 컴퓨터의 이름을 제공 합니다. 로컬 현재 사용자가 원격 컴퓨터의 관리자는 **/u** 작업을 예약 하는 것에 대 한 대체 권한의 제공 하는 매개 변수를 필요는 없습니다.

원격 컴퓨터에서 작업 예약, 모든 매개 변수는 원격 컴퓨터를 참조 note 하십시오. 지정 된 실행 파일 이므로 **/tr** 매개 변수는 원격 컴퓨터에서 MyApp.exe의 복사본을 참조 합니다.
```
schtasks /create /s SRV01 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc daily /mo 10
```
응답으로 **schtasks** 작업이 예약 됩니다 나타내는 성공 메시지를 표시 합니다.

#### <a name="a-user-schedules-a-command-on-a-remote-computer-case-1"></a>원격 컴퓨터 (사례 1)에서 명령을 예약 하는 경우

다음 명령은 MyApp 프로그램이 SRV06 원격 컴퓨터 3 시간 마다 실행 되도록 예약 합니다. 명령을 사용 하 여 작업을 예약 하려면 관리자 권한이 필요 합니다 때문에 **/u** 및 **/p** 사용자의 관리자의 자격 증명을 제공 하는 매개 변수 (Admin01 Reskits 도메인에서)를 고려 합니다. 기본적으로 이러한 권한은 작업을 실행 하도 사용 됩니다. 그러나 작업을 실행 하려면 관리자 권한이 필요 하지 않습니다, 명령에 포함 되어는 **/u** 및 **/rp** 기본값을 무시 하 고 원격 컴퓨터에서 사용자의 관리자가 아닌 계정 권한으로 작업을 실행 하는 매개 변수입니다.
```
schtasks /create /s SRV06 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc hourly /mo 3 /u reskits\admin01 /p R43253@4$ /ru SRV06\user03 /rp MyFav!!Pswd
```
응답으로 **schtasks** 작업이 예약 됩니다 나타내는 성공 메시지를 표시 합니다.

#### <a name="a-user-schedules-a-command-on-a-remote-computer-case-2"></a>원격 컴퓨터 (사례 2)에서 명령을 예약 하는 경우

다음 명령은 MyApp 프로그램이 매월 마지막 날에 SRV02 원격 컴퓨터에서 실행 되도록 예약 합니다. 명령을 사용 하 여 현재 로컬 사용자 (user03) 원격 컴퓨터의 관리자가 아니므로 **/u** 매개 변수를 사용자의 관리자의 자격 증명을 제공 계정 (Admin01 Reskits 도메인에서). 작업을 예약 하 고 작업을 실행 하려면 관리자 계정 권한이 사용 됩니다.
```
schtasks /create /s SRV02 /tn "My App" /tr "c:\program files\corpapps\myapp.exe" /sc monthly /mo LASTDAY /m * /u reskits\admin01
```
명령을 포함 하지 않은 때문에 **/p** (암호) 매개 변수를 **schtasks** 암호를 묻는 메시지를 표시 합니다. 다음 성공 메시지를 표시 하 고,이 경우 경고가 발생에서 합니다.
```
Type the password for reskits\admin01:********

SUCCESS: The scheduled task "My App" has successfully been created.

WARNING: The Scheduled task "My App" has been created, but may not run because
the account information could not be set.
```
이 경고는 원격 도메인 지정 하는 계정을 인증할 수 없습니다 나타냅니다는 **/u** 매개 변수입니다. 이 경우 원격 도메인 로컬 컴퓨터가 원격 컴퓨터 도메인에서 트러스트 된 도메인의 구성원이 아니므로 사용자 계정을 인증 하지 못했습니다. 이 경우 작업 작업 예약 된 작업의 목록에 표시 되지만 작업이 실제로 비어 있으며 실행 되지 않습니다.

자세한 정보는 쿼리에서 다음 표시 작업의 문제를 노출합니다. 디스플레이의 값 **다음 실행 시간** 는 **사용 안 함** 하 고 값을 **사용자로 실행** 는 **작업 스케줄러 데이터베이스에서 검색할 수 없습니다**합니다.

이 컴퓨터는 동일한 도메인 또는 트러스트 된 도메인의 멤버 였던는 성공적으로 예약 된 작업과 실행 되었던 지정 된 대로입니다.
```
HostName: SRV44
TaskName: My App
Next Run Time: Never
Status:
Logon mode: Interactive/Background
Last Run Time: Never
Last Result: 0
Creator: user03
Schedule: At 3:52 PM on day 31 of every month, start
 starting 12/14/2001
Task To Run: c:\program files\corpapps\myapp.exe
Start In: myapp.exe
Comment: N/A
Scheduled Task State: Disabled
Scheduled Type: Monthly
Start Time: 3:52:00 PM
Start Date: 12/14/2001
End Date: N/A
Days: 31
Months: JAN,FEB,MAR,APR,MAY,JUN,JUL,AUG,SEP,OCT,NO
V,DEC
Run As User: Could not be retrieved from the task sched
uler database
Delete Task If Not Rescheduled: Enabled
Stop Task If Runs X Hours and X Mins: 72:0
Repeat: Every: Disabled
Repeat: Until: Time: Disabled
Repeat: Until: Duration: Disabled
Repeat: Stop If Still Running: Disabled
Idle Time: Disabled
Power Management: Disabled
```

#### <a name="remarks"></a>설명

-   실행 하는 **/create** 명령을 사용 하 여 다른 사용자의 권한으로는 **/u** 매개 변수입니다. **/u** 매개 변수는 원격 컴퓨터에서 작업을 예약할 경우에 유효 합니다.
-   더 **schtasks /create** 예제에서 형식 **schtasks 만들기 / /?** .
-   사용 하 여 다른 사용자의 권한으로 실행 되는 작업을 예약 하려면는 **/ru** 매개 변수입니다. **/ru** 매개 변수는 로컬 및 원격 컴퓨터에서 작업에 대 한 유효 합니다.
-   사용 하 여 **/u** 매개 변수를 로컬 컴퓨터에서 원격 컴퓨터와 동일한 도메인에 있어야 또는 원격 컴퓨터 도메인에서 트러스트 된 도메인에 있어야 합니다. 그렇지 않으면 작업이 만들어지지 않습니다 또는 태스크 작업은 빈 나 작업이 실행 되지 않습니다.
-   **Schtasks** 제공 하지 않는 한, 현재 사용자 계정을 사용 하 여 로컬 컴퓨터에서 작업을 예약 하는 경우에 암호를 항상 메시지를 표시 합니다. 이 정상적인 동작에 대 한 **schtasks**합니다.
-   **Schtasks** 프로그램 파일의 위치 또는 사용자 계정 암호를 확인 하지 않습니다. 사용자 계정에 대 한 올바른 파일 위치 또는 올바른 암호를 입력 하지 않으면 작업은 만들어지지만 실행 되지 않습니다. 또한 계정의 암호가 변경 되거나 만료 되 면 및 작업에 저장 된 암호를 변경 하지 않는 경우 다음 작업이 실행 되지 않습니다.
-   시스템 계정에 대화식 로그온 권한이 없습니다. 사용자는 표시 되지 않으면 및 시스템 권한으로 실행 하는 프로그램과 상호 작용할 수 없습니다.
-   각 작업이 하나의 프로그램을 실행합니다. 그러나 여러 작업을 시작 하는 일괄 처리 파일을 만들고 배치 파일을 실행 하는 작업을 예약할 수 있습니다.
-   만든 즉시 작업을 테스트할 수 있습니다. 사용 하 여는 **실행** 작업을 테스트 하 고 다음 SchedLgU.txt 파일을 확인 하는 작업 (*SystemRoot*\SchedLgU.txt) 오류입니다.

## <a name="BKMK_change"></a>매개 변수 변경

작업의 다음 속성 중 하나 이상을 변경합니다.
-   작업을 실행 하는 프로그램 ( **/tr**).
-   작업이 실행 되는 사용자 계정 ( **/ru**).
-   사용자 계정의 암호 ( **/rp**).
-   작업에 전용 속성을 추가 ( **/it**).

### <a name="syntax"></a>구문

```
schtasks /change /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]] [/ru {[<Domain>\]<User> | System}] [/rp <Password>] [/tr <TaskRun>] [/st <StartTime>] [/ri <Interval>] [{/et <EndTime> | /du <Duration>} [/k]] [/sd <StartDate>] [/ed <EndDate>] [/{ENABLE | DISABLE}] [/it] [/z]
```

### <a name="parameters"></a>매개 변수

|          용어           |                                                                                                                                                                                                                                                                                                                                     정의                                                                                                                                                                                                                                                                                                                                      |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /tn \<작업 이름 >     |                                                                                                                                                                                                                                                                                                               변경 작업을 식별 합니다. 작업 이름을 입력 합니다.                                                                                                                                                                                                                                                                                                               |
|     /s \<컴퓨터 >      |                                                                                                                                                                                                                                                                               (백슬래시 없이 또는) 이름 또는 원격 컴퓨터의 IP 주소를 지정합니다. 기본값은 로컬 컴퓨터입니다.                                                                                                                                                                                                                                                                               |
|  /u [\<도메인 >\]<User>  |                                                                                                                                                                 이 명령은 지정된 된 사용자 계정 권한으로 실행 됩니다. 기본값은 로컬 컴퓨터의 현재 사용자의 권한. 지정된 된 사용자 계정에는 원격 컴퓨터에서 Administrators 그룹의 구성원 이어야 합니다. **/u** 및 **/p** 매개 변수는 원격 컴퓨터에서 작업 변경에 대해서만 유효 ( **/s**).                                                                                                                                                                  |
|     /p \<Password>      |                                                                                                                                                                                              에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. 사용 하는 경우는 **/u** 매개 변수를 생략 하는 **/p** 매개 변수 또는 password 인수 **schtasks** 암호를 묻는 메시지가 표시 됩니다.</br>**/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다.                                                                                                                                                                                               |
| /ru {[\<Domain>\]<User> |                                                                                                                                                                                                                                                                                                                                       System}                                                                                                                                                                                                                                                                                                                                       |
|     /rp \<암호 >     |                                                                                                                                                                                                                                                 기존 사용자 계정 또는 지정 된 사용자 계정에 대 한 새 암호를 지정 된 **/ru** 매개 변수입니다. 이 매개 변수는 로컬 시스템 계정으로 사용 된 무시 됩니다.                                                                                                                                                                                                                                                  |
|     /tr \<TaskRun>      |                                                                                                                                                                                  작업을 실행 하는 프로그램을 변경 합니다. 실행 파일, 스크립트 파일 또는 배치 파일의 정규화 된 경로 파일 이름을 입력 합니다. 경로 생략할 경우 **schtasks** 파일에 있다고 가정 합니다 \<systemroot > \System32 디렉터리입니다. 지정된 된 프로그램 작업이 실행 되는 원래 프로그램을 대체 합니다.                                                                                                                                                                                  |
|    /st \<Starttime >     |                                                                                                                                                                                                                                                              24 시간 형식 hh: mm를 사용 하 여 작업에 대 한 시작 시간을 지정 합니다. 예를 들어 오후 14시 30분 2 시 30 분의 12 시간제과 같습니다.                                                                                                                                                                                                                                                               |
|     /ri \<간격 >     |                                                                                                                                                                                                                                                                           예약된 된 작업에 대 한 되풀이 간격을 분 단위로 지정 합니다. 유효 범위는 1-599940 (599940 분 = 9, 999 시간).                                                                                                                                                                                                                                                                            |
|     /et \<EndTime>      |                                                                                                                                                                                                                                                               24 시간 형식 hh: mm를 사용 하 여 작업에 대 한 종료 시간을 지정 합니다. 예를 들어 오후 14시 30분 2 시 30 분의 12 시간제과 같습니다.                                                                                                                                                                                                                                                                |
|     /du \<기간 >     |                                                                                                                                                                                                                                                                                                     작업을 닫으려면 지정는 \<EndTime > 또는 <Duration>, 지정 된 경우.                                                                                                                                                                                                                                                                                                      |
|           /k            |                                                                                                                                                                   지정 된 시간에 작업을 실행 하는 프로그램을 중지 **/et** 또는 **/du**합니다. 없이 **/k**, **schtasks** 않습니다 하지 프로그램을 다시 시작 하 여 지정 된 시간에 도달한 후 **/et** 또는 **/du**, 하지만 여전히 실행 중이면 프로그램을 중지 하지 않습니다. 이 매개 변수가 선택적 이며 분 또는 매시간 일정에만 유효 합니다.                                                                                                                                                                   |
|    /sd \<StartDate >     |                                                                                                                                                                                                                                                                                              태스크를 실행 해야 하는 첫 번째 날짜를 지정 합니다. 날짜 형식은 MM/DD/YYYY입니다.                                                                                                                                                                                                                                                                                               |
|     /ed \<EndDate >      |                                                                                                                                                                                                                                                                                                 태스크를 실행 해야 하는 마지막 날짜를 지정 합니다. 형식은 MM/DD/YYYY입니다.                                                                                                                                                                                                                                                                                                  |
|         / 사용 사용         |                                                                                                                                                                                                                                                                                                                       예약 된 작업을 사용 하도록 지정 합니다.                                                                                                                                                                                                                                                                                                                       |
|        / 사용 안 함         |                                                                                                                                                                                                                                                                                                                      예약된 된 작업을 사용 하지 않도록 설정 하려면이 옵션을 지정 합니다.                                                                                                                                                                                                                                                                                                                       |
|           /it           | 예약된 된 작업을 실행 하도록 지정 경우에만 "으로 실행된" 사용자 (작업이 실행 되는 사용자 계정)가 컴퓨터에 로그온 합니다.</br>이 매개 변수는 시스템 권한으로 실행 되는 작업 또는 대화형 전용 속성 집합에 이미 있는 작업에 영향을 주지 않습니다. 속성을 제거 하는 전용 작업에서 변경 명령을 사용할 수 없습니다.</br>기본적으로 "작업으로 실행된" 사용자가 작업을 예약할 때 로컬 컴퓨터의 현재 사용자 또는 지정 하는 계정을 **/u** 매개 변수를 사용 하는 경우. 그러나 명령에 포함 된 경우는 **/ru** 매개 변수를 다음의 "으로 실행된" 사용자 지정 되는 계정으로는 **/ru** 매개 변수입니다. |
|           /z            |                                                                                                                                                                                                                                                                                                          일정 완료 시 작업을 삭제 하도록 지정 합니다.                                                                                                                                                                                                                                                                                                          |
|           /?            |                                                                                                                                                                                                                                                                                                                        명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                                                                                                                                         |

### <a name="remarks"></a>설명

-   **/tn** 및 **/s** 매개 변수는 작업을 식별 합니다. **/tr**, **/ru**, 및 **/rp** 매개 변수는 변경할 수 있는 작업의 속성을 지정 합니다.
-   **/ru**, 및 **/rp** 매개 변수는 작업이 실행 되는 사용 권한을 지정 합니다. **/u** 및 **/p** 매개 변수는 작업을 변경 하는 데 사용 권한을 지정 합니다.
-   원격 컴퓨터에서 작업을 변경 하려면 사용자는 원격 컴퓨터에서 Administrators 그룹의 구성원 인 계정으로 로컬 컴퓨터에 로그온 해야 합니다.
-   실행 하는 **/변경** 다른 사용자의 권한으로 명령 ( **/u**, **/p**), 로컬 컴퓨터에서 원격 컴퓨터와 동일한 도메인에 있어야 또는 원격 컴퓨터 도메인에서 트러스트 된 도메인에 있어야 합니다.
-   시스템 계정에 대화식 로그온 권한이 없습니다. 사용자는 표시 되지 않으면 및 시스템 권한으로 실행 하는 프로그램과 상호 작용할 수 없습니다.
-   사용 하 여 작업을 식별 하는 **/it** 속성을 자세한 정보는 쿼리를 사용 하 여 ( **//v 쿼리**). 지정한 작업의 자세한 정보 쿼리 표시에서 **/it**,  **로그온 모드** 필드의 값이 **대화형만**합니다.

### <a name="examples"></a>예

### <a name="to-change-the-program-that-a-task-runs"></a>작업을 실행 하는 프로그램을 변경 하려면

다음 명령은 VirusCheck2.exe에 VirusCheck.exe에서 바이러스 검사 태스크를 실행 하는 프로그램을 변경 합니다. 이 명령을 사용 하 여는 **/tn** 매개 변수 작업을 식별 하 고 **/tr** 매개 변수는 작업에 대 한 새 프로그램을 지정 합니다. (작업 이름을 변경할 수 없습니다.)
```
schtasks /change /tn "Virus Check" /tr C:\VirusCheck2.exe
```
응답으로 **SchTasks.exe** 성공 메시지를 표시 합니다.
```
SUCCESS: The parameters of the scheduled task "Virus Check" have been changed.
```
이 명령을 바이러스 검사 태스크는 이제 VirusCheck2.exe 실행 됩니다.

### <a name="to-change-the-password-for-a-remote-task"></a>원격 작업에 대 한 암호를 변경 하려면

다음 명령은 원격 컴퓨터 s v r 01에서 RemindMe 작업에 대 한 사용자 계정의 암호를 변경 합니다. 명령을 사용 하 여는 **/tn** 매개 변수 작업을 식별 하 고 **/s** 매개 변수를 원격 컴퓨터를 지정 합니다. 사용 된 **/rp** 새 암호를 지정 하려면 매개 변수 p@ssWord3합니다.

이 절차는 사용자 계정의 암호가 만료 되거나 변경 될 때마다 필요 합니다. 작업에 저장 된 암호를 더 이상 사용할 수, 작업이 실행 되지 않습니다.
```
schtasks /change /tn RemindMe /s Svr01 /rp p@ssWord3
```
응답으로 **SchTasks.exe** 성공 메시지를 표시 합니다.
```
SUCCESS: The parameters of the scheduled task "RemindMe" have been changed.
```
이 명령을 RemindMe 작업 지금 실행의 원래 사용자 계정 되지만 새 암호를 입력 합니다.

### <a name="to-change-the-program-and-user-account-for-a-task"></a>작업에 대 한 프로그램 및 사용자 계정을 변경 하려면

다음 명령은 작업을 실행 하는 프로그램 및 사용자 태스크가 실행 되는 계정을 변경 변경 합니다. 기본적으로, 새 작업에 대 한 이전 일정을 사용 합니다. 이 명령은 Notepad.exe를 매일 아침 오전 9시 시작 대신 Internet Explorer를 시작 하 되는 ChkNews 작업을 변경 합니다.

이 명령은 **/tn** 작업을 식별 하는 매개 변수입니다. 사용 하 여는 **/tr** 매개 변수는 작업을 실행 하는 프로그램을 변경 하 고 **/ru** 작업이 실행 되는 사용자 계정을 변경 하려면 매개 변수입니다.

**/ru**, 및 **/rp** 사용자 계정에 대 한 암호를 제공 하는 매개 변수를 생략 합니다. 계정에 대 한 암호를 제공 해야 하지만 사용할 수 있습니다는 **/ru**, 및 **/rp** 매개 변수 및 형식에 암호를 일반 텍스트로 나 대기 **SchTasks.exe** 하의 암호를 묻는 메시지가 표시 하 고 보이지 않는 텍스트로 암호를 입력 합니다.
```
schtasks /change /tn ChkNews /tr "c:\program files\Internet Explorer\iexplore.exe" /ru DomainX\Admin01
```
응답으로 **SchTasks.exe** 사용자 계정에 대 한 암호를 요청 합니다. 암호가 표시 되지 않으므로 힘들 텍스트를 입력 합니다.
```
Please enter the password for DomainX\Admin01: 
```
**/tn** 매개 변수를 식별 하 고 작업의 **/tr** 및 **/ru** 매개 변수가 작업의 속성을 변경 합니다. 다른 매개 변수를 사용 하 여 작업을 식별 하 없습니다 및 작업 이름을 변경할 수 없습니다.

응답으로 **SchTasks.exe** 성공 메시지를 표시 합니다.
```
SUCCESS: The parameters of the scheduled task "ChkNews" have been changed.
```
이 명령을 ChkNews 작업을 이제 Internet Explorer의 관리자 계정 권한으로 실행 합니다.

### <a name="to-change-a-program-to-the-system-account"></a>시스템 계정에 프로그램을 변경 하려면

다음 명령은 시스템 계정의 사용 권한으로 실행 되도록 SecurityScript 작업을 변경 합니다. 사용 하 여는 **/ru ""** 매개 변수를 시스템 계정을 나타냅니다.
```
schtasks /change /tn SecurityScript /ru ""
```
응답으로 **SchTasks.exe** 성공 메시지를 표시 합니다.
```
INFO: The run as user name for the scheduled task "SecurityScript" will be changed to "NT AUTHORITY\SYSTEM".
SUCCESS: The parameters of the scheduled task "SecurityScript" have been changed.
```
시스템 계정 권한으로 실행 되는 작업에는 암호를 요구 하지 않으므로 **SchTasks.exe** 하나 마다 표시 되지는 않습니다.

### <a name="to-run-a-program-only-when-i-am-logged-on"></a>로그인 하는 경우에 프로그램을 실행 하려면

다음 명령은 MyApp, 기존 작업을 전용 속성을 추가 합니다. 이 속성은 작업이 실행 되는 사용자 계정, 즉 "으로 실행된" 사용자가 컴퓨터에 로그온 하는 경우에 작업이 실행 되도록 보장 합니다.

명령을 사용 하 여는 **/tn** 매개 변수 작업을 식별 하 고 **/it** 작업에 전용 속성을 추가할 매개 변수입니다. 태스크는 이미 내 사용자 계정 권한으로 실행 하기 때문에 필자 필요가 없습니다 변경의 **/ru** 작업에 대 한 매개 변수입니다.
```
schtasks /change /tn MyApp /it
```
응답으로 **SchTasks.exe** 성공 메시지를 표시 합니다.
```
SUCCESS: The parameters of the scheduled task "MyApp" have been changed.
```

## <a name="BKMK_run"></a>실행 매개 변수

예약된 된 작업을 즉시 시작합니다. **실행** 작업 일정을 무시 하지만 프로그램 파일 위치, 사용자 계정 및 작업에 저장 된 암호를 사용 하 여 작업을 즉시 실행 합니다.

### <a name="syntax"></a>구문

```
schtasks /run /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>매개 변수

|         용어          |                                                                                                                                                                 정의                                                                                                                                                                  |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /tn \<작업 이름 >    |                                                                                                                                                       필수. 작업을 식별합니다.                                                                                                                                                        |
|    /s \<컴퓨터 >     |                                                                                                           (백슬래시 없이 또는) 이름 또는 원격 컴퓨터의 IP 주소를 지정합니다. 기본값은 로컬 컴퓨터입니다.                                                                                                           |
| /u [\<도메인 >\]<User> | 이 명령은 지정된 된 사용자 계정 권한으로 실행 됩니다. 기본적으로 명령은 로컬 컴퓨터의 현재 사용자의 권한으로 실행 합니다.</br>지정된 된 사용자 계정에는 원격 컴퓨터에서 Administrators 그룹의 구성원 이어야 합니다. **/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다. |
|    /p \<Password>     |                          에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. 사용 하는 경우는 **/u** 매개 변수를 생략 하는 **/p** 매개 변수 또는 password 인수 **schtasks** 암호를 묻는 메시지가 표시 됩니다.</br>**/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다.                           |
|          /?           |                                                                                                                                                    명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                     |

### <a name="remarks"></a>설명

-   이 작업을 사용 하 여 작업을 테스트 합니다. 작업 실행 되지 않으면 작업 스케줄러 서비스 트랜잭션 로그를 확인할 \<Systemroot > 오류에 대 한 \SchedLgU.txt 합니다.
-   작업을 실행 작업 일정에 영향을 주지 않는 및 작업에 대 한 예약 된 다음 실행된 시간을 변경 되지 않습니다.
-   작업을 원격으로 실행 하려면 원격 컴퓨터에서 작업을 예약 해야 합니다. 를 실행 하면 작업이 원격 컴퓨터 에서만 실행 됩니다. 작업을 원격 컴퓨터에서 실행 되 고 있는지를 확인 하려면 작업 관리자 또는 작업 스케줄러 트랜잭션 로그 사용 \<Systemroot > \SchedLgU.txt 합니다.

### <a name="examples"></a>예

### <a name="to-run-a-task-on-the-local-computer"></a>로컬 컴퓨터에서 작업을 실행 하려면

다음 명령은 "보안 스크립트" 작업을 시작합니다.
```
schtasks /run /tn "Security Script"
```
응답으로 **SchTasks.exe** 작업과 관련 된 스크립트를 시작 하 고 다음 메시지가 표시 됩니다.
```
SUCCESS: Attempted to run the scheduled task "Security Script".
```
메시지에서 알 수 있듯이 **schtasks** 을 만들었지만 해당 프로그램을 시작 하 여 프로그램이 실제로 시작 하는 매우 없습니다.

### <a name="to-run-a-task-on-a-remote-computer"></a>원격 컴퓨터에서 작업을 실행 하려면

다음 명령은 원격 컴퓨터 s v r 01에 업데이트 작업을 시작 합니다.
```
schtasks /run /tn Update /s Svr01
```
이 경우 **SchTasks.exe** 다음과 같은 오류 메시지가 표시 됩니다.
```
ERROR: Unable to run the scheduled task "Update".
```
오류의 원인을 찾으려고 C:\Windows\SchedLgU.txt s v r 01에 예약 된 작업 트랜잭션 로그를 확인 합니다. 이 경우 다음과 같은 항목이 로그에 나타납니다.
```
"Update.job" (update.exe) 3/26/2001 1:15:46 PM ** ERROR **
The attempt to log on to the account associated with the task failed, therefore, the task did not run.
The specific error is:
0x8007052e: Logon failure: unknown user name or bad password.
Verify that the task's Run-as name and password are valid and try again.
```
겉으로 보기 사용자 이름 또는 작업에는 암호가 올바르지 않습니다 시스템. 다음 **schtasks /change** 명령은 사용자 이름 및 s v r 01에 대해 업데이트 작업에 대 한 암호를 업데이트 합니다.
```
schtasks /change /tn Update /s Svr01 /ru Administrator /rp PassW@rd3
```
이후에 **변경** 명령이 완료 되 면는 **실행** 명령을 반복 합니다. 이 이번에 Update.exe 프로그램 시작 및 **SchTasks.exe** 다음 메시지가 표시 됩니다.
```
SUCCESS: Attempted to run the scheduled task "Update".
```
메시지에서 알 수 있듯이 **schtasks** 을 만들었지만 해당 프로그램을 시작 하 여 프로그램이 실제로 시작 하는 매우 없습니다.

## <a name="BKMK_end"></a>schtasks 끝

작업에 의해 시작 된 프로그램을 중지 합니다.

### <a name="syntax"></a>구문

```
schtasks /end /tn <TaskName> [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>매개 변수

|         용어          |                                                                                                                                                               정의                                                                                                                                                                |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /tn \<작업 이름 >    |                                                                                                                                         필수. 프로그램을 시작 하는 작업을 식별 합니다.                                                                                                                                         |
|    /s \<컴퓨터 >     |                                                                                                                        이름 또는 원격 컴퓨터의 IP 주소를 지정합니다. 기본값은 로컬 컴퓨터입니다.                                                                                                                        |
| /u [\<도메인 >\]<User> | 이 명령은 지정된 된 사용자 계정 권한으로 실행 됩니다. 기본적으로 명령은 로컬 컴퓨터의 현재 사용자의 권한으로 실행 합니다. 지정된 된 사용자 계정에는 원격 컴퓨터에서 Administrators 그룹의 구성원 이어야 합니다. **/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다. |
|    /p \<Password>     |                        에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. 사용 하는 경우는 **/u** 매개 변수를 생략 하는 **/p** 매개 변수 또는 password 인수 **schtasks** 암호를 묻는 메시지가 표시 됩니다.</br>**/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다.                         |
|          /?           |                                                                                                                                                             도움말을 표시 합니다.                                                                                                                                                              |

### <a name="remarks"></a>설명

**SchTasks.exe** 예약된 작업에 의해 시작 된 프로그램 인스턴스를 종료 합니다. 다른 프로세스를 중지 하려면 TaskKill를 사용 합니다. 자세한 내용은 참조 [Taskkill](taskkill.md)합니다.

### <a name="examples"></a>예

### <a name="to-end-a-task-on-a-local-computer"></a>로컬 컴퓨터에서 작업을 종료 하려면

다음 명령을 메모장 내 작업에 의해 시작 된 Notepad.exe의 인스턴스를 중지 합니다.
```
schtasks /end /tn "My Notepad"
```
응답으로 **SchTasks.exe** 작업이 시작 하 고 성공 메시지를 표시 하는 Notepad.exe의 인스턴스를 중지 합니다.
```
SUCCESS: The scheduled task "My Notepad" has been terminated successfully.
```

### <a name="to-end-a-task-on-a-remote-computer"></a>원격 컴퓨터에서 작업을 종료 하려면

다음 명령은 원격 컴퓨터 s v r 01에서 InternetOn 작업에 의해 시작 된 Internet Explorer의 인스턴스를 중지 합니다.
```
schtasks /end /tn InternetOn /s Svr01
```
응답으로 **SchTasks.exe** 작업이 시작 하 고 성공 메시지를 표시 하는 Internet Explorer의 인스턴스를 중지 합니다.
```
SUCCESS: The scheduled task "InternetOn" has been terminated successfully.
```

## <a name="BKMK_delete"></a>매개 변수 삭제

예약된 된 작업을 삭제합니다.

### <a name="syntax"></a>구문

```
schtasks /delete /tn {<TaskName> | *} [/f] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>매개 변수

|         용어          |                                                                                                                                                                 정의                                                                                                                                                                  |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   /tn {\<작업 이름 >    |                                                                                                                                                                     \*}                                                                                                                                                                     |
|          /f           |                                                                                                                                  확인 메시지를 표시 하지 않습니다. 경고 없이 작업이 삭제 됩니다.                                                                                                                                  |
|    /s \<컴퓨터 >     |                                                                                                           (백슬래시 없이 또는) 이름 또는 원격 컴퓨터의 IP 주소를 지정합니다. 기본값은 로컬 컴퓨터입니다.                                                                                                           |
| /u [\<도메인 >\]<User> | 이 명령은 지정된 된 사용자 계정 권한으로 실행 됩니다. 기본적으로 명령은 로컬 컴퓨터의 현재 사용자의 권한으로 실행 합니다.</br>지정된 된 사용자 계정에는 원격 컴퓨터에서 Administrators 그룹의 구성원 이어야 합니다. **/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다. |
|    /p \<Password>     |                          에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. 사용 하는 경우는 **/u** 매개 변수를 생략 하는 **/p** 매개 변수 또는 password 인수 **schtasks** 암호를 묻는 메시지가 표시 됩니다.</br>**/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다.                           |
|          /?           |                                                                                                                                                    명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                     |

### <a name="remarks"></a>설명

- **삭제** 작업 일정에서 작업을 삭제 합니다. 작업이 실행 되는 프로그램을 삭제 하거나 실행 중인 프로그램을 중단 하지 않습니다.
- 합니다 **삭제할 \\** * 명령은 모든 예약 된 작업에 컴퓨터 뿐 아니라 현재 사용자가 예약 된 작업을 삭제 합니다.

### <a name="examples"></a>예

### <a name="to-delete-a-task-from-the-schedule-of-a-remote-computer"></a>원격 컴퓨터의 일정에서 작업을 삭제 하려면

다음 명령은 원격 컴퓨터의 일정에서 "Start Mail" 작업을 삭제합니다. 사용 하 여는 **/s** 매개 변수를 원격 컴퓨터를 식별 합니다.
```
schtasks /delete /tn "Start Mail" /s Svr16
```
응답으로 **SchTasks.exe** 다음과 같은 확인 메시지가 표시 됩니다. 작업을 삭제 하려면 Y를 눌러<strong>합니다.</strong> 명령을 취소 하려면 다음을 입력 **n**:
```
WARNING: Are you sure you want to remove the task "Start Mail" (Y/N )? 
SUCCESS: The scheduled task "Start Mail" was successfully deleted.
```

### <a name="to-delete-all-tasks-scheduled-for-the-local-computer"></a>로컬 컴퓨터에 대 한 예약 된 모든 작업을 삭제 하려면

다음 명령을 다른 사용자가 예약 된 작업을 비롯 하 여 로컬 컴퓨터의 일정에서 모든 작업을 삭제 합니다. 사용 된 **/tn \\** * 컴퓨터의 모든 작업을 나타내는 매개 변수 및 **/f** 확인 메시지를 표시 하지 않으려면 매개 변수입니다.
```
schtasks /delete /tn * /f
```
응답으로 **SchTasks.exe** 만 실행 되도록 예약 된 작업 SecureScript, 삭제 됨을 나타내는 다음 성공 메시지가 표시 됩니다.

`SUCCESS: The scheduled task "SecureScript" was successfully deleted.`

## <a name="BKMK_query"></a>매개 변수 쿼리

컴퓨터에서 실행 하도록 예약 된 작업을 표시 합니다.

### <a name="syntax"></a>구문

```
schtasks [/query] [/fo {TABLE | LIST | CSV}] [/nh] [/v] [/s <Computer> [/u [<Domain>\]<User> [/p <Password>]]]
```

### <a name="parameters"></a>매개 변수

|         용어          |                                                                                                                                                                 정의                                                                                                                                                                  |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       / [쿼리]        |                                                                                                                        작업 이름은 선택 사항입니다. 입력 **schtasks** 매개 변수는 쿼리를 수행 하지 않고 있습니다.                                                                                                                         |
|      /fo {테이블       |                                                                                                                                                                    목록                                                                                                                                                                     |
|          /nh          |                                                                                                            테이블 표시에서 열 머리글을 생략합니다. 이 매개 변수는 유효한는 **테이블** 및 **CSV** 출력 형식입니다.                                                                                                             |
|          /v           |                                                                                                         디스플레이에 작업의 고급 속성을 추가합니다.</br>사용 하 여 쿼리 **/v** 여야 **목록** 또는 **CSV**합니다.                                                                                                          |
|    /s \<컴퓨터 >     |                                                                                                           (백슬래시 없이 또는) 이름 또는 원격 컴퓨터의 IP 주소를 지정합니다. 기본값은 로컬 컴퓨터입니다.                                                                                                           |
| /u [\<도메인 >\]<User> | 이 명령은 지정된 된 사용자 계정 권한으로 실행 됩니다. 기본적으로 명령은 로컬 컴퓨터의 현재 사용자의 권한으로 실행 합니다.</br>지정된 된 사용자 계정에는 원격 컴퓨터에서 Administrators 그룹의 구성원 이어야 합니다. **/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다. |
|    /p \<Password>     |                                        에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. 사용 하는 경우 **/u**, 생략 **/p** 또는 암호 인수 **schtasks** 암호를 묻는 메시지가 표시 됩니다.</br>**/u** 및 **/p** 매개 변수는 사용 하는 경우에 유효 **/s**합니다.                                         |
|          /?           |                                                                                                                                                    명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                     |

### <a name="remarks"></a>설명

**SchTasks.exe** 예약된 작업에 의해 시작 된 프로그램 인스턴스를 종료 합니다. 다른 프로세스를 중지 하려면 TaskKill를 사용 합니다. 자세한 내용은 참조 [Taskkill](taskkill.md)합니다.

### <a name="examples"></a>예

### <a name="to-display-the-scheduled-tasks-on-the-local-computer"></a>로컬 컴퓨터에서 예약 된 작업을 표시 하려면

다음 명령은 로컬 컴퓨터에 대 한 예약 된 모든 작업을 표시 합니다. 이 명령은 동일한 결과 생성 하 고 서로 교환해 서 사용할 수 있습니다.
```
schtasks
schtasks /query
```
응답으로 **SchTasks.exe** 는 다음 표에 나와 있는 것 처럼 기본적으로 간단한 테이블 형식으로 작업을 표시 합니다.
```
TaskName Next Run Time Status
========================= ======================== ==============
Microsoft Outlook At logon time
SecureScript 14:42:00 PM , 2/4/2001
```

### <a name="to-display-advanced-properties-of-scheduled-tasks"></a>예약 된 작업의 고급 속성 표시

다음 명령은 로컬 컴퓨터에서 작업의 자세한 표시를 요청합니다. 사용 하 여는 **/v** 자세한 (verbose) 표시를 요청 하려면 매개 변수 및 **/fo 목록** 매개 변수를 읽기 쉬운 목록으로 표시 형식을 지정 합니다. 가 사용 하 여 만든 작업이 의도 한 되풀이 지정 하는지 확인 하려면이 명령을 사용할 수 있습니다.

**schtasks /query /fo 목록 /v**

에 대 한 응답 **SchTasks.exe** 모든 작업에 대 한 자세한 속성 목록이 표시 됩니다. 다음 화면은 오전 4 시에 실행 되도록 예약 된 작업에 대 한 작업 목록을 보여 줍니다. 매월 마지막 금요일:
```
HostName: RESKIT01
TaskName: SecureScript
Next Run Time: 4:00:00 AM , 3/30/2001
Status: Not yet run
Logon mode: Interactive/Background
Last Run Time: Never
Last Result: 0
Creator: user01
Schedule: At 4:00 AM on the last Fri of every month, starting 3/24/2001
Task To Run: C:\WINDOWS\system32\notepad.exe
Start In: notepad.exe
Comment: N/A
Scheduled Task State: Enabled
Scheduled Type: Monthly
Modifier: Last FRIDAY
Start Time: 4:00:00 AM
Start Date: 3/24/2001
End Date: N/A
Days: FRIDAY
Months: JAN,FEB,MAR,APR,MAY,JUN,JUL,AUG,SEP,OCT,NOV,DEC
Run As User: RESKIT\user01
Delete Task If Not Rescheduled: Enabled
Stop Task If Runs X Hours and X Mins: 72:0
Repeat: Until Time: Disabled
Repeat: Duration: Disabled
Repeat: Stop If Still Running: Disabled
Idle: Start Time(For IDLE Scheduled Type): Disabled
Idle: Only Start If Idle for X Minutes: Disabled
Idle: If Not Idle Retry For X Minutes: Disabled
Idle: Stop Task If Idle State End: Disabled
Power Mgmt: No Start On Batteries: Disabled
Power Mgmt: Stop On Battery Mode: Disabled
```

### <a name="to-log-tasks-scheduled-for-a-remote-computer"></a>원격 컴퓨터에 예약 된 작업을 기록 하려면

다음 명령은 원격 컴퓨터에 예약 된 작업의 목록을 요청 하 고 로컬 컴퓨터에 쉼표로 구분 된 로그 파일의 작업을 추가 합니다. 이 명령 형식을 사용 하 여 수집 하 고 여러 컴퓨터에 대해 예약 된 작업을 추적할 수 있습니다.

명령을 사용 하 여는 **/s** Reskit16, 원격 컴퓨터를 식별 하는 매개 변수는 **/fo** 매개 변수를 형식 지정 및 **/nh** 를 열 머리글을 표시 하지 않는 매개 변수입니다. **>>**  p0102.csv 로컬 컴퓨터에 s v r 01에 작업 로그에 출력을 리디렉션하는 기호에 추가 합니다. 명령이 원격 컴퓨터에서 실행 하기 때문에 로컬 컴퓨터 경로 정규화 해야 합니다.
```
schtasks /query /s Reskit16 /fo csv /nh >> \\svr01\data\tasklogs\p0102.csv
```
응답으로 **SchTasks.exe** p0102.csv 파일을 로컬 컴퓨터에 s v r 01에 Reskit16 컴퓨터에 예약 된 작업을 추가 합니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
