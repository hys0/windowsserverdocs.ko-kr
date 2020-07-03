---
title: bootcfg ems
description: 사용자가 응급 관리 서비스 콘솔의 리디렉션 설정을 원격 컴퓨터로 추가 하거나 변경할 수 있는 bootcfg ems 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 57abdc50-c64a-45f1-8470-3f8c3a51f743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c24f8acf6beb368dd989e4b05c912b69c4e7b68
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926246"
---
# <a name="bootcfg-ems"></a>bootcfg ems

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용자를 추가 하 여 원격 컴퓨터에 응급 관리 서비스 콘솔의 리디렉션에 대 한 설정을 변경할 수 있습니다. 응급 관리 서비스를 사용 하도록 설정 하면 `redirect=Port#` Boot.ini 파일의 [부팅 로더] 섹션에 지정 된 운영 체제 항목 줄에 대 한 줄이입니다 옵션과 함께 추가 됩니다. 응급 관리 서비스 기능은 서버에만 사용 됩니다.

## <a name="syntax"></a>구문

```
bootcfg /ems {on | off | edit}[/s <computer> [/u <domain>\<user> /p <password>]] [/port {COM1 | COM2 | COM3 | COM4 | BIOSSET}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <osentrylinenum>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{on | off | edit}` | 다음을 포함 하 여 응급 관리 서비스 리디렉션에 대 한 값을 지정 합니다.<ul><li>**sign-on.** 지정 된에 대 한 원격 출력을 사용 하도록 설정 `<osentrylinenum>` 합니다. 는 지정 된에입니다 옵션을 추가 하 <osentrylinenum> 고 `redirect=com<X>` [부팅 로더] 섹션에도 추가 합니다. 의 값은 `com<X>` **/port** 매개 변수로 설정 됩니다.</li><li>**해제.** 원격 컴퓨터에 대 한 출력을 사용 하지 않도록 설정 합니다. 또한 지정 된 <osentrylinenum> 및 `redirect=com<X>` [부팅 로더] 섹션의 설정에 대 한입니다 옵션을 제거 합니다.</li><li>**편집할.** `redirect=com<X>`[부팅 로더] 섹션에서 설정을 변경 하 여 포트 설정을 변경할 수 있습니다. 의 값은 `com<X>` **/port** 매개 변수로 설정 됩니다.</li></ul> |
| `/s <computer>` | 원격 컴퓨터의 이름 또는 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않음). 기본값은 로컬 컴퓨터입니다. |
| `/u <domain>\<user>`  | 또는로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다 `<user>` `<domain>\<user>` . 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| `/p <password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| `/port {COM1 | COM2 | COM3 | COM4 | BIOSSET}` |  리디렉션에 사용할 COM 포트를 지정 합니다. BIOSSET 매개 변수는 BIOS 설정을 가져오도록 응급 관리 서비스에 지시 하 여 리디렉션에 사용할 포트를 결정 합니다. 원격으로 관리 되는 출력을 사용 하지 않는 경우이 매개 변수를 사용 하지 마세요. |
| `/baud {9600 | 19200 | 38400 | 57600 | 115200}` | 리디렉션에 사용할 전송 속도 지정 합니다. 원격으로 관리 되는 출력을 사용 하지 않는 경우이 매개 변수를 사용 하지 마세요. |
| `/id <osentrylinenum>` | 응급 관리 서비스 옵션 Boot.ini 파일의 [운영 체제] 섹션에 추가 된 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. 이 매개 변수는 응급 관리 서비스 값을 **on** 또는 **off**로 설정한 경우에 필요 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

**Bootcfg/ems** 명령을 사용 하려면 다음을 수행 합니다.

```
bootcfg /ems on /port com1 /baud 19200 /id 2
bootcfg /ems on /port biosset /id 3
bootcfg /s srvmain /ems off /id 2
bootcfg /ems edit /port com2 /baud 115200
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /ems off /id 2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bootcfg 명령](bootcfg.md)
