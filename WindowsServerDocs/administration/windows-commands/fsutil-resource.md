---
title: fsutil resource
description: 트랜잭션 리소스 관리자 및 해당 동작을 관리 하는 fsutil resource 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: b198d8ca-a5b7-430f-8911-5cbb9f50484c
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 75037d39a070f8c7391df4136ab958f671732e09
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933340"
---
# <a name="fsutil-resource"></a>fsutil resource

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

보조 트랜잭션 리소스 관리자를 만들거나 트랜잭션 리소스 관리자를 시작 또는 중지 하거나 트랜잭션 리소스 관리자 대 한 정보를 표시 하 고 다음 동작을 수정 합니다.

- 기본 트랜잭션 리소스 관리자 다음 탑재 시 트랜잭션 메타 데이터를 정리 하는지 여부입니다.

- 지정 된 트랜잭션 리소스 관리자 가용성에 대 한 일관성을 선호 합니다.

- 지정 된 트랜잭션 리소스 관리자 일관성 보다 가용성을 선호 합니다.

- 실행 중인 트랜잭션 리소스 관리자의 특징입니다.

## <a name="syntax"></a>구문

```
fsutil resource [create] <rmrootpathname>
fsutil resource [info] <rmrootpathname>
fsutil resource [setautoreset] {true|false} <Defaultrmrootpathname>
fsutil resource [setavailable] <rmrootpathname>
fsutil resource [setconsistent] <rmrootpathname>
fsutil resource [setlog] [growth {<containers> containers|<percent> percent} <rmrootpathname>] [maxextents <containers> <rmrootpathname>] [minextents <containers> <rmrootpathname>] [mode {full|undo} <rmrootpathname>] [rename <rmrootpathname>] [shrink <percent> <rmrootpathname>] [size <containers> <rmrootpathname>]
fsutil resource [start] <rmrootpathname> [<rmlogpathname> <tmlogpathname>
fsutil resource [stop] <rmrootpathname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| create | 보조 트랜잭션 리소스 관리자를 만듭니다. |
| `<rmrootpathname>` | 트랜잭션 리소스 관리자 루트 디렉터리 전체 경로 지정합니다. |
| 정보 | 지정 된 트랜잭션 리소스 관리자 정보를 표시 합니다. |
| setautoreset | 기본 트랜잭션 리소스 관리자의 다음 탑재 트랜잭션 메타 데이터를 정리 합니다 있는지 여부를 지정 합니다.<ul><li>**true** -기본적으로 트랜잭션 리소스 관리자 다음 탑재에서 트랜잭션 메타 데이터를 정리 하도록 지정 합니다.</li><li>**false** -기본적으로 트랜잭션 리소스 관리자 다음 탑재에서 트랜잭션 메타 데이터를 정리 하지 않도록 지정 합니다. |
| `<defaultrmrootpathname>` | 드라이브 이름 뒤에 콜론을 지정 합니다. |
| setavailable | 트랜잭션 리소스 관리자를 일관성 보다 가용성을 선호를 지정 합니다. |
| setconsistent | 트랜잭션 리소스 관리자 일관성 가용성 보다를 선호를 지정 합니다. |
| setlog | 트랜잭션 리소스 관리자를 이미 실행 되 고 특성을 변경 합니다. |
| growth | 트랜잭션 리소스 관리자 로그가 증가할 수 있는 크기를 지정 합니다.<p>증가 매개 변수는 다음과 같이 지정할 수 있습니다.<ul><li>다음 형식을 사용 하는 컨테이너 수:`<containers> containers`</li><li>다음 형식을 사용 하는 백분율:`<percent> percent`</li></ul> |
| `<containers>` | 트랜잭션 리소스 관리자에서 사용 되는 데이터 개체를 지정 합니다. |
| maxextent | 컨테이너의 최대 수에 대 한 지정된 된 트랜잭션 리소스 관리자를 지정합니다. |
| minextent | 컨테이너의 최소 수에 대 한 지정된 된 트랜잭션 리소스 관리자를 지정합니다. |
| 모드가`{full|undo}` | 모든 트랜잭션을 기록할지 ( **full**) 아니면 롤백 이벤트만 기록할지 (**실행 취소**) 지정 합니다. |
| 이름 바꾸기 | 트랜잭션 리소스 관리자에 대 한 GUID를 변경합니다. |
| 축소 | 트랜잭션 리소스 관리자 로그 자동으로 줄일 수 있는 백분율을 지정 합니다. |
| 크기 | 트랜잭션 리소스 관리자의 크기를 지정 된 수의 *컨테이너로*지정 합니다. |
| start | 지정된 된 트랜잭션 리소스 관리자를 시작합니다. |
| stop(정지) | 지정된 된 트랜잭션 리소스 관리자를 중지합니다. |

### <a name="examples"></a>예

*C:\test*에서 지정 하는 트랜잭션 리소스 관리자의 로그를 설정 하려면 5 개의 컨테이너를 자동으로 증가 시키려면 다음을 입력 합니다.

```
fsutil resource setlog growth 5 containers c:test
```

*C:\test*에 지정 된 트랜잭션 리소스 관리자에 대 한 로그를 설정 하려면 2%의 자동 증가를 수행 하려면 다음을 입력 합니다.

```
fsutil resource setlog growth 2 percent c:test
```

트랜잭션 리소스 관리자 기본 C 드라이브에서 다음 탑재 트랜잭션 메타 데이터를 정리 합니다를 지정 하려면 다음을 입력 합니다.

```
fsutil resource setautoreset true c:\
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [트랜잭션 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730726(v=ws.10))
