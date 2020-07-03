---
title: bootcfg dbg1394
description: 지정 된 운영 체제 항목에 대해 1394 포트 디버깅을 구성 하는 bootcfg dbg1394 명령에 대 한 참조 문서
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1f71edbabbf85c301bec24138a805523975d3f6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926344"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 운영 체제 항목에 대 한 1394 포트 디버깅을 구성 합니다.

## <a name="syntax"></a>구문

```
bootcfg /dbg1394 {on | off}[/s <computer> [/u <domain>\<user> /p <password>]] [/ch <channel>] /id <osentrylinenum>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{on | off}` | 다음을 포함 하 여 1394 포트 디버깅의 값을 지정 합니다.<ul><li>**sign-on.** 지정 된에/dbg1394 옵션을 추가 하 여 원격 디버깅을 지원할 수 있도록 합니다 `<osentrylinenum>` .</li><li>**해제.** 지정 된에서/dbg1394 옵션을 제거 하 여 원격 디버깅 지원을 사용 하지 않도록 설정 <osentrylinenum> 합니다.</li></ul> |
| `/s <computer>` | 원격 컴퓨터의 이름 또는 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않음). 기본값은 로컬 컴퓨터입니다. |
| `/u <domain>\<user>`  | 또는로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다 `<user>` `<domain>\<user>` . 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| `/p <password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| `/ch <channel>` | 디버깅에 사용할 채널을 지정 합니다. 유효한 값은 1에서 64 사이의 정수를 포함 합니다. 1394 포트 디버깅을 사용 하지 않도록 설정 하는 경우이 매개 변수를 사용 하지 마세요. |
| `/id <osentrylinenum>` | 운영 체제 로드 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

**Bootcfg/dbg1394**명령을 사용 하려면 다음을 수행 합니다.

```
bootcfg /dbg1394 /id 2
bootcfg /dbg1394 on /ch 1 /id 3
bootcfg /dbg1394 edit /ch 8 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bootcfg 명령](bootcfg.md)
