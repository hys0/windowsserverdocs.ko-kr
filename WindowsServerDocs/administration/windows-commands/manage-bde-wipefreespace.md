---
title: manage-bde WipeFreeSpace
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 35d5f5fe079485d35fa412502bec745a136fbce9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373781"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde.exe WipeFreeSpace



공간에 존재 했을 수 있는 모든 데이터 조각 제거 볼륨의 여유 공간을 초기화 합니다. "사용 중인 공간만" 암호화 방법을 사용 하 여 암호화 된 볼륨에서이 명령을 실행 하면 "전체 볼륨 암호화" 암호화 방법과 동일한 수준의 보호 기능이 제공 됩니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
manage-bde -WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<Drive >|그 뒤에 콜론, 볼륨 GUID 경로 또는 탑재 된 볼륨에 드라이브 문자를 나타냅니다.|
|-취소|프로세스에 있는 빈 공간의 초기화를 취소 합니다.|
|-computername|다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다.|
|\<이름 >|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="BKMK_Examples"></a>예와

다음 예제를 사용 하는 **-w** 를 만드는 명령을 C 드라이브의 가용 공간을 초기화
```
manage-bde -w C:
```
다음 예에서는- **w** 명령과 **-cancel** 매개 변수를 사용 하 여 C 드라이브의 사용 가능한 공간 초기화를 취소 하는 방법을 보여 줍니다.
```
manage-bde -w -Cancel C:
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)