---
title: bcdboot
description: 시스템 파티션을 빠르게 설정 하거나 시스템 파티션에 있는 부팅 환경을 복구 하는 bcdboot 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: def4052e8aaa4f1e32216b5de837706b5cde3d04
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923506"
---
# <a name="bcdboot"></a>bcdboot

시스템 파티션을 신속 하 게 설정 하거나 시스템 파티션에 있는 부팅 환경을 복구를 수 있습니다. 시스템 파티션은 빈 파티션이 간단한 집합 데이터 BCD (부팅 구성) 파일을 복사 하 여 설정 됩니다.

## <a name="syntax"></a>구문

```
bcdboot <source> [/l] [/s]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| source | 부팅 환경 파일을 복사 하기 위한 원본으로 사용 하 여 Windows 디렉터리의 위치를 지정 합니다. |
| /l | 로캘을 지정 합니다. 기본 로캘은 영어 (미국)입니다. |
| /s | 시스템 파티션의 볼륨 문자를 지정합니다. 기본값은 시스템 파티션을 펌웨어에서 식별 합니다. |

## <a name="examples"></a>예

BCDboot와이 명령을 사용 하는 방법에 대 한 예제를 찾을 수 있는 위치에 대 한 자세한 내용은 [Bcdboot 명령줄 옵션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824874(v=win.10)) 항목을 참조 하세요.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
