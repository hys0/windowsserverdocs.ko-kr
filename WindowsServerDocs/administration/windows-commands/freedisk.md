---
title: freedisk
description: 설치 프로세스를 계속 하기 전에 지정 된 크기의 디스크 공간을 사용할 수 있는지 확인 하는 freedisk 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 91c15166-5baa-4b80-9e0c-4cd815d00530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2135bd24e24235de7c687ed58e0603db20c68262
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436978"
---
# <a name="freedisk"></a>freedisk

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

설치 프로세스를 계속 하기 전에 지정된 된 디스크 공간 양을가 사용할 수 있는지 확인 합니다.

## <a name="syntax"></a>구문

```
freedisk [/s <computer> [/u [<domain>\]<user> [/p [<password>]]]] [/d <drive>] [<value>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /s`<computer>` | 이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다. 이 매개 변수는 모든 파일 및 명령에 지정 된 폴더에 적용 됩니다. |
| /u`[<domain>\]<user>` | 지정된 된 사용자 계정 권한으로 스크립트를 실행합니다. 기본값은 시스템 사용 권한. |
| /p [<password>] | 에 지정 된 사용자 계정의 암호를 지정 **/u**합니다. |
| d`<drive>` | 사용 가능한 공간의 가용성을 확인 하려면 원하는 드라이브를 지정 합니다. `<drive>`원격 컴퓨터에 대해를 지정 해야 합니다. |
| `<value>` | 사용 가능한 디스크 공간의 특정 크기를 확인. `<value>`바이트, KB, MB, GB, TB, PB, EB, ZB 또는 YB로 지정할 수 있습니다. |

#### <a name="remarks"></a>설명

- 사용 하는 **/s**, **/u**, 및 **/p** 명령줄 옵션을 사용 하는 경우에 사용할 수 **/s**합니다. 사용자 암호를 제공 하려면 **/p** 를 **/u**와 함께 사용 해야 합니다.

- 무인된 설치에 사용할 수 있습니다 **freedisk** 설치를 계속 하기 전에 필수 구성 요소 크기의 사용 가능한 공간이 확인 하려면 설치 배치 파일에 있습니다.

- 배치 파일에서 **freedisk** 를 사용 하는 경우 충분 한 공간이 있는 경우 **0** 을 반환 하 고 충분 한 공간이 없는 경우 **1** 을 반환 합니다.

### <a name="examples"></a>예

C: 드라이브에 사용 가능한 최소한 50 MB의 여유 공간이 있는지를 확인 하려면 다음을 입력 합니다.

```
freedisk 50mb
```

화면에 다음과 유사한 출력이 표시 됩니다.

```
INFO: The specified 52,428,800 byte(s) of free space is available on current drive.
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
