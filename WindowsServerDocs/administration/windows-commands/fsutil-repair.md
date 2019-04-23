---
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
title: Fsutil 복구
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 18c06b1f426105b098a5dc7e992b1e3becd3a4ca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846684"
---
# <a name="fsutil-repair"></a>Fsutil 복구
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

관리 및 모니터링 하는 NTFS 자체 복구 작업을 복구 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil repair [enumerate] <volumepath> [<LogName>]
fsutil repair [initiate] <VolumePath> <FileReference>
fsutil repair [query] <VolumePath>
fsutil repair [set] <VolumePath> <Flags>
fsutil repair [wait][<WaitType>] <VolumePath>

```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|열거|볼륨의 손상 로그의 항목을 열거합니다.|
|\<volumepath>|드라이브 이름 뒤에 콜론으로 볼륨을 지정 합니다.|
|\<LogName>|$ 손상-확인 된 손상 볼륨의 집합입니다.<br />$ 확인-볼륨의 잠재적인, 확인 되지 않은 손상의 집합입니다.|
|시작|NTFS 치유를 시작합니다.|
|\<FileReference>|NTFS 볼륨-특정 파일 ID (파일 참조 번호)을 지정합니다. 파일 참조는 파일의 세그먼트 수를 포함합니다.|
|쿼리|NTFS 볼륨의 자동 복구 상태를 쿼리합니다.|
|집합|볼륨의 자동 복구 상태를 설정합니다.|
|\<플래그 >|볼륨의 자동 복구 상태를 설정할 때 사용 되는 복구 방법을 지정 합니다.<br /><br />**플래그** 매개 변수는 세 가지 값으로 설정할 수 있습니다.<br /><br />-   **0x01**: 일반 복구를 활성화 합니다.<br />-   **0x09**: 복구 하지 않고 잠재적인 데이터 손실에 대 한 경고를 표시 합니다.<br />-   **0x00**: 자동 복구 작업을 복구 하는 NTFS를 사용 하지 않도록 설정 합니다.|
|state|시스템 또는 지정된 된 볼륨에 대 한 손상 상태를 쿼리합니다.|
|대기|Repair(s) 완료 될 때까지 기다립니다. 이 옵션 NTFS 기반이 복구가 수행 되는 볼륨에서 문제를 발견 했기를 하면 시스템이 복구 보류 중인 모든 스크립트를 실행 하기 전에 완료 될 때까지 대기 하도록 합니다.|
|[WaitType {0&#124;1}]|현재 복구를 완료 하거나 완료 하는 모든 복구 작업에 대 한 대기를 기다려야 하는지 여부를 나타냅니다. *WaitType* 다음과 같은 값으로 설정할 수 있습니다.<br /><br />-   **0**: 모든 복구가 완료 될 때까지 기다립니다. (기본값)<br />-   **1**: 현재 복구를 완료 될 때까지 기다립니다.|

## <a name="remarks"></a>설명

-   요구 하지 않고 온라인 NTFS 파일 시스템의 손상을 해결 하려고 NTFS를 자체 치유 **Chkdsk.exe** 실행 되도록 합니다. 이 기능은 Windows Server 2008에서 도입 되었습니다. 자세한 내용은 참조 [자체 치유 NTFS](https://go.microsoft.com/fwlink/?LinkID=165401)합니다.

## <a name="BKMK_examples"></a>예제

볼륨의 확인 된 손상의 열거 하려면 다음을 입력 합니다.

```
fsutil repair enumerate C: $Corrupt 
```

C 드라이브에 복구 자체 복구를 사용 하도록 설정 하려면 다음을 입력 합니다.

```
fsutil repair set c: 1
```

C 드라이브에 복구 자체 복구를 사용 하지 않으려면 다음을 입력 합니다.

```
fsutil repair set c: 0
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[자동 NTFS 복구](https://go.microsoft.com/fwlink/?LinkID=165401)


