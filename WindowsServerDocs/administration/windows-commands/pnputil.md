---
title: pnputil
description: 드라이버 패키지를 추가 하 고, 드라이버 패키지를 제거 하 고, pnputil.exe 유틸리티를 사용 하 여 드라이버 저장소에 있는 드라이버 패키지를 나열 하는 pnputil 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 01b8aee1aa4dfb85b590c9d4abbec471fc437da8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930243"
---
# <a name="pnputil"></a>pnputil

Pnputil.exe는 드라이버 저장소를 관리 하는 데 사용할 수 있는 명령줄 유틸리티입니다. 이 명령을 사용 하 여 드라이버 패키지를 추가 하 고, 드라이버 패키지를 제거 하 고, 저장소에 있는 드라이버 패키지를 나열할 수 있습니다.

## <a name="syntax"></a>구문

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| 지정하지 않을 경우 | 식별 된 INF 파일을 추가 하도록 지정 합니다. |
| -d | 식별 된 INF 파일을 삭제 하도록 지정 합니다. |
| -E | 모든 타사 INF 파일을 열거 하도록 지정 합니다. |
| -f | 식별 된 INF 파일을 강제로 삭제 하도록 지정 합니다. **– I** 매개 변수와 함께 사용할 수 없습니다. |
| -i | 식별 된 INF 파일을 설치 하도록 지정 합니다. **-F** 매개 변수와 함께 사용할 수 없습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

USBCAM 라는 INF 파일을 추가 합니다. INF, 형식:

```
pnputil.exe -a a:\usbcam\USBCAM.INF
```

C:\drivers에 있는 모든 INF 파일을 추가 하려면 다음을 입력 합니다.

```
pnputil.exe -a c:\drivers\*.inf
```

USBCAM를 추가 하 고 설치 합니다. INF 드라이버, 유형:

```
pnputil.exe -i -a a:\usbcam\USBCAM.INF
```

모든 타사 드라이버를 열거 하려면 다음을 입력 합니다.

```
pnputil.exe –e
```

Oem0 라는 INF 파일 및 드라이버를 삭제 하려면 다음을 입력 합니다.

```
pnputil.exe -d oem0.inf
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [popd 명령](popd.md)
