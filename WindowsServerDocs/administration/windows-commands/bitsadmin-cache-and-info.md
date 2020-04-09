---
title: bitsadmin 캐시 및 정보
description: '**Bitsadmin 캐시 및 정보**에 대 한 Windows 명령 항목으로, 특정 캐시 엔트리를 덤프 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e9c6ce1eb972a76408483b8a27a3abca5500e56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850896"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin 캐시 및 정보

특정 캐시 엔트리를 덤프합니다.

## <a name="syntax"></a>구문

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>매개 변수

| Paramreter | 설명 |
| -------------- | -------------- |
| recordID | 캐시 항목에 연결 된 GUID입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예에서는 recordID 값 {6511FB02-E195-40A2-B595-E8E2F8F47702}을 사용 하 여 캐시 엔트리를 덤프 합니다.

```
C:\>bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)