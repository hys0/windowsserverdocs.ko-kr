---
title: reg unload
description: Reg 로드 작업을 사용 하 여 로드 된 레지스트리의 섹션을 제거 하는 reg unload 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6728f898bd8c2c65aff922943ccef58d4d9fd738
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925986"
---
# <a name="reg-unload"></a>reg unload

사용 하 여 로드 레지스트리의 섹션을 제거는 **reg 부하** 작업 합니다.

## <a name="syntax"></a>구문

```
reg unload <keyname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|--|--|
| `<keyname>` | 하위 키의 전체 경로 지정합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름 (형식 `\\<computername>\` )을 *keyname*의 일부로 포함 합니다. 생략 `\\<computername>\` 하면 작업이 로컬 컴퓨터에 기본적으로 설정 됩니다. *Keyname* 은 올바른 루트 키를 포함 해야 합니다. 로컬 컴퓨터의 유효한 루트 키는 **HKLM**, **HKCU**, **HKCR**, **HKU**및 **hkcc**입니다. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키는 **HKLM** 및 **HKU**입니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Reg unload** 작업의 반환 값은 다음과 같습니다.

    | 값 | 설명 |
    |--|--|
    | 0 | 성공 |
    | 1 | 실패 |

## <a name="examples"></a>예

HKLM 파일에서 TempHive 하이브 언로드 작업을 입력 합니다.

```
reg unload HKLM\TempHive
```

> [!CAUTION]
> 대안이 없는 한 레지스트리를 직접 편집 하지 마십시오. 레지스트리 편집기의 성능이 저하, 하면 시스템이 손상 또는 Windows를 다시 설치 해야 할 수 있는 설정을 허용 표준 보호를 무시 합니다. 안전 하 게 제어판 또는 Microsoft Management Console (MMC)에서 프로그램을 사용 하 여 대부분의 레지스트리 설정을 변경할 수 있습니다. 레지스트리를 직접 편집 해야 하는 경우 먼저 백업 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [reg load 명령](reg-load.md)
