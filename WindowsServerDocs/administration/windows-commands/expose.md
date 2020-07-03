---
title: expose
description: 드라이브 문자, 공유 또는 탑재 지점으로 영구 섀도 복사본을 노출 하는 공개 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 816aad0ba57a30d9d3a05709941b1915d9a97d03
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932404"
---
# <a name="expose"></a>expose

드라이브 문자, 공유 또는 탑재 지점으로 영구 섀도 복사본을 노출합니다.

## <a name="syntax"></a>구문

```
expose <shadowID> {<drive:> | <share> | <mountpoint>}
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| shadowID | 노출 하려는 섀도 복사본의 그림자 ID를 지정 합니다. *ShadowID*대신 기존 별칭 또는 환경 변수를 사용할 수도 있습니다. 사용 하 여 **추가** 매개 변수 없이 기존 별칭을 참조 하십시오. |
| `<drive:>` | 드라이브 문자로 지정 된 섀도 복사본을 노출 합니다 (예: `p:` ). |
| `<share>` | 공유에 지정 된 섀도 복사본을 노출 합니다 (예: `\\machinename` ).   |
| `<mountpoint>` | 탑재 지점에 지정 된 섀도 복사본을 노출 합니다 (예: `C:\shadowcopy` ). |

### <a name="examples"></a>예

VSS_SHADOW_1 환경 변수와 연결 된 영구 섀도 복사본을 드라이브 X로 노출 하려면 다음을 입력 합니다.

```
expose %vss_shadow_1% x:
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [diskshadow 명령](diskshadow.md)
