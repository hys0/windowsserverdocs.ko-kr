---
title: ksetup
description: 컴퓨터에 정의 된 모든 영역에 대 한 영역 설정의 현재 상태를 표시 하는 ksetup 된 상태 설명 nand에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4ccb75ac143239d97b823fb7030f9a8020b4b4f6
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817743"
---
# <a name="ksetup-dumpstate"></a>ksetup

컴퓨터에 정의 된 모든 영역에 대 한 영역 설정의 현재 상태를 표시 합니다. 이 명령은 **ksetup** 명령과 동일한 출력을 표시 합니다.

## <a name="syntax"></a>구문

```
ksetup /dumpstate
```

### <a name="remarks"></a>설명

- 이 명령의 출력은 기본 영역 (컴퓨터의 구성원 인 도메인)를 포함 하 고이 컴퓨터에 정의 된 모든 영역입니다. 다음 각 영역에 대 한 포함 되어 있습니다.

  - 이 영역과 연결 된 모든 Kdc (키 배포 센터)입니다.

  - 이 영역에 대 한 모든 **집합 영역** 플래그입니다.

  - KDC 암호입니다.

- 이 명령은 DNS 검색에 지정 된 도메인 이름이 나 명령으로 표시 되지 않습니다 `ksetup /domain` .

- 이 명령은 명령을 사용 하 여 설정 된 컴퓨터 암호를 표시 하지 않습니다 `ksetup /setcomputerpassword` .

## <a name="examples"></a>예

컴퓨터에서 Kerberos 영역 구성을 찾으려면 다음을 입력 합니다.

```
ksetup /dumpstate
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [ksetup 명령](ksetup.md)