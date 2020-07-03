---
title: bootcfg timeout
description: 운영 체제 시간 제한 값을 변경 하는 bootcfg timeout 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa858eac-2bb7-4a27-a9bc-3e4a6eb8b2c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 280fb50f6e98024c58d33a174a294ac4309797ed
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924954"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

운영 체제 제한 시간 값을 변경합니다.

## <a name="syntax"></a>구문

```
bootcfg /timeout <timeoutvalue> [/s <computer> [/u <domain>\<user> /p <password>]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `/timeout <timeoutvalue>` | [부팅 로더] 섹션에서 시간 제한 값을 지정합니다. `<timeoutvalue>` 사용자는 NTLDR 기본값을 로드 하기 전에 운영 체제를 부팅 로더 화면에서 선택 해야 하는 시간 (초)입니다. 의 유효한 범위는 `<timeoutvalue>` 0-999입니다. 값이 0 이면 NTLDR은 부팅 로더 화면을 표시 하지 않고 기본 운영 체제를 즉시 시작 합니다. |
| `/s <computer>` | 원격 컴퓨터의 이름 또는 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않음). 기본값은 로컬 컴퓨터입니다. |
| `/u <domain>\<user>`  | 또는로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다 `<user>` `<domain>\<user>` . 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| `/p <password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

**Bootcfg/timeout** 명령을 사용 하려면 다음을 수행 합니다.

```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bootcfg 명령](bootcfg.md)
