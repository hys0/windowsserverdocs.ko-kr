---
title: pushprinterconnections
description: 그룹 정책에서 배포 된 프린터 연결 설정을 읽고 필요에 따라 프린터 연결을 배포/제거 하는 push프린터 연결 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b22fd5143a9477b40a515df44c9a0b5663dfd7a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931386"
---
# <a name="pushprinterconnections"></a>pushprinterconnections

그룹 정책에서 배포 된 프린터 연결 설정을 읽고 필요에 따라 프린터 연결을 배포/제거 합니다.

> [!IMPORTANT]
> 이 유틸리티는 컴퓨터 시작 또는 사용자 로그온 스크립트에서 사용 하기 위한 것 이며 명령줄에서 실행 해서는 안 됩니다.

## <a name="syntax"></a>구문

```
pushprinterconnections <-log> <-?>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| <-로그 > | 사용자 당 디버그 로그 파일을 *% temp*에 기록 하거나 컴퓨터 당 디버그 로그를 *%windir%\temp*에 씁니다. |
| <-? > | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)

- [그룹 정책을 사용 하 여 프린터 배포](https://go.microsoft.com/fwlink/?LinkId=230627)
