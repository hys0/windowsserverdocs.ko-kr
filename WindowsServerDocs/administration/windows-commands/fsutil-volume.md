---
title: fsutil volume
description: 하드 디스크 드라이브 또는 특정 클러스터를 사용 하는 파일에서 현재 사용 가능한 공간 크기를 확인 하기 위해 하드 디스크 드라이브를 쿼리 하는 fsutil volume 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 18671447664c47af48b4ca074aab823fd2b78625
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436838"
---
# <a name="fsutil-volume"></a>fsutil volume

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

볼륨을 분리 하거나 쿼리를 하드 디스크 드라이브 여유 공간을 하드 디스크 드라이브에서 현재 사용할 수 또는 파일에는 특정 클러스터를 사용 하는 경우를 확인 합니다.

## <a name="syntax"></a>구문

```
fsutil volume [allocationreport] <volumepath>
fsutil volume [diskfree] <volumepath>
fsutil volume [dismount] <volumepath>
fsutil volume [filelayout] <volumepath> <fileID>
fsutil volume [list]
fsutil volume [querycluster] <volumepath> <cluster> [<cluster>] … …
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| allocationreport | 지정 된 볼륨에서 저장소를 사용 하는 방법에 대 한 정보를 표시 합니다. |
| `<volumepath>` | 드라이브 문자를 지정 하 고 그 뒤에 콜론을 지정 합니다. |
| diskfree | 하드 디스크 드라이브에 사용 가능한 공간의 크기를 확인 하려면을 쿼리 합니다. |
| 분리 | 볼륨을 분리합니다. |
| filelayout | 지정 된 파일에 대 한 NTFS 메타 데이터를 표시 합니다. |
| `<fileID>` | 파일 id를 지정 합니다. |
| list | 시스템의 모든 볼륨을 나열 합니다. |
| querycluster | 파일은 지정된 된 클러스터를 사용 하 여 찾습니다. 여러 클러스터를 지정할 수는 **querycluster** 매개 변수입니다. |
| `<cluster>` | LCN (logical cluster number)을 지정 합니다. |

### <a name="examples"></a>예

할당 된 클러스터 보고서를 표시 하려면 다음을 입력 합니다.

```
fsutil volume allocationreport C:
```

C 드라이브에 볼륨을 탑재 하려면 다음을 입력 합니다.

```
fsutil volume dismount c:
```

C 드라이브에 볼륨의 사용 가능한 공간의 크기를 쿼리하려면 다음을 입력 합니다.

```
fsutil volume diskfree c:
```

지정 된 파일에 대 한 모든 정보를 표시 하려면 다음을 입력 합니다.

```
fsutil volume C: *
fsutil volume C:\Windows
fsutil volume C: 0x00040000000001bf
```

디스크의 볼륨을 나열 하려면 다음을 입력 합니다.

```
fsutil volume list
```

클러스터를 사용 하는 파일을 찾으려면 C 드라이브에서 논리 클러스터 번호 50 및 0x2000에 의해 지정 된 다음을 입력 합니다.

```
fsutil volume querycluster C: 50 0x2000
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [NTFS의 작동 원리](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc781134(v=ws.10))
