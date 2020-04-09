---
title: bitsadmin replaceremoteprefix
description: '**Bitsadmin replaceremoteprefix**에 대 한 Windows 명령 항목-필요에 따라 작업의 모든 파일에 대 한 원격 URL을 *oldprefix* 에서 *oldprefix*로 변경 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0cea0108a292815e31e893e91dc4079305c1da9a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849816"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

필요에 따라 작업의 모든 파일에 대 한 원격 URL을 *oldprefix* 에서 *oldprefix*로 변경 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| oldprefix | 기존 URL 접두사입니다. |
| oldprefix | 새 URL 접두사입니다. |

## <a name="examples"></a>예

다음 예에서는 *Mydownloadjob*이라는 작업의 모든 파일에 대 한 원격 URL을 *http://stageserver* 에서 *http://prodserver* 로 변경 합니다.

```
C:\>bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>추가 정보

- [명령줄 구문 키](command-line-syntax-key.md)