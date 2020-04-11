---
title: bitsadmin setpeercachingflags
description: '**Bitsadmin setpeercachingflags**에 대 한 Windows 명령 항목-작업의 파일을 캐시 하 고 동료에 게 제공할 수 있는지 여부와 작업에서 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 플래그를 설정 합니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b4a7807975fb46440301e30b1fdbd01784d7c85
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122773"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

피어에서 콘텐츠는 작업의 파일을 캐시 하 고 동료에 게 제공 하 고 작업을 다운로드할 수 하는 경우를 결정 하는 플래그를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| 값 | 다음을 포함 하는 부호 없는 정수입니다.<ul><li>**1.** 작업에서 피어에서 콘텐츠를 다운로드할 수 있습니다.</li><li>**2.** 작업의 파일을 캐시 하 고 동료에 게 제공할 수 있습니다.</li></ul> |

## <a name="examples"></a>예

다음 예제에서는 *Mydownloadjob*이라는 작업에 대 한 플래그를 설정 하 여 피어에서 콘텐츠를 다운로드할 수 있도록 합니다.

```
C:\>bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)