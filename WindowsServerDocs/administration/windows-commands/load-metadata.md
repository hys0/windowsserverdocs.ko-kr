---
title: 메타 데이터 로드
description: 전송 가능한 섀도 복사본을 가져오기 전에 메타 데이터 .cab 파일을 로드 하거나 복원 시 기록기 메타 데이터를 로드 하는 메타 데이터 로드 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c7dc967476412261e7afc228088566f74ec4208c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820193"
---
# <a name="load-metadata"></a>메타 데이터를 로드 합니다.

변환할 수 있는 섀도 복사본을 가져오기 전에 메타 데이터.cab 파일을 로드 하거나 복원 하는 경우 기록기 메타 데이터를 로드 합니다. 매개 변수 없이 사용 하는 경우 **메타 데이터를 로드** 명령 프롬프트에서 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
load metadata [<drive>:][<path>]<metadata.cab>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `[<drive>:][<path>]` | 메타 데이터 파일의 위치를 지정합니다. |
| 메타 데이터 .cab | 로드할 메타 데이터.cab 파일을 지정 합니다. |

## <a name="remarks"></a>설명

- 사용할 수는 **가져올** 전송 가능한 섀도 복사본을 가져오려면 명령에 지정 된 메타 데이터에 따라 **메타 데이터를 로드**합니다.

- 복원에 대해 선택한 작성기 및 구성 요소를 로드 하려면 **복원 시작** 명령 전에이 명령을 실행 해야 합니다.

## <a name="examples"></a>예

기본 위치에서 metafile.cab 라는 메타 데이터 파일을 로드 하려면 다음을 입력 합니다.

```
load metadata metafile.cab
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [diskshadow 명령 가져오기](import.md)

- [복원 명령 시작](begin-restore.md)
