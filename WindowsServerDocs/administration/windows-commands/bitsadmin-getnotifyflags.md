---
title: bitsadmin getnotifyflags
description: 지정 된 작업에 대 한 알림 플래그를 검색 하는 **bitsadmin getnotifyflags**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3138baea05f793cfb587d3f8fb669d446daea6b5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850586"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

지정 된 작업에 대 한 알림 플래그를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="remarks"></a>주의

작업은 다음 알림 플래그 중 하나 이상을 포함할 수 있습니다.

| 플래그 | 설명 |
| ----- | ----- |
| 0x001 | 작업의 모든 파일 전송 된 경우 이벤트를 생성 합니다. |
| 0x002 | 오류가 발생 하면 이벤트를 생성 합니다. |
| 0x004 | 알림을 사용 하지 않도록 설정 합니다. |
| 0x008 | 작업을 수정 하거나 진행 중인 전송 작업을 수행할 때 이벤트를 생성 합니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 알림 플래그를 검색 *Mydownloadjob*합니다.

```
C:\>bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)