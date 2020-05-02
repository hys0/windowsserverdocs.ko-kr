---
title: bootcfg query
description: Boot.ini에서 부팅 로더 및 운영 체제 섹션 항목을 쿼리하고 표시 하는 bootcfg 쿼리 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44c5ce60f55618d16e80d1f1efde3af1cbf6c609
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709329"
---
# <a name="bootcfg-query"></a>bootcfg query

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

쿼리하고 [부팅 로더]을 표시 하 고 [운영 체제] Boot.ini에서 항목입니다.

## <a name="syntax"></a>구문

```
bootcfg /query [/s <computer> [/u <domain>\<user> /p <password>]]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `/s <computer>` | 원격 컴퓨터의 이름 또는 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않음). 기본값은 로컬 컴퓨터입니다. |
| `/u <domain>\<user>`  | 또는 `<user>` `<domain>\<user>`로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
| `/p <password>` | 에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="sample-output"></a>샘플 출력

**Bootcfg/query** command에 대 한 샘플 출력:
  
```
Boot Loader Settings
----------
timeout: 30
default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
Boot Entries
------
Boot entry ID:   1
Friendly Name:
path: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
OS Load Options: /fastdetect /debug /debugport=com1:
```

- **부팅 로더 설정** 영역에는 boot.ini의 [부팅 로더] 섹션에 각 항목이 표시 됩니다.

- 부팅 **항목** 영역에는 boot.ini의 [운영 체제] 섹션에 각 운영 체제 항목에 대 한 자세한 정보가 표시 됩니다.

## <a name="examples"></a>예

**Bootcfg/query** 명령을 사용 하려면 다음을 수행 합니다.

```
bootcfg /query
bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
bootcfg /query /u hiropln /p p@ssW23
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bootcfg 명령](bootcfg.md)
