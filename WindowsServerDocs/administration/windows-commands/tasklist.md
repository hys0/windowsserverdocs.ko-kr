---
title: tasklist
description: 로컬 또는 원격 컴퓨터에서 실행 중인 프로세스의 목록을 표시 하는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8dbe30ee-1484-46be-917b-5ca3ff4fdc9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b43f4c9a89fa60f2244253d48d3dca646fe8e02d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833436"
---
# <a name="tasklist"></a>tasklist

로컬 컴퓨터 또는 원격 컴퓨터에서 현재 실행하고 있는 프로세스의 목록을 표시합니다. **Tasklist** 대체는 **tlist** 도구입니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
tasklist [/s <Computer> [/u [<Domain>\]<UserName> [/p <Password>]]] [{/m <Module> | /svc | /v}] [/fo {table | list | csv}] [/nh] [/fi <Filter> [/fi <Filter> [ ... ]]]
```

### <a name="parameters"></a>매개 변수

|          매개 변수           |                                                                                                                                            설명                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        /s \<컴퓨터 >        |                                                                                         이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                                                         |
| /u [\<도메인 >\\\]\<사용자 이름 > | *사용자 이름 또는* *도메인*\*사용자 이름으로 지정 된 사용자의 계정 권한으로 명령을 실행<em>합니다. \*\*/u</em>\*는 **/s** 가 지정 된 경우에만 지정할 수 있습니다. 기본값은 명령을 실행 하는 컴퓨터에 현재 로그온 한 사용자의 사용 권한입니다. |
|        /p \<암호 >        |                                                                                                       에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                                                        |
|         /m \<모듈 >         |                                                               DLL 모듈이 로드 패턴을 지정 된 이름과 일치 하는 모든 작업을 나열 합니다. 모듈 이름을 지정 하지 않으면이 옵션에 각 작업에 의해 로드 된 모듈을 모두 표시 됩니다.                                                                |
|             /svc             |                                                                                    잘림 없이 각 프로세스에 대 한 모든 서비스 정보를 나열합니다. 유효한 경우에는 **/fo** 매개 변수는 설정 **테이블**합니다.                                                                                    |
|              /v              |                                                                                 출력의 자세한 작업 정보를 표시합니다. 잘림 없이 전체 자세한 정보 출력을 사용 하 여 **/v** 및 **/svc** 함께 합니다.                                                                                 |
|  /fo {테이블 \| 목록 \| csv}  |                                                                             출력에 사용할 형식을 지정 합니다. 유효한 값은 **테이블**, **목록**, 및 **csv**합니다. 출력에 대 한 기본 형식은 **테이블**합니다.                                                                             |
|             /nh              |                                                                                             출력에서 열 머리글을 표시 하지 않습니다. 유효한 경우에는 **/fo** 매개 변수는 설정 **테이블** 또는 **csv**합니다.                                                                                              |
|        /fi \<필터 >         |                                                                          에 포함 하거나 쿼리에서 제외 하는 프로세스의 유형을 지정 합니다. 유효한 필터 이름, 연산자 및 값에 대 한 다음 표를 참조 합니다.                                                                          |
|              /?              |                                                                                                                                명령 프롬프트에 도움말을 표시합니다.                                                                                                                                |

### <a name="filter-names-operators-and-values"></a>필터 이름, 연산자 및 값

| 필터 이름 |    유효한 연산자     |                                                                 유효한 값                                                                 |
|-------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|   STATUS    |         eq, ne         |                                                                   RUNNING                                                                    |
|  IMAGENAME  |         eq, ne         |                                                                  이미지 이름                                                                  |
|     PID     | eq, ne, gt, lt, ge, le |                                                                  PID 값                                                                   |
|   세션   | eq, ne, gt, lt, ge, le |                                                                세션 번호                                                                |
| 세션 이름 |         eq, ne         |                                                                 세션 이름                                                                 |
|   CPU 시간   | eq, ne, gt, lt, ge, le | CPU 시간 형식에서 <em>HH</em> **:** <em>MM</em> **:** <em>SS</em>, 여기서 *MM* 및 *SS* 0에서 59 사이 및 *HH* 부호 없는 숫자는 |
|  MEMUSAGE   | eq, ne, gt, lt, ge, le |                                                              메모리 사용량 (kb)                                                              |
|  사용자 이름   |         eq, ne         |                                                             모든 유효한 사용자 이름                                                              |
|  서비스   |         eq, ne         |                                                                 서비스 이름                                                                 |
| WINDOWTITLE |         eq, ne         |                                                                 창 제목                                                                 |
|   모듈   |         eq, ne         |                                                                   DLL 이름                                                                   |

## <a name="remarks"></a>주의

원격 시스템에서 지정 된 경우에 WINDOWTITLE 및 상태 필터가 지원 되지 않습니다.

## <a name="examples"></a><a name="BKMK_examples"></a>예와

프로세스 id, 1000 보다 큰 모든 작업을 나열 하 고 CSV 형식으로 표시 하려면 다음을 입력 합니다.
```
tasklist /v /fi "PID gt 1000" /fo csv
```
현재 실행 중인 시스템 프로세스를 나열 하려면 다음을 입력 합니다.
```
tasklist /fi "USERNAME ne NT AUTHORITY\SYSTEM" /fi "STATUS eq running"
```
현재 실행 중인 모든 프로세스에 대 한 자세한 정보를 나열 하려면 다음을 입력 합니다.
```
tasklist /v /fi "STATUS eq running"
```
서비스에 정보를 모두 프로세스에 대 한 "Srvmain" DLL 이름이 "ntdll"로 시작 하는 원격 컴퓨터를 나열 하려면 다음을 입력 합니다.
```
tasklist /s srvmain /svc /fi "MODULES eq ntdll*"
```
"Srvmain," 현재 로그온 한 사용자 계정의 자격 증명을 사용 하 여 원격 컴퓨터의 프로세스를 나열 하려면 다음을 입력 합니다.
```
tasklist /s srvmain 
```
"Srvmain," Hiropln, 사용자 계정의 자격 증명을 사용 하 여 원격 컴퓨터의 프로세스를 나열 하려면 다음을 입력 합니다.
```
tasklist /s srvmain /u maindom\hiropln /p p@ssW23
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)