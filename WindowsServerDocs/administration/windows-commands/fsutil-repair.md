---
title: fsutil repair
description: NTFS 자동 복구 복구 작업을 관리 하 고 모니터링 하는 fsutil repair 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 700e1f713d503565321ab29f5384d74382c64f21
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931200"
---
# <a name="fsutil-repair"></a>fsutil repair

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

NTFS 자동 복구 복구 작업을 관리 하 고 모니터링 합니다. 자동 복구 NTFS는 **Chkdsk.exe** 를 실행 하지 않고도 온라인으로 ntfs 파일 시스템의 손상을 해결 하려고 시도 합니다. 자세한 내용은 [자동 복구 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))를 참조 하세요.

## <a name="syntax"></a>구문

```
fsutil repair [enumerate] <volumepath> [<logname>]
fsutil repair [initiate] <volumepath> <filereference>
fsutil repair [query] <volumepath>
fsutil repair [set] <volumepath> <flags>
fsutil repair [wait][<waittype>] <volumepath>

```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 목록을 | 볼륨의 손상 로그를 열거 합니다. |
| `<logname>` | 볼륨에서 `$corrupt` 확인 된 손상이 나 볼륨에서 확인 되지 않은 `$verify` 잠재적 손상의 집합인 집합 일 수 있습니다. |
| 시작 | NTFS 자동 복구를 시작 합니다. |
| `<filereference>` | NTFS 볼륨 특정 파일 ID (파일 참조 번호)를 지정 합니다. 파일 참조는 파일의 세그먼트 수를 포함합니다. |
| Query | NTFS 볼륨의 자동 복구 상태를 쿼리 합니다. |
| set | 볼륨의 자동 복구 상태를 설정 합니다. |
| `<flags>` | 볼륨의 자동 복구 상태를 설정할 때 사용할 repair 메서드를 지정 합니다.<p>이 매개 변수는 다음의 세 가지 값으로 설정할 수 있습니다.<ul><li>**0x01** -일반 복구를 사용 하도록 설정 합니다.</li><li>**0x09** -복구 하지 않고 잠재적인 데이터 손실에 대 한 경고를 표시 합니다.</li><li>**0x00** -NTFS 자동 복구 복구 작업을 사용 하지 않도록 설정 합니다.</li></ul> |
| state | 시스템 또는 지정 된 볼륨의 손상 상태를 쿼리 합니다. |
| wait | 복구가 완료 될 때까지 기다립니다. 이 옵션 NTFS 기반이 복구가 수행 되는 볼륨에서 문제를 발견 했기를 하면 시스템이 복구 보류 중인 모든 스크립트를 실행 하기 전에 완료 될 때까지 대기 하도록 합니다. |
| `[waittype {0|1}]` | 현재 복구를 완료 하거나 완료 하는 모든 복구 작업에 대 한 대기를 기다려야 하는지 여부를 나타냅니다. *Waittype* 매개 변수는 다음 값으로 설정할 수 있습니다.<ul><li>**0** -모든 복구가 완료 될 때까지 대기 합니다. (기본값)</li><li>**1** -현재 복구가 완료 될 때까지 기다립니다.</li></ul> |

### <a name="examples"></a>예

볼륨의 확인 된 손상을 열거 하려면 다음을 입력 합니다.

```
fsutil repair enumerate C: $Corrupt
```

C 드라이브에서 자동 복구 복구를 사용 하도록 설정 하려면 다음을 입력 합니다.

```
fsutil repair set c: 1
```

C 드라이브에서 자동 복구 복구를 사용 하지 않도록 설정 하려면 다음을 입력 합니다.

```
fsutil repair set c: 0
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [자동 복구 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))
