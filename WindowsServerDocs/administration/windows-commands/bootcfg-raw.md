---
title: bootcfg raw
description: 문자열로 지정 된 운영 체제 로드 옵션을 Boot.ini 파일의 운영 체제 섹션에 있는 운영 체제 항목에 추가 하는 bootcfg raw 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 74ab3c957623178e54b8a5debcf4aebffc942070
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926225"
---
# <a name="bootcfg-raw"></a>bootcfg raw

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

운영 체제 로드 옵션에는 운영 체제 항목을 문자열로 지정 된 추가 [운영 체제] Boot.ini 파일의 섹션입니다. 이 명령은 기존 운영 체제 항목 옵션을 덮어씁니다.

## <a name="syntax"></a>구문

```
bootcfg /raw [/s <computer> [/u <domain>\<user> /p <password>]] <osloadoptionsstring> [/id <osentrylinenum>] [/a]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `/s <computer>` | 원격 컴퓨터의 이름 또는 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않음). 기본값은 로컬 컴퓨터입니다. |
| `/u <domain>\<user>`  | 또는로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다 `<user>` `<domain>\<user>` . 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| `/p <password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| `<osloadoptionsstring>` | 운영 체제 항목에 추가할 운영 체제 로드 옵션을 지정 합니다. 이러한 로드 옵션은 운영 체제 항목과 관련 된 모든 기존 로드 옵션을 대체 합니다. 매개 변수에 대 한 유효성 검사는 없습니다 `<osloadoptions>` .
| `/id <osentrylinenum>` | 운영 체제 로드 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. |
| /a | 기존 운영 체제 옵션에 추가 해야 하는 운영 체제 옵션을 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

이 텍스트에는 **/debug**, **/fastdetect**, **/nodebug**, **/srrl**, **/crashdebug**및 **/sos**와 같은 올바른 OS 로드 옵션이 포함 되어야 합니다.

첫 번째 운영 체제 항목의 끝에 **/debug/fastdetect** 를 추가 하려면 이전 운영 체제 항목 옵션을 대체 합니다.

```
bootcfg /raw /debug /fastdetect /id 1
```

**Bootcfg/raw** 명령을 사용 하려면 다음을 수행 합니다.

```
bootcfg /raw /debug /sos /id 2
bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 /crashdebug  /id 2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bootcfg 명령](bootcfg.md)
