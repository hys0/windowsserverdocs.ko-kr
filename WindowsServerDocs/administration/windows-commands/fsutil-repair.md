---
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
title: Fsutil 복구
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 6e4e285bf8401d628f7e4bcbaeafb0c6defa3ad1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376915"
---
# <a name="fsutil-repair"></a>Fsutil 복구
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

NTFS 자동 복구 복구 작업을 관리 하 고 모니터링 합니다.

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
|목록을|볼륨의 손상 로그를 열거 합니다.|
|@no__t 0volumepath >|드라이브 이름 뒤에 콜론으로 볼륨을 지정 합니다.|
|\<LogName >|$Corrupt-볼륨의 확인 된 손상 집합입니다.<br />$Verify-볼륨에서 확인 되지 않은 잠재적 손상의 집합입니다.|
|시작|NTFS 자동 복구를 시작 합니다.|
|@no__t 0FileReference >|NTFS 볼륨 특정 파일 ID (파일 참조 번호)를 지정 합니다. 파일 참조는 파일의 세그먼트 수를 포함합니다.|
|query|NTFS 볼륨의 자동 복구 상태를 쿼리 합니다.|
|집합|볼륨의 자동 복구 상태를 설정 합니다.|
|\<Flags >|볼륨의 자동 복구 상태를 설정할 때 사용할 repair 메서드를 지정 합니다.<br /><br />**플래그** 매개 변수는 세 가지 값으로 설정할 수 있습니다.<br /><br />@no__t 0**0x01**: 일반 복구를 사용 하도록 설정 합니다.<br />-   **0x09**: 복구 하지 않고 잠재적인 데이터 손실에 대 한 경고를 표시 합니다.<br />-   **0x00**: NTFS 자동 복구 복구 작업을 사용 하지 않도록 설정 합니다.|
|state|시스템 또는 지정 된 볼륨의 손상 상태를 쿼리 합니다.|
|wait|복구가 완료 될 때까지 기다립니다. 이 옵션 NTFS 기반이 복구가 수행 되는 볼륨에서 문제를 발견 했기를 하면 시스템이 복구 보류 중인 모든 스크립트를 실행 하기 전에 완료 될 때까지 대기 하도록 합니다.|
|[WaitType {0&#124;1}]|현재 복구를 완료 하거나 완료 하는 모든 복구 작업에 대 한 대기를 기다려야 하는지 여부를 나타냅니다. *WaitType* 다음과 같은 값으로 설정할 수 있습니다.<br /><br />-   **0**: 모든 복구가 완료 될 때까지 기다립니다. (기본값)<br />-   **1**: 현재 복구가 완료 될 때까지 기다립니다.|

## <a name="remarks"></a>설명

-   자동 복구 NTFS는 **chkdsk.exe** 를 실행 하도록 요구 하지 않고 ntfs 파일 시스템의 손상을 온라인으로 수정 하려고 시도 합니다. 이 기능은 Windows Server 2008에서 도입 되었습니다. 자세한 내용은 참조 [자체 치유 NTFS](https://go.microsoft.com/fwlink/?LinkID=165401)합니다.

## <a name="BKMK_examples"></a>예와

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

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[NTFS 자동 복구](https://go.microsoft.com/fwlink/?LinkID=165401)


