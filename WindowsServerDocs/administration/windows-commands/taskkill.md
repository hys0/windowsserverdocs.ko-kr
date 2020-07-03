---
title: taskkill
description: 하나 이상의 작업 또는 프로세스를 종료 하는 taskkill에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2b71e792-08b6-46d4-95a5-cb6336a79524
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 061fd33e44f207b835987d35a812426899e6dd35
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936681"
---
# <a name="taskkill"></a>taskkill

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

하나 이상의 작업 또는 프로세스를 종료합니다. 프로세스는 프로세스 ID 또는 이미지 이름으로 종료할 수 있습니다. **taskkill** 은 **kill** 도구를 대체 합니다.

이 명령을 사용하는 방법의 예는 [예](#examples)를 참조하세요.

## <a name="syntax"></a>구문

```
taskkill [/s <computer> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/fi <Filter>] [...] [/pid <ProcessID> | /im <ImageName>]} [/f] [/t]
```

### <a name="parameters"></a>매개 변수

|         매개 변수         |                                                                                                                                        설명                                                                                                                                        |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /s\<computer>       |                                                                                    이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                                                     |
| /u\<Domain>\\\<UserName> | 에 지정 된 사용자의 계정 권한으로 명령을 실행 *UserName* 또는 *도메인*\\*UserName*합니다. **/u** 경우에 지정할 수 있습니다 **/s** 지정 됩니다. 기본값은 명령을 실행 하는 컴퓨터에 현재 로그온 한 사용자의 사용 권한입니다. |
|      /p\<Password>       |                                                                                                   에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                                                   |
|       /fi\<Filter>       |          작업 집합을 선택 하는 필터를 적용 합니다. 하나 이상의 필터를 사용 하거나 와일드 카드 문자 ( **\\** \* )를 사용 하 여 모든 작업 또는 이미지 이름을 지정할 수 있습니다. 다음을 참조 [유효한 필터 이름에 대 한 테이블](#filter-names-operators-and-values), 연산자 및 값입니다.           |
|     /pid\<ProcessID>     |                                                                                                                 종료할 프로세스의 프로세스 ID를 지정 합니다.                                                                                                                 |
|     /im\<ImageName>      |                                                                                종료할 프로세스의 이미지 이름을 지정 합니다. 와일드 카드 문자 ( **\\** \* )를 사용 하 여 모든 이미지 이름을 지정 합니다.                                                                                |
|            /f             |                                                                    프로세스가 강제로 종료 하도록 지정 합니다. 원격 프로세스에 대 한이 매개 변수는 무시 됩니다. 모든 원격 프로세스가 강제로 종료 됩니다.                                                                     |
|            /t             |                                                                                                          지정된 된 프로세스 및 종료 하는 모든 자식 프로세스를 종료 합니다.                                                                                                          |

#### <a name="filter-names-operators-and-values"></a>필터 이름, 연산자 및 값

| 필터 이름 |    유효한 연산자     |                                                                유효한 값                                                                |
|-------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|   상태    |         eq, ne         |                                                 실행 및 #124; 응답 중 & #124; 하지 알 수 없음                                                 |
|  IMAGENAME  |         eq, ne         |                                                                  이미지 이름                                                                  |
|     PID     | eq, ne, gt, lt, ge, le |                                                                  PID 값                                                                   |
|   SESSION   | eq, ne, gt, lt, ge, le |                                                                세션 번호                                                                |
|   CPUtime   | eq, ne, gt, lt, ge, le | CPU 시간 형식에서 <em>HH</em>**:**<em>MM</em>**:**<em>SS</em>, 여기서 *MM* 및 *SS* 0에서 59 사이 및 *HH* 부호 없는 숫자는 |
|  MEMUSAGE   | eq, ne, gt, lt, ge, le |                                                              메모리 사용량 (kb)                                                              |
|  USERNAME   |         eq, ne         |                                               모든 유효한 사용자 이름 (*사용자* 또는 *도메인*\\*사용자*)                                               |
|  서비스   |         eq, ne         |                                                                 서비스 이름                                                                 |
| WINDOWTITLE |         eq, ne         |                                                                 창 제목                                                                 |
|   모듈   |         eq, ne         |                                                                   DLL 이름                                                                   |

## <a name="remarks"></a>설명
* 원격 시스템에서 지정 된 경우에 WINDOWTITLE 및 상태 필터가 지원 되지 않습니다.
* **\\**<em>**/Im</em> 옵션에* 는 필터가 적용 될 때만 와일드 카드 문자 ()가 허용 됩니다.
* 원격 프로세스의 종료를 항상 수행 강제로, 여부에 관계 없이 **/f** 옵션을 지정 합니다.
* 컴퓨터 이름을 호스트 이름 필터에 제공 하면 종료 되 고 모든 프로세스가 중지 됩니다.
* 사용할 수 있습니다 **tasklist** 프로세스를 종료 하는 프로세스에 대 한 ID (PID) 확인 합니다.

## <a name="examples"></a>예

프로세스 Id 1230를 사용 하 여 프로세스를 끝내려면 1241, 및 1253를 입력 합니다.

```
taskkill /pid 1230 /pid 1241 /pid 1253
```

시스템에 의해 시작 된 경우 프로세스 Notepad.exe 강제로 종료 하려면 다음을 입력 합니다.

```
taskkill /f /fi USERNAME eq NT AUTHORITY\SYSTEM /im notepad.exe
```

Srvmain 사용자 계정에 대 한 자격 증명을 사용 하는 동안 note로 시작 하는 이미지 이름으로 원격 컴퓨터의 모든 프로세스를 종료 하려면 다음을 입력 합니다.

```
taskkill /s srvmain /u maindom\hiropln /p p@ssW23 /fi IMAGENAME eq note* /im *
```

프로세스 ID 2134 및 모든 자식 프로세스를 종료를 시작 했지만 해당 프로세스는 관리자 계정에 의해 시작 된 경우에 입력를 처리 합니다.

```
taskkill /pid 2134 /t /fi username eq administrator
```

이미지 이름에 관계 없이 1000 보다 크거나 같은 경우에 프로세스 ID를가지고 있는 모든 프로세스를 종료 하려면 다음을 입력 합니다.

```
taskkill /f /fi PID ge 1000 /im *
```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
