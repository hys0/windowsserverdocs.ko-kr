---
title: merge vdisk
description: 차이점 보관용 VHD (가상 하드 디스크)를 해당 부모 VHD와 병합 하는 merge vdisk 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41201885861b7084fa7b49be8b5bf5a0e7394981
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925039"
---
# <a name="merge-vdisk"></a>merge vdisk

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

차이점 보관용 가상 하드 디스크 (VHD) VHD 해당 부모와 함께 병합합니다. 부모 VHD 차이점 보관용 VHD에서 수정 내용을 적용 하도록 수정 됩니다. 이 명령은 부모 VHD를 수정 합니다. 결과적으로, 부모에 종속 되어 있는 기타 차이점 보관용 Vhd를 더 이상 유효 하지 않습니다.

> [!IMPORTANT]
> 이 작업이 성공 하려면 VHD를 선택 하 고 분리 해야 합니다. 사용 하 여는 **vdisk 선택** VHD를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="syntax"></a>구문

```
merge vdisk depth=<n>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 깊이 =`<n>` | 병합 부모 VHD 파일의 수를 나타냅니다. 예를 들어는 `depth=1` 차이점 보관용 VHD가 차이점 보관용 체인의 한 수준과 병합 됨을 나타냅니다. |

### <a name="examples"></a>예

VHD 부모를 사용 하 여 차이점 보관용 VHD를 병합 하려면 다음을 입력 합니다.

```
merge vdisk depth=1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [vdisk 명령 연결](attach-vdisk.md)

- [compact vdisk 명령](compact-vdisk.md)

- [detail vdisk 명령](detail-vdisk.md)

- [vdisk 명령 분리](detach-vdisk.md)

- [확장 vdisk 명령](expand-vdisk.md)

- [vdisk 명령 선택](select-vdisk.md)

- [list 명령](list.md)
