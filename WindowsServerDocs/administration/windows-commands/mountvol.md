---
title: mountvol
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fea8ad4d-f04a-4aaa-a3e5-75931e867b39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a3de8e5744c50acff3fdad0c7cf1dabf14fb144
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373581"
---
# <a name="mountvol"></a>mountvol



만들고, 삭제 또는 볼륨 탑재 지점을 나열 합니다.

이 명령을 사용 하는 방법의 예 참조 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문

```
mountvol [<Drive>:]<Path VolumeName>
mountvol [<Drive>:]<Path> /d
mountvol [<Drive>:]<Path> /l
mountvol [<Drive>:]<Path> /p
mountvol /r
mountvol [/n | /e]
mountvol <Drive>: /s
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[\<Drive >:]<Path>|탑재 지점이 있는 기존 NTFS 디렉터리를 지정 합니다.|
|\<VolumeName >|탑재 지점의 대상인 볼륨 이름을 지정 합니다. 볼륨 이름에 다음 구문을 사용 하 여 여기서 *GUID* 전역 고유 식별자입니다.</br>`\\\\?\Volume\{GUID}\`</br>대괄호 {}는 필요 합니다.|
|/d|지정된 된 폴더의 볼륨 탑재 지점을 제거합니다.|
|/l|지정된 된 폴더에 탑재 된 볼륨 이름을 나열합니다.|
|/p|지정된 된 디렉터리에서 볼륨 탑재 지점을 제거 하 고 기본 볼륨을 분리는 기본 볼륨을 오프 라인을 탑재할 수 없게 만드는 합니다. 다른 프로세스에서 볼륨을 사용 하는 경우 **mountvol** 에서 볼륨을 분리 하기 전에 열린 핸들을 닫습니다.|
|/r|볼륨 탑재 지점 디렉터리와 볼륨을 더 이상 자동으로를 방지 하는 시스템, 및 볼륨에 이전 볼륨 탑재 지점을 시스템에 다시 추가 하는 경우에 대 한 레지스트리 설정을 제거 합니다.|
|/n|새 기본 볼륨의 자동 탑재를 사용 하지 않도록 설정 합니다. 새 볼륨은 시스템에 추가 될 때 자동으로 탑재 되지 않습니다.|
|/e|새 기본 볼륨의 자동 탑재를 다시 설정합니다.|
|/s|지정 된 드라이브에 EFI 시스템 파티션을 탑재합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   **Mountvol** 드라이브 문자를 요구 하지 않고 볼륨을 연결할 수 있습니다.
-   사용 하 여 분리 되어 있는 볼륨 **/p** "하지 탑재 된 UNTIL A 볼륨 탑재 지점이 생성 됩니다."으로 볼륨 목록에 표시 됩니다 사용 하 여 볼륨의 탑재 지점이 여러 개 있으면 **/d** 사용 하기 전에 추가 탑재 지점을 제거 하려면 **/p**합니다. 다시 만들 수 있습니다 기본 볼륨 탑재 가능한 볼륨 탑재 지점을 할당 합니다.
-   를 다시 포맷 하거나 하드 드라이브의 교체 하지 않고 볼륨 공간을 확장 해야 하는 경우 다른 볼륨을 탑재 경로 추가할 수 있습니다. 여러 탑재 경로 볼륨 하나를 사용 하는 이점은 하나의 드라이브 문자를 사용 하 여 모든 로컬 볼륨에 액세스할 수 있는지 (예: `C:`). 드라이브 문자에 해당 하는 볼륨을 기억할 필요가 없습니다-할 수 있지만 로컬 볼륨을 탑재 하 고 드라이브 문자를 할당 합니다.

## <a name="BKMK_examples"></a>예와

탑재 지점을 만들려면 다음을 입력 합니다.
```
mountvol \sysmount \\?\Volume\{2eca078d-5cbc-43d3-aff8-7e8511f60d0e}\
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
